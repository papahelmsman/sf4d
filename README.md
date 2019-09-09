<p align="center"><img src="docs/assets/img/head_logo.svg" width="250"></p>

<h1 style="text-align:center;">sf4d </h1>
<h4 style="text-align:center;">Symfony run-time system based on Docker and Docker-compose Tools</h4>
</br>

nginx 17.2 - php7.3-fpm - postgresql 11.2 - redis


## Table of Contents

 * [Prerequisites](#Prerequisites)
 * [Runtime Installation](#Installation)
 * [Symfony Skeleton Installation](#Installation)
 * [Configuration Settings](#Congif)

## Prerequisites

In order to run this run-time system locally you will need a few tools installed:

  * [Git](https://git-scm.com/downloads)

  * [Docker](https://docs.docker.com/install/) 
  
  * [Docker-Compose](https://docs.docker.com/compose/install/)
  
  * [GNU Make](https://www.gnu.org/software/make/) 
    * [Windows Installation](https://chocolatey.org/packages/make)
        

## Installation

Clone the sf4d Git Repo from https://github.com/papahelmsman/sf4d to a new folder.


### 1.Cloning a repository

First, clone this repository :

``` bash
git clone https://github.com/papahelmsman/sf4d.git [path-tu-your-project-folder]
cd [path-tu-your-project-folder]
docker-compose up -d
```

Don't forget to add `sf4d.localhost` in your `hosts` file.

To run Docker, your machine must have a 64-bit operating system running Windows 7 or higher.

I use Docker Toolbox on Windows 7 (64-bit) and my host record is as follows:

```
192.168.99.100  sf4d.dockerhost
```

Check if your development environment is ready to go :

``` http request
sf4d.dockerhost
```

Your browser should redirect your request to secure connection:

``` http request
https://sf4d.dockerhost
```

And you should see your test `index` page.

```
Congrats! It works!
```

Now we can start development.

### 2.Installing a Symfony application

Next, put your Symfony application into `app` folder.

Stop your containers:

```
docker-compose down
```

Clean th `/app` folder. Remove `public` folder from `/app`.

Create Symfonyy application's template:

``` bash
composer create-project symfony/website-skeleton ./app
```

or if you prefer to use [`symfony` binary](https://symfony.com/download):

``` bash
symfony new --full ./app
```


Edit your doctrine cinfiguration file `//app/config/packages/doctrine.yaml`.

Add in the beginning:

``` yaml
parameters:
    # Adds a fallback DATABASE_URL if the env var is not set.
    # This allows you to run cache:warmup even if your
    # environment variables are not available yet.
    # You should not need to change this value.
    env(DATABASE_URL): ''
    
```

And change `dbal` section:

``` yaml
    dbal:
        # configure these for your database server
        driver: 'pdo_pgsql'
        server_version: '11.2'
        charset: utf8
        default_table_options:
            charset: utf8
            collate: ~

        url: '%env(resolve:DATABASE_URL)%'

        schema_filter: '~^(?!work_projects_tasks_seq)~'
```

Change the `DATABASE` parameters in `/app/.env`.

Comment out the following line:

``` dotenv
DATABASE_URL=mysql://db_user:db_password@127.0.0.1:3306/db_name
```

and add below:

``` dotenv
DATABASE_URL="pgsql://db_user:db_password@127.0.0.1:5432/db_name"
```
Substitute your credentials:

``` dotenv
DATABASE_URL=pgsql://symfonist:secret@192.168.99.100:54321/app_db
```


Then, run docker containers:

```bash
docker-compose up -d --build
```

### Use Adminer tool

``` http request
http://sf4d.dockerhost:2000/
```

### Default database credentials

System:     PostgreSQL
Server:     app-db
Username:   symfonist
Password:   secret
Database:   app_db 

You can change these credentials in the `.env` file and then rebuild containers using coamand:

``` bash
docker-compose up -d --build
```
