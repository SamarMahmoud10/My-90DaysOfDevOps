# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

##  Task Overview
Today, I successfully provisioned a cloud infrastructure instance, configured network security rules, installed the Nginx web server, verified its global accessibility via a browser, and extracted system log files back to my local machine.

---

##  Commands Used

### 1. System Updates & Prerequisites
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Nginx Installation & Management
```bash
# Install Nginx web server
sudo apt install nginx -y

# Verify Nginx service status
systemctl status nginx

# Ensure Nginx starts automatically on system boot
sudo systemctl enable nginx
```

### 3. Log Extraction & Manipulation
```bash
# View the last 50 entries of Nginx access logs
sudo tail -n 50 /var/log/nginx/access.log

# Save Nginx logs to a text file in the user's home directory
sudo cat /var/log/nginx/access.log > ~/nginx-logs.txt

# Change ownership of the log file to allow secure copying (SCP)
sudo chown ubuntu:ubuntu ~/nginx-logs.txt
```

### 4. Local Machine Secure Copy (SCP)
*Executed on my local personal machine terminal:*
```bash
# Securely download the log file from AWS EC2 instance
scp -i ~/.ssh/your-key.pem ubuntu@<YOUR_INSTANCE_PUBLIC_IP>:~/nginx-logs.txt ./nginx-logs.txt
```

---

##  Challenges Faced & Solutions

### Challenge 1: Connection Timed Out in Browser
* **Issue:** After successfully installing Nginx, trying to access `http://<YOUR_INSTANCE_IP>` in the browser resulted in a "Connection Timed Out" error.
* **Solution:** Discovered that the cloud firewall (AWS Security Group) was blocking inbound traffic. I updated the Security Group rules by adding an **Inbound Rule** for **HTTP** on **Port 80** from anywhere (`0.0.0.0/0`).

### Challenge 2: Permission Denied during SCP transfer
* **Issue:** Running the `scp` command failed with a permission denied error because the file `nginx-logs.txt` inside the server was originally owned by `root`.
* **Solution:** I ran `sudo chown ubuntu:ubuntu ~/nginx-logs.txt` on the remote cloud server to grant my deployment user full read permissions before initiating the file transfer.

---

## 🧠 What I Learned
* **Cloud Resource Provisioning:** Learned how to launch, configure, and connect to remote Ubuntu instances using SSH keys.
* **Network Firewalls (Security Groups):** Understood that instances are isolated by default, and ports like 80 (HTTP) or 22 (SSH) must be explicitly managed via inbound rules.
* **Log Management:** Practical experience locating web server operations in `/var/log/nginx/` and auditing incoming user requests.
* **Remote File Transfer (SCP):** Mastered using `scp` alongside SSH keys to securely sync diagnostics and assets between cloud clusters and local workstations.
