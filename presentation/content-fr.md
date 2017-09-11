# Hand's On Public Cloud
part 1 : OVH



## Hands On ?
### *« Learn quick by practice »*

* Introduction courte (~10m)
* Travaux pratiques (~30m)
* Fun ➜ N'hésitez pas à contribuer à ce point **☺**
* BYOD *(Bring your own device)*
* Déjeuner


## Slides

* Sur GitHub: https://goo.gl/uPZhoL



## Public Cloud ?

* *"Service over network, open for public use"*
* Infrasructure **mutualisée**
* Couche de **Virtualisation**
* IaaS
* Méchanismes d'isolation
* Paiement à l'usage


## Acteurs

* Amazon Web Services
* Google Compute Engine
* OVH Public Cloud
* Microsoft Azure
* Digital Ocean
* Rackspace
* IBM Softlayer
* …



## ![OVH Logo](./images/logo-ovh.png)<!-- .element: height="200px" -->
### *Innovation is freedom*


### Historique

* Fondée in 1999
* Par Octave Klaba : aka [@olesovhcom](https://twitter.com/olesovhcom) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->
* Siège: Roubaix
* Bureaux à Rennes depuis déc. 2014
  * R&D
  * Operations/Run
  * Dev


### Chiffres clés

* 3ème hébergeur mondial !
  * 260 000 serveurs
  * 20 datacenters
  * 17 pays
  * 18M applications web hébergées
  * 190 000 comptes VOIP
  * \>1M clients



## Public Cloud OVH


### Produits

* Compute
* Object storage - swift
* Archivage : Cold storage


### Quelle taille ?

* Juillet  2017
  * \>175 000 instances UP (*VM*)
  * 6 500 hosts
  * 15 régions
  * \>100 petabytes de stockage

and counting…


### Basé sur…

* *OpenStack*
* Hyperviseurs *KVM*
* Module réseau *Neutron* modifié
* Multi-datacenters
* Réseau privé : technologie *vRack* interne



## Ok? Go !


### Qu'est ce qui a été préparé ?

* Compte client OVH
  * Utilisé notamment pour le paiement
* Création d'un projet
  * Enveloppe virtuelle pour les VM (quotas)
* Login OpenStack
  * Création '*random*'


### Serveur de rebond

* Conteneurs Docker
* Déjà installé :
  * Outils OpenStack python CLI
  * Serveur SSH

➜ Ce sont vos **serveurs de rebond** !

`ssh root@XXXXXXXX -p PORT`

Où **PORT** est compris entre *50001* et *50030*

**Password:** `ostools@`


### Couple de clés

* Déjà générés sur les rebonds
* Partie **publique** déjà enregistrée sur le projet
* Remplacera le couple login/mot de passe sur les VM


### Pré-requis divers

* Web browser
  * https://horizon.cloud.ovh.net/
  * Username & Password : `cat credentials.txt` sur le rebond
* SSH client
  * Windows - ex: [www.putty.org](http://www.putty.org))
  * Linux - ex: `openssh-client`


### Nos objectifs

1. Créer une instance via le portail Web
2. Créer une instance via la command line
3. Découvrir…



## Portail Web


## VM via le portail Web (1)

1. Compute/Instances
1. **Launch instance**
1. Details
  * Instance Name: *YOUR_NAME-1*
  * Flavor: *s1-2* (smallest)
  * Count: *1*
  * Boot source: *Boot from image*
  * Image Name: *Ubuntu 16.04*

***Ne pas valider à ce stade !***


## VM via le portail Web (2)

1. Access & security
  * Key pair: *HandsOnKey*
  * Security group: *default*
1. Networking
  * Selected network: *Ext-Net*
1. Post-creation
  * Script source: *Direct Input*
  * Script data: Copier le **contenu** de https://goo.gl/eYNSz6
1. **Launch** !


### Se connecter à l'instance

* Depuis le **serveur de rebond**:
```bash
$ ssh ubuntu@INSTANCE_IPV4
ubuntu@YOUR_NAME $ echo HELLO WORLD !
```

* Go root:
```bash
ubuntu@YOUR_NAME $ sudo su
root@YOUR_NAME #
```


### Tester la post-configuration

* Depuis le portail Web Horizon
  * Explorer les derniers logs de l'instance
* Depuis votre navigateur Web
  * [http://<instance's IPv4>](http://<instance's IPv4>)



## Nouvelle instance en CLI


### Serveur de rebond

Restez connectés sur votre **serveur de rebond**


### Fichier OpenRC

*Fichier propre à un projet, qui contient les variables d'environnement utilsées par OpenStack*

* Téléchargeable depuis le portail Horizon
  * ➜ Compute/Access ➜ security/API access
* **Déjà préparé sur votre serveur de rebond ☺**
* Sourcer le fichier:
`. ~/openrc.sh`


### Lister les pré-requis

* Lister les images disponibles:
`openstack image list`
* Lister les réseaux disponibles:
`openstack network list [--fit-width]`


### Création de l'instance

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


### Informations sur l'instance

Découvrez les détails de votre instance:
```bash
openstack server list
openstack server show <<<YOUR_NAME>>>-2
openstack console log show <<<YOUR_NAME>>>-2
openstack console url show <<<YOUR_NAME>>>-2
```


### Se connecter à l'instance

* Récupérer le status et l'IP de l'instance:
```bash
openstack server show <<<YOUR_NAME>>>-2
```

* Quand vous l'avez :
```bash
ssh ubuntu@INSTANCE_IPV4
ubuntu@YOUR_NAME $ echo HELLO WORLD !
```



## Approfondir


### openrc.sh

* Comment fonctionne le fichier `openrc.sh` ?
```bash
cat ~/openrc.sh
```
* Quel est le résultat du "sourçage" du fichier?
```bash
env | grep OS
```

**Question**: Après avoir sourcé le fichier, êtes vous connecté au Public Cloud OVH ?


### Client OpenStack

* Package Ubuntu : `python-openstackclient`
* Explorer les possibilités:
```bash
openstack help
```


### Tokens temporaires

* Il est possible de remplacer le couple login/password
* Génération d'un token temporaire:
```bash
openstack token issue
```

**Question**: Combien de temps ce token est-il valable?


### All is API !

* La gestion OpenStack se réalise à travers des requêtes HTTP(s)
  * Le Public Cloud OVH aussi:
```
curl -s -H "X-Auth-Token: <<<YOUR TOKEN ID>>>" \
  https://$HO_IMAGES_URI | jq
```

**Question**: Serez vous capables de lister les gabarits, instances, réseaux ?

**Tip**: `env | grep HO`



## Questions ?


## Remerciements

* **OVH** public cloud team: [@ovh](https://twitter.com/ovh) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->/ [ovh.com](https://www.ovh.com)
  * Arnaud ‐ [@MangerDuChien](https://twitter.com/MangerDuChien) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->/ [arnaudmorin.fr](http://www.arnaudmorin.fr/)
  * Pierre ‐ [@pierre_libeau](https://twitter.com/pierre_libeau) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->
* **SII** Ouest: [@sii_ouest](https://twitter.com/sii_ouest) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" -->/ [rennes.groupe-sii.com/fr](http://rennes.groupe-sii.com/fr)
  * Ludo ‐ [@lrivallain](https://twitter.com/lrivallain) ![twitter](images/logo-twitter.png)  <!-- .element: class="twitter-logo" --> / [lri.ovh](https://lri.ovh/)
