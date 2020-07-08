# Laravel-Docker-Boilerplate

> Dockerized Laravel & MySQL starter project

This is a simple dockerized [Laravel](https://laravel.com/docs/7.x/installation) and MySQL boilerplate that I use to start developing without needing to worry about setting up docker, nginx etc...

## Getting Started

Firstly make sure you have docker installed. Check <https://docs.docker.com/compose/install/> for docker-compose and <https://docs.docker.com/install/> for docker.

Git clone the project and then create a .env file containing the following:

```bash
# Database Config

MYSQL_DATABASE=my_db
MYSQL_ROOT_PASSWORD=secret1
MYSQL_USER=myuser
MYSQL_PASSWORD=secret2
```

Edit the credentials accordingly and then start the containers by running:
```docker-compose up --build```

## Configuring the Laravel project

Now the laravel project has been created, we only need to make set some things up but firstly we need to enter our container's bash console with:
```bash
docker-compose exec app bash
```

Now that we're in the `app` container we can create the .env file using: ```cp .env.example .env``` and then edit it as shown below
using the credentials we put in the first .env file:
```bash
...

DB_CONNECTION=mysql
DB_HOST=database # don't change this --> it's referring to the mysql container
DB_PORT=3306
DB_DATABASE=my_db
DB_USERNAME=myuser
DB_PASSWORD=secret2
...
```
Now we need to run ```composer update``` and then set the permissions as so:
```
chmod -R 777 storage && chmod -R 777 bootstrap/cache
```

Finally we just need to generate the encryption key ```php artisan key:generate```

Restart the containers:

```bash
    docker-compose down -v
    docker-compose up
```

Your app will be running at: <http://localhost:82>


## License

This project is licensed under the GNU GENERAL PUBLIC LICENSE V3 - see the [LICENSE.md](LICENSE.md) file for details
