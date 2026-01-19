---
title: "Programming Season Challenges"
---

Complete these challenges in order. The first challenges focus on software concepts you can work on anywhere -- no hardware required. Later challenges introduce sensors, motors, and hands-on tuning at the shop.

---

## Challenge 1: Command-Based Fundamentals

**Prerequisites:** Sections 1, [Command-Based Programming](/command-based/)
**Hardware needed:** None (simulation only)

### Overview

Learn the command-based architecture by building a robot project -- no real hardware needed. You'll create subsystems, commands, command groups, and triggers that work entirely in code.

### Requirements

- Create a new robot project using the WPILib command-based template
- Use `SequentialCommandGroup` to create a multi-step "scoring sequence" that transitions through multiple commands
- Use `ParallelCommandGroup` to simulate two things happening at once
- Write subsystems
- Bind commands to controller buttons using `Trigger` bindings in RobotContainer

### Success criteria

- Code compiles and runs in simulation without errors
- Button presses trigger the correct commands
- Sequential and parallel command groups execute correctly

### Extra challenge

- Create a `RaceGroup` or `DeadlineGroup` to demonstrate advanced composition, and make it useful

---

## Challenge 2: Subsystem with Simulation

**Prerequisites:** Challenge 1, [Basic Motor Control](/motors/), [Subsystem IO Abstraction](/abstract-io/)
**Hardware needed:** None (simulation only)

### Overview

Build a complete subsystem with both real and simulated implementations using IO abstraction. Choose one of three options based on what hardware the team has available for later challenges.

### Choose your subsystem

#### Option A: Arm Subsystem (Recommended)

Build an arm that rotates between positions (stowed, intake, score).

