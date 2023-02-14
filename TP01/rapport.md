Introduction :

Après avoir trouvé une clé USB suspecte dans un parking, un employé nous la remise afin de pouvoir l'analyser et de savoir si elle est utilisable ou non 



Rapport :

Une fois que nous avons isolé notre machine du LAN de notre réseau, nous la testons sur un environnement Linux. Pour commencer, nous utilisons l'outil binwalk qui va nous permettre d'analyser l'iso de la clé et des trouver des fichiers ou des microprogrammes. On trouve des informations telles que des images PNG et JPEG. De plus, on peut remarquer la présence d'un fichier Adobe Flash. Cependant, le contenu de la clé USB est vide. Pour acceder à ces fichiers, j'ai essayé de monter la partition de la clé usb via mount mais sans aucun succès. J'ai cherché un outil pour faire de la récupération fichiers supprimés. J'ai découvert l'outil testdisk pour essayer de recupérer des partitions supprimées de la clé mais sans réussite aussi.
Via l'outil test disk, on peut utiliser Photorep qui est logiciel de recupération de fichiers effacés. Celui-ci va donc nous permettre de récupérer les photos. Après l'utilisation de la commande "photorep USB_Image", l'outil nous retourne 5 fichiers (voir "photos"). On remarque donc plusieurs photos d'animaux, dont deux flags et un fichier .ini.

En plus de ce travail, j'ai regardé le Header du fichier pour essayer de récupérer des informations (voir "hexdump"). On peut voir que le clé est sous du FAT32, sous du msdos 5. En amont, nous vérifions que le HASH n'a pas été modifié entre temps. Nous comparons celui donné et celui que nous trouvons dans la photo "sum". Ce sont donc les memes. Nous notons que si nous effectuons cette commande après un testdisk, le hash est modifié  




Conclusion

Après analyse de la clé USB, nous pouvons conclure que cette clé est sans danger et qu'elle ne présente aucun risque. Nous pouvons alors commencer à chercher son propriétaire.
