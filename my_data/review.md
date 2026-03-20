# 304 Major Option Track — Portfolio Evaluation

## Course Structure

The course has two tracks:
- **304.1** — Robot control and generative AI (Duckify project)
- **304.2** — Medical informatics and data science

---

## Introduction — Overarching Goal

Experience a realistic development scenario and demonstrate engineering competences by:
- Deploying competencies within a problem-centered project
- Producing an individual competencies portfolio weekly
- Defending the final portfolio in an oral discussion

The key framework: **Competency = "knowing how to act"** → demonstrated through decisions & outcomes under real constraints → supported & assessed via portfolio artifacts + oral defense.

---

## Specific Objectives — 11 Competencies

### A. Computer Science Engineer (4 competencies)

- **Analyser un problème informatique complexe** — Break down components at proper granularity, identify constraints (tech challenges, client expectations, environment), identify opportunities (existing solutions, optimizations), produce complete specifications (cahier des charges)
- **Concevoir une solution théorique modélisée** — Conduct deep theoretical research, model a logical/valid/justified approach satisfying complex multidisciplinary constraints
- **Implémenter une approche théorique modélisée** — Apply modern programming best practices, use proper tools (git, languages), demonstrate the software dev process (prototyping, debugging, unit-testing, deployment), deliver framework/software/hardware, respect time constraints
- **Évaluer un système informatique** — Set up targeted performance tests, use appropriate tools, critically comment on measured results, produce an objective report on system characteristics and performance

### B. Data Engineer (3 competencies)

- **Valoriser des ensembles de données hétérogènes et multimodales** — Statistically analyze data properties, propose appropriate data collection, clean/prepare heterogeneous data (images, text, signals), comment on data quality and value
- **Orchestrer un processus et une infrastructure de traitement de données** — Develop a complete processing pipeline (collect, clean, train, deploy), select justified methods (statistical analysis, computational modeling, ML, etc.), produce discriminative/predictive/generative solutions
- **Appliquer les compétences de l'ingénierie informatique au domaine des données** — For robotics: integrate sensor data in a perception → decision → action loop with robust software architecture. For medical informatics: build software chain transforming multimodal patient data into exploitable indicators with hospital system integration and security/traceability

### C. Professionalism / Soft Skills (4 competencies)

- **Communiquer clairement et efficacement** — Share on a wide range of topics (technical solutions, code, constraints), choose appropriate communication format (presentation, report, documentation), adapt language style to specific audiences (client, colleagues, public, experts)
- **Adopter une posture professionnelle facilitante** — Consider your work environment, participate proactively in technical work, collaborate actively and motivationally
- **Argumenter ses opinions et ses choix lors de processus décisionnels et stratégiques** — Base arguments on theoretical justifications, logical demonstrations, and quantitative/qualitative evaluations; debate fairly and respectfully
- **Critiquer le déroulement d'une production de manière auto-réflexive** — Step back to describe your reasoning and decision paths, judge a posteriori the correctness and adequacy of the work, suggest reasoned and motivated alternatives

---

## The Portfolio

**Definition:** A personal, evidence-based dossier documenting what you contributed and how those contributions demonstrate the target competences. It is a "portfolio-as-report": concise, structured, justified with concrete artifacts.

### Must contain:

- **Evidence (artifacts):** links to PRs & commits, architecture diagrams, API examples, test results, dashboards, device logs, model metrics, incident notes, meeting notes, etc.
- **Justification:** short explanations connecting each artifact to a competence ("what I did", "why", "trade-offs", "result")
- **Reflection:** what worked, what failed, what you learned, what you would change

### How it works:

- Weekly incremental work (Friday afternoon)
- **Reports:** role performed + key actions + 1-2 major outcomes + 1 blocker/resolution (including any LLM use, transparently) + evidence links
- **Synthesis** (end of course): overall contribution, growth across roles, strongest evidence per competence
- **3 hiring process Q&A per week:** questions useful to determine if a candidate is a good fit, reflecting that week's portfolio content. These may be used in final evaluation across portfolios.

### Evaluation:

- Individual portfolio defense: you present selected evidence, a cross-track panel probes understanding and impact
- 4 rating categories: very good / good / insufficient / failed

---

## Full-Time Simulation

Everyone plays a role: students are staff at a pretend company contracted by a client to deliver a product within 7 weeks. Professors and external collaborators play leadership/client roles.

Real engineering problem: technically challenging, with unclear requirements, trade-offs, integration issues, data quality concerns, deployment constraints, team dynamics. Both technical skills and soft skills required.

**Remote work policy:**
- Two 4h blocks of home office per week
- Team decides when (set at project start)
- Cannot be Monday morning, Friday afternoon, or a single full day
- Can be modified for robotics lab necessity (approved by professor)

---

## Schedule (W1–W7)

| Date | Event |
|------|-------|
| 16.02.2026 | Preparation day + CS/ML Seminar |
| 17.02.2026 | Course simulation kick-off (full day) |
| W1–W2 | Project work |
| 04.03 | Day off (Forum HES-SO) |
| 05.03 | CS/ML Seminar |
| 10.03 | Visit to Hôpital du Valais (TBC) / Voyage d'études |
| 12.03 | Corporate Social event |
| 13.03 | Portfolio assessment |
| 18.03 | Portfolio assessment |
| 19.03 | Day off (official holiday) |
| 20.03 | Mandatory remote day |
| 27.03 | Portfolio assessment |
| 01.04 | Evaluation w/304.1 track (full day) |
| 02.04 | Evaluation (afternoon) |
| 03.04 | Day off (official holiday) |

---

## Portfolio Evaluation Scorecard

### A. Computer Science Engineer

