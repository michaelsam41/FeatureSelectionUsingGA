# FeatureSelectionUsingGA
Feature selection in medical image analysis using Genetic Algorithms

#  Feature Selection Using Genetic Algorithm with Simulated Annealing Hybrid

This project applies a **Genetic Algorithm (GA)** for feature selection using a **K-Nearest Neighbors (KNN)** classifier to evaluate the fitness of selected feature subsets. The system integrates advanced techniques like **Simulated Annealing-inspired mutation decay**, **elitism**, **early stopping**, and customizable strategies for **selection**, **crossover**, and **mutation**—resulting in a powerful and flexible optimization tool.

---

##  Key Features

- **Fitness Evaluation**: Based on a multi-objective function combining:
  - F1 Score
  - Specificity
  - Feature Reduction (penalizes large feature sets)
- **Classifier**: K-Nearest Neighbors (KNN) used for fitness computation.

###  Genetic Algorithm Components

- **Selection Methods**:
  - Tournament Selection
  - Roulette Wheel Selection
  - Rank-Based Selection
- **Crossover Operators**:
  - Single-Point
  - Two-Point
  - N-Point
  - Uniform Crossover
- **Mutation Techniques**:
  - Bit Flip
  - Random Resetting
  - Multi-bit Mutation
- **Elitism**: Top 7% of individuals are preserved in each generation to retain high-performing solutions.
- **Early Stopping**: Stops the algorithm if no improvement is observed for a defined number of generations.

---

##  Hybrid GA with Simulated Annealing-Inspired Mutation

To improve exploration and convergence, a **Simulated Annealing-inspired mechanism** controls the mutation rate dynamically throughout the evolution process.

###  Motivation

- **Early exploration** (high mutation) helps avoid premature convergence.
- **Late-stage refinement** (low mutation) allows better fine-tuning.
- **Adaptive mutation boosts** prevent stagnation when the population stops improving.

###  How It Works

- Mutation rate **decays exponentially** across generations using a cooling schedule:
  
  \[
  \text{mutation\_rate} \propto e^{-kt}
  \]

- If the best fitness does **not improve** for `N` generations:
  - A **temporary mutation boost** is triggered to promote diversity and escape local optima.

### Benefits

- **Avoids local minima** by maintaining diversity.
- **Accelerates convergence** while balancing exploration and exploitation.
- **Improves robustness** of the GA by combining strengths from both paradigms.

This hybrid approach merges **Simulated Annealing's exploratory nature** with the **Genetic Algorithm's population-based optimization**, resulting in a more resilient and effective feature selector.

---

## Flow of the GA Evolution Loop

Each generation includes:

1. **Fitness Evaluation**: Evaluate each chromosome (feature subset) using KNN.
2. **Elitism**: Preserve top individuals unchanged.
3. **Stagnation Detection**: If no improvement, apply early stopping or temporary mutation boost.
4. **Selection & Crossover**: Generate offspring from selected parents.
5. **Mutation**: Apply mutation based on the current adaptive rate.
6. **Tracking & Logging**: Log best fitness, diversity, mutation effects, and feature count.

---

##  Parameter Settings

```python
population_size = 150
num_generations = 125
mutation_rate = 0.08
early_stopping_rounds = 15
crossover_rate = 0.8
