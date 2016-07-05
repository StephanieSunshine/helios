# Helios
A modern open source network router tailored for power users, families, and small offices.

# Purpose
This document serves as a brain dump of everything I've been mulling over for a while now.  This is a work in progress.  Some things listed might not even be possible at the moment.  This document is to serve as a launchpad to resolve what would be the most ideal configuration for a next generation router.  Later, this document will be moved into a wiki to enable easy collaboration.

# Problem
All software routers in the world suck.  Every single software router out there either is trying to do too much, trying to push you into their paid version, too bloated to be of any real use, looks like it hasn't been updated in 20 years, or is priced in such a way that makes you wonder what you are missing out on.  What irks me about so many of these "free*" routers is the soft limitations that are added to do nothing more than make money.  The last straw for me was WanOS.  I understand that they want to make money from this, but their "free" is completely unusable to me as a home user and to even consider their paid version with my current Internet connection would price it at roughly 1.5x what I'm paying.  No, just no.

I'm sick of it.  I've used and hacked on every little router hardware and software that I could get my hands on.  Nothing has been as stable, configurable, or expandable as a real server has been for me.  It's easy to understand why this is too, but the amount of resources that a router needs rarely eclipses a modern server.

Virtualization is here to stay.  Virtualized routers are wonderful things, abstract the real driver details away, just plug in and go.  Seems simple enough.  People like Sophos and Barracuda already have solutions, but once again, you start running into companies that are using soft limits to sell licenses when nothing is changing.

Does it make sense for a company that sells licenses off of cores and memory counts to use the most cycle and memory efferent methods?  No, it doesn't if they are in the business of making money and not making efficient routers.  A prime example of this is the Zentyal server.  So close, yet so far, it's literally a Mail and Directory server built on Ubuntu Desktop.

# Solution
I propose a new router, built with modern standards in mind.  A router that takes into account all of the software advancements of the last 25+ years.  A router that seamlessly integrates web acceleration, anonymous surfing, accounting and auditing, security, single sign on, network home folders, vpn, dynamic netbooting, and more.

# Requirements
This is to be a secure, fast, and dependable router.  Tools should be selected with security and speed in mind.  The idea of this router is to accelerate modern deployments using modern tricks.  OSv demonstrated that there is still a lot of potential left to be squished out of current virtualization using Kernel tricks.  Thus, Helios will be a project that focuses on supporting virtualized environments.  It could possibly run on bare metal, but the minor trade off in supported targets helps us focus the scope of the project.  I think it's wiser for a bare metal operating system that can be updated and cycled independently of the router to handle the low level driver stuff and then use exclusive bridges to bring in the interfaces.  This makes vlans, bonds, and bridge configurations independent of the router, thus simplifying the eco-system.


# Possible solutions

## General
### Distribution
Alpine Linux, either uclibc or musl hardened.  Leaning towards musl.

### Driver Support
Libvirtd
VMWare

### High Availability
Pacemaker

## Accountability
### Accounting
Route everything possible through the proxy to accelerate, dynamically route ( turn tor, vpn, or i2p on or off ), white list, black list, audit, using the centralized user directory

### Auditing & Metrics
Send everything into a DB like ES or Mongo

### Access Control Lists
Proxy should require someone to login with a user / password or an email as a "guest" ( if enabled )

## Low Level
### Routing
Linux Kernel

### DHCP
ISC-DHCPD

### NTP
NTPD

### DNS
Unbound

### Firewall

### QOS

### VPN
OpenVPN TFA

### Anonymous Routing
TOR
I2p

## High Level
### Certificate Server
### Forward Proxy
Apache Traffic Server

### IDS
AlienVault

### Anti Malware

### User Directory & Authentication
989 Directory Server maybe

### Network Home Folders
Samba
SSHFS

### Netbooting
Ipxe.  Http boot isos to install to local, or network targets.  Automatically generate and associate custom ipxe scripts per host as needed or a menu that allows the client to pick at boot time.

### SSH Mux
custom menu to allow ssh pass-through to a specific host or a menu to allow the client to pick which host they would like to jump too.  Should support agent and port forwarding.

### Other Tools
### GUI
Meteor.js using React on an open source Bootstrap 4 template.  Try to make as reactive and real-time as reasonably possible.
### CLI
Bash shell.
