---
title: "Разработка с помощью Duet Enterprise 2.0"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c3ef38aa-559e-4832-95c7-75e222c77624
ms.openlocfilehash: 15b9ac70484db215dd36a46d3648999aa26664e5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="developing-with-duet-enterprise-20"></a><span data-ttu-id="94036-102">Разработка с помощью Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="94036-102">Developing with Duet Enterprise 2.0</span></span>

## <a name="overview"></a><span data-ttu-id="94036-103">Обзор</span><span class="sxs-lookup"><span data-stu-id="94036-103">Overview</span></span>
<span data-ttu-id="94036-104"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-104"><a name="Overview"> </a></span></span>

<span data-ttu-id="94036-105">Duet Enterprise 2.0 является последней версии совместная работа между Microsoft и SAP, чтобы разрешить пользователям SharePoint для работы с данными из системы SAP. Объединяет компоненты SAP, а также SharePoint и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="94036-105">Duet Enterprise 2.0 is the latest version of a collaborative effort between Microsoft and SAP to give SharePoint users the ability to work with data from SAP systems.It combines components from SAP as well as SharePoint and SharePoint Online.</span></span> <span data-ttu-id="94036-106">Она дает разработчику создавать компоненты, которые позволяют пользователям для переноса данных из системы SAP в знакомой среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="94036-106">It gives a developer the ability to create components that will allow users to bring data from SAP systems into the familiar SharePoint environment.</span></span>
  
    
    

## <a name="features-of-duet-enterprise-20"></a><span data-ttu-id="94036-107">Функции Duet Enterprise 2.0</span><span class="sxs-lookup"><span data-stu-id="94036-107">Features of Duet Enterprise 2.0</span></span>
<span data-ttu-id="94036-108"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-108"><a name="Overview"> </a></span></span>

<span data-ttu-id="94036-109">При правильной установки и настройки, Duet Enterprise 2.0 будет предоставлять следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="94036-109">When properly installed and configured, Duet Enterprise 2.0 will provide the following features:</span></span>
  
    
    

- <span data-ttu-id="94036-110">Можно работать с данными в системы SAP в SharePoint с помощью Business данных веб-частей, внешних списков и пользовательских компонентов.</span><span class="sxs-lookup"><span data-stu-id="94036-110">You can work with data in SAP systems within SharePoint using Business Data Web parts, External lists and custom components.</span></span>
    
  
- <span data-ttu-id="94036-111">Использование данных SAP в SharePoint без кода с помощью встроенных компонентов.</span><span class="sxs-lookup"><span data-stu-id="94036-111">Use SAP data in SharePoint without code by using built-in components.</span></span>
    
  
- <span data-ttu-id="94036-112">С помощью отчетов систем внутри приложения SAP.</span><span class="sxs-lookup"><span data-stu-id="94036-112">Use SAP reporting systems inside of an app.</span></span>
    
  
- <span data-ttu-id="94036-113">Использовать специальные веб-части, установленные вместе с Duet Enterprise 2.0 для добавления данных SAP на страницы SharePoint</span><span class="sxs-lookup"><span data-stu-id="94036-113">Use special web parts installed with Duet Enterprise 2.0 to add SAP information to SharePoint pages</span></span>
    
  
- <span data-ttu-id="94036-114">Использование рабочего процесса SAP в приложении.</span><span class="sxs-lookup"><span data-stu-id="94036-114">Use SAP workflow in an app.</span></span>
    
  
- <span data-ttu-id="94036-115">JavaScript на стороне клиента могут использоваться разработчиками для взаимодействия с внешними данными SAP.</span><span class="sxs-lookup"><span data-stu-id="94036-115">Developers can use client-side JavaScript to interact with SAP external data.</span></span>
    
  
- <span data-ttu-id="94036-116">Обеспечение безопасной данных с помощью OAuth для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="94036-116">Secure data using OAuth for authentication.</span></span>
    
  

## <a name="setting-up-the-development-environment"></a><span data-ttu-id="94036-117">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="94036-117">Setting up the development environment</span></span>
<span data-ttu-id="94036-118"><a name="SettingUp"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-118"><a name="SettingUp"> </a></span></span>

