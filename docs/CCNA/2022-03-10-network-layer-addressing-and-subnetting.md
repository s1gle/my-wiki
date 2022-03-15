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

![IP Network and Host Portions](/assets/images/CCNA/ip-network-host.png)

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
