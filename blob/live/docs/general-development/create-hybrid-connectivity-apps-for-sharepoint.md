---
title: "Создание подключения к гибридных приложений для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 311f036e-3442-4497-b35e-442b665462d3
ms.openlocfilehash: 32d6e0471cf2bd5c29b2335edb309e40065e9119
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-hybrid-connectivity-apps-for-sharepoint"></a><span data-ttu-id="68529-102">Создание подключения к гибридных приложений для SharePoint</span><span class="sxs-lookup"><span data-stu-id="68529-102">Create hybrid connectivity apps for SharePoint</span></span>
<span data-ttu-id="68529-103">Сведения о процессе разработки и развертывания приложений для подключения к гибридные решения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68529-103">Learn about the process of developing and deploying apps for SharePoint hybrid connectivity solutions.</span></span>
## <a name="hybrid-connectivity-in-sharepoint-and-sharepoint-online"></a><span data-ttu-id="68529-104">Гибридного подключения в SharePoint и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="68529-104">Hybrid connectivity in SharePoint and SharePoint Online</span></span>
<span data-ttu-id="68529-105"><a name="bk_hybridconnectivity"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-105"><a name="bk_hybridconnectivity"> </a></span></span>

<span data-ttu-id="68529-106">По мере того как бизнеса с помощью SharePoint Online, они должны способ предоставления большого объема конфиденциальным данным надежно и безопасно.</span><span class="sxs-lookup"><span data-stu-id="68529-106">As businesses move to using SharePoint Online, they need a way to expose large amounts of proprietary data safely and securely.</span></span> <span data-ttu-id="68529-107">Чтобы решить эту проблему, SharePoint введена гибридного подключения.</span><span class="sxs-lookup"><span data-stu-id="68529-107">To help solve this challenge, SharePoint introduced hybrid connectivity.</span></span>
  
    
    
<span data-ttu-id="68529-108">Возможность подключения к гибридной Business Connectivity Services (BCS) позволяет SharePoint используют данные размещенное локально, внутри организации брандмауэров и защитить с различными формами проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="68529-108">The Business Connectivity Services (BCS) hybrid connectivity capability lets SharePoint consume data housed on-premises, inside corporate firewalls, and secured by various forms of authentication.</span></span> <span data-ttu-id="68529-109">С помощью подключения к гибридной среды SharePoint Online может безопасный доступ к эти данные в Интернете как если бы он был внутренней сети.</span><span class="sxs-lookup"><span data-stu-id="68529-109">With hybrid connectivity functionality, SharePoint Online can access this data securely over the web as if it was on the same internal network.</span></span> <span data-ttu-id="68529-110">После настройки гибридного подключения пользователи могут работать с данными, которые защищены в инфраструктуре бизнеса.</span><span class="sxs-lookup"><span data-stu-id="68529-110">Once hybrid connectivity is configured, users can work with data that is secured within the business' infrastructure.</span></span> <span data-ttu-id="68529-111">Они могут получить доступ к и работы с данными в соответствии с разрешений, предоставленных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68529-111">They can access and manipulate the data according to the permissions that they have been granted in SharePoint.</span></span>
  
    
    
