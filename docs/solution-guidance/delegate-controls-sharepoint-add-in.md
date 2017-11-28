---
title: "Делегирование элементов управления в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3981faf45be7a2a5e80dae40859b023d9dda9092
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="delegate-controls-in-the-sharepoint-add-in-model"></a>Делегирование элементов управления в объектная модель SharePoint
================================================

<a name="summary"></a>Summary
-------

Подхода, можно реализовать элементов управления делегированием в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия.  В типичных полного доверия кода (FTC) / сценарий решения фермы, делегат элементы управления были созданы как пользовательские элементы управления или веб-элементы управления, зарегистрированные с использованием функций и развернуты через решений SharePoint.

В SharePoint надстройки модели сценарии JavaScript встраивается в страницы SharePoint для реализации функциональных возможностей элементов управления делегированием.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем обеспечивает следующие рекомендации высокого уровня для создания элементов управления делегированием в новой модели надстройки SharePoint.

- Нет замена элемента управления не прямой делегат в модели надстройки SharePoint.
- Используйте внедренные JavaScript для реализации функциональных возможностей элементов управления делегированием с точки зрения конечного пользователя.
- Используйте SharePoint JavaScript клиента со стороны объектной модели (JSOM) и/или API-интерфейсы REST SharePoint и Office 365 для взаимодействия с данным и службам SharePoint.

В разделе [пользовательские элементы управления и веб-элементов управления (добавить в SharePoint рецептов модели)](user-controls-and-web-controls-sharepoint-add-in.md) для внедрения JavaScript на всех страницах SharePoint с помощью пользовательских действий и внедрения JavaScript непосредственно в макеты страниц и главных страниц.

<a name="related-links"></a>Ссылки по теме
=============
- [Кросс-структура навигации семейства сайтов (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================
- [OD4B. NavLinksInjection (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
