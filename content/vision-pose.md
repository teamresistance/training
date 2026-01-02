---
title: "Vision Pose Estimation"
---

Vision pose estimation answers one question:
**“Where is the robot on the field, right now?”**

Unlike odometry, vision provides nearly*absolute*field position. It updates significantly slower, maybe only 1 time
per second if moving quickly near a tag. Odometry, unlike vision, updates*continuously*. However, it drifts quickly -
vision corrects this. The goal is to fuse odometry with vision - take the less frequent but more accurate vision pose
and combine it with odometry to create the most accurate pose.

## High-Level Data Flow

A complete vision pose estimate follows this pipeline:

1. Camera detects AprilTags
1. Camera estimates camera-to-tag transform
1. Known tag pose converts to camera field pose
1. Camera-to-robot transform applied
1. Timestamp corrected for latency
1. Estimate fused into pose estimator

Every error introduced early compounds later. This is why calibration is key - if your odometry drifts slowly and your vision data isn't good you might be adding to the issue of inaccuracy.

## PhotonVision Pose Estimation

PhotonVision performs solvePnP on detected AprilTags to determine the 3D pose of the camera relative to the tag.

PhotonVision calculates the camera's pose to the to the apriltag using complex geometry - it only knows where the tag
is and what it looks like. Using Photon's estimated pose, you can apply a transformation of the camera pose to the
robot. For example, if the camera is at (1, 1) relative to the robot and PhotonVision estimates that that camera is
at (5, 5) on the field, you can deduce that the robot is at (4, 4) on the field. (rotation is also involved)

## AprilTag Field Layout

AprilTags become useful only because their poses are known in field coordinates.

WPILib provides official layouts:

```java
AprilTagFieldLayout layout =
    AprilTagFieldLayout.loadFromResource(
        AprilTagFields.k2024Crescendo.m_resourceFile);
```

Each tag has a fixed Pose3d on the field. Vision estimates work backwards from that known truth.

## Limelight MegaTag 1 vs MegaTag 2

It may sound easy, use the newer version! However, depending on the game and your movement, which model to use may change - it is important to test which works best.

### MegaTag 1

MegaTag 1 estimates pose from a single tag at a time.

- Works at long distances
- Higher ambiguity
- More susceptible to bad angles

The solvePnP problem has two valid solutions in many cases - ambiguity. It can (mostly) figure out which is correct.

### MegaTag 2

MegaTag 2 can use multiple tags simultaneously to solve a constrained optimization problem.

- Much lower ambiguity
- Far more stable rotation
- Works very well with multiple tags

## Camera-to-Robot Transform

Vision estimates the pose of the**camera**, not the robot. You must supply the transform from camera frame to robot frame.

```java
Transform3d robotToCam =
    new Transform3d(
        new Translation3d(0.25, 0.0, 0.45),
        new Rotation3d(0.0, 0.0, Math.PI));
```

If this transform is wrong:

- Pose estimates will shift with rotation
- Yaw will appear correct while X/Y drift
- Fusion will fight odometry, will stutter

## Latency Compensation

Vision data is always delayed. This delay includes:

- Camera exposure time
- Image processing
- Network transport

PhotonVision provides a timestamp for when the image was captured. This timestamp must be used.

```java
poseEstimator.addVisionMeasurement(
    visionPose,
    visionTimestampSeconds);
```

Without latency compensation, vision will**drag**your pose behind the robot during motion. Imagine always being 0.1 seconds behind! It can make a big difference.

## Pose Estimator Fusion

WPILib uses an Extended Kalman Filter internally. You do not tune gains directly. You tune trust.

Vision measurements are fused based on their covariance:

- Lower std dev = more trust on vision, accurate readings
- Higher std dev = less influence, less accurate

```java
poseEstimator.setVisionMeasurementStdDevs(
    VecBuilder.fill(0.7, 0.7, 1.2));
```

Poorly tuned vision std devs cause:

- Pose snapping
- Heading oscillation
- Auto path instability

## Rejecting Bad Measurements

Not all vision data should be trusted. Most of these will not occur super often, but can be depending on the game and your system. You should reject measurements when:

- Ambiguity is high
- No apriltags (no data, obvious)
- Estimated Z height is invalid, Z is almost never useful

Vision is a correction source, not a source of truth.

## Multi-Camera Fusion

Multiple cameras improve robustness, not accuracy. If one camera doesn't see a tag or doesn't get a reliable reading, you can have other camera(s) fill in. If many cameras see a tag reliably, you get ultra-precise estimates.

Each camera should:

- Have its own transform
- Have its own std devs
- Be fused with odometry independently

Never average poses manually. Let the estimator do the math!
