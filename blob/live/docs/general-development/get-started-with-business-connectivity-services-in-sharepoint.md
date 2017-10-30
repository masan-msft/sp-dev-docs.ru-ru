---
title: "Начало работы с Business Connectivity Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6bf3db0-db79-4b13-9834-891d24b2c9e5
ms.openlocfilehash: 71ff8cc2b13f8fc6dd9d65eab41cb2743d713f4f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-business-connectivity-services-in-sharepoint"></a><span data-ttu-id="cc808-102">Начало работы с Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-102">Get started with Business Connectivity Services in SharePoint</span></span>
<span data-ttu-id="cc808-103">Основные сведения о Business Connectivity Services (BCS) предоставляет разработчикам решений SharePoint, а также как приступить к работе с помощью службы BCS в различных типов решений.</span><span class="sxs-lookup"><span data-stu-id="cc808-103">Learn the basics of what Business Connectivity Services (BCS) provides to developers of SharePoint solutions, along with how to get started using BCS in various types of solutions.</span></span>
## <a name="what-is-business-connectivity-services"></a><span data-ttu-id="cc808-104">Что представляют собой Business Connectivity Services?</span><span class="sxs-lookup"><span data-stu-id="cc808-104">What is Business Connectivity Services?</span></span>

<span data-ttu-id="cc808-105">Business Connectivity Services (BCS) была введена в SharePoint Server 2010 как развитием каталога бизнес-данных, выпущенные в Office SharePoint Server 2007.</span><span class="sxs-lookup"><span data-stu-id="cc808-105">Business Connectivity Services (BCS) was introduced in SharePoint Server 2010 as an evolution of the Business Data Catalog released in Office SharePoint Server 2007.</span></span> <span data-ttu-id="cc808-106">Службы BCS дают SharePoint для работы с данными, которая размещается извне.</span><span class="sxs-lookup"><span data-stu-id="cc808-106">BCS enables SharePoint to work with data that is hosted externally.</span></span> <span data-ttu-id="cc808-107">Возможные источники могут включать баз данных, веб-служб, службы Windows Communication Foundation (WCF), Open Data Protocol (OData) источников и другие конфиденциальные данные, к которому осуществляется с помощью пользовательских сборок .NET.</span><span class="sxs-lookup"><span data-stu-id="cc808-107">Possible sources can include databases, web services, Windows Communication Foundation (WCF) services, Open Data Protocol (OData) sources, and other proprietary data that is accessed by using custom .NET assemblies.</span></span>

<a href="#SP15GettingStartedBCS_WhatDoYouNeed"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_WhatCanYouDo"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_LearnMore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a>

   
<span data-ttu-id="cc808-108">На рабочем месте динамические информационные работники необходим доступ к данным, которые находятся в отдельном программного обеспечения стандартов для примера:</span><span class="sxs-lookup"><span data-stu-id="cc808-108">In a dynamic workplace, information workers need access to data that resides in separate software worlds, for example:</span></span>
  
    
    

- <span data-ttu-id="cc808-109">Структурированные данные, существует ли в организации корпоративных приложений, таких как планирования ресурсов предприятия (ERP) и приложения управления (CRM) ресурсов клиента.</span><span class="sxs-lookup"><span data-stu-id="cc808-109">Structured data that exists in the organization's enterprise applications, such as enterprise resource planning (ERP) and customer resource management (CRM) applications.</span></span>
    
  
- <span data-ttu-id="cc808-110">Неструктурированных данных в бизнес-приложений повышения производительности, такие как Microsoft Office, групп и совместной работы приложений, таких как SharePoint и службы Web 2.0, такие как веб-приложений, вики-сайты, блоги и сайтов социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="cc808-110">Unstructured data in business productivity applications, such as those in Microsoft Office, in team and collaboration applications such as SharePoint, and in Web 2.0 services such as Internet applications, wikis, blogs, and social networking sites.</span></span>
    
  
<span data-ttu-id="cc808-111">Хотя большинство информационные работники большую часть их рабочего времени в рамках офисные приложения (например, среды Microsoft Office), они также необходим способ интеграции этой среде с корпоративных приложений и совместной работы программного обеспечения и службы, которые они используют.</span><span class="sxs-lookup"><span data-stu-id="cc808-111">Although most information workers spend much of their work time within the productivity applications (for example, the Microsoft Office environment), they also need a way to integrate that environment with the enterprise applications and collaboration software and services they use.</span></span> <span data-ttu-id="cc808-112">Службы BCS предоставляют этой возможности в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cc808-112">BCS provides that capability in SharePoint.</span></span>
  
    
    

