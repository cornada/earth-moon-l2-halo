# Earth–Moon L₂ Halo Orbit: Stabilization & Correction Strategy

Sister project of [sun-jupiter-l2-halo](https://github.com/cornada/sun-jupiter-l2-halo).
Numerical pipeline for periodic halo orbits near Earth–Moon L₂ in the Circular Restricted Three-Body Problem (CR3BP).

## 🚀 Interactive demo

**→ [Live 3D demo on GitHub Pages](https://cornada.github.io/earth-moon-l2-halo/)**

## 📘 Report

[`report.pdf`](report.pdf) — 41 pages, parallel structure to the Sun–Jupiter report.

## Key results

- **μ = 0.01215058**
- **x_L2 = 1.1557**
- Planar Lyapunov: T = 3.373 (≈ 14.6 days), λ_u = 1452, Jacobi drift 1.8·10⁻¹⁵
- Halo family: 7 orbits, Az ∈ [0.005, 0.022], T ≈ 3.41, λ_u 1128–1208
- Work-energy identity residual < 10⁻¹⁵
- Cheapest correction phase: perpendicular x-axis crossing, 1452× fuel advantage

## Pipeline

```bash
pip install numpy scipy matplotlib
python3 halo_correction_strategy.py
python3 halo_visualization.py       # figures 1–20
python3 halo_3d_family.py           # figures 21–35
python3 export_webdata.py           # regenerate docs/web_data.json
pdflatex report.tex && pdflatex report.tex
```

## License

CC BY 4.0.
