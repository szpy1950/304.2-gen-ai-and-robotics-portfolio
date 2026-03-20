# Detailed Work Journal — Pierre-Yves Savioz
## Duckify Project — Robotic Arm Subteam
### HES-SO Valais-Wallis — GenAI & Robotics Major Track 2026

*Sources: daily meeting notes, weekly presentations, lab report, research PDFs*

---

## Week 1 — February 16–20, 2026

**Role:** Developer — Robotic Arm group

### Monday Feb 16
Preparation day + CS/ML Seminar. Project concept introduced by the CEO: a pipeline to generate customisable rubber ducks on demand, with AI-generated textures and robotic arm painting.

### Tuesday Feb 17
Full-day kick-off. The whole group used Jira and Scrum to decompose the Duckify project into tasks, assign sub-team roles, and agree on Week 1 milestones. The team agreed on a pipeline with 3D printing, texture tracing, and robotic arm painting.

### Monday–Tuesday: Lab introduction
First hands-on session with the UR3e arm, in the presence of Richard Murielle and Loïc Azzalini. Familiarisation with the physical control console and the lab environment.

### Wednesday Feb 18 — Daily meeting
- Proposed rotating the scribe role, defined the order.
- Raised the point that the goal should be depth of understanding, not just delivery ("expert en connaissance, pas que tout soit fini").
- Asked for access to the simulation environment — needed to explore libraries before setting milestones.
- Asked about where to centralise links and repos for the team.

### Thursday Feb 19 — Daily meeting + Lab
**Lab:** First Python steps. Used URBasic to send movement commands to the UR3e from Python scripts. Confirmed that `movej` (joint space) and `movel` (Cartesian space) work. Confirmed gripper response.

**Key discovery:** URBasic (which talks to the real arm via RTDE) and the Gazebo Docker simulation (which expects ROS2 joint-state messages) are completely incompatible at the protocol level. They share no common interface.

**Action taken:** Built a first version of the ISCoinSim wrapper to bridge the two. The wrapper copies the URBasic API surface and translates calls into ROS2/Docker commands, so the simulation and the real arm can be controlled via the same Python interface with a single import change.

- Got the simulation software running on laptop.
- Confirmed: the Python libraries that work with the real robot are not compatible with the Gazebo simulation environment.

### Friday Feb 20 — Daily meeting
- Confirmed: libraries OK, MoveJ A→B movements working.
- Only 1 hour of real-arm access available this week → couldn't test everything.
- Plan: continue simulator tests over the weekend; no more real-arm access before Monday.
- Proposed centralised documentation and a personal repo/fork for development.
- Flagged that the test process is inherently slow because simulation validation is a required step before touching the real arm.

**Weekly presentation (Feb 20) — Feedback received:**
- Robot group: add a visual about the simulation environment and robot range.
- Presentation: always add bullet points, always show DONE/TODO status on milestones, always display sources.
- Organisation: define interfaces between teams early, define which `movej`/`movel` command type will suffice.

**Research done this week:**
- Studied FK/IK theory: Forward Kinematics (DH parameters, 6 homogeneous matrix chain, deterministic), Analytical IK (closed-form via spherical wrist decoupling, up to 8 solutions), Numerical IK (Jacobian-based iteration).
- **Decision: analytical IK retained** because the UR3e's known geometry allows exact closed-form solutions. URBasic already implements it. Numerical IK adds convergence risk and computation overhead with no benefit on a robot with known geometry.
- Started exploring simulation options: Pykin, PyBullet, Gazebo.

---

## Week 2 — February 23–27, 2026

**Role:** Developer — Robotic Arm group

### Monday Feb 23 — Daily meeting
- Working on presentation preparation for Friday.
- Modifying wrapper code and cleaning up the wrapper report.
- Sent email to Loïc Azzalini to request robot access for Tuesday.
- Objective for the week: draw a 2D shape on paper.

### Tuesday Feb 24 — Lab session + Daily meeting (PY as scribe)
**Lab:** Gripper integration in Python. First real drawings: a circle and the lemniscate (infinity symbol) traced on a flat sheet of paper. TCP calibration performed and configured.

