# dualboot_VMDK_Ubuntu_instructions
Instructions for installing an Ubuntu Image on a secondary Hard Drive and accessing that image through a vmdk using virtualbox

# Reference Videos:
- [instructions for creating an Ubuntu VM](https://www.youtube.com/watch?v=u5QyjHIYwTQ)
- [instructions for creating vmdk and boot iso](https://lifehacker.com/how-to-dual-boot-and-virtualize-the-same-partition-on-y-493223329)
- [video of creating vmdk and boot iso](https://www.youtube.com/watch?time_continue=11&v=D9TePODkYME&feature=emb_title)



# Instructions

## File Partioning Ubuntu
- All partitions are logical
  1. Set 20 GB for / (to install software)
  2. set 4 GB for swap
  3. Set the remainder for /home 

## Switch to Windows
- Using Admin CMD
  1. Note the device ID of the secondary harddrive `wmic diskdrive list brief /format:list`
  2.Create the VMDK with ` VBoxManage internal commands createrawvmdk -filename "C:\ABITRARYNAMEOFYOURVMDK.vmdk" -rawdisk \\.PhysicalDrive#` note that # is the number indicated from the device ID of the secondary harddrive.

## Switch to Ubuntu to create the bootable iso 
1. On the deskotop create folder structure `iso/boot/grub`
2. cp files with:
  - `cp /usr/lib/grub/i386-pc/* /home/USERNAME/Desktop/iso/boot/grub`
  - `cp /boot/grub/grub.cfg /home/USERNAME/Desktop/iso/boot/grub`
  - `cp /boot/grub/grub.cfg /home/USERNAME/Desktop/iso/boot/grub`
3. edit the grub.cfg to remove the option to boot into windows to prevent crash with: `sudo nano /home/USERNAME/Destop/iso/boot/grub/grub.cfg`
4. remove every line between ### BEGIN and ### End that references Windows
5. make the iso with grub-mkrescue -o boot.iso /home/USERNAME/Desktop/iso
6. install the required software (sudo apt install xorriso) && rerun the above command
7. move the boot.iso under /home to an external thumb drive

## switch to windows
1. create a new vm
2. add the vmdk as the hard drive
3. add the boot.iso as the disk
4. .

