---
title: "Making Use of Vendor Features"
---

Modern FRC motor controllers are not dumb speed controllers. TalonFXs and Spark MAXes contain onboard sensors, PID loops, motion profiling, current limiting, and safety logic. This page documents how those features actually work, when to use them, and how to configure them correctly in real robots.

## Why Use Onboard Vendor Control?

Vendor-side control runs directly on the motor controller, at a significantly higher frequency instead of the roboRIO’s 50 Hz loop. This gives:

- Lower latency and smoother motion
- Better handling of battery usage and CAN bandwidth usage
- Less complex code, as the motor controller firmware actually does stuff with your configuration

## TalonFX Integrated PID (Kraken x60/x44)

TalonFX-powered motors (krakens) contain an internal PID controller that can close the loop on position, velocity, or motion profiles using the built-in encoder.

## What Runs on the Motor

- Normal PID loop (P, I, D)
- Feedforward (kS, kV, kA, kG)
- Motion profiling (Motion Magic!!)
- Current limiting

When you call`setControl()`, the roboRIO sends a target, not raw motor power. The TalonFX then handles the control loop internally.

## Motion Magic (Kraken x60/x44)

Motion Magic is CTRE’s trapezoidal motion profiler built into the motor controller. You provide a target position, max velocity, and max acceleration.

## How It Works

1. The TalonFX generates a velocity profile internally
1. Velocity is fed into the PID + feedforward loop
1. The motor smoothly accelerates, cruises, and decelerates

This removes the need to write your own profiling code on the RIO and ensures motion stays smooth even during slowdowns caused by CAN overuse, code running slow, roboRIO issues, etc.

MotionMagic can be skipped for most cases (for normal positional control), but it can be useful in scenarios where you want to accelerate smoothly and avoid jerk, such as in long arms, light elevators, mechanisms with high backlash, etc.

## Spark MAX Integrated PID (NEO, Vortex, 550)

Spark MAX controllers include an onboard PID controller that works with either the NEO’s internal encoder or an external encoder. Basically the same as the TalonFX.

## Control Modes

- Velocity control
- Position control
- Smart Motion / MAXMotion

Like CTRE, once configured, the Spark MAX executes the control loop without relying on the roboRIO timing.

## MAXMotion Position Control

MAXMotion is REV’s equivalent to Motion Magic. It combines position PID with motion constraints to generate smooth movement profiles.

## What You Configure

- Maximum velocity
- Maximum acceleration
- Allowed closed-loop error

The Spark MAX handles the ramping internally, preventing aggressive starts and stops that damage gearboxes or trip breakers.

## Vendor Configuration / Control Programs

## CTRE Tuner X

Tuner X is used to configure CTRE devices such as TalonFXs, Pigeon2s (CTRE gyroscope), CANdles (LED controller), and more. It is used to:

- Firmware updates (SHOULD BE DONE REGULARLY!!)
- Set CAN IDs (needs to be done to new devices, especially when first starting to put code on the robot)
- Calibrate encoders
- Live-tune PID and feedforward
- Verify sensor direction and motor inversion
- Manually control and configure devices instead of re-deploying code with new values every time

Often times it's faster to use Tuner X to quickly test new PID control, current limits, or other configuration instead of updating your code and redeploying.

## REV Hardware Client

The REV Hardware Client is used to configure REV devices, primarily SparkMAX controllers. Tuner X and REV client are very similar in use, just for different vendors. It provides:

- Firmware updates (SHOULD BE DONE REGULARLY!!)
- Set CAN IDs (needs to be done to new devices, especially when first starting to put code on the robot)
- Calibrate encoders
- Live-tune PID and feedforward
- Verify sensor direction and motor inversion
- Manually control and configure devices instead of re-deploying code with new values every time

## Best Practices

- Always set current and speed limits before enabling closed-loop control, over time sending 60 amps to a motor (even for a split second) can damage it.
- Configure the basics before testing anything control-wise
- Log errors and faults during testing
- Please, try to simulate your code before putting it on a robot unless its heavily based on factors that only exist in the real world
- Try to view data as it is being tested using one of these tools if not AdvantageScope. More data means more things to make better!

## Summary

Vendor motor controllers provide powerful features that dramatically simplify robot code when used correctly. Understanding what runs on the controller versus the RIO is essential for building reliable, high-performance mechanisms.
