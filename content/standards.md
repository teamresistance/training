---
title: "Code Standards / Formatting"
---

### Naming

Variables should be properly named! Try to keep them as descriptive but not too long. For example, if you were storing a mechanism's setpoint, you would name it`elevatorTarget`, not`requestedElevatorPIDSetpointLocation`.

- **Classes:**UpperCamelCase (ex.`ElevatorSubsystem`)
- **Methods:**lowerCamelCase (ex.`setElevatorHeight()`) - methods should state exactly what they do as simply as possible, try to stick with "set" or "get" as well.
- **Variables:**lowerCamelCase (ex.`elevatorSpeed`)
- **Constants:**ALL_CAPS_WITH_UNDERSCORES (ex.`MAX_ELEVATOR_HEIGHT`)

### Organization

Good FRC code is predictable, consistent, and structured so anyone on the team can navigate it quickly. The goal is to eliminate “mystery code” by putting every file where people expect to find it and keeping subsystems, commands, and utilities clearly separated.

#### Project Layout

- **subsystems/**– One folder per subsystem, each holding a SubsystemIO, SubsystemReal, and SubsystemSim
- **commands/**– One file per command or command group
- **util/**– Reusable utilities (ex. GeomUtil)
- **Constants.java**– Store anything that should be easily changed and should be visible easily (ports, gains, limits, timing)
- **RobotContainer.java**– Triggers, auto setup, subsystem initialization
- **Main.java / Robot.java**– Never modify unless you have a REALLY good reason.

#### Keep Logic Where It Belongs

- **Subsystems own hardware + IO**
- **Commands own behavior**(what to do, not how to do it)
- **RobotContainer owns bindings**

### Constants

Every robot project has some values that are used in many places or should be easily changed. What if you're at a competition and you need to quickly edit the timings on scoring? You don't have time to find the 8 places where the number is used - create a constant for it and change that.

Constants are named in ALL_CAPS_WITH_UNDERSCORES. They are also always public, static, and final. They also go in the`Constants.java`file.

### Never-Do's

On a side note, there are a few things you should NEVER put in your code. These make the code less easy to work with and can cause issues down the line.

- Thread.sleep() or Timer.delay() - These will BREAK the robot. When the robot code thread sleeps, the robot keeps doing what it was doing because no new inputs can be received. So, if you're driving forward and you Thread.sleep(1000), you will be uncontrollably driving forwards for the next second. Dangerous!
- Manually scheduling commands - ALWAYS try to avoid doing this. This makes it much harder to "track" a command and keep control of it.
- "Magic Numbers" - If it's important, it gets a CONSTANT! Avoid putting random numbers only where they're used - it becomes a big challenge to change them later on. Don't put 0.125 in 10 places, create a VARIABLE_NAME_HERE constant and reference it.

### Spotless

We use a very convenient tool to format our code automatically. You can run it through the command line:`./gradlew spotlessApply`- it should format your indentation, line lengths, etc. Do this every time before you commit in git.
