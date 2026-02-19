---
title: "Vision - Target / Game Piece Tracking with Limelight"
---

## What is Limelight?

At its core, Limelight is a smart camera that:

- Sees the field using a camera + lime colored light
- Runs vision processing on the camera itself
- Sends processed results to your robot over NetworkTables

These features prove to be very strong and reliable while also being relatively easy to work with.

## Apriltags Versus Game Pieces (Key differences)

April tags are black and white markers that:

- Have a unique ID to be detected
- Have a given pose on the field
- Can provide a full 3D robot pose

Game Pieces vary by game, but they:

- Have no fixed ID or pose on the field
- Mainly detected by color and shape
- More sensitive to environmental changes like obstructions and lighting

In conclusion, Apriltags are for telling us information about the robot pose while game pieces tell us what the robot needs to pick up.

## How Limelight detects game pieces

Limelights often use **color-based pipelines** for game pieces.

The pipeline flow is listed below, with steps 2-5 needing configuration in the Limelight web UI.

1. Camera captures an image
1. Image is converted to HSV color space
1. Limelight filters pixels based on color range
1. It finds contours (blobs of matching color)
1. It selects the "best" contour
1. It calculates positional data

## How to read Limelight data in Java

Limelight data is accessed by NetworkTables, a class that allows us to communicate Limelight data directly to other parts of the code. This can be done by the following code:

```java
NetworkTable limelight = NetworkTableInstance.getDefault()
.getTable("limelight");

// tv == 1 when a piece is detected
// tx measures the x-distance from crosshair in degrees
// ta measures the area of the camera that shows the detected piece

double tv = limelight.getEntry("tv").getDouble(0);
double tx = limelight.getEntry("tx").getDouble(0);
double ta = limelight.getEntry("ta").getDouble(0);
```

Conceptually, we can use these values to command actions for the robot. For example, if the robot needs to pick up a game piece at an x-theta angle of 0, we could create code such as the following below (albeit very simplified):

```java
if (tv == 1) {
    double turn = turnPID.calculate(tx); // Turns the robot to try and make tx 0
    double forward = (ta < 2.5) ? 0.4 : 0; // Returns a value to be used by arcadeDrive based on the distance(ta) of the robot from the game piece
    drivetrain.arcadeDrive(forward, turn); // changes drive settings (For an arcadeDrive!!! We use swerve so this will be very different)
}

```
