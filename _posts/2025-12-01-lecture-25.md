---
layout: distill
title: "Lecture 25: Alignment, Explainability, and Open Directions in LLM Research"
description: >
  Improved lecture notes covering alignment, interpretability, fairness, scaling laws,
  and open research challenges in large language models.
date: 2025-12-01

lecturers:
  - name: Ben Lengerich
    url: "https://adaptinfer.org"

authors:
  - name: Abel Zewdie
---

## Overview and Learning Goals

This lecture examines how we **understand**, **trust**, and **align** large machine learning models—particularly large language models (LLMs)—with human values and real-world objectives. As models scale and become more capable, ensuring that they behave in reliable, interpretable, and value-aligned ways becomes increasingly important.

By the end of this lecture, students should be able to:
- Explain why interpretability is essential for modern ML systems
- Compare major interpretability approaches and understand their limitations
- Distinguish between **outer alignment** and **inner alignment**
- Describe how scaling laws complicate interpretability and alignment
- Identify key open challenges in responsible and aligned AI

---

## Phases of Model Training

Large modern models are typically developed through three distinct stages:

### Pre-training  
Models are trained in an unsupervised or self-supervised manner on massive datasets, allowing them to learn broad statistical patterns and general representations.

### Fine-tuning  
Pre-trained models are adapted for specific goals using supervised learning, reinforcement learning, or instruction-following objectives.

### In-context Learning  
At inference time, models adjust their behavior based on prompts and examples provided in the input, without modifying their underlying parameters.

![Phases of Training](assets/lecture25/lecture25_phases.png)

---

## Why Explainability Matters

Models trained on large-scale data are rarely interpretable by default. As model complexity increases, it becomes more difficult to understand **why** a model produces a particular output.

Explainability plays a critical role in:
- **Safety:** identifying harmful or unintended behaviors  
- **Trust:** enabling users to rely on model outputs  
- **Debugging:** diagnosing errors and failure modes  
- **Ethics and regulation:** meeting legal and societal expectations  

---

## Fairness and Sensitive Features

Removing sensitive attributes (such as race or gender) from training data does **not** guarantee fairness. Models may still encode sensitive information through correlated features like income, location, or education level.

More effective strategies include:
- Training with sensitive features and removing or correcting their influence after training  
- Designing objectives that explicitly penalize dependence on sensitive attributes  

**Example:**  
A healthcare model trained without race may still encode racial bias via proxy variables, obscuring rather than eliminating unfairness.

---

## Interpretability Approaches

### 1. Post-hoc Explanations

Post-hoc methods attempt to explain model behavior **after** predictions have been made.

- **LIME (Locally Interpretable Model-Agnostic Explanations):**  
  Approximates complex models locally using simpler surrogate models.

- **SHAP (SHapley Additive exPlanations):**  
  Uses Shapley values from cooperative game theory to assign feature importance scores.

- **Integrated Gradients:**  
  Attributes predictions to input features by integrating gradients from a baseline to the actual input.

![Post-hoc Methods](assets/lecture25/lecture25_lime_shap_ig.png)

While useful for interpreting individual predictions, these methods may fail to capture global model behavior and can be unstable under adversarial conditions.

---

### 2. Transparency by Design

Transparency-by-design approaches aim to build models that are interpretable by construction, rather than explaining black-box systems after the fact.

- **Generalized Additive Models (GAMs):**  
  Predictions are expressed as sums of simple, interpretable functions of individual features.

- **Monotonic Models:**  
  Enforce constraints ensuring certain features affect predictions in only one direction.

**Advantages:** clear, component-wise reasoning  
**Limitations:** may underperform on highly complex tasks

![GAMs](assets/lecture25/lecture25_gam.png)

---

### 3. Mechanistic Interpretability

Mechanistic interpretability seeks to understand **what neural network components are doing internally**, such as:
- Neuron activations  
- Learned circuits  
- Feature representations across layers  

This approach aims to uncover high-level computational motifs within networks, but remains an active and challenging research area.

---

## Caveats of Interpretability

All interpretability methods involve simplifying assumptions:
- Explanations are often partial or approximate  
- Different methods may produce inconsistent explanations  
- Adversarial inputs can undermine many explanation techniques  

Interpretability should therefore be treated as a tool for insight, not as definitive ground truth.

---

## Scaling Laws vs. Interpretability

Empirical scaling laws show that increasing model size and data often leads to predictable improvements in performance. However, as models scale, their internal reasoning becomes increasingly opaque.

![Scaling Laws](assets/lecture25/lecture25_scaling_laws.png)

One proposed response is **system-level design**, in which complex AI systems are decomposed into modular, interpretable components that balance performance with understanding.

---

## Information Acquisition

Traditional predictive models assume all measurements are fixed and freely available. In practice:
- Data collection can be expensive  
- Important information may be missing  
- Interpretability can reveal which measurements are most valuable  

This reframes learning as an **active information acquisition problem** rather than a passive prediction task.

---

## Modularity

Modular systems are composed of swappable, testable components:
- Each module serves a specific function  
- Components can be evaluated independently  
- Modularity supports long-term interpretability as systems grow more complex  

![Modularity](assets/lecture25/lecture25_modularity.png)

---

## Value Alignment

Alignment concerns whether a model optimizes for objectives that reflect human values and intentions.

- **Outer Alignment:**  
  Does the objective or loss function accurately capture what we want the model to do?

- **Inner Alignment:**  
  Does the model robustly pursue that objective in new or unexpected situations?

| Concept | Key Question | Risk if Violated |
|-------|--------------|------------------|
| Outer Alignment | Is the objective correct? | Optimizing the wrong goal |
| Inner Alignment | Does behavior generalize safely? | Unpredictable failures |

---

## Inner Alignment in Practice: Jagged Performance

A model may perform well on average yet fail catastrophically on specific inputs—a phenomenon known as **jagged performance**.

Examples include:
- Strong benchmark performance with rare but severe errors  
- High overall accuracy with isolated, unpredictable failures  

![Jagged Performance](assets/lecture25/lecture25_jagged_performance.png)

Such behavior is a key indicator of poor inner alignment and is particularly concerning in safety-critical domains.

---

## Risks of Misalignment and Goodhart’s Law

When a measurement becomes a target, it ceases to be a good measure—a principle known as **Goodhart’s Law**.

**Example:**  
A medical model learns that aggressive kidney treatment correlates with survival and recommends it universally. While statistically accurate, this behavior is unsafe when applied blindly.

![Goodhart’s Law](assets/lecture25/lecture25_goodharts_law.png)

---

## Open Challenges and Takeaways

Key open challenges in alignment research include:
- Robust reinforcement learning at scale  
- Designing stable, value-aligned reward functions  
- Continual learning instead of repeated retraining  
- Formal frameworks for alignment across diverse contexts  
- Ethical and societal impacts of increasingly capable models  

Alignment is not a single technique, but a **system-level research agenda** requiring technical, ethical, and societal considerations.

---

## Summary

- Interpretability is essential but inherently limited  
- Alignment requires careful objective design and robustness  
- Scaling improves performance while complicating understanding  
- Future AI systems must balance capability with responsibility  

These challenges define some of the most important open directions in modern AI research.
