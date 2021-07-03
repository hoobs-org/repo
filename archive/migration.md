It is highly recommended to backup your Homebridge config files.

HOOBS will automatically upgrade any version of HOOBS or Homebridge. It does have a different file structure so it is highly recommended to backup your Homebridge config files.

> Notes about this documentation. Commands you need to run in the terminal are prefixed with `~]$`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

## Backup
First things first. Backup your current config files. These can be found in `~/.homebridge`. Backup all files in this folder, including.

* persist/ folder
* accessories/ folder
* config.json
* auth.json

## Installing HOOBS
Now we are ready to install HOOBS.

```bash
~]$ wget -q -O - http://bit.ly/get-hoobs | sudo bash -
```

This script will setup NGINX and register HOOBS as a service. This will automatically reboot your device once it finishes.

HOOBS will initialize, and it will migrate all of your plugins and configuration. Apple Home will automatically reconnect.

## Next Steps
Congratulations you have upgraded HOOBS. Now let us walk you through the [User Interface](5e763b3ee87d1e02b6c19d2a).
