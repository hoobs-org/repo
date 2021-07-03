The HOOBS service is setup automatically for Fedora, Red Hat and Debian. If you are running macOS continue. 

For this tutorial we are using macOS Catalina. If you haven't installed HOOBS please go to [Installing HOOBS](5e763ebbe87d1e02b6c19d37).

> Notes about this documentation. Commands you need to run in the terminal are prefixed with `~%`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

## Create the HOOBS Service
First you need to create the `com.hoobs.plist` file.

```su
~% sudo nano /Library/LaunchDaemons/com.hoobs.core.plist
```

Enter this into the editor.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>Label</key>
        <string>com.hoobs.core</string>
        <key>EnvironmentVariables</key>
        <dict>
            <key>PATH</key>
            <string><![CDATA[/usr/local/bin:/usr/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin]]></string>
            <key>HOME</key>
            <string>/var/root</string>
        </dict>
        <key>Program</key>
        <string>/usr/local/bin/hoobs</string>
        <key>ProgramArguments</key>
        <array>
            <string>/usr/local/bin/hoobs</string>
        </array>
        <key>RunAtLoad</key>
        <true/>
        <key>KeepAlive</key>
        <true/>
        <key>SessionCreate</key>
        <true/>
    </dict>
</plist>
```

## Enable and Start the HOOBS Service
Now you need to enable the HOOBS service.

```su
~% sudo launchctl load -w /Library/LaunchDaemons/com.hoobs.core.plist
```

Check to see if the HOOBS service started.

```su
~% sudo launchctl list | grep com.hoobs.core
```

## Testing the Service
Simply reboot your Mac.

After your Mac boots, open your browser and navigate to [http://hoobs.local:8080](http://hoobs.local:8080).

## Next Steps
Now that you have HOOBS running on startup, lets take your setup to the next level and add remote access. [NGINX Proxy](5e763f44e87d1e02b6c19d3a).
