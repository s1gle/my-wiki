---
layout: default
title: Network Layer Addressing and Subnetting
parent: CCNA
---

# Network Layer and Subnetting

## Introduction to Binary

### Binary 101

Base 10 -> What we use in daily life.

Binary -> On(1)/Off(0)

### Converting Binary to Decimal

| 128's Place | 64's Place | 32's Place | 16's Place | 8's Place | 4's Place | 2's Place | 1's Place |
| :---------: | :--------: | :--------: | :--------: | :-------: | :-------: | :-------: | :-------: |
|      1      |     1      |     0      |     0      |     0     |     0     |     0     |     0     |
|    1*128    |    1*64    |    0*32    |    0*16    |    0*8    |    0*4    |    0*2    |    0*1    |

**128 + 64 = 192**

### Converting Decimal to Binary

Subtracting from each place must result in a positive or 0 value.

**Example: 210**

| 128's Place | 64's Place |          32's Place           | 16's Place |          8's Place          |          4's Place          | 2's Place |          1's Place          |
| :---------: | :--------: | :---------------------------: | :--------: | :-------------------------: | :-------------------------: | :-------: | :-------------------------: |
| 210-128=82  |  82-64=18  | Skip since 18-32 is negative. |  18-16=2   | Skip since 2-8 is negative. | Skip since 2-4 is negative. |   2-2=0   | Skip since 0-1 is negative. |
|      1      |     1      |               0               |     1      |              0              |              0              |     1     |              0              |

**Result: 11010010**

### Hexadecimal

| Binary | Hexadecimal | Decimal |
| :----: | :---------: | :-----: |
|  0000  |      0      |    0    |
|  0001  |      1      |    1    |
|  0010  |      2      |    2    |
|  0011  |      3      |    3    |
|  0100  |      4      |    4    |
|  0101  |      5      |    5    |
|  0110  |      6      |    6    |
|  0111  |      7      |    7    |
|  1000  |      8      |    8    |
|  1001  |      9      |    9    |
|  1010  |      A      |   10    |
|  1011  |      B      |   11    |
|  1100  |      C      |   12    |
|  1101  |      D      |   13    |
|  1110  |     14      |    E    |
|  1111  |     15      |    F    |

Every 4 digit Binary bits can be converted to Hexadecimal.

## Introduction to IP Addressing

**IP Address** - Identifier for a device on a network.

![IP Network and Host Portions](/assets/images/CCNA/ip-network-host.jpg)

### Classless Addressing (Post 1995)

|             IP Address              |             Subnet Mask             |
| :---------------------------------: | :---------------------------------: |
|            203.0.113.10             |            255.255.255.0            |
| 11001011 00000000 01110001 00001010 | 11111111 11111111 11111111 00000000 |

- The Subnet Mask classifies the Network and Host Portion of the IP Address.
- 255's identify the Network portion and 0's identify the host portion.
- It doesn't always have to be **255.255.255.0**.

### Classful Addressing (Pre 1995)

There were classes that IP addresses fell into that determined the Network and Host portion of the address.

![Classful Addressing](/assets/images/CCNA/classful-addressing.jpeg)

### Address Types

| Network Address                                       | Broadcast Address                                     | Host Address                            |
| ----------------------------------------------------- | ----------------------------------------------------- | --------------------------------------- |
| All binary 0's in the host portion of the IP address. | All binary 1's in the host portion of the IP address. | Anything except all binary 0's and 1's. |

**Host Address - Example**

|               IP Address                |               Subnet Mask               |
| :-------------------------------------: | :-------------------------------------: |
|              192.168.10.25              |              255.255.255.0              |
| 11000000 10101000 00001010 **00011001** | 11111111 11111111 11111111 **00000000** |

**Network Address - Example**

|               IP Address                |               Subnet Mask               |
| :-------------------------------------: | :-------------------------------------: |
|              10.128.224.64              |             255.255.255.224             |
| 00001010 10000000 11100000 010**00000** | 11111111 11111111 11111111 111**00000** |

**Broadcast Address - Example**

|               IP Address                |               Subnet Mask               |
| :-------------------------------------: | :-------------------------------------: |
|             192.168.10.255              |              255.255.255.0              |
| 11000000 10101000 00001010 **11111111** | 11111111 11111111 11111111 **00000000** |

### Private IP Address Range

|    From     |       To        |
| :---------: | :-------------: |
|  10.0.0.0   | 10.255.255.255  |
| 172.16.0.0  | 172.31.255.255  |
| 192.168.0.0 | 192.168.255.255 |

**127.0.0.1** -> Loopback Address

## Introduction to IPv6

Bit - 0 or 1

Nibble - 4 bits

Byte - 8 bits

Hextet - 16 bits

### IPv4 Address Size

32 bits long = 4 octets

192.168.10.10

### IPv6  Address Size

128 bits long = 32 nibbles = 8 hextets

2001:0DB8:0002:008D:0000:0000:00A5:52F5

### IPv6 Addresses

| Network Portion (64 Bits) | Interface Identifier (64 Bits) |
| ------------------------- | ------------------------------ |
| 2001:0DB8:0002:008D       | :0000:0000:00A5:52F5           |

