# Mon Readme

## Explications du fichier docker-compose

Le service "app" :
Ce service utilise l'image "php:8.2-fpm" (version 8.2 de php avec fpm ou FastCGI Process Manager), et nomme son container "symfony_app". Il se trouvera dans le dossier "var/www/html", met en place 3 volumes : un volume en bind mount sur "./app", et deux volumes nommés "app_logs" et "app_cache". Il est sur le network "symfony_network" et peut donc communiquer avec tous les autres services sur ce même network.
Ce service contient l'application et son code (frontend et backend).

Le service "webserver" :
Ce service utilise l'image "nginx:stable" (la version stable de nginx). Ce service est sur le port 80 et le host 8080. Il met en place 3 volumes, 2 en bind mount ("./app" et "./nginx") et un nommé "nginx_logs". Ce service dépend du service "app" et va donc attendre que ce service fonctionne avant de s'installer. Il est sur le network "symfony_network" et peut donc communiquer avec tous les autres services sur ce même network.
Ce service contient le serveur web.

Le service "database" :
Ce service utilise l'image "mysql:8.0" et nomme son container "symfony_db". Il a plusieurs variables d'environement (PMA_HOST : host de la base de données, ici "symfony_db"; MYSQL_ROOT_PASSWORD : variable essentielle pour le fonctionnement de mysql qui met en place un mot de passe par défaut pour "root"; MYSQL_DATABASE : nom de la base de données; MYSQL_USER : nom d'utilisateur; MYSQL_PASSWORD : le mot de passe). Il se trouve sur le port et l'host 3306, possède un volume nommé "db_data", et se trouve sur le network "symfony_network" et peut donc communiquer avec tous les autres services sur ce même network.
Ce service contient la base de données.

Le service "adminer" :
Ce service utilise l'image "adminer", et nomme son container "symfony_adminer". Il restart toujours son container si il s'arrête. Il est sur le port "8080" sur l'host "8081". Ce service a une dépendence, le service "database", et ne démarrera que lorsque ce service aura démarré. Il est sur le network "symfony_network" et peut donc communiquer avec tous les autres services sur ce même network.

Le service "phpmyadmin" :


