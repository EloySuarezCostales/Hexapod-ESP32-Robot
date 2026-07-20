# How to Use

## Serial commands

| Command | Action |
|---|---|
| 'u' | Stand up |
| 'd' | Sit down |
| 'r' | Spin right |
| 'l' | Spin left |
| 'p' | Blink the bottom LED ring |
| 'w' | Wave gait forward |
| 'g' | Ripple gait forward |

### 'u' - Stand up

Moves the robot from the sitting position to the support position.  
The servos move smoothly using time-based interpolation.

### 'd' - Sit down

Returns the robot to the initial sitting posture.

### 'r' - Spin right

Executes a right spin movement using tripod-based support phases.

### 'l' - Spin left

Executes a left spin movement using tripod-based support phases.

### 'b' - blinking LEDs ring

The 60 LEDs ring blinks 3 times, I mean, it switches on and off.

### 'w' - Wave gait

Executes the whole wave gait it makes one step forward.

### 'g' - Ripple gait

Executes the whole ripple gait forward, it makes two step forward.

### 'w' - Wave gait

Executes the whole wave agait forward, it makes two steps forward.


## Velocity

If you want to change the velocity from the different movements, you could determine the time you would like each movement to last.

DURATION_MOV: is the time that leg lasts to put it up.
DURATION_TOTAL_SPIN: is the total time that takes the hexapod to complete a spin of 20 degrees.
RIPPLE_PAIR_STEP_SECONDS: is the time taken by each pair of legs to move forward in seconds
TRIPOD_STEP_SECONDS: is the time taken by each tripod of legs to move forward in seconds
WAVE_GAIT_SECONDS: is the time taken by each leg to move forward in seconds

## Activate legs

This is a very useful file created just for the using of a function used in the main.cpp called activeLegsConfiguration. With this function you can select the legsyou want to deactivate in case they are broken or unuseful for any reason or maybe because you want to move just one leg so as to calibrate it. The fucntion is given 6 booleans one for each leg.

activeLegsConfiguration(true, true, true, true, true, true);
    //                  0      1      2     3      4      5

## Calibration mode

If you look at the platformio.ini file you would see two environments. The default one is the one related with the hexapod and executes every action. The other environment is the one with which you could calibrate your servo. This is the file called calibrationServo.cpp, to use this file you would have to go in the Visual Studio to the icon of Platformio with an icon similar to an alien. Once you are in there go to the calibrationServo project and press Upload and monitor. 

To choose which servo you would like to move or calibrate in the calibrationServo.cpp file, you would have to modify the pca that is control taht could be pca0(0x40) or pca1(0x41), and then select the servo you want to move by selecting its channel in the 9th line. Everytime you want to change the pca that you are using you would have to check that the new pca is updated in the whole file.


