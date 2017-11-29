---
title: "Варианты в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 8d389a61ed6af1edcdc4485d1e28d366496b29d1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="variations-in-the-sharepoint-add-in-model"></a><span data-ttu-id="be52d-102">Варианты в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="be52d-102">Variations in the SharePoint add-in model</span></span>
=========================================

<a name="summary"></a><span data-ttu-id="be52d-103">Summary</span><span class="sxs-lookup"><span data-stu-id="be52d-103">Summary</span></span>
-------

<span data-ttu-id="be52d-104">Выбор подхода к настройке вариантов отличается новой модели надстройки SharePoint от был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="be52d-104">The approach you take to configure variations is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="be52d-105">В типичных полного доверия кода (FTC) / сценарий решения фермы SharePoint Server-side Object Model (Microsoft.SharePoint.Publishing.Variations) была используется для настройки вариантов и функции, которые выполняет код были развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be52d-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, the SharePoint Server-side Object Model (Microsoft.SharePoint.Publishing.Variations) was used to configure variations, and features that executed the code were deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="be52d-106">В SharePoint надстройки модели сценарии использовании объектной модели SharePoint на стороне клиента (CSOM) или интерфейса API REST для настройки вариантов.</span><span class="sxs-lookup"><span data-stu-id="be52d-106">In an SharePoint Add-in model scenario, you use the SharePoint Client-side Object Model (CSOM) or REST API to configure variations.</span></span> <span data-ttu-id="be52d-107">Этот шаблон обычно называемую *удаленного подготовки шаблон*.</span><span class="sxs-lookup"><span data-stu-id="be52d-107">This pattern is commonly referred to as the *remote provisioning pattern*.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="be52d-108">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="be52d-108">High-level guidelines</span></span>
---------------------

<span data-ttu-id="be52d-109">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для настройки вариантов в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be52d-109">As a rule of a thumb, we would like to provide the following high-level guidelines to configure variations in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="be52d-110">Используйте SharePoint со стороны клиента API объектной модели (CSOM) для настройки вариантов, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="be52d-110">Use the SharePoint Client-side Object Model (CSOM) API to configure variations whenever possible.</span></span>
    - <span data-ttu-id="be52d-111">.NET клиентской объектной модели [класс вариантов (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.variations.aspx)</span><span class="sxs-lookup"><span data-stu-id="be52d-111">.Net Client side object model [Variations class (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.publishing.variations.aspx)</span></span>
    - <span data-ttu-id="be52d-112">JavaScript клиентской объектной модели [класс вариантов (документация по API MSDN)](https://msdn.microsoft.com/en-us/library/office/jj994778.aspx)</span><span class="sxs-lookup"><span data-stu-id="be52d-112">JavaScript Client side object model [Variations class (MSDN API Documentation)](https://msdn.microsoft.com/en-us/library/office/jj994778.aspx)</span></span>
- <span data-ttu-id="be52d-113">Не все параметры конфигурации вариантов в настоящее время доступны с помощью SharePoint CSOM API вариантов классы, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="be52d-113">Not all variation configuration settings are currently available via the SharePoint CSOM API Variations classes listed above.</span></span>
- <span data-ttu-id="be52d-114">Можно выходит за пределы предоставляют классы CSOM API вариантов, перечисленных выше и настроить некоторые параметры вариантов.</span><span class="sxs-lookup"><span data-stu-id="be52d-114">You can go beyond what the CSOM API Variations classes listed above provide and configure some variations settings.</span></span>  <span data-ttu-id="be52d-115">Чтобы сделать это, задайте значения для вариантов параметры хранятся в контейнеры свойств сайта и/или изменение элементов списка в списках, связанных с вариантов.</span><span class="sxs-lookup"><span data-stu-id="be52d-115">To do this, you set the values for variations settings stored in site property bags and/or modify list items in the lists associated with variations.</span></span>
    + <span data-ttu-id="be52d-116">[Класс VariationsExtensions.cs (PnP образец O365)](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) содержит несколько примеров, изменяющие контейнера и список элементов значения свойств для настройки параметров вариантов.</span><span class="sxs-lookup"><span data-stu-id="be52d-116">The [VariationsExtensions.cs class (O365 PnP Sample)](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) contains several examples that modify property bag and list item values to configure variations settings.</span></span>
    + <span data-ttu-id="be52d-117">[Класс VariationsExtensions.cs (PnP образец O365)](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) показано, как настроить ***все параметры*** , которые можно настроить на странице Параметры вариантов.</span><span class="sxs-lookup"><span data-stu-id="be52d-117">The [VariationsExtensions.cs class (O365 PnP Sample)](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs) illustrates how to configure ***all of the settings*** that you can set in the variations settings page.</span></span>
    + <span data-ttu-id="be52d-118">[Включить параметры вариантов, чтобы вы могли создать вариантов сайта (статья O365)](https://support.office.com/en-za/article/Turn-on-variations-settings-so-you-can-create-variations-of-your-site-fc021610-bdb5-4b5c-9d59-ce8af6699b4b) список элементов, можно настроить на странице Параметры вариантов и описание их функций.</span><span class="sxs-lookup"><span data-stu-id="be52d-118">The [Turn on variations settings so you can create variations of your site (O365 Support Article)](https://support.office.com/en-za/article/Turn-on-variations-settings-so-you-can-create-variations-of-your-site-fc021610-bdb5-4b5c-9d59-ce8af6699b4b) lists  the items you can configure in the variations settings page and describes what they do.</span></span>

<a name="related-links"></a><span data-ttu-id="be52d-119">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="be52d-119">Related links</span></span>
=============

- <span data-ttu-id="be52d-120">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="be52d-120">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="be52d-121">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="be52d-121">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="be52d-122">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="be52d-122">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="be52d-123">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="be52d-123">Related PnP samples</span></span>
===================

- [<span data-ttu-id="be52d-124">Класс VariationsExtensions.cs (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="be52d-124">VariationsExtensions.cs class (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP-Sites-Core/blob/master/Core/OfficeDevPnP.Core/Extensions/VariationExtensions.cs)
- <span data-ttu-id="be52d-125">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="be52d-125">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="be52d-126">Применимо к</span><span class="sxs-lookup"><span data-stu-id="be52d-126">Applies to</span></span>
==========
- <span data-ttu-id="be52d-127">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="be52d-127">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="be52d-128">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="be52d-128">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="be52d-129">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="be52d-129">SharePoint 2013 on-premises</span></span>
