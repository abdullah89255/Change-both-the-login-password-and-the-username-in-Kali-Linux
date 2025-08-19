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

---

## ⚠️ Important Notes

* Don’t change the username **while logged in as that user**. Always use root or another admin account.
* After changing the username, you may need to log out and log back in, or even reboot.
* If you’re using GUI (like GNOME), some settings may still reference the old username — fix manually if needed.

---

👉 Do you want me to give you a **step-by-step script** that changes both username and password in one go, safely?
