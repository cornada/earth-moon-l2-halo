# Earth–Moon L₂ Halo Orbit — Interactive Demo

Live 3D simulation of periodic halo orbits near the Earth–Moon L₂ libration point.
Sister project of [Sun–Jupiter L₂](https://cornada.github.io/sun-jupiter-l2-halo/); same pipeline, mass ratio μ = 0.01215.

## Quick start

```bash
cd docs/
python3 -m http.server 8765
# open http://localhost:8765/
```

## Key numbers

- **μ = 0.01215058** (Moon/Earth+Moon mass ratio)
- **x_L2 ≈ 1.1557** (non-dimensional; Moon-L2 distance ≈ 64,000 km)
- **Period T ≈ 3.373** (planar Lyapunov) ≈ **14.6 days** real
- **λ_u ≈ 1452** per revolution
- **Halo family** (7 members): Az ∈ [0.005, 0.022], T ≈ 3.41, λ_u from 1208 to 1128

## Scene cheatsheet

Same layout as the Sun–Jupiter demo with the Sun replaced by Earth (blue) and Jupiter replaced by the Moon (gray).

## Physics in one paragraph

Earth and Moon sit stationary in the rotating frame (co-rotating at lunar orbital period, 27.32 days). Five Lagrange points are equilibria of the pseudo-force; three collinear (L₁, L₂, L₃) and two triangular (L₄, L₅). L₂ is 64,000 km past the Moon on the far side, at the edge of the Moon's Hill sphere. Operational significance: all farside-communication relays (Chinese Queqiao, planned NASA communication birds) orbit in the L₂ halo family. The instability factor λ_u ≈ 1452 means position error grows three orders of magnitude per revolution — stationkeeping is mandatory.

## License

CC BY 4.0.
