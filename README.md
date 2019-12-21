# docker-laravel
a docker containers which contains three main containers [PHP, MYSQL, NGINX] that works good and fast using docker-compose

# Setup
This will work only on linux distros, also check that you have the latest docker and docker-compose
You can check docker-compose.yml for more configuration

```linux
$ cd /to/the/path/you/download/the/to

$ docker-compose up -d
```

>the NGINX will run in the background with the port of ':80', if you run linux distro locally just enter 'localhost' but if you are running virtual machine enter the linux distro 'xxx.xxx.xxx.xxx:80'


## Laravel commands
 to get laravel commands to work you should use this
 
 ```
$ cd project_name/src
```

to run php artisan 
```
$ docker-compose exec php php /var/www/html/artisan key:generate
```

## MYSQL 
in the docker-compose.yml there is a mysql section in the environment key you will find a global variables that will work with mysql,
you can change the database name, user and password 

```
mysql:
    image: mysql:5.7.22
    container_name: mysql
    restart: unless-stopped
    tty: true
    ports:
      - "4306:3306"
    volumes:
      - ./mysql:/var/lib/mysql
    environment:
      MYSQL_DATABASE: homestead
      MYSQL_USER: homestead
      MYSQL_PASSWORD: secret
      MYSQL_ROOT_PASSWORD: secret
      SERVICE_TAGS: dev
      SERVICE_NAME: mysql
    networks:
      - laravel
```

## NGINX
to change the nginx configuration in **default.conf** in **nginx/** folder 

```
server {
    listen 80;
    index index.php index.php;
    server_name localhost;
    error_log /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/html/public;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.*\.php)(/.*)$;
        fastcgi_pass php:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
}
```