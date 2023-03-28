# Coordinates resolver

## High level overview

Main functionality of this project is this: have a /coordinates endpoint which accepts 4 params: country code, city, street and postcode and as a response API should return coordinates (latitude and longitude) of provided address by using geocoding services.

## What this project contains 

* Doctrine entities + repository with two methods required for retrieving and saving (\App\Repository\ResolvedAddressRepository)
* Function to make geocoding requests to Google Maps and Here maps( \App\Controller\CoordinatesController::gmapsAction and \App\Controller\CoordinatesController::hmapsAction )
* API endpoint and controller action with GeocoderInterface injected as dependency placeholder.
* Maps services  (\App\Service\)

## How to start project

These are following steps to setup project:

```
cp .env.dist .env
```

then prepare docker environment:
```
docker-compose build
docker-compose up -d
docker-compose run php bash
```

final project steps inside of docker container:
```
composer install
bin/console doctrine:database:create
bin/console doctrine:schema:create
```

then go to `http://localhost/coordinates` and it should return 

```
{"lat":55.90742079144914,"lng":21.135541627577837}
```

JSON. If you want to check different address, then add params to url: http://localhost/coordinates?countryCode=DE&city=berlin&street=ritterstrase+9&postcode=10969