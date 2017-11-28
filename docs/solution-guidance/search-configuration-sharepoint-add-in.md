---
title: "Настройка поиска в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 9a84ae5aa1a12322227c9182c9ff0f5fb1798e48
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="search-configuration-in-the-sharepoint-add-in-model"></a>Настройка поиска в объектная модель SharePoint
===================================================

<a name="summary"></a>Summary
-------

Выбор подхода для настройки системы поиска отличается новой модели надстройки SharePoint от был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы, объектной модели SharePoint на сервере было используется для настройки поиска и развернуты через решений SharePoint.

В SharePoint надстройки модели сценарии используйте объектную модель SharePoint на стороне клиента (CSOM) или интерфейса API REST для настройки системы поиска. Этот шаблон обычно называемую *удаленного подготовки шаблон*.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для настройки системы поиска в новой модели надстройки SharePoint.

- Используйте SharePoint со стороны клиента API объектной модели (CSOM) для настройки поиска по возможности, Импорт и экспорт параметров конфигурации поиска.
- Не все параметры конфигурации поиска в настоящее время доступны через SharePoint CSOM API.
    + В разделе [экспорта и импорта параметров конфигурации настраиваемого поиска в SharePoint Server 2013 (статья TechNet)](https://technet.microsoft.com/en-us/library/jj871675.aspx#BKMK_2) для списка параметров поиска, которые можно экспортировать и импортировать.
    + Если параметр конфигурации поиска не может быть установлено с помощью CSOM пользовательский интерфейс администрирования требуется для установки значений конфигурации.
- API-Интерфейс REST SharePoint не может (в настоящее время) Импорт или экспорт параметров конфигурации поиска.

**Приступая к работе**

Следующий пример демонстрирует Импорт и экспорт параметров поиска между клиентами, семейств веб-сайтов и сайтов SharePoint.

- [Core.SearchSettingsPortability (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)

<a name="related-links"></a>Ссылки по теме
=============

- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Core.SearchSettingsPortability (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SearchSettingsPortability)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
