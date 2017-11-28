---
title: "Пользовательские элементы управления и веб-элементы управления в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: cd1f3b127a7ae2eb1ac06e75f5a23c8f13563a8f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="user-controls-and-web-controls-in-the-sharepoint-add-in-model"></a><span data-ttu-id="9aebb-102">Пользовательские элементы управления и веб-элементы управления в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="9aebb-102">User controls and Web controls in the SharePoint add-in model</span></span>
=============================================================

<a name="summary"></a><span data-ttu-id="9aebb-103">Summary</span><span class="sxs-lookup"><span data-stu-id="9aebb-103">Summary</span></span>
-------

<span data-ttu-id="9aebb-104">Подхода, можно реализовать пользовательских элементов управления в коде отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="9aebb-104">The approach you take to implement custom controls in your code is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="9aebb-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, настраиваемые элементы управления были созданы как пользовательские элементы управления или веб-элементы управления и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9aebb-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, custom controls were built as user controls or web controls and deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="9aebb-106">В модели сценарий надстройки SharePoint JavaScript встраивается в страницы SharePoint для реализации пользовательских элементов управления.</span><span class="sxs-lookup"><span data-stu-id="9aebb-106">In a SharePoint Add-in model scenario, the JavaScript is embedded in SharePoint pages to implement custom controls.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="9aebb-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="9aebb-107">High-level Guidelines</span></span>
---------------------

<span data-ttu-id="9aebb-108">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для создания пользовательских элементов управления в новой модели надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9aebb-108">As a rule of a thumb, we would like to provide the following high-level guidelines for creating custom controls in the new SharePoint Add-in model.</span></span>

- <span data-ttu-id="9aebb-109">Использование внедренных JavaScript для создания пользовательских элементов управления.</span><span class="sxs-lookup"><span data-stu-id="9aebb-109">Use embedded JavaScript to create custom controls.</span></span>
- <span data-ttu-id="9aebb-110">Используйте SharePoint ECMA клиента со стороны объектной модели (CSOM) и/или API-интерфейсы REST SharePoint и Office 365 для взаимодействия с данным и службам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9aebb-110">Use the SharePoint ECMA Client Side Object Model (CSOM), and/or the SharePoint/Office 365 REST APIs to interact with SharePoint data and services.</span></span>

<a name="options-to-embed-javascript-in-sharepoint-pages"></a><span data-ttu-id="9aebb-111">Параметры для внедрения JavaScript в страницы SharePoint</span><span class="sxs-lookup"><span data-stu-id="9aebb-111">Options to embed JavaScript in SharePoint pages</span></span>
-----------------------------------------------
<span data-ttu-id="9aebb-112">Существует несколько параметров для внедрения JavaScript в страницы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9aebb-112">You have a few options to embed JavaScript in SharePoint pages.</span></span>

