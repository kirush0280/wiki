# Установка САП

Сначала нужно подготовить операционную систему для установки ERP. Установка и настройка всех необходимых компонент описана в разделе «[Установка системных компонент](sistemnye-komponenty.md)».

### Создание каталога САП

```
sudo mdir -p /var/www/erp
sudo chown www-data:www-data /var/www/erp
cd /var/www/erp
```

Все инструкции далее будут показаны относительно текущего каталога **/var/www/erp**.

### Загрузка инсталляционной утилиты <a href="#bkmrk-d0-97-d0-b0-d0-b3-d1-80-d1-83-d0-b7-d0-ba-d0-b0-d0-b8-d0-bd-d1-81-d1-82-d0-b0-d0-bb-d0-bb-d1-8" id="bkmrk-d0-97-d0-b0-d0-b3-d1-80-d1-83-d0-b7-d0-ba-d0-b0-d0-b8-d0-bd-d1-81-d1-82-d0-b0-d0-bb-d0-bb-d1-8"></a>

```
sudo -u www-data wget -O install.phar https://d.cubalink.ru/install
```

### Запуск установки <a href="#bkmrk-d0-97-d0-b0-d0-bf-d1-83-d1-81-d0-ba-d1-83-d1-81-d1-82-d0-b0-d0-bd-d0-be-d0-b2-d0-ba-d0-b8" id="bkmrk-d0-97-d0-b0-d0-bf-d1-83-d1-81-d0-ba-d1-83-d1-81-d1-82-d0-b0-d0-bd-d0-be-d0-b2-d0-ba-d0-b8"></a>

```
sudo -u www-data php install.phar install
```

Нужно будет ввести ваш лицензионный ключ, выбрать версию ERP, ввести настройки подключения к базе данных, брокеру и redis, а также URL для ERP. Все эти учетные записи вы создали во время установки системных компонент.

После окончания установки нужно будет выполнить послеустановочную настройку.

### Настройка после установки <a href="#bkmrk-d0-9d-d0-b0-d1-81-d1-82-d1-80-d0-be-d0-b9-d0-ba-d0-b0-d0-bf-d0-be-d1-81-d0-bb-d0-b5-d1-83-d1-8" id="bkmrk-d0-9d-d0-b0-d1-81-d1-82-d1-80-d0-be-d0-b9-d0-ba-d0-b0-d0-bf-d0-be-d1-81-d0-bb-d0-b5-d1-83-d1-8"></a>

Скопируйте шаблоны конфигурационных файлов cron и supervisor:

```
sudo cp etc/us-core-worker.conf-example /etc/supervisor/conf.d/us-core-worker.conf
sudo cp microservice/poller/etc/usm_poller.conf-example /etc/supervisor/conf.d/usm_poller.conf
sudo cp etc/logrotate-example /etc/logrotate.d/cubalink
sudo cp microservice/poller/etc/logrotate-example /etc/logrotate.d/usm_poller
sudo cp etc/crontab-example /etc/cron.d/cubalink
```

Установите необходимые пакеты для работы poller.

```
cd microservice/poller
sudo -H python3.11 -m venv venv
sudo -H ./venv/bin/pip install -U pip wheel setuptools
sudo -H ./venv/bin/pip install -U -r requirements.txt
cd ../..
```

Перезапустите supervisor.

```
sudo systemctl restart supervisor
```

После запуска супервизора, спустя несколько секунд можно понаблюдать за состоянием всех контролируемых им служб. Все службы должны быть в состоянии RUNNING:

```
sudo supervisorctl status
```

