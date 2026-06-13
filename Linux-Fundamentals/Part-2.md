# 🐧 Linux Fundamentals: Part 2 (Self-Guided Lab)

This document records my self-guided laboratory session on Linux security controls, file privileges, and system log auditing.

---

## 🔐 1. File Permissions (`chmod`)
Linux manages security using a three-tier permission model for **User (u)**, **Group (g)**, and **Others (o)**.

### Numerical (Octal) Method
Permissions are calculated using numerical weights: **Read (4)**, **Write (2)**, and **Execute (1)**.
* `chmod 600 topsecret.txt` -> Sets `-rw-------` (Only the Owner can read and write).
* `chmod 777 hack.sh` -> Sets `-rwxrwxrwx` (Full access to everyone - *Nuclear Option*).

### Symbolic Method
Uses characters to add (`+`) or remove (`-`) privileges.
* `chmod +x hack.sh` -> Grants execution power to all users (`a+x`).
* `chmod u+x hack.sh` -> Grants execution power strictly to the **Owner only**.

---

## 👑 2. File Ownership (`chown`)
Controls which account owns the file and has structural authority over it.
* **Change Owner:** `sudo chown root hack.sh` (Transfers ownership to the system administrator).
* **Change User & Group:** `sudo chown root:root hack.sh` (Changes both domains simultaneously).
* **Revert Ownership:** `sudo chown kali:kali hack.sh` (Restores control back to the standard user).

---

## 🔍 3. System Log Auditing & Filtering
Modern Linux systems utilize `systemd-journald` for central monitoring instead of the traditional legacy `auth.log`.

### Overcoming Log Noise (Real-world Scenario)
High-volume applications (like Cloudflare WARP service logs) can flood the terminal. To isolate relevant security operations, specific query filters must be combined with the `grep` pipeline.

* **Targeted Query (Time-bound Filter):**
  ```bash
  sudo journalctl --since "today" | grep chown
