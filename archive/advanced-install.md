We try to make our install script work on most systems. However, sometimes things don't go as planned. So we are documenting how to install HOOBS without the scripts. There are two scripts we are covering here.

Before you continue with this document. There is a far easier way to install HOOBS. This script does everything in the document automatically.

```bash
~]$ wget -q -O - http://bit.ly/get-hoobs | sudo bash -
```

Here is the install flow for HOOBS  
1. Prerequisites - `wget -q -O - http://bit.ly/get-hoobs`.
2. Install HOOBS - `sudo npm install -g --unsafe-perm @hoobs/hoobs`.
3. Configure service and proxy - `sudo hoobs-init`

We will use Debian for this tutorial. These commands cover Raspbian on the Raspberry Pi.

## Prerequisites
The first thing you need to do is to make sure everything is available on the system.

Here are the prerequisites needed to run HOOBS
* curl
* tar
* mdns
* avahi
* perl
* python
* node
* npm
* yarn (experimental)

First make sure the repositories are up to date.

```bash
$ apt-get update
```

Now, install the prerequisites.

```bash
$ sudo apt-get install -y curl tar perl python make gcc g++ libavahi-compat-libdnssd-dev
```

Now we are ready to install Node. We will be installing the LTS version of Node. But first, you need to install from the apt-get repository to install the base libraries Node needs.

```bash
$ sudo apt-get install -y nodejs npm
```

Now get the architecture of your system.

```bash
$ uname -m
```

Your system architecture will be one of the following.
* x86_64
* armv7l
* armv8l

> If your architecture is not listed above, HOOBS might not run on your system.

Now you will need to download and install the proper version of Node. Only run the commands associated with your system architecture.

**x86_64**

```bash
$ curl -k https://nodejs.org/dist/v12.14.0/node-v12.14.0-linux-x64.tar.gz | sudo tar -xz -C /usr/local --strip-components=1 --no-same-owner
```

**armv7l**

```bash
$ curl -k https://nodejs.org/dist/v12.14.0/node-v12.14.0-linux-armv7l.tar.gz | sudo tar -xz -C /usr/local --strip-components=1 --no-same-owner
```

**armv8l**

```bash
$ curl -k https://nodejs.org/dist/v12.14.0/node-v12.14.0-linux-arm64.tar.gz | sudo tar -xz -C /usr/local --strip-components=1 --no-same-owner
```

Now verify that Node installed. You should see `v12.14.0`.

```bash
$ node -v
```

Now clean the NPM cache.

```bash
$ sudo npm cache clean --force
```

Make sure you are on the latest version of NPM.

```bash
$ sudo npm install -g npm
```

## Install HOOBS
Installing HOOBS is pretty straight forward. Simply run this command.

```bash
$ sudo npm install -g --unsafe-perm @hoobs/hoobs
```

HOOBS uses Node GYP and will build for your system during the install. If you installed prerequisites, this should work. If you get errors, you will need to troubleshoot and correct the errors before continuing.

## Run as a Service
Next you need to create the HOOBS service. This will start HOOBS when your device starts.

HOOBS creates a special user to run the service, so first we need to create the `hoobs` user.

```bash
$ sudo useradd -s /bin/bash -m -d /home/hoobs -p $(perl -e 'print crypt($ARGV[0], "password")' "hoobsadmin") hoobs
```

> We are using `hoobsadmin` for the password. You can change this to anything you want.

Now you need to add the `hoobs` user to the `sudo` group.

```bash
$ sudo usermod -a -G sudo hoobs
```

> If you are on Fedora, Red Hat or CentOS, the sudo group is called `wheel`.

Next, create the `hoobs.service` file.

```bash
$ sudo nano /etc/systemd/system/hoobs.service
```

Enter this into the file and save. (`ctrl + x` then `y` and `enter`).

```
[Unit]
Description=HOOBS
After=network-online.target

[Service]
Type=simple
User=hoobs
ExecStart=/usr/local/bin/hoobs
Restart=on-failure
RestartSec=3
KillMode=process

[Install]
WantedBy=multi-user.target
```

Then reload the systemd daemon.

```bash
$ sudo systemctl daemon-reload
```

Now enable the HOOBS service.

```bash
$ sudo systemctl enable hoobs.service
```

## Install the Reverse Proxy
HOOBS runs on port 8080. We use NGINX to proxy port 80 to port 8080. This is done to protect the actual port HOOBS runs on and makes it easier for remote access.

