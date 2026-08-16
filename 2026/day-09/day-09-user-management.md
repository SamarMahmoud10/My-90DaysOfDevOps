# Day 09 Challenge – Linux User & Group Management

##  Users & Groups Created
* **Users:** `tokyo`, `berlin`, `professor`, `nairobi`
* **Groups:** `developers`, `admins`, `project-team`

---

##  Group Assignments
* `tokyo` ➡️ `developers`, `project-team`
* `berlin` ➡️ `developers`, `admins` (Secondary groups)
* `professor` ➡️ `admins`
* `nairobi` ➡️ `project-team`

---

##  Directories Created & Permissions
1. **/opt/dev-project**
   * **Group Owner:** `developers`
   * **Permissions:** `775` (`drwxrwxr-x`)
2. **/opt/team-workspace**
   * **Group Owner:** `project-team`
   * **Permissions:** `775` (`drwxrwxr-x`)

---

##  Commands Used

### Task 1: Create Users
```bash
# Create users with home directories (-m) and default shell
sudo useradd -m -s /bin/bash tokyo
sudo useradd -m -s /bin/bash berlin
sudo useradd -m -s /bin/bash professor

# Set passwords for the users
echo "tokyo:password123" | sudo chpasswd
echo "berlin:password123" | sudo chpasswd
echo "professor:password123" | sudo chpasswd

# Verify user creation
cat /etc/passwd | grep -E "tokyo|berlin|professor"
ls -l /home/
```

### Task 2: Create Groups
```bash
# Create the security groups
sudo groupadd developers
sudo groupadd admins

# Verify groups exist
cat /etc/group | grep -E "developers|admins"
```

### Task 3: Assign Users to Groups
```bash
# Append users to groups (-aG)
sudo usermod -aG developers tokyo
sudo usermod -aG developers,admins berlin
sudo usermod -aG admins professor

# Verify group memberships
groups tokyo
groups berlin
groups professor
```

### Task 4: Shared Directory Deployment
```bash
# Create the shared directory
sudo mkdir -p /opt/dev-project

# Change group ownership to developers
sudo chgrp developers /opt/dev-project

# Set permissions to 775 (rwxrwxr-x)
sudo chmod 775 /opt/dev-project

# Test file creation as user 'tokyo'
sudo -u tokyo touch /opt/dev-project/tokyo-code.txt

# Test file creation as user 'berlin'
sudo -u berlin touch /opt/dev-project/berlin-plan.txt

# Verify files and permissions
ls -la /opt/dev-project
```

### Task 5: Team Workspace Setup
```bash
# Create nairobi and the new group
sudo useradd -m -s /bin/bash nairobi
echo "nairobi:password123" | sudo chpasswd
sudo groupadd project-team

# Add members to project-team
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo

# Create workspace and configure security
sudo mkdir -p /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace

# Test file creation as 'nairobi'
sudo -u nairobi touch /opt/team-workspace/nairobi-gold.txt

# Verify workspace setup
ls -la /opt/team-workspace
```

---

## 🧠 What I Learned
1. **Role-Based Access Control (RBAC):** Understood how Linux isolates environments by defining clear boundaries between different corporate roles (Developers vs. Admins).
2. **Shared Group Collaboration:** Learned how to create secure collaborative directories where multiple distinct users can read and write assets safely without utilizing the supreme `root` account.
3. **Impersonation Testing (`sudo -u`):** Mastered how to simulate and test application contexts by executing targeted operations under specific user profiles to audit access restrictions.
