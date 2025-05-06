---
sticker: emoji//0031-fe0f-20e3
---
## Asahi Linux
Link - https://asahilinux.org/
- Runs Linux (Fedora) on Apple Macs
- There is a Arch version but it's unofficial so I wanted to be safe

Enter the following code on terminal

```
curl https://alx.sh | sh
```

Then, follow the instructions **VERY** carefully

## Hyprland Setup
Link - https://github.com/JaKooLit/Fedora-Hyprland

I used JaKootLit's Fedora Hyprland script to get all the basic tools and styles/themes so I don't have to set it up myself and it saved so much time

```
git clone --depth=1 https://github.com/JaKooLit/Fedora-Hyprland.git ~/Fedora-Hyprland
cd ~/Fedora-Hyprland
chmod +x install.sh
./install.sh
```

You can follow the documentation to setup your colors and themes


This code fixed the crashing for Obsidian:

```
--js-flags="--nodecommit_pooled_pages"
```


This code is to auto add AppImages to Applications Folder:

```
wget -qO- https://raw.githubusercontent.com/apapamarkou/appimage-integrator/main/src/appimage-integrator-install-git | bash
```