# Hardware and Build Notes

## Hardware list

## Power system

## Voltage and current considerations

## Servo drivers

## Pin configuration

## PCA9685 channel mapping

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
