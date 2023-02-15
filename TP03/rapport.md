# Introduction :


Une attaque informatique, ciblée sur le site web de B0sh-cyber, aurait permis d'infiltrer des outils malveillants sur la machine. Le site Web a donc été mis en quarantaine et est inaccessible pour le moment. Nous pouvons faire remonter cette attaque 3 septembre, dans la matinée. 
A l'aide de nos connaissances informatiques, nous allons analyser cette attaque afin de se rendre compte de ce que le hacker a tenté d'introduire dans notre SI.

<br/>

# Méthodologie :

Tout d'abord, nous allons regarder les derniers fichiers qui ont été modifié. Avec la commande __find / -not -path '/sys*' -not -path '/dev*' -not -path '/proc*' -mmin -60__, nous remontons tous les fichiers modifiés il y a moins de 60 minutes, excluant les repertoires /sys, /dev, /proc. Voila ce que nous trouvons, ce qui nous amène a rien de concluant  :
<br/>
![image](https://user-images.githubusercontent.com/78368428/219013521-3cba3007-4c11-4fe3-9eab-2d46405ba78e.png)
<br/>


Ensuite, nous regardons les différents logs a notre disposition, situés dans __/var/log__. Comme notre serveur Web a été attaqué, on commence par les logs d'apache2, notament les fichiers __access.log__ et __error.log__
On ne remonte rien de particulier, une erreur critique sur le serveur concernant du SSL, à voir pour rajouter cette couche de sécurtité en plus et de bien tenir à jour ce serveur :
<br/>
![image](https://user-images.githubusercontent.com/78368428/219013582-2b07cc1d-511a-4406-8345-0dd2b308298d.png)
<br/>


On regarde aussi les logs d'apt pour voir si l'intrus n'a pas directement téléchargé des paquets. On ne trouve pas de nouveaux pasquets ni rien d'anormal.


Pour la suite, on regarde les commandes qui ont été effectué avant notre arrivée en lisant le fichier bash_history avec la commande __cat ~/.bash_history__, ce qui nous remonte :
<br/>
![image](https://user-images.githubusercontent.com/78368428/219013645-57454fdc-db5a-4fe7-8e94-a68c6fb56ee8.png)
<br/>


On peut remarquer enormément de points. Déjà, il a pu accéder à notre fichier __/etc/passwd__. Les mots de passes devront etre modifiés au plus vite.
Il a regardé les fichiers de configuration de notre site web et a tenté un ping vers un IP en 138.66.89.12, surement une de ses machines à distance.
On observe une modification dans la crontab du serveur. On regarde à l'intérieur du fichier avec __cat /etc/crontab__ :
<br/>
![image](https://user-images.githubusercontent.com/78368428/219013715-16cad26f-089b-4147-9c2e-5f178d1b8b63.png)
<br/>


On remarque une ligne qui est présente avec l'IP du hacker. Cette commande a pour but de créer connexion en shell à distance qui pourrait être utilisé par pour accéder à la machine à distance et exécuter des commandes.

<br/>

Enfin, on peut observer la réation d'un .zip appelé b0sch_cyber_tools, reprensant l'introduction d'outils malveillants par le hacker. Celui-ci se trouve dans le repertoire /opt/leak. Nous ne possedons pas le mot de passe pour l'unzip car il a été supprimé. 
Cependant, pour le zip, le mot de passe a du etre tappé, ainsi, les logs sont censés avoir gardé les traces étant donné que le pirate ne les a pas supprimés.
<br/>
Ainsi, nous cherchons une trace de ce mot de passe dans les fichiers de logs, d'autant plus que nous avons maintenant un adresse IP.
Dans le fichier __access.log__, avec la commande __cat access.log | grep "138.66.89.12" | grep "pass"__, nous trouvons la ligne avec le mot de passe :
<br/>
![image](https://user-images.githubusercontent.com/78368428/219013851-02cde0d5-dbaa-4363-b33b-2fdf45b865e3.png)
<br/>

Ainsi, nous pouvons tenté d'unzip le fichier. cela nous retourne une erreur de droit, nous devons alors l'unzip vers un autre répertoire avec la commande __unzip bosh_cyber_tools.zip -d /home/b0osh/__.
<br/>


On se retrouve alors avec un fichier .txt que nous ouvrons :
<br/>
![image](https://user-images.githubusercontent.com/78368428/219013961-e75d9bd2-f860-4880-a095-378e4c98d170.png)
<br/>



# Résultats/Conclusion : 

A la suite de l'attaque qu'a subi le serveur Web, nous pouvons faire remonter plusieurs informations : 

1. La tache planifiée dans la crontab
2. La présence du fichier b0sch_cyber_tools.zip
<br/>
L'attaquant a surrement utilisé une faille informatique via apache2 pour se connecter à distance. 

# Recommandations :

Afin de sécuriser au mieux le serveur, il est nécessaire de le tenir à jour et d'avoir des moyens de le sécurisé, que ce soit logique ou matériel. La mise en place de la d'une connexion via SSL pourrait résoudre l'erreur rencontrée et vu plus haut. A voir si une DMZ a été créé avec un reverse proxy pour en plus empêcher que le serveur soit en front sur Internet. De plus, le changement des mots de passe est nécessaire.<br/>
La tache planifiée doit aussi etre supprimée pour empêcher au pirate de se connecter à distance.









