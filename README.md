# Linux DFIR Investigation: Phishing, SSH Access & Source-Code Staging

## Project overview

I investigated a suspected compromise of a Linux system belonging to RobbCo in an isolated TryHackMe lab. I used the available authentication-log and file-anomaly triage scripts to identify areas for review, then manually examined the host artifacts and correlated them across ten investigation stages.

The investigation follows the evidence from an invoice-themed email and suspicious attachment through reconnaissance files, reverse-shell scripts, shell history, SSH account access, a suspicious script in `/usr/local/bin`, source-code access, and recovery of a Base64-encoded archive from `/dev/shm`.

This repository documents what I examined, the commands recorded in the investigation, what I observed, and what the available evidence does and does not establish.

## Investigation objectives

1. Review authentication activity and identify suspicious files.
2. Trace the phishing-related artifacts and reconnaissance output.
3. Correlate shell history with the SSH authentication events.
4. Examine suspicious scripts and account-access artifacts.
5. Determine what source-code material was present and recoverable from the staged archive.
6. Record limitations where the available host artifacts do not prove execution or successful external transfer.

## Investigation workflow

```text
Initial triage
     |
     v
Temporary files and reconnaissance output
     |
     v
Suspicious attachment and email review
     |
     v
Dropper and reverse-shell script review
     |
     v
Shell history and SSH account-access correlation
     |
     v
Suspicious sysmon script and source-code review
     |
     v
Base64 archive recovery
```

## Reconstructed sequence

1. **Email delivery:** The local mail artifact `email_invoice.eml` records an invoice-themed message from `akeane@poseidonenergy.net` to `j.morgan@robbco.com`, with `invoice_Q1_2075.ods` listed as the attachment.
2. **Attachment and reconnaissance artifacts:** The shell history records the spreadsheet being opened in LibreOffice. The attachment's inspected contents include commands that write reconnaissance information to `/tmp/invoice_dump.txt` and an HTTP POST command targeting `192.168.0.100:8080/collect.php`. The available evidence does not include listener logs or packet captures proving that the POST succeeded.
3. **Authentication and remote-shell artifacts:** Authentication-log triage identified a failed login for invalid user `admin` at `03:00:01`, an accepted password login for `j.morgan` at `03:01:02`, and an accepted public-key login for `r.house` at `03:15:00`. The scripts in `/tmp/.syncd` and `/tmp/.x` contain a download-and-launch sequence and a reverse-shell command targeting `10.0.0.66:4444`.
4. **SSH account access:** The captured reconnaissance output and `/home/j.morgan/.bash_history` contain the command `sudo nano /home/r.house/.ssh/authorized_keys`. The later accepted public-key login for `r.house` is consistent with this activity. The repository does not include the key file's before-and-after contents.
5. **Suspicious elevated script:** `/usr/local/bin/sysmon` contains a Bash reverse-shell command targeting `10.0.0.66:5555`. The available artifacts establish the script's contents, but do not show what mechanism, if any, automatically launched it.
6. **Source-code staging:** The investigation identified `mfboot_main.c` in the engineering directory and recovered the same path from the decoded archive `/dev/shm/.core_dump_2025.tgz.enc`. This establishes local staging of the source file. It does not establish successful external exfiltration.

## Repository navigation

| Area | Contents |
|---|---|
| [`investigation/`](investigation/) | Ten chronological stage reports, each with a direct screenshot link |
| [Evidence index](evidence/evidence-index.md) | Screenshot inventory, artifact references, and stage links |
| [`evidence/screenshots/`](evidence/screenshots/) | Ten original terminal screenshots |
| [`commands/`](commands/) | Commands documented in the investigation and archive-recovery workflow |
| [Attack timeline](findings/attack-timeline.md) | Ordered sequence with timestamps where available |
| [Key findings](findings/key-findings.md) | Findings separated from unverified interpretations |
| [Security recommendations](findings/security-recommendations.md) | Defensive recommendations tied to observed artifacts |
| [Investigation limitations](findings/investigation-limitations.md) | Boundaries of what the available evidence supports |
| [Contributions and scope](CONTRIBUTIONS.md) | First-person project scope and source boundaries |

## Evidence handling and interpretation

- The screenshots are the ten terminal captures supplied with the original investigation.
- Each stage links to its corresponding screenshot. The evidence index provides a second navigation route.
- The triage scripts `classify_logs.py` and `file_anomalies.py` were available in the lab environment. Their source code is not included here.
- I distinguish file contents and command history from proof that a process executed or a network transfer completed.
- No additional attack steps, scripts, datasets, or test results have been added to this repository.

## Main takeaway

The strongest part of this investigation is the correlation between separate host artifacts: the email and attachment name, the reconnaissance output, shell history, authentication events, suspicious scripts, source-code file, and recovered archive. The findings should be read alongside the limitations document so that local staging is not mistaken for confirmed external exfiltration.
