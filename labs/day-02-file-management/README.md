# Lab 02 — Linux File and Directory Management

## 1. Objective

The objective of this lab is to practise creating, inspecting, copying, moving, renaming, comparing, and safely removing files and directories using Linux command-line tools.

This lab builds practical Linux skills that are useful for system administration and future cybersecurity work.

## 2. Environment

- **Operating system:** Ubuntu
- **Shell:** Zsh
- **Lab type:** Local Linux practice
- **Difficulty:** Beginner
- **Scope:** File and directory management
- **Safety:** All file operations are performed inside my personal learning repository.

## 3. Commands Practiced

| Command | Purpose |
|---|---|
| `mkdir` | Create directories |
| `touch` | Create an empty file if it does not exist |
| `printf` | Generate formatted text |
| `cat` | Display file contents |
| `ls -lah` | List files and directories, including hidden entries |
| `cp` | Copy files |
| `mv` | Move or rename files |
| `diff` | Compare file contents |
| `rm -i` | Remove a file with an interactive confirmation |
| `rmdir` | Remove an empty directory |

## 4. Practical Exercises

### Exercise 1 — Create a Lab Workspace

**Commands executed:**

```bash
cd ~/cybersecurity-labs/linux-journey

mkdir -p labs/day-02-file-management/practice/{drafts,archive,reports}

cd labs/day-02-file-management/practice

pwd
ls -lah
```

**Expected result:**

The command sequence creates the `practice` directory and its three subdirectories: `drafts`, `archive`, and `reports`.

The `pwd` command displays the current directory, and `ls -lah` lists its contents.

**What I learned:**

The `mkdir -p` command can create nested directories and does not report an error simply because an existing directory is already present.

### Exercise 2 — Create and Inspect Files

**Commands executed:**

```bash
printf 'Day 2: Linux file management practice.\n' > notes.txt

printf 'This file will be copied and moved.\n' > source.txt

touch empty-file.txt

cat notes.txt

ls -lah
```

**Expected result:**

Three files are created:

- `notes.txt`, containing the Day 2 practice sentence.
- `source.txt`, containing the sentence about copying and moving.
- `empty-file.txt`, initially empty.

The `cat` command displays the contents of `notes.txt`.

**What I learned:**

The `printf` command can generate text that is written to a file using output redirection. The `touch` command creates an empty file if it does not exist. The `cat` and `ls -lah` commands help inspect file contents and directory entries.

The `>` operator overwrites existing file contents, so it must be used carefully.

### Exercise 3 — Copy and Compare a File

**Commands executed:**

```bash
cp source.txt drafts/source-copy.txt

ls -l drafts

cat drafts/source-copy.txt

diff source.txt drafts/source-copy.txt
```

**Expected result:**

The file `source-copy.txt` appears inside `drafts`. Its contents match those of `source.txt`.

If the two files are identical, `diff` produces no output.

**What I learned:**

The `cp` command creates a separate copy while keeping the original file in its original location. The `diff` command can help verify that the copied text matches the original.

### Exercise 4 — Move and Rename Files

**Commands executed:**

```bash
mv drafts/source-copy.txt archive/source-copy.txt

mv empty-file.txt renamed-empty-file.txt

ls -l drafts
ls -l archive
ls -l
```

**Expected result:**

The copied file is moved from `drafts` to `archive`. The empty file is renamed to `renamed-empty-file.txt`.

After the move, `source-copy.txt` no longer appears in `drafts`.

**What I learned:**

The `mv` command can move files between directories or rename them. Unlike copying, moving a file does not normally leave a separate copy at its original location.

### Exercise 5 — Create and Verify a Backup

**Commands executed:**

```bash
cp notes.txt reports/notes-backup.txt

diff notes.txt reports/notes-backup.txt
```

**Expected result:**

The backup file is created inside `reports`. If its contents match those of `notes.txt`, `diff` produces no output.

**What I learned:**

Creating backups can help preserve information before making changes. Comparing the original and backup is a useful way to verify that the contents match.

### Exercise 6 — Safely Remove a Practice File

**Commands executed:**

```bash
ls -l archive/source-copy.txt

rm -i archive/source-copy.txt
```

After inspecting the target, I confirm the removal when prompted.

Next, I remove the empty `drafts` directory:

```bash
rmdir drafts

ls -l archive
ls -l reports
```

**Expected result:**

The selected copy is removed from `archive`, and the empty `drafts` directory is deleted. The backup `reports/notes-backup.txt` remains in place.

**What I learned:**

The `rm` command removes files, while `rmdir` removes empty directories. The `-i` option requests confirmation before removing a file.

Checking the exact path before deletion is important because command-line deletion does not necessarily move files to the desktop Trash.

## 5. Final Lab Verification

After completing the exercises, the remaining contents of the practice directory should be:

```text
practice/
├── archive/
├── notes.txt
├── renamed-empty-file.txt
├── reports/
│   └── notes-backup.txt
└── source.txt
```

The `archive` directory and the renamed empty file remain, while the `drafts` directory has been removed.

The original files remain available, and the backup is stored in `reports`.

**Verification commands:**

```bash
pwd
find . -maxdepth 2 -print
diff notes.txt reports/notes-backup.txt
```

If the backup and original text are identical, the final `diff` command should produce no output.

## 6. Troubleshooting

Potential problems during this lab include:

- **File not found:** Check the current directory with `pwd` and inspect available files using `ls -lah`.
- **Incorrect destination path:** Verify that the destination directory exists before using `cp` or `mv`.
- **Directory not empty:** `rmdir` only removes empty directories. Inspect the directory contents before deciding what to do.
- **Unexpected file contents:** Use `cat` to inspect the file and `diff` to compare it with the intended copy.
- **Accidental overwrite:** Be careful when using `>` because it replaces existing contents.

No troubleshooting incident should be claimed unless it reflects an error that actually occurred during the lab.

## 7. Security and Safety Considerations

File-management operations are important in cybersecurity because administrators and analysts regularly handle configuration files, logs, backups, and scripts.

The following precautions were applied to this lab:

1. All practice files were created inside my own learning repository.
2. Files were inspected before deletion.
3. The interactive `rm -i` option was used to request confirmation.
4. No administrator privileges were needed.
5. Important original files were retained when practising copying and moving.

These practices help reduce accidental data loss and encourage careful handling of files.

## 8. Conclusion

This lab introduced essential Linux file-management operations through practical exercises.

I practised creating directories and files, displaying file contents, copying and comparing files, moving and renaming files, creating a backup, and safely removing a practice file.

I also learned the importance of checking the current directory, verifying command results, and inspecting deletion targets before removing them.

These skills establish a foundation for future Linux topics, including file permissions, ownership, process management, shell scripting, and cybersecurity investigations.

## 9. Further Practice

My next practice goals are:

- Learn more about file permissions and ownership.
- Explore copying and moving directories.
- Study wildcard patterns and filename matching.
- Practise using `find` to locate files.
- Learn how to use shell redirection and pipes safely.

The goal is to become comfortable performing these operations independently and understanding the effects of each command.
