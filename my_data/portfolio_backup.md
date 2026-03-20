# Portfolio

## Computer Science Engineering Skills

### Analyse a complex IT problem

I analysed the interface gap between the provided tools, compared IK approaches, and evaluated simulation options to define the project's technical needs.

??? abstract "Compare IK approaches for the UR3e"
    Studied two IK families: **analytical** (closed-form via spherical wrist decoupling, giving up to 8 exact solutions) and **numerical** (Jacobian-based iteration, more general but slower and not guaranteed to converge). Analysed URBasic's existing analytical IK to understand how it uses the UR3e's spherical wrist geometry, then compared with numerical alternatives from research papers. Conclusion: analytical IK is the right fit because the UR3e's known geometry allows exact closed-form solutions. Numerical would add cost and convergence risk for no gain.

    **Evidence:** [IK/FK report](assets/pdf/IK_fk.pdf)

??? abstract "Evaluate simulation and collision-checking tools"
    Compared three tools against our needs: **Pykin** (lightweight FK/IK library), **PyBullet** (physics simulation with URDF loading and collision detection), and **MoveIt2** (full ROS2 motion planning stack). PyBullet was chosen for collision testing and IK debugging. It provides a direct Python API, loads URDF models natively, and handles collision queries without requiring the full ROS2 stack. MoveIt2 was rejected as too heavy for our scope. Gazebo was kept for full environment simulation.

    **Evidence:** [Comparison report](assets/pdf/Comparaison.pdf)

??? abstract "Participate in initial project planning"
    In the kick-off session, the whole group used Jira and Scrum to break the Duckify project into small tasks, assign sub-team roles, and agree on Week 1 milestones. This turned a vague brief into a structured, workable plan.

    **Evidence:** [Initial planning](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260217_initial_planning.typ)

??? abstract "Map the real-arm / simulator incompatibility"
    The teacher provided two tools: URBasic (real arm control via RTDE) and a Gazebo Docker container (ROS2 simulation). After exploring both, I found that they use incompatible protocols and abstractions. URBasic sends high-level `movej`/`movel` commands over RTDE, while Gazebo expects ROS2 joint-state messages via topics. They share no common interface. This analysis showed the need for a translation layer (the wrapper) as the first task.

    **Evidence:** [Wrapper report](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md)

---

### Design a modelled theoretical solution

I designed the end-to-end painting pipeline and the overall project architecture before implementation began.

??? abstract "Design the JSON-to-paint pipeline for a real arm on a 3D model"
    Designed a full pipeline that takes JSON coordinates (produced by the tracing team) as input and drives the UR3e to physically paint them onto a 3D-printed model. The pipeline chains several stages: parse the JSON waypoints, transform them from the model's coordinate frame to the robot's base frame, compute joint angles via analytical IK, generate smooth motion trajectories between waypoints, orient the tool perpendicular to the surface at each point using mesh normals, and execute the resulting joint commands on the real arm. Each stage was specified with clear input/output contracts so that subteams could work in parallel.

    **Evidence:** <!-- TODO -->

??? abstract "Specify the project architecture"
    Before any code was written, defined the overall system architecture: FK/IK approach, TCP calibration strategy, and interface contracts between subteams, making sure everyone agreed on data formats and responsibilities.

    **Evidence:** [Architecture diagram](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/architecture.drawio)

---

### Implement a modelled theoretical approach

With the assistance of Claude Code, I built the math library (`src/`), developed the ISCoinSim wrapper, and step by step implemented drawing from flat surfaces to inclined faces to curved geometry.

