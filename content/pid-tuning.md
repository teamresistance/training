---
title: "Perfect PID Tuning"
---

This guide shows how to find near-perfect P, I, D, and F values for any mechanism, with a repeatable and precise tuning workflow.

### Find the Perfect P Value

The goal: maximum stiffness without oscillation.

#### 1. Increase P Until First Oscillation

Move to a setpoint far away (ex: 0 → 90°).

When you first see _clean_, rhythmic oscillation at the target → stop.

#### 2. Reduce P

Reduce P until you get to a very small amount of oscillation - it should still quickly go to its target. D can take care of the oscillation.

### Find the Perfect D Value

D should cancel oscillation without slowing the system.

#### 1. Add D Until Overshoot Stops

Increase D in tiny increments (0.0001–0.001 depending on scaling).

Watch the settling behavior:

- still oscillates → add more D
- sluggish / slow → too much D

#### 2. Target: Minimal Overshoot or Perfect Stop

The ideal D brings the mechanism to a stop exactly on it's target or overshoots minimally and can correct instantly.

### Find the Perfect I Value

Only used for eliminating long-term steady-state error.

#### 1. Check for Steady-State Error

If the mechanism stops short of the setpoint or sags under load → I needed.

#### 2. Increase I Until Drift Disappears

```java
controller.setI(I + very_small_step);
```

The mechanism should creep perfectly into the target after several seconds.

#### 3. If System Vibrates → I Too High

### Validation Tests for “Perfect” Tuning

#### 1. Step Response Test

Command min → max rapidly.

- minimal overshoot
- fast settle
- no chatter

#### 2. Hold Position Under Load

Push on the mechanism. It should resist without buzzing.

#### 3. Multi-Setpoint Sweep

Command several positions at various distances.

```java
0° → 30° → 90° → 45° → 75° → 10°
```

You want the same behavior no matter the distance.
