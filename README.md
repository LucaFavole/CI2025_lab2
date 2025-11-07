## CI2025_lab2 — Genetic algorithm for the TSP

This repository contains an experimental implementation of an evolutionary algorithm to solve instances of the Traveling Salesperson Problem (TSP) stored as cost matrices (`.npy`) in the `lab2` folder.

The main code is provided in the `tsp.ipynb` notebook, which demonstrates how to load problem instances, run the algorithm, and compare the EA solution with a random tour.

## Solution representation

A solution (tour) is represented as an array of integers containing a permutation of [0..N-1]. The tour is cyclic: after the last city the tour returns to the first city.

Cost function
- cost(adj, sol): sums the edge weights following the permutation order; implemented using a shift (`np.roll`) to sum each edge (i -> next(i)).

## Initial population

- starting_point(problem): generates a random permutation of the cities using `np.random.default_rng().permutation`. For reproducibility, explicitly initialize the generator with a fixed seed when needed.

## Genetic operators

- swap_mutation(solution, mutation_rate): with probability `mutation_rate` swaps two positions in the solution. This keeps the permutation valid and introduces local variation.

- order_crossover_ox1(parent1, parent2): OX1 operator for permutations. It selects two cut points, copies the segment from `parent1` into the child, then fills remaining positions with elements from `parent2` in order, skipping duplicates.

## Selection

- tournament_selection(population, costs, k): selects k individuals at random (without replacement) and returns the one with the lowest cost. The parameter `k` controls selection pressure: small values preserve diversity, larger values increase pressure.

## Evolutionary cycle

The function `evolutionary_algorithm(problem, population_size, num_generations, tournament_size, mutation_rate, elitism, verbose)` implements the standard cycle:

1. Initialization: create a random population.
2. Evaluation: compute the cost of each individual.
3. Elitism: copy the best `elitism` individuals into the new generation.
4. Reproduction: selection (tournament) → crossover (OX1) → mutation (swap).
5. Replacement: the new population replaces the old one.
6. Update: track the best-so-far solution.
7. Termination: stop after `num_generations` (or another stopping condition if implemented).

The notebook also contains a utility `run_single_experiment(filepath, ...)` to run the EA on individual `.npy` files and a simple batch loop that processes all files in `lab2` and writes results to `result1.txt`.

## Suggested parameters (examples)

- population_size: 50-200 (depends on problem size and available compute)
- num_generations: 500-2000 for more thorough experiments
- mutation_rate: 0.01–0.2
- tournament_size: 3–50 (larger values increase selection pressure)
- elitism: 1–10

Use these as starting points and tune according to problem size and quality/time trade-offs.

## Included files

- `tsp.ipynb`: notebook with implementation and batch script
- `lab2/*.npy`: TSP instances for testing
- `result.txt`, `result1.txt`: output files produced by experiments

## Notes
- The result.txt files contain the best costs found by the EA and the cost of a random tour for comparison.