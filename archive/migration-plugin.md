It is highly recommended to backup your Homebridge config files.

If you have a previous version of HOOBS or you have the homebridge-config-ui-x plugin installed you can use this method to upgrade. If you have a different setup, please follow the instructions in the [Upgrading Manually](5e764226e87d1e02b6c19d3b) section.

## Installing the Migration Utility 
We have created a Homebridge plugin that starts the upgrade process.

1. From the interface navigate to the Plugins section.

2. Search for **homebridge-to-hoobs** and click the **Install** button.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/ui-upgrade/install-plugin.png)

3. This will start the plugin install. (Installation can take several minutes - be patient)

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/ui-upgrade/plugin-installing.png)

4. Once the plugin finishes. You will see the message **Please Refresh Your Browser**.

> Known Issues: Upgrading also upgrades Node. If your current Node version is less then the required version of HOOBS, the install may fail. If it does, just repeat these steps.

## The Reboot Process
Rebooting the server can take a several minutes. You might see a screen like this while the server reboots.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/ui-upgrade/rebooting.png)

This screen will automatically refresh, and the screen will look like this while HOOBS initializes.

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/hoobs-box/loader.png)

The initialization process may take up to 10 minutes, or longer depending on how many plugins you have installed. Once it finishes, you will see the login screen.

Your users and passwords are automatically migrated over along with all of your plugins and configuration.


