---
title: "Локализация в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 33a39ac3c656c9de086432da14ce6fa6cac34870
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="localization-in-the-sharepoint-add-in-model"></a><span data-ttu-id="cfd9f-102">Локализация в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="cfd9f-102">Localization in the SharePoint add-in model</span></span>
===========================================

<a name="summary"></a><span data-ttu-id="cfd9f-103">Summary</span><span class="sxs-lookup"><span data-stu-id="cfd9f-103">Summary</span></span>
-------

<span data-ttu-id="cfd9f-104">Подхода, можно реализовать локализации для надстроек отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-104">The approach you take to implement localization for Add-ins is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="cfd9f-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, локализации для пользовательских компонентов, таких как веб-частей, пользовательские элементы управления и веб-элементы управления были реализованы сочетание файлы ресурсов, код под управлением .net, свойств и декларативного кода.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, localization for custom components such as Web Parts, User Controls, and Web Controls was implemented with a combination of resource files, .Net managed code, properties, and declarative code.</span></span>  <span data-ttu-id="cfd9f-106">Все артефакты были упакованный в компоненты, развернутые с помощью решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-106">All the artifacts were packaged in features deployed via SharePoint Solutions.</span></span>

<span data-ttu-id="cfd9f-107">В SharePoint надстройки модели сценарии используйте JavaScript или возможности локализации, связанный с этой технологии web, созданного вашей надстройки с помощью для реализации локализации.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-107">In an SharePoint Add-in model scenario, you use JavaScript or the localization capabilities associated with the web technology you build your Add-ins with to implement localization.</span></span> <span data-ttu-id="cfd9f-108">В зависимости от локализованных ресурсов также вы можете использовать файлы классический ресурсы, например, при необходимости развернуто надстройки-сети с помощью компонента элементы в определении надстройка lozalize элементов.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-108">Depending on the localized resource, you might also use classic resources files, for example when you need to lozalize elements deployed to add-in web using feature framework elements in the add-in definition.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="cfd9f-109">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="cfd9f-109">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="cfd9f-110">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации по внедрению локализации.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-110">As a rule of a thumb, we would like to provide the following high-level guidelines for implementing localization.</span></span>

- <span data-ttu-id="cfd9f-111">Необходимо установить соответствующие языковые пакеты в SharePoint в локальной среде и среде Office 365, чтобы разрешить пользователям создавать веб-сайты в конкретного языка и региональных параметров.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-111">You must install the appropriate Language Packs in your SharePoint on-premises and Office 365 environments to enable users to create websites in a specific language and culture.</span></span>
- <span data-ttu-id="cfd9f-112">С помощью JavaScript для реализации в SharePoint надстройки локализации также является подход, которые можно использовать для локализации содержимого в частях редактор сценариев надстройки.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-112">Using JavaScript to implement localization in SharePoint Add-ins is also an approach you may use to localize content in Script Editor Add-in Parts.</span></span> 

<a name="localization-scenarios"></a><span data-ttu-id="cfd9f-113">Локализация сценариев</span><span class="sxs-lookup"><span data-stu-id="cfd9f-113">Localization scenarios</span></span>
----------------------

<span data-ttu-id="cfd9f-114">Существует два различных сценария, где необходимо реализовать локализации для надстройки.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-114">There are two distinct scenarios where you may need to implement localization for an Add-in.</span></span>

- <span data-ttu-id="cfd9f-115">Размещение в SharePoint надстроек</span><span class="sxs-lookup"><span data-stu-id="cfd9f-115">SharePoint-hosted Add-ins</span></span>
- <span data-ttu-id="cfd9f-116">Размещение у поставщика надстроек</span><span class="sxs-lookup"><span data-stu-id="cfd9f-116">Provider-hosted Add-ins</span></span>

<a name="add-in-web-components-or-assets"></a><span data-ttu-id="cfd9f-117">Добавление в веб-компоненты или активов</span><span class="sxs-lookup"><span data-stu-id="cfd9f-117">Add-in web components or assets</span></span>
-------------------------
<span data-ttu-id="cfd9f-118">В этом сценарии локализации применяется к надстройки с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-118">In this scenario localization is applied to the Add-in via JavaScript.</span></span>

- <span data-ttu-id="cfd9f-119">Размещение в SharePoint надстройки нет доступа к файлам на стороне сервера ресурсов на серверах SharePoint, но у вас есть доступ на файлы resx элемент компонента</span><span class="sxs-lookup"><span data-stu-id="cfd9f-119">SharePoint-hosted Add-ins do not have access to server-based resource files in the SharePoint servers, but you have access on the feature element resx files</span></span> 
- <span data-ttu-id="cfd9f-120">Подход к локализации надстройка размещенных в SharePoint и Office Add-in очень похожи, так как они используют JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-120">The approach to localize a SharePoint-hosted Add-in and an Office Add-in are very similar because they both use JavaScript.</span></span>

<span data-ttu-id="cfd9f-121">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="cfd9f-121">**When is it a good fit?**</span></span>

<span data-ttu-id="cfd9f-122">При создании надстройки размещенных в SharePoint с помощью JavaScript является наилучшего соответствия, поскольку можно реализовать локализации с помощью JavaScript и развернуть все файлы JavaScript, необходимые для поддержки локализации с помощью надстройки размещенных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-122">When you are creating a SharePoint-hosted Add-in, using JavaScript is your best fit because you can implement localization with JavaScript and deploy all of the JavaScript files necessary to support localization with the SharePoint-hosted Add-in.</span></span> <span data-ttu-id="cfd9f-123">Можно также использовать преимущества этого подхода Если надстройка размещением у поставщика также содержит определенные web.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-123">You can also take advantage of this approach if your provider hosted add-in contains also specific add-in web.</span></span>

