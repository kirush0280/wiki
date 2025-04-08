# Кастомизация

В системе предусмотрены два файла, в которых Вы можете хранить свои java и css скрипты:

```
{DOCUMENT_ROOT}/public/main/js/user_script.js
{DOCUMENT_ROOT}/public/main/css/user_style.css
```

Если данные файлы отсутствуют, создайте их:

```
touch {DOCUMENT_ROOT}/public/main/js/user_script.js
touch {DOCUMENT_ROOT}/public/main/css/user_style.css
```

и присвойте им права:

```
chown www-data {DOCUMENT_ROOT}/public/main/js/user_script.js
chown www-data {DOCUMENT_ROOT}/public/main/css/user_style.css
```

Теперь можем попробовать изменить стиль, в файле user\_style.css, внесите изменения:

```
:root {
    --main-color-left-menu-icon: #008000;
}
```

{% hint style="warning" %}
Данные файлы не затираются при установке обновления.
{% endhint %}

Можно попробовать вариант предложенный @kirush80:

```
--main-color: #1871A5;
--main-color-hover: #3F51B5;
--main-color-left-menu-icon: #008000;
```
