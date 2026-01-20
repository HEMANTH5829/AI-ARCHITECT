# AI Architect

## Project Overview
I want to create an AI tool that converts user requirements into intelligent, space-saving interior layouts. The algorithm arranges all specified rooms efficiently according to user instructions, eliminates typical architectural design errors, and optimizes the overall floor plan. Additionally, the tool suggests and places space-saving furniture within the interior layout.

---

## Key GitHub Repositories
- Floor-Plan-Generator-Using-AI (z-aqib)
  - https://github.com/z-aqib/Floor-Plan-Generator-Using-AI
  - Generates floor plans from room requirements using Constraint Satisfaction Problem (CSP). Backend in Python; frontend in Java (Jython integration).
- AIBot-Interiors-Helper / InteriorsAIDesigner (TheMagicWorlds / MeetYourAI)
  - https://github.com/TheMagicWorlds/AIBot-Interiors-Helper
  - Static prototype for Interiors AI Design (GPL-3.0).
- DeepFloorplan (zlzeng)
  - https://github.com/zlzeng/DeepFloorplan
  - Multi-task network and resources for floor plan recognition (TFRecord datasets).
- RoomAligner (Ashad001)
  - https://github.com/Ashad001/RoomAligner
  - Tools to align room elements for better flow and space utilization.
- Intellidecor (prathameshparit)
  - https://github.com/prathameshparit/Intellidecor
  - AI-powered furnishing of empty rooms using OpenAI + diffusion models.
- FurnitureRecommenderSystem (shakewingo)
  - https://github.com/shakewingo/FurnitureRecommenderSystem
  - LDA-based living room furniture recommender (text + image).
- floorplans topic (browse more related repos)
  - https://github.com/topics/floorplans
- MSD (Benchmark dataset repo)
  - https://github.com/caspervanengelenburg/msd
- LCSF / dataset2 (furniture layouts)
  - https://github.com/CODE-SUBMIT/dataset2
- MLSTRUCT-FP (multi-unit floor plan dataset)
  - https://github.com/MLSTRUCT/MLSTRUCT-FP

---

## Training Datasets (recommended)
- MSD Dataset (Benchmark for floor plan generation of building complexes)
  - Paper / dataset page: https://arxiv.org/html/2407.10121v1
  - GitHub: https://github.com/caspervanengelenburg/msd
  - Scale: ~5.3K complex plans, 18.9K apartments; graph attributes and annotations.
- ResPlan (vector-graph dataset of residential floor plans)
  - Paper: https://arxiv.org/html/2508.14006v1
  - Scale: ~17K vector-graph residential floor plans (good for generative design and spatial reasoning).
- LCSF Dataset (Layout of Custom-size Furniture)
  - GitHub: https://github.com/CODE-SUBMIT/dataset2
  - Scale: ~710K custom furniture layouts with positions and sizes.
- MLSTRUCT-FP
  - GitHub: https://github.com/MLSTRUCT/MLSTRUCT-FP
  - Multi-unit floor plans with wall annotations in JSON (MIT licensed).
- DeepFloorplan data (R3D/R2V TFRecords)
  - Repo: https://github.com/zlzeng/DeepFloorplan
  - Useful for recognition/segmentation models.

Dataset comparison (quick):

| Dataset | Scale | Key Features | Best For |
|---|---:|---|---|
| MSD | 5.3K plans | Graphs, geometry, multi-apartment | Complex multi-unit layout generation |
| LCSF (dataset2) | 710K layouts | Furniture positions/sizes | Furniture placement and space-saving layouts |
| DeepFloorplan | Variable | Images, TFRecords | Floor plan recognition / segmentation |
| MLSTRUCT-FP | ~954 (multi-unit) | JSON wall annotations | Architectural analysis & recognition |

---

## Suggested Space-saving Layout Algorithms
- Interactive Genetic Algorithms (IGA) + Differential Evolution (DE): hybrid evolutionary approach to optimize room arrangement and avoid local optima.
- Squarified Treemaps: hierarchical rectangular partitioning based on room sizes and adjacency constraints.
- Ant Colony Optimization (ACO): iteratively optimizes room connectivity and corridor design via pheromone-based search.

## AI / ML Approaches
- Convolutional Neural Networks (CNN): two-stage models predicting rooms and walls (useful with RPLAN-style datasets).
- Graph Neural Networks (GNN): model floor plans as graphs to capture adjacency and spatial relations for generation.
- Generative models (Diffusion / VAE / GAN): for producing plausible layout variations conditioned on requirements.

## Furniture Placement Strategies
- Rule-based heuristics (clearances, circulation paths, functional zones).
- Optimization-based placement (constrained placement solving with occupancy/clearance objectives).
- Learning-based placement (train on furniture-layout datasets to predict furniture positions and orientations).

---

## Next Steps / Recommendations
1. Decide which datasets to prioritize (2D vector plans vs raster images vs furniture layout datasets).
2. Choose a development path: classic optimization (GA/DE/ACO) + heuristics, or ML-first (GNN/CNN + diffusion models).
3. I can add detailed DATASETS.md and ALGORITHMS.md, create a src/ scaffold, and add example notebooks and a Streamlit/Gradio demo.

---

## Citations & References
1. z-aqib/Floor-Plan-Generator-Using-AI — https://github.com/z-aqib/Floor-Plan-Generator-Using-AI
2. TheMagicWorlds/AIBot-Interiors-Helper — https://github.com/TheMagicWorlds/AIBot-Interiors-Helper
3. caspervanengelenburg/msd (MSD dataset) — https://github.com/caspervanengelenburg/msd
4. zlzeng/DeepFloorplan — https://github.com/zlzeng/DeepFloorplan
5. Ashad001/RoomAligner — https://github.com/Ashad001/RoomAligner
6. prathameshparit/Intellidecor — https://github.com/prathameshparit/Intellidecor
7. shakewingo/FurnitureRecommenderSystem — https://github.com/shakewingo/FurnitureRecommenderSystem
8. CODE-SUBMIT/dataset2 (LCSF) — https://github.com/CODE-SUBMIT/dataset2
9. MLSTRUCT/MLSTRUCT-FP — https://github.com/MLSTRUCT/MLSTRUCT-FP
10. ResPlan paper — https://arxiv.org/html/2508.14006v1

---

*If any links don’t open when you click them, tell me which ones and I will verify and fix the links or add direct download instructions.*