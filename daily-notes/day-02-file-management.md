# Day 2 — Linux File and Directory Management

## Objective

Learn how to create, inspect, copy, move, rename, compare, and safely remove files and directories using Linux command-line tools.

The goal of this session was to develop practical file-management skills and understand how these operations help with everyday Linux administration and cybersecurity work.

## Video Assignment

- **Resource:** [Microsoft Learn — How to Work with Directories in the Terminal with Bash](https://learn.microsoft.com/en-us/shows/bash-for-beginners/how-to-work-with-directories-in-the-terminal-with-bash-8-of-20-bash-for-beginners)
- **Key lessons:** Creating directories, creating files, copying and moving files, renaming files, and removing files and empty directories.

### What I Learned

The video introduced commands used to manage files and directories from the terminal. I learned that Linux provides separate commands for different file operations and that I should verify the results instead of assuming a command worked.

## Reading Assignment

- **Resource:** [Ubuntu — The Linux Command Line for Beginners](https://ubuntu.com/desktop/docs/en/latest/tutorial/the-linux-command-line-for-beginners/)
- **Topics studied:** File and directory manipulation, copying files, moving and renaming files, and removing files.

### Three Important Concepts

1. The `cp` command creates a copy of a file or directory.
2. The `mv` command moves a file to another location or renames it.
3. The `rm` and `rmdir` commands remove files and empty directories, respectively.

## Commands Practiced

- `mkdir` — Create directories.
- `touch` — Create an empty file if it does not exist or update its timestamps.
- `printf` — Produce formatted text, which can be redirected into a file.
- `cat` — Display file contents.
- `cp` — Copy files.
- `mv` — Move or rename files.
- `diff` — Compare files line by line.
- `rm -i` — Remove a file after interactively asking for confirmation.
- `rmdir` — Remove an empty directory.
- `ls -l` — Display directory contents in a detailed listing.

## Lab Results

### 1. Creating and Inspecting Files

I created a practice directory containing `drafts`, `archive`, and `reports` subdirectories.

I used `printf` to create text files and `touch` to create an empty file.

**Commands used:**

```bash
mkdir -p labs/day-02-file-management/practice/{drafts,archive,reports}

cd labs/day-02-file-management/practice

printf 'Day 2: Linux file management practice.\n' > notes.txt

printf 'This file will be copied and moved.\n' > source.txt

touch empty-file.txt

cat notes.txt

ls -lah
```

**Result:**

The directory structure was created, the text files contained the expected sentences, and the empty file was created.

**What I learned:**

The `mkdir` command creates directories, while `printf` and output redirection can be used to write text into files. The `cat` command displays a file's contents, and `ls -lah` provides a detailed listing that includes hidden entries.

I also learned that using `>` on an existing file replaces its contents, so I must use it carefully.

### 2. Copying and Comparing Files

I copied `source.txt` into the `drafts` directory.

**Commands used:**

```bash
cp source.txt drafts/source-copy.txt

ls -l drafts

cat drafts/source-copy.txt

diff source.txt drafts/source-copy.txt
```

**Result:**

A copy named `source-copy.txt` was created in the `drafts` directory. Its contents matched those of the original file.

The `diff` command produced no output when the files were identical.

**What I learned:**

The `cp` command creates a separate copy while leaving the original file in its original location. The `diff` command helps verify whether the contents of two files differ.

### 3. Moving and Renaming Files

I moved the copied file from `drafts` to `archive` and renamed an empty file.

**Commands used:**

```bash
mv drafts/source-copy.txt archive/source-copy.txt

mv empty-file.txt renamed-empty-file.txt

ls -l drafts
ls -l archive
ls -l
```

**Result:**

The copied file was moved into `archive`, and the empty file was renamed to `renamed-empty-file.txt`.

After the move, the copied file was no longer present in `drafts`.

**What I learned:**

The `mv` command can be used both to move files between directories and to change filenames. Moving a file is different from copying it because the file is relocated rather than duplicated.

### 4. Creating and Verifying a Backup

I created a backup of `notes.txt` in the `reports` directory.

**Commands used:**

```bash
cp notes.txt reports/notes-backup.txt

diff notes.txt reports/notes-backup.txt
```

**Result:**

The backup file was created, and `diff` produced no output because both files contained identical text.

**What I learned:**

Creating a copy before changing an important file can help preserve the original information. Comparing the original and backup files is a simple way to verify that their contents match.

### 5. Safely Removing a Practice File

Before removing the copied file, I inspected its location.

**Commands used:**

```bash
ls -l archive/source-copy.txt

rm -i archive/source-copy.txt
```

After running the second command, I confirmed the removal when prompted.

I then removed the empty `drafts` directory.

```bash
rmdir drafts

ls -l archive
ls -l reports
```

**Result:**

The selected practice file was removed, and the empty `drafts` directory was deleted successfully. The backup file remained in `reports`.

**What I learned:**

The `rm` command removes files, while `rmdir` removes empty directories. The `-i` option adds a confirmation step before removing a file.

I also learned to inspect the exact target before deleting it because command-line deletion may not be recoverable through the desktop Trash.

## Independent Challenge

### Challenge 1 — Create a New Working Directory

**Task:** Create a directory named `challenge` with an `archive` subdirectory.

**Commands used:**

```bash
mkdir -p labs/day-02-file-management/challenge/archive

cd labs/day-02-file-management/challenge

pwd
```

**Result:** The working directory was set to the new challenge directory.

**What I learned:** The `mkdir -p` command can create nested directories, including any required parent directories.

### Challenge 2 — Create the Original File

**Task:** Create a file named `original.txt` with a sentence of my choice.

**Command used:**

```bash
printf 'Practising Linux file management independently.\n' > original.txt

cat original.txt
```

**Result:** The file was created and displayed the intended sentence.

**What I learned:** I can use `printf` and output redirection to create files containing specific text.

### Challenge 3 — Copy and Rename the Backup

**Task:** Copy the original file and rename the copy.

**Commands used:**

```bash
cp original.txt backup.txt

mv backup.txt backup-final.txt

ls -l
```

**Result:** The directory contained the original file and the renamed backup.

**What I learned:** I can combine `cp` and `mv` to create a backup and then rename it without altering the original.

### Challenge 4 — Move and Verify the Backup

**Task:** Move the renamed backup into `archive` and compare its contents with the original file.

**Commands used:**

```bash
mv backup-final.txt archive/backup-final.txt

diff original.txt archive/backup-final.txt

ls -l archive
```

**Result:** The renamed backup was moved into `archive`. The `diff` command produced no output, indicating that the files had identical contents.

**What I learned:** I can use directory paths with `mv` to organize files and use `diff` to check whether a copied file matches its original.

### Challenge 5 — Remove the Backup Safely

**Task:** Remove only the backup file and confirm that the original remains.

**Commands used:**

```bash
rm -i archive/backup-final.txt

test -f original.txt && echo "original.txt still exists"

ls -la archive
```

When prompted by `rm -i`, I confirmed the removal.

**Result:** The original file remained in the challenge directory, and the archive directory was empty apart from its standard directory entries.

**What I learned:** I can selectively remove a backup file without deleting the original. Checking the filesystem after deletion helps confirm the result.

### Independent Challenge Reflection

The challenge required me to apply file-management commands in a different sequence from the guided lab.

I practised creating files, copying and renaming them, moving them into another directory, comparing their contents, and removing a selected file.

These exercises helped reinforce the importance of checking file locations and contents after each operation.

## Troubleshooting

During this lab, the most important precaution was checking the target and destination paths before moving or removing files.

The commands behaved as expected when the directories and filenames were correct.

If a command reports that a file or directory does not exist, I can use `pwd` to inspect my current location and `ls -lah` to check the available files and directories.

I should correct the path or filename before repeating the operation. I should never work around an unexpected deletion error by using more aggressive commands without understanding the cause.

## Knowledge Check

### 1. What is the difference between `cp` and `mv`?

The `cp` command creates a copy of a file or directory, leaving the original in place. The `mv` command moves a file or directory to another location or renames it. A successful move ordinarily removes the item from its original location.

### 2. What happens when I use `>` on a file that already contains text?

The `>` redirection operator replaces the existing contents of the destination file with the new output. If the file does not exist, it creates it.

For example:

```bash
printf 'New content\n' > notes.txt
```

This replaces the existing contents of `notes.txt`. I must be careful when using `>` because it can overwrite information.

### 3. What is the difference between `rm` and `rmdir`?

The `rm` command removes files. The `rmdir` command removes empty directories. `rmdir` will not normally remove a directory containing files.

For safer practice, I can use `rm -i` to receive a confirmation prompt before removing a file.

### 4. How can `diff` help verify a copy?

The `diff` command compares two files line by line. If two ordinary text files are identical, it normally produces no output. If their contents differ, it displays the differences.

For example:

```bash
diff original.txt backup.txt
```

No output indicates that the two files have matching contents.

### 5. Why is it important to inspect a target before deleting it?

Inspecting the target helps ensure that I am deleting the intended file rather than important data. Command-line deletion can permanently remove a file without placing it in the desktop Trash.

Using `ls -l` to verify the path and `rm -i` for confirmation reduces the risk of accidental deletion.

## Reflection

### What I Learned

I learned how to create directories and files, inspect file contents, copy files, move and rename files, compare files using `diff`, and safely remove practice files.

I also learned that verifying the results of commands is an important part of using Linux responsibly.

### Which Commands Can I Now Use Independently?

I can practise using `mkdir`, `touch`, `printf`, `cat`, `ls -l`, `cp`, `mv`, `diff`, `rm -i`, and `rmdir` to manage files in a controlled directory.

### Which Command Confused Me Most?

I need to identify the command that required the most thought during my own practice and record what made it difficult.

### What Mistake Did I Make, and What Did It Teach Me?

This section should document any actual mistake encountered during the lab. For example, if I used an incorrect path, I can explain how checking `pwd` and `ls` helped me locate the problem.

If I made no mistakes, I can record that and identify the parts that still require more practice.

### What Should I Practise Again?

I should practise using relative paths with `cp` and `mv`, verify copies with `diff`, and carefully check filenames and directories before deleting anything.

## Conclusion

Day 2 strengthened my Linux command-line skills by teaching me how to manage files and directories in a controlled environment.

I now understand the differences between copying and moving files, the importance of checking file contents, and the need to verify a deletion target before removing it.

These skills provide a foundation for future Linux topics, including permissions, ownership, shell scripting, system administration, and cybersecurity investigations.
