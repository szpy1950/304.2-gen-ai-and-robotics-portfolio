# Portfolio

## Analyse

I analysed the project scope, the UR3e arm's technical constraints, and the interface incompatibility between the real arm and the simulator.

??? abstract "Participate in initial project planning"
    In the kick-off session, the whole group used Jira and Scrum to decompose the Duckify project into granular tasks, assign sub-team roles, and agree on Week 1 milestones — turning an open-ended brief into a structured, workable plan.

    **Evidence:** [Initial planning](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260217_initial_planning.typ)

??? abstract "Gather arm constraints"
    Led cross-team discussions with the Tracing and 3D Printing teams and a dedicated session with the robotics teacher to collect joint limits, gripper reliability bounds, and TCP calibration requirements — producing the specification that drove the pipeline design.

    **Evidence:** [Robotic arm presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260220_robotic_arm.pdf)

??? abstract "Map the real-arm / simulator incompatibility"
    Identified that URBasic/RTDE (real arm) and ROS2/Gazebo in Docker (simulator) use incompatible protocols, command formats, and abstraction levels — a constraint that defined the scope of the Develop phase.

    **Evidence:** [Wrapper report](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md)

---

## Design

I designed the arm control pipeline and communicated the architectural decisions to the team.

??? abstract "Specify the arm pipeline"
    Before any code was written, I defined the FK/IK approach (DH convention, spherical wrist decoupling), TCP calibration strategy, and interface contracts between the wrapper and the rest of the system.

    **Evidence:** [Wrapper report](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md) · [Architecture diagram](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/architecture.drawio)

??? abstract "Present architecture at advancement meetings"
    Presented the arm architecture and open constraints to the CTO/PO, securing the team decision to prioritise motion control over camera registration.

    **Evidence:** [PR #9](https://github.com/Toys-R-Us-Rex/Duckify/pull/9) · [Advancement presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260227_duckify_meeting_week_2.pdf)

??? abstract "Act as team scribe"
    Structured team decisions and captured action items during daily meetings, ensuring shared understanding of next steps across the robotics group.

    **Evidence:** [Meeting notes](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/meetings/daily/2026-02-23.typ)

---

## Develop

I built ISCoinSim, a drop-in replacement for ISCoin that runs identical code on both the real UR3e and the Gazebo simulator.

??? abstract "Implement the ISCoinSim wrapper"
    Because URBasic/RTDE and ROS2/Gazebo are incompatible, I built a wrapper with full FK (DH convention), analytical IK (spherical wrist decoupling, up to 8 solutions), and a ROS2/Docker communication bridge. Switching between real and simulated arm is a single import line.

    **Evidence:** [Wrapper report](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md) · [Architecture](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/architecture.drawio) · [Code](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/main/my_simulation/iscoin_sim)

    <video controls width="100%" src="../assets/videos/simulation_python_wrapper.mp4"></video>

??? abstract "Validate joint-level control on the real arm"
    Confirmed joint-by-joint Python control and gripper operation on the physical UR3e, closing the loop between the wrapper implementation and the hardware.

    <video controls width="100%" src="../assets/videos/robot_control_python.mp4"></video>

??? abstract "Run lemniscate trajectory on the real arm"
    Executed a lemniscate drawing trajectory on the physical UR3e as an end-to-end test of the wrapper's motion pipeline.

    <video controls width="100%" src="../assets/videos/leminscate_drawing.mp4"></video>

---

## Evaluate

---

## Reflections

**Most unexpected challenge?**
The library/simulator incompatibility forced us to reprioritise and build the wrapper instead of moving straight to painting trajectories.

**Biggest practical constraint?**
Lab time with the real robotic arm is very limited — not enough to test calibration properly, and we had no procedure ready before the session.

**What would you do differently?**
Request library and simulator access from day one instead of mid-week. Also prepare a clear testing plan before each arm session.

**What went well?**
Communication in the robotics group was really good. Everyone helped each other, shared what they found, and jumped in when someone was stuck.

**Key takeaway on multi-team work?**
Agreeing on interfaces between teams early is just as important as the technical work itself.

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