**Collision strategy for 2D drawing:** Defined simple joint-range restrictions as a proxy for collision avoidance on flat surfaces. Noted explicitly that this approach is not transposable to 3D — a proper solution would be needed later.

- Scribed the meeting.
- Confirmed official access to the robot for testing that afternoon.

### Wednesday Feb 25 — Daily meeting
**2D drawing: SUCCESS.**
- Circle and lemniscate successfully drawn on flat paper.
- Immediately set the next objective: non-uniform surfaces, then 3D drawing.
- Started thinking about the full integration pipeline — what it would take to connect the tracing team's JSON output to the robot arm.

### Thursday Feb 26 — Daily meeting + Integration meeting
**Integration meeting** with Kevin (GenAI) and Louis (project manager):
- Defined the model to use for the first integration test.
- Discussed the robot's scope for integration: drawing on inclined plane surfaces, multi-line patterns.
- Discussion with the tracing team about the robot's input domain (what format, what coordinate frame).
- Decided to use **Trimesh** for collision checking (initial approach before later switching to PyBullet).
- Plan: test on real robot to finish the integration pipeline (simple test).

Also presented the architecture and the pipeline design to the team.

**Friday Feb 27 — Weekly presentation — Feedback received:**
- Robot milestone for the week: **FAILED** (planned: draw on 3D surface).
- What was shown: lemniscate drawing success video (2D), inverse kinematics presentation.
- Issue flagged: communication/vocabulary — "validation" as a milestone term needs more precision (visual validation vs. calculation validation).
- Communication issue with tracing team regarding data integration.
- **CTO/PO directive:** drawing on the duck is now critical — must happen soon or the project falls behind schedule.
- Week 3 robot objectives: draw on non-planar surface, draw with 2 pens, safely move robot arm.

---

## Week 3 — March 2–6, 2026

**Role:** Developer — Robotic Arm group

### Monday Mar 2 — Daily meeting
- Code reformatting and consolidation with the rest of the robot group.
- Planning deadlines for the upcoming tests.

### Tuesday Mar 3 — Lab session + CEO meeting (daily note)
**Lab (2h session):** Implemented the new pipeline including collision checking and reformatted pathfinding. Tested on robot.

**CEO presentation:**
- Presented robot advantages vs. human painting (speed, repeatability, precision with numbers).
- CEO committed to: Option Plus (550 CHF/month), the approved duck model, and the robotic arm as core delivery.
- CEO inputs: correct PV, send duck video by Friday 06.03.

### Wednesday Mar 4 — Day off (Forum HES-SO)

### Thursday Mar 5 — Daily meeting
- No robot access possible today (CS/ML Seminar day).
- Discussion with Loïc Azzalini: he advised using existing Docker solutions (MoveIt2-based) for safety and collision checking rather than building from scratch.
- **Decision to explore MoveIt2 integration** within the Docker container.
- M. Lettry suggested: for each small implementation step or improvement, add tests and visualisation (graphs) — this makes it possible to quantify progress and catch regressions.

### Friday Mar 6 — Weekly presentation — Feedback received:
**Robot milestones status:**
- Coordinate conversion: OK ✓
- Drawing on flat surface (no angle): OK ✓, but drawing with angle → FAIL (surface normal conversion error)
- Tool manipulation: OK in simulation, not tested on real arm
- Drawing on duck: NOT DONE
- Drawing with 2 pens: NOT DONE

**Root cause of angle failure:** Rotation vectors (not Euler angles) caused a mathematical comprehension issue — took time to understand why the tool orientation was wrong on inclined surfaces.

**Week 4 robot plan:**
- Tool manipulation on real arm
- 3D surface drawing
- Multiple pens
- Find and implement a safety/collision solution

**3 options for collision safety:**
1. From scratch (custom)
2. External Python library
3. MoveIt2 via Docker — feature-complete but heavy and complex

