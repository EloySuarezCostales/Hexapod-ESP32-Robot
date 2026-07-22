# How to Use

## Serial commands

### `u` - Stand up

Moves the robot from the sitting position to the support position.  
The servos move smoothly using time-based interpolation.

### `d` - Sit down

Returns the robot from the support position to the initial sitting posture.

### `q` - Static yaw left

Rotates the body slightly to the left while the feet remain fixed on the ground.  
This movement can be useful for scanning the surrounding area without changing the robot’s position.

### `e` - Static yaw right

Rotates the body slightly to the right while the feet remain fixed on the ground.  
Like the left yaw movement, it is intended for static scanning or sensor-based navigation.

### `c` - Return to centre

Returns the robot to the centred support position after a static yaw movement or a dance lean movement.  
After using an individual static movement, the robot must return to centre before executing another movement.

### `v` - Dance lean towards leg 0

Shifts the body weight towards leg 0 using a calibrated static posture.  
This command is mainly used for testing and calibrating the dance movement.

### `z` - Dance lean towards leg 1

Shifts the body weight towards leg 1 using a calibrated static posture.

### `n` - Dance lean towards leg 2

Shifts the body weight towards leg 2 using a calibrated static posture.

### `b` - Dance lean towards leg 3

Shifts the body weight towards leg 3 using a calibrated static posture.

### `x` - Dance lean towards leg 4

Shifts the body weight towards leg 4 using a calibrated static posture.

### `m` - Dance lean towards leg 5

Shifts the body weight towards leg 5 using a calibrated static posture.

### `o` - Automatic dance sequence

Executes the full dance sequence.  
The robot shifts its body weight from leg to leg without returning to the centre between each step, creating a continuous dance-like movement.  
At the end of the sequence, the robot automatically returns to the centred support position.

### `r` - Spin right

Executes a right spin movement using tripod-based support phases.

### `l` - Spin left

Executes a left spin movement using tripod-based support phases.

### `w` - Wave gait forward

Executes the wave gait forward sequence.  
This gait moves the legs in a highly stable order, making it suitable for slower and more controlled movement.

### `g` - Ripple gait forward

Executes the ripple gait forward sequence.  
This gait moves pairs of legs in a coordinated pattern, providing a balance between stability and speed.

### `t` - Tripod gait forward

Executes the tripod gait forward sequence.  
This gait moves two groups of three legs alternately and is designed for faster movement on more regular surfaces.

### `p` - Blink bottom LED ring

Makes the 60-LED bottom ring blink three times.


## Movement Timing and Speed

The speed of the different movements can be adjusted by modifying the timing parameters used in the code. These values define how long each movement or movement phase takes to complete.

- `DURACION_MOV`: defines the duration of the general leg movement used in posture transitions.

- `DURACION_TOTAL_SPIN`: defines the total time required for the hexapod to complete a spin movement of approximately 20 degrees.

- `RIPPLE_PAIR_STEP_SECONDS`: defines the time taken by each pair of legs to move forward during the ripple gait.

- `TRIPOD_STEP_SECONDS`: defines the time taken by each tripod group to move during the tripod gait.

- `WAVE_GAIT_SECONDS`: defines the time taken by each individual leg to move forward during the wave gait.

- `DANCE_STEP_SECONDS`: defines the time taken for each transition inside the automatic dance sequence.

- `DANCE_LEAN_SECONDS`: defines the time taken when executing an individual dance leaning movement.

- `DANCE_PAUSE_MS`: defines the delay between each movement inside the automatic dance sequence.

- `STATIC_YAW_SECONDS`: defines the time taken to perform a static yaw movement.


## Active Leg Selection

The project includes an active-leg selection system, which is useful for testing, debugging, and calibration. This system allows specific legs to be enabled or disabled from the main program.

This can be helpful if one leg is damaged, incorrectly calibrated, or temporarily not needed during testing. It is also useful when calibrating a single leg independently, since the rest of the legs can be disabled while only the selected leg is allowed to move.

The function receives six Boolean values, one for each leg:

configurarPatasActivas(true, true, true, true, true, true);
//                    0     1     2     3     4     5


## Calibration Mode

The `platformio.ini` file contains two different environments. The default environment is used to upload and execute the main hexapod control program. The second environment is used for servo calibration and runs the `calibrationServo.cpp` file.

To use the calibration environment, open the project in Visual Studio Code and go to the PlatformIO menu, which is represented by the alien-shaped icon. From there, select the calibration environment and press **Upload and Monitor**.

To choose which servo you want to move or calibrate, open `calibrationServo.cpp`. In this file, you must select the PCA9685 driver that controls the servo, either `pca0(0x40)` or `pca1(0x41)`, and then select the corresponding servo channel.

Every time you change the PCA9685 driver being used, make sure that the selected driver is updated consistently throughout the calibration file.

## Dance

## Dance

The dance movement is not essential for the basic operation of the robot, but it was added as an experimental and visual movement feature. If another hexapod uses this code, the dance movement should be calibrated again, since the correct angles will depend on the servo orientation, mechanical assembly, weight distribution, leg geometry, and individual calibration of each robot.

The idea of the dance is to shift the robot’s body weight from one leg to another, creating a wave-like motion around the body. There is one individual command for each leaning movement, and the automatic dance function executes all of them sequentially with a delay defined by `DANCE_PAUSE_MS`.

For individual leaning commands, the robot must return to the centre before executing any other movement. However, during the automatic dance sequence, the robot moves directly from one leaning posture to the next without returning to the centre between steps. This makes the movement more continuous and dance-like.

The following arrays show the final calibration used in this project:

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


These values should be understood as a hardware-specific calibration rather than a universal configuration.
