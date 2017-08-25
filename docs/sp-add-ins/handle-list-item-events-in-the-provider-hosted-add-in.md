# <a name="handle-list-item-events-in-the-provider-hosted-add-in"></a>Обработка событий элементов списков в надстройке, размещаемой у поставщика
В этой статье рассказывается, как обрабатывать события элементов списка для надстройки SharePoint, размещаемой у поставщика.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Это десятая часть серии статей, посвященной основам разработки надстроек, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.
 

-  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [Настройка внешнего вида надстройки SharePoint, размещенной у поставщика](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [Добавление настраиваемой кнопки в надстройку, размещенную у поставщика](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [Краткий обзор объектной модели SharePoint](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [Добавление операций записи SharePoint в надстройку, размещенную у поставщика](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 
-  [Добавление веб-части надстройки в надстройку, размещенную у поставщика](include-an-add-in-part-in-the-provider-hosted-add-in)
    
 
-  [Обработка событий надстройки, размещенной у поставщика](handle-add-in-events-in-the-provider-hosted-add-in)
    
 
-  [Добавление логики, выполняемой при первом запуске, в надстройку, размещаемую у поставщика](add-first-run-logic-to-the-provider-hosted-add-in)
    
 
-  [Программное развертывание настраиваемой кнопки в надстройке, размещаемой у поставщика](programmatically-deploy-a-custom-button-in-the-provider-hosted-add-in)
    
 

 **Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeRER.sln.
 

В одной из предыдущих статей этой серии мы рассказывали, что при размещении заказа он добавляется в таблицу **Orders** (Заказы) в корпоративной базе данных, а соответствующий ему элемент автоматически добавляется в список **Expected Shipments** (Ожидаемые отгрузки). Когда заказ прибывает в местный магазин, пользователь указывает в столбце **Arrived** (Прибыл) значение **Yes** (Да). При изменении значения поля для элемента создается событие обновления элемента, для которого можно добавить настраиваемый обработчик. Изучая данную статью, вы создадите обработчик этого события элемента списка, а затем программным способом развернете его в коде, выполняемом во время первого запуска надстройки SharePoint. Обработчик добавит элемент в таблицу **Inventory** (Запасы) корпоративной базы данных. Затем он задаст в столбце **Added to Inventory** (Добавлен в запасы) списка **Expected Shipments** (Ожидаемые отгрузки) значение **Yes** (Да). Кроме того, вы узнаете, как не допустить, чтобы второе событие обновления элемента создало бесконечный ряд новых событий обновления элемента.
 

## <a name="programmatically-deploy-the-expected-shipments-list"></a>Программное развертывание списка Expected Shipments (Ожидаемые отгрузки)


 **Примечание.** При повторном открытии решения параметры раздела "Начальные проекты" в Visual Studio обычно сбрасываются к значениям, используемым по умолчанию. Сразу же после повторного открытия примера решения в этой серии статей всегда выполняйте указанные ниже действия.
 


1. В **обозревателе решений** откройте файл Utilities\SharePointComponentDeployer.cs в проекте **ChainStoreWeb**. Добавьте указанный ниже метод в класс `SharePointComponentDeployer`. В этом коде нет новых возможностей, которых не было в предыдущей статье этой серии, но следует обратить внимание на указанные ниже моменты.
    
      - Код присваивает атрибуту **Required** (Обязательный) поля **Quantity** (Количество) значение **TRUE** (Истина), поэтому это поле всегда должно иметь значение. Затем он задает число 1 в качестве значения, используемого по умолчанию.
    
 
  - В форме New Item (Новый элемент) поля **Arrived** (Прибыл) и **Added to Inventory** (Добавлен в запасы) скрыты.
    
 
  - В идеальном случае в форме Edit Item (Изменение элемента) поле **Added to Inventory** (Добавлен в запасы) тоже должно быть скрыто, так как его значение следует изменить на **Yes** (Да) только тогда, когда обработчик события обновления элемента в первый раз добавит элемент в корпоративную таблицу **Inventory** (Запасы). По техническим причинам, о которых мы расскажем на одном из следующих этапов, это поле должно отображаться в форме Edit Item (Изменение элемента), если нам необходимо программным способом записывать в него данные из обработчика события обновления элемента.
    
 

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

2. В методе `DeployChainStoreComponentsToHostWeb` добавьте указанную ниже строку (сразу же после строки `RemoteTenantVersion = localTenantVersion`).
    
```
  CreateExpectedShipmentsList();
```


## <a name="create-the-list-item-event-receiver"></a>Создание приемника событий элемента списка


 **Примечание.** Если вы работали со статьями этой серии, то, вероятно, уже настроили собственную среду разработки для отладки удаленных приемников событий. Если вы еще не сделали этого, то прежде чем перейти к другим разделам данной статьи, прочитайте раздел [Настройка решения для отладки приемника событий](handle-add-in-events-in-the-provider-hosted-add-in#RERDebug).
 

Пакет Инструменты разработчика Office для Visual Studio включает элемент **Удаленный приемник событий**, который можно добавить в решение надстройки SharePoint. На момент написания данной статьи предполагается, что для этого элемента проекта список (для которого будет зарегистрирован приемник) находится на сайте надстройки и, соответственно, пакет инструментов создает сайт надстройки, а также ряд артефактов SharePoint в нем. Кроме того, предполагается, что приемник для надстройки Chain Store будет зарегистрирован (на одном из следующих этапов) для списка **Expected Shipments** (Ожидаемые отгрузки) на хост-сайте, поэтому для надстройки не требуется сайт надстройки. (Сведения о различиях между сайтами надстроек и хост-сайтами см. в статье [Надстройки SharePoint](sharepoint-add-ins).)
 

 

 **Примечание.** Приемники событий списка и элементов списка называются удаленными приемниками событий, так как их код является удаленным по отношению к SharePoint и размещен либо в облаке, либо на локальном сервере за пределами фермы SharePoint. Тем не менее события, запускающие их, находятся в SharePoint.
 


1. В **обозревателе решений** щелкните правой кнопкой мыши папку **Службы** в проекте **ChainStoreWeb** и выберите **Добавить | Служба WCF**.
    
 
2. Когда отобразится соответствующий запрос, укажите для службы имя RemoteEventReceiver1, а затем нажмите кнопку **OK**. 
    
 
3. Пакет средств создаст SVC-файл интерфейса и файл кода программной части. Нам не потребуется файл интерфейса IRemoteEventReceiver1.cs, поэтому удалите его. (Возможно, пакет средств открыл его автоматически. В этом случае закройте файл, а затем удалите его.)
    
     **Примечание.** Когда вы создавали приемники событий надстройки для событий установки и удаления в одной из предыдущих статей данной серии, пакет Инструменты разработчика Office для Visual Studio добавлял их URL-адреса в файл манифеста приложения. Приемники событий списка и элемента списка не зарегистрированы в манифесте приложения. Их необходимо зарегистрировать программным способом (в надстройке, размещаемой у поставщика). Вы сделаете это на одном из следующих этапов.
4. Откройте файл с выделенным кодом RemoteEventReceiver1.svc.cs. Замените все его содержимое указанным ниже кодом. Обратите внимание на указанные ниже особенности кода.
    
      - Интерфейс `IRemoteEventService` определен в пространстве имен **Microsoft.SharePoint.Client.EventReceivers**.
    
 
  - В надстройке Chain Store не будут обрабатываться события, возникающие до выполнения действий, но метод **ProcessEvent** является обязательным для интерфейса `IRemoteEventService`.
    
 

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

5. Добавьте указанный ниже код в метод  `ProcessOneWayEvent`. Обратите внимание, что **ItemUpdated** единственное событие, которое будет обрабатываться в данном примере, поэтому вместо оператора **switch** можно использовать простую структуру **if**. Приемники событий обычно обрабатывают несколько событий, поэтому желательно, чтобы вы изучили шаблон, который вы (как разработчик надстроек SharePoint) чаще всего будете использовать в своих обработчиках событий.
    
```C#
  switch (properties.EventType)
{
    case SPRemoteEventType.ItemUpdated:

        // TODO12: Handle the item updated event.
                    
        break;
}  
```

6. Замените  `TODO12` указанным ниже кодом. Здесь мы опять используем структуру **switch** в случае, когда достаточно использовать простую структуру **if**. Мы делаем это, чтобы показать вам стандартный шаблон, используемый в приемниках событий SharePoint.
    
```C#
  switch (properties.ItemEventProperties.ListTitle)
{
    case "Expected Shipments":

        // TODO13: Handle the arrival of a shipment.

        break;
}
```

7. Код, который реагирует на прибытие отгруженного товара, должен выполнять два указанных ниже действия.
    
      - Добавьте элемент, который прибыл в магазин, в корпоративные запасы.
    
 
  - В списке **Expected Shipments** (Ожидаемые загрузки) в поле **Added to Inventory** (Добавлен на склад) укажите значение **Yes** (Да). Но это следует сделать, только если элемент успешно добавлен в запасы.
    
 

    Добавьте указанный ниже код вместо `TODO13`. Методы `TryUpdateInventory` и `RecordInventoryUpdateLocally` мы создадим в следующих действиях.
    


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

8. Добавьте указанный ниже метод в класс `RemoteEventReceiver1`.
    
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

9. В списке **Expected Shipments** (Ожидаемые отгрузки) имеется пять столбцов, но нам не нужно, чтобы обработчик реагировал на большинство видов обновлений элемента. Например, если пользователь исправляет написание названия поставщика, возникает событие обновления элемента, но при этом наш обработчик не должен ничего делать. Он должен действовать только тогда, когда полю **Arrived** (Прибыл) присваивается значение **Yes** (Да). 
    
    Есть еще одно условие, которое необходимо проверять. Предположим, что поле **Arrived** (Прибыл) имеет значение **Yes** (Да), а продукт в элементе добавлен в запасы (соответственно, поле **Added to Inventory** [Добавлен в запасы] имеет значение **Yes**[Да]). Но позже пользователь по ошибке изменяет значение поля **Arrived** (Прибыл) для отгрузки обратно на **No** (Нет), а затем исправляет свою ошибку, снова присвоив полю значение **Yes** (Да). И ошибка, и ее исправление создают событие обновления элемента. Обработчик не будет реагировать на ошибку, так как он срабатывает только если полю **Arrived** (Прибыл) присваивается значение **Yes** (Да). Обработчик среагирует на исправление, при котором полю **Arrived** (Прибыл) снова будет присвоено значение **Yes** (Да). Из-за этого один и тот же продукт в одном и том же количестве будет еще раз добавлен в запасы. Поэтому обработчик должен срабатывать, только когда поле **Added to Inventory** (Добавлен в запасы) имеет значение **No** (Нет). 
    
    Таким образом, обработчику необходимо "знать" значения этих полей сразу же после того как пользователь обновит элемент. У объекта **SPRemoteEventProperties** есть свойство **ItemEventProperties**. В свою очередь, у этого свойства имеется индексированное свойство **AfterProperties**, в котором хранятся значения полей обновленного элемента. В коде ниже эти свойства используются для проверки того, необходимо ли срабатывать обработчику. Вставьте этот код вместо `TODO14`.
    


```C#
  var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);
var addedToInventory = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Added_x0020_to_x0020_Inventory"]);

if (arrived &amp;&amp; !addedToInventory)
{

    // TODO15: Add the item to inventory

    successFlag = true;
}
```

10. Замените `TODO15` указанным ниже кодом. Здесь в основном используется программирование для SQL и ASP.NET, и мы не будем подробно рассматривать его, но при этом учтите указанные ниже моменты.
    
      - Мы используем свойство **ItemEventProperties.WebUrl**, чтобы получить имя клиента, представляющее собой URL-адрес хост-сайта.
    
 
  - Мы еще раз используем **AfterProperties**, чтобы получить значения имени и количества продукта.
    
 
  - Мы ссылаемся на поле имени продукта, используя имя Title (Название), даже несмотря на то, что в методе  `CreateExpectedShipmentsList` отображаемое имя было изменено на Product (Продукт), так как для ссылки на поля всегда используются внутренние имена полей.
    
 

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

11. Когда метод `TryUpdateInventory` возвращает значение **true** (Истина), наш обработчик вызывает (еще не написанный) метод, который обновляет тот же элемент в списке **Expected Shipments** (Ожидаемые отгрузки), задавая для поля **Added to Inventory** (Добавлен в запасы) значение **Yes** (Да). Он представляет собой событие обновления элемента, поэтому обработчик будет вызван еще раз. (Так как теперь поле **Added to Inventory** [Добавлен в запасы] имеет значение **Yes** [Да], обработчик не будет еще раз добавлять одну и ту же отгрузку на склад, но он будет вызван.) 
    
    Когда событие обновления элемента возникает вследствие обновления программным путем, SharePoint ведет себя немного по-другому: *он включает (в **AfterProperties**) только те поля, которые были изменены при обновлении.* Таким образом, поле **Arrived** (Прибыл) будет отсутствовать, так как было изменено только поле **Added to Inventory** (Добавлен в запасы). При выполнении строки
    
     `var arrived = Convert.ToBoolean(properties.ItemEventProperties.AfterProperties["Arrived"]);`
    
     возникнет исключение **KeyNotFoundException**. 
    
    Существует несколько способов решения этой проблемы. В данном примере мы собираемся перехватить исключение и использовать блок **catch**, чтобы присвоить параметру `successFlag` значение **false** (Ложь). Благодаря этому элемент не будет обновлен в третий раз.
    
    Добавьте все в метод, который находится между первой строкой (`bool successFlag = false;`) и последней строкой (`return successFlag;`) в блоке **try**.
    
 
12. Добавьте указанный ниже блок **catch** сразу же после блока **try**.
    
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

13. Добавьте указанный ниже метод в класс  `RemoteEventReceiver1`. Этот шаблон кода должен быть знаком вам по предыдущим статьям этой серии. Тем не менее есть одно отличие. Код получает объект **ClientContext**, вызывая метод **TokenHelper.CreateRemoteEventReceiverClientContext**, а не метод **SharePointContext.CreateUserClientContextForSPHost**, который мы использовали в коде, который вызывался в SharePoint из страниц, например из страницы EmployeeAdder. Основная причина использования разных методов для получения объекта **ClientContext** состоит в том, что SharePoint передает приемникам событий информацию, необходимую для создания таких объектов, другим способом, чем страницам. В случае приемников событий он передает объект **SPRemoteEventProperties**, а в случае страниц он передает специальное поле, называемое маркером контекста, в тексте запроса, запускающего страницу надстройки.
    
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

14. Сохраните и закройте файл кода приемника.
    
 

## <a name="register-the-receiver"></a>Регистрация приемника

Последняя задача, которую необходимо выполнить, — это сообщить SharePoint, что у нас имеется пользовательский приемник, и мы хотим, чтобы SharePoint вызывал его при обновлении элемента в списке **Expected Shipments** (Ожидаемые отгрузки).
 

 

1. Откройте файл SharePointContentDeployer.cs и добавьте указанную ниже строку в метод  `DeployChainStoreComponentsToHostWeb` сразу же за строкой, в которой создается список **Expected Shipments** (Ожидаемые отгрузки). Мы добавим этот метод на следующем этапе. Обратите внимание, что в метод мы передаем объект **HttpRequest**, который начальная страница надстройки передавала в метод  `DeployChainStoreComponentsToHostWeb`.
    
```C#
  RegisterExpectedShipmentsEventHandler(request);
```

2. Добавьте указанный ниже метод в класс `SharePointComponentDeployer`.
    
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

3. Замените  `TODO16` указанными ниже строками. Обратите внимание, что для приемников событий существует "легковесный" класс ***CreationInformation**, аналогичный тому, который используется для списков и элементов списков.
    
```C#
  EventReceiverDefinitionCreationInformation receiver = new EventReceiverDefinitionCreationInformation();
receiver.ReceiverName = "ExpectedShipmentsItemUpdated";
receiver.EventType = EventReceiverType.ItemUpdated;

 // TODO17: Set the URL of the receiver.

expectedShipmentsList.EventReceivers.Add(receiver);

```

4. Теперь вам необходимо сообщить SharePoint URL-адрес приемника событий. В рабочей среде это будет тот же домен, что и для удаленных страниц (с путем /Services/RemoteEventReceiver1.svc). Так как обработчик зарегистрирован в коде, выполняемом при первом запуске и размещенном в начальной странице надстройки, то домен находится в заголовке узла объекта **HttpRequest** для запроса, вызвавшего эту страницу. Наш код передал этот объект из страницы в метод `DeployChainStoreComponentsToHostWeb`, который затем передал его в метод `RegisterExpectedShipmentsEventHandler`. Так что мы можем задать URL-адрес приемника с помощью указанного ниже кода.
    
     `receiver.ReceiverUrl = "https://" + request.Headers["Host"] + "/Services/RemoteEventReceiver1.svc";`
    
    К сожалению, этот способ не будет работать при отладке надстройки в Visual Studio. Когда вы выполняете отладку, приемник размещен в служебной шине Azure, а не по URL-адресу localhost, по которому размещены удаленные страницы. Нам необходимо использовать разные URL-адреса для приемника в зависимости от того, выполняем ли мы отладку, поэтому замените  `TODO17` указанной ниже структурой, в которой используются директивы компилятора C#. Обратите внимание, что в режиме отладки URL-адрес приемника считывается из параметра web.config. *Вы создадите этот параметр на одном из следующих этапов.* 
    


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

5. Добавьте указанный ниже оператор **using** в начало файла.
    
```C#
  using System.Web.Configuration;
```

6. Чтобы убедиться, что параметр `DEBUG` имеет значение true (Истина) тогда и только тогда, когда надстройка находится в состоянии отладки, выполните указанную ниже подпроцедуру.
    
1. В **обозревателе решений** щелкните правой кнопкой мыши проект **ChainStoreWeb** и выберите пункт **Свойства**.
    
 
2. В разделе **Свойства** откройте вкладку **Сборка**, а затем в раскрывающемся списке **Конфигурация** вверху выберите пункт **Отладить**.
    
 
3. Проверьте, установлен ли флажок **Определять константу DEBUG** (обычно он установлен по умолчанию). На снимке экрана ниже показаны правильные настройки.
    
  ![Вложенная вкладка "Сборка" вкладки "Свойства" в Visual Studio. В раскрывающемся списке "Конфигурация" выбран пункт "Отладка". Установлен флажок "Определить константу DEBUG".](../../images/4f81174f-d875-4a9e-bff4-adea0f176f00.PNG)
 

 

 
4. В раскрывающемся списке **Конфигурация** выберите пункт **Выпуск**, а затем убедитесь, что флажок **Определять константу DEBUG** ***не*** установлен (обычно по умолчанию он не установлен). На снимке экрана ниже показаны правильные настройки.
    
  ![Вложенная вкладка "Сборка" вкладки "Свойства". В раскрывающемся списке "Конфигурация" выбран пункт "Выпуск". Флажок "Определить константу DEBUG" не установлен.](../../images/7fd942de-a324-4f70-a750-f5304c993832.PNG)
 

 

 
5. Если вы внесли какие-либо изменения, сохраните их, а затем закройте вкладку **Свойства**.
    
 
7. Откройте файл web.config, а затем добавьте указанную ниже разметку в качестве дочерней разметки для элемента **appSettings**. Мы получим значение этого параметра в следующем разделе.
    
```XML
  <add key="RERdebuggingServiceBusUrl" value="" />
```


## <a name="get-the-receiver-url-for-debugging"></a>Получение URL-адреса приемника для отладки

Приемники событий надстройки и событий элементов списков представляют собой службы WCF, при этом каждая такая служба "знает" свою конечную точку и хранит ее в разных местах, включая объект **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**. Когда вы выполняете отладку, приемник надстройки размещен в конечной точке служебной шины Azure, которая почти такая же, как и конечная точка для приемника элемента списка. Разница состоит в том, что URL-адрес конечной точки надстройки имеет окончание AppEventReceiver.svc, а URL-адрес приемников элементов списков — RemoteEventReceiver1.svc. Таким образом, мы можем получить URL-адрес конечной точки в приемнике надстройки, немного изменить его окончание, а затем использовать его в качестве значения параметра **RERdebuggingServiceBusUrl** в файле web.config.
 

 

1. Откройте файл AppEventReceiver.svc.cs в папке **Services** (Службы) проекта **ChainStoreWeb**.
    
 
2. Добавьте указанный ниже код в качестве самой первой строки в методе **ProcessEvent**.
    
```C#
  string debugEndpoint = System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri.ToString(); 
```

3. Добавьте точку останова в следующую строку метода.
    
 
4. Нажмите клавишу F5, чтобы выполнить отладку надстройки. Так как файл web.config открыт, а пакет Инструменты разработчика Office для Visual Studio изменяет параметр при каждом нажатии клавиши F5, вам будет предложено перезагрузить его. Выберите вариант **Да**. 
    
 
5. При достижении точки останова наведите курсор на переменную  `debugEndpoint`. Когда появится подсказка по данным Visual Studio, щелкните стрелку вниз и выберите пункт **Средство визуализации текста**.
    
  ![Визуализатор текста в Visual Studio с URL-адресом служебной шины Azure.](../../images/494cf01e-3e17-4092-b239-9312ac4ab258.PNG)
 

 

 
6. Скопируйте значение строки из средства визуализации и вставьте его куда-нибудь.
    
 
7. Закройте средство визуализации, а затем остановите отладку в Visual Studio.
    
 
8. Удалите или закомментируйте строку, которую вы добавили на втором этапе этой процедуры, а затем удалите точку останова.
    
 
9. В скопированной вами строке замените текст AppEventReceiver.svc в конце текстом RemoteEventReceiver1.svc.
    
 
10. Скопируйте и вставьте измененный URL-адрес в качестве значения ключа **RERdebuggingServiceBusUrl** в файле web.config.
    
 

 **Примечание.** Ручное копирование URL-адреса служебной шины и вставка его (измененной версии) в файл web.config — это не единственный способ удовлетворить потребность в различных URL-адресах при отладке удаленного приемника событий, когда он выполняется в рабочей среде. Мы могли бы программным способом сохранить значение параметра **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri** где-нибудь в SharePoint или в удаленной базе данных, а затем наш код, выполняющийся при первом запуске, считал бы это значение и назначил бы его свойству `receiver.ReceiverUrl`. Мы могли бы зарегистрировать приемник событий элементов списков в качестве части обработчика событий, установленного надстройкой. Затем мы могли бы программным способом считать значение параметра **System.ServiceModel.OperationContext.Current.Channel.LocalAddress.Uri**, изменить его, а затем назначить его параметру `receiver.ReceiverUrl`, не сохраняя его нигде. При использовании этой стратегии также понадобилось бы создать список **Expected Shipments** (Ожидаемые отгрузки) в обработчике событий, установленном надстройкой, так как он должен существовать, прежде чем в нем будет зарегистрирован обработчик. (Кроме того, учтите, что мы могли бы объединить наш приемник событий надстройки и приемник событий элемента списка в один приемник (например, использовать одни и те же SVC- и SVC.CS-файлы). В этом случае не потребовалось бы изменять URL-адрес перед использованием его в качестве значения для параметра `receiver.ReceiverUrl`.) 
 


## <a name="run-the-add-in-and-test-the-list-item-receiver"></a>Запуск надстройки и тестирование приемника элемента списка


 

 

1. Откройте страницу **Содержимое сайта** веб-сайта магазина в Гонконге *и удалите список **Expected Shipments** (Ожидаемые отгрузки), если он там есть.* 
    
 
2. Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint и немедленно запускает ее. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.
    
 
3. Когда откроется начальная страница надстройки, нажмите кнопку **Вернуться на сайт** на расположенном в верхней части элементе управления хрома.
    
 
4. С начальной страницы магазина в Гонконге перейдите на страницу **Содержание сайта** и откройте список **Expected Shipments** (Ожидаемые отгрузки).
    
 
5. Создайте элемент и обратите внимание, что в форме нового элемента не отображаются поля **Arrived** (Прибыл) и **Added to Inventory** (Добавлен в запасы).
    
 
6. После создания элемента повторно откройте его для внесения изменений. Установите флажок **Arrived** (Прибыл) и сохраните элемент. В результате этих действий будет создано событие обновления элемента. Элемент будет добавлен в запасы, а значение поля **Added to Inventory** (Добавлен в запасы) будет изменено на **Yes** (Да). Чтобы отобразить изменения в поле **Added to Inventory** (Добавлен в запасы) вам, возможно, потребуется обновить страницу.
    
 
7. Нажимайте кнопку "Назад" в браузере, пока вы не вернетесь на начальную страницу надстройки Chain Store, а затем нажмите кнопку **Show Inventory** (Отобразить запасы). Теперь в списке появится элемент, для которого вы задали значение **Arrived** (Прибыл).
    
 
8. Перейдите обратно к списку **Expected Shipments** (Ожидаемые отгрузки) и добавьте другой элемент * с точно такими же именем продукта и названием поставщика*, но с другим количеством.
    
 
9. После создания элемента повторно откройте его для внесения изменений. Измените значение поля **Arrived** (Прибыл) на **Yes** (Да) и сохраните элемент.
    
 
10. Нажимайте кнопку "Назад" в браузере, пока вы не вернетесь на начальную страницу надстройки Chain Store, а затем нажмите кнопку **Show Inventory** (Отобразить запасы). В списке будет по-прежнему один элемент с нужными нами названиями продукта и поставщика, но теперь его количество будет представлять собой сумму количеств двух элементов в списке **Expected Shipments** (Ожидаемые отгрузки).
    
 
11. Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.
    
 
12. Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.
    
 

## 
<a name="Nextsteps"> </a>

Сведения о том, как публиковать надстройки на сайте SharePoint см. в статье  [Развертывание и установка надстроек для SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options). Углубленные сведения о разработке надстроек SharePoint см. на указанных ниже узлах MSDN.
 

 

-  [Проектирование надстроек SharePoint](design-sharepoint-add-ins)
    
 
-  [Разработка надстроек SharePoint](develop-sharepoint-add-ins)
    
 
-  [Публикация надстроек SharePoint](publish-sharepoint-add-ins)
    
 
-  [Средства и среды для разработки надстроек SharePoint](tools-and-environments-for-developing-sharepoint-add-ins)
    
 

