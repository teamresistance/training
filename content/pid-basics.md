---
title: "PID Basics"
---
A beginner-level explanation of PID control: what the numbers mean, how each term behaves, simple ways to find usable values, and how to apply PID in real robot code.
### What is PID?

PID stands for**Proportional–Integral–Derivative**. It is a feedback controller that attempts to push a mechanism toward a target position, angle, velocity, or any measurable quantity.
#### The Basic Idea

PID looks at the**error**(how far you are from the target) and outputs a correction:

This output goes to a motor.
### What the Terms Mean

#### Proportional (P)

The main driver. P is a direct scalar to the error. If P = 10 and error = 5, output = 50.
Large error → large correction. Small error → small correction.
- **Too low:**slow response, never reaches target
- **Too high:**oscillation, overshoot, shaking

#### Integral (I)

Fixes small remaining error that P alone can’t eliminate. Most of the time a well-tuned PID will not need this, or Feedforward will take care of it.
Builds up over time when the mechanism is close but not perfect.
- **Use sparingly.**
- Too high → drifting, runaway, overshoot
- Too low → mechanism may be "just a tad bit off" and unable to correct itself

#### Derivative (D)

Adds damping. Reacts to how fast the error is changing.
- Reduces overshoot
- Helps stop smoothly at target
- Too high → oscillation
- Too low → can still overshoot

#### Summary

```
`
Term | What it does              | If too low         | If too high
-----+---------------------------+--------------------+--------------------------
P    | Main movement force       | Slow, weak         | Oscillation, overshoot
I    | Fix long-term small error | Never perfect      | Drifting, runaway
D    | Stabilizes, adds braking  | Overshoot          | Oscillation
`
```

### Applications in FRC

- **Arm angle control**— needs P + D + feedforward to compensate for gravity
- **Elevators**— P + D + feedfoward
- **Turrets**— high D for stability
- **Flywheel velocity**— P only, a flywheel doesn't need to smoothly reach it's target speed!

### Getting the Numbers (Simple Method)

This is not “proper tuning,” but rather a quick way to get functional values.
#### 1. Start With Only kP

1. Set a small value like`0.01`.
1. Increase until the mechanism starts to oscillate.
1. Reduce by 20–30%.

#### 2. Add kD

Add derivative until overshoot stops.
1. Increase slowly.
1. If the mechanism becomes shaky → reduce.

#### 3. Add kI (Only If Needed)

Only add I when the mechanism gets close but never reaches target.
1. Start extremely small (`0.0001`).
1. Increase until the error goes away.

#### 4. Consider adding a Feedfoward

Adding a feedfoward can be as simple as this:`output = output+feedfoward`
There is a more proper way to do this, but this will work in some cases.
1. Test your motor by applying increasing power until it just starts to move
1. When your motor JUST starts to move, use this as your feedforward. This is the power needed to avoid gravity (an external force)

### PID Code Examples

#### Basic PID in a Subsystem

```
`
public class Arm extends SubsystemBase {
    private final PIDController pid =
        new PIDController(0.05, 0.0, 0.002);

    private double targetDeg = 0;

    public void setTarget(double deg) {
        targetDeg = deg;
    }

    @Override
    public void periodic() {
        double current = getArmAngleDegrees();
        double output = pid.calculate(current, targetDeg);
        motor.set(output);
    }
}
`
```

#### PID in a Command

```
`
public class MoveArmTo extends Command {
    private final Arm arm;
    private final double target;

    public MoveArmTo(Arm arm, double target) {
        this.arm = arm;
        this.target = target;
        addRequirements(arm);
    }

    @Override
    public void initialize() {
        arm.setTarget(target);
    }

    @Override
    public boolean isFinished() {
        return Math.abs(arm.getError()) < 2;
    }
}
`
```
