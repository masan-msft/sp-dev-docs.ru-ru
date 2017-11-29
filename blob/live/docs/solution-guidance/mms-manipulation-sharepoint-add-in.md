---
title: "Обработка MMS в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 0d1509b65fcd33068182b3747f21e1cb1db86238
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="mms-manipulation-in-the-sharepoint-add-in-model"></a><span data-ttu-id="6814f-102">Обработка MMS в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="6814f-102">MMS manipulation in the SharePoint add-in model</span></span>
===============================================

<a name="summary"></a><span data-ttu-id="6814f-103">Summary</span><span class="sxs-lookup"><span data-stu-id="6814f-103">Summary</span></span>
-------

<span data-ttu-id="6814f-104">Подхода, можно выполнять операции создания, чтения, обновления и удаления (CRUD) в службе управляемых метаданных (MMS) отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="6814f-104">The approach you take to perform Create, Read, Update and Delete (CRUD) operations in the Managed Metadata Service (MMS) is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span> <span data-ttu-id="6814f-105">В типичных полного доверия кода (FTC) / сценарий решения фермы операций MMS CRUD было выполнять с помощью кода на сервере объектной модели SharePoint и развернуты с помощью решений фермы.</span><span class="sxs-lookup"><span data-stu-id="6814f-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, MMS CRUD operations were performed with the SharePoint server-side object model code and deployed via Farm Solutions.</span></span> 

<span data-ttu-id="6814f-106">В модели сценарий надстройки SharePoint операций MMS CRUD выполняются с помощью клиентской объектной модели (CSOM).</span><span class="sxs-lookup"><span data-stu-id="6814f-106">In a SharePoint Add-in model scenario, MMS CRUD operations are performed with the client-side object model (CSOM).</span></span>

<span data-ttu-id="6814f-107">**CSOM предоставляет все операции, необходимые для репликации и синхронизации данных в MMS.**</span><span class="sxs-lookup"><span data-stu-id="6814f-107">**The CSOM provides all of the operations necessary to replicate and synchronize data in the MMS.**</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="6814f-108">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="6814f-108">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="6814f-109">Как правило эскиз рекомендуется использовать следующие инструкции высокого уровня для выполнения операций MMS CRUD.</span><span class="sxs-lookup"><span data-stu-id="6814f-109">As a rule of a thumb, we recommend the following high-level guidelines for performing MMS CRUD operations.</span></span>

- <span data-ttu-id="6814f-110">Должен быть реализован MMS операций с клиентской объектной модели.</span><span class="sxs-lookup"><span data-stu-id="6814f-110">MMS CRUD operations should be implemented with the client-side object model.</span></span>
- <span data-ttu-id="6814f-111">Выполнение кода CSOM с использованием учетной записи, имеющей соответствующие разрешения на выполнение операций MMS CRUD.</span><span class="sxs-lookup"><span data-stu-id="6814f-111">Execute the CSOM code with an account that has the appropriate permissions to perform MMS CRUD operations.</span></span>
- <span data-ttu-id="6814f-112">При синхронизации терминов, наборов использовать класс ChangeInformation, так как он работает лучше, чем использование GetAllTerms и перечисления условия каждый раз, которые необходимо синхронизировать.</span><span class="sxs-lookup"><span data-stu-id="6814f-112">When synchronizing term sets use the ChangeInformation class because it performs better than using GetAllTerms and enumerating the terms every time you want to sync.</span></span> 


<a name="options-to-copy-and-synchronize-mms-data"></a><span data-ttu-id="6814f-113">Параметры для копирования и синхронизации данных MMS</span><span class="sxs-lookup"><span data-stu-id="6814f-113">Options to copy and synchronize MMS data</span></span>
----------------------------------------

<span data-ttu-id="6814f-114">У вас есть две возможности для копирования и синхронизации данных MMS.</span><span class="sxs-lookup"><span data-stu-id="6814f-114">You have a couple of options to copy and synchronize MMS data.</span></span>

