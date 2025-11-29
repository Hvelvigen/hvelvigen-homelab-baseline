# Hvelvigen — Recipe Template (Updated)

A structural template for Hvelvigen recipes.  
Use this as a **copy → rename → fill in** starting point when creating a new recipe.

Recipes should:
- keep **all section headings** in this order (unless explicitly not needed)
- stay **outcome‑driven** (what the user ends up with, not just what they run)
- avoid inline troubleshooting and deep technical detail — that lives in guides

---

## Repository Location

```text
meta/
└── hvel_recipe_template.md   ← you are here
```

---

## 1. Purpose / Desired Outcome

A short paragraph explaining what the user will achieve by following this recipe.

Then, list the key end‑state outcomes as bullets. For example:

- a clearly defined system or service role
- a repeatable, security‑conscious baseline
- one or more services available on the LAN
- a clear understanding of where configuration and data live

Keep this section **service‑agnostic** when first drafting; refine once the recipe is scoped.

---

## 2. Who This Recipe Is For

Align the recipe with its intended audience:

- experience level (beginner / intermediate / advanced)
- expectations around prior knowledge (e.g. basic SSH and terminal usage)
- any assumptions about comfort with networking, Docker, hypervisors, etc.

You can optionally include links to lightweight reference material (cheat sheets, primers) that live under `reference/` or `docs/`.

---

## 3. Prerequisites

List what the user needs **before** they start.

Include both non‑technical and technical prerequisites, for example:

- hardware or virtualisation platform available (e.g. hypervisor VM, physical host, SBC)
- basic familiarity with SSH and terminal usage
- working network (DHCP and/or reserved/static IPs)
- estimated time to complete the full flow without rushing

Avoid commands here — this section is about readiness, not execution.

---

## 4. Supported Hardware Profiles (Optional)

If the recipe supports multiple hardware or deployment paths, define them here.

For each profile, include:

- **Profile name** — e.g. “x64 VM or physical host”, “Raspberry Pi (ARM64)”, “Low‑power node”
- **Typical scenarios** — where this path makes sense
- **Guide references** — installation guide(s) for the base OS, e.g.:
  - `systems/linux/ubuntu/ubuntu-server-installation.md`
  - `systems/linux/ubuntu/ubuntu-server-rpi-installation.md`

Profiles should converge on the same OS configuration and security baseline wherever possible.

If there is only one hardware path, you can either keep this section brief or omit it entirely.

---

## 5. Flow Overview

Provide a high‑level, non‑technical map of the phases in this recipe.

Example structure (adapt to suit the recipe):

1. Base OS installation  
2. OS post‑install configuration  
3. Access & security baseline  
4. Platform or service‑host profile (e.g. Docker host, hypervisor helper, storage node)  
5. Service pattern(s) (one or more applications or stacks)  
6. Validation & documentation  

This section is **conceptual only** — no commands, no file paths, no links.

---

## 6. Step‑By‑Step Recipe Flow

This is the core of the recipe.  
Each step sends the reader to a guide and then returns here to confirm the result.

Use one or more paths, depending on the supported profiles.

### Path A — <Profile Name>

#### 1. <Phase Name — e.g. Install Base OS>
Follow: `<systems/.../install-guide.md>`

**You should now have:**  
- brief checklist of expected state after this phase  
- e.g. “clean OS install”, “stable network”, “console login available”  

**Document:**  
- the key facts future‑you will care about  
- e.g. hostname, IP, OS version, hypervisor/host details

---

#### 2. <Phase Name — e.g. Post‑Install Configuration>
Follow: `<systems/.../post-install-guide.md>`

**You should now have:**  
- expected configured state for this phase

**Document:**  
- any deviations from the guide  
- anything notable you changed intentionally

---

#### 3. <Phase Name — e.g. Access & Security Baseline>
Follow: `<systems/.../ssh-configuration.md>`

**You should now have:**  
- expected security baseline (e.g. SSH port, key‑based access working, firewall enabled)

**Document:**  
- ports in use  
- firewall rules  
- locations of key configuration files

---

#### 4. <Phase Name — e.g. Service Host Profile>
Follow: `<systems/.../service-host-profile.md>`

**You should now have:**  
- the platform prepared for the target workload (e.g. Docker host, storage node)

**Document:**  
- directory structure  
- versions of key components  
- any important configuration decisions

---

#### 5. <Phase Name — e.g. Service Pattern / Application Stack>
Follow: `<systems/.../service-pattern.md>`

**You should now have:**  
- one or more services running and reachable via the intended access pattern

**Document:**  
- service URLs  
- container names / service identifiers  
- key volume mappings or data locations  

---

#### 6. Validation & Documentation
Use: `docs/documentation/lightweight-documentation.md` (or equivalent)

**You should now have:**  
- a stable, configured system that matches the recipe’s purpose

**Document:**  
- final state  
- known limitations  
- any “next time I’d do this differently” notes

---

### Path B — <Optional Second Profile>

Repeat the same structure for alternative hardware / deployment paths.  
After the OS install phases, paths should converge on the same core flow wherever possible.

---

## 7. Variants / Options (Optional)

If the recipe can be adapted into clearly distinct variants, list them here at a **conceptual** level.

Examples:

- LAN‑only vs reverse‑proxy fronted  
- minimal deployment vs extended stack  
- single‑node vs multi‑node pattern

Keep this brief and avoid full instructions — detailed variants belong in separate recipes or service‑pattern guides that build on this one.

---

## 8. Validation / Final Outcome

Define a short checklist the user can work through to confirm the recipe has succeeded.

Example items:

- remote access works as intended (SSH, web UI, API, etc.)  
- only the expected ports are open on the host  
- core services are running and reachable from the intended clients  
- persistent data is stored in the documented locations  

This section should be written so the user can answer **“yes” or “no”** for each point.

---

## 9. Troubleshooting

This section redirects to dedicated troubleshooting material rather than embedding fixes here.

Point to:

- system‑level troubleshooting (e.g. SSH, networking, storage)  
- platform‑level troubleshooting (e.g. Docker, hypervisor, specific service)  
- any relevant `reference/` or `systems/` troubleshooting guides  

The recipe stays focused on the **happy path**; troubleshooting lives elsewhere.

---

## 10. What’s Next / Optional Extensions

Suggest natural follow‑on work or upgrades, such as:

- adding monitoring, logging, or backup patterns  
- placing services behind a reverse proxy  
- extending with additional service patterns using the same host baseline  
- integrating with other recipes in the repo

Keep this forward‑looking and optional — these are **next steps**, not part of the core recipe.

---

*This template is intentionally descriptive rather than technical.  
When you create a new recipe, copy this file, rename it, and replace each section with concrete content while keeping the overall structure intact.*
