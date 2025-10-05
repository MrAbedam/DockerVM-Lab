# DockerVM-Lab

## Overview
**DockerVM-Lab** is a containerized environment that allows you to run full-featured virtual machines inside a Docker container.  
It combines **Ubuntu Desktop**, **QEMU**, and **noVNC**, enabling access to the VM’s graphical interface directly from a web browser.

Key features include:
- **Nested Virtualization:** Run a virtual machine inside Docker without installing additional hypervisors on the host.
- **Flexible Boot Options:** Boot from an ISO for a fresh OS install or from an existing qcow2 disk to continue previous work.
- **Persistent Disks:** Save VM state in qcow2 files for snapshots and reuse.
- **Browser-Based GUI:** Access both the Ubuntu desktop and nested VM through noVNC in any modern browser.
- **Cross-Platform Compatibility:** Works on any system with Docker installed.

This setup provides a sandboxed, portable environment to explore operating system installation, disk management, and virtualization concepts.


## Scenario Goal
- Run a full Ubuntu desktop environment inside Docker.
- Access the desktop and VMs through a browser via noVNC.
- Launch and manage a QEMU VM inside the container.
- Support booting from either an ISO image (fresh install) or an existing qcow2 disk.
 


## Setup and Execution
1. Build Docker Image
```bash
 docker build -t <image_name> .
```
2. Run Container
```bash
docker run -it -p 6080:6080 --name <container_name> <image_name>
```
3. Access Desktop via browser
```bash
http://localhost:6080/vnc.html
password = 123456
```
It only requires to put your desired .iso file in ISOHOLDER, Later on you can export the disk in .qcow2 form and boot other .iso or .qcow2 files.


