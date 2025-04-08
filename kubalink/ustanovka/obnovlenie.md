# Обновление

### Обновление файлов системы САП <a href="#bkmrk-d0-9e-d0-b1-d0-bd-d0-be-d0-b2-d0-bb-d0-b5-d0-bd-d0-b8-d0-b5-d1-84-d0-b0-d0-b9-d0-bb-d0-be-d0-b" id="bkmrk-d0-9e-d0-b1-d0-bd-d0-be-d0-b2-d0-bb-d0-b5-d0-bd-d0-b8-d0-b5-d1-84-d0-b0-d0-b9-d0-bb-d0-be-d0-b"></a>

Для обновления нужно перейти в каталог с установленной САП и выполнить команду установки:

```
cd /var/www/erp
sudo -u www-data php install.phar install
```

Если есть более новая версия, будет предложено обновиться на нее. Можно указать порядковый номер версии из списка (например, `1`) или ввести версию вручную (например, `7.25`).

### Обновление окружения для служб <a href="#bkmrk-d0-9e-d0-b1-d0-bd-d0-be-d0-b2-d0-bb-d0-b5-d0-bd-d0-b8-d0-b5-d0-be-d0-ba-d1-80-d1-83-d0-b6-d0-b" id="bkmrk-d0-9e-d0-b1-d0-bd-d0-be-d0-b2-d0-bb-d0-b5-d0-bd-d0-b8-d0-b5-d0-be-d0-ba-d1-80-d1-83-d0-b6-d0-b"></a>

После обновления ERP нужно обновить и компоненты, необходимые для работы служб.

```
cd /var/www/erp/microservice/poller
sudo venv/bin/pip install -r requirements.txt
sudo supervisorctl restart all
```

На этом процедура обновления завершена.
