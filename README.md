# Hourglass PCM Study for Thermal Management of a PCM-Cooled 18650 Lithium-Ion Battery

## Overview

This repository presents a computational fluid dynamics (CFD) investigation of an Hourglass Phase Change Material (PCM) geometry for passive thermal management of a cylindrical 18650 lithium-ion battery.

The work extends a previously validated ANSYS Fluent model based on the thermal management study presented by Nicholls (2024). The baseline model employed a uniform N-octadecane PCM jacket surrounding an 18650 cell. In the present study, the PCM volume was redistributed into an Hourglass configuration while maintaining approximately constant PCM volume.

The objective was to determine whether PCM redistribution could improve battery thermal performance relative to a conventional uniform PCM jacket.

---

## Research Objective

For a fixed PCM volume, determine the effect of an Hourglass PCM distribution on battery thermal performance and compare the results with:

* Baseline Uniform PCM Jacket (G1)
* Belly PCM Geometry (G2)
* Hourglass PCM Geometry (G3)

---

## Baseline Validation Case

The baseline model was reproduced from the validation case reported by Nicholls (2024).

### Battery Geometry

| Parameter      | Value                                 |
| -------------- | ------------------------------------- |
| Cell Type      | Cylindrical 18650 Lithium-Ion Battery |
| Diameter       | 18 mm                                 |
| Length         | 65 mm                                 |
| Battery Volume | 16,540 mm³                            |

### PCM Geometry

| Parameter     | Value              |
| ------------- | ------------------ |
| PCM Material  | N-octadecane       |
| Configuration | Uniform PCM Jacket |
| PCM Volume    | 5,973 mm³          |

### Validated Thermal Results

| Case                        | Average Temperature (K) | Maximum Temperature (K) |
| --------------------------- | ----------------------: | ----------------------: |
| Baseline Uniform PCM Jacket |                 302.134 |                 302.169 |

---

## Hourglass PCM Geometry (G3)

The Hourglass PCM configuration was developed as an inverse redistribution of the previously investigated Belly PCM geometry.

PCM volume was concentrated near the battery ends while reducing PCM thickness near the battery mid-plane.

### Battery Dimensions

| Parameter | Value |
| --------- | ----- |
| Diameter  | 18 mm |
| Length    | 65 mm |

### Hourglass PCM Profile

| Axial Position (mm) | Outer Diameter (mm) |
| ------------------: | ------------------: |
|                   0 |                25.7 |
|                  15 |                20.6 |
|                  50 |                20.6 |
|                  65 |                25.7 |

### PCM Volume

| Parameter            |       Value |
| -------------------- | ----------: |
| Hourglass PCM Volume | 5,991.5 mm³ |

The PCM volume differs from the baseline configuration by less than 0.4%, ensuring that performance differences are primarily caused by PCM distribution rather than PCM quantity.

---

## Computational Domain

The model consisted of:

* One battery body (solid)
* One PCM body (fluid)

Geometry structure:

```text
1 Part
2 Bodies

Battery = Solid
PCM = Fluid
```

---

## Mesh Generation

### Mesh Type

* Tetrahedral
* Patch Conforming

### Mesh Statistics

| Metric                     |   Value |
| -------------------------- | ------: |
| Nodes                      |  36,999 |
| Elements                   | 202,904 |
| Minimum Orthogonal Quality | 0.00963 |
| Average Orthogonal Quality |  0.7636 |
| Maximum Orthogonal Quality | 0.99426 |

The solution remained numerically stable throughout the transient simulation despite the low minimum orthogonal quality.

---

## ANSYS Fluent Setup

### Solver Configuration

| Parameter                | Setting        |
| ------------------------ | -------------- |
| Solver                   | Pressure-Based |
| Time Formulation         | Transient      |
| Flow Model               | Laminar        |
| Energy Equation          | Enabled        |
| Solidification & Melting | Enabled        |

### Thermal Boundary Conditions

| Parameter              |       Value |
| ---------------------- | ----------: |
| Heat Generation        | 65,000 W/m³ |
| Ambient Temperature    |    298.15 K |
| Convection Coefficient |     7 W/m²K |

