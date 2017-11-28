---
title: "Определение списка, аудио- и шаблон в объектная модель SharePoint списка"
ms.date: 11/03/2017
ms.openlocfilehash: c4a412493d0cc1768aa103b06cd98e189479d317
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="list-definition--list-template-in-the-sharepoint-add-in-model"></a><span data-ttu-id="506a7-102">Определение списка, аудио- и шаблон в объектная модель SharePoint списка</span><span class="sxs-lookup"><span data-stu-id="506a7-102">List definition / list template in the SharePoint add-in model</span></span>
==============================================================

<a name="summary"></a><span data-ttu-id="506a7-103">Summary</span><span class="sxs-lookup"><span data-stu-id="506a7-103">Summary</span></span>
-------

<span data-ttu-id="506a7-104">Подход, необходимые для создания определения списков и шаблонов списков отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="506a7-104">The approach you take to create list definitions / list templates is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="506a7-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, определений настраиваемых списков аудио- и шаблонов списков были созданы с помощью декларативного кода и развернуты через решений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="506a7-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, custom list definitions / list templates were created with declarative code and deployed via SharePoint Solutions.</span></span> 

<span data-ttu-id="506a7-106">В SharePoint надстройки модели сценарии одно для фактического Создание определений настраиваемых списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-106">In a SharePoint Add-in model scenario, one cannot actually create custom list definitions.</span></span>  <span data-ttu-id="506a7-107">Это просто невозможно сделать это.</span><span class="sxs-lookup"><span data-stu-id="506a7-107">It is simply impossible to do this.</span></span>  <span data-ttu-id="506a7-108">Тем не менее удаленных подготовки шаблон может быть использован для развертывания настраиваемых шаблонов списков (STP-файлы) в Office 365.</span><span class="sxs-lookup"><span data-stu-id="506a7-108">However, the remote provisioning pattern may used to deploy custom list templates (.stp files) to Office 365.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="506a7-109">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="506a7-109">High Level Guidelines</span></span>
---------------------

<span data-ttu-id="506a7-110">Как правило эскиз мы предлагаем для обеспечения высокого уровня следующее для реализации определений списков и шаблонов списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-110">As a rule of a thumb, we would like to provide the following high level guidelines to implement list definitions / list templates.</span></span>

- <span data-ttu-id="506a7-111">Шаблон удаленного подготовки к развертыванию шаблонов списков (STP-файлы) для сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="506a7-111">Use the remote provisioning pattern to deploy list templates (.stp files) to SharePoint sites.</span></span>
- <span data-ttu-id="506a7-112">Можно переопределить ожидания поведение создания списка поля для применения стандартных параметров для всех списков, созданных на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="506a7-112">You can override the out of the box list creation behavior to apply standardized settings to all lists created in a SharePoint site.</span></span>  <span data-ttu-id="506a7-113">Просмотрите Дополнительные сведения о такой подход ниже.</span><span class="sxs-lookup"><span data-stu-id="506a7-113">See more details about this approach below.</span></span>
- <span data-ttu-id="506a7-114">Можно создать надстройки SharePoint для создания списков с помощью стандартных параметров.</span><span class="sxs-lookup"><span data-stu-id="506a7-114">You can create a SharePoint Add-in to create lists with standardized settings.</span></span> <span data-ttu-id="506a7-115">Просмотрите Дополнительные сведения о такой подход ниже.</span><span class="sxs-lookup"><span data-stu-id="506a7-115">See more details about this approach below.</span></span>

<a name="options-to-ensure-standardized-settings-templates-are-applied-to-sharepoint-lists-upon-list-creation"></a><span data-ttu-id="506a7-116">Параметры для обеспечения стандартных параметров (шаблоны), применяются к спискам SharePoint после создания списка</span><span class="sxs-lookup"><span data-stu-id="506a7-116">Options to ensure standardized settings (templates) are applied to SharePoint lists upon list creation</span></span>
------------------------------------------------------------------------------------------------------

