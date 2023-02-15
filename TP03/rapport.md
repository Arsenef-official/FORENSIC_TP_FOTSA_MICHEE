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
nous avons trouver principalement trois types de log dans le dossier de log du serveur web /var/log/apache2, notre but etant de chercher l'adresse ip de notre hacker et voir ce qu'il a fait.
Nous avons examiner les fichiers error.log et access.log. 

Dans error.log nous avons trouver principalement trois problemes: avec la commande <<tail -n 50 /var/log/apache2/error.log>>

- la première erreur etait liée au à la connexion SSL qui à echouer,elle peut etre lier à in probleme de certificat ssl  
- la deuxieme grande erreur etait liée à une requette HTTP GET, est une erreur PHP indiquant que certaines variables ne sont pas définies 
-Et enfin des erreurs de connections recidives echouées, peuvent être liées à un problème de connectivité entre le serveur et les clients

Dans access.log nous avons trouver principalement plusieurs log de bots chargés de la maintenance des connection du sites web, nous avons donc lancer une commande permettant de rechercher l'addresse ip de l'attaquant : <<grep '138.66.89.12' | grep 'pass' access.log>>
et nous avons pu remarquer le mot de passe du fichier ZIP retrouvé precedement 
![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP03/img/Capture%20d'%C3%A9cran_20230215_163219.png "Logo Title Text 1")
nous sommes donc reparti dans le dosier /opt/leak et nous avons unziper le fichier bosch_cyber_tools.zip grace à la commande <<unzip bosch_cyber_tools.zip -d /home/b0sch/>> puis ajout du mot de passe trouvé, cette commande a donc deplacer le fichier vers le repertoire /home/b0osch/.

![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP03/img/Capture%20d'%C3%A9cran_20230215_163646.png "Logo Title Text 1")

![alt text](https://github.com/Arsenef-official/FORENSIC_TP_FOTSA_MICHEE/blob/master/TP03/img/Capture%20d'%C3%A9cran_20230215_164124.png "Logo Title Text 1")
## Conclusion 
En conclusion nous sommes passer par plusieurs etapes pour atteindre notre objetif et nous avons finalement trouver l'addresse de l'attaquant et ce qu'il a pu faire dans le SI, l'etape la plus crusial nous avons son flag 
## recommandation 
comme recommandation vous devriez tout d'abord chercher à acheter de nouveaux certificat SSL ensuite securisé vos entete http et enfin bien sécurisé les access au serveur web tout en diminuant la possibilité de connection distante, installer par la suite un EDR et un SIEM pour une gestion centraliser de vos logs 
## conclusion générale 

le site bosh à eu une attaque informatique l'attaquant à eu access à distance au serveur et nous avons pour but grace au log de determiner son addresse ip et ce qu'il a exflitré pourr cela nous avons , regarder l'historique de ses actions et vu tous ses mouvement , nous avons analyser ensuite ses logs pour voir ce son mot de passe et enfin nous avons avons deziper le fichier qu'il a caché dans notre SI 
