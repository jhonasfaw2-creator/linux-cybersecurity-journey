# Day 7 — Linux Package Management

## Objective

Understand how Ubuntu manages software using APT and dpkg, including package repositories, dependencies, installation, updates, upgrades, and package inspection.

The goal of this session was to learn how Linux administrators manage installed software, maintain packages, and keep systems updated and secure.

## Video Assignment

- **Resource:** Linux Basics for Beginners — How to Use APT
- **Link:** https://www.youtube.com/watch?v=c9-AbHhoCeI
- **Topics:** APT, software installation, package updates, upgrades, and package removal.

### Key Lessons Learned

I learned that Linux uses package management tools to install, update, remove, and maintain software.

APT provides a convenient way to manage software through configured repositories. It also handles package dependencies, reducing the need to install required components manually.

## Reading Assignment

### 1. Ubuntu — Install and Manage Packages

- **Resource:** Official Ubuntu Package Management Documentation
- **Link:** https://ubuntu.com/server/docs/how-to/software/package-management/

**Topics studied:**
- Package management in Ubuntu.
- APT and dpkg.
- Package repositories.
- Installing and removing packages.
- Managing software dependencies.

### 2. Ubuntu — Managing Your Software

- **Resource:** Ubuntu Managing Your Software
- **Link:** https://ubuntu.com/server/docs/tutorial/managing-software/

**Topics studied:**
- Refreshing package information.
- Installing software.
- Searching for packages.
- Checking available updates.
- Managing installed software.

## Commands Practiced

- `apt --version` — Display the installed APT version.
- `dpkg --version` — Display the installed dpkg version.
- `dpkg-query -W` — Display information about installed packages.
- `dpkg -S` — Identify which installed package owns a particular file.
- `apt search` — Search for available packages.
- `apt show` — Display detailed information about a package.
- `apt-cache policy` — Display package versions, repository information, and installation candidates.
- `sudo apt update` — Refresh package information from configured repositories.
- `apt list --upgradable` — Display installed packages with available upgrades.
- `apt-get -s install` — Simulate a package installation without performing it.
- `sudo apt install` — Install a package and its required dependencies.
- `dpkg -L` — List files associated with an installed package.

## Key Concepts Learned

### 1. What Is APT?

APT stands for Advanced Package Tool. It is a package management system used in Debian-based Linux distributions, including Ubuntu.

APT helps users install, update, upgrade, and remove software through configured package repositories.

It also manages dependencies, automatically identifying and retrieving additional packages required by the software being installed.

**Example command:**

```bash
sudo apt install tree
```

This command installs the `tree` package and its required dependencies, subject to the package manager's proposed changes and confirmation.

### 2. What Is dpkg?

`dpkg` is a lower-level Debian package management tool used to install, remove, and inspect `.deb` packages.

It maintains information about installed packages and their associated files.

APT and dpkg work together, but they have different responsibilities.

- **APT:** Manages packages through repositories, retrieves software, and handles dependencies.
- **dpkg:** Performs lower-level package operations and maintains the installed package database.

### Identifying Package Ownership with `dpkg -S`

I learned how to identify which installed software package owns a particular file using the `dpkg -S` command.

**Command practiced:**

```bash
dpkg -S "$(command -v cat)"
```

**Example output:**

```text
coreutils: /usr/bin/cat
```

**Explanation:**

- `command -v cat` identifies the location of the `cat` executable.
- `dpkg -S` searches the installed package database for the package associated with that file.
- `coreutils` is the package that provides the executable.

**What I learned:**

This command is useful for investigating installed software, identifying the package associated with a particular executable, and determining which package may need maintenance or a security update.

I also learned that `dpkg -S` identifies recorded package ownership but does not independently verify whether a file is authentic or uncompromised.

### 3. What Are Package Repositories?

Package repositories are software sources that contain packages and package information.

Ubuntu uses configured repositories to obtain software and updates.

