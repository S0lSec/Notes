# Add Cloud-Init Disk
1. Go to ISO directory
2. Import img file into the vm
	1. `qm importdisk 105 server.img NFS-VMs`
3. Go to VM you imported the img to
4. Go Hardware then double click the unused disk
5. Click Add
6. Edit Boot Order
7. Enable the disk and drag to the top
# Add Cloud-Init Drive
1. Go VM > Hardware
2. Click Add > CloudInit Drive
# Creating a Template
1. Right Click the VM
2. Click Convert to Template then Yes
# Deploying a Cloud-Init VM
1. Right Click the VM
2. Click Clone
3. Check the Clones Hard Disk size and make sure its enough
4. If not expand it
5. Go to Cloud-Init
6. Double Click user + password and add a user + password
7. Double Click IP Config and set IP address