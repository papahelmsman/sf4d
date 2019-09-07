
<p align="center"><img src="docs/assets/img/head_logo.svg" width="250"></p>

<h1 style="text-align:center;">sf4d </h1>
<h4 style="text-align:center;">Symfony run-time system based on Docker and Docker-compose Tools</h4>
</br>



# Давайте начнём !

## Установка

### 1.Предварительные требования

    Прежде всего, необходимо убедиться, что на Вашем компьютере установлены инструменты Docker.
    
## Содержание

 * [Предварительные требования](#треюования)
 * [Установка рабочего окружения](#Installation)
 * [Установка приложения Symfony](#Installation)
 * [Настройка окружения](#Congif)

## Предварительные требования

Для локального запуска этого окружения вам понадобится установить несколько инструментов:

  * [Docker](https://www.docker.com/get-docker) - (You can also use the easy install script at [https://get.docker.com/](https://get.docker.com/))


## Установка рабочего окружения

Клонируйте репозиторий sf4d c веб-сервиса Github по  адресу:
(https://github.com/papahelmsman/sf4d)

или просто выполните команду:

```bash
$ git clone https://github.com/papahelmsman/sf4d.git [your-preferred-project-name]
```



Затем, войдите в каталог вновь созданного проекта:

```bash
$ cd ~/Projects/sf4d
```

и выполните следующие команды:

```bash
$ docker-compose build
```

```bash
$ docker-compose up -d
```

Следующая команда покажет список докер-контейнеров а также их актуальное состояние
```bash
$ docker ps -a
```

```bash
IMAGE                COMMAND                  CREATED             STATUS                     PORTS                                      NAMES
sf4d_h2-proxy        "nginx -g 'daemon of"   2 seconds ago       Up 4 seconds               0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   h2-proxy
sf4d_nginx           "nginx -g 'daemon of"   2 seconds ago       Up 4 seconds               0.0.0.0:8080->80/tcp                       nginx
sf4d_php-fpm         "docker-php-entrypoi"   3 seconds ago       Up 5 seconds               9000/tcp                                   php-fpm
sf4d_php-cli         "docker-php-entrypoi"   3 seconds ago       Exited (0) 5 seconds ago                                              php-cli
postgres:12-alpine   "docker-entrypoint.s"   4 seconds ago       Up 6 seconds               0.0.0.0:54321->5432/tcp                    pgsql
redis:5-alpine       "docker-entrypoint.s"   4 seconds ago       Up 6 seconds               0.0.0.0:6379->6379/tcp                     redis
```


### 2.Installing a Symfony application

Next, put your Symfony application into `app` folder and do not forget to add loal domain in your `hosts` file.

Make sure you adjust `database_host` in `parameters.yml` to the database container alias "db"

Then, run:

```bash
$ docker-compose up
