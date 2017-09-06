# Hand's On Public Cloud
part 1 : OVH



## Hands On ?
### *« Learn quick by practice »*

* Short introduction (~10m)
* Practical work (~30m)
* Fun ➜ Feel free to contribute to this point **☺**
* BYOD *(Bring your own device)*
* Lunch



## Public Cloud ?

* *"Service over network, open for public use"*
* **Mutualized** infrastructure
* **Virtualization** layers
* IaaS
* Isolation mechanisms
* Usage billing


## Actors

* Amazon Web Services
* Google Compute Engine
* OVH Public Cloud
* Microsoft Azure
* Digital Oceam
* Rackspace
* IBM Softlayer
* …



## ![OVH Logo](./images/logo-ovh.png)<!-- .element: height="200px" -->
### *Innovation is freedom*


### History

* Founded in 1999
* By Octave Klaba : aka [@olesovhcom](https://twitter.com/olesovhcom) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->
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
  * \>175,000 running instances (*VM*)
  * 6500 hosts
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
  * SSH server daemon

➜ That's your **jump server** !

`ssh root@XXXXXXXX -p PORT`

Where **PORT** is between *50001* and *50030*

**Password:** `ostools@`


### Key pair

* Already generated for jump server
* **Public** part already registered on project
* Will replace login/password on first login on VM


### Other prerequisites

* Web browser
  * https://horizon.cloud.ovh.net/
  * Username & Password : *please refer on white-board*
* SSH client
  * Windows - ex: [www.putty.org](http://www.putty.org))
  * Linux - ex: `openssh-client`


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
  * Flavor: *s1-2* (smallest)
  * Count: *1*
  * Boot source: *Boot from image*
  * Image Name: *Ubuntu 16.04*

***Do not validate yet !***


## VM from GUI (2)

1. Access & security
  * Key pair: *HandsOnKey*
  * Security group: *default*
1. Networking
  * Selected network: *Ext-Net*
1. Post-creation
  * Script source: *Direct Input*
  * Script data: copy **content** of https://goo.gl/eYNSz6
1. **Launch** !


### Connect to your instance

* From **jump server**:
```bash
$ ssh ubuntu@INSTANCE_IPV4
ubuntu@YOUR_NAME $ echo HELLO WORLD !
```

* Go root:
```bash
ubuntu@YOUR_NAME $ sudo su
root@YOUR_NAME #
```


### Test post-configuration

* From Horizon portal
  * Check instance's logs
* From your Web browser
  * [http://<instance's IPv4>](http://<instance's IPv4>)



## New instance from CLI


### Jump server

Stay connected to the **jump server**


### OpenRC file

*Project-specific environment file that contains the credentials that all OpenStack services use.*

* Can be downloaded from Horizon
  * ➜ Compute/Access ➜ security/API access
* **Already prepared on jump server !**
* Source it:
`. ~/openrc.sh`


### List prerequisites

* List available images
`openstack image list`
* List available networks
`openstack network list [--fit-width]`


### Server create

```bash
openstack server create \
        --flavor "s1-2" \
        --image "Ubuntu 16.04" \
        --key-name HandsOnKey \
        --nic net-id=<<<NETWORK ID>>> \
        --security-group default \
        --wait \
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

* When ready :
```bash
ssh ubuntu@INSTANCE_IPV4
ubuntu@YOUR_NAME $ echo HELLO WORLD !
```



## Dig it


### openrc.sh

* How does the openrc.sh file works ?
```bash
cat ~/openrc.sh
```
* What the effect of sourcing it ?
```bash
env | grep OS
```

**Question**: When you source it, are you actually connected to the OVH cloud platform ?


### OpenStack client

* Ubuntu package name : `python-openstackclient`
* Explore capabilities
```bash
openstack help
```

**Question**: When you source it, are you actually connected to the OVH cloud platform ?


### Temporary tokens

* Its possible to replace login/password
* Generate a token with credentials
```bash
openstack token issue
```

**Question**: How long can you use this token for?


### All is API

* OpenStack management is done through HTTP(s) API
  * so OVH Public Cloud too:
```
curl -s -H "X-Auth-Token: <<<YOUR TOKEN ID>>>" \
  https://$HO_IMAGES_URI | jq
```

**Question**: Will you be able to list flavors, servers, networks ?

**Tip**: `env | grep HO`



## Thanks

* **OVH** public cloud team: [@ovh](https://twitter.com/ovh) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->/ [ovh.com](https://www.ovh.com)
  * Arnaud ‐ [@MangerDuChien](https://twitter.com/MangerDuChien) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->/ [arnaudmorin.fr](http://www.arnaudmorin.fr/)
  * Pierre ‐ [@pierre_libeau](https://twitter.com/pierre_libeau) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->
* **SII** Ouest: [@sii_ouest](https://twitter.com/sii_ouest) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->/ [rennes.groupe-sii.com/fr](http://rennes.groupe-sii.com/fr)
  * Ludo ‐ [@lrivallain](https://twitter.com/lrivallain) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" --> / [lri.ovh](https://lri.ovh/)
