# Naming Guidance

This document provides practical principles for designing a clear, consistent naming scheme for your homelab.  
A good naming scheme makes systems easier to understand, maintain, and document — especially as environments grow over time.

The goal is not to enforce one specific format, but to help you build a scheme that is predictable and works for your use case.

---

## Why Naming Matters
A consistent naming structure helps you:

- understand your environment at a glance  
- avoid confusion as you add more services or hardware  
- reduce errors when configuring systems or automation  
- create documentation that stays readable and future-proof  
- make backups, monitoring, and maintenance easier  

A naming scheme is successful when someone can predict what something is *before* opening it.

---

## Core Principles

### 1. **Clarity**
Names should be instantly understandable without needing a legend.

### 2. **Consistency**
Choose a pattern and apply it everywhere.

### 3. **Predictability**
A name should reflect the purpose or category of what it represents.

### 4. **Neutrality**
Avoid platform-specific formats so the same approach works across systems.

### 5. **Simplicity**
Shorter names are easier to read and remember—but not at the cost of clarity.

---

## Designing a Naming Scheme

### Step 1 — Define your categories
Most homelabs include categories like:

- hosts / hypervisors  
- virtual machines  
- containers  
- storage  
- networks  
- services  
- documentation  
- scripts  

Each category should have its own pattern.

---

### Step 2 — Pick a pattern for each category
Some common, effective patterns:

#### **Functional**
media-server
backup-node
monitoring-vm
router-core

#### **Role + number**
pve01
pve02
docker01
docker02

#### **Role + location**
core-vm
edge-switch
iot-gateway

#### **Named scheme (if desired)**
Themes are optional (colours, places, astronomy, etc.).  
If used, apply them consistently and document the mapping.

---

### Step 3 — Decide on separators
Use one separator style across your environment:

**Recommended:**  
- hyphens `(-)` for readability (`media-server`, `docker-host01`)  
- lowercase only

Avoid mixing hyphens, underscores, and camelCase unless you have strong reasons.

---

### Step 4 — Make rules for versioning and instances
Examples:

- multiple instances of a service → `service01`, `service02`  
- cluster members → `node-a`, `node-b`, `node-c`  
- configs → `config.example.yaml`, `config.local.yaml`
- versioned assets or files  

#### **Versioned files or assets**
If you keep multiple generations of a file (diagrams, exported configs, schema drafts), use simple sequential versions:
storage-layout-v1.md
storage-layout-v2.md
storage-layout-v3.md

Version numbers should be:
- incremental  
- meaningful to *you*  
- used consistently  

#### **Using Git for version control**
Git tracks changes automatically, so you generally don’t need to version every file manually.  
Use file versioning only when:
- you want to keep separate published versions  
- you maintain multiple variations of a template  
- you're producing stable “snapshots” for reference  

Everything else can rely on Git history, branches, and tags for full auditing.

In short:  
- **Git handles change history**  
- **your naming scheme handles distinct instances, variants, and published versions**

This separation keeps naming simple without losing clarity.

Document your naming rules once so future additions follow the same pattern.

---

### Step 5 — Apply patterns to each asset type

---

## Recommended Patterns by Asset Type

### 1. **Folders**
Use descriptive names:
proxmox/
home-assistant/
docker/
linux/
backup/
monitoring/

### 2. **Files**
Use hyphenated lowercase names:
setup.md
config.yaml
notes.md
docker-compose.yaml

### 3. **Virtual Machines**
Choose one pattern:

**Functional**
pve01
ha01
mon01

---

### 4. **Containers**
Keep service names short and functional:
plex
jellyfin
nginx
homeassistant
postgres

For multi-instance:
nginx-proxy
nginx-app

---

### 5. **Network & VLAN Naming**
Keep names role-based and clear:
vlan10-core
vlan20-servers
vlan30-iot
vlan40-media

Hostnames should follow the same logic as VM names.

---

### 6. **Documentation**
Use predictable naming for docs:
overview.md
setup.md
configuration.md
troubleshooting.md
operations.md

---

## Example Naming Scheme (Complete)
Below is one example showing a consistent approach:
systems/
proxmox/
setup.md
migration.md
home-assistant/
structure.md
yaml-examples/

reference/
networking/
vlan-basics.md
shell/
common-commands.md

tooling/
scripts/
cleanup-logs.sh
update-containers.ps1


---

## Summary
A naming scheme should be:

- easy to read  
- easy to extend  
- easy to predict  
- consistent across the entire homelab  

Use these guidelines to define a pattern that works for you and document it early.  
Future-you will thank present-you.
