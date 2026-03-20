# Evaluating an IT system

- *By implementing targeted and appropriate performance tests*
- *By using the right tools*
- *By critically commenting on the results produced and measured*
- *By producing an objective and relevant report describing the characteristics and performance of the system*

---

- **Incremental drawing tests on 3D surfaces** -- from flat paper to trapezoid faces to the duck, comparing PyBullet-generated toolpaths against physical results on the real UR3e.
- **Integration tests** -- `pybullet_collision_test.py` runs the full pipeline (JSON import to final waypoint list) to verify all modules work together.
- **Unit tests** -- TCP calibration accuracy and coordinate-frame transformation correctness validated individually.
- **Joint-angle trajectory plots** -- visualised planned paths to detect discontinuities (unsafe jumps between waypoints).
- **Simulation-to-reality validation** -- ran validated paths on the physical arm to confirm transfer accuracy.

<details>
<summary>Lemniscate drawing video</summary>
<video controls width="100%" src="../assets/videos/lemniscate_drawing.mp4"></video>
</details>

<details>
<summary>First successful drawing on the duck</summary>

![First successful drawing on the duck](../assets/photos/IMG20260318164349.jpg)
</details>

<details>
<summary>Joint-angle trajectory plot showing discontinuities</summary>

![Joint-angle trajectory plot showing discontinuities](../assets/photos/bad_plot.png)
</details>

**Evidence:**

- [Evaluation report](../assets/pdf/evaluation_report.pdf)
- [Demos / notebooks](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/dev/demos/my_simulation/demos): iterative validation
- [pybullet_collision_test.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/pybullet_collision_test.py): integration test (full pipeline)