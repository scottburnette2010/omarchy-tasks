# Transfer iPhone files and photos with `ifuse`

Use `ifuse` to mount the accessible parts of an iPhone over USB. This is
primarily useful for importing photos and videos from the camera roll.

## Install

Install the required packages:

```bash
omarchy pkg add ifuse libimobiledevice
```

If Omarchy's package command does not provide them, install them with:

```bash
sudo pacman -S ifuse libimobiledevice
```

## Connect and trust the computer

1. Connect the unlocked iPhone with a USB cable.
2. Unlock the iPhone.
3. Tap **Trust** on the **Trust This Computer?** prompt.
4. Enter the iPhone passcode.

## Pair the iPhone

Check that the phone is detected:

```bash
idevice_id -l
```

Pair it with the computer:

```bash
idevicepair pair
```

A successful result should say:

```text
SUCCESS: Paired with device
```

## Mount the iPhone

Create a mount directory and mount the phone:

```bash
mkdir -p ~/iPhone
ifuse ~/iPhone
```

The mounted files can be browsed in a file manager or from the terminal:

```bash
ls ~/iPhone
```

Photos and videos are typically under:

```text
~/iPhone/DCIM/
```

To copy them into the Pictures folder:

```bash
mkdir -p ~/Pictures/iPhone
cp -a ~/iPhone/DCIM/. ~/Pictures/iPhone/
```

## Unmount safely

Unmount the iPhone before unplugging the USB cable:

```bash
fusermount3 -u ~/iPhone
```

If `fusermount3` is unavailable, try:

```bash
fusermount -u ~/iPhone
```

## Limitations

`ifuse` does not expose the entire iPhone filesystem. It normally provides
access to the camera roll and, when an app identifier is supplied, files
belonging to individual apps. USB access may require the iPhone to remain
unlocked and trusted.
