# Mon Readme

## Explications du fichier docker-compose

services: = Contient les différents services que compose va mettre en place;
app: = Le service nommé "app";
image: php:8.2-fpm = L'image utilisée par le service, ici php version 8.2;
container_name: symfony_app = Le nom du container, ici le container se nommera "symfony_app";
working_dir: /var/www/html = Le chemin du dossier de travail;
volumes: = Les volumes qui permettent de garder les données en mémoire;
- ./app:/var/www/html = Volume en bind mount qui permet de mettre à jour les fichiers après modification;
- app_logs:/var/log/php = Volume nommé qui permet de garder les données même après un arrêt du container;
networks: = Les networks que doit utiliser le service. Ici, le service utilise seulement le network "symfony_network";
webserver: = Le service nommé "webserver";
image: nginx:stable = Ce service utilise l'image nginx (version stable);