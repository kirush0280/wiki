---
description: SMS-сообщения
---

# sms

```
Дополнительные параметры:
action - подкатегория запроса
```

## Подкатегории

### **send**

```
Описание: Отправка сообщения
Обязательные параметры:
 number - номер телефона
 msg - текст сообщения
Необязательные параметры:
 customer_id - ID абонента, к которому прикрепить SMS
Дополнительно возвращаемые данные:
 array(
  [id] => ID отправленного сообщения
 )
```

### **status**

```
Описание: Информация о сообщения
Обязательные параметры:
 id - ID сообщения (возможна подача нескольких значений через запятую)
Дополнительно возвращаемые данные:
 array(
  [data] => массив данных о сообщении
 )
```
