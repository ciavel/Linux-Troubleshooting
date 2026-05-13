# Linux Driver and HDMI Check Commands

Useful Linux commands for checking drivers, GPU/display hardware, HDMI output, HDMI audio, and related system logs.

## Basic System Information

```bash
uname -a
hostnamectl
```

## GPU / Display Driver

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

If `glxinfo` is missing on Fedora:

```bash
sudo dnf install -y mesa-demos
```

If `glxinfo` is missing on Ubuntu/Debian:

```bash
sudo apt install mesa-utils
```

## HDMI / Monitor Detection

Show connected displays, including HDMI, DisplayPort, and built-in displays:

```bash
xrandr --query
```

Common output names:

```text
HDMI-1 connected
HDMI-1 disconnected
DP-1 connected
DP-1 disconnected
eDP-1 connected
```

List detected monitors:

```bash
xrandr --listmonitors
```

For GNOME / Wayland, you can also try:

```bash
gnome-randr query
```

## Kernel Display Logs

Check display, GPU, HDMI, and EDID-related kernel logs:

```bash
sudo dmesg | grep -Ei "drm|hdmi|edid|display|gpu|nvidia|amdgpu|i915"
```

Watch live kernel logs while plugging or unplugging HDMI:

```bash
sudo dmesg -w
```

## HDMI Audio / Sound Devices

List audio output devices:

```bash
pactl list short sinks
```

Show audio cards:

```bash
aplay -l
```

Show detailed audio card information:

```bash
pactl list cards
```

Search specifically for HDMI or DisplayPort audio outputs:

```bash
pactl list cards | grep -Ei "hdmi|displayport|output"
```

Check PipeWire status:

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

Common driver modules:

```text
Intel GPU:    i915
AMD GPU:      amdgpu
Old AMD GPU:  radeon
NVIDIA open:  nouveau
NVIDIA prop:  nvidia
Audio:        snd_hda_intel
```

## USB-C / Thunderbolt Display Checks

List USB devices:

```bash
lsusb
```

List Thunderbolt devices:

```bash
boltctl
```

If `boltctl` is missing on Fedora:

```bash
sudo dnf install -y bolt
```

## Firmware, Boot, and Hardware Errors

Show warnings from the current boot:

```bash
journalctl -b -p warning
```

Search logs for HDMI, display, GPU, and driver messages:

```bash
journalctl -b | grep -Ei "hdmi|drm|edid|display|gpu|nvidia|amdgpu|i915"
```

## Fedora Driver Package Checks

Check installed graphics and driver-related packages:

```bash
dnf list installed | grep -Ei "mesa|nvidia|akmod|xorg-x11-drv|intel|amd|radeon|nouveau"
```

Check available driver-related packages:

```bash
dnf search nvidia
dnf search mesa
dnf search xorg-x11-drv
```

## Quick All-in-One Driver Check

```bash
echo "=== System ==="
uname -a
hostnamectl

echo
echo "=== GPU / Display Driver ==="
lspci -k | grep -EA3 "VGA|3D|Display"

echo
echo "=== Display Outputs ==="
xrandr --query

echo
echo "=== Audio Outputs ==="
pactl list short sinks

echo
echo "=== Audio Cards ==="
aplay -l

echo
echo "=== Loaded GPU / Audio Modules ==="
lsmod | grep -Ei "i915|amdgpu|radeon|nouveau|nvidia|snd_hda_intel"

echo
echo "=== HDMI / Display Logs ==="
journalctl -b | grep -Ei "hdmi|drm|edid|display|gpu|nvidia|amdgpu|i915" | tail -80
```

## Notes

If HDMI is not detected, try these steps:

1. Replug the HDMI cable.
2. Test another HDMI cable or monitor.
3. Check whether the port appears in `xrandr --query`.
4. Watch live logs with `sudo dmesg -w` while plugging in HDMI.
5. Check whether the correct GPU driver is loaded with `lspci -k`.
6. Log out and back in, or reboot after driver/theme/display changes.
