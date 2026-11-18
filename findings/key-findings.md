# Key Forensic Findings

The findings below are based on the artifacts described in the ten investigation stages. Where a conclusion relies on correlating separate artifacts, that relationship is stated explicitly.

## 1. Phishing-related email and attachment

The local email artifact `email_invoice.eml` records an invoice-themed message from `akeane@poseidonenergy.net` to `j.morgan@robbco.com`, with `invoice_Q1_2075.ods` listed as the attachment. The user's shell history records the attachment being opened in LibreOffice.

Inspection of the attachment with `cat` displayed shell-command text that writes reconnaissance information to `/tmp/invoice_dump.txt` and includes an HTTP POST command. The available evidence does not independently demonstrate the exact application execution mechanism or successful receipt of the POST.

## 2. Authentication events

The authentication-log triage recorded:
- `03:00:01`: failed password attempt for invalid user `admin` from `192.168.0.100`.
- `03:01:02`: accepted password login for `j.morgan` from `192.168.0.100`.
- `03:15:00`: accepted public-key login for `r.house` from `192.168.0.100`.

These events provide the timestamped authentication sequence used in the investigation.

## 3. Reconnaissance and shell-history correlation

`/tmp/invoice_dump.txt` contains enumerated usernames and a captured shell-history block. The same command sequence appears in `/home/j.morgan/.bash_history`, including `sudo nano /home/r.house/.ssh/authorized_keys`. The subsequent accepted public-key login for `r.house` is consistent with this activity. The key-file contents and fingerprint are not included in the repository.

## 4. Suspicious reverse-shell scripts

The hidden `/tmp/.syncd` script contains a command to download `payload.sh` from `10.0.0.66`, save it as `/tmp/.x`, mark it executable, and run it. The inspected `.x` file contains a Bash reverse-shell command targeting `10.0.0.66:4444`.

The file `/usr/local/bin/sysmon` contains a second Bash reverse-shell command targeting `10.0.0.66:5555`. These observations establish the contents of the scripts, not successful live connections. The available evidence does not show how `sysmon` was automatically launched, if it was.

## 5. Suspicious log entry and source-code access

The investigation recorded a single `bios_hook` entry in `/opt/robbco/sys/boot_monitor.log`, described in the original report as fabricated. The engineering file `/opt/robbco/engineering/MFBootAgent/mfboot_main.c` was present and readable during the investigation and referenced `RETROS-52EE5` and `UOS-2.3.0`.

## 6. Source-code archive staging

The hidden file `/dev/shm/.core_dump_2025.tgz.enc` contained Base64-encoded data. Decoding and extracting it recovered the `opt/robbco/engineering/MFBootAgent/mfboot_main.c` path. This is evidence of local source-code staging. It does not independently prove successful external exfiltration.
