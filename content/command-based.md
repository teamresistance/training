---
title: "Command-Based Programming"
---

The command-based framework is the recommended structure for FRC robots. It cleanly separates robot logic into**subsystems**(what your robot is) and**commands**(what your robot does).

The simplest way to understand it is this:

- Subsystems have methods and logic that runs hardware
- Commands run subsystem logic / methods
- Triggers run commands
- The command scheduler checks triggers

### How the Command-Based Framework Works

WPILib’s Command-Based architecture is built on a scheduler that constantly asks:*“What commands should run right now?”*Every robot loop (~20ms), the scheduler updates active commands, checks triggers, and ensures subsystem rules are followed.

#### The Scheduler

The scheduler is responsible for running, interrupting, and managing commands. It automatically:

- Runs`initialize()`when a command starts.
- Calls`execute()`every robot loop.
- Ends a command when`isFinished()`returns true or another command interrupts it.
- Enforces subsystem requirements (one command per subsystem at a time).

#### Command Lifecycle

```
`
+---------------+---------------------------+
| Method        | When It's Called          |
+---------------+---------------------------+
| initialize()  | When the command starts   |
| execute()     | Every 20ms while running  |
| isFinished()  | Checked every loop        |
| end()         | When ending or canceled   |
+---------------+---------------------------+
    `
```

### Triggers and Event Binding

Triggers listen for conditions and start/stop commands automatically. They can be bound to controller buttons, sensors, booleans, or custom logic.

#### Button Triggers (Typical)

```
`

driverController.rightTrigger()
    .whileTrue(new ShootCommand(shooter))
    .onFalse(new StopShooter(shooter));
    `
```

#### Boolean Triggers

Any function that returns a boolean can be used as a trigger.

```
`
Trigger armAtTop = new Trigger(() -> arm.getPosition() > 80);

armAtTop.onTrue(new HoldArmPosition(arm));
    `
```

#### Event-Driven Programming

- Commands start/stop based on events, not loops.
- Subsystems declare “who is controlling me right now” through requirements.
- Triggers make code reactive instead of procedural.

#### Command Groups and Compositions

The scheduler also runs composite commands:

- `SequentialCommandGroup`→ run commands in order
- `ParallelCommandGroup`→ run simultaneously
- `RaceGroup`→ stop all when one finishes
- `DeadlineGroup`→ run all until a “deadline” command ends

```
`
new SequentialCommandGroup(
    new HomeArm(arm),
    new WaitCommand(1),
    new MoveToPosition(arm, 45)
);
    `
```

### Subsystems

A subsystem represents hardware: motors, sensors, and logic that runs every loop. Each subsystem should control**one mechanical responsibility**.

#### Subsystem Responsibilities

- Own the hardware (motors, encoders, solenoids)
- Expose public methods (set Motor, go To Angle, shoot Ball)
- Run background logic in`periodic()`
- Optionally have a**default command**

#### Example Subsystem

```
`public class Arm extends SubsystemBase {
    private final MotorController motor = new TalonFX(3);
    private double targetDegrees = 0;

    public void setTarget(double deg) {
        targetDegrees = deg;
    }

    @Override
    public void periodic() {
        // Control loop
        motor.set(targetDegrees > getAngle() ? 0.4 : -0.4);
    }

    public double getAngle() {
        return encoder.getPosition();
    }
}
`
```

### Commands

A command is an action the robot performs: move arm, drive straight, shoot, etc. Commands run until they finish, get interrupted, or loop forever if continuous.

#### A Real Command Class

Use this when the logic is non-trivial or lasts over time:

```
`public class MoveArmTo extends Command {
    private final Arm arm;
    private final double target;

    public MoveArmTo(Arm arm, double target) {
        this.arm = arm;
        this.target = target;
        addRequirements(arm);
    }

    @Override
    public void execute() {
        arm.setTarget(target);
    }

    @Override
    public boolean isFinished() {
        return Math.abs(arm.getAngle() - target) < 2.0;
    }
}
`
```

#### When to Make a Dedicated Command File

- Action spans time (rotate arm to angle)
- Action requires state (store values internally)
- You need initialize/execute/end logic
- You want to reuse the command in multiple places

### Command Composition (inline commands)

Instead of making a whole file, WPILib allows “one-liner” commands composed from lambdas. These are ideal for simple actions.

#### Examples of Inline Commands

#### Instant Command (do something once)

```
`.onTrue(Commands.runOnce(() -> arm.setTarget(90)));`
```

#### Run Command (runs continuously)

```
`.whileTrue(Commands.run(() -> arm.setTarget(driverInput)));`
```

#### StartEnd Command (runs while held)

```
`.whileTrue(Commands.startEnd(
    () -> intake.setPower(0.8),
    () -> intake.setPower(0))
);`
```

#### Sequence

```
`Commands.sequence(
    intake.startEnd(() -> intake.setPower(1), () -> intake.setPower(0)).withTimeout(1),
    shooter.runOnce(() -> shooter.fire())
);`
```

#### Parallel Commands

```
`Commands.parallel(
    arm.runOnce(() -> arm.setTarget(80)),
    elevator.runOnce(() -> elevator.moveTo(40))
);`
```

#### When to Use Composition Instead of a Command File

- Behavior is extremely small
- No state needs to be stored
- No initialization logic required
- No finish condition needed
- Used only once (not reused)

### Requirements (addRequirements())

Requirements tell WPILib which subsystem(s) a command controls. Only one command at a time may use a subsystem.

#### Why Requirements Exist

- Prevents two commands from fighting over motors
- Ensures default commands stop when another command interrupts
- Makes concurrency safe

#### Example

```
`public MoveArmTo(Arm arm, double target) {
    this.arm = arm;
    this.target = target;
    addRequirements(arm);
}
`
```

#### What Happens Without Requirements?

- Both commands may try to control the same motor
- Robot behavior becomes inconsistent
- Default command keeps running even during an action
- WPILib can't automatically interrupt commands

#### When NOT to Use Requirements

- When command does NOT own hardware (e.g. vibration, LED logic separate from driving)
- When no issues will arise from multiple commands running on the same subsystem at once

### Default Commands

Every subsystem can have one default command that runs whenever no other command is using it.

#### Example: default drive command

```
`drive.setDefaultCommand(
    drive.run(() -> {
        drive.arcadeDrive(
            controller.getY(),
            controller.getX()
        );
    })
);
`
```

#### Rules for Default Commands

- Must have a requirement on the subsystem
- Runs continuously
- Stops when another command interrupts, continues afterwards
- Useful for operator control

### Best Practices

#### Subsystem Design

- One subsystem per mechanical system
- Keep periodic short
- Expose high-level methods (not raw motor sets)

#### Command Design

- Make files for reusable & multi-step actions
- Use composition for tiny one-off behaviors
- Always declare requirements
- Don’t put hardware in commands (only subsystems)

#### Operator Controls

```
`controller.a().onTrue(new MoveArmTo(arm, 90));
controller.b().onTrue(arm.runOnce(() -> arm.setTarget(0)));

controller.x().whileTrue(
    intake.startEnd(() -> intake.set(0.8), () -> intake.set(0))
);
`
```