- Create `ArmIO` interface with methods: `setTargetAngle(double degrees)`, `getAngle()`, `atSetpoint()`
- Create `ArmIOSim` that simulates arm physics using `SingleJointedArmSim` from WPILib
- Create `ArmIOReal` (placeholder -- just log "would move to X degrees")
- Arm should have positions: STOWED (0°), INTAKE (45°), SCORE (90°), AMP (120°)
- Simulate realistic movement time (arm shouldn't teleport)

#### Option B: Elevator Subsystem

Build an elevator that moves between height positions.

- Create `ElevatorIO` interface with methods: `setTargetHeight(double meters)`, `getHeight()`, `atSetpoint()`
- Create `ElevatorIOSim` that simulates elevator physics using `ElevatorSim` from WPILib
- Create `ElevatorIOReal` (placeholder -- just log "would move to X meters")
- Elevator should have positions: STOWED (0m), LOW (0.3m), MID (0.6m), HIGH (1.0m)
- Include simulated soft limits at min/max height

#### Option C: LED Strip Subsystem

Build a traffic light system using digital outputs (integrates with later sensor work).

- Create `LightsIO` interface with methods: `setRed(boolean on)`, `setYellow(boolean on)`, `setGreen(boolean on)`, `setAllOff()`
- Create `LightsIOSim` that logs light states to SmartDashboard as colored indicators
- Create `LightsIOReal` that uses `DigitalOutput` for each light
- Ensure only one light can be on at a time (mutex logic in subsystem)
- Add a "blink" mode that toggles a light on/off at a configurable rate

### Requirements (all options)

- Use the [IO abstraction pattern](/abstract-io/)
- Switch between real/sim implementations using `Robot.isReal()`
- Create [commands](/command-based/) to move to each position/state
- Log current state to [SmartDashboard](/telemetry/) (position, target, at-setpoint)
- Bind position commands to controller buttons

### Success criteria

- Simulation runs and shows realistic subsystem behavior
- SmartDashboard displays live subsystem status and telemetry
- Can switch between positions using controller
- Code cleanly separates IO interface from implementation

---

## Challenge 3: Autonomous Sequences

**Prerequisites:** Challenges 1-2
**Hardware needed:** None (simulation only)

### Overview

Create autonomous routines that use your subsystem from Challenge 2. Practice sequential command composition and autonomous mode selection.

### Requirements

- Create at least 3 different autonomous routines using your Challenge 2 subsystem
- Each routine should use `SequentialCommandGroup` with multiple steps
- Include `WaitCommand` for timing between actions
- Use `ParallelDeadlineGroup` in at least one routine (e.g., "move to position while waiting for 2 seconds max")
- Add a `SendableChooser` in SmartDashboard to select which autonomous routine to run
- Routines should work in simulation -- watch the subsystem move through its sequence

### Example routines (adapt to your subsystem)

- **Arm:** "Score High" → Score, wait, then return to home
- **Elevator:** "Cycle All" → Move to low, middle, and high positions with delays to demonstrate movement and control
- **Lights:** "Traffic Cycle" → Green 10s → Yellow 3s → Red 10s → repeat

### Success criteria

- Can select autonomous routine from SmartDashboard
- Selected routine runs when autonomous mode starts in simulation
- Routines complete their full sequence correctly
- Timing between steps is correct

### Extra challenge

- Create a "conditional" autonomous that checks subsystem status mid-routine and branches
- Add a command that uses `.until()` or `.withTimeout()` decorators

---

## Challenge 4: Sensor Integration

**Prerequisites:** Challenges 1-3, [Sensors](/sensors/), [Telemetry](/telemetry/)
**Hardware needed:** Test board with limit switches, beam break, or similar sensors

### Overview

Add sensor feedback to your subsystem. This challenge requires shop hardware -- coordinate with mentors to use the sensor test boards.

### Requirements

- Add at least one sensor input to your subsystem IO interface
- Implement both real (hardware) and simulated sensor readings
- Create a `Trigger` based on sensor state that fires a command
- Log sensor values to [SmartDashboard](/telemetry/)
- Use sensor feedback to modify subsystem behavior

### Sensor ideas by subsystem

- **Arm:** Limit switch at stowed position for homing, or "game piece detected" beam break
- **Elevator:** Top/bottom limit switches, or through-bore encoder for absolute position
- **Lights:** "Car sensor" using beam break -- when triggered, advance light sequence faster

### Success criteria

- Sensor values display correctly in SmartDashboard
- Trigger fires command when sensor condition is met
- Subsystem responds appropriately to sensor input
- Simulation still works with simulated sensor values

### Extra challenge

- Add debouncing to your sensor input to prevent false triggers
- Create a "calibration" command that uses sensor feedback to auto-home the subsystem

---

## Challenge 5: Motor Control

**Prerequisites:** Challenges 1-4, [Basic Motor Control](/motors/), [Vendors](/vendors/)
**Hardware needed:** Motor on test stand

### Overview

Connect your simulated subsystem to real motors. This challenge requires shop hardware -- coordinate with mentors to use the motor test stands.

### Requirements

- Update your `*IOReal` class to control actual motors
- Configure motor properly: idle mode, current limits, inversion
- Read encoder position from the motor and display on [SmartDashboard](/telemetry/)
- Implement basic open-loop control (percent output based on distance to target)
- Add soft limits in code to prevent over-travel
- Test that simulation and real modes both work correctly

### Motor configuration checklist

- Set idle mode to `BRAKE`
- Configure smart current limit (40A typical)
- Set correct inversion for your mechanism direction
- Burn flash after configuration changes

### Success criteria

- Motor moves when commands are triggered
- Encoder position displays correctly in SmartDashboard
- Soft limits prevent dangerous over-travel
- Motor stops cleanly when commands end
- Simulation still works when not connected to hardware

---

## Challenge 6: PID Position Control

**Prerequisites:** Challenges 1-5, [Basic PID Control](/pid-basics/), [Tuning PID](/pid-tuning/)
**Hardware needed:** Motor test stand, PIDlab tool

### Overview

Replace open-loop control with closed-loop PID. This is typically the most challenging step; mentors should be available during sessions.

### Requirements

- Implement PID control for your subsystem (position control)
- Use either WPILib `PIDController` or motor controller's built-in PID
- Add PID gains (P, I, D) as tunable values in [SmartDashboard](/telemetry/)
- Use the PIDlab tool to tune your controller
- Implement `atSetpoint()` method that returns true when within tolerance
- Commands should finish when setpoint is reached

### Tuning process

1. Start with P only (I=0, D=0)
2. Increase P until system oscillates, then back off 20%
3. Add small D to reduce overshoot
4. Only add I if there's steady-state error (usually not needed for position)
5. Test at multiple setpoints to verify tuning works across range

### Success criteria

- Subsystem moves to commanded position accurately
- Minimal overshoot and oscillation
- Commands finish when position is reached
- Position holds steady under load
- Tuning values are documented for future reference

### Extra challenge

- Add feedforward to improve response time
- Implement motion profiling for smoother movement (TrapezoidProfile)
- Create a "tuning mode" command that oscillates between two positions for easy PID adjustment
