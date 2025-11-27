# Ubuntu Server Post‑Installation Configuration
A clean, predictable baseline for homelab Ubuntu servers.  
This guide focuses on practical, low-noise, low-maintenance configuration — enough hardening to avoid silly problems without turning your homelab into a CIS-Level-4000 compliance nightmare.

---

## Before You Begin
This guide assumes you have completed the **Ubuntu Server Installation** guide from the repo and are now ready to apply a clean, consistent post-install baseline.

---

# System Updates

Before doing anything else, update the system.  
Fresh installs often have several pending updates, and applying them now avoids troubleshooting issues that patches would have already solved.

Refresh package lists and install all pending updates:

```bash
sudo apt-get update && sudo apt-get upgrade -y
```

This command does two things in sequence:

- `apt-get update` refreshes the package list so the system knows about the latest available versions.
- `apt-get upgrade -y` installs all available updates, and the `-y` flag pre-approves the changes so you're not prompted to confirm each one.

Chaining them with `&&` ensures the upgrade only runs if the update step completes successfully — a simple safety check that avoids half-completed operations.

---

## Enable Unattended Security Updates

Enable Ubuntu’s unattended security updates to keep the system patched automatically:

```bash
sudo apt-get install unattended-upgrades
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

This enables **security-only** automatic updates, which is the safest and most predictable approach for a homelab server.

### Optional: Update Strategy Tuning

If you want finer control, Ubuntu allows adjusting the update behaviour:

- **Security-only (default):** applies critical security patches automatically  
- **Critical-only:** restrict updates to high-severity items  
- **Deferred updates:** delay non-critical updates for stability  
- **Manual full updates:** suitable if you snapshot before patching or maintain a change window  

For most homelab systems, the default **security-only unattended updates** is ideal.

---

# Install btop

A lightweight, real-time system monitor that helps you understand what the machine is doing during configuration or troubleshooting.

```bash
sudo apt-get install btop
```

---

# Configure Audit Logging

Audit logging provides lightweight visibility into key system events.

Install and enable the audit daemon:

```bash
sudo apt-get install auditd
sudo systemctl enable --now auditd
```

The default rule set is fine for a homelab server.

---

# Systemd Journal Retention Controls

Prevent `journald` from consuming excessive disk space.

Create directory:

```bash
sudo mkdir -p /etc/systemd/journald.conf.d
```

Create retention config:

```bash
sudo nano /etc/systemd/journald.conf.d/size.conf
```

Add:

```
[Journal]
SystemMaxUse=200M
SystemMaxFileSize=50M
```

Apply changes:

```bash
sudo systemctl restart systemd-journald
journalctl --disk-usage
```

---

# Kernel Hardening (sysctl)

Apply a small set of safe, high-value network and kernel protections.

Open or create the file:

```bash
sudo nano /etc/sysctl.d/99-hardening.conf
```

Add:

```
net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.all.rp_filter = 1
kernel.kptr_restrict = 2
```

Apply:

```bash
sudo sysctl --system
```

---

# Summary Table for sysctl

| Setting | Purpose | Protection |
|--------|----------|------------|
| accept_source_route=0 | Block source-routed packets | Prevent path manipulation |
| accept_redirects=0 | Ignore ICMP redirects | Prevent rogue gateway attacks |
| send_redirects=0 | Stop sending redirects | Avoid routing interference |
| rp_filter=1 | Reverse-path validation | Blocks IP spoofing |
| kptr_restrict=2 | Hide kernel pointer addresses | Reduces exploitability |

---

# Reboot to Apply Everything

Some changes (especially kernel-level updates, sysctl behaviour, and security upgrades) apply immediately, but others take effect only after a reboot.

```bash
sudo reboot
```

A clean reboot at this stage ensures the system is running with all updated components, correct kernel modules, and fresh configuration.

---

# Next Steps

Your server now has:

- current packages  
- automated security updates  
- predictable logging behaviour  
- capped journal retention  
- active audit logging  
- hardened networking defaults  

It's ready for the next module — whether you're installing Docker, configuring SSH access, setting up monitoring, or deploying an internal service.

Now, go build something on top of it. Or don't. Reboots are great excuses to make a cup of coffee and pretend you're "waiting on systems". Everyone's done it at least once.  

---

# Rationale ("Why This Way")

### Updating First
Ubuntu images age quickly — even an ISO that's 'recent' can already be behind on security fixes and bug patches.  
Updating immediately gives you:

- a known-good starting point  
- consistent behaviour across deployments  
- reduced troubleshooting (no chasing issues that were fixed weeks ago)

It's like wiping the whiteboard before starting a new design: clean slate, no ghosts.

### Security-Only Auto Updates
Full unattended updates can be unpredictable.  
Security-only updates give you the important patches without suddenly pulling in higher-risk changes like major package upgrades.

This strikes a balance:

- keeps vulnerabilities closed  
- keeps behaviour stable  
- gives you control of when full updates happen (usually after a snapshot or planned window)

It's the 'sensible adult' setting for homelabs.

### btop
Linux gives you `top` and `htop`, but `btop` is far clearer, faster to read, and extremely helpful during early setup:

- CPU, RAM, disk, and network IO at a glance  
- great for spotting misbehaving services  
- ideal for verifying behaviour on lightweight VMs

It's the difference between 'technically usable' and 'actually helpful.'

### auditd
`auditd` provides a low-noise way to track security-relevant events:

- logins and authentication attempts  
- file access modifications  
- configuration changes  
- privilege escalation activity  

That's incredibly useful later when something changes and you need to know who did what and when — without enabling heavyweight monitoring.

You get some accountability without the overhead of a full SIEM.

### journald Caps
Ubuntu will quite happily let logs balloon until the disk is full — I've personally been bitten by this more times than I'd like to admit.
I'd have Docker containers suddenly stop for “no reason,” only to find `/` completely full because journald had eaten the entire OS disk and the system couldn't breathe.

If you've ever stared at a dead container wondering why "nothing works and everything is lying to me", this might just stop that happening in future.

Servers with small OS disks (16–32GB) are masters at hitting that wall with zero warning.

Setting retention caps ensures:

- logs never consume the entire disk  
- you always keep a sensible amount of history  
- you avoid the classic "system won't boot because `/var` is full"

Think of it as child-proofing your server from itself.

### sysctl Hardening
A small set of network and kernel-level protections give large security benefits:

- blocking redirected or source-routed packets  
- preventing spoofed traffic  
- stopping the server from broadcasting unnecessary network information  
- hiding kernel pointers from userland  

They don't change how your server behaves day-to-day — they just quietly remove attack surfaces that no modern system should have open.

---

# Recipe Building

This guide forms the **Post‑Installation Configuration** component for recipe building.  

---
