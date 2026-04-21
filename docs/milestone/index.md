---
title: Milestone
layout: default
nav_order: 3
---

# Milestone

[Homepage](https://cal-cs184-student.github.io/project-webpages-acdj/)

**Title:** Material Lab: A Physically-Based Shader Pack for Minecraft

**Team Members:** Daniel Wang, Anish Sasanur, Cedric Chan, Haoyu Yao

---

## Summary

Our goal was to replace Minecraft's default lighting with a unified, physically-backed BSDF pipeline using the Iris framework. We implemented a Minecraft Java Edition shader pack based on LabPBR to augment its specular lighting with a full Cook-Torrance BRDF. By parsing LabPBR texture standards, we extract per-pixel roughness and metallic data to drive our GGX normal distribution and Smith-GGX geometry shadowing.

---

## What We Have Accomplished

**BSDF Core**

We implemented the full Cook-Torrance microfacet model comprising:
- **Trowbridge-Reitz GGX (D)**: Normal distribution function controlling specular highlight shape from per-pixel roughness
- **Schlick's Fresnel (F)**: View-dependent reflectance increasing at grazing angles
- **Smith-GGX (G)**: Geometry shadowing/masking term accounting for microfacet self-occlusion

Per-pixel roughness and metallic values are decoded directly from the LabPBR specular texture atlas, enabling material-specific response across all block types without manual overrides.

**Translucent Materials**

We specialized the BSDF for translucent materials. By decoupling the depth logic for water and glass, we achieved accurate Fresnel-based transparency and architectural-grade glass tinting without depth conflicts.

**Screen Space Reflections (SSR)**

For high-fidelity reflections, we developed an SSR module using 64-step ray marching with 8-step binary search refinement. To eliminate sampling artifacts and moiré patterns, we integrated Interleaved Gradient Noise (IGN) for temporal-like stability.

**Procedural Skybox**

We replaced Minecraft's cubic skybox with a procedural sky dome using exponential atmospheric scattering, providing seamless day-night transitions with physically motivated luminance gradients based on world-space elevation angle.

---

## Preliminary Results

The shader runs in Minecraft Java Edition 26.1.2 via Iris Shaders. Screenshots from our test scenes demonstrate:

- **Glass towers** showing Fresnel-based transparency and architectural glass tinting without depth artifacts
- **Water surfaces** with SSR reflecting the surrounding scene geometry, including the city skyline and signage
- **Atmospheric sky** with a rich sunset gradient transitioning from deep orange at the horizon to dark blue at the zenith, seamlessly blending across the day-night cycle

The SSR output on water convincingly reflects the cityscape above, with the IGN jittering producing stable, artifact-free results across frames.

---

## Progress Relative to Plan

| Week | Planned | Status |
|------|---------|--------|
| Week 1 | Dev environment setup, pipeline definition, role assignments | Complete |
| Week 2 | Base material system + initial vanilla vs. enhanced comparisons | Complete |
| Week 3 | Material tuning, texture/normal mapping, final scene assembly | In Progress |
| Week 4 | Final renders, webpage, presentation polish | Planned |

We are **ahead of schedule** relative to the original proposal. SSR, originally listed as a stretch goal, is already implemented and producing high-quality results. The core BSDF, translucent materials, and procedural skybox are all complete.

Based on feedback from our project mentor, we are also **expanding scope** in two areas: (1) adding dynamic in-game lighting response (held torches, placed light sources driving per-fragment BRDF evaluation) as a core deliverable, and (2) adding a structured performance benchmarking component with FPS measurements across configurations and a dedicated optimization pass.

---

## Updated Work Plan

**Remaining Week 3 (April 20–25)**

- Normal mapping: build TBN matrix from `at_tangent` attribute for per-pixel surface normals
- Per-block PBR parameter tuning across metals, dielectrics, translucents, and emissives
- Begin dynamic lighting: per-frame injection of in-game light source positions and colors

**Week 4 (April 25 – May 1)**

- **Dynamic lighting (core deliverable)**: Full support for in-game point lights (torches, lanterns, glowstone) driving the BRDF per-fragment, with each source contributing its own diffuse and specular term
- **Performance benchmarking**: Record FPS in a controlled scene across four configurations, (1) vanilla Minecraft, (2) BSDF shader only, (3) shader + LabPBR textures, (4) shader + LabPBR + SSR + dynamic lighting, with frame time analysis identifying per-feature GPU cost
- **Optimization pass**: Profile with Iris debug tools; reduce shader branching, batch texture lookups, evaluate light loop culling
- **Enchantment glint effect**: Procedural animated shimmer overlay on enchanted items, driven by a time-varying UV distortion pass to simulate the characteristic iridescent sheen
- **Mace impact effect**: Vertex displacement shockwave in the terrain shader, a sinusoidal wave radiating outward from the point of impact, timed to the mace hit animation
- Final vanilla vs. PBR side-by-side comparison screenshots and video flythrough
- Complete final webpage and project report

---

## Resources

- [Milestone Slides](https://docs.google.com/presentation/d/1uaRI1bRegSA4cSa9Jimis39nfHwSqWpq/edit?usp=sharing&ouid=108387346108570320160&rtpof=true&sd=true)
- [Milestone Video](TODO)
