# Hard Drive Encryption
1. Go to Server > Shell
2. Lock Disk
	1. `cryptsetup luksFormat /dev/sdx`
3. Unlock Disk
	1. `cryptsetup LuksOpen /dev/sdx encrypted_disk`
# Formatting and Mounting an Encrypted Disk
1. Go to Server > Shell
2. `mkfs.ext4 /dev/mapper/encrypted_disk`
3. Mount Disk
4. Add Directory
	1. **Directory**: Mount location
	2. **Content**: Disk image, Container
# ZFS Encryption
1. Go to Server > Shell
2. `zpool create -O encryption=on -O keyformat=passphrase encrypted-zfs raidz1 sdd sde sdf`
3. Add ZFS in Datacenter Storage