??? abstract "Build the math library (`src/`)"
    Built a Python library containing: FK (DH convention), IK (adapted from URBasic's analytical approach), waypoint generation for painting paths, frame transformations between coordinate systems, calibration point reading from the real arm, collision checking via PyBullet, and Gazebo visualization helpers. This is the main original codebase that links the theoretical models to the physical/simulated arm.

    **Evidence:** [Source code](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/dev/clean-merge-pipeline/src)

??? abstract "Implement the ISCoinSim wrapper (with Claude AI assistance)"
    Because URBasic/RTDE and ROS2/Gazebo are incompatible, built a wrapper that copies the URBasic interface and translates calls to ROS2/Docker commands. **Built with help from Claude AI**: the AI helped set up the ROS2 communication layer and Docker integration, while I defined the interface needs, tested against the real arm, and debugged protocol mismatches. Switching between real and simulated arm is a single import change.

    **Evidence:** [Wrapper report](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md) · [Architecture](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/architecture.drawio) · [Code](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/main/my_simulation/iscoin_sim)

    <video controls width="100%" src="../assets/videos/simulation_python_wrapper.mp4"></video>

??? abstract "Progressive drawing implementation (lab weeks 2-3)"
    Went from flat-surface drawing to inclined-surface drawing to curved-surface attempts, each step needing new integration work:

    - **Flat surface**: circle and lemniscate on paper. Validated the basic motion pipeline (trajectory generation > IK > joint commands > pen contact).
    - **Inclined surface**: trapezoid faces. Required adding surface-normal-based tool orientation so the pen stays perpendicular to non-horizontal planes.
    - **Curved surface (duck)**: attempted full mesh-based drawing. Exposed calibration precision needs and axis inversion bugs.

    Each step combined gripper control, TCP calibration, and more complex orientation math.

    **Evidence:** <!-- TODO: link to drawing notebooks/scripts -->

---

### Evaluate an IT system

I validated the pipeline through step-by-step lab testing, with clear failure analysis at each stage.

??? abstract "Validate joint-level control on the real arm"
    Checked that each of the UR3e's 6 joints responds correctly to Python commands on the physical arm. Confirmed gripper open/close reliability. This basic check was needed before all later motion work.

    <video controls width="100%" src="../assets/videos/robot_control_python.mp4"></video>

    **Evidence:** [Lab report](assets/pdf/robot_labo report.pdf)

??? abstract "Verify coordinate transforms with a dedicated notebook"
    Wrote a Jupyter notebook to systematically verify that coordinate transformations between frames (model, camera, robot base) produce correct results. This allowed catching errors in the transform chain before running on the real arm, where debugging is slower and mistakes risk damaging hardware.

    **Evidence:** [Coordinate transform verification notebook](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/notebooks/coordinate_transform_verification.ipynb)

??? abstract "Iterative surface-drawing testing with failure analysis"
    Step-by-step progression with specific failure diagnosis at each step:

    - Circle + lemniscate on flat surface. First non-planar attempt failed: pen lost contact on inclined face because tool orientation was wrong (TCP pointing straight down instead of normal to surface).
    - Trapezoid top face failed due to TCP offset not calibrated for pen length. After TCP recalibration, top face succeeded. Then inclined faces succeeded: drew letters T, N, S on angled trapezoid sides using surface-normal orientation.
    - Duck mesh attempt failed. Found two issues: (1) calibration error from imprecise reference point collection, (2) axis inversion in the camera-to-robot frame transform (sign error on Y-axis).

    Each failure led to a specific diagnosis and fix: TCP offset correction, per-face normal recomputation, frame transform sign checking.

    **Evidence:** [Lab report](assets/pdf/robot_labo report.pdf)

??? abstract "Lemniscate end-to-end validation"
    Full pipeline test: trajectory generation (parametric lemniscate curve) > analytical IK (8 solutions filtered) > joint command execution on real arm > pen draws the figure. Validated the complete chain from math to physical output.

    <video controls width="100%" src="../assets/videos/leminscate_drawing.mp4"></video>

---

## Soft Skills

### Communicate clearly and effectively

??? abstract "Present architecture at advancement meetings"
    Presented the arm architecture and open constraints to the CTO/PO, which led to the team decision to focus on motion control before camera registration.

    **Evidence:** [PR #9](https://github.com/Toys-R-Us-Rex/Duckify/pull/9) · [Advancement presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260227_duckify_meeting_week_2.pdf)

??? abstract "Act as team scribe"
    Wrote down team decisions and action items during daily meetings, making sure everyone understood next steps across the robotics group.

    **Evidence:** [Meeting notes](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/meetings/daily/2026-02-23.typ)

---

### Critically self-reflect on the course of a production

**Most unexpected challenge?**
The library/simulator incompatibility forced us to change plans and build the wrapper instead of moving straight to painting trajectories.

**Biggest practical constraint?**
Lab time with the real robotic arm is very limited, not enough to test calibration properly, and we had no procedure ready before the session.

**What would you do differently?**
Request library and simulator access from day one instead of mid-week. Also prepare a clear testing plan before each arm session.

**What went well?**
Communication in the robotics group was really good. Everyone helped each other, shared what they found, and jumped in when someone was stuck.

**Key takeaway on multi-team work?**
Agreeing on interfaces between teams early is just as important as the technical work itself.

**Lab failure progression as learning evidence:**
Week 2 non-planar fail > Week 3 three sessions to crack the trapezoid (top face ✗ > top face ✓ > inclined faces ✓) > Week 4 duck fail exposed axis inversion. Each failure taught something specific: TCP calibration precision matters (millimetre offsets cause pen drift), surface normals must be recomputed per-face (not interpolated from neighbours), and frame transforms need careful sign checking (a single sign error on Y flipped the entire drawing).

---

## Interview questions

*Week 1*

1. How do you handle a situation where two parts of a project don't work together?
2. How do you decide which problem to solve first when you have several at the same time?
3. How do you make sure everyone in a team stays on the same page when working on related tasks?

*Week 2*

4. How do you explain a technical decision to people who are not involved in the implementation?
5. How do you make sure a piece of code works correctly before connecting it to the rest of the project?
6. What do you do when a task turns out to be much bigger than you expected?