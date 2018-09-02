### Pobranie obrazu
```docker pull php:latest```

### Jednorazowe uruchomienie kontenera i odpalenie skrypu
```docker run --rm -v /c/Users/projects/tuts/first-php-docker-application:/app php:latest php /app/hello.php```

### Przykład uruchomienia composer require
```docker run --rm -v /c/Users/projects/tuts/first-php-docker-application/weather-app:/app composer:latest require slim/slim "^3.0"```

### php & apache
```docker run --rm -p 38000:80 -v /c/Users/projects/tuts/first-php-docker-application/weather-app:/var/www/html php:apache```

### baza danych & zapis
```docker run -d --rm --name weather-db -e MYSQL_USER=admin -e MYSQL_DATABASE=weather -e MYSQL_PASSWORD=p23l%v11p -e MYSQL_RANDOM_ROOT_PASSWORD=true -v /c/Users/projects/tuts/first-php-docker-application/weather-app/.data:/var/lib/mysql mariadb:latest --innodb-flush-method=O_DSYNC --innodb-use-native-aio=0 --log_bin=ON```
