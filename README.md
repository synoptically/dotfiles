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

## Build dwm and dwmblocks

Install the build packages under [Required packages](#required-packages) first.

```
cd ~/dwm-6.8 && sudo make clean install
cd ~/Projects/dwmblocks-luke && make && cp dwmblocks ~/.local/bin/
```

Rebuild dwm after changing `config.h`. Restart dwm to load it.

## Set up screens

```
~/.local/bin/gen-screens
```

Puts each screen at its preferred resolution and fastest refresh rate, with the primary screen first. Saves the result as the autorandr `default` profile. Run it again whenever you change monitors.

Each screen gets its preferred resolution and fastest refresh rate.

### One monitor

Run it with no options.

### Two monitors

Run it with no options. If the screens are in the wrong order, pick one with `-p`:

- `-p l2r`: left to right, primary on the left (default)
- `-p r2l`: right to left, primary on the right
- `-p column`: stacked top to bottom, primary on top

Example: `~/.local/bin/gen-screens -p r2l`

### Three or more monitors

Plain `gen-screens` stops here. Place each screen yourself:

1. List the screen names: `~/.local/bin/gen-screens -l`
2. Give one `-m NAME:XxY` per screen. X and Y are the top-left corner in pixels. The first `-m` is the primary screen.

   ```
   ~/.local/bin/gen-screens -m HDMI-A-0:0x0 -m DisplayPort-1:1920x0 -m DisplayPort-2:3840x0
   ```

`-h` shows all options.

## Check

```
~/.local/bin/check-dotfiles
```

`ERROR` means something is broken. `WARN` means an optional tool is missing. Exits 1 on any error.

## Window manager

- [dwm](https://git.suckless.org/dwm): source in `~/dwm-6.8`
- [dwmblocks](https://github.com/LukeSmithxyz/dwmblocks): source in `~/Projects/dwmblocks-luke`

## Required packages

- Build: `gcc`, `make`, and the X11 headers for dwm and dwmblocks (libX11, libXinerama, libXft)
- Screens: `autorandr` (includes `autorandr-launcher`), `xrandr`
- Session: `feh` (wallpaper), `dbus` (`dbus-launch`), a display manager that starts dwm (this setup uses LightDM)
- Bar blocks: `wireplumber` (`wpctl`), `bluez` (`bluetoothctl`), `NetworkManager` (`nmcli`), `dmenu`, `systemd` or `elogind` (`loginctl`), `procps` (`pgrep`)
- Font: JetBrainsMono Nerd Font (bar icons and terminal)

## Optional packages

- `alacritty`: terminal
- `pavucontrol`: opened by a middle click on the volume block
- [genmix](https://github.com/synoptically/genmix): audio mixer, opened by a right click on the volume block (`make install` puts it in `~/.local/bin`)
- `playerctl`: play, pause, next, and previous for media players (used by DWM's keybindings)
- `blueman`: opened by a click on the bluetooth block
- `flatpak` and Sober: `~/.local/bin/sober`
- `xsetroot`: `~/.local/bin/statusbar`
- `neovim`, `btop`, `htop`, `neofetch`, `flameshot`, `vlc`
- `gentoo-pipewire-launcher`: `~/pipewire.sh` (Gentoo only)
