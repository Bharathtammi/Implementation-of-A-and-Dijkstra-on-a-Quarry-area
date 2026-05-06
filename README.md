# Path Planning on Quarry Maps: A* vs Dijkstra

This project compares **A\*** and **Dijkstra's algorithm** for shortest-path planning on occupancy-grid maps generated from a real quarry area at RELLIS Campus.[1]
Implemented in Python with Google Colab notebooks, the project evaluates how each algorithm behaves as map resolution becomes finer and search space grows larger.[1]

## Highlights

- Compares informed and uninformed graph-search algorithms on the same terrain maps.[1]
- Uses real occupancy-grid data derived from quarry-area PGM images.[1]
- Tests performance across 10x10 m, 5x5 m, and 2x2 m map resolutions.[1]
- Visualizes the planned route directly on the map output.[1]

## Table of Contents

- [Project Goal](#project-goal)
- [Why This Project Matters](#why-this-project-matters)
- [Algorithms Used](#algorithms-used)
- [Map Modeling](#map-modeling)
- [Repository Layout](#repository-layout)
- [How to Run](#how-to-run)
- [Performance Snapshot](#performance-snapshot)
- [Dependencies](#dependencies)
- [Author](#author)

## Project Goal

The main objective is to compute an optimal path between a start position and a goal position on quarry terrain maps represented as occupancy grids.[1]
The project then compares both algorithms using two practical criteria: pathfinding behavior and computation time.[1]

## Why This Project Matters

Path-planning performance changes sharply as resolution increases because the number of searchable cells rises and the algorithm must inspect more of the environment.[1]
This makes the project a useful demonstration of why heuristic-guided search such as A* is often preferred in robotics and autonomous navigation.[1]

## Algorithms Used

### A* Search — `A_star.ipynb`

A* is an informed search algorithm that combines accumulated travel cost with a heuristic estimate of the remaining distance to the goal.[1]
The implementation uses the evaluation function `f(n) = g(n) + h(n)`, where `g(n)` is the cost from the start node and `h(n)` is the Euclidean heuristic.[1]

**Key characteristics**
- 4-directional movement: up, down, left, right.[1]
- Priority-based expansion using `PriorityQueue`.[1]
- Helper routines for coordinate conversion, heuristic calculation, child-node generation, and core search execution.[1]

### Dijkstra's Algorithm — `Djkstra.ipynb`

Dijkstra's algorithm is an uninformed shortest-path method that expands nodes solely according to cumulative travel cost.[1]
Its evaluation function is `f(n) = g(n)`, which means no heuristic is used to guide the search toward the goal.[1]

**Key characteristics**
- 4-directional movement on the occupancy grid.[1]
- Priority-queue-based node expansion.[1]
- Core routines for search, neighbor generation, and node travel-cost computation.[1]

## Map Modeling

The terrain is represented using PGM occupancy-grid images of the quarry area.[1]
Cells are classified through `PerceptionMapper`, where pixels with intensity greater than or equal to 125 are treated as free space with cost `1`, and pixels below 125 are treated as obstacles with cost `1000`.[1]
The resulting path is displayed as an overlay on the Matplotlib-rendered map.[1]

## Repository Layout

```text
.
├── A_star.ipynb        # A* implementation and visualization
├── Djkstra.ipynb       # Dijkstra implementation and visualization
├── index.html          # Supporting HTML file
├── main.cpython-311.pyc
├── .gitignore
└── README.md
```

The repository is organized around two primary notebooks, each dedicated to one algorithm and its path-planning workflow.[1]

## How to Run

1. Open the project notebooks in Google Colab or Jupyter Notebook.[1]
2. Upload the required PGM quarry-area map files.[1]
3. Run all cells in either `A_star.ipynb` or `Djkstra.ipynb`.[1]
4. Review the generated visualization and the simulation-time output.[1]

During execution, the notebook loads the occupancy grid, runs the selected pathfinding algorithm for start and goal pairs, and plots the computed route over the map.[1]

## Performance Snapshot

| Resolution | Dijkstra | A* |
|---|---|---|
| 10x10 m | ~0.03 s [1] | Faster through heuristic guidance [1] |
| 5x5 m | ~0.5 s [1] | Faster through heuristic guidance [1] |
| 2x2 m | ~5.8 s [1] | Faster through heuristic guidance [1] |

The reported results show that A* outperforms Dijkstra in runtime, especially at finer map resolutions where the search space becomes larger.[1]

## Dependencies

- Python 3.x.[1]
- `numpy`.[1]
- `matplotlib`.[1]
- `queue` from the Python standard library.[1]
- `time` from the Python standard library.[1]
- `PIL` / `Pillow` for image loading.[1]

Install the required external packages with:

```bash
pip install numpy matplotlib Pillow
```

## Author

**Bharathtammi** created the project, which is described on GitHub as a Python implementation developed in Google Colab.[1]
