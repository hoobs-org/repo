For this tutorial we are using the [server edition](https://getfedora.org/en/server/download/) of Fedora 30.

> Notes about this documentation. Commands you need to run in the terminal are prefixed with `~]$`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

## Initial Setup

**Updating**  
It is a good idea to update Fedora, even if you just installed. The Fedora community is very active.

```bash
~]$ sudo yum update
```

**Setting the Hostname**  
To make things easier you need to set the hostname. We are using `hoobs` for this tutorial, but you can choose what ever you would like.

```bash
~]$ sudo hostnamectl set-hostname hoobs
```

Install Avahi

```bash
~]$ sudo yum install -y nss-mdns avahi
```

Enable Avahi

```bash
~]$ sudo systemctl enable avahi-daemon.service
```

Now reboot.

```bash
~]$ sudo reboot
```

## Sudo
If you do not want to enter your password in the command line, you can setup sudo to not prompt for a password.

Nano comes shipped with Fedora. You will need to edit your sudoers file.

```bash
~]$ sudo nano /etc/sudoers
```

By default your admin account is part of the wheel group. This is the entry you need to change.

Look for this line in the file.

`
%wheel	ALL=(ALL)	ALL
`

And change it to this.

`
%wheel	ALL=(ALL)	NOPASSWD: ALL
`

To exit nano, press `ctrl+x`, then `y` and then `enter` to save.

Now you can start HOOBS without a password.

> Note: If you choose to use sudo without a password, we advise you to always log out of all terminals and exit all ssh sessions if you are not around. You don't want to give your roommate, sibling or significant other full root access to your server.

## Installing HOOBS
Now we are ready to install HOOBS.

```bash
~]$ wget -q -O - http://bit.ly/get-hoobs | sudo bash -
```

The HOOBS install script will set everything up for you. Once HOOBS is installed, your device will automatically reboot.


## Accessing the Interface
Once you have HOOBS installed and started, you can access the interface from [http://hoobs.local](http://hoobs.local).
