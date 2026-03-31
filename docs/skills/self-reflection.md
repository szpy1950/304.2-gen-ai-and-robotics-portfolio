# Critiquing the production process in a self-reflective manner

- *By taking a step back to describe one's thought processes and decisions*
- *By judging, in hindsight, the accuracy and appropriateness of the implementation*
- *By suggesting reasoned and motivated alternatives*

---

- **Active reflection in daily meetings** -- I participated actively in every daily meeting, reflecting on what I had accomplished, what had gone wrong, what improvements I could make, and how my work connected with other groups. These meetings were a regular opportunity to step back and reassess my approach. [Daily meeting notes](https://github.com/Toys-R-Us-Rex/Duckify/tree/main/docs/meetings/daily)

- **Iterative pipeline redesign** -- I adjusted my part of the pipeline multiple times throughout the project. I started with simple joint-range restrictions for collision avoidance, moved to Trimesh, then completely switched to PyBullet. Each change was motivated by concrete failures that showed the previous solution was not adequate. In hindsight, starting with PyBullet earlier would have saved time, but the progression also helped me understand the problem better before committing to a heavier tool.

- **Seeking expert guidance** -- I contacted Loic Azzalini (robotics expert) several times throughout the project to ask for advice on calibration precision, collision safety strategies, and tool choices. For example, he suggested looking into MoveIt2 for safety, which I evaluated before ultimately choosing PyBullet for its lighter integration. These exchanges helped me make more informed decisions and avoid going too far in wrong directions.

- **Lab process improvement** -- After the first lab sessions were unproductive due to lack of preparation, I created a structured lab procedure and report template so that every session had clear objectives and documented outcomes. This change improved the efficiency of later sessions. [Lab template](../assets/pdf/labo_template.pdf)