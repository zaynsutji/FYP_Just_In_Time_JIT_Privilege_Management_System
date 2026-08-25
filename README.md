# Just-In-Time (JIT) SSH Privilege Management System

A Zero-Trust remote access control platform designed to eliminate static SSH key vulnerabilities by issuing short-lived, self-expiring SSH certificates for administrative server access.

---

## 📌 What the Project Does

The JIT SSH Privilege Management System provides a centralized web portal where administrators request temporary root or privileged access to remote Linux servers. Instead of relying on permanent, static SSH private keys stored indefinitely on client machines, this platform uses an internal Certificate Authority (CA) to sign public keys into ephemeral SSH certificates with strict Time-To-Live (TTL) expiration limits (e.g., 5 minutes).

Once the TTL expires, OpenSSH automatically rejects any new connection attempts without requiring manual key deletion or firewall rule updates on target servers.

---

## 🎯 Why the Project Is Useful

* **Eliminates Static Credential Theft:** Stolen or compromised private keys become useless to attackers because standing privileges are completely removed.
* **Enforces Zero-Trust & Least Privilege:** Access is granted strictly on-demand, for specific target servers, and limited to predefined duration windows.
* **Automated Key Revocation:** Removes the need for manual administrative tasks to revoke access across multiple endpoints.
* **Centralized Audit Logging:** Maintains an immutable record mapping every access request to the requesting user, target server IP, session duration, and certificate serial number.

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
