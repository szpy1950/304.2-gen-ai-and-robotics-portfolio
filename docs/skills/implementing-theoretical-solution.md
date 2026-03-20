# Implementing a theoretical modelled solution

- *By applying modern best practices in programming and development*
- *By using appropriate tools*
- *By demonstrating satisfactory implementation of the software development process*
- *By delivering a framework, software and/or hardware*
- *By respecting development constraints*

---

Implementing my part of the robotic arm control pipeline involved several modules within a collaborative Python package. I wrote a full kinematics library (`kinematics.py`) covering DH matrices, forward kinematics, analytical IK, and solution selection, and a motion planning module (`computation.py`) that converts duck-surface trace coordinates into TCP pose sequences with hover logic, path assembly, and joint-space smoothing. I also set up the PyBullet simulation environment (`pybullet_helpers.py`), loading the UR3e URDF and configuring joints, to test planned paths before any hardware run. Together with Cedric, I implemented the coordinate frame transformation (`transformation.py`) that maps duck-space coordinates into the robot's base frame. Work was carried out across multiple Git branches, with a dedicated safety module (`safety.py`) enforcing runtime constraints. The implementation is ongoing: self-collision handling and the path planner are under active development and refactoring.

**Evidence:**

- [kinematics.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/kinematics.py): FK/IK library
- [computation.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/computation.py): motion planning
- [pybullet_helpers.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/pybullet_helpers.py): simulation setup
- [transformation.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/transformation.py): frame transform (with Cedric)
- [Demos / notebooks](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/dev/demos/my_simulation/demos): iterative validation
