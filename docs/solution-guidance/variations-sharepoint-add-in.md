---
title: "Варианты в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 8d389a61ed6af1edcdc4485d1e28d366496b29d1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="variations-in-the-sharepoint-add-in-model"></a>Варианты в объектная модель SharePoint
=========================================

<a name="summary"></a>Summary
-------

Выбор подхода к настройке вариантов отличается новой модели надстройки SharePoint от был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы SharePoint Server-side Object Model (Microsoft.SharePoint.Publishing.Variations) была используется для настройки вариантов и функции, которые выполняет код были развернуты через решений SharePoint.

В SharePoint надстройки модели сценарии использовании объектной модели SharePoint на стороне клиента (CSOM) или интерфейса API REST для настройки вариантов. Этот шаблон обычно называемую *удаленного подготовки шаблон*.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для настройки вариантов в новой модели надстройки SharePoint.

- Используйте SharePoint со стороны клиента API объектной модели (CSOM) для настройки вариантов, когда это возможно.
    - .NET клиентской объектной модели [класс вариантов (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.variations.aspx)
    - JavaScript клиентской объектной модели [класс вариантов (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/jj994778.aspx)
- Не все параметры конфигурации вариантов в настоящее время доступны с помощью SharePoint CSOM API вариантов классы, перечисленных выше.
- Можно выходит за пределы предоставляют классы CSOM API вариантов, перечисленных выше и настроить некоторые параметры вариантов.  Чтобы сделать это, задайте значения для вариантов параметры хранятся в контейнеры свойств сайта и/или изменение элементов списка в списках, связанных с вариантов.
    + [Класс VariationsExtensions.cs (PnP образец O365)](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) содержит несколько примеров, изменяющие контейнера и список элементов значения свойств для настройки параметров вариантов.
    + [Класс VariationsExtensions.cs (PnP образец O365)](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) показано, как настроить ***все параметры*** , которые можно настроить на странице Параметры вариантов.
    + [Включить параметры вариантов, чтобы вы могли создать вариантов сайта (статья O365)](https://support.office.com/en-za/article/Turn-on-variations-settings-so-you-can-create-variations-of-your-site-fc021610-bdb5-4b5c-9d59-ce8af6699b4b) список элементов, можно настроить на странице Параметры вариантов и описание их функций.

<a name="related-links"></a>Ссылки по теме
=============

- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Класс VariationsExtensions.cs (O365 PnP образец)](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