**Eliminate Leading 0's**

| Network Portion (64 Bits) | Interface Identifier (64 Bits) |
| ------------------------- | ------------------------------ |
| 2001:DB8:2:8D             | :0:0:A5:52F5                   |

**Eliminate 0's with :: (Double Colon)**

| Network Portion (64 Bits) | Interface Identifier (64 Bits) |
| ------------------------- | ------------------------------ |
| 2001:DB8:2:8D             | ::A5:52F5                      |

### IPv6 Addresses Operation

Similar to IPv4, the network portion of the address must be the same for two devices to communicate.

![IPv6 Operation](/assets/images/CCNA/ipv6-operation.jpg)

### IPv6 unicast addresses

Unicast address represents a single interface. Packets addresses to a unicast address will be delivered to a specific network interface.

- **global unicast** - similar to IPv4 public IP addresses. These addresses are assigned by the IANA and used on public networks.
- **unique local** - similar to IPv4 private address. They are used in private networks and aren't routable on the Internet. They start with FC or FD.
- **link local** - these addresses are used for sending packets over the local subnet. Routers do not forward packets with this addresses to other subnets. IPv6 requires a link-local address to be assigned to every network interface on which the IPv6 protocol is enabled. These addresses have a prefix of FE80::/10.

### How many IPv6 Addresses

2<sup>64</sup> = 18,446,744,073,709,600,00

For EACH IPv6 Network!

### IPv6 Address Acquisition SLAAC

IPv6 Stateless Address Autoconfiguration or SLAAC allows devices on a network to automatically configure IPv6 addresses on its interface without managing a DHCP server.

1. Learn the IPv6 prefix used on the link, from any router, using NDP RS/RA messages.
2. Build an address from the prefix plus an interface ID, chosen either by using EUI-64 rules or as a random value.
3. Before using the address, first determine that no host is already using the same address.

### IPv6 Address Acquisition DHCP

To find an address with DHCP, the DHCP client sends messages to a DHCP server, and the server assigns a currently unused address in the correct subnet for the endpoint host to use. The proces relies on DHCP client functions in each device and a DHCP server configured and working in the network.

## IPv6 Subnetting

### IPv4 Address and Mask

32 bits long = 4 octets

|                  | Address         | Network Prefix                | Host Portion |
| ---------------- | --------------- | ----------------------------- | ------------ |
| **Host Address** | 192.168.10.10   | 11000000 10101000 00001010 00 | 001010       |
| **Subnet Mask**  | 255.255.255.192 | 11111111 11111111 11111111 11 | 000000       |

### IPv6 Mask

| Network Prefix      | Interface Identifier |
| ------------------- | -------------------- |
| 2001:0DB8:0002:008D | :0000:0000:00A5:52F5 |

**/64** used for individual network segments.

### Subnetting IPv6

Initially, the ISP obtains the IPv6 address from IANA regional registry.

![IPv6 Subnetting ISP](/assets/images/CCNA/ipv6-subnetting-1.jpg)

Next, they make use of the next 8 bits, after the network prefix to allocate IPv6 addresses.

![ipv6-subnetting-2](/assets/images/CCNA/ipv6-subnetting-2.jpg)

Those addresses then get assigned to their clients.

![ipv6-subnetting-3](/assets/images/CCNA/ipv6-subnetting-3.jpg)

The address assigned to the client then gets further broken down based on the number of networks they need for each region.

![ipv6-subnetting-4](/assets/images/CCNA/ipv6-subnetting-4.jpg)

Since, the first 48 bits is assigned by the ISP (and cannot be changed); the last 16 bits can be used for assigning network addresses to each of the regions.

![ipv6-subnetting-5](/assets/images/CCNA/ipv6-subnetting-5.jpg)

![ipv6-subnetting-6](/assets/images/CCNA/ipv6-subnetting-6.jpg)

After the networks have been assigned to each region, each address can be further broken down to encompass the cities within those regions.

![ipv6-subnetting-7](/assets/images/CCNA/ipv6-subnetting-7.jpg)

### Basic Router Operation

A router is a networking device that forwards data packets between multiple networks. This is a different to a switch, whereby, it only facilities communication within the same network.

For example, imagine we would like to send a `ping` message from our computer to a server on another network.

First, after running the command, the `ping` message gets encapsulated in a packet with the host and destination address.

![router-operation-1](/assets/images/CCNA/router-operation-1.jpg)

The packet then gets encapsulated into a frame, which is a layer 2 carrier for our packets. It contains the host (PC) and destination (default gateway) MAC address.

![router-operation-2](/assets/images/CCNA/router-operation-2.jpg)

Once the frame reaches the default gateway, it strips away the frame and encapsulates the packet into a new frame. The new frame has the source MAC address of the 10.0.0.129 interface and a destination MAC address of the server.

![router-operation-3](/assets/images/CCNA/router-operation-3.jpg)

Once the frame reaches the server, it strips away the frame and packet, determining the `ping` message. After this, the process happens in reverse for server to send a `ping` reply back to the PC.

![router-operation-4](/assets/images/CCNA/router-operation-4.jpg)
