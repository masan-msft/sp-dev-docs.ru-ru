# <a name="known-issues-and-frequently-asked-questions"></a>Известные проблемы и часто задаваемые вопросы

На этой странице представлены известные проблемы и ответы на часто задаваемые вопросы о SharePoint Framework. 

## <a name="known-issues"></a>Известные проблемы

**Проблема с сертификатом разработчика в Chrome (версии 58 и новее)**

- *Дата: 28 апреля*
- *Обновление: 2 мая*

Если вы используете браузер Chrome для разработки, у вас могут возникнуть проблемы с сертификатом разработчика независимо от того, выполняется ли команда `gulp trust-dev-cert`. В Chrome 58 изменилась модель проверки сертификатов, и во время доступа к локальной рабочей области может появиться такое сообщение: "Ваше подключение не защищено".

Следует обновить пакеты шаблонов Yeoman. Мы обновили логику создания сертификатов в пакете *@microsoft/gulp-core-build-serve*. Для существующих решений вы можете просто удалить эту папку и выполнить `npm install`, чтобы получить обновленный пакет. Кроме того, вам понадобится выполнить команды `untrust-dev-cert` и `trust-dev-cert` на компьютере, чтобы устранить проблему с логикой создания сертификатов. 

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

**Когда в SharePoint Framework будут доступны дополнительные действия и JSLink?**

- *Дата: 6 июня.*

Расширения SharePoint с дополнительными возможностями настройки для SharePoint Online теперь доступны в виде релиза-кандидата. В настоящий момент дата общей доступности неизвестна. Чтобы узнать, как создавать эти расширения, прочитайте следующие руководства.

* [Начало работы с расширениями SharePoint Framework](http://aka.ms/spfx-extensions)

**Будет ли платформа SharePoint Framework доступна локально?**

- *Дата: 6 июня.*
- *Обновлено: 12 сентября*

Клиентские веб-части SharePoint Framework теперь доступны в составе SharePoint 2016 с пакетом дополнительных компонентов 2 (FP2). 

## <a name="additional-resources"></a>Дополнительные ресурсы
Используйте указанные ниже ресурсы, чтобы отправлять отзывы, комментарии и вопросы, касающиеся разработки решений для SharePoint. 

* [Список проблем в репозитории sp-dev-docs на сайте GitHub](https://github.com/SharePoint/sp-dev-docs/issues)
* [Раздел, посвященный разработке решений для SharePoint, на сайте Microsoft Tech Community](https://aka.ms/sppnp-community)
