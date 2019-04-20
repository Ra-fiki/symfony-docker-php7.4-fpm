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

I wszystko jest już postawione

# Wolny start - Przygotowanie kontenerów #

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

* composer create-project symfony/website-skeleton `nazwa_projektu`
