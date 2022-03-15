---
layout: default
title: Introduction to Networking
parent: CCNA
---

# Introduction to Networking

## Local/Global Addressing 

| Method |    Example     |
| :----: | :------------: |
| Media  |   Air/Wires    |
| Local  |      Name      |
| Global |   Phone No.    |
|  Cues  | Setup/Teardown |
|  Data  |  Conversation  |

## Categorizing Data Transmission

| Method |        Example         |
| :----: | :--------------------: |
| Media  |   Wires/Radio/Glass    |
| Local  |        Ethernet        |
| Global | Internet Protocol (IP) |
|  Cues  |          TCP           |
|  Data  |     Website/Email      |

## The OSI Model

|    Layer    |      Example      |
| :---------: | :---------------: |
|  Physical   | Wires/Radio/Glass |
|  Data Link  |     Ethernet      |
|   Network   | Internet Protocol |
|  Transport  |        TCP        |
| Application |   Website/Email   |

## OSI Model vs. TCP/IP Model

|      TCP/IP       |                    OSI                     |
| :---------------: | :----------------------------------------: |
| Network Interface |          Physical<br />Data Link           |
|     Internet      |                  Network                   |
|     Transport     |                 Transport                  |
|    Application    | Session<br />Presentation<br />Application |

## Encapsulation

How a website makes its way to the end user.

### 7. Application 

A website is broken into chunks to be sent across the network.

### 4. Transport

**Segment** - a chunk of data with a transport layer header.

The **Packet** in this **Segment** is the chunk of data produced from the Application Layer.

| Source Port | Dest Port | Flags | Seq# | Ack# | Packet |
| ----------- | --------- | ----- | ---- | ---- | ------ |
|             |           |       |      |      |        |

### 3. Network

**Packet** - a chunk of data with a network header.

The **Segment** in this **Packet** is received from the Transport Layer.

| Source IP | Dest IP | TTL  | Other | Segment |
| --------- | ------- | ---- | ----- | ------- |
|           |         |      |       |         |

### 2. Data Link

**Frame** - a chunk of data with a data link header.

The **Packet** in this **Frame** is received from the Network Layer.

| Dest MAC | Source MAC | Layer 3 Protocol | Packet |
| -------- | ---------- | ---------------- | ------ |
|          |            |                  |        |

### 1. Physical

Signals then transmits the Frame across the network.

## Addressing the Network

![Home Network Diagram](/assets/images/CCNA/home-network-diagram.jpg)

### Data Link Layer (Network Interface)

#### Layer 2

Keywords:

- Frame
- MAC addresses 
- Local Communication

NIC: 

Frame -> Signal, 

Signal -> Frame

### Network Layer (Internet)

#### Layer 3

Keywords:

- IP address
- Routers

![Router Diagram](/assets/images/CCNA/router-diagram.jpg)

