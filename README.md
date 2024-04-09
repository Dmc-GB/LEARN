# LEARN

#!/bin/bash

# Chemin vers le dossier contenant les modules
modules_folder="./"

# Vérifie si le dossier modules existe
if [ ! -d "$modules_folder" ]; then
  echo "Le dossier modules n'existe pas."
  exit 1
fi

# Navigue vers le dossier modules
cd "$modules_folder" || exit

# Parcours chaque sous-dossier dans modules
for folder in */; do
  # Assurez-vous qu'il s'agit d'un dossier
  if [ -d "$folder" ]; then
    # Se déplace dans le sous-dossier
    cd "$folder" || continue
    
    # Ajoute tous les fichiers du sous-dossier
    git add .
    
    # Effectue un commit avec le nom du sous-dossier
    git commit -m "Creating special commit for the folder $folder"

    git tag -a "$folder" -m "Tag pour le dossier $folder"

    git push
    
    # Retourne au dossier modules
    cd ..
    #Retire le dossier précedemment commit
    git rm -r --cached "$folder"
  fi
done

#Ajoute tous les fichiers
git add --all

#retire script.sh
git reset -- script.sh

#retire purge.sh
git reset -- purge.sh

#Commit le tout
git commit -m "Updating modules repository with unique commit for each module"

#pousse l'ensemble
git push
