# 📦 Dantzig-Wolfe Decomposition for Structured Linear Programs

This repository implements the **Dantzig-Wolfe decomposition algorithm** in Python using **Pyomo**, tailored for solving large-scale linear programming problems with **block-angular structure** and **shared constraints**. The models decompose naturally into independent subproblems and a coordinating master problem.

---

## 📘 Problem Overview

Two structured linear programming models are considered:

### Model 1 

**Objective**:
Minimize: `-x₁ - 8x₂ - 5y₁ - 6y₂`

**Constraints**:

* Coupling constraint: `x₁ + 4x₂ + 5y₁ + 2y₂ ≤ 7`
* Subproblem 1 (x-block):

  * `5x₁ + x₂ ≤ 5`
  * `2x₁ + 3x₂ ≤ 6`
* Subproblem 2 (y-block):

  * `y₁ ≤ 4`
  * `3y₁ + 4y₂ ≥ 12`
  * `y₂ ≤ 3`

### Model 2

**Objective**:
Minimize: `-2x₁ - 3x₂ - 2y₁ + y₂`

**Constraints**:

* Coupling constraints:

  * `x₁ + y₁ ≤ 2`
  * `x₁ + x₂ + 2y₂ ≤ 3`
* Subproblem 1 (x-block):

  * `x₁ + 2x₂ ≤ 5`
  * `x₁ ≤ 2`
* Subproblem 2 (y-block):

  * `2y₁ + y₂ ≤ 6`
  * `-y₁ + y₂ ≤ 2`

---

## ⚙️ Algorithmic Approach

The algorithm performs the following:

1. **Formulate Master Problem (RMP)** with initial feasible corner points from subproblems.
2. **Iteratively solve subproblems** to generate new columns (extreme points).
3. **Update RMP** with columns having negative reduced cost.
4. **Terminate** when no improving columns exist (reduced costs ≥ 0).

Each subproblem is modeled in Pyomo and solved using **GLPK**. The dual values from the RMP guide the objective function of each subproblem.

---

## 🔁 Iterative Results Summary

### Model 1

* Iteration 1:

  * Reduced cost X: -16.0
  * Reduced cost Y: -20.0
* Iteration 2:

  * Reduced costs for both blocks = 0 → Optimal

**Final Solution**:

* Objective Value: **-20.0**
* X = \[0, 0.25], Y = \[0, 3]

---

### Model 2

* Iteration 1: X: -8.5, Y: -6.0
* Iteration 2: X: -4.29, Y: 0
* Iteration 3: X: 0, Y: 0 → Optimal

**Final Solution**:

* Objective Value: **-11.5**
* X = \[0, 2.5], Y = \[2, 0]

---

## 🛠 Tools & Technologies

* **Language**: Python 3.10
* **Modeling Library**: Pyomo
* **Solver**: GLPK
* **Dependencies**: `numpy`, `pyomo`

---

## 📁 Files

* `Dantzig- Wolfe Algorithm.ipynb`: Python implementation with full iteration logic
* `DantzigWolfe Decomposition Algorithm.docx`: Detailed explanation in Persian
* `Optimization Model 1.png`, `Optimization Model 2.png`: Model diagrams
