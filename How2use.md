# How to Use

## Serial Commands

The hexapod is controlled through the Serial Monitor.  
Each command is sent as a single character followed by Enter.

---

## Command Summary

| Command | Action |
|---|---|
| `u` | Stand up |
| `d` | Sit down |
| `q` | Static yaw left |
| `e` | Static yaw right |
| `h` | Raise body height |
| `j` | Lower body height |
| `c` | Return to default support position |
| `v` | Dance lean towards leg 0 |
| `z` | Dance lean towards leg 1 |
| `n` | Dance lean towards leg 2 |
| `b` | Dance lean towards leg 3 |
| `x` | Dance lean towards leg 4 |
| `m` | Dance lean towards leg 5 |
| `o` | Automatic dance sequence |
| `r` | Spin right |
| `l` | Spin left |
| `w` | Wave gait forward |
| `g` | Ripple gait forward |
| `t` | Tripod gait forward |
| `p` | Blink bottom LED ring |

---

## Posture Commands

### `u` - Stand up

Moves the robot from the sitting position to the default support position.

The servos move smoothly using time-based interpolation.  
This command should be used before executing any walking, spinning, static movement, dance movement, or body-height adjustment.

This command is blocked if the body height has been modified.  
If the body has been raised or lowered using `h` or `j`, the robot must first return to the default support position using command `c`.

---

### `d` - Sit down

Returns the robot from the support position to the initial sitting posture.

This command is blocked if the body height has been modified.  
If the robot has been raised or lowered using `h` or `j`, it must first return to the default support position using command `c`.

---

## Static Body Movements

### `q` - Static yaw left

Rotates the body slightly to the left while the feet remain fixed on the ground.

This movement can be useful for scanning the surrounding area without changing the robot’s position.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `e` - Static yaw right

Rotates the body slightly to the right while the feet remain fixed on the ground.

Like the left yaw movement, it is intended for static scanning or sensor-based navigation.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

## Body Height Adjustment

### `h` - Raise body height

Raises the robot body by one height step.

This command modifies the active support position of the robot.  
After using `h`, the new raised posture becomes the current support position, so the robot can continue walking using this new body height.

The command can be used multiple times in a row:

```text
h
h
h
```

Each time the command is executed, the body is raised one additional step.

There is no fixed software limit on the number of times this command can be used.  
The practical limit depends on the mechanical range of the servos, the leg geometry, the power supply, and the operator’s judgement.

The amount of movement is controlled mainly by:

```cpp
STATIC_LIFT_FEMUR_STEP
STATIC_LIFT_TIBIA_UP_STEP
STATIC_LIFT_SECONDS
```

`STATIC_LIFT_TIBIA_UP_STEP` defines how much the tibias open when the body is raised.

---

### `j` - Lower body height

Lowers the robot body by one height step.

This command also modifies the active support position.  
After using `j`, the new lowered posture becomes the current support position, so the robot can continue walking using this new body height.

The command can be used multiple times in a row:

```text
j
j
j
```

Each time the command is executed, the body is lowered one additional step.

There is no fixed software limit on the number of times this command can be used.  
The practical limit depends on the mechanical range of the servos, the leg geometry, the power supply, and the operator’s judgement.

The amount of movement is controlled mainly by:

```cpp
STATIC_LIFT_FEMUR_STEP
STATIC_LIFT_TIBIA_DOWN_STEP
STATIC_LIFT_SECONDS
```

`STATIC_LIFT_TIBIA_DOWN_STEP` defines how much the tibias close when the body is lowered.

---

### Purpose of the body-height system

The body-height adjustment system was added to help the robot pass over obstacles.

For example, if the robot needs to move over an object, the operator can raise the body using `h`, continue walking using one of the gait commands, and later return to the default support position using `c`.

Example:

```text
u
h
h
w
g
j
t
c
```

In this example:

1. The robot stands up.
2. The body is raised twice.
3. The robot walks using the raised support posture.
4. The body is lowered once.
5. The robot continues walking.
6. The robot returns to the default support position.

The gait functions use the active support position, so the robot does not need to return to the default support position before walking.

---

### Movements blocked after height adjustment

Some movements are blocked while the body height is modified because they rely on calibrated default postures.

The following movements are blocked after using `h` or `j`:

- stand up
- sit down
- static yaw left
- static yaw right
- individual dance movements
- automatic dance sequence

