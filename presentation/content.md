# Hand's On Public Cloud
part 1 : OVH



## Public Cloud ?

* *"Service over network, open for public use"*
* **Mutualized** infrastructure
* **Virtualization** layers
* IaaS
* Isolation mechanisms


## Actors

* Amazon Web Services
* Google Compute Engine
* OVH Public Cloud
* Microsoft Azure
* Rackspace
* IBM Softlayer
* …



## OVH
### *Innovation is freedom*


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

* July  2017
  * \>175,000 running instances (*VM*), on 6500 hosts
  * 15 regions
  * \>100 petabytes

and counting…


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


### Jump server

* Already set up :
  * small docker containers
  * OpenStack python CLI tools
  * (A SSH server daemon)

➜ That's our **jump server** !

```ssh root@XXXXXXXX -p PORT```

Where **PORT** is between *50001* and *50030*


### Key pair

* Already generated for jump server
* **Public** part already registered on project
* Will replace login/password on first login on VM


### Other prerequisites

* A web browser (common…)
  * https://horizon.cloud.ovh.net/
  * Username :
  * Password :
* A SSH client
  * Windows - ex: [www.putty.org](http://www.putty.org))
  * Linux - ex: ```openssh-client```


### Our targets

1. Create an instance from GUI access
2. Create an instance from command line
3. Discover…



## VM from GUI


## VM from GUI (1)

1. Compute/Instances
1. **Launch instance**
1. Details
  * Instance Name: *YOUR_NAME-1*
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

* From **jump server**: ```ssh ubuntu@<instance's IPv4>```
```bash
ubuntu@YOUR_NAME $ echo HELLO WORLD !
```

* Go root: ```sudo su```
```bash
root@YOUR_NAME #
```



## New instance from CLI


### Jump server

Stay connected to the **jump server**


### OpenRC file

*Project-specific environment file that contains the credentials that all OpenStack services use.*

* Can be downloaded from Horizon
  * ➜ Compute/Access ➜ security/API access
* **Already prepared on jump server !**
* Source it:
```bash
. ~/openrc.sh
```


### List prerequisites

* List available images
```bash
openstack image list
```
* List available networks
```bash
openstack network list
```


### Server create

```bash
openstack server create \
        --flavor "s1-2" \
        --image "Ubuntu 16.04" \
        --key-name handsonkey \
        --nic net-id=<<<NETWORK ID>>> \
        --security-group default \
        "<<<YOUR_NAME>>>-2"
```


### Server informations

Get more details about your instance(s):
```bash
openstack server list
openstack server show <<<YOUR_NAME>>>-2
openstack console log show <<<YOUR_NAME>>>-2
openstack console url show <<<YOUR_NAME>>>-2
```


### Connect to your instance

* Check instance state and get its IP:
```bash
openstack server show <<<YOUR_NAME>>>-2
```
* When ready : ```ssh ubuntu@<instance's IPv4>```
```bash
ubuntu@YOUR_NAME $ echo HELLO WORLD !
```
