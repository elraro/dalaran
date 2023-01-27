# Adguard

More info: https://adguard.com/es/welcome.html

## Networking

If you want to use vlan networks for better segmentation and security, first you need to create the interface. For example, vlan 100:

```
ip link add link eth0 name eth0.100 type vlan id 100
ip link set eth0.100 up
```

And then, specify it in the Docker Compose.
