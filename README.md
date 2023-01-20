# dalaran
Raspberry Pi 4 repository for my Docker compose files.

I'm using Ubuntu Server 22.04 for the OS. More info: https://ubuntu.com/download/raspberry-pi

Please follow the next guide to install Docker: https://docs.docker.com/engine/install/ubuntu/

Also, please follow the next guide to install Docker Compose: https://docs.docker.com/compose/install/linux/

## Requirements

Have installed Docker and Docker Compose. Also, please install `linux-modules-extra-raspi` for support IPvlan and Macvlan.

```
apt install linux-modules-extra-raspi
```

## Create vlan networks

If you want to use vlan networks for better segmentation and security, first you need to create the interface. For example, vlan 100:

```
ip link add link eth0 name eth0.100 type vlan id 100
ip link set eth0.100 up
```

And then, create the Docker network with the vlan:

```
docker network create -d ipvlan --subnet=192.168.100.0/24 --gateway=192.168.100.1 -o ipvlan_mode=l2 -o parent=eth0.100 vlan100
```

More information: https://docs.docker.com/network/ipvlan/
