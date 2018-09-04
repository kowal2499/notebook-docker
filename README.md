### Pobranie obrazu ###
```docker pull php:latest```

### Usunięcie obrazu ###
``` docker rmi [id] ```

### Jednorazowe uruchomienie kontenera i odpalenie skrypu ###
```docker run --rm -v /c/Users/projects/tuts/first-php-docker-application:/app php:latest php /app/hello.php```

### Przykład uruchomienia composer require ###
```docker run --rm -v /c/Users/projects/tuts/first-php-docker-application/weather-app:/app composer:latest require slim/slim "^3.0"```

### php & apache ###
```docker run --rm -p 38000:80 -v /c/Users/projects/tuts/first-php-docker-application/weather-app:/var/www/html php:apache```

### baza danych & zapis ###
```docker run -d --rm --name weather-db -e MYSQL_USER=admin -e MYSQL_DATABASE=weather -e MYSQL_PASSWORD=p23l%v11p -e MYSQL_RANDOM_ROOT_PASSWORD=true -v /c/Users/projects/tuts/first-php-docker-application/weather-app/.data:/var/lib/mysql mariadb:latest --innodb-flush-method=O_DSYNC --innodb-use-native-aio=0 --log_bin=ON```

### uruchomienie komendy mysql w kontenerze
```docker exec -it weather-db mysql --user=admin --password=p23l%v11p weather```

### Dockerfile - php z opcjami ###
```
FROM php:apache

RUN docker-php-source extract && docker-php-ext-install mysqli && docker-php-source delete
```

### build ###
```docker build . -t shiphp/weather-app```
```docker build --file .docker/Dockerfile -t laravel-docker . ```

### build bez cache ###
```docker build --no-cache --file .docker/Dockerfile -t romek-docker .```

### uruchomienie kontenera shiphp/weather-app i podlinkowanie go do bazy danych ###
```docker run -d --rm --name=weather-app -p 38000:80 -v /c/Users/projects/tuts/first-php-docker-application/weather-app:/var/www/html --link weather-db shiphp/weather-app ```

### przekazanie zmiennych środowiskowych ###
```docker run -d --rm --name=weather-app -p 38000:80 -v /c/Users/projects/tuts/first-php-docker-application/weather-app:/var/www/html --link weather-db -e DATABASE_HOST='weather-db' -e DATABASE_USER='admin' -e DATABASE_PASSWORD='p23l%v11p' -e DATABASE_NAME='weather' shiphp/weather-app```

### wejście do kontenera ###
```docker exec -it weather-db bash```

### docker-compose zbuduj ###
```docker-compose build```

### bash ###
```docker-compose exec app bash```
