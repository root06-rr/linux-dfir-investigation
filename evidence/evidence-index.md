# Forensic Evidence & Screenshot Index

All ten terminal screenshots captured during the investigation are stored in `evidence/screenshots/` and linked directly within their corresponding stage files in `investigation/`.

| Stage | Screenshot File | Primary Artifact(s) Shown | What the Capture Verifies |
| :--- | :--- | :--- | :--- |
| **01** | `screenshots/01_initial_triage_ml_logs.png` | `/var/log/auth.log`, `classify_logs.py`, `file_anomalies.py` | Virtual environment activation, `03:00:01`–`03:15:00` SSH events from `192.168.0.100`, and 9 flagged files |
| **02** | `screenshots/02_tmp_directory_inspection.png` | `/tmp/dock-replace.log`, `/tmp/invoice_dump.txt` | Directory listing of `/tmp` showing staged non-system files |
| **03** | `screenshots/03_invoice_dump_recon.png` | `/tmp/invoice_dump.txt` | Formatted reconnaissance output enumerating local users and captured `.bash_history` |
| **04** | `screenshots/04_phishing_ods_payload.png` | `/home/j.morgan/Documents/Invoices/invoice_Q1_2075.ods` | Embedded shell reconnaissance commands and `curl` POST to `192.168.0.100:8080/collect.php` |
| **05** | `screenshots/05_phishing_email_eml.png` | `/home/j.morgan/Mail/inbox/email_invoice.eml` | Phishing email headers (`akeane@poseidonenergy.net` -> `j.morgan@robbco.com`) and invoice lure |
| **06** | `screenshots/06_hidden_dropper_reverse_shell.png` | `/tmp/.syncd`, `/tmp/.x` | Hidden dropper fetching `10.0.0.66/payload.sh` and interactive reverse shell to `10.0.0.66:4444` |
| **07** | `screenshots/07_bash_history_sudo_ssh.png` | `/home/j.morgan/.bash_history` | Authentic shell history confirming `sudo nano /home/r.house/.ssh/authorized_keys` |
| **08** | `screenshots/08_sysmon_persistence_backdoor.png` | `/usr/local/bin/sysmon` | Masqueraded script containing root reverse shell to `10.0.0.66:5555` |
| **09** | `screenshots/09_fake_boot_log_source_code.png` | `/opt/robbco/sys/boot_monitor.log`, `/opt/robbco/engineering/MFBootAgent/mfboot_main.c` | Fabricated `bios_hook` log entry and proprietary `MFBootAgent` C source file |
| **10** | `screenshots/10_shm_archive_recovery.png` | `/dev/shm/.core_dump_2025.tgz.enc` | Base64 decoding and `tar` extraction of `opt/robbco/engineering/MFBootAgent/mfboot_main.c` |
