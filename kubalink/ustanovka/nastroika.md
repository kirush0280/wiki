# Настройка

Следующие настройки вам пригодятся дальше при [установке ](sistemnye-komponenty.md)САП "Кубалинк", поэтому запишите создаваемые имена пользователей, их пароли, названия базы данных и т.д.

### База данных Postgresql <a href="#bkmrk-d0-91-d0-b0-d0-b7-d0-b0-d0-b4-d0-b0-d0-bd-d0-bd-d1-8b-d1-85-postgres-1" id="bkmrk-d0-91-d0-b0-d0-b7-d0-b0-d0-b4-d0-b0-d0-bd-d0-bd-d1-8b-d1-85-postgres-1"></a>

Создать пользователя базы данных, базу данных и активировать расширение PostGIS в ней. Вместо `имя_пользователя` укажите имя создаваемого пользователя. После выполнения первой команды нужно будет дважды ввести пароль создаваемого пользователя.

```
sudo -u postgres createuser имя_пользователя -P
sudo -u postgres createdb -e -E "UTF-8" -l "ru_RU.UTF-8" -O имя_пользователя -T template0 cubalink
sudo -u postgres psql -d cubalink -c "CREATE EXTENSION postgis"
```

### RabbitMQ <a href="#bkmrk-rabbitmq-1" id="bkmrk-rabbitmq-1"></a>

Создайте файл **/etc/rabbitmq/rabbitmq.conf** с настройками:

```
listeners.tcp.default = 5672
web_stomp.port = 15674
web_stomp.cowboy_opts.max_keepalive = 60
```

Теперь нужно создать пользователя с полными правами для ERP и еще одного пользователя с ограниченными правами для WebSocket.

Вместо `имя_пользователя` (`имя_websocket_пользователя`) и `пароль_пользователя` (`пароль_websocket_пользователя`) укажите соответственно имя и пароль создаваемого пользователя.

Основной пользователь:

```
sudo rabbitmqctl add_user имя_пользователя пароль_пользователя
sudo rabbitmqctl set_user_tags имя_пользователя administrator monitoring
sudo rabbitmqctl set_permissions имя_пользователя ".*" ".*" ".*"
```

WebSocket пользователь:

```
sudo rabbitmqctl add_user имя_websocket_пользователя пароль_websocket_пользователя
sudo rabbitmqctl set_permissions имя_websocket_пользователя "^erp-stomp:id-.*" "" "^erp-stomp:id-.*"
```

Имя и пароль этого пользователя вам нужно будет ввести в настройках ERP после установки.

### PHP <a href="#bkmrk-php-1" id="bkmrk-php-1"></a>

* В файлах /etc/php/8.3/fpm/php.ini и /etc/php/8.3/fpm/fpm.ini укажите ваш часовой пояс в `date.timezone`

{% code title="/etc/php/8.3/fpm/php.ini" %}
```
max_execution_time = 300

post_max_size = 100M
upload_max_filesize = 100M

cgi.fix_pathinfo = 0

```
{% endcode %}

{% code title="/etc/php/8.3/fpm/pool.d/www.conf" %}
```
request_terminate_timeout = 300
```
{% endcode %}

* Настройте ProcessManager следующим образом:

{% code title=" /etc/php/8.3/fpm/pool.d/www.conf " %}
```
pm.max_children = 75
pm.min_spare_servers = 4
pm.max_spare_servers = 8
pm.start_servers = 8
```
{% endcode %}

### Redis <a href="#bkmrk-redis-1" id="bkmrk-redis-1"></a>

Вы можете дополнительно настроить пароль, но в этом нет необходимости, если вы будете использовать Redis изолированно на том же сервере. Пароль настраивается в файле /etc/redis/redis.conf в параметре `requirepass`.

### Nginx <a href="#bkmrk-nginx-1" id="bkmrk-nginx-1"></a>

В конфигурационном файле /etc/nginx/nginx.conf измените значение для `user` на:

```
user www-data www-data;
```

Удалите файл /etc/nginx/conf.d/default.conf и вместо него создайте новый файл со следующим содержимым (вместо `erp.mycompany.com` укажите ваше доменное имя):

```
server {
    listen       80 default_server;
    server_name  erp.mycompany.com;
    charset      utf-8;
    client_max_body_size 100M;

    access_log  /var/log/nginx/erp-access.log;
    error_log   /var/log/nginx/erp-error.log;

    root   /var/www/erp/public;
    index  index.php;

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~* ^.+\.(css|js|ogg|ogv|svg|svgz|eot|otf|woff|mp4|ttf|rss|atom|jpg|jpeg|gif|png|ico|zip|tgz|gz|rar|bz2|doc|xls|exe|ppt|tar|mid|midi|wav|bmp|rtf)$ {
        access_log    off;
        log_not_found off;
        expires       max;
        add_header    Pragma public;
        add_header    Cache-Control "public";
    }

    location ~ \.php$ {
        try_files     $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass  unix:/run/php/php8.3-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_read_timeout 300;
        include       fastcgi_params;
    }

    location /ws {
        proxy_pass http://127.0.0.1:15674/ws;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header Host $host;
    }

    location ~ /\.ht { deny  all; }
}
```

### Перезапуск <a href="#bkmrk-d0-9f-d0-b5-d1-80-d0-b5-d0-b7-d0-b0-d0-bf-d1-83-d1-81-d0-ba" id="bkmrk-d0-9f-d0-b5-d1-80-d0-b5-d0-b7-d0-b0-d0-bf-d1-83-d1-81-d0-ba"></a>

Перезапустите операционную систему целиком или все настраиваемые службы:

```
sudo systemctl restart rabbitmq-server
sudo systemctl restart php8.3-fpm
sudo systemctl restart nginx
sudo systemctl restart redis
```
