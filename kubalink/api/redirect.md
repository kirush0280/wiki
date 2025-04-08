---
description: Переадресация на карточку объекта по какому-то признаку
---

# redirect

{% code overflow="wrap" %}
```
Дополнительные параметры:
action - тип объекта (возможное значение: abon, switch)
typer - тип анализируемых данных (возможное значение: для abon: tel, ip, dognumber; для switch: ip, additional_data)
value - данные (текстовое значение)
```
{% endcode %}

Пример запроса:

```
api.php?key=apikey&cat=redirect&action=abon&typer=tel&value=380971234567
```
