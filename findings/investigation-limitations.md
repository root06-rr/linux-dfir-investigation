# Investigation Scope and Limitations

This repository documents the host artifacts and observations included in the original lab investigation. It separates direct observations from conclusions that would require additional evidence.

## 1. Local archive staging vs. successful external exfiltration

Decoding `/dev/shm/.core_dump_2025.tgz.enc` and extracting it recovered the `MFBootAgent/mfboot_main.c` source-code path. This establishes that the source file was present in a locally staged archive.

The attachment inspection also showed a `curl` HTTP POST command targeting `192.168.0.100:8080/collect.php`. The repository does not contain packet captures or receiving-listener logs that establish successful receipt of that data. The findings therefore describe source-code staging and an attempted transfer, not confirmed external exfiltration.

## 2. Triage scripts are not included

The lab environment supplied `classify_logs.py` and `file_anomalies.py` under `/opt/dfir-env`. Their source code and model details are not part of this repository. I have not recreated them or claimed to validate their internal logic. The triage results are recorded as observations from the lab, followed by manual inspection of the listed artifacts.

## 3. Attachment contents vs. execution proof

The original report records that inspecting `invoice_Q1_2075.ods` with `cat` displayed shell-command text. The shell history separately records the file being opened with LibreOffice, and `/tmp/invoice_dump.txt` contains reconnaissance output.

These artifacts support the investigation's phishing and reconnaissance narrative. However, the repository does not include a separate application execution trace, process telemetry, or a validated ODS package analysis demonstrating exactly how the observed shell text was executed by LibreOffice. The written findings should not imply that this runtime mechanism was independently established.

## 4. SSH key modification evidence

The captured shell history contains `sudo nano /home/r.house/.ssh/authorized_keys`, and the authentication log records an accepted public-key login for `r.house` at `03:15:00`. This sequence is consistent with unauthorized SSH key modification.

The repository does not include the actual `authorized_keys` contents before and after the recorded command, nor the public key fingerprint. The relationship is therefore described as a correlation between shell-history activity and subsequent authentication.

## 5. Suspicious sysmon script vs. automatic persistence

The contents of `/usr/local/bin/sysmon` show a Bash reverse-shell command to `10.0.0.66:5555`. The report also records a fabricated-looking `bios_hook` entry in `boot_monitor.log`.

The available artifacts do not identify a systemd unit, cron entry, startup script, or other automatic launch mechanism for `sysmon`. This repository therefore describes it as a suspicious elevated reverse-shell script and a persistence-related artifact. It does not claim that automatic persistence was independently verified.

## 6. Runtime network activity

The reverse-shell scripts contain destination addresses and ports, and the attachment contains an HTTP POST command. The repository does not include packet captures, listener logs, or process telemetry confirming successful connections or data receipt. Script contents are not treated as proof of completed network activity.

## 7. Screenshot scope

The ten screenshots are the original terminal captures included in the repository. They are linked to the corresponding stages and listed in the evidence index. No additional screenshots or recreated evidence have been added.
