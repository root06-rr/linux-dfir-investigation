# Reconstructed Intrusion Timeline

| Sequence | Timestamp / Order | Source Artifact | Event Description | Attacker Objective |
| :--- | :--- | :--- | :--- | :--- |
| **1** | Pre-Execution | `/home/j.morgan/Mail/inbox/email_invoice.eml` | Spear-phishing email sent from `akeane@poseidonenergy.net` to `j.morgan@robbco.com` with subject `URGENT - Outstanding Invoice Q1 2075` and attachment `invoice_Q1_2075.ods` | Initial Access |
| **2** | Post-Delivery | `/home/j.morgan/.bash_history` | User `j.morgan` navigated to `~/Documents/Invoices/` and opened `invoice_Q1_2075.ods` in LibreOffice | Execution |
| **3** | Post-Execution | `/tmp/invoice_dump.txt`, `invoice_Q1_2075.ods` | Embedded script collected `/etc/passwd` users, `who` sessions, SSH config, and `.bash_history` into `/tmp/invoice_dump.txt` and attempted HTTP POST to `http://192.168.0.100:8080/collect.php` | Local Discovery & Staging |
| **4** | `03:00:01` | `/var/log/auth.log` | Failed SSH password login for invalid user `admin` from `192.168.0.100` | Account Probing |
| **5** | `03:01:02` | `/var/log/auth.log` | Accepted SSH password login for `j.morgan` from `192.168.0.100` | Remote Access |
| **6** | Post-Access | `/tmp/.syncd`, `/tmp/.x` | Hidden dropper `.syncd` downloaded `http://10.0.0.66/payload.sh` to `/tmp/.x`, launching an interactive Bash reverse shell to `10.0.0.66:4444` | Unprivileged C2 |
| **7** | Prior to `03:15:00` | `/home/j.morgan/.bash_history` | Attacker inspected `.ssh/config` and `/etc/motd`, then ran `sudo nano /home/r.house/.ssh/authorized_keys` to inject an unauthorized SSH public key | Privilege Escalation |
| **8** | `03:15:00` | `/var/log/auth.log` | Accepted SSH public-key login for privileged user `r.house` from `192.168.0.100` | Administrative Access |
| **9** | Post-Escalation | `/usr/local/bin/sysmon`, `/opt/robbco/sys/boot_monitor.log` | Attacker planted a root Bash reverse shell at `/usr/local/bin/sysmon` (`10.0.0.66:5555`) and created a fabricated `bios_hook` entry in `boot_monitor.log` | Persistence & Masquerading |
| **10** | Post-Escalation | `/dev/shm/.core_dump_2025.tgz.enc` | Proprietary source code (`/opt/robbco/engineering/MFBootAgent/mfboot_main.c`) was archived, Base64-encoded, and staged in `/dev/shm` | Source-Code Staging |
