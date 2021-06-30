HOOBS has a set of command line options that control the way HOOBS runs. You can view more about the HOOBS command by using `hoobs --help`.

> Notes about this documentation. Commands impacting the HOOBS Service must be ran via SSH. The HOOBS UI terminal cannot run without the HOOBS service running. Commands you need to run in the terminal are prefixed with `~]$`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

### Elevated Permissions
If you do not want to setup sudo with the NOPASSWD option, you need to run HOOBS with the **-p** or **--pass** flag. This allows you to set the password used for the sudo command.

```bash
~]$ hoobs -p 'My Password'
```

This allows HOOBS to control the system via the user interface.


### Debug Mode
Debug mode dumps more messages to the log. This is helpful when developing plugins or troubleshooting a problem.

To enable debug mode use the **-d** or **--debug** flag.

```bash
~]$ hoobs -d
```


### Modes
HOOBS can be ran in different modes.

* server
* client

If you don't set a mode, HOOBS will run both the server and client.

If you are not running instances, you should run HOOBS in the default mode.

```bash
~]$ hoobs
```


### Service Control
HOOBS has service control build in.

* Start - `sudo hoobs service start` Starts the hoobs.service
* Stop - `sudo hoobs service stop` Stops the hoobs.service
* Restart - `sudo hoobs service restart` Restarts the hoobs.service
* Log - `sudo hoobs service log` Show the output from the hoobs.service
* Install - `sudo hoobs service install` Creates the hoobs.service


### Running a Cluster Client
When running instances, you will need to run the client somewhere in the same network. This provides the user interface that can access all of your running instances.

```bash
~]$ hoobs client
```

> The HOOBS cluster client can run on the same device as other instances, but it can not run on the same device with a non clustered HOOBS service.

**Automatic Setup**  
HOOBS has made setting up a cluster easy. To setup a cluster client run the following command.

```bash
~]$ sudo hoobs cluster client
```

This will ask you to setup a cluster account. This will be the main administrator account for the client and any instance you create. Then it will create a service for the client and start it.

> Note: You will need the IP address or domain name of the cluster client, to create instances.

**Manual Configuration**  
You will need to tell the client about your instances. The client uses the main `config.json` file located in `~/.hoobs/etc/`.

In the client section, you need to define the **interfaces** variable. This is an array of the URLs for each instance.

The config file should look something like this.

```javascript
{
    "server": {
        "port": 8080,
        "polling_seconds": 2
    },
    "client": {
        "instances": [
            "http://192.168.86.25:52827",
            "http://192.168.86.128:53827"
        ],
        "default_route": "status",
        "inactive_logoff": 30,
        "theme": "hoobs-dark",
        "locale": "en",
        "temp_units": "fahrenheit",
        "country_code": "US",
        "postal_code": 80526
    },
    "bridge": {},
    "description": "",
    "ports": {},
    "plugins": [],
    "interfaces": [],
    "accessories": [],
    "platforms": []
}
```

The **server** section has a **port** field. This is the port the client will run on. It needs to be different then any instance running on the same device.

Notice that there is an **instances** array, in the **client** section. This contains the full URL for each instance, including the port.

Once all of your instances are running and you have the client running. There will be an instance drop-down in the interface next to the service menu. This allows you to switch the instance, and you can configure and control each instance from the same interface.

> Note. HOOBS supports instances across multiple devices. This means you can access all of the instances on the same network from one client.


### Running a Cluster Instance
Running a server only mode requires the **-i** or **--instance** flag. This is used to define an instance

```bash
~]$ hoobs server -i 'SmartThings'
```

> For this we are using the name **SmartThings** for the instance. You can replace **SmartThings** with the name you call your instances.

This will run a server with an API labeled SmartThings. When you start a server only instance. A directory will be added in `~/.hoobs/etc/`, with the name of the instance.


**Automatic Setup**  
HOOBS has scripts built in to automatically create and configure cluster instances. To create a cluster instance, run the following command.

```bash
~]$ sudo hoobs cluster create
```

This will ask you a series of questions. Then it will create a service for the instance and start it.

> Note: You will first need to create a cluster client. This will ask you for the cluster account username and password. It will also ask you for the URL of the cluster client. It is best to define the direct port to the client, for example http://hoobs.local:8080. It's also best to ping the client, to see if the device can see it.

**Manual Configuration**  
Each instance gets its own `config.json` file. It is found in the `~/.hoobs/etc/SmartThings` directory.

The `config.json` file will look something like this.

```javascript
{
    "server": {
        "port": 52827,
        "autostart": true,
        "home_setup_id": "X-HM://",
        "client": "http://hoobs.local:8080",
        "polling_seconds": 2
    },
    "client": {},
    "bridge": {
        "name": "HOOBS [SmartThings]",
        "port": 51826,
        "pin": "231-45-154",
        "username": "CD:15:BB:C7:6B:75"
    },
    "description": "",
    "ports": {},
    "plugins": [
        "homebridge-smartthings-tonesto7"
    ],
    "interfaces": [],
    "accessories": [],
    "platforms": [
        {
            "platform": "SmartThings",
            "name": "SmartThings",
            "app_url": "https://",
            "app_id": "",
            "access_token": "",
            "plugin_map": {
                "plugin_name": "homebridge-smartthings-tonesto7"
            }
        }
    ],
    "system": "hoobs"
}
```

Notice the **port** field in the **server** section. This is the port the instance's API runs on. It needs to be different per instance on the same device.

You will also need to change the **port** field in the **bridge** section. This needs to be different per instance on the same device.

> Note. The bridge and the API can not run on the same port as any other bridge and API on the same device. If the API or bridge will not start, check the other instances' port numbers.

If you want to add each instance to HomeKit, you will need to have different bridge names and usernames. It also is a good idea to change the pin code too.

**Cluster Syncing**  
All instances get their authentication from the client. When you add or edit users on the client they are pushed to the instances. Instances will also register with the client, so each instance is aware of the client and the client is aware of all instances that have registered with it.


### Cluster Control
From the HOOBS command you can view and control cluster instance services.

To list the instances on a device, run this command.

```bash
~]$ sudo hoobs cluster
```

To control instance services. For this example, I am using a **SmartThings** instance.
* Start - `sudo hoobs cluster SmartThings start` Starts the hoobs.smartthings.service
* Stop - `sudo hoobs cluster SmartThings stop` Stops the hoobs.smartthings.service
* Restart - `sudo hoobs cluster SmartThings restart` Restarts the hoobs.smartthings.service
* Log - `sudo hoobs cluster SmartThings log` Show the output from the hoobs.smartthings.service


### System Switch
If you upgraded from HOOBS 2.1.1 or Homebridge, HOOBS keeps them around just-in-case. This will only work if your previous install is setup with the homebridge.service on systemd.

To switch from HOOBS to Homebridge.

```bash
~]$ sudo hoobs switch homebridge
```

> Note: The two systems are not in sync. Changes made to either service will not change the other.

To switch from Homebridge to HOOBS

```bash
~]$ sudo hoobs switch hoobs
```

If you want to remove Homebridge to save space.

```bash
~]$ sudo hoobs switch uninstall
```

> Note: This will remove your Homebridge configuration completely, including plugins.
