# Hexapod
This project is an ESP32-based hexapod robot controlled with two PCA9685 servo drivers and WS2812B LEDs. The robot supports standing, sitting, spinning, and experimental gait patterns.

## Hardware
ESP32 Dev Module                                      x1
PCA9685 16-channel servo drivers                      x2
servo motors MG99GR TowerPro                          x18
8 LED WS2812CB ring                                   x1
16 LED WS2812B ring                                   x1
60 LED WS2812B ring                                   x1
External Battery
PCB personlised

## Pin configuration

| I2C SDA          | GPIO 25  |
| I2C SCL          | GPIO 26  |
| PCA9685 #0       | 0x40     |
| PCA9685 #1       | 0x41     |
| Main LED strips  | GPIO 27  |
| LED ring         | GPIO 14  |
