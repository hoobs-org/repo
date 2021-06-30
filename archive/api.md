HOOBS has an API built-in that allows you to monitor, configure and control your device.

> Notes about this documentation. URLs are prefixed with either a `GET`, `POST`, `PUT` or `DELETE` these document what HTTP verb the request accepts. If the request requires a body it will be prefixed with a `Body:`.

## Postman
If you don't already have Postman installed, you can download it here.  
[https://www.getpostman.com/](https://www.getpostman.com/)

For your convenience we have created Postman collections for you.  
[https://github.com/hoobs-org/HOOBS/raw/master/postman.zip](https://github.com/hoobs-org/HOOBS/raw/master/postman.zip)

1. Open the enviornment settings and import the `enviornment.json` file.
2. In the collections panel import each collection JSON file.

## Authentication
This is the main entry point to the API. You can use this to authenticate and recieve an authorization token.

```
POST /api/auth
Body: application/json
```

Request body.
```javascript
{
    "username": "luke_skywalker",
    "password": "MayTheForceBeWithYou"
    "remember": false
}
```

Response
```javascript
{
    "token": "THVrZSBTa3l3YWxrZXI="
}
```

The token will be null if authentication has failed. The token can now be used in the **authroization** header for all other requests to the API.

Determine if an initial user has been created.

```
GET /api/auth
```

Response.
```javascript
{
    "state": -1
}
```

This method doesn't require a token unless the system has a user. If the state is `-1`. The system needs to be initilized. You will need to access the user interface to create the main administrator account.


## Service Information
This fetches basic information about the HOOBS service. Non admin users will recieve limited information.

```
GET /api/status
```

This returns basic information about HOOBS.

```javascript
{
    "bridge_name": "Homebridge",
    "hoobs_version": "0.4.50",
    "username": "CC:22:3D:E3:CE:30",
    "homebridge_port": 51826,
    "home_setup_pin": "031-45-154",
    "home_setup_id": "X-HM://",
    "application_path": ".../hoobs-core",
    "configuration_path": ".../hoobs-core/etc",
    "local_modules_path": ".../hoobs-core/node_modules",
    "global_modules_path": "/usr/local/lib/node_modules",
    "homebridge_path": ".../hoobs-core/node_modules/homebridge"
}
```

To reboot the device.

```
PUT /api/reboot
```

To update the HOOBS software.

```
PUT /api/update
```

Generating a backup.

```
POST /api/backup
```

This returns a status and a filename. You can use this filename to download the backup.

```javascript
{
    success: true,
    filename: "/backup-123456.hbf"
}
```

Restoring.

```
POST /api/restore
```

This is a multipart form endpoint. You need to upload a HOOBS backup file for this to work.

Here is an example using fetch.

```javascript
const field = document.getElementById("file");
const data = new FormData();

// append the file from a file field
data.append("file", field.files[0]);

// post the form data to the server
const response = await fetch("/api/restore", {
    method: "POST",
    body: data,
    headers: {
        "Authorization": token
    }
});

// get the results from the response
const results = await response.json();

if (results.success) {

    // restore complete

}
```

## Service Control
This controls the Homebridge service. Admin users can start, stop and restart the Homebridge service.

```
GET /api/service
```

Returns the current status of the Homebridge service.

```javascript
{
    "version": "0.4.50",
    "running": true,
    "status": "running",
    "time": 1355538
}
```

To change the state of the Homebridge service.

```
POST /api/service/:action [start|stop|restart|clean]
```

> The clean action will remove the /persist folder. This addresses known issues when running Homebridge on a Mac.


## Accessory Control
This API gives you access to monitor and control your accessories attached to HOOBS.

```
GET /api/accessories
```

This fetches your accessories in room layout. If an accessory is not in a room an Unassigned room is added to the layout.

```javascript
{
    "rooms": [
        {
            "name": "Climate",
            "accessories": [
                {
                    "aid": 43,
                    "type": "thermostat",
                    "name": "House",
                    "characteristics": [
                        {
                            "type": "heating_cooling_state",
                            "value": 0,
                        }
                    ],
                    "values": {
                        "heating_cooling_state": 0
                    }
                }
            ]
        },
        {
            "name": "Unassigned",
            "accessories": []
        }
    ],
    "hidden": [
        18,
        23
    ]
}
```

> This example is truncated

To fetch a all accessories without the room layout

```
GET /api/accessories/list
```

To fetch just the room layout

```
GET /api/layout
```

Room layout results.

```javascript
{
    "rooms": [
        {
            "name": "Climate",
            "accessories": [
                43,
                44
            ]
        },
        {
            "name": "Unassigned",
            "accessories": []
        }
    ],
    "hidden": [
        18,
        23
    ]
}
```

> This example is truncated

To update the room layout.

```
POST /api/layout
Body: application/json
```

> The post body is simply the complete modified room layout JSON data.

To fetch a single accessory

```
GET /api/accessory/:id [integer - accessory.aid]
```

To control an accessory.

```
PUT /api/accessory/:id/:service [integer - accessory.aid, integer - characteristic.iid]
Body: application/json
```

Request body.
```javascript
{
    "value": 50
}
```

To update an editable field on an accessory.

```
POST /api/accessory/:id/:service [integer - accessory.aid, integer - characteristic.iid]
Body: application/json
```

Request body.
```javascript
{
    "field": "value"
}
```

Current editable fields.

* alias

To fetch the current dashboard layout.

```
GET /api/layout/dashboard
```

Response
```javascript
[
    {
        "x": 0,
        "y": 0,
        "w": 2,
        "h": 7,
        "i": "0",
        "component": "setup-pin"
    },
    {
        "x": 2,
        "y": 0,
        "w": 10,
        "h": 7,
        "i": "1",
        "component": "system-load"
    },
    {
        "x": 0,
        "y": 7,
        "w": 7,
        "h": 7,
        "i": "2",
        "component": "weather",
        "units": "imperial"
    },
    {
        "x": 0,
        "y": 14,
        "w": 7,
        "h": 8,
        "i": "3",
        "component": "favorite-accessories"
    },
    {
        "x": 7,
        "y": 7,
        "w": 5,
        "h": 15,
        "i": "4",
        "component": "system-info"
    }
]
```

To change the dashboard layout.

```
POST /api/layout/dashboard
Body: application/json
```

> The request body is simply a modified version of the complete dashboard layout JSON.


## Users
Control access to the system. Admin users can add, edit and delete users.

```
GET /api/users
```

This fetches a list of users.

```javascript
[
    {
        "id": 1,
        "name": "Administrator",
        "admin": true,
        "username": "admin"
    },
    {
        "id": 2,
        "name": "Luke Skywalker",
        "admin": false,
        "username": "luke_skywalker"
    }
]
```

To add a user.

```
PUT /api/users
Body: application/json
```

Request body.
```javascript
{
    "name": "Hans Solo",
    "admin": false,
    "username": "hans",
    "password": "MilleniumFalcon"
}
```

Fetch a single user

```
GET /api/user/:id [integer - user.id]
```

To update a user

```
POST /api/user/:id [integer - user.id]
Body: application/json
```

And this deletes a user

```
DELETE /api/user/:id [integer - user.id]
```

## Configuration
Admin users can view and update the main configuration file from this API.

```
GET /api/config
```

This returns the current configuration

```javascript
{
    "bridge": {
        "name": "Homebridge",
        "username": "CC:22:3D:E3:CE:30",
        "port": 51826,
        "pin": "031-45-154"
    },
    "description": "",
    "ports": {},
    "paths": {
        "application": ".../hoobs-core",
        "config": ".../hoobs-core/etc",
        "modules": {
            "local": ".../hoobs-core/node_modules",
            "global": "/usr/local/lib/node_modules"
        },
        "homebridge": ".../hoobs-core/node_modules/homebridge"
    },
    "accessories": [],
    "platforms": []
}
```

To get just the client portion of the config.

```
GET /api/config/client
```

> The client config is available when you are running a client only server.

To save a new configuration.

```
POST /api/config
Body: application/json
```

> The request body is simply a modified version of the config JSON.

To backup your configuration.

```
POST /api/config/backup
```

The backup method simply makes a copy of the current config in the `~/.hoobs/etc/` directory with a timestamp.


## Plugins
This allows admin users to find, install, uninstall and update plugins.

```
GET /api/plugins
```

This lists the current installed plugins.

```javascript
[{
    "name": "wink",
    "scope" "hoobs",
    "version": "2.0.1",
    "details": {
        "type": "platform",
        "path": "@hoobs/wink",
        "alias": "Wink"
    },
    "intalled": "2.0.1",
    "description": "Homebridge plugin for wink.com",
    "links": {
        "npm": "https://www.npmjs.com/package/homebridge-wink-schmittx",
        "homepage": "https://github.com/schmittx/homebridge-wink",
        "repository": "https://github.com/schmittx/homebridge-wink",
        "bugs": "https://github.com/schmittx/homebridge-wink/issues"
    }
}]
```

> This example is truncated

Search available plugins.

```
POST /api/plugins/:query/:limit [integer 1 - 250]
```

Returned search results

```javascript
[{
    "name": "homebridge-nest",
    "version": "2.1.4",
    "installed": false,
    "description": "Nest plugin for homebridge",
    "links": {
        "npm": "https://www.npmjs.com/package/homebridge-nest",
        "homepage": "https://github.com/chrisjshull/homebridge-nest#readme",
        "repository": "https://github.com/chrisjshull/homebridge-nest",
        "bugs": "https://github.com/chrisjshull/homebridge-nest/issues"
    }
}]
```

> This example is truncated

To show details of a single package.

```
GET /api/plugins/:package [valid package on npmjs.com]
```

> This will fetch any available package. If it is installed you will see a version in the installed field.

To install a plugin.

```
PUT /api/plugins/:package [valid package on npmjs.com]
```

> Note: The package is the same as the NPM install command. These formats are supported.
> 
> * homebridge-ring
> * @hoobs/wink
> * homebridge-ring@4.1.8
> * @hoobs/ring@4.1.8
> * homebridge-wink@latest
> * @hoobs/nest@latest
> 
> Remember to URL encode the value, "@" and "/" are special URL characters.

To remove a plugin

```
DELETE /api/plugins/:package [valid package on npmjs.com]
```

To update a plugin

```
POST /api/plugins/:package [valid package on npmjs.com]
```

> Note: The package is the same as the NPM install command. These formats are supported.
> 
> * homebridge-ring
> * @hoobs/wink
> * homebridge-ring@4.1.8
> * @hoobs/ring@4.1.8
> * homebridge-wink@latest
> * @hoobs/nest@latest
> 
> Remember to URL encode the value, "@" and "/" are special URL characters.


## System Information
This API fetches information about the system. Non admin users only have access to the CPU and Memory load.

```
GET /api/system
```

Returns basic system information

```javascript
{
    "system": {
        "manufacturer": "HOOBS.org",
        "model": "LP-1"
    },
    "bios": {
        "vendor": "Apple Inc.",
        "version": ""
    },
    "motherboard": {
        "manufacturer": "Apple Inc.",
        "model": "MacBookPro14,2"
    },
    "chassis": {
        "manufacturer": "Apple Inc.",
        "model": "MacBookPro14,2"
    },
    "battery": {
        "hasbattery": true,
        "cyclecount": 41
    },
    "os": {
        "platform": "darwin",
        "distro": "Mac OS X"
    }
}
```

> This example is truncated

To get CPU information

```
GET /api/system/cpu
```

To get memory information

```
GET /api/system/memory
```

To get system load/activity

```
GET /api/system/activity
```

To get the current file system use.

```
GET /api/system/filesystem
```

To get the current CPU temprature.

```
GET /api/system/temp
```
