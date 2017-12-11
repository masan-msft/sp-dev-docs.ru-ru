---
title: "Использование источников OData со службами Business Connectivity Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7a87e5bf-4428-4055-b113-7665a93e7326
ms.openlocfilehash: 40dcb00b9ab16c621aafd053691315ea9f4f99f7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="using-odata-sources-with-business-connectivity-services-in-sharepoint"></a><span data-ttu-id="50b34-102">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-102">Using OData sources with Business Connectivity Services in SharePoint</span></span>
<span data-ttu-id="50b34-103">Узнайте, как приступить к созданию внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office 2013 компонентов.</span><span class="sxs-lookup"><span data-stu-id="50b34-103">Learn how to get started creating external content types based on OData sources and using that data in SharePoint or Office 2013 components.</span></span>
## <a name="odata-and-the-odata-connector"></a><span data-ttu-id="50b34-104">OData и соединитель OData</span><span class="sxs-lookup"><span data-stu-id="50b34-104">OData and the OData connector</span></span>
<span data-ttu-id="50b34-105"><a name="SP15getstartedOdata_whatisodata"> </a></span><span class="sxs-lookup"><span data-stu-id="50b34-105"></span></span>

<span data-ttu-id="50b34-p101">Open Data protocol (OData) позволяет получить доступ к источнику данных, таких как базы данных, просмотрев имеющиеся специально созданный URL-адрес. Это позволяет упрощенный подход для подключений и работа с источниками данных, размещенных в пределах организации.</span><span class="sxs-lookup"><span data-stu-id="50b34-p101">The Open Data protocol (OData) lets you access a data source, such as a database, by browsing to a specially constructed URL. This allows for a simplified approach for connecting to and working with data sources that are hosted within an organization.</span></span> 
  
    
    
<span data-ttu-id="50b34-p102">OData  это протокол, который используется HTTP, Atom и Нотация объектов JavaScript (JSON) позволяет разработчикам создавать приложения, которые взаимодействуют с возрастающих число источников данных. Microsoft поддерживает создание этот стандарт, чтобы разрешить обмен данными между приложениями и хранилища данных, доступных из Интернета.</span><span class="sxs-lookup"><span data-stu-id="50b34-p102">OData is a protocol that uses HTTP, Atom, and JavaScript Object Notation (JSON) to enable developers to write applications that communicate with an ever-growing number of data sources. Microsoft supports the creation of this standard as a way to enable the exchange of data between applications and data stores that can be accessed from the web.</span></span>
  
    
    
<span data-ttu-id="50b34-110">Новый соединитель OData позволяет связываться с поставщиками OData SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50b34-110">The new OData connector enables SharePoint to communicate with OData providers.</span></span>
  
    
    
<span data-ttu-id="50b34-111">В SharePoint Business Connectivity Services (BCS) могут обмениваться данными источников OData или производители, без написания кода непосредственно к источнику OData.</span><span class="sxs-lookup"><span data-stu-id="50b34-111">In SharePoint, Business Connectivity Services (BCS) can communicate with OData sources, or producers, without having to code directly to the OData source.</span></span> <span data-ttu-id="50b34-112">Производители предоставляют доступ к своим данным структурированным способом с помощью веб-службы.</span><span class="sxs-lookup"><span data-stu-id="50b34-112">Producers expose their data in a structured way via a web service.</span></span> <span data-ttu-id="50b34-113">Некоторые производители могут разрешить обновление базовых данных, а некоторые могут разрешить доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="50b34-113">Some producers may allow updating of the underlying data, and some may allow only read access.</span></span> <span data-ttu-id="50b34-114">Для целей рекламу, какие операции можно выполнить производитель имеет службы документа в указанный URL-адрес конечной.</span><span class="sxs-lookup"><span data-stu-id="50b34-114">For purposes of advertising what operations are available, the producer has a service document found at a specified URL endpoint.</span></span> <span data-ttu-id="50b34-115">SharePoint уже производитель OData.</span><span class="sxs-lookup"><span data-stu-id="50b34-115">SharePoint is already a producer of OData.</span></span> <span data-ttu-id="50b34-116">Данные списка SharePoint в виде источника OData для любого объекта-получателя, имеющей соответствующие права.</span><span class="sxs-lookup"><span data-stu-id="50b34-116">SharePoint list data is exposed as an OData source for any consumer that has the appropriate rights.</span></span>
  
    
    

### <a name="examples-of-odata-producers"></a><span data-ttu-id="50b34-117">Примеры поставщики OData</span><span class="sxs-lookup"><span data-stu-id="50b34-117">Examples of OData producers</span></span>
<span data-ttu-id="50b34-118"><a name="ExamplesOfODataProducers"> </a></span><span class="sxs-lookup"><span data-stu-id="50b34-118"></span></span>

<span data-ttu-id="50b34-p104">Ниже приведены некоторые примеры реализаций OData. Эти приложения и службы предоставляют доступ к своим данным через протокол OData.</span><span class="sxs-lookup"><span data-stu-id="50b34-p104">The following are some examples of implementations of OData. These applications and services expose their data through the OData protocol.</span></span>
  
    
    

