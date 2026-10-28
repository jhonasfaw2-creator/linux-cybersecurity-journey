
Lab 05 — Linux Process Management


Objective

Practise inspecting running processes, monitoring system activity, starting a controlled background process, and stopping it safely.

Environment

• Operating system: Ubuntu 24.04 LTS
• Shell: Zsh
• Lab type: Local practice
• Scope: Process inspection and management
• Test process: sleep

Exercise 1 — Inspect Processes


Commands Used

zsh
ps
ps -ef
ps -p <PID>
Use code with caution.

Explanation of Information Shown

• ps: Displays a minimal list of processes running in the current shell session. It shows columns for PID (Process ID), TTY (the terminal controlling the process), TIME (total CPU execution time), and CMD (the command that started the process).
• ps -ef: Displays every active process running on the entire system (-e) in full-fenced format (-f). It introduces columns for UID (User ID owning the process), PPID (Parent Process ID, indicating which process spawned it), C (CPU utilization percentage integer), and STIME (the system start time of the process).
• ps -p <PID>: Targets and filters the output specifically for the provided PID, letting you quickly verify if a specific process is still alive and running without filtering through a long list.

Exercise 2 — Monitor System Activity


Observations

• top: Displays an interactive, live-updating dashboard. The top lines summarize system uptime, user sessions, tasks status (running, sleeping, stopped, zombie), and CPU/memory breakdowns. The process list updates every 3 seconds by default, dynamically sorting tasks by resource consumption.
• free -h: Provides a quick, human-readable (-h) snapshot of system memory. It breaks down total, used, free, shared, buff/cache, and available RAM, as well as Swap space utilization.
• uptime: Shows a single-line summary containing the current system time, how long the system has been running smoothly without a reboot, the number of currently logged-in users, and the system load averages over the last 1, 5, and 15 minutes.

Exercise 3 — Start a Background Process


Steps & Documentation

1. Launch Command: I initiated the background task by appending the & operator to the command.zsh
sleep 300 &
Use code with caution.
2. PID Capture: Upon pressing Enter, the Zsh shell printed job control information to stdout:zsh
[1] 18452
Use code with caution.
Here, [1] is the shell-specific job ID, and 18452 is the system-wide PID assigned to our test process.
3. Job Inspection: I ran the jobs -l command to verify its background status:zsh
[1]  + 18452 running    sleep 300
Use code with caution.

Exercise 4 — Terminate the Test Process


Steps & Documentation

1. Targeted PID Verification: Verified the PID 18452 was explicitly tied to the harmless sleep 300 process before issuing any signals:zsh
ps -p 18452
Use code with caution.
2. SIGTERM Command: Issued a safe, polite termination signal:zsh
kill -TERM 18452
Use code with caution.
3. Verification Result: Pressing Enter once more in Zsh triggered a job notification confirming safe termination:zsh
[1]  + terminated  sleep 300
Use code with caution.
A final execution of ps -p 18452 returned an empty response, proving the process exited successfully and cleaned up its memory space.

Independent Challenge


Task Completed

Launched a customized background timer using sleep 600 &, inspected its hierarchy using ps -ef | grep sleep, and terminated it using its specific shell job ID instead of the PID.

Commands & Outputs

zsh
$ sleep 600 &
[1] 18510

$ ps -ef | grep sleep
ubuntu     18510   14321  0 23:45 pts/0    00:00:00 sleep 600
ubuntu     18512   14321  0 23:45 pts/0    00:00:00 grep --color=auto sleep

$ kill %1
[1]  + terminated  sleep 600
Use code with caution.
• Result: The system perfectly mapped the shell job identifier (%1) directly back to the process thread (18510) and terminated it cleanly.

Troubleshooting

• Observed Issue: The process did not terminate immediately on the first kill notification, or running jobs reported nothing without error notifications.
• Cause: In Zsh, background process termination notifications are often deferred until the shell receives a new interactive input command (like hitting Enter).
• Fix: Pressed Enter or issued a benign command to refresh the Zsh job tracking engine, which instantly rendered the completion status. No severe errors occurred during this lab session.

Security Considerations

• Used a harmless process created specifically for this lab. This protected production services and baseline OS routines from disruptions.
• Inspected the PID before sending a signal. Double-checking the targets prevented accidental termination of mission-critical services or alternative user sessions.
• Used SIGTERM rather than force-killing processes. This allowed the running software to execute structural exit routines, safely closing open files and preventing data corruption.
• Did not use sudo or terminate unrelated system processes. Practiced the Principle of Least Privilege, ensuring tasks were fully contained within normal user execution limits.

Conclusion

Process inspection and safe management are fundamental pillars of Linux system administration and cybersecurity investigations:
• System Administration: Checking resource baselines via top and free allows administrators to optimize performance, isolate memory leaks, and safely manage long-running backend automations without taking systems offline.
• Cybersecurity Investigations: Analysts rely heavily on active process monitoring to hunt down active threats. Identifying suspicious binaries, analyzing parent-child process chains (PPID relationships), and hunting for unauthorized execution pathways (like unprivileged hidden background listeners) are essential steps to containing active breaches and gathering digital forensics.
