# Ограничение доступа

В файле /etc/nginx/conf.d/ваш\_конфиг.conf добавить строку, после "server {"

```
include /etc/nginx/conf.d/blacklist.conf;
```

В файле blacklist.conf, описываем подсети которым разрешен доступ к ERP:

```
allow 192.168.0.0/16; # Local 
allow 172.16.0.0/16; # Local
```

выполняем проверку конфига:

```
sudo nginx -t
```

если все успешно, выполняем рестарт nginx:

```
sudo /etc/init.d/nginx restart
```
