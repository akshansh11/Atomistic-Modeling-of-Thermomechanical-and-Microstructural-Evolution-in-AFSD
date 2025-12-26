# Atomistic Modeling of Thermomechanical and Microstructural Evolution in Additive Friction Stir Deposition

![AFSD Paper](afsd%20paper.png)

## Overview

This repository contains a LAMMPS molecular dynamics simulation for **Additive Friction Stir Deposition (AFSD)**, a solid-state additive manufacturing process. The simulation provides atomistic-scale insights into the thermomechanical and microstructural evolution during AFSD, including frictional heating, material flow, phase transformation, and layer deposition.

## Publication

This simulation is based on research published in the following paper:

**[Preprint Available Here](https://www.preprints.org/manuscript/202512.2302?utm_source=researchgate.net&utm_medium=article)**

Please cite this work if you use or reference this simulation in your research.

## Features

- **High-resolution molecular dynamics** simulation of AFSD process
- **Multi-stage process modeling**:
  - Equilibration
  - Tool engagement
  - Active deposition
  - Steady-state deposition
  - Cooldown
- **Advanced material tracking**:
  - Oxide layer identification
  - Core tracer particles
  - Interface monitoring
- **Comprehensive output**:
  - Temperature profiles
  - Stress distributions
  - Coordination analysis
  - Centro-symmetry parameters
  - Voronoi volume analysis

## Simulation Details

### System Configuration

- **Material**: Aluminum (Al) using EAM/alloy potential
- **Lattice**: FCC with 4.05 Å lattice parameter
- **Domain**: 100 × 100 × 120 units³
- **Components**:
  - Fixed substrate base (z = 0-3)
  - Mobile substrate (z = 3-25)
  - Rotating/translating feedstock cylinder (radius = 7.0 Å)

### Process Parameters

- **Rotation speed**: 300 RPM (ω = 31.4 rad/s)
- **Traverse speed**: 0.00212 Å/fs
- **Feed rate**: -0.00212 Å/fs (vertical)
- **Temperature range**: 300-1000 K
- **Timestep**: 0.001 ps

### Key Physics

1. **Thermal management**:
   - NVT thermostat for substrate and feedstock
   - Frictional heating in contact zone
   - Heat dissipation at boundaries

2. **Mechanical interactions**:
   - Rotation-induced centrifugal forces
   - Linear translation and feeding
   - Fixed bottom boundary condition

3. **Material conversion**:
   - Dynamic tracking of depositing material
   - Conversion from feedstock (type 2) to deposited (type 3)

## Requirements

- **LAMMPS** (Large-scale Atomic/Molecular Massively Parallel Simulator)
- **EAM potential file**: `Al99.eam.alloy` (not included - obtain from LAMMPS potential library)
- Sufficient computational resources (recommended: multi-core CPU or GPU-accelerated LAMMPS)

## Usage

### Running the Simulation

```bash
lmp -in afsd_simulation.lammps
```

Or with MPI for parallel execution:

```bash
mpirun -np 4 lmp -in afsd_simulation.lammps
```

### Output Files

The simulation generates several output files:

- `dump.afsd.*` - Complete atomic trajectories
- `oxide.lammpstrj.*` - Oxide layer tracking
- `tracers.lammpstrj.*` - Core tracer particles
- `interface.lammpstrj.*` - Interface region analysis
- `temp_profile.dat` - Spatial temperature distribution
- `coordination.dat` - Average coordination number
- `stress.dat` - Stress tensor components
- `energy.dat` - Total energy evolution
- `displacement.dat` - Average atomic displacement
- `restart.afsd.a/b` - Restart files
- `final_state.data` - Final configuration

### Visualization

Output dump files can be visualized using:
- **OVITO** (recommended)
- **VMD** (Visual Molecular Dynamics)
- **AtomEye**
- **ParaView** (with LAMMPS reader)

## Simulation Stages

1. **Equilibration** (5,000 steps): System initialization at 300 K
2. **Tool Engagement** (10,000 steps): Feedstock heating and contact
3. **Active Deposition** (150,000 steps): Primary material deposition
4. **Steady State** (100,000 steps): Continuous deposition process
5. **Cooldown** (50,000 steps): System relaxation to room temperature

**Total simulation time**: ~315 ps

## Analysis Tools

The script includes several compute commands for real-time analysis:

- `centro` - Centro-symmetry parameter (defect detection)
- `cna` - Common Neighbor Analysis (phase identification)
- `coord` - Coordination number (bonding environment)
- `voronoi` - Voronoi volume (local density)
- `stress/atom` - Atomic stress tensor
- `pe/atom` and `ke/atom` - Energy decomposition

## Customization

Key parameters that can be adjusted:

- Rotation speed: Modify `variable omega`
- Traverse/feed rates: Modify `v_traverse` and `v_feed`
- Temperature targets: Adjust NVT fix temperatures
- Deposition threshold: Change `deposit_threshold` variable
- Output frequency: Modify `dump` and `fix ave/time` intervals

## Known Limitations

- Simplified representation of oxide layer (geometric definition)
- Classical MD limitations (no electronic effects)
- Single material system (pure aluminum)
- Idealized boundary conditions

## Author

**Akshansh Mishra**

GitHub: [@akshansh11](https://github.com/akshansh11)

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">
  <img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
</a>

This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

### License Terms

- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material
- **NonCommercial** — You may not use the material for commercial purposes
- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page on the GitHub repository.

## Acknowledgments

- LAMMPS development team
- NIST Interatomic Potentials Repository
- Open-source computational materials science community

## Citation

If you use this simulation in your research, please cite:

```bibtex
@article{mishra2025afsd,
  title={Atomistic Modeling of Thermomechanical and Microstructural Evolution in Additive Friction Stir Deposition},
  author={Mishra, Akshansh},
  journal={Preprints.org},
  year={2025},
  url={https://www.preprints.org/manuscript/202512.2302}
}
```

---

**Last Updated**: December 2025

For questions or collaboration opportunities, please open an issue or contact via GitHub.
