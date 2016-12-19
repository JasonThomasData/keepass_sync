This file is useful for syncing keepass files between Linux and Android. This is a kind of naive
approach to doing it, since it replaces the oldest file with the newest one. This isn't going to work
if you update both files without syncing them.

This uses the Unix resource, stat, to get the time a device was last modified.

On my Motorola Android, my keepass file is: `/storage/emulated/0/keepass/passwords.kdbx`. My
desktop keepass file is in the same folder as this project. I implore you, if you use a password
manager, to make a master passphrase no shorter than 30 characters or more.

###Setup

I run a Linux Mint (Sarah) PC and a Motorola Android, so this worked for me:

Install ADB - `sudo apt-get install adb`

Run lsusb to get the device idVendor and idProduct numbers. Those are the first and second numbers in
a combo that looks like VVVV:PPPP

Take that number and create a file called: `/etc/udev/rules.d/70-android.rules` and make sure this
line is there: `SUBSYSTEM=="usb", ATTR{idVendor}=="VVVV", ATTR{idProduct}=="PPPP", MODE="0666", GROUP="plugdev"`

You also need to put the idVendor number in a file called: `~/.android/adb_usb.ini` like this: `0xVVVV`.

You need to make sure usb debugging is enabled on the device and be sure to allow the RSA fingerprint.

###Troubleshooting

If these things don't work, you can try: a) `sudo service udev restart`, b) deleting the `adbkey` and
`adbkey.pub` files in `~/.android`, c) restart the device and d) make sure the files you've made have
the right permissions.

My Motorola Android will give me usb permission when: usb tethering is turned off and usb debugging
is turned on.
