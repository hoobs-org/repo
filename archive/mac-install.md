For this tutorial we are using macOS Catalina.

> Notes about this documentation. Commands you need to run in the terminal are prefixed with `~%`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

## Initial Setup

**Setting the Hostname**  
To make things easier you need to set the hostname. We are using `hoobs.local` for this tutorial, but you can choose what ever you would like.

1. From the Apple menu click **System Preferences...**.

2. Click on the **Sharing** icon.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/mac-install/sharing-settings.png)

3. To the right of the Computer Name field, click on the **Edit...** button.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/mac-install/hostname.png)

4. Set the **Local Hostname** to `hoobs`.

5. Click **OK**.

6. Close **System Preferences**.

7. Reboot.

## Prerequisites
XCode is required by some plugins and HOOBS. You will need to install XCode from the Apple App Store.

After XCode installs. You will need to start XCode. When XCode starts it will ask you to install additional componets. You will need to install this.

After the XCode Command Line Tools install you will need to configure the system to use it.

Open the terminal and run this command.

```bash
~% sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```

Now verify that the Command Line Tools installed corectly.

```bash
~% xcodebuild -version
```

The output should look something like this.

```
Xcode 11.1
Build version 11A1027
```

Node.js and NPM are required to run HOOBS and Homebridge

Download the LTS version of Node.js. As of this writing the LTS version is `12.13.1`.  
[https://nodejs.org](https://nodejs.org)

Follow the onscreen instructions.

## Installing HOOBS
Now we are ready to install HOOBS.

Open the **Terminal** and run the following command.

```bash
~% sudo npm install -g --unsafe-perm @hoobs/hoobs
```

> Note: You must use the `--unsafe-perm` flag. This is because HOOBS needs to run post install scripts as root.

## Starting HOOBS
Now you are ready to start HOOBS for the first time.

Open the **Terminal** and run the following command. Replace `password for current user` with your password.

```bash
~% hoobs -p 'password for current user'
```

> Note: HOOBS uses sudo commands to manage NPM's cache, rebooting and upgrading.

## Sudo
If you do not want to enter your password in the command line, you can setup sudo to not prompt for a password.

Open the **Terminal** and run the following command.

Nano comes shipped with macOS. You will need to edit your sudoers file.

```bash
~% sudo nano /etc/sudoers
```

By default your admin account is part of the wheel group. This is the entry you need to change.

Look for this line in the file.

`
%admin		ALL = (ALL) ALL
`

And change it to this.

`
%admin		ALL = (ALL) NOPASSWD: ALL
`

To exit nano, press `ctrl+x`, then `y` and then `enter` to save.

Now you can start HOOBS without a password.

```bash
~% hoobs
```

> Note: If you choose to use sudo without a password, we advise you to always log out of all terminals and exit all ssh sessions if you are not around.

## Accessing the Interface
Once you have HOOBS installed and started, you can access the interface from [http://hoobs.local:8080](http://hoobs.local:8080).
