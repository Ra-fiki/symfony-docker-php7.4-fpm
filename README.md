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

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/orm-pack && composer require --dev symfony/maker-bundle"

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

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/orm-pack && composer require --dev symfony/maker-bundle"


# Database connection:

Database credentials are in `.env` file in project
For postgre database need to change `DATABASEURL` to

* DATABASE_URL=postgresql://db_user:db_password@127.0.0.1:5432/db_name?serverVersion=11&charset=utf8

and change `db_user`, `db_password`, `127.0.0.1`, `db_name`

# Security issues:

If during console execute error show with authentication then you should in
`project/config/packages/security.yaml` comment firewalls, section `main`


#Extra commends:
docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/security-bundle symfony/validator symfony/form symfony/orm-pack --dev symfony/maker-bundle"

docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && php bin/console make:user"

docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && php bin/console make:entity"

docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && php bin/console make:migration"

docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && php bin/console doctrine:migrations:migrate"

docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && php bin/console make:auth"

docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && php bin/console make:controller ProductController"