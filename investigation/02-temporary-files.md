# Stage 02: Temporary-File Investigation (`/tmp`)

## 1. Investigation Objective
Inspect the `/tmp` directory to identify non-standard or attacker-staged files flagged during initial anomaly triage.

## 2. Evidence Examined
* `/tmp` directory listing

## 3. Linux Commands Used
```bash
cd /tmp
ls
```

## 4. What I Observed
Alongside standard system service sockets and directories, two non-standard files were present in `/tmp`:
* `dock-replace.log`
* `invoice_dump.txt`

## 5. How I Interpreted the Evidence
World-writable temporary directories like `/tmp` are commonly used to stage reconnaissance output and scripts. `invoice_dump.txt` stood out immediately as a non-system artifact warranting direct inspection.

## 6. Screenshot of the Actual Investigation
![Stage 02 Temporary Files](../evidence/screenshots/02_tmp_directory_inspection.png)

## 7. What the Finding Established
Confirmed the presence of staged artifact `/tmp/invoice_dump.txt` for content analysis in Stage 03.
