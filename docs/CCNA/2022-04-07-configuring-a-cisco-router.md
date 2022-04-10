---
layout: default
title: Configuring a Cisco Router
parent: CCNA
nav_order: 3
---

# Configuring a Cisco Router

## Cisco Router

![Cisco Router Labelled](/assets/images/CCNA/cisco-router-labelled.jpeg)

This is an example of what Configuration Ports look like on a Cisco Router.

It is important to note that the Console & Aux ports do not pass any networking traffic. These ports are only used for configuration and need to be connected using a rollover cable.

## Boot Process

### PC Boot Process

1. Power of Self Test
   - PC checks its hardware
2. Load BIOS from ROM
3. Load Operating System
4. Load Personal Settings
   - User authentication
   - Display background
   - Bookmarks, etc.

### Router Boot Process

The router boot process follows a similar process to the PC.

1. Power on Self Test
2. Load Bootstrap
   - BIOS
   - 'Kicks the router into action'
3. Load IOS (Operating System)
4. Load Configuration
   - startup-config file

## Cisco Router Files and Licensing

### Router Memory

- **EEPROM** stores Bootstrap
- **Flash** stores IO
  - This could either be on the board or a removable device.

- **NVRAM** (Non-volatile RAM) holds the `startup-config`
- **RAM** holds the `running-config`
  - All our config is stored here.
  - Typically, we make a copy of the `running-config` to the **NVRAM**. This is to ensure that our change sticks and the config is run on next boot.

### Internetworking Operating System

This is the OS used by Cisco devices.

**Platform**

- Router
- Layer 3 Switch
- Switch
- Model Number

**Trains** - Major Releases

This can be thought of as the same as releases of Windows 7,8,10,11.

12.2-12.4 - 15.0 -15.1

**Throttles** - Minor Releases

These are smaller releases, usually updating the major release.

12.2(10) - 12.4(20) - 15.0(1) - 15.1(3)

**Rebuilds**

Typically an update released to fix a bug.

12.2(10b) - 12.4(20)T3 - 15.0(1)M8 - 15.1(3)T2

**File Name Format**

**c1841-adventerprisek9-mz.124-24.T5.bin**

- **c1841** - Cisco 1800 Series Router model 1841
- **adventerprise9-mz** - Advance Enterprise Feature Set
- **124** - Train
- **24** - Throttle
- **T5** - Rebuild
- **Bin** - Binary File System

### IOS Licensing

To retrieve an IOS License for a Cisco Router, there are several steps involved. Typically, a person will buy a certificate from a **Cisco Value Added Reseller**. After retrieving this certificate, the person will that uplod this information to a **Cisco License Server**. The licensing server will then grant the person the key which unlocks the feature set that they purchased.

## Router Configuration

In basic terms, a router is used to route traffic from one network to another. This section covers the basic configuration required to setup a Cisco Router.

![Router Setup](/assets/images/CCNA/router-setup.jpg)

### CLI modes

**User mode**

```tcl
Router> 
```

**Privileged mode**

```tcl
Router#
```

**Global Configuration mode**

```tcl
Router(config)#
```

### Base Config

The following changes the router's hostname, domain name and motd (message of the day).

```tcl
Router(config)# hostname RossRouter
RossRouter(config)# ip domain-name pluralsight.com
RossRouter(config)# banner motd # 
Authorized Use Only! #
```

### Enable Password for User mode

```tcl
RossRouter> enable
RossRouter# conf t
RossRouter(config)# line console 0
RossRouter(config-line)# password cisco
RossRouter(config-line)# login
RossRouter(config-line)# line aux 0
RossRouter(config-line)# password cisco
RossRouter(config-line)# login
RossRouter(config-line)# exit
```

### Enable Password for Privilleged mode

```tcl
RossRouter> enable
RossRouter# conf t
RossRouter(config)# enable secret cisco
RossRouter(config)# exit
```

### Show Running Config

```tcl
RossRouter> enable
RossRouter# show running-config
```

### Make logging synchronous

This is used to allow you to continue typing your command, even after a log message appears.

```tcl
RossRouter# config t
RossRouter(config)# line con 0 
RossRouter(config-line)# logging sync
RossRouter(config-line)# line aux 0
RossRouter(config-line)# logging sync
RossRouter(config-line)# exit
RossRouter(config)# exit
```

### Configure SSH access

This gives you shell access to the router when you are unable to access it physically.

```tcl
RossRouter# conf t
RossRouter(config)# crypto key generate rsa general-keys
RossRouter(config)# ip ssh version 2
RossRouter(config)# username ross secret cisco
RossRouter(config-line)# transport input ssh
RossRouter(config-line)# login local
RossRouter(config-line)# logging sync
```

### Configuring an Interface

```tcl
RossRouter(config)# interface fastethernet 0/0
RossRouter(config-if)# ip address 10.0.0.1 255.255.255.128
RossRouter(config-if)# shutdown
! This command enables an interface (brings it up).
RossRouter(config-if)# no shutdown
```

### Save `running-config` to `startup-config`

```tcl
RossRouter# copy running-config startup-config
```

## Router Configuration with Shortcuts and IPv6

