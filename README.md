# gparted-launch

A lightweight GParted wrapper for Linux.

![Image](https://github.com/user-attachments/assets/8eafc5a4-edde-4431-a380-cca7c2b34a53)

Inspired by the original `gparted_shell` from Puppy Linux, rewritten for modern Linux systems using `yad` and `lsblk` instead of `gtkdialog` and `probedisk`.

## Why this wrapper

GParted launched directly will scan **all** connected drives at startup. On systems with multiple disks or USB devices this causes a slow and unnecessary probe. This wrapper lets you pick exactly the drive you want before GParted opens — making it faster to start and safer to use, since there is no risk of accidentally operating on the wrong device.

One drive, one window, on purpose.

## Dependencies

| Package | Purpose |
|---|---|
| `gparted` | The partition editor |
| `yad` | GTK dialog for drive selection |
| `lsblk` | Drive detection (part of `util-linux`) |

## Installation

```bash
chmod +x gparted-launch
cp gparted-launch /path/to/bin

```

Optionally add the `.desktop` file to your application menu:
```bash
cp gparted-launch.desktop ~/.local/share/applications/
```

## Usage

Run from terminal or launch via menu:
```bash
gparted-launch
```

A dialog lists all detected drives with name, type, size and model. Select one and click **Launch**. GParted opens directly on that device. To work on a different drive, close GParted and run the launcher again.

## License

MIT
