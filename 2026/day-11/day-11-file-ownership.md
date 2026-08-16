# Day 11 Challenge – Linux File Ownership (chown & chgrp)

##  Files & Directories Created
* `devops-file.txt`
* `team-notes.txt`
* `project-config.yaml`
* `app-logs/` (Directory)
* `heist-project/` (Deep Directory Structure)
* `bank-heist/` (Practice Challenge Directory)

---

##  Ownership Changes (Before & After)

| File / Directory | Original Owner:Group | New Owner:Group | Command Type Used |
| :--- | :--- | :--- | :--- |
| `devops-file.txt` | `dell:dell` | `berlin:dell` | Individual User Change |
| `team-notes.txt` | `dell:dell` | `dell:heist-team` | Individual Group Change |
| `project-config.yaml` | `dell:dell` | `professor:heist-team` | Combined Single-line Change |
| `app-logs/` | `dell:dell` | `berlin:heist-team` | Combined Directory Change |
| `heist-project/` | `dell:dell` | `professor:planners` | Recursive Global Change (`-R`) |
| `bank-heist/access-codes.txt`| `dell:dell` | `tokyo:vault-team` | Practice Scenario 1 |
| `bank-heist/blueprints.pdf`  | `dell:dell` | `berlin:tech-team` | Practice Scenario 2 |
| `bank-heist/escape-plan.txt`  | `dell:dell` | `nairobi:vault-team`| Practice Scenario 3 |

---

##  Commands Used & Flow

### Task 1: Understanding Ownership Structural Layout
```bash
# Inspecting default home directories configuration layout
ls -l ~
```
* **Analysis:** The 3rd column lists the absolute account owner who possesses specific read/write/execute rights, while the 4th column lists the associated group profile.

### Task 2, 3 & 4: Core Ownership Mutations
```bash
# Task 2: Mutating User Ownership
touch devops-file.txt
sudo chown tokyo devops-file.txt
sudo chown berlin devops-file.txt

# Task 3: Mutating Group Ownership
touch team-notes.txt
sudo groupadd heist-team
sudo chgrp heist-team team-notes.txt

# Task 4: Combined Single-Line Configurations
touch project-config.yaml
sudo chown professor:heist-team project-config.yaml

mkdir app-logs
sudo chown berlin:heist-team app-logs/
```

### Task 5: Recursive Traversal Execution
```bash
# Construct nested infrastructure tree
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf

# Execute deep recursive ownership transfer
sudo groupadd planners
sudo chown -R professor:planners heist-project/

# Verify down the tree
ls -lR heist-project/
```

### Task 6: Final Lab Practice Challenge
```bash
# Ensuring teams and targets are provisioned
sudo groupadd vault-team
sudo groupadd tech-team
mkdir bank-heist
touch bank-heist/access-codes.txt bank-heist/blueprints.pdf bank-heist/escape-plan.txt

# Partitioning files across distinct organizational owners
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt

# Verify exact compliance mapping
ls -l bank-heist/
```

---

## 🧠 What I Learned
1. **The Asymmetric Binding Model:** Linux decouples individual account scope (`chown`) from collaborative collective team identities (`chgrp`), allowing dual-layered authorization policies.
2. **The Danger & Utility of Recursion (`-R`):** Mastered how recursive tree-traversal instantly inherits administrative identities downward through complex file directory systems.
3. **Enterprise Compliance Simulation:** Modeled real-world production setups where discrete files (e.g., config keys, database assets) inside a single directory must answer to distinct application operators.
