HOOBS uses Homebridge under the hood. So developing a plugin for HOOBS is the same as Homebridge.

> Notes about this documentation. Commands you need to run in the terminal are prefixed with `~]$`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

There are two basic types of plugins:
* Single accessories: controls, for example, a single light bulb.
* Platform accessories: a "meta" accessory that controls many sub-accessories. For example, a bridge that translates to many other devices on a specialized channel.

There are many existing plugins you can study; you might start with the included [Example Plugins](https://github.com/nfarina/homebridge/tree/master/example-plugins). Right now this contains a single plugin that registers a platform that offers fake light accessories. This is a good example of how to use the Homebridge Plugin API. You can also find an example plugin that [publishes an individual accessory](https://github.com/nfarina/homebridge/tree/6500912f54a70ff479e63e2b72760ab589fa558a/example-plugins/homebridge-lockitron).

For more example on how to construct HomeKit Services and Characteristics, see the many Accessories in the [Legacy Plugins](https://github.com/nfarina/homebridge-legacy-plugins/tree/master/accessories) repository.

You can also view the [full list of supported HomeKit Services and Characteristics in the HAP-NodeJS protocol repository](https://github.com/KhaosT/HAP-NodeJS/blob/master/lib/gen/HomeKitTypes.js).

See more examples on how to create Platform classes in the [Legacy Plugins](https://github.com/nfarina/homebridge-legacy-plugins/tree/master/platforms) repository.

## Development Environment
The HOOBS stack overrides the Homebridge plugin path. So to develop and test plugins, you will need to install a vanilla copy of Homebridge.

Some of the tools you will need:
* A Unix based system (Linux, Mac)
* git (included with Xcode Command Line Tools on Mac)
* An IDE like Visual Studio Code

On my development computer, I have a folder `~/Projects/Plugins`, you can choose any directory you need.

First get a development copy of Homebridge.

```bash
~]$ cd ~/Projects/Plugins
~]$ git clone https://github.com/nfarina/homebridge.git
```

Create a folder to hold your config files.

```bash
~]$ mkdir homebridge-dev-config
```

Install dependencies.

```bash
~]$ cd homebridge
~]$ npm install
```

Test to see if Homebridge starts.

```bash
~]$ bin/homebridge
```

> Note: Your config file should located in `~/.homebridge/config.json`. If not you will need to create one.

Using this method will not conflict with any other installiation of HOOBS or Homebridge. All code will be contained in `~/Projects/Plugins` and the `/homebridge` folder.

## Running Homebridge
When writing your plugin, you'll want Homebridge to load it from your development directory instead of publishing it to npm each time.

> Note: I am assuming that your current working directory is where you have your development copy of Homebridge installed. In my case I am using `~/Projects/Plugins/homebridge`.

You can tell Homebridge to look for your plugin at a specific location using the command-line parameter -P. For example, if you are in the Homebridge directory (as checked out from Github), you might type:

```bash
~]$ bin/homebridge -D -P ../my-great-plugin/
```

This will start up Homebridge and load your in-development plugin from a nearby directory. Note that you can also direct Homebridge to load your configuration from somewhere besides the default `~/.homebridge`, for example:

```bash
~]$ bin/homebridge -D -U ../homebridge-dev-config -P ../my-great-plugin/
```

This is very useful when you are already using your development machine to host a "real" Homebridge instance (with all your accessories) that you don't want to disturb.

## HOOBS Certification
HOOBS has a plugin certification program that can help promote your plugin on the HOOBS platform.

Another benifit to having your plugin certified, is HOOBS support can help users setup these plugins. This frees up you, as the developer from basic support. If we find something that needs your attention we will create an issue in your repository.

Here a set of rules that need to be followed to get you plugin certified.

**One Platform, One Plugin Rule**  
This is an important one. There are countless plugins where there is already a plugin for the same platform. We do not discourage this. However, we can only certify one plugin.

For example, we have a certified Nest plugin. So we will not certify another Nest plugin.

We do this stop confustion in the community. When a user searches for a plugin, there should only be one certified solution.

If you think you have a better way we encourge you to;

* Contact the original developer, and colloraborate.
* If the orginal developer is MIA, send an email to info@hoobs.org, and we will either track down the orginal developer, or start the process of moving ownership of the certified plugin.
* If you are taking over a plugin, the new plugin should behave the same as the old. A user can not expect to do things differently with their current configuration.
* The new plugin should support the old configuration.

**Don't Overload the Platform Configuration**  
Homebridge is designed to use platforms to configure plugins that dynamically define their accessories. Plugins that need a specific configuration belong in the accessories section of the config.json.

Why do we have this rule

* Simplifies the configuration
* In a configuration schema file, you can't have a dropdown with variable complex JSON.
* We have a system for configuring accessories that makes it easy for end users.

> Note: Yes we can do a recursive dialog based interface to support this, but it would make for a complex interface which could be more confusing than editing the JSON.

Sometimes it is easier to just add the definitions to the platform JSON, but solving this problem in your plugin will make your plugin more stable and conform the the Homebridge design.

And yes a plugin can have both a platform and accessory configuration, and values from the platform are accessible from an accessory.

**Don't Make the User Install or Call External Commands**  
I see many plugins that require the user to install a plugin and then open the terminal and run a command to get other information.

Yes some systems need to do this, however your plugin is running on Node. You are able to make calls from your application, and programmatically obtain the information needed.

If you need to run a command on install, NPM has a post install directive that can run a command to initialize things.

> Note: Systems like SmartThings require further setup in SmartThings. We are OK with this, as long as it is documented.

**Documentation**  
Since HOOBS handles the burden of support, we need clear documentation. We prefer that this documentation be on your readme in your repository.

Part of our certification process is, can we understand your documentation?

**Configuration Schema**  
HOOBS uses JSON schema to read in your config to the interface. We use a standard found [here](https://json-schema.org/learn/getting-started-step-by-step.html).

There are two schema files your plugin needs.
* platform.schema.json
* accessories.schema.json

These files need to be in the root of your project and included when published.

Here is an example of the `platform.schema.json` file.

```json
{
    "plugin_alias": "Shelly",
    "schema": {
        "type": "object",
        "properties": {
            "platform": {
                "title": "Platform",
                "type": "string",
                "const": "Shelly",
                "readOnly": true
            },
            "username": {
                "title": "Username",
                "type": "string"
            },
            "password": {
                "title": "Password",
                "type": "string",
                "options": {
                    "hidden": true
                }
            }
        }
    }
}
```

Here is an example of the `accessories.schema.json` file.

```json
{
    "plugin_alias": "XiaomiRoborockVacuum",
    "schemas": [{
        "title": "Roborock Vacuum",
        "type": "object",
        "properties": {
            "accessory": {
                "title": "Accessory",
                "type": "string",
                "const": "XiaomiRoborockVacuum",
                "readOnly": true
            },
            "name": {
                "title": "Name",
                "type": "string",
                "default": "Roborock Vacuum",
                "required": true
            },
            "ip": {
                "title": "IP Address",
                "type": "string",
                "required": true
            },
            "token": {
                "title": "Access Token",
                "type": "string",
                "required": true,
                "options": {
                    "hidden": true
                }
            },
            "pause": {
                "title": "Show Pause Switch",
                "type": "boolean",
                "default": false,
                "required": true
            },
            "dock": {
                "title": "Show Dock Sensor",
                "type": "boolean",
                "default": true,
                "required": true
            }
        }
    }]
}
```

The `accessories.schema.json` file is a collection of schemas. This is why it uses a `schema` directive. This is an array for the different types of accessories a user may need to configure.

```json
{
    "plugin_alias": "demo",
    "schemas": [{
        "title": "Accessory 1",
        "type": "object",
        "properties": {
            
        }
    }, {
        "title": "Accessory 2",
        "type": "object",
        "properties": {
            
        }
    }, {
        "title": "Accessory 3",
        "type": "object",
        "properties": {
            
        }
    }]
}
```

These are addressed by index. So if a user configures an `Accessory 1` the `plugin_map` in the config file will include an `index: 0` value.

> Note: It is important to keep the order of the schemas when pushing updates. If you add a new accessory to the top, users who already have accessories defined, their current config will be wrong when they update. Always add new accessories to the bottom of your schemas array.

Each schema file has a `plugin_alias` directive. In Homebridge the package and plugin name are not equal. This value will tie the plugin name to the package name. For example;

* The Nest plugin's name is `Nest`.
* The plugin package is called `homebridge-nest`.
* The HOOBS certified package is called `@hoobs/nest`.

As you can see the values are not equal, and HOOBS uses the `plugin_alias` to tie it all together.

**Branding**  
HOOBS ties pictures to each certified plugin. This helps users associate a plugin to a device. For example the Nest plugin has a `product.png` file in the `branding` folder in the repository. This is a picture of a Nest thermostat.

Here are some guidelines on the image.
* It needs to have a transparent background. This is needed because the interface is themed.
* The image needs to be 512px square.
* The image needs to represent the "most associated" device. For example the Wink plugin has a picture of a Wink Hub 2.

The `branding` folder is a great place to store other images associated with your plugin like images for your readme and logos.

**Keywords**  
HOOBS uses keywords to classify your plugin. As of this writing the categories are;

* category-voice-assistant
* category-climate
* category-lighting
* category-video
* category-hubs
* category-security
* category-outdoor
* category-media

You will need to add one or more keywords to your plugin. This will place your plugin in the proper category.

We will add the `hoobs-certified` keyword to your plugin when we approve it. We do this when we create a downstream of your plugin and publish it under the @hoobs scope. We will also remove the `homebridge-plugin`. We do this because Homebridge can not load scoped plugins, and we need to remove it from the searches.

Also we will add the `hoobs-plugin` keyword. it is OK to add this before your plugin is certified. We fully support Homebridge plugins.

**Publishing**  
Once your plugin is certified we will create a downstream of your repository (fork). And we will freeze the released version. This helps control the user experience. If you make updates, we will test the changes and update the certified version for you.

If you get your plugin certified, it is OK to publish the non certified version for Homebridge. In fact we encourage it. This helps test your upstream to make a solid plugin. (Like Red Hat and Fedora)
