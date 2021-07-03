<img src="https://raw.githubusercontent.com/hoobs-org/HOOBS/main/docs/HOOBS4/header.jpg" width="100%">

The entire HOOBS core has been rebuilt from the ground up on a new, extensible architecture which allows an easier deployment and modular, independent upgrades of components. Many enhancements and bug fixes have been implemented based on all the feedback we received from you.



# Overall System Improvements


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



# Plugins and Community improvements



#### New Plugin Library
A redesigned plugin page which allows you to browse available plugins by different criteria and categories. Plugin reviews from the community help you select the best ones. Version swapping in one click is also available.

####  More Certified Plugins
With HOOBS 3 we released the new configuration schema which enabled code free configuration for a lot of plugins. Many of them have now been certified and will soon be featured on the plugins page. If you have a suggestion for a plugin certification please let us know.

#### Shareable Bridges
You can now export every individual bridge with all its plugins and configurations from the bridges page. This can be used to mirror migrate your bridges to another HOOBS device or to share particular setups and configurations with the community and developers.



# User Interface enhancements


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



# Desktop Apps


#### MacOS Application
A web UI is nice and practical, but you know what's even nicer? Not having to deal with browser issues, router incompatiblities with the .local domain or having to find the local IP address of your HOOBS. Automatic discovery of your device takes care of all that. 

#### Windows Application
If your operating system of choice is Windows, we've got you covered too! The app gives you full control over your HOOBS device without the need of a browser. This also brings control of your smart home into Windows, a first in the home automation industry!
