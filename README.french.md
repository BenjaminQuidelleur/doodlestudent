Lire le Readme.md qui contient le rapport du projet.
Ce readme est juste un mémo des commandes de déploiement.

## Deploiement

Pour déployer l'application via docker-compose il faut au préalable construire les images
du front et du backend si elles n'existent pas déjà.

### Build front image 

1) se placer dans front 
2) sudo docker build -t front .

### Build back image 

1) sudo mvn package -DskipTests
2) docker build -f src/main/docker/Dockerfile.jvm -t quarkus/code-with-quarkus-jvm .
