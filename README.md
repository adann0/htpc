# re

Ce repo était un try de serveur NAS/Media, pour expérimenter Docker, ect... Projet a l'abandon car un Raspberry Pi + Disque Dur USB = Trop lent en vitesse de lecture pour les données que l'on souhaite envoyer a plusieurs utilisateurs simultanés qui utiliseraient le serveur. Pour 1 seul utilisateur c'est ok, avec des films qui ne sont pas en 4k.

ToDo : passer Samba en dehors de Docker, et voir avec un partage NFS classique ou un RAID...

# Post Install

https://gist.github.com/adann0/9eff3e831e514988579337dc11492570

# GlusterFS

https://gist.github.com/adann0/4aad4526145044aceb40d8caf26524d1

# Docker Swarm

On the master :

    $ docker swarm init 
    
We have in return a command to enter on the workers instances :
    
    $ docker swarm join --token SWMTKN-1-17fw99pvvhyf8og91i09ujgy3upzg0nnce3hav0ecjylr2anr3-c7xgby5qequwa0w679q9gx5it 192.168.0.210:2377

To verify, on the master :

    $ docker node ls
    
Set more masters :

    $ docker node promote <node_id>
    
# Let's Encrypt

    https://github.com/adann0/docker-nginx-letsencrypt
    https://github.com/adann0/openldap-armv7#openldap-certificates

## Stack Deploy

    $ docker stack deploy -c docker-compose.yml <stack>
    $ docker stack services <stack>

# Sources :

- GlusterFS :
  - https://medium.com/running-a-software-factory/setup-3-node-high-availability-cluster-with-glusterfs-and-docker-swarm-b4ff80c6b5c3
  - http://banoffeepiserver.com/glusterfs/set-up-glusterfs-on-two-nodes.html
  - https://docs.gluster.org/en/v3/Administrator%20Guide/Managing%20Volumes/
  - GlusterFS Fail to Mount on Boot with Fstab : https://serverfault.com/a/823582
  
- Let's Encrypt + Nginx + Docker + Swarm :
  - https://www.humankode.com/ssl/how-to-set-up-free-ssl-certificates-from-lets-encrypt-using-docker-and-nginx
  - https://medium.com/@rhrn/setup-front-docker-machine-in-swarm-mode-with-letsencrypt-and-registry-890a4a1df090

- Scaling :
  - https://medium.com/brian-anstett-things-i-learned/high-availability-and-horizontal-scaling-with-docker-swarm-76e69845825e

- Enable Docker Experimental Features : https://github.com/docker/docker-ce/blob/master/components/cli/experimental/README.md

# Three

    /mnt/
    ├── config/
    │   ├── samba/
    │   ├── cloud/
    │   ├── nginx/
    │   ├── letsencrypt/
    │   └── .../
    ├── data/
    │   ├── portainer/
    │   ├── mysql/
    │   ├── openldap/
    │   │   ├── slapd/
    │   │   └── ldap/
    │   ├── media/
    │   │   ├── movie/
    │   │   └── music/
    │   └── cloud/
    └── www/
        ├── mediaserver.tk/
        │   ├── cloud/
        │   └── .../
        ├── radio.xyz/
        └── .../
        
 # Images Armv7
 
    https://github.com/adann0/samba-ldap-armv7
    https://github.com/adann0/mariadb-armv7
    https://github.com/adann0/openldap-armv7
    https://github.com/adann0/docker-images-armv7

# ToDo :

    - Env Files
    - Reverse Proxy sur toutes les apps
    - Docker Secret
