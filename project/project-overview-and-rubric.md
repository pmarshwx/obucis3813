# CIS 3813A – Advanced Data Science: Final Project Guide & Rubric

**Spring 2026 · Dr. Patrick Marsh · Oklahoma Baptist University**

---

## Overview

The Final Project is your capstone opportunity to demonstrate mastery of the machine learning concepts and workflows covered throughout the semester. You will independently select a real-world dataset, apply appropriate ML techniques, interpret your findings, and communicate your results both in writing and through a live presentation.

The Final Project is worth **40% of your final grade** and is divided into three independently scored components:

| Component | Weight | C-Level | B-Level | A-Level |
|---|---|---|---|---|
| **Project Check-in (Proposal)** | 5% | Submit proposal on time | Thoughtful topic + rationale | Exceptional depth & planning |
| **Final Project Report (Notebook)** | 25% | Code runs correctly | + Process explanation & Q&A | + Originality & sophistication |
| **Final Project Presentation** | 10% | Basic delivery | Clear, organized, on-time | Professional; strong Q&A |
| **TOTAL** | **40%** | | | |

Each component is assessed separately. Performing well on one component does not guarantee a high grade on another — each must stand on its own merits.

> **Key Dates**
>
> **Project Check-in (Proposal):** Due Monday, March 30, 2026 by 11:59 PM CT (night of class — no grace period)
>
> **Final Project Report:** Due Monday, May 4, 2026 by 6:00 PM CT (before final class)
>
> **Final Project Presentation:** Monday, May 4, 2026 during class (live, 10 minutes)

---

## Part 1: Project Check-in / Proposal (5%)

### What to Submit

A **one-page written proposal** describing your intended Final Project. This is a planning document, not code — its purpose is to ensure you have a clear, feasible direction before you invest significant time in development.

### Required Content

- **Dataset description:** What dataset will you use? Where is it from? How many rows/features does it have?
- **Problem statement:** What question are you trying to answer? Is this a regression or classification problem?
- **Proposed approach:** Which algorithm(s) do you plan to use and why?
- **Anticipated challenges:** What difficulties do you expect to encounter?
- **Success criteria:** How will you evaluate whether your model is successful?

### Submission Details

| | |
|---|---|
| **Format** | One page (PDF, Word, or Markdown) — submitted via Canvas |
| **Due Date** | Monday, March 23, 2026 by 11:59 PM CT |
| **Grace Period** | None — this is a planning document, not code |
| **Late Policy** | The "Unsolvable Bug" pass cannot be used for this component |

### Proposal Rubric

| Criterion | F/D (< 70%) | C (70–79%) | B (80–89%) | A (90–100%) |
|---|---|---|---|---|
| **Problem Clarity** | No clear problem or dataset identified | Dataset named; problem vague or generic | Clear problem + dataset with relevant context | Compelling, well-scoped problem with thoughtful dataset rationale |
| **Proposed Approach** | No methodology mentioned | Algorithm named but no justification | Algorithm + reasoning; shows course knowledge | Sophisticated approach with alternatives considered |
| **Feasibility & Challenges** | No feasibility discussed | Minimal thought given to challenges | Realistic challenges identified | Proactive mitigation strategies proposed |
| **Writing Quality** | Incomplete or unreadable | Hard to follow; missing sections | Clear and complete; meets length requirement | Professional, concise, well-structured |

---

## Part 2: Final Project Report (25%)

### What to Submit

An individual **Jupyter Notebook** demonstrating your ability to apply course concepts to a real-world dataset. The notebook must include both working code and written explanation (via Markdown cells). A separate written summary is acceptable but not required if the Markdown in your notebook is sufficiently thorough.

### Required Sections

Your notebook must address each of the following sections. Use Markdown headers to clearly delineate them:

**1. Introduction & Problem Statement**
- Describe the dataset: source, size, features, and target variable
- Clearly state the prediction problem and why it matters
- Identify whether this is a regression or classification task

**2. Data Exploration & Visualization**
- Summary statistics (shape, dtypes, describe())
- At least three meaningful visualizations (distributions, correlations, class balance, etc.)
- Written interpretation of each visualization — what does it tell you?

**3. Data Preprocessing & Feature Engineering**
- Handle missing values — document your strategy and rationale
- Encode categorical variables as needed
- Scale/normalize features where appropriate
- Create or select features intentionally; explain why

**4. Model Building & Training**
- Implement at least two different algorithms from the course
- Use train/test split (or cross-validation) appropriately
- Document hyperparameter choices and any tuning performed

