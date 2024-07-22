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

### Set up permissions  
Add user to the input group  
Important: After executing this command, log out and log back in for the changes to take effect.  
```sh
sudo usermod -aG input $USER
```  
Create udev rules and reload the udev rules
```sh
echo 'KERNEL=="uinput", GROUP="input", TAG+="uaccess"' | sudo tee /etc/udev/rules.d/99-input.rules
sudo udevadm control --reload-rules
sudo udevadm trigger
reboot
```

### Install GNOME Shell Extension for xremap (for GNOME users)  
If you're using GNOME, you need to install the xremap GNOME Shell extension:
  
Visit https://extensions.gnome.org/extension/5060/xremap/  
Click on the toggle switch to install the extension.  
If prompted, allow the browser to install GNOME Shell extensions.  
After installation, the toggle should turn blue, indicating that the extension is active.  
  
  
Note: You may need to restart GNOME Shell (Alt+F2, then type 'r' and press Enter) or log out and log back in for the changes to take effect.  
  
### Create a file named `xremap.service` in the ~/.config/systemd/user/` with the content:
```
[Unit]
Description=xremap service

[Service]
Type=simple
ExecStartPre=/bin/sleep 10
ExecStart=~/.cargo/bin/xremap ~/.config/xremap/config.yml
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
