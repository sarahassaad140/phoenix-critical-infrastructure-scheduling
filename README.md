# Phoenix – Critical Infrastructure Repair Scheduling

## Overview

Phoenix is an Artificial Intelligence planning and optimization project that simulates the recovery of critical infrastructure following a conflict or natural disaster.

The project focuses on restoring three essential services:

- 💧 Water Network
- ⚡ Power Network
- 📡 Communication Network

Using Artificial Intelligence search algorithms, the system determines the optimal repair schedule that maximizes the number of citizens receiving essential services as early as possible while operating under limited resources and time constraints.

---

## Problem Statement

Following a large-scale infrastructure failure, multiple districts lose access to critical services.

Decision-makers must answer:

- Which repair tasks should be performed first?
- How should limited crews be allocated?
- Which sequence of actions maximizes citizen benefit?

The objective is to restore services to the largest number of citizens in the shortest amount of time.

---

## Scenario

The simulation models 8 districts:

- Beirut (Source Node)
- Baabda
- Metn
- Keserwan
- Jbeil
- Zahle
- Saida
- Tripoli

Each district has a population weight representing the number of citizens that benefit once the district becomes fully functional.

---

## Infrastructure Layers

The project models three independent but interconnected infrastructure networks:

### 💧 Water Network
Represents water distribution pipelines between districts.

### ⚡ Power Network
Represents electrical transmission and distribution systems.

### 📡 Communication Network
Represents communication and fiber connectivity.

A district becomes functional only when it is connected to Beirut through all three networks simultaneously.

---

## Constraints

### Available Resources
- Maximum Crews: **K = 2**

### Planning Horizon
- Total Time: **12 Hours**

### Scheduling Rules
- Repair jobs are non-preemptive
- Crews cannot be split during execution
- Limited repair capacity
- Different repair durations for each task

---

## Objective Function

The goal is to maximize the number of functional citizens over time.

### Functional Citizens

\[
F(t)=\sum_{v \in V} Pop(v)\cdot 1(v \text{ functional at } t)
\]

where:

- Pop(v) = district population
- F(t) = number of citizens receiving all services at time t

---

### Area Under the Curve (AUC)

The optimization target is:

\[
AUC=\int_0^T F(t)\,dt
\]

This rewards restoration plans that bring districts online earlier rather than later.

A district restored at hour 3 contributes more benefit than the same district restored at hour 8.

---

## Search Problem Representation

Phoenix is formulated as a State-Space Search Problem.

### State

Each state contains:

- Current time
- Completed repairs
- Running repairs
- Available crews
- Functional districts

### Actions

Start one or more feasible repair tasks while respecting crew constraints.

### Transition

Advance to the next repair completion event and update the system state.

---

## Search Algorithms Implemented

### Breadth-First Search (BFS)

- Explores all states level by level
- Complete
- Extremely expensive for large search spaces

### Depth-First Search (DFS)

- Explores one path deeply before backtracking
- Low memory usage
- Not guaranteed to find optimal solutions

### Uniform Cost Search (UCS)

- Expands nodes with minimum accumulated cost
- Complete and optimal
- Computationally expensive

### Greedy Search

- Uses only heuristic information
- Fast
- Can produce suboptimal solutions

### A* Search

Uses:

\[
f(n)=g(n)+h(n)
\]

where:

- g(n) = accumulated cost
- h(n) = heuristic estimate

A* combines path cost and future benefit estimation, providing the best balance between efficiency and solution quality.

---

## A* Heuristic Design

The heuristic estimates the remaining citizen benefit that can still be recovered.

The search prioritizes schedules that:

- Restore high-population districts first
- Minimize downtime
- Maximize total citizen-hours

This significantly reduces the search space compared to uninformed algorithms.

---

## Technologies Used

- Python
- Artificial Intelligence
- Graph Theory
- Search Trees
- State-Space Search
- BFS
- DFS
- Uniform Cost Search
- Greedy Search
- A* Search
- Optimization Techniques

---

## Project Architecture

```text
District Networks
        │
        ▼
 State Representation
        │
        ▼
 Search Tree Generation
        │
        ▼
 Search Algorithms
(BFS / DFS / UCS / Greedy / A*)
        │
        ▼
 Schedule Evaluation
        │
        ▼
 AUC Maximization
        │
        ▼
 Optimal Recovery Plan
```

## Results

The project demonstrates the strengths and weaknesses of classical search algorithms for large-scale scheduling problems.

### Findings

- DFS quickly finds complete plans but often poor ones.
- BFS becomes infeasible because of state-space explosion.
- UCS guarantees optimality but explores too many states.
- Greedy search is fast but shortsighted.
- A* provides the best balance between solution quality and computational efficiency.

A* was selected as the preferred strategy for infrastructure restoration planning.

---

## Skills Demonstrated

- Artificial Intelligence
- Search Algorithms
- Heuristic Design
- Optimization
- Scheduling Systems
- Graph Modeling
- Decision Support Systems
- Resource Allocation
- Operations Research

---

## Future Improvements

- Reinforcement Learning-based planning
- Multi-day recovery scheduling
- Dynamic crew allocation
- Stochastic repair durations
- Real-time disaster response simulation
- GIS integration and visualization

---

## Team

- Sarah Assaad
- Fady Abi Rached
- Mirella Sarkis

Faculty of ESIB – Saint Joseph University of Beirut

---

## Author

**Sarah Assaad**

Master's Student in Data Science & Artificial Intelligence

Université Saint-Joseph (USJ) & Université Paris-Saclay
