# Justifying one's opinions and choices during decision-making and strategic processes

- *By relying on theoretical justifications, logical demonstrations and quantitative or qualitative assessments*
- *By debating the arguments of other parties fairly and respectfully*

---

- **Simulation tool selection** -- produced a structured comparison of Pykin, PyBullet, MoveIt2, and Gazebo, evaluating each against our requirements (collision detection, URDF support, Python API, ROS2 dependency). Used this to argue for PyBullet as the team's simulation and collision tool. [Comparison report](../assets/pdf/Comparaison.pdf)
- **Analytical IK over numerical IK** -- justified retaining the analytical approach based on the UR3e's known spherical-wrist geometry, which allows exact closed-form solutions. Numerical IK adds convergence risk and computation overhead with no benefit for a robot with known geometry. [FK/IK research](../assets/pdf/IK_fk.pdf)
