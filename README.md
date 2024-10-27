# iperf3

This is a Docker image for iperf3. Similar to Michel Labbé's iperf3 image, but using hardened alpine from ironpeakservices.

## Installation

The installation is done in the following steps:
1. Acquiring the container tar file
2. Installing the container to the device
3. Starting the container

For the first step, there are multiple ways to achieve that.
#### Easiest

Just download my ready-to-use tar file from releases: [iperf3.tar](https://github.com/rikeardi/iperf3/releases/download/alpine-3.20.3_iperf3-3.17.1-r0/iperf3.tar).

If You trust my word, that is. As a common caution you should not install software on your network without verifying the code.

#### Bit more hands-on

Prerequisites:
An internet-connected Linux system with git and docker installed

1. Read the Dockerfile on my repo. The comments explain what is done there. Verify there are no backdoors.
2. Read the Dockerfile also on the Iron Alpine [repo](https://github.com/ironpeakservices/iron-alpine).

If at this point You feel confident on my repo, you can clone it on your linux system with command ```git clone https://github.com/rikeardi/iperf3.git```

Next you'll need to cd to the directory of the repo with ```cd iperf3``` and build the docker image ```docker build -t my-own/iperf3 .```

If you want, you can edit the Dockerfile before the build to suit your needs.

After the image is built, you can save it to tar file with ```docker save docker.io/my-own/iperf3 -o iperf3.tar```. Now you have the same iperf3 tar file you can download from the releases, but you have verified the contents.

## Credits
[Michel Labbé's iperf3](https://github.com/michellabbe/docker-iperf3)

[Ironpeak services Iron Alpine](https://github.com/ironpeakservices/iron-alpine)

[Cisco DevNet instructions for iperf on Cisco device](https://developer.cisco.com/docs/app-hosting/deploy-iperf3-performance-monitoring-application/)