## <a name="get-started-with-business-connectivity-services"></a><span data-ttu-id="cc808-113">Начало работы со службами Business Connectivity Services</span><span class="sxs-lookup"><span data-stu-id="cc808-113">Get started with Business Connectivity Services</span></span>
<span data-ttu-id="cc808-114"><a name="SP15GettingStartedBCS_WhatDoYouNeed"> </a></span><span class="sxs-lookup"><span data-stu-id="cc808-114"></span></span>

<span data-ttu-id="cc808-115">Для начала разработки с помощью службы BCS, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="cc808-115">To get started developing with BCS, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="cc808-116">SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-116">SharePoint</span></span>
    
  
- <span data-ttu-id="cc808-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc808-117">Visual Studio</span></span>
    
  
- <span data-ttu-id="cc808-118">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="cc808-118">Office Developer Tools for Visual Studio 2012</span></span>
    
    <span data-ttu-id="cc808-119">или</span><span class="sxs-lookup"><span data-stu-id="cc808-119">or</span></span>
    
  
- <span data-ttu-id="cc808-120">SharePoint Designer</span><span class="sxs-lookup"><span data-stu-id="cc808-120">SharePoint Designer</span></span>
    
  
<span data-ttu-id="cc808-121">Сведения о том, как настроить среду разработки см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="cc808-121">For information about how to set up your development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="business-connectivity-services-essentials"></a><span data-ttu-id="cc808-122">Основные службы подключения к бизнес-функции</span><span class="sxs-lookup"><span data-stu-id="cc808-122">Business Connectivity Services essentials</span></span>

<span data-ttu-id="cc808-123">В следующей таблице указаны основные концепции, которые необходимо ознакомиться с быстро приступить к разработке решений BCS.</span><span class="sxs-lookup"><span data-stu-id="cc808-123">The following table highlights the core concepts that you will need to be familiar with to start developing BCS solutions.</span></span>
  
    
    

<span data-ttu-id="cc808-124">**В таблице 1. Основные понятия, которые для понимания BCS**</span><span class="sxs-lookup"><span data-stu-id="cc808-124">**Table 1. Core concepts for understanding BCS**</span></span>


