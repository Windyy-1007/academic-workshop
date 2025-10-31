+++
title = "IJCNN 2026: The 2nd Challenge — Explainable AI for Educational Question-Answering"
template = "page.html"
+++

# The 2nd Challenge: Explainable AI for Educational Question-Answering

**International Joint Conference on Neural Networks (IJCNN) 2026**

---

## Introduction

Large Language Models (LLMs) have demonstrated impressive abilities in question-answering systems, including those applied in educational contexts. However, these models often generate only brief, single-answer responses without providing any reasoning or explanatory detail. In educational environments, this lack of transparency poses significant challenges:

**Quality of Answers:** When an answer is incorrect, we cannot trace or understand the source of the error. When it is correct, we have no visibility into how it was derived or whether it was properly verified.

**Complex Reasoning:** Educational domains often involve intricate rules, policies, and multi-step logical reasoning, which can be challenging for purely data-driven LLMs to handle reliably.

A promising approach to address these challenges is **Symbolic Reasoning**, an emerging direction in Explainable AI (XAI). By incorporating a Symbolic Engine—either standalone or integrated with an LLM—the reasoning process can be explicitly represented. This integration enhances both the accuracy and interpretability of educational QA systems, making them more suitable for transparent and verifiable use in learning environments.

### Example Queries

Below are two sample queries that illustrate how an XAI-enhanced system is expected to provide clear and transparent explanations:

| Query | Expected Answer |
|-------|----------------|
| This semester, I scored 8 points on the final exam for the DSA course. However, I was absent for the lab exam. Can I still get a B in this course? | **No.** Because you missed the lab exam, you received a score of 0 for lab work. According to Regulation #13 of X University, a student with 0 lab points cannot pass the course. |
| Calculate the equivalent resistance of the following circuit, given that each resistor has a resistance of r. | Since the resistors are connected together at both ends, the circuit can be redrawn to show that the three resistors are connected in parallel. Therefore, the equivalent resistance is: **R = r / 3** |

In this season's challenge, the system will not only handle academic regulation questions but also be capable of reasoning within a natural science domain, specifically **Physics**—focusing on electric circuit problems. The goal remains the same: to combine Symbolic Logic and LLM-based reasoning to produce transparent, step-by-step explanations.

---

## Challenge Objectives

This challenge aims to **advance Explainable AI for Education** by fostering innovative hybrid approaches that integrate symbolic reasoning with language-based understanding. Specifically, we seek to:

- **Promote transparent and interpretable reasoning** in educational QA systems  
- **Encourage the use of symbolic logic and LLMs** for complex, rule-based problem-solving  
- **Extend XAI research into STEM domains** such as physics (electric circuits)  
- **Provide benchmark datasets and evaluation frameworks** to support future developments in neurosymbolic AI for education

### What You'll Build

Participating teams will develop systems that:

- **Provide correct final answers** to educational queries
- **Generate clear, structured, and verifiable explanations** (premises + reasoning path)
- **Combine symbolic logic engines** (e.g., Z3 or custom solvers) with open-source LLMs for natural-language parsing or translation to logic

---
{{ new_block() }}



## Judges and Chairmans

{{ grid(
    text = [
        ["Judge A","Institution A"], 
        ["Judge B","Institution B"],
        ["Chairman C","Institution C"],
        ["Chairman D","Institution D"],
        ["Chainman E","Institution E"],
    ],
    urls = [
        "https://aterenin.github.io/academic-workshop#speaker_a",
        "https://aterenin.github.io/academic-workshop#speaker_b",
        "https://aterenin.github.io/academic-workshop#speaker_c",
        "https://aterenin.github.io/academic-workshop#speaker_d",
        "https://aterenin.github.io/academic-workshop#speaker_e",
    ],
    images = [
        "placeholder.svg",
        "placeholder.svg",
        "placeholder.svg",
        "placeholder.svg",
        "placeholder.svg",
    ],
    narrow = true) }}


---
## Competition Rules

### DO

**Integrate a Symbolic Engine:** Participants must incorporate symbolic reasoning to verify and explain answers based on predefined regulations or rules. Solutions may use Z3 Solver or a custom-built symbolic engine to ensure logical consistency and transparency.

**Generate Clear Explanations:** Every generated answer must be accompanied by a structured explanation, citing relevant policies, regulations, or logical steps. The explanation should be concise, interpretable, and verifiable, ensuring transparency in reasoning.

**Use Open-Source LLMs (if applicable):** If an LLM is used for Natural Language to Logic conversion or answer generation, it must be open-source and **under 8 billion parameters**. This encourages transparency and prevents reliance on proprietary, black-box models.

