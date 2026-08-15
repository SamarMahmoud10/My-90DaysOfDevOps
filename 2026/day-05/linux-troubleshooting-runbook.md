# Day 05 – Linux Troubleshooting Runbook: CPU, Memory, and Logs

## Target Service / Process
* **Target Service:** Docker Daemon (`dockerd`)
* **Purpose:** Core containerization platform for running application microservices.

---

## 1. Environment Basics & Filesystem Sanity
Before checking resources, I verified the system environment and tested basic disk write capabilities.

* **Command 1 (System Information):**
  ```bash
  uname -a
  ```
  * **Observation:** Confirmed the Linux kernel version and architecture are running stable within the WSL environment.

* **Command 2 (OS Release Details):**
  ```bash
  cat /etc/os-release
  ```
  * **Observation:** Verified the OS distribution details (Ubuntu) to ensure package manager compatibility.

* **Command 3 (Filesystem Write Test):**
  ```bash
  mkdir /tmp/runbook-demo && cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo
  ```
  * **Observation:** Successfully created a temporary directory and copied a file, confirming that the root filesystem is NOT in read-only mode and permissions are fine.

---

## 2. Resource Snapshot: CPU & Memory
Checking if the Docker process or containers are exhausting the system memory or compute power.

* **Command 4 (Memory Usage):**
  ```bash
  free -h
  ```
  * **Observation:** Total and available memory are within safe margins. Swap space usage is normal, meaning no memory leaks are present.

* **Command 5 (Process Resource Allocation):**
  ```bash
  ps -o pid,pcpu,pmem,comm -C dockerd
  ```
  * **Observation:** The core Docker daemon (`dockerd`) is consuming less than 2% CPU and less than 5% total system RAM, showing healthy operation.

---

## 3. Resource Snapshot: Disk & Network
Ensuring Docker has enough storage space to pull images and that container network ports are active.

* **Command 6 (Disk Space Allocation):**
  ```bash
  df -h
  ```
  * **Observation:** The root partition has plenty of available storage space. Docker won't fail due to "No space left on device" errors.

* **Command 4 (Log Directory Size):**
  ```bash
  sudo du -sh /var/log
  ```
  * **Observation:** Checked the system log sizes. Total log storage is minimal, meaning log rotation is functioning properly.

---

## 4. Resource Snapshot: Network & Ports
Verifying that Docker is listening on the required local sockets or ports.

* **Command 7 (Active Network Ports):**
  ```bash
  sudo ss -tulpn
  ```
  * **Observation:** Checked active TCP/UDP listeners. Docker sockets are properly allocated and listening without conflicting with other system services.

---

## 5. Logs Reviewed
Inspecting system event logs to trace hidden container or daemon failures.

* **Command 8 (Docker Systemd Logs):**
  ```bash
  sudo journalctl -u docker -n 50
  ```
  * **Observation:** Reviewed the last 50 lines of logs. Verified smooth container startup sequences and found zero "Error" or "Fatal" log tags.

---

## 6. Quick Findings
* The overall health of the Docker service is **Excellent**.
* No CPU spikes or RAM exhaustion were detected during active process analysis.
* Filesystem read/write functionalities are operational, and disk space is sufficient.

---

## 7. If This Worsens (Next Steps)
If the Docker service crashes, stops responding, or experiences heavy performance degradation in production under pressure, follow these exact 3 technical steps:

1. **Graceful Restart Strategy:** Attempt a safe service reload or restart using `sudo systemctl restart docker` to clear hung processes without crashing underlying data volumes.
2. **Increase Log Verbosity (Debug Mode):** Modify the `/etc/docker/daemon.json` configuration file to include `"debug": true`, then reload the daemon to capture deep internal trace logs.
3. **Trace System Calls with Strace:** Find the specific process ID (PID) of the lagging container or daemon and execute `sudo strace -p <PID> -c` to locate exactly which system call is causing the lockup or latency.
