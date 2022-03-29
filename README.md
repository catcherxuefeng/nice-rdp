# nice-rdp
linux rdp to windows
## 功能
- 转发本机的home & media目录
- 扬声器&麦克风
- 动态分辨率
- 自动重连
- 共享剪贴板
- 转发打印机
## 基于 xfreerdp 
```bash
apt install freerdp2-x11 -y
```

## 两个文件
### 一个启动脚本
注意位置&权限
```bash
#!/usr/bin/env bash
# 改成你自己的地址  
CLIENT_USER=
RDP_USER=administrator
RDP_PASS=123456
#RDP_DOMAIN="MYDOMAIN"
RDP_IP=192.168.100.25
RDP_PORT=3389
RDP_SCALE=100
#RDP_FLAGS=""
#MULTIMON="true"
#DEBUG="true"



if [ -z "$(which xfreerdp)" ]; then
        echo "You need xfreerdp!"
        echo "  sudo apt-get install -y freerdp2-x11"
        exit
fi

xfreerdp ${RDP_FLAGS} /d:"${RDP_DOMAIN}" /u:"${RDP_USER}" /p:"${RDP_PASS}" /v:${RDP_IP}:${RDP_PORT} /scale:${RDP_SCALE} /size:70%h60%w /drive:media,/media/${CLIENT_USER} /dynamic-resolution +clipboard +auto-reconnect +home-drive +aero /printer /sound /microphone /wm-class:"Microsoft Windows" 1> /dev/null 2>&1 &
```
### 一个桌面图标文件
把 $USER 改为你自己的用户名
位置 /home/$USER/.local/share/applications/win11.desktop
```bash
[Desktop Entry]
Name=Win11
Exec=/bin/bash /home/catcher/Shells/win11.sh
Terminal=false
Type=Application
StartupWMClass=Micorosoft Windows
Comment=Micorosoft Windows
Categories=Windows
```
