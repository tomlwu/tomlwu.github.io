---
layout: single
title: "Visual Inverse Kinematics (VIK)"
permalink: /vik
---

**How can a robot find a valid configuration to see an object, without being told exactly where to place its camera?**

This is the challenge addressed in our work on **Visual Inverse Kinematics (VIK)** — a novel approach that merges geometric reasoning with visual perception constraints.

---

## 🔍 Motivation

In many real-world scenarios — such as robotic inspection, underwater manipulation, or drone photography — it is more practical to define **what needs to be seen** rather than the exact pose of the robot’s end-effector.

Traditional **inverse kinematics (IK)** solves for joint configurations given a specific target pose.

But what if:
- There is **no target pose**, just the **requirement** to **see an object**?
- You want the object to be visible **from a certain angle**, or **stay centered in the image**?
- The robot must stay within its physical constraints?

**This is the Visual IK problem.**

---

## 🎯 Problem Statement

The **Visual Inverse Kinematics (VIK)** problem is to find a **feasible robot configuration** such that:
- The robot **keeps a known object in its field of view**, and
- **Satisfies all joint and kinematic constraints**, without relying on actual image measurements.

---

## 🧠 Key Challenges

1. **Visibility ≠ Feasibility**: Not all camera poses that satisfy the field-of-view (FoV) constraint are reachable by the robot.
2. **Nonlinearity**: The mapping from joint configurations to camera FoV is **nonlinear and non-convex**.
3. **Coupled Constraints**: Vision-based and kinematic constraints must be solved **simultaneously**.

---

## ⚙️ Our Method

We solve the VIK problem using a two-stage optimization approach:

1. **Convex Relaxation**  
   We approximate the problem using **semidefinite programming (SDP)** with convex constraints.

2. **Rank Minimization**  
   We then project the solution back onto the **space of feasible robot configurations** using a custom **rank minimization algorithm**.

### 🧩 Key Insight: Virtual Kinematic Chains

To model visibility constraints, we introduce a **virtual kinematic chain**:
- Connects the object to the camera using **prismatic and spherical joints**
- Encodes field-of-view as a **conic constraint**
- Allows visibility to be treated like a joint constraint!

---

## 🎯 Vision-Based Objectives

We support several flexible visual goals:

- 📏 **Levelness**: Keep the camera aligned upright with the world.
- 🎯 **Centering**: Keep the object in the **center** of the image.
- 📸 **Reprojection Matching**: Recreate a previously seen image from a new configuration.

These can be **combined** to adapt to the task.

---

## 🧪 Experiments

We validate our method on a **7-DOF Sawyer arm** and **PUMA 560** robot with multiple simulated scenarios:

- Tasks: Keeping quadrotors in view, matching a reference image, centering visual targets.
- Results: Our method finds configurations that satisfy visibility constraints **without initialization**, even in cluttered or constrained environments.

![Sawyer example](/images/work_vik.png)
*Fig: Example configurations of the Sawyer robot targeting visual objectives.*
![Puma example](/images/vs_puma.jpg)
*Fig: VIK can serve as a good initialization for Visual Servoing as opposed to using random poses.*

---

## 🧠 Why VIK Matters

- VIK can **initialize visual servoing** more reliably than random sampling.
- It can be used to plan **vision-based inspection**, **camera-aware manipulation**, and more.
- Bridges the gap between **perception** and **control** in robotics.

---

## 📄 Publication

> Wu, Liangting & Tron, Roberto  
> *Visual Inverse Kinematics: Finding Feasible Robot Poses under Kinematic and Vision Constraints*  
> [PDF Link](https://arxiv.org/abs/2403.12235)

---

## 📬 Contact

**Authors:** Liangting Wu and Roberto Tron  
Department of Mechanical Engineering, Boston University  
[Email Liangting Wu](mailto:tomwu@bu.edu) | [Email Roberto Tron](mailto:tron@bu.edu)
