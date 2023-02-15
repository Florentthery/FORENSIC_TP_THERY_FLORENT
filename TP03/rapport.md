Introduction :


Une attaque informatique, ciblée sur le site web de B0sh-cyber, aurait permis d'infiltrer des outils malveillants sur la machine. Le site Web a donc été mis en quarantaine et est inaccessible pour le moment. Nous pouvons faire remonter cette attaque 3 septembre, dans la matinée. 
A l'aide de nos connaissances informatiques, nous allons analyser cette attaque afin de se rendre compte de ce que le hacker a tenté d'introduire dans notre SI.



Méthodologie :

Tout d'abord, nous allons regarder les derniers fichiers qui ont été modifié. Avec la commande __find / -not -path '/sys*' -not -path '/dev*' -not -path '/proc*' -mmin -60__, nous remontons tous les fichiers modifiés il y a moins de 60 minutes, excluant les repertoires /sys, /dev, /proc. Voila ce que nous trouvons, ce qui nous amène a rien de concluant  :



Ensuite, nous regardons les différents logs a notre disposition, situés dans __/var/log__. Comme notre serveur Web a été attaqué, on commence par les logs d'apache2, notament les fichiers __access.log__ et __error.log__
On ne remonte rien de particulier, une erreur critique sur le serveur concernant du SSL, à voir pour rajouter cette couche de sécurtité en plus et de bien tenir à jour ce serveur :


On regarde aussi les logs d'apt pour voir si l'intrus n'a pas directement téléchargé des paquets. On ne trouve pas de nouveaux pasquets ni rien d'anormal.









