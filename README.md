# OTDR-Based Temperature Sensor Employing a D-Shaped Fiber

Bachelor of Science (Hons) in Physics final year project, Universiti Sains Malaysia (USM), 2026.

**Author:** Muhammad Aqil Bin Mohd Yusri  
**Supervisor:** Dr. Afiq Arif Aminuddin Jafry  
**Project partner:** Muhammad Ariff Bin Roshidi  

---

## Summary

This project develops a point temperature sensor that pairs a side-polished **D-shaped single-mode fiber (SMF-28)** with a commercial **Optical Time-Domain Reflectometer (OTDR)** operating at 1550 nm. Temperature changes in the surrounding water alter its refractive index, which changes the Fresnel reflection peak at the cleaved fiber end as seen on the OTDR trace. The peak height is the measurand.

OTDR-based temperature sensing normally suffers from weak sensitivity, because standard silica fiber is almost inert to heat. Exposing the evanescent field through a D-shaped geometry is proposed as a simple structural modification. To our knowledge, this exact configuration (D-shaped fiber + OTDR for temperature) had not been reported before.

## Objectives

1. Fabricate and characterize D-shaped fibers with several polishing depths using side-polishing.
2. Evaluate their temperature sensitivity and linearity with an OTDR as the interrogator.

## Method

The sensor is a single-ended OTDR link: **VIAVI SmartOTDR (SC/APC) → 2 km SMF-28 launch spool (FC/UPC) → D-shaped sensing probe (FC/UPC) → open-cleaved far end**, joined with FC/FC adapters. The 2 km spool pushes the sensing region beyond the OTDR dead zone and provides a stable linear backscatter baseline; the open-cleaved far end produces a strong Fresnel reflection that marks the probe position.

### 1. Probe fabrication

**Fiber preparation.** The acrylate buffer was stripped over a 30–40 mm length with a Signal Fire 9-in-1 mechanical stripper, wiped once (single direction) with an IPA-soaked lint-free wipe, and cleaved with a Signal Fire high-precision cleaver. End-faces with an angle >1.0° or visible defects were rejected and re-cleaved.

**Fusion splicing.** Prepared ends were joined with a Signal Fire AI-9 fusion splicer using its automated 3-axis core-alignment routine and the pre-programmed SMF-to-SMF arc profile (unmodified across all samples). Splices exceeding a **0.02 dB** loss estimate were rejected and repeated.

**D-shape polishing.** Cladding was removed from one side using a custom rig: a **Dremel 200** rotary tool fitted with a **4 mm diamond-grit bit**, mounted vertically on a rigid stand above a multi-axis translation stage holding the fiber. Rotational speed was varied — higher for bulk cladding removal, lower near the target depth. Insertion loss was monitored in real time with the SmartOTDR in **CW VFL mode** and a **Wintact WT65 optical power meter** at the far end; polishing stopped when the transmitted power had dropped by the target loss. The diamond bit was chosen over sandpaper for a flatter, more geometrically consistent D-section and a fabrication time under one minute per probe.

**Probes.** One unpolished SMF-28 control plus five D-shaped probes at target insertion losses of **2, 4, 6, 7, and 8 dB**, each a progressively deeper polish.

**Geometric characterization.** Each probe was imaged side-on with a **Motic BA310** optical microscope, with digital line-profiling in ToupView. Insertion loss is treated as the operational proxy for evanescent-field exposure rather than an absolute diameter measurement.

### 2. OTDR configuration

All acquisition parameters were fixed at the start of each run; only the pulse width was varied.

| Parameter | Setting |
|---|---|
| Wavelength | 1550 nm |
| Measurement range | 5 km |
| Acquisition time | 10 s |
| Sampling resolution | 32 cm |
| Pulse width | 5 ns and 10 ns |

1550 nm was chosen for deeper evanescent penetration into water (~400 nm vs ~280 nm at 1310 nm) and lower SMF-28 attenuation (0.18 vs 0.32 dB/km). The 10 s acquisition gave a usable SNR without needlessly lengthening each run, and 32 cm is the finest sampling available at the 5 km range.

### 3. Thermal control and data acquisition

The polished region was submerged in **deionized water** in a beaker centred on a **Brandon BHS-II-4D digital ceramic hotplate stirrer**. Water temperature at the sensing region was read directly with a **thermocouple and multimeter**, not the hotplate's surface display.

Each of the six probes was measured in a separate session with the chain reassembled from scratch. Connectors were cleaned with a one-click cleaner and a smart test confirmed no anomalous reflection or loss events before each session. The probe was submerged before heating, and the thermocouple tip placed alongside the sensing region.

The water was heated from **40 to 80 °C in 5 °C steps**, with a **2-minute stabilization** at each step before acquiring traces at both 5 ns and 10 ns. Sensitivity was extracted by ordinary least squares:

```
S = Σ(xᵢ − x̄)(yᵢ − ȳ) / Σ(xᵢ − x̄)²
```

where xᵢ is temperature and yᵢ the peak loss at point i.

**Stability test.** The bare control and the 7 dB probe were held at a static 60 °C, with 10 consecutive traces acquired at 2-minute intervals (20 min total) to assess repeatability.

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
