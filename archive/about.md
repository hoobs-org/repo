HOOBS has it's roots in an old Homebridge plugin called [homebridge-config-ui](https://github.com/mkellsy/homebridge-config-ui). This is one of the first configuration interfaces for Homebridge. It has been copied and reused by many other plugins, including some very popular plugins. homebridge-config-ui's mission was to make Homebridge easier, and back when we started, it was tough.

## HOOBS 4
The entire HOOBS core has been rebuilt from the ground up on a new, extensible architecture which allows an easier deployment and modular, independent upgrades of components. Many enhancements and bug fixes have been implemented based on all the feedback we received from you.

### Overall System Improvements
#### Performance Upgrades
Major improvements were done on the UI speed and accessory control. Accessory state now instantly reflects in the HOOBS dashboard when controlled from an outside source. Memory usage has been massively reduced making HOOBS lightning fast!

#### 1 Plugin per Bridge
When installing a plugin you have the option to spawn a new bridge or add it to an existing bridge. Running a single plugin per bridge ensures stability for all other accessories in case a plugin misbehaves.

#### Encrypted Backups
Your entire HOOBS 4 system can be backed up and restored from the Hub Settings in the top right menu. The backup files are encrypted for secure storage on your computer. Backups are lightning fast and a fraction of the size compared to HOOBS 3.

#### Recovery Terminal
Tired of having to SSH into HOOBS if something goes wrong and you get locked out? You can now access an independent terminal at this address and simply reset your device: http://hoobs.local:9090

#### System and Node Updates from the User Interface
No more manual updates of any dependencies using the terminal. Each HOOBS component now runs independent of eachother which allows updating the Server, Interface and System directly from the UI.

### Plugins and Community improvements
#### New Plugin Library
A redesigned plugin page which allows you to browse available plugins by different criteria and categories. Plugin reviews from the community help you select the best ones. Version swapping in one click is also available.

#### More Certified Plugins
With HOOBS 3 we released the new configuration schema which enabled code free configuration for a lot of plugins. Many of them have now been certified and will soon be featured on the plugins page. If you have a suggestion for a plugin certification please let us know.

#### Shareable Bridges
You can now export every individual bridge with all its plugins and configurations from the bridges page. This can be used to mirror migrate your bridges to another HOOBS device or to share particular setups and configurations with the community and developers.

### User Interface enhancements
#### Cameras! All of them!
Get a full view of your home directly in your HOOBS Dashboard. All cameras added via the camera-ffmpeg plugin as well as Ring and Nest cams will now be displayed in the HOOBS accessories. Snapshots and snapshot streaming is available by default for all cameras. Supported cameras can toggle live stream from the camera accessory settings.

#### Simple, Filtered Log
No more trying to dechiper thousands of lines of logs to find what you’re looking for. Logs can now be filtered by plugin, by bridge or by system. Debug log is toggled off by default. This keeps the log clean and only outputs important information.

#### Code Free Configuration
HOOBS 4 provides full configuration schema support for all plugins that offer it. This enables easy configuration with no manual JSON entry.

#### Dashboard Widgets
Each accessory is now an individual widget. Additional system widgets are also available. Build your own dashboard just the way you like it by drag & dropping and resizing each widget freely.

#### Custom Accessory Icons
Personalization just got better. You can now choose from a list of over a thousand icons to assign to each one of your static accessories.

#### Infinite Personalization
Your home, your theme. Choose one of the template themes or generate your own by uploading your favorite background image. HOOBS will automatically pick the best colors to go along with your image.

### Desktop Apps
#### MacOS Application
A web UI is nice and practical, but you know what's even nicer? Not having to deal with browser issues, router incompatiblities with the .local domain or having to find the local IP address of your HOOBS. Automatic discovery of your device takes care of all that.

#### Windows Application
If your operating system of choice is Windows, we've got you covered too! The app gives you full control over your HOOBS device without the need of a browser. This also brings control of your smart home into Windows, a first in the home automation industry!


## HOOBS 3
Now that Homebridge(X) has matured. It proves to be a new way of running Homebridge. We renamed the project to HOOBS 3 and started the beta. HOOBS 3 is a software stack, with an API and the interface from the orginal homebridge-config-ui plugin. Where the API and interface are seperate processes from Homebridge. HOOBS 3 also creates a "user mode" for Homebridge. This allows us to keep things secure. Plugins no longer have system wide access, they are contained within the HOOBS 3 processes.

