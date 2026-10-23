# Linux Environment Baseline

## Objective

Document my current Linux environment and record my initial understanding of Linux fundamentals and the command-line interface (CLI) before moving on to more advanced Linux and cybersecurity topics.

## System Information

- **Date:** October 22, 2026
- **Distribution and version:** Ubuntu 26.04
- **Kernel version:** 7.0.0-38-generic
- **Architecture:** x86_64 (64-bit)
- **Configured shell:** Zsh (`/usr/bin/zsh`)
- **Git version:** 2.53.0

## Commands Practiced

The following commands were used to inspect my Linux environment:

- `cat /etc/os-release` — Displays information about the Linux distribution and its version.
- `uname -r` — Displays the running kernel version.
- `uname -m` — Displays the system's machine architecture.
- `echo "$SHELL"` — Displays the configured shell path stored in the `SHELL` environment variable.
- `free -h` — Displays memory usage in a human-readable format.
- `df -h` — Displays filesystem disk space usage in a human-readable format.

## Observations and Learning Notes

During this session, I studied Linux fundamentals, the command-line interface, and the basic concepts needed to work comfortably in a Linux environment.

### 1. What Is Linux?

Linux is an open-source operating-system kernel. It manages system resources and provides the core functionality that allows software to communicate with computer hardware.

Linux-based operating systems, commonly called Linux distributions, combine the Linux kernel with system utilities, applications, and other software.

### 2. What Is Linux Used For?

Linux is used in many areas of computing, including:

- **Servers:** Hosting websites, applications, databases, and other services.
- **Cloud infrastructure:** Running virtual machines, containers, and cloud workloads.
- **Enterprise systems:** Supporting business applications and organizational infrastructure.
- **Embedded systems:** Powering devices such as routers and other specialized equipment.
- **Cybersecurity:** Providing an environment for security tools, system administration, networking, and authorized security testing.
- **Desktop computing:** Providing a graphical and command-line environment for everyday computer use.

Linux is widely used in server and cloud environments, making it an important operating system to understand in cybersecurity.

### 3. Why Learn the Linux Command-Line Interface?

The command-line interface (CLI) allows users to interact with the operating system by entering commands.

Learning the CLI is important because it provides:

- **Efficiency:** Many administrative tasks can be performed quickly.
- **Control:** Users can manage files, processes, permissions, and system settings.
- **Automation:** Repetitive tasks can be automated using shell scripts.
- **Remote administration:** Linux systems can be managed remotely through tools such as SSH.
- **Troubleshooting:** Commands provide useful information for investigating system behavior and diagnosing problems.

### 4. Examples of Linux Distributions

Some common Linux distributions include:

- Ubuntu
- Debian
- Fedora
- Red Hat Enterprise Linux (RHEL)
- Kali Linux

Different distributions are designed for different purposes and may have different default tools, package managers, and configurations.

### 5. What Is a Terminal?

A terminal emulator is an application that provides an interface for entering commands and viewing their output.

For example, Ubuntu Terminal allows a user to interact with a shell without relying entirely on graphical applications.

### 6. What Is a Shell?

A shell is a program that interprets commands and allows users to interact with the operating system.

Examples include:

- Bash
- Zsh
- Fish

My configured shell is Zsh, located at `/usr/bin/zsh`.

The terminal provides the interface, while the shell interprets the commands entered through that interface.

## Key Takeaways

- Linux is an open-source kernel used by many operating systems.
- Linux distributions combine the kernel with utilities and other software.
- The CLI provides an efficient way to interact with and administer a Linux system.
- The terminal and the shell are related but have different roles.
- Linux knowledge is valuable for system administration, networking, and cybersecurity.
- Basic system-information commands help establish an understanding of the environment before conducting practical labs.

## Reflection

This session helped me establish a baseline for my Linux learning journey. I reviewed important Linux concepts and practiced commands for identifying my operating system, kernel version, architecture, shell, memory, and disk usage.

My next goal is to become more comfortable navigating the filesystem, managing files and directories, understanding permissions, and using commands independently rather than simply memorizing them.

## Next Steps

- Practice navigating the Linux filesystem.
- Learn essential file and directory management commands.
- Understand absolute paths and relative paths.
- Practice reading manual pages and command-line help.
- Continue documenting practical exercises and troubleshooting experiences in this repository.
