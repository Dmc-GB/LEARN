#  TERRAFORM

## What is it ?

Terraform est un outil d'infrastructure as Code (IaC).

### Explications

Dans la définition proposée nous avons deux mots importants à retenir : *Infrastructure* et *Code*

* Une infrastructure fait référence à des composants combinés(mis ensemble) qui sont néccessaires au fonctionnement et la gestion de l'environnement informatique.
* Un code bah c'est un code 😅. C'est un ensemble d'écriture dans un langage compréhensible par l'ordinateur.

Et donc Terraform c'est un outil qui permet de définir votre infrastructure en tant que code et d'ensuite exécuter ce code pour déployer les différents composants/ressources que vous avez défini dans votre code.

### Pourquoi l'Infrastruture as Code ?

Pour répondre à cette question, jetons un coup d'oeil a la méthode manuelle.
La méthode manuelle permet de déployer rapidement une ou des ressources dans votre environnement. Cependant il pose plusieurs problème à savoir:
* Il est facile de faire des erreurs en tant qu'humain
* Il n'y a pas forcément d'historique donc c'est compliqué de transmettre de manièe fiable les configurations faites à d'autres personnes
* Il est difficile de gérer l'état de configuration attendu pour la conformité
*- Déployer une seule ressource c'est bien. Mais quand il faut dupliquer cette ressource avec exactement les mêmes configurations et à grande échelle, cela devient compliqué avec des risques de mauvaises configurations.

D'où l'infrastructure as Code.

L'infrastructure as Code c'est :

-* Des scripts pour autmatiser les déploiements, mises à jours et destruction de l'infrastructure
-* Un plan complet de votre infrastructure avec les différentes ressources et configurations "WYSIWYG pour What You See Is What You Get" (ce qui veut dire que vous aurez en résultats ce que vous avez marqué dans votre script.
-* Simplicité de partage et de versionning des configurations de votre infrastructure
-* Idempotence : c'est à dire que peu importe le nombre de fois où vous rejoués le code, vous aurez le même résultat expecté
-* Planifier des mutations/évolution via le code

### Pourquoi Terraform ?

* Une syntaxe déclarative simple et compréhensible par les humains (même les noms programmeurs peuvent comprendre le code Terraform)
* Des modules installables
* Plannification et prédictons des changements
* Gestions des dépendances
* Gestion d'états
* Intégration possible avec plusieurs d'autres langages connus
* Un régistre avec plus de 1000+ fournisseurs


## Les Bases de Terraform

### Lyfecycle

Terraform passe par 6 phases principales à savoir

* L'écriture du code : bien évidemment pour déployer votre infrastructure il faudra écrire du code (lol 😆)
* L'initialisation (init): L'étape où on initialise le projet et télécharge les différents modules et providers
* La planification (plan): Générer un plan de ce qui sera déployé ou détruit
* La validation (validate) : s'assurer que tout est OK: les attributs requis, les erreours de syntaxe etc..
* L'application (apply) : L'étape d'exécution du code et du déploiement des ressources
* La destruction (destroy) : L'étape de destruction de ce qui a été déployé

## Architecture

Terraform est constitués de deux composants : le *core* et les *plugins*


### Le cœur de Terraform et les plugins :

**Le cœur de Terraform (Terraform Core):**

* C'est le binaire `terraform` que vous utilisez pour exécuter vos configurations.
* Il est écrit en langage Go et gère la communication avec les plugins.
* Il ne comprend aucune logique métier pour les différents services cloud ou plateformes.

**Les plugins Terraform:**

* Ce sont des extensions qui ajoutent des fonctionnalités à Terraform.
* Ils sont écrits en langage Go et s'exécutent comme des processus séparés.
* Il existe deux types de plugins principaux:

    * **Providers:** Ils implémentent la logique métier pour les différents services cloud ou plateformes, comme AWS, Azure, Google Cloud Platform, etc.
    * **Provisioners:** Ils permettent d'exécuter des scripts sur les instances créées par Terraform pour les configurer et les initialiser.

**Comment le cœur et les plugins interagissent:**

* Le cœur de Terraform utilise des RPC (Remote Procedure Calls) pour communiquer avec les plugins.
* Lorsque vous exécutez une commande Terraform, le cœur charge les plugins nécessaires et leur envoie des requêtes.
* Les plugins répondent aux requêtes en fournissant des informations sur les ressources disponibles et en effectuant des actions sur les infrastructures.

**Avantages de l'architecture plugin:**

* **Extensible:** Permet d'ajouter facilement de nouveaux fournisseurs et provisioners.
* **Modulaire:** Facilite la maintenance et la mise à jour de Terraform.
* **Flexible:** Permet d'adapter Terraform à des besoins spécifiques.

**Pour en savoir plus:**

* How Terraform Works With Plugins: [https://developer.hashicorp.com/terraform/plugin/how-terraform-works](https://developer.hashicorp.com/terraform/plugin/how-terraform-works)
* Plugin Development: [https://developer.hashicorp.com/terraform/plugin](https://developer.hashicorp.com/terraform/plugin)
* Terraform Providers: [https://www.terraform.io/docs/providers/index.html](https://www.terraform.io/docs/providers/index.html)
* Terraform Provisioners: [https://www.terraform.io/docs/provisioners/index.html](https://www.terraform.io/docs/provisioners/index.html)

**Voici quelques exemples de plugins populaires:**

* **Providers:** AWS, Azure, Google Cloud Platform, Kubernetes, Docker, etc.
* **Provisioners:** Shell, Ansible, Chef, Puppet, etc.
