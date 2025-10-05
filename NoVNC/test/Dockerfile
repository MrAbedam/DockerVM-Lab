FROM ubuntu:latest


ENV PASSWORD=123456 \
    USER=root \
    DISPLAY=:1

RUN apt update && apt install -y \
    xfce4 xfce4-goodies tightvncserver \
    novnc websockify python3-numpy \
    build-essential net-tools curl git \
    software-properties-common && \
    apt clean && rm -rf /var/lib/apt/lists/*

RUN apt update && apt install -y dbus-x11

RUN mkdir -p /root/.vnc && \
 echo "$PASSWORD" | vncpasswd -f > /root/.vnc/passwd && \
  chmod 600 /root/.vnc/passwd

RUN touch /root/.Xauthority && chmod 600 /root/.Xauthority


RUN echo "#!/bin/bash\nxrdb \$HOME/.Xresources\nstartxfce4 &" > /root/.vnc/xstartup && \
    chmod +x /root/.vnc/xstartup


RUN echo '#!/bin/bash\n\
vncserver -kill :1 2>/dev/null\n\
rm -rf /tmp/.X11-unix/X1 /tmp/.X1-lock ~/.vnc/*:1*\n\
vncserver :1\n\
websockify -D --web=/usr/share/novnc/ --cert=/etc/ssl/novnc.pem 6080 localhost:5901\n' > /usr/local/bin/start-vnc.sh && \
chmod +x /usr/local/bin/start-vnc.sh


RUN mkdir -p /etc/ssl && \
    openssl req -x509 -nodes -newkey rsa:2048 \
    -keyout /etc/ssl/novnc.pem \
    -out /etc/ssl/novnc.pem \
    -days 365 \
    -subj "/C=US/ST=State/L=City/O=Organization/OU=Unit/CN=localhost" && \
    chmod 644 /etc/ssl/novnc.pem


RUN apt update && apt install qemu-system-x86 -y

COPY ./IsoHolder/iso.ISO /root/iso.ISO

RUN echo '#!/bin/bash\n\
ISO_PATH="/root/iso.ISO"\n\
DISK_PATH="/root/mydisk.qcow2"\n\
HELLO_FILE="/root/hello.txt"\n\
\n\
echo "Choose boot mode:"\n\
echo "1. Boot from ISO (fresh install)"\n\
echo "2. Boot from disk (existing OS)"\n\
read -p "Enter 1 or 2: " BOOTMODE\n\
\n\
if [ "$BOOTMODE" == "1" ]; then\n\
  echo "Booting from ISO..."\n\
  qemu-img create -f qcow2 "$DISK_PATH" 50G\n\
  echo "Hello from ISO install!" > "$HELLO_FILE"\n\
  qemu-system-x86_64 -m 4096 -smp 2 \\\n\
    -drive file="$DISK_PATH",format=qcow2,if=ide \\\n\
    -usb -device usb-mouse -device usb-kbd  -device usb-tablet \\\n\
    -boot d -cdrom "$ISO_PATH" \\\n\
    -display sdl\\\n\
    -device VGA,vgamem_mb=64\n\
elif [ "$BOOTMODE" == "2" ]; then\n\
  echo "Booting from disk..."\n\
  echo "Attempting to read persisted file:"\n\
  cat "$HELLO_FILE"\n\
  qemu-system-x86_64 -m 4096 -smp 2 \\\n\
    -drive file="$DISK_PATH",format=qcow2,if=ide \\\n\
    -usb -device usb-mouse -device usb-kbd  -device usb-tablet \\\n\
    -boot c \\\n\
    -display sdl\\\n\
    -device VGA,vgamem_mb=64\n\
else\n\
  echo "Invalid selection. Exiting."\n\
fi\n' > /usr/local/bin/start-qemu.sh && \
chmod +x /usr/local/bin/start-qemu.sh



CMD ["/bin/bash", "-c", "start-vnc.sh; start-qemu.sh ;tail -f /dev/null"]

