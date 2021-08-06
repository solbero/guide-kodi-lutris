## Index

* [1. MinimalCD install of Xubuntu 18.04](#1-minimalcd-install-of-xubuntu-1804)
   * [1.1 Creating a bootable USB flash drive](#11-creating-a-bootable-usb-flash-drive)
   * [1.2 Installation](#12-installation)
* [2. SSH and configuration](#2-ssh-and-configuration)
   * [2.1. Connecting to your HTPC through SSH](#21-connecting-to-your-htpc-through-ssh)
   * [2.2. Creating a user with limited privileges](#22-creating-a-user-with-limited-privileges)
   * [2.3. Adding PPAs and programs](#23-adding-ppas-and-programs)
   * [2.4. Installing a web browser](#24-installing-a-web-browser)
   * [2.5. Creating a Kodi Openbox session](#25-creating-a-kodi-openbox-session)
   * [2.6. Defining a keyboard layout](#26-defining-a-keyboard-layout)
   * [2.7. Setting up auto login](#27-setting-up-auto-login)
   * [2.8. Adding a Kodi splash screen](#28-adding-a-kodi-splash-screen)
   * [2.9. Rebooting and applying changes](#29-rebooting-and-applying-changes)
* [3. Gluing together Kodi and Lutris](#3-gluing-together-kodi-and-lutris)
   * [3.1. Installing the Lutris Kodi add-on](#31-installing-the-lutris-kodi-add-on)
   * [3.2. Configuring Lutris](#32-configuring-lutris)
* [4. Additional information](#4-additional-information)

TOC created with [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)

## 1. MinimalCD install of Xubuntu 18.04

### 1.1 Creating a bootable USB flash drive

I will assume for the rest of this guide that you have an understanding of basic [Linux terminal commands](http://www.comptechdoc.org/os/linux/usersguide/linux_ugbasics.html) and [SSH](https://en.wikipedia.org/wiki/Secure_Shell). If these two concepts are new to you, I would recommend reading these two articles first: [Connecting via SSH to your server](https://mediatemple.net/community/products/dv/204403684/connecting-via-ssh-to-your-server) and [Common SSH commands](https://mediatemple.net/community/products/dv/204643550/common-ssh-commands).

The first thing you will do is to install the minimal Xubuntu 18.04 [ISO](https://en.wikipedia.org/wiki/ISO_image) image on your HTPC. Download the [Ubuntu 18.04 LTS MinimalCD ISO image](https://help.ubuntu.com/community/Installation/MinimalCD) for your architecture (most likely 64-bit if you are using modern hardware). You must download it to another computer than the HTCP you want to install the ISO image to.

To install the ISO image to your HTPC, you need to create a bootable USB flash drive containing the image you just downloaded. There are many programs available which you could use for creating a bootable USB flash drive, but one that is cross-platform and well regarded is [UNetBootIn](https://unetbootin.github.io/). If you have never created and booted from a USB flash drive before you should have a look at the [Ubuntu documentation](https://help.ubuntu.com/community/Installation/FromUSBStick) on how to do this.

Before booting you HTPC from the USB flash drive, make sure that it is connected to the Internet by a wired connection, as the MinimalCD image downloads the packages and programs it needs during installation.

### 1.2 Installation

Installing the MinimalCD image is straight forward, but it looks intimidating since it is not done through a fancy GUI. If you screw up, it is not a problem. Simply turn off your HTPC and start the installation process from the beginning.

Many of the steps shown below are copied and modified from the Kodi Community Forum thread [Automated XBMC minimal installer v0.93 for Ubuntu 12.04 > 14.04](http://forum.kodi.tv/showthread.php?tid=189241&pid=1653111#pid1653111) by Hack_kid which in turn is based on a guide written by bram77.

1. Connect a keyboard and a mouse to your HTPC. Make sure your HTPC is turned off.
2. Take the USB flash drive containing the ISO image you created earlier and insert it into one of your HTPC’s USB slots, then power the HTPC on.
3. In most cases no BIOS adjustments are required and your HTPC will automatically boot from the USB flash drive. If it didn’t, you need to [specify in BIOS](https://www.lifewire.com/how-to-enter-bios-2624481) that you want to boot from the USB flash drive. Most computers also have an option to press a specific key at boot time (usually labeled “Boot order”) which will bring up a dialog where you can select the USB flash drive as your boot option.
4. Unetbootin will display a screen where you can choose different ways to start the MinimalCD installation. Choose “Install” or “Default” on this screen.
5. Choose your preferred installation language, preferably English because that’s the language I’ll be using in this guide. You will be able to choose your preferred language for Kodi in Kodi’s settings later on.
6. Choose the country you reside in (for me it’s “Other” → “Europe” → “Norway”).
7. Choose your preferred [locale](https://en.wikipedia.org/wiki/Locale_\(computer_software\)). Your choice will determine the number format, time format, date format and other minor settings for this installation. I selected “Norway”. The best option for you might be the one that’s pre-selected.
8. In “Configure the keyboard” select “No” and manually choose the keyboard type you want to use (“Norwegian (eliminate dead keys)” in my case)
9. The installer will automatically configure the [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) settings. After this has succeeded, you’ll have a working network connection.
10. Enter the HTPC’s [hostname](https://en.wikipedia.org/wiki/Hostname) (I used “htpc”). Make sure there are no other computers with the same hostname on your [LAN](https://en.wikipedia.org/wiki/Local_area_network). Make a note of the hostname you selected as you’ll need it later on in the guide.
11. Confirm the next two screens with Enter (Ubuntu repositories mirror, default is OK).
12. If you use a proxy server, please enter the proper configuration in the related screen. Otherwise, skip this option by pressing “Enter”.
13. Enter your preferred username for the administrator account (I used “administrator”) and a strong password. This user will from now on be referred to as $ADMIN (whenever you see $ADMIN in this guide, substitute $ADMIN with the username you selected in this step). However, Kodi and all programs associated with it will be run by a user with limited privileges which you’ll create later.
14. In the next screen, the installer will ask you if you want to encrypt the home directory of the user you just created, select “No”. It is very important that you select “No”, because if you select “Yes”, then the automatic login into Kodi won’t work.
15. The installer will now retrieve the necessary packages and programs from a mirror site. Once it’s done, it will prompt you to reformat your hard drive. I assume that you are going to use the whole hard drive, so in this case, select “Guided – use entire disk”. If not, you can select “Manual” and configure the partitioning scheme manually. I won’t go into details on manual partitioning here.
16. When prompted on how you want the security updates to be done, select “Install Security Updates Automatically”.
17. The next screen is an important one. This is where you choose what to install on your HTPC. When prompted to install software packages, select the following from the list: “Minimal Xubuntu minimal installation” and “OpenSSH server”. You have to select packages with “Space”, confirm with “Enter”.
18. The last thing you’ll need to install is the [GRUB boot loader](https://en.wikipedia.org/wiki/GNU_GRUB). Select “Yes” if this is the only OS running on the HTPC. If you have any other OSes on the HTPC, select ”No”.
19. When the installation is complete, you’ll be prompted to remove the USB flash drive from the HTPC and perform a reboot. After the reboot, you should be greeted by a login screen.

## 2. SSH and configuration

### 2.1. Connecting to your HTPC through SSH

To be able to connect over SSH to the HTPC, you will need to use a [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator). In Linux, you can press “Ctrl+Alt+T” to bring up a terminal. In macOS, go to “Applications” → “Utilities” → “Terminal”.

On Linux and macOS, write the command below into the terminal emulator. It is important that you replace $ADMIN and $HOSTNAME in the command below with the administrator username and hostname that you selected during installation.

```sh
ssh $ADMIN@$HOSTNAME
```

You’ll now be prompted to trust the connection, then enter your password. Note that you’ll not see your cursor moving, nor any characters, when typing your password.

If you’re connecting through a computer running Windows, download [PuTTY](http://www.putty.org/) and follow this [guide](https://mediatemple.net/community/products/dv/204404604/using-ssh-in-putty-).

When you have made a successful connection to the HTPC, you should see a terminal prompt looking like the one below. $ADMIN will be replaced by your username and $HOSTNAME with the HTPC’s hostname.

```sh
$ADMIN@$HOSTNAME:~$
```

### 2.2. Creating a user with limited privileges

Kodi and Lutris will be run by a user with limited privileges. The reason for this is security since this user will have no password and will log in automatically. The limited user will have restricted access to the OS (e.g. it will not be able to install programs or change security settings).

To create a limited user account with a disabled password, copy the commands below, one at a time (to paste into a terminal, you have to use “Ctrl+Shift+V”). Remember to replace $USER with the username you’d like for the limited user account (I used “htpc”). From now on, replace $USER in all commands with the username of your limited user account.

```sh
sudo adduser --disabled-password --gecos "" $USER
```

When prompted for a password, enter the $ADMIN password you selected during installation.

With the command below, enable the user account you created in the previous step able to login without a password.

```sh
sudo usermod -a -G nopasswdlogin $USER
```

You also have to assign some privileges to the user account. Remember to replace $USER.

```sh
sudo usermod -a -G cdrom,video,plugdev,users,input,netdev,dialout $USER
```

This command gives the limited user account access to the CD-ROM (cdrom), video devices (video), connected external devices (plugdev), controller and joystick input (input), and connected wireless and Ethernet networks (netdev).

### 2.3. Adding PPAs and programs

The minimal Xubuntu desktop ships with Kodi available in its [repositories](https://en.wikipedia.org/wiki/Software_repository). However, by adding the [Kodi Stable PPA](https://launchpad.net/~team-xbmc/+archive/ubuntu/ppa) it is possible to get the latest stable version.

First, add the PPA with the command below.

```sh
sudo apt-add-repository ppa:team-xbmc/ppa
```

Press “Enter” when prompted.

Lutris is not included in Xubuntu 18.04 by default, therefore you need to add the Lutris PPA to be able to download it. Please note that each line in the code box below must be entered as a separate command.

```sh
ver=$(lsb_release -sr); if [ $ver != "18.04" -a $ver != "17.10" -a $ver != "17.04" -a $ver != "16.04" ]; then ver=18.04; fi

echo "deb http://download.opensuse.org/repositories/home:/strycore/xUbuntu_$ver/ ./" | sudo tee /etc/apt/sources.list.d/lutris.list

wget -q http://download.opensuse.org/repositories/home:/strycore/xUbuntu_$ver/Release.key -O- | sudo apt-key add -
```

To be able to install Steam, you must enable the [Multiverse repository](https://help.ubuntu.com/community/Repositories#Multiverse).

```sh
sudo add-apt-repository multiverse
```

The following command will install Kodi, the Kodi driver for joysticks and gamepads, Lutris, Steam and any dependencies they require.

```sh
sudo apt install kodi kodi-peripheral-joystick lutris steam
```

Press “Y” when prompted.

Also, at this point, it is a good idea to check for any general updates.

```sh
sudo apt full-upgrade
```

### 2.4. Installing a web browser

You should also install a web browser, as it is not included by default with the minimal Xubuntu install. I installed [Midori](https://en.wikipedia.org/wiki/Midori_(web_browser)), which is a lightweight and fast web browser. However, you might prefer Firefox or [Chromium](https://en.wikipedia.org/wiki/Chromium_(web_browser)) (the open source version of Chrome). Only use one of the commands below (you do not need three browsers).

To install Midori:

```sh
sudo apt install midori
```

To install Firefox:

```sh
sudo apt install firefox
```

To install Chromium:

```sh
sudo apt install chromium-browser
```

### 2.5. Creating a Kodi Openbox session

There are several guides on the Internet and on the [Kodi Community Forum](http://forum.kodi.tv/) which explain how to create a separate login session for Kodi to run in. These usually involve a lot of scripting and editing of [init files](https://en.wikipedia.org/wiki/Init). The easiest solution I have found is to download and use [kodi-openbox](https://github.com/lufinkey/kodi-openbox) created by lufinkey. This is a collection of scripts that includes an [Openbox](https://en.wikipedia.org/wiki/Openbox) session that runs Kodi and a script that will launch external programs and manage their windows.

First, install Openbox and its dependencies.

```sh
sudo apt install openbox
```

To install kodi-openbox, download the latest .zip file from the GitHub master branch using the command below.

```sh
cd ~/

wget -O kodi-openbox-master.zip https://github.com/lufinkey/kodi-openbox/archive/master.zip
```

Extract the .zip file.

```sh
unzip kodi-openbox-master.zip
```

If you get a prompt saying that you are missing the package unzip, install it using the command below, then repeat the command above.

```sh
sudo apt install unzip
```

Move into the extracted directory, create a [.deb package](https://en.wikipedia.org/wiki/Deb_\(file_format\)) from the extracted content and then install the .deb.

```sh
cd kodi-openbox-master

./build.sh

sudo dpkg -i kodi-openbox.deb
```

If you get a warning that you have unmet dependencies, enter this command.

```sh
sudo apt -f install
```

Then, remove the files you downloaded and extracted with the following command.

```sh
cd ~/

rm -r kodi-openbox-master kodi-openbox-master.zip
```

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

Save the file and exit nano by pressing “Ctrl+X” and then “Enter”.

If you need to specify the keyboard model and/or variant, consult the [Arch Wiki’s entry](https://wiki.archlinux.org/index.php/Keyboard_configuration_in_Xorg#Setting_keyboard_layout) on setxkbmap.


### 2.7. Setting up auto login

When the HTPC is turned on, the idea is that $USER should be automatically logged in to the Kodi Openbox session. To accomplish this, you need to configure [LightDM](https://en.wikipedia.org/wiki/LightDM), the login manager used by Xubuntu 18.04.

To do so, you need to edit LightDM’s configuration file. The file will be created automatically by the command below if it doesn’t already exist.

```sh
sudo nano /etc/lightdm/lightdm.conf
```

Paste in the following configuration. Make sure that you replace $USER with the limited account’s username.

```sh
[Seat:*]
autologin-user=$USER
autologin-session=kodi-openbox
```

Save the file by pressing “Ctrl+X” and then press “Enter”.

### 2.8. Adding a Kodi splash screen

If you want to get rid of the default Xubuntu splash screen during boot, it is possible to change it to a Kodi one. I have set up a [repository](https://github.com/solbero/plymouth-theme-kodi-animated-logo) containing [Kodibuntu’s](http://kodi.wiki/view/Kodibuntu) animated logo splash screen and adapted it for Ubuntu 16.04 and later versions.

To install the plymouth-theme-kodi-animated-logo, download the latest .zip file from the GitHub master branch using the command below.

```sh
cd ~/

wget -O plymouth-theme-kodi-animated-logo-master.zip https://github.com/solbero/plymouth-theme-kodi-animated-logo/archive/master.zip
```

Extract the .zip file.

```sh
unzip plymouth-theme-kodi-animated-logo-master.zip
```

Move into the extracted directory, create a .deb package from the extracted content and install the .deb.

```sh
cd plymouth-theme-kodi-animated-logo-master

./build.sh

sudo dpkg -i plymouth-theme-kodi-animated-logo.deb
```

Remove the files you downloaded.

```sh
cd ~/

rm -r plymouth-theme-kodi-animated-logo-master plymouth-theme-kodi-animated-logo-master.zip
```

### 2.9. Rebooting and applying changes

Reboot the HTPC to apply all the changes that you have made since part 2.1.

```sh
sudo reboot
```

Congratulations, if everything went well, you should now have automatically launched Kodi in the Kodi Openbox session.

## 3. Gluing together Kodi and Lutris

### 3.1. Installing the Lutris Kodi add-on

In this last section you’ll install the Lutris Kodi Add-on which will display, in Kodi, the games organized by Lutris.

Since you restarted your HTPC at the end of the last section, you will have lost your remote SSH connection. To connect to your HTPC over SSH again, follow the instructions in 2.1.

When you are connected, paste the command below which will change your remote user from $ADMIN to $USER.

```sh
sudo su - $USER
```

The terminal prompt should now look like this.

```sh
$USER@$HOSTNAME:~$
```

Now you need to install the [Lutris Kodi add-on](https://github.com/RobLoach/script.lutris) created by RobLoach. To get the add-on you need to install a third party repository to Kodi.

```sh
cd ~/

wget -O repository.solbero.matrix.zip https://github.com/solbero/repository.solbero.matrix/raw/master/repository.solbero.matrix/repository.solbero.matrix.zip
```

To install the repository you have to allow “Unknown Sources” in Kodi. This is not done through the terminal, but through Kodi. To do so, visit “Settings” → “System” → “Add-ons” and make sure it is enabled.

To install the repository, go to “Settings” → “Add-ons” → “Install from zip file”. Navigate to your Home folder where you should see a file named solbero.repository.matrix.zip.

Navigate back to the add-ons menu and select “Install from repository”. From there, go to “solbero's Kodi add-ons repository” → “Program add-ons” → “Lutris”. Select and install the add-on.

The add-on will be located in Kodi at “Add-ons” → “Program Add-ons” → “Lutris”.

Afterwards, in the terminal, remove the files you downloaded.

```sh
cd ~/

rm repository.solbero-1.0.1.zip
```

To log out of the remote SSH connection, enter this command.

```sh
exit
```

Most Kodi skins, except the default skin, Estuary, support [custom home menu items](http://kodi.wiki/view/Custom_home_items). I have added the Lutris Kodi Addon as a custom home menu item in the skin I’m using. Consult the documentation for the skin you plan on using to see whether this option is available.

### 3.2. Configuring Lutris

Configuration and installation of games in Lutris, Steam and other game providers such as Itch and GOG cannot be done through Kodi. Instead, you need to log into a Xubuntu session. To do so, go to “Power” in the main menu of Kodi and select “Exit” in the dialog. This will log you out of the Kodi and the Kodi Openbox session.

You should now see the LightDM login screen. Before you log in as $USER, you need to select the session you want to log into. In the upper right-hand corner of the login screen there is a session icon you can click which will show you a drop-down list of the available sessions. Click the icon and select “Xubuntu Session”. Then log in as $USER.

![Change session illustration](./images/change_session.png)

To get back to the Kodi Openbox session later you can either restart your HTPC or log out of your current session, select the Kodi Openbox session from the drop-down and log in as $USER.

You should now see a very minimal Xubuntu desktop. The small Xubuntu icon in the upper left-hand corner is the application menu. Click on it, find Lutris and open the program.

I would strongly suggest that you create an account on lutris.net before you add any games to Lutris.

> Like Steam or Desura, Lutris has two parts: a website and a client application, which communicate. On the website, you can browse the supported games, add them to your personal library and start their installation by clicking on the Install link for the version of the game you possess (if someone bothered to make an installer for it). Granted that you have installed the client software, it will open the game installation window, leading you through the steps to finalize the game’s setup. Once it’s done, you will be able to launch the game directly or close the installation window and the game will be present in your local library the next time you start Lutris.

To create an account click on “Lutris” → “Register account” in Lutris. The page [lutris.net/user/register/](https://lutris.net/user/register/) should open up in the web browser you installed earlier. After you have created a Lutris account, you can link your Steam account to it if you like.

> To import your Steam library, go to your Lutris profile and click the “Sign in through Steam” button. You will then be redirected to Steam and will be asked to login. This steps associates your Steam account with your Lutris account. This procedure does not grant Lutris any rights on your Steam account, the only info we get from this is your Steam account identifier. Your Steam account has to be public in order for the library sync to work, if you like it private, you can make it public before the import and switch it back when completed.

After you have created an account, go to “Lutris” → “Connect” to link the client with the website. If you linked your Steam account, all your Steam games should be automatically added to Lutris.

You could also tell Lutris to search for newly installed games from local game sources at startup. To do so, go to “Lutris” → “Import” and switch the toggle next to the game source from “Off” to “On“. At the moment of writing, Steam, Steam for Windows, Desktop Games and ScummVM are supported.

To install games, you can use automatic installer scripts. Go to [lutris.net/games/](https://lutris.net/games/) and search for the game you wish to install. Make sure that you use an installer script written for the store from which you bought the game, or WINE if installing a Windows game in Linux. All games you install with the automatic scripts will be installed to `~/Games/`, except for Steam games which are installed to `~/.steam/`.

If there is no installer script for the game you wish to install, you can add it manually to Lutris. You need to have installed the game beforehand.

> You also have the ability to manually add games to the client, from the “Game” → “Add” menu or from the toolbar button. The Add Game window will let you enter the game’s name, pick the runner [[1\]](https://lutris.net/about/#about-runners) (more runners can be installed from the runners management window, available from “Lutris” → “Manage runners”), browse for the main executable/ROM and enter other necessary details before saving.

When you have installed your games and added them to Lutris, it is time to test everything out. Log out of the Xubuntu session, select the Kodi Openbox session from the drop-down in LightDM and log in as $USER.

Navigate to the Lutris add-on in Kodi and play a game!

## 4. Additional information

This section is not a part of the main guide. I have included it so that those familiar with Linux can get some more information on customizing this HTPC setup. I will mostly provide links to guides and other web pages.

* If your controller is not automatically detected by Kodi, you might have [configure it](http://kodi.wiki/view/HOW-TO:Configure_controllers).
* Gamepads which work out of the box on Linux include, but are not limited to, the Sony DualShock 3, DualShock 4 and Sixaxis; Steam Controller; Microsoft Xbox 360; Logitech F310, F510, F710; and gamepads made by 8Bitdo.
* I’m using [MoltenGamepad](https://github.com/jgeumlek/MoltenGamepad) as an abstraction layer for all my controllers. It makes games agnostic to what controller I’m actually using.
* You can use [AntiMicro](https://github.com/AntiMicro/antimicro) and write custom game launch scripts to make a controller simulate a mouse and keyboard in games which don’t support controllers.
* If you are using Intel or AMD graphics hardware you should install the latest, stable version of [MESA](https://en.wikipedia.org/wiki/Mesa_(computer_graphics)) provided from the [“Ubuntu-X” team PPA](https://launchpad.net/~ubuntu-x-swat/+archive/ubuntu/updates).
* If you are using nVidia hardware, you can install the latest stable and long-lived branches of the nVidia closed source driver from the [Proprietary GPU Drivers PPA](https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa).
* You can [autostart](http://openbox.org/wiki/Help:Autostart) programs and commands when the Kodi Openbox session is launched. You can do this by adding the relevant commands to `/.config/openbox/autostart`. You might have to create the file since it doesn’t exist by default.
* You can also autostart programs and commands when Kodi is started, terminated or killed in the Kodi Openbox session. You can do this by adding the relevant commands to `~/.kodi-openbox/onstart`, `~/.kodi-openbox/onfinish` or `~/.kodi-openbox/onkill`.
* Lutris (v0.4.9) currently supports the following runners: Linux (Native games), Steam, Web, WINE, WINE + Steam, Libretro, DOSBox, MAME, MESS, ScummVM, ResidualVM, Adventure Game Studio, Mednafen, FS-UAE, Vice, Stella, Atari800, Hatari, Virtual Jaguar, Snes9x, Mupen64Plus, Dolphin, PCSX-Reloaded, PCSX2, PPSSPP, Osmose, Reicast, Frotz, jzIntv, O2EM, ZDoom, Citra, DeSmuME, DGen and more.
