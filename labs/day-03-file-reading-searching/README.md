# Lab 03 — Linux File Reading and Text Searching

## Objective
Practise reading text files, searching for specific entries, counting matching lines, and combining commands to summarize a simulated log file.

## Environment
* **Operating system:** Ubuntu
* **Shell:** Zsh
* **Lab type:** Local practice
* **Data:** Fictional log entries created for this lab
* **Scope:** Text inspection and basic log analysis

---

## Exercise 1 — Create the Sample Log
Created the `practice` directory and `sample.log` containing ten fictional log entries with INFO, WARNING, and ERROR messages.

### Command Used
```bash
mkdir -p practice
cat << 'EOF' > practice/sample.log
[INFO] 2026-10-26 08:00:01 - System service initialized successfully.
[INFO] 2026-10-26 08:15:22 - User authentication service started.
[WARNING] 2026-10-26 09:30:10 - High memory utilization detected (82%).
[ERROR] 2026-10-26 10:05:45 - Database connection timeout on primary node.
[INFO] 2026-10-26 11:00:00 - Routine backup task scheduled.
[WARNING] 2026-10-26 12:45:12 - SSL certificate expiration approaching in 14 days.
[ERROR] 2026-10-26 14:20:33 - Failed to bind port 8080: Address already in use.
[INFO] 2026-10-26 15:00:00 - Configuration reload triggered.
[WARNING] 2026-10-26 16:10:50 - Slow query execution recorded (1.4s).
[INFO] 2026-10-26 17:00:00 - Daily log rotation completed.
EOF
