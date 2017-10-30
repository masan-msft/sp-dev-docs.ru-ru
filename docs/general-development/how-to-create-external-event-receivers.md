---
title: "Как создание приемников внешних событий"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6d5f486-6247-47f9-9876-fab12f13342f
ms.openlocfilehash: 638e2df70d22bd82a1f6eb0ba710515392642702
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-create-external-event-receivers"></a>Как: создание приемников внешних событий
Познакомьтесь с действиями для создания приемников внешних событий для локальных установок Службы Business Connectivity Services (BCS) внешних списков. Приемники событий внешнего являются классы, обеспечивающие Надстройки SharePoint для обработки событий, происходящих с объектами SharePoint, такие как списки или элементы списка. Например можно реагировать на события списка, такие как добавление или удаление поля; события элемента списка, такие как добавление или удаление элемента списка или вложения в элемент списка; или веб-события, такие как добавление или удаление сайта или семейства веб-сайтов. Удаленного приемника событий можно добавить в существующее решение Visual Studio, содержащий Надстройка SharePoint.
  
    
    

В этой статье описывается в образце кода [SharePoint: Создание удаленного приемника событий для внешних данных](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c). В этом примере показано создание все компоненты, необходимые для настройки и использования уведомлений о событиях внешней системы.
В этом примере выполните следующие действия.
  
    
    


1. Создание внешней системы на основании образце базы данных Northwind
    
  
2. Предоставление доступа к образца данных через OData, создав Windows Communication Foundation (WCF) службы.
    
  
3. Создание опроса служба, которая будет отслеживать изменения в данных и уведомить SharePoint эти изменения.
    
  
4. Создание приемника внешних событий, который выполняет, когда элементы добавляются к внешним данным и в результате создается новый элемент списка в список уведомлений.
    
  

## <a name="prerequisites-and-system-set-up"></a>Необходимые условия и настройка системы
<a name="bkmk_Prerequisites"> </a>

Для выполнения в этом примере, необходимо следующее:
  
    
    

- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2013
    
  
- SQL Server
    
  
- SharePoint
    
  
- Службы Internet Information Services 7.0
    
  
- Образец базы данных "Борей"
    
  

## <a name="build-the-components-for-external-systems"></a>Построение компонентов для внешних систем
<a name="BuildingTheComponents"> </a>

Максимальный часть конфигурации фактически происходит во внешней системе. Приемники событий внешнего правильной работы следующие компоненты должны иметь имеются во внешней системе.
  
    
    

- **Хранилища подписок:** Таблица, содержащая сведения о подписчиков, чтобы получать уведомления об изменениях к внешним данным.
    
  
- **Хранения изменений:** Таблица, которая используется для хранения изменений элементов данных. Работает как временное хранение только так, как службы опроса удаляет элемент в таблице, если уведомления отправляются подписчикам в SharePoint.
    
  
- **Опроса службы:** Требуется в этом сценарии, как средство проверки при была изменена и предоставленные изменить таблицу данных. Служба опроса запрос таблицы изменений и собирает пакет уведомлений, которое отправляется на адрес доставки SharePoint (конечная точка REST), хранящийся в хранилище подписки.
    
  
- **Службы данных OData WCF:** Представление данных из базы данных внешней системы, необходимо создать службы WCF. Эта служба на Internet Information Services (IIS), предоставляет интерфейс RESTful и канал OData, необходимые для этого сценария.
    
  

## <a name="set-up-the-external-system"></a>Настройка внешней системы
<a name="bkmk_SetUpTheExternalSystem"> </a>

Первая задача  настроить во внешней системе.
  
    
    

### <a name="attach-the-northwind-sample-database"></a>Присоединение образце базы данных Northwind

Первая часть Подготовка серверной системе заключается в добавлении образце базы данных Northwind запущенный экземпляр SQL Server. Если уже установлены образце базы данных Northwind, можно запустить скрипты в следующем разделе, чтобы создать дополнительные объекты, необходимые для внешних событий уведомлений для работы.
  
    
    
