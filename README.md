OVERVIEW
========

This repository contains **wmaker** pkgsrc collection: build scripts
and files for Window Maker & dockapps packages.

Packages in this collection must depend only on **desktop**, **xorg**,
**system** and **core** pkgsrc collections.


SETUP
=====

Build and install `pkgsrc-wmaker` packages:

```sh
sudo pkgman install --deps --group wmaker wmaker-dockapps wmaker-themes
```

Prepare your `.xinitrc` file.  You can use the following skeleton:

```sh
#!/bin/sh -ex
#
# ~/.xinitrc: xinit(1) startup configuration
#

# Merge the X server resources and keymaps.
# These files contain configuration for X applications and keyboard
# mappings.
userresources=$HOME/.Xresources
usermodmap=$HOME/.Xmodmap
sysresources=/etc/X11/xinit/.Xresources
sysmodmap=/etc/X11/xinit/.Xmodmap
[ -f $sysresources  ] && xrdb -merge $sysresources
[ -f $sysmodmap     ] && xmodmap $sysmodmap
[ -f $userresources ] && xrdb -merge $userresources
[ -f $usermodmap    ] && xmodmap $usermodmap

# Start programs shipped with X11.
# This loop executes any shell scripts found in
# /etc/X11/xinit/xinitrc.d.
if [ -d /etc/X11/xinit/xinitrc.d ]; then
    for f in /etc/X11/xinit/xinitrc.d/?*.sh; do
        [ -x "$f" ] && . "$f"
    done
    unset f
fi

# Set keyboard layout.
# Configures English and Romanian layouts, with Caps Lock as a group
# toggle, and right-hand Windows key as Compose.  Adjust as needed.
setxkbmap en,ro -option grp_led:caps,grp:caps_toggle,compose:rwin &

# Desktop applications autostarter.
# `dapper` helps manage autostarting applications.  To install, run
# the following command:  `pkgman install --deps --group dapper`
dapper --user-dir --system-dirs &

# Start automatic screen locker unless it's already started.
# `xautolock` automatically locks your screen, using `slock` as the
# locker.
if ! pgrep -u $(whoami) xautolock >/dev/null 2>&1; then
    xautolock -locker slock
fi &

# Custom key bindings.
# `xbindkeys` allows you to define custom keyboard shortcuts.
if ! pgrep -u $(whoami) xbindkeys >/dev/null 2>&1; then
    xbindkeys
fi

# Start Window Maker.
# This is the final command that launches the Window Maker session.
exec wmaker

# Optional: Per-machine setups using WMAKER_USER_ROOT for custom path
# for configuration files and use logging.
#export WMAKER_USER_ROOT=~/GNUstep-$(whoami).$(hostname)
#exec wmaker > $WMAKER_USER_ROOT/wmaker.log 2>&1
```

Adjust conform your needs, and `startx`.


REFERENCES
==========

* [Window Maker: User Guide](https://www.windowmaker.org/docs/guide_toc.html)
* [Window Maker: FAQ](https://www.windowmaker.org/docs/FAQ.html)


LICENSE
=======

`pkgsrc-wmaker` is licensed through the GNU General Public License v3
or later <http://gnu.org/licenses/gpl.html>.
Read the COPYING file for copying conditions.
Read the COPYRIGHT file for copyright notices.