Repositories help administrators obtain software from trusted distribution sources instead of downloading and installing unknown packages from random websites.

Examples include Ubuntu's official Main, Universe, Restricted, and Multiverse repository components.

### 4. What Are Dependencies?

Dependencies are additional packages or components that a program requires to function correctly.

For example, an application might depend on a particular library or another software component.

APT automatically identifies and manages many of these dependencies during installation and upgrades.

This makes software installation easier and helps maintain compatibility between packages.

### 5. Understanding Package Updates and Upgrades

One of the most important things I learned was the difference between `apt update` and `apt upgrade`.

**`sudo apt update`**

This refreshes the local package indexes by retrieving updated package information from configured repositories.

It does not automatically upgrade the installed software.

**`sudo apt upgrade`**

This upgrades installed packages when newer versions are available, subject to dependency and package-management constraints.

For security and system maintenance, both commands are important, but they perform different operations.

### 6. Why Are Security Updates Important?

Software can contain vulnerabilities that attackers may exploit.

Security updates help fix known vulnerabilities, correct software defects, and improve system reliability.

Keeping software maintained and obtaining updates from trusted repositories reduces the risk associated with outdated or vulnerable packages.

### 7. Understanding Installation Simulation

The `apt-get -s install` command simulates an installation instead of performing it.

For example:

```bash
apt-get -s install tree
```

This allows an administrator to inspect the proposed package operations and dependencies before making actual system changes.

I learned that reviewing proposed changes before confirming an installation is an important system administration practice.

## Lab Results

### 1. Package Management Tool Inspection

**Commands executed:**

```bash
apt --version
dpkg --version
```

**Results:**

The commands displayed the installed versions of APT and dpkg.

- APT version: Recorded from terminal output.
- dpkg version: Recorded from terminal output.

**Observation:**

APT and dpkg are both package management tools, but they operate at different levels of the Debian-based package management system.

### 2. Inspecting Installed Packages

**Command:**

```bash
dpkg-query -W coreutils
```

**Result:**

The command displayed package information for `coreutils`.

**What I learned:**

The `dpkg-query` tool allows administrators to inspect information stored in the installed package database.

### 3. Searching for Packages

**Command:**

```bash
apt search tree
```

**Result:**

APT returned packages matching the search term `tree`.

**What I learned:**

The package search function helps identify available software without manually browsing repository websites.

### 4. Inspecting Package Information

**Commands:**

```bash
apt show tree
apt-cache policy tree
```

**Result:**

The commands displayed package information, including its description, version information, and available installation candidates.

**What I learned:**

Before installing software, I should inspect the package details and understand where the software is coming from.

### 5. Refreshing the Package Index

**Command:**

```bash
sudo apt update
```

**Result:**

The command attempted to retrieve updated package information from the configured repositories.

**What I learned:**

Refreshing package information allows APT to identify newer versions of software available through the configured repositories.

### 6. Checking Available Updates

**Command:**

```bash
apt list --upgradable
```

**Result:**

The command displayed the installed packages for which newer versions were available, based on the refreshed package information.

**What I learned:**

This command helps administrators inspect available updates before deciding whether to upgrade installed software.

### 7. Simulating Package Installation

**Command:**

```bash
apt-get -s install tree
```

**Result:**

APT simulated the installation and displayed the proposed package operations without actually performing the installation.

**What I learned:**

Installation simulation provides an opportunity to inspect dependencies and proposed changes before making modifications to the system.

### 8. Installing and Inspecting a Package

If the installation was performed:

```bash
sudo apt install tree
```

Verify the executable:

```bash
tree --version
command -v tree
```

**What I learned:**

I learned how to install a software package through APT and verify that its executable is available.

### 9. Inspecting Installed Package Files

**Commands:**

```bash
dpkg-query -W tree
dpkg -L tree | head -n 15
dpkg -S "$(command -v tree)"
```

**Result:**

These commands allow me to inspect the installed package, list some of its associated files, and identify the package that owns its executable.

