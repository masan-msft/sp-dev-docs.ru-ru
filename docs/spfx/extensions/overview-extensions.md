# <a name="overview-of-sharepoint-framework-extensions-preview"></a>Обзор расширений SharePoint Framework (ознакомительная версия)

С помощью расширений SharePoint Framework разработчики могут дополнять пользовательский интерфейс SharePoint, настраивая такие аспекты интерфейса SharePoint, как области уведомлений, панели инструментов SharePoint и представления данных списков. Расширения SharePoint Framework доступны для тестирования в клиентах разработчиков приложений для Office 365 во время ознакомительного периода, а после выпуска общедоступной версии станут доступны во всех клиентах. 

> Вы можете бесплатно получить клиент разработчика приложений для Office 365, приняв участие в [программе для разработчиков](http://dev.office.com/devprogram).

Расширения SharePoint Framework добавляют новые возможности улучшения пользовательского интерфейса SharePoint на современных страницах и в библиотеках документов, используя знакомые средства и библиотеки для клиентской разработки из SharePoint Framework. В частности, SharePoint Framework включает три новых типа расширений:

- **ApplicationCustomizer** позволяет разработчикам добавлять на страницу скрипты, а также получать доступ к заполнителям известных элементов HTML и расширять их с помощью настраиваемой отрисовки;
- **FieldCustomizer** можно использовать для предоставления измененных представлений данных для полей списка;
- **CommandSet** позволяет разработчикам расширять поверхности команд SharePoint, добавляя новые действия, а также клиентский код, с помощью которого можно реализовать поведение.

Помимо проектов на обычном JavaScript, вы можете создавать расширения на таких распространенных платформах скриптов, как AngularJS и React. Например, вы можете использовать React вместе с компонентами из Office UI Fabric React, чтобы быстро создавать интерфейсы на основе тех же компонентов, которые используются в Office 365.

## <a name="getting-started"></a>Начало работы
Если вы еще не установили SharePoint Framework, ознакомьтесь со следующим руководством, чтобы подготовиться к разработке на платформе SharePoint Framework:

* [Настройка среды разработки](../set-up-your-development-environment)

Если вы еще не установили платформу SharePoint Framework, выполните следующую команду, чтобы обновить шаблоны Yeoman до последней версии:

```
npm install -g @microsoft/generator-sharepoint
```

Начните с руководств по разработке расширений SharePoint Framework:

* [Создание первого расширения SharePoint Framework (Hello World, часть 1)](./get-started/build-a-hello-world-extension)

## <a name="updates--feedback"></a>Обновления и отзывы

Чтобы следить за улучшениями SharePoint Framework, в том числе за выпуском расширений, используйте следующие ресурсы:

* [@SharePoint](https://twitter.com/sharepoint) и [@OfficeDev](https://twitter.com/officedev) в Twitter.
* [Блог разработчиков Office](http://dev.office.com/blogs).

## <a name="provide-feedback-during-preview"></a>Отправка отзывов во время ознакомительного периода
Ознакомительный выпуск расширений SharePoint Framework призван помочь разработчикам SharePoint собирать отзывы о планируемых возможностях и функциях. Чтобы присоединиться к обсуждению с разработчиками SharePoint, используйте следующие ресурсы:

- [sp-dev-docs repository issue list](https://github.com/SharePoint/sp-dev-docs/issues) — вопросы, проблемы и комментарии.
* [SharePoint StackExchange](http://sharepoint.stackexchange.com/) (используйте теги [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) и [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/)).
* Группа [SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev) (SharePoint для разработчиков) в сообществе технических специалистов Майкрософт.
* [UserVoice для разработчиков SharePoint](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform) — предложения новых возможностей и функций.


## <a name="additional-resources"></a>Дополнительные ресурсы

- [Обзор платформы SharePoint Framework](../sharepoint-framework-overview)
- [Средства разработки и библиотеки платформы SharePoint Framework](../tools-and-libraries)