**5. Model Evaluation**
- Report appropriate metrics (accuracy, F1, RMSE, ROC-AUC, etc.)
- Compare model performance side-by-side
- Interpret results — which model performed best and why?

**6. Discussion & Reflection**
- What surprised you? What would you do differently?
- What are the limitations of your model?
- Ethical considerations: who could this model affect? Are there bias concerns?

**7. Conclusion**
- Summarize your findings in plain language
- State the practical takeaway from your analysis

**8. AI Attribution Declaration**

As required by the course AI policy, include a properly formatted attribution cell at the top of your notebook. For B/A-level credit, also include inline attribution cells adjacent to any AI-assisted code. Failure to attribute AI use is an academic integrity violation.

### Submission Details

| | |
|---|---|
| **Format** | .ipynb file (Jupyter Notebook) — submitted via Canvas |
| **Due Date** | Monday, May 4, 2026 by 6:00 PM CT (before class begins) |
| **Grace Period** | Grace period applies through Wednesday, May 6 at 11:59 PM CT |
| **Unsolvable Bug Pass** | May be used; however, late submission can only extend to Saturday, May 9 (final grades are due Monday morning) |

### Report Rubric

| Criterion | F/D (< 70%) | C (70–79%) | B (80–89%) | A (90–100%) |
|---|---|---|---|---|
| **Data Exploration & Visualization** | Little/no EDA; missing visuals | Basic stats + 1–2 visuals; minimal interpretation | 3+ meaningful visuals with written interpretation | Insightful EDA that directly informs modeling decisions |
| **Preprocessing & Feature Engineering** | Raw data passed to model; errors likely | Basic cleaning; no feature rationale | Thoughtful preprocessing with documented decisions | Advanced features; clear impact on model performance shown |
| **Model Implementation** | Code doesn't run or uses wrong tool entirely | One model runs; no comparison | Two+ models implemented and compared correctly | Sophisticated models with well-reasoned hyperparameter choices |
| **Model Evaluation** | No metrics or incorrect metrics used | Correct metric reported; no interpretation | Appropriate metrics with interpretation; models compared | Deep interpretation; metric choice justified for problem type |
| **Discussion & Reflection** | Missing or superficial | Brief reflection; no limitations or ethics | Limitations and one ethical consideration addressed | Nuanced reflection; bias, fairness, and real-world impact discussed |
| **Code Quality & Documentation** | Code is unclear or not commented | Runs but poorly documented | Well-commented with logical structure | Professional-quality notebook; easy to follow for any reader |
| **AI Attribution** | No attribution | Attribution present but incomplete | Complete attribution (tool, prompt, learning, sections) | Inline + summary attribution; used AI as a professional tool |
| **Written Communication** | Unreadable or missing prose | Choppy; technical without explanation | Clear explanation of decisions and results | Compelling narrative; accessible to non-technical audience |

---

## Part 3: Final Project Presentation (10%)

### What to Expect

During the final class session (Monday, May 4, 2026), each student will deliver a **10-minute live presentation** of their Final Project. The presentation will be followed by a brief Q&A in which Dr. Marsh may ask clarifying or probing questions. This Q&A is a key component of the A-level assessment — it tests whether you can explain and defend your own work without relying on notes or AI.

### Presentation Structure (suggested)

You have 10 minutes. A suggested breakdown:

| Time | Content | Duration |
|---|---|---|
| Opening | Problem introduction — what are you predicting and why does it matter? | ~1 min |
| Data | Dataset overview — key features, size, interesting patterns from your EDA | ~2 min |
| Methods | Algorithms used, preprocessing choices, and why you made those decisions | ~2.5 min |
| Results | Model performance, comparison, visualizations of results | ~2.5 min |
| Takeaways | What you learned, limitations, and one ethical consideration | ~2 min |

### Presentation Tips

- You do not need slides — live demo of your Jupyter Notebook is perfectly acceptable (and often more impressive)
- Practice your timing — 10 minutes goes faster than you expect
- Prepare for Q&A: be ready to explain any cell in your notebook, any metric you report, and any decision you made
- Speak to the problem, not just the code — your audience includes non-technical stakeholders in the real world

### Presentation Rubric

