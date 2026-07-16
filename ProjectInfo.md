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

-------0

5------------1

4------------2

-------3

This numbering is used throughout the code to identify each leg when executing movements, gaits, calibration tests, and active-leg filtering.


## LED system

In order to give special and personalised style I added LEDs which also will be very cool for recording videos at night and so on. In the LedEffects.cpp and LEDsRing.cpp files you could see all the set of LED functions programmed and used in the rest of the code. 
There you could see commands like:
switchOFFallintern:  that switches off every light on.
switchONallintern: that switches on every light with the color you wish to
switchOFFstrip: that switches off the strip you ordered
runInternLight: this is a command with which only one light is on by each time and the light runs all over the two LED strips
fillInternStrip: this is a command similar to the previous one but the time the lights runs to the next led the previous leds keep the lights on in order to fullfil the strip or ring
blinkingNOTblocking: this command is a command that makes the whole LED blink three times, not using delay() this way the hexapod is never stopping while it is being executed

### Active LEDs sequences

1. Every time you initialize the running program, a sequence is started in the from part. First a light runs quickly through the small circle and then it runs the second and once it is finished, it starts filling slowly both strips, this tries to simulate somthing similar to a LOADING pattern

2. The robor is assumed to start and end always at the same position, so the it is compulsory to run the standUp and sit down commands for the final and the end of each exploration, so each time you run this functions the front LED strips will be blinking trying to simulating that the robort is trying to get asleep or get up or somehow.

3. The last pattern is that the robot has a command, that if you press b from blinking, the lights situated at the bottom lights will blink three times.

4. The rest of the time all the LEDs should be switched on.

## Design challenges and solutions

### Current Spikes in the buck converter

#### Issue

The buck converter supplying power to the servos may not be capable of delivering the high transient currents required when multiple servos start or move simultaneously. These current spikes can cause voltage drops, unexpected resets, unstable servo behaviour, and, in extreme cases, mechanical instability of the robot.

#### Solution

Several measures can be adopted to mitigate this issue:

-Use a buck converter with sufficient current capacity to handle peak current demand rather than only the average load.

-Increase the converter's current limit when supported by the hardware.

-Isolate the logic power supply (ESP32) from the servo power supply while maintaining a common ground reference.

-Install large electrolytic capacitors (typically 1000–4700 µF) close to the servo power rail to absorb transient current peaks.

-Distribute the electrical load across multiple buck converters when powering a large number of servos.

-Use appropriately sized power cables and keep high-current connections as short as possible to minimise voltage losses.


In this project, the issue was successfully resolved by increasing the current limit of the buck converter to accommodate the expected peak current requirements.


### I2C Bus Instability

#### Issue

Electrical noise generated by the servos, together with high transient currents, can interfere with the SDA and SCL lines of the I²C bus. This may result in communication errors, intermittent freezes, or unreliable operation of the hexapod. Loose or poorly secured wiring can further increase electrical noise due to movement and vibrations during operation.

#### Solution

To improve communication reliability, the following measures are recommended:

-Keep the I²C cables as short as possible.

-Physically separate the I²C wiring from the high-current power lines supplying the servos.

-Use shielded cables when longer cable runs are unavoidable.

-Ensure that appropriate pull-up resistors (typically between 2.2 kΩ and 4.7 kΩ) are used, depending on the bus length and operating speed.

-Reduce the I²C clock frequency (e.g., from 400 kHz to 100 kHz) when communication becomes unreliable.

-Ensure that all devices share a low-impedance common ground.


For this project, the most effective solution was the design of a custom PCB that securely mounted the ESP32 and fixed the signal wiring in place. This significantly reduced cable movement, electrical noise, and intermittent communication failures, resulting in a much more reliable I²C connection.



## Fixes and lessons learned

## Hardware list

- ESP32 Dev Module
- 2x PCA9685 16-channel servo drivers
- 18x servo motors
- WS2812B LED strips
- 60 LED WS2812B ring
- External 5V power supply
- 3D printed hexapod body parts
