---
layout: default
title: Ethernet Operation and Switch Configuration
parent: CCNA
nav_order: 4
---

# Ethernet Operation and Switch Configuration

## Physical Layer Technologies

### Twisted Pair

| Category | Application               |
| -------- | ------------------------- |
| Cat 1    | Doorbell                  |
| Cat 2    | Token Ring                |
| Cat 3    | Telephone/10Mbps Ethernet |
| Cat 4    | Token Ring                |
| Cat 5    | 100Mb Ethernet            |
| Cat 5e   | Gigabit Ethernet          |
| Cat 6    | Gigabit Ethernet          |

### EIA/TIA-568-B

![EIA/TIA-568-B](/assets/images/CCNA/eia-tia-568-b.jpg)

![EIA/TIA-568-B Colors](/assets/images/CCNA/eia-tia-568-b-colors.jpg)

### When to Use a Crossover

You use a crossover cable when you connect two devices of the same type.

![Crossover Cable](/assets/images/CCNA/crossover-cable.jpg)

### Fiber Optics

![Fiber Optic Cable Types](/assets/images/CCNA/fiber-optic-types.jpg)

![Single Mode vs. Multi-Mode](/assets/images/CCNA/single-mode-multi-mode.jpg)

- Multi-mode (orange) is used to connect switches within the same building. 
- Single-mode (yellow) connects the two sites together due to its longer range.

### The Electromagnetic Spectrum

![EMS Diagram](/assets/images/CCNA/ems-diagram.jpeg)

- Data network communication happens on roughly the same wavelength as Microwaves.

## Data Link Layer Technologies

### Ethernet

- Ethernet is one of the oldest protocols still working on the internet.

**IEEE - 802.3**

![IEEE - 802.3](/assets/images/CCNA/ieee-802.3.jpg)

**IEEE Wireless Ethernet Protocols**

![IEEE Wireless Ethernet Protocols](/assets/images/CCNA/ieee-wireless.jpg)

| Protocol | Description                                                  |
| -------- | ------------------------------------------------------------ |
| 802.11a  | - Uses 5.0 GHz spectrum ONLY<br />- Up to 54Mbps bandwidth<br />- Initially for enterprise use |
| 802.11b  | - Uses 2.4 GHz spectrum ONLY<br />- Up to 11Mbps bandwidth<br />- Initially for SOHO use |
| 802.11g  | - Uses 2.4 GHz spectrum ONLY<br />- Up to 54Mbps bandwidth<br />- Enterprise/SOHO |
| 802.11n  | - Uses 2.4 and 5.0 GHz spectrum<br />- Up to 300Mbps bandwidth<br />- Uses MIMO (multiple in-multiple out) |
| 802.11ac | - Uses 5.0 GHz spectrum ONLY<br />- Up to 1.3Gbps bandwidth<br />- MIMO and beamforming |

## Introduction to Ethernet

### CSMA/CD - Carrier Sense Multiple Access with Collision Detection

![CMSA/CD Diagram](/assets/images/CCNA/cmsa-cd.jpg)

- All these devices take turns to communicate.
- All devices hear about the message.
- This can cause a collision.

**Collision Domain**

- A group of networked devices that will simultaneously detect a voltage spike.

### Duplex and Speed

**Half duplex**

- One device communicates at a time.
- E.g. Walkie Talkie

**Full duplex**

- Two devices communicate at same time.
- E.g. Telephone

### Ethernet Speed

| Name              | Speed   |
| ----------------- | ------- |
| Ethernet          | 10Mbps  |
| FastEthernet      | 100Mbps |
| GigabitEthernet   | 1Gbps   |
| 10GigabitEthernet | 10Gbps  |
| 40GigabitEthernet | 40Gbps  |

- The bottom 3 speeds require **Full Duplex**.

### Ethernet II Frame

| Destination MAC Address | Source MAC Address | Type    | Data (Packet)  | FCS     |
| ----------------------- | ------------------ | ------- | -------------- | ------- |
| 48 bits                 | 48 bits            | 16 bits | MAX 1500 Bytes | 32 bits |

**Packet**

- From Network Layer - 3

**Type**

IPv4 - 0000 1000 0000 0000

Hex 0 8 0 0

IPv4 - 0x0800

IPv6 - 0x86DD

ARP - 0x0806

**FCS - Frame Check Sequence**

