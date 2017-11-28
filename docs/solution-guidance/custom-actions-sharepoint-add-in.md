---
title: "Настраиваемые действия в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d721746d8db8b5a6b01e71a1ea8d031bfd7b4330
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="custom-actions-in-the-sharepoint-add-in-model"></a><span data-ttu-id="0dd46-102">Настраиваемые действия в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="0dd46-102">Custom actions in the SharePoint add-in model</span></span>
=============================================

<a name="summary"></a><span data-ttu-id="0dd46-103">Summary</span><span class="sxs-lookup"><span data-stu-id="0dd46-103">Summary</span></span>
-------

<span data-ttu-id="0dd46-104">Подход, выполните для изменения меню элемента списка и ленты в SharePoint отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="0dd46-104">The approach you take to modify list item menus and the ribbon in SharePoint is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="0dd46-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, меню элемента списка и изменения ленты были определены в формате XML (настраиваемые действия), упакованный в функции и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0dd46-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, list item menus and ribbon modifications were defined in XML (custom actions), packaged in features, and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="0dd46-106">В SharePoint надстройки модели сценарии используйте объектную модель SharePoint на стороне клиента (CSOM) или интерфейса API REST для создания настраиваемых действий, изменяющие меню элемента списка и ленты.</span><span class="sxs-lookup"><span data-stu-id="0dd46-106">In an SharePoint Add-in model scenario, you use the SharePoint Client-side Object Model (CSOM) or REST API to create custom actions that modify list item menus and the ribbon.</span></span> <span data-ttu-id="0dd46-107">Этот шаблон обычно называемую *удаленного подготовки шаблон*.</span><span class="sxs-lookup"><span data-stu-id="0dd46-107">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="0dd46-108">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="0dd46-108">High-level guidelines</span></span>
---------------------

<span data-ttu-id="0dd46-109">Как правило эскиз мы хотели бы предоставляют следующие высокого уровня рекомендации по созданию и развертыванию настраиваемых действий в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0dd46-109">As a rule of a thumb, we would like to provide the following high-level guidelines for creating and deploying custom actions in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="0dd46-110">Настраиваемые действия могут быть использованы для изменения ленты и меню элемента списка.</span><span class="sxs-lookup"><span data-stu-id="0dd46-110">Custom actions may be used to modify list item menus and the ribbon.</span></span>
- <span data-ttu-id="0dd46-111">Нельзя скрыть элементы меню с помощью настраиваемого действия непосредственно из надстройки, который реализует настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="0dd46-111">You cannot hide menu items using a custom action directly from an Add-in that implements a custom action.</span></span>
    + <span data-ttu-id="0dd46-112">Причина этого заключается в [Элемент HideCustomAction (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/ms414790.aspx) недоступен в SharePoint ECMA ide клиентов объектной модели (CSOM) - [Свойства UserCustomAction (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.usercustomaction_properties.aspx)или API-интерфейсы REST SharePoint и Office 365 — [SP. UserCustomActionCollection object (sp.js) (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/jj247124.aspx).</span><span class="sxs-lookup"><span data-stu-id="0dd46-112">This is because the [HideCustomAction Element (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/office/ms414790.aspx) is not available in the SharePoint ECMA Clients-ide Object Model (CSOM) - [UserCustomAction properties (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.usercustomaction_properties.aspx), or the SharePoint/Office 365 REST APIs - [SP.UserCustomActionCollection object (sp.js) (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/office/jj247124.aspx).</span></span>
    + <span data-ttu-id="0dd46-113">Если необходимо скрыть элементы меню, необходимо использовать настраиваемое действие для внедрения JavaScript или CSS, настраиваемых в страницы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0dd46-113">If you need to hide menu items, you must use a custom action to embed JavaScript or customized CSS in SharePoint pages.</span></span> <span data-ttu-id="0dd46-114">JavaScript или CSS, внедренных в страницы SharePoint скрывает элемента меню.</span><span class="sxs-lookup"><span data-stu-id="0dd46-114">The JavaScript or CSS embedded in the SharePoint pages hides the menu item.</span></span>
- <span data-ttu-id="0dd46-115">Для реализации настраиваемого действия можно используйте объектную модель SharePoint на стороне клиента (CSOM) и/или API-интерфейсы REST SharePoint и Office 365.</span><span class="sxs-lookup"><span data-stu-id="0dd46-115">Use the SharePoint Client-side Object Model (CSOM), and/or the SharePoint/Office 365 REST APIs to implement custom actions.</span></span>

<span data-ttu-id="0dd46-116">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="0dd46-116">**Getting started**</span></span>

<span data-ttu-id="0dd46-117">В следующем примере показано, как добавить настраиваемое действие в меню Параметры сайта на хост-сайте, способ отображения диалогового окна на настраиваемое действие, как скрыть диалоговое окно, на котором размещается страница из удаленного веб-надстройки и порядок использования настраиваемого действия для создания списков и настройки темы веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="0dd46-117">The following sample demonstrates how to add a custom action to the site settings menu in the host web, how to show a dialog in a custom action, how to hide a dialog that hosts a page from a remote add-in web, and how to use a custom action to create lists and set the theme of a web.</span></span>

- [<span data-ttu-id="0dd46-118">Provisioning.SiteModifier (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="0dd46-118">Provisioning.SiteModifier (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)

    <span data-ttu-id="0dd46-119">Здесь можно увидеть, что ссылку настраиваемого действия в пример добавляет в меню "Параметры сайта".</span><span class="sxs-lookup"><span data-stu-id="0dd46-119">Here you can see the link the custom action in the sample adds to the Site Settings menu.</span></span>
    
    ![В меню Параметры Office 365 отображается с пункта меню Изменение сайтов с выделением.](media/Recipes/CustomActions/Custom-Action-In-Site-Settings.png)
    
    <span data-ttu-id="0dd46-121">Вы видите открыть с помощью ссылки на сайт изменение всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="0dd46-121">Here you can see the popup window opened via the Modify Site link.</span></span>
    
    ![Всплывающее окно Изменение сайта отображается с группой флажок с именем списки, который содержит два флажка, проекты и контактов.](media/Recipes/CustomActions/Custom-Action-Popup-Menu.png)

<a name="related-links"></a><span data-ttu-id="0dd46-125">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="0dd46-125">Related links</span></span>
=============

- [<span data-ttu-id="0dd46-126">Пользовательские элементы управления и веб-элементов управления (добавить в SharePoint набора команд)</span><span class="sxs-lookup"><span data-stu-id="0dd46-126">User controls and Web controls (SharePoint Add-in Recipe)</span></span>](user-controls-and-web-controls-sharepoint-add-in.md)
- <span data-ttu-id="0dd46-127">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="0dd46-127">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="0dd46-128">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="0dd46-128">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="0dd46-129">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="0dd46-129">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="0dd46-130">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="0dd46-130">Related PnP samples</span></span>
===================

- [<span data-ttu-id="0dd46-131">Provisioning.SiteModifier (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="0dd46-131">Provisioning.SiteModifier (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteModifier)
- <span data-ttu-id="0dd46-132">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="0dd46-132">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="0dd46-133">Применимо к</span><span class="sxs-lookup"><span data-stu-id="0dd46-133">Applies to</span></span>
==========
- <span data-ttu-id="0dd46-134">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="0dd46-134">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="0dd46-135">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="0dd46-135">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="0dd46-136">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="0dd46-136">SharePoint 2013 on-premises</span></span>
