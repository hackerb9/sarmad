# sarmad
Set external display backlight using builtin brightness keys

Ever plug in an external display and find that the brightness keys on
your laptop don't work with it? This program solves that problem.

Sarmad sets the brightness on *all* displays to follow what is set by
builtin keys and typical tools such as Gnome's brightness slider.  It
does this by reading values set in /sys/class/backlight/*/brightness.
Sarmad then uses xrandr to attempt to set every display's backlight
directly. If that fails (for example, with HDMI connections) it uses
xrandr to adjust brightness in software.

## Installation

It's just a shell script, so just
[download it](https://github.com/hackerb9/sarmad/raw/master/sarmad),
mark it executable, and put it in your path. 
```
wget https://github.com/hackerb9/sarmad/raw/master/sarmad
chmod 755 sarmad
sudo mv sarmad /usr/local/bin/sarmad
```

## Usage

Just run `sarmad` and then hit your brightness keys.

To have it automatically start at login, run it in the background from
`~/.xsessionrc`.

```
echo 'sarmad &'  >> ~/.xsessionrc
```

## Caveats

This only works on machines with a detected backlight, such as
laptops. It reads the current brightness level from the file
`/sys/class/backlight/*/brightness`. 

If you don't have that, then you'll want to use a different tool, such
as binding a keyboard shortcut to run `xbacklight +10` or using
`acpi_listen` to detect brightness up and down key strokes.

The reason I went with this odd, indirect way is so that other
backlight control tools, particularly Gnome's brightness slider, would
work automatically.

## What's with the weird name?

A descriptive name would've been too long, so I named it after
@sarmadka, whose
[script](https://github.com/pop-os/pop/issues/73#issuecomment-381296708)
inspired this one. It's also indirectly named after Sarmad Kashani,
the mystic poet who “once was bathed in the Light of Truth within...”
