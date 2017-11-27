---
title: "Создание службы данных OData для использования в качестве внешней системы BCS"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7d7b3aa6-85b7-400d-8ea5-50bebac56a1d
ms.openlocfilehash: 71c2397d1064746db45a55b05452352dc6c8ef5c
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="create-an-odata-data-service-for-use-as-a-bcs-external-system"></a>Создание службы данных OData для использования в качестве внешней системы BCS

Узнайте, как создать интернет-адресуемую службу WCF, которая использует OData для отправки уведомлений в SharePoint при изменении базовых данных. Эти уведомления используются для запуска событий, которые прикреплены ко внешним спискам.

В этой статье описывается создание службы данных ASP.NET Windows Communication Foundation (WCF) для предоставления образца базы данных AdventureWorks 2012 LT. Это позволяет получать доступ к данным посредством протокола Open Data protocol (OData). Если доступ установлено через OData, можно настроить Business Connectivity Services (BCS) внешнего типа контента, который будет включен SharePoint для использования данных из внешней базы данных. Для дальнейшего улучшения этого источника OData, можно добавить контракты службы для службы WCF, которая позволит BCS для подписки на уведомления, оповещающие об изменении внешних данных.
  
    
    


## <a name="prerequisites-for-creating-the-odata-service"></a>Необходимые условия для создания службы OData
<a name="bkmk_Prerequisites"> </a>

Создание службы OData в этой статье необходимо соблюдение следующих условий:
  
    
    

