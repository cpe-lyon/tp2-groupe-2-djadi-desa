# Compte rendu TP2

## Exercice 1 - Variables d'environnement

1. Le dossier des commandes tapées par l'user est **/user/bin/bash**.

2. La variable d'environnement qui permet à la commande **cd** de nous ramener dans notre répertoire personnel est **HOME**.

3.  Variables | Rôles
    --------- | -----
    **LANG** | Elle détermine la langue que les logiciels utilisent pour communiquer avec l’utilisateur
    **PWD** | Elle permet d'afficher le chemin d'accès vers le répertoire où se situe l'utilisateur qui a entré la commande
    **OLDPWD** | (OLD **P**rint **W**orking **D**irectory) contient le répertoire avant la dernière commande **cd**
    **SHELL** | Elle permet d'aller dans le répertoire des scripts **/bin/bash**
    **_** | Elle signifie le dernier argument de la commande précédente

4. export MY_VAR="yourself" ; printenv MY_VAR

