---
layout: single
title: "Robot Obstacle Avoidance via SDP and Rank Minimization"
permalink: /sdp_obstacle
---

## Problem Statement

The obstacle avoidance constraint can be formulated as mixed-integer constraints as discussed in [1] and [2]. Suppose the collision-free workspace is decomposed into \\( N \\) convex polytopes excluding the obstacles. Each polytope is parameterized as \\( \mathcal{P}_i = \{ x \mid A_i x \leq b_i \} \\). Suppose the collision body of a robot is modeled as a sphere centered at \\( p \\) with radius \\( r \\). The condition that the sphere is confined within the \\( i \\)th polytope can be written as \\( A_i p \leq b_i - a_i r \\), where \\( a_i(j) = A_i(j,:) \\). The obstacle avoidance constraint restricts the sphere to lie in **one** of the convex polytopes, which can be written as:

$$
\begin{aligned}
y_1 + \dots + y_N &= p \\
A_i y_i &\leq (b_i - A_i r) z_i, \quad i = 1, \dots, N \\
z_1 + \dots + z_N &= 1, \quad z_i \in \{0, 1\}
\end{aligned} \tag{1}
$$

where \\( y_i = p \\) if \\( z_i = 1 \\) and \\( y_i = 0 \\) if \\( z_i = 0 \\).

The above obstacle avoidance constraint can also be formulated using an SDP relaxation:

$$
\begin{aligned}
y_1 + \dots + y_N &= p \\
A_i y_i &\leq (b_i - A_i r) \left( \frac{\theta_i + 1}{2} \right), \quad i = 1, \dots, N \\
\theta_1 + \dots + \theta_N &= 2 - N, \quad \theta_i \in \{-1, 1\}
\end{aligned} \tag{2}
$$

We introduce the following variable:

$$
\Theta_i =
\begin{bmatrix}
\theta_i^2 & \theta_i \\
\theta_i & 1
\end{bmatrix}.
$$

Clearly, \\( \Theta_i \\) is a rank-1 matrix. When \\( \Theta_i(1,1) = \Theta_i(2,2) = 1 \\) and \\( \operatorname{rank}(\Theta_i) = 1 \\), we have \\( \theta_i = \pm 1 \\). Therefore, we can write (2) as linear constraints in \\( \Theta_i \\) along with the rank constraint \\( \operatorname{rank}(\Theta_i) = 1 \\), which can be solved using the rank minimization method discussed in [3].

---

## Implementation

This example solves the following problem:

$$
\begin{aligned}
\text{minimize}_{\{y_i\}, \Theta} \quad & -d^T p \\
\text{subject to} \quad & \theta_1 + \dots + \theta_N = 2 - N, \quad \theta_i \in \{-1, 1\} \\
\forall i = 1, \dots, N: \quad & A_i y_i \leq (b_i - A_i r) \left( \frac{\theta_i + 1}{2} \right) \\
& \Theta_i(1,1) = \Theta_i(2,2) = 1 \\
& \Theta_i \succeq 0 \\
& \operatorname{rank}(\Theta_i) = 1
\end{aligned} \tag{3}
$$

where \\( p = y_1 + \dots + y_N \\), \\( \Theta_i = [\theta_1, \theta_2, \dots, \theta_N] \\), and \\( d \\) is a desired direction in which we want the robot to move as far as possible from the origin.

This problem is convex except for the rank constraint, which is non-convex. The solution process involves two steps:
1. Solve the relaxed problem **without** the rank constraint to get an initial solution.
2. Apply a rank minimization algorithm from [3] to iteratively move the solution toward rank-1 matrices.

---

## Comparison with MIP

We compare our solution with that of (1) using the mixed-integer programming solver Gurobi.

**Case 1: Both methods find the same solution**

![MIP and SDP compare 1](/images/mip_sdp_compare1.png)

**Case 2: Solutions differ, but both are optimal**

![MIP and SDP compare 2](/images/work_obstacle.png)

Although the SDP approach may be slower than the MIP method, it involves solving only convex problems and can be tested within the framework in [3] to handle obstacle avoidance constraints, such as those found in robot kinematics problems.

---

## References

1. Blackmore L, Ono M, Bektassov A, and Williams BC. "A probabilistic particle-control approximation of chance-constrained stochastic predictive control." *IEEE Transactions on Robotics*, 26(3): 502–517, 2010.  
2. Hongkai Dai, Gregory Izatt, and Russ Tedrake. "Global inverse kinematics via mixed-integer convex optimization." *The International Journal of Robotics Research*, vol. 38, no. 12-13, pp. 1420–1441, 2019.  
3. Liangting Wu and Roberto Tron. "An SDP optimization formulation for the inverse kinematics problem." In *2023 62nd IEEE Conference on Decision and Control (CDC)*, pp. 4731–4738, 2023.
