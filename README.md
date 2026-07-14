# Hexapod
This project is an ESP32-based hexapod robot controlled with two PCA9685 servo drivers and WS2812B LEDs. The robot supports standing, sitting, spinning, and experimental gait patterns.

## Project goal
The aim of this project is to design and build a stable six-legged robot capable of operating on uneven and challenging terrain. The robot will be controlled via Bluetooth and should be able to perform multiple movement patterns, including standing up, sitting down, rotating, and walking using different gait strategies. The main objective is to explore hexapod locomotion and develop a modular control system that allows the robot to execute reliable and adaptable movements.

## Main features

- ESP32-based control system
- 18-servo hexapod structure with 3 degrees of freedom per leg
- Two PCA9685 servo drivers for controlling all leg servos
- Smooth servo movement using time-based interpolation
- Stand-up and sit-down posture control
- Left and right rotation movements
- Experimental walking gaits: Wave gait, Ripple gait, Tripod gait
- Active-leg filtering system for testing individual legs or groups of legs
- WS2812B LED feedback system
- 60-LED ring support
- Servo calibration mode
- Modular code structure for adding new movements and gaits
- Bluetooth controller support

## High-level architecture

## Implemented movements

## Gait research

## Documentation

- [How to use the robot](docs/how-to-use.md)
- [Hexapod research notes](docs/hexapod-research-notes.md)
- [Hardware and build notes](docs/hardware-and-build-notes.md)

## Current status

## License

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
