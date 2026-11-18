# Screenshot Evidence Register

## Purpose

I use this register to connect each original terminal screenshot to the investigation stage and the specific observation it supports. E-01 to E-10 are documentation references, not original forensic acquisition IDs.

| Evidence ID | Screenshot | Stage | Observation supported | Evidence boundary |
|---|---|---|---|---|
| E-01 | [01_initial_triage_ml_logs.png](screenshots/01_initial_triage_ml_logs.png) | [Stage 01](../investigation/01-initial-triage.md) | Authentication events and anomaly-triage output | The displayed triage output does not expose the scripts' internal detection logic. |
| E-02 | [02_tmp_directory_inspection.png](screenshots/02_tmp_directory_inspection.png) | [Stage 02](../investigation/02-temporary-files.md) | Presence of dock-replace.log and invoice_dump.txt in /tmp | A listing does not identify who created the files or prove execution or transfer. |
| E-03 | [03_invoice_dump_recon.png](screenshots/03_invoice_dump_recon.png) | [Stage 03](../investigation/03-reconnaissance.md) | User enumeration and captured command-history text | Captured output does not prove every listed command completed. |
| E-04 | [04_phishing_ods_payload.png](screenshots/04_phishing_ods_payload.png) | [Stage 04](../investigation/04-phishing-analysis.md) | Shell-command text observed in the attachment, including the output path and HTTP POST command | Does not prove the LibreOffice execution mechanism or successful HTTP receipt. |
| E-05 | [05_phishing_email_eml.png](screenshots/05_phishing_email_eml.png) | [Stage 05](../investigation/05-email-investigation.md) | Email headers, lure text, and attachment name | Does not by itself prove the recipient opened the attachment. |
| E-06 | [06_hidden_dropper_reverse_shell.png](screenshots/06_hidden_dropper_reverse_shell.png) | [Stage 06](../investigation/06-reverse-shell-analysis.md) | Dropper and reverse-shell script contents | Script contents do not prove download, launch, or network connection completed. |
| E-07 | [07_bash_history_sudo_ssh.png](screenshots/07_bash_history_sudo_ssh.png) | [Stage 07](../investigation/07-privilege-escalation.md) | Recorded sudo command targeting r.house's authorized_keys file | Before-and-after key contents and the key fingerprint are not included. |
| E-08 | [08_sysmon_persistence_backdoor.png](screenshots/08_sysmon_persistence_backdoor.png) | [Stage 08](../investigation/08-ssh-persistence.md) | Reverse-shell command inside /usr/local/bin/sysmon | Does not identify an automatic launch mechanism or prove a live connection. |
| E-09 | [09_fake_boot_log_source_code.png](screenshots/09_fake_boot_log_source_code.png) | [Stage 09](../investigation/09-source-code-access.md) | Boot-log entry and readable mfboot_main.c source file | Does not independently establish who created the boot-log entry. |
| E-10 | [10_shm_archive_recovery.png](screenshots/10_shm_archive_recovery.png) | [Stage 10](../investigation/10-archive-recovery.md) | Encoded archive and recovered source-code path | Establishes local staging, not external transmission. |

## Evidence handling notes

- These are the ten original terminal screenshots already supplied with the investigation.
- Each image is linked from its corresponding stage report and the [evidence index](evidence-index.md).
- The evidence IDs are organizational labels. They do not imply a formal acquisition process.
- No file hashes, acquisition timestamps, original device metadata, or chain-of-custody records are claimed because those details are not present in the source material.
- A screenshot documents what was displayed during the investigation. It should be read with the associated artifact description and limitations. It does not automatically prove process execution, successful network communication, or external data receipt.
