# Test technique QA

Le but de ce test est de mesurer le niveau technique du candidat et la façon de résoudre une logique de test.

Le langage utiliser est au choix javascript ou php (avec ou sans librairies/framework)

La ou les solutions de tests sont libres.

Vous devrez indiquer comment installer votre projet (installation manuelle, docker, vagrant, etc).

## Step 1 - Problématique

On souhaite créer un simulateur pour calculer sa capacité de remboursement en fonction du taux, de la durée souhaitée en mois et des mensualités souhaitées.

Il faut créer un formulaire avec 3 entrées :
 - Montant emprunté en € de type entier
 - Taux d'intérêt annuel en % de type flottant
 - Durée de remboursement en mois de type entier

Lors que l'on valide le formulaire on doit avoir en page de résultat avec au minimum :
 - Le montant de la mensualitée de type entier
 - Le coût total du crédit de type entier

La page de résultat ne doit pas être affichée si au moins l'un des 3 champs est vide.

Le formulaire ne peut pas être soumis si :
 - Un des champs est vide
 - Un des champs n'a pas le bon type

Les calculs sont les suivant :

 - Mensualité : [capital × (taux/12)]/[1 – (1 + (taux/12) – (nombre de mois de remboursement))]
 - Coût total : mensualité * durée du remboursement en mois


## Step 2 - Test unitaire

Vous devez mettre en place des tests unitaires afin de valider les calculs avec ces exemples de jeu de tests :

Test 1 :
 - Montant emprunté : 200 000 €
 - Taux d'intérêt : 2,1%
 - Durée de remboursement : 240

 - Mensualité : 1021 €
 - Montant du crédit : 245 105 €

Test 2 :
 - Montant emprunté : 140 000 €
 - Taux d'intérêt : 2,43%
 - Durée de remboursement : 204

 - Mensualité : 838 €
 - Montant du crédit : 171 042 €


## Step 3 - Tests fontionnels

Vous devez mettre en place des tests fonctionnels pour valider les scénarii suivant.

Formulaire invalide 1 :

 - Je suis sur la page du formulaire
 - Je complète le champs montant emprunté avec 200000
 - Je complète le champs taux d'intérêt avec 2,1
 - Je valide le formulaire
 - Je dois voir un message d'erreur "La durée de remboursement n'est pas indiqué"

Formulaire invalide 2 :

 - Je suis sur la page du formulaire
 - Je complète le champs montant emprunté avec 200000
 - Je complète le champs taux d'intérêt avec 2,1
 - Je complète le champs durée de remboursement avec 4,5
 - Je valide le formulaire
 - Je dois voir un message d'erreur "La durée de remboursement doit être un nombre entier"

Formulaire valide :
 - Je suis sur la page du formulaire
 - Je complète le champs montant emprunté avec 200000
 - Je complète le champs taux d'intérêt avec 2,1
 - Je complète le champs durée de remboursement avec 240
 - Je valide le formulaire
 - Je dois voir écrit "Votre mensualité sera de 838 €"
 - Et je dois voir écrit "Votre montant de crédit sera de 245 105 €"