### DO NOT

**Use Closed-Source Models:** Solutions must not rely on commercial LLMs such as GPT, DeepSeek, etc. While these models can be used during development, submissions based entirely on closed-source models will be ranked lower than those leveraging fine-tuned, lightweight open-source models.

**Undisclosed Data Usage:** All external datasets used for fine-tuning LLMs or Symbolic Engines must be fully disclosed. Submissions must include details on data source, purpose, and usage. **Failure to disclose external data usage will result in disqualification.**

---

## Datasets

The official datasets will be released at the kickoff meeting. Two dataset types will be provided:

### Dataset Type 1: Logic-Based Educational Queries

**1,000 records** designed to evaluate logical reasoning and inference capabilities. Each record includes:

- **Premises** in both natural language and first-order logic (FOL) representation
- **Questions** derived from the premises, including:
  - Yes/No/Uncertain-type questions
  - Listing-type questions
  - "How many"-type questions
- **Ground truth answers** corresponding to each question type

**Sample Record:**

| Statements | FOL Representation |
|------------|-------------------|
| 1. Every course contains knowledge. | `∀c (Course(c) → ContainsKnowledge(c))` |
| 2. If a student takes a course and passes the exam, they acquire knowledge. | `∀s, c (Takes(s, c) ∧ Passes(s, c) → AcquiresKnowledge(s))` |
| 3. If a student acquires knowledge, they gain understanding. | `∀s (AcquiresKnowledge(s) → GainsUnderstanding(s))` |
| 4. Tuan attended the course "Natural Language Processing Semester 242" taught by Thơ and passed the exam. | `Takes(Tuan, NLP) ∧ Passes(Tuan, NLP) ∧ Student(Tuan) ∧ Course(NLP)` |

**Questions:**
- Does "Natural Language Processing Semester 242" contain knowledge? → **True** (`ContainsKnowledge(NLP)`)
- Does Tuan have more understanding than before? → **True** (`GainsUnderstanding(Tuan)`)
- Will a student gain more knowledge when they have understanding? → **Uncertain** (`∀s (GainsUnderstanding(s) → AcquiresKnowledge(s))`)

### Dataset Type 2: ViPPS (Vietnamese Physics Problems)

**5,520 multimodal physics problems** focusing on electric circuits:

- **3,750 examples** include at least one diagram
- **1,770 examples** are text-only
- **448 unique schematic images** ranging from clean textbook illustrations to hand-drawn student sketches
- All problems and diagrams are in **Vietnamese**

For each problem, your model should return:
- **Final Answer** (numeric or conceptual, exactly as requested)
- **Explanation** summarizing the reasoning steps (equations used, circuit laws applied, diagram cues interpreted, assumptions, and unit checking)

There are **no mandatory intermediate formalisms** (no FOL proofs or fixed rule engines required). Use any reasoning style—chain-of-thought, tool-use, diagram parsing, or hybrid methods—provided the outcome is an accurate answer plus a concise justification.

**External Datasets:** Participants may use external datasets for fine-tuning, testing, or evaluation, provided that their usage is clearly declared at submission.

---

## Evaluation Criteria

Submissions will be evaluated based on the following three criteria:

| Criterion | Description |
|-----------|-------------|
| **P1: Correctness of Answers** | Generating accurate and precise answers for the given queries |
| **P2: Relevance of Premises** | Correctly identifying and applying the relevant premises used for reasoning |
| **P3: Logical Reasoning Flow** | Providing a structured and coherent reasoning process that leads to the correct answer |

**Final Score:** The final score will be computed as a weighted average of P1, P2, and P3. Specific weights will be published with the official dataset release.

**Live Evaluation:** A live evaluation session will be conducted using a private test dataset containing **50-100 questions**, where the submitted APIs will be tested in real-time. The organizers will livestream the evaluation process, and teams must join to observe results, verify correctness, and provide feedback if necessary.

---

## Submission Requirements

Teams will have **one day** to submit both their API and a brief solution description (1-2 pages) detailing their approach, models used, and the dataset used for training.

### API Format

The API must return, for each query:

- **Generated Answer** (final answer)
- **Number of Premises Used**
- **List of Premises Utilized**
- **Reasoning Path** (structured or natural language explanation leading to the answer)

The detailed API specification and submission portal will be announced at the dataset release and kickoff meeting.

### Expected Output Structure

