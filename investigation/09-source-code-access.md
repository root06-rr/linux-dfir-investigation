# Stage 09: Persistence Deception & Source-Code Access (`mfboot_main.c`)

## 1. Investigation Objective
Inspect the flagged files under `/opt/robbco` to investigate the fabricated telemetry log and verify whether proprietary engineering source code had been accessed.

## 2. Evidence Examined
* `/opt/robbco/sys/boot_monitor.log`
* `/opt/robbco/engineering/MFBootAgent/mfboot_main.c`

## 3. Linux Commands Used
```bash
cd /opt/robbco/sys
ls -la
cat boot_monitor.log

cd /opt/robbco/engineering/MFBootAgent
ls -la
cat mfboot_main.c
```

## 4. What I Observed
* `/opt/robbco/sys/boot_monitor.log` contained a single fabricated entry:
  ```text
  Jan 15 03:22:10 bios_hook: UOS boot intercepted at 0x400f2
  ```
* `/opt/robbco/engineering/MFBootAgent/mfboot_main.c` was intact and readable, containing proprietary C source code implementing `start_boot_sequence()` and referencing `RETROS-52EE5` and `UOS-2.3.0`.

## 5. How I Interpreted the Evidence
The fake `boot_monitor.log` entry was planted to provide a plausible cover story for `/usr/local/bin/sysmon`. Meanwhile, manual inspection proved that `mfboot_main.c`—which had been flagged by the anomaly script—was legitimate proprietary RobbCo firmware code rather than malware, indicating it was a target of intellectual property theft.

## 6. Screenshot Evidence

**Evidence ID:** E-09

![E-09 Boot log and source-code review](../evidence/screenshots/09_fake_boot_log_source_code.png)

*Figure E-09. Boot log and source-code review.*

**What this image supports:** The `boot_monitor.log` entry and the readable `mfboot_main.c` source file shown during the review.

**Evidence boundary:** The screenshot supports what was displayed during inspection. The available artifacts do not independently establish who created the log entry.

## 7. What the Finding Established
Confirmed the deception artifact supporting `/usr/local/bin/sysmon` and identified the targeted proprietary source code repository (`/opt/robbco/engineering/MFBootAgent/`).

## 8. Evidence Correlation

The `mfboot_main.c` file was present and readable in the engineering directory during this stage. Stage 10 later recovers the same relative path from the decoded archive in `/dev/shm`. This connects the source-code file observed in the engineering directory with the file contained in the locally staged archive. The single `bios_hook` line is described as fabricated in the original investigation, but the repository does not include additional log provenance or execution records that independently establish who created it.
