# wsl_mountusb

A small WSL utility to mount removable USB drives into WSL using `drvfs`.

This tool provides a clean, predictable way to manually mount and unmount Windows‑assigned removable drives inside WSL, without interfering with Windows’ own eject logic.

---

## Features

- Detects removable drives via PowerShell  
- Mounts **all** drives or a **specific drive letter**  
- Supports `--list`, `--umount`, and `--help`  
- Companion command `umountusb` for unmounting  
- Idempotent: avoids double‑mounting  
- Protects against running outside WSL  
- Simple, explicit workflow that avoids Windows eject conflicts  

---

## Installation

Copy the scripts from the `bin/` directory into a location on your PATH, typically `~/.local/bin`, and ensure they are executable:

```bash
cp bin/mountusb ~/.local/bin/
cp bin/umountusb ~/.local/bin/
chmod +x ~/.local/bin/mountusb ~/.local/bin/umountusb
```

---

## Usage

### Mount all removable USB drives
```bash
mountusb
```

### Mount a specific drive
Drive letters may be given as `x`, `X`, `x:`, or `X:`.

```bash
mountusb x
```

### List removable drives and their mount status
```bash
mountusb --list
```
or
```bash
mountusb -ls
```

### Unmount all removable drives
```bash
mountusb --umount
```
or
```bash
umountusb
```

### Unmount a specific drive
```bash
mountusb x --umount
```
or 
```bash
umountusb x
```

### Shortcut command
A companion command is provided:

```bash
umountusb
```

This is equivalent to:

```bash
mountusb --umount
```

---

## Notes

- This utility works **only under WSL**. It will refuse to run on native Linux.  
- Mounts use WSL’s `drvfs` layer and appear as `type 9p` with `aname=drvfs`.  
- Automatic mounting is intentionally avoided to prevent interfering with Windows’ “Safely Remove Hardware” behavior.  

---
