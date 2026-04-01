# Critiquing the production process in a self-reflective manner

- *By taking a step back to describe one's thought processes and decisions*
- *By judging, in hindsight, the accuracy and appropriateness of the implementation*
- *By suggesting reasoned and motivated alternatives*

---

- **Collision strategy evolution** -- I started with simple joint-range restrictions for 2D drawing, knowing they would not work for 3D. I then moved to Trimesh, and finally to PyBullet once physics-based collision checking proved necessary. In hindsight, starting with PyBullet earlier would have saved the Trimesh detour. This progression is documented in the [collision strategy retrospective](../assets/pdf/collision_retrospective.pdf).

- **Duck drawing failure analysis** -- I attempted to draw on the duck twice in W4 and both attempts failed. Instead of applying workarounds, I traced each failure to its root cause: calibration imprecision and a Y-axis sign inversion in the coordinate frame transform. Fixing the fundamentals enabled the first successful duck drawing in W5. The analysis is documented in the [lab report](../assets/pdf/w5_report_lab.pdf).

- **Rotation math lesson** -- Orientation errors in W3-W4 came from my misunderstanding of rotation vectors vs Euler angles. I had to stop and study the theory properly before the transformation code could work. If starting over, I would invest more time upfront in rotation representations. My notes on this are in the [rotation research notes](../assets/pdf/rotation_notes.pdf).

- **Pipeline architecture retrospective** -- After reaching a working pipeline in W5, I looked back at the overall architecture and identified what I would redesign: better separation between the simulation layer and the execution layer, and a clearer interface with the tracing team from the start. This is discussed in the [architecture retrospective](../assets/pdf/architecture_retrospective.pdf).

- **Lab process improvement** -- After the first lab sessions were unproductive due to lack of preparation, I created a structured lab procedure and report template so that every session had clear objectives and documented outcomes. This change improved the efficiency of later sessions. [Lab template](../assets/pdf/labo_template.pdf)