- <span data-ttu-id="9aebb-113">Использование настраиваемых пользовательских действий</span><span class="sxs-lookup"><span data-stu-id="9aebb-113">Use custom user actions</span></span>
- <span data-ttu-id="9aebb-114">Внедрение JavaScript непосредственно в макеты страниц</span><span class="sxs-lookup"><span data-stu-id="9aebb-114">Embed JavaScript directly into page layouts</span></span>
- <span data-ttu-id="9aebb-115">Внедрение JavaScript непосредственно в настраиваемых главных страниц (не рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="9aebb-115">Embed JavaScript directly into custom master pages (not recommended)</span></span>

<a name="use-custom-user-actions"></a><span data-ttu-id="9aebb-116">Использование настраиваемых пользовательских действий</span><span class="sxs-lookup"><span data-stu-id="9aebb-116">Use custom user actions</span></span>
-----------------------
<span data-ttu-id="9aebb-117">В этом шаблоне настраиваемого пользовательского действия используются для внедрения JavaScript в страницу во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9aebb-117">In this pattern, custom user actions are used to embed JavaScript into a page at run time.</span></span>

- <span data-ttu-id="9aebb-118">Такой подход поддерживается абсолютно и — допустимый подход.</span><span class="sxs-lookup"><span data-stu-id="9aebb-118">This approach is absolutely supported and is a valid approach.</span></span>

<span data-ttu-id="9aebb-119">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="9aebb-119">**When is it a good fit?**</span></span>

<span data-ttu-id="9aebb-120">При необходимости для внедрения JavaScript в все страницы SharePoint, этот параметр используется подходит.</span><span class="sxs-lookup"><span data-stu-id="9aebb-120">When you need to embed JavaScript into all of your SharePoint pages, this option is a good fit.</span></span>

<span data-ttu-id="9aebb-121">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="9aebb-121">**Getting started**</span></span>

<span data-ttu-id="9aebb-122">Следующие статьи и сопутствующий видео демонстрируется использование настраиваемых пользовательских действий для внедрения JavaScript в страницах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9aebb-122">The following article and accompanying video demonstrates how to use custom user actions to embed JavaScript into SharePoint pages.</span></span>

- [<span data-ttu-id="9aebb-123">Core.EmbedJavaScript (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9aebb-123">Core.EmbedJavaScript (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [<span data-ttu-id="9aebb-124">OD4B. NavLinksInjection (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9aebb-124">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [<span data-ttu-id="9aebb-125">Кросс-структура навигации семейства сайтов (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="9aebb-125">Cross site collection navigation (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)

<a name="embed-javascript-directly-into-page-layouts"></a><span data-ttu-id="9aebb-126">Внедрение JavaScript непосредственно в макеты страниц</span><span class="sxs-lookup"><span data-stu-id="9aebb-126">Embed JavaScript directly into page layouts</span></span>
-------------------------------------------

<span data-ttu-id="9aebb-127">В этом шаблоне JavaScript встроена непосредственно в макеты страниц на сайтах публикации.</span><span class="sxs-lookup"><span data-stu-id="9aebb-127">In this pattern, JavaScript is embedded directly in page layouts in publishing sites.</span></span>  

- <span data-ttu-id="9aebb-128">Такой подход поддерживается абсолютно и — допустимый подход.</span><span class="sxs-lookup"><span data-stu-id="9aebb-128">This approach is absolutely supported and is a valid approach.</span></span>
- <span data-ttu-id="9aebb-129">Такой подход работает с сайтами публикации.</span><span class="sxs-lookup"><span data-stu-id="9aebb-129">This approach works with publishing sites.</span></span>

<span data-ttu-id="9aebb-130">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="9aebb-130">**When is it a good fit?**</span></span>

<span data-ttu-id="9aebb-131">При необходимости для внедрения JavaScript в определенных макетов страниц SharePoint на сайтах публикации в сценарии управления веб-Контентом, этот параметр используется подходит.</span><span class="sxs-lookup"><span data-stu-id="9aebb-131">When you need to embed JavaScript into specific SharePoint page layouts in publishing sites in a WCM scenario, this option is a good fit.</span></span>

<a name="embed-javascript-directly-into-custom-master-pages"></a><span data-ttu-id="9aebb-132">Внедрение JavaScript непосредственно в настраиваемых главных страниц</span><span class="sxs-lookup"><span data-stu-id="9aebb-132">Embed JavaScript directly into custom master pages</span></span>
--------------------------------------------------

<span data-ttu-id="9aebb-133">В этом шаблоне JavaScript встроена непосредственно в настраиваемых главных страниц.</span><span class="sxs-lookup"><span data-stu-id="9aebb-133">In this pattern, JavaScript is embedded directly in custom master pages.</span></span>  

- <span data-ttu-id="9aebb-134">Такой подход не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="9aebb-134">This approach is not recommended.</span></span>
- <span data-ttu-id="9aebb-135">Такой подход — допустимый подход.</span><span class="sxs-lookup"><span data-stu-id="9aebb-135">This approach is a valid approach.</span></span>
- <span data-ttu-id="9aebb-136">Внедрение JavaScript непосредственно в настраиваемых главных страниц, но оставьте учитывать в результате вы дополнительные долгосрочные затраты и проблемы, связанные с с будущими обновлениями.</span><span class="sxs-lookup"><span data-stu-id="9aebb-136">You can embed JavaScript directly in custom master pages, but keep in mind this will cause you additional long-term costs and challenges with future updates.</span></span>
    + <span data-ttu-id="9aebb-137">Если вы решили использовать настраиваемые главные страницы, будьте готовым применить изменения к настраиваемых главных страниц, когда основные функциональные обновления применяются к Office 365.</span><span class="sxs-lookup"><span data-stu-id="9aebb-137">If you chose to use custom master pages, be prepared to apply changes to the custom master pages when major functional updates are applied to Office 365.</span></span>

<span data-ttu-id="9aebb-138">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="9aebb-138">**When is it a good fit?**</span></span>

<span data-ttu-id="9aebb-139">Когда следует применять внедрения JavaScript в каждой главной страницы, так как она позволяет управлять которого главные страницы, JavaScript в это является хорошим выбором.</span><span class="sxs-lookup"><span data-stu-id="9aebb-139">When you need to embed JavaScript on a per master page basis, this is a good option because it allows you to control which master pages the JavaScript is embedded in.</span></span>

<a name="related-links"></a><span data-ttu-id="9aebb-140">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="9aebb-140">Related links</span></span>
=============
- [<span data-ttu-id="9aebb-141">Кросс-структура навигации семейства сайтов (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="9aebb-141">Cross site collection navigation (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Cross-site-collection-navigation)
- <span data-ttu-id="9aebb-142">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="9aebb-142">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="9aebb-143">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="9aebb-143">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="9aebb-144">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="9aebb-144">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="9aebb-145">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="9aebb-145">Related PnP samples</span></span>
===================
- [<span data-ttu-id="9aebb-146">Core.EmbedJavaScript (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9aebb-146">Core.EmbedJavaScript (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript)
- [<span data-ttu-id="9aebb-147">OD4B. NavLinksInjection (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9aebb-147">OD4B.NavLinksInjection (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/OD4B.NavLinksInjection)
- [<span data-ttu-id="9aebb-148">Core.EmbedJavaScript.WeekNumbers (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9aebb-148">Core.EmbedJavaScript.WeekNumbers (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScript.WeekNumbers)
- [<span data-ttu-id="9aebb-149">Core.EmbedJavaScriptJSOM (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="9aebb-149">Core.EmbedJavaScriptJSOM (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EmbedJavaScriptJSOM)
- [<span data-ttu-id="9aebb-150">Core.JavaScriptCustomization (O365 PnP сценария с помощью компонента PnP ядра)</span><span class="sxs-lookup"><span data-stu-id="9aebb-150">Core.JavaScriptCustomization (O365 PnP Scenario using PnP Core component)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization)
- <span data-ttu-id="9aebb-151">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="9aebb-151">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="9aebb-152">Применимо к</span><span class="sxs-lookup"><span data-stu-id="9aebb-152">Applies to</span></span>
==========
- <span data-ttu-id="9aebb-153">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="9aebb-153">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="9aebb-154">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="9aebb-154">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="9aebb-155">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="9aebb-155">SharePoint 2013 on-premises</span></span>