**Milestone target defined by CTO:**
> "Using the complete pipeline, draw AI-generated shape contours with a selected GenAI solution, on a duck, installed on a stable support, using multiple colors, while changing colors automatically."

---

## Week 4 — March 9–13, 2026

**Role:** Developer — Robotic Arm group

### Monday Mar 9 — Daily meeting (PY as scribe)
- **Decision confirmed: PyBullet chosen** as the collision and simulation tool (over Pykin and MoveIt2).
  - Pykin: no collision detection, useless for safety checking.
  - MoveIt2: too heavy, requires full ROS2 infrastructure, slow to iterate.
  - PyBullet: direct Python API, loads URDF/STL natively (UR3e + duck + trapeze), built-in collision detection, `calculateInverseKinematics()` in the API, `addUserDebugLine` for trajectory visualisation. Resources pointed by expert M. Azzalini confirmed the approach.
- Restructuring of the codebase needed but scoped as "not immense".
- Discussed calibration precision improvements with M. Lettry, particularly pen pressure and precision below the millimetre level.

### Tuesday Mar 10 — Daily meeting
- Setting up PyBullet collision simulation.
- Integrating the duck mesh (STL) and the tracing team's waypoint traces into the PyBullet simulation scene.
- Goal: visually validate the toolpath on the 3D model before sending commands to the real arm.

### Wednesday Mar 11 — Lab session + Daily meeting
**Lab (Wednesday):** Attempt to draw on the duck — FAIL. Two issues identified:
1. Calibration error: imprecise reference point collection shifted the entire coordinate frame.
2. Axis inversion: sign error on the Y-axis in the camera-to-robot frame transform caused mirrored positioning.

**Daily meeting:**
- Completed integration of: collisions, self-collision detection, `get_reachable` function.
- **Blockers:**
  - Normal computation problem at the duck's eyes area (abrupt normal changes).
  - Infinity symbol attempt: not all points reachable, missing point in the trajectory.
  - Normals varying too abruptly between adjacent faces.
- Today's plan: fix the blocking elements, then draw on the duck.

### Thursday Mar 12 — Daily meeting
- Finished PyBullet collision code and simulation setup.
- Set up the Python simulation file.
- Fixed a code organisation error.
- Today: combine the full pipeline for robot on simulation, fix remaining error.
- Note: prepare Ethernet adapter and materials for lab tests.

### Friday Mar 13 — Lab session + Daily meeting + Weekly presentation
**Lab:** Attempt to draw on the duck — still blocked due to matrix problems. The transformation matrix between the camera frame and the robot frame was incorrect, causing the computed positions to not match the real duck position. Also, a left/right orientation confusion in the duck rotation was shifting the drawing to the wrong side.

**Retrospective:**
- Redid the architecture to allow running code in the lab without crashing the programme (stability issue from previous sessions).
- **Blocker discovered:** collision with the table — an invisible virtual plane was generating false collision events and blocking trajectory execution.

**Weekly presentation feedback:**
- Robot: integrate code into the main Duckify repo, clean the codebase.
- Week 5 objectives: optimise calibration precision, constant drawing pressure, control drawing angle.
- Test pen change on the trapezoid.
- Portfolio template coming.

---

## Week 5 — March 16–20, 2026

**Role:** Developer — Robotic Arm group + Integration contributor

### Monday Mar 16 — Daily meeting
- Refactoring of the PyBullet simulation module (collision, stand/support objects).
- Identified bug: arm "teleportation" — incoherent joint positions between consecutive waypoints, the arm jumps instead of moving smoothly.
- Working on pathfinding improvements.
- **Constraint:** code integration across the robot group is a blocking issue — different branches not yet merged.

### Tuesday Mar 17 — Daily meeting (PY as scribe, K absent)
**Yesterday (Mar 16):**
- Restructured the PyBullet functions.
- The PyBullet file was poorly organised → refactored into multiple separate files for clarity.
- Investigated merge situation.
- **Solved the "hover points" problem** — previously, the arm would pause incorrectly at lift-off points between strokes, causing timing issues.

