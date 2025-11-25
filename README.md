# Hvelvigen Homelab Baseline

*Ett helt valv för din homelab‑resa*

A collection of modular, platform-agnostic baselines designed to help you build a clean, maintainable, and well-documented homelab.  
Rather than defining one “correct” way to build a system, this repository presents **multiple valid approaches**, allowing you to mix, match, and adapt based on your environment and skill level.

## Name (EN_GB)
*(uttalas/pronounced: "VEL-vee-yen")* 
**Hvelvigen** is drawn from Swedish roots: *hel* (whole, complete) and *valv* (vault, arch), with the archaic **hv** spelling.  
The meaning — *det hela valvet* (“the complete vault”) — reflects the repository’s role as a secure, structured place where code, documentation, and ideas are preserved.

## Namn (SV_SE)
**Hvelvigen** kommer från svenska ord: *hel* (hel, fullständig) och *valv* (valv, ark). Med den äldre stavningen **hv** får namnet en mer tidlös känsla.  
Betydelsen — *det hela valvet* — speglar att detta repo är en trygg och strukturerad plats där kod, dokumentation och idéer bevaras.

## Purpose
Provide structured, repeatable starting points for documenting and building a homelab.  
The baselines in this repository encourage best practices, clear organisation, and thoughtful configuration, while offering **alternative solutions** for common homelab tasks.

Whether you're running Proxmox or Hyper-V, Docker or Podman, Plex or Jellyfin, this project aims to show *how* things can be done—not dictate *how they must be done*.

## Scope
This repository includes:
- Modular directory templates and patterns  
- Example configurations for multiple platforms and tools  
- Alternative implementations for identical workflows  
- Documentation and organisation templates  
- Naming guidance and structure recommendations  
- Optional tooling suggestions  

This repository does *not* include:
- Environment-specific or personal details  
- Cloud-specific configuration  
- Proprietary diagrams or layouts  

## Repository Structure
/templates/ – reusable templates for documentation, config, and automation
/systems/ – platform-specific baselines (Proxmox, Hyper-V, Home Assistant, Docker, Linux, etc.)
/reference/ – command collections, cheat sheets, and best-practice notes
/docs/ – written guidance on structure, naming, and homelab organisation
/tooling/ – optional helper scripts and generic utilities
/meta/ – repo governance, roadmap, and evolution notes


## Included Templates
- Directory structures for organising services, systems, and documentation  
- Generic configuration templates (YAML, JSON, `.env`, etc.)  
- Markdown templates for documentation and operational notes  
- Optional starter files for automation (shell, PowerShell, etc.)  

Templates remain intentionally minimal so they can be adapted to different setups and platforms.

## How to Use This Baseline
Hvelvigen is modular. You can:
- adopt a full structure  
- combine baselines from different platforms  
- copy only the folders or templates relevant to your build  
- compare multiple implementations of the same service  

Suggested workflow:
1. Explore the `/systems` section to see platform options (e.g., Proxmox, Hyper-V).  
2. Copy relevant structures from `/templates`.  
3. Review `/reference` for command sets and operational guidance.  
4. Use `/docs` to help maintain clarity and consistency over time.  
5. Apply or extend optional tooling from `/tooling` as needed.

No assumptions are made about your existing environment, experience level, or preferred tooling.

## Recommended Tooling
These tools support most homelab workflows:
- Git / GitHub / Gitea for version control  
- Markdown editors for documentation  
- Container tooling (Docker, Podman, Compose)  
- Monitoring tools (open-source, platform-neutral)  
- Automation scripting (shell, PowerShell, task runners)  

All recommendations are optional and interchangeable.

## Naming Guidance
The naming principles aim to support long-term maintainability:
- clarity over cleverness  
- consistency over complexity  
- predictable structure and naming  

Detailed naming guidance is available in `/docs/naming.md`.



## Licence
This repository is licensed under the GNU GENERAL PUBLIC LICENSE.  
Feel free to adapt, reuse, and build upon these baselines in any environment.