Your system should produce:
- **Answers** structured around Yes/No responses and enumerations, ensuring clarity and consistency
- **Supporting premises** that justify the provided answers, helping to establish transparency in reasoning
- **Reasoning paths** that outline the step-by-step process leading to the final answers, presented in either natural language or another structured format that is easy to interpret

---

## Timeline

| Activity | Details | Date |
|----------|---------|------|
| **Team Registration** | Teams register with a maximum of 5 members per team. Individual participants may request to be assigned to a team by the organizers. | **TBD** |
| **Pre-selection** (if required) | If the number of teams is greater than 20, a pre-selected challenge of MCQ questions about LLM and XAI will be held to select 10 best teams for the competition. | **TBD** |
| **Workshop & Dataset Release** | Organizers will release the dataset, detailed competition rules (including evaluation criteria), and conduct a literature review session to help teams understand the problem, explore related works, and review baseline models for reference. | **TBD** |
| **On-event Challenge** | Teams are free to apply any symbolic reasoning-based approach to address the challenge requirements, as long as it complies with the rules. Development period: **2-3 weeks**. | **TBD** |
| **API Submission** | Teams are required to host their API in the specified format and submit it along with a brief solution description detailing their approach, methodology, and dataset usage. | **TBD** |
| **Public Test Day** | Organizers will livestream the evaluation process, testing each system on individual queries. Teams must join to observe results, verify correctness, and provide feedback if necessary. | **TBD** |
| **Result Announcement** | The top-performing teams will be announced based on the evaluation criteria. | **TBD** |
| **Paper Submission** | The top 10 teams with the highest scores will be invited to submit a research paper describing their approach and findings. The top 3 highest-rated teams will be invited to present in Maastricht and compete for championship titles. | **TBD** |

**Note:** The dates provided are for reference only and may be adjusted or extended depending on the circumstances. Any changes will be regularly communicated to all participating teams.

---

## Prizes and Awards

The competition will award the following prizes:

### First Prize
- Trophy
- Cash prize
- Opportunity to publish as a **regular paper** in the International Workshop on Trustworthiness and Reliability in Neurosymbolic AI proceedings (IJCNN 2026)
- Invitation to present in **Maastricht**

### Second Prize
- Trophy
- Cash prize
- Opportunity to publish as a **regular paper** in the International Workshop on Trustworthiness and Reliability in Neurosymbolic AI proceedings (IJCNN 2026)
- Invitation to present in **Maastricht**

### Third Prize
- Trophy
- Cash prize
- Opportunity to publish as a **regular paper** in the International Workshop on Trustworthiness and Reliability in Neurosymbolic AI proceedings (IJCNN 2026)
- Invitation to present in **Maastricht**

### Additional Recognition

- **Top 10 teams:** Will have their papers published as challenge papers on the official challenge website
- **All valid participants:** Will receive an official certificate issued by the workshop chairs

---

## Jury Composition and Conflict-of-Interest Policy

### Jury Composition

The evaluation jury will consist of:

- **Academic Experts** specializing in Explainable AI, Symbolic Reasoning, and Educational Technologies
- **Organizing Committee Members** from the Understanding and Reasoning with AI (URA) group

### Conflict-of-Interest (COI) Policy

To ensure fairness, transparency, and impartiality:

- Jury members must declare any direct or indirect affiliation with participating teams  
- Members with a COI (e.g., advisor-student relationships, institutional overlap, or prior collaborations) will be recused from evaluating the corresponding teams  
- The COI process will be documented and verified by the competition's oversight chair

---

## Organizers and Sponsors

This challenge is organized by:

**Understanding and Reasoning with AI (URA)**  
Ho Chi Minh City University of Technology  
Vietnam National University, Ho Chi Minh City

**Sponsored by:**
- Ho Chi Minh City University of Technology - Vietnam National University, Ho Chi Minh City
- University of Naples Parthenope, Naples, Italy

---

## Registration and Contact

**Minimum Requirement:** The challenge requires at least **7 participating teams** to be held.

**Team Formation:** If the number of teams is greater than 20, a pre-selected challenge of MCQ questions about LLM and XAI will be held to select 10 best teams for the competition.

### Contact Information

**Email:** [ura.hcmut@gmail.com](mailto:ura.hcmut@gmail.com)

Once registration is finalized, the organizers will set up a communication platform (e.g., Discord) to facilitate discussions with the teams.

---

*This challenge aims to advance the field of Explainable AI in education by bringing together researchers, practitioners, and students to develop innovative neurosymbolic systems that provide transparent, verifiable, and interpretable reasoning for educational question-answering.*
