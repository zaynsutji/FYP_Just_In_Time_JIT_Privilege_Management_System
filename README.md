```markdown
# Just-In-Time (JIT) SSH Privilege Management System

A Zero-Trust remote access control platform designed to eliminate static SSH key vulnerabilities by issuing short-lived, self-expiring SSH certificates for administrative server access[cite: 1].

---

## 📌 What the Project Does

The JIT SSH Privilege Management System provides a centralized web portal where administrators request temporary root or privileged access to remote Linux servers[cite: 1]. Instead of relying on permanent, static SSH private keys stored indefinitely on client machines, this platform uses an internal Certificate Authority (CA) to sign public keys into ephemeral SSH certificates with strict Time-To-Live (TTL) expiration limits (e.g., 5 minutes)[cite: 1].

Once the TTL expires, OpenSSH automatically rejects any new connection attempts without requiring manual key deletion or firewall rule updates on target servers[cite: 1].

---

## 🎯 Why the Project Is Useful

* **Eliminates Static Credential Theft:** Stolen or compromised private keys become useless to attackers because standing privileges are completely removed[cite: 1].
* **Enforces Zero-Trust & Least Privilege:** Access is granted strictly on-demand, for specific target servers, and limited to predefined duration windows[cite: 1].
* **Automated Key Revocation:** Removes the need for manual administrative tasks to revoke access across multiple endpoints[cite: 1].
* **Centralized Audit Logging:** Maintains an immutable record mapping every access request to the requesting user, target server IP, session duration, and certificate serial number[cite: 1].

---

## 🚀 How Users Can Get Started

### Prerequisites

* **Operating System:** Linux (Ubuntu 22.04 / Debian 12 recommended) or Virtual Machines via VirtualBox/VMware
* **Python:** Version 3.10 or higher
* **SSH Engine:** OpenSSH Server (`sshd`) on target nodes
* **CA Tool:** Smallstep (`step-ca`) or native OpenSSH CA utilities

---

### Step 1: Clone the Repository

```bash
git clone [https://github.com/your-username/jit-ssh-privilege-manager.git](https://github.com/your-username/jit-ssh-privilege-manager.git)
cd jit-ssh-privilege-manager

```

---

### Step 2: Set Up the Python Environment

```bash
# Create virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

```

---

### Step 3: Configure Target Servers

On each target Linux server you wish to manage, configure OpenSSH to trust your CA's public key:

1. Copy your CA public key to `/etc/ssh/ca_user_key.pub` on the target server.
2. Edit `/etc/ssh/sshd_config` and append:
```text
TrustedUserCAKeys /etc/ssh/ca_user_key.pub

```


3. Restart the SSH service:


```bash
sudo systemctl restart ssh

```



---

### Step 4: Run the Web Application

```bash
# Initialize database
python3 init_db.py

# Start the Flask portal
python3 app.py

```

Access the portal in your web browser at `http://localhost:5000`.

---

## 💡 How to Use

1. Log into the JIT Web Portal.


2. Select your **Target Server** and desired **Access Duration** (e.g., 5 Minutes).


3. Upload or paste your SSH public key (`id_rsa.pub`).


4. Click **Request Access** to download your short-lived certificate (`id_rsa-cert.pub`).


5. Connect via terminal:
```bash
ssh -i id_rsa -i id_rsa-cert.pub root@<target-server-ip>

```



---

## 💬 Where Users Can Get Help

If you encounter bugs, setup issues, or have feature suggestions:

* Open an **Issue** on this GitHub repository.
* Refer to the official [OpenSSH Certificate Documentation](https://www.openssh.com/manual.html) or [Smallstep `step-ca` Docs](https://smallstep.com/docs/step-ca).

---

## 👤 Who Maintains and Contributes

* **Author / Maintainer:** Muhammad Zahin Iman Bin Abu Hanipah


* **Institution:** Universiti Tenaga Nasional (UNITEN) — College of Computing and Informatics


* **Project Context:** Final Year Project (FYP) for Bachelor of Computer Science (Cybersecurity / Systems)



---

*Contributions, issues, and feature requests are welcome!*

```

```
