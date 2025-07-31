# Void Linux Install Gnome + Pipewire + Gaming
Guided install for my user preferences


## How to install with encrypted drive

https://docs.voidlinux.org/installation/guides/fde.html

### Use 80%free

`lvcreate --name home -l 80%FREE voidcrypt`

https://docs.voidlinux.org/installation/guides/fde.html#encrypted-volume-configuration

### Important step for grub

`grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id="Void"`

`mkdir -p /boot/efi/EFI/BOOT`

`cp /boot/efi/EFI/Void/grubx64.efi /boot/efi/EFI/BOOT/BOOTX64.efi`


https://docs.voidlinux.org/installation/guides/chroot.html#installing-on-removable-media-or-non-compliant-uefi-systems

# Post install

## User

https://docs.voidlinux.org/config/users-and-groups.html#sudo

`useradd murky`
`usermod -aG wheel,video,audio,murky murky`

## Internet

`cp -R /etc/sv/dhcpcd-eth0 /etc/sv/dhcpcd-enp6s0` 

`sed -i 's/eth0/enp6s0/' /etc/sv/dhcpcd-enp6s0/run`

`ln -s /etc/sv/dhcpcd-enp6s0 /var/service/`

https://docs.voidlinux.org/config/network/index.html#dhcpcd

## Initial Packages
`xbps-install -Su` Update 

https://docs.voidlinux.org/xbps/index.html#updating

`xbps-install void-repo-nonfree void-repo-multilib void-repo-multilib-nonfree` Repos

https://docs.voidlinux.org/xbps/repositories/index.html#subrepositories

`xbps-install xtools xmirror vim` Tools

`xmirror` Set mirror to CDN

`xi -S linux-firmware-amd` Firmware 

https://docs.voidlinux.org/config/firmware.html#amd

`xi -S mesa-dri mesa-dri-32bit vulkan-loader vulkan-loader-32bit mesa-vulkan-radeon mesa-vulkan-radeon-32bit amdvlk amdvlk-32bit xf86-video-amdgpu xf86-video-amdgpu-32bit mesa-vaapi mesa-vaapi-32bit mesa-vdpau mesa-vdpau-32bit` Graphical Drivers 

https://docs.voidlinux.org/config/graphical-session/graphics-drivers/amd.html

`ln -s /etc/sv/dbus /var/service/` D-Bus 

https://docs.voidlinux.org/config/session-management.html#d-bus

`xi -S elogind` elogind 

https://docs.voidlinux.org/config/session-management.html#elogind

`xi -S dejavu-fonts-ttf xorg-fonts noto-fonts-ttf noto-fonts-cjk noto-fonts-emoji nerd-fonts` Fonts 

https://docs.voidlinux.org/config/graphical-session/fonts.html

## Gnome

`xi -S gnome gnome-apps`

`ln -s /etc/sv/gdm /var/service/`

https://docs.voidlinux.org/config/graphical-session/gnome.html

## Audio with Pipewire

`xi -S pipewire`

`mkdir -p /etc/pipewire/pipewire.conf.d`

`ln -s /usr/share/examples/wireplumber/10-wireplumber.conf /etc/pipewire/pipewire.conf.d/`

`ln -s /usr/share/examples/pipewire/20-pipewire-pulse.conf /etc/pipewire/pipewire.conf.d/`

`vim /etc/xdg/autostart/pipewire.desktop`

```
[Desktop Entry]
Type=Application
Name=Pipewire
Exec=pipewire
```

https://np.reddit.com/r/backtickbot/comments/o59fym/httpsnpredditcomrvoidlinuxcommentso590vxautostarti/

https://docs.voidlinux.org/config/media/pipewire.html

## Steam, Lutris & Wine

`xi -S steam lutris wine wine-devel wine-32bit winetricks gamemode libgcc-32bit libstdc++-32bit libdrm-32bit libglvnd-32bit mono mesa-32bit vulkan-loader mesa-dri-32bit`

less /usr/share/doc/steam/README.voidlinux

https://github.com/UltraToon/void-guide?tab=readme-ov-file#desktop-guide-install-gui-terminal-and-browser

## ESYNC (Alter murky for your user)

`sudo echo 'murky hard nofile 524288' >> /etc/security/limits.conf`

https://gist.github.com/craftybloxy/852d1093c8d7c51440ef1980b1344ebf#step-1-editing-limitsconf
