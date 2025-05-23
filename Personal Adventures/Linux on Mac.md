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


### Using the Terminal (Flatpak and Snap)
There are 2 providers that make it easy to install apps 
- Flatpak - https://flatpak.org/
- Snap - https://snapcraft.io/
**NOTE: Make sure the app is Arm64 Compatible** 


### Using AppImages
There are many ways to launch AppImages. However, I prefer to use AppImageLauncher - https://github.com/TheAssassin/AppImageLauncher/tree/v2.2.0

Once it is installed, simply download any AppImage and run the following command:

```
ail-cli integrate <path to AppImage>
```

#### Optional
There are times when your GPU can cause rendering issues that will cause apps to disappear after some time. If this does happen, you can go to the .desktop file of your application (located in `~/.local/share/applications`) and include this line of code in the *Exec line*

```
--js-flags="--nodecommit_pooled_pages"
```

This is caused by Electron ...

## Battery Life Optimization (If you are on a Macbook)
There are 2 options that will improve battery life:
1. TLP - Can be customized to not enable things like Wifi, Bluetooth, etc
2. AutoCPU-Freq - Focuses more on the CPU (has better performance in my case)

### TLP
```
sudo dnf install tlp
```

```
sudo tlp start
```

### AutoCpu-Freq
Link - https://github.com/AdnanHodzic/auto-cpufreq?tab=readme-ov-file#installing-auto-cpufreq

```
git clone https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq && sudo ./auto-cpufreq-installer
```

Run the following code to let auto-cpufreq open on startup
```
sudo auto-cpufreq --install
```

**NOTE: DO NOT RUN BOTH OF THESE AT THE SAME TIME!** 

## Touch pad Optimization
If your touch pad is being funny, use this optimization
https://github.com/tascvh/trackpad-is-too-damn-big

You can run `sudo evtest` to see which event is your touch pad

Run `sudo  ~/trackpad-is-too-damn-big/build/./titdb -d /dev/input/event#` in your terminal to activate it or you can activate it automatically

*Note: Replace # with the correct event number of your touchpad*

## Something Fun for You!

Run this code in your terminal for a surprise
```
bash <(curl -s https://raw.githubusercontent.com/wick3dr0se/matrix/main/matrix)
```