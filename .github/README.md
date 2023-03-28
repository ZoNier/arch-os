<div align="center">
   <h1>Arch Linux Distro</h1>
   <p><img src="screenshots/installer.png" /></p>
   <p>
      <img src="https://img.shields.io/badge/MAINTAINED-YES-green?style=for-the-badge">
      <img src="https://img.shields.io/badge/LICENSE-MIT-blue?style=for-the-badge">
   </p>
   <p>Minimal Arch Linux Distribution with GNOME, preinstalled Paru as AUR Helper and enabled MultiLib.</p>
</div>

## Features

- 100% TUI Installation
- LTS Kernel & GNOME Desktop
- Systemd Bootloader
- Disk Encryption
- Network Manager
- Reflector Service
- Pacman Parallel Downloads
- Silent Boot & Bootsplash
- AUR Helper & Multilib
- Graphics Driver
- Works in GNOME Boxes

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

## Recommendation

By default gnome-software will download updated packages from the Arch Linux repositories. This forces GNOME Software to refresh the package lists for pacman automatically. This is the equivalent to `pacman -Sy`. If the user ignores the GNOME software update prompt, but does install a new package, that will result in partial upgrades, which are unsupported. To prevent GNOME Software from refreshing the package lists set the following dconf setting after Arch Linux installation:

```
gsettings set org.gnome.software download-updates false
```

## Desktop Customization

<p><img src="screenshots/desktop.jpg" /></p>

### GNOME Shell Extensions

#### Recommendation

- https://extensions.gnome.org/extension/1010/archlinux-updates-indicator/
- https://extensions.gnome.org/extension/1160/dash-to-panel/
- https://extensions.gnome.org/extension/3193/blur-my-shell/
- https://extensions.gnome.org/extension/3843/just-perfection/
- https://extensions.gnome.org/extension/3733/tiling-assistant/

#### Additional

- https://extensions.gnome.org/extension/19/user-themes/
- https://extensions.gnome.org/extension/615/appindicator-support/
- https://extensions.gnome.org/extension/5237/rounded-window-corners/
- https://extensions.gnome.org/extension/5612/focus-indicator/

### Theming

- Icon Theme: https://github.com/vinceliuice/Tela-icon-theme
- Firefox Theme: https://github.com/rafaelmardojai/firefox-gnome-theme
- Libadwaita GTK Theme: https://github.com/lassekongo83/adw-gtk3
- Libadwaita GTK Colors: https://github.com/lassekongo83/adw-colors
- Libadwaita Customization Tool: https://github.com/GradienceTeam/Gradience