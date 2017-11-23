---
title: "Службы приложений Office 2013 и SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f962922c-2967-492f-9a89-5ad10a1a6dd3
ms.openlocfilehash: d976ee840824abe4a12e7cacc28b1cf46cb11c94
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="office-2013-and-sharepoint-application-services"></a><span data-ttu-id="52938-102">Службы приложений Office 2013 и SharePoint</span><span class="sxs-lookup"><span data-stu-id="52938-102">Office 2013 and SharePoint application services</span></span>
<span data-ttu-id="52938-103">Сведения о Службы Access, Службы Excel, Служба машинного перевода, Службы PerformancePoint Services, Службы автоматизации PowerPoint, Службы Visio и Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="52938-103">Learn about Access Services, Excel Services, Machine Translation Service, PerformancePoint Services, PowerPoint Automation Services, Visio Services, and Word Automation Services.</span></span>
## <a name="overview-and-usage-scenarios-for-office-and-sharepoint-services-in-sharepoint"></a><span data-ttu-id="52938-104">Общие сведения и сценарии использования служб Office и SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="52938-104">Overview and usage scenarios for Office and SharePoint services in SharePoint</span></span>
<span data-ttu-id="52938-105"><a name="bkmk_servicesOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="52938-105"></span></span>

<span data-ttu-id="52938-p101">Службы Office и SharePoint выполняются на серверах отдельных приложений в ферме и предоставляют широкий набор функций. Службы, описанные в этом разделе предоставляют функциональные возможности в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="52938-p101">Office and SharePoint services run on individual application servers in the farm and provide a wide range of functionality. The services that are described in this section provide functionality across the following scenarios:</span></span>
  
    
    

- <span data-ttu-id="52938-108">**Бизнес-аналитики (BI) и обмена мнениями** Включение поиска, анализа и обмена информацией об их работы или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="52938-108">**Business intelligence (BI) and Insights** enable people to find, analyze, and share information about their work or business.</span></span>
    
  
- <span data-ttu-id="52938-109">**Простого приложения** позволяют пользователям создание базового приложения, которые содержат надежного резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="52938-109">**Simple apps** let users create basic apps that contain a reliable backing store.</span></span>
    
  
- <span data-ttu-id="52938-110">**Преобразование файла** преобразует файлы Word и PowerPoint и потоков в других форматах.</span><span class="sxs-lookup"><span data-stu-id="52938-110">**File conversion** converts Word and PowerPoint files and streams to other formats.</span></span>
    
  
- <span data-ttu-id="52938-111">**Перевода** переводит сайты, документы и потоков для многоязыковой поддержки.</span><span class="sxs-lookup"><span data-stu-id="52938-111">**Translation** translates sites, documents, and streams for multilingual support.</span></span>
    
  
<span data-ttu-id="52938-112">В следующей таблице показаны сценариев высокого уровня, которые применяются к службам, описанных в данном разделе.</span><span class="sxs-lookup"><span data-stu-id="52938-112">The following table shows high-level scenarios that apply to the services described in this section.</span></span>
  
    
    

<span data-ttu-id="52938-113">**В таблице 1. Сценарии для Office и SharePoint services в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="52938-113">**Table 1. Scenarios for Office and SharePoint services in SharePoint**</span></span>


