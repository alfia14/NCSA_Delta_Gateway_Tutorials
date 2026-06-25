# 4D Whole Cell (Delta Gateway) — Optimized stack

## Contents

| File | Description |
|------|-------------|
| [Tutorial_4dwcm_gateway.ipynb](Tutorial_4dwcm_gateway.ipynb) | **Start here** — run the optimized 4DWCM on the Gateway |

## What is 4DWCM?

**4D Whole-Cell Model (4DWCM)** simulates the genetically minimal cell **JCVI-syn3A** in **3D space over time**. It couples spatial stochastic chemistry (**RDME**), **CME** and **ODE** metabolism, and **Brownian-dynamics** chromosome modeling (btree_chromo 2.0 + Kokkos LAMMPS on GPU).

This tutorial uses the **optimized production fork** (~3× faster than the paper baseline):

- **Code:** [Optimize_4DWCM_Minimal_Cell](https://github.com/luthey-schulten-chemistry/Optimize_4DWCM_Minimal_Cell)
- **Container:** Gateway GPU Environment **`4DCell Optimized`** (`4dcell_delta_btree2.sif`)
- **GPUs:** 2 (RDME/CME on GPU 0, async DNA on GPU 1 via `DNA_GPU_ID=1`)
- **DNA path:** `-dsd /Software/opt/` (btree_chromo 2.0 + sc_chain_generation)
- **Python:** `PYTHONPATH=/Software/Lattice_Microbes_2.6/src/pylm` (kernel label may still say LM 2.5)

## Steps

1. **Gateway session:** start Jupyter with **4DCell Optimized**, **2 GPUs**, kernel **LM 2.5 (Python 3.7)**.
2. Open **`NCSA_Delta_Gateway_Tutorials/4D Whole Cell/Tutorial_4dwcm_gateway.ipynb`** and run all cells. Section 1 copies the simulation code from `/projects/bgvl/containers/Optimize_4DWCM_Minimal_Cell` into your workspace automatically (~13 MB; no `Data/`).

## Performance

| Run | Wall time (7200 s biological) |
|-----|-------------------------------|
| Unoptimized baseline | ~78 h |
| **Optimized (this tutorial)** | **~25 h** (2× A100) |

## References

- [4D Minimal Cell (site)](https://minimalcell4d.web.illinois.edu/home/)
- [Thornburg *et al.*, *Cell* 2026](https://www.cell.com/cell/fulltext/S0092-8674(26)00174-1)
- [Optimize_4DWCM_Minimal_Cell README](https://github.com/luthey-schulten-chemistry/Optimize_4DWCM_Minimal_Cell)
