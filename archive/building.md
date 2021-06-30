HOOBS is open source. If you need to build HOOBS from source. Here's how you do it.

HOOBS uses these technologies.
* Node
* Docker
* RPI Build Tools

## Repositories
To build HOOBS you need to clone four repositories
* hoobs-core
* hoobs-upgrade
* hoobs-gen
* hoobs-connect

All of these repositories are available from our GitHub organization.  
[https://github.com/hoobs-org](https://github.com/hoobs-org)

The `hoobs-core` repository is the root of the project. This is where the build tools are. And you can access them from the `npm run` command.

To view the the options, run this command.

```bash
~]% npm run hoobs -- --help
```

## HOOBS Core
First you need to build

```bash
~]% npm run hoobs build
```

Then to publish run this command

```bash
~]% npm run hoobs publish
```

## HOOBS Upgrade Utility
This is the utility used to upgrade older versions of HOOBS or any install using UI-X.

To build you will need to clone the hoobs-upgrade repository at the same level as hoobs-core.

To build run this.

```bash
~]% npm run hoobs utility build
```

And to publish

```bash
~]% npm run hoobs utility publish
```

## HOOBS Raspberry Pi Images
HOOBS uses the RPI Gen tool to build the SD card images. The code that does this is available in the `hoobs-gen` repository.

**Dependencies**  
This requires a Debian 10+ is required to run the build process.

To build you need to install the required dependencies.

```bash
apt-get install -y coreutils quilt parted qemu-user-static debootstrap zerofree zip dosfstools bsdtar libcap2-bin grep rsync xz-utils file git curl
```

If you have Docker installed you can use the --container flag. This will allow you to build the images without Debian.

**Building**  
There is a build script included with this repository. Run this command to see the options.

```
~%]% image --help
```

You will first need to set the current working directory to the `hoobs-gen` project.

```
~%]% cd ~/hoobs-gen/
```

To build stable images.

```
~%]% image build
```

To build stable images using a Docker container

```
~%]% image build --container
```

To clean the work and deploy directories.

```
~%]% image clean
```

## HOOBS Connect
The HOOBS connect utility is used to aid in connecting a headless Raspberry Pi to a WiFi network. HOOBS connect is a modified version of Balina WiFi Connect.

The HOOBS Connect build is included with the `hoobs-gen` build script. To build the HOOBS Connect interface run the following command.

```
~%]% image build connect
```

## HOOBS Docker Image
HOOBS Core has Docker build files included. From this repository you are able to build the image, create a container locally and control that container.

You will need to install the latest version of Docker Desktop to build.  
[https://hub.docker.com/?overlay=onboarding](https://hub.docker.com/?overlay=onboarding)

HOOBS uses Docker Buildx for it's images. You will need to edit the Docker Desktop settings and enable the "Expermental" tools. Here is some more information on this.  
[https://docs.docker.com/buildx/working-with-buildx/](https://docs.docker.com/buildx/working-with-buildx/)


**Building**  
Building the image.

```bash
~]% npm run hoobs container build
```

**Volume**  
HOOBS uses a volume to keep the configs and plugins. You will need to create a volume so your HOOBS instance doesn't reset when building.

To create the HOOBS volume.

```bash
~]% npm run hoobs volume create
```

And to delete the volume.

```bash
~]% npm run hoobs volume remove
```

**Local Container**  
Creating the HOOBS container locally

```bash
~]% npm run hoobs container create
```

Start the HOOBS container locally

```bash
~]% npm run hoobs container start
```

Stop the HOOBS container locally

```bash
~]% npm run hoobs container stop
```

Removing the local HOOBS container

```bash
~]% npm run hoobs container remove
```