<span data-ttu-id="506a7-117">У вас есть две возможности для обеспечения стандартизованной (шаблоны) применяются к спискам SharePoint после создания списка.</span><span class="sxs-lookup"><span data-stu-id="506a7-117">You have a couple of options to ensure standardized settings (templates) are applied to SharePoint lists upon list creation.</span></span>

- <span data-ttu-id="506a7-118">Переопределите ожидания поведение создания поля списка.</span><span class="sxs-lookup"><span data-stu-id="506a7-118">Override the out of the box list creation behavior.</span></span>   
- <span data-ttu-id="506a7-119">Создание надстройки с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="506a7-119">Create a SharePoint Add-in.</span></span> 

<a name="override-the-out-of-the-box-list-creation-behavior"></a><span data-ttu-id="506a7-120">Переопределите ожидания поведение создания поля списка</span><span class="sxs-lookup"><span data-stu-id="506a7-120">Override the out of the box list creation behavior</span></span>
--------------------------------------------------
<span data-ttu-id="506a7-121">В этом шаблоне изменение ожидания поведение создания списка поле путем добавления приемника событий для события ListAdded.</span><span class="sxs-lookup"><span data-stu-id="506a7-121">In this pattern you modify the out of the box list creation behavior by adding an event receiver to the ListAdded event.</span></span>  <span data-ttu-id="506a7-122">Затем в случае приемника настроены для ListAdded события удаленного подготовки шаблон используется для применения стандартных настроек для каждого списка, которая создается.</span><span class="sxs-lookup"><span data-stu-id="506a7-122">Then, in the event receiver configured for the ListAdded event you use the remote provisioning pattern to apply standardized configurations to each list that is created.</span></span>

<span data-ttu-id="506a7-123">Эти стандартизованной конфигурации могут включать добавление типов контента, параметру типа контента по умолчанию, добавление столбцов списка, задание параметров version и другие списка тип конфигурации, которые могут быть установлены.</span><span class="sxs-lookup"><span data-stu-id="506a7-123">These standardized configurations may include adding content types, setting the default content type, adding list columns, setting the version settings, and any other list type configurations that may be set.</span></span> 
    
- <span data-ttu-id="506a7-124">Такой подход позволяет применять стандартизированные параметры для всех списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-124">This approach allows you to apply standardized settings for all lists.</span></span>
- <span data-ttu-id="506a7-125">Такой подход позволяет применять стандартизированные параметры для различных типов списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-125">This approach allows you to apply standardized settings to different types of lists.</span></span>
    + <span data-ttu-id="506a7-126">Например: Если создайте библиотеку документов и список задач, который можно определить в приемнике событий ListAdded, какой тип списка вы создали и можно применять различные стандартизированные параметры на основе типа списка.</span><span class="sxs-lookup"><span data-stu-id="506a7-126">For example: If you create a document library and a tasks list you can determine in the ListAdded event receiver which type of list you created and you can apply different standardized settings based on the list type.</span></span>  <span data-ttu-id="506a7-127">Возможно всех библиотек документов должны один набор типов контента, примененных к ним, пока все список задач требуется другой набор типов контента, примененных к ним.</span><span class="sxs-lookup"><span data-stu-id="506a7-127">Perhaps all document libraries need one set of content types applied to them, while all tasks list need a different set of content types applied to them.</span></span>
- <span data-ttu-id="506a7-128">Такой подход не поддерживает различные варианты другой шаблон для применения к спискам.</span><span class="sxs-lookup"><span data-stu-id="506a7-128">This approach does not support applying multiple different template options to lists.</span></span>
    + <span data-ttu-id="506a7-129">Например: Если создайте библиотеку документов и список задач, который можно определить в приемнике событий ListAdded, какой тип списка вы создали и можно применять различные стандартизированные параметры на основе типа списка.</span><span class="sxs-lookup"><span data-stu-id="506a7-129">For example: If you create a document library and a tasks list you can determine in the ListAdded event receiver which type of list you created and you can apply different standardized settings based on the list type.</span></span>  <span data-ttu-id="506a7-130">Тем не менее не могут применять различные шаблоны одну библиотеку документов, создаваемых и другая библиотека документов, которые можно создать.</span><span class="sxs-lookup"><span data-stu-id="506a7-130">However, you cannot apply different templates to one document library you create versus another document library you create.</span></span>

