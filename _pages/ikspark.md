---
layout: single
title: "IKSPARK: Solving Inverse Kinematics for Complex Robots"
permalink: /ikspark
---

> **Given a robot with complicated kinematic chains and an end-effector pose, can we efficiently and correctly compute the configurations of the robot?**  
> This work addresses challenges like this.

## Challenges in Inverse Kinematics

1. **Nonlinear Kinematic Mapping**  
   The relationship between joint angles and the end-effector's position and orientation is inherently nonlinear, complicating the computation of joint parameters for a specific end-effector pose.

2. **Multiple Solutions**  
   Depending on the robot's structure and the target pose, there may be zero, one, or multiple valid joint configurations, necessitating a method to identify all possible solutions.

3. **Physical Constraints**  
   Robots often have joint limits, self-collision constraints, and may include closed kinematic chains, all of which must be considered to ensure feasible and safe movements.

## Our Approach: IKSPARK

To address these challenges, we introduce **IKSPARK** (Inverse Kinematics using Semidefinite Programming And RanK minimization), a novel solver that reformulates the inverse kinematics problem by parameterizing it over the set of rotation matrices, SO(3).

This approach allows the kinematic constraints to be expressed as **convex constraints on rotation matrices**.  
To handle the nonlinearity of the SO(3) manifold, we employ a **semidefinite relaxation** followed by a **rank minimization algorithm**, ensuring both efficiency and correctness in computing robot configurations.

The solver is capable of solving Inverse Kinematics for robots with:
- revolute/prismatic/spherical joints;
- closed kinematic chains;
- the robot parameterization is general using rotation matrices, compatable to any robots.

![Robot arm schematic](/images/work_ik.jpg)

📄 [Read the full paper on arXiv](https://arxiv.org/pdf/2403.12235)

📂 Code: [IKSPARK](https://bitbucket.org/liangtingwu/ikspark)
