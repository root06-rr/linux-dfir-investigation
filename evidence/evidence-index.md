# Forensic Evidence and Screenshot Index

The repository contains ten terminal screenshots from the original investigation. Each image is linked directly from its corresponding stage file. This index provides a second route from an artifact or finding to the relevant stage and screenshot.

| Stage | Investigation | Screenshot | Main artifact(s) shown |
|---|---|---|---|
| 01 | [Initial triage](../investigation/01-initial-triage.md) | [01_initial_triage_ml_logs.png](screenshots/01_initial_triage_ml_logs.png) | Authentication-log triage, `classify_logs.py`, `file_anomalies.py` |
| 02 | [Temporary files](../investigation/02-temporary-files.md) | [02_tmp_directory_inspection.png](screenshots/02_tmp_directory_inspection.png) | `/tmp/dock-replace.log`, `/tmp/invoice_dump.txt` |
| 03 | [Reconnaissance](../investigation/03-reconnaissance.md) | [03_invoice_dump_recon.png](screenshots/03_invoice_dump_recon.png) | `/tmp/invoice_dump.txt`, usernames, captured shell history |
| 04 | [Attachment analysis](../investigation/04-phishing-analysis.md) | [04_phishing_ods_payload.png](screenshots/04_phishing_ods_payload.png) | Raw contents observed in `invoice_Q1_2075.ods` |
| 05 | [Email investigation](../investigation/05-email-investigation.md) | [05_phishing_email_eml.png](screenshots/05_phishing_email_eml.png) | `email_invoice.eml`, sender, recipient, subject, attachment |
| 06 | [Reverse-shell analysis](../investigation/06-reverse-shell-analysis.md) | [06_hidden_dropper_reverse_shell.png](screenshots/06_hidden_dropper_reverse_shell.png) | `/tmp/.syncd`, `/tmp/.x` |
| 07 | [Privilege escalation review](../investigation/07-privilege-escalation.md) | [07_bash_history_sudo_ssh.png](screenshots/07_bash_history_sudo_ssh.png) | `/home/j.morgan/.bash_history` |
| 08 | [Suspicious sysmon script](../investigation/08-ssh-persistence.md) | [08_sysmon_persistence_backdoor.png](screenshots/08_sysmon_persistence_backdoor.png) | `/usr/local/bin/sysmon` |
| 09 | [Source-code access](../investigation/09-source-code-access.md) | [09_fake_boot_log_source_code.png](screenshots/09_fake_boot_log_source_code.png) | `boot_monitor.log`, `mfboot_main.c` |
| 10 | [Archive recovery](../investigation/10-archive-recovery.md) | [10_shm_archive_recovery.png](screenshots/10_shm_archive_recovery.png) | `/dev/shm/.core_dump_2025.tgz.enc`, decoded archive paths |

## How to use this index

1. Select the investigation stage relevant to the artifact.
2. Open the stage report to read the objective, commands, observations, and interpretation.
3. Open the screenshot link to view the corresponding terminal capture.

The screenshot filenames and images are retained from the existing repository. No replacement or recreated evidence images have been added.
