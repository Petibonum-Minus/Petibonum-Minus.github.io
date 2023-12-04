# ![](img/debian_25.png) Linux

## Connexion wifi - command line

[Source](https://linuxhint.com/3-ways-to-connect-to-wifi-from-the-command-line-on-debian/)
## Dockerfile

#### 1. Créer son Dockerfile

```bash=
FROM kalilinux/kali-rolling
RUN apt-get -y update && apt-get -y dist-upgrade && apt-get -y autoremove && apt-get clean
RUN apt-get -y install nmap
CMD ["/bin/bash"]
```
#### 2. Build Image

```bash=
sudo docker build -t nmap -f Dockerfile.
```

Vérification de la création de l'image : 
```bash=
sudo docker image ls
```

    REPOSITORY               TAG       IMAGE ID       CREATED          SIZE
    <none>                   <none>    14f7a4289e50   4 minutes ago    114MB
    pentest_img              latest    e9c44ba94204   14 minutes ago   1.02GB
    <none>                   <none>    d6a75ea21da0   14 minutes ago   1.02GB
    <none>                   <none>    142d08b79bec   19 minutes ago   168MB
    kalilinux/kali-rolling   latest    d4bd98a89b78   5 days ago       126MB
    debian                   buster    9e1a64aca99c   11 days ago      114MB
#### 3. Run Container

```bash=
sudo docker run --name nmap_cont --rm -i -t nmap bash
```

Vérification de la création de l'image : 
```bash=
sudo docker container ls
```
```bash=
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS     NAMES
a49cd245b80d   14f7a4289e50   "/bin/sh -c 'apt-get…"   5 minutes ago   Up 5 minutes             dreamy_mendeleev
```

La commande final "bash" permet d'ouvrir un shell root du container.

#### 4. Save Container 

```bash=
sudo docker ps
sudo docker commit -p <id_container> <backup_name>
sudo docker save -o ~/<backup_name>.tar <backup_name>
```

#### 5. Restore Container

```bash=
sudo docker load -i ~/<backup_name>.tar
```

#### 6. Docker compose

```bash=
version: '3.9'
services:

    ## ORCHESTRATOR
    ## SERVER
    server:
        build:
        context: .
        dockerfile: /home/petibonum/GOTHAM/Install/docker_gotham_server
        deploy:
        mode: replicated
        replicas: 1

    ## DATA-CENTER
    dc:
        build:
        context: .
        dockerfile: /home/petibonum/GOTHAM/Install/docker_gotham_dc
        deploy:
        mode: replicated
        replicas: 1
```
#### RUN Docker compose from image dockerfile

```bash=
sudo docker-compose up --build
```

## Ports en écoute sur la machine

```bash=
sudo netstat -tulpn | grep LISTEN
```


## Config prompt PS1 .bashrc

[Prompt Generator](https://scriptim.github.io/bash-prompt-generator/)

## Recherche FIND et redirection des erreurs

```find / -type f -name <file_name> 2>/dev/null```
## FTP connexion

```bash=
┌──(root💀b545f5615cd0)-[~]
└─# ftp 10.10.54.235
Connected to 10.10.54.235.
220 (vsFTPd 3.0.3)
Name (10.10.54.235:root): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> pas
Passive mode on.
ftp>
```
## MD to PDF

[PANDOC](https://pandoc.org/getting-started.html)

```bash=
pandoc <origin>.md -f markdown -t pdf -s -o <destination>.pdf
pandoc <origin>.md -o <destination>.pdf
```

## Connexion dhclient

### Refaire la connexion DHCP

```bash=
sudo dhclient -v -r eth0
sudo dhclient -v eth0
```
### Ajouter une ip à l'interface eth0

```bash=
sudo ip a add <ip>/<mask> dev eth0
```
### Supprimer une interface :

```bash=
sudo ip link delete <interface>
```
### Changement de route linux
Changement de route sur la machine à rediriger
```bash=
sudo ip r add default <new_route_ip>
```
### Autoriser le Nat sur Nat et le port forwarding

```bash=
vérifier que la machine à rediriger peut bien ping Internet

sudo sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/g' /etc/sysctl.conf
reboot ou sudo sysctl -w net.ipv4.ip_forward=1
sudo iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
```
### Fichiers important à modifier :
* /etc/resolv.conf (DNS google --> 8.8.8.8 + 1.1.1.1)
* /etc/hosts 

## Mounf disk image
```bash=
modprobe loop # Pour être sûr
sudo ewfmount galaxy_S6_full_4K.E01 mnt # Forcement en sudo
sudo mount -o ro,norecovery,offset=$((4096 * 1046784)),user=adam ./mnt/ewf1 ./userdata
```