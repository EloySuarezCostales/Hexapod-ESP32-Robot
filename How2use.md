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


## Velocity

If you want to change the velocity from the different movements, you could determine the time you would like each movement to last.

DURATION_MOV: is the time that leg lasts to put it up.

DURATION_TOTAL_SPIN: is the total time that takes the hexapod to complete a spin of 20 degrees.

RIPPLE_PAIR_STEP_SECONDS: is the time taken by each pair of legs to move forward in seconds

TRIPOD_STEP_SECONDS: is the time taken by each tripod of legs to move forward in seconds

WAVE_GAIT_SECONDS: is the time taken by each leg to move forward in seconds

DANCE_STEP_SECONDS: is the time taken for each of the 6 steps of the dance

DANCE_LEAN_SECONDS: this is the time taken for each movement each time you execute a single leaning movement

DANCE_PAUSE_MS: this is the lapse of time between each dance movement

STATIC_YAW_SECONDS: this is the time taken to do the yaw spin


## Activate legs

This is a very useful file created just for the using of a function used in the main.cpp called activeLegsConfiguration. With this function you can select the legsyou want to deactivate in case they are broken or unuseful for any reason or maybe because you want to move just one leg so as to calibrate it. The fucntion is given 6 booleans one for each leg.

activeLegsConfiguration(true, true, true, true, true, true);
    //                  0      1      2     3      4      5

## Calibration mode

If you look at the platformio.ini file you would see two environments. The default one is the one related with the hexapod and executes every action. The other environment is the one with which you could calibrate your servo. This is the file called calibrationServo.cpp, to use this file you would have to go in the Visual Studio to the icon of Platformio with an icon similar to an alien. Once you are in there go to the calibrationServo project and press Upload and monitor. 

To choose which servo you would like to move or calibrate in the calibrationServo.cpp file, you would have to modify the pca that is control taht could be pca0(0x40) or pca1(0x41), and then select the servo you want to move by selecting its channel in the 9th line. Everytime you want to change the pca that you are using you would have to check that the new pca is updated in the whole file.

## Dance

This is not a necessary movement, but in case you wanna do it, I suggest you to calibrate your own dance instead of copying my own calibration because it would depend on many things, so it will probably be different for every hexapod. The idea of the dance is that the robot leans on every leg doing sort of a wave. We have one command for each single movement and for the dance we execute every single movement within a separation of (DANCE_PAUSE_MS). As you could check in my code this is my final calibration.

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
