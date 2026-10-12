---
title: "ML Potentials for Phonons and Thermal Transport"
summary: "Machine-learning interatomic potentials validated against phonons and heat transport, combined with symmetry-adapted Green–Kubo, modal analysis and atomistic Green's functions for quasi-1D and defect-laden systems."
tags:
- PhD
- Machine Learning
- Thermal Transport
- Green-Kubo
- Symmetry
- Python
date: "2023-07-12"
---

## Overview

Heat conduction at the nanoscale is carried by phonons, and predicting it from first principles is expensive. This project uses machine-learning interatomic potentials to reach the length and time scales transport needs, and symmetry to make the results interpretable.

## Key Contributions

- **Active-learning MLIPs**: Fine-tuned a neuroevolution potential (NEP) for a WS₂–MoS₂ double-walled nanotube in two rounds of active learning on VASP data, validated on phonons and transport rather than only on energy and force errors.
- **Symmetry-resolved modal analysis**: Built the modal basis from line-group projection operators, so each conduction channel carries well-defined symmetry labels in Green–Kubo and nonequilibrium MD modal analysis.
- **Defects and symmetry breaking**: Coupled an Allegro equivariant potential with a symmetry-adapted atomistic Green's-function framework and showed that symmetry-breaking defects make a disordered WS₂–MoS₂ nanotube conduct heat ~60% better, confirmed by Green–Kubo MD.

## Related Publications

- *Ab-initio heat transport in defect-laden quasi-1D systems from a symmetry-adapted perspective* — npj Computational Materials (2026)
- *Symmetry-based modal analysis of heat transport in molecular dynamics of quasi-1D systems* — arXiv:2609.02397 (2026)
- *Accelerating first-principles molecular-dynamics thermal conductivity calculations for complex systems* — J. Chem. Theory Comput. (2025)
