# Stage 01: Initial Triage (`auth.log` & Anomaly Triage)

## 1. Investigation Objective
Activate an isolated analysis environment and run initial triage scripts across authentication logs and sensitive system directories to identify suspicious logins and anomalous files without altering host evidence.

## 2. Evidence Examined
* `/var/log/auth.log` (via `/opt/dfir-env` triage tooling)
* Target directories: `/opt/robbco`, `/tmp`, `/dev/shm`, `/usr/local/bin`

## 3. Linux Commands Used
```bash
source /opt/dfir-env/bin/activate
python3 classify_logs.py
python3 file_anomalies.py
```

## 4. What I Observed
* `classify_logs.py` flagged three authentication events originating from `192.168.0.100`:
  1. `03:00:01` — Failed password attempt for invalid user `admin`.
  2. `03:01:02` — Accepted password login for user `j.morgan`.
  3. `03:15:00` — Accepted public-key login for privileged user `r.house`.
* `file_anomalies.py` flagged 9 files across `/opt/robbco`, `/tmp`, `/dev/shm`, and `/usr/local/bin` exhibiting high entropy or irregular metadata attributes.

## 5. How I Interpreted the Evidence
The sequence of a failed `admin` probe followed one minute later by a successful login for `j.morgan`—and fourteen minutes later by a public-key login for administrative user `r.house`—pointed to initial compromise of `j.morgan` followed by privilege escalation into `r.house`. The flagged files provided concrete starting paths for manual verification.

## 6. Screenshot of the Actual Investigation
![Stage 01 Initial Triage](../evidence/screenshots/01_initial_triage_ml_logs.png)

## 7. What the Finding Established
Established the initial timeline anchors (`03:00:01` to `03:15:00`), identified the two affected user accounts (`j.morgan` and `r.house`), and narrowed manual filesystem inspection to four target directories.
