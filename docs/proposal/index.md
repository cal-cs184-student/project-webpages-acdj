---
title: Proposal
layout: default
nav_order: 2
---

# Proposal

[Homepage](https://cal-cs184-student.github.io/project-webpages-acdj/)

**Title:** Material Lab: A Physically-Based Shader Pack for Minecraft

**Team Members:** Daniel Wang, Anish Sasanur, Cedric Chan, Haoyu Yao

---

## Summary

We will modify an existing Minecraft Java Edition shader pack to replace/augment its current diffuse/specular lighting with a simplified Cook–Torrance microfacet BRDF. We will evaluate how the BRDF changes material appearance (stone vs metal vs glass/water) and quantify the performance impact in a controlled, repeatable scene. Our final deliverables will include a demo video, side-by-side visual comparisons, and a report analyzing quality/performance trade-offs.

---

## Problem Description

Minecraft's default renderer prioritizes simplicity and performance, using largely uniform shading with minimal differentiation between material types. As a result, surfaces like stone, glass, and metal look visually similar aside from their textures, lacking the rich appearance differences seen in real life or physically-based rendering systems.

The core challenge is introducing **material-specific light interaction** into Minecraft's voxel world. Real materials differ not just in color and texture, but in how they reflect, absorb, and transmit light (glass refracts and reflects, metals produce view-dependent highlights, and rough surfaces like terracotta scatter light diffusely). Beyond the material models themselves, adapting physically-based rendering to a discrete, grid-based voxel world introduces unique challenges around block boundaries and data transmission from the game to the GPU.

Our approach is to build a **modular shader system** that supports diverse material behaviors while remaining compatible with Minecraft's rendering pipeline, using the Complementary shader framework.

---

## Goals and Deliverables

### Plan to Deliver

**Core System**

- A working shader pack built on top of Complementary
- A modular material interface supporting multiple surface types
- A consistent Minecraft scene with controlled lighting and camera setup

**Speculative Material Implementations**

- **Glass** — reflection and refraction with view-dependent behavior
- **Metal** — specular highlights that vary with viewing angle
- **Stone or terracotta** — diffuse scattering with surface detail
- **Ceramic or coated surface** — combined diffuse and glossy response

**Visual Outputs**

- Side-by-side comparisons of vanilla Minecraft shading vs. our enhanced materials
- Per-material render studies
- A unified final Minecraft scene containing all four materials together

**Evaluation**

- Visual realism improvement over vanilla baseline
- How different materials affect rendering complexity and noise
- Performance impact of more complex material models
- What tradeoffs exist between Minecraft's simplicity and physical realism

---

### Hope to Deliver

- Frosted or rough glass variants
- Layered material effects (e.g., glazed terracotta)
- Simple translucency for blocks like ice or leaves
- Procedural surface variation within block types
- Dynamic lighting response to in-game light sources (e.g., held torches)
- A polished final scene with a short flythrough video

---

## Schedule

**Week 1 — Setup**
Set up the Complementary development environment, establish the shader pipeline, define the shared material interface, and finalize which material each team member will implement.

**Week 2 — Core Implementation**
Implement the base material system and each member's assigned material. Integrate into the shared pipeline and produce initial vanilla vs. enhanced comparisons.

**Week 3 — Refinement**
Tune material parameters, add texture and normal mapping where appropriate, analyze convergence and noise behavior across materials, and assemble the final unified Minecraft scene.

**Week 4 — Finalization**
Generate final renders and comparisons, prepare the project webpage and presentation, and polish visual output and analysis.

---

## Resources

- **Platform:** Minecraft Java Edition
- **Framework:** Complementary Minecraft Shader
- **Languages:** Java (mod logic), GLSL (shader kernels)
- **References:** CS184 lecture notes, LearnOpenGL PBR, Real-Time Rendering 4th Ed., Scratchapixel
- **Assets:** Minecraft block assets, HDR environment maps, LabPBR-standard material textures
