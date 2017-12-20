---
title: "Известные проблемы и часто задаваемые вопросы"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1208a2a19432fdda3597efe81a84bf8a7abfb16f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
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

Расширения SharePoint с дополнительными возможностями настройки для SharePoint Online теперь доступны в SharePoint Online. Дополнительные сведения о расширениях SharePoint Framework можно найти в соответствующей документации.

- [Обзор расширений SharePoint Framework](./extensions/overview-extensions.md)
- [Руководство по расширениям SharePoint Framework](./extensions/get-started/build-a-hello-world-extension.md)

**Будет ли платформа SharePoint Framework доступна локально?**

- *Дата: 6 июня.*

Клиентские веб-части SharePoint Framework на классических страницах выпущены для SharePoint 2016 в составе пакета дополнительных компонентов 2 (FP2). Мы пока не планируем добавлять возможности SharePoint Framework в SharePoint 2013. Полного списка возможностей SharePoint Framework, которые будут включены в выпуск SharePoint 2019, нет.

## <a name="see-also"></a>См. также
Используйте указанные ниже ресурсы, чтобы отправлять отзывы, комментарии и вопросы, касающиеся разработки решений для SharePoint. 

* [Список проблем в репозитории sp-dev-docs на сайте GitHub](https://github.com/SharePoint/sp-dev-docs/issues)
* [Раздел, посвященный разработке решений для SharePoint, на сайте Microsoft Tech Community](https://aka.ms/sppnp-community)
