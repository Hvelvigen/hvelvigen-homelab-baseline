# Ubuntu Server 24.04.3 LTS Installation
A consistent and repeatable process for deploying Ubuntu Server within a homelab.  
The aim is a clean, minimal starting point that behaves the same every time — easy to follow whether this is your first install or your fiftieth.

Keyboard-only inputs appear in brackets; each `[]` represents a single key press.

---

## Before You Begin
This guide assumes:

- The VM meets the following **system requirements**:
  - 1 vCPU (2+ recommended)
  - 1–2 GB RAM minimum (4 GB recommended)
  - System disk: 16–32 GB
  - Data disk: sized according to service workload
  - Reliable network connectivity (LAN/VLAN)

- The VM has **two disks**:
  - a **system disk** (size varies — we use lightweight disks for OS-only images),
  - a **secondary data disk** for Docker, apps, logs, and anything that shouldn’t be cluttering `/`.  
    Only the system disk is touched during installation.

- VLANs, routing, and DNS resolution have already been tested from the hypervisor layer.

- No LVM or encrypted root filesystem is required for this baseline.

---

## Scope
This document covers the base installation of Ubuntu Server 24.04.3 LTS on a virtual machine.  
It does not include post-install configuration, hardening, or service setup — those are documented separately.

---

## Installation Guide

1. Start the VM.

2. Let GRUB (the Bootloader) autoload, or press **[Enter]** when *“Try or Install Ubuntu Server”* is highlighted.

3. Wait...

4. From the language selection screen, select your **language/locale**.

5. From the keyboard settings page, Confirm keyboard settings (press **[Enter]** if they’re correct).

6. Ensure **Ubuntu Server** is selected → **Done** → **[Enter]**.

---

### Network Configuration

7. Network Configuration depends on your environment, you may need to set this manually if using non-DHCP reserved static assignments (hello Excel!).
  
    **7.1 DHCP with no reservation (not recommended):**  
    Simply select **Done** → **[Enter]**.

    **7.2 Manual IP assignment:**  
   - Highlight the correct Ethernet adapter → **[Enter]**  
   - Select **Edit IPv4** → **[Down][Down][Enter]**  
   - Change **IPv4 Method** from DHCP to **Manual** → **[Down][Enter]**  
   - Enter addressing details using **[Tab]** between fields  
     - Subnet must be CIDR (e.g., `10.10.0.0/24`)  
   - **[Tab]** to **Done** → **[Enter]**
    
    **7.3 DHCP Reservation (recommended):**  
    Confirm the IP Address matches your schema.

8. **[Tab]** to **Done** → **[Enter]**.

9. Leave the proxy field empty unless you actually use one → **[Tab][Enter]**.

---

### Mirror Test

10. If networking is correct, the mirror test will pass.  
    Select **Done** → **[Enter]**.  
    If not, revisit Step 7 and try again — Ubuntu is usually right when it says something can’t reach the internet.

---

### Storage Configuration

11. In the guided storage screen:  
    - Ensure **Use an entire disk** is selected  
    - Confirm the correct disk (system disk) is chosen  
    - **Uncheck** *Set up this disk as an LVM group* → **[Tab][Tab][Space]**  
    - Select **Done** → **[Tab][Tab][Enter]**

12. From the storage configuration screen:
    Review the layout. Required mount points:  
    - `/`  
    - `/boot/efi`  
    Select **Done** → **[Enter]**.

13. Confirm changes → **Continue** → **[Down][Enter]**.

---

### Profile Setup

14. Enter your user details.  
    Navigate using **[Tab]** → **Done** → **[Enter]**.

---

### Ubuntu Pro

15. Ubuntu Pro is optional.  
    For a simple, controllable baseline, I recommend skipping for now, until you've established a baseline of your own.

---

### SSH and Snap Packages

16. Skip SSH (we’ll configure it properly later) → **[Tab][Enter]**.

17. Skip snaps → **[Tab][Enter]**.

---

### Finalisation

18. Wait ... 

