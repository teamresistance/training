---
title: "Telemetry & Logging"
---
Telemetry is how the robot reports information for tuning, debugging, and analysis. This page covers both SmartDashboard and AdvantageKit logging.
### SmartDashboard

SmartDashboard is the simplest telemetry system built into WPILib. It sends key-value pairs to NetworkTables and can be viewed from any tool.
#### When to Use SmartDashboard

- Quick debugging
- Live values during testing
- Basic telemetry during matches

#### Basic Example

```
`import edu.wpi.first.wpilibj.smartdashboard.SmartDashboard;

public void periodic() {
    SmartDashboard.putNumber("Arm Angle", getAngle());
    SmartDashboard.putBoolean("Has Game Piece", hasPiece());
}
`
```

#### Reading SmartDashboard Values

You can also read values from the dashboard (use sparingly):
```
`double setpoint = SmartDashboard.getNumber("Arm Setpoint", 0.0);
pidController.setSetpoint(setpoint);
`
```

### AdvantageKit

AdvantageKit is a high-performance logging framework used for real-time telemetry and replay. It records everything the robot does for offline debugging.
#### What AdvantageKit Provides

- Full match logging
- Automatic timestamping
- Replay simulator
- Plots, charts, time-aligned telemetry
- Swerve and path debugging

You don't need to know all the special stuff - just the`recordOutput()`method.
#### Basic Logger Example

```
`import org.littletonrobotics.junction.Logger;

public void periodic() {
    Logger.recordOutput("Arm/Angle", getAngle());
    Logger.recordOutput("Arm/Target", targetAngle);
    Logger.recordOutput("Intake/HasPiece", hasPiece());
}
`
```

#### Logging a Complex Object

AdvantageKit supports Pose2d, Rotation2d, and other geometry types automatically.
```
`Logger.recordOutput("Drive/Pose", drivetrain.getPose());
`
```

#### Logging Motor/Encoder Data

```
`Logger.recordOutput("Arm/MotorTemp", motor.getTemperature());
Logger.recordOutput("Arm/EncoderPosition", encoder.getPosition());
`
```

### Best Practices

#### What to Log

- Subsystem states (enabled, disabled, idling)
- Sensor values (encoders, limit switches)
- Odometry / robot pose

#### Use Namespace Folders

...and DON'T change the spelling or capitalization.
```
`Logger.recordOutput("Arm/Angle", angle);
Logger.recordOutput("Arm/Target", target);
Logger.recordOutput("Drive/LeftVelocity", leftVel);
`
```