### Time Integration

| Parameter                |  Value |
| ------------------------ | -----: |
| Time Step Size           |    1 s |
| Total Simulation Time    | 1000 s |
| Iterations per Time Step |     20 |

---

## Results

### Hourglass PCM Thermal Performance

| Case               | Average Temperature (K) | Maximum Temperature (K) |
| ------------------ | ----------------------: | ----------------------: |
| Hourglass PCM (G3) |                 304.164 |                 304.508 |

### Comparison with Baseline Uniform PCM

| Metric                       | Difference |
| ---------------------------- | ---------: |
| Average Temperature Increase |   +2.030 K |
| Maximum Temperature Increase |   +2.339 K |

---

## Comparison with Other PCM Distributions

| Geometry                    | Average Temperature (K) | Maximum Temperature (K) |
| --------------------------- | ----------------------: | ----------------------: |
| Uniform PCM Jacket (G1)     |                 302.134 |                 302.169 |
| Belly PCM Geometry (G2)     |                 304.242 |                 304.585 |
| Hourglass PCM Geometry (G3) |                 304.164 |                 304.508 |

### Relative Performance Ranking

| Rank | Geometry                  |
| ---- | ------------------------- |
| 1    | Uniform PCM Jacket (Best) |
| 2    | Hourglass PCM Geometry    |
| 3    | Belly PCM Geometry        |

---

## Temperature Evolution

Battery temperature increased smoothly throughout the transient simulation.

Analysis of the temperature-monitor history showed accelerated heating after approximately 600–700 seconds, indicating a reduction in PCM thermal buffering effectiveness as melting progressed.

The final average battery temperature reached:

```text
304.164 K
```

after 1000 seconds of simulation time.

---

## Discussion

The primary objective of the study was to determine whether redistributing PCM while maintaining constant PCM volume could improve thermal performance.

Results demonstrated that:

* Uniform PCM distribution produced the lowest battery temperatures.
* Redistributing PCM away from a uniform jacket increased battery temperature.
* The Hourglass configuration performed slightly better than the Belly configuration.
* The difference between Hourglass and Belly geometries was small (~0.08 K).

Temperature contours revealed that the battery mid-plane remained the dominant thermal hotspot throughout the simulation. Consequently, reducing PCM thickness near the center of the cell decreased thermal effectiveness despite increasing PCM volume near the battery ends.

These findings indicate that under uniform volumetric heat generation, a uniformly distributed PCM jacket provides superior thermal management compared with the investigated non-uniform PCM distributions.

---

## Key Findings

1. Uniform PCM distribution achieved the best thermal performance.
2. Hourglass PCM increased average battery temperature by approximately 2.03 K relative to the baseline.
3. Hourglass PCM increased maximum battery temperature by approximately 2.34 K relative to the baseline.
4. Hourglass PCM performed marginally better than Belly PCM.
5. PCM redistribution away from the battery mid-plane reduced thermal effectiveness under uniform heat generation conditions.

---

## Repository Contents

```text
Geometry/
├── Iso View.png
├── Side View.png
└── Top View.png

Mesh/
├── Iso View.png
└── Side View.png

Results/
├── battery_avg_temp.out
├── battery_max_temp.out
├── Temp iso Contour.png
├── temp side contour.png
└── Final results.txt

Python/
└── comparison plot.py

Report/
└── Summary.txt

Ansys Files/
├── Workbench Project
├── Fluent Case Files
├── Fluent Data Files
└── Mesh Files
```

---

## Future Work

The present study assumes uniform volumetric heat generation throughout the battery volume.

Future investigations may explore:

* Non-uniform heat-generation distributions
* Axial thermal gradients
* Tab-region heating effects
* Multi-Scale Multi-Domain (MSMD) battery models
* Electrochemically derived heat-generation profiles
* Geometry optimization under realistic battery loading conditions

---

## References

1. Nicholls, R. A. (2024). *Thermal Management of Lithium-Ion Batteries Using Phase Change Materials.*

2. Drake, S. J., et al. (2015). *Heat Generation Measurements for Lithium-Ion Battery Cells.*