19. When prompted:  
    - Select **Reboot Now** → **[Tab][Down][Enter]**  
    - *Then* remove the ISO/USB from the VM.  
      Ubuntu will briefly shout about failing to unmount the device — that’s normal, and it’s your cue to detach the installation media.

20. After reboot, the system will land on the **login:** prompt and is ready for post-install configuration.

This concludes the Installation Guide

---

## Why These Choices Were Made

This section explains the reasoning behind the decisions taken during the installation, so there's no ambiguity later about why certain options were used or skipped.

---

### Why Use the Default “Ubuntu Server” Option?
The installer’s default **Ubuntu Server** selection is intentionally used here because it provides:
- a clean, predictable server base,
- a well-supported package set,
- and none of the desktop or unnecessary service overheads.

It’s not a “minimal” installation — it’s the standard baseline Ubuntu expects you to build upon.  
That makes behaviour consistent across reinstalls, updates, and future guides.

---

### Why Use a Two-Disk Layout?
Using a dedicated **system disk** keeps the OS self-contained and disposable.  
The **secondary disk** becomes the home for Docker, service data, logs, and anything designed to persist across rebuilds.

The advantages:
- Rebuilding the OS does not risk wiping your containers or data  
- Maintenance stays tidier  
- Storage layout stays consistent regardless of VM role  
- You avoid Ubuntu scattering persistent data across `/var` on the system disk

It’s a simple structure that scales nicely and avoids “where did Ubuntu put *that*?” moments.

---

### Why No LVM?
LVM is useful for environments where you extend volumes dynamically or juggle physical disks.  
In a homelab VM:
- disks are virtual,
- expansion is done at the hypervisor layer,
- and complexity slows everything down for no practical benefit.

Disabling LVM gives you:
- a simpler partition scheme,
- less abstraction,
- and an easier time snapshotting, backing up, or rebuilding.

---

### Why Handle Networking Manually (or via DHCP Reservation)?
Networking is one of the easiest ways an installation can go sideways.

The guide supports three approaches because different homelabs behave differently:
- **DHCP (temporary)** when you just need connectivity  
- **Manual** when you want predictable addressing  
- **DHCP reservation** when you want predictability *and* set-and-forget convenience  

Reserved/static addressing keeps the system exactly where you expect it to be, avoids future reconfiguration, and aligns with IP schemas you control (well.. hello again, Excel).

---

### Why Skip SSH During Installation?
The installer enables SSH with defaults you don’t control — and those defaults often don’t match a good baseline hardening.

Skipping SSH now means:
- you install it cleanly after first boot,
- you apply your own security baseline,
- and you avoid Ubuntu silently enabling features you weren’t ready for.

It’s not skipped because SSH is “bad”; it’s skipped so *you* decide how it starts.

---

### Why Skip Snaps?
Snaps:
- auto-update,
- operate under confinement rules,
- and place runtime data in non-standard paths.

This creates unpredictable behaviour when trying to maintain a reproducible homelab environment.

Skipping snaps:
- keeps things cleaner,
- ensures file paths are where you expect them,
- and prevents packages updating themselves out of sync with the rest of the system.

If you want snaps later, you install them intentionally — not because the installer offered them.

---

### Why Postpone Ubuntu Pro?
Ubuntu Pro is useful, but not required for establishing a clean baseline.

By skipping it during installation:
- you avoid mixing subscription and token flow with setup,
- you ensure the base OS works consistently without external dependencies,
- and you decide later if you actually want Pro features.

It keeps the *first build* simple and reproducible.

---

### Why This Level of Detail?
The goal is clarity for all experience levels.  
Someone installing Ubuntu for the first time should be able to follow this without stress.  
Someone experienced should be able to skim the headings and still know exactly what the installer will do.

It also helps **future me** — who will inevitably revisit this and ask,
“Why did I set it up like this?”

This section is here so I don’t have to make eye contact with myself while answering.

---

## Next Steps
With the operating system installed, the VM is now ready for post-install configuration, hardening, and service deployment. 


---

## Recipe Building
This guide forms the **Base Operating System** component for recipe building.  
