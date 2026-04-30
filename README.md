# 🧱 Salt Minion Automation: The Lego House Project

This project uses **Ansible** to bootstrap **SaltStack**. It automates the annoying beginning hassle of installing the minion on a device, setting IPs, and fixing firewall issues if it occurs, so you can get straight to managing your infrastructure.

## 🚀 Quick Start: How to make it work

### 0. Get the Files
First, you need to bring this project from GitHub onto your computer. Open your terminal and run:

```bash
git clone https://github.com/dameancruzz/Auto_Ans-salt
cd Auto_Ans-salt
```

### 1. **The Inventory:** Open the `hosts` file using vim (the best editor), sudo or other editors.
   - Add your target VM IPs under `[remote_nodes]`.
   - **Optional:** If you want to test on your own laptop first, basically making it so you rmaster also becomes a minion you can remove the `#` from `master_node` at the very very bottom of the file hosts. This is a grea way to test it works before adding other IP's to the hosts file. 

### 2. **The Launch:** Run this command in your terminal:

   ```bash
   ansible-playbook -i hosts deploy_minions.yml
   ```

### 3. **The Passwords:** Ansible will ask for your **SSH password** (to deliver your key) and your **SUDO password** (to install Salt). 

### 4. **The Result:** Once it finishes, your VM is a Salt Minion and your laptop is the Master. No more passwords needed!

---

## 📜 A Little History: Ansible vs. Salt

Imagine you want 10 friends across the world to build a super-specific **Lego house** exactly the same way.

> **Ansible (The Mail Carrier)**  
> Like a mail carrier, Ansible delivers a letter (**Playbook**) over **SSH**. The carrier stays and reads instructions line-by-line. If they leave, the work stops. Once they are done, they head home. It’s perfect for the "First Touch."

> **Salt (The Smart Home)**  
> Salt installs a speaker in the house (**Minion**). You push a button from your laptop (**Master**) and it broadcasts a blueprint (**SLS file**). The house "listens" and stays in that state. If a Lego piece falls off, it "self-heals" automatically!

**The Strategy:** Use Ansible to **build** the house and Salt to **live in and manage** it.

---

## 🛠️ The Cheat Sheet: What’s under the hood?

### The "Logic" Words
*   **vars_prompt:** Prompts for passwords so they are never hardcoded in your GitHub history.
*   **delegate_to: localhost:** Tells the playbook to run a task on *your* laptop (like finding your IP) instead of the VM.
*   **block/rescue:** "Plan A and Plan B." If the install fails, the rescue block reports exactly why.
*   **notify/handlers:** A reminder system. If a config file changes, it triggers a service restart at the very end.

### The Modules (The Tools)
*   **authorized_key:** Delivers your "Digital ID" (`id_ed25519.pub`) to the VM for passwordless access.
*   **dnf:** The package manager that downloads the Salt Minion and Python "batteries."
*   **lineinfile:** The text editor that finds the `master:` line and points it to your laptop's IP.
*   **firewalld:** The security guard that opens ports 4505/4506 and keeps them open after a reboot.

---

## 📊 Technical Summary
*   **The Delivery (Ansible & SSH):** Your delivery truck. It walks in, sets up the speaker, and drives away.
*   **The Intercom (SaltStack & ZeroMQ):** A permanent, high-speed "always on" tunnel. 
*   **The Shout (Commands & Grains):** You broadcast a signal to 1,000 friends as easily as one, and they respond in milliseconds.
