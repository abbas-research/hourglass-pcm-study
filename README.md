# Hourglass PCM Study for Thermal Management of a PCM-Cooled 18650 Lithium-Ion Battery

## Overview

This repository presents a Computational Fluid Dynamics (CFD) investigation of an Hourglass Phase Change Material (PCM) geometry for passive thermal management of a cylindrical 18650 lithium-ion battery.

The study extends a previously validated ANSYS Fluent model based on the work of Nicholls (2024). Unlike the baseline configuration, which employed a uniform PCM jacket, the present study redistributes the PCM into an Hourglass geometry while maintaining approximately constant PCM volume.

The objective is to evaluate how PCM redistribution influences battery thermal behaviour under uniform volumetric heat generation conditions.

---

## Research Objective

Investigate the thermal performance of a volume-matched Hourglass PCM geometry surrounding a cylindrical 18650 lithium-ion battery.

The study evaluates how redistributing PCM toward the battery ends influences thermal behaviour while maintaining approximately constant PCM volume.

---

## Geometry

### Hourglass PCM Geometry

![Hourglass Geometry](Geometry/Iso%20View.png)

### Battery Geometry

| Parameter    | Value                              |
| ------------ | ---------------------------------- |
| Battery Type | Cylindrical 18650 Lithium-Ion Cell |
| Diameter     | 18 mm                              |
| Length       | 65 mm                              |

### Hourglass PCM Profile

| Axial Position (mm) | Outer Diameter (mm) |
| ------------------: | ------------------: |
|                   0 |                25.7 |
|                  15 |                20.6 |
|                  50 |                20.6 |
|                  65 |                25.7 |

### PCM Volume

| Parameter  |       Value |
| ---------- | ----------: |
| PCM Volume | 5,991.5 mm³ |

The Hourglass geometry was developed by redistributing PCM away from the battery mid-plane and increasing PCM volume near the battery ends while maintaining approximately constant PCM volume.

---

## Computational Domain

The model consists of:

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

## Mesh

### Computational Mesh

![Mesh](Mesh/Iso%20View.png)

### Mesh Statistics

| Metric                     |   Value |
| -------------------------- | ------: |
| Nodes                      |  36,999 |
| Elements                   | 202,904 |
| Minimum Orthogonal Quality | 0.00963 |
| Average Orthogonal Quality |  0.7636 |
| Maximum Orthogonal Quality | 0.99426 |

Mesh generation was performed using a tetrahedral patch-conforming mesh with a body sizing of 0.001 m.

---

## ANSYS Fluent Setup

### Solver Configuration

| Parameter                      | Setting        |
| ------------------------------ | -------------- |
| Solver Type                    | Pressure-Based |
| Simulation Type                | Transient      |
| Flow Model                     | Laminar        |
| Energy Equation                | Enabled        |
| Solidification & Melting Model | Enabled        |

### Thermal Boundary Conditions

| Parameter                  |       Value |
| -------------------------- | ----------: |
| Volumetric Heat Generation | 65,000 W/m³ |
| Ambient Temperature        |    298.15 K |
| Convection Coefficient     |     7 W/m²K |

### Time Integration

| Parameter                |  Value |
| ------------------------ | -----: |
| Time Step Size           |    1 s |
| Simulation Duration      | 1000 s |
| Iterations per Time Step |     20 |

---

## Temperature Distribution

### Final Temperature Contour (1000 s)

![Temperature Contour](Results/Temp%20iso%20Contour.png)

Temperature contours indicate that the highest temperatures occur near the battery mid-plane, while lower temperatures are observed near the battery ends.

---

## Results

### Hourglass PCM Thermal Performance

| Metric                      |     Value |
| --------------------------- | --------: |
| Average Battery Temperature | 304.164 K |
| Maximum Battery Temperature | 304.508 K |

### Comparison with Baseline Validation Case

The baseline validation model reproduced the uniform PCM jacket case reported by Nicholls (2024).

| Case                        | Average Temperature (K) | Maximum Temperature (K) |
| --------------------------- | ----------------------: | ----------------------: |
| Baseline Uniform PCM Jacket |                 302.134 |                 302.169 |
| Hourglass PCM Geometry      |                 304.164 |                 304.508 |

### Difference Relative to Baseline

| Metric                       | Difference |
| ---------------------------- | ---------: |
| Average Temperature Increase |   +2.030 K |
| Maximum Temperature Increase |   +2.339 K |

---

## Discussion

The objective of the study was to evaluate whether redistributing PCM while maintaining approximately constant PCM volume could improve battery thermal performance.

Results indicate that the Hourglass PCM geometry produced higher battery temperatures than the baseline uniform PCM configuration.

Temperature contours show that the battery mid-plane remains the dominant thermal hotspot throughout the transient simulation. Consequently, reducing PCM thickness near the centre of the battery decreased the effectiveness of heat absorption and thermal buffering.

The results suggest that, under uniform volumetric heat generation, relocating PCM away from the battery mid-plane is detrimental to thermal performance.

---

## Key Findings

* Hourglass PCM geometry reached an average battery temperature of 304.164 K.
* Hourglass PCM geometry reached a maximum battery temperature of 304.508 K.
* Average battery temperature increased by approximately 2.03 K relative to the baseline uniform PCM jacket.
* Maximum battery temperature increased by approximately 2.34 K relative to the baseline uniform PCM jacket.
* The battery mid-plane remained the dominant thermal hotspot throughout the simulation.
* Redistributing PCM toward the battery ends reduced thermal effectiveness under uniform heat generation conditions.

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
├── Workbench Project Files
├── Fluent Case Files
├── Fluent Data Files
└── Mesh Files
```

---

## Future Work

Future investigations may examine:

* Non-uniform battery heat-generation distributions
* Axial thermal gradients
* Battery tab heating effects
* Multi-Scale Multi-Domain (MSMD) battery models
* Electrochemically derived heat-generation profiles
* PCM geometry optimization under realistic battery operating conditions

---

## References

1. Nicholls, R. A. (2024). *Thermal Management of Lithium-Ion Batteries Using Phase Change Materials.*

2. Drake, S. J., et al. (2015). *Heat Generation Measurements for Lithium-Ion Battery Cells.*
