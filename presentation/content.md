# Hand's On Public Cloud
part 1 : OVH



## Public Cloud ?

* *"Service over network, open for public use"*
* Mutualized infrastructure
* Virtualization layers
* IaaS
* Isolation mechanisms



## OVH
### Innovation is freedom


### History

* Founded in 1999
* By Octave Klaba : aka _@olesovhcom_
* Headquarters: Roubaix
* Rennes office since dec. 2014
  * R&D
  * Operations/Run
  * Dev


### Key numbers

* Third internet hosting company in the world !
  * 260,000 servers
  * 20 datacenters
  * 17 countries
  * 18M web applications hosted
  * 190,000 VOIP accounts
  * 1M customers



## OVH's Public Cloud


### Products

* Compute
* Object storage - swift
* Cold storage solution


### Sizing

* March  2017
  * \>150,000 running instances (*VM*)
  * \>100 petabytes

and counting...


### Based on…

* *OpenStack*
* *KVM* Hypervisors
* Modified *Neutron* network components
* Multi-datacenters
* Private networking with *vRack* technology



## Ok? Go !


### What was already prepared ?

* OVH account
  * Used for billing considerations
* Project creation
  * virtual wrapper for VM management
* OpenStack credentials
  * Randomized creation


### Our targets

1. Create an instance from GUI access
2. Create an instance from command line
3. Discover...


### Prerequisites

* A web browser (common...)
  * https://horizon.cloud.ovh.net/
  * Username :
  * Password :
* A SSH client (ex: [www.putty.org](http://www.putty.org))
* A SSH key pair : `ssh-keygen` or  `puttygen.exe`


### Key pair

1. Compute/Access & security
2. Import Key Pair
3. Give it a name: *your name*
4. Copy **public** part of your key



## VM from GUI


## VM from GUI (1)

1. Compute/Instances
1. **Launch instance**
1. Details
  * Instance Name: *your choice*
  * Gabarit: *s1-2* (smallest)
  * NB: *1*
  * Source: *Image*
  * Image Name: *Ubuntu 16.04*


## VM from GUI (2)

1. Access & security
  * Key pair: *Your key pair*
  * Security group: *default*
1. Networking
  * Selected network: *Ext-Net*
1. Post-creation
  * Script source: *Direct Input*
  * Script data: content of http://goo.gl/aazdad
1. **Launch** !


### Connect to your instance

* **Linux**: ```ssh ubuntu@<instance's IPv4>```
* **Windows**: Putty
  * Hostname : *&#60;instance's IPv4&#62;*
  * Connection/ssh/Auth : *Your private key file*
  * Open
    * Username : *ubuntu*



## New instance from CLI


### Jump server

* Already set up :
  * small docker containers
  * openstack tools installed
  * an SSH server daemon

➜ That's your **jump server** !

```ssh root@XXXXXXXX -p PORT```

Where **port** is between *50001* and *50030*


### OpenRC file

Project-specific environment file that contains the credentials that all OpenStack services use.

* Can be downloaded from Horizon
  * Compute/Access & security/API access
* **Already prepared on jump server !**
