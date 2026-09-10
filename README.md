# 🚚 Library Logistics Optimization: A Rich VRP Solver

## 📌 Overview
This repository implements an advanced two-phase optimization approach (First-Cluster-Then-Route) to solve a complex logistics network for 210 libraries in the Province of Brescia. The project tackles a **Rich Vehicle Routing Problem (VRP)** that incorporates several advanced operational constraints.

## ⚙️ Operational Constraints Handled
*   **Simultaneous Pickup & Delivery (VRPSPD):** Vehicles must handle both delivering new books and picking up returns at every stop, causing dynamic load fluctuations.
*   **Hard Time Windows:** Strict adherence to the opening and closing hours of each library.
*   **Heterogeneous Fleet:** Optimization across a fleet of vehicles with varying cargo capacities (e.g., 30, 50, 80 units) using a First-Fit algorithm.

## 🧠 Methodology & Algorithms

### Phase 1: Strategic Clustering ($p$-Median Model)
To overcome the NP-hard nature of the global routing problem, the territory is first divided into $p=8$ optimal clusters. 
*   **Solver:** Exact resolution using **Gurobi** (Mixed Integer Linear Programming).
*   **Result:** Extracts the most populated cluster (37 libraries) to act as an independent sub-problem for the routing phase.

### Phase 2: Initial Routing (Constructive Heuristic)
Generates a fast, feasible initial solution using a Greedy approach.
*   **Algorithm:** Adapted **Clarke & Wright Savings Algorithm**.
*   **Validation:** A deterministic Feasibility Oracle checks time windows and capacity constraints before merging any routes.

### Phase 3: Metaheuristic Optimization
Refines the initial solution to escape local optima and minimize the total routing distance.
*   **Algorithm:** **Tabu Search**.
*   **Mechanics:** Explores the neighborhood using a *Relocate* operator, implementing a Short-Term Memory (Tabu List with tenure = 15) and an Aspiration Criterion to accept strictly better solutions.

## 🛠️ Tech Stack
*   **Python**
*   **Gurobi Optimizer** (for exact mathematical modeling)
*   **NumPy** (for distance matrix calculations)
*   **Matplotlib** (for geospatial visualization of the clusters)
