# Implementing a theoretical modelled solution

- *By applying modern best practices in programming and development*
- *By using appropriate tools*
- *By demonstrating satisfactory implementation of the software development process*
- *By delivering a framework, software and/or hardware*
- *By respecting development constraints*

---

- **Pathfinding pipeline** -- I implemented the full pipeline that converts surface traces into collision-free joint trajectories for the UR3e. It validates surface points with analytical IK and collision checking in PyBullet, groups them into drawable runs, finds safe hover approach points, assembles the motion sequence (TRAVEL/APPROACH/DRAW segments), and plans collision-free travel paths using the BiRRT planner. The following files demonstrate this implementation: [pathfinding.py](https://github.com/Toys-R-Us-Rex/Duckify/blob/feat/docstrings/robot/src/pathfinding.py), [safety.py](https://github.com/Toys-R-Us-Rex/Duckify/blob/feat/docstrings/robot/src/safety.py), [computation.py](https://github.com/Toys-R-Us-Rex/Duckify/blob/feat/docstrings/robot/src/computation.py)

- **Joint trajectory smoothing** -- I identified that without smoothing, the IK solver picks different equivalent configurations for consecutive points, causing the robot to flip unpredictably. I implemented a smoothing pass that uses the previous point's joints as reference so solutions chain continuously, with a fallback to the closest valid solution when the solver fails. This can be seen in [computation.py](https://github.com/Toys-R-Us-Rex/Duckify/blob/feat/docstrings/robot/src/computation.py).

- **Coordinate frame transformation (with Cedric)** -- Together with Cedric, I co-developed the module that maps duck-space coordinates into the robot's base frame, using calibration points and least-squares estimation. The code is available in [transformation.py](https://github.com/Toys-R-Us-Rex/Duckify/blob/feat/docstrings/robot/src/transformation.py).

- **Iterative validation notebooks** -- Throughout development, I built demo notebooks to test each part of the pipeline at its current state before integrating it further. This allowed me to catch errors early and validate each step independently. These notebooks are available in the [demos folder](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/dev/demos/my_simulation/demos).
