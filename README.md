# wordpress-sqlite
Lightweight Wordpress on Alpine with php-fpm ondemand and SQLite instead of MySQL.

```bash
docker pull naviarh/wordpress-sqlite
```
[Docker Hub milanb/wordpress-sqlite](https://hub.docker.com/r/milanb/wordpress-sqlite/)

Can be used in conjunction with [wordpress-nginx](https://github.com/milanboers/wordpress-nginx) ([Docker Hub milanb/wordpress-nginx](https://hub.docker.com/r/milanb/wordpress-nginx/)) to provide a full lightweight Wordpress solution.

Example docker-compose.yml for both:
```yaml
version: '3'

services:
    
    wp:
        image: milanb/wordpress-sqlite
        restart: unless-stopped
        environment:
            - WP_HOME=http://localhost:8001
            - WP_SITEURL=http://localhost:8001
        volumes:
            - "./db:/var/www/db"
            - "./html:/var/www/html"
    
    http:
        image: milanb/wordpress-nginx
        restart: unless-stopped
        links:
            - wp:wordpress
        #volumes_from:
            #- wp
        volumes:
            - "./db:/var/www/db"
            - "./html:/var/www/html"
        ports:
            - "8001:80"
```
