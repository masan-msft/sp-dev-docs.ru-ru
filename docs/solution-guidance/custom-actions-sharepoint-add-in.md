---
title: "Настраиваемые действия в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d721746d8db8b5a6b01e71a1ea8d031bfd7b4330
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="custom-actions-in-the-sharepoint-add-in-model"></a>Настраиваемые действия в объектная модель SharePoint
=============================================

<a name="summary"></a>Summary
-------

Подход, выполните для изменения меню элемента списка и ленты в SharePoint отличается в новой модели надстройки SharePoint не был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы, меню элемента списка и изменения ленты были определены в формате XML (настраиваемые действия), упакованный в функции и развернуты через решений SharePoint.

В SharePoint надстройки модели сценарии используйте объектную модель SharePoint на стороне клиента (CSOM) или интерфейса API REST для создания настраиваемых действий, изменяющие меню элемента списка и ленты. Этот шаблон обычно называемую *удаленного подготовки шаблон*.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы хотели бы предоставляют следующие высокого уровня рекомендации по созданию и развертыванию настраиваемых действий в новой модели надстройки SharePoint.

- Настраиваемые действия могут быть использованы для изменения ленты и меню элемента списка.
- Нельзя скрыть элементы меню с помощью настраиваемого действия непосредственно из надстройки, который реализует настраиваемое действие.
    + Причина этого заключается в [Элемент HideCustomAction (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/ms414790.aspx) недоступен в SharePoint ECMA ide клиентов объектной модели (CSOM) - [Свойства UserCustomAction (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.usercustomaction_properties.aspx)или API-интерфейсы REST SharePoint и Office 365 — [SP. UserCustomActionCollection object (sp.js) (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/jj247124.aspx).
    + Если необходимо скрыть элементы меню, необходимо использовать настраиваемое действие для внедрения JavaScript или CSS, настраиваемых в страницы SharePoint. JavaScript или CSS, внедренных в страницы SharePoint скрывает элемента меню.
- Для реализации настраиваемого действия можно используйте объектную модель SharePoint на стороне клиента (CSOM) и/или API-интерфейсы REST SharePoint и Office 365.

**Приступая к работе**

В следующем примере показано, как добавить настраиваемое действие в меню Параметры сайта на хост-сайте, способ отображения диалогового окна на настраиваемое действие, как скрыть диалоговое окно, на котором размещается страница из удаленного веб-надстройки и порядок использования настраиваемого действия для создания списков и настройки темы веб-сайта.

- [Provisioning.SiteModifier (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)

    Здесь можно увидеть, что ссылку настраиваемого действия в пример добавляет в меню "Параметры сайта".
    
    ![В меню Параметры Office 365 отображается с пункта меню Изменение сайтов с выделением.](media/Recipes/CustomActions/Custom-Action-In-Site-Settings.png)
    
    Вы видите открыть с помощью ссылки на сайт изменение всплывающее окно.
    
    ![Всплывающее окно Изменение сайта отображается с группой флажок с именем списки, который содержит два флажка, проекты и контактов. Ниже списков является группу флажок с именем различных которых содержит поле с именем Применение темы. Внизу две кнопки с именем подтверждение и Отмена.](media/Recipes/CustomActions/Custom-Action-Popup-Menu.png)

<a name="related-links"></a>Ссылки по теме
=============

- [Пользовательские элементы управления и веб-элементов управления (добавить в SharePoint набора команд)](user-controls-and-web-controls-sharepoint-add-in.md)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Provisioning.SiteModifier (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
