# Linux Virtualization Guide

## 1. Check if Your CPU Supports Virtualization

Open a terminal and run the following command:
```
lscpu
```


Look in the output for one of these extensions:
```
grep vmx /proc/cpuinfo # For Intel processors
grep svm /proc/cpuinfo # For AMD processors

vmx: Support for Intel VT-x
svm: Support for AMD-V
```


---

## 2. Install Virtualization Tools

Install the necessary packages using APT:
```
sudo apt update
sudo apt install virt-manager # Graphical interface (GUI)
sudo apt install libvirt-daemon-system libvirt-clients # Backend and CLI
```


Note: `virsh` is included with `libvirt-clients`.

---

## 3. Create Virtual Machines with Virt-Manager (GUI)

Open Virt-Manager from the application menu or by running:
```
virt-manager
```


Click on **"Create a new virtual machine"** and follow the setup wizard.

---

## 4. Configure Serial Console Output in the VM

This allows you to connect to the VM using `virsh` over a serial console.

### a. Edit GRUB Configuration in the VM

Inside the VM, edit the following file:
```
sudo nano /etc/default/grub
```

Add or modify this line:
```
GRUB_CMDLINE_LINUX_DEFAULT="console=tty0 console=ttyS0,115200n8"
```


### b. Update GRUB
```
sudo update-grub
```


### c. Power Off the VM from Virt-Manager

Use the GUI to shut down the virtual machine normally.

---

## 5. Manage VMs via `virsh` (Command Line)

### List all virtual machines
```
virsh list --all
```

### Start a virtual machine
```
virsh start name_of_the_vm
```

### Check if the VM is running
```
virsh list
```

### Connect to the serial console of a VM (e.g., `debian12`)
```
virsh console name_of_the_vm
```

To exit the console, use the key combination:
```
Ctrl + ]
```
