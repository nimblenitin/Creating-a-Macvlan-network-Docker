# Creating-a-Macvlan-network-Docker

Some applications, especially legacy applications or applications which monitor network traffic, expect to be directly connected to the physical network. In this type of situation, you can use the macvlan network driver to assign a MAC address to each container’s virtual network interface, making it appear to be a physical network interface directly connected to the physical network. 

Steps to create a Macvlan network -

```
1. Create a Macvlan network in bridge mode. Create a Macvlan network in bridge mode with subnet, gateway, and parent values.
$ sudo docker network create -d macvlan \
> --subnet=172.16.86.0/24 \
> --gateway=172.16.86.1 -o \
> parent=docker0 macvlan-net

2. List all the networks to check the newly created macvlan network
$ sudo docker network ls

3. Inspect the macvlan network and check the Driver type
$ sudo docker network inspect macvlan-net

4. Create an Alpine container and attach it to the Macvlan network. Start an Alpine container and attach it to the macvlan-net network.
$ sudo docker run --rm -dit \
> --network macvlan-net \
> --name macvlan-alpine alpine:latest ash

5. Inspect the macvlan-alpine container and observe MacAddress key in the Networks key
$ sudo docker container inspect macvlan-alpine

6. Run the following command to check how the container sees its network interfaces:
$ sudo docker exec macvlan-alpine ip route

```