<span data-ttu-id="94036-119">Разработка надстройки SharePoint с помощью Duet Enterprise 2.0, в основном совпадает с точно создание стандартной надстройки SharePoint. Visual Studio можно использовать для расширения возможностей приложений и работать в среде надежной среды разработки Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94036-119">Developing SharePoint Add-ins using Duet Enterprise 2.0, for the most part, is exactly the same as creating standard SharePoint Add-ins. You can use Visual Studio to extend your apps and work within the robust framework of the Visual Studio integrated development environment.</span></span>
  
    
    

## <a name="adding-external-content-types"></a><span data-ttu-id="94036-120">Добавление внешних типов контента</span><span class="sxs-lookup"><span data-stu-id="94036-120">Adding external content types</span></span>
<span data-ttu-id="94036-121"><a name="AddingECT"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-121"><a name="AddingECT"> </a></span></span>

<span data-ttu-id="94036-122">Для доступа к внешним данным, размещенное в системе SAP, необходимо добавить внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="94036-122">In order to access the external data housed on the SAP system, you will have to add an external content type.</span></span> <span data-ttu-id="94036-123">Поскольку данных SAP предоставляется через конечные точки OData, средства для автоматического создания, установленные в Visual Studio можно использовать для [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) , областью действия на уровне приложения.</span><span class="sxs-lookup"><span data-stu-id="94036-123">Since SAP data is exposed through OData endpoints, the auto-generation tools installed in Visual Studio can be used to  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) that is scoped at the app level.</span></span>
  
    
    
<span data-ttu-id="94036-124">Выполните следующие действия для создания внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="94036-124">Follow these steps to create an external content type:</span></span>
  
    
    

### <a name="creating-an-external-content-type-from-an-sap-odata-endpoint"></a><span data-ttu-id="94036-125">Создание внешнего типа контента из конечную точку SAP OData</span><span class="sxs-lookup"><span data-stu-id="94036-125">Creating an external content type from an SAP OData endpoint</span></span>


1. <span data-ttu-id="94036-126">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **типы контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="94036-126">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content types for External Data source**.</span></span>
    
  
2. <span data-ttu-id="94036-127">На странице **Укажите источника OData** введите URL-адрес службы рабочих процессов Duet Enterprise.</span><span class="sxs-lookup"><span data-stu-id="94036-127">On the **Specify OData Source** page, enter the URL of the Duet Enterprise Workflow Service.</span></span>
    
  
3. <span data-ttu-id="94036-128">Выберите имя для источника OData.</span><span class="sxs-lookup"><span data-stu-id="94036-128">Choose a name for your OData source.</span></span>
    
  
4. <span data-ttu-id="94036-129">Выбор сущностей, которые требуются.</span><span class="sxs-lookup"><span data-stu-id="94036-129">Select the entities that are needed.</span></span>
    
  
5. <span data-ttu-id="94036-130">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="94036-130">Choose **Finish**.</span></span>
    
  
<span data-ttu-id="94036-131">Visual Studio создаст новую папку с именем внешних типов контента, где можно найти только что созданный модели BDC.</span><span class="sxs-lookup"><span data-stu-id="94036-131">Visual Studio will create a new folder named External Content Types where you will find the newly created BDC model.</span></span>
  
    
    

## <a name="configuring-the-bdc-model"></a><span data-ttu-id="94036-132">Настройка модели BDC</span><span class="sxs-lookup"><span data-stu-id="94036-132">Configuring the BDC model</span></span>
<span data-ttu-id="94036-133"><a name="ConfiguringProject"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-133"><a name="ConfiguringProject"> </a></span></span>

<span data-ttu-id="94036-p103">Важно сделайте проект работать, заключается в добавлении свойство **ODataExtensionProvider** для модели BDC. Это свойство определяет поставщик расширения, который предоставляет BCS с расширениями SAP, необходимые для создания кода приложения.</span><span class="sxs-lookup"><span data-stu-id="94036-p103">The most important thing to make the project work, is to add the **ODataExtensionProvider** property to the BDC model. This property defines the extension provider that provides BCS with the SAP extensions needed for creating app code.</span></span>
  
    
    
<span data-ttu-id="94036-136">В этом примере показаны свойства, добавленные в модели BDC:</span><span class="sxs-lookup"><span data-stu-id="94036-136">This sample shows the properties added to the BDC model:</span></span>
  
    
    