- Службы IIS сервера
    
  
- .NET Framework 3.5 или более поздней версии
    
  
- SharePoint
    
  
-  [Сценарий 20012 AdventureWorks LT](http://msftdbprodsamples.codeplex.com/releases/view/55330)
    
  
-  [LT данных AdventureWorks 2012 г.](http://msftdbprodsamples.codeplex.com/releases/view/55330)
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
Сведения о настройке среды разработки см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="core-concepts-for-creating-an-odata-service"></a>Основные понятия, которые создания службы OData

В таблице 1 приведены статьи, которые помогут вам понять основные концепции создания WCF службы с помощью OData и внешнее содержимое.
  
    
    

**В таблице 1. Основные понятия, которые создания службы OData**


|**Ресурс**|**Описание**|
|:-----|:-----|
| [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |Представлены сведения, которые помогут приступить к созданию внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office 2013 компонентов.  <br/> |
| [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |Узнайте, как использовать Visual Studio 2012 для обнаружения опубликованного источника OData и создать для повторного использования внешний тип контента для использования в BCS в SharePoint.  <br/> |
| [Open Data Protocol](http://www.odata.org) <br/> |Предоставляет сведения о протокола Open Data protocol, включая определения протокола, сведения о структуре и примеры их использования.  <br/> |
| [Обзор служб данных WCF](http://msdn.microsoft.com/en-us/library/cc668794.aspx) <br/> |WCF Службы данных включает создание и использование служб данных для веб-сайта или в интрасети с помощью OData. OData позволяет предоставлять данные как ресурсы, которые являются адресации с помощью URI.  <br/> |
| [Разработка и развертывание служб данных WCF](http://msdn.microsoft.com/en-us/library/gg258442) <br/> |Предоставляет сведения о разработке и развертывании WCF службы данных.  <br/> |
   

### <a name="steps-involved-in-creating-the-external-system"></a>Действия для создания внешней системы

Необходимо выполнить следующие действия 
  
    
    

- Установка образца базы данных AdventureWorks LT 2012 г.
    
  
- Создание службы OData
    
  
- Настройка разрешений на доступ
    
  
- Тестирование службы
    
  
- Добавление возможности для дополнительные функциональные возможности BCS
    
  

## <a name="installing-the-sample-database"></a>Установка образца базы данных
<a name="bkmk_Prerequisites"> </a>

Внешняя система обычно представляет собой базу данных и по этой причине в этом примере показано, как использовать образца базы данных AdventureWorks 2012 LT для представления собственный источник данных.
  
    
    
Следующие шаги будут 
  
    
    

## <a name="how-to-create-the-wcf-odata-service"></a>Как создать WCF службы OData
<a name="bkmk_CreatingTheService"> </a>

Создание службы Windows Communication Foundation (WCF), который может осуществляться через протокол OData относительно несложно. Visual Studio 2012 предоставляет несколько средств для автоматического обнаружения и моделирование данных из различных источников данных. Это позволяет создавать подключения и интерфейсы к данным в базах данных SQL Server и другие типы хранилищ данных, которые можно работать с программным путем с помощью обширную объектную модель.
  
    
    
Тем не менее для SharePoint для включения BCS для получения уведомлений из удаленных систем при изменении базовых данных, необходимо изменить службы WCF для ответа на такие изменения.
  
    
    

### <a name="to-create-a-new-wcf-project"></a>Чтобы создать проект на основе WCF


1. В Visual Studio, в меню **файл** выберите **Создать**, **проект**.
    
  
2. В диалоговом окне **Создать проект** выберите **веб-** шаблон и выберите **Веб-приложение ASP.NET**.
    
  
3. Введите **AdventureWorksService** для имени проекта и нажмите **кнопку ОК**.
    
  
4. В **Окне Обозреватель решений** откройте контекстное меню для проекта ASP.NET, который вы только что создали и выберите пункт **Свойства**.
    
  
5. Перейдите на вкладку **Web** и установите значение текстовое поле **конкретных портов**8008.
    
  

### <a name="to-define-the-data-model"></a>Чтобы определить модели данных


1. В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите команду **Добавить новый элемент**.
    
  
2. В диалоговом окне **Добавление нового элемента** выберите шаблон данных и выберите **Модель данных ADO.NET сущности**.
    
  
3. Имя модели данных введите **AdventureWorks.edmx**.
    
  
4. В окне **Мастера модели данных сущности** выберите **Создать из базы данных** и нажмите кнопку **Далее**.
    
  
5. Подключения к базе данных модели данных, выполнив одно из следующих действий и нажмите кнопку **Далее**.
    
  - Если у вас уже настроено подключение к базе данных, выберите **Новое подключение** и создайте новое подключение.
    
  
  - При наличии подключения к базе данных, уже настроена для подключения к базе данных Northwind, выберите это подключение в списке подключения.
    
  
  - На последней странице мастера установите флажки для всех таблиц в базе данных и снимите флажки для представлений и хранимых процедур.
    
  
6. Нажмите кнопку **Готово**, чтобы закрыть мастер.
    
  

### <a name="to-create-the-data-service"></a>Чтобы создать службу данных


1. В **Обозревателе решений** откройте контекстное меню для проекта ASP.NET и выберите команду **Добавить новый элемент**.
    
  
2. В диалоговом окне **Добавление нового элемента** выберите **Службы данных WCF**.
    
  
3. Имя службы введите **AdventureWorks**.
    
    Visual Studio создает XML-файлы разметки и кода для новой службы. По умолчанию откроется окно Редактор кода. В **Окне Обозреватель решений**, служба будет иметь имя **AdventureWorks** с расширением. svc.cs или. svc.vb.
    
  
4. Замените комментарий  `/* TODO: put your data source class name here */` в определение класса, который определяет службу данных с типом, который является контейнером сущностей в модели данных, который в данном случае является **AdventureWorksEntities**. Определения класса должен выглядеть следующим образом:
    
```cs
  
public class AdventureWorks : DataService<AdventureWorksEntities>
```

По умолчанию при создании службы WCF, он становится недоступной из-за его настройки безопасности. Следующий шаг позволяет указать пользователей, которые могут обращаться к ней и права у них.
  
    
    

### <a name="to-enable-access-to-data-service-resources"></a>Чтобы разрешить доступ к ресурсам службы данных


- В коде для службы данных замените заполнитель код в функцию **InitializeService** следующее.
    
```cs
  
      config.SetEntitySetAccessRule("*", EntitySetRights.All);
      config.SetServiceOperationAccessRule("*", ServiceOperationRights.All);
```


    This enables authorized clients to have read and write access to resources for the specified entity sets.
    
    > **Note:**
      > Any client that can access the ASP.NET application can also access the resources that are exposed by the data service. In a production data service, to prevent unauthorized access to resources, you should also secure the application itself. For more information, see  [Securing WCF Data Services](http://msdn.microsoft.com/en-us/library/dd728284.aspx). 
Для BCS для получения уведомлений должен быть механизм в источнике данных, которая будет принимать запрос для добавления и удаления из подписки на уведомления. 
  
    
    
На последнем этапе Создание службы является добавление операции службы для **Subscribe** и **Unsubscribe** стереотипов, определенных в модели BDC.
  
    
    

### <a name="to-add-service-operations-for-subscribe-and-unsubscribe-stereotypes"></a>Чтобы добавить операции службы для подписки на и отписаться стереотипов


- На странице AdventureWorks.cs добавьте следующее объявление переменной строки.
    
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


## <a name="next-steps"></a>Дальнейшие действия
<a name="bkmk_Next"> </a>

Для уведомления SharePoint, что были внесены изменения, необходимо создать служба, которая запрашивает источник данных для изменения, а затем отправляет уведомления для всех тех, подписка на уведомления.
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_Addresources"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Внешние события и оповещения в SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