|<span data-ttu-id="cc808-125">**Статья**</span><span class="sxs-lookup"><span data-stu-id="cc808-125">**Article**</span></span>|<span data-ttu-id="cc808-126">**Описание**</span><span class="sxs-lookup"><span data-stu-id="cc808-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="cc808-127">Ключевые понятия модели данных сущности</span><span class="sxs-lookup"><span data-stu-id="cc808-127">Entity Data Model Key Concepts</span></span>](http://msdn.microsoft.com/en-us/library/ee382840.aspx) <br/> |<span data-ttu-id="cc808-p103">Модели данных сущности (EDM) использует три основные понятия для описания структуры данных: тип сущности, тип связи и свойства. Это наиболее важных концепций описания структуры данных в любой реализации EDM.</span><span class="sxs-lookup"><span data-stu-id="cc808-p103">The Entity Data Model (EDM) uses three key concepts to describe the structure of data: entity type, association type, and property. These are the most important concepts in describing the structure of data in any implementation of the EDM.</span></span>  <br/> |
| [<span data-ttu-id="cc808-130">Рекомендации по обеспечению безопасности базовой для веб-приложений</span><span class="sxs-lookup"><span data-stu-id="cc808-130">Basic Security Practices for Web Applications</span></span>](http://msdn.microsoft.com/en-us/library/zdh19h94.aspx) <br/> |<span data-ttu-id="cc808-p104">Широкое тема создания безопасного веб-приложения. В этом примере рассмотрения понять уязвимые места системы безопасности. Также необходимо ознакомиться с помощью средств безопасности операционной системы Windows, .NET Framework и ASP.NET. И, наконец очень важно понять, как использовать эти функции для борьбы с угрозами.</span><span class="sxs-lookup"><span data-stu-id="cc808-p104">The topic of creating a secure web application is extensive. It requires study to understand security vulnerabilities. You also need to become familiar with the security facilities of the Windows operating system, the .NET Framework, and ASP.NET. Finally, it is essential to understand how to use these security features to counter threats.</span></span>  <br/> |
| [<span data-ttu-id="cc808-135">Службы данных WCF</span><span class="sxs-lookup"><span data-stu-id="cc808-135">WCF Data Services</span></span>](http://msdn.microsoft.com/en-us/data/odata.aspx) <br/> |<span data-ttu-id="cc808-136">Службы данных WCF, ранее называлась служб данных ADO.NET, включите Создание и использование службы OData для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="cc808-136">WCF Data Services, formerly known as ADO.NET Data Services, enable the creation and consumption of OData services for the web.</span></span>  <br/> |
| [<span data-ttu-id="cc808-137">Open Data Protocol (OData)</span><span class="sxs-lookup"><span data-stu-id="cc808-137">Open Data Protocol (OData)</span></span>](http://www.odata.org) <br/> |<span data-ttu-id="cc808-p105">OData  это стандартный протокол для доступа к данным через URL-адрес. В основном он располагается в верхней части протокола HTTP, чтобы предоставить разрешение на чтение и запись функциями с помощью существующих команд HTTP.</span><span class="sxs-lookup"><span data-stu-id="cc808-p105">OData is an industry standard protocol for accessing data through URLs. It basically sits on top of the HTTP protocol to provide read and write functions using existing HTTP verbs.</span></span>  <br/> |
| [<span data-ttu-id="cc808-140">Службы IIS</span><span class="sxs-lookup"><span data-stu-id="cc808-140">Internet Information Services</span></span>](http://www.iis.net/) <br/> |<span data-ttu-id="cc808-p106">Internet Information Services (IIS)  платформа, работающей в среде SharePoint. Следует понять, как создать веб-сайтов, виртуальные каталоги, веб-служб, URL-адреса, веб-безопасности и другие технологии, связанные с IIS.</span><span class="sxs-lookup"><span data-stu-id="cc808-p106">Internet Information Services (IIS) is the platform that SharePoint runs on. You should understand how to create websites, virtual directories, web services, URLs, web security, and other technologies related to IIS.</span></span>  <br/> |
| [<span data-ttu-id="cc808-143">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-143">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="cc808-p107">Внешние типы контента описаны внешних систем, которые они представляют. Они являются для повторного использования, при импорте в SharePoint и могут использоваться для создания сложных решений без использования кода, с помощью SharePoint Designer 2013, Outlook 2013, веб-частей, внешних списков и пользовательских клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="cc808-p107">External content types are descriptions of the external systems that they represent. They are reusable when imported into SharePoint and can be used to create complex code-free solutions using SharePoint Designer 2013, Outlook 2013, Web Parts, external lists, and custom client applications.</span></span>  <br/> |
| [<span data-ttu-id="cc808-146">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-146">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md) <br/> |<span data-ttu-id="cc808-147">SharePoint предоставляет возможность доступа к все объекты через тщательно построенный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cc808-147">SharePoint provides the ability to access all objects through a carefully constructed URL.</span></span> <span data-ttu-id="cc808-148">Чтобы реализовать этот же функциональные возможности расширен BCS.</span><span class="sxs-lookup"><span data-stu-id="cc808-148">BCS has been extended to provide this same functionality.</span></span>  <br/> |
   

## <a name="what-can-you-do-with-business-connectivity-services"></a><span data-ttu-id="cc808-149">Что можно делать со службами Business Connectivity Services</span><span class="sxs-lookup"><span data-stu-id="cc808-149">What can you do with Business Connectivity Services?</span></span>
<span data-ttu-id="cc808-150"><a name="SP15GettingStartedBCS_WhatCanYouDo"> </a></span><span class="sxs-lookup"><span data-stu-id="cc808-150"></span></span>

<span data-ttu-id="cc808-p109">С BCS можно импортировать данные в SharePoint из множества различных источников. Например можно свести данные из базы данных внешнего SQL Server, традиционные веб-службы, службы WCF, собственный систем и службы OData.</span><span class="sxs-lookup"><span data-stu-id="cc808-p109">With BCS, you can bring information into SharePoint from many different sources. For example, you can bring data from an external SQL Server database, a traditional web service, a WCF service, proprietary systems, and OData services.</span></span>
  
    
    

<span data-ttu-id="cc808-153">**В таблице 2. Основные задачи по работе со службами Business Connectivity Services**</span><span class="sxs-lookup"><span data-stu-id="cc808-153">**Table 2. Basic tasks for working with Business Connectivity Services**</span></span>


|<span data-ttu-id="cc808-154">**Задача**</span><span class="sxs-lookup"><span data-stu-id="cc808-154">**Task**</span></span>|<span data-ttu-id="cc808-155">**Описание**</span><span class="sxs-lookup"><span data-stu-id="cc808-155">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="cc808-156">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-156">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md) <br/> |<span data-ttu-id="cc808-157">Сведения о создании Службы Business Connectivity Services (BCS) внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="cc808-157">Learn about creating Business Connectivity Services (BCS) external content types.</span></span>  <br/> |
| [<span data-ttu-id="cc808-158">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-158">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |<span data-ttu-id="cc808-159">Найдите сведения, которые необходимо приступить к созданию внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office компонентов.</span><span class="sxs-lookup"><span data-stu-id="cc808-159">Find information that is needed to get started creating external content types based on OData sources and using that data in SharePoint or Office components.</span></span>  <br/> |
| [<span data-ttu-id="cc808-160">Как: создание приемников внешних событий</span><span class="sxs-lookup"><span data-stu-id="cc808-160">How to: Create external event receivers</span></span>](how-to-create-external-event-receivers.md) <br/> |<span data-ttu-id="cc808-161">Узнайте концепции создания приемников событий, которые можно присоединить к внешним спискам и будет выполняться при обновлении внешних данных, представляемых списком.</span><span class="sxs-lookup"><span data-stu-id="cc808-161">Learn the concepts behind creating event receivers that can be attached to external lists and will execute when the external data that the list represents is updated.</span></span>  <br/> |
| [<span data-ttu-id="cc808-162">Как: создание добавить в пределах внешнего типа контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-162">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md) <br/> |<span data-ttu-id="cc808-163">Узнайте, как создать внешние типы контента, для которых установлены или областью действия на уровне приложения, что дает возможность создавать насыщенные приложения с помощью внешних источников данных.</span><span class="sxs-lookup"><span data-stu-id="cc808-163">Learn how to create external content types that are installed or scoped at the app level, enabling developers to create data-rich apps using external data sources.</span></span>  <br/> |
| [<span data-ttu-id="cc808-164">Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-164">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |<span data-ttu-id="cc808-165">Сведения об использовании клиентской объектной модели SharePoint для работы с BCS в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="cc808-165">Learn how to use the SharePoint client object model to work with BCS in SharePoint.</span></span>  <br/> |
   

## <a name="beyond-the-basics-learn-more-about-business-connectivity-services"></a><span data-ttu-id="cc808-166">От простого к сложному: Узнайте больше о Business Connectivity Services</span><span class="sxs-lookup"><span data-stu-id="cc808-166">Beyond the basics: Learn more about Business Connectivity Services</span></span>
<span data-ttu-id="cc808-167"><a name="SP15GettingStartedBCS_LearnMore"> </a></span><span class="sxs-lookup"><span data-stu-id="cc808-167"></span></span>

<span data-ttu-id="cc808-168">Когда главные основные понятия BCS, расширенные возможности можно использовать для создания многих эффективные типы решений.</span><span class="sxs-lookup"><span data-stu-id="cc808-168">When you master the basic concepts of BCS, you can use the more advanced features to build many powerful types of solutions.</span></span>
  
    
    

<span data-ttu-id="cc808-169">**В таблице 3. Расширенные концепции в BCS**</span><span class="sxs-lookup"><span data-stu-id="cc808-169">**Table 3. Advanced concepts in BCS**</span></span>


|<span data-ttu-id="cc808-170">**Статья**</span><span class="sxs-lookup"><span data-stu-id="cc808-170">**Topic**</span></span>|<span data-ttu-id="cc808-171">**Описание**</span><span class="sxs-lookup"><span data-stu-id="cc808-171">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="cc808-172">Как: создать службу данных OData для использования в качестве внешней системы BCS</span><span class="sxs-lookup"><span data-stu-id="cc808-172">How to: Create an OData data service for use as a BCS external system</span></span>](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md) <br/> |<span data-ttu-id="cc808-p110">Узнайте, как создать интернет-адресуемую службу WCF, которая использует OData для отправки уведомлений в SharePoint при изменении базовых данных. Эти уведомления используются для запуска событий, которые прикреплены ко внешним спискам.</span><span class="sxs-lookup"><span data-stu-id="cc808-p110">Learn how to create an Internet-addressable WCF service that uses OData to send notifications to SharePoint when the underlying data changes. These notifications are used to trigger events that are attached to external lists.</span></span>  <br/> |
| [<span data-ttu-id="cc808-175">Справочник по схеме модели BDC для SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-175">BDC model schema reference for SharePoint</span></span>](bdc-model-schema-reference-for-sharepoint.md) <br/> |<span data-ttu-id="cc808-176">Найдите справочную документацию по схеме модели BDC.</span><span class="sxs-lookup"><span data-stu-id="cc808-176">Find reference documentation for the schema of the BDC model.</span></span>  <br/> |
| [<span data-ttu-id="cc808-177">BCS клиента Справочник по объектной модели для SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-177">BCS client object model reference for SharePoint</span></span>](bcs-client-object-model-reference-for-sharepoint.md) <br/> |<span data-ttu-id="cc808-178">Получите сводку объектов, доступных для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемые Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="cc808-178">Get a summary of the objects that are available for creating client-side scripts using the SharePoint client object model to access external data exposed by Business Connectivity Services (BCS).</span></span>  <br/> |
| [<span data-ttu-id="cc808-179">Справочник по API-Интерфейс REST BCS для SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-179">BCS REST API reference for SharePoint</span></span>](bcs-rest-api-reference-for-sharepoint.md) <br/> |<span data-ttu-id="cc808-180">Найдите справочные сведения для создания представлений состояния (REST) коды URI используются для доступа и управления источников OData.</span><span class="sxs-lookup"><span data-stu-id="cc808-180">Find reference information for constructing Representational State Transfer (REST) URIs used for accessing and manipulating OData sources.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="cc808-181">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cc808-181">Additional resources</span></span>
<span data-ttu-id="cc808-182"><a name="SP15GettingStartedBCS_LearnMore"> </a></span><span class="sxs-lookup"><span data-stu-id="cc808-182"></span></span>


-  [<span data-ttu-id="cc808-183">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-183">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="cc808-184">Веб-сайт Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="cc808-184">Open Data Protocol website</span></span>](http://www.odata.org/)
    
  
-  [<span data-ttu-id="cc808-185">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-185">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="cc808-186">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-186">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="cc808-187">Внешние события и оповещения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-187">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="cc808-188">Добавьте в пределах внешних типов контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-188">Add-in-scoped external content types in SharePoint</span></span>](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="cc808-189">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="cc808-189">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