**Today (Mar 17):**
- Change the pipeline order (movement steps): resequencing the trajectory execution to produce smoother motion.

### Tuesday Mar 17 — Lab session (Week 5) ← MAJOR MILESTONE
**Objective:** Draw a circle on the duck using the full pipeline.

**Pipeline used:**
1. Measure 4 calibration points on the duck to determine its position and orientation in space.
2. Generate waypoints in PyBullet (the circle path on the duck surface).
3. Validate the trajectory in Gazebo (collision checking with the real environment model).
4. Execute on the real UR3e arm.

**Result: A circle was successfully drawn on the duck. ✅ FIRST SUCCESSFUL DUCK DRAWING.**
The complete pipeline worked end-to-end: calibration → PyBullet → Gazebo → real arm.

**Problems encountered and resolved:**
- *Incorrect transformation matrix*: the computed position did not correspond to the real duck position. Fixed by checking and correcting the reference frames.
- *Duck orientation confusion*: left/right confusion in the duck rotation caused the drawing to be placed on the wrong side. Corrected.
- *Auto-collisions*: during trajectory generation between waypoints, the arm was colliding with itself. Resolved by adjusting intermediate joint configurations.

**Next steps from this session:**
- Draw more complex shapes (lines, curves, closed forms).
- These will pose new collision problems between waypoints.
- Main objective: improve trajectory planning to handle collision avoidance automatically.

### Wednesday Mar 18 — Daily meeting
**Retrospective:**
- Working on joint plotting: trying to fix the problem of robot joints changing drastically between two nearby waypoints (discontinuous joint-space path even for close Cartesian positions). This is not ideal or physically realistic — the IK solver finds a solution in a different joint configuration even for nearby Cartesian positions, causing jumps.
- Louis collaborated with Cédric and PY on the robot interface needs, developed a graphical prototype of the UI.
- Louis assigned to help PY resolve the unstable arm position problem + integration of the robot part into the global pipeline.

### Thursday Mar 19 — Official holiday

### Friday Mar 20 — Mandatory remote day
- (Today — ongoing work)

---

## Technical Research Summary (across all weeks)

### URBasic + RTDE control
- `movej` (joint space) and `movel` (Cartesian space) commands.
- 6D pose management (position + orientation as rotation vector).
- Automated movement sequences from Python scripts.

### Forward & Inverse Kinematics
- DH parameters of the UR3e used to model the kinematic chain.
- FK: 6 homogeneous matrix multiplications → deterministic, one result per joint configuration.
- Analytical IK: closed-form, up to 8 solutions per pose, relies on spherical wrist geometry of UR3e.
- Numerical IK: Jacobian-based, general but slow and not convergence-guaranteed → rejected.
- FK used to cross-check IK results against URBasic's returned poses.

### Coordinate frames and affine transforms
- 4×4 homogeneous transformation matrices for position + orientation in 3D.
- Rotation matrices and affine transforms to change between coordinate frames.
- Frames involved: camera frame, duck/model frame, robot base frame.
- Least-squares estimation to compute the transform between frames from corresponding calibration points.

### Surface normals for 3D drawing
- Per-face normals computed from the mesh to orient the tool perpendicular to the surface.
- Handling of normal discontinuities at face boundaries (rotation vector transitions).
- Problem found: at curved regions (duck eyes, beak), normals vary too abruptly → causes tool orientation jumps.

### Simulation tools comparison
| Tool | Decision | Reason |
|------|----------|--------|
| Pykin | Rejected | FK/IK only, no collision detection |
| PyBullet | **Retained** | Direct Python API, URDF/STL loading, collision detection, trajectory visualisation |
| MoveIt2 | Rejected | Too heavy, full ROS2 required |
| Gazebo | Retained (secondary) | Full environment simulation, but slower to iterate |

