# Install
- Download zip file and transfer it to SD Card with **Etcher**.

# BurpSuite
- Download **ARM64 Compressed Archive** from Oracle. 
- Install java
  ```bash
  mkdir /opt/java && cd /opt/java
  tar zxvf jdk-11.0.21_linux-aarch64_bin.tar.gz
  nano ~/.bashrc
  # export JAVA_HOME=/opt/java/jdk-11.0.21
  # export PATH=$PATH:$JAVA_HOME/bin
  source ~/.bashrc
  java -version
  ```

# SSH Tunnel
- Install Putty and run it.
  ```bash
  apt install putty
  putty
  ```
- Putty config
  - Host Name: 49.13.57.86
  - Connection  →  SSH  →  Tunnels  →  Source port: 1080 / Dynamic / Auto  →  Add  →  Open
- Browser config
  - Socks5 / 127.0.0.1:1080
- Putty alternative
  ```bash
  ssh -D 1080 root@cvefix.ir
  ```

# VNC
- Install
  ```bash
  apt install tightvncserver
  ```
- Connect to wifi & Add static IP
  ```bash
  vncserver :1
  # Type your password
  # Type no when asked for a view only password
  ```
- Config
  ```
  nano /etc/systemd/system/vncserver.service
  ```
  ```bash
  [Unit]
  Description=TightVNC remote desktop server
  After=network.target
 
  [Service]
  User=root
  Type=forking
  ExecStart=/usr/bin/vncserver :1
  ExecStop=/usr/bin/vncserver -kill :1
 
  [Install]
  WantedBy=multi-user.target
  ```
- Run
  ```bash
  chown root:root /etc/systemd/system/vncserver.service
  chmod 644 /etc/systemd/system/vncserver.service
  systemctl start vncserver
  systemctl enable vncserver
  netstat -tupln                              # check listening port
  ```
- install a VNC Viewer App on android

# ALFA WiFi Adaptor
- Method 1
  ```bash
  iwconfig
  # wlan1 (Mode:Managed)
  ifconfig wlan1 down	
  airmon-ng start wlan1
  iwconfig
  # wlan1mon
  ```
- Method 2
  ```bash
  airmon-ng check kill
  ip link set wlan1 down
  iw dev wlan1 set type monitor
  ip link set wlan1 up
  airmon-ng start wlan1
  airodump-ng wlan1
  airodump-ng wlan1 --bssid E0:24:81:EF:01:B8 --channel 5 --write test
  aircrack-ng test-01.cap -w dic.txt
  ```
