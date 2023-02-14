                                                      ## introduction
Le but etant de faire une analyse d'une clé trouvée par un agent de police, la premiere etape a été de la copiée et la  Zipée de bout en bout pour faire cette anlyse de cette copie, IL S'agira pour moi tout au long de ce TP d'analyser le ZIP de cette clé et fournir tous les resultats obtenus.
 
prérequis : l'environment d'exploitation de cette analyse sera essentiellment une machine Debian dediée à ce travail pour eviter toute compromission possible de notre SI.       

                                                       ANALYSE 
                                                   
1ére etape : j'ai tout d'abord unziper le dossier grace à la commande UNZIP et j'ai trouvé le fichier ayant le contenu de la clé nommé USB_Image et le sujet du TD.
2 éme étape: j'ai verifié quels sont les dernieres modifications faites sur cette clé et qui les a fait grace à la commande -lh.
3éme etape j'ai utilisé la plateforme virus total pour verifier les paquets de ce ZIP et apres analyse j'ai trouvé un malware ayant un score ai= 60 se nommant baidu dans archive.Bomb.
il y'avait precisement 2 menaces détéctés les images sont jointes au dossier.
En 4éme etape j'ai utilisé le hash pour chercher si de potentiel similutude dans les bases de données de fichiers corrompu existantes,
Ensuite pour chercher le flag j'ai installé foremost pour continuer mon anlyse, apres son installation j'ai ouvert le fichier USB_Image avec formost et apres analyse j'ai trouvé 6 images à l'interieur ces images etaient respectivement en 3 en jpeg et 3 en png.
Pour finir j'ai inspecté chaque image et j'ai pu decouvrir le flag qui est BOSCH (1MAG3).
la prochaine etape pour nous sera de faire des recherche sur cet element important.
