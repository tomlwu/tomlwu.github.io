---
layout: single
title: "Dual, Iterative H₂-Conic Controller Synthesis"
permalink: /h2_control
---

This project presents a new method for synthesizing **observer-based controllers** that are both **robust and optimal** by combining conic sector constraints with H₂ performance objectives.

---

##  Motivation

Modern control systems require both **robust stability** and **high performance**, especially in the presence of delays and uncertainties.

Traditionally, techniques like the Small Gain and Passivity Theorems have been used for robust stability, but they fall short when dealing with **open-loop unstable systems**. The **Conic Sector Theorem** generalizes these approaches and allows for more flexible controller design.

This work extends previous methods by introducing a **dual formulation** that improves:
- Feasibility for a wider class of plants
- Performance through reduced H₂-norm
- Convergence speed in iterative controller synthesis

---

##  Core Idea

The method aims to synthesize a **conic, observer-based controller** by:
1. **Minimizing an upper-bound** on the **closed-loop H₂-norm**
2. Ensuring input-output **robust stability** using the **Conic Sector Theorem**
3. Using a **dual formulation**: designing the observer matrix instead of the feedback gain
4. Applying **iterative convex optimization** with Linear Matrix Inequality (LMI) constraints

---

##  Simulation Results

###  Test Case: Heat Exchanger with Input Delay

- Compared against traditional H₂-optimal and conic controllers.
- The proposed method achieved:
  - **Smaller final H₂-norm**
  - **Faster convergence**
- Plots show improved Nyquist and Bode performance under delay.

![Controller performance](/images/CostIt_new.png)
![Controller delay performance](/images/H2Delays.png)

> The dual iterative method finds conic controllers with better performance and improved robustness to delay.

---

##  Why This Matters

- Adds a **new tool** to the robust control design toolbox.
- Provides a **feasible alternative** when traditional methods fail.
- Leverages **modern convex optimization** to solve hard controller synthesis problems.

---

## Publication

> **Liangting Wu** and **Leila Jasmine Bridgeman**  
> *Dual, Iterative H₂-Conic Controller Synthesis*  
> Presented at the 2020 American Control Conference (ACC)  
> IEEE Xplore Link: [https://ieeexplore.ieee.org/document/9147643](https://ieeexplore.ieee.org/document/9147643)

---