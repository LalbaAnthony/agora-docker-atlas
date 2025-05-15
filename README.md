# Docker example for Agora

`front/` is a Nuxt
`back/` is a Laravel

## Start

```bash
# Create necessary directories
mkdir -p docker/nginx/conf.d docker/nginx/logs

# Start the containers
docker-compose up -d

# Install Laravel dependencies (first time)
docker-compose exec backend composer install

# Run Laravel migrations
docker-compose exec backend php artisan migrate
```