| # | Competency | Present? | Score | Comments |
|---|-----------|----------|-------|----------|
| C1 | Analyser un problème informatique | Yes | 7/10 | 4 solid artifacts (IK comparison, tool evaluation, project planning, incompatibility mapping). Good constraint/opportunity identification. Missing: no formal cahier des charges (specifications document), and granularity analysis could be deeper. Two evidence links are missing elsewhere but this section is fine. |
| C2 | Concevoir une solution théorique modélisée | Yes | 5/10 | 2 artifacts (JSON-to-paint pipeline, architecture diagram). The pipeline design description is good BUT the evidence link is (empty). Architecture diagram link exists. Missing: no explicit mention of theoretical research conducted, no justification of why this approach satisfies constraints vs alternatives. |
| C3 | Implémenter une approche théorique modélisée | Yes | 7/10 | 3 artifacts (math library, ISCoinSim wrapper, progressive drawing). Good transparency about Claude AI usage. Videos are a nice touch. Missing: one evidence link is (drawing notebooks/scripts). No mention of unit testing, no mention of respecting time constraints. |
| C4 | Évaluer un système informatique | Yes | 7/10 | 4 artifacts (joint validation, coordinate notebook, iterative testing, lemniscate). Strong failure analysis progression. Missing: no formal performance metrics/quantitative results (e.g., accuracy in mm, success rates), no structured "evaluation report" as such. |

### B. Data Engineer

| # | Competency | Present? | Score | Comments |
|---|-----------|----------|-------|----------|
| C5 | Valoriser des ensembles de données hétérogènes et multimodales | No | 1/10 | Completely absent. You work with sensor data, calibration points, mesh coordinates, camera frames. You should document data analysis, quality assessment, cleaning steps. |
| C6 | Orchestrer un processus et une infrastructure de traitement de données | No | 1/10 | Completely absent. Your pipeline (JSON > transforms > IK > execution) IS a data processing pipeline. You should frame it as such: collection, cleaning, processing, deployment. |
| C7 | Appliquer les compétences de l'ingénierie informatique au domaine des données | Partial | 3/10 | Your work IS the perception > decision > action loop described in the PDF, but you never frame it that way. The sensor integration, coordinate transforms, and robust architecture are there in substance but not presented as this competency. |

### C. Professionalism / Soft Skills

| # | Competency | Present? | Score | Comments |
|---|-----------|----------|-------|----------|
| C8 | Communiquer clairement et efficacement | Yes | 5/10 | 2 artifacts (advancement meeting, scribe). Thin. Missing: no evidence of adapting language to different audiences, no documentation/report artifacts beyond meeting notes. |
| C9 | Adopter une posture professionnelle facilitante | No | 1/10 | Completely absent as a section. Your journal hints at collaboration but the portfolio page has zero dedicated evidence for proactive participation, environment awareness, or motivating collaboration. |
| C10 | Argumenter ses opinions et ses choix | No | 1/10 | Completely absent. You made decisions (analytical IK over numerical, PyBullet over MoveIt2) but never frame them as argued choices with theoretical justification and debate with others. |
| C11 | Critiquer le déroulement d'une production de manière auto-réflexive | Yes | 6/10 | The Q&A-style reflection exists and the failure progression is genuinely good. Missing: no structured "stepping back" to describe decision paths, no a posteriori judgment of whether the overall approach was adequate, no suggested alternatives with motivation. |

### D. Portfolio Structure & Required Elements

| Element | Present? | Score | Comments |
|---------|----------|-------|----------|
| Evidence (artifacts) | Partial | 6/10 | Good links overall but 2 placeholders are unacceptable. Some evidence is links to code without explanation. |
| Justification per artifact | Partial | 5/10 | Most artifacts have "what I did" but often lack "why this choice", "trade-offs considered", and "result achieved". |
| Reflection | Partial | 5/10 | Exists at the end but is shallow. Needs deeper "what I learned" and "what I would change" per competency, not just globally. |
| Weekly reports (role + actions + outcomes + blocker + LLM use) | No | 2/10 | Journal page has Week 1 only. No weekly reports with the required structure (role, key actions, 1-2 outcomes, 1 blocker/resolution, LLM use transparency, evidence links). You're in W5. |
| Hiring Q&A (3 per week) | Partial | 4/10 | Only W1 and W2 (6 questions). Missing W3, W4, W5. Questions exist but answers are missing entirely. The PDF says "three questions AND answers". |
| Synthesis | No | 1/10 | Not expected yet (end of course), but keep it in mind. |

---

## Summary

| Category | Average Score |
|----------|--------------|
| CS Engineer (C1–C4) | 6.5/10 |
| Data Engineer (C5–C7) | 1.7/10 |
| Soft Skills (C8–C11) | 3.3/10 |
| Structure/Format | 3.8/10 |
| **Overall** | **~4/10** |

---

## Top Priority Fixes

1. **Fill the evidence links** (C2 pipeline, C3 drawing scripts) — easy win
2. **Add sections for C5, C6, C7** — reframe your existing work (calibration data, coordinate pipeline, sensor-to-action loop) as data engineering competencies
3. **Add sections for C9 and C10** — document collaboration examples and argued decisions
4. **Write weekly reports for W2–W5** in journal with the required structure (role + actions + outcomes + blocker + LLM use)
5. **Add W3–W5 hiring Q&A with answers** — you're missing 9 Q&A and all answers
6. **Deepen justifications** — for each artifact, add "why this choice", "what alternatives", "trade-offs"
7. **Strengthen C11** — add structured retrospective per phase, not just a global Q&A

The technical content is solid. The main gap is that you have 3 entirely missing competencies (C5, C6, C9, C10) and the weekly reporting structure is incomplete.