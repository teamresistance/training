---
title: "Sensors in FRC"
---
An overview of common FRC sensors, how they work, and how we use them to create reliable robot behavior.
### Banner Sensors

Banner sensors are small optical sensors used for object detection.
- Digital output (true/false)
- Fast and reliable
- Detects if something is in the way - super simple

#### Example (Digital Input)

```
`private DigitalInput banner = new DigitalInput(0);

public boolean hasPiece() {
    return banner.get();
}
`
```

### Encoders

Encoders measure rotation accurately and are used to know how many times a motor has rotated.
#### Types of Encoders

- **Integrated encoders:**Neo/Kraken built-in sensors
- **External encoders:**SRX Mag, Through-Bore
- **Absolute encoders:**Gives the true angle at startup
- **Relative encoders:**Counts movement from zero, wherever it was when it powered on is "0 rotations"

#### Example (SparkMAX Built-In Relative Encoder)

```
`private RelativeEncoder encoder = sparkMotorController.getEncoder();

public double getPosition() {
    return encoder.getDistance();
}
`
```

### Absolute vs Relative Encoders

#### Absolute Encoders

- Know angle on startup
- Used particularly on swerve, helpful in other places if precision is absolutely needed
- Not affected by missed counts

#### Relative Encoders

- Start at 0 on boot
- Require homing
- Used for mostly everything that doesn't need to be ultra-precise or can't be reasonably put in a home position

### Limit Switches

Limit switches detect endpoints of travel and protect mechanisms.
- Not as common anymore
- Digital input (true/false)
- Often used for homing

#### Example (Limit Switch)

```
`private DigitalInput limit = new DigitalInput(1);

public boolean atHome() {
    return limit.get();
}
`
```

### Homing a Mechanism

Homing establishes a known zero position for a mechanism.
#### Common Homing Methods

- Drive into a limit switch → reset encoder
- Move slowly until hard-stop → reset encoder
- Put the mechanism in the right place before powering on the robot

#### Example (Homing using a limit switch)

```
`if (limitSwitch.get()) {
    encoder.setPosition(0);
}
`
```