HOOBS 3 also opens the door for some very exciting features. Backup, Restore and Factory Reset. This includes the plugins you have installed. Now you can get HOOBS 3 setup perfectly and back it up. Then if anything happens, you can restore HOOBS 3 to your once perfect setup.

## The Homebridge Community
We would like to thank the entire Homebridge community. Without your continued use and your ability to push the envelope on what Homebridge can do, there would be no need for HOOBS. HOOBS aims to not only make Homebridge easier for everyone, we also want to help create those new technologies, that make even the most advanced of us excited. So you may hear HOOBS is for noobs, and it is, but really it's for us all.

## Partners & Open Source
We would like to reconize some of our partners and open source software that we use.

### two4you business solution
[Website](https://two4you.business)

HOOBS Hardware is Manufactured by two4you business solution gmbh

two4you business solution gmbh is the official Manufacturer of HOOBS in a Box and HOOBS on microSD.
### Homebridge
[Website](https://homebridge.io)

HOOBS is based on Homebridge. Homebridge is a lightweight NodeJS server that emulates the iOS HomeKit API.
Homebridge allows you to integrate with smart home devices that do not support the HomeKit protocol. Here are just some of the manufacturers you can integrate with. Homebridge is brought to you by thousands of plugin developers, dozens of core contributors, @pieceofsummer who reverse engineerered HomeKit, @KhaosT who built the HAP server, this guy @nfarina, and home hackers like you.

### HAP NodeJS
[Website](https://github.com/KhaosT/HAP-NodeJS/blob/master/README.md)

HAP-NodeJS is a Node.js implementation of the HomeKit Accessory Server. With HAP NodeJS you can create your own HomeKit Accessory on a Raspberry Pi, Intel Edison, or any other platform that can run Node.js

### Vue.js
[Website](https://vuejs.org)

Vue.js is an MIT-licensed open source project with its ongoing development made possible entirely by the support of these awesome [backers](https://github.com/vuejs/vue/blob/dev/BACKERS.md).

### Express
[Website](https://expressjs.com/)

Fast, unopinionated, minimalist web framework for [node](http://nodejs.org).

### Node.JS
[Website](https://nodejs.org)

HOOBS / Homebridge is based on Node JS
As an asynchronous event driven JavaScript runtime, Node is designed to build scalable network applications.

### Raspbian
[Website](https://raspbian.org)

HOOBS runs on Raspbian. Raspbian is a free operating system based on Debian, optimized for the Raspberry Pi hardware.
An operating system is the set of basic programs and utilities that make your Raspberry Pi run. However, Raspbian provides more than a pure OS: it comes with over 35,000 packages, pre-compiled software bundled in a nice format for easy installation on your Raspberry Pi.

## Translators
HOOBS is available in these languages:

* 🇺🇸 English by MKellsy 
* 🇧🇬 Bulgarian by Angelov Nikolay 
* 🇨🇳 Chinese by Bing Feng Yeh
* 🇨🇿 Czech by kvasnicka robert 
* 🇳🇱 Dutch by Jorg de Boer 
* 🇫🇷 French by Frederic Barthelet 
* 🇩🇪 German by Bobby Slope 
* 🇬🇷 Greek by Konstantinos Koukoulakis 
* 🇮🇱 Hebrew by GalZilbermann 
* 🇮🇹 Italian by Luca Sias 
* 🇳🇴 Norwegian by Jahn Juliussen 
* 🇵🇱 Polish by Tomasz Bzymek 
* 🇪🇸 Spanish by David Muñoz and Felipe Alfaro 
* 🇻🇳 Vietnamese by CiCi 
* 🇷🇺 Russian by Kunanov
* 🇷🇴 Romanian by Rãzvan Vizitiu
* 🇵🇹 Portuguese by João Miguel Luz
* 🇦🇪 Arabic by Ali Hassan

We are searching Support for translators to even more languages. If you like to help us. Please drop us a line with your name and the languages your are able to translate.

Please send us an email to [translation@hoobs.org](mailto:translation@hoobs.org) with subject: [Translation, your Language] and we will invite you to our translating System. We add more strings to translate day by day and when you’re registered in the translation system you get notified when something new is there to translate. 

Thanks so much for your help
