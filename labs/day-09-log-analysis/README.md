# Day 9 Lab — Linux Log Analysis

## Objective
Inspect Linux logs and identify system events.

## Tasks and Evidence

### 1. Recent Logs
```bash
journalctl -n 20 --no-pager
```
![Recent logs](screenshots/01-recent-logs.png)

### 2. Current Boot Logs
```bash
journalctl -b -n 30 --no-pager
```
![Boot logs](screenshots/02-boot-logs.png)

### 3. Error Messages
```bash
journalctl -p err -n 20 --no-pager
```
![Error logs](screenshots/03-error-logs.png)

### 4. Available Log Files
```bash
ls -lah /var/log
```
![Log files](screenshots/04-log-files.png)

### 5. Authentication Logs
```bash
sudo tail -n 20 /var/log/auth.log
```
![Authentication logs](screenshots/05-auth-logs.png)

## Findings
- Errors observed:
- Authentication activity:
- Important observations:

## Conclusion
Practiced inspecting Linux logs for troubleshooting and basic security monitoring.
