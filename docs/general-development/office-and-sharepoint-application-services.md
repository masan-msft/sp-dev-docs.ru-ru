---
title: "Службы приложений Office 2013 и SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f962922c-2967-492f-9a89-5ad10a1a6dd3
ms.openlocfilehash: e649ad7e40cada921cbee105d69668bf0633cc6f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="office-2013-and-sharepoint-application-services"></a><span data-ttu-id="02ef5-102">Службы приложений Office 2013 и SharePoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-102">Office 2013 and SharePoint application services</span></span>
<span data-ttu-id="02ef5-103">Сведения о Службы Access, Службы Excel, Служба машинного перевода, Службы PerformancePoint Services, Службы автоматизации PowerPoint, Службы Visio и Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="02ef5-103">Learn about Access Services, Excel Services, Machine Translation Service, PerformancePoint Services, PowerPoint Automation Services, Visio Services, and Word Automation Services.</span></span>
## <a name="overview-and-usage-scenarios-for-office-and-sharepoint-services-in-sharepoint"></a><span data-ttu-id="02ef5-104">Общие сведения и сценарии использования служб Office и SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-104">Overview and usage scenarios for Office and SharePoint services in SharePoint</span></span>
<span data-ttu-id="02ef5-105"><a name="bkmk_servicesOverview"> </a></span><span class="sxs-lookup"><span data-stu-id="02ef5-105"></span></span>

<span data-ttu-id="02ef5-p101">Службы Office и SharePoint выполняются на серверах отдельных приложений в ферме и предоставляют широкий набор функций. Службы, описанные в этом разделе предоставляют функциональные возможности в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="02ef5-p101">Office and SharePoint services run on individual application servers in the farm and provide a wide range of functionality. The services that are described in this section provide functionality across the following scenarios:</span></span>
  
    
    

- <span data-ttu-id="02ef5-108">**Бизнес-аналитики (BI) и обмена мнениями** Включение поиска, анализа и обмена информацией об их работы или бизнеса.</span><span class="sxs-lookup"><span data-stu-id="02ef5-108">**Business intelligence (BI) and Insights** enable people to find, analyze, and share information about their work or business.</span></span>
    
  
- <span data-ttu-id="02ef5-109">**Простого приложения** позволяют пользователям создание базового приложения, которые содержат надежного резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="02ef5-109">**Simple apps** let users create basic apps that contain a reliable backing store.</span></span>
    
  
- <span data-ttu-id="02ef5-110">**Преобразование файла** преобразует файлы Word и PowerPoint и потоков в других форматах.</span><span class="sxs-lookup"><span data-stu-id="02ef5-110">**File conversion** converts Word and PowerPoint files and streams to other formats.</span></span>
    
  
- <span data-ttu-id="02ef5-111">**Перевода** переводит сайты, документы и потоков для многоязыковой поддержки.</span><span class="sxs-lookup"><span data-stu-id="02ef5-111">**Translation** translates sites, documents, and streams for multilingual support.</span></span>
    
  
<span data-ttu-id="02ef5-112">В следующей таблице показаны сценариев высокого уровня, которые применяются к службам, описанных в данном разделе.</span><span class="sxs-lookup"><span data-stu-id="02ef5-112">The following table shows high-level scenarios that apply to the services described in this section.</span></span>
  
    
    

<span data-ttu-id="02ef5-113">**В таблице 1. Сценарии для Office и SharePoint services в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="02ef5-113">**Table 1. Scenarios for Office and SharePoint services in SharePoint**</span></span>


||<span data-ttu-id="02ef5-114">**Бизнес-Аналитики и обмена мнениями**</span><span class="sxs-lookup"><span data-stu-id="02ef5-114">**BI/Insights**</span></span>|<span data-ttu-id="02ef5-115">**Простого приложения**</span><span class="sxs-lookup"><span data-stu-id="02ef5-115">**Simple apps**</span></span>|<span data-ttu-id="02ef5-116">**Преобразование файла**</span><span class="sxs-lookup"><span data-stu-id="02ef5-116">**File conversion**</span></span>|<span data-ttu-id="02ef5-117">**Преобразование**</span><span class="sxs-lookup"><span data-stu-id="02ef5-117">**Translation**</span></span>|
|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="02ef5-118">Службы Access</span><span class="sxs-lookup"><span data-stu-id="02ef5-118">Access Services</span></span>  <br/> |<span data-ttu-id="02ef5-119">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-119">X</span></span>  <br/> |<span data-ttu-id="02ef5-120">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-120">X</span></span>  <br/> |||
|<span data-ttu-id="02ef5-121">Службы Excel</span><span class="sxs-lookup"><span data-stu-id="02ef5-121">Excel Services</span></span>  <br/> |<span data-ttu-id="02ef5-122">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-122">X</span></span>  <br/> ||||
|<span data-ttu-id="02ef5-123">Служба машинного перевода</span><span class="sxs-lookup"><span data-stu-id="02ef5-123">Machine Translation Service</span></span>  <br/> ||||<span data-ttu-id="02ef5-124">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-124">X</span></span>  <br/> |
|<span data-ttu-id="02ef5-125">Службы PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="02ef5-125">PerformancePoint Services</span></span>  <br/> |<span data-ttu-id="02ef5-126">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-126">X</span></span>  <br/> ||||
|<span data-ttu-id="02ef5-127">Службы автоматизации PowerPoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-127">PowerPoint Automation Services</span></span>  <br/> |||<span data-ttu-id="02ef5-128">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-128">X</span></span>  <br/> ||
|<span data-ttu-id="02ef5-129">Службы Visio</span><span class="sxs-lookup"><span data-stu-id="02ef5-129">Visio Services</span></span>  <br/> |<span data-ttu-id="02ef5-130">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-130">X</span></span>  <br/> ||||
|<span data-ttu-id="02ef5-131">Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="02ef5-131">Word Automation Services</span></span>  <br/> |||<span data-ttu-id="02ef5-132">X</span><span class="sxs-lookup"><span data-stu-id="02ef5-132">X</span></span>  <br/> ||
   

