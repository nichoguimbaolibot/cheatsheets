Switch
- To connect networks within the IP range.

Router
- connect two network with different IP ranges by connecting it to their switches
- But in order for a router to connect to a two different IP ranges you need to setup a gateway to the routing table.
To do that this is the commands:

    A(eth0)-----------switch-----------B(eth0)                  C(eth0)------------switch--------------D(eth0)
192.168.1.10        192.168.1.0                                192.168.2.10       192.168.2.0         192.168.2.11
                        |                                                            |
                        |          192.168.1.1                                       |
                        -----------------------------router---------------------------
                                                       |
                                                       |
                                                       |
                                                    internet
                                                  172.217.194.0


```bash
route #to view the routing table

ip link #to list and modift interfaces
ip addr # to see ip addreses

ip addr add 192.168.1.10/24 dev eth0 #to set an ip to the interface

ip route add 192.168.2.0/24 via 192.168.1.1 #add entries to the routing table

cat /proc/sys/net/ipv4/ip_forward #to check if ip forwarding is enable

echo > 1 /proc/sys/net/ipv4/ip_forward #to enable ip_forward

/etc/sysctl.conf #to persist the changes for enabling ip_forward

ip route add 192.168.2.0/24 via 192.168.1.1 # this will connect two different networks
ip route add 192.168.1.0/24 via 192.168.2.1 # this will connect two different networks
ip route add 172.217.194.0 via 192.168.2.1 # in order to connect to the internet
# but there is an easy way you can use this to automatically connect all of the networks and the internet
ip route add default via 192.168.2.1
```

# DNS

```bash
#in order to redirect the managing of the dns
cat /etc/resolv.conf
nameserver ${ip_address_of_dns} #e.g. 192.168.1.100
search mycompany.com #this will append if you `ping web` then it will ping web.company.com automatically
```

Record Types
A is for ip address
AAAA is for ipv6
CNAMES is for hostnames like web.company.com, eat.company.com

Other alternative for `ping` is `nslookup`

nslookup - only queries to the dns server