# 4D Whole Cell (Delta Gateway)


## Contents

| File | Description |
|------|-------------|
| [Tutorial_4dwcm_gateway.ipynb](Tutorial_4dwcm_gateway.ipynb) | **Start here** — NCSA Delta notebook: paths, LM environment, logs, `nohup` / `tail`, process checks, and running the 4D whole-cell driver. |

## What is 4DWCM?

**4D Whole-Cell Model (4DWCM)** simulates the genetically minimal cell **JCVI-syn3A** in **3D space over time** (“4D” = **space + time**). It **couples** spatial stochastic chemistry (**RDME** via Lattice Microbes), **CME** and **ODE** components, and **Brownian-dynamics** chromosome modeling (e.g. LAMMPS/Kokkos on GPU) into one spatiotemporal model.

The **simulation code** is not stored in this repo. Clone and run it from [Luthey-Schulten-Lab/Minimal_Cell_4DWCM](https://github.com/Luthey-Schulten-Lab/Minimal_Cell_4DWCM). The notebook uses a typical **gateway** layout (e.g. model under `/home/user/workspace/Minimal_Cell_4DWCM`).

## References

- [4D Minimal Cell (site)](https://minimalcell4d.web.illinois.edu/home/)  
- [Thornburg *et al.*, *Cell* 2026](https://www.cell.com/cell/fulltext/S0092-8674(26)00174-1)  
