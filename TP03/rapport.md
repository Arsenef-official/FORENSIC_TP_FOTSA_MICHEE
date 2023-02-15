# INTRODUCTION
 
La compromission du site Bosch cyber est une situation très préoccupante car l'attaquant 
aurait exfiltré des outils secrets très dangereux.Notre responsabilité sera de mener
une analyse complète pour identifier les outils exfiltrés et déterminer l'identité 
de l'attaquant. Cette analyse va nous permettre de comprendre comment l'attaquant 
a pu réussir à compromettre le site et de fournir des recommandations pour 
renforcer la sécurité des systèmes informatiques de Bosch cyber. Pour ce faire, nous allons tout 
d'abord faire une evaluation de l'etendu de compromission puis une analyse des logs.
Grace à ces logs nous allons identifier les outils exfiltrés et  enfin identifier 
les attaquants.


#Methodologie 

pour s'assurer d'une analyse globale et complete nous devons tout d'abord verifier
si le site est bel est bien mis en maintenance en utilisant la commande "systemctl status apache2".

La reponse nous montre qu'actuellement le site n'est pas en cours d'execution de ce fait nous pouvons
démmarer. 
1ére étape l'evalution de l'etendu de la compromission.
pour cela nous sommes aller voir l'historique de modification et nous avons remarquer une connection ssh 
des actions menées 
entre autres :
- une connexion distance grace puis pind de l'ip 138.66.89.12
- l'untilisation de crontab avec crontab -e 
- mise en place d'un zip et ajout de son mot de passe dans le fichier (/tmp/mypassword) grece à la commande 

- Ensuite l'attaquant creer un dossier opt/leak et à deplacer le zip vers ce dossier 
- puis, l'attaquant à supprimmer le fichier "mypsasswd" qui contenait le mot de passe ainsi qu
