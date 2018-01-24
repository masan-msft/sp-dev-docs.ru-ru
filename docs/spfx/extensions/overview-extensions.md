---
title: "Обзор расширений SharePoint Framework (SPFx)"
description: "Используйте расширения SPFx, чтобы настроить области уведомлений, панели инструментов, представления данных списков и другие аспекты SharePoint."
ms.date: 01/11/2018
ms.prod: sharepoint
ms.openlocfilehash: a39bfdc82e3557fb791c43db21e889448f75b785
ms.sourcegitcommit: 6b547679670b719f2222f9709732382739956f90
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="overview-of-sharepoint-framework-extensions"></a>Обзор расширений SharePoint Framework

Используя расширения SharePoint Framework (SPFx), можно сделать SharePoint удобнее для пользователей. Используя расширения SharePoint Framework, можно настроить области уведомлений, панели инструментов, представления данных списков и другие аспекты SharePoint. Расширения SharePoint Framework доступны во всех клиентах Office 365 для производственного использования. 

> [!NOTE] 
> Вы можете бесплатно получить клиент Office 365 для разработчиков, приняв участие в [специальной программе](http://dev.office.com/devprogram).

Расширения SharePoint Framework позволяют дополнять пользовательский интерфейс SharePoint на современных страницах и в библиотеках документов, используя знакомые библиотеки и средства SharePoint Framework для клиентской разработки. SharePoint Framework включает три новых типа расширений:

- **Настройщики заполнителей**. Позволяют добавлять скрипты на страницу, а также изменять стандартные заполнители, добавляя собственные элементы HTML.
- **Настройщики полей**. Позволяют настраивать отображение данных в полях списка.
- **Наборы команд**. Позволяют добавлять действия на панели команд SharePoint, а также внедрять действия с помощью встроенного клиентского кода.

Помимо проектов plainJS, вы можете создавать расширения на таких распространенных платформах создания скриптов, как AngularJS и React. Например, вы можете использовать React вместе с компонентами из Office UI Fabric React, чтобы создавать решения на основе тех же компонентов, которые используются в Office 365.

> [!NOTE]
> Мы знаем о проблеме с поддержкой расширений библиотеки и списков на классических страницах. Сейчас их можно использовать только в контексте современных сайтов группы. Мы работаем над устранением этой проблемы. 

## <a name="get-started"></a>Начало работы

1. Если вы не устанавливали SharePoint Framework, выполните действия [по настройке среды разработки](../set-up-your-development-environment.md).

2. Когда установите SharePoint Framework, выполните следующую команду, чтобы обновить шаблоны Yeoman до последней версии:

    ```
    npm install -g @microsoft/generator-sharepoint
    ```

3. Далее вы можете [создать свое первое расширение SharePoint Framework (Hello World, часть 1)](get-started/build-a-hello-world-extension.md).

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