||<span data-ttu-id="52938-114">**Бизнес-Аналитики и обмена мнениями**</span><span class="sxs-lookup"><span data-stu-id="52938-114">**BI/Insights**</span></span>|<span data-ttu-id="52938-115">**Простого приложения**</span><span class="sxs-lookup"><span data-stu-id="52938-115">**Simple apps**</span></span>|<span data-ttu-id="52938-116">**Преобразование файла**</span><span class="sxs-lookup"><span data-stu-id="52938-116">**File conversion**</span></span>|<span data-ttu-id="52938-117">**Преобразование**</span><span class="sxs-lookup"><span data-stu-id="52938-117">**Translation**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="52938-118">Службы Access</span><span class="sxs-lookup"><span data-stu-id="52938-118">Access Services</span></span>  <br/> |<span data-ttu-id="52938-119">X</span><span class="sxs-lookup"><span data-stu-id="52938-119">X</span></span>  <br/> |<span data-ttu-id="52938-120">X</span><span class="sxs-lookup"><span data-stu-id="52938-120">X</span></span>  <br/> |||
|<span data-ttu-id="52938-121">Службы Excel</span><span class="sxs-lookup"><span data-stu-id="52938-121">Excel Services</span></span>  <br/> |<span data-ttu-id="52938-122">X</span><span class="sxs-lookup"><span data-stu-id="52938-122">X</span></span>  <br/> ||||
|<span data-ttu-id="52938-123">Служба машинного перевода</span><span class="sxs-lookup"><span data-stu-id="52938-123">Machine Translation Service</span></span>  <br/> ||||<span data-ttu-id="52938-124">X</span><span class="sxs-lookup"><span data-stu-id="52938-124">X</span></span>  <br/> |
|<span data-ttu-id="52938-125">Службы PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="52938-125">PerformancePoint Services</span></span>  <br/> |<span data-ttu-id="52938-126">X</span><span class="sxs-lookup"><span data-stu-id="52938-126">X</span></span>  <br/> ||||
|<span data-ttu-id="52938-127">Службы автоматизации PowerPoint</span><span class="sxs-lookup"><span data-stu-id="52938-127">PowerPoint Automation Services</span></span>  <br/> |||<span data-ttu-id="52938-128">X</span><span class="sxs-lookup"><span data-stu-id="52938-128">X</span></span>  <br/> ||
|<span data-ttu-id="52938-129">Службы Visio</span><span class="sxs-lookup"><span data-stu-id="52938-129">Visio Services</span></span>  <br/> |<span data-ttu-id="52938-130">X</span><span class="sxs-lookup"><span data-stu-id="52938-130">X</span></span>  <br/> ||||
|<span data-ttu-id="52938-131">Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="52938-131">Word Automation Services</span></span>  <br/> |||<span data-ttu-id="52938-132">X</span><span class="sxs-lookup"><span data-stu-id="52938-132">X</span></span>  <br/> ||
   

