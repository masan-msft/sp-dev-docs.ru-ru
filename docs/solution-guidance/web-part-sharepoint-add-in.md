---
title: "Веб-часть в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 65e236df834b82d9649d2e43cd3dfef37ebdcdb4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="web-part-in-the-sharepoint-add-in-model"></a>Веб-часть в объектная модель SharePoint
=======================================

<a name="summary"></a>Summary
-------

Подхода, можно создавать компоненты portable страницы отличается в новой модели надстройки SharePoint не был с кодом полного доверия.  В типичных полного доверия кода (FTC) / сценарий решения фермы, веб-части были созданы для реализации компонентов portable страницы.

В SharePoint надстройки модели сценарии частей Add-in (части приложения) создаются для реализации компонентов portable страницы.  Добавьте в части будут использовать коде на стороне клиента.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы хотели бы предоставляют следующие рекомендации высокого уровня по части надстройки.

- Нельзя запустить серверного кода в частях надстройки.
- Не удается создать пользовательский редактор частей частей Add-in.
- Используйте Add-in часть скрипта для связи с JavaScript, который используется для взаимодействия с SharePoint и другие службы и создания пользовательского интерфейса.
- По умолчанию настраиваемые свойства, добавляемые к частям редактора всегда отображаются как окончательный группы в части "редактор".
    + Чтобы переопределить внешний вид и функции части редактора для части Add-in можно использовать JavaScript.
    + Следующий пример, в котором показано, как это делается в разделе. 
    + [Core.AppPartPropertyUIOverride (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)

**Приступая к работе**

Части надстройки могут легко создавать с помощью ожидания поле Add-in части скрипта.  Это позволяет указать ссылку на файл JavaScript, размещенных в любом месте.  Файл JavaScript коде на стороне клиента использует для взаимодействия с SharePoint или других служб и отображения пользовательского интерфейса.

Со следующей статьей описание шаблона Add-in части скрипта и использовать его.

- [Краткие сведения о шаблон части скрипта приложений для модели приложения Office 365 (статья блога MSDN)](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)

Следующий пример демонстрирует использование части скрипта Add-in можно интегрировать с Yammer, Bing Maps и Google карт.

- [Core.AppScriptPart (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)

Следующем видеоролике описывается пример кода.

- [Core.AppScriptPart (O365 PnP видео)](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)

<a name="related-links"></a>Ссылки по теме
=============

- [Краткие сведения о шаблон части скрипта приложений для модели приложения Office 365 (статья блога MSDN)](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)
- [Core.AppScriptPart (O365 PnP видео)](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Core.AppPartPropertyUIOverride (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)
- [Core.AppScriptPart (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
