# Hardware and Build

## Hardware list

ESP32 Dev Module                                      x1
PCA9685 16-channel servo drivers                      x2
servo motors MG996R TowerPro                          x18
8 LED WS2812CB ring                                   x1
16 LED WS2812B ring                                   x1
60 LED WS2812B ring                                   x1
External Battery                                      x1
PCB personlised                                       x1

## Voltage and current considerations
The power system was one of the most important aspects of the build. The WS2812B LEDs require a 5V supply, while the PCA9685 logic is powered from 3.3V. The servo motors are powered separately using an external supply limited to a maximum voltage of 6V. The current limit was set to approximately 10.10A. Although this value may seem high, it is mainly intended to handle current peaks produced when several servos move at the same time. The robot is not expected to draw this amount of current continuously during normal operation, but having enough current margin helps prevent voltage drops, resets, and unstable servo behaviour. It is important that all grounds are connected together, including the ESP32 ground, the PCA9685 ground, the LED ground, and the external servo power supply ground.

## Pin configuration

| Component | Pin / Address |
|---|---|
| I2C SDA | GPIO 25 |
| I2C SCL | GPIO 26 |
| PCA9685 #1 | 0x40 |
| PCA9685 #2 | 0x41 |
| Main LED strips | GPIO 27 |
| LED ring | GPIO 14 |

## PCA9685 configuration

The PCA9685 servo driver allows multiple servos to be controlled using only the I2C bus. Each PCA9685 board provides 16 PWM channels, which is enough for 16 servos. Since the robot uses 18 servos in total, two PCA9685 boards are required. In this project, each PCA9685 controls one side of the robot. This means that each board controls 9 servos instead of using all 16 available channels. This distribution keeps the wiring more organized and makes the servo mapping easier to understand. To use two PCA9685 boards on the same I2C bus, each board must have a different I2C address. One board keeps the default address 0x40, while the second one is configured as 0x41 by soldering the corresponding address pad on the board. 

The servo distribution used in the code is shown below:

Pata patas[6] = {
  {0, 2, 1, 0},
  {0, 6, 5, 4},
  {0, 13, 14, 15},

  {1, 2, 1, 0},
  {1, 9, 10, 8},
  {1, 15, 14, 13}
};

Each entry follows this structure:

{PCA_number, coxa_channel, femur_channel, tibia_channel}

For example:

{0, 2, 1, 0}

means that this leg is connected to PCA9685 number 0, with the coxa servo on channel 2, the femur servo on channel 1, and the tibia servo on channel 0.

Leg Numbering

The robot uses the following leg numbering convention:

       0
   5       1

   4       2
       3

This numbering is used throughout the code to identify each leg when executing movements, gaits, calibration tests, and active-leg filtering.

## LED system

## 3D printed parts

## Assembly notes

## Problems encountered

## Fixes and lessons learned

## Tech stack

## Hardware list

- ESP32 Dev Module
- 2x PCA9685 16-channel servo drivers
- 18x servo motors
- WS2812B LED strips
- 60 LED WS2812B ring
- External 5V power supply
- 3D printed hexapod body parts

## Pin configuration

| Component | Pin / Address |
|---|---|
| I2C SDA | GPIO 25 |
| I2C SCL | GPIO 26 |
| PCA9685 #1 | 0x40 |
| PCA9685 #2 | 0x41 |
| Main LED strips | GPIO 27 |
| LED ring | GPIO 14 |

## Hardware
ESP32 Dev Module                                      x1
PCA9685 16-channel servo drivers                      x2
servo motors MG99GR TowerPro                          x18
8 LED WS2812CB ring                                   x1
16 LED WS2812B ring                                   x1
60 LED WS2812B ring                                   x1
External Battery
PCB personlised


I would do four files one called how2use were I will explain how to implement it and how does each commmand function, thr main README where I will expose the idea, the description the object and where I will share links to understand the gaits and see other types, another one with diverse information I have piled abou hexapods in my research project and one with especific information such as voltage current, how I printed the pieces, problems encountered, parts hardware, pin configuration, tech stack needed etc

This project is an ESP32-based hexapod robot controlled with two PCA9685 servo drivers and WS2812B LEDs. The robot supports standing, sitting, spinning, and experimental gait patterns.

## Pin configuration

| I2C SDA          | GPIO 25  |
| I2C SCL          | GPIO 26  |
| PCA9685 #0       | 0x40     |
| PCA9685 #1       | 0x41     |
| Main LED strips  | GPIO 27  |
| LED ring         | GPIO 14  |

## Problems encountered

### Servo orientation

Some servos are mounted in mirrored positions, so the same movement requires opposite angle directions depending on the side of the robot.

### Power stability

The servos and LEDs require an external 5V power supply. Powering them directly from the ESP32 is not suitable.

### Gait tuning

The walking gaits require manual tuning of coxa, femur, and tibia angles.
