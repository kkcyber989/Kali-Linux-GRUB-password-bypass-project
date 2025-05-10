# Kali Linux GRUB Password Bypass

https://www.youtube.com/watch?v=D1cou0Wf6hI

This project demonstrates how to bypass a forgotten Kali Linux user password by exploiting the GRUB bootloader. By modifying the boot parameters at startup, a user can gain root shell access and reset any account password without knowing the original credentials. This highlights the importance of physical security and full disk encryption in Linux-based systems.

## 🔧 Tools & Environment
- Kali Linux (VM or Bare Metal)
- GRUB Bootloader
- Root Shell (`/bin/bash`)
- Basic Linux CLI

## 🛠️ Exploit Steps

1. **Interrupt Boot at GRUB:**
   - When the GRUB menu appears, press `e` to edit the default boot entry.

2. **Modify the Linux Line:**
   - Scroll to the line starting with `linux` (e.g., `linux /boot/vmlinuz-...`)
   - Add the following to the end of the line:
     ```
     init=/bin/bash
     ```

3. **Boot with Modified Config:**
   - Press `Ctrl + X` or `F10` to boot into a root shell.

4. **Reset the User Password (Full Bash Block Below):**
   ```bash
   mount -o remount,rw /
   passwd your_username
   # You'll be prompted:
   # New password:
   # Retype new password:
   # If successful, you'll see:
   # password updated successfully
   exec /sbin/init
   # If that fails, force reboot:
   # reboot -f

See the /screenshots folder for a visual walkthrough of the attack and password reset.

**Recommendations**

Use full disk encryption during installation.
Add a GRUB password to prevent unauthorized editing.
Restrict physical access to secure machines.
