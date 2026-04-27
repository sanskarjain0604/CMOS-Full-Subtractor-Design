# Full Subtractor Layout Design in 65nm CMOS

This project presents the complete design flow of a **Full Subtractor** circuit, from schematic capture and transistor sizing to layout optimization and post-layout verification.  
The design targets **low area** and **low power** while maintaining correct functionality across different **PVT corners**.

---

## Project Overview

- **Technology Node:** 65nm CMOS
- **Operating Voltage:** 1.0 V
- **Total Transistor Count:** 36
  - 18 NMOS
  - 18 PMOS
- **Outputs:** Difference (`D`) and Borrow-out (`Bout`)

---

## Full Subtractor Functionality

A full subtractor computes the difference between three binary inputs:

- `A`
- `B`
- `Bin` (Borrow-in)

It produces:

- `D` = Difference
- `Bout` = Borrow-out

### Truth Table

| Bin | B | A | Difference (D) | Borrow (Bout) |
|-----:|--:|--:|---------------:|--------------:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 0 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

---

## Layout Optimization

Two layout versions were developed to compare the impact of floorplanning and routing strategy.

### Comparison of Layout Versions

| Feature | Version 1 (Unoptimized) | Version 2 (Optimized) |
|---------|--------------------------|------------------------|
| Strategy | Complex routing, high Metal2 use | Planned routing, shared Nwell/Diffusion |
| Dimensions | 13 Tracks (H) × 42 Tracks (W) | 13 Tracks (H) × 37 Tracks (W) |
| Total Area | 21.83 µm² | 19.3 µm² |

### Optimization Result

The optimized layout achieves approximately **11.6% area reduction** through:

- strategic poly routing
- shared diffusion regions
- reduced M2 usage
- better floorplanning

---

## PVT Corner Analysis

Performance was evaluated across **Typical-Typical (TT)**, **Slow-Slow (SS)**, and **Fast-Fast (FF)** corners.

### Pre- vs. Post-Layout Results

| Condition | Parameter | Pre-Layout | Post-Layout |
|----------|-----------|-----------:|------------:|
| Typical (1.0 V, 25°C) | Prop. Delay (`Tpd`) | 125.7 ps | 136.5 ps |
| Typical (1.0 V, 25°C) | Dynamic Power | 52.2 µW | 56.7 µW |
| Slow (0.8 V, 125°C) | Prop. Delay (`Tpd`) | 258.05 ps | 274.4 ps |
| Fast (1.32 V, -40°C) | Prop. Delay (`Tpd`) | 84.55 ps | 91.13 ps |

### Observations

- Post-layout delay is slightly higher than pre-layout delay due to parasitic effects.
- Dynamic power also increases after layout extraction.
- The circuit remains functional across all tested corners.

---

## Statistical Verification

Monte Carlo simulations were performed to study process variation impact on:

- `T_PLH`
- `T_PHL`
- overall propagation delay

This verifies robustness of the design under manufacturing variation.

---

## Design and Verification Flow

1. Schematic design
2. Transistor sizing
3. Layout creation
4. DRC checking
5. LVS verification
6. Parasitic extraction
7. Post-layout simulation
8. PVT corner analysis
9. Monte Carlo analysis
---

## Tools Used

- **Calibre** for DRC/LVS
- **Eldo** for simulation
- CMOS layout design tools for schematic and layout implementation

---

## Key Result

The optimized version of the full subtractor layout achieved:

- **smaller area**
- **better routing efficiency**
- **clean verification across PVT conditions**