Install NGINX.

```bash
$ sudo apt-get install -y nginx
```

Configure the base server.

```bash
$ sudo nano /etc/nginx/nginx.conf
```

Edit the file with this.

```
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;

events {
    worker_connections 1024;
}

http {
    access_log  /var/log/nginx/access.log;

    sendfile                     on;
    tcp_nopush                   on;
    tcp_nodelay                  on;
    keepalive_timeout            65;
    types_hash_max_size          4096;

    include                      mime.types;
    default_type                 application/octet-stream;
    gzip                         on;

    ssl_protocols                TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers    on;

    include /etc/nginx/conf.d/*.conf;
}
```

Next, create the HOOBS site config file.

```bash
$ sudo nano /etc/nginx/conf.d/hoobs.conf
```

Enter this into the `hoobs.conf` file.

```
server {
    listen 80;
    listen [::]:80;
    server_name hoobs;
    client_max_body_size 2048M;

    error_page 502 /loader.html;

    location / {
        proxy_pass            "http://127.0.0.1:8080";

        proxy_set_header      X-Real-IP $remote_addr;
        proxy_set_header      Upgrade $http_upgrade;
        proxy_set_header      Connection \"upgrade\";

        add_header            Cache-Control \"no-store, no-cache, must-revalidate, proxy-revalidate, max-age=0\";

        if_modified_since     off;
        expires               off;
        etag                  off;
    }

    location = /loader.html {
        root /usr/share/hoobs;
        internal;
    }
}
```

Now you need to create the NGINX loader site.

```bash
$ sudo nano /usr/share/hoobs/loader.html
```

Then enter this into the `loader.html` file.

```html
<!DOCTYPE html>
<html>
<head>

<meta name="viewport" content="width=device-width, initial-scale=1">
<title>HOOBS</title>

<style>
    body {
        margin: 0;
        background-color: #feb400;
    }

    .content {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        height: 100vh;
    }

    .marquee {
        overflow: hidden;
        position: relative;
        width: 450px;
        max-width: 90vw;
        height: 3px;
        margin: 20px 0 50px 0;
        background: #ffffff42;
    }

    .marquee div {
        position: absolute;
        width: 40%;
        margin: 0;
        height: 3px;
        background: #fff;
        animation: loading-marquee 2s linear infinite alternate;
    }

    @keyframes loading-marquee {
        0% {
            transform: translateX(280%);
        }

        100% {
            transform: translateX(-140%);
        }
    }
</style>

<script>
    (async function () {
        const check = setInterval(async () => {
            const response = await fetch("/");

            if (response.status === 200) {
                clearInterval(check);
                location.reload(true);
            }
        }, 4000);
    }());
</script>

</head>
<body>

<div class="content">
    <div class="marquee">
        <div></div>
    </div>
</div>

</body>
</html>
```

After changing the files, you need to reload the systemd daemon.

```bash
$ sudo systemctl daemon-reload
```

Then, enable the NGINX service.

```bash
$ sudo systemctl enable nginx.service
```

## Firewall
This is optional. If you are running a firewall, ie. the one that comes with Fedora.

Find the default zone.

```bash
$ sudo firewall-cmd --get-default-zone
```

Enable port 80. Replace [default-zone] with the results from above.

```bash
$ sudo firewall-cmd --zone=[default-zone] --add-port=80/tcp --permanent
```

Enable port 8080. Replace [default-zone] with the results from above.

```bash
$ sudo firewall-cmd --zone=[default-zone] --add-port=8080/tcp --permanent
```

Enable port 51826. Replace [default-zone] with the results from above.

```bash
$ sudo firewall-cmd --zone=[default-zone] --add-port=51826/tcp --permanent
```

Now reload the firewall.

```bash
$ sudo firewall-cmd --reload
```

## SELinux
This is optional. If your system uses SELinux, you need to tell SELinux that you intend to allow network connections.

```bash
$ sudo setsebool -P httpd_can_network_connect 1
```

> We don't recommend disabling SELinux. SELinux helps keep your device secure.

## Reboot
Now you should reboot to test if everything starts.

```bash
$ sudo shutdown -r now
```

Once the system is back up you should be able to access the interface at `http://hostname.local`. (Replace hostname with your device's hostname, we use `hoobs` on the SD cards).
