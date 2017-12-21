# <a name="overview-of-sharepoint-framework-extensions"></a>Обзор расширений SharePoint Framework

Расширить возможности взаимодействия с пользователями SharePoint можно с помощью расширений SharePoint Framework. Благодаря расширениям SharePoint Framework вы можете настроить больше аспектов SharePoint, в том числе области уведомлений, панели инструментов, а также представления данных списков. Расширения SharePoint Framework доступны во всех клиентах Office 365 для производственного использования. 

> [!NOTE] 
> Вы можете бесплатно получить клиент Office 365 для разработчиков, приняв участие в [специальной программе](http://dev.office.com/devprogram).

Расширения SharePoint Framework позволяют дополнять пользовательский интерфейс SharePoint на современных страницах и в библиотеках документов, используя знакомые библиотеки и средства SharePoint Framework для клиентской разработки. SharePoint Framework включает три новых типа расширений:

- **ApplicationCustomizers.** Позволяет добавлять скрипты на страницу, а также получать доступ к заполнителям известных элементов HTML и дополнять их с использованием специальной отрисовки.
- **FieldCustomizers.** Предоставляет измененные представления данных для полей списка.
- **CommandSets.** Позволяет добавлять новые действия для команд SharePoint, а также предоставляет клиентский код, с помощью которого можно реализовать определенное поведение.

Помимо проектов plainJS, вы можете создавать расширения на таких распространенных платформах создания скриптов, как AngularJS и React. Например, вы можете использовать React вместе с компонентами из Office UI Fabric React, чтобы создавать решения на основе тех же компонентов, которые используются в Office 365.

> [!NOTE]
> Мы знаем о проблеме с поддержкой расширений библиотеки и списков в классических интерфейсах. Сейчас их можно использовать только в контексте современных сайтов группы, или сопоставленных с группой сайтов группы. Мы работаем над устранением этой проблемы. 

## <a name="get-started"></a>Начало работы
Если вы не устанавливали SharePoint Framework, выполните действия [по настройке среды разработки](../set-up-your-development-environment.md).

Когда установите SharePoint Framework, выполните следующую команду, чтобы обновить шаблоны Yeoman до последней версии:

```
npm install -g @microsoft/generator-sharepoint
```

Далее вы можете [создать свое первое расширение SharePoint Framework (Hello World, часть 1)](get-started/build-a-hello-world-extension.md).

## <a name="stay-up-to-date"></a>Своевременное обновление
Чтобы следить за улучшениями SharePoint Framework, в том числе за обновлением расширений, используйте следующие ресурсы:

* [@SharePoint](https://twitter.com/sharepoint) и [@OfficeDev](https://twitter.com/officedev) в Twitter.
* [Блог для разработчиков решений для Office](http://dev.office.com/blogs).

## <a name="provide-feedback"></a>Предоставление отзывов 
Предлагаем отправить отзывы об общедоступном выпуске SharePoint Framework. Отправить отзывы непосредственно команде разработчиков SharePoint можно с помощью таких ресурсов:

- [Список проблем, касающихся репозитория sp-dev-docs](https://github.com/SharePoint/sp-dev-docs/issues) (вопросы, проблемы и комментарии).
* [SharePoint StackExchange](http://sharepoint.stackexchange.com/) (используйте теги [#spfx](http://sharepoint.stackexchange.com/tags/spfx/), [#spfx-extensions](http://sharepoint.stackexchange.com/tags/spfx-extensions/) и [#spfx-tooling](http://sharepoint.stackexchange.com/tags/spfx-tooling/)).
* [SharePoint Developer](https://techcommunity.microsoft.com/t5/SharePoint-Developer/bd-p/SharePointDev) (группа в сообществе технических специалистов Майкрософт, в которой участвуют разработчики решений для SharePoint).
* [UserVoice разработчиков SharePoint](https://sharepoint.uservoice.com/forums/329220-sharepoint-dev-platform) (здесь можно предложить добавить новые возможности и функции).


## <a name="see-also"></a>См. также

- [Обзор платформы SharePoint Framework](../sharepoint-framework-overview.md)
- [Средства разработки и библиотеки платформы SharePoint Framework](../tools-and-libraries.md)
