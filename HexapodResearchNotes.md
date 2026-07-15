# Hexapod Research Notes

## What is a hexapod?
A hexapod is a six-legged robot designed to move using coordinated leg patterns called gaits. Because it has six legs, it can keep several points of contact with the ground at the same time, making it more stable on uneven or difficult terrain.

## Why six legs?

At the beginning of the project, I considered using a four-legged design instead of a hexapod. A quadruped would probably be faster, more agile, and more flexible in terms of movement. However, it would also require more precise balance control, stronger mechanical design, and more complex movement algorithms. For this project, stability and adaptability to uneven terrain are more important than speed. A six-legged robot can keep more contact points with the ground, making it more stable and reliable on difficult surfaces. For that reason, the hexapod structure is a better fit for the goal of this robot.

## Types of Hexapods
Another important design decision was the type of hexapod structure I wanted to build. Depending on the body shape and leg distribution, I had to choose between a rectangular, tank-like architecture and a hexagonal architecture. In general, a rectangular hexapod tends to perform better in straight-line walking, while a hexagonal hexapod usually has advantages in turning movements. Assuming the same leg design and overall robot size, the hexagonal configuration can provide better turning ability, a higher stability margin, and, in some conditions, a greater stride length.

For this reason, the body architecture has a direct impact on the robot’s movement capabilities, stability, and adaptability to different terrains.

### Rectangular / Tank-like Architecture

![Rectangular hexapod architecture](hexapodtank.jpg)

### Hexagonal Architecture

![Hexagonal hexapod architecture](hexagonal_hexapod.jpg)

## Legs

The final design decision was whether the legs should have a straight structure or a curved, C-shaped structure. After comparing both options and analysing their advantages and limitations, I decided that the curved design was the most suitable for this project.The main advantage of a straight leg is that the contact point with the ground is clearly defined. This makes the final position of the leg easier to calculate and predict, which simplifies stability analysis and movement control.However, a curved leg offers greater versatility. Its shape is more similar to a biological leg, and it allows the robot to support itself using different parts of the leg depending on the terrain. This makes it more suitable for irregular surfaces, as the contact with the ground is more progressive and less abrupt.

The main drawback of this design is that the support point is harder to predict. As a result, calculating the exact position, stability margin, and effective leg length becomes more complex. Even so, the curved structure is still the better option for this robot, as it improves adaptability to uneven terrain and allows the robot to tolerate small positioning errors and changes in elevation.

So, this is the final shape the legs will have:
![LEG hexapod architecture](CLEG.jpg)
The legs will have each one three servo motors, each one for the coxa, femur and shinbone.

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