### Erase Startup-config and reload

```tcl
RossRouter> enable
RossRouter# show startup-config
RossRouter# erase startup-config
RossRouter# show startup-config
RossRouter# reload
```

### Configuration with Shortcuts

**List all available commands**

```tcl
Router> ?
```

**List all commands starting with the letter 'e'**

```tcl
Router> e?
```

Use the 'tab' key for auto-completion.

### Connecting to the Router via SSH

By default, when connecting to the router via SSH, it doesn't log console messages. To ensure console messages are logged, run the following command.

```shell
RossRouter# terminal monitor
```

**Don't cut your own arm off** - remember to never shutdown an interface (e.g. f0/0) via SSH. This makes the interface inaccessible, meaning you will loss connection to the router. The only way to remedy this is to be physically present to the router and connect directly.

### Adding IPv6n Address to the Router

![Cisco Router IPv6 Setup](/assets/images/CCNA/router-ipv6-config.jpg)

```tcl
RossRouter# conf t
RossRouter(config)# ipv6 unicast-routing
RossRouter(config)# int f0/0
RossRouter(config-if)# ipv6 address 2001:db8:4:A::1/64
RossRouter(config-if)# ipv6 address 2001:db8:4:B::1/64
RossRouter(config-if)# exit
RossRouter(config)# exit
```

## Upgrading IOS

### Preparing the Router for an IOS Upgrade

```tcl
RossRouter> en
RossRouter# show version
! This command checks the space left on the flash drive.
RossRouter# show flash
```

If there isn't enough space for the new OS, we'll have to delete the old one before proceeding with the upgrade.

### Transfer the IOS image to the Router

To transfer the IOS image to the Router, we need to have a TFTP (Trivial File Transfer Protocol) server setup with the files present. We can setup a TFTP server on our local machines using a client available online.

```tcl
RossRouter# copy tftp flash
```

### Verifying File Transfer and Booting the Router with New IOS image

```tcl
RossRouter# config t
RossRouter(config)# boot system flash:/c1841-advipservicesk9-mz.124-15.T8.bin
RossRouter(config)# exit
RossRouter(config)# copy run start
```

### Verifying the IOS Upgrade

```tcl
RossRouter# show ver
```

## Check Your Knowledge

### Interrupt Boot Process

When a Router is in the process of booting up, we issue a `break` command to interrupt the boot process. We might do this to alter the 'Configuration Register' which tells the Router what to do when it is booting up.

**Configuration Register**

0x2102 - 0010 0001 0000 0010

- The last four digits in the 'Configuration Register' is the 'Boot Fields'.
- In this register, the Boot Fields is set to Boot as configured in Boot System field in Startup-Config.

### Router Password Recovery

Typically, we want to interrupt the router's boot process when we need to reset the password. To recover the password for Cisco Router we have to follow these steps:

1. Shutdown the Router
2. Power the Router back on and issue the `break` command
3. The Router will now go into ROM monitor mode
4. Issue the command `confreg 0x2142` which tells the Router to ignore startup-config
5. Reset the Router
6. Elevate to Privilleged mode
7. `copy startup-config running-config`
8. Change password
9. Go back into configure mode - `conf t`
10. Issue the command `config-register 0x2102`, changing changes the 'Configuration Register' back to its original state
11. `copy run start`
12. We need to manually bring up the interfaces, as copying the running config to startup doesn't do this for us
    - `show ip interface-brief` - displays the statuses of the interfaces
    - `no shutdown` - brings the interface back up
13. `copy run start`

### Troubleshooting Boot Process

The following steps indicate how to go about erasing the flash memory on a Cisco Router.

1. Authenticate via serial

2. ```tcl
   RossRouter> en
   RossRouter# show flash
   ```

3. ```tcl
   RossRouter# erase flash:
   ```

4. ```tcl
   RossRouter# reload
   ```

If there is no IOS on the flash, the Router will have nothing to boot. To recover the IOS, you have several options depending on the model of the Router.

**Method 1**

If the Router has a removable flash card, you can remove that card and add files to it manually from a PC. After inserting the IOS on the card, you can insert back into the Router and it will boot the OS.

**Method 2**

Some models of Routers can use TFTP from ROM monitor mode, meaning you can copy the IOS files remotely. To determine if your router has this functionality, visit cisco.com.

**Other Options**

If you face this situation, the best option is to google for a solution. There should be plenty of options based on your Router's model.

### Useful IOS Show Commands

Show IOS version and Configuration Register

```tcl
RossRouter# show version
```

Show files on flash registry and available space

```tcl
RossRouter# show flash
```

Show state of all the Router's interfaces

```tcl
RossRouter# show ip interface brief
RossRouter(config)# do show ip interface brief
```

Show all details about an interface, e.g. MAC address, IP address, MTU, Bandwidth. Particularly useful when you need to investigate issues/erros with the interface.

```tcl
RossRouter# show interface f0/0
```

Prevent attempts to establist Telnet connection with supposed domain name entered. This stops your Cisco Router attempting to connect with a device when you have incorrectly typed a command.

```tcl
RossRouter(config)# no ip domain-lookup
```
