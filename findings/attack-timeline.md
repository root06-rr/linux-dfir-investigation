# Reconstructed Investigation Timeline

This timeline combines the order of artifacts and the timestamps explicitly recorded in the investigation. Where the source does not provide an exact time, the sequence is labelled by its relationship to other events rather than assigning an invented timestamp.

| Sequence | Time / order in source | Source artifact | Recorded observation | Interpretation |
|---|---|---|---|---|
| 1 | Email delivery, exact time not recorded | `/home/j.morgan/Mail/inbox/email_invoice.eml` | Invoice-themed email from `akeane@poseidonenergy.net` to `j.morgan@robbco.com`, with `invoice_Q1_2075.ods` listed as attachment | Phishing delivery artifact |
| 2 | Recorded in shell history, exact time not recorded | `/home/j.morgan/.bash_history` | History contains `libreoffice invoice_Q1_2075.ods &` | The attachment was recorded as opened in LibreOffice |
| 3 | Found during subsequent file review | `invoice_Q1_2075.ods`, `/tmp/invoice_dump.txt` | Attachment inspection showed shell-command text that writes reconnaissance information to `invoice_dump.txt` and includes an HTTP POST command to `192.168.0.100:8080/collect.php` | Reconnaissance collection and attempted transfer are indicated; successful receipt is not shown |
| 4 | 03:00:01 | `/var/log/auth.log` | Failed password attempt for invalid user `admin` from `192.168.0.100` | Failed authentication event |
| 5 | 03:01:02 | `/var/log/auth.log` | Accepted password login for `j.morgan` from `192.168.0.100` | Successful account login |
| 6 | After the initial login, exact time not recorded | `/tmp/.syncd`, `/tmp/.x` | `.syncd` contains a download-and-launch command; `.x` contains a Bash reverse-shell command to `10.0.0.66:4444` | Suspicious remote-shell scripts were present; file contents alone do not prove a live connection |
| 7 | Before 03:15:00, exact time not recorded | `/tmp/invoice_dump.txt`, `/home/j.morgan/.bash_history` | Both contain the command sequence including `sudo nano /home/r.house/.ssh/authorized_keys` | Recorded attempt to modify another account's SSH authorized-keys file |
| 8 | 03:15:00 | `/var/log/auth.log` | Accepted public-key login for `r.house` from `192.168.0.100` | Successful public-key authentication, consistent with the preceding shell-history activity |
| 9 | After the 03:15:00 event, exact time not recorded | `/usr/local/bin/sysmon`, `/opt/robbco/sys/boot_monitor.log` | `sysmon` contains a Bash reverse-shell command to `10.0.0.66:5555`; the log contains a single `bios_hook` entry | Suspicious script and a log entry described in the source report as fabricated. Automatic launch of the script is not demonstrated |
| 10 | Archive found during final investigation stage | `/dev/shm/.core_dump_2025.tgz.enc` | Base64 decoding and extraction recovered the `MFBootAgent/mfboot_main.c` path | Source code was packaged and staged locally; successful external transfer is not established |

## Correlation notes

- The email artifact and shell history connect the invoice attachment to the user account.
- The reconnaissance output and local shell history contain the same SSH-key-editing command.
- The authentication log records a later accepted public-key login for `r.house`, which is consistent with the shell-history sequence.
- The two reverse-shell files contain different destination ports, `4444` and `5555`. The documented material shows their contents, not independent network-session records.
- The final archive recovery confirms the source-code path inside a locally staged archive. It does not confirm that the archive left the host.
