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
![Screenshot 1](screenshots/Screenshot%20From%202026-11-02%2022-26-56.png)

### 2. List Running Services
```bash
systemctl list-units --type=service --state=running
```
**Screenshot 2:** 
![Screenshot 2](screenshots/Screenshot%20From%202026-11-02%2022-28-30.png)

![Screenshot 3](screenshots/Screenshot%20From%202026-11-02%2022-28-36.png)
### 3. Inspect a Service
```bash
systemctl status NetworkManager
```
**Screenshot 3:** 

![Screenshot 4](screenshots/Screenshot%20From%202026-11-02%2022-30-08.png)
### 4. Check Failed Services
```bash
systemctl --failed
```
**Screenshot 4:** 
![Screenshot 5](screenshots/Screenshot%20From%202026-11-02%2022-31-14.png)

### 5. Inspect System Logs
```bash
journalctl -n 20 --no-pager
```
**Screenshot 5:** 

![Screenshot 6](screenshots/Screenshot%20From%202026-11-02%2022-32-05.png)

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
