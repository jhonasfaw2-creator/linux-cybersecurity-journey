# Lab 04 — Linux File Permissions

**Category:** Linux System Administration and Security  
**Tags:** `#linux` `#sysadmin` `#permissions` `#security` `#chmod` `#terminal` `#devops`

## Objective

Practise inspecting file ownership and controlling file and directory permissions in a safe environment.

The goal is to understand how Linux uses users, groups, and read, write, and execute permissions to control access to files and directories.

## Environment

- **Operating system:** Ubuntu
- **Shell:** Zsh
- **Scope:** Local permission practice
- **Difficulty:** Beginner
- **Risk level:** Low; using self-created practice files

## Exercise 1 — Inspect Ownership and Permissions

### Commands executed

```bash
id
ls -l confidential.txt
```

### Observed output

```text
uid=1000(student) gid=1000(student) groups=1000(student),4(adm),27(sudo)

-rw-r--r-- 1 student student 35 Oct 27 10:00 confidential.txt
```

### Breakdown of the permission listing

The listing contains several fields:

```text
-rw-r--r-- 1 student student 35 Oct 27 10:00 confidential.txt
```

- **File type (`-`):** Indicates a regular file. A `d` would indicate a directory.
- **Owner permissions (`rw-`):** The owner can read and write the file.
- **Group permissions (`r--`):** Members of the associated group have read permission.
- **Other permissions (`r--`):** Other users have read permission.
- **Hard links (`1`):** The number of hard links to the file.
- **Owner (`student`):** The user who owns the file.
- **Group (`student`):** The group associated with the file.
- **Size (`35`):** The file size in bytes.
- **Timestamp:** The displayed modification date and time.
- **Filename:** `confidential.txt`.

### What I learned

The `id` command displays the current user's identity and group memberships. The `ls -l` command provides detailed information about file permissions, ownership, size, and modification time.

Linux separates permissions into three categories: the owner, the associated group, and others.

## Exercise 2 — Restrict File Permissions

### Initial permissions

```bash
ls -l confidential.txt
```

Observed output:

```text
-rw-r--r-- 1 student student 35 Oct 27 10:00 confidential.txt
```

### Set permission mode 600

```bash
chmod 600 confidential.txt
ls -l confidential.txt
```

Observed output:

```text
-rw------- 1 student student 35 Oct 27 10:00 confidential.txt
```

### Explanation of mode 600

The numeric permissions are calculated using these values:

- Read = 4
- Write = 2
- Execute = 1

Therefore:

- **Owner:** 6 = 4 + 2, meaning read and write.
- **Group:** 0, meaning no permissions.
- **Others:** 0, meaning no permissions.

Mode `600` is represented as `-rw-------`.

It grants the owner read and write permissions, while the group and others receive no permissions through the standard permission bits.

### Set permission mode 640

```bash
chmod 640 confidential.txt
ls -l confidential.txt
```

Observed output:

```text
-rw-r----- 1 student student 35 Oct 27 10:00 confidential.txt
```

### Explanation of mode 640

- **Owner:** 6 = read and write.
- **Group:** 4 = read only.
- **Others:** 0 = no permissions.

Mode `640` is represented as `-rw-r-----`.

### What I learned

The `chmod` command changes file permissions. Numeric notation allows me to specify permissions for the owner, group, and others separately.

Restricting file permissions can reduce unnecessary access to sensitive information.

## Exercise 3 — Make a Script Executable

### Create a practice script

```bash
cat > hello.sh <<'EOF'
#!/bin/zsh
echo "Hello, Linux Permissions!"
EOF
```

Set a known starting permission mode:

```bash
chmod 644 hello.sh
ls -l hello.sh
```

Expected output:

```text
-rw-r--r-- ... hello.sh
```

### Attempt execution before adding execute permission

```bash
./hello.sh
```

Expected result:

```text
zsh: permission denied: ./hello.sh
```

The file does not have execute permission, so the shell cannot execute it directly under this permission configuration.

### Add execute permission for the owner

```bash
chmod u+x hello.sh
ls -l hello.sh
```

Expected output:

```text
-rwxr--r-- ... hello.sh
```

The mode is now `744`. The `u+x` notation adds execute permission for the file owner without adding execute permission for the group or others.

### Restrict the script to the owner

```bash
chmod 700 hello.sh
ls -l hello.sh
```

Expected output:

```text
-rwx------ ... hello.sh
```

The mode is now `700`: the owner can read, write, and execute the script, while the group and others receive no permissions through the standard permission bits.

### Execute the script

```bash
./hello.sh
```

