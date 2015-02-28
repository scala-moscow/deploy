# Deploy for all *.scala.moscow servers & containers


## Схема

Provisioning с помощью ansible, сервисы запускаются в контейнерах docker.

В данный момент используется один VDS с 512mb RAM и SSD, в котором стартуют все 
docker контейнеры. При необходимости количество VDS можно будет увеличить и 
разнести по ним docker контейнеры.

С помощью ansible playbook `setup_basehost0.yml` настраивается `basehost0` 
и docker контейнеры. Docker контейнеры создаются в нём на основе 
[phusion baseimage](https://github.com/phusion/baseimage-docker).
Основная конфигурация внутри контейнера делается тоже силами docker, 
а не Dockerfiles.

### Docker контейнеры

* `front` - входной nginx и 
  статические сайты 
  ([scala.moscow](https://github.com/scala-moscow/scala.moscow)).
* `hub` - [hub.scala.moscow](https://github.com/scala-moscow/hub.scala.moscow)


## Локальный запуск

* поставить [vagrant](https://www.vagrantup.com/downloads.html)
* поставить [ansible](http://docs.ansible.com/intro_installation.html#installation)
* находясь в корне репозитория `vagrant up`
* будет установлен vagrant машина с ip адресом `192.168.78.10`
* прописать в `/etc/hosts` домены для scala.moscow
```
192.168.78.10 scala.moscow.local hub.scala.moscow.local feed.scala.moscow.local
```

* запустить ansible для настройки `basehost0`
```
ansible-playbook -i vargant.hosts setup_basehost0.yml
```

* запустить ansible для настройки контейнеров *TODO*

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
