# Уведомления в Telegram

[![image.png](https://wiki.cuba-link.ru/uploads/images/gallery/2024-11/scaled-1680-/ynzimage.png)](https://wiki.cuba-link.ru/uploads/images/gallery/2024-11/ynzimage.png)

Переходим в сотрудника, которому хотим настроить уведомления, нажимаем снизу "редактировать".

Поле "Уведомления - Telegram chat\_id" должно быть заполнено. Как узнать ID сотрудника? В недавном времени в telegram появился такой функционал в разделе Настройки->Расширенные настройки->Экспериментальные настройки

[![image.png](https://wiki.cuba-link.ru/uploads/images/gallery/2024-11/scaled-1680-/CAwimage.png)](https://wiki.cuba-link.ru/uploads/images/gallery/2024-11/CAwimage.png)

Теперь кликнув на аватарку сотрудника в Telegram, Вы можете найти его ID.

Нужно зарегистрировать бота в telegram, описывать процедуру регистрации не будем - много статей в интернете.

Переходим в Настройки->Уведомления->Messenger, активируем и заполняем поле Bot token, сюда вписывает API токен полученный при регистрации.

[![image.png](https://wiki.cuba-link.ru/uploads/images/gallery/2024-11/scaled-1680-/W5timage.png)](https://wiki.cuba-link.ru/uploads/images/gallery/2024-11/W5timage.png)

{% hint style="info" %}
Сотрудник, который хочет получать уведомления должен первым написать боту любое сообщение. После того как он написал, можно проверять - создать заявку на данного сотрудника и в заявке нажать ссылку Telegram, сотруднику в течение 1 минуты должно поступить уведомление с заявкой.
{% endhint %}

На какой тип заявки отправлять уведомления можно настроить в Настройка->Задания, в настройках необходимого задания.
