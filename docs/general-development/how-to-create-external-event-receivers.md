---
title: "Создание приемников внешних событий"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6d5f486-6247-47f9-9876-fab12f13342f
ms.openlocfilehash: 598eb37d4a20f323439283901d17fa0784e7a48e
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-external-event-receivers"></a><span data-ttu-id="14215-102">Создание приемников внешних событий</span><span class="sxs-lookup"><span data-stu-id="14215-102">Create external event receivers</span></span>

<span data-ttu-id="14215-103">Узнайте, инструкции по созданию приемников внешних событий для локальных установок Business Connectivity Services (BCS) с помощью внешних списков.</span><span class="sxs-lookup"><span data-stu-id="14215-103">Learn the steps for creating external event receivers for on-premises installations of Business Connectivity Services (BCS) external lists.</span></span>

<span data-ttu-id="14215-104">Приемники событий внешнего являются классы, обеспечивающие надстройки SharePoint для обработки событий, происходящих с объектами SharePoint, такие как списки или элементы списка.</span><span class="sxs-lookup"><span data-stu-id="14215-104">External event receivers are classes that enable SharePoint Add-ins to respond to events that occur to SharePoint items, such as lists or list items.</span></span> <span data-ttu-id="14215-105">Например можно реагировать на события списка, такие как добавление или удаление поля; события элемента списка, такие как добавление или удаление элемента списка или вложения в элемент списка; или веб-события, такие как добавление или удаление сайта или семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="14215-105">For example, you can respond to list events, such as adding or removing a field; list item events, such as adding or removing a list item or attachment to a list item; or web events, such as adding or deleting a site or site collection.</span></span> <span data-ttu-id="14215-106">Удаленного приемника событий можно добавить в существующее решение Visual Studio, содержащий надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14215-106">You can add a remote event receiver to an existing Visual Studio solution that contains an SharePoint Add-in.</span></span>
  
    
    

<span data-ttu-id="14215-107">В этой статье описывается в образце кода [SharePoint: Создание удаленного приемника событий для внешних данных](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).</span><span class="sxs-lookup"><span data-stu-id="14215-107">This article accompanies the code sample  [SharePoint: Create a remote event receiver for external data](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).</span></span> <span data-ttu-id="14215-108">В этом примере показано создание все компоненты, необходимые для настройки и использования уведомлений о событиях внешней системы.</span><span class="sxs-lookup"><span data-stu-id="14215-108">It shows how to create all the components needed to configure and use external system event notifications.</span></span>
<span data-ttu-id="14215-109">В этом примере выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="14215-109">In this example, you will do the following:</span></span>
  
    
    


1. <span data-ttu-id="14215-110">Создание внешней системы на основании образце базы данных Northwind</span><span class="sxs-lookup"><span data-stu-id="14215-110">Create an external system based on the Northwind sample database</span></span>
    
  
2. <span data-ttu-id="14215-111">Предоставление доступа к образца данных через OData, создав Windows Communication Foundation (WCF) службы.</span><span class="sxs-lookup"><span data-stu-id="14215-111">Expose the sample data through OData by creating a Windows Communication Foundation (WCF) service.</span></span>
    
  
3. <span data-ttu-id="14215-112">Создание опроса служба, которая будет отслеживать изменения в данных и уведомить SharePoint эти изменения.</span><span class="sxs-lookup"><span data-stu-id="14215-112">Create a polling service that will monitor for changes in the data and notify SharePoint of those changes.</span></span>
    
  
4. <span data-ttu-id="14215-113">Создание приемника внешних событий, который выполняет, когда элементы добавляются к внешним данным и в результате создается новый элемент списка в список уведомлений.</span><span class="sxs-lookup"><span data-stu-id="14215-113">Create an external event receiver that executes when items are added to the external data and, as a result, creates a new list item on a notifications list.</span></span>
    
  

## <a name="prerequisites-and-system-set-up"></a><span data-ttu-id="14215-114">Необходимые условия и настройка системы</span><span class="sxs-lookup"><span data-stu-id="14215-114">Prerequisites and system set up</span></span>
<span data-ttu-id="14215-115"><a name="bkmk_Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-115"><a name="bkmk_Prerequisites"> </a></span></span>

<span data-ttu-id="14215-116">Для выполнения в этом примере, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="14215-116">To complete this example, you will need the following prerequisites:</span></span>
  
    
    

- <span data-ttu-id="14215-117">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="14215-117">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="14215-118">Инструменты разработчика Office для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="14215-118">Office Developer Tools for Visual Studio 2013</span></span>
    
  
- <span data-ttu-id="14215-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="14215-119">SQL Server</span></span>
    
  
- <span data-ttu-id="14215-120">SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-120">SharePoint</span></span>
    
  
- <span data-ttu-id="14215-121">Службы Internet Information Services 7.0</span><span class="sxs-lookup"><span data-stu-id="14215-121">Internet Information Services 7.0</span></span>
    
  
- <span data-ttu-id="14215-122">Образец базы данных "Борей"</span><span class="sxs-lookup"><span data-stu-id="14215-122">Northwind sample database</span></span>
    
  

## <a name="build-the-components-for-external-systems"></a><span data-ttu-id="14215-123">Построение компонентов для внешних систем</span><span class="sxs-lookup"><span data-stu-id="14215-123">Build the components for external systems</span></span>
<span data-ttu-id="14215-124"><a name="BuildingTheComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-124"><a name="BuildingTheComponents"> </a></span></span>

<span data-ttu-id="14215-p103">Максимальный часть конфигурации фактически происходит во внешней системе. Приемники событий внешнего правильной работы следующие компоненты должны иметь имеются во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="14215-p103">The biggest part of the configuration actually happens on the external system. For external event receivers to work correctly, the following components must be present and working on the external system:</span></span>
  
    
    

- <span data-ttu-id="14215-127">**Хранилища подписок:** Таблица, содержащая сведения о подписчиков, чтобы получать уведомления об изменениях к внешним данным.</span><span class="sxs-lookup"><span data-stu-id="14215-127">**Subscription store:** A table that contains information about the subscribers that want to be notified of changes to the external data.</span></span>
    
  
- <span data-ttu-id="14215-p104">**Хранения изменений:** Таблица, которая используется для хранения изменений элементов данных. Работает как временное хранение только так, как службы опроса удаляет элемент в таблице, если уведомления отправляются подписчикам в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14215-p104">**Changes store:** A table that is used to store the changes to the data items. It functions as temporary storage only because the polling service deletes the item in the table when notifications are sent back to subscribers in SharePoint.</span></span>
    
  
- <span data-ttu-id="14215-p105">**Опроса службы:** Требуется в этом сценарии, как средство проверки при была изменена и предоставленные изменить таблицу данных. Служба опроса запрос таблицы изменений и собирает пакет уведомлений, которое отправляется на адрес доставки SharePoint (конечная точка REST), хранящийся в хранилище подписки.</span><span class="sxs-lookup"><span data-stu-id="14215-p105">**Polling service:** Required in this scenario as a means of checking when data has been changed and submitted to the change table. The polling service queries the change table and assembles a notification package that is sent to the SharePoint delivery address (REST endpoint) stored in the subscription store.</span></span>
    
  
- <span data-ttu-id="14215-p106">**Службы данных OData WCF:** Представление данных из базы данных внешней системы, необходимо создать службы WCF. Эта служба на Internet Information Services (IIS), предоставляет интерфейс RESTful и канал OData, необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="14215-p106">**OData WCF Data Service:** To expose the data from the external system's database, you have to create a WCF service. This service, running on Internet Information Services (IIS), provides the RESTful interface and OData feed that is needed for this scenario.</span></span>
    
  