Before executing any of these movements, the robot must return to the default support position using command `c`.

Walking gaits can still be executed after using `h` or `j`, because they use the current active support position.

---

## Return to Default Support Position

### `c` - Return to default support position

Returns the robot to the default support position.

This command is used after:

- a static yaw movement
- an individual dance lean movement
- one or more body-height changes using `h` or `j`

When the body height has been modified, command `c` restores the original default support posture saved when the robot first stood up.

This allows the operator to temporarily change the height of the robot, walk using the modified height, and later return to the original support posture.

---

## Dance Commands

### `v` - Dance lean towards leg 0

Shifts the body weight towards leg 0 using a calibrated static posture.

This command is mainly used for testing and calibrating the dance movement.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `z` - Dance lean towards leg 1

Shifts the body weight towards leg 1 using a calibrated static posture.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `n` - Dance lean towards leg 2

Shifts the body weight towards leg 2 using a calibrated static posture.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `b` - Dance lean towards leg 3

Shifts the body weight towards leg 3 using a calibrated static posture.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `x` - Dance lean towards leg 4

Shifts the body weight towards leg 4 using a calibrated static posture.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `m` - Dance lean towards leg 5

Shifts the body weight towards leg 5 using a calibrated static posture.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

### `o` - Automatic dance sequence

Executes the full dance sequence.

The robot shifts its body weight from leg to leg without returning to the center between each step, creating a continuous dance-like movement.

At the end of the sequence, the robot automatically returns to the centered support position.

This command is blocked if the body height has been modified.  
The robot must first return to the default support position using command `c`.

---

## Spin Commands

### `r` - Spin right

Executes a right spin movement using tripod-based support phases.

The movement is based on alternating support and lifted leg groups.  
The coxa servos move towards calibrated extreme positions while the other legs keep the robot supported.

---

### `l` - Spin left

Executes a left spin movement using tripod-based support phases.

Like the right spin, this movement uses alternating leg groups to rotate the body while maintaining support.

---

## Gait Commands

### `w` - Wave gait forward

Executes the wave gait forward sequence.

This gait moves the legs in a highly stable order, making it suitable for slower and more controlled movement.

The wave gait uses the current active support position.  
This means it can be executed after raising or lowering the body with `h` or `j`.

---

### `g` - Ripple gait forward

Executes the ripple gait forward sequence.

This gait moves pairs of legs in a coordinated pattern, providing a balance between stability and speed.

The ripple gait uses the current active support position.  
This means it can be executed after raising or lowering the body with `h` or `j`.

---

### `t` - Tripod gait forward

Executes the tripod gait forward sequence.

This gait moves two groups of three legs alternately and is designed for faster movement on more regular surfaces.

The tripod gait uses the current active support position.  
This means it can be executed after raising or lowering the body with `h` or `j`.

---

## LED Command

### `p` - Blink bottom LED ring

Makes the 60-LED bottom ring blink three times.

This command is mainly used as a visual feedback test for the bottom LED ring.

---

# Parameters

This section lists the main parameters that can be adjusted to tune the behaviour of the hexapod.

Most of these values are hardware-specific.  
They depend on the servo orientation, mechanical assembly, robot weight, leg geometry, power supply, and calibration of each individual robot.

---

## General Movement Parameters

### `SERVO_UPDATE_INTERVAL_MS`

Controls the update interval between servo interpolation steps.

A lower value makes the movement update more frequently and can make the motion smoother, but it also increases the number of commands sent to the servos.

Example:

```cpp
int SERVO_UPDATE_INTERVAL_MS = 90;
```

---

### `POSTURE_MOVEMENT_SECONDS`

Defines the duration of the general posture transitions, such as standing up and sitting down.

Higher values make posture transitions slower and smoother.  
Lower values make them faster but more abrupt.

Example:

```cpp
float POSTURE_MOVEMENT_SECONDS = 3.0f;
```

---

### `TOTAL_SPIN_SECONDS`

Defines the total time used to execute a spin movement.

Higher values make the spin slower and more controlled.  
Lower values make the spin faster.

Example:

```cpp
float TOTAL_SPIN_SECONDS = 4.0f;
```

---

## Static Height Parameters

### `STATIC_LIFT_SECONDS`

Defines the time taken to raise or lower the body height by one step.

Example:

```cpp
float STATIC_LIFT_SECONDS = 1.0f;
```

