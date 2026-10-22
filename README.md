# gparted-launch 

[![Release](https://img.shields.io/gitea/v/release/linux-bird/gparted-launch?gitea_url=https://codeberg.org)](https://codeberg.org/linux-bird/gparted-launch/releases/latest)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

A lightweight GParted wrapper for Linux. (en, pl, es, nl)

<img src="https://github.com/user-attachments/assets/a4a6e940-b7f0-42c3-9079-a5f1d24c9df8" width="500" />

  <img src="https://github.com/user-attachments/assets/761cdef6-b8a6-42d6-a3db-4861074a0886" width="500" />

Inspired by the original `gparted_shell` from Puppy Linux, rewritten for modern Linux systems using `yad` and `lsblk` instead of `gtkdialog` and `probedisk`.

## Why this wrapper

GParted launched directly will scan **all** connected drives at startup. On systems with multiple disks or USB devices this causes a slow and unnecessary probe. This wrapper lets you pick exactly the drive you want before GParted opens — making it faster to start and safer to use, since there is no risk of accidentally operating on the wrong device.

One drive, one window, one purpose.

## Dependencies

| Package | Purpose |
|---|---|
| `gparted` | The partition editor |
| `yad` | GTK dialog for drive selection |
| `lsblk` | Drive detection (part of `util-linux`) |
| `xhost` | **Wayland only** — lets the root GParted reach the display (`xorg-xhost`) |

> **How privilege escalation works:** the launcher runs `gparted` as your normal user
> and lets GParted's own launcher (`/usr/bin/gparted`) handle the rest — it raises the
> polkit password prompt via `pkexec`, and on a Wayland session it temporarily grants the
> root user access to the X server (`xhost +SI:localuser:root`, revoked on exit) so GParted
> can display through XWayland. Install `xorg-xhost` for the Wayland case. On X11 nothing
> extra is needed.

### Installation

**Debian / Ubuntu:** a `.deb` is published up to [v1.1.2](https://codeberg.org/linux-bird/gparted-launch/releases/tag/v1.1.2). Newer versions are not packaged.
```bash
sudo apt install ./gparted-launch_*.deb
```
To build one from a newer checkout, set the version in `debian/changelog`, then run from the repo root:
```bash
sudo apt install build-essential debhelper dpkg-dev
dpkg-buildpackage -us -uc -b
sudo apt install ../gparted-launch_*.deb
```

**Manual install (any distro):**

1. Make the script executable and install it to a directory in your `$PATH`:
   ```bash
   chmod +x gparted-launch
   cp gparted-launch ~/.local/bin/
   ```
   *(Replace `~/.local/bin/` with your preferred location, e.g., `~/bin/` if it exists or `/usr/local/bin/`.)*

2. **(Optional) Install the desktop shortcut:**
   - Edit `gparted-launch.desktop` and update the `Exec=` line to match the path where you installed `gparted-launch`.
   - Copy the file to your applications directory:
     ```bash
     cp gparted-launch.desktop ~/.local/share/applications/
     ```

## Usage

Run from terminal or launch via menu:
```bash
gparted-launch
```

- A dialog lists all detected drives with name, type, size and model. 
- Select one and click **Launch**. 
- GParted opens directly on that device. 
- To work on a different drive, close GParted and run the launcher again.

## License

MIT
