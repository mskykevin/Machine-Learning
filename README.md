# Machine-Learning

My machine learning workspace. It has two parts:

1. **[`study/`](#study)**: notes and exercises from studying ML systems.
2. **[`projects/`](#projects)**: standalone ML projects, each built end to end.

Both parts follow the structure of Chip Huyen's *Designing Machine Learning Systems*
(O'Reilly, 2022). The book treats ML as a whole system, not just a model: data,
features, training, deployment, monitoring, iteration, infrastructure and people. Using
its chapters as the backbone keeps what I study and what I build connected. Every concept
in `study/` has a matching stage in every project.

---

## Repository layout

```
Machine-Learning/
├── README.md
├── study/                                  # learning: notes (.md) and coding practice
│   ├── README.md
│   ├── ml-fundamentals/                    # core ML concepts (Ace the Data Science Interview)
│   │   ├── Machine-Learning-Key-Concepts.md
│   │   └── practice/                       # coding exercises
│   ├── 01-overview-of-ml-systems/
│   ├── 02-ml-systems-design/
│   ├── 03-data-engineering-fundamentals/
│   ├── 04-training-data/
│   ├── 05-feature-engineering/
│   ├── 06-model-development-and-offline-evaluation/
│   ├── 07-model-deployment-and-prediction-service/
│   ├── 08-data-distribution-shifts-and-monitoring/
│   ├── 09-continual-learning-and-test-in-production/
│   ├── 10-infrastructure-and-tooling-for-mlops/
│   └── 11-human-side-of-ml/
│
└── projects/                               # building: one folder per project
    ├── _template/                          # copy this to start a new project
    └── <project-name>/
```

---

## Study

`study/` holds my notes and coding practice. See [`study/README.md`](study/README.md).

### ML fundamentals

Core ML concepts (algorithms, model evaluation, the math) that the systems book assumes
you already know:

- [**Machine Learning Key Concepts**](study/ml-fundamentals/Machine-Learning-Key-Concepts.md):
  key concepts from the Machine Learning chapter of *Ace the Data Science Interview*, with
  self-check questions and a progress checklist.
- [`practice/`](study/ml-fundamentals/practice/): coding exercises for those concepts.

### Designing Machine Learning Systems

Notes on the book, plus outside reading (papers, blog posts, courses) filed under the
chapter it relates to.

| # | Chapter | Focus | Folder |
|---|---------|-------|--------|
| 1 | Overview of Machine Learning Systems | When ML is the right tool; ML in research vs. production; ML systems vs. traditional software | `study/01-overview-of-ml-systems/` |
| 2 | Introduction to Machine Learning Systems Design | Business and ML objectives; requirements (reliability, scalability, maintainability, adaptability); framing a problem as an ML task | `study/02-ml-systems-design/` |
| 3 | Data Engineering Fundamentals | Data sources and formats; data models and storage; batch vs. stream processing | `study/03-data-engineering-fundamentals/` |
| 4 | Training Data | Sampling; labeling (including weak supervision and active learning); class imbalance; data augmentation | `study/04-training-data/` |
| 5 | Feature Engineering | Common feature operations; data leakage; feature importance and generalization | `study/05-feature-engineering/` |
| 6 | Model Development and Offline Evaluation | Model selection; ensembles; experiment tracking; distributed training; AutoML; offline evaluation | `study/06-model-development-and-offline-evaluation/` |
| 7 | Model Deployment and Prediction Service | Batch vs. online prediction; model compression; ML on the cloud and at the edge | `study/07-model-deployment-and-prediction-service/` |
| 8 | Data Distribution Shifts and Monitoring | Causes of ML failure; types of shift and how to detect them; monitoring and observability | `study/08-data-distribution-shifts-and-monitoring/` |
| 9 | Continual Learning and Test in Production | Stateless vs. stateful retraining; how often to retrain; shadow deployment, A/B tests, canaries, bandits | `study/09-continual-learning-and-test-in-production/` |
| 10 | Infrastructure and Tooling for MLOps | Storage and compute; development environment; resource management; ML platforms; build vs. buy | `study/10-infrastructure-and-tooling-for-mlops/` |
| 11 | The Human Side of Machine Learning | User experience; team structure; responsible AI | `study/11-human-side-of-ml/` |

### What goes in each chapter folder

```
study/04-training-data/
├── notes.md           # key ideas in my own words, plus open questions
├── exercises/         # notebooks and small experiments that try the ideas out
└── resources.md       # papers, posts and talks related to the chapter
```

How I take notes:
- Write the ideas in my own words. Don't copy the book.
- End each `notes.md` with a section called **"How this applies to my projects"** that
  links to the matching stage of a real project in `projects/`.
- A small experiment is better than a long summary. Put runnable code in `exercises/`.

### Progress

| Topic | Status |
|---------|--------|
| ML fundamentals (Ace the Data Science Interview) | Key concepts written; practice not started |
| DMLS chapters 1–11 | Not started |

---

## Projects

Each folder in `projects/` is one self-contained ML project. Every project follows the
same lifecycle, taken from the book, so any project can be read the same way and picked up
quickly.

### Standard project layout

```
projects/<project-name>/
├── README.md                     # problem, status, results, how to run
├── PROGRESS.md                   # live status: current stage, tasks, blockers, next steps
├── docs/
│   ├── 01-problem-framing.md     # Ch 1–2: business goal, ML objective, requirements, success metrics
│   ├── 02-data.md                # Ch 3–4: sources, storage, sampling, labeling, data quality
│   ├── 03-features.md            # Ch 5: feature list, leakage checks, feature importance
│   ├── 04-modeling.md            # Ch 6: baselines, experiments, offline evaluation
│   ├── 05-deployment.md          # Ch 7: batch vs. online, serving design, latency budget
│   ├── 06-monitoring.md          # Ch 8: metrics to watch, drift detection, alerts
│   ├── 07-iteration.md           # Ch 9: retraining strategy, testing in production
│   ├── 08-infrastructure.md      # Ch 10: tools, compute, platform choices
│   ├── 09-responsible-ml.md      # Ch 11: users, fairness, privacy, failure modes
│   └── decisions/                # short decision records (0001-chose-xgboost.md, ...)
├── data/                         # local data only; gitignored (raw/, interim/, processed/)
├── notebooks/                    # exploration (numbered: 01-eda.ipynb, ...)
├── src/
│   ├── data/                     # ingestion and validation
│   ├── features/                 # feature pipelines
│   ├── models/                   # training and evaluation
│   └── serving/                  # prediction service or batch job
├── tests/
├── configs/                      # experiment and pipeline configs
└── requirements.txt | pyproject.toml
```

Not every project needs every stage. A Kaggle-style project might stop at `04-modeling.md`.
Keep the numbered files anyway and write one line explaining why a stage was skipped, so
the gap is a deliberate choice.

### Lifecycle checklist

Use this checklist in each project's `PROGRESS.md`:

- [ ] **Framing:** business objective, ML objective and success metric written down; ML
      confirmed to be the right tool
- [ ] **Data:** sources documented; train/validation/test split strategy chosen (time-based
      where it matters); label quality checked
- [ ] **Features:** leakage review done; features computed the same way in training and
      serving
- [ ] **Modeling:** a simple baseline (heuristic or linear model) beaten by a measured
      margin; experiments tracked
- [ ] **Offline evaluation:** beyond the headline metric, includes slice-based evaluation,
      calibration and perturbation checks
- [ ] **Deployment:** prediction mode chosen (batch or online); latency and cost measured
- [ ] **Monitoring:** input, prediction and outcome metrics defined; drift checks in place
- [ ] **Iteration:** retraining trigger and cadence defined; plan for testing in production
- [ ] **Responsible ML:** who the model affects, how it can fail, and what happens when it
      does

### Project index

| Project | Problem | Stage | Status |
|---------|---------|-------|--------|
| _none yet_ | | | |

---

## Starting a new project

1. `cp -r projects/_template projects/<project-name>`
2. Fill in `docs/01-problem-framing.md` before writing any code.
3. Add a row to the [project index](#project-index).
4. Update `PROGRESS.md` at the end of every working session.

## Reference

- Nick Singh & Kevin Huo, *Ace the Data Science Interview*, 2021.
- Chip Huyen, *Designing Machine Learning Systems: An Iterative Process for
  Production-Ready Applications*, O'Reilly Media, 2022.