<span data-ttu-id="506a7-131">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="506a7-131">**When is it a good fit?**</span></span>

<span data-ttu-id="506a7-132">Когда следует применять в качестве стандарта глобальные параметры для всех списков или списков определенного типа.</span><span class="sxs-lookup"><span data-stu-id="506a7-132">When you need to apply standardized global settings to all lists or lists of a specific type.</span></span>

<span data-ttu-id="506a7-133">**Если это не подходит?**</span><span class="sxs-lookup"><span data-stu-id="506a7-133">**When is it a not good fit?**</span></span>

<span data-ttu-id="506a7-134">Когда следует применять различные варианты различные шаблоны списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-134">When you need to apply multiple different templates options to lists.</span></span>

<span data-ttu-id="506a7-135">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="506a7-135">**Getting Started**</span></span>

<span data-ttu-id="506a7-136">Следующие надстройки SharePoint модель набора команд описан процесс внедрения приемников событий.</span><span class="sxs-lookup"><span data-stu-id="506a7-136">The following SharePoint Add-in model recipe describes how to implement event receivers.</span></span>

- [<span data-ttu-id="506a7-137">Приемники событий (добавить в SharePoint модель набора команд)</span><span class="sxs-lookup"><span data-stu-id="506a7-137">Event Receivers (SharePoint Add-in model recipe)</span></span>](event-receiver-and-list-event-receiver-sharepoint-add-in.md)

<a name="create-a-sharepoint-add-in"></a><span data-ttu-id="506a7-138">Создание надстройки с SharePoint</span><span class="sxs-lookup"><span data-stu-id="506a7-138">Create a SharePoint Add-in</span></span>
--------------------------

<span data-ttu-id="506a7-139">В этом шаблоне создание надстройки SharePoint для создания списков с помощью стандартных параметров и информировать пользователей для использования надстройки SharePoint для создания новых списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-139">In this pattern you create a SharePoint Add-in to create lists with standardized settings and instruct your users to use the SharePoint Add-in to create new lists.</span></span>  <span data-ttu-id="506a7-140">По сути надстройки SharePoint предоставляет пользователям с вариантами выбора разных списков для создания.</span><span class="sxs-lookup"><span data-stu-id="506a7-140">Essentially, the SharePoint Add-in provides users with choices of different lists to create.</span></span>  <span data-ttu-id="506a7-141">Надстройки SharePoint позволяет пользователям создавать списки для различных определяются в бизнес и реализован разработчиком.</span><span class="sxs-lookup"><span data-stu-id="506a7-141">The different lists the SharePoint Add-in allows users to create are defined by the business and implemented by a developer.</span></span> <span data-ttu-id="506a7-142">Заполнении формы в SharePoint надстройки для указания метаданных списка и выберите предоставляет список для создания из параметров надстройки.</span><span class="sxs-lookup"><span data-stu-id="506a7-142">Users fill out a form in the SharePoint Add-in to specify the list meta-data and choose which list to create from the choices the Add-in offers.</span></span> <span data-ttu-id="506a7-143">Add-in удаленного подготовки шаблон используется для создания списка соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="506a7-143">The Add-in uses the remote provisioning pattern to create the list accordingly.</span></span>
    
