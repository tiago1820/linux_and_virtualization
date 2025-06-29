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

## 4. Edit /boot/loader.conf
Inside the FreeBSD VM, open a terminal as root and run:

```
echo 'console="comconsole"' >> /boot/loader.conf
```

This tells the bootloader to use the serial console.

Edit /etc/ttys
Open the file:

```
ee /etc/ttys
```

Look for the following line (it might be commented out or set to "off"):

```
ttyu0   "/usr/libexec/getty std.9600"   vt100   on secure
```

Make sure it's exactly like that — with on secure, and without a # at the beginning.

Save and close the file.

Reboot FreeBSD

```
reboot
```

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

### Connect to the serial console of a VM (e.g., `freebsd`)
```
virsh console name_of_the_vm
```

To exit the console, use the key combination:
```
Ctrl + ]
```
