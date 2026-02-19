# Week 1 — Project Kickoff

**Date:** _Fill in_
**Status:** In progress

---

## What happened this week

> Replace this section with what actually happened during week 1.

We had our first team meeting to define the project scope and split responsibilities. The overall goal of **Duckify** is to build an end-to-end pipeline from a text prompt to a physically painted 3D-printed duck, using generative AI at every step and a robotic arm for the final painting stage.

### Team structure

We split into three sub-teams:

- **Application team** — handles the LLM prompting interface and 3D model generation
- **Captors team** — handles camera vision, workpiece detection, and quality feedback
- **Robotics team** (me) — handles the 6-DOF robotic arm, kinematics, and painting toolpath

### My work this week

- Attended kickoff meeting and understood the full pipeline
- Researched available robot SDK / ROS integration options
- Started reading the robot arm documentation and joint limits
- Wrote initial notes on the coordinate frames we'll need (base frame → TCP frame → duck surface)

---

## Skills demonstrated

!!! note "Robotics"
    Understanding of robot coordinate frames, TCP definition, and forward kinematics basics.

!!! note "Team collaboration"
    Participated in pipeline architecture design across all sub-teams.

---

## Next week

- Set up the robot SDK development environment
- Write a basic joint-space motion test
- Define the duck workpiece registration strategy
