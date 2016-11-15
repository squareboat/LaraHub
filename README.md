# LaraHub
LaraHub is a Docker PHP development environment. It facilitate running PHP App on Docker.

LaraHub is configured to run Laravel Apps by default, and it can be modifyed to run all kinds of PHP Apps.

## Requirements
- [Git](https://git-scm.com/downloads)
- [Docker](https://www.docker.com/products/docker/) `>= 1.12`

## Installation & Usage
LaraHub strives to make the PHP development experience easier and faster.

It contains pre-packaged Docker Images that provides you a wonderful development environment without requiring you to install PHP, APACHE2, MySQL, REDIS, and any other software on your machines.

### Usage Overview
You've to just run a couple of commands to setup your enviornment which is fully equipped with the tools which are sufficient to run Laravel.

1. Get LaraHub inside your Laravel project: 

```
git clone https://github.com/squareboat/LaraHub.git
```

**Note:** Can also use [Git Submodule Concept](https://git-scm.com/book/en/v2/Git-Tools-Submodules) (will update soon)

2. Enter into the `larahub` directory and run these containers in detach mode (in background)

```
docker-compose up -d apache2 mysql redis
```

3. Open your `.env` file and set your DB & Redis configuration there:

	- `DB_HOST` to `mysql`
	- `REDIS_HOST` to `redis`

4. And its done, you're good to go. Just open up your favourite browser and visit:
	- `http://localhost`.

### Important Notes
- Please ensure that your ports should be free or unutilized as LaraHub will map apache2, mysql, etc on ports which maybe currently utilized by something else in your system.

- You can open up `docker-compose.yml` file to configure the enviornment according to your requirements.

## Included Containers
- **Database Engine(s):**
	- MySQL

- **Cache Engine(s):**
	- Redis
	- Memcached

- **PHP Server(s):**
	- Apache2

- **PHP Compiler(s):**
	- PHP-FPM

- **Tools:**
	- Workspace (PHP-7 CLI, Composer, Git, Node, Gulp, SQLite, XDebug, Vim, Nano, etc...)
	- PhpMyAdmin

> We'll try to add more tools by time and will update soon.
> If you can't find the software/tool which you require, just find the specific tool and add to this list.


## Usage & Commands
- **Run Containers: (Make sure you are in the larahub folder before running the docker-compose** 

**Note:** The `workspace` and `php-fpm` will run automatically in most of the cases, so no need to specify them in the up command. If you couldn't find them running then you need specify them as follow: `docker-compose up -d apache2 php-fpm mysql workspace`.

```
docker-compose up -d apache2 mysql redis
```

- **Enter into the containers, to execute commands like (Artisan, Composer, Gulp, etc...)**

```
docker-compose exec mysql bash
docker-compose exec workspace bash
```

- **Check out the running containers**

```
docker-compose ps
docker-compose ps -a
```

- **Closing the running containers**

```
docker-compose stop
docker-compose stop {container_name} // To stop single container
```

- **Deleting all existing containers**

```
docker-compose down
```

### Editing a Docker Image

1. Find a `dockerfile` of the image you want to edit, example for `mysql` it will be `mysql/Dockerfile`

2. Edit the file the you want.

3. Re-build the container

```
docker-compose build
```

### View Logs
The `Apache2` log file will be found in `logs/apache2`.

You may see log files for other containers by running the command:

```
docker-compose {container_name}
```

### Changing MySQL Configurations
- Just go inside `docker-compose.yml` file and find the container named - `mysql` and just change the configuration from the enviornment section:

```
mysql:
    build: ./mysql
    volumes:
        - mysql:/var/lib/mysql
    ports:
        - "3306:3306"  <------ Port Mapping
    environment:
        MYSQL_DATABASE: DB_NAME
        MYSQL_USER: MYSQL_USERNAME
        MYSQL_PASSWORD: MYSQL_PASSWORD
        MYSQL_ROOT_PASSWORD: MYSQL_ROOT_PASSWORD
```

You can find more about it on [Official MySQL Image on Docker](https://hub.docker.com/r/_/mysql)

## LICENSE
The MIT License. Please see [License File](LICENSE.md) for more information. Copyright © 2016 [SquareBoat](https://squareboat.com)