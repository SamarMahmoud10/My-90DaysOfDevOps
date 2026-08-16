# Day 10 Challenge – File Permissions & File Operations

##  Files & Directories Created
* `devops.txt`: Created empty using `touch`.
* `notes.txt`: Created with text content using `echo`.
* `script.sh`: Created as a shell script using `vim` containing `echo "Hello DevOps"`.
* `project/`: A directory created with `755` permissions.

---

##  Permission Changes (Before & After)

### 1. `script.sh` (Making it Executable)
* **Before:** `-rw-r--r--` (Numeric: `644`) -> No one can execute.
* **After:** `-rwxr-xr-x` (Numeric: `755`) -> Executable by owner, group, and others.

### 2. `devops.txt` (Setting to Read-Only)
* **Before:** `-rw-r--r--` (Numeric: `644`) -> Owner can write.
* **After:** `-r--r--r--` (Numeric: `444`) -> Completely read-only for everyone.

### 3. `notes.txt` (Setting to 640)
* **Before:** `-rw-r--r--` (Numeric: `644`)
* **After:** `-rw-r-----` (Numeric: `640`) -> Owner can read/write, group can read, others have zero access.

---

##  Commands Used & Verification

### Task 1 & 2: File Creation and Reading Operations
```bash
# Create files
touch devops.txt
echo "Continuous Integration and Continuous Deployment (CI/CD) is core to DevOps." > notes.txt

# Create script using vim (or echo for simulation)
echo '#!/bin/bash' > script.sh
echo 'echo "Hello DevOps"' >> script.sh

# Read and verify content
cat notes.txt
view script.sh # Opens in Read-Only mode inside Vim

# Inspect system boundaries
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
```

### Task 4: Modifying Permissions
```bash
# Task 4.1: Make script executable and run it
chmod +x script.sh
./script.sh

# Task 4.2: Set devops.txt to read-only
chmod -w devops.txt

# Task 4.3: Set notes.txt to 640
chmod 640 notes.txt

# Task 4.4: Create directory with 755
mkdir project
chmod 755 project
```

---

##  Task 5: Testing Boundaries & Error Analysis

### 1. Writing to a Read-Only file:
* **Command:** `echo "New Code" >> devops.txt`
* **Error Message:** `-bash: devops.txt: Permission denied`
* **Analysis:** Linux strictly respected the `444` permission set, guarding the storage block even against its own creator user until explicitly revoked or executed via `sudo`.

### 2. Executing a file without Execute permission:
* **Command:** Before running `chmod +x`, attempting `./script.sh`
* **Error Message:** `-bash: ./script.sh: Permission denied`
* **Analysis:** Linux relies solely on the metadata security flags (`x`) to execute binaries, completely ignoring file extensions like `.sh`.

---

## 🧠 What I Learned
1. **The Dynamic Triad of Linux Security:** Deepened my operational mastery over the User-Group-Others boundaries and how bitmask logic maps natively to real-world roles.
2. **Strict Execution Paradigm:** Proved empirically that extensions are cosmetic in Linux; execution is a hard privilege governed strictly by permission flags (`x`).
3. **Auditing Restrictions:** Learned how to safely verify file stability states by intentionally forcing failed file-write cycles to ensure security configurations are locked down.
