# Designing a theoretical modelled solution

- *By conducting in-depth theoretical research*
- *By developing a theoretical, logical, valid and justified model that satisfies the constraints of a complex, multidisciplinary problem and its context*

To design the robotic arm's painting pipeline, I conducted research across the main technical challenges: UR3e kinematics (Denavit-Hartenberg parameters, forward kinematics, and two IK approaches), coordinate frame transformations for mapping duck and robot frames, surface normals for perpendicular tool orientation on 3D surfaces, and simulation tool options. This research informed two key design decisions: adopting the analytical IK already implemented in URBasic rather than the slower numerical approach, and selecting PyBullet as the simulation environment over Pykin, MoveIt2, and Gazebo, based on its URDF support, collision detection, and direct Python API without requiring ROS2.

**Evidence:**

- [List of technical research](../../assets/pdf/robot_research.pdf)
- [FK/IK research](../../assets/pdf/IK_fk.pdf)
- [Collider simulator comparison](../../assets/pdf/Comparaison.pdf)
- [Robotic arm tech presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260220_robotic_arm.pdf)
