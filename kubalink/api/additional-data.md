---
description: Действие с дополнительными полями/данными
---

# additional data

```
Дополнительные параметры:
action - подкатегория запроса
```

Дополнительные поля имеют категории (cat\_id)

```
6 - Радиооборудование
7 - Здания
8 - Коммутаторы
9 - Медиаконвертеры
10 - Системные устройства
12 - Тарифы (только для ручных биллингов)
13 - Дополнительные услуги (только для ручных биллингов)
14 - Сооружения связи
15 - Кроссы/ODF
16 - VLAN
17 - Задания
18 - Автотранспорт
19 - Рекламные кампании
20 - Произвольные устройства
21 - Поставщики
23 - Делители/Уплотнители
24 - Собственники
25 - ТМЦ
26 - Кабельные каналы
27 - Кабельные трассы (кабельных линий)
28 - Абоненты
29 - Ключи
30 - Наименования ТМЦ
40 - Адресные единицы
48 - Склады
102 - Объекты на карте
999 - Сотрудники
```

\
Дополнительные поля имеют тип поля (type)

```
1 - Текст
2 - Число
3 - Флаг
4 - Выбор из списка
5 - Текстовое поле
6 - Выбор из списка (в т.ч. свой вариант)
7 - Дата
8 - Выбор из списка (несколько значений)
```

## Подкатегории

### **get\_list**

{% code overflow="wrap" %}
```
Описание: Получение списка полей
Обязательные параметры:
 section - Категория дополнительных полей [house|node|task|switch|inventory|...числовые значения из каталога выше...]
```
{% endcode %}

### **add\_field**

```
Описание: Добавление доп.поля 
Обязательные параметры:
 cat_id - категория (см.выше справочник)
 name - наименование
Необязательные параметры
 type - тип поля (см.выше справочник)
 size - размер поля
 max_size - максимальный размер поля
 is_active - флаг - поле включено
 position - позиция поля среди остальных
 is_require - флаг - обязательное к заполнению
```

### **edit\_field**

{% code overflow="wrap" %}
```
Описание: Редактирование доп.поля 
Обязательные параметры:
 cat_id - категория (см.выше справочник)
 id - id поля
Необязательные параметры
 См. из метода add_field
 value_list - возможные значения для типа поля "Выбор из списка" (разделитель - вертикальная черта "|")
```
{% endcode %}

### **delete\_field**

```
Описание: Удаление доп.поля (удаляется только если нет записей с этим доп.полем)
Обязательные параметры:
 cat_id - категория (см.выше справочник)
 id - id поля
```

### **get\_value**

```
Описание: Получение значений полей
Обязательные параметры:
 field_id - id поля
Необязательные параметры:
 cat_id - категория (см.выше справочник)
 object_id - id объекта (по которому значение поля)
 value - значение поля
```

### **change\_value**

```
Описание: Изменение значения доп.поля 
В случае отсутствия такого доп.поля у объекта - оно будет создано.
Обязательные параметры:
 field_id - id дополнительного поля
 object_id - id объекта
 value - значение
 cat_id - категория (см.выше справочник)
```

### **change\_value\_mass**

```
Описание: Массовое изменение значения доп.поля для множества объектов
В случае отсутствия такого доп.поля у объекта - оно будет создано.
Обязательные параметры:
 cat_id - категория (см.выше справочник)
 field_id - id дополнительного поля
 data[] - id объекта|значение
 data[] - id объекта|значение
 data[] - id объекта|значение
 ...
```
