# devops-notes - Linux Networking

> Personal DevOps learning notes covering Linux, networking, SSH, backend deployment practices and others as needed.

Basic Linux networking CLI commands.

---

### Note: `<value>` represents a variable to be replaced with actual value

## Interfaces - <i>ip link</i>

---


```bash
ip link show                                                          # See all interfaces.

ip link show <interface-name>                                         # See a specific interface
                                                                      # example: ip link show eth0

sudo ip link set <interface-name> up                                  # Bring an interface up.

sudo ip link set <interface-name> down                                # Bring an interface down.

sudo ip link set <old-name> name <new-name>                           # Rename an interface.
```

## IP addresses - <i>ip addr</i>

---


```bash
ip addr show                                                          # See all IP addresses.

ip addr show <interface-name>                                         # See a specific interface
                                                                      # example: ip addr show eth0

sudo ip addr add <ip-addr>/<prefix-len> dev <interface-name>          # Add an ip address.
                                                                      # example: ip addr add 10.10.10.1/24 dev eth0

sudo ip addr del <ip-addr>/<prefix-len> dev <interface-name>          # Remove an ip address.
                                                                      # example: ip addr del 10.10.10.1/24 dev eth0

```

## Routing - <i>ip route</i>

---


```bash
ip route                                                              # Show routing table.

ip route get <ip-address>                                             # Show how the system would route to <ip-address>

sudo ip route add <ip-addr>/<prefix-len> \
      via <next-hop-ip> dev <interface-name>                          # Add a route.
                                                                      # example: sudo ip route add 172.16.50.0/24 \
                                                                      # via 10.10.10.1 dev eth0

sudo ip route del <ip-addr>/<prefix-len> \
      via <next-hop-ip> dev <interface-name>                          # Delete a route.

```

## ARP/Neighbour table - <i>ip neigh</i>

---


```bash
ip neigh                                                              # Show neighbours.

ip neigh show dev <interface-name>                                    # See a specific interface
                                                                      # example: ip neigh show dev eth0

```

## Network namespaces - <i>ip netns</i>

---


```bash
ip netns list                                                         # List namespaces.

sudo ip netns exec <namespace> <command>                              # Run a command inside a namespace.
                                                                      # example: sudo ip netns exec router2 ip route
                                                                      # example: sudo ip netns exec router2 bash
                                                                      
sudo ip netns add <namespace>                                         # Create a network namespace.
                                                                      # example: sudo ip netns add router2
                                                                      
sudo ip netns del <namespace>                                         # Delete a network namespace.
                                                                      # example: sudo ip netns del router2

```

## Virtual Ethernet - <i>ip link</i>

---


```bash
sudo ip link add <one-end> type veth peer name <other-end>            # Create a virtual ethernet pair.
                                                                      # example: sudo ip link add veth-r1 type veth \
                                                                      #             peer name veth-r2

                                                                      
sudo ip link set <veth> netns <namespace>                             # Move one end into a namespace.
                                                                      # example: sudo ip link set \
                                                                      #           veth-r2 netns router2

```

## Virtual Bridge - <i>ip link</i>

---


```bash
sudo ip link add <iterface-name> type bridge                          # Create a virtual bridge.
                                                                      # example: sudo ip link add br-dhcp type bridge

                                                                      
sudo ip link set <interface-name> master <bridge-name>                # Attach an interface to bridge.
                                                                      # example: sudo ip link set \
                                                                      #           veth-r1 master br-dhcp
                                                                      
ip link show <bridge-name>                                            # See bridge information.
                                                                      # example: ip link show br-dhcp
                                                                      
sudo ip link set <interface-name> nomaster                            # Detach <interface-name> from the bridge.
                                                                      
bridge link                                                           # Show which interfaces belong to bridges.

```

## Packet capture - <i>tcpdump</i>

---


```bash
sudo tcpdump -ni eth0                                                 # Capture on an interface.

sudo tcpdump -ni wlan0                                                # Capture on wi-fi.

sudo tcpdump -ni eth0 icmp                                            # Capture ICMP on eth0.

sudo tcpdump -ni eth0 -e                                              # Show ethernet MAC addresses.

sudo tcpdump -ni eth0 -e -vvv                                         # More verbose.

sudo tcpdump -ni eth0 -e -vvv 'icmp'                                  # More verbose.
                                                                      # -n          don't resolve names
                                                                      # -i eth0     capture eth0
                                                                      # -e          show ethernet headers/MACs
                                                                      # -vvv        very verbose
                                                                      # 'icmp'      only ICMP

```

## TCP connections - <i>ss</i>

---


```bash
ss -lnt                                                 # Show listening TCP ports.

sudo ss -lntp                                           # Show listening TCP + process.

sudo ss -lntup                                          # Show listening TCP + UDP + process.

```

## System/Network Configuration - <i>sysctl</i>

---


```bash
sudo sysctl -w net.ipv4.ip_forward=1                    # Enable IPv4 forwarding.
                                                        # 1 = enabled, 0 = disabled

cat /proc/sys/net/ipv4/ip_forward                       # Check ip forwarding status.

```


## Firewall/NAT - <i>nft</i>

---


```bash
sudo nft list ruleset                                   # Display complete rule set.

```
