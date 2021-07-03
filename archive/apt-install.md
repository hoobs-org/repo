For this tutorial we are using [Debian 10](https://www.debian.org/distrib/).

> Notes about this documentation. Commands you need to run in the terminal are prefixed with a `$`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

## Initial Setup
Debian by default doesn't ship with sudo. We will need to set it up to continue. While we are at it, it's a good idea to upgrade the system.

Access root.

```bash
$ su
```

Next let's install Sudo and Avahi.

```bash
$ apt-get update && apt-get install -y sudo avahi-daemon
```

Now you will need to add the admin account to the sudo group. We setup our admin account as `hoobs`.

```bash
$ /usr/sbin/usermod -a -G sudo hoobs
```

**Setting the Hostname**  
To make things easier you need to set the hostname. We are using `hoobs` for this tutorial.

> Note. Setting the hostname is usually done during install. We are including this in this tutorial, in case you need to change it.

Edit the `hostname` file.

```bash
$ nano /etc/hostname
```

The hostname file is a single line with the hostname. Change it to `hoobs` or any name you would like.

> To save changes from nano, press `ctrl+x`, then `y` and then `enter`.

Now that you have the hostname set you need to reboot for the changes to take effect.

```bash
$ reboot
```


## Sudo
If you do not want to enter your password in the command line, you can setup sudo to not prompt for a password.

You will need to edit your sudoers file.

```bash
$ sudo nano /etc/sudoers
```

Look for this line in the file.

`%sudo ALL=(ALL:ALL) ALL`

And change it to this.

`%sudo ALL=(ALL:ALL) NOPASSWD: ALL`

To exit nano, press `ctrl+x`, the `y` and then `enter` to save.

Now you can start HOOBS without a password.

> Note: If you choose to use sudo without a password, we advise you to always log out of all terminals and exit all ssh sessions if you are not around.


## Installing HOOBS
Now we are ready to install HOOBS.

```bash
$ wget -q -O - http://bit.ly/get-hoobs | sudo bash -
```

The HOOBS install script will set everything up for you. Once HOOBS is installed, your device will automatically reboot.


## Accessing the Interface
Once you have HOOBS installed and started, you can access the interface from [http://hoobs.local](http://hoobs.local).


Congratulations you have completely configured HOOBS, complete with remote access.
