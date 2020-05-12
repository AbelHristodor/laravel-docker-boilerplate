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

## Creating the Laravel project

In order to create the laravel project open another terminal window (or stop the containers with `docker-compose down` and then rerun them in detached mode with `docker-compose up -d`) and run:

```bash
docker-compose exec app bash
```

Now that we're in the `app` container we can create the [Laravel](https://laravel.com/docs/7.x/installation) project:

```bash
composer create-project --prefer-dist laravel/laravel your_project_name
```

Now change while in the root of the [Laravel](https://laravel.com/docs/7.x/installation) project edit the .env file and change the portion of the file regarding the database:

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

Add the credentials you entered in the first .env file.

At last cd into the root of the project, and go to ` /config/nginx/conf.d/ ` and edit the `app.conf` file changing the `root` config accordingly:

```bash
...
    root /var/www/my_project_name/public;
...
```

Restart the containers:

```bash
    docker-compose down -v
    docker-compose up
```

Your app will be running at: <http://localhost:82>

## License

This project is licensed under the GNU GENERAL PUBLIC LICENSE V3 - see the [LICENSE.md](LICENSE.md) file for details
