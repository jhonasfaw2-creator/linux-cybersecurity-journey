Day 4 — Linux Users, Groups and Permissions

## Objective

Understand file ownership, user groups, and Linux read, write, and execute permissions.

## Video Assignment

Resource: Travis Media — Linux File Permissions in 5 Minutes

Key lessons: Permission groups (ugo), rwx breakdown, chmod command usage, and numeric/octal modes.

# Reading Assignment

Ubuntu — Welcome to the Terminal


## Commands Practiced

whoami

id

groups

ls -l

ls -ld

stat

chmod

cat

## Key Concepts Learned

Differences between:

Owner, group and others: The owner is the specific user who owns the file; the group is a collection of users sharing access rights; others refers to every other user on the system.

Read, write and execute permissions: Read (r) lets you view file contents or list directory files; write (w) lets you modify or delete files; execute (x) lets you run scripts/binaries or traverse into directories.

Symbolic and numeric chmod notation: Symbolic notation uses letters and operators (e.g., u+x, g-w), while numeric notation uses 3-digit octal values based on the sum of read (4), write (2), and execute (1) values (e.g., 755, 640).

File permissions and directory permissions: On a file, permissions control reading, writing, and running code. On a directory, execute permission is required just to enter (cd) into the directory or access paths inside it.

## Lab Results

## Observed permission modes:

confidential.txt: -rw-------

hello.sh: -rwxr-xr-x

private/: drwx------

shared/: drwxr-xr-x

## Independent Challenge

Created test files and directories (confidential.txt, hello.sh, private/, and shared/). Inspected their default modes using ls -l and ls -ld. Applied various permission changes using both numeric (chmod 640, chmod 755) and symbolic modes (chmod u+x), and verified each change using stat and ls -l.

## Troubleshooting

Error: Permission denied when trying to execute ./hello.sh.

Cause: The script lacked the execute (x) permission bit.

Solution: Granted execute permission using chmod +x hello.sh.

## Knowledge Check

What does rwx mean? Read (r), write (w), and execute (x) permissions.

How does chmod 640 differ from chmod 600? 640 gives the file owner read/write access and the group read access, whereas 600 restricts read/write access exclusively to the owner.

What does chmod u+x do? Adds execute permission for the file owner.

Why are directory execute permissions important? Without execute permission on a directory, you cannot enter it or access any files inside it, even if you have read or write permissions on the files themselves.

Why should we avoid granting unnecessarily broad permissions? To maintain security, protect private data from unauthorized access, and follow the Principle of Least Privilege.

## Reflection

What did I understand well? How octal numbering (4, 2, 1) maps directly to read, write, and execute permissions.

Which command do I need to practise again? chmod with complex symbolic multi-user flags (e.g., g+s, a+r).

How can file permissions help protect a Linux system? They isolate user spaces, prevent unauthorized file modifications, and ensure sensitive system binaries or configs cannot be tampered with.

What do I want to learn next? Advanced ownership changes (chown, chgrp) and default permission masks (umask).

## Next Steps

Study additional permission modes, ownership, groups and default permissions through controlled practice. 





