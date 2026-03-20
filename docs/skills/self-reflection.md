# Critiquing the production process in a self-reflective manner

- *By taking a step back to describe one's thought processes and decisions*
- *By judging, in hindsight, the accuracy and appropriateness of the implementation*
- *By suggesting reasoned and motivated alternatives*

---

- **Collision strategy evolution** -- started with simple joint-range restrictions, knowingly insufficient for 3D. Moved to Trimesh, then PyBullet once physics-based collision checking proved necessary. In hindsight, starting with PyBullet earlier would have saved the Trimesh detour.
- **Duck drawing failure analysis** -- two failed attempts traced to root causes (calibration imprecision, Y-axis sign inversion) rather than patched with workarounds. Fixing the fundamentals enabled the first successful duck drawing.
- **Rotation math lesson** -- orientation errors in W3-W4 came from misunderstanding rotation vectors vs Euler angles. If starting over, I would invest more time upfront in rotation representations before writing transformation code.

**Evidence:**

- [Week 5 lab report](../assets/pdf/w5_report_lab.pdf)
