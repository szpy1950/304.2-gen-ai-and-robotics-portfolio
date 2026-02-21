# Week 1 - Project Kickoff

**Dates:** February 16-20, 2026
**Role:** Developer - Robotic Arm group (simulation, library exploration)
**Group repo:** [Toys-R-Us-Rex/Duckify](https://github.com/Toys-R-Us-Rex/Duckify)

## Context

On Monday the **CEO** presented the project idea: a system that generates customisable rubber ducks on demand. A meeting with the **CTO** on Tuesday helped us discuss milestones and goals. By mid-week the team agreed on a pipeline with 3D printing, texture tracing, and robotic-arm painting. Daily meetings kept everyone aligned, and we closed the week with a presentation on Friday 20.02.2026.

## Skills demonstrated

### Communication & coordination

Early in the week I discussed interface questions with the Tracing and 3D Printing groups to make sure we agree on data formats and responsibilities. I took part in the [initial planning](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260217_initial_planning.typ) and helped define the [team milestones](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/planning/steps_milestones.typ). With the robotics teacher I prepared and led a 1-hour session covering joint limits, gripper reliability, and camera calibration. Based on what we learned about TCP calibration effort and camera complexity, I suggested we focus on motion control first and leave camera registration for later. On Friday I delivered the [advancement presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260220_duckify_meeting_week_1.pdf) to the CTO and PO. Progress is also tracked in the daily meeting notes ([18.02](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/meetings/daily/2026-02-18.typ), [19.02](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/meetings/daily/2026-02-19.typ), [20.02](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/meetings/daily/2026-02-20.typ)).

### Robotics engineering

The first step was understanding how the UR3e works (6-DOF joint-space model). It turned out the UR3e control library (high-level commands) and the Docker-based simulator (raw joint angles) use incompatible interfaces — the interface analysis, forward/inverse kinematics research, and calibration findings are documented in the [robotic arm presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260220_robotic_arm.pdf). After mapping out both interfaces (URBasic on one side, simulator waypoints on the other), I proposed a wrapper as the bridge and detailed the approach in an [interface study and solution design](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md). I also researched TCP calibration precision, wrist-camera options, and how to hold the duck in place, which helped the sub-team decide what to prioritise. During our Thursday session with the real arm I tested joint-level control from Python, confirming we could move each joint to target angles reliably:

<video controls width="100%" src="../../assets/videos/robot_control_python.mp4"></video>

### Software engineering

Because the UR3e control library and the simulator use incompatible interfaces (see Robotics above), we needed a translation layer. Following the [wrapper specification](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/architecture/robot/wrapper_report.md), I built a [Python wrapper](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/main/my_simulation/iscoin_sim) that takes real-arm API calls and converts them into the simulator's JSON keyframe format. I set up the Docker simulation environment (ISCoin) and worked from my own fork to avoid breaking the shared code. To validate things, I built [demo notebooks](https://github.com/Toys-R-Us-Rex/ur3e-control/tree/main/my_simulation/demos) that test commands on both the real arm and the simulator. At the end of the week we evaluated our progress against the [milestones](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/planning/steps_milestones.typ) defined at the start, reporting which goals were met and which remained open in the [weekly presentation](https://github.com/Toys-R-Us-Rex/Duckify/blob/main/docs/presentations/20260220_duckify_meeting_week_1.pdf):

<video controls width="100%" src="../../assets/videos/simulation_python_wrapper.mp4"></video>

## Reflections

**Most unexpected challenge?**
The library/simulator incompatibility (discovered Wednesday) forced us to reprioritise and build the wrapper instead of moving straight to painting trajectories.

**Biggest practical constraint?**
We only have one hour on Thursday afternoon with the real robotic arm. That's way too short. We couldn't test everything we wanted, especially calibration. We didn't have a clear calibration procedure ready before the session, and then there wasn't enough time to figure it out and test it properly.

**What would you do differently?**
Ask for library and simulator access from day one. We only got it on Wednesday and lost two days. Also, have a clear plan ready before the arm session so we don't waste time deciding what to do on the spot.

**What went well?**
Communication in the robotics group was really good. Everyone helped each other, shared what they found, and jumped in when someone was stuck. That made a big difference with such a tight schedule.

**Key takeaway on multi-team work?**
Agreeing on interfaces between teams early on is just as important as the technical work. The hardest questions this week were about data formats and responsibilities, not code.

## Interview questions

1. How did you handle the mismatch between the UR3e control library and the simulator?
2. Why did you focus on motion control first instead of camera calibration?
3. How did you coordinate work inside the robotics group when multiple people were working on related tasks?