**What I learned:**

The package database provides useful information about the software installed on a Linux system and the files associated with each package.

## Independent Challenge

### Objective

Practise identifying packages, inspecting software information, and understanding package installation without making unnecessary changes to the system.

### Challenge 1 — Inspect Package Versions

```bash
apt --version
dpkg --version
```

**Result:** Identify the installed versions of both tools.

### Challenge 2 — Search for a Package

```bash
apt search tree
```

**Result:** Identify the package and review the search results.

### Challenge 3 — Inspect Package Information

```bash
apt show tree
```

**Result:** Identify the package description, version, and dependencies.

### Challenge 4 — Simulate Another Installation

```bash
apt-get -s install cowsay
```

**Result:** Inspect the proposed changes and identify any dependencies without installing the package.

### Challenge 5 — Identify Package Ownership

```bash
dpkg -S "$(command -v cat)"
```

**Result:**

The package database identifies `coreutils` as the package associated with `/usr/bin/cat`.

### Challenge Reflection

This challenge helped reinforce the difference between searching for available packages, inspecting installed software, simulating installations, and identifying package ownership.

I learned that package management is not simply about installing applications. It also involves understanding software sources, dependencies, installed files, and maintenance.

## Troubleshooting

Package management commands depend on configured repositories and network connectivity.

Potential errors include:

- Failed repository connections.
- Package not found.
- Package installation conflicts.
- Missing dependencies.
- Insufficient privileges.

When troubleshooting, I should first inspect the actual error message, verify network connectivity, check repository configuration, and review package information.

I should avoid adding unknown repositories or executing installation commands without understanding their proposed changes.

Record any actual errors encountered during the exercises and how they were resolved. If no errors occurred, state that explicitly.

## Security Considerations

- Used configured Ubuntu repositories for package management.
- Inspected package details before installation.
- Used installation simulation to review proposed changes.
- Avoided adding untrusted third-party repositories.
- Did not automatically upgrade the entire system during the learning exercise.
- Used package inspection commands to understand installed software.
- Learned why keeping software updated is important for security.

## Knowledge Check

### 1. What is APT?

APT stands for Advanced Package Tool. It is a package management system used in Ubuntu and other Debian-based distributions to install, update, upgrade, and remove software using configured repositories.

It also manages package dependencies automatically.

### 2. What is the difference between APT and dpkg?

APT is a higher-level package management tool that retrieves packages from repositories, manages dependencies, and simplifies software installation and updates.

dpkg is a lower-level tool that manages Debian packages and maintains information about installed software and its files.

APT uses dpkg to perform many of its package installation and removal operations.

### 3. What does `apt update` do?

The `apt update` command refreshes the local package indexes by retrieving updated package information from configured repositories.

It does not install software updates.

### 4. What does `apt upgrade` do?

The `apt upgrade` command upgrades installed packages when newer versions are available and the required package changes can be performed within its upgrade rules.

It helps keep installed software current, including applicable security updates.

### 5. What is a package repository?

A package repository is a software source containing packages and information about their versions and dependencies.

APT uses configured repositories to locate and retrieve software for installation and maintenance.

Using trusted repositories helps reduce the risk of installing modified or malicious packages.

### 6. Why should I inspect a simulated installation before proceeding?

An installation simulation allows me to review which packages would be installed, upgraded, or otherwise changed before making actual modifications.

This helps identify unexpected dependencies or package operations and reduces the risk of unwanted system changes.

### 7. Why are security updates important?

Security updates fix known vulnerabilities in software and help protect systems against potential attacks.

Keeping software maintained reduces exposure to vulnerabilities that attackers may exploit and improves system reliability.

## Reflection

### 1. Which package-management command was most useful?

I found `apt show` and `dpkg -S` particularly useful.

`apt show` provides information about available packages before installation, while `dpkg -S` helps identify which installed package owns a particular file.

### 2. What did I learn about dependencies?

I learned that software packages often depend on other packages and libraries to function correctly.

