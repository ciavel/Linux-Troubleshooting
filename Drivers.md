# Linux Driver and HDMI Troubleshooting Commands

This section contains useful Linux commands for checking drivers, graphics hardware, HDMI/display output, audio over HDMI, and related system logs.

## Basic System Info

```bash
uname -a
hostnamectl
```

## GPU and Display Driver

Show graphics hardware:

```bash
lspci | grep -Ei "vga|3d|display"
```

Show graphics hardware with the driver currently in use:

```bash
lspci -k | grep -EA3 "VGA|3D|Display"
```

Show detailed display hardware information:

```bash
sudo lshw -C display
```

Show OpenGL renderer and active graphics stack:

```bash
glxinfo -B
```

If `glxinfo` is not installed on Fedora:

```bash
sudo dnf install -y mesa-demos
```

If `glxinfo` is not installed on Ubuntu or Debian:

```bash
sudo apt install mesa-utils
```

## HDMI and Monitor Detection

Show connected displays, including HDMI, DisplayPort, and laptop display:

```bash
xrandr --query
```

Example output may include:

```text
HDMI-1 connected
HDMI-1 disconnected
DP-1 connected
eDP-1 connected
```

List detected monitors:

```bash
xrandr --listmonitors
```

For GNOME on Wayland, this may also help:

```bash
gnome-randr query
```

## Kernel Display Logs

Show display-related kernel logs:

```bash
sudo dmesg | grep -Ei "drm|hdmi|edid|display|gpu|nvidia|amdgpu|i915"
```

Watch live kernel logs while plugging or unplugging HDMI:

```bash
sudo dmesg -w
```

## HDMI Audio and Sound Devices

List audio output devices:

```bash
pactl list short sinks
```

Show audio cards:

```bash
aplay -l
```

Show detailed audio device information:

```bash
pactl list cards
```

Search for HDMI or DisplayPort audio outputs:

```bash
pactl list cards | grep -Ei "hdmi|displayport|output"
```

Check PipeWire service status:

```bash
systemctl --user status pipewire
systemctl --user status wireplumber
```

## Loaded Driver Modules

Show all loaded kernel modules:

```bash
lsmod
```

Search for common graphics and audio driver modules:

```bash
lsmod | grep -Ei "i915|amdgpu|radeon|nouveau|nvidia|snd_hda_intel"
```

Common Linux driver modules:

```text
Intel graphics:   i915
AMD graphics:     amdgpu
Older AMD/Radeon: radeon
NVIDIA official:  nvidia
NVIDIA open:      nouveau
HDMI audio:       snd_hda_intel
```

## USB-C and Thunderbolt Display Checks

Show USB devices:

```bash
lsusb
```

Show Thunderbolt devices:

```bash
boltctl
```

If `boltctl` is not installed on Fedora:

```bash
sudo dnf install -y bolt
```

## Firmware, Boot, and Hardware Errors

Show boot warnings:

```bash
journalctl -b -p warning
```

Search logs for HDMI, display, and GPU messages:

```bash
journalctl -b | grep -Ei "hdmi|drm|edid|display|gpu|nvidia|amdgpu|i915"
```

## Fedora Driver Package Check

Check installed graphics-related packages on Fedora:

```bash
dnf list installed | grep -Ei "mesa|nvidia|akmod|xorg-x11-drv|intel|amd|radeon|nouveau"
```

## Quick All-in-One Driver Check

Run this command block to quickly check GPU, display outputs, audio outputs, and recent display logs:

```bash
echo "=== GPU ==="
lspci -k | grep -EA3 "VGA|3D|Display"

echo
echo "=== Displays ==="
xrandr --query

echo
echo "=== Audio sinks ==="
pactl list short sinks

echo
echo "=== HDMI / Display logs ==="
journalctl -b | grep -Ei "hdmi|drm|edid|display|gpu|nvidia|amdgpu|i915" | tail -80
```

## Notes

If HDMI is not detected, try plugging the cable in again and then run:

```bash
sudo dmesg -w
```

If the monitor appears but there is no sound, check HDMI audio outputs with:

```bash
pactl list short sinks
pactl list cards | grep -Ei "hdmi|displayport|output"
```

If the GPU driver is not loaded, check:

```bash
lspci -k | grep -EA3 "VGA|3D|Display"
lsmod | grep -Ei "i915|amdgpu|radeon|nouveau|nvidia"
```

## Notes

If HDMI is not detected, try these steps:

1. Replug the HDMI cable.
2. Test another HDMI cable or monitor.
3. Check whether the port appears in `xrandr --query`.
4. Watch live logs with `sudo dmesg -w` while plugging in HDMI.
5. Check whether the correct GPU driver is loaded with `lspci -k`.
6. Log out and back in, or reboot after driver/theme/display changes.