<span data-ttu-id="68529-112">Полное описание Настройка гибридного решения работа в разделе [гибридной среды для SharePoint](http://technet.microsoft.com/en-us/library/jj838715.aspx).</span><span class="sxs-lookup"><span data-stu-id="68529-112">For a complete description of how to configure a working hybrid solution, see  [Hybrid for SharePoint](http://technet.microsoft.com/en-us/library/jj838715.aspx).</span></span> <span data-ttu-id="68529-113">В этих статьях описывается все требования к настройке источников данных, обратных прокси-серверов, поиска, безопасности, сети и все необходимые для настройки-сквозного сценария.</span><span class="sxs-lookup"><span data-stu-id="68529-113">This series of articles walks you through all the requirements of configuring data sources, reverse proxies, search, security, networking, and everything else needed to set up the end-to-end scenario.</span></span>
  
    
    

> <span data-ttu-id="68529-114">**Осторожность:** Чтобы настроить гибридную среду SharePoint, необходимо сочетание экспертов навыки и значительные практические навыки работы с SharePoint, SharePoint Online и связанных с ними продуктов и технологий.</span><span class="sxs-lookup"><span data-stu-id="68529-114">**Caution:** To configure a hybrid SharePoint environment, you need a combination of expert skills and significant hands-on experience with SharePoint, SharePoint Online, and related products and technologies.</span></span> <span data-ttu-id="68529-115">Мы рекомендуем сами участвовать Microsoft Consulting Services предоставление технических рекомендаций и поддержки во время разработки и развертывания гибридной среды.</span><span class="sxs-lookup"><span data-stu-id="68529-115">We recommend that you engage Microsoft Consulting Services to provide technical guidance and support during the design and deployment of your hybrid environment.</span></span> <span data-ttu-id="68529-116">> Для получения дополнительных сведений см [Microsoft Services](http://www.microsoft.com/en-us/microsoftservices/deploy.aspx).</span><span class="sxs-lookup"><span data-stu-id="68529-116">> For more information, see  [Microsoft Services](http://www.microsoft.com/en-us/microsoftservices/deploy.aspx).</span></span> 
  
    
    

<span data-ttu-id="68529-117">Для вы должны иметь возможность создавать приложения, которое использует данные из внутреннего источника данных через службы BCS и гибридного подключения в этой статье предполагается, что уже были выполнены процедуры для настройки гибридной среды.</span><span class="sxs-lookup"><span data-stu-id="68529-117">For you to be able to create an app that consumes data from an internal data source through BCS and the hybrid connection, this article assumes that you have already followed the procedures to configure your hybrid environment.</span></span>
  
    
    

## <a name="create-hybrid-connectivity-apps"></a><span data-ttu-id="68529-118">Создание подключения к гибридных приложений</span><span class="sxs-lookup"><span data-stu-id="68529-118">Create hybrid connectivity apps</span></span>
<span data-ttu-id="68529-119"><a name="bkmk_CreatingHybridConnectivityApps"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-119"><a name="bkmk_CreatingHybridConnectivityApps"> </a></span></span>

<span data-ttu-id="68529-120">Создание гибридного Надстройка SharePoint практически не отличается от создания любого Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68529-120">Creating a hybrid SharePoint Add-in is essentially the same as creating any SharePoint Add-in.</span></span>
  
    
    
<span data-ttu-id="68529-121">Выполните следующие действия для создания гибридного приложения.</span><span class="sxs-lookup"><span data-stu-id="68529-121">Follow these steps to create a hybrid app:</span></span>
  
    
    

-  [<span data-ttu-id="68529-122">Подготовка источника данных</span><span class="sxs-lookup"><span data-stu-id="68529-122">Prepare the data source</span></span>](#bkmk_PrepareDataSource)
    
  
-  [<span data-ttu-id="68529-123">Создание Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="68529-123">Create an SharePoint Add-in</span></span>](#bkmk_CreateAnApp)
    
  
-  [<span data-ttu-id="68529-124">Создание внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="68529-124">Create an external content type</span></span>](#bkmk_CreateECT)
    
  
-  [<span data-ttu-id="68529-125">Развертывание гибридного приложения</span><span class="sxs-lookup"><span data-stu-id="68529-125">Deploy the hybrid app</span></span>](#bkmk_DeployHybridApp)
    
  

### <a name="prepare-the-data-source"></a><span data-ttu-id="68529-126">Подготовка источника данных</span><span class="sxs-lookup"><span data-stu-id="68529-126">Prepare the data source</span></span>
<span data-ttu-id="68529-127"><a name="bkmk_PrepareDataSource"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-127"><a name="bkmk_PrepareDataSource"> </a></span></span>

<span data-ttu-id="68529-p105">В большинстве случаев, источник данных уже существует и обслуживание любое число бизнес-приложений. Тем не менее эти данные только могут быть доступны из внутри корпоративной безопасности инфраструктуры. Если данные существует на сервере, расположенном внутри корпоративного брандмауэра или защищен другими средствами, следующим шагом является данных для BCS, который также размещенное в сети брандмауэра. Сеть устройство настроено для перевода вызовы от SharePoint Online на внутренний фермы SharePoint. Это устройство называется «обратного прокси-сервер» и позволяет Надстройка SharePoint находится в облаке, чтобы позвонить в BCS, расположенный в сети брандмауэра. BCS обрабатывает все подключения к данным из него.</span><span class="sxs-lookup"><span data-stu-id="68529-p105">Most of the time, the data source is already in place and is servicing any number of business applications. However, that data may only be available from inside the corporate security infrastructure. If your data does exist on a server located on the inside of a corporate firewall, or is secured by some other means, the next step is to expose that data to BCS, which is also housed inside the firewall. A network device is configured to translate calls from SharePoint Online to the internal SharePoint farm. This device is referred to as a "reverse proxy" and allows the SharePoint Add-in located in the cloud to call into BCS located inside the firewall. BCS handles all the data connectivity from there.</span></span>
  
    
    
<span data-ttu-id="68529-p106">Сделать данные доступными для BCS, следует вывести ее в качестве источника OData. Для этого необходимо создать Internet Information Services (IIS) веб-сайта, который будет размещаться службы и разрешить BCS для обращаться к источнику данных через конечные точки OData и представлений состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="68529-p106">To make this data available to BCS, you should expose it as an OData source. You do this by creating an Internet Information Services (IIS) website that will host the service and allow BCS to talk to the data source through OData and Representational State Transfer (REST) endpoints.</span></span>
  
    
    
<span data-ttu-id="68529-136">Чтобы создать конечную точку OData, необходимо выполните следующие действия для создания данных службы Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="68529-136">To create an OData endpoint, you will need to follow these steps for creating a Windows Communication Foundation (WCF) data service.</span></span>
  
    
    

### <a name="to-create-a-wcf-data-service"></a><span data-ttu-id="68529-137">Создание службы данных WCF</span><span class="sxs-lookup"><span data-stu-id="68529-137">To create a WCF data service</span></span>


1. <span data-ttu-id="68529-p107">Создание веб-сайта IIS, выполнив по крайней мере Microsoft .NET Framework 4. Обеспечение безопасности сайта, обычную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="68529-p107">Create an IIS website running at least Microsoft .NET Framework 4. Secure the site using basic authentication.</span></span>
    
    > <span data-ttu-id="68529-140">**Примечание:** Не требуется для SharePoint для установки на этом сервере.</span><span class="sxs-lookup"><span data-stu-id="68529-140">**Note:** It's not necessary for SharePoint to be installed on this server.</span></span> <span data-ttu-id="68529-141">На самом деле для простоты и производительности, лучше Если SharePoint не установлен на сервере, на котором размещается служба данных WCF.</span><span class="sxs-lookup"><span data-stu-id="68529-141">In fact, for the sake of simplicity and performance, it's better if SharePoint is not installed on the server that hosts the WCF data service.</span></span> 
2. <span data-ttu-id="68529-142">Создайте новый проект в Visual Studio 2012 на основе шаблона **Пустой веб-приложения ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="68529-142">Create a new project in Visual Studio 2012 using the **ASP.NET Empty Web Application** template.</span></span>
    
  
3. <span data-ttu-id="68529-143">В **Обозревателе решений** добавьте новую **Модель ADO.NET сущности**.</span><span class="sxs-lookup"><span data-stu-id="68529-143">In **Solution Explorer** add a new **ADO.NET Entity Data Model**.</span></span>
    
  
4. <span data-ttu-id="68529-144">Выберите параметр **Создать из базы данных** в **Модели данных сущности**.</span><span class="sxs-lookup"><span data-stu-id="68529-144">Choose the **Generate from database** option in the **Entity Data Model Wizard**.</span></span>
    
  
5. <span data-ttu-id="68529-145">Выбор существующего подключения или создайте новый.</span><span class="sxs-lookup"><span data-stu-id="68529-145">Select an existing connection, or create a new one.</span></span>
    
  
6. <span data-ttu-id="68529-146">Предоставляют сведения о безопасности URL-адрес и подключения.</span><span class="sxs-lookup"><span data-stu-id="68529-146">Provide the URL and connection security information.</span></span>
    
  
7. <span data-ttu-id="68529-147">Выберите элементы, которые необходимо включить в модель и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="68529-147">Select the items that you want to include in the model, and choose **Finish**.</span></span>
    
  
8. <span data-ttu-id="68529-148">Еще раз в **Обозревателе решений** выберите Добавление новой **Службы данных WCF**, с помощью шаблона Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68529-148">Again in **Solution Explorer**, add a new **WCF Data Service** using the Visual Studio template.</span></span>
    
  
9. <span data-ttu-id="68529-149">Имя службы данных и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="68529-149">Name the data service, and choose **Next**.</span></span>
    
    <span data-ttu-id="68529-150">На этом этапе будет создана модель сущностей и результирующие классы, которые будут включены в проекте.</span><span class="sxs-lookup"><span data-stu-id="68529-150">At this point, the entity model will be created and the resulting classes will be included in your project.</span></span>
    
  
10. <span data-ttu-id="68529-151">Набор вы только что создана и указание какие сущности, необходимо предоставить разрешения на модель безопасности для сущности, созданные путем замены  `/* TODO: put your data source class name here */` с именем класса сущности.</span><span class="sxs-lookup"><span data-stu-id="68529-151">Set the security to the entities created by replacing the  `/* TODO: put your data source class name here */` with the class name of the entity model you just created and specifying which entities you want to grant permissions to.</span></span>
    
  
<span data-ttu-id="68529-152">Полное руководство, необходимых установить это см.:</span><span class="sxs-lookup"><span data-stu-id="68529-152">For a complete tutorial of how to set this up, see the following:</span></span> 
  
    
    

-  [<span data-ttu-id="68529-153">Приступая к работе с OData часть 1: построение службы OData</span><span class="sxs-lookup"><span data-stu-id="68529-153">Getting Started With OData Part 1: Building an OData Service</span></span>](http://msdn.microsoft.com/en-us/data/gg601462)
    
  
-  [<span data-ttu-id="68529-154">Краткое руководство (службы данных WCF)</span><span class="sxs-lookup"><span data-stu-id="68529-154">Quickstart (WCF Data Services)</span></span>](http://msdn.microsoft.com/en-us/library/cc668796.aspx)
    
  

### <a name="create-an-sharepoint-add-in"></a><span data-ttu-id="68529-155">Создание Надстройка SharePoint</span><span class="sxs-lookup"><span data-stu-id="68529-155">Create an SharePoint Add-in</span></span>
<span data-ttu-id="68529-156"><a name="bkmk_CreateAnApp"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-156"><a name="bkmk_CreateAnApp"> </a></span></span>

<span data-ttu-id="68529-p109">Один из предположения создадим здесь  это разработке приложения внутри корпоративного брандмауэра. Представляет сценарий, где разработчик, работающий в компании будет иметь компьютер находится за защиту инфраструктуры безопасности, разработки и тестирования приложения, пока не готова к развертыванию. Это упрощает процесс подключения к источнику данных из Visual Studio и использует Инструменты разработчика Office для Visual Studio 2013 для автоматического создания внешнего типа контента на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="68529-p109">One of the assumptions we are making here is that you are developing your app inside the corporate firewall. This represents a scenario where a developer working for a company would have a computer located behind the protection of the security infrastructure, developing and testing the app until it is ready to be deployed. This simplifies the process of connecting to the data source from Visual Studio, and uses Office Developer Tools for Visual Studio 2013 to automatically generate the external content type in the next step.</span></span>
  
    
    

### <a name="to-create-a-new-app"></a><span data-ttu-id="68529-160">Чтобы создать новое приложение</span><span class="sxs-lookup"><span data-stu-id="68529-160">To create a new app</span></span>


1. <span data-ttu-id="68529-161">Откройте Visual Studio 2012 на компьютере для разработки с Office Developer Tools для Visual Studio 2013 и установки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68529-161">Open Visual Studio 2012 on your development computer that has Office Developer Tools for Visual Studio 2013 and SharePoint installed.</span></span>
    
  
2. <span data-ttu-id="68529-162">Создание нового приложения для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="68529-162">Create a new app for SharePoint.</span></span>
    
  
3. <span data-ttu-id="68529-p110">Укажите имя приложения, локальный URL-адрес SharePoint, в котором будет размещаться сайт для тестирования, и способа отображения приложения для размещения. Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="68529-p110">Specify the name of the app, the local SharePoint URL that will host your site for testing, and how you want the app to be hosted. Choose **Finish**.</span></span>
    
  

### <a name="create-an-external-content-type"></a><span data-ttu-id="68529-165">Создание внешнего типа контента</span><span class="sxs-lookup"><span data-stu-id="68529-165">Create an external content type</span></span>
<span data-ttu-id="68529-166"><a name="bkmk_CreateECT"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-166"><a name="bkmk_CreateECT"> </a></span></span>

<span data-ttu-id="68529-167">Чтобы добавить в проект модели BDC или внешний тип контента, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="68529-167">To add a BDC model or external content type to your project, do the following.</span></span>
  
    
    

### <a name="to-add-an-external-content-type"></a><span data-ttu-id="68529-168">Чтобы добавить внешний тип контента</span><span class="sxs-lookup"><span data-stu-id="68529-168">To add an external content type</span></span>


1. <span data-ttu-id="68529-169">С помощью нового проекта по-прежнему откройте, откройте контекстное меню для решения и выберите **Добавить**, **типов контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="68529-169">With your new project still open, open the shortcut menu for the solution, and choose **Add**, **Content types for an External Data source**.</span></span>
    
  
2. <span data-ttu-id="68529-p111">Первая страница мастера используется для указания URL-адрес службы данных. На странице **Укажите источника OData** введите URL-адрес, который вы хотите подключиться к службы OData. URL-адрес должен выглядеть следующим образом: **http://services.odata.org/Northwind/Northwind.svc/**.</span><span class="sxs-lookup"><span data-stu-id="68529-p111">The first page of the wizard is used to specify the URL of the data service. On the **Specify OData Source** page, enter the URL of the OData service that you want to connect to. The URL should resemble the following: **http://services.odata.org/Northwind/Northwind.svc/**.</span></span>
    
  
3. <span data-ttu-id="68529-173">Выберите имя для источника OData и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="68529-173">Choose a name for your OData source, and then choose **Next**.</span></span>
    
  
4. <span data-ttu-id="68529-p112">Появится список сущностей данные, предоставляемые интерфейсом службы OData. Убедитесь в том, что установлен флажок **создать экземпляры списков для сущностей выделенные данные**.</span><span class="sxs-lookup"><span data-stu-id="68529-p112">A list of data entities that are being exposed by the OData service appears. Make sure that the **Create list instances for the selected data entities** check box is selected.</span></span>
    
  
5. <span data-ttu-id="68529-176">Выберите один или несколько сущностей и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="68529-176">Select one or more of the entities, and choose **Finish**.</span></span>
    
  
6. <span data-ttu-id="68529-177">Самое последнее, которые необходимо выполнить перед развертыванием  это изменение URL-адреса в файле только что созданный внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="68529-177">The last thing you have to do before deployment is modify the URL in your newly created external content type file.</span></span>
    
    <span data-ttu-id="68529-178">Откройте файл .ect в редакторе XML.</span><span class="sxs-lookup"><span data-stu-id="68529-178">Open the .ect file in an XML editor.</span></span>
    
  
7. <span data-ttu-id="68529-179">Измените свойство  `ODataServiceMetadataUrl` для указания на URL-адрес, который позволяет получить доступ через обратный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="68529-179">Modify the  `ODataServiceMetadataUrl` property to point to the URL that allows access through the reverse proxy.</span></span>
    
  
8. <span data-ttu-id="68529-180">Измените свойство  `ODataServiceUrl` с URL-адресом, обеспечивающий доступ через обратный прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="68529-180">Modify the  `ODataServiceUrl` property with the URL that allows access through the reverse proxy.</span></span>
    
  
<span data-ttu-id="68529-181">Сведения о добавлении основе внешнего типа контента можно [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="68529-181">For information about how to add an OData-based external content type, see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
  
    
    

### <a name="deploy-the-hybrid-app"></a><span data-ttu-id="68529-182">Развертывание гибридного приложения</span><span class="sxs-lookup"><span data-stu-id="68529-182">Deploy the hybrid app</span></span>
<span data-ttu-id="68529-183"><a name="bkmk_DeployHybridApp"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-183"><a name="bkmk_DeployHybridApp"> </a></span></span>

<span data-ttu-id="68529-p113">При развертывании приложения имеется несколько вариантов. Его можно развернуть и напрямую для клиента с помощью развертывания F5 или его можно упаковать создание App-файл с помощью функции публикации Visual Studio. Этот файл можно присваиваемый администратор клиента SharePoint Online и отправить.</span><span class="sxs-lookup"><span data-stu-id="68529-p113">When it is time to deploy your app, you have a couple of choices. You can deploy it directly to a tenancy using F5 deployment, or you can package it using the publishing features of Visual Studio to create an .app file. This file can then be given to the SharePoint Online tenant administrator and uploaded.</span></span>
  
    
    
<span data-ttu-id="68529-187">Сведения о развертывании Надстройки SharePoint см.:</span><span class="sxs-lookup"><span data-stu-id="68529-187">For information about deploying SharePoint Add-ins, see the following:</span></span> 
  
    
    

-  [<span data-ttu-id="68529-188">Развертывание и установка надстроек для SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="68529-188">Deploying and installing SharePoint Add-ins: methods and options</span></span>](http://msdn.microsoft.com/library/d15a74a7-3c10-485a-9885-7ef11aaa0d90%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="68529-189">Публикация надстройки для SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68529-189">Publish SharePoint Add-ins by using Visual Studio</span></span>](http://msdn.microsoft.com/library/8137d0fa-52e2-4771-8639-60af80f693bb%28Office.15%29.aspx)
    
  
<span data-ttu-id="68529-p114">Можно воспользоваться BDCM-файла, созданные для внешнего типа контента и извлечения, который будет использоваться на любой уровень выше приложения. Это показано в  [Как: преобразование добавить в пределах внешнего типа контента на уровне клиента](how-to-convert-an-add-in-scoped-external-content-type-to-tenant-scoped.md).</span><span class="sxs-lookup"><span data-stu-id="68529-p114">You can also take the BDCM file created for the external content type and extract that to be used at any level above the app. This is demonstrated in  [How to: Convert an add-in-scoped external content type to tenant-scoped](how-to-convert-an-add-in-scoped-external-content-type-to-tenant-scoped.md).</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="68529-192">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="68529-192">Additional resources</span></span>
<span data-ttu-id="68529-193"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="68529-193"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="68529-194">Hybrid for SharePoint</span><span class="sxs-lookup"><span data-stu-id="68529-194">Hybrid for SharePoint</span></span>](http://technet.microsoft.com/en-us/library/jj838715.aspx)
    
  
-  [<span data-ttu-id="68529-195">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="68529-195">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="68529-196">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="68529-196">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="68529-197">Публикация надстройки для SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68529-197">Publish SharePoint Add-ins by using Visual Studio</span></span>](http://msdn.microsoft.com/library/8137d0fa-52e2-4771-8639-60af80f693bb%28Office.15%29.aspx)
    
  

