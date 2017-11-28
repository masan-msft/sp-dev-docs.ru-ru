---
title: "Политики управления сведениями в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: f395b7fa40f4798b2184bd637ca752c468b9289d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="information-management-policy-in-the-sharepoint-add-in-model"></a><span data-ttu-id="71958-102">Политики управления сведениями в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="71958-102">Information management policy in the SharePoint add-in model</span></span>
============================================================

<a name="summary"></a><span data-ttu-id="71958-103">Summary</span><span class="sxs-lookup"><span data-stu-id="71958-103">Summary</span></span>
-------

<span data-ttu-id="71958-104">Подхода, можно применить политику управления сведениями отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="71958-104">The approach you take to apply information management policy is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="71958-105">В типичных полного доверия кода (FTC) сценарий решения фермы, сведений политики управления был управляемых и применяется с помощью объектной модели SharePoint Server со стороны и развернуты через решения в ферме SharePoint, как правило, как часть таймера задания.</span><span class="sxs-lookup"><span data-stu-id="71958-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, information management policy was managed and applied via the SharePoint Server Side Object Model and deployed via SharePoint Farm Solutions, usually as part of a Timer Job.</span></span> 

<span data-ttu-id="71958-106">В модели сценарий SharePoint Add-in SharePoint клиента со стороны объектной модели (CSOM) и задания таймера удаленного используются для управления и применение политики управления сведениями.</span><span class="sxs-lookup"><span data-stu-id="71958-106">In a SharePoint Add-in model scenario, the SharePoint Client Side Object Model (CSOM) and remote timer jobs are used to manage and apply information management policy.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="71958-107">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="71958-107">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="71958-108">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее по управлению и применение политик управления сведениями к сайтам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="71958-108">As a rule of a thumb, we would like to provide the following high level guidelines to manage and apply information management policies to SharePoint sites.</span></span>  

- <span data-ttu-id="71958-109">Имейте в виду при определении политики управления сведениями на уровне семейства сайтов и владельцев семейства сайтов может отключить их.</span><span class="sxs-lookup"><span data-stu-id="71958-109">Keep in mind, when information management policies are defined at the site collection level then site collection owners may disable them.</span></span>
    + <span data-ttu-id="71958-110">При использовании удаленного модели и CSOM настраивать политики управления сведения владелец семейства сайтов не могут отключить их.</span><span class="sxs-lookup"><span data-stu-id="71958-110">When using the remote model and CSOM to set information management policies a site collection owner cannot disable them.</span></span>  <span data-ttu-id="71958-111">Удаленный модели подход заключается в более понятное модель предприятия и обеспечивает политик управления сведениями всегда включена во всей среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="71958-111">The remote model approach is a more enterprise friendly model that ensures information management policies are always enabled throughout a SharePoint environment.</span></span>
- <span data-ttu-id="71958-112">Используйте SharePoint CSOM в задания таймера удаленного управления и применение политик управления сведениями.</span><span class="sxs-lookup"><span data-stu-id="71958-112">Use the SharePoint CSOM in a remote timer job to manage and apply information management policies.</span></span>

- <span data-ttu-id="71958-113">Убедитесь, что вы не нарушают пределы регулирования Office 365 SharePoint API при работе с большими наборами данных и рекурсивный обходит как проверять артефактов на веб-сайтах SharePoint и применение политик управления сведениями для них соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="71958-113">Ensure you are not violating the Office 365 SharePoint API throttle limits when working with large data sets and recursive crawls as you inspect artifacts in your SharePoint sites and apply information management policies to them accordingly.</span></span>
    + <span data-ttu-id="71958-114">[Core.Throttling (Pnp образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) показано, как создавать intelligent код для обработки регулирования Office 365 SharePoint API.</span><span class="sxs-lookup"><span data-stu-id="71958-114">The [Core.Throttling (O365 Pnp Sample)](https://github.com/SharePoint/PnP/tree/master/Samples/Core.Throttling) demonstrates how to write intelligent code to handle Office 365 SharePoint API throttling.</span></span>

<span data-ttu-id="71958-115">**Примечание:** В настоящее время CSOM не имеет методов, чтобы задать хранения для типов контента (только на сайтах).</span><span class="sxs-lookup"><span data-stu-id="71958-115">**Note:** Currently, the CSOM does not have methods to set retention on content types (only on sites).</span></span>

<span data-ttu-id="71958-116">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="71958-116">**Getting Started**</span></span>

<span data-ttu-id="71958-117">Следующий пример кода O365 PnP и видео показано, как управлять и применение политики управления сведениями для сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="71958-117">The following O365 PnP Code Sample and video demonstrates how to manage and apply information management policy for SharePoint sites.</span></span>  <span data-ttu-id="71958-118">В этом примере кода выполняется итерация по типов контента, применяется к библиотекам документов в семействах сайтов SharePoint и применяет политику хранения.</span><span class="sxs-lookup"><span data-stu-id="71958-118">In this example, the code iterates through the content types applied to document libraries in SharePoint site collections and applies a retention policy.</span></span>

- [<span data-ttu-id="71958-119">Governance.ContentTypeEnforceRetention (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="71958-119">Governance.ContentTypeEnforceRetention (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)

<span data-ttu-id="71958-120">Следующем видеоролике описывается пример кода.</span><span class="sxs-lookup"><span data-stu-id="71958-120">The following video walks through the code sample.</span></span>

- [<span data-ttu-id="71958-121">Политики управления сведениями с моделью приложений (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="71958-121">Information management policy with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)

<a name="related-links"></a><span data-ttu-id="71958-122">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="71958-122">Related links</span></span>
=============
- [<span data-ttu-id="71958-123">Политики управления сведениями с моделью приложений (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="71958-123">Information management policy with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Information-management-policy-wtih-app-model)
- <span data-ttu-id="71958-124">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="71958-124">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="71958-125">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="71958-125">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="71958-126">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="71958-126">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="71958-127">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="71958-127">Related PnP samples</span></span>
===================

- [<span data-ttu-id="71958-128">Governance.ContentTypeEnforceRetention (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="71958-128">Governance.ContentTypeEnforceRetention (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Governance.ContentTypeEnforceRetention)
- <span data-ttu-id="71958-129">Примеры и содержимое в https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="71958-129">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="71958-130">Применимо к</span><span class="sxs-lookup"><span data-stu-id="71958-130">Applies to</span></span>
==========
- <span data-ttu-id="71958-131">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="71958-131">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="71958-132">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="71958-132">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="71958-133">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="71958-133">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="71958-134">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="71958-134">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
