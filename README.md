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
    
 ## II. Notion de ports et SSH    
    
### 1. Exploration des ports locaux

On va commencé par taper ss -4lnp,
Cela nous donne **sshh** ecoute sur le port 22 

### 2. SSH

On va commencer par l'installation de putty, suite a cela je rentre **l'ip de ma vm 192.168.127.10**, ssh par defaut. je tape mon login et mon mot de passe et la connection et effectuer 

### 3. Firewall
#### A. SSH :-
Le ssh est bien ouvert sur le **port 2222**

je doit donc autorisé le firewall avec la conexion sur le port 2222 la commande **firewall-cmd --add-port=2222/tcp –permanent**

Connexion reussite 

#### B. netcat

Il faut installer netcat avec la commande "yum install nc"

Dans la Console de la vm : **ncat -l -p 5454** 

Dans le PowerShell je tape **ncat 192.168.127.10 5454**

Les mots taper dans le PowerShell apparaise bien dans la vm.

## III. Routage statique

###1. Préparation des hôtes

Préparation fillaire 

- PC1 IP : 192.168.112.1/30

- PC2 IP : 192.168.112.2/30

Vérification des ping PC 

Préparation VirtualBox

Changer l'ip dans la VM je tape **nano /etc/sysconfig/network-scripts/ifcfg-enp0s8**

Je modifie l'ip en :

**- VM1 (sur PC1) : 192.168.101.10**

**- VM2 (sur PC2) : 192.168.102.10**

#### Check
 Les ping entre les differente s'effectue bien 

### Activation du routage sur les PCs

-Modification de la clé registre HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\ Services\Tcpip\Parameters\IPEnableRouter en passant sa valeur de 0 à 1

-Activation de la table de Routage :

  + Windows + R, service.msc puis entrer 


