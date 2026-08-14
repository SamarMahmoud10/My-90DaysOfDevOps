#  Ultra-Complete DevOps Linux Commands Cheat Sheet (Day 03)

A comprehensive, production-grade command reference guide optimized for infrastructure engineers, covering system monitoring, process reaping, log parsing, and advanced network triage.

---

##  1. System & Resource Monitoring (Infrastructure Health)

### `htop` / `top` - Real-Time Resource Profiler
*   **Usage:** Monitor live CPU cores, RAM allocation, Swap space, and system Load Averages.
*   **Advanced Flags:**
    *   `htop -u jenkins` : Filters and shows processes owned only by the 'jenkins' user.
    *   `top -b -n 1` : Batch mode operation. Spits out a single static text snapshot of system resource metrics (highly useful for automation scripts).

### `df -hT` & `df -ih` - Disk Space & File Allocation Table
*   **Usage:** Checks storage metrics across all mounted file systems.
*   **Advanced Flags:**
    *   `df -hT` : Displays disk space in a human-readable format (GB/MB) along with the filesystem type (e.g., ext4, xfs, overlay).
    *   `df -ih` : Displays **Inode** capacity status. Crucial for diagnosing "No space left on device" errors caused by millions of tiny files when physical storage appears empty.

### `free -m` - Memory Allocation Grid
*   **Usage:** Displays total, occupied, and unallocated RAM and Swap space.
*   **DevOps Focus:** Always inspect the `available` column rather than `free`, as Linux utilizes unused memory for Buffers/Cache but frees it instantly upon application request.

### `uptime` - Server Continuity Ledger
*   **Usage:** Displays current system time, server runtime duration since last boot, logged-in sessions, and the load average metrics over 1, 5, and 15-minute intervals.

---

##  2. Process Management & Signal Reaping

### `ps aux` - Global Process Topology Snapshot
*   **Usage:** Formats and prints out an extensive breakdown of every process active on the OS.
*   **Flags Decoded:** `a` (all users) + `u` (displays resource consumption & user details) + `x` (includes background daemons detached from a terminal).

### `pgrep <process_name>` - Name-to-PID Translation
*   **Usage:** Searches the active process table and returns the exact numerical Process IDs matching the process name query, bypassing the need for long pipes.

### `kill`, `pkill`, & `killall` - Signal Dispatches
*   **Usage:** Transmits process lifecycle modification signals to active operations.
*   **Commands Framework:**
    *   `kill <PID>` : Dispatches default `SIGTERM (15)` to request a safe, graceful application shutdown.
    *   `kill -9 <PID>` : Dispatches unblockable `SIGKILL (9)` forcing the Kernel to wipe the process instantly.
    *   `pkill -9 nginx` : Forcibly terminates all operational units running under the name string "nginx".

---

##  3. Advanced File System & Production Log Inspection

### `tail -f` & `tail -F` - Dynamic Output Streaming
*   **Usage:** Prints the trailing edges of dynamic output files.
*   **Advanced Flags:**
    *   `tail -f /var/log/nginx/error.log` : Keeps the stdout stream alive, printing new errors in real-time.
    *   `tail -F /var/log/syslog` : Tracks the log file even if it gets closed, rotated, and recreated by logrotate policies under the hood without breaking the script.

### `grep` - Global Regex Extraction Token
*   **Usage:** Standard parsing engine to filter text data patterns out of immense static configurations or logs.
*   **Advanced Flags:**
    *   `grep -ri "error" /var/log/` : Recursively (`-r`) scans all logs for the keyword string while ignoring case sensitivity (`-i`).
    *   `grep -C 3 "Exception" app.log` : Context Flag. Prints the line containing "Exception", plus the 3 lines preceding it and the 3 lines directly following it.

### `find` - Structural Disk Searching Array
*   **Usage:** Locates localized file assets based on multi-variate metadata parameters.
*   **Production Routine:** `find /var/log -name "*.log" -mtime +7 -exec rm -f {} \;` - Automatically identifies log files older than 7 days and purges them to prevent disk execution blocks.

### `chmod` & `chown` - Authorization & Security Mapping
*   **Usage:** Edits operating system operational barriers and security tags.
*   **Execution Commands:**
    *   `chmod 755 deployment.sh` : Grants full execution rights to the owner, and read/execute rights to all other systemic tiers.
    *   `chown -R www-data:www-data /var/www` : Recursively modifies owner and group bindings of web directories to the isolated `www-data` service worker account.

---

##  4. Network Layer Connectivity & Socket Triage

### `ip addr show` (or `ip a`) - Inter-Network Interface Index
*   **Usage:** Displays hardware configuration blocks for physical and virtual NICs, subnet structures, and localized IPv4/IPv6 address assignments.

### `ping -c 4 <Target_IP>` - ICMP Echo Echo Diagnostics
*   **Usage:** Verifies low-level transport layer path availability to clear out routing faults. Limiting execution to 4 echo dispatches via `-c 4`.

### `curl` - Multi-Protocol Endpoint Request System
*   **Usage:** Transfers data payloads across remote nodes. Excellent for querying Microservices and internal endpoints.
*   **Advanced Flags:**
    *   `curl -I https://github.com` : Fetches HTTP response headers only. Crucial for assessing load-balancer routing success (e.g., catching 502/504 gateways instantly).
    *   `curl -v https://api.internal` : Verbose Mode. Displays full TCP/TLS handshakes, certificate details, and header streams.

### `ss -tunlp` - Kernel Network Socket Matrix
*   **Usage:** Scans the active network boundaries to identify application port conflicts.
*   **Flags Decoded:** `t` (TCP) + `u` (UDP) + `n` (numeric port formatting) + `l` (listening sockets only) + `p` (binds the monitoring string to the actual program PID).

### `dig <domain>` & `nslookup <domain>` - Domain Resolution Tracers
*   **Usage:** Queries specific authoritative Domain Name Servers to confirm structural mapping rules and isolate external network lookup delays.
