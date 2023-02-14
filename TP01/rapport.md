 ## Introduction
Le but etant de faire l'analyse d'une clé USB trouvée par un agent de police,L'etape reflexe pour nous a été de copier et Ziper de bout en bout cette clé pour faire cette anlyse sur une copie. IL S'agira pour moi tout au long de ce TP d'analyser le ZIP de cette clé et fournir tous les resultats obtenus.
 
#### prérequis:
l'environment d'exploitation de cette analyse sera essentiellment une machine Debian dediée à ce travail pour eviter toute compromission possible de notre SI.       

## Analyse de la clé
                                                   
__1ére étape__ : j'ai tout d'abord unziper le dossier grace à la commande UNZIP et j'ai trouvé le fichier ayant le contenu de la clé nommé USB_Image et le sujet du TD.


![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP01/img/unzipp.png "Logo Title Text 1")


__2 éme étape__: j'ai verifié quels sont les dernieres modifications faites sur cette clé et qui les a fait grace à la commande -lh, mais je n'ai pas obtenu le resultat espéré.

![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP01/img/ls%20-lh.png "Logo Title Text 1")


__3éme étape__ j'ai utilisé la plateforme virus total pour verifier les paquets de ce ZIP et apres analyse j'ai trouvé un malware ayant un score ai= 60 se nommant baidu dans archive.Bomb, il y'avait principalement 2 grandes menaces detectées comme presente l'image ci dessous.

![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP01/img/capture1.png "Logo Title Text 1")

__4éme etape__ je me suis tourné vers le hash deja j'ai utilisé la commande sha656sum pour trouver le hash de l'image puis j'ai cherché si ce hash existe déja dans les bases de données de fichiers corrompu existantes;


__la derniere étape__ etait de  chercher le flag j'ai installé foremost pour continuer mon anlyse, apres son installation j'ai ouvert le fichier USB_Image avec foremost.

![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP01/img/foremost.png "Logo Title Text 1")


__Apres analyse j'ai trouvé 6 images à l'interieur ces images etaient respectivement en 3 en jpeg et 3 en png.__

![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP01/img/Capture%20d'%C3%A9cran_20230214_100557.png "Logo Title Text 1")

__Pour finir j'ai inspecté chaque image grace à la commande eog et j'ai pu decouvrir le flag qui est BOSCH (1MAG3).__

![alt text]( https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP01/img/Capture%20d'%C3%A9cran_20230214_102115.png "Logo Title Text 1")

la prochaine etape pour nous sera de faire des recherche sur cet element important.
