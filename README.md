# Docker example for Agora

`front/` is a Nuxt
`back/` is a Laravel

## Start

```bash
# Stop, build and start the containers
docker-compose down -v ; docker-compose up --build -d

# Install Laravel dependencies (first time)
docker-compose exec backend composer install

# Run Laravel migrations
docker-compose exec backend php artisan migrate
```
