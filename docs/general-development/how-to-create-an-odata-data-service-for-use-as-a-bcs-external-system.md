---
title: "Как создать службу данных OData для использования в качестве внешней системы BCS"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7d7b3aa6-85b7-400d-8ea5-50bebac56a1d
ms.openlocfilehash: 288a2b15329c934de74436e3bef4c319a07e6d7d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system"></a><span data-ttu-id="2bd8a-102">Как: создать службу данных OData для использования в качестве внешней системы BCS</span><span class="sxs-lookup"><span data-stu-id="2bd8a-102">How to: Create an OData data service for use as a BCS external system</span></span>
<span data-ttu-id="2bd8a-103">Узнайте, как создать Интернет адресации WCF службу, которая использует OData для отправки уведомлений в SharePoint при изменении базовых данных.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-103">Learn how to create an Internet-addressable WCF service that uses OData to send notifications to SharePoint when the underlying data changes.</span></span> <span data-ttu-id="2bd8a-104">Такие уведомления используются для активируют события, подключенные к внешним спискам.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-104">These notifications are used to trigger events that are attached to external lists.</span></span>
<span data-ttu-id="2bd8a-105">В этой статье описывается создание службы данных ASP.NET Windows Communication Foundation (WCF) для предоставления образца базы данных AdventureWorks 2012 LT.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-105">This article describes how to create an ASP.NET Windows Communication Foundation (WCF) Data Service to expose the AdventureWorks 2012 LT sample database.</span></span> <span data-ttu-id="2bd8a-106">Это позволяет получать доступ к данным посредством протокола Open Data protocol (OData).</span><span class="sxs-lookup"><span data-stu-id="2bd8a-106">This enables you to access the data through the Open Data protocol (OData).</span></span> <span data-ttu-id="2bd8a-107">Если доступ установлено через OData, можно настроить Business Connectivity Services (BCS) внешнего типа контента, который будет включен SharePoint для использования данных из внешней базы данных.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-107">When access is established through OData, you can configure a Business Connectivity Services (BCS) external content type that will enable SharePoint to consume the data from the external database.</span></span> <span data-ttu-id="2bd8a-108">Для дальнейшего улучшения этого источника OData, можно добавить контракты службы для службы WCF, которая позволит BCS для подписки на уведомления, оповещающие об изменении внешних данных.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-108">To further enhance this OData source, you can add service contracts to the WCF service that will enable BCS to subscribe to notifications that indicate that the external data has changed.</span></span>
  
    
    


## <a name="prerequisites-for-creating-the-odata-service"></a><span data-ttu-id="2bd8a-109">Необходимые условия для создания службы OData</span><span class="sxs-lookup"><span data-stu-id="2bd8a-109">Prerequisites for creating the OData service</span></span>
<span data-ttu-id="2bd8a-110"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="2bd8a-110"><a name="bkmk_Prerequisites"> </a></span></span>

<span data-ttu-id="2bd8a-111">Создание службы OData в этой статье необходимо соблюдение следующих условий:</span><span class="sxs-lookup"><span data-stu-id="2bd8a-111">The following are required to create the OData service in this article:</span></span>
  
    
    

