---
title: "Basic Motor Control"
---

Motors are the backbone of FRC power transmission. They convert power into rotary motion in the motor shaft - motors used in FRC are incredibly powerful. This section will cover simple control of motors in FRC.

### Motors

In FRC, you do not directly control a motor. Instead, you send signals to a Motor Controller (SparkMax, TalonFX) which controls the motor's power for you. This makes controlling the motors much easier because you don't have to manually write control code, you just set it's input power percentage/voltage.

For example, the SparkMAX can be controlled as such: `intakeMotor.set(1.0)` - what does this do? This tells the motor controller that you would like 100% power to be supplied to the motor - full speed. What do you think `intakeMotor.set(-1.0)` would do? Full reverse speed! Motors can also be controlled to go backwards as shown.

You can create a motor in your code just like any other constructor, such as `TalonFX armMotor = new TalonFX(1)` - what does the 1 mean? 1 is the CAN address of the device. You can think of it as sending a letter - the letter tells the motor controller what to do, and the CAN address is like the address so that it can get to the right place.

### Types of Motor Controllers

The two main types of motor controllers are the SparkMAX and TalonFX. The SparkMAX controls REV Robotics motors and the TalonFX (mostly) controls Kraken motors. You don't need to know all about the actual motors, just that each one should be controlled through their respective motor controller.

Each motor requires its own Vendor Library in the robot project - REVlib for the SparkMAX and Phoenix 6 for the TalonFX. You must install these through the vendor dependency manager in WPILib to use these controllers!

### Configuring Motors

One of the most important things in code is configuring your motors properly. The two main features you'll use are the idle/neutral mode and inversion. A motor's idle mode specifies if it will try and resist motion (brake) or not (coast) when no power is applied. Inversion specifies if positive power (ex. 100%, 45%) should spin clockwise or counterclockwise - useful in a gearbox or when mounted strangely.

For example, to configure a SparkMAX, you would do `SparkMaxConfig config = new SparkMaxConfig().withIdleMode(IdleMode.kBrake)` and `motorController.configure(config)` to set the motor the SparkMAX controls into brake mode.

There are many other ways to control motors - such as built-in PID controllers, CTRE's Motion Magic, and a couple others - but these are more advanced.
