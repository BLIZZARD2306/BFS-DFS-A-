# Pathfinding Lab

An interactive visualizer for three classic pathfinding algorithms: **breadth-first search (BFS)**, **depth-first search (DFS)** and **A\***. Draw a maze, pick an algorithm, and watch it search for the goal.

The whole project is one file, `pathfinding-lab.html`, with plain HTML, CSS and JavaScript. There are no dependencies and no build step.

## Features

- Three algorithms, selectable from cards at the top of the page
- A 32 × 18 grid where you can draw walls and move the start and goal
- Animated search: discovered cells, visited cells, then the final path
- Each card keeps the results of its last run (cells visited and path length), so you can run all three on the same maze and compare
- Speed slider and a random-walls generator
- Black-and-white interface with automatic light and dark themes
- Touch support and a reduced-motion fallback

## Getting started

Download `pathfinding-lab.html` and open it in any current browser.

## Using it

| Action | How |
| --- | --- |
| Draw walls | Click and drag on empty cells |
| Erase walls | Click and drag starting on a wall |
| Move start or goal | Drag the green (start) or red (goal) dot |
| Choose an algorithm | Click the BFS, DFS or A\* card |
| Run the search | Press **Run** |
| Remove the search overlay | Press **Clear path** (walls stay) |
| Generate a random maze | Press **Random walls** |
| Wipe the board | Press **Reset** |

The board is locked while a search runs. Editing the board clears the stored results on the cards, so they always match the current maze.

## The algorithms

| Algorithm | Data structure | Shortest path | Behavior |
| --- | --- | --- | --- |
| BFS | Queue | Yes | Expands in layers; visits many cells but never misses the shortest route |
| DFS | Stack | No | Follows one branch before backtracking; often finds a long, winding path |
| A\* | Priority list ordered by f = g + h | Yes | Uses distance to the goal as a hint; usually visits far fewer cells than BFS |

Implementation notes:

- Movement is 4-directional and every step costs 1.
- A\* uses Manhattan distance, which never overestimates on this grid, so its path is always a shortest one.
- If the goal is walled off, the search ends with a "No path" message.

## Customizing

Grid size is set near the top of the script:

```js
const C = 32, R = 18;  // columns and rows
```

If you change `C`, also update `grid-template-columns: repeat(32, 1fr)` on `#grid`.

Colors are CSS variables at the top of the stylesheet, with separate light and dark values. Each algorithm is a branch of `solve()`, which returns a list of discover and visit events plus the final path; the animation only replays that list. To add an algorithm, add a branch there and an entry in `INFO`.

## Possible extensions

- Diagonal movement
- Weighted cells, to show where BFS and Dijkstra differ
- Dijkstra and greedy best-first search
- A side-by-side race mode
