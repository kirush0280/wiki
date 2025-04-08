# API

Данный раздел описывает возможности использования встроенного API, который позволяет интегрировать функционал системы в сторонние проекты и приложения.

**Принцип работы**

Взаимодействие с API осуществляется через файл `/api.php`. Поддерживаются как GET, так и POST запросы.

**Входящие параметры:**

**Обязательные параметры:**

* `key` — ключ API, необходимый для авторизации запроса.
* `cat` — категория запроса, определяющая тип выполняемой операции.

**Необязательные параметры:**

* `skip_internal_api` — флаг, указывающий на необходимость отключения внутренних триггеров системы. Рекомендуется использовать, если ваш метод API является реакцией на определённый триггер, чтобы избежать зацикливания.

**Дополнительные параметры:**\
В зависимости от категории запроса могут потребоваться дополнительные параметры. Например:

* `customer_id` — идентификатор абонента.
* `is_potential` — флаг, который может принимать значения `1` или `0`. Большинство флагов имеют префикс `is_`.

**Пример запроса**

```html
api.php?key=apikey&cat=abon&action=msg&usercode=1
```

**Возвращаемые данные**

Если запрос предполагает выполнение действия или возврат информации, данные будут возвращены в формате JSON. Пример структуры ответа:

```json
{
  [Result]: "OK / ERROR",
  [ErrorText]: "В случае ошибки - текст ошибки"
}
```

Также рекомендуется проверять HTTP-код ответа. В случае возникновения ошибок или некорректных запросов, HTTP-код будет отличаться от `200`.

**Примечания**

{% hint style="danger" %}
Убедитесь, что используемый ключ API имеет необходимые права доступа для выполнения запрашиваемой операции.
{% endhint %}

{% hint style="warning" %}
В случае ошибки, поле `ErrorText` будет содержать описание проблемы, что поможет в диагностике.
{% endhint %}

Этот API предоставляет гибкие возможности для интеграции и автоматизации процессов, что делает его мощным инструментом для разработчиков.

## Категории

* [address](https://wiki.cuba-link.ru/kubalink/api/address) - Адреса
* [attach](https://wiki.cuba-link.ru/kubalink/api/attach) - Прикрепляемые файлы
* [additional\_data](https://wiki.cuba-link.ru/kubalink/api/additional-data) - Дополнительные поля/данные для объектов
* [advertising](https://wiki.cuba-link.ru/kubalink/api/advertising) - Рекламные кампании
* [billing](https://wiki.cuba-link.ru/kubalink/api/billing) - Биллинги
* [cable\_route](https://wiki.cuba-link.ru/kubalink/api/cable-route) - Кабельные трассы и каналы
* [call](https://wiki.cuba-link.ru/kubalink/api/call) - Звонки
* [commutation](https://wiki.cuba-link.ru/kubalink/api/commutation) - Коммутация объектов
* [cross](https://wiki.cuba-link.ru/kubalink/api/cross) - ODF/Кроссы
* [customer](https://wiki.cuba-link.ru/kubalink/api/customer) - Абоненты. Большинство действий актуально для ручных биллингов
* [cwdm](https://wiki.cuba-link.ru/kubalink/api/cwdm) - CWDM
* [device](https://wiki.cuba-link.ru/kubalink/api/device) - Оборудование
* [employee](https://wiki.cuba-link.ru/kubalink/api/employee) - Сотрудники&#x20;
* [fiber](https://wiki.cuba-link.ru/kubalink/api/fiber) - Кабельные линии
* [gps](https://wiki.cuba-link.ru/kubalink/api/gps) - GPS-трекеры
* [inventory](https://wiki.cuba-link.ru/kubalink/api/inventory) - Склад
* [key](https://wiki.cuba-link.ru/kubalink/api/key) - Ключи
* [map](https://wiki.cuba-link.ru/kubalink/api/map) - Карты покрытия
* [newin](https://wiki.cuba-link.ru/kubalink/api/newin) - Заявка на подключение
* [node](https://wiki.cuba-link.ru/kubalink/api/node) - Сооружения связи _(узлы связи, муфты, опоры, колодцы)_
* [notepad](https://wiki.cuba-link.ru/kubalink/api/notepad) - Блокнот&#x20;
* [owner](https://wiki.cuba-link.ru/kubalink/api/owner) - Собственники объектов
* [redirect](https://wiki.cuba-link.ru/kubalink/api/redirect) - Переадресация на карточку объекта по какому-то признаку
* [service](https://wiki.cuba-link.ru/kubalink/api/service) - Дополнительные услуги
* [setting](https://wiki.cuba-link.ru/kubalink/api/setting) - Настройка
* [sms](https://wiki.cuba-link.ru/kubalink/api/sms) - SMS-сообщения
* [splitter](https://wiki.cuba-link.ru/kubalink/api/splitter) - Делители/уплотнители
* [system](https://wiki.cuba-link.ru/kubalink/api/system) - Системная информация и операции
* [tariff](https://wiki.cuba-link.ru/kubalink/api/tariff) - Тарифы
* [task](https://wiki.cuba-link.ru/kubalink/api/task) - Задания
* [trader](https://wiki.cuba-link.ru/kubalink/api/trader) - Поставщики
* [vehicle](https://wiki.cuba-link.ru/kubalink/api/vehicle) - Автотранспорт
* [vlan](https://wiki.cuba-link.ru/kubalink/api/vlan) - Vlan
