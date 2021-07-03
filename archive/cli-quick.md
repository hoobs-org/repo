Go to the top right menu -> terminal

![](https://raw.githubusercontent.com/hoobs-org/HOOBS/master/docs/system/terminal.png)

The terminal is the command line for the device HOOBS is running on. 
This works on on the HOOBS Image, Raspbian, all other Linux Distros and MacOS. 
This option is not available on Docker


### General Start
```hoobs``` - starts HOOBS in the default mode
```hoobs -D``` -  Starts HOOBS in debug mode

### Instances
```hoobs client``` - starts the HOOBS UI (used for instances)
```hoobs server -I 'Name'``` - starts a headless HOOBS instance

### Remote Support
```hoobs cockpit``` - starts a remote session without the UI

### Service Control
```sudo hoobs service start``` - starts the HOOBS service
```sudo hoobs service stop ``` - stops the HOOBS service
```sudo hoobs service restart``` - restarts the HOOBS service
```sudo hoobs service enable``` - enables the HOOBS service to start with the system (automatic with install)
```sudo hoobs service disable``` -  disables the HOOBS service without removing it

### Service Log
```sudo hoobs service log``` -  shows a live log from the HOOBS service


### Upgrade
```sudo hoobs upgrade``` -  used by NPM install for after upgrading

### Install FFMPEG Manually
```wget -q -O - http://bit.ly/get-ffmpeg | sudo bash -``` - Installs FFMPEG (automatic with install)

### Change Node Version
```wget -q -O - http://bit.ly/get-hoobs | sudo bash /dev/stdin --node 12.14.0``` 
works with any node version, just change the version number at the end of the command

### Factory Reset
```wget -q -O - http://bit.ly/get-hoobs | sudo bash /dev/stdin --reset ``` Used to Factory Reset HOOBS

### Advanced Options List
**HOOBS man page**
help: hoobs [-v | --version] [command] [-d | --debug] [-i | --instance name] [-p | -pass password]
    Display information about builtin commands.

    Starts the HOOBS service and controls the HOOBS service.
    and cluster clients and instances. This also can install
    the HOOBS service and cluster clients and instances.

    Commands:
        *                         run in default mode
        client                    run a cluster client
        server                    run a cluster instance
        service log               (elevated) show the output of the current service or cluster client
        service start             (elevated) start the current service or cluster client
        service stop              (elevated) stop the current service or cluster client
        service restart           (elevated) restart the current service or cluster client
        service enable            (elevated) enable the current service or cluster client
        service disable           (elevated) disable the current service or cluster client
        service install           (elevated) install a default service
        cluster                   (elevated) list all cluster instances
        cluster client            (elevated) configure and install a cluster client service
        cluster create            (elevated) configure and install a named cluster instance service
        cluster [name] log        (elevated) show the output of a named cluster instance
        cluster [name] start      (elevated) start a named cluster instance
        cluster [name] stop       (elevated) stop a named cluster instance
        cluster [name] restart    (elevated) restart a named cluster instance
        cluster [name] enable     (elevated) enable a named cluster instance
        cluster [name] disable    (elevated) disable a named cluster instance
        switch homebridge         (elevated) switches to the homebridge services if installed
        switch hoobs              (elevated) switches to the hoobs service
        switch uninstall          (elevated) remove homebridge and the switch function
        upgrade                   (elevated) used by npm postinstall when upgrading
        cockpit                   starts an unattached remote terminal session

    Options:
        -v, --version             output the version number
        -d, --debug               turn on debug level logging
        -i, --instance [name]     start homebridge as a named instance
        -p, --pass [password]     password to use for elevated commands
        -h, --help                displays this help menu


**Install Script man page**
help: install [-r | --reboot] [-i | --instance] [-n | --node version]
    Display information about builtin commands.

    Installs HOOBS with prequsits, including Node, NPM and Avachi.
    This script allows you to adjust the version of Node, using
    the -n (or --node) flag. It also allows you to adjust the
    version of NPM using -m (or --npm) flag.

    Note:
        This script requires elevated permissions, please run this with
        SUDO or ROOT privileges.

    Options:
        -r, --reboot              reboots after install
        -i, --instance            install for instances
        -n, --node [version]      the desired Node version
        -m, --npm [version]       the desired NPM version
        -c, --core [file]         file path to NPM pack file
        --reset                   resets to factory settings
        -h, --help                displays this help menu

    Returns:
        Returns success unless the install fails.
