# Assignment 4: Agent-Based Modeling for Surface Panelization

## Table of Contents

- [Project Overview](#project-overview)
- [Pseudo-Code](#pseudo-code)
- [Technical Explanation](#technical-explanation)
- [Design Variations](#design-variations)
- [Challenges and Solutions](#challenges-and-solutions)
- [AI Acknowledgments](#ai-acknowledgments)
- [References](#references)

---

## Project Overview

*(Briefly summarize your project in 1–2 paragraphs.)*

- What surface did you start from (e.g., your Assignment 3 heightmap-based surface)?
- Which **geometric signals** did you use (curvature, slope, vector/force fields, scalar fields, distance/spatial influences)?
- How do your agents explicitly respond to **at least two** geometric signal categories (e.g., curvature + slope, scalar field + spatial influences)? Briefly describe how these signals affect movement, life-cycle rules (if any), and the resulting panelization.
- What is the overall **panelization / tessellation strategy**?
- What kinds of patterns or structural logics do your agents generate?

---

## Pseudo-Code

*(Provide detailed pseudo-code explaining the logic of your program. Outline your modules, classes, methods, and how data flows between them. This should be specific enough that someone else could re-implement your system from it.)*

### 1. Module-Level Structure

You must submit at least three Python modules:

- `surface_generator.py` — base surface generation using a NumPy heightmap (or comparable scalar field).
- `agent_builder.py` — agent class definitions and agent initialization.
- `agent_simulator.py` — simulation loop, update logic, state evolution.

*(Optionally describe any additional modules, such as `field_generator.py`, `panelization.py`, `visualization_utils.py`.)*

Example outline:

```text
surface_generator.py
  - build_heightmap(W, H, params) -> np.ndarray
  - build_surface_from_heightmap(H_array, params) -> surface_id

field_generator.py (optional)
  - compute_curvature_field(surface_id, W, H) -> curvature_field (H x W)
  - compute_slope_field(surface_id or heightmap) -> slope_field (H x W)
  - compute_vector_field(W, H, params) -> force_field (H x W x 2)

agent_builder.py
  - class Agent:
      attributes: uv, velocity_uv, state, lifetime, history, etc.
      methods: sense_fields(...), move(...), update_state(...), spawn_children(...)
  - build_agents(surface_id, n_agents, init_params) -> list[Agent]

agent_simulator.py
  - simulate(surface_id, agents, fields, sim_params) -> (agent_histories, panel_geometry)
    loop t in [0..T):
      for each agent:
        agent.sense_fields(curvature_field, slope_field, force_field, distance_queries, ...)
        agent.move(dt)
        agent.update_state()
        (optionally) spawn/kill/respawn agents based on rules
      record positions / geometry seeds
    post-process agent histories into panelization geometry
```

### 2. Main Simulation Loop

Describe your main loop in clear pseudo-code, including:

- Initialization (surface, fields, agents, parameters).
- Per-step updates (sensing, decision-making, movement, life-cycle changes).
- How and when you record data for panelization (e.g., sample positions, trajectories, impact on tessellation).

### 3. Agent Class / Classes

Describe:

- **Attributes**:
  - Position in UV (and/or 3D), velocity, state variables, age/lifetime, IDs, etc.
- **Methods**:
  - `sense_fields(...)`: how signals are sampled.
  - `decide(...)`: how rules are applied (e.g., thresholds, weighted combinations of signals).
  - `move(...)`: how position changes based on signals/velocity.
  - `spawn_children(...)` or `die(...)`: optional life-cycle rules.
  - `record_history(...)`: how trajectories are stored.

### 4. Panelization / Geometry Generation

Explain, at a pseudo-code level, how you convert simulation data into geometry:

- How do you choose which agent positions/trajectories become panel boundaries, mesh vertices, or ribs?
- How do you construct panels (e.g., quad mesh, tri mesh, hybrid, strips)?
- How do geometric signals influence panel **density**, **orientation**, or **topology**?

---

## Technical Explanation

*(Explain in prose how your system works and the design rationale behind it.)*

You may use the following structure:

### 1. Overall Pipeline

- Describe the full pipeline from:
  1. Surface generation (`surface_generator.py`),
  2. Field / signal computation (e.g., curvature, slope, force/scalar fields),
  3. Agent initialization (`agent_builder.py`),
  4. Simulation (`agent_simulator.py`),
  5. Panelization / geometry output.

### 2. Surface Generation and Fields

- How did you generate or reuse your surface (e.g., from Assignment 3 heightmap)?
- Which fields did you compute (curvature, slope, vector fields, scalar fields)?
- How are fields represented (e.g., curvature field as `(H, W)` array, force field as `(H, W, 2)` in UV space)?
- How do you map agent UV coordinates `(u, v)` to field indices `(i, j)`?

### 3. Geometric Signals and Agent Behaviors

For each signal you use (at least two):

- **Curvature**: How do agents respond to curvature (e.g., slow down, branch more, seek/avoid high curvature)?
- **Slope**: Do agents follow steepest descent, avoid steep regions, or target them?
- **Force / Vector Fields**: How do you define and use vector fields in UV? How do they blend with curvature/slope directions?
- **Scalar Fields**: How do scalar values (e.g., height, density, probability) affect branching, speed, or state?
- **Distance / Spatial Influences**: How do attractors, repulsors, or obstacles (points/curves/surfaces) influence agent decisions?

Explain how you **combine** signals (e.g., weighted sums, thresholds, conditional rules).

### 4. Agent Life-Cycle and Interactions

- What are the rules for spawning, killing, and/or respawning agents?
- How do agents interact with each other (e.g., separation, alignment, cohesion, collision avoidance)?
- How do these interactions contribute to the final panelization pattern?

### 5. Simulation and Panelization Strategy

- How many steps do you simulate, and what are your stopping criteria?
- How do you transform simulation results (paths, states, densities) into:
  - Panel boundaries
  - Meshes or strip systems
  - Structural ribs or seams
- How does your strategy **rationalize** the surface (e.g., smaller panels in high-curvature zones, alignment with flow directions)?

### 6. Multi-Module Design

- Justify how and why you split the project into multiple modules.
- Explain any additional modules (e.g., `field_generator.py`, `panelization.py`) and their responsibilities.

---

## Design Variations

*(Include images and descriptions of your generated design variations.)*

You are expected to produce at least **three** visually distinct configurations. For each variation, clearly indicate:

- Which signals are active and how they are weighted.
- Key parameters (e.g., step size, thresholds, branching depth, number of agents).
- How the resulting panelization differs (density, orientation, topology, regularity, etc.).

### Parameter and Signal Table (Example)

```markdown
| Design | Signals Used                     | Key Parameters                                           | Notes                                 |
|--------|----------------------------------|----------------------------------------------------------|----------------------------------------|
| A      | curvature + slope                | n_agents=200, step=0.01, curv_w=0.7, slope_w=0.3        | Dense panels in high-curvature zones  |
| B      | curvature + force field          | n_agents=100, force_w=0.6, curv_thresh=0.02             | Panels aligned to synthetic flow      |
| C      | scalar field + distance to curve | n_agents=150, spawn_thresh=0.5, attractor_radius=5.0    | Clustering near attractor geometry    |
```

### Variation 1: [Name/Description]

![Variation 1](images/variation1.jpg)

- **Signals Used**: e.g., curvature + slope
- **Parameters Changed**: list the main parameters and their values.
- **Description**: explain how these settings influence agent behaviors and the resulting panelization.

### Variation 2: [Name/Description]

![Variation 2](images/variation2.jpg)

- **Signals Used**: e.g., curvature + force field
- **Parameters Changed**: …
- **Description**: …

### Variation 3: [Name/Description]

![Variation 3](images/variation3.jpg)

- **Signals Used**: e.g., scalar field + distance
- **Parameters Changed**: …
- **Description**: …

*(Add more variations if needed.)*

Also include at least **one** image or diagram that explicitly visualizes **agent trajectories and/or fields** (e.g., curvature heatmap, flow lines, vector field arrows).

---

## Challenges and Solutions

*(Discuss any challenges you faced and how you addressed them.)*

Possible topics:

- **Signal computation issues**: numerical stability, resolution of fields, mapping UV → indices.
- **Agent behavior tuning**: agents getting stuck, diverging, or clustering too much.
- **Panelization quality**: distorted panels in high-curvature zones, gaps, overlaps.
- **Performance**: large numbers of agents, many time steps, or high field resolutions.
- **Software integration**: transferring data between Grasshopper, GhPython, and Rhino geometry.

For each challenge, describe:

- What the problem was.
- How you diagnosed it.
- What changes you made (algorithmic, parametric, or structural) to solve or mitigate it.

---

## AI Acknowledgments

*(If you used AI tools at any point, briefly describe how.)*

- List the tools and prompts you used (e.g., ChatGPT for refactoring a function, debugging an error message).
- Clarify what parts of the implementation or documentation they influenced.
- Confirm that algorithmic choices and core implementation remain your own.

If you did **not** use any AI tools, state that explicitly.

---

## References

*(List any resources you used or found helpful.)*

- **Object-Oriented Programming in Python**
  - [Python Official Tutorial – Classes](https://docs.python.org/3/tutorial/classes.html)
  - [Real Python – Object-Oriented Programming](https://realpython.com/python3-object-oriented-programming/)

- **Python in Rhino and Grasshopper**
  - [Rhino.Python Guides](https://developer.rhino3d.com/guides/rhinopython/)
  - [RhinoScriptSyntax Reference](https://developer.rhino3d.com/api/RhinoScriptSyntax/)

- **Agent-Based Modeling and Design**
  - Any ABM references, papers, or tutorials you used (e.g., flocking, swarm intelligence, emergent behavior in architecture).

- **Additional Resources**
  - Any other libraries, articles, or tutorials that informed your approach.

*(Feel free to expand these sections to fully capture your work and learning process.)*