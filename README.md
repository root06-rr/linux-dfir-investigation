# Linux DFIR Investigation: Phishing, SSH Persistence & Source-Code Staging

## Project Overview
This repository documents an end-to-end Digital Forensics and Incident Response (DFIR) investigation conducted on a compromised Linux system belonging to **RobbCo** inside an isolated lab environment. Starting from ML-assisted authentication log triage and filesystem anomaly flags, I manually traced the intrusion across ten investigative stages—correlating authentication logs, staged temporary files, a malicious spreadsheet payload, local email records, reverse-shell scripts, shell command history, unauthorized SSH key injection, persistence masquerading, and an encoded archive staged in shared memory.

## Investigation Scenario & Objectives
Following suspected unauthorized access on a RobbCo Linux host, I conducted a forensic investigation to:
1. Verify whether unauthorized access occurred and identify the initial access vector.
2. Trace post-exploitation activity, privilege escalation, and persistence mechanisms.
3. Determine whether proprietary engineering source code (**RETROS BIOS**, **MF Boot Agent**, and **Unified Operating System**) had been accessed or staged for exfiltration.
4. Preserve findings, commands, and visual evidence in a reproducible, forensically accurate structure.

## Reconstructed Intrusion Sequence
1. **Initial Access:** A spear-phishing email (`email_invoice.eml`) from `akeane@poseidonenergy.net` delivered an invoice attachment (`invoice_Q1_2075.ods`) to `j.morgan@robbco.com`.
2. **Execution & Reconnaissance:** Opening `invoice_Q1_2075.ods` triggered an embedded script that harvested local user accounts, active sessions, SSH configurations, and `.bash_history` into `/tmp/invoice_dump.txt` and attempted an HTTP POST transfer to `192.168.0.100:8080/collect.php`.
3. **Initial Remote Access:** Hidden files in `/tmp` (`.syncd` and `.x`) downloaded and executed a Bash reverse shell connecting to `10.0.0.66:4444` under `j.morgan`.
4. **Privilege Escalation & SSH Account Access:** Shell history confirmed the attacker leveraged `j.morgan`'s `sudo` permissions with `nano` to append an unauthorized public key into `/home/r.house/.ssh/authorized_keys`, enabling an SSH public-key login as `r.house` at `03:15:00`.
5. **Elevated Persistence & Masquerading:** Under administrative privileges, the attacker placed a root reverse-shell script at `/usr/local/bin/sysmon` (`10.0.0.66:5555`) and created a fabricated log entry in `/opt/robbco/sys/boot_monitor.log` to disguise its purpose.
6. **Source-Code Targeting & Staging:** Proprietary source code in `/opt/robbco/engineering/MFBootAgent/mfboot_main.c` was accessed, compressed, and Base64-encoded into `/dev/shm/.core_dump_2025.tgz.enc`.
7. **Archive Recovery:** I Base64-decoded and extracted `/dev/shm/.core_dump_2025.tgz.enc` into `/tmp/stolen_source`, confirming the staged engineering files.

## Repository Navigation
* **[`investigation/`](investigation/)**: Ten chronological stage reports from initial triage (`01-initial-triage.md`) to archive recovery (`10-archive-recovery.md`), each linked directly to its corresponding terminal screenshot.
* **[`evidence/evidence-index.md`](evidence/evidence-index.md)**: Complete inventory of all ten investigation screenshots mapped to stages and artifacts.
* **[`commands/`](commands/)**: Structured reference of the Linux forensic and archive-recovery commands executed during the investigation.
* **[`findings/`](findings/)**: Correlated attack timeline, key findings, security hardening recommendations, and explicit scope limitations.
