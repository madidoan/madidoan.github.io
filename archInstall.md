# Arch Linux Installation Documentation 
## After creating and opening your virtual environment, put firmware=”efi” in .vmx file using text editor 
## Check if Pre-Installation worked 
## Check if you installed the right firmware and the output should be 64 
    cat /sys/firmware/efi/fw_platform_size 
## Check network 
    ip link 
    ping archlinux.org 
## Date and time check
    Datetimectl 
    Was at  2023-10-28 19:49:57 
## Partitioning Disks 
    Fdisk -l 
    Fdisk /dev/sda2 to make partition  
### Type m to see manual options, I typed n after that to create a partition 
    Should be partition number 1 and 2048 +500M to partition sda1 
### Type n again to make partition 2 and the rest of the settings should be default to make sda2 use the rest of the space 
## Since I did not partition a third swap disk, just hit w to save the partitions and that’s it 
    Mkfs.ext4 /dev/sda2 and mkfs.fat  -F /dev/sda1 to format the partitions 
## Mount the partitions using 
    mount /dev/root_partition /mnt and mount --
    mkdir /dev/efi_system_partition /mnt/boot 
## Installation 
# Install base system (could take a while) 
    pacstrap -K /mnt base linux linux-firmware 
    genfstab -U /mnt >> /mnt/etc/fstab  
## to change to the root of new system, the root color changed for me
    arch-chroot /mnt
# Set time zone
    ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime 
## to make sure the clocks will remain synchronized 
    Hwclock –systohc 
## Edit /etc/locale.gen so you can localize and make LANG=en_US.UTF-8 
## Create hostname file in /etc/hostname, you may need to install nano for the past couple steps to edit the files. 
### Name hostname 
    nano /etc/hosts 
## Do this exact thing for some reason: 
    Set root password using psswd 
    Create users using useradd[name] and give them a password using passwd 
    Install sudo using pacman -s sudo 
    Youll need to specifier sudoers using EDITOR=nano visudo 
    Scroll and uncomment line that says “%wheel ALL=(ALL) ALL”  
## Wheel is an alias for sudo so to give a user sudo privileges do usermod -aG wheel[user] 
## Install grub  
### using pacman -S efibootmgr dosfstools os-prober mtools 
    Mkdir /boot/EFI, then mount using mount /dev/sda1 /bootEFI 
## Bootloader 
    using Grub-install –target=x86_64-efi –bootloader-id=grub_uefi –recheck 
    Grub-mkconfig -o /boot/grub/grub.cfg 
# Network Manager
    Pacman -S networkmanager vim 
    Pacman -Syu 
## Installing SSH 
    Pacman -S openssh 
## Enable Network Manager 
    Systemctl enable networkmanager 
## Reboot 
    Exit then unmount -l /mnt and Shutdown 
## LXDE UI installation 
    Pacman -S lxde, might need sudo 
    Sudo pacman -S xorg-xinit 
    Nano .xintric 
    Write “exec startlxde’ to start 
    Startx 
# There should be a clear change of environment 
# Install Git 
    Sudo pacman -S git 
# Installing browser 
    Git clone https://aur.archlinux.org/browsh.git 
    Sudo pacman -S base-devel 
    Makepkg make sure youre in the directory with PKGBUILD 
    Sudo pacman -U firefox 
# Installing zsh 
    Sudo pacman -S zsh zsh-completions 
    Zsh 
    0 
# Aliases
    Alias c="clear"
    Alias ls='ls -color=auto"