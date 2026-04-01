# Justifying one's opinions and choices during decision-making and strategic processes

- *By relying on theoretical justifications, logical demonstrations and quantitative or qualitative assessments*
- *By debating the arguments of other parties fairly and respectfully*

---

- **Simulation tool selection** -- produced a structured comparison of Pykin, PyBullet, MoveIt2, and Gazebo, evaluating each against our requirements (collision detection, URDF support, Python API, ROS2 dependency). Used this to argue for PyBullet as the team's simulation and collision tool. [Comparison report](../assets/pdf/Comparaison.pdf)
- **Analytical IK over numerical IK** -- justified retaining the analytical approach based on the UR3e's known spherical-wrist geometry, which allows exact closed-form solutions. Numerical IK adds convergence risk and computation overhead with no benefit for a robot with known geometry. [FK/IK research](../assets/pdf/IK_fk.pdf)
- **Filtering unreachable and dangerous points** -- decided to remove points on the bottom of the duck and bound surface normals above the horizon to avoid collisions. Also excluded the beak from drawable points after proving the arm could not reach it safely. [Technical choices report](../assets/pdf/technical_choices.pdf)
- **Duck rotation during drawing** -- proposed rotating the duck 180 degrees mid-session because reachability analysis showed that not all points are accessible from a single orientation. [Technical choices report](../assets/pdf/technical_choices.pdf)
- **Joint-by-joint waypoints over movel** -- a colleague wanted to use movel (linear TCP movement), but this caused collision problems on complex surfaces. I argued for a joint-by-joint waypoint approach instead, which avoids unpredictable TCP paths between points. [Technical choices report](../assets/pdf/technical_choices.pdf)
- **Accepting high point density (tradeoff)** -- a colleague proposed keeping a high number of waypoints, which is slower to compute but produces smoother and safer paths. I accepted this tradeoff after evaluating that computation time was acceptable compared to the gain in drawing quality. [Technical choices report](../assets/pdf/technical_choices.pdf)
- **Pattern selection based on difficulty** -- contributed to choosing the final drawing patterns based on what the robot could realistically achieve, avoiding overly complex shapes that would fail due to reachability or collision constraints. [Technical choices report](../assets/pdf/technical_choices.pdf)
