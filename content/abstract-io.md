---
title: "Subsystem IO Abstraction"
---

IO Abstraction separates hardware access from subsystem logic. This allows you to swap between real hardware, simulation, replay, and unit tests without changing subsystem code.

## What Is IO Abstraction?

The concept is simple: every subsystem talks to an**IO interface**instead of directly accessing motor controllers, encoders, or sensors.

This gives you:

- Cleaner subsystem code
- Real vs. simulated implementations
- Easier hardware swap flexibility

## The Structure

A subsystem usually has:

- **An IO interface**— defines inputs/outputs
- **A real implementation**— talks to actual hardware
- **A fake/sim implementation**- for simulating robot code

## Defining the IO Interface

This interface defines**what the subsystem needs**. It does not know anything about CAN IDs or motor types.

```java
public interface ArmIO extends Subsystem {

    // This method works the same as it does in a subsystem class!
    // This means the periodic() method in each implementation will be called automatically just the same.
    @Override
    void periodic();

    // All non-default methods must be implemented by the real and sim classes.
    void setWristAngle(double degrees);
    void setTargetAngle(double degrees);
    void home();

    // Default methods are not required to be implemented in the real/sim class.
    // If a default method is not changed by an implementation, the default code is used (in this case, a placeholder);
    default double degreesToMotorRotations(double degrees) { return 0; }
    default double motorRotationsToDegrees(double rotations) { return 0; }
}
```

## Real Hardware Implementation

This class uses real hardware—TalonFX, SparkMAX, encoders, limit switches, etc.

```java
// ArmReal.java
public class ArmReal implements ArmIO {

    private final TalonFX motor = new TalonFX(1);

    public ArmReal() {
        register(); // THIS IS REQUIRED!!!!! The Subsystem class does not auto-register on the command scheduler!
    }

    @Override
    public void periodic() {
        // ... periodically run code when on a robot
    }

    @Override
    public void setWristAngle(double degrees) {
        // ... code that runs real hardware
    }

    @Override
    public void setTargetAngle(double degrees) {
        // ... code that runs real hardware
    }

    @Override
    public void home() {
        motor.setPosition(0);
    }
}
```

## Fake / Simulation Implementation

Used for simulation, unit tests, or AdvantageKit replay.

```java
// ArmSim.java
public class ArmSim implements ArmIO {

    public ArmSim() {
        register(); // THIS IS REQUIRED!!!!! The Subsystem class does not auto-register on the command scheduler!
    }

    private double simulatedArmAngle = 0;

    @Override
    public void periodic() {
        // ... periodically run code while not on a real robot
    }

    @Override
    public void setWristAngle(double degrees) {
        // ... simulated movement
    }

    @Override
    public void setTargetAngle(double degrees) {
        // ... simulated movement
    }

    @Override
    public void home() {
        // ... homing has no use in sim! we can leave this blank
    }
}
```

## Selecting Real vs Sim in RobotContainer

You choose the implementation at runtime:

```java
// RobotContainer.java
public class RobotContainer {

    private final ArmIO arm;

    public RobotContainer() {
        if (Robot.isReal()) {
            armIO = new ArmReal();
            // ... other subsystems
        } else {
            armIO = new ArmSim();
            // ... other subsystems
        }
    }
}
```

## Why Teams Use This Pattern

WPILib does not force IO abstraction, but the best teams use it because:

- Simulation works instantly
- No conflict between simulated logic and real logic
- AdvantageKit integrates perfectly

There will be more covered on how to set up and use simulation later.
