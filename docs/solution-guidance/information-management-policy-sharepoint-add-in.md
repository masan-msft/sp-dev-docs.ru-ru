---
title: "Политики управления сведениями в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: f395b7fa40f4798b2184bd637ca752c468b9289d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="information-management-policy-in-the-sharepoint-add-in-model"></a>Политики управления сведениями в объектная модель SharePoint
============================================================

<a name="summary"></a>Summary
-------

Подхода, можно применить политику управления сведениями отличается в новой модели надстройки SharePoint не был с кодом полного доверия.  В типичных полного доверия кода (FTC) сценарий решения фермы, сведений политики управления был управляемых и применяется с помощью объектной модели SharePoint Server со стороны и развернуты через решения в ферме SharePoint, как правило, как часть таймера задания. 

В модели сценарий SharePoint Add-in SharePoint клиента со стороны объектной модели (CSOM) и задания таймера удаленного используются для управления и применение политики управления сведениями.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее по управлению и применение политик управления сведениями к сайтам SharePoint.  

- Имейте в виду при определении политики управления сведениями на уровне семейства сайтов и владельцев семейства сайтов может отключить их.
    + При использовании удаленного модели и CSOM настраивать политики управления сведения владелец семейства сайтов не могут отключить их.  Удаленный модели подход заключается в более понятное модель предприятия и обеспечивает политик управления сведениями всегда включена во всей среде SharePoint.
- Используйте SharePoint CSOM в задания таймера удаленного управления и применение политик управления сведениями.

- Убедитесь, что вы не нарушают пределы регулирования Office 365 SharePoint API при работе с большими наборами данных и рекурсивный обходит как проверять артефактов на веб-сайтах SharePoint и применение политик управления сведениями для них соответствующим образом.
    + [Core.Throttling (Pnp образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) показано, как создавать intelligent код для обработки регулирования Office 365 SharePoint API.

**Примечание:** В настоящее время CSOM не имеет методов, чтобы задать хранения для типов контента (только на сайтах).

**Приступая к работе**

Следующий пример кода O365 PnP и видео показано, как управлять и применение политики управления сведениями для сайтов SharePoint.  В этом примере кода выполняется итерация по типов контента, применяется к библиотекам документов в семействах сайтов SharePoint и применяет политику хранения.

- [Governance.ContentTypeEnforceRetention (образец кода PnP O365)](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)

Следующем видеоролике описывается пример кода.

- [Политики управления сведениями с моделью приложений (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)

<a name="related-links"></a>Ссылки по теме
=============
- [Политики управления сведениями с моделью приложений (O365 PnP видео)](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Governance.ContentTypeEnforceRetention (образец кода PnP O365)](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)
- Примеры и содержимое в https://github.com/SharePoint/PnP

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D) *частично*
- SharePoint 2013 в локальной — *частично*

*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*
