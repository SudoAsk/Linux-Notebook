Installing slackware 14.1 on my laptop
======================================

Selecting the packages to install
---------------------------------
Select the following packages:

    A  - Base Linux System
         Everything

    AP - Various Applications that do not need X
         alsa-utils
         ghostscript
         groff
         man
         man-pages

    F -  FAQ lists,  HOWTO documentation
         Everything

    L -  System Libraries (Needed by KDE, GNOME, X, and more)
         alsa-lib
         alsa-oss
         dbus-glib
         dbus-python
         glib2
         libffi
         libnl3
         pygobject
         urwid

    N -  Networking (TCP/IP, UUCP, Mail, News)
         dhcpcd
         iputils
         net-toolsdf
         network-scripts
         wireless-tools
         wpa-supplicant

Booting straight to slackware
-----------------------------
Run the following commands:

    # vi /etc/lilo.conf

Perform the following edits:

- Comment the section named Boot BMP Image
- Uncomment the section named Standard menu

Perform the following edits:

    append="logo.nologo vt.default_uft8=1"
    compact
    # prompt
    vga=791

Run the following commands:

    # lilo

Mounting the DVD drive
----------------------
Run the following commands:

    # vi /etc/fstab

Perform the following edits:

- Uncomment the line starting with /dev/cdrom

Then run the following commands to mount a DVD:

    # su root
    # mount /dev/cdrom
    # exit

    # cd /mnt/cdrom

Connecting to a network
-----------------------
Run the following commands:

    # vi /etc/rc.d/rc.inet1.conf

Perform the following edits:

    IPADDR[0]=""
    NETMASK[0]=""
    USE_DHCP[0]=""
    DHCP_HOSTNAME[0]=""
    GATEWAY[0]=""

Run the following commands:

    # installpkg /mnt/cdrom/extra/wicd/wicd-1.7.2.4-x86_64-4.txz

Run the following commands to disable automatic networking:

    # chmod -x /etc/rc.d/rc.wicd

Then run the following commands to connect to a network:

    # su root
    # wicd
    # wicd-curses
    # exit

Displaying UTF-8 characters
---------------------------
Run the following commands:

    # vi /etc/profile.d/lang.sh

Perform the following edits:

    # export LANG=en_US
    export LANG=en_US.UTF-8

Run the following commands:

    # installpkg /mnt/cdrom/slackware64/ap/terminus-font-4.38-noarch-1.txz

Run the following commands:

    # echo "setfont ter-v18n" >> ~/.bash_profile

Connecting a printer
--------------------
Get information about the printer:

- Browse to www.openprinting.org
- Find the printer model in the database
- Download and install the recommended driver if applicable
- Download the printer PPD file if applicable

Alternatively:

- Browse to the manufacturer web site
- Download and install the printer driver

Run the following commands to launch the printing daemon:

    # cupsd

Perform the following actions:

- Browse to localhost:631
- Click on Administration / Add printer then select the printer
- Give the printer a friendly name, let's say Samsung
- Select the printer model if applicable
- Select the PPD file if applicable

Run the following commands to set the deault printer:

    # lpadmin -d Samsung

Then run the following commands to print a document:

    # su root
    # cupsd
    # exit

    # lp document.txt

Making noises
-------------
Run the following commands:

    # su root
    # alsactl init
    # alsamixer

Perform the following actions:

- Adjust the default volume levels
- Beware that the value MM indicates a muted channel
- Type the m key to toggle muting

Run the following commands:

    # alsactl store
    # exit

Then run the following commands to play music:

    # aplay music.wav

And optionally run the following commands to adjust volume:

    # alsamixer