## <a name="set-up-the-external-system"></a><span data-ttu-id="14215-134">Настройка внешней системы</span><span class="sxs-lookup"><span data-stu-id="14215-134">Set up the external system</span></span>
<span data-ttu-id="14215-135"><a name="bkmk_SetUpTheExternalSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-135"><a name="bkmk_SetUpTheExternalSystem"> </a></span></span>

<span data-ttu-id="14215-136">Первая задача  настроить во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="14215-136">The first task is to set up the external system.</span></span>
  
    
    

### <a name="attach-the-northwind-sample-database"></a><span data-ttu-id="14215-137">Присоединение образце базы данных Northwind</span><span class="sxs-lookup"><span data-stu-id="14215-137">Attach the Northwind sample database</span></span>

<span data-ttu-id="14215-p107">Первая часть Подготовка серверной системе заключается в добавлении образце базы данных Northwind запущенный экземпляр SQL Server. Если уже установлены образце базы данных Northwind, можно запустить скрипты в следующем разделе, чтобы создать дополнительные объекты, необходимые для внешних событий уведомлений для работы.</span><span class="sxs-lookup"><span data-stu-id="14215-p107">The first part of preparing the back-end system is to add the Northwind sample database to a running instance of SQL Server. If you already have the Northwind sample database installed, you can run the scripts in the following section to create the additional objects needed for external eventing notifications to work.</span></span>
  
    
    
