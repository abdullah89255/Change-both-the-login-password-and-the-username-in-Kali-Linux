# Change-both-the-login-password-and-the-username-in-Kali-Linux
Got it 👍 You want to change both the **login password** and the **username** in Kali Linux. I’ll walk you through both:

---

## 🔑 Change Login Password

1. Open a terminal.
2. Run:

   ```bash
   passwd
   ```
3. Enter your **current password**, then type your **new password** twice.
   ✅ Done! Your password is now changed.

If you want to change the password for a specific user (not the one logged in):

```bash
sudo passwd username
```

---

## 👤 Change Username

Changing username is a bit trickier because it’s tied to your home directory and permissions.

1. Log in as **root** or another admin account.
   If you don’t have root enabled, use:

   ```bash
   sudo su
   ```
2. Change the username with:

   ```bash
   usermod -l newusername oldusername
   ```

   Example:

   ```bash
   usermod -l ayesha kali
   ```
3. (Optional but recommended) Rename the home directory:

   ```bash
   usermod -d /home/newusername -m newusername
   ```

   Example:

   ```bash
   usermod -d /home/ayesha -m ayesha
   ```
4. Update the display name (the one you see on login screen):

   ```bash
   chfn -f "New Full Name" newusername
   ```
Perfect 👍 I’ll give you a **safe step-by-step script** that will change both the **username** and the **password** in Kali Linux.

---

## 🚀 Script to Change Username & Password

1. **Log in as root (or switch to root):**

   ```bash
   sudo su
   ```

2. **Copy and paste this script** (replace `olduser`, `newuser`, and `newpassword` with your own):

   ```bash
   #!/bin/bash
   # Script to change Kali username and password safely

   olduser="kali"          # current username
   newuser="ayesha"        # new username
   newpassword="MyNewPass" # new password

   echo "[*] Changing username from $olduser to $newuser..."

   # Change username
   usermod -l "$newuser" "$olduser"

   # Rename home directory
   usermod -d /home/$newuser -m $newuser

   # Update password
   echo "$newuser:$newpassword" | chpasswd

   echo "[+] Username and password successfully updated!"
   echo "    New login -> Username: $newuser | Password: $newpassword"
   ```

3. Save it as:

   ```bash
   nano change-user.sh
   ```

   Paste the script inside, then press **CTRL+O → Enter → CTRL+X** to save and exit.

4. Make it executable:

   ```bash
   chmod +x change-user.sh
   ```

5. Run it:

   ```bash
   ./change-user.sh
   ```

6. **Reboot** to apply changes:

   ```bash
   reboot
   ```

---

## ⚠️ Important Warnings

* Always run as **root** or with `sudo`.
* Make sure no process is using the old username when you run the script.
* After reboot, log in with your **new username and password**.

---

👉 Do you want me to also add a **backup step** (just in case something goes wrong), so you can recover your account if login fails?

---

## ⚠️ Important Notes

* Don’t change the username **while logged in as that user**. Always use root or another admin account.
* After changing the username, you may need to log out and log back in, or even reboot.
* If you’re using GUI (like GNOME), some settings may still reference the old username — fix manually if needed.

---


