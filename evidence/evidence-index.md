# Forensic Evidence and Screenshot Index

The repository contains ten original terminal screenshots. Each has a stable documentation reference (E-01 to E-10), is embedded in its matching investigation stage, and is cross-referenced in the [screenshot evidence register](screenshot-evidence-register.md).

| Evidence ID | Stage | Investigation | Screenshot | What it supports |
|---|---:|---|---|---|
| E-01 | 01 | [Open stage 01](../investigation/01-initial-triage.md) | [View screenshot](screenshots/01_initial_triage_ml_logs.png) | Authentication events and anomaly-triage output |
| E-02 | 02 | [Open stage 02](../investigation/02-temporary-files.md) | [View screenshot](screenshots/02_tmp_directory_inspection.png) | Presence of dock-replace.log and invoice_dump.txt in /tmp |
| E-03 | 03 | [Open stage 03](../investigation/03-reconnaissance.md) | [View screenshot](screenshots/03_invoice_dump_recon.png) | User enumeration and captured command-history text |
| E-04 | 04 | [Open stage 04](../investigation/04-phishing-analysis.md) | [View screenshot](screenshots/04_phishing_ods_payload.png) | Shell-command text observed in the attachment, including the output path and HTTP POST command |
| E-05 | 05 | [Open stage 05](../investigation/05-email-investigation.md) | [View screenshot](screenshots/05_phishing_email_eml.png) | Email headers, lure text, and attachment name |
| E-06 | 06 | [Open stage 06](../investigation/06-reverse-shell-analysis.md) | [View screenshot](screenshots/06_hidden_dropper_reverse_shell.png) | Dropper and reverse-shell script contents |
| E-07 | 07 | [Open stage 07](../investigation/07-privilege-escalation.md) | [View screenshot](screenshots/07_bash_history_sudo_ssh.png) | Recorded sudo command targeting r.house's authorized_keys file |
| E-08 | 08 | [Open stage 08](../investigation/08-ssh-persistence.md) | [View screenshot](screenshots/08_sysmon_persistence_backdoor.png) | Reverse-shell command inside /usr/local/bin/sysmon |
| E-09 | 09 | [Open stage 09](../investigation/09-source-code-access.md) | [View screenshot](screenshots/09_fake_boot_log_source_code.png) | Boot-log entry and readable mfboot_main.c source file |
| E-10 | 10 | [Open stage 10](../investigation/10-archive-recovery.md) | [View screenshot](screenshots/10_shm_archive_recovery.png) | Encoded archive and recovered source-code path |

## How to review an evidence item

1. Open the investigation stage for its objective, commands, observations, and interpretation.
2. Review the embedded screenshot and caption.
3. Use the evidence register to check the specific claim the image supports and its limitations.
4. Compare related evidence IDs when a finding depends on more than one artifact.

The screenshots are the original terminal captures. E-01 to E-10 are documentation labels, not original forensic acquisition IDs. No acquisition timestamps, hashes, or chain-of-custody details are claimed.
