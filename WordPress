# WordPress / Docker Project
## Make sure you have docker installed
    docker compose ps
## Make WordPress directory and change into it
    mkdir -p /srv/wordpress
    cd /srv/wordpress
## Create YAML/YML file
    sudo nano docker-compose.yaml
## Enter code using nano or vim
    services:
    db:
      # We use a mariadb image which supports both amd64 & arm64 architecture
      image: mariadb:10.6.4-focal
      # If you really want to use MySQL, uncomment the following line
      #image: mysql:8.0.27
      command: '--default-authentication-plugin=mysql_native_password'
      volumes:
        - db_data:/var/lib/mysql
      restart: always
      environment:
        - MYSQL_ROOT_PASSWORD=somewordpress
        - MYSQL_DATABASE=wordpress
        - MYSQL_USER=wordpress
        - MYSQL_PASSWORD=wordpress
      expose:
        - 3306
        - 33060
    wordpress:
      image: wordpress:latest
      volumes:
        - wp_data:/var/www/html
      ports:
        - 80:80
      restart: always
      environment:
        - WORDPRESS_DB_HOST=db
        - WORDPRESS_DB_USER=wordpress
        - WORDPRESS_DB_PASSWORD=wordpress
        - WORDPRESS_DB_NAME=wordpress
    volumes:
      db_data:
      wp_data:
  
## Save and run WordPress
   sudo docker compose up -d
## Check for port 80 and visit local host to access the site
Picture of my dashboard: 
![image](https://github.com/madidoan/WordPress/assets/124703457/a3c7bb50-8383-49b9-b93e-d5769ac7217b)
I used this for my guide: https://github.com/docker/awesome-compose/tree/master/official-documentation-samples/wordpress/
