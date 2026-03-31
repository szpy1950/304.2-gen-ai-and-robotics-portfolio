# Designing a theoretical modelled solution

- *By conducting in-depth theoretical research*
- *By developing a theoretical, logical, valid and justified model that satisfies the constraints of a complex, multidisciplinary problem and its context*

---

- **Technical research** -- I conducted research across the main technical challenges of the robotic arm pipeline: UR3e kinematics (Denavit-Hartenberg parameters, forward kinematics, analytical vs numerical IK), coordinate frame transformations, and surface normals for tool orientation on 3D surfaces. My research is documented in [this report](../assets/pdf/robot_research.pdf).

- **FK/IK design decision** -- I studied both analytical IK (closed-form, up to 8 solutions using the UR3e's spherical wrist geometry) and numerical IK (Jacobian-based iteration). I concluded that analytical IK was the right choice because it gives exact solutions with no convergence risk. This analysis is documented in my [FK/IK research report](../assets/pdf/FK_IK.pdf).

- **Simulation tool selection** -- I compared Pykin, PyBullet, MoveIt2, and Gazebo against our requirements (collision detection, URDF support, Python API, ROS2 dependency). I selected PyBullet because it provides a direct Python API with collision detection and URDF loading without requiring the full ROS2 stack. The comparison is available in the [comparison report](../assets/pdf/Comparaison.pdf).

- **Pipeline design** -- I designed the end-to-end painting pipeline that takes JSON coordinates from the tracing team and drives the UR3e to paint them onto the duck. I specified each stage with clear input/output contracts so that the robot sub-team could work in parallel. The pipeline model is documented in [this report](../assets/pdf/pipeline_design_model.pdf).

- **Pathfinding pipeline design** -- I designed the pathfinding part of the pipeline, which takes cartesian positions already transformed by my colleagues and computes the real robot joint movements. This includes solving IK for each point, checking for self-collisions and obstacle collisions in PyBullet, and planning safe travel paths between drawing segments. The design is documented in [this report](../assets/pdf/pathfinding_pybullet.pdf).
