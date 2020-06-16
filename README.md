# Setting up Ubuntu for Hyperledger Fabric

Instructions how to setup a basic system with all prerequisites for Hyperledger Fabric on Ubuntu.


# Table of contents
1. [Install Hyperledger Fabric Essentials](#essentials)
    1. [Install Docker and Docker Compose](#docker)
    2. [Install Go](#go)
    3. [Install Node.js Runtime and NPM](#node-and-npm)
    
2. [Download Docker Images](#docker-images)

## Install Hyperledger Fabric Essentials <a name="essentials"></a>

### Install Docker and Docker Compose <a name="docker"></a>

Open a terminal and install curl, docker and docker-compose:

```console
$ sudo apt-get install curl docker docker-compose
```

Make sure that Docker and Docker Compose versions are above the required (17.06.2-ce and 1.14.0)

```console
$ docker --version
$ docker-compose --version
```
Add user to the Docker group and reboot to apply the changes:

```console
$ sudo usermod -a -G docker $USER
$ reboot
```

### Install Go <a name="go"></a>

Install the recommended version of 1.11.x manually:

First, go to [Go download page](https://golang.org/dl/) and copy the url of the latest go1.14.x.linux-amd64.tar.gz file. Then, in the terminal:

```console
$ wget https://dl.google.com/go/go1.14.1.linux-amd64.tar.gz
```

Next, unpack the package and move the go directory to `/usr/local`.

```console
$ tar -xvf go1.14.1.linux-amd64.tar.gz
$ sudo chown -R root:root ./go
$ sudo mv go /usr/local
```

Next, set some paths for Go. Open .profile in an editor and add the following to the end of the file:

```console
$ export GOROOT=/usr/local/go
$ export GOPATH=$HOME/go
$ export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
```
Save and close the file, then apply changes:
```console
$ source ~/.profile
```

### Install Node.js Runtime and NPM <a name="node-and-npm"></a>

This step is necessary if you're planning to write chaincode in Javascript.

First, install the [Node Version Manager](https://github.com/nvm-sh/nvm)
```console
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
Close and re-open the terminal, so that the nvm command is available. Then, install latest LTS of node:
```console
$ nvm install --lts
```

## Download Docker Images <a name="docker-images"></a>

Hyperledger Fabric provides a bootstrap script, which downloads all available docker images. 
Enter the following commands in your terminal to download the latest version:

```console
$ mkdir fabric && cd fabric
$ curl -sSL https://bit.ly/2ysbOFE | bash -s
```
If you want to download specific versions, modify the above command:
```console
$ curl -sSL https://bit.ly/2ysbOFE | bash -s -- <fabric_version> <fabric-ca_version> <thirdparty_version>
```

The command above downloads and executes a bash script that will download and extract all of the platform-specific binaries you will need to set up your network.

You're done!