- <span data-ttu-id="50b34-121">SharePoint Foundation 2010</span><span class="sxs-lookup"><span data-stu-id="50b34-121">SharePoint Foundation 2010</span></span>
    
  
- <span data-ttu-id="50b34-122">SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="50b34-122">SharePoint Server 2010</span></span>
    
  
- <span data-ttu-id="50b34-123">SQL Azure</span><span class="sxs-lookup"><span data-stu-id="50b34-123">SQL Azure</span></span>
    
  
- <span data-ttu-id="50b34-124">Хранение таблицы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="50b34-124">Microsoft Azure Table Storage</span></span>
    
  
- <span data-ttu-id="50b34-125">Microsoft Azure Магазин</span><span class="sxs-lookup"><span data-stu-id="50b34-125">Microsoft Azure Marketplace</span></span>
    
  
-  <span data-ttu-id="50b34-126">Службы SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="50b34-126">SQL Server Reporting Services</span></span>
    
  
- <span data-ttu-id="50b34-127">Microsoft Dynamics CRM 2011 г.</span><span class="sxs-lookup"><span data-stu-id="50b34-127">Microsoft Dynamics CRM 2011</span></span>
    
  
- <span data-ttu-id="50b34-128">Windows Live</span><span class="sxs-lookup"><span data-stu-id="50b34-128">Windows Live</span></span>
    
  
<span data-ttu-id="50b34-129">Список поставщики служб OData в разделе  [веб-сайт Open Data Protocol](http://www.odata.org/ecosystem).</span><span class="sxs-lookup"><span data-stu-id="50b34-129">For a list of producers of OData services, see the  [Open Data Protocol website](http://www.odata.org/ecosystem).</span></span>
  
    
    

## <a name="prerequisites-for-working-with-the-bcs-odata-connector"></a><span data-ttu-id="50b34-130">Необходимые условия для работы с BCS соединитель OData</span><span class="sxs-lookup"><span data-stu-id="50b34-130">Prerequisites for working with the BCS OData connector</span></span>
<span data-ttu-id="50b34-131"><a name="SP15GetstartedOdata_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="50b34-131"></span></span>

<span data-ttu-id="50b34-132">Чтобы разработать основе внешних типов контента, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="50b34-132">To develop OData-based external content types, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="50b34-133">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="50b34-133">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="50b34-134">SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-134">SharePoint</span></span>
    
  
- <span data-ttu-id="50b34-135">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="50b34-135">Office Developer Tools for Visual Studio 2012</span></span>
    
  
<span data-ttu-id="50b34-136">Сведения о том, как настроить среду разработки см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="50b34-136">For information about how to set up your development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="creating-external-content-types-for-odata-data-sources"></a><span data-ttu-id="50b34-137">Создание внешних типов контента для источников данных OData</span><span class="sxs-lookup"><span data-stu-id="50b34-137">Creating external content types for OData data sources</span></span>
<span data-ttu-id="50b34-138"><a name="SP15GetstartedOdata_creatingECT"> </a></span><span class="sxs-lookup"><span data-stu-id="50b34-138"></span></span>

<span data-ttu-id="50b34-p105">Для SharePoint использовать данные, предоставляемые элементом определенного producer OData внешний тип контента должен быть создан внутри SharePoint. Как с помощью всех SharePoint внешних типов контента, он содержит все сведения о подключении, необходимые для подключения и взаимодействия с внешней системы.</span><span class="sxs-lookup"><span data-stu-id="50b34-p105">For SharePoint to use the data exposed by a specific OData producer, an external content type must be created inside SharePoint. As with all SharePoint external content types, it contains all the connectivity information that is needed to connect and communicate with the external system.</span></span>
  
    
    
<span data-ttu-id="50b34-141">Создание внешнего типа контента, который использует источник данных OData похоже на создание любой внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="50b34-141">Creating an external content type that uses an OData data source is similar to creating any external content type.</span></span> <span data-ttu-id="50b34-142">Можно использовать Visual Studio 2012 для автоматического создания OData внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="50b34-142">You can use Visual Studio 2012 to automatically generate OData external content types.</span></span> <span data-ttu-id="50b34-143">Необходимо просто предоставить представлений состояния (REST) конечной точки источника OData при создании внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="50b34-143">You merely provide the Representational State Transfer (REST) endpoint of the OData source when you create the external content type.</span></span> <span data-ttu-id="50b34-144">Дополнительные сведения можно [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="50b34-144">For more information see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
  
    
    

## <a name="in-this-section"></a><span data-ttu-id="50b34-145">В этой статье</span><span class="sxs-lookup"><span data-stu-id="50b34-145">In this section</span></span>
<span data-ttu-id="50b34-146"><a name="SP15GetstartedOdata_inthissect"> </a></span><span class="sxs-lookup"><span data-stu-id="50b34-146"></span></span>


-  [<span data-ttu-id="50b34-147">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-147">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="50b34-148">Как: создать службу данных OData для использования в качестве внешней системы BCS</span><span class="sxs-lookup"><span data-stu-id="50b34-148">How to: Create an OData data service for use as a BCS external system</span></span>](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md)
    
  
-  [<span data-ttu-id="50b34-149">Как: Создание внешнего списка с помощью источника данных OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-149">How to: Create an external list using an OData data source in SharePoint</span></span>](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md)
    
  

## <a name="see-also"></a><span data-ttu-id="50b34-150">См. также</span><span class="sxs-lookup"><span data-stu-id="50b34-150">See also</span></span>
<span data-ttu-id="50b34-151"><a name="SP15GetstartedOdata_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="50b34-151"></span></span>


-  [<span data-ttu-id="50b34-152">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-152">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="50b34-153">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-153">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="50b34-154">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-154">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="50b34-155">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="50b34-155">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

