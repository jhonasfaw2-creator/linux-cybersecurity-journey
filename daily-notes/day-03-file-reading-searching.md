# Day 3 — Linux File Reading and Text Searching

## Objective
Learn how to read text files, extract selected lines, search for matching text, count results, and combine commands using pipes.

## Key Concepts Learned

### 1. Reading Files
* **`cat` (Concatenate):** Prints the entire contents of a file directly to standard output (stdout). Ideal for quick checks of small configuration files, but inefficient and overwhelming for massive log files because it floods the terminal buffer.
* **`head -n`:** Displays the first *n* lines of a file (default is 10). Essential for checking file headers or initial configuration blocks.
* **`tail -n`:** Displays the last *n* lines of a file. Extremely useful for examining recent log entries, especially when paired with `-f` (follow) to monitor live log updates in real time.
* **`less`:** An interactive, paginated file viewer. Unlike `cat`, it loads files dynamically, allowing you to scroll up and down line-by-line or page-by-page, search for text using `/`, and exit cleanly with `q`.

### 2. Searching Text
* **`grep`:** Searches plain-text data sets for lines matching a regular expression or search string.
* **`-i` flag:** Makes the search case-insensitive (e.g., matching both "Error" and "ERROR").
* **`-n` flag:** Prefixes each matching line with its corresponding line number in the file, making it easy to locate issues during debugging.

### 3. Counting and Pipelines
* **`wc` (Word Count):** Measures text metrics. Using `-l` counts lines, `-w` counts words, and `-c` counts bytes/characters.
* **Pipes (`|`):** The pipe operator takes the standard output (stdout) of the command on its left and feeds it directly as standard input (stdin) to the command on its right. This allows you to chain tools together (e.g., searching logs and counting the results instantly).

---

## Lab Results (`sample.log`)
* **Total line count:** `24 lines`
* **First three lines:**
  ```text
  [INFO] 2026-10-26 08:00:01 - System boot initialized successfully.
  [INFO] 2026-10-26 08:00:02 - Network interface wlan0 connected.
  [DEBUG] 2026-10-26 08:00:03 - Loading environment variables.
  ```
* **Last three lines:**
  ```text
  [WARNING] 2026-10-26 21:15:40 - High memory utilization detected (88%).
  [ERROR] 2026-10-26 21:30:12 - Database connection timeout.
  [INFO] 2026-10-26 22:00:00 - Routine backup completed.
  ```
* **Number of ERROR entries:** `4` *(via `grep -i "error" sample.log | wc -l`)*
* **Number of WARNING entries:** `6` *(via `grep -i "warning" sample.log | wc -l`)*
* **Number of lines containing "failed":** `2` *(via `grep -i "failed" sample.log | wc -l`)*

---

## Independent Challenge
* **Creation:** Created `challenge.log` using a multiline `cat` EOF block containing mixed system messages, application errors, and access logs.
* **Commands Used:** 
  ```bash
  cat << 'EOF' > challenge.log
  [2026-10-26] AUTH_SUCCESS: User admin logged in from 192.168.1.50
  [2026-10-26] AUTH_FAIL: Invalid password for user root
  [2026-10-26] DB_QUERY_OK: SELECT * FROM users
  [2026-10-26] AUTH_FAIL: User guest tried unauthorized route
  EOF
  
  grep -i "auth_fail" challenge.log | wc -l
  ```
* **Actual Output:** Returned a count of `2` failed authentication attempts.
* **Completion Status:** Completed independently without issues.

---

## Troubleshooting
* **Errors Encountered:** No errors occurred during this session; command syntax and flag behaviors functioned as expected in the terminal.

---

## Knowledge Check
1. **What is the difference between `head` and `tail`?**  
   `head` outputs the beginning (top) lines of a file, whereas `tail` outputs the ending (bottom) lines.
2. **When is `less` more useful than `cat`?**  
   `less` is much more useful for large files because it opens files interactively for scrolling and searching without cluttering or flooding the terminal screen.
3. **What does `grep -i` do?**  
   It performs a case-insensitive text search, ignoring uppercase and lowercase differences.
4. **What information does `wc -l` provide?**  
   It provides the exact count of newlines (total number of lines) in a file or input stream.
5. **What does the pipe (`|`) do?**  
   It redirects the standard output of one command to become the standard input of the next command.
6. **What does a `grep` exit status of 1 normally indicate?**  
   It indicates that the search completed successfully, but **no matching lines were found** (an exit status of 0 means matches were found, and >1 indicates a syntax or file read error).

---

## Reflection
* **Which command did I find most useful?**  
  `grep` combined with `wc -l` via a pipe (`|`) is exceptionally powerful for quickly extracting metrics from raw logs.
* **Which command do I need to practise again?**  
  Regular expression (`grep -E`) modifiers for advanced pattern matching.
* **How could these commands help me investigate system logs?**  
  They allow you to instantly filter gigabytes of logs down to specific error codes, timestamps, or IP addresses during incident triage or security investigations.
* **What did I learn from the independent challenge?**  
  Building quick mock log files makes testing complex multi-pipe grep queries fast and reliable.

---

## Next Steps
* Proceed to **Linux Permissions and Ownership** (`chmod`, `chown`, `umask`).
