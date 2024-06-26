### Install xremap
```sh
cargo install xremap --features x11     # X11
cargo install xremap --features gnome   # GNOME Wayland
cargo install xremap --features kde     # KDE-Plasma Wayland
cargo install xremap --features wlroots # Sway, Hyprland, etc.
cargo install xremap                    # Others
```

### Clone the configuration repository
```sh
git clone git@github.com:mindils/xremap-config.git ~/.config/xremap
```

### Create a file named `xremap.service` in the ~/.config/systemd/user/` with the content:
```
[Unit]
Description=xremap service

[Service]
Type=simple
ExecStartPre=/bin/sleep 10
ExecStart=/home/leontyevas/.cargo/bin/xremap --watch /home/leontyevas/.config/xremap/config.yml
Restart=always
RestartSec=3

[Install]
WantedBy=graphical.target
```

```sh 
# Enable xremap to autoload on startup
systemctl --user enable xremap.service

# Start the xremap service
systemctl --user start xremap.service

# Restart the xremap service
systemctl --user restart xremap.service

# Stop the xremap service
systemctl --user stop xremap.service
```
