# Hyper-V
1. Delete disk from Proxmox VM
2. Get *.vhdx*
3. Convert to *.raw*
	1. `qemu-img convert -f vhdx Hyper-V.vhdx -O raw Hyper-V.raw`
4. Import as disk
	1. `qm importdisk 100 Hyper-V.raw NFS-VMs`
	2. **(Note: 100 is the VM ID)**
5. Double click on unused disk in VM
6. Click Add
7. Edit the BIOS, selecting *OVMF (UEFI)*
8. Go into Options and add disk to boot order
9. Set disk to position 1 in boot order
# VirtualBox/VMWare
1. Allow Storage server to import
	1. Go to cluster
	2. Select storage
	3. Edit content
	4. Add import
2. Go to Server storage
3. Upload *.ova* file
4. Import *.ova* as VM