# LEARN

#!/bin/bash

# Chemin vers le dossier contenant les modules
modules_folder="/chemin/vers/votre/dossier/modules"

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
    git commit -m "Commit pour le dossier $folder"
    
    # Pousse les modifications
    git push
    
    # Retourne au dossier modules
    cd ..
  fi
done