---

### `STATIC_LIFT_FEMUR_STEP`

Defines how much the femur servos move during each body-height step.

This value is used both when raising and lowering the body.

Example:

```cpp
int STATIC_LIFT_FEMUR_STEP = 15;
```

---

### `STATIC_LIFT_TIBIA_UP_STEP`

Defines how much the tibia servos move when the body is raised using command `h`.

This parameter is independent from the lowering tibia movement because the tibias may need to open faster when raising the body.

Example:

```cpp
int STATIC_LIFT_TIBIA_UP_STEP = 15;
```

---

### `STATIC_LIFT_TIBIA_DOWN_STEP`

Defines how much the tibia servos move when the body is lowered using command `j`.

This parameter is independent from the raising tibia movement because the tibias may need a different closing movement when lowering the body.

Example:

```cpp
int STATIC_LIFT_TIBIA_DOWN_STEP = 10;
```

---

## Static Yaw Parameters

### `STATIC_YAW_SECONDS`

Defines the time taken to perform a static yaw movement.

Example:

```cpp
float STATIC_YAW_SECONDS = 1.0f;
```

---

### `COXA_YAW_LEFT`

Defines the coxa target angle used for the static yaw left movement.

Example:

```cpp
static const int COXA_YAW_LEFT = 40;
```

---

### `COXA_YAW_RIGHT`

Defines the coxa target angle used for the static yaw right movement.

Example:

```cpp
static const int COXA_YAW_RIGHT = 140;
```

---

## Spin Parameters

### `COXA_LEFT_EXTREME`

Defines one of the coxa extreme positions used during spin movements.

Example:

```cpp
static const int COXA_LEFT_EXTREME = 70;
```

---

### `COXA_RIGHT_EXTREME`

Defines the opposite coxa extreme position used during spin movements.

Example:

```cpp
static const int COXA_RIGHT_EXTREME = 110;
```

---

### `LIFT_DELTA`

Defines how much the legs are lifted during the spin movement.

In the spin module, this parameter controls the femur and tibia offset used when a tripod group is lifted.

Example:

```cpp
static const int LIFT_DELTA = 25;
```

---

### `BLOCK_PAUSE_MS`

Defines the pause between spin movement blocks.

A higher value makes the spin more segmented and slower.  
A lower value makes the transition between spin phases faster.

Example:

```cpp
static const int BLOCK_PAUSE_MS = 500;
```

---

## Tripod Gait Parameters

### `TRIPOD_STEP_SECONDS`

Defines the duration of each tripod movement phase.

Higher values make the tripod gait slower and more controlled.  
Lower values make it faster.

Example:

```cpp
static const float TRIPOD_STEP_SECONDS = 1.5f;
```

---

### `SUPPORT_PAUSE_MS`

Defines the pause between support phases in the tripod gait.

Example:

```cpp
static const int SUPPORT_PAUSE_MS = 300;
```

---

### `LIFT_DELTA`

Defines how much the legs are lifted during the tripod gait.

This value may appear locally inside the tripod gait file.  
It controls how much the femur and tibia angles change when a tripod group is lifted.

Example:

```cpp
static const int LIFT_DELTA = 25;
```

---

### `YAW_LEFT`

Defines a yaw or coxa offset used during a turning or directional tripod movement, if enabled in the gait version.

This value can be adjusted to increase or decrease the amount of lateral rotation.

Example:

```cpp
static const int YAW_LEFT = 20;
```

---

## Ripple Gait Parameters

### `RIPPLE_PAIR_STEP_SECONDS`

Defines the time taken by each pair of legs to move forward during the ripple gait.

Higher values make the ripple gait slower and more stable.  
Lower values make it faster.

Example:

```cpp
static const float RIPPLE_PAIR_STEP_SECONDS = 1.5f;
```

---

### `LIFT_DELTA`

Defines how much the selected legs are lifted during the ripple gait.

Example:

```cpp
static const int LIFT_DELTA = 15;
```

---

## Wave Gait Parameters

### `NUM_LEGS`

Defines the number of legs used by the gait logic.

For this hexapod, the value is always 6.

Example:

```cpp
static const int NUM_LEGS = 6;
```

---

### `WAVE_LEG_STEP_SECONDS`

Defines the time taken by each individual leg to move forward during the wave gait.

