---
title: "User Input"
---

The driver needs to tell the robot what to do! WPILib provides us with multiple choices in which we can communicate with a robot/simulation. In Team Resistance, we mainly use Xbox Controllers and Joysticks.(although less commonly used amongst teams) `GenericHID` is the parent class for every other controller. `GenericHID` can be used when external button systems are used as controllers, providing us more versatility in our User Input mechanisms.


### Xbox Controllers

The team often uses xbox controllers to control the robot - they have a lot of buttons and are easy to understand! Luckily, instead of having to remember button IDs, WPILib provides the `CommandXboxController` class. Assigning buttons is as easy as `controller.b().onTrue(...)` . Simply specify the button and watch your action get executed. One special feature of Xbox Controllers is that they can **rumble**, sending a vibration to the driver based on a certain trigger to notify them of an event. If the robot is in position to shoot a ball, for example, send the driver a rumble so that they can gain additional information without having to eyeball anything. 

#### Basic Xbox Controller Binding

```java
    // Example: bind A button to a command
    new JoystickButton(driverController, XboxController.Button.kA.value)
        .whileTrue(new RunIntakeCommand());
```

### Joysticks

Joysticks are older controllers that have many buttons and are useful for testing. Simply press a button and trigger an action. These buttons are useful for actions that require instant activation like shooting or pneumatic activations. You can map buttons pretty easily: `new JoystickButton(js, 1).whileTrue(new RunIntakeCommand())`. Joysticks are limited in their functionality nowadays due to less ergonomic design and less intuitive control mechanisms.

#### Basic Joystick Binding

```java
// Example: Bind button 1 to a command
new JoystickButton(operatorJoystick, 1)
    .whileTrue(new RunShooterCommand())
```

### Common features

A **deadband** is a small range of input values around zero that are intentionally treated as zero. Real joysticks do not always perfectly return to a value of exactly 0.0. For example, if a deadband of 0.08 is set, a raw input of -0.03 or 0.05 will be treated as 0. Deadbands stop motors from whining and overheating and drivetrains creeping. An Xbox Controller would implement a deadband with `applyDeadband(XboxController.getRightX(), 0.08)`

For both Joysticks and Xbox Controllers, the y-value of the joysticks are **inverted**. To fix this, simply multiply the value recieved by a joystick by -1.
