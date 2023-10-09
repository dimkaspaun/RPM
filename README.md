## Создать свой RPM пакет

**1. Cкачать новый бокс для VirtualBox https://app.vagrantup.com/almalinux/boxes/8**
   
**2. Создаем файл Vagranfile и запускаем образ.**
   
**Для данного задания нам понадобятся следующие установленные пакеты:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_1.png)

**● Для примера возьмем пакет NGINX и соберем его с поддержкой openssl**

**● Загрузим SRPM пакет NGINX для дальнейшей работы над ним:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_2.png)
![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_3.png)

**При установке такого пакета в домашней директории создается древо каталогов для
сборки:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_4.png)

**● Заранее поставим все зависимости, чтобы в процессе сборки не было ошибок**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_5.png)
![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_6.png)

**● Также нужно скачать и разархивировать последний исходник для openssl - он
потребуется при сборке**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_7.png)

**● Ну и собственно поправить сам spec файл, чтобы NGINX собирался с необходимыми нам опциями:**

Все содержимое скопировал в spec файл https://gist.github.com/lalbrekht/6c4a989758fccf903729fc55531d3a50

Скопировал папку openssl  в домашнюю папку  root 
--with-openssl=/root/openssl-1.1.1a

**● Теперь можно приступить к сборке RPM пакета:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_8.png)

**● Убедимся, что пакеты создались:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_9.png)

**● Теперь можно установить наш пакет и убедиться, что nginx работает**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_10.png)

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_11.png)

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_12.png)

## Создать свой репозиторий и разместить там ранее собранный RPM

**● Теперь приступим к созданию своего репозитория. Директория для статики у NGINX по умолчанию /usr/share/nginx/html. Создадим там каталог repo:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_13.png)



**Копируем туда наш собранный RPM и, например, RPM для установки репозитория Percona-Server:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_14.png)

**● Инициализируем репозиторий командой:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_15.png)

**● Для прозрачности настроим в NGINX доступ к листингу каталога:**

**● В location / в файле /etc/nginx/conf.d/default.conf добавим директиву autoindex on. В
результате location будет выглядеть так:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_16.png)

**● Проверяем синтаксис и перезапускаем NGINX:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_17.png)

**● Теперь ради интереса можно посмотреть в браузере или curl-анут:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_18.png)

**● Все готово для того, чтобы протестировать репозиторий.**

**● Добавим его в /etc/yum.repos.d:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_19.png)

**● Убедимся, что репозиторий подключился и посмотрим, что в нем есть:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_20.png)

**● Так как NGINX у нас уже стоит, установим репозиторий percona-release:**

![](https://github.com/dimkaspaun/RPM/blob/main/screen/1_21.png)
