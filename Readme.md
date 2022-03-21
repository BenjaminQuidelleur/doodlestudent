# TLC rendu
## Benjamin Quidelleur - Benjamin Navet - Guillaume Subra


Vous trouverez le dépôt Git de notre projet ici sur la branche main :
https://github.com/BenjaminQuidelleur/doodlestudent

Nous avons réalisé les étapes 1 à 4 complètement et nous avons tenté la tâche 5 sans y parvenir.

### Etape 1

Il y a 1 dockerfile pour le back, 1 pour le front et un docker compose pour l'ensemble des services.

Pour le back nous avons choisi ce dockerfile :
https://github.com/BenjaminQuidelleur/doodlestudent/blob/main/api/src/main/docker/Dockerfile.jvm
Il embarque la JVM (donc plus lourd et au final plus lent au démarrage que le natif) mais l'execution du code s'optimisera au runtime. De plus ce back n'est pas vraiment découpé en micro-services auquel le natif se prête davantage.
Vous trouverez le dockerfile du front ici : https://github.com/BenjaminQuidelleur/doodlestudent/blob/main/front/Dockerfile
Vous trouverez le docker compose ici : https://github.com/BenjaminQuidelleur/doodlestudent/blob/main/docker-compose.yaml

### Etape 2

Nous avons suivie les indications du sujet du projet afin de configurer le bunkerized-nginx dans notre docker-compose. Nous avons utilisé le fichier exemple de configuration. Il faut particulièrement faire attention à bien monter les fichiers au bon endroit et faire attention à la configuration des noms de domaines dans le etc/host.

### Etape 3

Nous avons déployé l'application sur une machine de l'ISTIC, vous pouvez y accéder ici : http://148.60.11.219/

Pour pourvoir déployer, nous avons buildé les deux images docker du front et de du back, nommés respectivement "front" et "code-with-quarkus-jvm". Ensuite nous avons fait un docker-compose up -d pour que l'application tourne en processus de fond, tout le temps, sur la machine de l'ISTIC 148.60.11.219. Pour information, elle s'appelle Periscol car il s'agit de la même machine utilisé en PIT.

### Etape 4

Nous avons déployé l'ensemble des containers Nginx, Mail, le backend Quarkus, Etherpad enfin la base de données. L'ensemble est coordonné selon le diagramme suivant:
![](https://codimd.math.cnrs.fr/uploads/upload_b51b7c3f822da3e93198d0648001b0cf.png)

En orange sur fond noir il s'agit du nom des containers initialisés par notre docker-compose.

### Etape 5

Objectif : "Mettre en place un mécanisme de déploiement continu qui permette de déployer la nouvelle version de l’application automatiquement si un nouveau commit est activé sur le back ou le front."

Nous avons voulu mettre en place un GitHub action, que nous avions déjà utilisé cette année dans d'autres projet, afin notamment d'avoir un workflow à chaque push des développeurs de l'équipe, et qui a pour but d'executer une batterie de tests préalable à la validation du push.

Dans le cadre de cette étape 5, c'est différent puisqu'il s'agit de déploiement continu et non d'intégration continue, en faisant en sorte que le push génère des actions de déploiement sur une machine distante. Cela implique un lien entre la machine distante et DockerHub(dans le cadre de Github), où l'image de l'application est uploadée après chaque push, créant à son tour une alerte pour la VM qui vient récupérer cette image et la déployer. Dans notre cas, nous avons seulement réalisé la création du workflow et non la connexion avec le DockerHub. Le workflow s'active à chaque push sur la branche Dev du repository, et réalise les étapes du déploiement décrites à l'étape 3. En conséquence cette manipulation ne s'effectue qu'au niveau du serveur Github et non sur la VM de l'ISTIC.

Nous n'avons pas fait de DockerHub, ni de GitLab Runner par manque de temps, nos stages ayant commencé depuis le 7 mars. Nous sommes arrivés au bout de ce que l'on peut produire pour ce projet.

Le workflow est disponible sur la branche Dev ici : https://github.com/BenjaminQuidelleur/doodlestudent/blob/Dev/.github/workflows/main.yml. Pour information, l'étape 5 n'ayant pas abouti nous n'avons pas voulu rappatrier ce code sur le main.


# TP

Vous trouverez le fichier dockercompose de l’étape 2 et le docker file de l’étape 3 ici :

https://github.com/BenjaminQuidelleur/doodlestudent/tree/main/TP

Il s'agit du code dévoloppé pendant le TP, que nous avons fait ensemble.
