# Lightweight Cybersecurity Threat Detector

A research project that trains a small, fast machine-learning model to classify network
activity as **Normal**, **Suspicious**, or **Malicious/Attack**, using the public
**CICIDS2017** dataset.

**Research question:**
> How much detection performance can be retained while reducing the computational,
> memory, and model-size requirements of a machine-learning-based cybersecurity threat
> detector?

Author: Anush Jindal

---

## New here? Start with the setup guide

If you have never used Git, GitHub, Python, or Google Colab before, do not start with this
README — start with **[SETUP_GUIDE.md](SETUP_GUIDE.md)**. It walks through every tool,
every command, and every button-click in plain language, from zero.

Once your environment is set up, come back here for the project map.

---

## Where this project is right now

This repo currently covers **Stage 1 → Stage 4** of the full project plan:

| Stage | Name | Status |
|---|---|---|
| 1 | Research | Templates ready in `research/` — fill in as you learn |
| 2 | Dataset | Guide + notebook ready — `notebooks/01_dataset_exploration.ipynb` |
| 3 | Preprocessing | Guide + notebook ready — `notebooks/02_preprocessing.ipynb` |
| 4 | Feature Engineering | **You write this one** — see `notebooks/03_FEATURE_ENGINEERING_GUIDE.md` |
| 5+ | Baseline model, optimization, benchmarking, app/game | **Not started on purpose** — see note below |

**We deliberately stop before training the first model.** The point of Stages 1-4 is to
fully understand and prepare the data. Only once that is solid (and reviewed) do we move
on to training a Decision Tree baseline. Jumping ahead defeats the point of the exercise —
you would be tuning a model on data you don't actually understand yet.

Use **[CHECKLIST.md](CHECKLIST.md)** to confirm each stage is genuinely done before moving
to the next one.

---

## Folder structure

```
anush/
├── README.md                          ← you are here
├── SETUP_GUIDE.md                     ← start here if you're new to any of this
├── CHECKLIST.md                       ← verification checklist for Stages 1-4
├── setup.bat                          ← one-click local environment setup (Windows)
├── requirements.txt                   ← Python libraries this project needs
├── .gitignore                         ← tells Git which files NOT to track (e.g. raw data)
│
├── research/
│   ├── research_question.md           ← the research question, spelled out
│   ├── literature_review.md           ← template — fill in as you read about IDS/ML
│   ├── references.md                  ← every official link you need, in one place
│   ├── attack_categories.md           ← what each CICIDS2017 attack type actually means
│   └── feature_documentation_template.md  ← Feature | Meaning | Type | Keep/Remove | Reason
│
├── notebooks/
│   ├── 01_dataset_exploration.ipynb   ← load the data, inspect it, understand it
│   ├── 02_preprocessing.ipynb         ← clean it, split it safely (no data leakage)
│   ├── 03_feature_engineering.ipynb   ← SKELETON — you fill this in
│   └── 03_FEATURE_ENGINEERING_GUIDE.md ← step-by-step instructions + resources for the above
│
├── data/
│   └── README.md                      ← which CICIDS2017 file to use + where to get it
│                                         (the actual .csv file is NEVER committed to GitHub)
│
├── models/                            ← trained models get saved here (not committed yet)
│
└── experiments/
    ├── results.csv                    ← one row per experiment (empty template for now)
    └── experiment_notes.md            ← your running notes on what you tried and why
```

`src/`, `app/`, `game/` are intentionally **not created yet** — they belong to later stages
(model training, optimization, and the application/game) and we don't want empty,
meaningless folders cluttering the repo before there's real code to put in them.

---

## The full pipeline (for context)

```
Public Cybersecurity Dataset → Data Understanding → Preprocessing → Feature Engineering
   → Baseline ML Model → Lightweight Model Optimization → Resource Benchmarking
   → Application/Game → Research Analysis
```

We are working on the first four boxes. Everything after "Feature Engineering" is future
work — do not start it yet (see `CHECKLIST.md`).

## Hardware note

No GPU is required or used anywhere in this project. Everything runs on free CPU-only
Google Colab, and the final model is specifically meant to be small enough to run on an
ordinary laptop CPU.
