# 🚚 Library Logistics Optimization: A Rich VRP Solver

## 📌 Overview
This repository implements an advanced two-phase optimization approach (First-Cluster-Then-Route) to solve a complex logistics network for 210 libraries in the Province of Brescia. The project tackles a **Rich Vehicle Routing Problem (VRP)**[cite: 11] that incorporates several advanced operational constraints.

## ⚙️ Operational Constraints Handled
*   **Simultaneous Pickup & Delivery (VRPSPD):** Vehicles must handle both delivering new books and picking up returns at every stop, causing dynamic load fluctuations[cite: 11].
*   **Hard Time Windows:** Strict adherence to the opening and closing hours of each library[cite: 11].
*   **Heterogeneous Fleet:** Optimization across a fleet of vehicles with varying cargo capacities (e.g., 30, 50, 80 units) using a First-Fit algorithm[cite: 11].

## 🧠 Methodology & Algorithms

### Phase 1: Strategic Clustering ($p$-Median Model)
To overcome the NP-hard nature of the global routing problem, the territory is first divided into $p=8$ optimal clusters[cite: 11]. 
*   **Solver:** Exact resolution using **Gurobi** (Mixed Integer Linear Programming)[cite: 11].
*   **Result:** Extracts the most populated cluster (37 libraries) to act as an independent sub-problem for the routing phase[cite: 11].

### Phase 2: Initial Routing (Constructive Heuristic)
Generates a fast, feasible initial solution using a Greedy approach[cite: 11].
*   **Algorithm:** Adapted **Clarke & Wright Savings Algorithm**[cite: 11].
*   **Validation:** A deterministic Feasibility Oracle checks time windows and capacity constraints before merging any routes[cite: 11].

### Phase 3: Metaheuristic Optimization
Refines the initial solution to escape local optima and minimize the total routing distance[cite: 11].
*   **Algorithm:** **Tabu Search**[cite: 11].
*   **Mechanics:** Explores the neighborhood using a *Relocate* operator, implementing a Short-Term Memory (Tabu List with tenure = 15) and an Aspiration Criterion to accept strictly better solutions[cite: 11].

## 🛠️ Tech Stack
*   **Python**[cite: 11]
*   **Gurobi Optimizer** (for exact mathematical modeling)[cite: 11]
*   **NumPy** (for distance matrix calculations)[cite: 11]
*   **Matplotlib** (for geospatial visualization of the clusters)[cite: 11]
