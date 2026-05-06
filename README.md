# Implementation of A* and Dijkstra on a Quarry Area

This project implements and compares two classic pathfinding algorithms — **A\*** and **Dijkstra's** — on occupancy grid maps derived from a real-world quarry area (Rellis Campus). The project is implemented in Python using Google Colab.

---

## Table of Contents

- [Overview](#overview)
- [Algorithms](#algorithms)
- [Map Representation](#map-representation)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Results](#results)
- [Dependencies](#dependencies)

---

## Overview

The goal of this project is to find the optimal path between a start and goal position on quarry terrain maps at multiple resolutions (10x10m, 5x5m, and 2x2m). The maps are derived from PGM (Portable Gray Map) occupancy grid images of the Rellis Campus quarry area.

Both algorithms are evaluated and compared based on:
- Path quality
- Computation / simulation time

---

## Algorithms

### A* Search (`A_star.ipynb`)

A* is an informed search algorithm that uses a heuristic to guide pathfinding efficiently.

- **Cost function:** `f(n) = g(n) + h(n)`
  - `g(n)` — cost from start to current node
  - `h(n)` — Euclidean distance heuristic to the goal
- **Movement:** 4-directional (up, down, left, right)
- **Data structure:** `PriorityQueue` ordered by f-cost
- **Key methods:**
  - `grid_to_index()` / `index_to_grid()` — coordinate conversions
  - `calculate_heuristic_cost()` — Euclidean distance to goal
  - `find_child_nodes()` — generates valid 4-neighbors
  - `astar_search()` — main loop expanding lowest f-cost nodes

### Dijkstra's Algorithm (`Djkstra.ipynb`)

Dijkstra's is an uninformed search algorithm that explores all nodes uniformly by cost.

- **Cost function:** `f(n) = g(n)` (no heuristic)
- **Movement:** 4-directional (up, down, left, right)
- **Data structure:** Priority queue ordered by travel cost
- **Key methods:**
  - `dijkstra_search()` — main loop expanding least-cost nodes
  - `find_child_nodes()` — generates valid 4-neighbors
  - `travel_to_node_cost()` — computes edge traversal cost

---

## Map Representation

- **Source:** PGM occupancy grid images of Rellis Campus quarry area
- **Resolutions tested:** 10x10m, 5x5m, 2x2m
- **Cell encoding via `PerceptionMapper`:**
  - Free space (pixel intensity >= 125): cost = `1`
  - Obstacle (pixel intensity < 125): cost = `1000`
- Path is visualized as red polygons overlaid on the matplotlib map

---

## Project Structure

```
.
├── A_star.ipynb        # A* algorithm implementation and visualization
├── Djkstra.ipynb       # Dijkstra's algorithm implementation and visualization
├── index.html          # Supporting HTML file
├── main.cpython-311.pyc
├── .gitignore
└── README.md
```

---

## How to Run

1. Open the notebooks in [Google Colab](https://colab.research.google.com/) or Jupyter Notebook.
2. Upload the required quarry area PGM map files.
3. Run all cells sequentially in either `A_star.ipynb` or `Djkstra.ipynb`.
4. The notebook will:
   - Load and parse the occupancy grid map
   - Run the pathfinding algorithm for multiple start/goal pairs
   - Display the computed path overlaid on the map
   - Print simulation times for each run

---

## Results

| Resolution | Algorithm  | Approx. Simulation Time |
|------------|------------|-------------------------|
| 10x10m     | Dijkstra   | ~0.03s                  |
| 5x5m       | Dijkstra   | ~0.5s                   |
| 2x2m       | Dijkstra   | ~5.8s                   |
| 10x10m     | A*         | Faster (heuristic-guided) |
| 5x5m       | A*         | Faster (heuristic-guided) |
| 2x2m       | A*         | Faster (heuristic-guided) |

A* significantly outperforms Dijkstra in speed due to its heuristic-guided search, especially at finer resolutions.

---

## Dependencies

- Python 3.x
- `numpy`
- `matplotlib`
- `queue` (Python standard library)
- `time` (Python standard library)
- `PIL` / `Pillow` (for image loading)

Install dependencies:

```bash
pip install numpy matplotlib Pillow
```

---

## Author

**Bharathtammi**  
Project implemented in Google Colab (Python)
