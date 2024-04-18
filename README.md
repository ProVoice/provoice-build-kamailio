# provoice-build-kamailio
ProVoice packages build environment for Kamailio using Docker

## About

This project aims to make reproducable Debian packages of Kamailio for Ubuntu 22.04 LTS by using Docker. We have chosen to use upstream MySQL packages instead of the default packages in the Ubuntu repository. Feel free to remove these lines in the Dockerfile if that would fit your environment better. Create an empty directory for the packages and run the container to build the Debian packages.

Kamailio is part of the [ProVoice platform](https://provoice.eu).

## Building the packages

1. Clone the repository, initialize the Git submodules and build the Docker image
```bash
git clone https://github.com/ProVoice/provoice-build-kamailio.git
cd provoice-build-kamailio
git submodule init
git submodule update --remote
( cd kamailio; git checkout 5.8.1 )
sudo docker build -t provoice-build-kamailio .
```
2. Create a directory for the packages
```bash
mkdir packages
```
3. Run the container to build the packages
```bash
sudo docker run -it \
 --rm \
 -v `pwd`/packages:/app/packages \
provoice-build-kamailio
```
The packages and source files should now be in the `packages` directory and ready to install on Ubuntu 22.04 LTS.
