HOOBS tries to make configuring as easy as possiable. We have developed an interface that helps seperate the configuration into easy chunks.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/interface.png)

> Note. You can change sections without loosing your changes. You can make all of your changes in one session. When done click the **Save Changes** button to apply those changes to the server.

**Interface**

We start with the **Interface** settings. From here you can control the look and feel of the user interface.

**Bridge Settings**

The bridge settings controls the Homebridge service. This is where you can set the bridge name, username and pin code.

**Port Ranges**

This is part of Homebridge. This section is used to control the range of ports that separate accessories (like a camera or television) should be bound to.

**Plugins**

Each plugin you install will show in the config. We seperate each plugin into it's own section. This helps with keeping everything straight.

Plugins can contain a configuration schema. This is what we use to make the fields. If your favorite plugin doesn't have a configuration schema, add an issue on their GitHub repository and direct them to this document.  
[Developing Plugins](5e764eb6e87d1e02b6c19d4e)

Plugins that have either a **platform.schema.json**, **accessories.schema.json** or a **config.schema.json** file will show like this.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/defined-platform.png)

Or like this.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/defined-accessory.png)

If the plugin does not define their config settings, they will look like this.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/undefined-platform.png)

And if it is an accessory type plugin, without a definition file.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/undefined-accessory.png)

> Note. If a plugin doesn't have a configuration definition file, it doesn't mean the plugin is bad. All it means is the plugin developer hasn't had time to create one, or doesn't know about them.

As you can see we have tried to make configuring as easy as possiable. Even with undefined configuration settings, we seperate each plugin and accessory so you can't screw too much up :)

Also we have included validation in the fields, that will highlight errors for you. It will catch things like a missing comma and other syntax errors.

**Advanced Editor**

The **Advanced** setion allows you to manually configure HOOBS. This is not recommended, but sometimes it is needed.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/advanced.png)

Everything can be configured without this screen. But what is cool is, this updates when you change something in other sections.

For example, you add a garage door opener in the Chamberlain plugin section. After you do that you can look at the **Advanced** section to see what it did.

> Note. The advanced section doesn't include the entire configuration. There are sections that are hidden in the interface. These sections control the server, and require restarting HOOBS. If you ever need to change these settings, it is advised to use SSH.

**Backup**

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/config/backup.png)

This section allows you to download a copy of the configuration and logs. You can also download a complete backup which includes your plugins and accessory cache and layout. Simply click the **System** button. It is recommended to do this before installing plugins or upgrading the system.

> Note. HOOBS backup files (.hbf) are encrypted. This is done to protect any passwords and access tokens you may have in your configuration. It is not recommended to share your backup files for this reason.

**Restore**

HOOBS allows you to restore the system using a HOOBS backup file. To restore click the **Select Backup** button. Then select a backup (.hbf) file. After your system is restored, your device will reboot.

> Warning. This will delete your current configuration.

## Next
[User Accounts](5e764529e87d1e02b6c19d44)
