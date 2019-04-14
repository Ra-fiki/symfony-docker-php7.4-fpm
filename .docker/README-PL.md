HOW TO
==================================

# Przygotowanie kontenerów #

Wymyślamy nazwę naszego projektu, np `symfony`

**UWAGA**

Jeśli wybierzemy inną nazwę projektu to zanim wykonamy kroki niżej musimy edytować plik `.docker/nginx/nginx.conf`
i w linii nr 9 `root /var/www/symfony/public;` zamiast `symfony` podać naszą nazwę(bez spacji)

Przechodzimy w konsoli do katalogu z projektem i wywołujemy polecenie

* docker-compose build

a po zakończeniu

* docker-compose up -d

# Utworzenie katalogów i zaciągnięcie bibliotek #

Wchodzi na utworzony kontener z php-em, w naszym przypadku to `symfony_php-fpm`

* docker exec -it -u www-data symfony_php-fpm bash

Projekt będzie się nazywał `symfony` więc wykonujemy polecenie

* composer create-project symfony/website-skeleton `symfony`

Jeśli wybraliśmy inną nazwę dla projektu to musimy nazwę `symfony` zastąpić wybraną w poleceniu

* composer create-project symfony/website-skeleton `nazwa_projektu`

# Podsumowanie #

* docker-compose build

* docker-compose up -d

* docker exec -it -u www-data symfony_php-fpm bash -c "composer create-project symfony/website-skeleton symfony"
