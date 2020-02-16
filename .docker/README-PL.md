HOW TO
==================================

# SZYBKI START #

* Odkomentuj w pliku `docker-compose.yml` jedną bazę danych (jeśli będziesz używać)

* `docker-compose build`

* `docker-compose up -d`

web:

* `docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/website-skeleton symfony"`

microservices, console applications or APIs:

* `docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/skeleton symfony"`

# Połączenie do bazy danych - Doctrine #

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/orm-pack && composer require --dev symfony/maker-bundle"

I wszystko jest już postawione
==================================


# Normalny start #

Wymyślamy nazwę naszego projektu, np `symfony`

**UWAGA**

Jeśli wybierzemy inną nazwę projektu to zanim wykonamy kroki niżej musimy edytować plik `.docker/nginx/nginx.conf`
i w linii nr 9 `root /var/www/symfony/public;` zamiast `symfony` podać naszą nazwę(bez spacji)

Przechodzimy w konsoli do katalogu z projektem i wywołujemy polecenie

* `docker-compose build`

a po zakończeniu

* `docker-compose up -d`

W kontenerze www-data jest właścicielem plików. Identyfikator użytkownika jest mapowany na użytkownika systemu (jak „zalecają”)
więc jeśli będziesz wchodził do kontenera używaj `docker exec -it -u www-data ...`

# Utworzenie katalogów i zaciągnięcie bibliotek #

Utworzony kontener z php-em, w naszym przypadku to `symfony-php-fpm`
a projekt będzie się nazywał `symfony` więc wykonujemy polecenie na konenerze:

* docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/website-skeleton symfony"

Jeśli wybraliśmy inną nazwę dla projektu to musimy nazwę `symfony` zastąpić wybraną w poleceniu

* docker exec -it -u www-data symfony-php-fpm bash -c "composer create-project symfony/website-skeleton `nazwa_projektu`"

# Połączenie do bazy danych - Doctrine #

* docker exec -it -u www-data symfony-php-fpm bash -c "cd `symfony` && composer require symfony/orm-pack && composer require --dev symfony/maker-bundle"

# Database connection:

Database credentials are in `.env` file in project
For postgre database need to change `DATABASEURL` to

* DATABASE_URL=postgresql://db_user:db_password@127.0.0.1:5432/db_name?serverVersion=11&charset=utf8

and change `db_user`, `db_password`, `127.0.0.1`, `db_name`

# Problemy bezpieczeństwa:

Jeśli podczas wykonywania w konsoli wyskoczy błąd z autoryzacją to trzeba w pliku
`project/config/packages/security.yaml` zakomentować w sekcji firewalls, punkt `main`