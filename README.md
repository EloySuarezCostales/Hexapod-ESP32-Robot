# Hexapod

## Description
This project is an ESP32-based hexapod robot designed to explore stable six-legged locomotion on uneven and challenging terrain. The robot uses two PCA9685 servo drivers to control its leg servos and WS2812B LEDs for visual feedback.

The system supports multiple movement behaviours, including standing up, sitting down, rotating, and experimental walking gaits such as wave gait and ripple gait. The project focuses on developing a modular control architecture that makes it easier to test, tune, and expand different movement patterns.

The long-term goal is to control the robot via Bluetooth and improve its ability to perform reliable and adaptable movements across difficult surfaces.


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

- [How to use the robot](How2use.md)
- [Research](Research.md)
- [Project Information](ProjectInfo.md)