> <span data-ttu-id="52938-133">**Примечание:** Не все службы и сценарии, представленные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="52938-133">**Note:** Not all services and scenarios are represented in this section.</span></span> <span data-ttu-id="52938-134">Ссылки на документацию по разработке для других служб в разделе [Дополнительные ресурсы](#bkmk_Resources).</span><span class="sxs-lookup"><span data-stu-id="52938-134">For links to developer documentation for other services, see  [Additional resources](#bkmk_Resources).</span></span> 
  
    
    


## <a name="in-this-section"></a><span data-ttu-id="52938-135">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="52938-135">In this section</span></span>
<span data-ttu-id="52938-136"><a name="bkmk_inThisSection"> </a></span><span class="sxs-lookup"><span data-stu-id="52938-136"></span></span>

<span data-ttu-id="52938-137">Используйте ссылки в таблице 2 для получения дополнительных сведений о разработке с использованием служб Office и SharePoint, описанных в данном разделе: Службы Access, Службы Excel, Служба машинного перевода, Службы PerformancePoint Services, Службы автоматизации PowerPoint, Службы Visio и Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="52938-137">Use the links in Table 2 to learn more about developing with the Office and SharePoint services described in this section: Access Services, Excel Services, Machine Translation Service, PerformancePoint Services, PowerPoint Automation Services, Visio Services, and Word Automation Services.</span></span> 
  
    
    

<span data-ttu-id="52938-138">**В таблице 2. Обзор служб Office и SharePoint в этом разделе**</span><span class="sxs-lookup"><span data-stu-id="52938-138">**Table 2. Overview of Office and SharePoint services in this section**</span></span>


|<span data-ttu-id="52938-139">**Служба**</span><span class="sxs-lookup"><span data-stu-id="52938-139">**Service**</span></span>|<span data-ttu-id="52938-140">**Описание**</span><span class="sxs-lookup"><span data-stu-id="52938-140">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="52938-141">Службы Access</span><span class="sxs-lookup"><span data-stu-id="52938-141">Access Services</span></span>  <br/> <span data-ttu-id="52938-142">Просмотреть  [Разработка веб-приложений Access](develop-access-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="52938-142">See  [Develop Access web apps](develop-access-web-apps.md)</span></span> <br/> |<span data-ttu-id="52938-143">Позволяет пользователям создавать, развертывания и управления приложениями совместной работы на основе веб технологий Access.</span><span class="sxs-lookup"><span data-stu-id="52938-143">Enables users to create, deploy, and manage collaborative web-based Access applications.</span></span>  <br/> |
|<span data-ttu-id="52938-144">Службы Excel</span><span class="sxs-lookup"><span data-stu-id="52938-144">Excel Services</span></span>  <br/> <span data-ttu-id="52938-145">Просмотреть [служб Excel в SharePoint](excel-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="52938-145">See  [Excel Services in SharePoint](excel-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="52938-146">Позволяет пользователям загружать, вычисление и отображение книг Excel на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="52938-146">Enables users to load, calculate, and display Excel workbooks on SharePoint sites.</span></span>  <br/> |
|<span data-ttu-id="52938-147">Служба машинного перевода</span><span class="sxs-lookup"><span data-stu-id="52938-147">Machine Translation Service</span></span>  <br/> <span data-ttu-id="52938-148">Просмотреть [службы машинного перевода в SharePoint](machine-translation-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="52938-148">See  [Machine Translation Services in SharePoint](machine-translation-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="52938-149">Обеспечивает автоматическую машинного перевода сайтов, документов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="52938-149">Provides automatic machine translation of sites, documents, and sites.</span></span>  <br/> |
|<span data-ttu-id="52938-150">Службы PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="52938-150">PerformancePoint Services</span></span>  <br/> <span data-ttu-id="52938-151">Просмотреть [PerformancePoint Services в SharePoint](performancepoint-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="52938-151">See  [PerformancePoint Services in SharePoint](performancepoint-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="52938-152">Создает и публикует панелей мониторинга, которые содержат визуализации интерактивных данных (например, систем показателей и reports.md), которые позволяют людей для мониторинга и анализа производительности их бизнеса.</span><span class="sxs-lookup"><span data-stu-id="52938-152">Creates and publishes dashboards that contain interactive data visualizations (such as scorecards and reports.md) that enable people to monitor and analyze their business performance.</span></span>  <br/> |
|<span data-ttu-id="52938-153">Службы автоматизации PowerPoint</span><span class="sxs-lookup"><span data-stu-id="52938-153">PowerPoint Automation Services</span></span>  <br/>  [<span data-ttu-id="52938-154">PowerPoint Automation Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="52938-154">PowerPoint Automation Services in SharePoint</span></span>](powerpoint-automation-services-in-sharepoint.md) <br/> |<span data-ttu-id="52938-155">Предоставляет выполнять на сервере преобразование PowerPoint презентаций в других форматах.</span><span class="sxs-lookup"><span data-stu-id="52938-155">Provides unattended, server-side conversion of PowerPoint presentations into other formats.</span></span>  <br/> |
|<span data-ttu-id="52938-156">Службы Visio</span><span class="sxs-lookup"><span data-stu-id="52938-156">Visio Services</span></span>  <br/> <span data-ttu-id="52938-157">Просмотреть [служб Visio в SharePoint](visio-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="52938-157">See  [Visio Services in SharePoint](visio-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="52938-158">Позволяет пользователям работать с рисунки Visio, хранящихся на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="52938-158">Enables users to view and interact with Visio drawings stored on SharePoint sites.</span></span>  <br/> |
|<span data-ttu-id="52938-159">Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="52938-159">Word Automation Services</span></span>  <br/> <span data-ttu-id="52938-160">Просмотреть  [Новые возможности Word Automation Services для разработчиков (en)](what-s-new-in-word-automation-services-for-developers.md)</span><span class="sxs-lookup"><span data-stu-id="52938-160">See  [What's new in Word Automation Services for developers](what-s-new-in-word-automation-services-for-developers.md)</span></span> <br/> |<span data-ttu-id="52938-161">Предоставляет выполнять на сервере преобразование документов, поддерживаемых приложением Word.</span><span class="sxs-lookup"><span data-stu-id="52938-161">Provides unattended, server-side conversion of documents that are supported by Word.</span></span>  <br/> |
   
<span data-ttu-id="52938-p103">Не все службы и сценарии, представленные в этом разделе. Ссылки на документацию по разработке для других служб в разделе  [Дополнительные ресурсы](#bkmk_Resources).</span><span class="sxs-lookup"><span data-stu-id="52938-p103">Not all services and scenarios are represented in this section. For links to developer documentation for other services, see  [Additional resources](#bkmk_Resources).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="52938-164">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="52938-164">Additional resources</span></span>
<span data-ttu-id="52938-165"><a name="bkmk_Resources"> </a></span><span class="sxs-lookup"><span data-stu-id="52938-165"></span></span>


-  [<span data-ttu-id="52938-166">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="52938-166">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="52938-167">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="52938-167">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="52938-168">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="52938-168">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="52938-169">Установка компонентов бизнес-Аналитики SQL Server с помощью SharePoint (PowerPivot и служб отчетов)</span><span class="sxs-lookup"><span data-stu-id="52938-169">Install SQL Server BI Features with SharePoint (PowerPivot and Reporting Services)</span></span>](http://msdn.microsoft.com/ru-ru/library/hh231671)
    
  

