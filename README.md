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

Good catch 👍 You’re right: when you change a username in Kali (or any Debian-based Linux with **GNOME**), some config files, shortcuts, and cached settings may still reference the **old username**. Here’s how you can clean it up:

---

## 🛠️ Fixing GUI Issues After Username Change

### 1. Update Display Manager (login screen)

* If you use **GDM (GNOME Display Manager)**, check:

  ```bash
  sudo nano /etc/gdm3/custom.conf
  ```

  Make sure any `AutomaticLogin=olduser` line is updated to:

  ```
  AutomaticLogin=newuser
  ```

---

### 2. Update `.desktop` Files

Sometimes application shortcuts may hardcode the old home path:

* Check inside:

  ```bash
  grep -r "/home/olduser" /home/newuser/.local/share/applications/
  ```
* If found, edit them:

  ```bash
  nano /home/newuser/.local/share/applications/app.desktop
  ```

  Replace `/home/olduser/` with `/home/newuser/`.

---

### 3. Update GNOME Settings Database

GNOME stores paths in **dconf**. Reset cached references:

```bash
dconf reset -f /
```

⚠️ This resets GNOME settings to default (wallpapers, dock favorites, etc.), but fixes broken references.

---

### 4. Fix File Permissions

If you copied/renamed the home directory, some files may still belong to the old username. Run:

```bash
sudo chown -R newuser:newuser /home/newuser
```

---

### 5. Update Autostart Apps

Check:

```bash
ls /home/newuser/.config/autostart/
```

Open each `.desktop` file and replace any `/home/olduser` with `/home/newuser`.

---

### 6. Check Systemd Services

If you had user-level services (like Docker, VSCode server, etc.), reload them:

```bash
sudo loginctl enable-linger newuser
```

---

✅ After these fixes, your GNOME desktop should work smoothly with the **new username**.

---

👉 Do you want me to prepare a **post-username-change cleanup script** that automates most of these fixes for GNOME?



