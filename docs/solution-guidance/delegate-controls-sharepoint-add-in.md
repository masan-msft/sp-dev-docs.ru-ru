---
title: "Делегирование элементов управления в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 3981faf45be7a2a5e80dae40859b023d9dda9092
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="delegate-controls-in-the-sharepoint-add-in-model"></a><span data-ttu-id="b6f6e-102">Делегирование элементов управления в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="b6f6e-102">Delegate controls in the SharePoint add-in model</span></span>
================================================

<a name="summary"></a><span data-ttu-id="b6f6e-103">Summary</span><span class="sxs-lookup"><span data-stu-id="b6f6e-103">Summary</span></span>
-------

<span data-ttu-id="b6f6e-104">Подхода, можно реализовать элементов управления делегированием в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-104">The approach you take to implement delegate controls in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="b6f6e-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, делегат элементы управления были созданы как пользовательские элементы управления или веб-элементы управления, зарегистрированные с использованием функций и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, delegate controls were built as user controls or web controls, registered with features, and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="b6f6e-106">В SharePoint надстройки модели сценарии JavaScript встраивается в страницы SharePoint для реализации функциональных возможностей элементов управления делегированием.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-106">In an SharePoint Add-in model scenario, JavaScript is embedded in SharePoint pages to implement the same functionality as delegate controls.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="b6f6e-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="b6f6e-107">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="b6f6e-108">Как правило эскиз мы предлагаем обеспечивает следующие рекомендации высокого уровня для создания элементов управления делегированием в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-108">As a rule of a thumb, we would like to provide the following high level guidelines for creating delegate controls in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="b6f6e-109">Нет замена элемента управления не прямой делегат в модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-109">There is no direct delegate control replacement in the SharePoint Add-in model.</span></span>
- <span data-ttu-id="b6f6e-110">Используйте внедренные JavaScript для реализации функциональных возможностей элементов управления делегированием с точки зрения конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-110">Use embedded JavaScript to implement the same functionality as delegate controls from an end-user's perspective.</span></span>
- <span data-ttu-id="b6f6e-111">Используйте SharePoint JavaScript клиента со стороны объектной модели (JSOM) и/или API-интерфейсы REST SharePoint и Office 365 для взаимодействия с данным и службам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-111">Use the SharePoint JavaScript Client Side Object Model (JSOM), and/or the SharePoint/Office365 REST APIs to interact with SharePoint data and services.</span></span>

<span data-ttu-id="b6f6e-112">В разделе [пользовательские элементы управления и веб-элементов управления (добавить в SharePoint рецептов модели)](user-controls-and-web-controls-sharepoint-add-in.md) для внедрения JavaScript на всех страницах SharePoint с помощью пользовательских действий и внедрения JavaScript непосредственно в макеты страниц и главных страниц.</span><span class="sxs-lookup"><span data-stu-id="b6f6e-112">See the [User controls and web controls (SharePoint Add-in Model Recipe)](user-controls-and-web-controls-sharepoint-add-in.md) to learn how to embed JavaScript to all SharePoint pages with custom user actions and how to embed JavaScript directly into page layouts and master pages.</span></span>

<a name="related-links"></a><span data-ttu-id="b6f6e-113">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="b6f6e-113">Related links</span></span>
=============
- [<span data-ttu-id="b6f6e-114">Кросс-структура навигации семейства сайтов (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="b6f6e-114">Cross site collection navigation (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- <span data-ttu-id="b6f6e-115">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="b6f6e-115">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="b6f6e-116">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="b6f6e-116">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="b6f6e-117">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="b6f6e-117">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="b6f6e-118">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="b6f6e-118">Related PnP samples</span></span>
===================
- [<span data-ttu-id="b6f6e-119">OD4B. NavLinksInjection (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="b6f6e-119">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- <span data-ttu-id="b6f6e-120">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="b6f6e-120">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="b6f6e-121">Применимо к</span><span class="sxs-lookup"><span data-stu-id="b6f6e-121">Applies to</span></span>
==========
- <span data-ttu-id="b6f6e-122">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="b6f6e-122">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="b6f6e-123">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="b6f6e-123">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="b6f6e-124">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="b6f6e-124">SharePoint 2013 on-premises</span></span>
