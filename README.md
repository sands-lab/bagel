# BAGEL: Bootstrap AGgregated Ensemble Layer

> **A modular, lightweight, and incrementally updatable framework for malicious prompt detection in Large Language Models.**

## 🥯 Overview

Current LLM defenses force a trade-off between the opacity of black-box APIs and the prohibitive computational costs of white-box and monolithic "LLM-as-a-judge" systems. Furthermore, keeping these systems updated against rapidly evolving attack vectors often requires expensive end-to-end retraining.

**BAGEL** offers a modular alternative. It is an ensemble framework inspired by bootstrap aggregation and mixture-of-experts, designed to provide "safety in depth" without the computational overhead.

Unlike traditional bagging, BAGEL trains each small ensemble member of 86M parameters (which we call 'promptcops') on **entirely different attack datasets** to ensure specialization. At inference, it utilizes a hybrid strategy: a Random Forest router identifies the most suitable promptcop based on structural prompt features, while **stochastic selection** samples additional promptcops to ensure robustness. The predictions from the chosen ensemble subset of promptcops are aggregated for the final prompt classification.

### Key Performance Indicators
*   **Efficiency and Performance:** Delivers an F1 score of **0.922**, with a low Attack Success Rate (0.095) and False Positive Rate (0.066) even with an effective footprint of just **430M parameters** (selection size = 5), significantly smaller than billion-parameter baselines.
*   **Incremental Updates:** Solves the adaptability challenge. New attack types are handled by fine-tuning a single new promptcop and adding it to the ensemble, eliminating the need for full-system retraining.
*   **Interpretability:** The router’s structural features provide transparent insights into malicious prompting patterns.


## 📂 Repository Structure

Below is a list and description of the project files and folder.

### Core Framework

- `bagel_main_experiments.ipynb`
  - Contains the code for finetuning promptcops and evaluating them across varying selection sizes while introducing new datasets/promptcops over time, thus replicating Experiments 1 and 2.


### Datasets

- `datasets/`
  - Contains some datasets used during evaluations. We provide these as they either required manual downloading from their sources or because we have applied certain pre-processing steps to them.
