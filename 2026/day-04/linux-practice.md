# Day 04 – Linux Practice: Processes and Services

## 1. Process Checks
In this section, I inspected the active processes and system resource consumption.

* **First Command (Static Process Snapshot):**
  * Command Run: `ps aux`
  * Observation: It displayed a full snapshot of all running processes, their PIDs, and memory usage.


* **Second Command (Live Resource Monitoring):**
* Command Run: `htop`
* Observation: It showed a live, interactive view of CPU cores, RAM usage, and active tasks. Everything looked stable.

## 2. Service Checks
In this section, I picked the **Docker** service to inspect its status and configuration.

* **Third Command (Checking Service Status):**
* Command Run: `systemctl status docker`
* Observation: The service is active and running fine without any errors.


* **Fourth Command (Listing System Services):**
* Command Run: `systemctl list-units --type=service`
* Observation: It listed all the background services currently loaded into the system.


## 3. Log Checks
In this section, I inspected system logs to check the history of events.

* **Fifth Command (Viewing General System Logs):**
* Command Run: `sudo tail -n 50 /var/log/syslog`
* Observation: It showed the latest 50 system events securely. No critical warnings were found.

 **Sixth Command (Viewing Specific Service Logs):**
* Command Run: `journalctl -u docker`
* Observation: Checked the dedicated logs for Docker, confirming successful container startups. 

## 4. Mini Troubleshooting Flow
* **Observation:** I monitored the running processes, verified the Docker service state, and analyzed its logs.
* **Result:** The Docker service is completely stable and running in an **Active** state. Resource utilization in `htop` is perfectly normal, and logs contain no errors or critical failures. The system is healthy and ready for deployment tasks.