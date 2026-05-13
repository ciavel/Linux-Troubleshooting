# Big Sur / WhiteSur Setup For Fedora

This is my Fedora 44 GNOME setup styled like macOS Big Sur using WhiteSur themes, WhiteSur icons, Dash to Dock, Blur My Shell, and other GNOME extensions.

## Installed Themes

| Type | Theme |
|---|---|
| GTK theme | `WhiteSur-Dark` |
| Icon theme | `WhiteSur` |
| Cursor theme | `WhiteSur-cursors` |
| GNOME Shell theme | `WhiteSur-Dark` |

## Enabled GNOME Extensions

```text
blur-my-shell@aunetx
runcat@kolesnikov.se
shotzy@SamkitJain660.github.io
system-monitor@gnome-shell-extensions.gcampax.github.com
apps-menu@gnome-shell-extensions.gcampax.github.com
launch-new-instance@gnome-shell-extensions.gcampax.github.com
drive-menu@gnome-shell-extensions.gcampax.github.com
status-icons@gnome-shell-extensions.gcampax.github.com
dash-to-dock@micxgx.gmail.com
user-theme@gnome-shell-extensions.gcampax.github.com
```

## Installation

### 1. Install required packages

```bash
sudo dnf install -y git gnome-tweaks gnome-extensions-app gnome-browser-connector sassc gtk-murrine-engine gtk2-engines
```

### 2. Install WhiteSur GTK theme

```bash
mkdir -p ~/Downloads
cd ~/Downloads

git clone https://github.com/vinceliuice/WhiteSur-gtk-theme.git
cd WhiteSur-gtk-theme

./install.sh -d ~/.themes
./install.sh -d ~/.themes -s
./install.sh -d ~/.themes -HD
./install.sh -d ~/.themes -s -HD
```

### 3. Install WhiteSur icon theme

```bash
cd ~/Downloads

git clone https://github.com/vinceliuice/WhiteSur-icon-theme.git
cd WhiteSur-icon-theme

./install.sh -d ~/.local/share/icons
```

### 4. Apply WhiteSur theme

```bash
gsettings set org.gnome.desktop.interface gtk-theme 'WhiteSur-Dark'
gsettings set org.gnome.desktop.interface icon-theme 'WhiteSur'
gsettings set org.gnome.desktop.interface cursor-theme 'WhiteSur-cursors'
gsettings set org.gnome.shell.extensions.user-theme name 'WhiteSur-Dark'
```

### 5. Enable GNOME extensions

```bash
gnome-extensions enable blur-my-shell@aunetx
gnome-extensions enable runcat@kolesnikov.se
gnome-extensions enable shotzy@SamkitJain660.github.io
gnome-extensions enable system-monitor@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable apps-menu@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable launch-new-instance@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable drive-menu@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable status-icons@gnome-shell-extensions.gcampax.github.com
gnome-extensions enable dash-to-dock@micxgx.gmail.com
gnome-extensions enable user-theme@gnome-shell-extensions.gcampax.github.com
```

### 6. Make Alt+Tab switch windows instead of applications

```bash
gsettings set org.gnome.desktop.wm.keybindings switch-applications "[]"
gsettings set org.gnome.desktop.wm.keybindings switch-windows "['<Alt>Tab']"
gsettings set org.gnome.desktop.wm.keybindings switch-windows-backward "['<Shift><Alt>Tab']"
```

## Optional Install Script

Save this as:

```text
install-fedora-whitesur.sh
```

```bash
#!/usr/bin/env bash
set -e

echo "Installing required packages..."
sudo dnf install -y git gnome-tweaks gnome-extensions-app gnome-browser-connector sassc gtk-murrine-engine gtk2-engines

mkdir -p ~/Downloads
cd ~/Downloads

echo "Installing WhiteSur GTK theme..."
if [ ! -d "WhiteSur-gtk-theme" ]; then
    git clone https://github.com/vinceliuice/WhiteSur-gtk-theme.git
fi

cd WhiteSur-gtk-theme
git pull || true

./install.sh -d ~/.themes
./install.sh -d ~/.themes -s
./install.sh -d ~/.themes -HD
./install.sh -d ~/.themes -s -HD

cd ~/Downloads

echo "Installing WhiteSur icon theme..."
if [ ! -d "WhiteSur-icon-theme" ]; then
    git clone https://github.com/vinceliuice/WhiteSur-icon-theme.git
fi

cd WhiteSur-icon-theme
git pull || true

./install.sh -d ~/.local/share/icons

echo "Applying WhiteSur theme..."
gsettings set org.gnome.desktop.interface gtk-theme 'WhiteSur-Dark'
gsettings set org.gnome.desktop.interface icon-theme 'WhiteSur'
gsettings set org.gnome.desktop.interface cursor-theme 'WhiteSur-cursors'

echo "Applying GNOME Shell theme..."
gnome-extensions enable user-theme@gnome-shell-extensions.gcampax.github.com || true
gsettings set org.gnome.shell.extensions.user-theme name 'WhiteSur-Dark'

echo "Enabling installed extensions..."
gnome-extensions enable blur-my-shell@aunetx || true
gnome-extensions enable runcat@kolesnikov.se || true
gnome-extensions enable shotzy@SamkitJain660.github.io || true
gnome-extensions enable system-monitor@gnome-shell-extensions.gcampax.github.com || true
gnome-extensions enable apps-menu@gnome-shell-extensions.gcampax.github.com || true
gnome-extensions enable launch-new-instance@gnome-shell-extensions.gcampax.github.com || true
gnome-extensions enable drive-menu@gnome-shell-extensions.gcampax.github.com || true
gnome-extensions enable status-icons@gnome-shell-extensions.gcampax.github.com || true
gnome-extensions enable dash-to-dock@micxgx.gmail.com || true
gnome-extensions enable user-theme@gnome-shell-extensions.gcampax.github.com || true

echo "Optional keyboard behavior..."
gsettings set org.gnome.mutter overlay-key ''
gsettings set org.gnome.desktop.wm.keybindings switch-applications "[]"
gsettings set org.gnome.desktop.wm.keybindings switch-windows "['<Alt>Tab']"
gsettings set org.gnome.desktop.wm.keybindings switch-windows-backward "['<Shift><Alt>Tab']"

echo
echo "Done."
echo "Log out and log back in if the shell theme or extensions do not update immediately."
```

Make it executable:

```bash
chmod +x install-fedora-whitesur.sh
```

Run it:

```bash
./install-fedora-whitesur.sh
```

## Notes

This setup appears to be installed mostly from GitHub theme folders and GNOME Extensions rather than Fedora design packages.

If the shell theme or extensions do not update immediately, log out and log back in.
