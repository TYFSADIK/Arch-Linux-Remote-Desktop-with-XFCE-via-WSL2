# Arch-Linux-Remote-Desktop-with-XFCE-via-WSL2
I hate carrying my beast laptop that's why I build it. Now I can use it from anywhere in this world. I just need a single device and I can access my any distro and any operating system without changing router port forwarding.  

# 🌐 Remote XFCE Desktop on Arch Linux via noVNC & Ngrok

## ✅ Overview
Set up a fully functional XFCE desktop on Arch Linux and access it remotely from a browser using TigerVNC, noVNC, and ngrok tunneling.

---

## 📦 Requirements
- Arch Linux (VM or bare-metal)
- Root/sudo access
- Verified [ngrok](https://ngrok.com/) account
- Internet connection

---

## 🛠️ Setup Steps

### 1. Install XFCE, TigerVNC, and dependencies
```bash
sudo pacman -Syu
sudo pacman -S xfce4 xfce4-goodies xorg-xinit dbus tigervnc unzip
```

### 2. Set VNC Password
```bash
vncpasswd
```

### 3. Configure the VNC Startup Script
```bash
mkdir -p ~/.vnc
nano ~/.vnc/xstartup
```
Paste:
```bash
#!/bin/sh
startxfce4 &
```
Make it executable:
```bash
chmod +x ~/.vnc/xstartup
```

### 4. Start VNC Server
```bash
vncserver :1
```
Confirm it’s running on `:1` (port 5901).

---

## 🧩 Set Up noVNC

### 5. Clone noVNC and websockify
```bash
cd /opt
git clone https://github.com/novnc/noVNC
cd noVNC
git clone https://github.com/novnc/websockify
```

### 6. Start noVNC
```bash
./utils/launch.sh --vnc localhost:5901
```
Or manually:
```bash
./websockify/run 6080 localhost:5901
```

---

## 🌍 Expose with ngrok

### 7. Download and configure ngrok
```bash
cd /opt
curl -O https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-stable-linux-amd64.zip
unzip ngrok-stable-linux-amd64.zip
sudo mv ngrok /usr/local/bin/
```

### 8. Authenticate ngrok
```bash
ngrok config add-authtoken <your_auth_token>
```

### 9. Start the public tunnel
```bash
ngrok http 6080
```
You’ll get a public URL like `https://random-id.ngrok-free.app`.

---

## 📸 Suggested Screenshots

1. `vncserver :1` running
2. XFCE desktop loaded
3. noVNC dashboard or client open
4. `ngrok` terminal with public URL
5. Access from browser
6. `curl ifconfig.me` showing public IP

---

## 🔐 Security Tips

- Use a strong password in `vncpasswd`
- Don’t expose direct VNC port to the internet
- Use ngrok’s authentication and HTTPS tunnel options

---

## 🧠 Bonus Ideas
- Setup `systemd` service for auto-start
- Secure with a self-signed or Let’s Encrypt SSL
- Wrap everything in a Docker container

---

## 📁 Repo Files
- `README.md` (this file)
- `.gitignore` (for `.vnc`, `*.log`, and cache files)
- Screenshot folder `screenshots/`
- Configs (optional): `xstartup`, `ngrok.yml`

---

Made with ❤️ on Arch Linux



---

## 🧠 Credits
**By TYF Sadik**
Inspired by the desire to create a globally accessible Arch Linux desktop from scratch using open tools.

---

## 📜 License
MIT License (Feel free to reuse this setup)






