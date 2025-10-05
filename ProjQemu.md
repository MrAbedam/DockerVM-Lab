# 🐋 Docker Training Scenario — Nested Virtualization with Ubuntu + QEMU + noVNC

## Overview
In this project, students will create and run an Ubuntu desktop environment inside a Docker container, and within that container, start a virtual machine (VM) using QEMU. The graphical interface will be accessible directly from a web browser through noVNC. 

The VM can boot either from an ISO image (for a fresh OS installation) or from an existing qcow2 disk file. This setup provides a sandboxed, portable environment to explore operating system installation, disk management, and virtualization concepts.

---

## Scenario Goal
- Run a full Ubuntu desktop inside Docker.
- Access it through a browser (noVNC).
- Use QEMU to launch a VM inside the container.
- Support booting from either an ISO or an existing qcow2 disk.
- (Bonus) Convert VirtualBox (.vdi) or VMware (.vmdk) disks to qcow2 and boot them.

---

## Learning Objectives
By completing this scenario, you will learn:
- How to run GUI-based Docker containers
- How to configure and use noVNC
- How to launch and manage VMs inside Docker using QEMU
- How to work with qcow2 disk images and snapshots
- How to convert and reuse disks from other virtualization platforms
- The concept of nested virtualization and isolated execution environments

---

## Bonus Challenges
1. Add a simple text-based menu for managing multiple ISOs or disks.
2. Experiment with KVM acceleration and measure performance differences.
3. Create automatic snapshot-and-restore scripts.
4. Reduce the image size using multi-stage Docker builds.
5. Integrate system monitoring tools (htop, vnstat, etc.) inside the container.

---

## Deliverables
To complete the assignment, students should demonstrate:
1. A working Docker container accessible via browser (noVNC on port 6080).
2. Successful launch of a QEMU VM from both ISO and existing disk.
3. Persistent qcow2 storage in DiskHolder.
4. (Bonus) Booting a converted VirtualBox or VMware disk.

---

## Troubleshooting Tips
- If the desktop doesn’t load, check container logs: docker logs ubuntu-desktop
- To enter the container shell: docker exec -it ubuntu-desktop bash
- To stop the container: docker stop ubuntu-desktop
- Always shut down the VM gracefully to prevent disk corruption.
- If port 6080 is in use, change it in the docker run command (e.g., -p 6090:6080).

---

## References
QEMU Documentation: https://www.qemu.org/documentation/  
Dockerfile Reference: https://docs.docker.com/engine/reference/builder/  
noVNC GitHub: https://github.com/novnc/noVNC  
QEMU Disk Formats: https://wiki.qemu.org/Documentation/Images  

---

This project provides a controlled sandbox for exploring OS installation, disk persistence, and nested virtualization.  
By the end of the lab, you will have a fully functional graphical environment that runs a VM inside Docker, accessible entirely from your web browser.
