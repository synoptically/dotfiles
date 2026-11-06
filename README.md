# dotfiles

Shell startup files, dwm and dwmblocks sources, and config for the apps I use. Everything else in `~` is ignored.

## Clone

Run in `~`. Files with the same names are overwritten, so back up first.

```
cd ~
git init -q
git remote add origin https://github.com/synoptically/dotfiles.git
git fetch -q
git checkout -f -B main origin/main
```

## Check

```
~/.local/bin/check-dotfiles
```

Prints `ERROR` for a broken setup and `WARN` for missing optional tools. Exits 1 on any error.