- <span data-ttu-id="2bd8a-112">Службы IIS сервера</span><span class="sxs-lookup"><span data-stu-id="2bd8a-112">A server hosting Internet Information Services (IIS)</span></span>
    
  
- <span data-ttu-id="2bd8a-113">.NET Framework 3.5 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="2bd8a-113">.NET Framework 3.5 or later</span></span>
    
  
- <span data-ttu-id="2bd8a-114">SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-114">SharePoint</span></span>
    
  
-  [<span data-ttu-id="2bd8a-115">Сценарий 20012 AdventureWorks LT</span><span class="sxs-lookup"><span data-stu-id="2bd8a-115">AdventureWorks 20012 LT script</span></span>](http://msftdbprodsamples.codeplex.com/releases/view/55330)
    
  
-  [<span data-ttu-id="2bd8a-116">LT данных AdventureWorks 2012 г.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-116">AdventureWorks 2012 LT Data</span></span>](http://msftdbprodsamples.codeplex.com/releases/view/55330)
    
  
- <span data-ttu-id="2bd8a-117">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2bd8a-117">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="2bd8a-118">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2bd8a-118">Office Developer Tools for Visual Studio 2012</span></span>
    
  
<span data-ttu-id="2bd8a-119">Сведения о настройке среды разработки см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="2bd8a-119">For information about setting up your development environment, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

### <a name="core-concepts-for-creating-an-odata-service"></a><span data-ttu-id="2bd8a-120">Основные понятия, которые создания службы OData</span><span class="sxs-lookup"><span data-stu-id="2bd8a-120">Core concepts for creating an OData service</span></span>

<span data-ttu-id="2bd8a-121">В таблице 1 приведены статьи, которые помогут вам понять основные концепции создания WCF службы с помощью OData и внешнее содержимое.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-121">Table 1 lists articles that will help you understand the core concepts of building a WCF service using OData and external content.</span></span>
  
    
    

<span data-ttu-id="2bd8a-122">**В таблице 1. Основные понятия, которые создания службы OData**</span><span class="sxs-lookup"><span data-stu-id="2bd8a-122">**Table 1. Core concepts for creating an OData service**</span></span>


|<span data-ttu-id="2bd8a-123">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="2bd8a-123">**Resource**</span></span>|<span data-ttu-id="2bd8a-124">**Описание**</span><span class="sxs-lookup"><span data-stu-id="2bd8a-124">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="2bd8a-125">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-125">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |<span data-ttu-id="2bd8a-126">Представлены сведения, которые помогут приступить к созданию внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office 2013 компонентов.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-126">Provides information to help you start creating external content types based on OData sources and using that data in SharePoint or Office 2013 components.</span></span>  <br/> |
| [<span data-ttu-id="2bd8a-127">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-127">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |<span data-ttu-id="2bd8a-128">Узнайте, как использовать Visual Studio 2012 для обнаружения опубликованного источника OData и создать для повторного использования внешний тип контента для использования в BCS в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-128">Learn how to use Visual Studio 2012 to discover a published OData source and create a reusable external content type to use in BCS in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="2bd8a-129">Open Data Protocol</span><span class="sxs-lookup"><span data-stu-id="2bd8a-129">Open Data Protocol</span></span>](http://www.odata.org) <br/> |<span data-ttu-id="2bd8a-130">Предоставляет сведения о протокола Open Data protocol, включая определения протокола, сведения о структуре и примеры их использования.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-130">Provides information about the Open Data protocol, including protocol definitions, architectural information and usage examples.</span></span>  <br/> |
| [<span data-ttu-id="2bd8a-131">Обзор служб данных WCF</span><span class="sxs-lookup"><span data-stu-id="2bd8a-131">WCF Data Services Overview</span></span>](http://msdn.microsoft.com/en-us/library/cc668794.aspx) <br/> |<span data-ttu-id="2bd8a-p102">WCF Службы данных включает создание и использование служб данных для веб-сайта или в интрасети с помощью OData. OData позволяет предоставлять данные как ресурсы, которые являются адресации с помощью URI.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-p102">WCF Data Services enables creation and consumption of data services for the web or an intranet by using OData. OData enables you to expose your data as resources that are addressable by URIs.</span></span>  <br/> |
| [<span data-ttu-id="2bd8a-134">Разработка и развертывание служб данных WCF</span><span class="sxs-lookup"><span data-stu-id="2bd8a-134">Developing and Deploying WCF Data Services</span></span>](http://msdn.microsoft.com/en-us/library/gg258442) <br/> |<span data-ttu-id="2bd8a-135">Предоставляет сведения о разработке и развертывании WCF службы данных.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-135">Provides information about developing and deploying WCF Data Services.</span></span>  <br/> |
   

### <a name="steps-involved-in-creating-the-external-system"></a><span data-ttu-id="2bd8a-136">Действия для создания внешней системы</span><span class="sxs-lookup"><span data-stu-id="2bd8a-136">Steps involved in creating the external system</span></span>

<span data-ttu-id="2bd8a-137">Необходимо выполнить следующие действия</span><span class="sxs-lookup"><span data-stu-id="2bd8a-137">The following steps will need to be completed</span></span> 
  
    
    

- <span data-ttu-id="2bd8a-138">Установка образца базы данных AdventureWorks LT 2012 г.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-138">Install the AdventureWorks 2012 LT sample database</span></span>
    
  
- <span data-ttu-id="2bd8a-139">Создание службы OData</span><span class="sxs-lookup"><span data-stu-id="2bd8a-139">Create the OData Service</span></span>
    
  
- <span data-ttu-id="2bd8a-140">Настройка разрешений на доступ</span><span class="sxs-lookup"><span data-stu-id="2bd8a-140">Set access permissions</span></span>
    
  
- <span data-ttu-id="2bd8a-141">Тестирование службы</span><span class="sxs-lookup"><span data-stu-id="2bd8a-141">Test the service</span></span>
    
  
- <span data-ttu-id="2bd8a-142">Добавление возможности для дополнительные функциональные возможности BCS</span><span class="sxs-lookup"><span data-stu-id="2bd8a-142">Add capabilities for additional BCS functionality</span></span>
    
  

## <a name="installing-the-sample-database"></a><span data-ttu-id="2bd8a-143">Установка образца базы данных</span><span class="sxs-lookup"><span data-stu-id="2bd8a-143">Installing the sample database</span></span>
<span data-ttu-id="2bd8a-144"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="2bd8a-144"><a name="bkmk_Prerequisites"> </a></span></span>

<span data-ttu-id="2bd8a-145">Внешняя система обычно представляет собой базу данных и по этой причине в этом примере показано, как использовать образца базы данных AdventureWorks 2012 LT для представления собственный источник данных.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-145">An external system is usually a database and for that reason, this example shows how to use the AdventureWorks 2012 LT sample database to represent a proprietary datasource.</span></span>
  
    
    
<span data-ttu-id="2bd8a-146">Следующие шаги будут</span><span class="sxs-lookup"><span data-stu-id="2bd8a-146">The following steps will</span></span> 
  
    
    

## <a name="how-to-create-the-wcf-odata-service"></a><span data-ttu-id="2bd8a-147">Как создать WCF службы OData</span><span class="sxs-lookup"><span data-stu-id="2bd8a-147">How to create the WCF OData service</span></span>
<span data-ttu-id="2bd8a-148"><a name="bkmk_CreatingTheService"> </a></span><span class="sxs-lookup"><span data-stu-id="2bd8a-148"><a name="bkmk_CreatingTheService"> </a></span></span>

<span data-ttu-id="2bd8a-p103">Создание службы Windows Communication Foundation (WCF), который может осуществляться через протокол OData относительно несложно. Visual Studio 2012 предоставляет несколько средств для автоматического обнаружения и моделирование данных из различных источников данных. Это позволяет создавать подключения и интерфейсы к данным в базах данных SQL Server и другие типы хранилищ данных, которые можно работать с программным путем с помощью обширную объектную модель.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-p103">Creating a Windows Communication Foundation (WCF) service that can be accessed through the OData protocol is relatively straightforward. Visual Studio 2012 provides several tools for automatically discovering and modeling the data from various data sources. This allows you to create connections and interfaces to data in SQL Server databases and other types of data stores that can then be worked with programmatically using an extensive object model.</span></span>
  
    
    
<span data-ttu-id="2bd8a-152">Тем не менее для SharePoint для включения BCS для получения уведомлений из удаленных систем при изменении базовых данных, необходимо изменить службы WCF для ответа на такие изменения.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-152">However, for SharePoint to enable BCS to receive notifications from remote systems when the underlying data has changed, you must modify the WCF service to respond to those changes.</span></span>
  
    
    

### <a name="to-create-a-new-wcf-project"></a><span data-ttu-id="2bd8a-153">Чтобы создать проект на основе WCF</span><span class="sxs-lookup"><span data-stu-id="2bd8a-153">To create a new WCF project</span></span>


1. <span data-ttu-id="2bd8a-154">В Visual Studio, в меню **файл** выберите **Создать**, **проект**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-154">In Visual Studio, on the **File** menu, choose **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="2bd8a-155">В диалоговом окне **Создать проект** выберите **веб-** шаблон и выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-155">In the **New Project** dialog box, choose the **Web** template, and then choose **ASP.NET Web Application**.</span></span>
    
  
3. <span data-ttu-id="2bd8a-156">Введите **AdventureWorksService** для имени проекта и нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-156">Enter **AdventureWorksService** for the project name, and choose **OK**.</span></span>
    
  
4. <span data-ttu-id="2bd8a-157">В **Окне Обозреватель решений** откройте контекстное меню для проекта ASP.NET, который вы только что создали и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-157">In **Solution Explorer**, open the shortcut menu for the ASP.NET project that you just created, and choose **Properties**.</span></span>
    
  
5. <span data-ttu-id="2bd8a-158">Перейдите на вкладку **Web** и установите значение текстовое поле **конкретных портов**8008.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-158">Select the **Web** tab, and set the value of the **Specific port** text box to8008.</span></span>
    
  

### <a name="to-define-the-data-model"></a><span data-ttu-id="2bd8a-159">Чтобы определить модели данных</span><span class="sxs-lookup"><span data-stu-id="2bd8a-159">To define the data model</span></span>


1. <span data-ttu-id="2bd8a-160">В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите команду **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-160">In **Solution Explorer**, open the shortcut menu for the ASP.NET project, and choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="2bd8a-161">В диалоговом окне **Добавление нового элемента** выберите шаблон данных и выберите **Модель данных ADO.NET сущности**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-161">In the **Add New Item** dialog box, choose the Data template, and then choose **ADO.NET Entity Data Model**.</span></span>
    
  
3. <span data-ttu-id="2bd8a-162">Имя модели данных введите **AdventureWorks.edmx**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-162">For the name of the data model, enter **AdventureWorks.edmx**.</span></span>
    
  
4. <span data-ttu-id="2bd8a-163">В окне **Мастера модели данных сущности** выберите **Создать из базы данных** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-163">In the **Entity Data Model Wizard**, choose **Generate from Database**, and then choose **Next**.</span></span>
    
  
5. <span data-ttu-id="2bd8a-164">Подключения к базе данных модели данных, выполнив одно из следующих действий и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-164">Connect the data model to the database by doing one of the following steps, and then choose **Next**.</span></span>
    
  - <span data-ttu-id="2bd8a-165">Если у вас уже настроено подключение к базе данных, выберите **Новое подключение** и создайте новое подключение.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-165">If you do not have a database connection already configured, choose **New Connection**, and create a new connection.</span></span>
    
  
  - <span data-ttu-id="2bd8a-166">При наличии подключения к базе данных, уже настроена для подключения к базе данных Northwind, выберите это подключение в списке подключения.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-166">If you have a database connection already configured to connect to the Northwind database, choose that connection in the list of connections.</span></span>
    
  
  - <span data-ttu-id="2bd8a-167">На последней странице мастера установите флажки для всех таблиц в базе данных и снимите флажки для представлений и хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-167">On the final page of the wizard, select the check boxes for all tables in the database, and clear the check boxes for views and stored procedures.</span></span>
    
  
6. <span data-ttu-id="2bd8a-168">Нажмите кнопку **Готово**, чтобы закрыть мастер.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-168">Choose **Finish** to close the wizard.</span></span>
    
  

### <a name="to-create-the-data-service"></a><span data-ttu-id="2bd8a-169">Чтобы создать службу данных</span><span class="sxs-lookup"><span data-stu-id="2bd8a-169">To create the data service</span></span>


1. <span data-ttu-id="2bd8a-170">В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите команду **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-170">In **Solution Explorer**, open the shortcut menu for your ASP.NET project, and then choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="2bd8a-171">В диалоговом окне **Добавление нового элемента** выберите **Службы данных WCF**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-171">In the **Add New Item** dialog box, choose **WCF Data Service**.</span></span>
    
  
3. <span data-ttu-id="2bd8a-172">Имя службы введите **AdventureWorks**.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-172">For the name of the service, enter **AdventureWorks**.</span></span>
    
    <span data-ttu-id="2bd8a-p104">Visual Studio создает XML-файлы разметки и кода для новой службы. По умолчанию откроется окно Редактор кода. В **Окне Обозреватель решений**, служба будет иметь имя **AdventureWorks** с расширением. svc.cs или. svc.vb.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-p104">Visual Studio creates the XML markup and code files for the new service. By default, the code-editor window opens. In **Solution Explorer**, the service will have the name, **AdventureWorks**, with the extension .svc.cs or .svc.vb.</span></span>
    
  
4. <span data-ttu-id="2bd8a-p105">Замените комментарий  `/* TODO: put your data source class name here */` в определение класса, который определяет службу данных с типом, который является контейнером сущностей в модели данных, который в данном случае является **AdventureWorksEntities**. Определения класса должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2bd8a-p105">Replace the comment  `/* TODO: put your data source class name here */` in the definition of the class that defines the data service with the type that is the entity container of the data model, which in this case is **AdventureWorksEntities**. The class definition should look like the following:</span></span>
    
```cs
  
public class AdventureWorks : DataService<AdventureWorksEntities>
```

<span data-ttu-id="2bd8a-p106">По умолчанию при создании службы WCF, он становится недоступной из-за его настройки безопасности. Следующий шаг позволяет указать пользователей, которые могут обращаться к ней и права у них.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-p106">By default, when a WCF service is created, it cannot be accessed due to its security configuration. The next step lets you specify who can access it, and what rights they have.</span></span>
  
    
    

### <a name="to-enable-access-to-data-service-resources"></a><span data-ttu-id="2bd8a-180">Чтобы разрешить доступ к ресурсам службы данных</span><span class="sxs-lookup"><span data-stu-id="2bd8a-180">To enable access to data service resources</span></span>


- <span data-ttu-id="2bd8a-181">В коде для службы данных замените заполнитель код в функцию **InitializeService** следующее.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-181">In the code for the data service, replace the placeholder code in the **InitializeService** function with the following.</span></span>
    
```cs
  
      config.SetEntitySetAccessRule("*", EntitySetRights.All);
      config.SetServiceOperationAccessRule("*", ServiceOperationRights.All);
```


    This enables authorized clients to have read and write access to resources for the specified entity sets.
    
    > **Note:**
      > Any client that can access the ASP.NET application can also access the resources that are exposed by the data service. In a production data service, to prevent unauthorized access to resources, you should also secure the application itself. For more information, see  [Securing WCF Data Services](http://msdn.microsoft.com/en-us/library/dd728284.aspx). 
<span data-ttu-id="2bd8a-182">Для BCS для получения уведомлений должен быть механизм в источнике данных, которая будет принимать запрос для добавления и удаления из подписки на уведомления.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-182">For BCS to receive notifications, there must be a mechanism on the back-end data source that will accept a request to be added and removed from notification subscriptions.</span></span> 
  
    
    
<span data-ttu-id="2bd8a-183">На последнем этапе Создание службы является добавление операции службы для **Subscribe** и **Unsubscribe** стереотипов, определенных в модели BDC.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-183">The last step in creating the service is to add service operations for the **Subscribe** and **Unsubscribe** stereotypes that are defined in the BDC model.</span></span>
  
    
    

### <a name="to-add-service-operations-for-subscribe-and-unsubscribe-stereotypes"></a><span data-ttu-id="2bd8a-184">Чтобы добавить операции службы для подписки на и отписаться стереотипов</span><span class="sxs-lookup"><span data-stu-id="2bd8a-184">To add service operations for Subscribe and Unsubscribe stereotypes</span></span>


- <span data-ttu-id="2bd8a-185">На странице AdventureWorks.cs добавьте следующее объявление переменной строки.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-185">In the AdventureWorks.cs page, add the following string variable declaration.</span></span>
    
```cs
  
public string subscriptionStorePath = @"\\\\[SHARE_NAME]\\SubscriptionStore\\SubscriptionStore.xml";
```


    > **Note:**
      > This file is an XML file that is updated with the new subscriptions. Access to this file will be made by the server process, so make sure you have granted sufficient rights for this file access. > You might also want to create a database solution for storing subscription information. 

    Then add the following two **WebGet** methods to handle the subscriptions.
    


```cs
  [WebGet]
        public string Subscribe(string deliveryUrl, string eventType)
        {
            string subscriptionId = Guid.NewGuid().ToString();
            
            XmlDocument subscriptionStore = new XmlDocument();
            
            subscriptionStore.Load(subscriptionStorePath);

            // Add a new subscription element.
            XmlNode newSubNode = subscriptionStore.CreateElement("Subscription");

            // Add subscription ID element to the subscription element.
            XmlNode subscriptionIdStart = subscriptionStore.CreateElement("SubscriptionID");
            subscriptionIdStart.InnerText = subscriptionId;
            newSubNode.AppendChild(subscriptionIdStart);

            // Add delivery URL element to the subscription element.
            XmlNode deliveryAddressStart = subscriptionStore.CreateElement("DeliveryAddress");
            deliveryAddressStart.InnerText = deliveryUrl;
            newSubNode.AppendChild(deliveryAddressStart);

            // Add event type element to the subscription element.
            XmlNode eventTypeStart = subscriptionStore.CreateElement("EventType");
            eventTypeStart.InnerText = eventType;
            newSubNode.AppendChild(eventTypeStart);

            // Add the subscription element to the root element. 
            subscriptionStore.AppendChild(newSubNode);

            
            subscriptionStore.Save(subscriptionStorePath);

            return subscriptionId;
        }

        [WebGet]
        public void Unsubscribe(string subscriptionId)
        {
            XmlDocument subscriptionStore = new XmlDocument();
            subscriptionStore.Load(subscriptionStorePath);

            XmlNodeList subscriptions = subscriptionStore.DocumentElement.ChildNodes;
            foreach (XmlNode subscription in subscriptions)
            {
                XmlNodeList subscriptionList = subscription.ChildNodes;
                if (subscriptionList.Item(0).InnerText == subscriptionId)
                {
                    subscriptionStore.DocumentElement.RemoveChild(subscription);
                    break;
                }
            }

            subscriptionStore.Save(subscriptionStorePath);
        }

```


## <a name="next-steps"></a><span data-ttu-id="2bd8a-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2bd8a-186">Next steps</span></span>
<span data-ttu-id="2bd8a-187"><a name="bkmk_Next"> </a></span><span class="sxs-lookup"><span data-stu-id="2bd8a-187"></span></span>

<span data-ttu-id="2bd8a-188">Для уведомления SharePoint, что были внесены изменения, необходимо создать служба, которая запрашивает источник данных для изменения, а затем отправляет уведомления для всех тех, подписка на уведомления.</span><span class="sxs-lookup"><span data-stu-id="2bd8a-188">To notify SharePoint that changes have been made, you also need to create a service that queries the data source for changes, and then sends notifications to all those subscribed to notifications.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="2bd8a-189">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2bd8a-189">Additional resources</span></span>
<span data-ttu-id="2bd8a-190"><a name="bkmk_Addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2bd8a-190"></span></span>


-  [<span data-ttu-id="2bd8a-191">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-191">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2bd8a-192">Использование источников OData со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-192">Using OData sources with Business Connectivity Services in SharePoint</span></span>](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2bd8a-193">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-193">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2bd8a-194">Внешние события и оповещения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-194">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2bd8a-195">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-195">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2bd8a-196">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="2bd8a-196">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

