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

## Documentation

- [How to use the robot](docs/How2use.md)
- [Research](docs/Research.md)
- [Project Information](docs/ProjectInfo.md)
