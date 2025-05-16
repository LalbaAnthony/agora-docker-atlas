# Introduction à Docker

## 1. Qu’est-ce que Docker ?

Docker est une plateforme permettant de créer, déployer et exécuter des applications dans des conteneurs.

Concepts clés :
- Conteneur: mini-machine légère et isolée avec tout le nécessaire pour faire tourner une application.
- Image Docker: un modèle de conteneur, avec tous les outils nécessaires (OS, Apache, PHP…).
- Dockerfile: un script décrivant comment construire une image.
- Docker Compose: un outil pour gérer plusieurs conteneurs avec un seul fichier (docker-compose.yml).

# 2. Pourquoi Docker ?

- Standardise les environnements de développement.
- Emballe l’appli avec toutes ses dépendances.
- Facilite le déploiement, le scaling et les tests.
- Fini les "ça marche chez moi".

# 3. Exemple basique

`index.php`:
```php
<?php
phpinfo();
```

`Dockerfile`:
```Dockerfi
FROM php:8.2-apache
COPY . /var/www/html/
```

```bash
docker build -t mon-php-apache .
docker run -p 8080:80 mon-php-apache
```
Accès : http://localhost:8080

# 4. Docker Compose

`docker-compose.yml`:
```yaml
services:
  web:
    image: php:8.2-apache
    volumes:
      - .:/var/www/html
    ports:
      - "8080:80"

    db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: test
        MYSQL_USER: user
        MYSQL_PASSWORD: password
```

```bash
docker-compose up
```

# 5. Commandes utiles

| Commande | Description |
|----------|-----------------|
| `docker run` | Lance un conteneur |
| `docker ps -a` | Liste les conteneurs actifs |
| `docker-compose up` | Démarre tous les services |
| `docker-compose down` | Arrête tous les services |
| `docker exec -it <container> bash` | Ouvre un terminal dans un conteneur |