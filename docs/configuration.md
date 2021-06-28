### 2.6. Defining a keyboard layout

If you are using a keyboard layout other than US, then you need to tell Openbox to use this layout. First, you need to create the folder where Openbox looks for the its autostart file in which you’ll define the keyboard layout.

```sh
mkdir ~/.config/openbox
```

Then copy over the default Openbox autostart file to the newly created folder.

```sh
cp /etc/xdg/openbox/autostart ~/.config/openbox/
```

Open the file with the terminal text editor nano.

```sh
nano ~/.config/openbox/autostart
```

Append these lines to the bottom of the file.

```sh
# Set keyboard layout
setxkbmap $KB_LAYOUT
```

Replace $KB_LAYOUT with the language code for your preferred keyboard layout. You can see your installed layouts and languages by issuing the command `less /usr/share/X11/xkb/rules/base.lst`.

Save the file and exit nano by clicking “Ctrl+X” and then “Enter”.

If you need to specify the keyboard model and/or variant, consult the [Arch Wiki’s entry](https://wiki.archlinux.org/index.php/Keyboard_configuration_in_Xorg#Setting_keyboard_layout) on setxkbmap.

### 2.9. Rebooting and applying changes

Reboot the HTPC to apply all the changes that you have made since part 2.1.

```sh
sudo reboot
```

Congratulations, if everything went well, you should now have automatically launched Kodi in the Kodi Openbox session.