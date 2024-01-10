# grub-windows-and-linux

Installing grub after windows is a task.

This repository provides instructions and commands for restoring the GRUB bootloader on a system where Windows has been installed after Ubuntu, resulting in GRUB being overwritten by the Windows bootloader.

## Dual Booting Ubuntu with Windows

If you decide to dual boot Ubuntu with Windows, there are two scenarios to consider:

1. **Install Ubuntu After Windows:**
   - No special steps are required in this case. Ubuntu's installer (GRUB) will automatically detect Windows and provide a dual-boot menu during startup.

2. **Install Windows After Ubuntu:**
   - Installing Windows after Ubuntu can overwrite the GRUB bootloader, causing the system to boot directly into Windows without presenting the dual-boot menu.

## Instructions for Restoring GRUB after Windows Installation

Follow these steps after installing Windows to restore the GRUB bootloader:

### 1. Boot into an Ubuntu Live USB:

   Boot your computer using an Ubuntu Live USB. You can create a Live USB using tools like Rufus or BalenaEtcher.

### 2. Open a Terminal and Run the Following Commands:

   ```bash
   sudo mount /dev/nvme1n1p2 /mnt
   sudo mount /dev/nvme1n1p1 /mnt/boot/efi
   sudo mount --bind /dev /mnt/dev
   sudo mount --bind /sys /mnt/sys
   sudo mount --bind /proc /mnt/proc
   sudo mount --bind /run /mnt/run
   ```

### 3. Chroot into the Mounted System:

   ```bash
   sudo chroot /mnt
   ```

### 4. Update GRUB:

   ```bash
   os-prober
   update-grub
   ```

### 5. Exit the Chroot Environment:

   ```bash
   exit
   ```

### 6. Unmount the System Partitions:

   ```bash
   sudo umount --bind /dev /mnt/dev
   sudo umount --bind /sys /mnt/sys
   sudo umount --bind /proc /mnt/proc
   sudo umount --bind /run /mnt/run
   sudo umount /mnt/boot/efi
   sudo umount /mnt
   ```

After completing these steps, restart your computer. You should now see the GRUB menu during startup, allowing you to choose between Ubuntu and Windows.

Good luck with your dual-boot setup!
