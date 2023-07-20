# Networking Basics
- Switching
- Routing
- Default Gateway
- DNS Configurations on Linux

## Switching

To connect two devices we need as switch, with an interface on each host (e.g. eth0). To see the interfaces for the host, use the `ip link` command.

If our network has the address 192.168.1.0, we can assign two addresses in that range (one for each device) like so:

`ip addr add 192.168.1.10/24 dev eth0`
`ip addr add 192.168.1.11/24 dev eth0`

Once up, the devices can now talk to one another - we can check by pinging one:

`ping 192.168.1.11`

It can receive packets within the network and deliver it to other hosts within the same network.


## Routing

But if we another network with the address 192.168.2.0 (with devices that have IPs of 192.168.2.10 and 192.168.2.11), how do we get our first network to be able to talk to? A router...

Since the router connects to the two separate networks, it gets two IPs assigned - to correctly deliver packets, it needs to know where to "route" the traffic. This is where the gateway comes in...

## Gateway

To see the routes our kernel knows of, run the `route` command.

```shell-session
$ route

Kernel IP routing table

Destination   Gateway   Genmask   Flags Metric Ref   Use Iface
```

Currently, system B will not be able to reach system C (because it only knows about its own network - 192.168.2.0 (Iface))

To configure a gateway on system B so that it can talk to system C we can use the following command:

`ip route add 192.168.2.0/24 via 192.168.1.1`

If we run `route` again we'll see our update routes... However, this needs to be configured for every system (e.g. each needs its own route entry).

Suppose these systems need access to the internet e.g. Google at 172.217.194.0 you can add another route. But this doesn't work with the sheer amount of websites your router isn't aware of...

Instead you can assign a route `ip route add default via 192.168.2.1` meaning that any request to outside of your existing network goes to this particular router. Instead of default you could also add `0.0.0.0` aka any destination.

However, if you have two routers (one for your internal network, and one for the wider internet), you'll need to have two separate entries in each network - one entry for the internal private network, and another 