### PyBullet specifics
- Loads UR3e URDF and any STL (duck, trapeze, table) into the scene.
- `calculateInverseKinematics()` for IK debug.
- `addUserDebugLine()` for visual trajectory traces.
- Self-collision and object-collision detection.
- `get_reachable` function to check which waypoints are accessible before execution.
- Timestep is manual — must be configured explicitly.
- Resources from M. Azzalini: `pyb_utils`, Adam Heins collision detection blog.

### Gazebo + ROS2 wrapper (ISCoinSim)
- Docker container with Gazebo for Arch Linux (XWayland for display under Hyprland).
- Wrapper built with Claude AI (Anthropic) for the ROS2 communication layer and Docker integration.
- Wrapper replicates the URBasic Python API → switching real/simulated arm = single import change.

---

## Lab Sessions Summary

| Week | Date | Session | Result |
|------|------|---------|--------|
| W1 | Mon Feb 16 | Introduction with Richard + Loïc | Environment familiarisation |
| W1 | Thu Feb 20 | First Python movements | movej working via URBasic |
| W2 | Tue Feb 25 | Gripper + circle + lemniscate + TCP calibration | SUCCESS: 2D drawing |
| W2 | Fri Feb 28 | TCP correction + pen grip + non-planar attempt | FAIL: non-planar |
| W3 | Tue Mar 3 | Trapezoid top face attempt | FAIL |
| W3 | Wed Mar 4 (approx) | Trapezoid top face retry | SUCCESS top face; FAIL inclined faces |
| W3 | Fri Mar 6 | Inclined faces (trapezoid) | SUCCESS: drew letters T, N, S |
| W4 | Wed Mar 12 | Duck drawing attempt | FAIL: calibration error + Y-axis inversion |
| W4 | Fri Mar 13 | Duck drawing attempt 2 | FAIL: matrix problems + duck orientation |
| W5 | Tue Mar 17 | Circle on duck — full pipeline | SUCCESS: first duck drawing |

*All sessions ~1h, participants: Pierre-Yves Savioz, Cédric Mariethoz, Nathan Antonietti*

---

## Key Decisions Made (with rationale)

1. **Analytical IK over Numerical IK** — The UR3e's spherical wrist geometry allows a closed-form solution (up to 8 exact solutions). Numerical IK adds convergence risk and computation cost with no benefit for a robot with known geometry. URBasic already implements analytical IK.

2. **PyBullet over Pykin/MoveIt2** — Pykin has no collision detection (useless for safety validation). MoveIt2 requires a full ROS2 infrastructure (too heavy for our scope). PyBullet gives a direct Python API with URDF/STL loading and collision detection, and can be used without ROS2.

3. **ISCoinSim wrapper design** — Rather than rewriting all code for both environments, a thin translation wrapper preserving the URBasic API allows a single-import switch between real and simulated arm. This unblocked parallel development.

4. **Trimesh → PyBullet transition** — Initially used Trimesh for collision geometry. Switched to PyBullet once it became clear we needed physics-based collision checking and visual trajectory debugging, not just geometry queries.

5. **Simple joint-range restrictions for 2D collision (W2)** — A pragmatic short-term choice for flat-surface drawing, consciously noted as not generalisable to 3D. Replaced in later weeks.

---

## Blockers and Resolutions

| Blocker | When | Resolution |
|---------|------|-----------|
| URBasic/Gazebo protocol incompatibility | W1 | Built ISCoinSim wrapper |
| Non-planar surface drawing fails | W2 | Added surface-normal-based tool orientation |
| TCP offset not calibrated for pen length | W3 | TCP recalibration → top face success |
| Rotation vector math (not Euler) | W3 | Studied and re-implemented correctly |
| Duck drawing fails — calibration imprecision | W4 | Under investigation |
| Duck drawing fails — Y-axis sign inversion | W4 | Sign error on camera→robot frame transform |
| Invisible table collision blocker | W4 | Identified; fix in W5 |
| Hover points causing arm pauses | W5 | Solved Mar 17 |
| Joint discontinuity between nearby waypoints | W5 | Under investigation (Louis collaborating) |
| Code integration across robot group | W5 | Ongoing — blocking full pipeline test |