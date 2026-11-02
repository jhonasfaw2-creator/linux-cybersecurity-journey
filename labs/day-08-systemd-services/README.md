# Day 8 Lab — Linux Services and systemd

## Objective
Inspect Linux services and understand how systemd manages them.

## Lab Tasks

### 1. Check systemd
```bash
systemctl --version
ps -p 1 -o pid,comm,args
```
**Screenshot 1:** 
/home/johannes/Pictures/Screenshots/Screenshot From 2026-11-02 22-26-56.png

### 2. List Running Services
```bash
systemctl list-units --type=service --state=running
```
**Screenshot 2:** 
/home/johannes/Pictures/Screenshots/Screenshot From 2026-11-02 22-28-30.png
/home/johannes/Pictures/Screenshots/Screenshot From 2026-11-02 22-28-36.png

### 3. Inspect a Service
```bash
systemctl status NetworkManager
```
**Screenshot 3:** 
/home/johannes/Pictures/Screenshots/Screenshot From 2026-11-02 22-30-08.png

### 4. Check Failed Services
```bash
systemctl --failed
```
**Screenshot 4:** 
/home/johannes/Pictures/Screenshots/Screenshot From 2026-11-02 22-31-14.png

### 5. Inspect System Logs
```bash
journalctl -n 20 --no-pager
```
**Screenshot 5:** 
/home/johannes/Pictures/Screenshots/Screenshot From 2026-11-02 22-32-05.png

## Results
Record your actual findings:
- systemd version:
- Running services observed:
- NetworkManager status:
- Failed services:
- Log observations:
## Conclusion
This lab introduced systemd and practical Linux service monitoring.

## Evidence
Screenshots are stored in the `screenshots/` folder.
