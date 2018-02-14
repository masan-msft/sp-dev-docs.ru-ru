---
title: "SharePoint Framework: известные проблемы и часто задаваемые вопросы"
description: "Здесь вы найдете ответы на проблемы и часто задаваемые вопросы, связанные с SharePoint Framework."
ms.date: 01/12/2018
ms.prod: sharepoint
ms.openlocfilehash: 79b580fd263636ccab392f99f11983c24ac08e8b
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="sharepoint-framework-known-issues-and-frequently-asked-questions"></a>SharePoint Framework: известные проблемы и часто задаваемые вопросы

На этой странице представлены известные проблемы и ответы на часто задаваемые вопросы о SharePoint Framework. 

## <a name="known-issues"></a>Известные проблемы

### <a name="dev-certificate-issue-with-chrome-v58-"></a>Проблема с сертификатом разработчика в Chrome (версии 58 и новее)

- *Дата: 28 апреля 2017 г.*
- *Обновлено: 2 мая 2017 г.*

Если вы используете браузер Chrome для разработки, у вас могут возникнуть проблемы с сертификатом разработчика независимо от того, выполняется ли команда `gulp trust-dev-cert`. В Chrome версии 58 и более новых изменилась модель проверки сертификатов, и во время доступа к локальной рабочей области может появиться такое сообщение: "Ваше подключение не защищено".

Следует обновить пакеты шаблонов Yeoman. Мы обновили логику создания сертификатов в пакете [*@microsoft/gulp-core-build-serve*](https://www.npmjs.com/package/@microsoft/gulp-core-build-serve). 

Для существующих решений вы можете просто удалить эту папку и запустить `npm install`, чтобы получить обновленный пакет. Кроме того, необходимо выполнить команды `untrust-dev-cert` и `trust-dev-cert` на компьютере, чтобы устранить проблему с логикой создания сертификатов. 

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы

### <a name="when-will-custom-actions-and-jslink-be-available-in-the-sharepoint-framework"></a>Когда в SharePoint Framework будут доступны дополнительные действия и JSLink?

- *Дата: 6 июня 2017 г.*

Расширения SharePoint Framework с дополнительными возможностями настройки теперь доступны в SharePoint Online. Дополнительные сведения о расширениях SharePoint Framework можно найти в нашей документации:

- [Обзор расширений SharePoint Framework](./extensions/overview-extensions.md)
- [Руководства по расширениям SharePoint Framework](./extensions/get-started/build-a-hello-world-extension.md)

### <a name="will-sharepoint-framework-be-available-in-on-premises"></a>Будет ли платформа SharePoint Framework доступна локально?

- *Дата: 6 июня 2017 г.*

Клиентские веб-части SharePoint Framework на классических страницах выпущены для SharePoint 2016 в составе пакета дополнительных компонентов 2 (FP2). Мы пока не планируем добавлять возможности SharePoint Framework в SharePoint 2013. Полного списка возможностей SharePoint Framework, которые будут включены в выпуск SharePoint 2019, нет.

## <a name="see-also"></a>См. также

Используйте указанные ниже ресурсы, чтобы отправлять отзывы, комментарии и вопросы, касающиеся разработки решений для SharePoint. 

- [Проблемы с sp-dev-docs на сайте GitHub](https://github.com/SharePoint/sp-dev-docs/issues)
- [Пространство в сообществе технических специалистов Майкрософт, в котором участвуют разработчики решений для SharePoint](https://aka.ms/sppnp-community)

