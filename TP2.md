# Compte rendu TP2

## Exercice 1 - Variables d'environnement

1. Le dossier des commandes tapées par l'user est **/user/bin/bash**.

2. La variable d'environnement qui permet à la commande **cd** de nous ramener dans notre répertoire personnel est **HOME**.

3. Variables | Rôles
    --------- | -----
    **LANG** | Elle détermine la langue que les logiciels utilisent pour communiquer avec l’utilisateur
    **PWD** | Elle permet d'afficher le chemin d'accès vers le répertoire où se situe l'utilisateur qui a entré la commande
    **OLDPWD** | (OLD **P**rint **W**orking **D**irectory) contient le répertoire avant la dernière commande **cd**
    **SHELL** | Elle permet d'aller dans le répertoire des scripts **/bin/bash**
    **_** | Elle signifie le dernier argument de la commande précédente

4. > export MY_VAR="yourself" ; printenv MY_VAR

5. **MY_VAR** n'est plus là après avoir tapé la commande ```bash```.

7. > export NOMS="DJADI DE_SA"
   > printenv NOMS
   
8. > echo "Bonjour a vous deux, $NOMS"

9. **unset** permet d'enlever la variable et non de lui donner une valeur vide.

10. > echo \$HOME=$HOME

## Exercice 2 - Contrôle de mot de passe

``` BASH

#!/bin/bash

PASSWORD=moula
read -p 'Saisissez un mot de passe' -s a
echo -e "\n"
if [ $PASSWORD == $a ]; then
        echo "Mot de passe accepté"
else
        echo "Accès refusé"
fi

```

## Exercice 3 - Expressions rationnelles

``` BASH
#!/bin/bash

function is_number()
{
        re='^[+-]?[0-9]+([.][0-9]+)?$'

        if ! [[ $1 =~ $re ]]; then
                return 1
        else
                return 0
        fi
}

arg=$1

if is_number $arg
then
        echo $arg" est bien un nombre réel"
else
        echo "Erreur, relancer le script"
fi

```

## Exercice 4 - Contrôle d'utilisateur

``` BASH
#!/bin/bash
#set -x

monuser="jojo"

if [ $# == 0 ]; then
        echo "Utilisation: "$0" nom_utilisateur"
elif [ $1 == $monuser ]; then
        echo "Username valide"
else
        echo "Username non valide"
fi

```

## Exercice 5 - Factorielle

``` BASH
#!/bin/bash

n=$1
i=1
resultat=1
if [ $n == 0 ]; then
        echo 1
else
        while [ $i -le $n ]
        do
                let "resultat=$resultat * $i"
                let "i=$i + 1"
        done
        echo $resultat
fi

```

## Exercice 6 - Le juste prix

``` BASH

#!/bin/bash

num=$((RANDOM % 1000 + 1))

#Pas trouvé - boucle infini
while [ 1 -eq 1 ]; do

    echo -n "Votre num : "
    read numOk
    
    #Condition de si trop petit ou trop grand
    if [ $numOk -gt $num ]; then
        echo "Plus petit"
    elif [ $numOk -lt $num ]; then
        echo "Plus grand"
    else
        echo "Enfin trouve !"
        break
    fi
done
```

## Exercice 7 - Statistiques

1. 
``` BASH
#!bin/bash

if [ $# -ne 3 ]; then
    echo "3 arguments requis"
    exit 1
fi

function si_nbre() {
    res='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $res ]]; then
        return 1
    else
        return 0
    fi
}

min=0
max=0
moy=0
i=1

# Est-ce bien un nombre ?
for var in "$@"; do
    si_nbre $var
    if [ $? == "1" ]; then
        echo $var "Pas un nombre"
        exit 1
    else
        if [ $i -eq 1 ]; then
            min=$var
            max=$var
            moy=$((moy + $var))
        else
            if [ $var -lt $min ]; then
                min=$var
            elif [ $var -gt $max ]; then
                max=$var
            fi
            moy=$((moy + $var))
        fi
    fi
    i=$((i + 1))
done

#Moyenne calcul
i=$((i - 1))
moy=$((moy / $i))

echo min : $min
echo max : $max
echo moy : $moy
```

2.
``` BASH
#!/bin/bash

function si_nbre() {
    res='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[$1 =~ $res]]; then
        return 1
    else
        return 0
    fi
}

min=0
max=0
moy=0
i=1

for var in "$@"; do
    si_nbre $var
    if [ $? == "1" ]; then
        echo $var "Pas un nombre"
        exit 1
    else
        if [ $i -eq 1 ]; then
            min=$var
            max=$var
            moy=$((moy + $var))
        else
            if [ $var -lt $min ]; then
                min=$var
            elif [ $var -gt $max ]; then
                max=$var
            fi
            moy=$((moy + $var))
        fi
    fi
    i=$((i + 1))
done

i=$((i - 1))
moy=$((moy / $i))

echo min : $min
echo max : $max
echo moy : $moy
```

3.
``` BASH
#!/bin/bash

function si_nbre() {
    res='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $res ]]; then
        return 1
    else
        return 0
    fi
}

declare -a array
while [ 1 -eq 1 ]; do
    echo -n "Votre numero (A pour arrêt) : "
    read numOk
    
    if [ $numOk = "A" ]; then
        break
    fi
    
    si_nbre $numOk
    if [ $? == "1" ]; then
        echo $numOk "Pas un nombre"
    else
        array+=($numOk)
    fi
done

# Affichage du tableau
echo ${array[@]}

min=0
max=0
moy=0
i=1

for var in "${array[@]}"; do
    if [ $i -eq 1 ]; then
        min=$var
        max=$var
        moy=$((moy + $var))
    else
        if [ $var -lt $min ]; then
            min=$var
        elif [ $var -gt $max ]; then
            max=$var
        fi
        moy=$((moy + $var))
    fi
    i=$((i + 1))
done

i=$((i - 1))
moy=$((moy / $i))

echo min : $min
echo max : $max
echo moy : $moy
```
