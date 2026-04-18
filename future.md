# Evolution journal — Earth-Moon L₂ halo orbit stabilization

Cumulative append-only log. NEVER overwrite or summarize previous entries.

---

## Session 2026-04-17 (inception, sister project of Sun-Jupiter)

### Context
Bootstrapped from `/Users/aleksandrvolkov/2/` (Sun-Jupiter L₂ halo project) as a parallel deployment for the Earth-Moon system. Mass ratio changed from µ = 9.53·10⁻⁴ to µ = 1.215·10⁻². Everything else — math, architecture, correction strategy, deployment pattern — kept identical as a test of pipeline transferability.

### What was done
- Cloned 5 Python scripts from Sun-Jupiter project, substituted mu.
- Ran the full pipeline: DC, Floquet, continuation, manifolds, multi-shooting, visualization.
- Adapted `demo.html` (color palette: Earth blue, Moon gray).
- Bulk-substituted `report.tex` strings; manually repaired semantic issues from overly aggressive sed.
- Compiled 41-page report.
- Deployed to `cornada/earth-moon-l2-halo` on GitHub, enabled Pages at `cornada.github.io/earth-moon-l2-halo/`.

### Quantitative results
- x_L2 = 1.1557 (Moon-to-L2 distance in CR3BP units = 0.168 ≈ 64 400 km).
- Planar Lyapunov: x₀ = 1.1577, vy₀ = -0.01093, T = 3.373 (≈ 14.6 days real).
- λ_u (planar) = 1452.
- Halo family: 7 members at Az ∈ [0.005, 0.022]. Halo x₀ - x_L2 ≈ -0.036 (inner side, like Sun-Jupiter). T ≈ 3.41. λ_u from 1208 down to 1128.
- Jacobi drift per revolution: 1.8·10⁻¹⁵.
- Fuel advantage of cheapest phase: 1452× (= λ_u for planar).
- Work-energy identity residual: < 10⁻¹⁵.

### Insights

1. **Architecture transfer was clean.** A single-variable mu substitution produced a correct, working pipeline. Validates that the Floquet correction strategy is fundamentally µ-independent; only the numerical values change.

2. **λ_u is µ-robust to within 20%.** Sun-Jupiter (µ=9.5e-4): λ_u=1752. Earth-Moon (µ=1.2e-2): λ_u=1452. Despite 13× mass-ratio difference, instability factor is in the same order. Suggests λ_u at collinear points is set by saddle geometry, not strongly by µ itself.

3. **Halo bifurcation threshold scales with µ.** Smaller Az_min for Sun-Jupiter (~0.002), larger for Earth-Moon (~0.005). The frequency-matching condition ω_p(Ax,Az) = ω_v(Ax,Az) requires different amplitudes depending on the linearized ω_p, ω_v gap.

4. **Halo on inner side (x₀ < x_L2) persists in Earth-Moon.** Same geometric feature as Sun-Jupiter. This is a monodromy-eigenstructure property at collinear L2, not a µ accident.

5. **Physical time scales differ 300×.** Lyapunov T = 3.37 CR3BP units. In real time: 3.37 × (27.32 days / 2π) ≈ 14.6 days. For Sun-Jupiter: 3.18 × (11.86 years / 2π) ≈ 6 years. Same dimensionless orbit = very different time scale. The instability "per revolution" means very different absolute rates: Earth-Moon L2 error doubles 3 orders of magnitude per 2-3 weeks, Sun-Jupiter per ~20 years.

### Mistakes and failures

1. **Bulk sed over-replaced Jupiter → Moon in URLs.** "cornada/sun-jupiter-l2-halo" became "cornada/sun-moon-l2-halo" (3 places in report). Caught by grep, fixed.

2. **Bulk sed broke semantic comparison sentences.** "Unlike Sun-Jupiter, Earth-Moon…" became "Unlike Sun-Moon, Earth-Moon…" (tautological). Required manual rewrites of 4 paragraphs.

3. **`rep = family[7]` hardcoded index.** Crashed because only 7 halo orbits converged for Earth-Moon, making index 7 out of range. Changed to `family[len(family)//2]` for robustness.

4. **Small-Az halos didn't converge.** Az = 0.002 (which works for Sun-Jupiter) fails for Earth-Moon — below the bifurcation threshold. Adjusted continuation range to start at 0.005.

5. **shell cwd auto-reset between bash invocations.** `cd /Users/aleksandrvolkov/earth-moon-l2 && pdflatex …` in one invocation worked, but cd from a previous invocation didn't persist. Forced use of `-output-directory=.` with explicit chained commands.

### Future ideas

- **Complete the µ-trilogy with Sun-Earth** (µ = 3.04e-6). Expected λ_u ≈ 1500 based on literature.
- **Write comparison paper** — side-by-side tables of λ_u, T, halo-family shape, manifold tube geometry across Sun-Jupiter / Sun-Earth / Earth-Moon. Three deployed demos linked from a single landing page.
- **Ephemeris correction for Earth-Moon is qualitatively different from Sun-Jupiter.** Moon has non-negligible eccentricity (0.0549) and inclination relative to ecliptic (5.145°). The CR3BP assumption degrades faster here. Worth explicit quantification.
- **Operational context:** Earth-Moon L2 is where all upcoming lunar farside missions will operate (Queqiao, LuSEE-Night, proposed radio interferometers). A live, interactive, correct-to-machine-precision demo has pedagogical value the Sun-Jupiter version doesn't.
- **Bridge to NRHO (Near-Rectilinear Halo Orbit).** NASA's Lunar Gateway will use an NRHO, which sits on a different branch of the halo family (very large Az, nearly vertical). Extending the continuation to that amplitude regime would directly serve operational needs.

### Deployed artifacts
- Repo: `github.com/cornada/earth-moon-l2-halo`
- Live demo: `cornada.github.io/earth-moon-l2-halo/`
- Sister project: `github.com/cornada/sun-jupiter-l2-halo`
