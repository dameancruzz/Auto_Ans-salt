🧱 Salt Minion Automation: The Lego House Project
===============

This project uses a **Ansible** playbook to jumpstart **SaltStack**. It automates the annoying beginning hassle of <ins>installing the minion</ins> on a device, <ins>setting IPs</ins>, and <ins>fixing firewall issues</ins> (_if it occurs_), so you can get straight to managing your infrastructure using **Salt**.  
  
  
---

### ✅ Quick Start: **How to make it work**

## 0️⃣ **Get the Files**
First, you need to bring this project from GitHub onto your device. Open your terminal and run:

```bash
git clone https://github.com/dameancruzz/Auto_Ans-salt
cd Auto_Ans-salt
```

## 1️⃣ **The Inventory** 

Open the `hosts` file using vim (the best editor), sudo or other editors.

   - Add your target VM IPs under `[remote_nodes]`.
     
   - **Optional:**
If you want to test on your own laptop first, basically making it so your master also becomes a minion, you can remove the `#` from `master_node` at the very very bottom of the file hosts. This is a great way to test the playbook works before adding other IP's to the hosts file.


## 2️⃣ **The Launch:** Run this command in your terminal:

   ```bash
   ansible-playbook -i hosts deploy_minions.yml
   ```

This command is basically telling Ansible to use the hosts list to find your targets and execute the deploy_minions instructions on them. ansible-playbook (the tool) ; -i (the inventory flag) ; hosts (the target list) ; deploy_minions.yml (the instructions).

     
**The Passwords**  
Ansible will ask for your **SSH password** (to deliver your key) and your **SUDO password** (to install Salt).

**The Result**  
Once it finishes, your VM is a Salt Minion and your laptop is the Master. No more    passwords needed!

#3️⃣ **Accept key**  



---

## 📜 A Little History: Ansible vs. Salt

Imagine you want 10 friends across the world to build a super-specific **Lego house** exactly the same way.

**Ansible (The Mail Carrier)**
Like a mail carrier, Ansible delivers a letter (**Playbook**) over **SSH**. The carrier stays and reads instructions line-by-line. If they leave, the work stops. Once they are done, they head home. It’s perfect for the "First Touch."

**Salt (The Smart Home)**  
 Salt installs a speaker in the house (**Minion**). You push a button from your laptop (**Master**) and it broadcasts a blueprint (**SLS file**). The house "listens" and stays in that state. If a Lego piece falls off or the master disconnects, it will "self-heals" automatically!

**The Strategy** 
Use Ansible to **build** the house and Salt to **live in and manage** it.

---

## 🛠️ The Cheat Sheet: What’s under the hood?

### The "Logic" Words
*   **vars_prompt:** Prompts for passwords so they are never hardcoded in your GitHub history.
*   **delegate_to: localhost:** Tells the playbook to run a task on *your* laptop (like finding your IP) instead of the VM.
*   **block/rescue:** "Plan A and Plan B." If the install fails, the rescue block reports exactly why.
*   **notify/handlers:** A reminder system. If a config file changes, it triggers a service restart at the very end.

### The Modules (The Tools)
*   **authorized_key:** Delivers your "Digital ID" (`id_ed111.pub`) to the VM for passwordless access.
*   **dnf:** The package manager that downloads the Salt Minion and Python "batteries."
*   **lineinfile:** The text editor that finds the `master:` line and points it to your laptop's IP.
*   **firewalld:** The security guard that opens ports 4505/4506 and keeps them open after a reboot.

---