- This uses the Cyclical Redundancy Check (CRC) algorithm.
- It checks whether the sent & received frame contains the same values.
- If the values aren't the same, the frame gets thrown out.

## Ethernet Switching

### Network Topologies

- Bus
- Ring
- Star - we mainly use this topology in modern times.

**Collision Domain**

- With a star topology, all devices will stop sending traffic, wait and then resend traffic.

### Layer 2 Switch

**MAC Address Table**

![MAC Address Table](/assets/images/CCNA/mac-address-table.jpg)

- The MAC address table is continously updated as long as the interface is up and receiving frames.
- When an entry is missing from the table and a device attempts to make communication, the frame is flooded to all interfaces. When a frame is sent back from the receiving device, the switch will populate the table.

**Flooding**

When the destination MAC address of the frame is not in the MAC address table, the frame is sent out all active interfaces, except the receiving interface.

**Broadcast**

When the destination MAC address of the frame is all Fs, the frame is sent out all active interfaces, except the receiving interface.

**Broadcast Domain**
Group of networked devices which will receive a layer 2 broadcast message.

### Examine the MAC Address Table

```tcl
Switch > en
Switch# show mac address-table
```

- The command above lists all the MAC addresses it knows about.
- The output starts with statis entries specific to the device.

## Switch Configuration

### Switch Memory

![Switch Memory](/assets/images/CCNA/switch-memory.jpg)

- The NVRAM is a virtual NVRAM on the Flash.
- It was created like this to replicate similar behaviour to the routers.

### Switch Configuration with SSH

- Unlike a router, we can use a switch without configuration.
- Configuration allows SSH + VLAN.

**Initial Config**

```tcl
Switch> en
Switch#
Switch# conf t
Switch(config)# hostname Switch1
Switch1(config)# ip domain name pluralsight.com
Switch1(config)# banner motd #this is Ross's switch#
```

**Enable SSH**

```tcl
Switch1(config)# enable secret cisco
Switch1(config)# username ross secret cisco
Switch1(config)# crypto key generate rsa
Switch1(config)# ip ssh ver 2
Switch1(config)# service password-encryption
```

**Enable Password for Console**

```tcl
Switch1(config)# line con 0
Switch1(config-line)# password cisco
Switch1(config-line)# login
Switch1(config-line)# exit
```

**Enable Password for SSH**

```tcl
Switch1(config)# line vty 0 4
Switch1(config-line)# login
```

**Only SSH connection types**

```tcl
Switch1(config)# transport input ssh
Switch1(config)# exit
```

**Add IP address for SSH Purposes**

```tcl
Switch1(config)# interface vlan 1
! The following ip-address is used for SSH only.
Switch1(config-if)# ip address 10.0.0.5 255.255.255.0
Switch1(config-if)# no shutdown
Switch1(confif-if)# exit
Switch1(config)# exit
```

**Show and copy running-config**

```tcl
Switch1# show running-config
Switch1# copy running-config startup-config
! The following command should out a config.text file. This is the startup-config.
Switch1# show flash:
```

### Reset Password

1. Go into ROM monitor mode.

2. Initialise flash memory.

   ```tcl
   switch: flash_init
   ```

3. Rename `config.text`

   ```tcl
   switch: dir flash:
   switch: rename flash: config.text flash: config.bak
   switch: dir flash:
   ```

4. Boot switch

   ```tcl
   switch: boot
   ```

5. Rename `config.bak`
   ```tcl
   Switch# rename flash: config.bak flash: config.text
   Switch# show flash
   Switch# show startup-config
   ```

6. Copy `flash:/config.text running-config`

7. Change Password back

   ```tcl
   Switch1# config t
   Switch1(config)# enable secret cisco
   Switch1(config)# exit
   Switch1# copy running-config startup-config
   ```

### Upgrade the IOS

1. Check existing OS

   ```tcl
   Switch1# show flash
   ! OS files must end with a .bin
   ```

2. Upload IOS file

   ```
   Switch1# copy tftp flash
   ! You will have to enter the ip-address, filename and destination filename.

3. Boot new IOS

   ```tcl
   Switch1# show flash
   Switch1# conf t
   Switch1(config)# boot system flash:/{new os filename}
   Switch1# copy running-config startup-config
   Switch1# reload
   ```

4. Check OS version

   ```tcl
   Switch1# show version
   ```

Note: Typically we should check that the file has integrity. You can do this using the following command.

```tcl
Switch1# verify /md5 flash:/{new os filename}
```

