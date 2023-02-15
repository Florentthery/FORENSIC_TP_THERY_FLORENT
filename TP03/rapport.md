Introduction :


Une attaque informatique, ciblé sur le site web de B0sh-cyber, aurait permis d'infiltrer des outils malveillants sur la machine. Le site Web a donc été mis en quarantaine et est inaccessible pour le moment. Nous pouvons faire remonter cette attaque 4 septembre, dans la matinée. 
A l'aide de nos connaissances informatiques, nous allons analyser cette attaque afin de se rendre compte de ce que le hacker a tenté d'introduire dans notre SI.

//
//

Méthodologie :

Tout d'abord, nous allons regarder les derniers fichiers qui ont été modifié. Avec la commande *find / -not -path '/sys*' -not -path '/dev*' -not -path '/proc*' -mmin -60*
