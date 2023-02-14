# Exercice 
cet exercice consistera à mettre en place une pipeline donnant le nombre de commune ayant pour nom canteleu.


# solution:
pour mettre en place cette pipeline nous utiliserons principalement trois commandes cat, grep et sed 
on l'utilisera comme suit:

cat consommation-annuelle-residentielle-par-adresse.csv | grep -w "canteleu" | sed '/^$/d' | wc -l

reponse 41
