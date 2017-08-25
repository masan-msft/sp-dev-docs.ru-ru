# <a name="handle-list-item-events-in-the-provider-hosted-add-in"></a><span data-ttu-id="4c490-101">Обработка событий элементов списков в надстройке, размещаемой у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-101">Handle list item events in the provider-hosted add-in</span></span>
<span data-ttu-id="4c490-102">В этой статье рассказывается, как обрабатывать события элементов списка для надстройки SharePoint, размещаемой у поставщика.</span><span class="sxs-lookup"><span data-stu-id="4c490-102">Learn how to handle list item events in a provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="4c490-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="4c490-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="4c490-p102">Это десятая часть серии статей, посвященной основам разработки надстроек, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="4c490-p102">Learn how to handle list item events in a provider-hosted SharePoint Add-in. This is the tenth in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="4c490-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="4c490-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [<span data-ttu-id="4c490-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="4c490-111">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c490-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [<span data-ttu-id="4c490-112">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-112">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="4c490-113">Добавление веб-части надстройки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-113">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="4c490-114">Обработка событий надстройки, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-114">Handle add-in events in the provider-hosted add-in</span></span>](handle-add-in-events-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="4c490-115">Добавление логики, выполняемой при первом запуске, в надстройку, размещаемую у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-115">Add first-run logic to the provider-hosted add-in</span></span>](add-first-run-logic-to-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="4c490-116">Программное развертывание настраиваемой кнопки в надстройке, размещаемой у поставщика</span><span class="sxs-lookup"><span data-stu-id="4c490-116">Programmatically deploy a custom button in the provider-hosted add-in</span></span>](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in)
    
 

 <span data-ttu-id="4c490-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeRER.sln.</span><span class="sxs-lookup"><span data-stu-id="4c490-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeRER.sln file.</span></span>
 

<span data-ttu-id="4c490-p104">В одной из предыдущих статей этой серии мы рассказывали, что при размещении заказа он добавляется в таблицу **Orders** (Заказы) в корпоративной базе данных, а соответствующий ему элемент автоматически добавляется в список **Expected Shipments** (Ожидаемые отгрузки). Когда заказ прибывает в местный магазин, пользователь указывает в столбце **Arrived** (Прибыл) значение **Yes** (Да). При изменении значения поля для элемента создается событие обновления элемента, для которого можно добавить настраиваемый обработчик. Изучая данную статью, вы создадите обработчик этого события элемента списка, а затем программным способом развернете его в коде, выполняемом во время первого запуска надстройки SharePoint. Обработчик добавит элемент в таблицу **Inventory** (Запасы) корпоративной базы данных. Затем он задаст в столбце **Added to Inventory** (Добавлен в запасы) списка **Expected Shipments** (Ожидаемые отгрузки) значение **Yes** (Да). Кроме того, вы узнаете, как не допустить, чтобы второе событие обновления элемента создало бесконечный ряд новых событий обновления элемента.</span><span class="sxs-lookup"><span data-stu-id="4c490-p104">You saw in an earlier article in this series that when an order is placed, it is added to the **Orders** table in the corporate database and an item for it is automatically added to the **Expected Shipments** list. When it arrives at the local store, a user sets the **Arrived** column to **Yes**. Changing a field value for an item creates an item updated event for which you can add a custom handler. In this article, you will create a handler for this list item event and then programmatically deploy it in the first-run logic of the SharePoint Add-in. Your handler will add the item into the **Inventory** table in the corporate database. It will then set the **Added to Inventory** column of the **Expected Shipments** list to **Yes**. You will also learn how to prevent this second item updated event from setting off an infinite series of item updated events.</span></span>
 

## <a name="programmatically-deploy-the-expected-shipments-list"></a><span data-ttu-id="4c490-126">Программное развертывание списка Expected Shipments (Ожидаемые отгрузки)</span><span class="sxs-lookup"><span data-stu-id="4c490-126">Programmatically deploy the Expected Shipments list</span></span>


 <span data-ttu-id="4c490-p105">**Примечание.** При повторном открытии решения параметры раздела "Начальные проекты" в Visual Studio обычно сбрасываются к значениям, используемым по умолчанию. Сразу же после повторного открытия примера решения в этой серии статей всегда выполняйте указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4c490-p105">**Note** The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span>
 


1. <span data-ttu-id="4c490-p106">В **обозревателе решений** откройте файл Utilities\SharePointComponentDeployer.cs в проекте **ChainStoreWeb**. Добавьте указанный ниже метод в класс `SharePointComponentDeployer`. В этом коде нет новых возможностей, которых не было в предыдущей статье этой серии, но следует обратить внимание на указанные ниже моменты.</span><span class="sxs-lookup"><span data-stu-id="4c490-p106">In **Solution Explorer**, open the UtilitiesSharePointComponentDeployer.cs file in the **ChainStoreWeb** project. Add the following method to the `SharePointComponentDeployer` class. This code doesn't introduce any functionality that you haven't already seen in a previous article of this series, but note the following:</span></span>
    
      - <span data-ttu-id="4c490-p107">Код присваивает атрибуту **Required** (Обязательный) поля **Quantity** (Количество) значение **TRUE** (Истина), поэтому это поле всегда должно иметь значение. Затем он задает число 1 в качестве значения, используемого по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4c490-p107">It sets the **Required** attribute of the **Quantity** field to **TRUE** so the field must always have a value. It then sets the default value to 1.</span></span>
    
 
  - <span data-ttu-id="4c490-134">В форме New Item (Новый элемент) поля **Arrived** (Прибыл) и **Added to Inventory** (Добавлен в запасы) скрыты.</span><span class="sxs-lookup"><span data-stu-id="4c490-134">The **Arrived** and **Added to Inventory** fields are hidden on the New Item form.</span></span>
    
 
  - <span data-ttu-id="4c490-p108">В идеальном случае в форме Edit Item (Изменение элемента) поле **Added to Inventory** (Добавлен в запасы) тоже должно быть скрыто, так как его значение следует изменить на **Yes** (Да) только тогда, когда обработчик события обновления элемента в первый раз добавит элемент в корпоративную таблицу **Inventory** (Запасы). По техническим причинам, о которых мы расскажем на одном из следующих этапов, это поле должно отображаться в форме Edit Item (Изменение элемента), если нам необходимо программным способом записывать в него данные из обработчика события обновления элемента.</span><span class="sxs-lookup"><span data-stu-id="4c490-p108">Ideally, the **Added to Inventory** field would also be hidden on the Edit Item form, because it should only be changed to **Yes** when the item updated event handler has first added the item to the corporate **Inventory** table. For technical reasons that we'll explain in a later step, a field has to be visible in the Edit Item form, if we want to programmatically write to it in an item updated event handler.</span></span>
    
 

```C#
  private static void CreateExpectedShipmentsList()
 {
    using (var clientContext = sPContext.CreateUserClientContextForSPHost())
    {
        var query = from list in clientContext.Web.Lists
                    where list.Title == "Expected Shipments"
                    select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();
                   
        if (matchingLists.Count() == 0)
        {
                ListCreationInformation listInfo = new ListCreationInformation();
                listInfo.Title = "Expected Shipments";
                listInfo.TemplateType = (int)ListTemplateType.GenericList;
                listInfo.Url = "Lists/ExpectedShipments";
                List expectedShipmentsList = clientContext.Web.Lists.Add(listInfo);

                Field field = expectedShipmentsList.Fields.GetByInternalNameOrTitle("Title");
                field.Title = "Product";
                field.Update();

                expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Supplier'" 
                                                            + " Type='Text' />", 
                                                            true,
                                                            AddFieldOptions.DefaultValue);
                expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Quantity'" 
                                                            + " Type='Number'" 
                                                            + " Required='TRUE' >" 
                                                            + "<Default>1</Default></Field>",
                                                            true, 
                                                            AddFieldOptions.DefaultValue);
                expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Arrived'" 
                                                           + " Type='Boolean'"
                                                           + " ShowInNewForm='FALSE'>"
                                                           + "<Default>FALSE</Default></Field>",
                                                            true, 
                                                            AddFieldOptions.DefaultValue);
                expectedShipmentsList.Fields.AddFieldAsXml("<Field DisplayName='Added to Inventory'" 
                                                            + " Type='Boolean'" 
                                                            + " ShowInNewForm='FALSE'>"
                                                            + "<Default>FALSE</Default></Field>", 
                                                            true, 
                                                            AddFieldOptions.DefaultValue);

                clientContext.ExecuteQuery();
        }
     }
 }
```

2. <span data-ttu-id="4c490-137">В методе `DeployChainStoreComponentsToHostWeb` добавьте указанную ниже строку (сразу же после строки `RemoteTenantVersion = localTenantVersion`).</span><span class="sxs-lookup"><span data-stu-id="4c490-137">In the  `DeployChainStoreComponentsToHostWeb` method, add the following line, just above the line `RemoteTenantVersion = localTenantVersion`.</span></span>
    
```
  CreateExpectedShipmentsList();
```


## <a name="create-the-list-item-event-receiver"></a><span data-ttu-id="4c490-138">Создание приемника событий элемента списка</span><span class="sxs-lookup"><span data-stu-id="4c490-138">Create the list item event receiver</span></span>


 <span data-ttu-id="4c490-p109">**Примечание.** Если вы работали со статьями этой серии, то, вероятно, уже настроили собственную среду разработки для отладки удаленных приемников событий. Если вы еще не сделали этого, то прежде чем перейти к другим разделам данной статьи, прочитайте раздел [Настройка решения для отладки приемника событий](handle-add-in-events-in-the-provider-hosted-add-in#RERDebug).</span><span class="sxs-lookup"><span data-stu-id="4c490-p109">**Note** If you have been working through this series of articles, then you have already configured your development environment for debugging remote event receivers. If you have not done that, see  [Configure the solution for event receiver debugging](handle-add-in-events-in-the-provider-hosted-add-in#RERDebug) before you go any further in this topic.</span></span>
 

<span data-ttu-id="4c490-p110">Пакет Инструменты разработчика Office для Visual Studio включает элемент **Удаленный приемник событий**, который можно добавить в решение надстройки SharePoint. На момент написания данной статьи предполагается, что для этого элемента проекта список (для которого будет зарегистрирован приемник) находится на сайте надстройки и, соответственно, пакет инструментов создает сайт надстройки, а также ряд артефактов SharePoint в нем. Кроме того, предполагается, что приемник для надстройки Chain Store будет зарегистрирован (на одном из следующих этапов) для списка **Expected Shipments** (Ожидаемые отгрузки) на хост-сайте, поэтому для надстройки не требуется сайт надстройки. (Сведения о различиях между сайтами надстроек и хост-сайтами см. в статье [Надстройки SharePoint](sharepoint-add-ins).)</span><span class="sxs-lookup"><span data-stu-id="4c490-p110">The Office Developer Tools for Visual Studio include a **Remote Event Receiver** item that can be added to a SharePoint Add-in solution. However, at the time this article was written, this project item assumes that the list (with which the receiver will be registered) is on the add-in web, and consequently the tools create an add-in web and some SharePoint artifacts in it. But the receiver for the Chain Store add-in is going to be registered (in a later step) with the **Expected Shipments** list on the host web, so the add-in does not need an add-in web. (For a reminder of the distinction between add-in webs and host webs, see [SharePoint Add-ins](sharepoint-add-ins).)</span></span>
 

 

 <span data-ttu-id="4c490-p111">**Примечание.** Приемники событий списка и элементов списка называются удаленными приемниками событий, так как их код является удаленным по отношению к SharePoint и размещен либо в облаке, либо на локальном сервере за пределами фермы SharePoint. Тем не менее события, запускающие их, находятся в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c490-p111">**Note** List and list item event receivers are called remote event receivers (RER) because their code is remote from SharePoint, either in the cloud or in an on-premises server outside the SharePoint farm. However, the events that trigger them are in SharePoint.</span></span>
 


1. <span data-ttu-id="4c490-147">В **обозревателе решений** щелкните правой кнопкой мыши папку **Службы** в проекте **ChainStoreWeb** и выберите **Добавить | Служба WCF**.</span><span class="sxs-lookup"><span data-stu-id="4c490-147">In **Solution Explorer**, right-click the **Services** folder in the **ChainStoreWeb** project and select **Add | WCF Service**.</span></span>
    
 
2. <span data-ttu-id="4c490-148">Когда отобразится соответствующий запрос, укажите для службы имя RemoteEventReceiver1, а затем нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c490-148">When prompted, name the service RemoteEventReceiver1, and then press **OK**.</span></span> 
    
 
3. <span data-ttu-id="4c490-p112">Пакет средств создаст SVC-файл интерфейса и файл кода программной части. Нам не потребуется файл интерфейса IRemoteEventReceiver1.cs, поэтому удалите его. (Возможно, пакет средств открыл его автоматически. В этом случае закройте файл, а затем удалите его.)</span><span class="sxs-lookup"><span data-stu-id="4c490-p112">The tools create an interface file, a *.svc file, and a code behind file. We don't need the interface file IRemoteEventReceiver1.cs, so delete it. (The tools may have opened it automatically. If so, close and delete it.)</span></span>
    
     <span data-ttu-id="4c490-p113">**Примечание.** Когда вы создавали приемники событий надстройки для событий установки и удаления в одной из предыдущих статей данной серии, пакет Инструменты разработчика Office для Visual Studio добавлял их URL-адреса в файл манифеста приложения. Приемники событий списка и элемента списка не зарегистрированы в манифесте приложения. Их необходимо зарегистрировать программным способом (в надстройке, размещаемой у поставщика). Вы сделаете это на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="4c490-p113">**Note** When you created the add-in event receivers for the installed and uninstalling events in an earlier article in this series, the Office Developer Tools for Visual Studio added their URLs to the app manifest file. List and list item event receivers are not registered in the app manifest. Instead, they are registered (in a provider-hosted add-in) programmatically. You'll do that in a later step.</span></span>
4. <span data-ttu-id="4c490-p114">Откройте файл с выделенным кодом RemoteEventReceiver1.svc.cs. Замените все его содержимое указанным ниже кодом. Обратите внимание на указанные ниже особенности кода.</span><span class="sxs-lookup"><span data-stu-id="4c490-p114">Open the code behind file: RemoteEventReceiver1.svc.cs. Replace its entire contents with the following code. Note the following about this code:</span></span>
    
      - <span data-ttu-id="4c490-160">Интерфейс `IRemoteEventService` определен в пространстве имен **Microsoft.SharePoint.Client.EventReceivers**.</span><span class="sxs-lookup"><span data-stu-id="4c490-160">The interface  `IRemoteEventService` is defined in the **Microsoft.SharePoint.Client.EventReceivers** namespace.</span></span>
    
 
  - <span data-ttu-id="4c490-161">В надстройке Chain Store не будут обрабатываться события, возникающие до выполнения действий, но метод **ProcessEvent** является обязательным для интерфейса `IRemoteEventService`.</span><span class="sxs-lookup"><span data-stu-id="4c490-161">There won't be any "before" events handled in the Chain Store add-in, but the **ProcessEvent** method is required by the `IRemoteEventService` interface.</span></span>
    
 

```C#
  using System;
using System.Collections.Generic;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.EventReceivers;
using System.Data.SqlClient;
using System.Data;
using ChainStoreWeb.Utilities;

namespace ChainStoreWeb.Services
{
    public class RemoteEventReceiver1 : IRemoteEventService
    {
        /// <summary>
        /// Handles events that occur before an action occurs, 
        /// such as when a user is adding or deleting a list item.
        /// </summary>
        /// <param name="properties">Holds information about the remote event.</param>
        /// <returns>Holds information returned from the remote event.</returns>
        public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {
            throw new NotImplementedException();
        }

        /// <summary>
        /// Handles events that occur after an action occurs, 
        /// such as after a user adds an item to a list or deletes an item from a list.
        /// </summary>
        /// <param name="properties">Holds information about the remote event.</param>
        public void ProcessOneWayEvent(SPRemoteEventProperties properties)
        {

        }
    }
}
```

5. <span data-ttu-id="4c490-p115">Добавьте указанный ниже код в метод  `ProcessOneWayEvent`. Обратите внимание, что **ItemUpdated** единственное событие, которое будет обрабатываться в данном примере, поэтому вместо оператора **switch** можно использовать простую структуру **if**. Приемники событий обычно обрабатывают несколько событий, поэтому желательно, чтобы вы изучили шаблон, который вы (как разработчик надстроек SharePoint) чаще всего будете использовать в своих обработчиках событий.</span><span class="sxs-lookup"><span data-stu-id="4c490-p115">Add the following code to the  `ProcessOneWayEvent` method. Note that the **ItemUpdated** event is the only one that this sample will handle, so we could have used a simple **if** structure instead of a **switch**. But event receivers typically handle multiple events, so we want you to see the pattern you'll most commonly be using in your event handlers as a SharePoint add-in developer.</span></span>
    
```C#
  switch (properties.EventType)
{
    case SPRemoteEventType.ItemUpdated:

        // TODO12: Handle the item updated event.
                    
        break;
}  
```

6. <span data-ttu-id="4c490-p116">Замените  `TODO12` указанным ниже кодом. Здесь мы опять используем структуру **switch** в случае, когда достаточно использовать простую структуру **if**. Мы делаем это, чтобы показать вам стандартный шаблон, используемый в приемниках событий SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4c490-p116">Replace  `TODO12` with the following code. Again, here, we are using a **switch** structure when a simple **if** structure would do, because we want you to see the common pattern in SharePoint event receivers.</span></span>
    
```C#
  switch (properties.ItemEventProperties.ListTitle)
{
    case "Expected Shipments":

        // TODO13: Handle the arrival of a shipment.

        break;
}
```

7. <span data-ttu-id="4c490-167">Код, который реагирует на прибытие отгруженного товара, должен выполнять два указанных ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4c490-167">The code that responds to the arrival of a shipment should do two things:</span></span>
    
      - <span data-ttu-id="4c490-168">Добавьте элемент, который прибыл в магазин, в корпоративные запасы.</span><span class="sxs-lookup"><span data-stu-id="4c490-168">Add the item that has arrived at the store into the corporate inventory.</span></span>
    
 
  - <span data-ttu-id="4c490-p117">В списке **Expected Shipments** (Ожидаемые загрузки) в поле **Added to Inventory** (Добавлен на склад) укажите значение **Yes** (Да). Но это следует сделать, только если элемент успешно добавлен в запасы.</span><span class="sxs-lookup"><span data-stu-id="4c490-p117">Set the **Added to Inventory** field on the **Expected Shipments** list to **Yes**. But this should only happen if the item was successfully added to the inventory.</span></span>
    
 

    <span data-ttu-id="4c490-p118">Добавьте указанный ниже код вместо `TODO13`. Методы `TryUpdateInventory` и `RecordInventoryUpdateLocally` мы создадим в следующих действиях.</span><span class="sxs-lookup"><span data-stu-id="4c490-p118">Add the following code in place of  `TODO13`. The two methods,  `TryUpdateInventory` and `RecordInventoryUpdateLocally` are created in later steps.</span></span>
    


```C#
  bool updateComplete = TryUpdateInventory(properties);
if (updateComplete)
{
    RecordInventoryUpdateLocally(properties);
}
```


    The  `ProcessOneWayEvent` method should now look like the following:
    


```C#
  public void ProcessOneWayEvent(SPRemoteEventProperties properties)
{
    switch (properties.EventType)
    {
        case SPRemoteEventType.ItemUpdated:

            switch (properties.ItemEventProperties.ListTitle)
            {
                case "Expected Shipments":
                    bool updateComplete = UpdateInventory(properties);
                    if (updateComplete)
                    {
                        RecordInventoryUpdateLocally(properties);
                    }
                    break;
            }
            break;
    }          
}
```

8. <span data-ttu-id="4c490-173">Добавьте указанный ниже метод в класс `RemoteEventReceiver1`.</span><span class="sxs-lookup"><span data-stu-id="4c490-173">Add the following method to the  `RemoteEventReceiver1` class.</span></span>
    
```C#
  private bool TryUpdateInventory(SPRemoteEventProperties properties)
{
    bool successFlag = false;

        // TODO14: Test whether the list item is changing because the product has arrived
        // or for some other reason. If the former, add it to the inventory and set the success flag
        // to true.     

    return successFlag;
}
```

9. <span data-ttu-id="4c490-p119">В списке **Expected Shipments** (Ожидаемые отгрузки) имеется пять столбцов, но нам не нужно, чтобы обработчик реагировал на большинство видов обновлений элемента. Например, если пользователь исправляет написание названия поставщика, возникает событие обновления элемента, но при этом наш обработчик не должен ничего делать. Он должен действовать только тогда, когда полю **Arrived** (Прибыл) присваивается значение **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="4c490-p119">There are five columns on the **Expected Shipments** list, but we don't want to the handler to react to most kinds of updates to an item. For example, if a user corrects the spelling of a supplier's name, the item updated event is triggered, but our handler should do nothing. The handler should only act when the **Arrived** field has just been set to **Yes**.</span></span> 
    
    <span data-ttu-id="4c490-p120">Есть еще одно условие, которое необходимо проверять. Предположим, что поле **Arrived** (Прибыл) имеет значение **Yes** (Да), а продукт в элементе добавлен в запасы (соответственно, поле **Added to Inventory** [Добавлен в запасы] имеет значение **Yes**[Да]). Но позже пользователь по ошибке изменяет значение поля **Arrived** (Прибыл) для отгрузки обратно на **No** (Нет), а затем исправляет свою ошибку, снова присвоив полю значение **Yes** (Да). И ошибка, и ее исправление создают событие обновления элемента. Обработчик не будет реагировать на ошибку, так как он срабатывает только если полю **Arrived** (Прибыл) присваивается значение **Yes** (Да). Обработчик среагирует на исправление, при котором полю **Arrived** (Прибыл) снова будет присвоено значение **Yes** (Да). Из-за этого один и тот же продукт в одном и том же количестве будет еще раз добавлен в запасы. Поэтому обработчик должен срабатывать, только когда поле **Added to Inventory** (Добавлен в запасы) имеет значение **No** (Нет).</span><span class="sxs-lookup"><span data-stu-id="4c490-p120">There's another condition that needs to be tested. Suppose **Arrived** is set to **Yes** and the product in the item is added to inventory (and **Added to Inventory** is set to **Yes**). But later a user mistakenly changes the **Arrived** field of a shipment back to **No** and then fixes his mistake by setting it again to **Arrived**. Both the mistake and the fix, trigger the item updated event. The handler won't react to the mistake because it only acts when **Arrived** is **Yes**, but it would react to the fix that sets **Arrived** back to **Yes**, so the same product and quantity would get added into the inventory a second time. For this reason, the handler should only act when the **Added to Inventory** value is **No**.</span></span> 
    
    <span data-ttu-id="4c490-p121">Таким образом, обработчику необходимо "знать" значения этих полей сразу же после того как пользователь обновит элемент. У объекта **SPRemoteEventProperties** есть свойство **ItemEventProperties**. В свою очередь, у этого свойства имеется индексированное свойство **AfterProperties**, в котором хранятся значения полей обновленного элемента. В коде ниже эти свойства используются для проверки того, необходимо ли срабатывать обработчику. Вставьте этот код вместо `TODO14`.</span><span class="sxs-lookup"><span data-stu-id="4c490-p121">So the handler needs to know what the values of these fields are just after the user updates the item. The **SPRemoteEventProperties** object has an **ItemEventProperties** property. And, in turn, it has an indexed **AfterProperties** property that holds the values of the fields in the updated item. The following code uses these properties to test whether the handler should react. Put this in place of `TODO14`.</span></span>
    


```C#
  var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

if (arrived &amp;&amp; !addedToInventory)
{

    // TODO15: Add the item to inventory

    successFlag = true;
}
```

10. <span data-ttu-id="4c490-p122">Замените `TODO15` указанным ниже кодом. Здесь в основном используется программирование для SQL и ASP.NET, и мы не будем подробно рассматривать его, но при этом учтите указанные ниже моменты.</span><span class="sxs-lookup"><span data-stu-id="4c490-p122">Replace  `TODO15` with the following code. This is mainly SQL and ASP.NET programming, so we don't discuss it in detail, but note:</span></span>
    
      - <span data-ttu-id="4c490-190">Мы используем свойство **ItemEventProperties.WebUrl**, чтобы получить имя клиента, представляющее собой URL-адрес хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="4c490-190">We use the **ItemEventProperties.WebUrl** property to get the tenant name, which is the host web URL.</span></span>
    
 
  - <span data-ttu-id="4c490-191">Мы еще раз используем **AfterProperties**, чтобы получить значения имени и количества продукта.</span><span class="sxs-lookup"><span data-stu-id="4c490-191">We use the **AfterProperties** again to get the values of the product name and quantity.</span></span>
    
 
  - <span data-ttu-id="4c490-192">Мы ссылаемся на поле имени продукта, используя имя Title (Название), даже несмотря на то, что в методе  `CreateExpectedShipmentsList` отображаемое имя было изменено на Product (Продукт), так как для ссылки на поля всегда используются внутренние имена полей.</span><span class="sxs-lookup"><span data-stu-id="4c490-192">We refer to the product name field as "Title", even though the display name was changed to "Product" (in the  `CreateExpectedShipmentsList` method) because fields are always referred to by their internal names.</span></span>
    
 

```C#
  using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
using (SqlCommand cmd = conn.CreateCommand())
{
    conn.Open();
    cmd.CommandText = "UpdateInventory";
    cmd.CommandType = CommandType.StoredProcedure;
    SqlParameter tenant = cmd.Parameters.Add("@Tenant", SqlDbType.NVarChar);
    tenant.Value = properties.ItemEventProperties.WebUrl + "/";
    SqlParameter product = cmd.Parameters.Add("@ItemName", SqlDbType.NVarChar, 50);
    product.Value = properties.ItemEventProperties.AfterProperties["Title"]; // not "Product"
    SqlParameter quantity = cmd.Parameters.Add("@Quantity", SqlDbType.SmallInt);
    quantity.Value = Convert.ToUInt16(properties.ItemEventProperties.AfterProperties["Quantity"]);
    cmd.ExecuteNonQuery();
}
```


    We are not finished with the  `TryUpdateInventory` method yet, but at this point it should look like the following.
    


```C#
  private bool TryUpdateInventory(SPRemoteEventProperties properties)
{
    bool successFlag = false;

    var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
    var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

    if (arrived &amp;&amp; !addedToInventory)
    {
        using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
        using (SqlCommand cmd = conn.CreateCommand())
        {
            conn.Open();
            cmd.CommandText = "UpdateInventory";
            cmd.CommandType = CommandType.StoredProcedure;
            SqlParameter tenant = cmd.Parameters.Add("@Tenant", SqlDbType.NVarChar);
            tenant.Value = properties.ItemEventProperties.WebUrl + "/";
            SqlParameter product = cmd.Parameters.Add("@ItemName", SqlDbType.NVarChar, 50);
            product.Value = properties.ItemEventProperties.AfterProperties["Title"]; // not "Product"
            SqlParameter quantity = cmd.Parameters.Add("@Quantity", SqlDbType.SmallInt);
            quantity.Value = Convert.ToUInt16(properties.ItemEventProperties.AfterProperties["Quantity"]);
            cmd.ExecuteNonQuery();
        }            
        successFlag = true;
    }  
    return successFlag;
}
```

11. <span data-ttu-id="4c490-p123">Когда метод `TryUpdateInventory` возвращает значение **true** (Истина), наш обработчик вызывает (еще не написанный) метод, который обновляет тот же элемент в списке **Expected Shipments** (Ожидаемые отгрузки), задавая для поля **Added to Inventory** (Добавлен в запасы) значение **Yes** (Да). Он представляет собой событие обновления элемента, поэтому обработчик будет вызван еще раз. (Так как теперь поле **Added to Inventory** [Добавлен в запасы] имеет значение **Yes** [Да], обработчик не будет еще раз добавлять одну и ту же отгрузку на склад, но он будет вызван.)</span><span class="sxs-lookup"><span data-stu-id="4c490-p123">When the  `TryUpdateInventory` method returns **true**, our handler will call a method (not yet written) that will update the same item in the **Expected Shipments** list by setting the **Added to Inventory** field to **Yes**. This is itself a item update event, so the handler will be called again. (The fact that the **Added to Inventory** field is now **Yes**, will prevent the handler from adding the same shipment to inventory a second time, but the handler is still called.)</span></span> 
    
    <span data-ttu-id="4c490-p124">Когда событие обновления элемента возникает вследствие обновления программным путем, SharePoint ведет себя немного по-другому: *он включает (в **AfterProperties**) только те поля, которые были изменены при обновлении.* Таким образом, поле **Arrived** (Прибыл) будет отсутствовать, так как было изменено только поле **Added to Inventory** (Добавлен в запасы). При выполнении строки</span><span class="sxs-lookup"><span data-stu-id="4c490-p124">But SharePoint behaves a little differently when the item updated event is triggered by a programmatic update:  *it only includes, in the **AfterProperties**, the fields that changed in the update.*  So, the **Arrived** field won't be present, since only the **Added to Inventory** field changed. The line --</span></span>
    
     `var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);`
    
     <span data-ttu-id="4c490-199">возникнет исключение **KeyNotFoundException**.</span><span class="sxs-lookup"><span data-stu-id="4c490-199">-- will throw a **KeyNotFoundException**.</span></span> 
    
    <span data-ttu-id="4c490-p125">Существует несколько способов решения этой проблемы. В данном примере мы собираемся перехватить исключение и использовать блок **catch**, чтобы присвоить параметру `successFlag` значение **false** (Ложь). Благодаря этому элемент не будет обновлен в третий раз.</span><span class="sxs-lookup"><span data-stu-id="4c490-p125">There is more than one way to resolve this problem. In this sample we are going to catch the exception and use the **catch** block to ensure that the `successFlag` is set to **false**. Doing this ensures that the item isn't updated a third time.</span></span>
    
    <span data-ttu-id="4c490-203">Добавьте все в метод, который находится между первой строкой (`bool successFlag = false;`) и последней строкой (`return successFlag;`) в блоке **try**.</span><span class="sxs-lookup"><span data-stu-id="4c490-203">Put everything in the method that is between the first line,  `bool successFlag = false;`, and the last line,  `return successFlag;` , in a **try** block.</span></span>
    
 
12. <span data-ttu-id="4c490-204">Добавьте указанный ниже блок **catch** сразу же после блока **try**.</span><span class="sxs-lookup"><span data-stu-id="4c490-204">Add the following **catch** block just below the **try** block.</span></span>
    
```C#
  catch (KeyNotFoundException)
{
    successFlag = false;
}
```


     **Note**  The  **KeyNotFoundException** is also the reason why we have to leave the **Added to Inventory** field visible on the Edit Item form. SharePoint does not include fields that are hidden on the Edit Item form in **AfterProperties**.

    The entire method should now look like the following.
    


```C#
  private bool TryUpdateInventory(SPRemoteEventProperties properties)
{
    bool successFlag = false;
    
    try 
    {
        var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
        var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

        if (arrived &amp;&amp; !addedToInventory)
        {
            using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
            using (SqlCommand cmd = conn.CreateCommand())
            {
                conn.Open();
                cmd.CommandText = "UpdateInventory";
                cmd.CommandType = CommandType.StoredProcedure;
                SqlParameter tenant = cmd.Parameters.Add("@Tenant", SqlDbType.NVarChar);
                tenant.Value = properties.ItemEventProperties.WebUrl + "/";
                SqlParameter product = cmd.Parameters.Add("@ItemName", SqlDbType.NVarChar, 50);
                product.Value = properties.ItemEventProperties.AfterProperties["Title"]; // not "Product"
                SqlParameter quantity = cmd.Parameters.Add("@Quantity", SqlDbType.SmallInt);
                quantity.Value = Convert.ToUInt16(properties.ItemEventProperties.AfterProperties["Quantity"]);
                cmd.ExecuteNonQuery();
            }            
            successFlag = true;
        }  
    }
    catch (KeyNotFoundException)
    {
        successFlag = false;
    }
    return successFlag;
}
```

13. <span data-ttu-id="4c490-p126">Добавьте указанный ниже метод в класс  `RemoteEventReceiver1`. Этот шаблон кода должен быть знаком вам по предыдущим статьям этой серии. Тем не менее есть одно отличие. Код получает объект **ClientContext**, вызывая метод **TokenHelper.CreateRemoteEventReceiverClientContext**, а не метод **SharePointContext.CreateUserClientContextForSPHost**, который мы использовали в коде, который вызывался в SharePoint из страниц, например из страницы EmployeeAdder. Основная причина использования разных методов для получения объекта **ClientContext** состоит в том, что SharePoint передает приемникам событий информацию, необходимую для создания таких объектов, другим способом, чем страницам. В случае приемников событий он передает объект **SPRemoteEventProperties**, а в случае страниц он передает специальное поле, называемое маркером контекста, в тексте запроса, запускающего страницу надстройки.</span><span class="sxs-lookup"><span data-stu-id="4c490-p126">Add the following method to the  `RemoteEventReceiver1` class. By now this pattern of code is familiar from earlier articles in this series. But note one difference. The code gets the **ClientContext** object by calling **TokenHelper.CreateRemoteEventReceiverClientContext** method, instead of the **SharePointContext.CreateUserClientContextForSPHost** method as we used in code that called into SharePoint from pages, such as the EmployeeAdder page. The primary reason for having different methods to get a **ClientContext** object is that SharePoint passes the information needed to create such objects differently to event receivers from how it passes it to pages. For event receivers, it passes a **SPRemoteEventProperties** object, but for pages it passes a special field, called a context token, in the body of the request that launches the add-in page.</span></span>
    
```C#
  private void RecordInventoryUpdateLocally(SPRemoteEventProperties properties)
{
    using (ClientContext clientContext = TokenHelper.CreateRemoteEventReceiverClientContext(properties))
    {
        List expectedShipmentslist = clientContext.Web.Lists.GetByTitle(properties.ItemEventProperties.ListTitle);
        ListItem arrivedItem = expectedShipmentslist.GetItemById(properties.ItemEventProperties.ListItemId);
        arrivedItem["Added_x0020_to_x0020_Inventory"] = true;
        arrivedItem.Update();
        clientContext.ExecuteQuery();
    }
}
```

14. <span data-ttu-id="4c490-211">Сохраните и закройте файл кода приемника.</span><span class="sxs-lookup"><span data-stu-id="4c490-211">Save and close the receiver code file.</span></span>
    
 

## <a name="register-the-receiver"></a><span data-ttu-id="4c490-212">Регистрация приемника</span><span class="sxs-lookup"><span data-stu-id="4c490-212">Register the receiver</span></span>

<span data-ttu-id="4c490-213">Последняя задача, которую необходимо выполнить, — это сообщить SharePoint, что у нас имеется пользовательский приемник, и мы хотим, чтобы SharePoint вызывал его при обновлении элемента в списке **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="4c490-213">The final task is to tell SharePoint that we have a custom receiver that we want SharePoint to call whenever an item on the **Expected Shipments** list is updated.</span></span>
 

 

1. <span data-ttu-id="4c490-p127">Откройте файл SharePointContentDeployer.cs и добавьте указанную ниже строку в метод  `DeployChainStoreComponentsToHostWeb` сразу же за строкой, в которой создается список **Expected Shipments** (Ожидаемые отгрузки). Мы добавим этот метод на следующем этапе. Обратите внимание, что в метод мы передаем объект **HttpRequest**, который начальная страница надстройки передавала в метод  `DeployChainStoreComponentsToHostWeb`.</span><span class="sxs-lookup"><span data-stu-id="4c490-p127">Open the SharePointContentDeployer.cs file and add the following line to the  `DeployChainStoreComponentsToHostWeb` method just below the line that creates the **Expected Shipments** list. We'll add this method in the next step. Note that we are passing to the method the **HttpRequest** object that the add-in's start page passed to the `DeployChainStoreComponentsToHostWeb`method.</span></span>
    
```C#
  RegisterExpectedShipmentsEventHandler(request);
```

2. <span data-ttu-id="4c490-217">Добавьте указанный ниже метод в класс `SharePointComponentDeployer`.</span><span class="sxs-lookup"><span data-stu-id="4c490-217">Add the following method to the  `SharePointComponentDeployer` class.</span></span>
    
```C#
  private static void RegisterExpectedShipmentsEventHandler(HttpRequest request)
{
    using (var clientContext = sPContext.CreateUserClientContextForSPHost())    
    {
        var query = from list in clientContext.Web.Lists
                    where list.Title == "Expected Shipments"
                    select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        List expectedShipmentsList = matchingLists.Single();

        // TODO16: Add the event receiver to the list's collection of event receivers.       

        clientContext.ExecuteQuery();
    }
}
```

3. <span data-ttu-id="4c490-p128">Замените  `TODO16` указанными ниже строками. Обратите внимание, что для приемников событий существует "легковесный" класс ***CreationInformation**, аналогичный тому, который используется для списков и элементов списков.</span><span class="sxs-lookup"><span data-stu-id="4c490-p128">Replace  `TODO16` with the following lines. Note that there is a light weight ***CreationInformation** class for event receivers just as there is for lists and list items.</span></span>
    
```C#
  EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
receiver.ReceiverName = "ExpectedShipmentsItemUpdated";
receiver.EventType = EventReceiverType.ItemUpdated;

 // TODO17: Set the URL of the receiver.

expectedShipmentsList.EventReceivers.Add(receiver);

```

4. <span data-ttu-id="4c490-p129">Теперь вам необходимо сообщить SharePoint URL-адрес приемника событий. В рабочей среде это будет тот же домен, что и для удаленных страниц (с путем /Services/RemoteEventReceiver1.svc). Так как обработчик зарегистрирован в коде, выполняемом при первом запуске и размещенном в начальной странице надстройки, то домен находится в заголовке узла объекта **HttpRequest** для запроса, вызвавшего эту страницу. Наш код передал этот объект из страницы в метод `DeployChainStoreComponentsToHostWeb`, который затем передал его в метод `RegisterExpectedShipmentsEventHandler`. Так что мы можем задать URL-адрес приемника с помощью указанного ниже кода.</span><span class="sxs-lookup"><span data-stu-id="4c490-p129">Now you need to tell SharePoint the URL of the event receiver. In production, it's going to be at the same domain as the remote pages, with the path of /Services/RemoteEventReceiver1.svc. Since the handler is being registered in first-run logic from the add-in's start page, the domain is in the host header of the **HttpRequest** object for the request that called the page. Our code has passed that object from the page to the `DeployChainStoreComponentsToHostWeb` method, which itself passed it to the `RegisterExpectedShipmentsEventHandler` method. So we can set the receiver's URL with the following code.</span></span>
    
     `receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc";`
    
    <span data-ttu-id="4c490-p130">К сожалению, этот способ не будет работать при отладке надстройки в Visual Studio. Когда вы выполняете отладку, приемник размещен в служебной шине Azure, а не по URL-адресу localhost, по которому размещены удаленные страницы. Нам необходимо использовать разные URL-адреса для приемника в зависимости от того, выполняем ли мы отладку, поэтому замените  `TODO17` указанной ниже структурой, в которой используются директивы компилятора C#. Обратите внимание, что в режиме отладки URL-адрес приемника считывается из параметра web.config. *Вы создадите этот параметр на одном из следующих этапов.*</span><span class="sxs-lookup"><span data-stu-id="4c490-p130">Unfortunately, this won't work when you are debugging the add-in from Visual Studio. When you are debugging, the receiver is hosted in the Azure Service Bus, not in the localhost URL where the remote pages are hosted. We need to set distinct URLs for the receiver depending on whether we are debugging or not, so replace  `TODO17` with the following structure that uses C# compiler directives. Note that in debug mode the receiver's URL is read from a web.config setting. *You will create this setting in a later step.*</span></span> 
    


```C#
  #if DEBUG
                    receiver.ReceiverUrl = WebConfigurationManager.AppSettings["RERdebuggingServiceBusUrl"].ToString();
#else
                    receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc"; 
#endif

```


    The whole  `RegisterExpectedShipmentsEventHandler` method should now look like the following.
    


```C#
  private static void RegisterExpectedShipmentsEventHandler(HttpRequest request)
{    
    using (var clientContext = sPContext.CreateUserClientContextForSPHost())
    {
        var query = from list in clientContext.Web.Lists
                    where list.Title == "Expected Shipments"
                    select list;
        IEnumerable<List> matchingLists = clientContext.LoadQuery(query);
        clientContext.ExecuteQuery();

        List expectedShipmentsList = matchingLists.Single();

        EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
        receiver.ReceiverName = "ExpectedShipmentsItemUpdated";
        receiver.EventType = EventReceiverType.ItemUpdated;

#if DEBUG
        receiver.ReceiverUrl = WebConfigurationManager.AppSettings["RERdebuggingServiceBusUrl"].ToString();
#else
        receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc"; 
#endif
        expectedShipmentsList.EventReceivers.Add(receiver);
        clientContext.ExecuteQuery();
    }
}
```

5. <span data-ttu-id="4c490-230">Добавьте указанный ниже оператор **using** в начало файла.</span><span class="sxs-lookup"><span data-stu-id="4c490-230">Add the following **using** statement to the top of the file.</span></span>
    
```C#
  using System.Web.Configuration;
```

6. <span data-ttu-id="4c490-231">Чтобы убедиться, что параметр `DEBUG` имеет значение true (Истина) тогда и только тогда, когда надстройка находится в состоянии отладки, выполните указанную ниже подпроцедуру.</span><span class="sxs-lookup"><span data-stu-id="4c490-231">To ensure that  `DEBUG` is true if, and only if, the add-in is being debugged, carry out the following subprocedure:</span></span>
    
1. <span data-ttu-id="4c490-232">В **обозревателе решений** щелкните правой кнопкой мыши проект **ChainStoreWeb** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4c490-232">In **Solution Explorer**, right click the **ChainStoreWeb** project and select **Properties**.</span></span>
    
 
2. <span data-ttu-id="4c490-233">В разделе **Свойства** откройте вкладку **Сборка**, а затем в раскрывающемся списке **Конфигурация** вверху выберите пункт **Отладить**.</span><span class="sxs-lookup"><span data-stu-id="4c490-233">Open the **Build** tab of the **Properties**, and then select **Debug** from the **Configuration** drop down at the top.</span></span>
    
 
3. <span data-ttu-id="4c490-p131">Проверьте, установлен ли флажок **Определять константу DEBUG** (обычно он установлен по умолчанию). На снимке экрана ниже показаны правильные настройки.</span><span class="sxs-lookup"><span data-stu-id="4c490-p131">Ensure that the **Define DEBUG constant** box is checked. (It usually is by default.) The following screen shot shows the proper setting.</span></span>
    
  ![Вложенная вкладка "Сборка" вкладки "Свойства" в Visual Studio. В раскрывающемся списке "Конфигурация" выбран пункт "Отладка". Установлен флажок "Определить константу DEBUG".](../../images/4f81174f-d875-4a9e-bff4-adea0f176f00.PNG)
 

 

 
4. <span data-ttu-id="4c490-p133">В раскрывающемся списке **Конфигурация** выберите пункт **Выпуск**, а затем убедитесь, что флажок **Определять константу DEBUG** ***не*** установлен (обычно по умолчанию он не установлен). На снимке экрана ниже показаны правильные настройки.</span><span class="sxs-lookup"><span data-stu-id="4c490-p133">Change the **Configuration** drop down to **Release**, and then ensure that the **Define DEBUG constant** box is ***not*** checked. (It usually is not by default.) The following screen shot shows the proper setting.</span></span>
    
  ![Вложенная вкладка "Сборка" вкладки "Свойства". В раскрывающемся списке "Конфигурация" выбран пункт "Выпуск". Флажок "Определить константу DEBUG" не установлен.](../../images/7fd942de-a324-4f70-a750-f5304c993832.PNG)
 

 

 
5. <span data-ttu-id="4c490-244">Если вы внесли какие-либо изменения, сохраните их, а затем закройте вкладку **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4c490-244">If you made any changes, save and then close the **Properties** tab.</span></span>
    
 
7. <span data-ttu-id="4c490-p135">Откройте файл web.config, а затем добавьте указанную ниже разметку в качестве дочерней разметки для элемента **appSettings**. Мы получим значение этого параметра в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="4c490-p135">Open the web.config file, and add the following mark up as a child of the **appSettings** element. We get the value of the setting in the next section.</span></span>
    
```XML
  <add key="RERdebuggingServiceBusUrl" value="" />
```


## <a name="get-the-receiver-url-for-debugging"></a><span data-ttu-id="4c490-247">Получение URL-адреса приемника для отладки</span><span class="sxs-lookup"><span data-stu-id="4c490-247">Get the receiver URL for debugging</span></span>

<span data-ttu-id="4c490-p136">Приемники событий надстройки и событий элементов списков представляют собой службы WCF, при этом каждая такая служба "знает" свою конечную точку и хранит ее в разных местах, включая объект **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**. Когда вы выполняете отладку, приемник надстройки размещен в конечной точке служебной шины Azure, которая почти такая же, как и конечная точка для приемника элемента списка. Разница состоит в том, что URL-адрес конечной точки надстройки имеет окончание AppEventReceiver.svc, а URL-адрес приемников элементов списков — RemoteEventReceiver1.svc. Таким образом, мы можем получить URL-адрес конечной точки в приемнике надстройки, немного изменить его окончание, а затем использовать его в качестве значения параметра **RERdebuggingServiceBusUrl** в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="4c490-p136">The add-in event and list item event receivers are Windows Communication Service (WCF) services and every WCF service knows its own endpoint and stores it in multiple places, including the **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** object. When you are debugging, the add-in receiver is hosted at an Azure Service Bus endpoint that is almost same as the endpoint for the list item receiver. The difference is that the URL of the add-in endpoint ends with "AppEventReceiver.svc", but the list item receivers URL ends with "RemoteEventReceiver1.svc". So we can get the URL of the endpoint in the add-in receiver, make a small change to the end of it, and then use it as the value of our web.config **RERdebuggingServiceBusUrl** setting.</span></span>
 

 

1. <span data-ttu-id="4c490-252">Откройте файл AppEventReceiver.svc.cs в папке **Services** (Службы) проекта **ChainStoreWeb**.</span><span class="sxs-lookup"><span data-stu-id="4c490-252">Open the AppEventReceiver.svc.cs file in the **Services** folder of the **ChainStoreWeb** project.</span></span>
    
 
2. <span data-ttu-id="4c490-253">Добавьте указанный ниже код в качестве самой первой строки в методе **ProcessEvent**.</span><span class="sxs-lookup"><span data-stu-id="4c490-253">Add the following as the very first line in the **ProcessEvent** method.</span></span>
    
```C#
  string debugEndpoint = System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri.ToString(); 
```

3. <span data-ttu-id="4c490-254">Добавьте точку останова в следующую строку метода.</span><span class="sxs-lookup"><span data-stu-id="4c490-254">Add a breakpoint to the very next line of the method.</span></span>
    
 
4. <span data-ttu-id="4c490-p137">Нажмите клавишу F5, чтобы выполнить отладку надстройки. Так как файл web.config открыт, а пакет Инструменты разработчика Office для Visual Studio изменяет параметр при каждом нажатии клавиши F5, вам будет предложено перезагрузить его. Выберите вариант **Да**.</span><span class="sxs-lookup"><span data-stu-id="4c490-p137">Press F5 to debug the add-in. Because web.config is open and Office Developer Tools for Visual Studio changes a setting in it every time you press F5, you will be prompted to reload it. Select **Yes**.</span></span> 
    
 
5. <span data-ttu-id="4c490-p138">При достижении точки останова наведите курсор на переменную  `debugEndpoint`. Когда появится подсказка по данным Visual Studio, щелкните стрелку вниз и выберите пункт **Средство визуализации текста**.</span><span class="sxs-lookup"><span data-stu-id="4c490-p138">When the breakpoint is hit, hover the cursor over the  `debugEndpoint` variable. When the Visual Studio Data Tip appears, click the down arrow and select **Text Visualizer**.</span></span>
    
  ![Визуализатор текста в Visual Studio с URL-адресом служебной шины Azure.](../../images/494cf01e-3e17-4092-b239-9312ac4ab258.PNG)
 

 

 
6. <span data-ttu-id="4c490-261">Скопируйте значение строки из средства визуализации и вставьте его куда-нибудь.</span><span class="sxs-lookup"><span data-stu-id="4c490-261">Copy the string value from the visualizer and paste it somewhere.</span></span>
    
 
7. <span data-ttu-id="4c490-262">Закройте средство визуализации, а затем остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c490-262">Close the visualizer, and then stop debugging in Visual Studio.</span></span>
    
 
8. <span data-ttu-id="4c490-263">Удалите или закомментируйте строку, которую вы добавили на втором этапе этой процедуры, а затем удалите точку останова.</span><span class="sxs-lookup"><span data-stu-id="4c490-263">Delete or comment out the line you added in the second step of this procedure, and then delete the breakpoint as well.</span></span>
    
 
9. <span data-ttu-id="4c490-264">В скопированной вами строке замените текст AppEventReceiver.svc в конце текстом RemoteEventReceiver1.svc.</span><span class="sxs-lookup"><span data-stu-id="4c490-264">In the string you copied, replace the "AppEventReceiver.svc" at the end with "RemoteEventReceiver1.svc".</span></span>
    
 
10. <span data-ttu-id="4c490-265">Скопируйте и вставьте измененный URL-адрес в качестве значения ключа **RERdebuggingServiceBusUrl** в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="4c490-265">Copy and paste the modified URL as the value of the **RERdebuggingServiceBusUrl** key in the web.config file.</span></span>
    
 

 <span data-ttu-id="4c490-p139">**Примечание.** Ручное копирование URL-адреса служебной шины и вставка его (измененной версии) в файл web.config — это не единственный способ удовлетворить потребность в различных URL-адресах при отладке удаленного приемника событий, когда он выполняется в рабочей среде. Мы могли бы программным способом сохранить значение параметра **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** где-нибудь в SharePoint или в удаленной базе данных, а затем наш код, выполняющийся при первом запуске, считал бы это значение и назначил бы его свойству `receiver.ReceiverUrl`. Мы могли бы зарегистрировать приемник событий элементов списков в качестве части обработчика событий, установленного надстройкой. Затем мы могли бы программным способом считать значение параметра **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**, изменить его, а затем назначить его параметру `receiver.ReceiverUrl`, не сохраняя его нигде. При использовании этой стратегии также понадобилось бы создать список **Expected Shipments** (Ожидаемые отгрузки) в обработчике событий, установленном надстройкой, так как он должен существовать, прежде чем в нем будет зарегистрирован обработчик. (Кроме того, учтите, что мы могли бы объединить наш приемник событий надстройки и приемник событий элемента списка в один приемник (например, использовать одни и те же SVC- и SVC.CS-файлы). В этом случае не потребовалось бы изменять URL-адрес перед использованием его в качестве значения для параметра `receiver.ReceiverUrl`.)</span><span class="sxs-lookup"><span data-stu-id="4c490-p139">**Note**   Manually copying the service bus URL and pasting (a modified version of) it into the web.config is not the only way of dealing with the need for a different URL when debugging a remote event receiver from when it is running in production. We could programmatically store the value of **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** somewhere in SharePoint or the remote database, and then have our first-run code read it and assign it to the `receiver.ReceiverUrl` property. We could register the list item event receiver as part of the add-in installed event handler. Then we could programmatically read **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**, modify it, and assign it to  `receiver.ReceiverUrl` without having to store it anywhere. This strategy would require that the **Expected Shipments** list also be created in the add-in installed event handler, since it would have to exist before the handler could be registered with it. (Note also, that we could combine our add-in event receiver and list item event receiver into a single receiver (that is, the same .svc and .svc.cs files). In that case, no modification of the URL is necessary before using it as the value of `receiver.ReceiverUrl`.)</span></span> 
 


## <a name="run-the-add-in-and-test-the-list-item-receiver"></a><span data-ttu-id="4c490-273">Запуск надстройки и тестирование приемника элемента списка</span><span class="sxs-lookup"><span data-stu-id="4c490-273">Run the add-in and test the list item receiver</span></span>


 

 

1. <span data-ttu-id="4c490-274">Откройте страницу **Содержимое сайта** веб-сайта магазина в Гонконге *и удалите список **Expected Shipments** (Ожидаемые отгрузки), если он там есть.*</span><span class="sxs-lookup"><span data-stu-id="4c490-274">Open the **Site Contents** page of the Hong Kong store's website *and remove the **Expected Shipments** list if there is one!*</span></span> 
    
 
2. <span data-ttu-id="4c490-p140">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="4c490-p140">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span>
    
 
3. <span data-ttu-id="4c490-279">Когда откроется начальная страница надстройки, нажмите кнопку **Вернуться на сайт** на расположенном в верхней части элементе управления хрома.</span><span class="sxs-lookup"><span data-stu-id="4c490-279">When the add-in's start page opens, click the **Back to Site** button on the chrome control at the top.</span></span>
    
 
4. <span data-ttu-id="4c490-280">С начальной страницы магазина в Гонконге перейдите на страницу **Содержание сайта** и откройте список **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="4c490-280">From the home page of the Hong Kong store, navigate to the **Site Contents** page and open the **Expected Shipments** list.</span></span>
    
 
5. <span data-ttu-id="4c490-p141">Создайте элемент и обратите внимание, что в форме нового элемента не отображаются поля **Arrived** (Прибыл) и **Added to Inventory** (Добавлен в запасы).</span><span class="sxs-lookup"><span data-stu-id="4c490-p141">Create an item, and on the new item form. Notice that the **Arrived** and **Added to Inventory** fields do not appear on form.</span></span>
    
 
6. <span data-ttu-id="4c490-p142">После создания элемента повторно откройте его для внесения изменений. Установите флажок **Arrived** (Прибыл) и сохраните элемент. В результате этих действий будет создано событие обновления элемента. Элемент будет добавлен в запасы, а значение поля **Added to Inventory** (Добавлен в запасы) будет изменено на **Yes** (Да). Чтобы отобразить изменения в поле **Added to Inventory** (Добавлен в запасы) вам, возможно, потребуется обновить страницу.</span><span class="sxs-lookup"><span data-stu-id="4c490-p142">After the item is created, reopen it for editing. Check the **Arrived** box and save the item. This will trigger the item updated event. The item will be added to inventory and the value of the **Added to Inventory** field will be changed to **Yes**. (You may have to refresh the page to see the change to **Added to Inventory**.)</span></span>
    
 
7. <span data-ttu-id="4c490-p143">Нажимайте кнопку "Назад" в браузере, пока вы не вернетесь на начальную страницу надстройки Chain Store, а затем нажмите кнопку **Show Inventory** (Отобразить запасы). Теперь в списке появится элемент, для которого вы задали значение **Arrived** (Прибыл).</span><span class="sxs-lookup"><span data-stu-id="4c490-p143">Use the browser's back button until you are back at the start page for Chain Store add-in, and then press the **Show Inventory** button. The item you marked as **Arrived** is now listed.</span></span>
    
 
8. <span data-ttu-id="4c490-290">Перейдите обратно к списку **Expected Shipments** (Ожидаемые отгрузки) и добавьте другой элемент * с точно такими же именем продукта и названием поставщика*, но с другим количеством.</span><span class="sxs-lookup"><span data-stu-id="4c490-290">Navigate back to the **Expected Shipments** list and add another item *with exactly the same product name and supplier name*, but a different quantity.</span></span>
    
 
9. <span data-ttu-id="4c490-p144">После создания элемента повторно откройте его для внесения изменений. Измените значение поля **Arrived** (Прибыл) на **Yes** (Да) и сохраните элемент.</span><span class="sxs-lookup"><span data-stu-id="4c490-p144">After the item is created, reopen it for editing. Change the value of **Arrived** to **Yes** and save the item.</span></span>
    
 
10. <span data-ttu-id="4c490-p145">Нажимайте кнопку "Назад" в браузере, пока вы не вернетесь на начальную страницу надстройки Chain Store, а затем нажмите кнопку **Show Inventory** (Отобразить запасы). В списке будет по-прежнему один элемент с нужными нами названиями продукта и поставщика, но теперь его количество будет представлять собой сумму количеств двух элементов в списке **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="4c490-p145">Use the browser's back button until you are back at the start page for Chain Store add-in, and then press the **Show Inventory** button. There is still just one item for the product name and supplier, but the quantity is now the total of the two items on the **Expected Shipments** list.</span></span>
    
 
11. <span data-ttu-id="4c490-p146">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="4c490-p146">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
12. <span data-ttu-id="4c490-p147">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="4c490-p147">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="4c490-299"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="4c490-299"></span></span>

<span data-ttu-id="4c490-p148">Сведения о том, как публиковать надстройки на сайте SharePoint см. в статье  [Развертывание и установка надстроек для SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options). Углубленные сведения о разработке надстроек SharePoint см. на указанных ниже узлах MSDN.</span><span class="sxs-lookup"><span data-stu-id="4c490-p148">See  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options) to learn how to publish your add-in to a SharePoint site. Or go on to advanced work in SharePoint add-in development with these nodes of MSDN:</span></span>
 

 

-  [<span data-ttu-id="4c490-302">Проектирование надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c490-302">Design SharePoint Add-ins</span></span>](design-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="4c490-303">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c490-303">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="4c490-304">Публикация надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c490-304">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="4c490-305">Средства и среды для разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="4c490-305">Tools and environments for developing SharePoint Add-ins</span></span>](tools-and-environments-for-developing-sharepoint-add-ins)
    
 

