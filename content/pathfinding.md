---
title: "Pathfinding & PathPlanner"
---

Sometimes, it is worth it to pre-plan paths for robot movement and actions instead of doing it on the fly. This page covers PathPlanner, a tool to do so.

## What is Path Planning?

Path planning produces time-parameterized sequences of poses (x, y, rotation) plus velocities/accelerations. Benefits:

- Smooth, repeatable motion
- Velocity & acceleration constraints
- Event markers to trigger commands mid-path
- Easy visualization & editing via an editor

## PathPlanner Overview

## Tool

PathPlanner (pathplanner.dev) is a GUI editor that exports path and autos into your robot project deploy folder:

## Editor Features

- Draw and edit waypoints
- Assign velocity/accel constraints
- Add event markers (strings) triggering commands
- Generate multi-path autos

## Integrating PathPlanner with your Robot

## Dependencies

Add PathPlanner lib to your vendor dependencies through the vendor dependency manager.

## Key Concepts

- **Path**- single trajectory file.
- **Auto**- sequence of paths + events.
- **Named Command**- how PathPlanner calls commands during an auto

## Load & Run a Path

```java
// This code goes in the RobotContainer - this is how you will typically create an auto selector.
  private LoggedDashboardChooser configureAutos() {

    // Set up auto routines
    LoggedDashboardChooser autoChooser =
        new LoggedDashboardChooser<>("Auto Choices", AutoBuilder.buildAutoChooser());

    return autoChooser;
  }
```

## Named Commands

Named commands are defined in-code and can be run by PathPlanner in an auto.

## Example

```java
NamedCommands.registerCommand(
    "autoScore", new DeferredCommand(() -> new AutoScoreCommand(reef, drive, elevator)));
```

These commands run just the same as normal commands - but PathPlanner will wait to continue until they finish.

## Making On-the-Fly / Teleop Paths

You can generate short paths at runtime (helpful for driver-assist or snapping to a scoring pose).

## Simple runtime path from current pose → target pose

```java
public static Command followPoses(SwerveDriveIO drive, double transitionVelocity, Supplier pointArraySupplier) {
    Pose2d[] points = pointArraySupplier.get();
    List waypoints = PathPlannerPath.waypointsFromPoses(points);
    PathPlannerPath path =
        new PathPlannerPath(
            waypoints,
            Constants.PATH_CONSTRAINTS,
            new IdealStartingState(
                drive.getPose().getTranslation().getDistance(points[0].getTranslation()),
                points[0].getRotation()),
            new GoalEndState(0, points[points.length - 1].getRotation()));

    path.preventFlipping = true;
    return Commands.sequence(
        AutoBuilder.pathfindToPose(points[0], Constants.PATH_CONSTRAINTS, transitionVelocity),
        AutoBuilder.followPath(path));
  }
```

## Semi-Auto Uses

- Drive to scoring position on button
- Auto-align to vision target then let driver finish
- Path-based assist modes

## When to Use PathPlanner vs Hand-built

## Use PathPlanner when

- You want quick, repeatable autos
- You don't want any possible interference
- You want to do the same thing, every time.

## Create your own auto command sequence when

- You can sacrifice a tiny bit of consistency to be significantly more efficient
- You want your auto to move on to the next thing ASAP, not with pre-set wait times
- The game is too complex to create full paths for every scenario, and you could instead just define start/end positions

## PathFinder

PathFinder is a sub-branch of pathplanner that allows the robot to drive to a set pose, while avoiding obstacles on the field. `AutoBuilder.pathfindToPose(...)` Use it when you want to autonomously get around field elements in teleop without much driver input.
