# Arch-Linux-Remote-Desktop-with-XFCE-via-WSL2
I hate carrying my beast laptop that's why I build it. Now I can use it from anywhere in this world. I just need a single device and I can access my any distro and any operating system without changing router port forwarding.  

# Arch Linux Remote Desktop with XFCE, TigerVNC, noVNC, and Ngrok

This project sets up an **Arch Linux** environment with a remote desktop accessible globally via **noVNC** and **Ngrok**.

## 📦 Components
- **Arch Linux** as the base OS
- **XFCE4** as the desktop environment
- **TigerVNC** as the VNC server
- **noVNC** to access VNC from a browser
- **Ngrok** to expose the local noVNC server to the internet

---

## 🚀 Quick Setup Instructions

### 1. Install Required Packages
```bash
sudo pacman -Syu
sudo pacman -S tigervnc xfce4 xfce4-goodies xorg-xinit dbus unzip
```

### 2. Configure VNC and XFCE
```bash
mkdir -p ~/.vnc
nano ~/.vnc/xstartup
```
Paste this:
```bash
#!/bin/sh
exec startxfce4
```
Then:
```bash
chmod +x ~/.vnc/xstartup
```

### 3. Start VNC Server
```bash
vncserver :1
```

### 4. Set Up noVNC
```bash
cd /opt
curl -O https://github.com/novnc/noVNC/archive/refs/heads/master.zip
unzip master.zip
mv noVNC-master noVNC
cd noVNC
```

### 5. Install Websockify (in virtualenv)
```bash
python -m venv ~/.venv/novnc
source ~/.venv/novnc/bin/activate
pip install websockify
```

### 6. Start Websockify
```bash
~/.venv/novnc/bin/websockify --web=/opt/noVNC 0.0.0.0:6080 localhost:5901
```

### 7. Install and Start Ngrok
```bash
cd /opt
curl -O https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-stable-linux-amd64.zip
unzip ngrok-stable-linux-amd64.zip
sudo mv ngrok /usr/local/bin/
ngrok config add-authtoken <YOUR_AUTHTOKEN>
ngrok http 6080
```

---

## 🌐 Access Remotely
After `ngrok` runs, use the provided `https://your-subdomain.ngrok-free.app` in your browser to access the XFCE desktop.

---

## 📁 File Structure
```
/opt/noVNC               # Web-based VNC viewer
~/.vnc/xstartup          # VNC XFCE startup script
/usr/local/bin/ngrok     # Ngrok binary
```

## 🔒 Security Considerations
- Use a strong VNC password
- Set up HTTPS (ngrok does this automatically)
- Use SSH tunnels or add authentication to the noVNC page if using long-term

---

## 🧠 Credits
**By Aisha Jamal Jeniya**
Inspired by the desire to create a globally accessible Arch Linux desktop from scratch using open tools.

---

## 📜 License
MIT License (Feel free to reuse this setup)