- <span data-ttu-id="506a7-144">Такой подход позволяет применять стандартизированные параметры для всех списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-144">This approach allows you to apply standardized settings for all lists.</span></span>
- <span data-ttu-id="506a7-145">Такой подход позволяет применять стандартизированные параметры для различных типов списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-145">This approach allows you to apply standardized settings to different types of lists.</span></span>
- <span data-ttu-id="506a7-146">Такой подход позволяет применять различные варианты другой шаблон для списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-146">This approach allows you to apply multiple different template options to lists.</span></span>

<span data-ttu-id="506a7-147">**Когда это подходит?**</span><span class="sxs-lookup"><span data-stu-id="506a7-147">**When is it a good fit?**</span></span>

<span data-ttu-id="506a7-148">Когда следует применять различные варианты различные шаблоны списков.</span><span class="sxs-lookup"><span data-stu-id="506a7-148">When you need to apply multiple different templates options to lists.</span></span>

<span data-ttu-id="506a7-149">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="506a7-149">**Getting Started**</span></span>

<span data-ttu-id="506a7-150">Следующий пример кода PnP O365 и видео показано, как создать надстройки SharePoint, который предоставляет пользовательский интерфейс, который позволяет конечным пользователям создавать новые библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="506a7-150">The following O365 PnP Code Sample and video demonstrates how to create a SharePoint Add-in that provides a user interface that allows end users to create new document libraries.</span></span>  <span data-ttu-id="506a7-151">Также демонстрируется создание библиотеки документов с определенным конфигурации, которые совместно представляют шаблона.</span><span class="sxs-lookup"><span data-stu-id="506a7-151">It also demonstrates how to create a document library with specific configurations that collectively represent a template.</span></span>

- [<span data-ttu-id="506a7-152">ECM. DocumentLibraries (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="506a7-152">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)

<span data-ttu-id="506a7-153">Следующем видеоролике описывается пример кода.</span><span class="sxs-lookup"><span data-stu-id="506a7-153">The following video walks through the code sample.</span></span>

- [<span data-ttu-id="506a7-154">Шаблоны документов и списков с моделью приложений (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="506a7-154">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)

<a name="related-links"></a><span data-ttu-id="506a7-155">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="506a7-155">Related links</span></span>
=============

- [<span data-ttu-id="506a7-156">Экземпляр списка (добавить в SharePoint модель набора команд)</span><span class="sxs-lookup"><span data-stu-id="506a7-156">List Instance (SharePoint Add-in model recipe)</span></span>](list-instance-sharepoint-add-in.md)
- [<span data-ttu-id="506a7-157">Приемники событий (добавить в SharePoint модель набора команд)</span><span class="sxs-lookup"><span data-stu-id="506a7-157">Event Receivers (SharePoint Add-in model recipe)</span></span>](event-receiver-and-list-event-receiver-sharepoint-add-in.md)
- [<span data-ttu-id="506a7-158">Шаблоны документов и списков с моделью приложений (O365 PnP видео)</span><span class="sxs-lookup"><span data-stu-id="506a7-158">Document and list templates with app model (O365 PnP Video)</span></span>](http://channel9.msdn.com/blogs/OfficeDevPnP/Document-and-list-templates-with-app-model)
- <span data-ttu-id="506a7-159">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="506a7-159">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="506a7-160">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="506a7-160">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="506a7-161">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="506a7-161">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="506a7-162">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="506a7-162">Related PnP samples</span></span>
===================

- [<span data-ttu-id="506a7-163">ECM. DocumentLibraries (образец кода PnP O365)</span><span class="sxs-lookup"><span data-stu-id="506a7-163">ECM.DocumentLibraries (O365 PnP Code Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/ECM.DocumentLibraries)
- <span data-ttu-id="506a7-164">Примеры и содержимое в https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="506a7-164">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="506a7-165">Применимо к</span><span class="sxs-lookup"><span data-stu-id="506a7-165">Applies to</span></span>
==========
- <span data-ttu-id="506a7-166">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="506a7-166">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="506a7-167">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="506a7-167">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="506a7-168">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="506a7-168">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="506a7-169">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="506a7-169">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
