# Hexapod

## Description
This project is an ESP32-based hexapod robot built to move across uneven and challenging terrain. The robot uses two PCA9685 servo drivers to control its leg servos and WS2812B LEDs for visual feedback. It is controlled via Bluetooth, allowing the user to operate the robot wirelessly and execute different movement commands. The system supports multiple movement behaviours, including standing up, sitting down, rotating, and walking using different gait patterns. The project focuses on developing a modular control architecture that makes it easier to test, tune, and expand different movement patterns, improving the robot’s ability to perform reliable and adaptable movements across difficult surfaces.

## My project

[Watch my hexapod robot movement](https://youtube.com/shorts/M2XZRYnYeiA?feature=share)

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

## Tecnologies Used

- C
- C++
- PlataformIO
- Arduino
- I2C
- PWM
- Fast LED
  
## Documentation

- [How to use the robot](How2use.md)
- [Research](HexapodResearch.md)
- [Project Information](ProjectInfo.md)

## Limitations

- The robot does not use inverse kinematics yet.
- There is no closed-loop feedback from the servos.
- Walking stability depends on servo calibration, surface conditions, and weight distribution.

  ## Future Improvements

- Add inverse kinematics.
- Add sensor feedback for better stability.
- Improve mechanical robustness and cable management.