<span data-ttu-id="14215-140">Если у вас нет данных "Борей" установлен, видеть  [Установка образца базы данных Northwind](http://msdn.microsoft.com/library/2f92cfc3-6310-4327-b2f2-8610f7385c86%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="14215-140">However, if you don't have Northwind installed, see  [Installing the Northwind Sample Database](http://msdn.microsoft.com/library/2f92cfc3-6310-4327-b2f2-8610f7385c86%28Office.15%29.aspx).</span></span>
  
    
    
<span data-ttu-id="14215-141">Базы данных включен в пример кода: [SharePoint: Создание удаленного приемника событий для внешних данных](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).</span><span class="sxs-lookup"><span data-stu-id="14215-141">The database is also included with the code sample:  [SharePoint: Create a remote event receiver for external data](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).</span></span>
  
    
    

### <a name="create-the-subscription-store"></a><span data-ttu-id="14215-142">Создание хранилища подписок</span><span class="sxs-lookup"><span data-stu-id="14215-142">Create the subscription store</span></span>

<span data-ttu-id="14215-143">При установке базы данных Northwind, откройте новое окно запроса и выполните следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="14215-143">When the Northwind database is installed, open a new query window and execute the following script.</span></span>
  
    
    

```

USE [Northwind]
GO
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[EntitySubscribe](
    [SubscriptionId] [int] IDENTITY(1,1) NOT NULL,
    [EntityName] [nvarchar](250) NULL,
    [DeliveryURL] [nvarchar](250) NULL,
    [EventType] [int] NULL,
    [UserId] [nvarchar](50) NULL,
    [SubscribeTime] [timestamp] NULL,
    [SelectColumns] [nvarchar](10) NULL,
 CONSTRAINT [PK_Subscribe] PRIMARY KEY CLUSTERED 
(
    [SubscriptionId] ASC
)WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
```

<span data-ttu-id="14215-p108">Это создает таблицу в базе данных Northwind, с именем EntitySubscribe. Это служит в качестве хранилища подписок делается ссылка для более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="14215-p108">This creates a table in the Northwind database named EntitySubscribe. This serves as the subscription store referred to earlier.</span></span>
  
    
    

### <a name="create-the-change-store"></a><span data-ttu-id="14215-146">Создание хранилища изменений</span><span class="sxs-lookup"><span data-stu-id="14215-146">Create the change store</span></span>

<span data-ttu-id="14215-147">Выполните следующий скрипт, чтобы создать таблицу изменений, который будет записывать изменения данных в таблице Customers.</span><span class="sxs-lookup"><span data-stu-id="14215-147">Run the following script to create the change table that will record changes to the data in the Customers table.</span></span>
  
    
    

```

USE [Northwind]
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE TABLE [dbo].[Customers_Updates](
    [CustomerID] [nchar](5) NOT NULL,
    [CompanyName] [nvarchar](40) NOT NULL,
    [ContactName] [nvarchar](30) NULL,
    [ContactTitle] [nvarchar](30) NULL,
    [Address] [nvarchar](60) NULL,
    [City] [nvarchar](15) NULL,
    [Region] [nvarchar](15) NULL,
    [PostalCode] [nvarchar](10) NULL,
    [Country] [nvarchar](15) NULL,
    [Phone] [nvarchar](24) NULL,
    [Fax] [nvarchar](24) NULL,
    [TimeAdded] [datetime] NULL,
    [EventType] [int] NULL,
 CONSTRAINT [PK_Customers_Updates] PRIMARY KEY CLUSTERED 
(
    [CustomerID] ASC
)WITH (PAD_INDEX  = OFF, STATISTICS_NORECOMPUTE  = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS  = ON, ALLOW_PAGE_LOCKS  = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
```

<span data-ttu-id="14215-148">Это добавляет таблицу с именем Customers_Updates, в которой хранятся сведения о записи, который был добавлен к таблице Customers.</span><span class="sxs-lookup"><span data-stu-id="14215-148">This adds a table named Customers_Updates that stores the information about the record that was added to the Customers table.</span></span>
  
    
    

### <a name="create-the-change-trigger"></a><span data-ttu-id="14215-149">Создание изменение триггеров</span><span class="sxs-lookup"><span data-stu-id="14215-149">Create the change trigger</span></span>

<span data-ttu-id="14215-p109">Изменение триггера при изменения к таблице Customers. Запись при добавлении клиентов, SQL Server выполняется триггер, который вставляет новую запись в таблицу Customers_Updates со сведениями о записи.</span><span class="sxs-lookup"><span data-stu-id="14215-p109">The change trigger is fired when changes happen to the Customers table. Whenever a record is added to Customers, SQL Server executes the trigger, which inserts a new record in the Customers_Updates table with the information about the record.</span></span>
  
    
    
<span data-ttu-id="14215-152">Чтобы создать триггер, выполните следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="14215-152">To create the trigger, execute the following query.</span></span>
  
    
    



```

USE [Northwind]
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE trigger [dbo].[Customer_insupd] on [dbo].[Customers] for
INSERT
AS
DECLARE 
    @CustomerID nchar(5),
    @CompanyName nvarchar(40),
    @ContactName nvarchar(30) ,
    @ContactTitle nvarchar(30) ,
    @Address nvarchar(60) ,
    @City nvarchar(15) ,
    @Region nvarchar(15) ,
    @PostalCode nvarchar(10) ,
    @Country nvarchar(15) ,
    @Phone nvarchar(24) ,
    @Fax nvarchar(24), 
    @TimeAdded datetime,
    @EventType int
    
    Select @CustomerID = CustomerId, @CompanyName=CompanyName,
    @ContactName=ContactName, @ContactTitle=ContactTitle,
    @Address=Address, @City=City, @Region=Region,
    @PostalCode =PostalCode, @Country=Country,
    @Phone=Phone,@Fax=Fax,@EventType=1 
    from inserted
    
    insert into Customers_Updates 
    (CustomerId,CompanyName,
    ContactName, ContactTitle,
    Address, City, Region,
    PostalCode,Country,
    Phone,Fax,TimeAdded,EventType) values
    (@CustomerId,@CompanyName,
    @ContactName, @ContactTitle,
    @Address, @City, @Region,
    @PostalCode,@Country,
    @Phone,@Fax,SYSDATETIME(),@EventType)
    
GO

```

> [!NOTE]
> <span data-ttu-id="14215-153">f при использовании пользовательских хранимых процедур, определенных в модели BDC, можно также для создания, удаления и обновления триггеров.</span><span class="sxs-lookup"><span data-stu-id="14215-153">f you are using your own custom stored procedures as defined in your BDC model, you might also want to create the delete and update triggers.</span></span> <span data-ttu-id="14215-154">Дополнительные триггеров не рассматриваются как часть этого сценария.</span><span class="sxs-lookup"><span data-stu-id="14215-154">The additional triggers are not be covered as part of this scenario.</span></span> 
  
    
    


### <a name="create-the-stored-procedures"></a><span data-ttu-id="14215-155">Создайте хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="14215-155">Create the stored procedures</span></span>

<span data-ttu-id="14215-p111">При использовании прямого доступа к таблицам с помощью служб Business Connectivity Services этих процедур не является необходимым. Тем не менее при определении собственных процедур и пользовательского кода во внешней системе, может потребоваться добавьте следующие инструкции о предоставлении доступа к таблице из SQL Server.</span><span class="sxs-lookup"><span data-stu-id="14215-p111">If you are using direct table access with Business Connectivity Services, these procedures won't be necessary. However, if you are defining your own procedures and custom code on the external system, you might want to add these to allow access to the table from SQL Server.</span></span>
  
    
    

```

// DeleteEventRecords stored procedure
USE [Northwind]
GO
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE PROCEDURE [dbo].[proc_DeleteEventRecords]
    @CustomerID nchar(5), @EventType int
    AS
    Delete from Customers_Updates 
    WHERE  CustomerID like @CustomerID AND EventType=@EventType

GO

```

<span data-ttu-id="14215-158">**SubscribeEntity** хранимые процедуры будет создать запись в хранилище данных подписки.</span><span class="sxs-lookup"><span data-stu-id="14215-158">The **SubscribeEntity** stored procedure will create a record in the subscription store.</span></span>
  
    
    



```

// SubscribeEntity 
USE [Northwind]
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE PROCEDURE [dbo].[SubscribeEntity] 
    @EntityName Varchar(255),
    @EventType Integer,
    @DeliveryAddress Varchar(255),
    @SelectColumns Varchar(10)

AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;

    -- Insert statements for procedure here
    
    Insert into EntitySubscribe(EntityName,DeliveryURL,EventType,SelectColumns)
    values (@EntityName,@DeliveryAddress,@EventType,@SelectColumns)


END

GO

```


## <a name="create-the-odata-service"></a><span data-ttu-id="14215-159">Создание службы OData</span><span class="sxs-lookup"><span data-stu-id="14215-159">Create the OData Service</span></span>
<span data-ttu-id="14215-160"><a name="bkmk_CreatingTheODataService"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-160"><a name="bkmk_CreatingTheODataService"> </a></span></span>

<span data-ttu-id="14215-p112">Веб-канал OData размещается внутри **Службы данных WCF**. Эта служба WCF, затем, размещенным IIS в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="14215-p112">The OData feed is hosted inside a **WCF Data Service**. This WCF service is then hosted by IIS in a web application.</span></span>
  
    
    
<span data-ttu-id="14215-163">Следующие шаги создания новой службы данных ASP.NET WCF.</span><span class="sxs-lookup"><span data-stu-id="14215-163">The following steps create a new ASP.NET WCF data service.</span></span>
  
    
    

### <a name="to-create-the-wcf-data-service-application"></a><span data-ttu-id="14215-164">Создание приложения-службы данных WCF</span><span class="sxs-lookup"><span data-stu-id="14215-164">To create the WCF Data Service application</span></span>


1. <span data-ttu-id="14215-165">В Visual Studio 2012 в меню **файл** выберите **Создать**, **проект**.</span><span class="sxs-lookup"><span data-stu-id="14215-165">In Visual Studio 2012, on the **File** menu, choose **New**, **Project**.</span></span>
    
  
2. <span data-ttu-id="14215-166">В диалоговом окне **Новый проект** разверните узел Visual C# и выберите **веб-** шаблон и выберите **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="14215-166">In the **New Project** dialog box, under the Visual C# node, choose the **Web** template, and then choose **ASP.NET Web Application**.</span></span>
    
  
3. <span data-ttu-id="14215-167">Введите NorthwindService в качестве имени проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="14215-167">Enter NorthwindService as the name of the project, and then choose **OK**.</span></span>
    
  
<span data-ttu-id="14215-168">Затем с помощью мастера Visual Studio, вы обнаружения схемы источника данных и используйте его для создания модели данных сущности ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="14215-168">Next, using the Visual Studio wizard, you discover the schema of the data source and use it to create an ADO.NET entity data model.</span></span>
  
    
    

### <a name="to-define-the-data-model"></a><span data-ttu-id="14215-169">Чтобы определить модели данных</span><span class="sxs-lookup"><span data-stu-id="14215-169">To define the data model</span></span>


1. <span data-ttu-id="14215-170">В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="14215-170">In **Solution Explorer**, open the shortcut menu for the ASP.NET project, and choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="14215-171">В диалоговом окне **Добавление нового элемента** выберите шаблон **данных** и выберите **Модель данных ADO.NET сущности**.</span><span class="sxs-lookup"><span data-stu-id="14215-171">In the **Add New Item** dialog box, choose the **Data** template, and then choose **ADO.NET Entity Data Model**.</span></span>
    
  
3. <span data-ttu-id="14215-172">Имя модели данных введите Northwind.edmx.</span><span class="sxs-lookup"><span data-stu-id="14215-172">For the name of the data model, enter Northwind.edmx.</span></span>
    
  
4. <span data-ttu-id="14215-173">В мастере модели данных сущности выберите **Создать из базы данных** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14215-173">In the Entity Data Model Wizard, choose **Generate from Database**, and then choose **Next**.</span></span>
    
  
5. <span data-ttu-id="14215-174">Подключения к базе данных модели данных, выполнив одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="14215-174">Connect the data model to the database by doing one of the following steps:</span></span>
    
1. <span data-ttu-id="14215-p113">Если у вас уже настроено подключение к базе данных, выберите **Новое подключение** и создайте новое подключение. Дополнительные сведения можно [как: Создание подключения к базам данных SQL Server](http://msdn.microsoft.com/library/360c340d-e5a6-4a7e-a569-e95d500be43d%28Office.15%29.aspx). В этом экземпляре SQL Server должны иметь присоединенное образце базы данных Northwind. Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14215-p113">If you do not have a database connection already configured, choose **New Connection** and create a new connection. For more information, see [How to: Create Connections to SQL Server Databases](http://msdn.microsoft.com/library/360c340d-e5a6-4a7e-a569-e95d500be43d%28Office.15%29.aspx). This SQL Server instance must have the Northwind sample database attached. Choose **Next**.</span></span>
    
    <span data-ttu-id="14215-179">-или-</span><span class="sxs-lookup"><span data-stu-id="14215-179">-or-</span></span>
    
  
2. <span data-ttu-id="14215-180">При наличии подключения к базе данных, уже настроена для подключения к базе данных Northwind, выберите это подключение в списке подключения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="14215-180">If you have a database connection already configured to connect to the Northwind database, choose that connection from the list of connections, and then choose **Next**.</span></span>
    
  
6. <span data-ttu-id="14215-181">На последней странице мастера установите флажки для всех таблиц в базе данных и снимите флажки для представлений и хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="14215-181">On the final page of the wizard, select the check boxes for all tables in the database, and clear the check boxes for views and stored procedures.</span></span>
    
  
7. <span data-ttu-id="14215-182">Нажмите кнопку **Готово**, чтобы закрыть мастер.</span><span class="sxs-lookup"><span data-stu-id="14215-182">Choose the **Finish** button to close the wizard.</span></span>
    
  
<span data-ttu-id="14215-183">На следующем этапе создания фактической службы, размещенном в IIS, который будет предоставлять означает, что для доступа к внешним данным через представлений состояния (REST).</span><span class="sxs-lookup"><span data-stu-id="14215-183">In the next step, you create the actual service that is hosted by IIS that will provide the means to access external data through Representational State Transfer (REST).</span></span>
  
    
    

### <a name="to-create-the-wcf-data-service"></a><span data-ttu-id="14215-184">Создание службы данных WCF</span><span class="sxs-lookup"><span data-stu-id="14215-184">To create the WCF Data Service</span></span>


1. <span data-ttu-id="14215-185">В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите команду **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="14215-185">In **Solution Explorer**, open the shortcut menu for your ASP.NET project, and choose **Add New Item**.</span></span>
    
  
2. <span data-ttu-id="14215-186">В диалоговом окне **Добавление нового элемента** выберите **Службы данных WCF**.</span><span class="sxs-lookup"><span data-stu-id="14215-186">In the **Add New Item** dialog box, choose **WCF Data Service**.</span></span>
    
  
3. <span data-ttu-id="14215-187">Имя службы введите Northwind.</span><span class="sxs-lookup"><span data-stu-id="14215-187">For the name of the service, enter Northwind.</span></span>
    
  
4. <span data-ttu-id="14215-p114">В примере кода для службы данных в определение класса, который определяет службу данных замените комментарий  `/* TODO: put your data source class name here */` тип, контейнер сущностей в модели данных, который в данном случае является `NorthwindEntities`. Определения класса должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="14215-p114">In the code for the data service, in the definition of the class that defines the data service, replace the comment  `/* TODO: put your data source class name here */` with the type that is the entity container of the data model, which in this case is `NorthwindEntities`. The class definition should look like the following.</span></span>
    
```cs
  
public class Northwind : DataService<NorthwindEntities>

```


### <a name="to-set-the-security-on-the-service"></a><span data-ttu-id="14215-190">Настройка безопасности в службе</span><span class="sxs-lookup"><span data-stu-id="14215-190">To set the security on the service</span></span>


- <span data-ttu-id="14215-p115">Теперь необходимо изменить параметры безопасности, чтобы разрешить доступ к данным из веб-канал с внешним потребителей OData. При создании службы WCF, все отказано в доступе по умолчанию. Внесите следующие изменения в только что созданный класс.</span><span class="sxs-lookup"><span data-stu-id="14215-p115">You now have to modify the security to allow access to the data from the OData feed by external consumers. When a WCF service is created, all access is denied by default. Make the following changes to the class you just created.</span></span>
    
```cs
  
config.SetEntitySetAccessRule("*", EntitySetRights.All);
config.SetServiceOperationAccessRule("*", ServiceOperationRights.All);
```


### <a name="create-the-subscribe-service-operation-optional"></a><span data-ttu-id="14215-194">Создайте операцию службы подписки на (необязательно)</span><span class="sxs-lookup"><span data-stu-id="14215-194">Create the Subscribe service operation (optional)</span></span>

<span data-ttu-id="14215-p116">Службы WCF также можно запрограммировать позволяют обрабатывать запросы подписки на и отказаться от SharePoint. Если вы решили создать пользовательские хранимые процедуры для приложения каждый обрабатывается операцией службы.</span><span class="sxs-lookup"><span data-stu-id="14215-p116">The WCF service can also be coded with a means to handle the Subscribe and Unsubscribe requests from SharePoint. If you choose to create custom stored procedures for your application these will each be handled by a service operation.</span></span>
  
    
    
 <span data-ttu-id="14215-p117">**Подписки на**: Подпишитесь операция принимает запрос, отправляемый SharePoint и получает адрес доставки, тип события и сущность. Он также должен создать **subscriptionId** и затем записать все эти в таблице базы данных.</span><span class="sxs-lookup"><span data-stu-id="14215-p117">**Subscribe**: The Subscribe operation takes the request sent by SharePoint and retrieves the delivery address the event type and the entity. It also has to generate a **subscriptionId** and then record all of these into the database table.</span></span>
  
    
    



```cs

/// The Subscribe service operation maps directly to the Subscribe stereotype
/// found in the BDC model

[WebGet]
public string Subscribe(string deliveryUrl, string eventType)
{
   // Generate a new Guid that will function as the subscriptionId.
            string subscriptionId = new Guid().ToString();

            // This sproc will be used to create the subscription in the database.
            string subscribeSproc = "SubscribeEntity";

            // Create connection to database.
            using (SqlConnection conn = new SqlConnection(sqlConn))
            {
                SqlCommand cmd = new SqlCommand(subscribeSproc, conn);
                cmd.Parameters.Add(new SqlParameter("SubscriptionId", subscriptionId));
                cmd.Parameters.Add(new SqlParameter("EntityName", entityName));
                cmd.Parameters.Add(new SqlParameter("EventType", eventType));
                cmd.Parameters.Add(new SqlParameter("DeliveryAddress", deliveryUrl));
                cmd.Parameters.Add(new SqlParameter("SelectColumns", selectColumns));

                try
                {
                    conn.Open();
                    cmd.ExecuteNonQuery();
                }
                catch (Exception e)
                {
                    throw e;
                }
                finally
                {
                    conn.Close();
                }

                return subscriptionId;
            }
```

> [!NOTE]
> <span data-ttu-id="14215-p118">[!Примечание] Если настроить SQL Server для проверки подлинности Windows, он будет пытаться проверки подлинности запроса с удостоверение пула приложений. Убедитесь в том, что учетную запись, настроенную в пуле приложений имеет права на чтение и запись в базу данных.</span><span class="sxs-lookup"><span data-stu-id="14215-p118">If SQL Server is set up for Windows authentication, it will try to authenticate the request with the App Pool identity. Make sure that the account configured in the App Pool has rights to read and write in the database.</span></span> 
  
    
    


## <a name="create-the-polling-service"></a><span data-ttu-id="14215-201">Создание опроса службы</span><span class="sxs-lookup"><span data-stu-id="14215-201">Create the polling service</span></span>
<span data-ttu-id="14215-202"><a name="bkmk_CreateThePollingService"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-202"><a name="bkmk_CreateThePollingService"> </a></span></span>

<span data-ttu-id="14215-203">Опрос службы — это служба Windows, который несет ответственность за запрос таблицы изменений и создания и отправки уведомлений в SharePoint или SharePoint Online по адресу доставки.</span><span class="sxs-lookup"><span data-stu-id="14215-203">The polling service is a Windows service that is responsible for querying the change table and creating and sending notifications to SharePoint or SharePoint Online at the specific delivery address.</span></span>
  
    
    
<span data-ttu-id="14215-p119">Далее создайте новый проект службы Windows, который будет зарегистрирован на главном компьютере WCF. После регистрации проекта запущенной службы можно просматривать в консоли управления (MMC).</span><span class="sxs-lookup"><span data-stu-id="14215-p119">Next, you create a new Windows Service project that will be registered on the WCF host machine. Once the project is registered, you can view the running service in the Microsoft Management Console (MMC).</span></span>
  
    
    

### <a name="to-create-a-new-project"></a><span data-ttu-id="14215-206">Создание нового проекта</span><span class="sxs-lookup"><span data-stu-id="14215-206">To create a new project</span></span>


1. <span data-ttu-id="14215-207">Откройте Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="14215-207">Open Visual Studio 2012.</span></span>
    
  
2. <span data-ttu-id="14215-208">Создайте новый проект на основе шаблона службы Windows, назовите проект PollingServiceи нажмите кнопку « **ОК** ».</span><span class="sxs-lookup"><span data-stu-id="14215-208">Create a new project using the Windows Service template, name the project PollingService, and choose the **OK** button.</span></span>
    
  
3. <span data-ttu-id="14215-209">При создании проекта, откройте файл PollingService.cs в представлении кода.</span><span class="sxs-lookup"><span data-stu-id="14215-209">When the project is created, open the PollingService.cs file in code view.</span></span>
    
  
4. <span data-ttu-id="14215-210">Добавьте следующий код в только что созданный класс.</span><span class="sxs-lookup"><span data-stu-id="14215-210">Add the following code in the newly created class.</span></span>
    
```cs
  
public partial class PollingService : ServiceBase
{
   string subscriptionStorePath = string.Empty;

   public PollingService()
   {
      InitializeComponent();
   }

   protected override void OnStart(string[] args)
   {

      // This is the timer which fires every minute.           
      System.Timers.Timer aTimer = new System.Timers.Timer();
      aTimer.Elapsed += new System.Timers.ElapsedEventHandler(SendEventNotification);
      aTimer.Interval = 60000;
      aTimer.Enabled = true;
   }
   protected override void OnStop()
   {}

   private void SendEventNotification(object sender, EventArgs e)
   {
      try
      {
         List<ItemChange> events = itemChangeLookUp();             
         triggerEventPerSubscription(events);
      }
      catch (Exception ex)
      {
         EventLog.Log = "Application";
         EventLog.Source = ServiceName;
         EventLog.WriteEntry("PollingService" + ex.Message, EventLogEntryType.Error);
      }
   }

   private void triggerEventPerSubscription(List<ItemChange> events)
   {           
      foreach (ItemChange itemChangeEvent in events)
      {                        
         SendNotification(itemChangeEvent, itemChangeEvent.DeliveryAddress);
         string message = string.Format("PollingService.TriggerEventPerSubscription: Notification sent for item {0} of eventType 
                          {1}", itemChangeEvent.CustomerId, itemChangeEvent.EventType);
         EventLog.Log = "Application";
         EventLog.Source = ServiceName;
         EventLog.WriteEntry(message);                   
      }
   }

   private List<ItemChange> itemChangeLookUp()
   {
      EventLog.Log = "Application";
      EventLog.Source = ServiceName;
      EventLog.WriteEntry("Polling for Item Change");
      List<ItemChange> itemChangeList = new List<ItemChange>();          
      string connectionString = "Data Source=.;Initial Catalog=Northwind;Integrated Security=true";

      // Provide the query string with a parameter placeholder.
      string queryString = "Proc_RetrieveEventRecords";

      // Specify the parameter value.
      int paramValue = -50;

      using (SqlConnection connection = new SqlConnection(connectionString))
      {
         SqlCommand command = new SqlCommand(queryString, connection);
         command.CommandType = CommandType.StoredProcedure;
         command.Parameters.AddWithValue("@TimeSince", paramValue);
         try
         {
            connection.Open();
            SqlDataReader reader = command.ExecuteReader();
            while (reader.Read())
            {
               ItemChange item = new ItemChange(reader["CustomerID"].ToString(), Int32.Parse(reader["EventType"].ToString()), 
               reader[14].ToString(), reader["DeliveryUrl"].ToString(), reader["CompanyName"].ToString(), 
               reader["ContactName"].ToString(),reader["ContactTitle"].ToString(), reader["Address"].ToString(), 
               reader["City"].ToString(), reader["Region"].ToString(), reader["Country"].ToString(), reader["PostalCode"].ToString(), 
               reader["Phone"].ToString(), reader["Fax"].ToString());
               itemChangeList.Add(item);
            }
            reader.Close();
         }
         catch (Exception ex)
         {
            EventLog.Log = "Application";
            EventLog.Source = ServiceName;
            EventLog.WriteEntry("PollingService : ItemChangeLookup " + ex.Message, EventLogEntryType.Error);
         }
      } 
      string message = string.Format("{0} items changes", itemChangeList.Count);
      EventLog.Log = "Application";
      EventLog.Source = ServiceName;
      EventLog.WriteEntry(message);

      return itemChangeList;
   }

```

<span data-ttu-id="14215-211">Следующим шагом является создание исполняемого файла, который можно добавить в запущенных служб на компьютере OData.</span><span class="sxs-lookup"><span data-stu-id="14215-211">The next step is to build an executable file that can be added to the running services on the OData computer.</span></span>
  
    
    

### <a name="to-compile-and-deploy-the-polling-service"></a><span data-ttu-id="14215-212">Чтобы скомпилировать и развернуть службу опроса</span><span class="sxs-lookup"><span data-stu-id="14215-212">To compile and deploy the polling service</span></span>


1. <span data-ttu-id="14215-213">Нажмите клавишу F5, чтобы построить проект.</span><span class="sxs-lookup"><span data-stu-id="14215-213">Press F5 to build your project.</span></span>
    
  
2. <span data-ttu-id="14215-214">Откройте окно **командной строки для VS2012**.</span><span class="sxs-lookup"><span data-stu-id="14215-214">Open the **Command Prompt for VS2012**.</span></span>
    
  
3. <span data-ttu-id="14215-215">В командной строке перейдите к папке выходных данных проекта.</span><span class="sxs-lookup"><span data-stu-id="14215-215">At the prompt, navigate to your project output location.</span></span>
    
  
4. <span data-ttu-id="14215-216">В каталоге Bin найдите файл PollingService.exe.</span><span class="sxs-lookup"><span data-stu-id="14215-216">In the Bin directory, find the PollingService.exe file.</span></span>
    
  
5. <span data-ttu-id="14215-217">Введите installutil PollingService.exe и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="14215-217">Enter installutil PollingService.exe and press Enter.</span></span>
    
  
6. <span data-ttu-id="14215-218">Убедитесь, что служба запуска путем выполнения служб консоли Управления.</span><span class="sxs-lookup"><span data-stu-id="14215-218">Verify that the service is running by running the Services MMC.</span></span>
    
  

## <a name="required-sharepoint-components"></a><span data-ttu-id="14215-219">Необходимые компоненты SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-219">Required SharePoint components</span></span>
<span data-ttu-id="14215-220"><a name="bkmk_SharePointComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-220"><a name="bkmk_SharePointComponents"> </a></span></span>

<span data-ttu-id="14215-221">Для выполнения всей системы на сервере, на котором работает SharePoint необходимы следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="14215-221">To complete the whole system, the following components are required on the server that is running SharePoint.</span></span>
  
    
    

- <span data-ttu-id="14215-p120">**Внешнего типа контента:** Внешний тип контента по сути является определение XML из внешнего источника данных. Для этого сценария будет использовать новые средства Автоматическое формирование в Visual Studio 2012 для обнаружения источника данных и автоматически создать внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="14215-p120">**External content type:** The external content type is basically an XML definition of the external data source. For this scenario, you will use the new autogeneration tools in Visual Studio 2012 to discover the data source and create the external content type automatically.</span></span>
    
  
- <span data-ttu-id="14215-224">**Приемника внешних событий:** Приемник событий удаленного или внешнего является то, что позволяет действия на изменения внешних данных в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14215-224">**External event receiver:** The remote or external event receiver is the thing that makes actions on external data changes possible in SharePoint.</span></span> <span data-ttu-id="14215-225">Вы можете создать приемников событий для внешних списков и entities.</span><span class="sxs-lookup"><span data-stu-id="14215-225">You can create event receivers for external lists and for entities.</span></span>
    
    <span data-ttu-id="14215-p122">Приемник событий, созданный для внешнего списка похож на другие приемники событий в списки SharePoint. Создание кода и подключить его в список. Когда действие, которое выполняется на данных, представленного списка, выполняет приемника событий.</span><span class="sxs-lookup"><span data-stu-id="14215-p122">An event receiver that is created for an external list is similar to other event receivers for SharePoint lists. You create the code and attach it to the list. When an action is performed on the data that is represented by the list, the event receiver executes.</span></span>
    
    <span data-ttu-id="14215-p123">Приемника событий для сущностей выполняется так же, как приемник событий на основе списка, за исключением того, не подключенного к списку. Так же, как она получает уведомления, но она не требуется интерфейс, который связан с пример на основе списка. Это преимущество  можно программным путем перехвата уведомления и создавать код для выполнения некоторых действий. В этом сценарии это действие используется для создания новой записи в список уведомлений</span><span class="sxs-lookup"><span data-stu-id="14215-p123">An event receiver for entities is executed just like a list-based event receiver, except it doesn't need to be attached to a list. It receives notifications the same way, but it doesn't need the interface that is associated with the list-based example. The benefit of this is that you can intercept the notifications programmatically and create code to perform some action. In this scenario, that action is to create a new record in the notifications list</span></span> 
    
  
- <span data-ttu-id="14215-p124">**Список уведомлений:** Список уведомлений, простого списка SharePoint, который используется для записи уведомлений, полученных от внешней системы. Для каждой новой записи, добавлена к внешней системе запись будет создан в список уведомлений.</span><span class="sxs-lookup"><span data-stu-id="14215-p124">**Notifications list:** The notifications list is a simple SharePoint list that is used to record notifications received from the external system. For each new record added to the external system, a record is created in the notifications list.</span></span>
    
  

## <a name="set-up-the-sharepoint-components"></a><span data-ttu-id="14215-235">Настройка компонентов SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-235">Set up the SharePoint components</span></span>
<span data-ttu-id="14215-236"><a name="bkmk_SettingUpTheSharePointComponents"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-236"><a name="bkmk_SettingUpTheSharePointComponents"> </a></span></span>

<span data-ttu-id="14215-p125">Теперь, когда у вас есть внешней системы, Настройка, настало время перейти к созданию вторая уравнения. Теперь будет создавать компоненты для размещения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14215-p125">Now that you have the external system set up, it's time to move on to creating the other half of the equation. You will now create the components to be hosted on SharePoint.</span></span>
  
    
    

### <a name="to-create-a-new-visual-studio-2012-project"></a><span data-ttu-id="14215-239">Создание нового проекта Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="14215-239">To create a new Visual Studio 2012 project</span></span>


1. <span data-ttu-id="14215-240">Выберите **Новый проект** в Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="14215-240">In Visual Studio 2012, choose **New Project**.</span></span>
    
  
2. <span data-ttu-id="14215-241">Выберите шаблон проекта приложения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="14215-241">Choose the SharePoint app project template.</span></span>
    
  
<span data-ttu-id="14215-242">Инструменты разработчика Office для Visual Studio 2013 добавлена автоматическое формирование мастера будет обнаружение схемы в источнике данных, а затем создать внешний тип контента из того, что.</span><span class="sxs-lookup"><span data-stu-id="14215-242">Office Developer Tools for Visual Studio 2013 added an autogeneration wizard that will discover a data source's schema and then create an external content type from that.</span></span>
  
    
    

### <a name="to-add-a-new-external-content-type"></a><span data-ttu-id="14215-243">Чтобы добавить новый внешний тип контента</span><span class="sxs-lookup"><span data-stu-id="14215-243">To add a new external content type</span></span>


- <span data-ttu-id="14215-244">В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **Типов контента для внешнего источника данных**.</span><span class="sxs-lookup"><span data-stu-id="14215-244">In **Solution Explorer**, open the shortcut menu for the project, and choose **Add**, **Content Types for an External Data Source**.</span></span>
    
    <span data-ttu-id="14215-245">Будет запущен **Мастер настройки SharePoint**, который используется для автоматического создания внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="14215-245">This starts the **SharePoint Customization Wizard**, which is used to build the external content type automatically.</span></span>
    
    <span data-ttu-id="14215-246">Дополнительные сведения о том, как создать внешние типы контента можно [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="14215-246">For more information about how to create external content types, see  [How to: Create an external content type from an OData source in SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).</span></span>
    
  
<span data-ttu-id="14215-p126">Теперь будет использоваться для изменения XML, созданного на предыдущем шаге, чтобы добавить метод для подписки на. Это позволит BCS для связи с внешней системы, когда кто-то подписывается уведомлений об изменении внешних данных.</span><span class="sxs-lookup"><span data-stu-id="14215-p126">You will now modify the XML that was generated in the previous step to add a method for Subscribe. This will allow BCS to communicate with the external system when someone subscribes to be notified about external data changes.</span></span>
  
    
    

### <a name="to-add-the-subscribe-method-to-the-external-content-type-xml"></a><span data-ttu-id="14215-249">Добавление метода подписки на внешний тип контента XML</span><span class="sxs-lookup"><span data-stu-id="14215-249">To add the Subscribe method to the external content type XML</span></span>


1. <span data-ttu-id="14215-250">В **Обозревателе решений** найдите новый узел с именем **Внешних типов контента**.</span><span class="sxs-lookup"><span data-stu-id="14215-250">In **Solution Explorer**, find the new node named **External Content Types**.</span></span>
    
  
2. <span data-ttu-id="14215-251">Найдите файл **Customers.ect** и откройте его с помощью редактора XML.</span><span class="sxs-lookup"><span data-stu-id="14215-251">Find the **Customers.ect** file, and open it with an XML editor.</span></span>
    
  
3. <span data-ttu-id="14215-252">Прокрутите список вниз до конца страницы и вставьте следующий метод в разделе  `<Methods>` .</span><span class="sxs-lookup"><span data-stu-id="14215-252">Scroll down to the bottom of the page, and paste the following method into the  `<Methods>` section.</span></span>
    
```XML
  
<Method Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe" IsStatic="true">
              <Properties>
                <Property Name="ODataEntityUrl" Type="System.String">/EntitySubscribes</Property>
                <Property Name="ODataHttpMethod" Type="System.String">POST</Property>
                <Property Name="ODataPayloadKind" Type="System.String">Entry</Property>
                <Property Name="ODataFormat" Type="System.String">application/atom+xml</Property>
                <Property Name="ODataServiceOperation" Type="System.Boolean">false</Property>
              </Properties>
              <AccessControlList>
                <AccessControlEntry Principal="NT Authority\\Authenticated Users">
                  <Right BdcRight="Edit" />
                  <Right BdcRight="Execute" />
                  <Right BdcRight="SetPermissions" />
                  <Right BdcRight="SelectableInClients" />
                </AccessControlEntry>
              </AccessControlList>
              <Parameters>
                <Parameter Direction="In" Name="@DeliveryURL">
                  <TypeDescriptor TypeName="System.String" Name="DeliveryURL" >
                    <Properties>
                      <Property Name="IsDeliveryAddress" Type="System.Boolean">true</Property>
                    </Properties>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="In" Name="@EventType">
                  <TypeDescriptor TypeName="System.Int32" Name="EventType" >
                    <Properties>
                      <Property Name="IsEventType" Type="System.Boolean">true</Property>
                    </Properties>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="In" Name="@EntityName">
                  <TypeDescriptor TypeName="System.String" Name="EntityName" >
                    <DefaultValues>
                      <DefaultValue MethodInstanceName="SubscribeCustomer" Type="System.String">Customers</DefaultValue>
                    </DefaultValues>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="In" Name="@SelectColumns">
                  <TypeDescriptor TypeName="System.String" Name="SelectColumns" >
                    <DefaultValues>
                      <DefaultValue MethodInstanceName="SubscribeCustomer" Type="System.String">*</DefaultValue>
                    </DefaultValues>
                  </TypeDescriptor>
                </Parameter>
                <Parameter Direction="Return" Name="SubscribeReturn">
                  <TypeDescriptor Name="SubscribeReturnRootTd" TypeName="Microsoft.BusinessData.Runtime.DynamicType">
                    <TypeDescriptors>
                      <TypeDescriptor Name="SubscriptionId" TypeName="System.String" >
                        <Properties>
                          <Property Name="SubscriptionIdName" Type="System.String">Default</Property>
                        </Properties>
                        <Interpretation>
                          <ConvertType LOBType="System.Int32" BDCType="System.String"/>
                        </Interpretation>
                      </TypeDescriptor>
                      <TypeDescriptor Name="DeliveryURL" TypeName="System.String" />
                      <TypeDescriptor Name="SelectColumns" TypeName="System.String" >
                      </TypeDescriptor>
                      <TypeDescriptor Name="EntityName" TypeName="System.String" />
                      <TypeDescriptor Name="EventType" TypeName="System.Int32" />
                      <TypeDescriptor Name="UserId" TypeName="System.String" />
                      <!--TypeDescriptor Name="SubscribeTime" TypeName="System." /-->
                    </TypeDescriptors>
                  </TypeDescriptor>
                </Parameter>
              </Parameters>
              <MethodInstances>
                <MethodInstance Type="EventSubscriber" ReturnParameterName="SubscribeReturn" ReturnTypeDescriptorPath="SubscribeReturnRootTd" Default="true" Name="SubscribeCustomer" DefaultDisplayName="Customer Subscribe">
                  <AccessControlList>
                    <AccessControlEntry Principal="NT Authority\\Authenticated Users">
                      <Right BdcRight="Edit" />
                      <Right BdcRight="Execute" />
                      <Right BdcRight="SetPermissions" />
                      <Right BdcRight="SelectableInClients" />
                    </AccessControlEntry>
                  </AccessControlList>
                </MethodInstance>
              </MethodInstances>
            </Method>
```

<span data-ttu-id="14215-253">Теперь добавим код клиента, позволяющие списке, чтобы подписаться на уведомления о событиях.</span><span class="sxs-lookup"><span data-stu-id="14215-253">You will now add client code to allow your list to subscribe to event notifications.</span></span>
  
    
    

### <a name="to-add-code-to-the-appjs-file-to-initiate-the-subscription"></a><span data-ttu-id="14215-254">Добавление кода в файл App.js для инициации подписки</span><span class="sxs-lookup"><span data-stu-id="14215-254">To add code to the App.js file to initiate the subscription</span></span>


- <span data-ttu-id="14215-p127">В папке Scripts Надстройка SharePoint проекта откройте файл **App.js**. Вставьте следующий метод в файл.</span><span class="sxs-lookup"><span data-stu-id="14215-p127">In the Scripts folder of your SharePoint Add-in project, open the **App.js** file. Paste the following method into the file.</span></span>
    
```
  
function SubscribeEntity()
{
    var notificationCallback = new SP.BusinessData.Runtime.NotificationCallback(context, "http://[MACHINE NAME]:8585");
    var url = myweb.get_url();
    notificationCallback.set_notificationContext(url);
    context.load(notificationCallback);
    var subscription = entity.subscribe(1, notificationCallback, "", "SubscribeCustomer", lobSystemInstance);
    context.load(subscription);
    context.executeQueryAsync(OnSubscribeSuccess, failmethod);
}
```

<span data-ttu-id="14215-257">Чтобы зарегистрировать приемника событий с помощью этого сценария, необходимо создать кнопку на страницу Default.aspx в вашем проекте и вызовите **SubscribeEntity()** из метода **onclick()**.</span><span class="sxs-lookup"><span data-stu-id="14215-257">To register the event receiver with this script, you have to create a button on the Default.aspx page in your project and call the **SubscribeEntity()** from the **onclick()** method.</span></span>
  
    
    

- <span data-ttu-id="14215-258">Откройте страницу Default.aspx и добавьте следующий HTML-код.</span><span class="sxs-lookup"><span data-stu-id="14215-258">Open the Default.aspx page, and add the following HTML.</span></span>
    
```HTML
  
<input type="button" value="Subscribe" onclick="SubscribeEntity();"/>
```

<span data-ttu-id="14215-p128">Для регистрации событий для работы необходимо также включить списка SharePoint для принятия внешние события. Для этого, включите функцию внешние события.</span><span class="sxs-lookup"><span data-stu-id="14215-p128">For eventing to work, you must also enable the SharePoint list to accept external events. This is done by turning on the External Events feature.</span></span>
  
    
    
<span data-ttu-id="14215-261">Ниже приведен сценарий, который будет включен компонент с помощью клиентского кода.</span><span class="sxs-lookup"><span data-stu-id="14215-261">The following is a script that will turn on the feature using client code.</span></span>
  
    
    



```cs
function EnableEventing_Clicked()
{
    var clientContext = SP.ClientContext.get_current();
    var web = clientContext.get_web();
    var features = web.get_features();

    clientContext.load(features);

    // The GUID provided here is the feature that allows external events and alerts.
    var eventingFeatureId = new SP.Guid('5B10D113-2D0D-43BD-A2FD-F8BC879F5ABD');

    var eventingFeature = features.add(eventingFeatureId, true, SP.FeatureDefinitionScope.farm);

    clientContext.load(eventingFeature);
    var onEventingFeatureActivated = function () {
        alert("eventing feature activated");
    };
    clientContext.executeQueryAsync(Function.createDelegate(this,
    onEventingFeatureActivated));
}
```

<span data-ttu-id="14215-262">Так же, как с помощью **Subscribe**добавляется кнопка на страницу, которая будет включена функция.</span><span class="sxs-lookup"><span data-stu-id="14215-262">Just like with **Subscribe**, you will add a button to the page that will turn on the feature.</span></span>
  
    
    
<span data-ttu-id="14215-263">Добавьте следующий HTML-код на страницу Default.aspx непосредственно под кнопкой **подписаться**.</span><span class="sxs-lookup"><span data-stu-id="14215-263">Add the following HTML to the Default.aspx page, right below the **Subscribe** button.</span></span>
  
    
    



```HTML

<input type="button" value="EnableEventing" onclick="EnableEventing_Clicked();"" />
```

<span data-ttu-id="14215-264">Рассмотрим процедуру для этого сценария необходимо добавить список уведомлений, которое будет показывать уведомления, отправляемые внешней системой.</span><span class="sxs-lookup"><span data-stu-id="14215-264">Next, for this scenario you must add a notifications list that will show the notifications sent by the external system.</span></span>
  
    
    

### <a name="to-add-the-notifications-list"></a><span data-ttu-id="14215-265">Чтобы добавить список уведомлений</span><span class="sxs-lookup"><span data-stu-id="14215-265">To add the notifications list</span></span>


1. <span data-ttu-id="14215-266">В **Обозревателе решений** откройте контекстное меню для имени проекта и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="14215-266">In **Solution Explorer**, open the shortcut menu for the project name, and choose **Add**.</span></span>
    
  
2. <span data-ttu-id="14215-267">Выберите шаблон **списка** и имя спискаNotificationList.</span><span class="sxs-lookup"><span data-stu-id="14215-267">Choose the **List** template, and name the listNotificationList.</span></span>
    
  
<span data-ttu-id="14215-p129">Имитация приемника событий, который зарегистрирован с помощью SharePoint в глобальном кэше сборок, в примере задаются консольное приложение, которое будет запущен процесс прослушивание изменений. При получении уведомления, **NotificationList**добавляет элемент списка.</span><span class="sxs-lookup"><span data-stu-id="14215-p129">To mimic an event receiver that is registered with SharePoint in the global assembly cache, the sample provides a console application that will start listening for changes. When it receives a notification, it adds a list item to the **NotificationList**.</span></span>
  
    
    

### <a name="to-start-the-command-line-event-receiver"></a><span data-ttu-id="14215-270">Чтобы запустить приемника событий командной строки</span><span class="sxs-lookup"><span data-stu-id="14215-270">To start the command-line event receiver</span></span>


1. <span data-ttu-id="14215-271">Откройте **RemoteEventReceiverConsoleApp**.</span><span class="sxs-lookup"><span data-stu-id="14215-271">Open the **RemoteEventReceiverConsoleApp**.</span></span>
    
  
2. <span data-ttu-id="14215-272">Откройте файл **Program.cs** и измените имя на локальный компьютер (или компьютере с запущенным приемника событий).</span><span class="sxs-lookup"><span data-stu-id="14215-272">Open the **Program.cs** file, and change the name of your local computer (or the computer where the event receiver will be running).</span></span>
    
  
3. <span data-ttu-id="14215-273">В Visual Studio для запуска консольного приложения, нажмите кнопку **Пуск**.</span><span class="sxs-lookup"><span data-stu-id="14215-273">Click the **Start** button in Visual Studio to run the console application.</span></span>
    
    <span data-ttu-id="14215-p130">Откроется окно командной строки, который указывает, что приложение было выполнено успешно и прослушивает уведомления об изменении из внешней системы. Не закрывайте это окно во время этой проверки.</span><span class="sxs-lookup"><span data-stu-id="14215-p130">A command window opens, which indicates that the application has compiled correctly, and it is listening for change notifications from the external system. Leave this window open during this test.</span></span>
    
  

### <a name="to-deploy-the-app-to-sharepoint"></a><span data-ttu-id="14215-276">Чтобы развернуть приложение для SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-276">To deploy the app to SharePoint</span></span>


- <span data-ttu-id="14215-277">Нажмите клавишу F5, с помощью Visual Studio откройте построение и развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="14215-277">Press F5 with Visual Studio open to build and deploy the app.</span></span>
    
  

## <a name="test-the-app"></a><span data-ttu-id="14215-278">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="14215-278">Test the app</span></span>
<span data-ttu-id="14215-279"><a name="bkmk_testApp"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-279"><a name="bkmk_testApp"> </a></span></span>

<span data-ttu-id="14215-280">Теперь можно видеть приложения в действии.</span><span class="sxs-lookup"><span data-stu-id="14215-280">Now you can see the app in action.</span></span>
  
    
    

1. <span data-ttu-id="14215-281">Обзор вокруг приложение, чтобы просмотреть различные списки, которые представляют данные во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="14215-281">Browse around the app to see the different lists that represent the data in the external system.</span></span>
    
  
2. <span data-ttu-id="14215-282">Щелкните список **клиентов**.</span><span class="sxs-lookup"><span data-stu-id="14215-282">Click the **Customers** list.</span></span>
    
  
3. <span data-ttu-id="14215-283">Добавление нового клиента.</span><span class="sxs-lookup"><span data-stu-id="14215-283">Add a new customer.</span></span>
    
  
4. <span data-ttu-id="14215-284">Просмотр нового элемента списка, который вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="14215-284">View the new list item you just created.</span></span>
    
  
5. <span data-ttu-id="14215-285">Перейдите к списку уведомления, чтобы увидеть, что во внешней системе уведомил SharePoint внесение изменений в таблице Customers.</span><span class="sxs-lookup"><span data-stu-id="14215-285">Go to the notifications list to see that the external system has notified SharePoint of a change to the Customers table.</span></span>
    
    <span data-ttu-id="14215-p131">Имейте в виду, таймера задано значение отправлять уведомления каждую минуту. Во время тестирования, может потребоваться ожидания короткого периода, прежде чем Просмотр персональных уведомления.</span><span class="sxs-lookup"><span data-stu-id="14215-p131">Keep in mind that the timer is set to send notifications every one minute. While testing, you might have to wait for a short period before you see the notifications posted.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="14215-288">См. также</span><span class="sxs-lookup"><span data-stu-id="14215-288">See also</span></span>
<span data-ttu-id="14215-289"><a name="bkmk_additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="14215-289"><a name="bkmk_additionalresources"> </a></span></span>


-  [<span data-ttu-id="14215-290">Внешние события и оповещения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-290">External events and alerts in SharePoint</span></span>](external-events-and-alerts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="14215-291">Как: создание добавить в пределах внешнего типа контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-291">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="14215-292">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-292">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="14215-293">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-293">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="14215-294">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-294">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="14215-295">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="14215-295">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

