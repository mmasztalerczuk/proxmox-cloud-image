# 🚀 Cloud image with installed promox and cloud-init

## 📄 The image should be used for educational/homelab purposes and not for commercial use. 


The image is created in github actions. You can view the entire pipeline here

## ✅ List of installed packages:
 
- wget
- dialog
- os-prober 
- ifupdown2
- network-manager
- resolvconf
- locales
- build-essential
- module-assistant 
- cloud-init
- grub-pc
- grub2
- linux-image-amd64
- proxmox-default-kernel
- proxmox-ve 
- postfix 
- open-iscsi  

## 🚀 Getting Started
      
### 🍴 Preparation

- Download image
- Prepare cloud-init file

For example:

```
#cloud-config
preserve_hostname: false
hostname: {{ vm_name }}
users:
  - name: mariusz
    sudo: ALL=(ALL) NOPASSWD:ALL
    groups: users, admin
    home: /home/mariusz
    shell: /bin/bash
    lock_passwd: false


disable_root: false
chpasswd:
  list: |
     mariusz:mariusz123
     root:linux321
  expire: False
```

- Run new virtual machine with downloaded image and cloud-init config

For example:

```
virt-install --name {{ vm_name }} --mac={{ machine_mac }} --connect=qemu://system --memory 9000 --noreboot --cloud-init user-data=/tmp/cloud_init.cfg --network network=mainnetwork --disk {{ libvirt_pool_dir }}/{{ vm_name }}.qcow2 --os-variant debian12 --noautoconsole
      
```

- Proxmox should be available under port 8006. It is best to set a static IP for the selected mac address in your dhcp server.

## Thanks 🤝