Если у вас нет данных "Борей" установлен, видеть  [Установка образца базы данных Northwind](http://msdn.microsoft.com/library/2f92cfc3-6310-4327-b2f2-8610f7385c86%28Office.15%29.aspx).
  
    
    
Базы данных включен в пример кода: [SharePoint: Создание удаленного приемника событий для внешних данных](http://code.msdn.microsoft.com/SharePoint-Create-a-095c594c).
  
    
    

### <a name="create-the-subscription-store"></a>Создание хранилища подписок

При установке базы данных Northwind, откройте новое окно запроса и выполните следующий скрипт.
  
    
    

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

Это создает таблицу в базе данных Northwind, с именем EntitySubscribe. Это служит в качестве хранилища подписок делается ссылка для более ранних версий.
  
    
    

### <a name="create-the-change-store"></a>Создание хранилища изменений

Выполните следующий скрипт, чтобы создать таблицу изменений, который будет записывать изменения данных в таблице Customers.
  
    
    

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

Это добавляет таблицу с именем Customers_Updates, в которой хранятся сведения о записи, который был добавлен к таблице Customers.
  
    
    

### <a name="create-the-change-trigger"></a>Создание изменение триггеров

Изменение триггера при изменения к таблице Customers. Запись при добавлении клиентов, SQL Server выполняется триггер, который вставляет новую запись в таблицу Customers_Updates со сведениями о записи.
  
    
    
Чтобы создать триггер, выполните следующий запрос.
  
    
    



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


> **Примечание:** При использовании пользовательских хранимых процедур, определенных в модели BDC можно также для создания, удаления и обновления триггеров. Дополнительные триггеров не рассматриваются как часть этого сценария. 
  
    
    


### <a name="create-the-stored-procedures"></a>Создайте хранимые процедуры

При использовании прямого доступа к таблицам с помощью служб Business Connectivity Services этих процедур не является необходимым. Тем не менее при определении собственных процедур и пользовательского кода во внешней системе, может потребоваться добавьте следующие инструкции о предоставлении доступа к таблице из SQL Server.
  
    
    

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

**SubscribeEntity** хранимые процедуры будет создать запись в хранилище данных подписки.
  
    
    



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


## <a name="create-the-odata-service"></a>Создание службы OData
<a name="bkmk_CreatingTheODataService"> </a>

Веб-канал OData размещается внутри **Службы данных WCF**. Эта служба WCF, затем, размещенным IIS в веб-приложении.
  
    
    
Следующие шаги создания новой службы данных ASP.NET WCF.
  
    
    

### <a name="to-create-the-wcf-data-service-application"></a>Создание приложения-службы данных WCF


1. В Visual Studio 2012 в меню **файл** выберите **Создать**, **проект**.
    
  
2. В диалоговом окне **Новый проект** разверните узел Visual C# и выберите **веб-** шаблон и выберите **Веб-приложение ASP.NET**.
    
  
3. Введите NorthwindService в качестве имени проекта и нажмите кнопку **ОК**.
    
  
Затем с помощью мастера Visual Studio, вы обнаружения схемы источника данных и используйте его для создания модели данных сущности ADO.NET.
  
    
    

### <a name="to-define-the-data-model"></a>Чтобы определить модели данных


1. В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите **Добавить новый элемент**.
    
  
2. В диалоговом окне **Добавление нового элемента** выберите шаблон **данных** и выберите **Модель данных ADO.NET сущности**.
    
  
3. Имя модели данных введите Northwind.edmx.
    
  
4. В мастере модели данных сущности выберите **Создать из базы данных** и нажмите кнопку **Далее**.
    
  
5. Подключения к базе данных модели данных, выполнив одно из следующих действий:
    
1. Если у вас уже настроено подключение к базе данных, выберите **Новое подключение** и создайте новое подключение. Дополнительные сведения можно [как: Создание подключения к базам данных SQL Server](http://msdn.microsoft.com/library/360c340d-e5a6-4a7e-a569-e95d500be43d%28Office.15%29.aspx). В этом экземпляре SQL Server должны иметь присоединенное образце базы данных Northwind. Нажмите кнопку **Далее**.
    
    -или-
    
  
2. При наличии подключения к базе данных, уже настроена для подключения к базе данных Northwind, выберите это подключение в списке подключения и нажмите кнопку **Далее**.
    
  
6. На последней странице мастера установите флажки для всех таблиц в базе данных и снимите флажки для представлений и хранимых процедур.
    
  
7. Нажмите кнопку **Готово**, чтобы закрыть мастер.
    
  
На следующем этапе создания фактической службы, размещенном в IIS, который будет предоставлять означает, что для доступа к внешним данным через представлений состояния (REST).
  
    
    

### <a name="to-create-the-wcf-data-service"></a>Создание службы данных WCF


1. В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите команду **Добавить новый элемент**.
    
  
2. В диалоговом окне **Добавление нового элемента** выберите **Службы данных WCF**.
    
  
3. Имя службы введите Northwind.
    
  
4. В примере кода для службы данных в определение класса, который определяет службу данных замените комментарий  `/* TODO: put your data source class name here */` тип, контейнер сущностей в модели данных, который в данном случае является `NorthwindEntities`. Определения класса должен выглядеть следующим образом.
    
```cs
  
public class Northwind : DataService<NorthwindEntities>

```


### <a name="to-set-the-security-on-the-service"></a>Настройка безопасности в службе


- Теперь необходимо изменить параметры безопасности, чтобы разрешить доступ к данным из веб-канал с внешним потребителей OData. При создании службы WCF, все отказано в доступе по умолчанию. Внесите следующие изменения в только что созданный класс.
    
```cs
  
config.SetEntitySetAccessRule("*", EntitySetRights.All);
config.SetServiceOperationAccessRule("*", ServiceOperationRights.All);
```


### <a name="create-the-subscribe-service-operation-optional"></a>Создайте операцию службы подписки на (необязательно)

Службы WCF также можно запрограммировать позволяют обрабатывать запросы подписки на и отказаться от SharePoint. Если вы решили создать пользовательские хранимые процедуры для приложения каждый обрабатывается операцией службы.
  
    
    
 **Подписки на**: Подпишитесь операция принимает запрос, отправляемый SharePoint и получает адрес доставки, тип события и сущность. Он также должен создать **subscriptionId** и затем записать все эти в таблице базы данных.
  
    
    



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


> **Примечание:** Если настроить SQL Server для проверки подлинности Windows, он будет пытаться проверки подлинности запроса с удостоверение пула приложений. Убедитесь в том, что учетную запись, настроенную в пуле приложений имеет права на чтение и запись в базу данных. 
  
    
    


## <a name="create-the-polling-service"></a>Создание опроса службы
<a name="bkmk_CreateThePollingService"> </a>

Опрос службы — это служба Windows, который несет ответственность за запрос таблицы изменений и создания и отправки уведомлений в SharePoint или SharePoint Online по адресу доставки.
  
    
    
Далее создайте новый проект службы Windows, который будет зарегистрирован на главном компьютере WCF. После регистрации проекта запущенной службы можно просматривать в консоли управления (MMC).
  
    
    

### <a name="to-create-a-new-project"></a>Создание нового проекта


1. Откройте Visual Studio 2012.
    
  
2. Создайте новый проект на основе шаблона службы Windows, назовите проект PollingServiceи нажмите кнопку « **ОК** ».
    
  
3. При создании проекта, откройте файл PollingService.cs в представлении кода.
    
  
4. Добавьте следующий код в только что созданный класс.
    
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

Следующим шагом является создание исполняемого файла, который можно добавить в запущенных служб на компьютере OData.
  
    
    

### <a name="to-compile-and-deploy-the-polling-service"></a>Чтобы скомпилировать и развернуть службу опроса


1. Нажмите клавишу F5, чтобы построить проект.
    
  
2. Откройте окно **командной строки для VS2012**.
    
  
3. В командной строке перейдите к папке выходных данных проекта.
    
  
4. В каталоге Bin найдите файл PollingService.exe.
    
  
5. Введите installutil PollingService.exe и нажмите клавишу ВВОД.
    
  
6. Убедитесь, что служба запуска путем выполнения служб консоли Управления.
    
  

## <a name="required-sharepoint-components"></a>Необходимые компоненты SharePoint
<a name="bkmk_SharePointComponents"> </a>

Для выполнения всей системы на сервере, на котором работает SharePoint необходимы следующие компоненты.
  
    
    

- **Внешнего типа контента:** Внешний тип контента по сути является определение XML из внешнего источника данных. Для этого сценария будет использовать новые средства Автоматическое формирование в Visual Studio 2012 для обнаружения источника данных и автоматически создать внешний тип контента.
    
  
- **Приемника внешних событий:** Приемник событий удаленного или внешнего является то, что позволяет действия на изменения внешних данных в SharePoint. Вы можете создать приемников событий для внешних списков и entities.
    
    Приемник событий, созданный для внешнего списка похож на другие приемники событий в списки SharePoint. Создание кода и подключить его в список. Когда действие, которое выполняется на данных, представленного списка, выполняет приемника событий.
    
    Приемника событий для сущностей выполняется так же, как приемник событий на основе списка, за исключением того, не подключенного к списку. Так же, как она получает уведомления, но она не требуется интерфейс, который связан с пример на основе списка. Это преимущество  можно программным путем перехвата уведомления и создавать код для выполнения некоторых действий. В этом сценарии это действие используется для создания новой записи в список уведомлений 
    
  
- **Список уведомлений:** Список уведомлений, простого списка SharePoint, который используется для записи уведомлений, полученных от внешней системы. Для каждой новой записи, добавлена к внешней системе запись будет создан в список уведомлений.
    
  

## <a name="set-up-the-sharepoint-components"></a>Настройка компонентов SharePoint
<a name="bkmk_SettingUpTheSharePointComponents"> </a>

Теперь, когда у вас есть внешней системы, Настройка, настало время перейти к созданию вторая уравнения. Теперь будет создавать компоненты для размещения в SharePoint.
  
    
    

### <a name="to-create-a-new-visual-studio-2012-project"></a>Создание нового проекта Visual Studio 2012


1. Выберите **Новый проект** в Visual Studio 2012.
    
  
2. Выберите шаблон проекта приложения SharePoint.
    
  
Инструменты разработчика Office для Visual Studio 2013 добавлена автоматическое формирование мастера будет обнаружение схемы в источнике данных, а затем создать внешний тип контента из того, что.
  
    
    

### <a name="to-add-a-new-external-content-type"></a>Чтобы добавить новый внешний тип контента


- В **Обозревателе решений** откройте контекстное меню для проекта и выберите команду **Добавить**, **Типов контента для внешнего источника данных**.
    
    Будет запущен **Мастер настройки SharePoint**, который используется для автоматического создания внешнего типа контента.
    
    Дополнительные сведения о том, как создать внешние типы контента можно [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).
    
  
Теперь будет использоваться для изменения XML, созданного на предыдущем шаге, чтобы добавить метод для подписки на. Это позволит BCS для связи с внешней системы, когда кто-то подписывается уведомлений об изменении внешних данных.
  
    
    

### <a name="to-add-the-subscribe-method-to-the-external-content-type-xml"></a>Добавление метода подписки на внешний тип контента XML


1. В **Обозревателе решений** найдите новый узел с именем **Внешних типов контента**.
    
  
2. Найдите файл **Customers.ect** и откройте его с помощью редактора XML.
    
  
3. Прокрутите список вниз до конца страницы и вставьте следующий метод в разделе  `<Methods>` .
    
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

Теперь добавим код клиента, позволяющие списке, чтобы подписаться на уведомления о событиях.
  
    
    

### <a name="to-add-code-to-the-appjs-file-to-initiate-the-subscription"></a>Добавление кода в файл App.js для инициации подписки


- В папке Scripts Надстройка SharePoint проекта откройте файл **App.js**. Вставьте следующий метод в файл.
    
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

Чтобы зарегистрировать приемника событий с помощью этого сценария, необходимо создать кнопку на страницу Default.aspx в вашем проекте и вызовите **SubscribeEntity()** из метода **onclick()**.
  
    
    

- Откройте страницу Default.aspx и добавьте следующий HTML-код.
    
```HTML
  
<input type="button" value="Subscribe" onclick="SubscribeEntity();"/>
```

Для регистрации событий для работы необходимо также включить списка SharePoint для принятия внешние события. Для этого, включите функцию внешние события.
  
    
    
Ниже приведен сценарий, который будет включен компонент с помощью клиентского кода.
  
    
    



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

Так же, как с помощью **Subscribe**добавляется кнопка на страницу, которая будет включена функция.
  
    
    
Добавьте следующий HTML-код на страницу Default.aspx непосредственно под кнопкой **подписаться**.
  
    
    



```HTML

<input type="button" value="EnableEventing" onclick="EnableEventing_Clicked();"" />
```

Рассмотрим процедуру для этого сценария необходимо добавить список уведомлений, которое будет показывать уведомления, отправляемые внешней системой.
  
    
    

### <a name="to-add-the-notifications-list"></a>Чтобы добавить список уведомлений


1. В **Обозревателе решений** откройте контекстное меню для имени проекта и нажмите кнопку **Добавить**.
    
  
2. Выберите шаблон **списка** и имя спискаNotificationList.
    
  
Имитация приемника событий, который зарегистрирован с помощью SharePoint в глобальном кэше сборок, в примере задаются консольное приложение, которое будет запущен процесс прослушивание изменений. При получении уведомления, **NotificationList**добавляет элемент списка.
  
    
    

### <a name="to-start-the-command-line-event-receiver"></a>Чтобы запустить приемника событий командной строки


1. Откройте **RemoteEventReceiverConsoleApp**.
    
  
2. Откройте файл **Program.cs** и измените имя на локальный компьютер (или компьютере с запущенным приемника событий).
    
  
3. В Visual Studio для запуска консольного приложения, нажмите кнопку **Пуск**.
    
    Откроется окно командной строки, который указывает, что приложение было выполнено успешно и прослушивает уведомления об изменении из внешней системы. Не закрывайте это окно во время этой проверки.
    
  

### <a name="to-deploy-the-app-to-sharepoint"></a>Чтобы развернуть приложение для SharePoint


- Нажмите клавишу F5, с помощью Visual Studio откройте построение и развертывание приложения.
    
  

## <a name="test-the-app"></a>Тестирование приложения
<a name="bkmk_testApp"> </a>

Теперь можно видеть приложения в действии.
  
    
    

1. Обзор вокруг приложение, чтобы просмотреть различные списки, которые представляют данные во внешней системе.
    
  
2. Щелкните список **клиентов**.
    
  
3. Добавление нового клиента.
    
  
4. Просмотр нового элемента списка, который вы только что создали.
    
  
5. Перейдите к списку уведомления, чтобы увидеть, что во внешней системе уведомил SharePoint внесение изменений в таблице Customers.
    
    Имейте в виду, таймера задано значение отправлять уведомления каждую минуту. Во время тестирования, может потребоваться ожидания короткого периода, прежде чем Просмотр персональных уведомления.
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_additionalresources"> </a>


-  [Внешние события и оповещения в SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Как: создание добавить в пределах внешнего типа контента в SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  

