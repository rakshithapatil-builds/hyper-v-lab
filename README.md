# Hyper-V + Ubuntu Lab

Built a virtual lab on Windows using Hyper-V to learn virtualization, networking, and Linux administration.

## What I Built

- 2 Ubuntu VMs running on Hyper-V
- External, Internal, and Private Virtual Switches
- Static IP networking between VMs
- Checkpoint for rollback

## Lab 1: Single VM + Virtual Switch

1. Enabled Hyper-V on Windows
2. Downloaded Ubuntu 26.04 ISO - `ubuntu-26.04.1-desktop-amd64.iso`
3. Created Generation 2 VM - `ubuntu-lab`
   - 4GB RAM, 30GB Disk, UEFI
4. Fixed Secure Boot error by changing template to `Microsoft UEFI Certificate Authority`
5. Created Virtual Switches:
   - External Switch - VM gets real internet
   - Internal Switch - VM talks to host only
   - Private Switch - VM talks to other VMs only
6. Verified networking with `ip a` and `ping google.com`
7. Created Checkpoint for clean working state

## Lab 2: Two VMs Networking

1. Created 2nd VM - `ubuntu-lab-2` - 2GB RAM, 20GB Disk
2. Connected both VMs to `Private-Switch`
3. Private Switch has no DHCP, so configured Static IP manually:

   - VM-1: `192.168.10.11/24`
   - VM-2: `192.168.10.12/24`

4. Edited Netplan file `/etc/netplan/50-cloud-init.yaml`:
   ```yaml
   network:
     version: 2
     ethernets:
       eth0:
         dhcp4: false
         addresses:
           - 192.168.10.12/24
