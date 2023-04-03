<div align="center">
   <h1>Arch Linux Distro</h1>

   <p><img src="./screenshots/desktop.jpg" /></p>
   <p>
      <img src="https://img.shields.io/badge/MAINTAINED-YES-green?style=for-the-badge">
      <img src="https://img.shields.io/badge/LICENSE-MIT-blue?style=for-the-badge">
   </p>
   <p>Minimal Arch Linux Distribution with GNOME, preinstalled Paru as AUR Helper and enabled MultiLib.</p>
</div>

## Test

- GNOME Boxes: `43.4-stable`
- Arch ISO: `archlinux-2023.04.01-x86_64.iso`

## Features

- 100% TUI Installation
- LTS Kernel & GNOME Desktop
- Systemd Bootloader
- Disk Encryption
- Network Manager
- Reflector Service
- Pacman Parallel Downloads
- Silent Boot & [Themed Bootsplash](https://github.com/murkl/plymouth-theme-arch-elegant)
- AUR Helper & Multilib
- Graphics Driver

## Step by Step Installation

### 1. Prepare bootable USB Device

- Download latest Arch Linux ISO from **[here](https://www.archlinux.de/download)**
- Write to device: `dd bs=4M if=archlinux-*.iso of=/dev/sdX status=progress`
- Alternatively use **[Etcher](https://www.balena.io/etcher)**

### 2. Configure BIOS Settings

- Disable Secure Boot
- Set Boot Mode to UEFI
- Set Real Time Clock to **[UTC](https://time.is/de/UTC)**

### 3. Boot from USB Device

- Load Keyboard Layout: `loadkeys de-latin1` (use prefered language)
- Connect to WLAN, run `iwctl` and type into console: `station wlan0 connect "SSID"`
- Run Installer: `curl -Ls http://arch.webhop.me | bash`

<p><img src="./screenshots/installer.png" /></p>

#### Custom Properties

If the file `default.conf` exists, it will be sourced automatically by the `installer.sh` script and the values for Arch Linux installation will be overridden.

```
ARCH_HOSTNAME="virt"
ARCH_USERNAME="moritz"
ARCH_PASSWORD="secret"
ARCH_DISK="/dev/vda"
ARCH_BOOT_PARTITION="/dev/vda1"
ARCH_ROOT_PARTITION="/dev/vda2"
ARCH_ENCRYPTION_ENABLED="true"
ARCH_SWAP_SIZE="8"
ARCH_LANGUAGE="german"
ARCH_TIMEZONE="Europe/Berlin"
ARCH_LOCALE_LANG="de_DE.UTF-8"
ARCH_LOCALE_GEN_LIST=("de_DE.UTF-8 UTF-8" "de_DE ISO-8859-1")
ARCH_VCONSOLE_KEYMAP="de-latin1-nodeadkeys"
ARCH_VCONSOLE_FONT="eurlatgr"
ARCH_KEYBOARD_LAYOUT="de"
ARCH_KEYBOARD_VARIANT="nodeadkeys"
ARCH_DRIVER="none"
```

## Recommendation

By default gnome-software will download updated packages from the Arch Linux repositories. This forces GNOME Software to refresh the package lists for pacman automatically. This is the equivalent to `pacman -Sy`. If the user ignores the GNOME software update prompt, but does install a new package, that will result in partial upgrades, which are unsupported. To prevent GNOME Software from refreshing the package lists set the following dconf setting after Arch Linux installation:

```
gsettings set org.gnome.software download-updates false
```

## Desktop Customization

- Icon Theme: https://github.com/vinceliuice/Tela-icon-theme
- Firefox Theme: https://github.com/rafaelmardojai/firefox-gnome-theme
- Libadwaita GTK Theme: https://github.com/lassekongo83/adw-gtk3
- Libadwaita GTK Colors: https://github.com/lassekongo83/adw-colors
- Libadwaita Customization Tool: https://github.com/GradienceTeam/Gradience

### GNOME Shell Extensions

- https://extensions.gnome.org/extension/1010/archlinux-updates-indicator/
- https://extensions.gnome.org/extension/1160/dash-to-panel/
- https://extensions.gnome.org/extension/3193/blur-my-shell/
- https://extensions.gnome.org/extension/3843/just-perfection/

#### Additional Extensions

- https://extensions.gnome.org/extension/19/user-themes/
- https://extensions.gnome.org/extension/615/appindicator-support/
- https://extensions.gnome.org/extension/5237/rounded-window-corners/
- https://extensions.gnome.org/extension/3733/tiling-assistant/

## Rescue & Recovery

If you need to rescue your Arch Linux in case of a crash, boot from a USB device and follow these instructions.

### 1. Disk Information

- Show disk info: `lsblk`
  - Example Disk: `/dev/sda`
  - Example Boot: `/dev/sda1`
  - Example Root: `/dev/sda2`

**Note:** _You may have to replace `/dev/sda` with your own disk_

### 2. Mount

- Create mount dir: `mkdir -p /mnt/boot`
- Mount root partition
  - a) Encryption enabled
    - `cryptsetup open /dev/sda2 cryptroot`
    - `mount /dev/mapper/cryptroot /mnt`
  - b) Encryption disabled
    - `mount /dev/sda2 /mnt`
- Mount boot partition: `mount /dev/sda1 /mnt/boot`

### 3. Chroot

- Enter chroot: `arch-chroot /mnt`
- _Fix your Arch Linux..._
- Exit: `exit`