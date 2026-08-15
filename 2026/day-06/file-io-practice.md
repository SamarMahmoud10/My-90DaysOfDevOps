# Day 06 – Linux Fundamentals: Read and Write Text Files

## Task Overview
Today, I practiced basic file input/output (I/O) operations using Linux fundamental commands. I focused on creating, writing, appending, and reading text files directly via the CLI, building the fundamental skills required to manage configurations and automation scripts in DevOps.

---

## 1. Step-by-Step Command Flow & Practice Log

Here is the exact sequence of commands I ran on my system to practice file management:

### Step 1: Create an Empty File
* **Command Run:**
  ```bash
  touch notes.txt
  ```
* **Observation:** An empty text file named `notes.txt` was successfully created in the current working directory.

### Step 2: Write Initial Line (Overwrite Mode)
* **Command Run:**
  ```bash
  echo "Line 1: Learning Linux File I/O for DevOps." > notes.txt
  ```
* **Observation:** The single bracket `>` created the content and wrote the first line into the file.

### Step 3: Append Additional Content
* **Command Run:**
  ```bash
  echo "Line 2: Practicing redirection operators like double brackets." >> notes.txt
  ```
* **Observation:** The double bracket `>>` appended the second line to the end of the file safely without overwriting Line 1.

### Step 4: Write and Display Simultaneously Using `tee`
* **Command Run:**
  ```bash
  echo "Line 3: Using the tee command to write and stream output at the same time." | tee -a notes.txt
  ```
* **Observation:** The `tee -a` command successfully added the third line to the file while printing the exact text to my terminal screen instantly.

---

## 2. Reading and Inspecting File Content

### Step 5: Read the Entire File
* **Command Run:**
  ```bash
  cat notes.txt
  ```
* **Output Observed:**
  ```text
  Line 1: Learning Linux File I/O for DevOps.
  Line 2: Practicing redirection operators like double brackets.
  Line 3: Using the tee command to write and stream output at the same time.
  ```

### Step 6: Inspecting Specific Parts (File Head)
* **Command Run:**
  ```bash
  head -n 2 notes.txt
  ```
* **Output Observed:**
  ```text
  Line 1: Learning Linux File I/O for DevOps.
  Line 2: Practicing redirection operators like double brackets.
  ```
* **Note:** It isolated and printed only the first 2 lines from the top of the file.

### Step 7: Inspecting Specific Parts (File Tail)
* **Command Run:**
  ```bash
  tail -n 2 notes.txt
  ```
* **Output Observed:**
  ```text
  Line 2: Practicing redirection operators like double brackets.
  Line 3: Using the tee command to write and stream output at the same time.
  ```
* **Note:** It isolated and printed only the last 2 lines from the bottom of the file.

---

## 3. DevOps Takeaway
Manipulating text files quickly from the terminal is an essential routine for configuring files, setting up environment variables, and analyzing dense system logs. Mastering these standard redirection operators (`>`, `>>`) and stream filters (`tee`, `head`, `tail`) ensures faster troubleshooting and reliable automation workflows.
