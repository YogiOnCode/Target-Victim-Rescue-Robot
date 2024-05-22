# Target Victim Rescue Robot

![C++](https://img.shields.io/badge/C%2B%2B-00599C?logo=cplusplus&logoColor=white)
![ROS 2](https://img.shields.io/badge/ROS%202-Nav2-22314E?logo=ros&logoColor=white)
![Eigen](https://img.shields.io/badge/Eigen-linear%20algebra-informational)

A team project from a robotics course. A single mobile robot (the **Shelfino** platform) has to rescue
as many high-value victims as possible inside a time limit, while avoiding obstacles in the arena.

---

## Problem

- Victims are circles with a radius of 0.5 m, and each one has a **value**. The goal is to maximize the total value rescued.
- To rescue a victim, the robot must **pass through its centre**. It does not need to stop.
- The robot moves at **constant speed**, so it cannot stop or slow down.
- The robot and the victims start at random positions, and the rescue order is free.

Because the robot cannot turn on the spot, paths must respect a minimum turning radius. This makes
**Dubins curves** a natural fit.

## My contribution: motion planning with Dubins curves

I implemented the Dubins path module (`dubins.cpp`):

- All six Dubins words (**LSL, RSR, LSR, RSL, RLR, LRL**), solved in a normalized (scaled) frame
- `dubins_shortest_path`: picks the shortest feasible curve between two poses
- **Collision checking** of curve arcs against segments and polygons (obstacles and map borders)
- Sampling curves into waypoints (uniform or proportional to arc length) and exporting them as JSON

`shelfino_nav.launch.py` brings up the **ROS 2 Nav2** stack (map server, AMCL, planner, controller,
behaviour tree navigator, velocity smoother) used to run the robot in simulation.

> **Status:** This is an ongoing collaborative coursework project. The repository contains my modules,
> not the full system.

## Repository contents

```
├── dubins.cpp               # Dubins curves, shortest path, collision checks
└── shelfino_nav.launch.py   # ROS 2 Nav2 launch configuration for Shelfino
```

## Tech stack

C++ · Eigen · ROS 2 · Nav2 · Python (launch files)

## License

No license is provided. This is a collaborative team project, so please contact me before reusing the code.

## Author

**Yogeswaran Amsavalli** · [GitHub](https://github.com/YogiOnCode)
