# <a name="overview-of-sharepoint-framework-extensions-preview"></a>Обзор расширений SharePoint Framework (предварительная версия)

С помощью расширений SharePoint Framework можно дополнять пользовательский интерфейс SharePoint, настраивая такие его аспекты, как области уведомлений, панели инструментов и представления данных списков. Расширения SharePoint Framework доступны для тестирования в клиентах Office 365 для разработчиков во время ознакомительного периода. 

> **Примечание.** Вы можете бесплатно получить клиент Office 365 для разработчиков, приняв участие в [программе для разработчиков](http://dev.office.com/devprogram).

Расширения SharePoint Framework позволяют дополнять пользовательский интерфейс SharePoint на современных страницах и в библиотеках документов, используя знакомые библиотеки и средства SharePoint Framework для клиентской разработки. SharePoint Framework включает три новых типа расширений:

- **ApplicationCustomizers.** Позволяет добавлять скрипты на страницу, а также получать доступ к заполнителям известных элементов HTML и дополнять их с использованием специальной отрисовки.
- **FieldCustomizers.** Предоставляет измененные представления данных для полей списка.
- **CommandSets.** Позволяет добавлять новые действия для команд SharePoint, а также предоставляет клиентский код, с помощью которого можно реализовать определенное поведение.

Помимо проектов plainJS, вы можете создавать расширения на таких распространенных платформах создания скриптов, как AngularJS и React. Например, вы можете использовать React вместе с компонентами из Office UI Fabric React, чтобы создавать решения на основе тех же компонентов, которые используются в Office 365.

## <a name="get-started"></a>Начало работы
Если вы не устанавливали SharePoint Framework, выполните действия [по настройке среды разработки](../set-up-your-development-environment).

Когда установите SharePoint Framework, выполните следующую команду, чтобы обновить шаблоны Yeoman до последней версии:

```
npm install -g @microsoft/generator-sharepoint
```

Далее вы можете [создать свое первое расширение SharePoint Framework (Hello World, часть 1)](./get-started/build-a-hello-world-extension).

## <a name="stay-up-to-date"></a>Своевременное обновление
Чтобы следить за улучшениями SharePoint Framework, в том числе за обновлением расширений, используйте следующие ресурсы:

* [@SharePoint](https://twitter.com/sharepoint) и [@OfficeDev](https://twitter.com/officedev) в Twitter.
* [Блог для разработчиков решений для Office](http://dev.office.com/blogs).

## <a name="provide-feedback"></a>Предоставление отзывов 
Предлагаем предоставить отзывы о предварительном выпуске расширений SharePoint Framework. Отправить эти отзывы непосредственно команде разработчиков SharePoint можно с помощью одного из указанных ниже ресурсов.

- [Список проблем, касающихся репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues) (вопросы, проблемы и комментарии).
* [SharePoint StackExchange](http://sharepoint.stackexchange.com/) (используйте теги [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) и [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/)).
* [SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev) (группа в сообществе технических специалистов Майкрософт, в которой участвуют разработчики решений для SharePoint).
* [UserVoice разработчиков SharePoint](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform) (здесь можно предложить добавить новые возможности и функции).


## <a name="additional-resources"></a>Дополнительные ресурсы

- [Обзор платформы SharePoint Framework](../sharepoint-framework-overview)
- [Средства разработки и библиотеки платформы SharePoint Framework](../tools-and-libraries)
