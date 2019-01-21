# TP3 - Plusieurs réseaux : routage statique

## I. Création et utilisation simples d'une VM CentOS :

### 1. Création :

Installation de la VM CentOS sur VirtualBox faite en cours ensemble.

### 2. Installation de l'OS

Installation de la VM CentOS sur VirtualBox faite en cours ensemble.

### 3. Premier boot

Installation de la VM CentOS sur VirtualBox faite en cours ensemble.

### 4. Configuration réseau d'une machine CentOS

- a : Prouver que nous avons internet sur la VM :

J'utilise la commande **curl**. Une réponse apparaît, je suis donc connectée à internet.

- b : Prouver que le PC et la VM communiquent :

J'effectue un **ping adresse IP du pc hôte sur la VM**. Une réponse apparaît, ils communiquent.

J'effectue un autre **ping adresse IP de la VM**. Une réponse apparaît, Ils communquent.

Le PC hôte et la Vm communiquent bien dans les deux sens.

- c : affichage de la table de routage et explication :

Pour afficher la table de routage on tape **ip route** sur la VM. 4 lignes apparaissent.

1ère ligne: Affiche le protocole utilisé, ici le protocole **DHCP**.

→ **default via 10.0.2.2 dev enp0s3 proto dhcp metric 100**

Cette première ligne définie la carte réseau permettant d'accéder au réseaux auquels la machine n'est pas directement connectés, la carte qui renvoit à la passerelle. 
Ici **"dhcp"** signifie que la passerelle utilisé est celle donnée automatiquement par le serveur dhcp.

→ **10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100**
Cette deuxième ligne indique à la machine que pour accéder à ce précis (ici 10.0.2.0/24) il faut utiliser le lien (carte réseau physique, carte réseau virtuelle ou autre dans certains cas) ayant telle adresse IP (ici 10.0.2.15).

→ **192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101**
Là il s'agit de la même chose que la ligne précedente mais pour le réseau 192.168.127.0/24 via l'adresse 192.168.127.10.
### 5. Faire joujou avec quelques commandes

- ping :
    - ping hôte → VM : ping 127.0.0.1
    - ping VM → hôte : ping 10.33.2.248
- afficher la table de routage :
    - de l'hôte : route print
    - de la VM : ip route
- ligne qui leur permet de discuter via le réseau host-only:
    - hôte : 127.0.0.1  255.255.255.255  On-link  127.0.0.1  331
    - VM : 192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101
- commande dig sur la VM :
dig Nous permet de trouver l'adresse ip d'un site internet
    - pour **ynov.com
