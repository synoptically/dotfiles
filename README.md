# dotfiles

Shell, X session, dwm, dwmblocks, and app config.

> **Run `~/.local/bin/gen-screens` after cloning.** Screen layouts are per machine, so this repo ships none. Without it, login loads no layout.

## Clone

Run in `~`. Files with the same names are overwritten, so back up first.

```
cd ~
git init -q
git remote add origin https://github.com/synoptically/dotfiles.git
git fetch -q
git checkout -f -B main origin/main
```

## Set up screens

```
~/.local/bin/gen-screens
```

Puts each screen at its preferred resolution and fastest refresh rate, with the primary screen first. Saves the result as the autorandr `default` profile. Run it again whenever you change monitors.

- `-p row`: side by side, left to right (default)
- `-p column`: stacked, top to bottom
- `-h`: show help

## Check

```
~/.local/bin/check-dotfiles
```

`ERROR` means something is broken. `WARN` means an optional tool is missing. Exits 1 on any error.

## Window manager

- [dwm](https://git.suckless.org/dwm) (source in `~/dwm-6.8`): `cd ~/dwm-6.8 && sudo make clean install`
- [dwmblocks](https://github.com/LukeSmithxyz/dwmblocks) (source in `~/Projects/dwmblocks-luke`): `cd ~/Projects/dwmblocks-luke && make && cp dwmblocks ~/.local/bin/`

## Required packages

- Build: `gcc`, `make`, and the X11 headers for dwm and dwmblocks (libX11, libXinerama, libXft)
- Screens: `autorandr` (includes `autorandr-launcher`), `xrandr`
- Session: `feh` (wallpaper), `dbus` (`dbus-launch`), a display manager that starts dwm (this setup uses LightDM)
- Bar blocks: `wireplumber` (`wpctl`), `bluez` (`bluetoothctl`), `NetworkManager` (`nmcli`), `dmenu`, `systemd` or `elogind` (`loginctl`), `procps` (`pgrep`)
- Font: JetBrainsMono Nerd Font (bar icons and terminal)

## Optional packages

- `alacritty`: terminal
- `pavucontrol`: opened by a click on the volume block
- `blueman`: opened by a click on the bluetooth block
- `flatpak` and Sober: `~/.local/bin/sober`
- `xsetroot`: `~/.local/bin/statusbar`
- `neovim`, `btop`, `htop`, `neofetch`, `flameshot`, `vlc`
- `gentoo-pipewire-launcher`: `~/pipewire.sh` (Gentoo only)
