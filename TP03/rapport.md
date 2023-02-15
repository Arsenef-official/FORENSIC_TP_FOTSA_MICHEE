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
des actions menées avec la commande "history"
![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP03/img/Capture%20d'%C3%A9cran_20230215_154231.png "Logo Title Text 1")
entre autres :
- une connexion distance grace de l'ip 138.66.89.12
- l'untilisation de crontab avec crontab -e 
- mise en place d'un zip et ajout de son mot de passe dans le fichier (/tmp/mypassword)  
- Ensuite l'attaquant creer un dossier opt/leak et à deplacer le zip vers ce dossier 
- puis, l'attaquant à supprimmer le fichier "mypsasswd" qui contenait le mot de passe ainsi quque le dossier tmp
sa connection à distace est visible depuis le dossier cronlab dans etc :
![alt text]( https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP03/img/Capture%20d'%C3%A9cran_20230215_154639.png "Logo Title Text 1")
de ce fait avec l'addresse ip du hacker et sachant dans quel dossier se cache mot de passe nous pouvons deja aller continuer nos recherches dans les logs
  
2éme Analyse des logs 
nous avons trouver principalement trois types de log dans le dossier de log du serveur web /var/log/apache2
nous avons examiner les 
