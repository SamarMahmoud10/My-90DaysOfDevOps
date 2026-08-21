# Day 12 – Breather & Revision (Days 01–11)

##  Day 01 - Mindset & Plan Review
- My goals from Day 01 are still on track. 
- I need to focus more on hands-on practice rather than just reading.

##  Hands-on Rerun Observations

### 1. Processes & Services (Days 04-05)
I ran the following commands to check system health:
- `systemctl status ssh` -> Observed that the SSH service is active and running.
- `ps aux | grep top` -> Monitored active processes efficiently.

### 2. File Skills & Permissions (Days 06-11)
I practiced quick operations using:
- `mkdir test_dir` and `touch test_file.txt` to test file creation.
- `chmod 755 test_file.txt` to modify permissions.
- Verified changes using `ls -l`.

### 3. User & Group Sanity
- Recreated a quick user test using `id` to check the current user's groups and privileges.

---

## 📝 Mini Self-Check Answers

### 1 Which 3 commands save you the most time right now, and why?
- `ls -la`: Quickly lists all files including hidden ones with details.
- `history`: Helps me reuse complex commands I ran earlier without retyping.
- `chmod`: Fast and essential for fixing permission issues on the fly.

### 2 How do you check if a service is healthy? List the exact 2–3 commands you’d run first.
- `systemctl status <service-name>`
- `journalctl -u <service-name> --no-pager | tail -n 20`
- `ps aux | grep <service-name>`

### 3 How do you safely change ownership and permissions without breaking access? Give one example command.
- I use descriptive or exact permissions rather than `777`.
- **Example:** `sudo chown webuser:webgroup index.html && chmod 644 index.html` (This grants read/write to owner, and read-only to others).

### 4 What will you focus on improving in the next 3 days?
- I will focus on improving my understanding of  Git branching or Bash scripting syntax .

---
