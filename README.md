# Omarchy wallpaper timer

These files configure a systemd user timer that advances the Omarchy wallpaper
every 30 minutes.

## Install

Copy the files into the matching user configuration directory:

```bash
mkdir -p ~/.config/systemd/user
cp .config/systemd/user/omarchy-wallpaper.service ~/.config/systemd/user/
cp .config/systemd/user/omarchy-wallpaper.timer ~/.config/systemd/user/
```

Put wallpapers for the current theme in:

```text
~/.config/omarchy/backgrounds/<theme-slug>/
```

Find the current theme with:

```bash
omarchy theme current
```

Then enable the timer:

```bash
systemctl --user daemon-reload
systemctl --user enable --now omarchy-wallpaper.timer
```

Check its schedule with:

```bash
systemctl --user list-timers omarchy-wallpaper.timer
```

The interval can be changed by editing `OnUnitActiveSec` in
`omarchy-wallpaper.timer`, for example `10min`, `1h`, or `2h`.

Disable the timer with:

```bash
systemctl --user disable --now omarchy-wallpaper.timer
```