The wave gait moves one leg at a time, so this parameter has a strong effect on the total duration of the gait cycle.

Example:

```cpp
static const float WAVE_LEG_STEP_SECONDS = 1.5f;
```

---

### `LIFT_DELTA`

Defines how much each individual leg is lifted during the wave gait.

Example:

```cpp
static const int LIFT_DELTA = 15;
```

---

## Dance Parameters

### `DANCE_LEAN_SECONDS`

Defines the time taken when executing an individual dance leaning movement.

Example:

```cpp
float DANCE_LEAN_SECONDS = 0.4f;
```

---

### `DANCE_STEP_SECONDS`

Defines the time taken for each transition inside the automatic dance sequence.

Example:

```cpp
float DANCE_STEP_SECONDS = 0.6f;
```

---

### `DANCE_PAUSE_MS`

Defines the delay between each movement inside the automatic dance sequence.

Example:

```cpp
static const int DANCE_PAUSE_MS = 100;
```

---

## Servo Calibration Parameters

### `SERVO_MIN`

Defines the minimum PWM pulse used for servo angle mapping.

Example:

```cpp
int SERVO_MIN = 150;
```

---

### `SERVO_MAX`

Defines the maximum PWM pulse used for servo angle mapping.

Example:

```cpp
int SERVO_MAX = 600;
```

---

## Parameter Tuning Notes

The values included in this project are calibrated for this specific robot.

When using the code on another hexapod, the following parameters will probably need to be adjusted:

- servo pulse limits
- support position angles
- sitting position angles
- gait lift values
- coxa forward and backward angles
- static yaw angles
- spin coxa extremes
- body-height adjustment values
- dance calibration arrays
- movement durations

Small changes should be tested first.  
Large changes in servo angles can create unstable movements, excessive current peaks, or mechanical stress.

---

# Active Leg Selection

The project includes an active-leg selection system, which is useful for testing, debugging, and calibration.

This system allows specific legs to be enabled or disabled from the main program.

This can be helpful if:

- one leg is damaged
- one servo is incorrectly calibrated
- only one leg needs to be tested
- the robot is being debugged progressively
- the power supply is not ready to move all legs at once

The function receives six Boolean values, one for each leg:

```cpp
configureActiveLegs(true, true, true, true, true, true);
//                  0     1     2     3     4     5
```

Each value corresponds to one leg of the robot.

A value of `true` enables the leg.  
A value of `false` disables the leg.

Example for testing only leg 4:

```cpp
configureActiveLegs(false, false, false, false, true, false);
//                   0      1      2      3      4     5
```

Before using the full robot, all legs should be enabled again:

```cpp
configureActiveLegs(true, true, true, true, true, true);
```

---

# Calibration Mode

The `platformio.ini` file contains two different environments.

The default environment is used to upload and execute the main hexapod control program.

The second environment is used for servo calibration and runs the `servoCalibration.cpp` file.

---

## Main environment

The main environment compiles the full robot program.

```ini
[env:esp32dev]
build_src_filter =
    +<*>
    -<servoCalibration.cpp>
```

This environment excludes `servoCalibration.cpp`, so only the main robot firmware is compiled.

---

## Servo calibration environment

The calibration environment compiles only the servo calibration file.

```ini
[env:servo_calibration]
build_src_filter =
    -<*>
    +<servoCalibration.cpp>
```

This avoids compiling two different files with `setup()` and `loop()` at the same time.

---

## How to use calibration mode

To use the calibration environment:

1. Open the project in Visual Studio Code.
2. Open the PlatformIO menu.
3. Select the calibration environment.
4. Press **Upload and Monitor**.

To choose which servo you want to move or calibrate, open `servoCalibration.cpp`.

In this file, select the PCA9685 driver that controls the servo:

```cpp
Adafruit_PWMServoDriver pca0(0x40);
```

or:

```cpp
Adafruit_PWMServoDriver pca1(0x41);
```

Then select the corresponding servo channel.

Every time the PCA9685 driver is changed, make sure that the selected driver is updated consistently throughout the calibration file.

---

# Dance

The dance movement is not essential for the basic operation of the robot, but it was added as an experimental and visual movement feature.

If another hexapod uses this code, the dance movement should be calibrated again, since the correct angles will depend on:

- servo orientation
- mechanical assembly
- weight distribution
- leg geometry
- individual calibration of each robot

