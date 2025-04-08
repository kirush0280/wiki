# API: как добавить ONU

Добавляем ONU на склад:\
&#x20;**cat=inventory\&action=add\_inventory**

```
Описание: Приход ТМЦ
Обязательные параметры:
 inventory_catalog_id - ID наименования ТМЦ
 trader_id - ID поставщика
 storage_id - ID склада, на который выполнить приход
Необязательные параметры:
 amount - количество (по-умолчанию: 1)
 cost - стоимость (по-умолчанию: 0)
 comment - заметки
 sn - серийный номер
 barcode - штрихкод
 inventory_number - инвентарный номер
 document_number - номер документа прихода
 document_date - дата документа прихода
 additional_data_ip - IP-адрес (для ТМЦ-оборудования)
 additional_data_mac - MAC-адрес (для ТМЦ-оборудования)
 is_check_serial_number - проверять на совпадение серийный номер с уже существующими ТМЦ
```

Перемещаем ONU на абонента\
**cat=inventory\&action=transfer\_inventory**

```
Описание: Перемещение ТМЦ
Обязательные параметры:
 inventory_id - ID ТМЦ
 dst_account - Счет-получатель
Необязательные параметры
 comment - заметки
 employee_id - ID сотрудника - автора операции
```

Выполняем кроссировку\
**cat=commutation\&action=add**

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

