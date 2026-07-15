# Hexapod Research Notes

## What is a hexapod?
A hexapod is a six-legged robot designed to move using coordinated leg patterns called gaits. Because it has six legs, it can keep several points of contact with the ground at the same time, making it more stable on uneven or difficult terrain.

## Why six legs?

At the beginning of the project, I considered using a four-legged design instead of a hexapod. A quadruped would probably be faster, more agile, and more flexible in terms of movement. However, it would also require more precise balance control, stronger mechanical design, and more complex movement algorithms. For this project, stability and adaptability to uneven terrain are more important than speed. A six-legged robot can keep more contact points with the ground, making it more stable and reliable on difficult surfaces. For that reason, the hexapod structure is a better fit for the goal of this robot.

## Types of Hexapods
Another important design decision was the type of hexapod structure I wanted to build. Depending on the body shape and leg distribution, I had to choose between a rectangular, tank-like architecture and a hexagonal architecture. In general, a rectangular hexapod tends to perform better in straight-line walking, while a hexagonal hexapod usually has advantages in turning movements. Assuming the same leg design and overall robot size, the hexagonal configuration can provide better turning ability, a higher stability margin, and, in some conditions, a greater stride length.

For this reason, the body architecture has a direct impact on the robot’s movement capabilities, stability, and adaptability to different terrains.

### Rectangular / Tank-like Architecture

![Rectangular hexapod architecture](../media/photos/rectangular-hexapod.jpg)

### Hexagonal Architecture

![Hexagonal hexapod architecture](../media/photos/hexagonal-hexapod.jpg)

## Static vs dynamic gait

## Wave gait

## Ripple gait

## Tripod gait

## Other possible gaits

## Useful references

## Wave gait

The wave gait moves one leg at a time. This keeps five legs on the ground, making it one of the most stable gaits. However, it is slower than ripple or tripod gait.

## Ripple gait

The ripple gait moves legs in a sequential pattern, usually with more than three legs on the ground. It is a compromise between stability and speed.

## Tripod gait

The tripod gait moves two groups of three legs alternately. It is faster, but less stable than wave or ripple gait.
