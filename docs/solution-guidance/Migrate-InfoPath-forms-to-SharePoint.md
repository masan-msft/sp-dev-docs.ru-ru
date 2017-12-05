---
title: "Перенос форм InfoPath в SharePoint 2013"
ms.date: 11/03/2017
ms.openlocfilehash: f53ff1c78524e1a18e7082317dc9bc5c0aa56cdf
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="migrate-infopath-forms-to-sharepoint-2013"></a><span data-ttu-id="243ec-102">Перенос форм InfoPath в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="243ec-102">Migrate InfoPath forms to SharePoint 2013</span></span>

<span data-ttu-id="243ec-103">Перенос форм InfoPath в SharePoint add-ins в других поддерживаемых решений, такие как приложения Access, изолированные решения или модель надстройки.</span><span class="sxs-lookup"><span data-stu-id="243ec-103">Migrate InfoPath forms in your SharePoint add-ins to other supported solutions, such as Access applications, sandbox solutions, or the add-in model.</span></span>

<span data-ttu-id="243ec-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="243ec-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="243ec-105">Если вы используете InfoPath в качестве основы для создания форм в вашей надстроек, необходимо на данном этапе для подумать о переходе формы на другие решения.</span><span class="sxs-lookup"><span data-stu-id="243ec-105">If you're using InfoPath as the basis for creating forms in your add-ins, now is the time to start thinking about migrating your forms to other solutions.</span></span> <span data-ttu-id="243ec-106">Хотя InfoPath в настоящее время поддерживаются, InfoPath 2013 — это последний выпуск рабочего стола клиента InfoPath и InfoPath Forms Services в SharePoint 2013 — это последний выпуск службы InfoPath Forms Services.</span><span class="sxs-lookup"><span data-stu-id="243ec-106">Although InfoPath is currently supported, InfoPath 2013 is the last release of the desktop InfoPath client, and InfoPath Forms Services in SharePoint 2013 is the last release of InfoPath Forms Services.</span></span> <span data-ttu-id="243ec-107">Клиент и в локальной версии InfoPath Forms Services в SharePoint 2013 будет полностью поддерживаться до 2023.</span><span class="sxs-lookup"><span data-stu-id="243ec-107">The client and the on-premises version of InfoPath Forms Services in SharePoint 2013 will be fully supported until 2023.</span></span> <span data-ttu-id="243ec-108">Службы форм будут поддерживаться в Office 365 до по крайней мере Далее основной версии Office.</span><span class="sxs-lookup"><span data-stu-id="243ec-108">The forms service will be supported in Office 365 until at least the next major release of Office.</span></span>

<span data-ttu-id="243ec-109">Чтобы заменить формы InfoPath, можно выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="243ec-109">To replace your InfoPath forms, you can choose one of the following alternatives:</span></span>

- <span data-ttu-id="243ec-110">Использование приложений Access.</span><span class="sxs-lookup"><span data-stu-id="243ec-110">Use Access applications.</span></span>

- <span data-ttu-id="243ec-111">С помощью Microsoft потока и Microsoft PowerApps.</span><span class="sxs-lookup"><span data-stu-id="243ec-111">Use Microsoft Flow and Microsoft PowerApps.</span></span>
    
- <span data-ttu-id="243ec-112">Перемещение сложных типов поведения новые надстройки модели и клиента со стороны разработки.</span><span class="sxs-lookup"><span data-stu-id="243ec-112">Move complex behaviors to new add-in model and client side developments.</span></span>
    
<span data-ttu-id="243ec-113">Мы рекомендуем первые два решения, так как их реализации информационных работников, не знаете, как создавать и развертывать на основе кода альтернативы.</span><span class="sxs-lookup"><span data-stu-id="243ec-113">We recommend the first two solutions, because information workers who don't know how to write and deploy code-based alternatives can implement them.</span></span> <span data-ttu-id="243ec-114">В следующей таблице описаны сценарии, для которых больше всего подходит каждого из вариантов.</span><span class="sxs-lookup"><span data-stu-id="243ec-114">The following table describes the scenarios for which each alternative is best suited.</span></span>

<span data-ttu-id="243ec-115">**Альтернативы InfoPath в SharePoint 2013**</span><span class="sxs-lookup"><span data-stu-id="243ec-115">**Alternatives to InfoPath in SharePoint 2013**</span></span>

|<span data-ttu-id="243ec-116">**Альтернатива**</span><span class="sxs-lookup"><span data-stu-id="243ec-116">**Alternative**</span></span>|<span data-ttu-id="243ec-117">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="243ec-117">**Scenario**</span></span>|
|:-----|:-----|
|<span data-ttu-id="243ec-118">Получать доступ к приложениям</span><span class="sxs-lookup"><span data-stu-id="243ec-118">Access applications</span></span>|<span data-ttu-id="243ec-119">Этот параметр поддерживает несколько форм, которые обрабатывают реляционные данные, содержащиеся в нескольких таблиц Access, таблиц Excel, и/или списки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="243ec-119">This option supports multiple forms that handle relational data contained in multiple Access tables, Excel tables, and/or SharePoint lists.</span></span>|
|<span data-ttu-id="243ec-120">Использование Microsoft потока и Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="243ec-120">Use Microsoft Flow and Microsoft PowerApps</span></span>|<span data-ttu-id="243ec-121">Это наш рекомендуемый подход для расширения списков SharePoint опытных пользователей.</span><span class="sxs-lookup"><span data-stu-id="243ec-121">This is the our recommended approach for extending lists by SharePoint power users .</span></span>|
|<span data-ttu-id="243ec-122">Новые надстройки модели и клиента со стороны разработки</span><span class="sxs-lookup"><span data-stu-id="243ec-122">New add-in model and client side developments</span></span> |<span data-ttu-id="243ec-123">Можно преобразовать сложных форм, управляемых с помощью с много кода на стороне провайдера, надстройки или веб-частей со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="243ec-123">You can convert complex forms driven by extensive code into provider-hosted add-ins or client side web parts.</span></span> <span data-ttu-id="243ec-124">Этот параметр требует ресурсы для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="243ec-124">This option requires developer resources.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="243ec-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="243ec-125">Additional resources</span></span>
<span data-ttu-id="243ec-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="243ec-126"></span></span>

-  [<span data-ttu-id="243ec-127">Шаблоны и рекомендации по InfoPath преобразования</span><span class="sxs-lookup"><span data-stu-id="243ec-127">Patterns and Practices InfoPath transformation guidance</span></span>](https://github.com/SharePoint/PnP-Transformation/tree/master/InfoPath) 

-  [<span data-ttu-id="243ec-128">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="243ec-128">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="243ec-129">Шаблоны и рекомендации по разработке решений для Office 365 на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="243ec-129">Office 365 Development Patterns and Practices on GitHub</span></span>](https://github.com/SharePoint/PnP)