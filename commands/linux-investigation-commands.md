# Linux Forensic Investigation Command Reference

This reference catalogs the exact Linux commands executed across Stages 01–09, organized by investigative purpose.

## 1. Environment Activation & Initial Triage (Stage 01)
```bash
# Activate isolated Python virtual environment for forensic triage
source /opt/dfir-env/bin/activate
```
* **Purpose:** Isolates forensic analysis dependencies from the host environment.

## 2. Filesystem & Hidden Artifact Discovery (Stages 02, 06, 08, 09)
```bash
# List visible files in /tmp
cd /tmp && ls

# List all files including hidden dot-files, permissions, owners, and timestamps
ls -la /tmp
ls -la /home/j.morgan
ls -la /usr/local/bin
ls -la /opt/robbco/sys
ls -la /opt/robbco/engineering/MFBootAgent
```
* **Purpose:** Uncovers hidden scripts (`.syncd`, `.x`), masqueraded binaries (`/usr/local/bin/sysmon`), and recent file modification timestamps.

## 3. Artifact Inspection & Output Formatting (Stages 03, 04, 05, 07, 08, 09)
```bash
# Format wide reconnaissance output cleanly to terminal width
cat /tmp/invoice_dump.txt | column -c $(tput cols)

# Inspect suspicious spreadsheet payload and phishing email source
cat /home/j.morgan/Documents/Invoices/invoice_Q1_2075.ods
cat /home/j.morgan/Mail/inbox/email_invoice.eml

# Inspect hidden scripts, user shell history, and masqueraded persistence files
cat /tmp/.syncd
cat /tmp/.x
cat /home/j.morgan/.bash_history
cat /usr/local/bin/sysmon
cat /opt/robbco/sys/boot_monitor.log
cat /opt/robbco/engineering/MFBootAgent/mfboot_main.c
```
* **Purpose:** Performs direct content verification without triggering script execution.
