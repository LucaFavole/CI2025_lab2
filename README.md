# TSP via Evolutionary Algorithm

This project uses an Evolutionary Algorithm (EA) to solve a complex Traveling Salesperson Problem (TSP).

## Problem

The cost matrix (`problem`) defines an **Asymmetric TSP (ATSP)**. Key features include:
* Negative costs
* Non-zero diagonal
* No triangular inequality

These traits require a meta-heuristic approach.

## Algorithm Architecture

The EA (`evolutionary_algorithm`) evolves a population of permutation-based solutions using:

* **Selection:** `tournament_selection` (selects the best of `k` random individuals).
* **Crossover:** `order_crossover_ox1` (OX1) to create valid offspring.
* **Mutation:** `swap_mutation` (swaps two random cities).
* **Survival:** Elitism (preserves the best `elitism` individuals).

## Execution

Run the final notebook cell to execute `evolutionary_algorithm`. Key parameters can be adjusted:

* `POP_SIZE`: Population size
* `GENERATIONS`: Number of iterations
* `MUTATION_RATE`: Mutation probability
* `TOURNAMENT_K`: Tournament size for selection
* `ELITISM_COUNT`: Number of elite individuals to save