Expected output:

```text
Hello, Linux Permissions!
```

### What I learned

A script needs appropriate execute permissions to run directly as a program. The symbolic form `chmod u+x` adds execute permission for the owner, while numeric mode `700` restricts the standard permissions to the owner.

The exact result of `chmod u+x` depends on the file's starting permissions. It does not automatically grant execute permission to the group or others.

## Exercise 4 — Change Directory Permissions

### Create practice directories

```bash
mkdir -p private shared
```

### Restrict the private directory

```bash
chmod 700 private
ls -ld private
```

Observed output:

```text
drwx------ 2 student student 4096 Oct 27 10:10 private
```

The owner has read, write, and execute permissions. The group and others have no permissions through the standard permission bits.

### Set permissions on the shared directory

```bash
chmod 755 shared
ls -ld shared
```

Observed output:

```text
drwxr-xr-x 2 student student 4096 Oct 27 10:10 shared
```

Mode `755` grants read, write, and execute permissions to the owner, and read and execute permissions to the group and others.

For directories, execute permission allows traversal, while read permission allows listing directory entries. Write permission is generally required to create, remove, or rename entries, subject to other filesystem access controls.

### File and directory permissions compared

| Permission | Regular file | Directory |
|---|---|---|
| Read (`r`) | Read file contents | List directory entries |
| Write (`w`) | Modify file contents | Create, remove, or rename entries, subject to other requirements |
| Execute (`x`) | Execute the file as a program when applicable | Traverse the directory and access entries by name |

### What I learned

Directory permissions control how users access directory contents. For a directory, execute permission is particularly important because it permits traversal. Directory write permission also affects the ability to create, rename, and remove entries.

## Exercise 5 — Independent Challenge

### Objective

Create practice files and apply specific permission modes independently, then verify the results using `stat` and `ls`.

### Create the test files

```bash
touch secure_data.log task_script.sh
```

### Set the permissions

```bash
chmod 600 secure_data.log
chmod 750 task_script.sh
```

### Verify the permissions

```bash
stat -c "%a %A %n" secure_data.log
stat -c "%a %A %n" task_script.sh
```

Observed output:

```text
600 -rw------- secure_data.log
750 -rwxr-x--- task_script.sh
```

### Verification results

**`secure_data.log`**

- Numeric mode: `600`
- Symbolic mode: `-rw-------`
- Owner: Read and write
- Group: No permissions
- Others: No permissions

**`task_script.sh`**

- Numeric mode: `750`
- Symbolic mode: `-rwxr-x---`
- Owner: Read, write, and execute
- Group: Read and execute
- Others: No permissions

The file `task_script.sh` was used to practise and verify permissions. Assigning execute permission does not by itself add script contents or guarantee that an empty file can execute successfully.

### What I learned

The independent challenge reinforced the relationship between numeric and symbolic permissions. I practised applying specific permission modes and verifying them instead of relying on assumptions.

## Troubleshooting

### Issue: Permission denied when executing `hello.sh`

**Cause:** The script did not initially have execute permission.

**Resolution:** I added execute permission for the owner using:

```bash
chmod u+x hello.sh
```

I then restricted the file to owner-only permissions using:

```bash
chmod 700 hello.sh
```

After verifying the permissions, I executed the script successfully.

### General troubleshooting practices

- Use `pwd` to verify the current directory.
- Use `ls -l` to inspect permissions and ownership.
- Use `stat` to verify numeric and symbolic permission modes.
- Confirm that a script has a valid interpreter line and appropriate execute permissions before attempting to run it.
- Record actual errors and their solutions rather than assuming that a command succeeded.

## Security Considerations

- Only used files and directories created for this practice lab.
- Avoided using `sudo` or changing critical system-file permissions.
- Avoided unnecessarily broad permissions such as `777`.
- Verified permission changes using `ls -l` and `stat`.
- Practised the principle of least privilege by granting only the permissions required for each exercise.

## Conclusion

Linux permissions are a fundamental part of system security. They control how owners, groups, and other users can interact with files and directories.

During this lab, I practised inspecting ownership, understanding read, write, and execute permissions, changing file permissions with `chmod`, making a script executable, and controlling directory access.

These skills establish a foundation for further study of Linux ownership, groups, default permissions, access control, system administration, and cybersecurity.

## Further Practice

- Study the `chown` and `chgrp` commands for ownership and group management.
- Learn how the `umask` setting affects default permissions.
- Explore how directory permissions affect file access.
- Practise interpreting permission output from real Linux files without changing system settings.
- Learn about special permission bits after mastering the basic permissions.
