To setup remote access we need to setup a NGINX web server. This is a lightweight server that is very popular with Node.js applications because NGINX comes with a reverse proxy.

> You will need to know how to access your router to enable port forwarding to access HOOBS remotely.

> Notes about this documentation. Commands you need to run in the terminal are prefixed with `~%`. You don't enter the prefix in to the terminal. If you don't see the prefix, this means the content is either example output or content you need to enter into a file.

## Installing Homebrew
NGINX doesn't come with macOS, and there is no downloadable package. You will need to install Homebrew to get NGINX.

Run this command to install NGINX.

```bash
~% /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

After Homebrew installs, you need to reset XCode.

```bash
~% sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```

> This needs to be done because Homebrew tries to reset it, but fails. Both Homebrew and Node can use the command line tools that come with XCode.

## Installing NGINX
Now let's install NGINX.

```bash
~% brew install nginx
```

> Homebrew handles macOS permissions automatically, you should never use sudo when installing packages from Homebrew.

Now let's enable the NGINX server.

```bash
~% sudo brew services start nginx
```

## Configuring
NGINX requires some configuration, but don't worry, we have you covered.

Edit the `nginx.conf` file

```bash
~% nano /usr/local/etc/nginx/nginx.conf
```

Replace the contents of the file with this.

```
worker_processes 1;

events {
    worker_connections 1024;
}

http {
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

    include servers/*;
}
```

> Note: You can use `ctrl+k` to delete a line in nano.

Now let's create the `hoobs.conf` file. This defines the reverse proxies.

```bash
~% mkdir /usr/local/etc/nginx/servers
~% nano /usr/local/etc/nginx/servers/hoobs.conf
```

Enter the following into the file.

```
server {
    listen 80;
    listen [::]:80;
    server_name hoobs;
    client_max_body_size 2048M;

    error_page 502 /loader.html;

    location / {
        proxy_pass            "http://127.0.0.1:8080";
        proxy_http_version    1.1;
        proxy_set_header      X-Real-IP $remote_addr;
        proxy_set_header      Upgrade $http_upgrade;
        proxy_set_header      Connection "upgrade";
    }

    location = /loader.html {
        root /usr/local/share/hoobs;
        internal;
    }
}
```

> For this tutorial we are using port `80`. You can choose any port you need, simply change the `listen` directives.

## Setup the HOOBS Site
One advantage to using NGINX, is we now have the ability to show a nice loader when the server is booting.

Create the directory for the site.

```bash
~% sudo mkdir /usr/local/share/hoobs
~% sudo chown -R $(whoami) /usr/local/share/hoobs
```

Download the HOOBS loader page.

```bash
~% curl https://raw.githubusercontent.com/hoobs-org/hoobs-core/master/config/loader.html --output /usr/local/share/hoobs/loader.html
```

## Start NGINX
Now you need to restart NGINX.

```bash
~% sudo brew services restart nginx
```

## Configuring your Router
Everyone has a different router, please refer to your router's manual or online help. You will need to forward port `80` to your HOOBS server.

Some routers require you to reserve the IP address to enable port forwarding.

## Next Steps
Congratulations you have completely configured HOOBS, complete with remote access. Now let us walk you through the [User Interface](5e763b3ee87d1e02b6c19d2a).
