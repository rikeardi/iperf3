# iperf3

This is a Docker image for iperf3. Similar to Michel Labbé's iperf3 image, but using hardened alpine from ironpeakservices.

## Installation

The installation is done in the following steps:
1. Acquiring the container tar file
2. Installing the container to the device
3. Using the container
4. Protecting the container with an ACL

### 1. Acquiring the Tar file

For the first step, there are multiple ways to achieve the result.

#### Easiest

Just download my ready-to-use tar file from releases: [iperf3.tar](https://github.com/rikeardi/iperf3/releases/download/alpine-3.20.3_iperf3-3.17.1-r0/iperf3.tar).

If You trust my word, that is. As a common caution you should not install software on your network without verifying the code. I do promise though, that what you see is what you get with this one.

#### Bit more hands-on

Prerequisites:
An internet-connected Linux system with git and docker installed

1. Read the Dockerfile on my repo. The comments explain what is done there. Verify there are no backdoors.
2. Read the Dockerfile also on the Iron Alpine [repo](https://github.com/ironpeakservices/iron-alpine).

If at this point You feel confident on my repo, you can clone it on your linux system with command ```git clone https://github.com/rikeardi/iperf3.git```

Next you'll need to cd to the directory of the repo with ```cd iperf3``` and build the docker image ```docker build -t my-own/iperf3 .```

If you want, you can edit the Dockerfile before the build to suit your needs.

After the image is built, you can save it to tar file with ```docker save docker.io/my-own/iperf3 -o iperf3.tar```. Now you have the same iperf3 tar file you can download from the releases, but you have verified the contents.

### 2. Install the container

You can follow Cisco's DevNet [instructions](https://developer.cisco.com/docs/app-hosting/deploy-iperf3-performance-monitoring-application/).

### 3. Run the container

The last part in the DevNet guide is running the server. However, if You'd like to use the device as iperf client, you need to access the container.

You can verify the container is running with ```show app-hosting list```
There should be the iPerf app listed and state RUNNING.

Now you can access the container with ```app-hosting connect appid iPerf session``` and run iperf3 client commands from there. Leave the container with ```exit```.

### 4. Protect the container

Running an open iperf server on your network device leaves a door open for intentional and unintentional DDoS attack. So it is highly recommended to use an access list to limit the possible clients using your iperf server.

This is an example of an ACL allowing iperf from the network 192.168.1.0/24 to our iperf server in 192.168.5.21.
```
ip access-list extended IPERF-ACL
 10 permit tcp 192.168.1.0 0.0.0.255 host 192.168.5.21 eq 5201
 20 permit tcp host 192.168.5.21 192.168.1.0 0.0.0.255 eq 5201
 30 permit udp 192.168.1.0 0.0.0.255 host 192.168.5.21 eq 5201
 40 permit udp host 192.168.5.21 192.168.1.0 0.0.0.255 eq 5201
 99999999 deny ip any any log-input
```


## Credits
[Michel Labbé's iperf3](https://github.com/michellabbe/docker-iperf3)

[Ironpeak services Iron Alpine](https://github.com/ironpeakservices/iron-alpine)

[Cisco DevNet instructions for iperf on Cisco device](https://developer.cisco.com/docs/app-hosting/deploy-iperf3-performance-monitoring-application/)

[Cisco - Use iPerf on Catalyst 9000 Switches to Perform Bandwidth Tests](https://www.cisco.com/c/en/us/support/docs/switches/catalyst-9200-series-switches/220197-use-iperf-on-catalyst-9000-switches-to-p.html)

