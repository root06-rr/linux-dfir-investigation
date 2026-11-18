# Investigation Scope & Limitations

To maintain strict forensic accuracy, this repository distinguishes between directly verified host artifacts and mechanisms that could not be independently confirmed from the available lab data:

1. **Local Staging vs. Confirmed External Exfiltration:**
   * Decoding `/dev/shm/.core_dump_2025.tgz.enc` proves that RobbCo's `MFBootAgent` source code was compressed, encoded, and staged locally for exfiltration. Similarly, `invoice_Q1_2075.ods` contained a `curl` POST command targeting `192.168.0.100:8080/collect.php`. However, because full packet captures (PCAPs) or listener logs were not part of the host evidence, successful external data transfer is documented as **source-code staging and attempted exfiltration** rather than confirmed network transfer.
2. **Pre-Built Triage Scripts (`classify_logs.py` & `file_anomalies.py`):**
   * These two scripts were provided inside `/opt/dfir-env` in the lab environment to assist initial log and anomaly triage. Their source code is not included or recreated in this repository; all findings reported here were verified manually via standard Linux CLI commands (`cat`, `ls -la`, `base64`, `tar`).
3. **Static File Inspection vs. Runtime Execution Proofs:**
   * For `/home/j.morgan/Documents/Invoices/invoice_Q1_2075.ods` and `/usr/local/bin/sysmon`, the investigation established their exact file contents, timestamps, and correlation with `.bash_history` and `auth.log`, rather than capturing live process memory (`ps`/`/proc`) at the moment of execution.
4. **Screenshot Inventory:**
   * All 10 terminal captures from the original investigation are indexed in `evidence/evidence-index.md` and linked across Stages 01–10.