<span data-ttu-id="cfd9f-124">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="cfd9f-124">**Getting Started**</span></span>

<span data-ttu-id="cfd9f-125">Сценарий 2 в [Core.JavaScriptCustomization (O365 PnP образец))](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) демонстрируется использование JavaScript для локализации текста в надстройку, а также атрибуты, связанные с элементами HTML в надстройку.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-125">Scenario 2 in the [Core.JavaScriptCustomization (O365 PnP Sample))](https://github.com/SharePoint/PnP/tree/master/Samples/Core.JavaScriptCustomization) demonstrates how to use JavaScript to localize the text in an Add-in as well as attributes associated with the HTML elements in the Add-in.</span></span>

<span data-ttu-id="cfd9f-126">[Локализация SharePoint надстройки](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx) также демонстрируется использование JavaScript для локализации активов на-сайте.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-126">The [Localize SharePoint Add-ins](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx) also demonstrates how to use JavaScript to localize assets in the add-in web.</span></span>

<a name="remote-components"></a><span data-ttu-id="cfd9f-127">Удаленные компоненты</span><span class="sxs-lookup"><span data-stu-id="cfd9f-127">Remote components</span></span>
-------------------------
<span data-ttu-id="cfd9f-128">В этом сценарии локализации применяется к надстройки с помощью технологий локализации, связанный с веб-технологии, размещения надстройки.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-128">In this scenario localization is applied to the Add-in via the localization technologies associated with the web technology hosting the Add-in.</span></span>

- <span data-ttu-id="cfd9f-129">При использовании ASP.NET для реализации надстройки файлов ресурсов и файлов JavaScript используются для локализации его.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-129">When ASP.NET is used to implement the Add-in, resource files and JavaScript files are used to localize it.</span></span>
- <span data-ttu-id="cfd9f-130">Если другой технологии, такие как PHP, Python или транскрипцию, используемых для реализации надстройки используется возможности локализации, связанный с этим платформ.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-130">When another technology such as PHP, Python, or Ruby are used to implement the Add-in the localization capabilities associated with those platforms is used.</span></span>

<span data-ttu-id="cfd9f-131">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="cfd9f-131">**When is it a good fit?**</span></span>

<span data-ttu-id="cfd9f-132">При создании надстройки размещением у поставщика с помощью технологии локализации, поступающие платформе размещения веб-является наиболее подобрать так как построении надстройки, чтобы не вводить пользовательский код или дополнительная сложность.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-132">When you are creating a Provider-hosted Add-in, using the localization technology that comes with the web hosting platform is the best fit because you are building the Add-in in a way that does not introduce custom code or additional complexity.</span></span>

<span data-ttu-id="cfd9f-133">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="cfd9f-133">**Getting Started**</span></span>

<span data-ttu-id="cfd9f-134">Следующие статьи описывается, как локализовать размещение у поставщика в список надстроек с помощью файлов ресурсов и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cfd9f-134">The following articles describes how to localize Provider-hosted Add-ins with resource files and JavaScript.</span></span>

- <span data-ttu-id="cfd9f-135">[Локализация SharePoint Add-ins (статья MSDN)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-135">[Localize SharePoint Add-ins (MSDN Article)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span></span>
- [<span data-ttu-id="cfd9f-136">Локализация web надстройки, хост-сайта и удаленных компонентов add-in (пример кода MSDN)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-136">Localize the add-in web, host web, and remote components of an add-in  (MSDN Code Sample)</span></span>](https://code.msdn.microsoft.com/office/SharePoint-2013-Bookstore-328060fc)

<a name="related-links"></a><span data-ttu-id="cfd9f-137">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="cfd9f-137">Related links</span></span>
=============

- <span data-ttu-id="cfd9f-138">[Локализация SharePoint Add-ins (статья MSDN)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-138">[Localize SharePoint Add-ins (MSDN Article)](https://msdn.microsoft.com/en-us/library/fp179919(v=office.15).aspx)</span></span>
- [<span data-ttu-id="cfd9f-139">Локализация web надстройки, хост-сайта и удаленных компонентов add-in (образец репозиториев разработчиков Office)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-139">Localize the add-in web, host web, and remote components of an add-in  (Office Dev GitHub sample)</span></span>](https://github.com/SharePoint/SharePoint-Add-in-Localization)
- <span data-ttu-id="cfd9f-140">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="cfd9f-140">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="cfd9f-141">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="cfd9f-141">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="cfd9f-142">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="cfd9f-142">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="cfd9f-143">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="cfd9f-143">Related PnP samples</span></span>
===================

- [<span data-ttu-id="cfd9f-144">Класс VariationsExtensions.cs (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-144">VariationsExtensions.cs class (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP-Sites-Core/tree/master/Core/OfficeDevPnP.Core/AppModelExtensions/VariationExtensions.cs)
- <span data-ttu-id="cfd9f-145">Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-145">Samples and content at [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="cfd9f-146">Применимо к</span><span class="sxs-lookup"><span data-stu-id="cfd9f-146">Applies to</span></span>
==========
- <span data-ttu-id="cfd9f-147">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-147">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="cfd9f-148">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="cfd9f-148">Office 365 Dedicated (D)</span></span>
- <span data-ttu-id="cfd9f-149">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="cfd9f-149">SharePoint 2013 on-premises</span></span>
