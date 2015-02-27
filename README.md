# Deploy for all *.scala.moscow servers & containers

## Схема

Provisioning с помощью ansible, сервисы запускаются в контейнерах docker.

В данный момент используется один VDS с 512mb RAM и SSD, в котором стартуют все 
docker контейнеры. При необходимости количество VDS можно будет увеличить и 
разнести по ним docker контейнеры.


### Docker контейнеры

* nginx front
* www - [scala.moscow](https://github.com/scala-moscow/scala.moscow)
* hub - [hub.scala.moscow](https://github.com/scala-moscow/hub.scala.moscow)


## Локальный запуск

* поставить [vagrant](https://www.vagrantup.com/downloads.html)
* поставить [ansible](http://docs.ansible.com/intro_installation.html#installation)
* находясь в корне репозитория `vagrant up`
* будет установлен vagrant машина с ip адресом `192.168.78.10`
* прописать в `/etc/hosts` домены для scala.moscow
```
192.168.78.10 scala.moscow hub.scala.moscow feed.scala.moscow
```
* запустить ansible для настройки host'ов *TODO*
* запустить ansible для настройки контейнеров *TODO*


## Production запуск
* *TODO*