- <span data-ttu-id="6814f-115">Локальные</span><span class="sxs-lookup"><span data-stu-id="6814f-115">On-premises</span></span>
    + <span data-ttu-id="6814f-116">Копия базы данных</span><span class="sxs-lookup"><span data-stu-id="6814f-116">Copy database</span></span>
    + <span data-ttu-id="6814f-117">Использование CSOM для копирования данных</span><span class="sxs-lookup"><span data-stu-id="6814f-117">Use CSOM to copy data</span></span>
    + <span data-ttu-id="6814f-118">Использование CSOM для синхронизации данных</span><span class="sxs-lookup"><span data-stu-id="6814f-118">Use CSOM to sync data</span></span>
- <span data-ttu-id="6814f-119">Office 365</span><span class="sxs-lookup"><span data-stu-id="6814f-119">Office 365</span></span>
    + <span data-ttu-id="6814f-120">Использование CSOM для копирования данных</span><span class="sxs-lookup"><span data-stu-id="6814f-120">Use CSOM to copy data</span></span>
    + <span data-ttu-id="6814f-121">Использование CSOM для синхронизации данных</span><span class="sxs-lookup"><span data-stu-id="6814f-121">Use CSOM to sync data</span></span>

<a name="on-premises---copy-database"></a><span data-ttu-id="6814f-122">Локальные - копию базы данных</span><span class="sxs-lookup"><span data-stu-id="6814f-122">On-premises - copy database</span></span>
---------------------------
<span data-ttu-id="6814f-123">Если у вас есть в локальной среде SharePoint базы данных MMS можно скопировать из одной фермы в другую для быстро репликации термины.</span><span class="sxs-lookup"><span data-stu-id="6814f-123">If you have an on-premises SharePoint environment you can copy the MMS database from one farm to another to quickly replicate terms.</span></span>

<span data-ttu-id="6814f-124">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="6814f-124">**When is it a good fit?**</span></span>

<span data-ttu-id="6814f-125">Когда в локальной среде SharePoint и выполнении односторонней копию термины, это является хорошим выбором, так как он может быть реализован быстро и легко без какого-либо кода.</span><span class="sxs-lookup"><span data-stu-id="6814f-125">When you have an on-premises SharePoint environment and you are performing a one-way copy of terms, this is a good option because it may be implemented quickly and easily without writing any code.</span></span>

<a name="on-premises--o365---use-csom-to-copy-data"></a><span data-ttu-id="6814f-126">Локальные организации и O365 - CSOM используется для копирования данных</span><span class="sxs-lookup"><span data-stu-id="6814f-126">On-premises & O365 - Use CSOM to copy data</span></span>
------------------------------------------
<span data-ttu-id="6814f-127">Если у вас есть локальный или среду Office 365 SharePoint CSOM можно использовать для копирования данных MMS из одной фермы или клиента в другой.</span><span class="sxs-lookup"><span data-stu-id="6814f-127">If you have an on-premises or Office 365 SharePoint environment you can use CSOM to copy MMS data from one farm/tenancy to another.</span></span>  <span data-ttu-id="6814f-128">***Может включать локальные и Office 365 ферм при использовании этого подхода.***</span><span class="sxs-lookup"><span data-stu-id="6814f-128">***You can include both on-premises and Office 365 farms with this approach.***</span></span>

<span data-ttu-id="6814f-129">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="6814f-129">**When is it a good fit?**</span></span>

<span data-ttu-id="6814f-130">При наличии локального развертывания SharePoint или Office 365 или гибридной среды и выполняется копирование данных MMS между двумя или более ферм/участки SharePoint, это является хорошим выбором, поскольку он обеспечивает гибкость для копирования данных MMS из одной фермы.</span><span class="sxs-lookup"><span data-stu-id="6814f-130">When you have an on-premises SharePoint or Office 365 or a hybrid environment and you are copying MMS data between two or more SharePoint farms/tenancies, this is a good option because it gives you the flexibility to copy the MMS data from one farm to another.</span></span>

<span data-ttu-id="6814f-131">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="6814f-131">**Getting started**</span></span>

<span data-ttu-id="6814f-132">Следующий пример демонстрирует для выполнения операций MMS CRUD.</span><span class="sxs-lookup"><span data-stu-id="6814f-132">The following sample demonstrates how to perform MMS CRUD operations.</span></span>

