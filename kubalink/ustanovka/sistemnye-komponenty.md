# Системные компоненты

Для работы Cubalink ERP нужно установить следующие компоненты:

1. PostgreSQL + PostGIS
2. RabbitMQ + WebSTOMP + Management
3. PHP 8.3 с расширениями ctype, gd, json, libxml, mbstring, openssl, pdo, pdo\_pgsql, posix, simplexml, snmp, sockets, zlib, pcntl
4. Redis
5. Python 3.11 + venv + pip + dev
6. Supervisor
7. NGINX или другой WEB-сервер

{% hint style="danger" %}
Пожалуйста, используйте только актуальные поддерживаемые версии операционных систем, например, **Debian 12 bookworm**, чтобы не возникло проблем с установкой или обновлениями компонент. Некоторые компоненты не могут быть установлены на операционные системы, для которых закончилась поддержка.
{% endhint %}

### PostgreSQL <a href="#bkmrk-postgresql" id="bkmrk-postgresql"></a>

Инструкции по установке под вашу операционную систему доступны [на официальном сайте](https://www.postgresql.org/download/).

Рекомендуется явно устанавливать версию 16. Не забудьте про расширение PostGIS-3.

```
sudo apt install -y postgresql-16 postgresql-16-postgis-3
```

После установки желательно [выполнить настройку](https://pgconfigurator.cybertec.at/) Postgres для достижения максимальной производительности.

### RabbitMQ <a href="#bkmrk-rabbitmq" id="bkmrk-rabbitmq"></a>

Инструкции по установки под вашу операционную систему доступны [на официальном сайте](https://www.rabbitmq.com/docs/platforms).

После установки Erlang и RabbitMQ вам нужно будет активировать плагины: rabbitmq\_management и rabbitmq\_web\_stomp.

```
sudo rabbitmq-plugins enable rabbitmq_management --offline
```

и

```
sudo rabbitmq-plugins enable rabbitmq_web_stomp --offline
```

### PHP <a href="#bkmrk-php" id="bkmrk-php"></a>

PHP необходим версии 8.3. Другие версии не поддерживаются. Необходимо установить php и требуемый набор расширений. Если вы планируете использовать WEB-сервер NGINX, то установите расширение php-fpm, как показано далее; если Apache2, то php-fpm устанавливать не нужно, вместо этого установите apache2-php.

```
sudo apt install -y php8.3-{fpm,cli,common,curl,intl,mbstring,opcache,pgsql,readline,xml,zip,snmp,gd}
```

### Redis <a href="#bkmrk-redis" id="bkmrk-redis"></a>

Инструкции по установке под вашу операционную систему доступны [на официальном сайте](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/).

### Python <a href="#bkmrk-python" id="bkmrk-python"></a>

Подходит Python 3.9 и новее. Например, Debian 12 содержит версию Python 3.11. Если у вас версия Python ниже 3.9, то вам нужно обновить Python.

В любом случае вам нужно установить следующие дополнительные компоненты:

* venv
* pip

На Debian 12 это делается следующим образом:

```
sudo apt install -y python3-venv python3-pip python3-dev
```

### Supervisor <a href="#bkmrk-supervisor" id="bkmrk-supervisor"></a>

Supervisor является пакетом Python. Установите supervisor одним из подходящих способов, описанных [на официальном сайте](http://supervisord.org/installing.html).

Для Debian также существует системный пакет, который можно установить используя **apt**.

### Nginx <a href="#bkmrk-nginx" id="bkmrk-nginx"></a>

Инструкции по установке под вашу операционную систему доступны [на официальном сайте](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/).