APT can identify and manage these dependencies automatically during installation, reducing the amount of manual configuration required.

### 3. What is the difference between an installed package and an available package?

An installed package is software that is already registered in the system's package database.

An available package is a package that can be found through configured repositories, whether or not it has been installed.

A newer available version does not necessarily mean that the installed version has already been upgraded.

### 4. How does software maintenance relate to cybersecurity?

Software maintenance is an important part of cybersecurity because outdated software may contain vulnerabilities that attackers can exploit.

Regularly inspecting installed software, obtaining updates from trusted repositories, and applying appropriate security patches help reduce the attack surface of a Linux system.

## First Week Review — Days 1–7

Completing the first week of my Linux learning journey helped establish important foundations for Linux system administration and cybersecurity.

### Day 1 — Linux Filesystem and Navigation

Learned how to navigate the Linux filesystem using `pwd`, `ls`, and `cd`.

Understood the difference between the root directory, home directory, absolute paths, and relative paths.

### Day 2 — File and Directory Management

Practised creating, inspecting, copying, moving, renaming, comparing, and safely removing files and directories.

Learned commands such as `mkdir`, `touch`, `cp`, `mv`, `diff`, and `rm -i`.

### Day 3 — File Reading and Text Searching

Learned how to display file contents, inspect selected lines, search for specific text, and count results.

Practised `cat`, `head`, `tail`, `less`, `grep`, `wc`, and pipes.

### Day 4 — Users, Groups and File Permissions

Studied Linux ownership and access permissions.

Practised using `ls -l`, `chmod`, and `stat` to inspect and control read, write, and execute permissions.

### Day 5 — Processes and System Monitoring

Learned how to inspect running processes, identify process IDs, monitor system activity, and control a background test process.

Practised `ps`, `top`, `jobs`, `sleep`, and `kill -TERM`.

### Day 6 — Linux Networking Fundamentals

Learned how to inspect network interfaces, IP addresses, routing information, connectivity, DNS resolution, and listening sockets.

Practised `ip`, `ping`, `getent`, and `ss`.

### Day 7 — Linux Package Management

Learned how Ubuntu manages software through APT and dpkg.

Practised package searching, inspecting package information, refreshing package indexes, simulating installations, and identifying package ownership.

## Commands I Can Now Practise More Confidently

1. `pwd`, `ls`, and `cd` — Navigating the filesystem.
2. `cp`, `mv`, and `mkdir` — Managing files and directories.
3. `grep`, `wc`, and `less` — Reading and searching text.
4. `chmod` and `stat` — Managing and inspecting permissions.
5. `ps` and `top` — Inspecting running processes.
6. `ip` and `ss` — Inspecting network configuration and sockets.
7. `apt` and `dpkg` — Managing and inspecting software packages.

## Topics I Need to Revise

1. **Linux permissions:** Become more comfortable with numeric permissions, symbolic permissions, ownership, and groups.
2. **Networking:** Develop a deeper understanding of IPv4, CIDR notation, TCP, UDP, DNS, routing, and ports.
3. **Process management:** Practise process states, parent processes, foreground and background jobs, and signals.
4. **Package management:** Improve my understanding of dependencies, package repositories, and software updates.

## Overall Reflection

My first week focused on developing practical Linux foundations rather than simply memorizing commands.

I learned how to navigate the filesystem, manage files, search text, control permissions, inspect processes, investigate network configuration, and manage software packages.

I also learned the importance of documenting commands, verifying results, troubleshooting errors, and understanding what each command does before using it.

My next goal is to become more independent with the Linux command line and gradually apply these skills to real system administration and cybersecurity exercises.

## Next Steps

- Study Linux services and systemd.
- Learn how to inspect running services.
- Explore system logs and journalctl.
- Develop Bash scripting fundamentals.
- Practise Linux system monitoring and troubleshooting.
- Begin connecting Linux administration concepts with cybersecurity investigations.
