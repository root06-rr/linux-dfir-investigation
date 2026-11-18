# Linux Forensic Investigation Command Reference

This reference groups the commands explicitly documented in the ten investigation stages. It is a navigation aid for the original lab work, not a claim that every command below was run as part of a separate automated workflow.

## 1. Initial triage (Stage 01)

```bash
source /opt/dfir-env/bin/activate
python3 classify_logs.py
python3 file_anomalies.py
```

**Purpose:** Activate the isolated Python environment and run the two triage scripts supplied in the lab. Their source code is not included in this repository. The results were followed by manual artifact inspection.

## 2. Temporary directory review (Stages 02 and 06)

```bash
cd /tmp
ls
ls -la
cat .syncd
cat .x
```

**Purpose:** Review the visible temporary-directory entries, then inspect hidden files and the contents of the two suspicious scripts.

## 3. Reconnaissance output and shell history (Stages 03 and 07)

```bash
cat invoice_dump.txt | column -c $(tput cols)
cd /home/j.morgan
ls -la
cat .bash_history
```

**Purpose:** Read the collected reconnaissance output and compare the captured command history with the user's local `.bash_history`.

## 4. Attachment and email review (Stages 04 and 05)

```bash
cd /home/j.morgan/Documents/Invoices/
cat invoice_Q1_2075.ods

cd /home/j.morgan/Mail
cd inbox
ls
cat email_invoice.eml
```

**Purpose:** Inspect the attachment's observed raw contents and the local email artifact. The report records shell-command text in the attachment inspection. It does not include a separate LibreOffice runtime trace proving how the content was executed.

## 5. SSH and suspicious system-file review (Stages 07 to 09)

```bash
sudo nano /home/r.house/.ssh/authorized_keys

cd /usr/local/bin
ls -la
cat sysmon

cd /opt/robbco/sys
ls -la
cat boot_monitor.log

cd /opt/robbco/engineering/MFBootAgent
ls -la
cat mfboot_main.c
```

**Purpose:** The `sudo nano` command appears in the captured shell history. The remaining commands are the inspection commands documented for the suspicious script, log, and source file. The repository does not include the before-and-after contents of `authorized_keys`.

## 6. Archive recovery (Stage 10)

See [archive-recovery.md](archive-recovery.md) for the complete documented decode and extraction sequence.

```bash
cd /dev/shm
ls -la
cat .core_dump_2025.tgz.enc
base64 -d /dev/shm/.core_dump_2025.tgz.enc > /tmp/stolen.tar.gz
mkdir -p /tmp/stolen_source && tar -xzvf /tmp/stolen.tar.gz -C /tmp/stolen_source
```

## Interpretation note

Commands that appear in captured shell history are evidence of recorded command activity. A command's presence in history alone does not independently prove its successful completion. Likewise, a script containing a network command does not prove that a remote listener received data.
