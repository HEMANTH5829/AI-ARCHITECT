# Algorithms for AI-ARCHITECT

This document summarizes recommended algorithms for generating space-saving interior layouts and furniture placement. It includes descriptions, key parameters, fitness metrics, pseudocode, and small Python snippets or library hints to get started.

## 1. Hybrid Interactive Genetic Algorithm (IGA) + Differential Evolution (DE)

Description
- Use a GA to explore discrete room arrangements (ordering, adjacency) and DE for fine-tuning continuous variables (room dimensions, positions).
- Fitness combines space utilization, adjacency satisfaction, circulation score, and lighting/ventilation heuristics.

Pseudocode
1. Initialize population of floorplan chromosomes (discrete + continuous parts).
2. Evaluate fitness for each individual.
3. While not converged:
   a. Select parents (tournament / roulette).
   b. Apply crossover/mutation on discrete part (GA operators).
   c. Apply DE mutation/recombination on continuous part.
   d. Repair infeasible solutions (overlap, negative areas) using backtracking.
   e. Replace population (elitism).
4. Return best individual.

Small Python sketch (DEAP + numpy outline)
```python
# simplified sketch
from deap import base, creator, tools
import numpy as np

creator.create("FitnessMax", base.Fitness, weights=(1.0,))
creator.create("Individual", list, fitness=creator.FitnessMax)

# individual encodes room order (permutation) + continuous dims
# ... build toolbox, evaluate, mate, mutate, selection ...
```  

Key notes
- Use constraint repair to enforce non-overlap and minimum clearance.
- Interactive loop: allow a user to pick favorites and bias the population.

## 2. Squarified Treemaps (Hierarchical Rectangular Partitioning)

Description
- Partition the overall bounding rectangle into sub-rectangles proportional to room area requirements while respecting adjacency constraints using hierarchical splitting.
- Fast and deterministic; good for initial layouts.

Pseudocode
1. Take list of rooms with target areas and adjacency groups.
2. Sort rooms by area descending.
3. Use squarified treemap algorithm to place rectangles into the bounding box.
4. Apply local optimization to swap or split to satisfy adjacency constraints.

Library hints
- Implement with a treemap library or write a simple squarified treemap (recursive packing).
- After placement, run smoothing pass to align edges and ensure minimum circulation space.

## 3. Ant Colony Optimization (ACO) for Adjacency & Circulation

Description
- Model rooms as nodes; pheromone trails represent preferred adjacencies and corridor routes. ACO finds sequences/orderings that minimize corridor length and maximize required adjacencies.

Pseudocode
1. Initialize pheromone matrix between room pairs.
2. Each ant constructs a sequence placing rooms into layout guided by pheromones and heuristics (size compatibility, function).
3. Evaluate constructed layout (fitness: adjacency satisfaction, corridor length).
4. Update pheromones based on best ants; evaporate.
5. Repeat until convergence.

Notes
- Combine with local improvement (2-opt style) on room ordering.

## 4. Constraint Programming (CSP) for Exact Layout Constraints (OR-Tools)

Description
- Use CP-SAT or CP-Solver (Google OR-Tools) to enforce exact constraints: room sizes, adjacency, minimum clearances, fixed locations (windows/doors), circulation paths.

Python example (OR-Tools CP-SAT sketch)
```python
from ortools.sat.python import cp_model
model = cp_model.CpModel()
# Example: place rectangles (x,y,width,height) as integers
# Add non-overlap constraints and area constraints
# Solve and extract positions
```

Use cases
- Precise legal/regulatory constraints or furniture-in-room packing.
- Use CP to validate or repair candidate layouts from heuristic methods.

## 5. Two-stage CNN approach (Room then Walls) — Recognition & Parsing

Description
- For datasets with raster floorplan images, use a CNN to first predict rooms (semantic segmentation) then a second stage to predict walls and vectorize them.
- Use DeepFloorplan and R3D/R2V datasets for training.

Training hints
- Use U-Net or HRNet backbones for segmentation.
- Use polygonization or post-processing to convert segmentation to vector walls.

## 6. Graph Neural Networks (GNN) for Graph-based Generation

Description
- Represent floorplans as graphs: nodes = rooms, edges = adjacency relations, attributes = size, function, door positions.
- Use graph generation models to sample plausible adjacency graphs, then embed spatial layout via node placement network or solver.

Library hints
- PyTorch Geometric (PyG) or DGL for building GNNs.
- Train to predict adjacency matrices and node geometry attributes.

## 7. Generative Models (Diffusion / VAE / GAN) for Layout Variation

Description
- Learn distribution of floorplans conditioned on room list and constraints. Use conditional diffusion or VAE to produce many candidate layouts for user selection.

Notes
- Diffusion models work well for high-quality raster outputs; add a vectorization step to convert to CAD-like representations.

## 8. Furniture Placement Strategies

Approaches
- Rule-based: clearance rules, standard placements (sofa against wall, bed aligned to wall), functional grouping.
- Optimization-based: formulate placement as ILP or continuous optimization minimizing overlap and maximizing function scores.
- Learning-based: train a model (CNN/GNN) on furniture-layout datasets (LCSF / dataset2) to predict positions and orientations.

ILP sketch (pulp)
```python
import pulp
# binary variables for discretized furniture placement positions
# objective: maximize coverage/score - penalty for overlap
```

## 9. Metrics & Fitness Functions

Common terms to include in fitness:
- Space Utilization = used_area / total_area
- Circulation Efficiency = average path length between key rooms
- Adjacency Satisfaction = fraction of required adjacencies met
- Natural Light Score = sum of room exposure to window-facing walls
- Ventilation Score = open-wall connectivity and cross-ventilation paths
- Furniture Fit = fraction of furniture placements that meet clearance rules

## 10. Integration Strategy

Recommended pipeline
1. Input parsing: user requirements -> room list + constraints.
2. Quick initial layout: squarified treemap or simple heuristic to provide instant feedback.
3. Optimization stage: run hybrid GA+DE or ACO+local search to improve layout for space-usage and adjacencies.
4. CSP repair: run OR-Tools to fix hard constraints.
5. Furniture placement: rule-based pass followed by optimization or learned model.
6. Post-process: lighting/ventilation check, user interaction loop, export (JSON/CAD/SVG).

## 11. Implementation Notes & Libraries

- Optimization & metaheuristics: DEAP, pygad, nevergrad
- CP & exact solving: OR-Tools
- GNNs: PyTorch Geometric (PyG), DGL
- CNNs & diffusion: PyTorch, torchvision, timm, Hugging Face diffusers
- Packing & packing libraries: rectpack, shapely for geometry
- ILP: pulp, OR-Tools linear solver
