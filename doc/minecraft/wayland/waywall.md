# waywall

- **waywall** is a Wayland compositor designed to run inside your existing Wayland session. It provides various convenient features for speedrunning, including but not limited to:
  - Window resizing
  - Key remapping
  - Ninjabrain Bot support
  - Mirrors (i.e. magnifiers for eye measuring, F3, etc.) without using OBS
  - Lots of custom functionality.
- If you're using **X11**, please use [resetti](../x11/resetti.html) instead.

## Installation 

- You can install waywall on most Linux distributions via three methods. Choose the one matching your preference:
  - **Built-in script (Recommended):** Officially maintained, one-click installer for Arch/Fedora/Debian derivatives, no manual GLFW patch/compile needed.
  - **Manual install:** Officially maintained, compile from source and patch GLFW as required.
  - **Package manager:** Third-party packages (one-click) but you still may need to patch GLFW.


## Built-in Script Install
- Distributions derived from Fedora (rpm), Debian/Ubuntu (dpkg/apt), and Arch Linux (pacman) are supported. Other distributions that support one of these package managers may work but are not officially supported. [Linux distribution families](https://en.wikipedia.org/wiki/List_of_Linux_distributions#Official_derivatives).

- To install waywall using the built-in script you need to follow the steps under "Building from build-packages.sh" on the [README.md](https://github.com/tesselslate/waywall/blob/main/README.md) file from the waywall repository.

## Manual Install

### Fedora-based
```bash
sudo dnf install libspng-devel cmake meson mesa-libEGL-devel luajit-devel libwayland-client libwayland-server libwayland-cursor libxkbcommon-devel xorg-x11-server-Xwayland-devel wayland-protocols-devel wayland-scanner
```
### Debian-based
```bash
apt update && sudo apt install libgles2-mesa-dev libegl-dev pkg-config debhelper-compat wayland-protocols meson build-essential libspng-dev libluajit-5.1-dev libwayland-dev libxkbcommon-dev xwayland cmake wayland-scanner++ libegl1 luajit libspng0 libwayland-client0 libwayland-cursor0 libwayland-egl1 libwayland-server0 libxcb1 libxcb-composite0-dev libxcb-res0-dev libxcb-xtest0-dev libxkbcommon0 curl git
```
##### Debian features an old version of libxcb, to get around this we need to patch waywall (Do this inside the waywall folder):
```bash
curl -o mod.patch https://files.catbox.moe/my3adv.patch
git apply mod.patch
```
### Arch Linux-based
```bash
sudo pacman -S --noconfirm ninja meson wayland-protocols libegl libgles luajit libspng libxcb libxkbcommon xorg-xwayland
```

- Then, run the commands on this page of the [waywall documentation](https://tesselslate.github.io/waywall/00_installation.html#compiling).

- Users on Debian-based distros may have trouble building waywall manually. If you're having trouble, join the [Linux MCSR Discord server](https://discord.gg/fwZA2VJh7k).

- Run `waywall` in a terminal to check it's installed properly.
  - Use the absolute path to the waywall executable if this doesn't work (i.e. if you built waywall in `/home/username/waywall/build/waywall`, run `/home/username/waywall/build/waywall/waywall`).
  - The wrapper command for your instance in the next step should also use this path instead of `waywall`.
 
#### Manual installs require the GLFW patch described in the Post-Install section.

## Package Manager Install
- On Arch Linux, [you can install waywall through the AUR](https://aur.archlinux.org/packages/waywall-working-git).
- On NixOS, [you can install waywall through its package manager](https://search.nixos.org/packages?channel=25.11&show=waywall&query=waywall)

#### Package manager installs may still require the GLFW patch described in the Post-Install section.

## Post-Install
- If you used either **Manual Install** or **Package Manager Install** (without patched GLFW), you need to visit the [next page of the documentation](https://tesselslate.github.io/waywall/00_setup.html) to patch GLFW. You also need it to set up your instance to launch within waywall.

- After this, move to the [next section](waywall_config.html) to install an example config and learn how to customize it to your liking.

## Troubleshooting

- On dual-GPU setups (i.e. laptops with integrated and dedicated graphics), waywall may not display mirrors correctly, specifically if the desired GPU is an NVIDIA one.
  - To fix this:
    - Fedora users should check `akmod-nvidia` is installed.
    - Arch users should check `nvidia-prime` is installed.
  - Then, modify your wrapper command in your instance's settings in Prism like so:

    ```bash
    sh -c "waywall wrap -- prime-run $INST_JAVA \"$@\""
    ```

  - Remember to replace `waywall` with the absolute path if you must.
