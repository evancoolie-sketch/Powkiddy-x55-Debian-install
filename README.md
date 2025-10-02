# Powkiddy-x55-Debian-install
Powkiddy x55 Debian install


sudo apt update -y
sudo apt install -y qemu-user-static debootstrap squashfs-tools
mkdir ~/debian-arm64-rootfs
sudo debootstrap --arch=arm64 --foreign stable ~/debian-arm64-rootfs http://deb.debian.org/debian/
sudo cp /usr/bin/qemu-aarch64-static ~/debian-arm64-rootfs/usr/bin/


sudo mount --bind /dev ~/debian-arm64-rootfs/dev
sudo mount --bind /dev/pts ~/debian-arm64-rootfs/dev/pts
sudo mount --bind /proc ~/debian-arm64-rootfs/proc
sudo mount --bind /sys ~/debian-arm64-rootfs/sys
sudo mount --bind /tmp ~/debian-arm64-rootfs/tmp


#this command puts you inside of the future system#
sudo chroot ~/debian-arm64-rootfs /bin/bash

#after chroot feel free to keep copy and pasting multiple commands# 

/debootstrap/debootstrap --second-stage

apt install -y locales dialog

#echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
#locale-gen
#update-locale LANG=en_US.UTF-8

export DEBIAN_FRONTEND=noninteractive
apt update
apt install -y xfce4 xfce4-goodies lightdm xserver-xorg xinit dbus-x11 mesa-utils mesa-vulkan-drivers libgl1-mesa-dri firmware-linux network-manager pulseaudio
###
#apt install -y xfce4 xfce4-goodies lightdm
#apt install -y xserver-xorg xinit dbus-x11
#apt install -y mesa-utils mesa-vulkan-drivers libgl1-mesa-dri
#apt install -y firmware-linux network-manager pulseaudio
###
systemctl enable lightdm






#after all the chroot stuff#
exit

#unmounts the mounted directories from before#
sudo umount ~/debian-arm64-rootfs/tmp
sudo umount ~/debian-arm64-rootfs/sys
sudo umount ~/debian-arm64-rootfs/proc
sudo umount ~/debian-arm64-rootfs/dev/pts
sudo umount ~/debian-arm64-rootfs/dev


sudo mksquashfs ~/debian-arm64-rootfs debian-arm64.squashfs -comp xz
