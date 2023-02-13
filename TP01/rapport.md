Introduction :

Après avoir trouvé une clé USB suspecte dans un parking, un employé nous la remise afin de pouvoir l'analyser et de savoir si elle est utilisable ou non 



Rapport :

Une fois que nous avons isolé notre machine du LAN de notre réseau, nous la testons sur un environnement Linux. Pour commencer, nous utilisons l'outil binwalk qui va nous permettre d'analyser l'iso de la clé. On trouve des informations qui ne sont pas normalement présentes dans ce genre de fichier, tel que des images PNG et JPEG. De plus, on peut remarquer la présence d'un fichier Adobe Flash. Pour acceder à ce fichier, j'ai essayé de monter la partition de la clé usb via mount mais sans aucun succès. Je n'ai pas reussi à lire les images.

J'ai utilisé l'outil testdisk pour essayer de recupérer des elements supprimé de la clé mais sans réussite aussi

J'ai regardé le Header du fichier et vérifier que le HASH était le bon. 