```XML

<LobSystem Type="OData" Name="LOB_SYSTEM_NAME">
                     <Properties>
                          <Property Name="ODataServiceMetadataUrl" Type="System.String">
                               https://<DUET_METADATA_URL>:443/sap/opu/odata/sap/ 
                               ZANDY_PO_HEADER_SRV/$metadata</Property>
                          <Property Name="ODataServicesVersion" Type="System.String">2.0</Property>
                          <Property Name="ODataExtensionProvider" Type="System.String"> 
                               OBA.Server.Canary.ObaOdataServerExtensionProvider, 
                               OBA.Server.SSOProvider, 
                               Version=15.0.0.0, 
                               Culture=neutral, 
                               PublicKeyToken=71e9bce111e9429c</Property>
                          <Property Name="TraceHeader" Type="System.String">SAP-PASSPORT</Property>
                     </Properties>

```


## <a name="using-duet-starter-services-to-develop-custom-apps"></a><span data-ttu-id="94036-137">Использование Duet starter services для разработки настраиваемых приложений</span><span class="sxs-lookup"><span data-stu-id="94036-137">Using Duet starter services to develop custom apps</span></span>
<span data-ttu-id="94036-138"><a name="UsingDuetStarterServices"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-138"><a name="UsingDuetStarterServices"> </a></span></span>

<span data-ttu-id="94036-139">Duet Enterprise 2.0 устанавливается несколько служб starter к файловой системе на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="94036-139">Duet Enterprise 2.0 installs several starter services to the file system on the SharePoint server.</span></span> <span data-ttu-id="94036-140">Установка по умолчанию, эти файлы находятся в C:\\Program Files\\Duet Enterprise\\2.0\\решений\\Starter Services.</span><span class="sxs-lookup"><span data-stu-id="94036-140">In a default installation, the files are found at C:\\Program Files\\Duet Enterprise\\2.0\\Solutions\\Starter Services.</span></span> <span data-ttu-id="94036-141">Эти действия включают:</span><span class="sxs-lookup"><span data-stu-id="94036-141">Among these are:</span></span> 
  
    
    

- <span data-ttu-id="94036-142">OBACustomerWorkspace</span><span class="sxs-lookup"><span data-stu-id="94036-142">OBACustomerWorkspace</span></span>
    
  
- <span data-ttu-id="94036-143">OBAOrderToCash</span><span class="sxs-lookup"><span data-stu-id="94036-143">OBAOrderToCash</span></span>
    
  
- <span data-ttu-id="94036-144">OBAPortal</span><span class="sxs-lookup"><span data-stu-id="94036-144">OBAPortal</span></span>
    
  
- <span data-ttu-id="94036-145">OBAProductCenter</span><span class="sxs-lookup"><span data-stu-id="94036-145">OBAProductCenter</span></span>
    
  
<span data-ttu-id="94036-146">Каждый из этих решений содержит WSP файлов, решения и другие вспомогательные файлы, необходимые для их реализации.</span><span class="sxs-lookup"><span data-stu-id="94036-146">Each of these solutions contains WSP files, solution and other supporting files needed to implement them.</span></span>
  
    
    
<span data-ttu-id="94036-147">Эти решения можно использовать для просмотра, что можно сделать с Duet Enterprise 2.0 и какие шаблоны разработки, но не поддерживаются для использования в Надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="94036-147">These solutions can be used to see what can be done with Duet Enterprise 2.0 and what the development patterns are, but they are not supported for use in SharePoint Add-ins.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="94036-148">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="94036-148">Additional resources</span></span>
<span data-ttu-id="94036-149"><a name="ConNavExample_resources"> </a></span><span class="sxs-lookup"><span data-stu-id="94036-149"><a name="ConNavExample_resources"> </a></span></span>


-  [<span data-ttu-id="94036-150">Duet Enterprise для Microsoft SharePoint и SAP Server 2.0</span><span class="sxs-lookup"><span data-stu-id="94036-150">Duet Enterprise for Microsoft SharePoint and SAP Server 2.0</span></span>](http://technet.microsoft.com/ru-ru/library/ff972436.aspx)
    
  
-  [<span data-ttu-id="94036-151">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="94036-151">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="94036-152">Центр разработчиков Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94036-152">Visual Studio Developer Center</span></span>](http://msdn.microsoft.com/en-us/vstudio/default)
    
  
-  [<span data-ttu-id="94036-153">Разработка на базе Office с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94036-153">Office Development with Visual Studio</span></span>](http://msdn.microsoft.com/en-us/office/hh133430)
    
  

