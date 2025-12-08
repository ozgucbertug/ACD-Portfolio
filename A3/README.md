# Assignment 3: Parametric Structural Canopy

![Example Canopy](images/canopy.jpg)

## Objective

In this assignment you will design and generate a **parametric structural canopy** in **Grasshopper** using the **GhPython (Python 3)** component. You will combine: (1) a **NumPy-driven heightmap** that modulates a NURBS surface, (2) **tessellation** of the resulting surface, and (3) **recursive, branching vertical supports** with controlled randomness. Your goal is to produce a small **family of design solutions** by varying parameters and algorithms, then communicate your process and results in a clear, reproducible report. You are asked to present **three** visually distinct designs. Each design must vary at least **two** of the implemented computational logic (heightmap-based surface geometry, tessellation strategy, branching supports).

---

## Repository Structure

```
Assignment3/
├── README.md               # Final writeup (your write-up + images)
├── TEMPLATE.md             # Minimal writeup structure for the report
├── BRIEF.md                # Assignment handout (this file)
├── parametric_canopy.py    # GhPython script
├── parametric_canopy.gh    # Grasshopper definition
└── images/
    └── (Output images)
```

---