HOW TO
==================================

# Container preparation #

We come up with the name of our project, e.g. `symfony`

**ATTENTION**

If we choose a different project name, before we take the steps below, we need to edit the file `.docker/nginx/nginx.conf`
and in line 9 `root /var/www/symfony/public;` instead `symfony` give our name (without spaces)

We pass the console to the project directory and call the command

* `docker-compose build`

and after finishing

* `docker-compose up -d`

# Creation of directories and import of the libraries #

Created container with php, in our case it is `symfony_php-fpm`
and the project will be called `symfony` so we execute the command in container

* docker exec -it -u www-data symfony_php-fpm bash -c "composer create-project symfony/website-skeleton `symfony`"

If we have chosen a different name for the project then `symfony` replace the one selected in the command

* docker exec -it -u www-data symfony_php-fpm bash -c "composer create-project symfony/website-skeleton `project_name`"

# Summary #

* `docker-compose build`

* `docker-compose up -d`

* `docker exec -it -u www-data symfony_php-fpm bash -c "composer create-project symfony/website-skeleton symfony"`