The idea of the dance is to shift the robot’s body weight from one leg to another, creating a wave-like motion around the body.

There is one individual command for each leaning movement, and the automatic dance function executes all of them sequentially with a delay defined by `DANCE_PAUSE_MS`.

For individual leaning commands, the robot must return to the default support position before executing any other movement.

However, during the automatic dance sequence, the robot moves directly from one leaning posture to the next without returning to the center between steps.  
This makes the movement more continuous and dance-like.

These values should be understood as a hardware-specific calibration rather than a universal configuration.

---

## Dance Calibration Values

```cpp
// ======================================================
// Calibration area
// ======================================================
//
// Leg numbering:
//
//      0
//   5     1
//
//   4     2
//      3
//
// Each group represents the full robot posture when the body
// leans towards one specific leg.

// ------------------------------------------------------
// Lean towards leg 0
// Command: v
// ------------------------------------------------------

static const int COXA_TO_LEG_0[6] = {
  90, 90, 90,
  90, 90, 90
};

static const int FEMUR_TO_LEG_0[6] = {
  160, 130, 75,
  135, 120, 65
};

static const int TIBIA_TO_LEG_0[6] = {
  130, 130, 70,
  100, 120, 60
};

// ------------------------------------------------------
// Lean towards leg 1
// Command: z
// ------------------------------------------------------

static const int COXA_TO_LEG_1[6] = {
  90, 90, 90,
  90, 90, 90
};

static const int FEMUR_TO_LEG_1[6] = {
  120, 145, 130,
  130, 145, 130
};

static const int TIBIA_TO_LEG_1[6] = {
  105, 125, 130,
  130, 140, 130
};

// ------------------------------------------------------
// Lean towards leg 2
// Command: n
// ------------------------------------------------------

static const int COXA_TO_LEG_2[6] = {
  90, 90, 90,
  90, 90, 90
};

static const int FEMUR_TO_LEG_2[6] = {
  90, 130, 160,
  65, 120, 135
};

static const int TIBIA_TO_LEG_2[6] = {
  90, 130, 130,
  60, 120, 100
};

// ------------------------------------------------------
// Lean towards leg 3
// Command: b
// ------------------------------------------------------

static const int COXA_TO_LEG_3[6] = {
  90, 90, 90,
  90, 90, 90
};

static const int FEMUR_TO_LEG_3[6] = {
  30, 95, 110,
  60, 75, 130
};

static const int TIBIA_TO_LEG_3[6] = {
  40, 80, 120,
  120, 80, 130
};

// ------------------------------------------------------
// Lean towards leg 4
// Command: x
// ------------------------------------------------------

static const int COXA_TO_LEG_4[6] = {
  90, 90, 90,
  90, 90, 90
};

static const int FEMUR_TO_LEG_4[6] = {
  65, 50, 65,
  65, 50, 65
};

static const int TIBIA_TO_LEG_4[6] = {
  60, 50, 60,
  60, 50, 60
};

// ------------------------------------------------------
// Lean towards leg 5
// Command: m
// ------------------------------------------------------

static const int COXA_TO_LEG_5[6] = {
  90, 90, 100,
  75, 90, 90
};

static const int FEMUR_TO_LEG_5[6] = {
  95, 95, 30,
  130, 75, 60
};

static const int TIBIA_TO_LEG_5[6] = {
  95, 90, 40,
  130, 80, 120
};

// Automatic dance order

static const int DANCE_SEQUENCE[6] = {
  0, 1, 2, 3, 4, 5
};
```

---

# Practical Use Example

A normal test sequence could be:

```text
u
w
g
t
c
d
```

A sequence for obstacle testing could be:

```text
u
h
h
w
g
j
t
c
d
```

A sequence for testing static movements could be:

```text
u
q
c
e
c
d
```

A sequence for testing dance movements could be:

```text
u
v
c
z
c
o
d
```

---

# Safety Notes

The robot uses many servos at the same time, so current peaks can be high.

Before testing full movements:

- make sure the servo power supply can provide enough current
- use a common ground between the ESP32, PCA9685 boards, LEDs, and servo power supply
- test movements slowly first
- avoid large angle changes without calibration
- keep the robot lifted or supported during early tests
- check that no leg is mechanically blocked
- monitor overheating in servos and voltage drops in the power supply

If the robot behaves unexpectedly, stop the test and return to a known safe posture.
