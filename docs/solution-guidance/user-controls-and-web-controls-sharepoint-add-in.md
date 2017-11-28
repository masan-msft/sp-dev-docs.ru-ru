---
title: "Пользовательские элементы управления и веб-элементы управления в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: cd1f3b127a7ae2eb1ac06e75f5a23c8f13563a8f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="user-controls-and-web-controls-in-the-sharepoint-add-in-model"></a>Пользовательские элементы управления и веб-элементы управления в объектная модель SharePoint
=============================================================

<a name="summary"></a>Summary
-------

Подхода, можно реализовать пользовательских элементов управления в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы, настраиваемые элементы управления были созданы как пользовательские элементы управления или веб-элементы управления и развернуты через решений SharePoint.

В модели сценарий надстройки SharePoint JavaScript встраивается в страницы SharePoint для реализации пользовательских элементов управления.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для создания пользовательских элементов управления в новой модели надстройки SharePoint.

- Использование внедренных JavaScript для создания пользовательских элементов управления.
- Используйте SharePoint ECMA клиента со стороны объектной модели (CSOM) и/или API-интерфейсы REST SharePoint и Office 365 для взаимодействия с данным и службам SharePoint.

<a name="options-to-embed-javascript-in-sharepoint-pages"></a>Параметры для внедрения JavaScript в страницы SharePoint
-----------------------------------------------
Существует несколько параметров для внедрения JavaScript в страницы SharePoint.

- Использование настраиваемых пользовательских действий
- Внедрение JavaScript непосредственно в макеты страниц
- Внедрение JavaScript непосредственно в настраиваемых главных страниц (не рекомендуется)

<a name="use-custom-user-actions"></a>Использование настраиваемых пользовательских действий
-----------------------
В этом шаблоне настраиваемого пользовательского действия используются для внедрения JavaScript в страницу во время выполнения.

- Такой подход поддерживается абсолютно и — допустимый подход.

**Когда это подходит?**

При необходимости для внедрения JavaScript в все страницы SharePoint, этот параметр используется подходит.

**Приступая к работе**

Следующие статьи и сопутствующий видео демонстрируется использование настраиваемых пользовательских действий для внедрения JavaScript в страницах SharePoint.

- [Core.EmbedJavaScript (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [OD4B. NavLinksInjection (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [Кросс-структура навигации семейства сайтов (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)

<a name="embed-javascript-directly-into-page-layouts"></a>Внедрение JavaScript непосредственно в макеты страниц
-------------------------------------------

В этом шаблоне JavaScript встроена непосредственно в макеты страниц на сайтах публикации.  

- Такой подход поддерживается абсолютно и — допустимый подход.
- Такой подход работает с сайтами публикации.

**Когда это подходит?**

При необходимости для внедрения JavaScript в определенных макетов страниц SharePoint на сайтах публикации в сценарии управления веб-Контентом, этот параметр используется подходит.

<a name="embed-javascript-directly-into-custom-master-pages"></a>Внедрение JavaScript непосредственно в настраиваемых главных страниц
--------------------------------------------------

В этом шаблоне JavaScript встроена непосредственно в настраиваемых главных страниц.  

- Такой подход не рекомендуется.
- Такой подход — допустимый подход.
- Внедрение JavaScript непосредственно в настраиваемых главных страниц, но оставьте учитывать в результате вы дополнительные долгосрочные затраты и проблемы, связанные с с будущими обновлениями.
    + Если вы решили использовать настраиваемые главные страницы, будьте готовым применить изменения к настраиваемых главных страниц, когда основные функциональные обновления применяются к Office 365.

**Когда это подходит?**

Когда следует применять внедрения JavaScript в каждой главной страницы, так как она позволяет управлять которого главные страницы, JavaScript в это является хорошим выбором.

<a name="related-links"></a>Ссылки по теме
=============
- [Кросс-структура навигации семейства сайтов (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================
- [Core.EmbedJavaScript (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [OD4B. NavLinksInjection (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [Core.EmbedJavaScript.WeekNumbers (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript.WeekNumbers)
- [Core.EmbedJavaScriptJSOM (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScriptJSOM)
- [Core.JavaScriptCustomization (O365 PnP сценария с помощью компонента PnP ядра)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