> [!NOTE]
> <span data-ttu-id="02ef5-p102">[!Примечание] Не все службы и сценарии, представленные в этом разделе. Ссылки на документацию по разработке для других служб в разделе  [Дополнительные ресурсы](#bkmk_Resources).</span><span class="sxs-lookup"><span data-stu-id="02ef5-p102">Not all services and scenarios are represented in this section. For links to developer documentation for other services, see  [Additional resources](#bkmk_Resources).</span></span> 
  
    
    


## <a name="in-this-section"></a><span data-ttu-id="02ef5-135">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="02ef5-135">In this section</span></span>
<span data-ttu-id="02ef5-136"><a name="bkmk_inThisSection"> </a></span><span class="sxs-lookup"><span data-stu-id="02ef5-136"></span></span>

<span data-ttu-id="02ef5-137">Используйте ссылки в таблице 2 для получения дополнительных сведений о разработке с использованием служб Office и SharePoint, описанных в данном разделе: Службы Access, Службы Excel, Служба машинного перевода, Службы PerformancePoint Services, Службы автоматизации PowerPoint, Службы Visio и Word Automation Services.</span><span class="sxs-lookup"><span data-stu-id="02ef5-137">Use the links in Table 2 to learn more about developing with the Office and SharePoint services described in this section: Access Services, Excel Services, Machine Translation Service, PerformancePoint Services, PowerPoint Automation Services, Visio Services, and Word Automation Services.</span></span> 
  
    
    

<span data-ttu-id="02ef5-138">**В таблице 2. Обзор служб Office и SharePoint в этом разделе**</span><span class="sxs-lookup"><span data-stu-id="02ef5-138">**Table 2. Overview of Office and SharePoint services in this section**</span></span>


|<span data-ttu-id="02ef5-139">**Служба**</span><span class="sxs-lookup"><span data-stu-id="02ef5-139">**Service**</span></span>|<span data-ttu-id="02ef5-140">**Описание**</span><span class="sxs-lookup"><span data-stu-id="02ef5-140">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="02ef5-141">Службы Access</span><span class="sxs-lookup"><span data-stu-id="02ef5-141">Access Services</span></span>  <br/> <span data-ttu-id="02ef5-142">Просмотреть  [Разработка веб-приложений Access](develop-access-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="02ef5-142">See  [Develop Access web apps](develop-access-web-apps.md)</span></span> <br/> |<span data-ttu-id="02ef5-143">Позволяет пользователям создавать, развертывания и управления приложениями совместной работы на основе веб технологий Access.</span><span class="sxs-lookup"><span data-stu-id="02ef5-143">Enables users to create, deploy, and manage collaborative web-based Access applications.</span></span>  <br/> |
|<span data-ttu-id="02ef5-144">Службы Excel</span><span class="sxs-lookup"><span data-stu-id="02ef5-144">Excel Services</span></span>  <br/> <span data-ttu-id="02ef5-145">Просмотреть [служб Excel в SharePoint](excel-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="02ef5-145">See  [Excel Services in SharePoint](excel-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="02ef5-146">Позволяет пользователям загружать, вычисление и отображение книг Excel на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="02ef5-146">Enables users to load, calculate, and display Excel workbooks on SharePoint sites.</span></span>  <br/> |
|<span data-ttu-id="02ef5-147">Служба машинного перевода</span><span class="sxs-lookup"><span data-stu-id="02ef5-147">Machine Translation Service</span></span>  <br/> <span data-ttu-id="02ef5-148">Просмотреть [службы машинного перевода в SharePoint](machine-translation-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="02ef5-148">See  [Machine Translation Services in SharePoint](machine-translation-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="02ef5-149">Обеспечивает автоматическую машинного перевода сайтов, документов и сайтов.</span><span class="sxs-lookup"><span data-stu-id="02ef5-149">Provides automatic machine translation of sites, documents, and sites.</span></span>  <br/> |
|<span data-ttu-id="02ef5-150">Службы PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="02ef5-150">PerformancePoint Services</span></span>  <br/> <span data-ttu-id="02ef5-151">Просмотреть [PerformancePoint Services в SharePoint](performancepoint-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="02ef5-151">See  [PerformancePoint Services in SharePoint](performancepoint-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="02ef5-152">Создает и публикует панелей мониторинга, которые содержат визуализации интерактивных данных (например, систем показателей и reports.md), которые позволяют людей для мониторинга и анализа производительности их бизнеса.</span><span class="sxs-lookup"><span data-stu-id="02ef5-152">Creates and publishes dashboards that contain interactive data visualizations (such as scorecards and reports.md) that enable people to monitor and analyze their business performance.</span></span>  <br/> |
|<span data-ttu-id="02ef5-153">Службы автоматизации PowerPoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-153">PowerPoint Automation Services</span></span>  <br/>  [<span data-ttu-id="02ef5-154">PowerPoint Automation Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-154">PowerPoint Automation Services in SharePoint</span></span>](powerpoint-automation-services-in-sharepoint.md) <br/> |<span data-ttu-id="02ef5-155">Предоставляет выполнять на сервере преобразование PowerPoint презентаций в других форматах.</span><span class="sxs-lookup"><span data-stu-id="02ef5-155">Provides unattended, server-side conversion of PowerPoint presentations into other formats.</span></span>  <br/> |
|<span data-ttu-id="02ef5-156">Службы Visio</span><span class="sxs-lookup"><span data-stu-id="02ef5-156">Visio Services</span></span>  <br/> <span data-ttu-id="02ef5-157">Просмотреть [служб Visio в SharePoint](visio-services-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="02ef5-157">See  [Visio Services in SharePoint](visio-services-in-sharepoint.md)</span></span> <br/> |<span data-ttu-id="02ef5-158">Позволяет пользователям работать с рисунки Visio, хранящихся на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="02ef5-158">Enables users to view and interact with Visio drawings stored on SharePoint sites.</span></span>  <br/> |
|<span data-ttu-id="02ef5-159">Word Automation Services</span><span class="sxs-lookup"><span data-stu-id="02ef5-159">Word Automation Services</span></span>  <br/> <span data-ttu-id="02ef5-160">Просмотреть  [Новые возможности Word Automation Services для разработчиков (en)](what-s-new-in-word-automation-services-for-developers.md)</span><span class="sxs-lookup"><span data-stu-id="02ef5-160">See  [What's new in Word Automation Services for developers](what-s-new-in-word-automation-services-for-developers.md)</span></span> <br/> |<span data-ttu-id="02ef5-161">Предоставляет выполнять на сервере преобразование документов, поддерживаемых приложением Word.</span><span class="sxs-lookup"><span data-stu-id="02ef5-161">Provides unattended, server-side conversion of documents that are supported by Word.</span></span>  <br/> |
   
<span data-ttu-id="02ef5-p103">Не все службы и сценарии, представленные в этом разделе. Ссылки на документацию по разработке для других служб в разделе  [Дополнительные ресурсы](#bkmk_Resources).</span><span class="sxs-lookup"><span data-stu-id="02ef5-p103">Not all services and scenarios are represented in this section. For links to developer documentation for other services, see  [Additional resources](#bkmk_Resources).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="02ef5-164">См. также</span><span class="sxs-lookup"><span data-stu-id="02ef5-164">See also</span></span>
<span data-ttu-id="02ef5-165"><a name="bkmk_Resources"> </a></span><span class="sxs-lookup"><span data-stu-id="02ef5-165"></span></span>


-  [<span data-ttu-id="02ef5-166">Добавление возможностей SharePoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-166">Add SharePoint capabilities</span></span>](add-sharepoint-capabilities.md)
    
  
-  [<span data-ttu-id="02ef5-167">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-167">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="02ef5-168">Поиск в SharePoint</span><span class="sxs-lookup"><span data-stu-id="02ef5-168">Search in SharePoint</span></span>](search-in-sharepoint.md)
    
  
-  [<span data-ttu-id="02ef5-169">Установка компонентов бизнес-Аналитики SQL Server с помощью SharePoint (PowerPivot и служб отчетов)</span><span class="sxs-lookup"><span data-stu-id="02ef5-169">Install SQL Server BI Features with SharePoint (PowerPivot and Reporting Services)</span></span>](http://msdn.microsoft.com/en-us/library/hh231671)
    
  

