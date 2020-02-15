HOW TO
==================================

# FAST START #

* Uncomment in file `docker-compose.yml` one of the databases (if you will use)

* `docker-compose build`

* `docker-compose up -d`

web:

* `docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/website-skeleton symfony"`

microservices, console applications or APIs:

* `docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/skeleton symfony"`

# Data Base - Doctrine #

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/orm-pack" && docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require --dev symfony/maker-bundle"

And you have all ready. http://localhost
=================================


# Normal set #

We come up with the name of our project, e.g. `symfony`

**ATTENTION**

If we choose a different project name, before we take the steps below, we need to edit the file `.docker/nginx/nginx.conf`
and in line 9 `root /var/www/symfony/public;` instead `symfony` give our name (without spaces)

We pass the console to the project directory and call the command

* `docker-compose build`

and after finishing

* `docker-compose up -d`

In container www-data is the owner of the files. User Id is mapped on your system user(as "they" recommend)
so if you will enter container use `docker exec -it -u www-data ...`

# Creation of directories and import of the libraries #

Created container with php, in our case it is `symfony-php-fpm`
and the project will be called `symfony` so we execute the command in container

* docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/website-skeleton `symfony`"

If we have chosen a different name for the project then `symfony` replace the one selected in the command

* docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/website-skeleton `project_name`"

# Connection to Data Base - Doctrine #

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/orm-pack"

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require --dev symfony/maker-bundle"

