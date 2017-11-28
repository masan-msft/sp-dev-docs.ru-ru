---
title: "Веб-часть в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 65e236df834b82d9649d2e43cd3dfef37ebdcdb4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="web-part-in-the-sharepoint-add-in-model"></a><span data-ttu-id="49604-102">Веб-часть в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="49604-102">Web part in the SharePoint add-in model</span></span>
=======================================

<a name="summary"></a><span data-ttu-id="49604-103">Summary</span><span class="sxs-lookup"><span data-stu-id="49604-103">Summary</span></span>
-------

<span data-ttu-id="49604-104">Подхода, можно создавать компоненты portable страницы отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="49604-104">The approach you take to create portable page components is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="49604-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, веб-части были созданы для реализации компонентов portable страницы.</span><span class="sxs-lookup"><span data-stu-id="49604-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, Web Parts were created to implement portable page components.</span></span>

<span data-ttu-id="49604-106">В SharePoint надстройки модели сценарии частей Add-in (части приложения) создаются для реализации компонентов portable страницы.</span><span class="sxs-lookup"><span data-stu-id="49604-106">In an SharePoint Add-in model scenario, Add-in Parts (App Parts) are created to implement portable page components.</span></span>  <span data-ttu-id="49604-107">Добавьте в части будут использовать коде на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="49604-107">Add-in parts use client side code.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="49604-108">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="49604-108">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="49604-109">Как правило эскиз мы хотели бы предоставляют следующие рекомендации высокого уровня по части надстройки.</span><span class="sxs-lookup"><span data-stu-id="49604-109">As a rule of a thumb, we would like to provide the following high level guidelines regarding Add-in Parts.</span></span>

- <span data-ttu-id="49604-110">Нельзя запустить серверного кода в частях надстройки.</span><span class="sxs-lookup"><span data-stu-id="49604-110">You cannot run server side code in Add-in Parts.</span></span>
- <span data-ttu-id="49604-111">Не удается создать пользовательский редактор частей частей Add-in.</span><span class="sxs-lookup"><span data-stu-id="49604-111">You cannot create custom editor parts for Add-in Parts.</span></span>
- <span data-ttu-id="49604-112">Используйте Add-in часть скрипта для связи с JavaScript, который используется для взаимодействия с SharePoint и другие службы и создания пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="49604-112">Use the Add-in Script Part to link to JavaScript that is used to interact with SharePoint and other services and create a user interface.</span></span>
- <span data-ttu-id="49604-113">По умолчанию настраиваемые свойства, добавляемые к частям редактора всегда отображаются как окончательный группы в части "редактор".</span><span class="sxs-lookup"><span data-stu-id="49604-113">By default, custom properties you add to editor parts are always shown as the final group in an editor part.</span></span>
    + <span data-ttu-id="49604-114">Чтобы переопределить внешний вид и функции части редактора для части Add-in можно использовать JavaScript.</span><span class="sxs-lookup"><span data-stu-id="49604-114">You can use JavaScript to override the look and feel of an editor part for an Add-in Part.</span></span>
    + <span data-ttu-id="49604-115">Следующий пример, в котором показано, как это делается в разделе.</span><span class="sxs-lookup"><span data-stu-id="49604-115">See the following sample that demonstrates how this is done.</span></span> 
    + [<span data-ttu-id="49604-116">Core.AppPartPropertyUIOverride (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="49604-116">Core.AppPartPropertyUIOverride (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)

<span data-ttu-id="49604-117">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="49604-117">**Getting Started**</span></span>

<span data-ttu-id="49604-118">Части надстройки могут легко создавать с помощью ожидания поле Add-in части скрипта.</span><span class="sxs-lookup"><span data-stu-id="49604-118">Add-in Parts may be easily created by using the out of the box Add-in Script Part.</span></span>  <span data-ttu-id="49604-119">Это позволяет указать ссылку на файл JavaScript, размещенных в любом месте.</span><span class="sxs-lookup"><span data-stu-id="49604-119">This allows you to provide a link to a JavaScript file hosted anywhere.</span></span>  <span data-ttu-id="49604-120">Файл JavaScript коде на стороне клиента использует для взаимодействия с SharePoint или других служб и отображения пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="49604-120">The JavaScript file uses client side code to interact with SharePoint or other services and render a user interface.</span></span>

<span data-ttu-id="49604-121">Со следующей статьей описание шаблона Add-in части скрипта и использовать его.</span><span class="sxs-lookup"><span data-stu-id="49604-121">The following article describes the Add-in Script Part pattern and how to use it.</span></span>

- [<span data-ttu-id="49604-122">Краткие сведения о шаблон части скрипта приложений для модели приложения Office 365 (статья блога MSDN)</span><span class="sxs-lookup"><span data-stu-id="49604-122">Introducing app script part pattern for Office365 app model (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)

<span data-ttu-id="49604-123">Следующий пример демонстрирует использование части скрипта Add-in можно интегрировать с Yammer, Bing Maps и Google карт.</span><span class="sxs-lookup"><span data-stu-id="49604-123">The following sample demonstrates how to use an Add-in Script Part to integrate with Yammer, Bing Maps, and Google Maps.</span></span>

- [<span data-ttu-id="49604-124">Core.AppScriptPart (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="49604-124">Core.AppScriptPart (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)

<span data-ttu-id="49604-125">Следующем видеоролике описывается пример кода.</span><span class="sxs-lookup"><span data-stu-id="49604-125">The following video walks you through the code sample.</span></span>

- [<span data-ttu-id="49604-126">Core.AppScriptPart (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="49604-126">Core.AppScriptPart (O365 PnP Video)</span></span>](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)

<a name="related-links"></a><span data-ttu-id="49604-127">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="49604-127">Related links</span></span>
=============

- [<span data-ttu-id="49604-128">Краткие сведения о шаблон части скрипта приложений для модели приложения Office 365 (статья блога MSDN)</span><span class="sxs-lookup"><span data-stu-id="49604-128">Introducing app script part pattern for Office365 app model (MSDN Blog Article)</span></span>](http://blogs.msdn.com/b/vesku/archive/2014/07/08/introducing-app-script-part-pattern-for-office365-app-model.aspx)
- [<span data-ttu-id="49604-129">Core.AppScriptPart (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="49604-129">Core.AppScriptPart (O365 PnP Video)</span></span>](https://channel9.msdn.com/Blogs/Office-365-Dev/App-Script-Parts-in-SharePoint-Office-365-Developer-Patterns-and-Practices)
- <span data-ttu-id="49604-130">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="49604-130">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="49604-131">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="49604-131">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="49604-132">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="49604-132">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="49604-133">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="49604-133">Related PnP samples</span></span>
===================

- [<span data-ttu-id="49604-134">Core.AppPartPropertyUIOverride (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="49604-134">Core.AppPartPropertyUIOverride (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppPartPropertyUIOverride)
- [<span data-ttu-id="49604-135">Core.AppScriptPart (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="49604-135">Core.AppScriptPart (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppScriptPart)
- <span data-ttu-id="49604-136">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="49604-136">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="49604-137">Применимо к</span><span class="sxs-lookup"><span data-stu-id="49604-137">Applies to</span></span>
==========
- <span data-ttu-id="49604-138">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="49604-138">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="49604-139">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="49604-139">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="49604-140">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="49604-140">SharePoint 2013 on-premises</span></span>
