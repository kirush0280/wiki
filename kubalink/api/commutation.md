---
description: Коммутация объектов
---

# commutation

```
Дополнительные параметры:
action - подкатегория запроса
```

## Подкатегории

### **add**

```
Описание: Коммутация объектов
Обязательные параметры:
 object_type - тип объекта [customer|switch|fiber|cross|splitter]
 object_id - id объекта
 object1_side - сторона объекта 1 (для кабельных линий)
 object1_port - порт объекта 1
 object2_type - тип объекта 2 [switch|fiber|cross|splitter]
 object2_id - id объекта 2
 object2_side - сторона объекта 2 (для кабельных линий)
 object2_port - порт объекта 2
```

### **delete**

```
Описание: Очистка коммутации
Обязательные параметры:
 object_type - Тип объекта [customer|device]
 object_id - id объекта
Небязательные параметры:
 object_port - Номер порта (для device)
```

### **get\_data**

```
Описание: Получение массива коммутации
Обязательные параметры:
 object_type - Тип объекта для выборки [customer|switch|radio|cross|fiber|splitter]
Необязательные параметры:
 object_id - id объекта для выборки
 is_finish_data - Флаг - выводить конечную точку коммутации
Дополнительно возвращаемые данные:
 array(
   [data] = array(
     [object_type] => Тип объекта
     [object_id] => id объекта
     [direction] => Сторона коммутации (например для ВОЛС)
     [interface] => Номер интерфейса
     [comment] => Заметки
     [connect_id] => id записи о коммутации
   )
```
