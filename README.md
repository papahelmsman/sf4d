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
  
  * [Docker-Compose](https://getcomposer.org/)
  
  * [GNU Make](https://getcomposer.org/) 
  
        

## Installation

Clone the sf4d Git Repo from https://github.com/papahelmsman/sf4d to a new folder structure martingale/ui:


### 1.Cloning a repository

First, clone this repository :

``` bash
git clone https://github.com/papahelmsman/sf4d.git [path-tu-your-project-folder]
cd [path-tu-your-project-folder]
docker-compose up -d
```

### 2.Installing a Symfony application

Next, put your Symfony application into `app` folder and do not forget to add loal domain in your `hosts` file.

Make sure you adjust `database_host` in `parameters.yml` to the database container alias "db"

Then, run:

```bash
$ docker-compose up -d
