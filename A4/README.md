# Assignment 4: Agent-Based Modeling for Surface Panelization

![Example Structural Panelization](images/structural_tessellation.jpg)

---

## Objective

In this assignment, you will develop an **agent-based system for surface rationalization** using **Object-Oriented Programming (OOP)** in Python. Building on the surface you generated in Assignment 3 (or a comparable heightmap-driven surface), you will design agents that respond to geometric signals and collectively produce **panelization patterns**. The core idea is that agents move, interact, and make decisions based on how they sample the geometry, and their trajectories and interactions become the basis for a rationalized panelization of that surface.

Your implementation must incorporate **at least two types of geometric signals** (chosen from curvature, slope, vector fields, scalar fields, and spatial influences) when defining agent behavior. The primary outputs of this assignment are: (1) a rationalized panelization of your surface and (2) simulated agent trajectories and fields that you document and analyze.

---

## Repository Structure
```
Assignment4/
├── BRIEF.md                # Assignment handout (this file)
├── README.md               # Documentation with pseudo-code and explanations
├── TEMPLATE.md             # Minimal documentation template
├── agent_panelization.gh   # Your grasshopper definition
├── surface_generator.py    # Python script to generate a complex surface using a numpy array generated with a continuous function
├── agent_builder.py        # Python script used in defining and initializing agents
├── agent_simulator.py      # Python script used in simulating agent behaviors
├── (additional scripts)    # Any additional modules for field generation, panelization, analysis, or visualization
├── images/
│   └── (Output Images)
```

---