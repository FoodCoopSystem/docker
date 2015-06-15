# Development environment for FoodCoopSystem

This repository includes docker container sources for a docker image including www server for foodcoopsystem developers. It's basically a Apache + PHP (5.6) server, but has some addons that might be usefull in foodcoopsystem (and probably any Drupal based) application.

## Short specification
This image includes following tools:

* Installed composer
* Installed latest stable drush from 7.x branch
* Installed development and profiling extensions like php5-xdebug and php5-xhprof.
* Installed PHP 5.6 (as apache2 module and php5-cli).


## Credencials

This is all port forwarding and access details you will need to work with docker.

* SSH
  * Host ssh port: **9022**
  * User: **root**
  * Password: **root**
* DataBase
  * Host MySQL port: **3306**
  * User: **root**
  * Password: **root** 
  * Database: **foodcoop**
* WWW
  * Host apache2 port: **80**

If you are logged in to ssh service, host name for mysql server is "db". You can access those services, simple by specifing `127.0.0.1` as your host and one of required ports.


## Creating your docker environement (Ubuntu)
> Note: This instruction will fail, if you have apache/nginx/\<other web server\> or mysql server running on your machine. This instruction assumes that ports 80 and 3306 are free. You can simply fix this just stopping your service. E.g. on ubuntu: `sudo service apache2 stop` and `sudo service mysql stop`

1. Install docker: http://docs.docker.com/installation/
1. Install docker-compose: http://docs.docker.com/compose/install/
1. Install drush on your machine: http://docs.drush.org/en/master/install/
1. Add alias for foodcoop installation in your `/etc/hosts` file: `sudo echo "127.0.0.1 www.foodcoopsystem.local" >> /etc/hosts`
1. Copy `drush/foodcoopsystem.aliases.drushrc.php` into `~/.drush/` subdirectory (create it if it doesn't exist)
1. Copy `compose/docker-compose.yml` file into your foodcoop codebase. 
1. Execute `docker-compose up` (This will pull dependencies and create all required containers).
1. Copy your public key into www container: `ssh-copy-id root@www.foodcoopsystem.local`
1. If you want to stop containers: `docker-compose stop`
1. If you want to return to work, and start environement: `docker-compose start`

File `docker-compose.yml` will share app subdirectory from foodcoop codebase as `/var/www` directory at www container. You can use drush with alias `@foodcoopsystem.local` without need to change to working directory so from any place in the system. E.g.: You can access it from you home dir `$ cd ~; drush @foodcoopsystem.local status`
