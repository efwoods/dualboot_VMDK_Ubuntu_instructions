# dualboot_VMDK_Ubuntu_instructions
Instructions for installing an Ubuntu Image on a secondary Hard Drive and accessing that image through a vmdk using virtualbox

# Reference Videos:


# Instructions

## File Partioning Ubuntu
All partitions are logical
Set 20 GB for / (to install software)
set 4 GB for swap
Set the remainder for /home 

## Switch to Windows
Using Admin CMD
Note the device ID of the secondary harddrive `wmic diskdrive list brief /format:list`
Create the VMDK with ` VBoxManage internal commands createrawvmdk -filename "C:\ABITRARYNAMEOFYOURVMDK.vmdk" -rawdisk \\.PhysicalDrive#` note that # is the number indicated from the device ID of the secondary harddrive.

## Switch to Ubuntu to create the bootable iso 
On the deskotop create folder structure `iso/boot/grub`
cp files with `cp /usr/lib/grub/i386-pcf/* /home/USERNAME/Desktop/iso/boot/grub`
`cp /usr/lib/grub/i386-pcf/* /home/USERNAME/Desktop/iso/boot/grub`
`cp /boot/grub/grub.cfg /home/USERNAME/Desktop/iso/boot/grub`
edit the grub.cfg to remove the option to boot into windows to prevent crash with: `sudo nano /home/USERNAME/Destop/iso/boot/grub/grub.cfg`
remove every line between ### BEGIN and ### End that references Windows
make the iso with grub-mkrescue -o boot.iso /home/USERNAME/Desktop/iso
install the required software (sudo apt install xorriso) && rerun the above command
move the iso to an external thumb drive

## switch to windows
create a new vm
add the vmdk as the hard drive
add the boot.iso as the disk
.

