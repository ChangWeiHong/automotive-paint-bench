# Automotive Paint Bench

A single-page three.js tool that shows a car in modelled daylight and compares
two lighting conditions side by side (A and B): region, timezone, date, time,
sky/weather, air temperature, humidity, aerosol haze, altitude, ozone, street
light and headlights. A spectrum chart and "paint as seen" swatches show how the
light changes the colour you perceive (ΔE between A and B).

Car paint is layered like factory paint: a base coat that shifts colour with
viewing angle, metallic/mica flakes, and an orange-peel clearcoat. Finishes:
solid, metallic, pearl, candy, satin.

## Run

```bash
python3 -m http.server 8080   # then open http://127.0.0.1:8080
```

A local server is required; browsers block model loads from `file://`.

## Models

`models/*.glb` — metres, Y up, length along X. The page centres each model,
faces its front toward the camera and repaints the largest opaque non-trim
material as the body.

| Model | Source |
| --- | --- |
| Myvi, Myvi v2 | awantech `GLB/` |
| Compact hatchback | awantech `compact-hatchback/GLB/` |
| Sedan, Cybertruck | exported from STEP in `automotive-cad-model-preview/models/STEP/` with `cadgen glb build` |
| Smart fortwo, Angular pickup | awantech `text-to-cad.ready/models/*/GLB/` |

## Model limits

The atmosphere is a simplified single-scattering model at 10 nm steps
(Rayleigh, Ångström aerosol, Chappuis ozone, H₂O and O₂ bands, cloud diffusion)
converted with CIE 1931 colour matching. It is built for side-by-side
comparison, not calibrated colour grading. Clock times are standard time.
