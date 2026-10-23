# Day 1 — Linux Filesystem and Navigation

## Objective

Learn to navigate the Linux filesystem and understand absolute paths, relative paths, and basic directory navigation.

## Video Assignment

- **Resource:** [Linux Filesystem Basics — Structure, Navigation, Absolute and Relative-to-Home Pathnames](https://youtu.be/WT5SepOmye0)
- **Key lessons:** Filesystem navigation, directory structure, and pathnames.
- **My notes:** Record the most useful lessons from the video.

## Reading Assignment

- **Resource:** [Ubuntu — The Linux Command Line for Beginners](https://ubuntu.com/desktop/docs/en/latest/tutorial/the-linux-command-line-for-beginners/)
- **Concepts studied:**
  1. Navigating files and directories.
  2. Understanding the filesystem root and home directory.
  3. Understanding absolute and relative paths.

## Commands Practiced

- `pwd` — Display the current working directory.
- `ls` — List directory contents.
- `ls -lah` — Show detailed information, including hidden entries.
- `cd /` — Navigate to the filesystem root.
- `cd /etc` — Navigate to the system configuration directory.
- `cd ~` — Navigate to my home directory.
- `cd ..` — Move to the parent directory.
- `cd -` — Return to the previous working directory.

## Key Concepts Learned

### 1. Filesystem Root

The `/` directory is the starting point of the Linux filesystem tree. Other directories and files are organized beneath it.

### 2. Home Directory

The home directory is the personal directory assigned to a user. The `~` shortcut represents the current user's home directory.

### 3. Absolute Paths

An absolute path specifies a location starting from the filesystem root.

Example: `/var/log`

### 4. Relative Paths

A relative path specifies a location in relation to the current working directory.

Example: `labs/day-01-filesystem`

### 5. Hidden Entries

Linux filenames beginning with a period are normally hidden from ordinary `ls` output. The `-a` option displays them.

## Independent Challenges

For each challenge, record the actual result after running the commands.

### Challenge 1 — Navigate to `/var/log`

```bash
cd /var/log
pwd
```

- **Expected result:** `/var/log`
- **Actual result:** [Record your output]
- **Status:** [Completed / Needs practice]

### Challenge 2 — Return to My Home Directory

```bash
cd ~
pwd
```

- **Actual result:** [Record your output]
- **Status:** [Completed / Needs practice]

### Challenge 3 — Navigate Using a Relative Path

```bash
cd ~/cybersecurity-labs/linux-journey
cd labs
pwd
```

- **Actual result:** [Record your output]
- **Status:** [Completed / Needs practice]

### Challenge 4 — Display Hidden Entries

```bash
ls -lah ~
```

- **Actual result:** [Describe what appeared]
- **Status:** [Completed / Needs practice]

### Challenge 5 — Return to the Previous Directory

```bash
cd /var/log
cd ~
cd -
pwd
```

- **Expected result:** `/var/log`
- **Actual result:** [Record your output]
- **Status:** [Completed / Needs practice]

## Knowledge Check

Answer these questions in my own words.

1. What is the filesystem root?
2. What is the difference between an absolute path and a relative path?
3. What do `.` and `..` represent?
4. Why is `ls -lah` useful?

## Troubleshooting

Record any errors encountered, what caused them, and how they were resolved.

If no errors occurred, record that no errors were encountered.

## Reflection

- What did I understand well?
- Which commands can I use independently?
- What still confuses me?
- What should I practise again?

## Next Steps

Continue with Linux file and directory management, including creating, copying, moving, renaming, and inspecting files.
