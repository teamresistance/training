---
title: "WPILib Geometry Classes"
---
WPILib provides geometry classes to handle positions, rotations, and transforms in 2D space. These classes simplify robot math such as aiming, distance calculation, and field-relative movement.WARNING: All code you write using these classes should be based on a BLUE alliance origin. (0,0) should be on the bottom blue corner! Look up "FRC Blue Side Origin" for more info
### Translation2d

Represents a point or vector on a 2D plane (x, y). Useful for distances and positions.
#### Creating a Translation

```
`
Translation2d point = new Translation2d(2.0, 3.0); // x=2m, y=3m
`
```

#### Distance and Vector Math

```
`
Translation2d a = new Translation2d(1, 1);
Translation2d b = new Translation2d(4, 5);

double distance = a.getDistance(b); // 5 meters
Translation2d vector = b.minus(a);   // vector from a to b
`
```

### Rotation2d

Stores an angle, provides sine/cosine helpers, and supports combining rotations.
#### Creating a Rotation

```
`
Rotation2d rot = Rotation2d.fromDegrees(90);
double radians = rot.getRadians();
`
```

#### Combining Rotations

```
`
Rotation2d a = Rotation2d.fromDegrees(30);
Rotation2d b = Rotation2d.fromDegrees(20);
Rotation2d c = a.plus(b); // 50 degrees
`
```

### Pose2d

Combines a translation and rotation, representing the robot’s full position on the field.
#### Creating a Pose

```
`
Pose2d robot = new Pose2d(
    new Translation2d(2.0, 1.0),
    Rotation2d.fromDegrees(90)
);
`
```

#### Applying a Transform

```
`
Transform2d movement = new Transform2d(
    new Translation2d(1.0, 0.0),
    Rotation2d.fromDegrees(45)
);

Pose2d newPose = robot.plus(movement);
`
```

### Transform2d

Represents a relative movement (translation + rotation) between poses.
#### Creating a Transform

```
`
Transform2d t = new Transform2d(
    new Translation2d(1.0, 0.5),
    Rotation2d.fromDegrees(15)
);
Pose2d movedPose = robot.plus(t);
`
```

### Targeting and Angles

You can use the robot pose and target pose to calculate angles, distances, etc. for aiming.
#### Angle to Target

```
`
Translation2d target = new Translation2d(5, 3);
Translation2d toTarget = target.minus(robot.getTranslation());

Rotation2d aimAngle = new Rotation2d(Math.atan2(
    toTarget.getY(),
    toTarget.getX()
));
`
```

#### Degrees to Rotate

```
`
Rotation2d currentAngle = robot.getRotation();
Rotation2d neededTurn = aimAngle.minus(currentAngle);

double degrees = neededTurn.getDegrees();
`
```

#### Distance to Target

```
`
double dist = robot.getTranslation().getDistance(target);
`
```
