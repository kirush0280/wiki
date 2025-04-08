# Миграция с Userside

Возможна миграция с ERP Userside версии 3.12 и более новой.

Убедитесь, что все необходимые [системные компоненты](sistemnye-komponenty.md) установлены. В зависимости от версии Userside, которую вы используете, у вас уже могут быть установлены те или иные компоненты. Убедитесь, что всё необходимое есть в наличии. Если чего-то не хватает — установите и выполните его настройку.

Сделайте резервную копию своего Userside — файлов и базы данных. Это обязательный шаг, потому как успешная миграция на Cubalink не может быть гарантирована в полной мере.

После того, как резервная копия выполнена, остановите работу cron (закомментируйте запуск userside cron и модулей), supervisor, nginx, php-fpm.

```
sudo systemctl stop supervisor
sudo systemctl stop nginx
sudo systemctl stop php-fpm
```

Служба из последней команды может называться иначе, например, php7.1-fpm, в зависимости от версии PHP, которая у вас используется.

### Перенастройка САП "Кубалинк"

Вам необходимо перенастроить установленные ранее для Userside компоненты.

Первым делом переименуйте основной каталог:

```
sudo mv /var/www/userside /var/www/erp
```

### PHP <a href="#bkmrk-php" id="bkmrk-php"></a>

Установите PHP 8.3 и все необходимые модули и выполните их настройку, как показано в разделах [Установка PHP](https://wiki.cuba-link.ru/books/sap-kubalink-EHP/page/ustanovka-sistemnyx-komponent#bkmrk-php) и [Настройка PHP](https://wiki.cuba-link.ru/books/sap-kubalink-EHP/page/ustanovka-sistemnyx-komponent#bkmrk-nginx-1).

### Nginx <a href="#bkmrk-nginx" id="bkmrk-nginx"></a>

Создайте каталог **/var/www/erp/public** и сделайте его владельцем пользователя www-data:

```
sudo mkdir -p /var/www/erp/public
sudo chown www-data:www-data /var/www/erp/public
```

Теперь нужно отредактировать файл настройки сервера NGINX. У вас он может называться по-разному или даже настройка для Userside может быть внутри какого-то другого файла конфигурации сервера. В самом простом случае вы можете удалить текущий файл и создать новый, как указано в [разделе про настройку Nginx после установки](https://docs.cubalink.ru/system_install.html#setup-nginx).

Если вы решили отредактировать ваш существующий файл, то нужно внести следующие изменения:

**Web root.** Строку:

```
/var/www/userside/userside3;
```

заменить на:

```
/var/www/erp/public
```

**Корневой location /.** Строку:

```
try_files $uri $uri/ =404;
```

заменить на:

```
try_files $uri $uri/ /index.php$is_args$args;
```

**fastcgi\_pass для php-fpm.** Строку:

```
fastcgi_pass unix:/run/php/php8.1-fpm.sock;
```

заменить на:

```
fastcgi_pass  unix:/run/php/php8.3-fpm.sock;
```

### Websocket пользователь <a href="#bkmrk-websocket-d0-bf-d0-be-d0-bb-d1-8c-d0-b7-d0-be-d0-b2-d0-b0-d1-82-d0-b5-1" id="bkmrk-websocket-d0-bf-d0-be-d0-bb-d1-8c-d0-b7-d0-be-d0-b2-d0-b0-d1-82-d0-b5-1"></a>

Если вы установили RabbitMQ только что перед процедурой миграции и создали всех пользователей по инструкции, то следующие команды не выполняйте и переходите к следующему разделу.

Если у вас Userside 3.17 и новее, то вероятней всего пользователь для websocket у вас уже есть.

Если вы сомневаетесь, есть ли у вас уже пользователь для websocket, выполните команду:

```
sudo rabbitmqctl list_users
```

Если среди пользователей вы видите пользователя с именем похожим на websock или на stomp, вероятно такой пользтватель уже есть. Посмотрите, какие права он имеет (вместо `имя_пользователя` укажите имя найденного пользователя):

```
sudo rabbitmqctl list_user_permissions имя_пользователя
```

Если в результате вы видите права доступа вроде таких:

```
user	configure	write	read
websocket	^userside-stomp:id-.*		^userside-stomp:id-.*
```

то это точно означает, что пользователь для websocket у вас уже есть.

В этом случае вам нужно изменить права доступа, выполнив следующие команды:

```
sudo rabbitmqctl clear_permissions имя_пользователя
sudo rabbitmqctl set_permissions имя_пользователя "^erp-stomp:id-.*" "" "^erp-stomp:id-.*"
```

Здесь также не забудьте указать имя настоящего пользователя вместо `имя_пользователя`.

### Postgres <a href="#bkmrk-postgres" id="bkmrk-postgres"></a>

Рекомендуется использовать последние стабильные версии PostgreSQL, так как помимо расширения функциональности они в некоторых случаях работают заметно быстрее.

Вы можете обновить [кластер](https://www.postgresql.org/docs/current/glossary.html) (так называется набор баз данных даже на одном сервере, даже если база данных одна) на последнюю версию. Для этого существуют готовые скрипты под debian и ubuntu из пакета [postgresql-common](https://packages.debian.org/sid/postgresql-common).

Документация по обновлению кластера от Postgres: [https://www.postgresql.org/docs/current/upgrading.html](https://www.postgresql.org/docs/current/upgrading.html)

{% hint style="danger" %}
Не забудьте об обязательном резервном копировании баз данных перед подобными операциями.
{% endhint %}

### Перезапуск служб <a href="#bkmrk-d0-9f-d0-b5-d1-80-d0-b5-d0-b7-d0-b0-d0-bf-d1-83-d1-81-d0-ba-d1-81-d0-bb-d1-83-d0-b6-d0-b1" id="bkmrk-d0-9f-d0-b5-d1-80-d0-b5-d0-b7-d0-b0-d0-bf-d1-83-d1-81-d0-ba-d1-81-d0-bb-d1-83-d0-b6-d0-b1"></a>

После редактирования конфигурации нужно перезапустить все затронутые службы:

```
sudo systemctl restart php8.3-fpm
sudo systemctl restart nginx
```

### Запуск процедуры миграции <a href="#bkmrk-d0-97-d0-b0-d0-bf-d1-83-d1-81-d0-ba-d0-bf-d1-80-d0-be-d1-86-d0-b5-d0-b4-d1-83-d1-80-d1-8b-d0-b" id="bkmrk-d0-97-d0-b0-d0-bf-d1-83-d1-81-d0-ba-d0-bf-d1-80-d0-be-d1-86-d0-b5-d0-b4-d1-83-d1-80-d1-8b-d0-b"></a>

Процедура миграции ничем не отличается от процедуры новой инсталляции. Поэтому вы можете обратиться к главе [Установка ERP](ustanovka-sap.md) и выполнять все действия последовательно из нее (кроме создания каталога /var/www/erp, так как он у вас уже существует).
