# Portfolio Mockup — Skills Reference

Internal working document. Tracks agreed angle, evidence, and status for each skill page.

---

## 1. Analysing a complex IT problem
**Status:** Done

**Rubric criteria (italic at top of page):**
- By detailing its components with adequate granularity
- By identifying the constraints (technological challenges, client expectations, environmental requirements, etc.)
- By identifying opportunities (existing solutions, potential optimisations, etc.)
- By producing a complete set of requirements

**Agreed angle:** Global project view — contributed to breaking down the full Duckify pipeline (prompt → LLM → textures → robotic arm → duck) into components, identifying technical constraints across sub-teams, and defining project requirements in the initial planning session. This fed into the milestone plan.
Distinct from colleague angle (colleague focused on planning/collaboration; this page focuses on "understand the system before acting").

**Evidence:**
- [Initial planning](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260217_initial_planning.typ)
- [Milestones](assets/pdf/Milestones.pdf)

---

## 2. Designing a theoretical modelled solution
**Status:** Done

**Rubric criteria:**
- By conducting in-depth theoretical research
- By developing a theoretical, logical, valid and justified model that satisfies the constraints of a complex, multidisciplinary problem and its context

**Agreed angle:** Research-to-design decisions — covered IK (analytical vs numerical) and simulation tool selection (PyBullet chosen over Pykin, MoveIt2, Gazebo). robot_research.pdf covers the breadth of technical challenges (DH parameters, FK, IK, coordinate frame transformations for duck and robot frames, surface normals, simulation tools); IK_fk.pdf and Comparaison.pdf each contain a concrete design conclusion. No camera in the pipeline.

**Evidence:**
- [List of technical research](assets/pdf/robot_research.pdf)
- [FK/IK research](assets/pdf/IK_fk.pdf)
- [Collider simulator comparison](assets/pdf/Comparaison.pdf)
- [Robotic arm tech presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260220_robotic_arm.pdf)

---

## 3. Implementing a theoretical modelled solution
**Status:** Done (video link pending)

**Rubric criteria:**
- By applying modern best practices in programming and development
- By using appropriate tools
- By demonstrating satisfactory implementation of the software development process
- By delivering a framework, software and/or hardware
- By respecting development constraints

**Agreed angle:** Three-part delivery: PyBullet sim setup (solo), kinematics + motion planning (solo), coordinate frame transformation (joint with Cedric). Modules claimed: kinematics.py, computation.py, pybullet_helpers.py, pathfinding.py, safety.py (solo) + transformation.py (joint). NOT claiming executor.py (rewritten by colleague) or the full src/ package.
After `dev/clean-merge-pipeline` merges to main, update all links from `blob/dev/clean-merge-pipeline/src/` to `blob/main/src/` (or new pipeline repo URL).

**Evidence:**
- [kinematics.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/kinematics.py): FK/IK library
- [computation.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/computation.py): motion planning
- [pybullet_helpers.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/pybullet_helpers.py): simulation setup
- [transformation.py](https://github.com/Toys-R-Us-Rex/ur3e-control/blob/dev/clean-merge-pipeline/src/transformation.py): frame transform (with Cedric)
- [Demos / notebooks](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/dev/demos/my_simulation/demos): iterative validation
- PyBullet simulation video — add file to docs/assets/videos/ then add link to skill page

---

## 4. Evaluating an IT system
**Status:** Stub

**Rubric criteria:**
- By implementing targeted and appropriate performance tests
- By using the right tools
- By critically commenting on the results produced and measured
- By producing an objective and relevant report describing the characteristics and performance of the system

**Agreed angle:** TBD

**Evidence:** TBD

---

## 5. Communicating clearly and efficiently
**Status:** Stub

**Rubric criteria:**
- By sharing on a wide range of topics
- By choosing the appropriate communication medium
- By adapting the style of language to specific audiences

**Agreed angle:** TBD

**Evidence:** TBD

---

## 6. Adopting a professional attitude
**Status:** Stub

**Rubric criteria:**
- By taking into account one's working environment
- By proactively participating in technical achievements
- By collaborating actively and in a motivating manner

**Agreed angle:** TBD

**Evidence:** TBD

---

## 7. Justifying one's opinions and choices
**Status:** Stub

**Rubric criteria:**
- By relying on theoretical justifications, logical demonstrations and quantitative or qualitative assessments
- By debating the arguments of other parties fairly and respectfully

**Agreed angle:** TBD

**Evidence:** TBD

---

## 8. Critiquing the production process (self-reflection)
**Status:** Stub

**Rubric criteria:**
- By taking a step back to describe one's thought processes and decisions
- By judging, in hindsight, the accuracy and appropriateness of the implementation
- By suggesting reasoned and motivated alternatives

**Agreed angle:** TBD

**Evidence:** TBD
