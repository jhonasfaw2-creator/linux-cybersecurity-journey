# Lab 01 — Linux Filesystem Navigation

## Objective

Practise navigating the Linux filesystem using terminal commands and understand the difference between absolute and relative paths.

## Environment

- Operating system: Ubuntu
- Shell: Zsh
- Lab type: Local Linux practice
- Risk level: Beginner
- Scope: Filesystem navigation and directory inspection

## Exercise 1 — Identify the Current Directory

**Command:**

```bash
pwd
```

**Purpose:** Display the current working directory.

**Result:** Record the directory displayed by your terminal.

**What I learned:** The `pwd` command helps identify my current location in the filesystem.

## Exercise 2 — List Directory Contents

**Commands:**

```bash
ls
ls -lah
```

**Purpose:** Inspect directory contents and compare an ordinary listing with a detailed listing.

**Result:** Record the differences you observed.

**What I learned:** The `-l` option displays detailed information, `-a` includes hidden entries, and `-h` makes file sizes easier to read.

## Exercise 3 — Explore the Filesystem Root

**Commands:**

```bash
cd /
pwd
ls
```

**Purpose:** Navigate to the filesystem root and inspect its contents.

**Result:** Record the directory displayed and a few directories you observed.

**What I learned:** Linux organizes its filesystem beneath the root directory, `/`.

## Exercise 4 — Explore `/etc`

**Commands:**

```bash
cd /etc
pwd
ls
```

**Purpose:** Navigate to the system configuration directory and inspect its contents.

**Result:** Record the displayed working directory and examples of entries you observed.

**What I learned:** `/etc` contains many system-wide configuration files and directories.

## Exercise 5 — Navigate to the Home Directory

**Commands:**

```bash
cd ~
pwd
```

**Purpose:** Return to my own home directory.

**Result:** Record the actual path displayed.

**What I learned:** The `~` shortcut represents the current user's home directory.

## Exercise 6 — Practise Relative Navigation

**Commands:**

```bash
cd ~/cybersecurity-labs/linux-journey
mkdir -p labs/day-01-filesystem
cd labs/day-01-filesystem
pwd
cd ..
pwd
```

**Purpose:** Create the lab directory, enter it using a relative path, and then move to its parent directory.

**Result:** Record the paths displayed after each `pwd` command.

**What I learned:** Relative paths depend on the current working directory, while `..` refers to the parent directory.

## Overall Findings

Summarize what the exercises demonstrated about directory navigation, pathnames, and the Linux filesystem.

## Troubleshooting

Document any error messages, their causes, and the solutions.

If no errors occurred, state that explicitly.

## Conclusion

Summarize what I can now do independently and which filesystem concepts require further practice.

## Evidence

Optional: Include a sanitized screenshot showing a successful command and its output. Avoid exposing unnecessary personal or system information.
