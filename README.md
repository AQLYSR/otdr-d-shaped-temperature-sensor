# OTDR-Based Temperature Sensor Employing a D-Shaped Fiber

Bachelor of Science (Hons) in Physics final year project, Universiti Sains Malaysia (USM), 2026.

**Author:** Muhammad Aqil Bin Mohd Yusri
**Supervisor:** Dr. Afiq Arif Aminuddin Jafry
**Project partner:** Muhammad Ariff Bin Roshidi

---

## Summary

This project develops a point temperature sensor that pairs a side-polished **D-shaped single-mode fiber (SMF-28)** with a commercial **Optical Time-Domain Reflectometer (OTDR)** operating at 1550 nm. Temperature changes in the surrounding water alter its refractive index, which changes the Fresnel reflection peak at the cleaved fiber end as seen on the OTDR trace. The peak height is the measurand.

OTDR-based temperature sensing normally suffers from weak sensitivity, because standard silica fiber is almost inert to heat. Exposing the evanescent field through a D-shaped geometry is proposed as a simple structural fix. To our knowledge, this exact configuration (D-shaped fiber + OTDR for temperature) had not been reported before.

## Objectives

1. Fabricate and characterize D-shaped fibers with several polishing depths using side-polishing.
2. Evaluate their temperature sensitivity and linearity with an OTDR as the interrogator.

## Method

| Item | Detail |
|---|---|
| Fiber | SMF-28, side-polished with a Dremel 200 and 4 mm diamond-grit bit |
| Polishing depth control | Real-time insertion loss monitoring (VFL source + optical power meter) |
| Probes | Bare (control), 2 dB, 4 dB, 6 dB, 7 dB, 8 dB |
| OTDR | VIAVI SmartOTDR, 1550 nm, 5 km range, 10 s acquisition, 32 cm sampling |
| Pulse widths | 5 ns and 10 ns |
| Launch fiber | 2 km SMF spool to clear the OTDR dead zone |
| Medium | Deionized water on a ceramic hotplate |
| Reference | Thermocouple + multimeter |
| Range | 40 to 80 °C in 5 °C steps, 2 min stabilization per step |
| Analysis | Ordinary least squares fit of peak loss vs. temperature (sensitivity and R²) |

## Key Results

**Sensitivity and linearity at 5 ns pulse width**

| Probe | Sensitivity (dB/°C) | Linearity (R²) |
|---|---|---|
| Bare fiber | 0.0006 | 0.8259 |
| 2 dB | 0.0005 | 0.6394 |
| 4 dB | 0.0003 | 0.8637 |
| 6 dB | 0.0012 | 0.8843 |
| **7 dB** | **0.0008** | **0.9552** |
| 8 dB | 0.0013 | 0.4422 |

- **7 dB is the optimal probe:** best linearity with moderate sensitivity.
- **8 dB is likely over-polished:** highest slope but poor linearity, which is consistent with the core being exposed.
- **5 ns pulse width is required.** At 10 ns the response flattens to about 0.0000 to 0.0003 dB/°C, since the pulse spans roughly 1 m and averages out the millimeter-scale sensing zone.
- **Stability at 60 °C over 20 min (10 traces):** standard deviation 0.00097 dB (bare) and 0.00236 dB (7 dB D-shaped), with a slow drift of 0.0008 dB/trial for the 7 dB probe.

**Mechanism:** the signal is dominated by Fresnel reflection at the glass-water interface. Water has a negative thermo-optic coefficient (about -1×10⁻⁴ /K), so heating lowers its refractive index, raises the index contrast with silica, and increases the reflected peak. The D-shaped region makes the end-face reflection respond to the water temperature, which the bare fiber barely does.

## Limitations and Future Work

- Single-point sensing only; no quasi-distributed or distributed configuration.
- Sensitivity is modest (<0.002 dB/°C) because no thermally responsive coating is used.
- No unified model yet links evanescent-field exposure to Fresnel reflection amplitude.

Recommended next steps: coat the polished surface (ZnO, MoS₂, PDMS), cascade several probes along one fiber for multi-point sensing, and develop a boundary-value electromagnetic model.

## Repository Structure

```
.
├── README.md
├── thesis/
│   └── thesis.pdf
├── data/
│   ├── raw/          # OTDR trace exports (e.g. .sor/.csv) per probe, pulse width, temperature
│   └── processed/    # peak loss vs. temperature tables, stability trial data
├── analysis/         # scripts/notebooks for OLS fits, plots, stability statistics
├── figures/          # exported figures used in the thesis
└── LICENSE
```

## Citation

```
M. A. Mohd Yusri, "Development of an Optical Time-Domain Reflectometer-Based
Temperature Sensor Employing a D-Shaped Fiber," B.Sc. (Hons) thesis,
Universiti Sains Malaysia, 2026.
```