- [<span data-ttu-id="6814f-133">Core.MMS (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="6814f-133">Core.MMS (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)

<a name="on-premises--o365---use-csom-to-sync-data"></a><span data-ttu-id="6814f-134">Локальные организации и O365 - CSOM используется для синхронизации данных</span><span class="sxs-lookup"><span data-stu-id="6814f-134">On-premises & O365 - Use CSOM to sync data</span></span>
------------------------------------------
<span data-ttu-id="6814f-135">При наличии в локальной среде SharePoint CSOM можно использовать для синхронизации данных MMS между фермами.</span><span class="sxs-lookup"><span data-stu-id="6814f-135">If you have an on-premises SharePoint environment you can use CSOM to sync MMS data between farms.</span></span> <span data-ttu-id="6814f-136">***Может включать локальные и Office 365 ферм/клиенты при использовании этого подхода.***</span><span class="sxs-lookup"><span data-stu-id="6814f-136">***You can include both on-premises and Office 365 farms/tenancies with this approach.***</span></span>

<span data-ttu-id="6814f-137">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="6814f-137">**When is it a good fit?**</span></span>

<span data-ttu-id="6814f-138">При наличии локального развертывания SharePoint или Office 365 или гибридной среды и выполняется синхронизация данных MMS между двумя или более ферм/участки SharePoint, это является хорошим выбором, поскольку он обеспечивает гибкость значение true, синхронизации и включив как Количество источников, как вы хотите.</span><span class="sxs-lookup"><span data-stu-id="6814f-138">When you have an on-premises SharePoint or Office 365 or a hybrid environment and you are synchronizing MMS data between two or more SharePoint farms/tenancies, this is a good option because it gives you the flexibility to perform true synchronization and include as many sources as you like.</span></span>

<span data-ttu-id="6814f-139">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="6814f-139">**Getting started**</span></span>

<span data-ttu-id="6814f-140">Следующий пример демонстрирует построение средства синхронизации данных MMS.</span><span class="sxs-lookup"><span data-stu-id="6814f-140">The following sample demonstrates how to build a synchronization tool for MMS data.</span></span>

- [<span data-ttu-id="6814f-141">Core.MMSSync (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="6814f-141">Core.MMSSync (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)

<a name="related-links"></a><span data-ttu-id="6814f-142">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="6814f-142">Related links</span></span>
=============
- [<span data-ttu-id="6814f-143">Синхронизация наборов терминов, с помощью CSOM (документация по статье блог MSDN)</span><span class="sxs-lookup"><span data-stu-id="6814f-143">Synchronize term sets using CSOM (MSDN Blog Article Documentation)</span></span>](http://blogs.msdn.com/b/frank_marasco/archive/2014/06/29/synchronize-term-sets-with-the-term-store-csom.aspx)
- <span data-ttu-id="6814f-144">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="6814f-144">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="6814f-145">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="6814f-145">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="6814f-146">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="6814f-146">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="6814f-147">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="6814f-147">Related PnP samples</span></span>
===================

- [<span data-ttu-id="6814f-148">Core.MMS (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="6814f-148">Core.MMS (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMS)
- [<span data-ttu-id="6814f-149">Core.MMSSync (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="6814f-149">Core.MMSSync (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.MMSSync)
- <span data-ttu-id="6814f-150">Примеры и содержимое в [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span><span class="sxs-lookup"><span data-stu-id="6814f-150">Samples and content at [https://github.com/SharePoint/PnP](https://github.com/SharePoint/PnP)</span></span>

<a name="applies-to"></a><span data-ttu-id="6814f-151">Применимо к</span><span class="sxs-lookup"><span data-stu-id="6814f-151">Applies to</span></span>
==========
- <span data-ttu-id="6814f-152">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="6814f-152">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="6814f-153">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="6814f-153">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="6814f-154">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="6814f-154">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="6814f-155">*Шаблоны для выделенных и в локальной, совпадают с помощью методов Add-in модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="6814f-155">*Patterns for dedicated and on-premises are identical with Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
