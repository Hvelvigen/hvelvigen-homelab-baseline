# Hvelvigen — Recipe Template (Bare‑Bones Structure)

This file defines the **structural skeleton** for all Hvelvigen recipes.  
It contains *no technical steps*, *no commands*, and *no descriptive prose*.  
It is a framework for building modular, outcome‑driven recipes that orchestrate guides.

---

## 1. Recipe Name
Short, clear, outcome‑focused.  
*Example: “Docker on Linux for Media”*

---

## 2. Purpose / Desired Outcome
A single paragraph describing what the user will achieve by following this recipe.  
Outcome‑driven only.

---

## 3. Who This Recipe Is For
A brief alignment check based on audience experience level.  
Should match the tone and audience described in the root README.
eg: Suitable for beginners — no prior Docker experience needed.

---

## 4. Prerequisites
Non‑technical prerequisites such as:

- basic familiarity with SSH and the terminal  
- network access  
- prepared hardware or virtual environment  

No steps, no commands.

---

## 5. Supported Hardware Profiles
Each recipe can support one or more hardware paths.

Each profile includes:
- short introduction  
- link to the appropriate OS installation guide (anchor)  
- hardware‑specific notes  

Examples:
- **Profile A — x64 System**  
- **Profile B — Raspberry Pi (ARM64)**

---

## 6. Flow Overview
A high‑level conceptual map of the phases that the recipe will guide the user through:

1. Hardware → OS installation  
2. OS post‑install configuration  
3. Access & security baseline  
4. Service host profile (e.g., Docker host)  
5. Service pattern (e.g., media stack)  

This section contains *no links* and *no steps* — it is purely the flow map.

---

## 7. Step‑By‑Step Recipe Flow (No Technical Steps)
The core of the recipe.

For each supported hardware profile, list the sequence of guides to open.

Example structure:

### Path A — x64 Hardware
1. Install OS → *guide link + anchor*  
2. Post‑install configuration → *guide link*  
3. SSH & security baseline → *guide link*  
4. Service host profile → *guide link*  
5. Service pattern → *guide link*  

### Path B — Raspberry Pi
Equivalent path, using RPi‑specific installation guide and anchors.

The recipe does **not** contain commands — only instructions on which guide to follow next.

---

## 8. Documentation Checkpoints
Recipes prompt lightweight documentation after each major phase.

Each checkpoint includes:
- **What you should now have**  
- **What to record in your documentation**  

Standard checkpoint types:
- OS Installation Checkpoint  
- OS Configuration Checkpoint  
- Security Baseline Checkpoint  
- Service Host Checkpoint  
- Service Pattern Checkpoint  

---

## 9. Variants / Options (Optional)
Used only if the recipe offers multiple outcome paths, e.g.:

- LAN‑only vs HTTPS exposure  
- minimal vs extended deployment  
- additional add‑on services  

This section remains conceptual and short.

---

## 10. Validation / Final Outcome
A simple checklist confirming the expected final state, such as:

- system reachable  
- services running  
- containers operational  
- reverse proxy responding  

No troubleshooting — just validation.

---

## 11. Troubleshooting Redirect
A section pointing to:

- troubleshooting guides  
- relevant categories of known issues  

Contains *no inline troubleshooting steps*.

---

## 12. What’s Next / Optional Extensions
Pointers to further improvements such as:

- monitoring  
- backups  
- additional service patterns  
- recommended next recipes

---

*This file will live in `/meta/` once finalised.*