| Criterion | F/D (< 70%) | C (70–79%) | B (80–89%) | A (90–100%) |
|---|---|---|---|---|
| **Problem Communication** | Problem not explained or unclear | Problem stated but lacking context | Clear problem statement with motivation | Compelling framing; audience understands stakes immediately |
| **Technical Accuracy** | Major errors in explanation or methodology | Some confusion about methods/results | Accurate explanation of methods and results | Expert-level explanation; can field difficult questions |
| **Visual Communication** | No visuals or visuals are confusing | Visuals present but not explained | Visuals are clear and referenced in narrative | Polished, purposeful visuals that drive the story |
| **Time Management** | Significantly over or under time | Slightly over/under; pacing uneven | Within time; reasonable pacing | Confident pacing; strong opening and close |
| **Q&A / Live Mastery** | Cannot answer basic questions about own work | Partial answers; relies heavily on notes | Answers questions accurately with some depth | Defends decisions confidently; shows genuine mastery |

---

## Choosing Your Dataset

You are free to choose any dataset that interests you, provided it meets the requirements below. Good datasets come from a variety of sources:

- **Kaggle** (kaggle.com) — wide variety of datasets and competitions
- **UCI Machine Learning Repository** (archive.ics.uci.edu)
- **Google Dataset Search** (datasetsearch.research.google.com)
- **Data.gov** — U.S. government open data
- **Your own area of interest** — sports, music, public health, finance, etc.

### Dataset Requirements

- At least **500 rows** of data
- At least **5 meaningful features** (not including the target variable)
- A clearly defined **target variable** (what you are predicting)
- Appropriate for a **regression or classification** task
- **Not** a toy dataset from scikit-learn's built-in library (e.g., Iris, Titanic, Boston Housing are not acceptable)

If you are unsure whether your dataset is appropriate, bring it to office hours before the Check-in deadline. Dr. Marsh can help you assess feasibility and scope.

---

## Proficiency-Based Grading Reminder

This project uses the same proficiency-based grading philosophy as the rest of the course:

- **C-Level (70–79%):** Your code works and produces correct results. AI assistance is expected and acceptable. Basic attribution is required.
- **B-Level (80–89%):** Everything from C-level, plus you can explain your code and demonstrate understanding of your decisions through your written summary and Q&A responses.
- **A-Level (90–100%):** Everything from B-level, plus your work shows originality, sophistication, and evidence of independent mastery. You can discuss your project in depth without relying on AI-generated explanations.

**Your grade reflects your level of understanding, not whether you used AI.**

---

## Frequently Asked Questions

**Can I use AI tools on the Final Project?**
Yes — within the AI policy outlined in the syllabus. During Weeks 10–13, you are expected to use AI professionally with full attribution. You must be able to explain every line of your code. The live Q&A during your presentation will reveal your actual level of understanding. AI use without attribution is academic dishonesty.

**Can I work with a partner?**
No. The Final Project is an individual assignment. You may discuss ideas with classmates, but all code and written work must be your own.

**Does the "Unsolvable Bug" pass apply to the Report?**
Yes — but with an important caveat. Because final grades are due to the Registrar on Monday morning after the last class, using the pass on your Final Project Report extends the deadline to Saturday, May 9, 2026 at 11:59 PM CT (not the usual Monday). Plan accordingly.

**What if I change my dataset or approach after the Check-in?**
That is fine — the Check-in is a planning tool, not a binding contract. If you make a significant pivot, briefly note the change in your Final Report and explain your reasoning. If you are unsure, email Dr. Marsh.

**How long should the notebook be?**
There is no cell minimum or maximum. Notebooks that earn A-level grades tend to have thorough Markdown explanations throughout — not just code. Quality of reasoning matters more than quantity of output.

**What counts as an "ethical consideration"?**
Think about the real people behind the data. Who could be affected if this model makes a wrong prediction? Are certain groups over- or under-represented in the dataset? Could the predictions be used in a way that causes harm? Even a brief, genuine engagement with these questions is valued. This connects directly to the Faith Integration emphasis of the course.

---

> **A Note on Faith & Responsibility**
>
> *Every data point in your dataset may represent a human being created in God's image. When you build a predictive model — whether forecasting loan defaults, medical outcomes, or consumer behavior — you are making decisions that affect real lives. The Final Project is not just a technical exercise; it is an opportunity to practice the kind of ethical discernment that separates a good data scientist from a great one.*
>
> **"…to search out a matter is the glory of kings." — Proverbs 25:2**

---

*Questions? Reach out via OBU email (patrick.marsh@okbu.edu) or stop by office hours. Don't wait until the last week — early feedback leads to better projects!*