# docker-laravel
a docker containers which contains three main containers [PHP, MYSQL, NGINX] that works good and fast using docker-compose

# Setup
This will work only on linux distros, also check that you have the latest docker and docker-compose
You can check docker-compose.yml for more configuration

```linux
$ cd /to/the/path/you/download/the/to

$ docker-compose up -d
```

the NGINX will run in the background with the port of ':80', if you run linux distro locally just enter 'localhost' but if you are running virtual machine enter the linux distro 'xxx.xxx.xxx.xxx:80'
