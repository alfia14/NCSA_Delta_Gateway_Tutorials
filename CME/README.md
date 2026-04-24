# Coupled Genetic Information Processes and Metabolism in Minimal Cell, JCVI-syn3A

> **Setup:** see the top-level [README](../README.md) for how to log into the QCB Delta Gateway, open JupyterHub, select the **`LM 2.5`** kernel, and clone this repository. This file covers only the **science** of the CME tutorial.

## Description

<img align="right" width="300" src="./figs/figs_WCM/syn3A_wcomplex.png">

In ***Coupled Genetic Information Processes and Metabolism in the Minimal Cell*** tutorial, you will first learn the basics of stochastic kinetic simulation using a [bimolecular reaction](bimolecule/), followed by a model of [genetic information processing](GIP/) solved using chemical master equations (**CMEs**). The essential metabolism[^breuer_metabolism] in Syn3A imports nutrients from the growth medium and further converts them to generate ATP molecules, which energize cellular processes, and monomers for the synthesis of proteins, RNAs, and the chromosome. To simulate the [co-evolution of GIP and metabolism in Syn3A](WCM/), we employ a hybrid stochastic-deterministic algorithm[^bianchi_CMEODE], where stepwise communication describes the interactions between these two subsystems.

*This tutorial was prepared for the NSF Science and Technology Center for Quantitative Cell Biology Summer School organized in July.*

## Outline

1. Introduction to Lattice Microbes, a GPU-accelerated stochastic simulation platform
2. Tutorial: bimolecular reaction solved stochastically in CME
3. Tutorial: stochastic genetic information processes in CME
4. Tutorial: CME-ODE whole-cell model of a genetically minimal cell, JCVI-syn3A

---

## 1. Introduction to Lattice Microbes and Stochastic Simulation

**Go to [Introduction](introduction/)**

## 2. Tutorial: Bimolecular Reaction Solved in ODE and CME

**Go to [bimolecule](bimolecule/)**

## 3. Tutorial: Genetic Information Processes in CME

**Go to [Genetic Information Processes](GIP/)**

## 4. Tutorial: CME-ODE Whole-Cell Model of a Genetically Minimal Cell, JCVI-Syn3A

**Go to [CME-ODE WCM of Syn3A](WCM/)**

---

## References

[^breuer_metabolism]: Breuer, M., Earnest, T. M., Merryman, C., Wise, K. S., Sun, L., Lynott, M. R., Hutchison, C. A., Smith, H. O., Lapek, J. D., Gonzalez, D. J., De Crécy-Lagard, V., Haas, D., Hanson, A. D., Labhsetwar, P., Glass, J. I., & Luthey-Schulten, Z. (2019). Essential metabolism for a minimal cell. *eLife*, 8. https://doi.org/10.7554/elife.36842

[^bianchi_CMEODE]: Bianchi, D. M., Peterson, J. R., Earnest, T. M., Hallock, M. J., & Luthey‐Schulten, Z. (2018). Hybrid CME–ODE method for efficient simulation of the galactose switch in yeast. *IET Systems Biology*, 12(4), 170–176. https://doi.org/10.1049/iet-syb.2017.0070
