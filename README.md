# Deploy for all *.scala.moscow servers & containers


## Схема

Настройка с помощью [ansible](http://docs.ansible.com/index.html),
сервисы запускаются в контейнерах [docker](https://docs.docker.com/).

В данный момент используется один VDS с 512mb RAM и SSD, в котором стартуют все 
docker контейнеры. При необходимости количество VDS можно будет увеличить и 
разнести по ним docker контейнеры.

С помощью ansible playbook `setup_basehost0.yml` настраивается `basehost0` 
и docker images внутри него, но не создаются контейнеры. Docker images создаются
на основе [phusion baseimage](https://github.com/phusion/baseimage-docker).

Image создаются только если image с таким названием и версией ещё нет в локальном хранилище.
Поэтому для пересборки image нужно поднять в [group_vars/basehosts](group_vars/basehosts)
соотвествующую версию в настройке `docker_%NAME%_image_version`.

Основная конфигурация внутри images делается силами ansible, а не Dockerfiles.
Для этого создаётся временный контейнер, который настраивается с помощью ansible через
playbook с названием `setup_%IMAGE%_image.yml`. После конфигурации через ansible
изменения во временном конейтнере commit'яться и получается конечный image.

На основе созданных images уже строятся различные контейнеры.

### Docker images

* `base` - phusion baseimage (ubuntu 14.04) + ansible
* `nginx` - `base` + nginx

### Docker контейнеры

* `front` - на основе `nginx`: входной nginx и статические сайты
  ([scala.moscow](https://github.com/scala-moscow/scala.moscow)).
* `hub` - *TODO* - [hub.scala.moscow](https://github.com/scala-moscow/hub.scala.moscow)


## Локальный запуск

* поставить [vagrant](https://www.vagrantup.com/downloads.html)
* поставить [ansible](http://docs.ansible.com/intro_installation.html#installation)
* находясь в корне репозитория `vagrant up`
* будет запущена vagrant машина с ip адресом `192.168.78.10`
* прописать в `/etc/hosts` домены для scala.moscow
```
192.168.78.10 scala.moscow.local hub.scala.moscow.local feed.scala.moscow.local
```

* запустить ansible для настройки `basehost0`
```
ansible-playbook -i vargant.hosts setup_basehost0.yml
```

* запустить ansible для создания и настройки контейнера `front` *TODO*

* запустить ansible для создания и настройки контейнера `hub` *TODO*

### Shell доступ

* basehost0
```
vagrant ssh
```

* контейнеры
```
vagrant ssh
docker exec -ti NAME bash
```

## Production запуск

* *TODO*
