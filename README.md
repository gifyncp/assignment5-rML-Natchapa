# Assignment 5: Adversarial Machine Learning Audit

**Course:** DNSC 6330 – Responsible Machine Learning  
**Instructor:** Michael Akinwumi  
**Student:** Natchapa Aunkay (Gift)  

---

## Overview
This project implements an adversarial machine learning (AML) audit on predictive models using the COMPAS dataset. The goal is to evaluate model vulnerability across **security, fairness, and privacy dimensions** under intentional attacks.

This assignment extends Lecture 04 (robustness) into **Lecture 05 (ML security and abuse pathways)**, focusing on how adversaries exploit model weaknesses.

---

## Objectives
The notebook evaluates model behavior under three major adversarial threats:

- **Evasion Attacks (PGD)** → Can inputs be manipulated to fool the model?
- **Data Poisoning** → Can training data be corrupted to degrade fairness?
- **Membership Inference** → Can attackers infer training data membership?

---

## Models Used
- Logistic Regression (LR)
- Gradient Boosted Tree (GBT)

---

## Dataset
- COMPAS dataset (recidivism prediction)
- Target variable: `two_year_recid`

---

## Libraries Used
- pandas  
- numpy  
- matplotlib  
- seaborn  
- scikit-learn  
- statsmodels  

---

## How to Run

1. Open the notebook in Google Colab or Jupyter Notebook  
2. Install required libraries if needed:
   ```bash
   pip install statsmodels
3. Run all cells from top to bottom
4. Ensure dataset is loaded correctly

---

## Project Structure

🔹 Part 1: PGD Evasion Audit
Apply Projected Gradient Descent (PGD) attack across ε values
Measure:
False Positive Rate (FPR) by race
Adverse Impact Ratio (AIR)
Key Finding:
Logistic Regression is highly vulnerable → FPR increases dramatically
GBT remains stable → more robust to perturbations
AIR approaching 1.0 does not indicate fairness, but model collapse

🔹 Part 2: Poisoning Loop with Fairness Monitoring
Simulate label-flip poisoning at different rates
Track:
AUC (performance)
AIR (fairness)
Key Finding:
AUC remains stable → attack is not detectable via performance
AIR changes significantly → fairness is degraded
Identifies a stealth attack (fairness breaks without accuracy drop)

🔹 Part 3: Membership Inference Attack
Implement shadow model pipeline
Evaluate:
MI AUC
Confidence gap distribution
Key Finding:
MI AUC ≈ 0.50 → no strong privacy leakage
Confidence overlap suggests low inference risk
Generalization gap does not strongly predict MI risk in this case

🔹 Part 4: Reflection & Risk Assessment
Highest Risk Identified:
Stealth poisoning attack that degrades fairness without affecting performance
Mitigation Strategies:
Proactive: Fairness-aware monitoring (track AIR alongside AUC)
Reactive: Data integrity controls (audit training labels, secure pipelines)
Tradeoffs:
Fairness improvements may reduce accuracy
Increased monitoring adds operational complexity
Balancing fairness, robustness, and performance is inherently difficult

---

## Key Insights
Models can appear accurate while being fundamentally compromised
Fairness metrics are critical for detecting hidden failures
Traditional monitoring (e.g., AUC, PSI) is insufficient against adversarial attacks
Security, fairness, and privacy must be evaluated jointly, not separately

---

## Responsible ML Perspective
This project demonstrates that:
ML systems are vulnerable to intentional manipulation, not just data drift
Attacks can target:
Integrity (poisoning)
Availability (evasion)
Privacy (membership inference)
Trustworthy AI requires:
Robustness testing
Fairness monitoring
Security-aware design

---

## AI Usage Disclosure
Generative AI (ChatGPT) was used to assist with formatting and improving clarity. All analysis, modeling decisions, and interpretations are my own.
