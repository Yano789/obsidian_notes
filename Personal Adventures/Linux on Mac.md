---
sticker: emoji//1f4bb
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


## Installing Apps
There are 2 ways to install apps on Linux (Fedora):
1. Using the Terminal
2. Using AppImages


###### Using the Terminal (Flatpak and Snap)
There are 2 providers that make it easy to install apps 
- Flatpak - https://flatpak.org/
- Snap - https://snapcraft.io/
**NOTE: Make sure the app is Arm64 Compatible** 


###### Using AppImages
There are many ways to launch AppImages. However, I prefer to use **AppImage-Integrator** by apapamarkou

Link - https://github.com/apapamarkou/appimage-integrator

Make sure to install the dependency so that it runs smoothly:

```
sudo dnf install inotify-tools git wget
```


Once you install the dependency, run this code is to auto create an Applications Folder in your home directory:

```
wget -qO- https://raw.githubusercontent.com/apapamarkou/appimage-integrator/main/src/appimage-integrator-install-git | bash
```

Once that is done, you can place your AppImages into this applications folder and you will be able to find it in rofi (Super + D).

#### Optional
There are times when your gpu can cause rendering issues that will cause apps to disappear after some time. If this does happen, you can go to the .desktop file of your application (located in `~/.local/share/applications`) and include this line of code

```
--js-flags="--nodecommit_pooled_pages"
```

This is caused by Electron ...

## Battery Life Optimization
There are 2 options that will improve battery life:
1. TLP - Focuses on more parts of the OS
2. AutoCPU-Freq - Focuses more on the CPU (has better performance in my case)

###### TLP
```
sudo dnf install tlp
```

```
sudo tlp start
```

###### AutoCpu-Freq
Link - https://github.com/AdnanHodzic/auto-cpufreq?tab=readme-ov-file#installing-auto-cpufreq

```
git clone https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq && sudo ./auto-cpufreq-installer
```

Run the following code to let auto-cpufreq open on startup
```
sudo auto-cpufreq-install
```

**NOTE: DO NOT RUN BOTH OF THESE AT THE SAME TIME!** 