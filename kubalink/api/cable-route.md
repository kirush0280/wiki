---
description: Кабельные трассы и каналы
---

# cable route

```
Дополнительные параметры:
action - подкатегория запроса
```

ID типов начальных и конечных объектов трассы:

```
1 - абонент
19 - здание
22 - сооружение связи
```

## Подкатегории

### **add\_route**

```
Описание: Добавление кабельной трассы
Обязательные параметры:
 object_first_type - тип начального объекта
 object_first_id - id начального объекта
 object_second_type - тип конечного объекта
 object_second_id - id конечного объекта
Дополнительные параметры:
 name - наименование
 comment - заметка
 length - длина
 date_install - дата фактической установки
```

### **add\_duct**

```
Описание: Добавление кабельного канала
Обязательные параметры:
 cable_route_id - id кабельной трассы
Дополнительные параметры:
 number - номер
 comment - заметка
 diameter - диаметр
 date_install - дата фактической установки
```

### **get\_route**

```
Описание: Список кабельных трасс
Обязательные параметры:
 нет
Дополнительные параметры:
 id - id объектов (можно через запятую)
```

### **get\_duct**

```
Описание: Список кабельных каналов
Обязательные параметры:
 нет
Дополнительные параметры:
 id - id объектов (можно через запятую)
 cable_route_id - id кабельной трассы (можно через запятую)
```
