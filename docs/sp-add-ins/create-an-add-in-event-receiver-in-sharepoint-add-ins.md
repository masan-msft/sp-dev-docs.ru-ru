---
title: Создание приемника событий надстройки в надстройках для SharePoint
description: Создайте обработчики для событий установки и удаления надстройки в надстройках SharePoint.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: c5b909ae48ce6fc6178829a7aade19355d53220a
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="create-an-add-in-event-receiver-in-sharepoint-add-ins"></a>Создание приемника событий в надстройках SharePoint

Для начала желательно иметь представление о надстройках SharePoint с размещением у поставщика, а также разработать несколько надстроек, которые были бы хоть немного сложнее уровня "Hello World". См. статью [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).

Кроме того, следует ознакомиться со статьей [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md). 

## <a name="get-more-code-samples"></a>Дополнительные примеры кода

Ознакомившись с развернутым примером, приведенным в этой статье, вы получите готовый пример кода. Ниже представлены другие примеры. Не все они соответствуют архитектуре, описанной в этой статье. Существует несколько хороших способов создать приемник событий надстроек. Кроме того, помните, что руководства от Майкрософт могут изменяться со временем. 

- Пример кода [SharePoint/PnP/Samples/Core.AppEvents.HandlerDelegation](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation) наиболее близко соответствует примеру, приведенному в этой статье.
- В [SharePoint/PnP/Samples/Core.AppEvents](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents) показано, как решить задачу, аналогичную приведенной в предыдущем примере кода, когда нельзя использовать стратегию делегирования обработчиков.
- [SharePoint/PnP/Samples/Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers)
- [Создание надстройки с размещением у поставщика, которая настраивает установку надстройки](https://code.msdn.microsoft.com/sharepoint-2013-create-a-f27752e0)
    

## <a name="add-an-add-in-installed-event-receiver"></a>Добавление приемника событий установки надстройки

1. Откройте в Visual Studio проект размещаемого у поставщика Надстройка SharePoint (при добавлении обработчика события к надстройке, размещаемой в SharePoint, Инструменты разработчика Office для Visual Studio преобразует ее в надстройку, размещаемую у поставщика).

2. В **обозревателе решений** выберите узел для надстройки SharePoint.

3. В окне **Свойства** задайте для параметра **Управление установленными надстройками** значение **True**. 
    
    ![События приложения в окне свойств](../images/SP_VS_Properties_Window_AppEvents.PNG)
 
    Инструменты разработчика Office для Visual Studio делают следующее:

    - Добавляют файл AppEventReceiver.svc, содержащий скелетный код на языке C# (или VB.NET). Это служба, которая будет обрабатывать событие надстройки.

    - Добавляют в раздел **Свойства** файла AppManifest.xml следующую запись: `<InstalledEventEndpoint>~remoteAppUrl/AppEventReceiver.svc</InstalledEventEndpoint>`. Она регистрирует приемник событий надстройки в SharePoint. 
    
        > [!NOTE] 
        > Маркер **~remoteAppUrl** также используется для удаленного веб-приложения в надстройке SharePoint с размещением у поставщика. Инструменты разработчика Office для Visual Studio предполагают, что домены веб-приложения и обработчика событий совпадают. В редких случаях, когда это не так, необходимо вручную заменить маркер **~remoteAppUrl** настоящим доменом службы.
 
    - Создают веб-проект, если в проекте надстройки SharePoint его еще нет. Кроме того, эти инструменты также проверяют, настроен ли манифест надстройки для размещения у поставщика. Они также добавляют страницы, сценарии, CSS-файлы и другие артефакты. Если из удаленных компонентов надстройки требуется только веб-служба обработки событий, вы можете удалить их из проекта. Кроме того, проверьте, чтобы элемент **StartPage** в манифесте надстройки не указывал на удаленную страницу.
 
4. Если Visual Studio и ваша тестовая ферма SharePoint развернуты на разных компьютерах, настройте проект для отладки с помощью служебной шины Microsoft Azure. Дополнительные сведения см. в статье [Устранение неполадок и отладка удаленного приемника событий в надстройке SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md). 

5. Если в файле AppEventReceiver.svc есть метод `ProcessOneWayEvent`, его реализация должна содержать только строку `throw new NotImplementedException();`, поскольку этот метод невозможно использовать в обработчике событий надстройки. 

    *Обработчики событий надстройки должны возвращать объект, который сообщает среде SharePoint, следует ли завершить событие или отменить его, а метод `ProcessOneWayEvent` не возвращает никаких данных.* 

6. Файл будет включать метод `ProcessEvent`, который имеет следующий вид. (Он также может содержать блок кода, который иллюстрирует получение контекста клиента. Удалите или закомментируйте его.) 

    ```C#
    public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
    {
        SPRemoteEventResult result = new SPRemoteEventResult();

        return result;
    }
    ``` 

    Обратите внимание на следующие особенности этого кода:

    - Объект **SPRemoteEventProperties** отправляется веб-службе обработчика в виде сообщения SOAP, которое содержит контекстные сведения из SharePoint, включая свойство **EventType**, которое идентифицирует событие.
 
    - Объект **SPRemoteEventResult**, возвращаемый обработчиком, содержит свойство **Status**, которое может принимать значения **SPRemoteEventServiceStatus.Continue**, **SPRemoteEventServiceStatus.CancelNoError** и **SPRemoteEventServiceStatus.CancelWithError**. По умолчанию свойство **Status** имеет значение **Continue**, которое сообщает среде SharePoint, что необходимо завершить событие. Остальные два значения сообщают SharePoint, что нужно:
    
        - Запустить обработчик еще три раза.
        - Если обработчик по-прежнему получает состояние "Отмена", отмените событие и выполните полный откат всех изменений, выполненных в рамках этого события. 

7. Сразу после строки объявления переменной `result` добавьте следующую развилку, чтобы определить, какое событие обрабатывается.
        
    ```C#
    switch (properties.EventType)
    {
        case SPRemoteEventType.AppInstalled:
            break;
        case SPRemoteEventType.AppUpgraded:
            break;
        case SPRemoteEventType.AppUninstalling:
            break;
    }
    ```

    > [!NOTE] 
    > Если у вас есть обработчики для событий **AppInstalled**, **AppUpdated** и **AppInstalling**, каждый из них получает собственный URL-адрес, зарегистрированный в манифесте надстройки. Таким образом, они *могут* иметь разные конечные точки, но в этой статье (и Инструментах разработки Office для Visual Studio) предполагается, что они имеют одну и ту же конечную точку, поэтому в коде должно быть определено, какое событие ее вызвало.

8. Как объясняется в разделе [Включение логики отката и логики проверки выполненных действий в обработчики событий надстроек](handle-events-in-sharepoint-add-ins.md#Rollback), если в логике установки происходит сбой, почти всегда следует отменять установку: среда SharePoint должна отменить действия, выполненные для установки, а вам нужно отменить все действия, выполненные обработчиком. 

    Для этого можно добавить следующий код в оператор **case** для события AppInstalled.
    
    ```C#
    case SPRemoteEventType.AppInstalled:
    try
    {
        // Add-in installed event logic goes here.
    }
    catch (Exception e)
    {
        result.ErrorMessage = e.ErrorMessage;
        result.Status = SPRemoteEventServiceStatus.CancelWithError;

        // Rollback logic goes here.
    }
    break;
    ```

    > [!NOTE] 
    > Переместите код установки, который занимает более 30 секунд, в саму надстройку. Вы можете добавить его в код, выполняемый при первом запуске надстройки. Надстройка может показывать сообщение типа "Идет подготовка". Кроме того, надстройка может предложить пользователю запустить код инициализации.
    
    > Если логика первого запуска не подходит для вашей надстройки, обработчик события может запускать удаленный асинхронный процесс, а затем сразу возвращать объект **SPRemoteEventResult**, где для свойства **Status** задано значение **Continue**. Недостаток этого подхода заключается в том, что невозможно сообщить среде SharePoint о необходимости отменить установку надстройки.

9. Как описано в разделе [Стратегии архитектуры обработчиков событий надстройки](handle-events-in-sharepoint-add-ins.md#Strategies), стратегия делегирования обработчиков предпочтительна, но ее можно использовать не во всех сценариях. В данном примере показано, как реализовать стратегию делегирования обработчиков при добавлении списка на хост-сайт. Сведения о том, как создать похожий обработчик события AppInstalled, не использующий стратегию делегирования обработчиков, см. в примере [SharePoint/PnP/Samples/Core.AppEvents](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents).
    
    Ниже представлена новая версия блока **case** для события AppInstalled. Обратите внимание, что логика инициализации, которая применяется ко всем событиям, находится над блоком **switch**. Так как устанавливаемый список удаляется в обработчике события AppUninstalling, этот список определяется там же.

    ```C#
    SPRemoteEventResult result = new SPRemoteEventResult();
    String listTitle = "MyList";

    switch (properties.EventType)
    {               
        case SPRemoteEventType.AppInstalled:
                        
    try
    {
            string error = TryCreateList(listTitle, properties);
            if (error != String.Empty)
            {
                throw new Exception(error);            
            }
    }
        catch (Exception e)
    {
            // Tell SharePoint to cancel the event.
            result.ErrorMessage = e.Message;
            result.Status = SPRemoteEventServiceStatus.CancelWithError;               
        }
            break;
        case SPRemoteEventType.AppUpgraded:
        break;
        case SPRemoteEventType.AppUninstalling:
        break;
    }                      
    ```

10. Добавьте метод создания списка в класс **AppEventReceiver** как метод **private** со следующим кодом. Обратите внимание, что класс `TokenHelper` содержит специальный метод, оптимизированный для получения контекста клиента для события надстройки. Значение **false** для последнего параметра указывает, что контекст предназначен для хост-сайта.
    
    ```C#
    private string TryCreateList(String listTitle, SPRemoteEventProperties properties)
    {    
        string errorMessage = String.Empty;          

        using (ClientContext clientContext =
            TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
        {
            if (clientContext != null)
            {
            }
        }
        return errorMessage;
    }

    ```

11. Логика отката, по сути, является логикой обработки исключений, а SharePoint CSOM (клиентская объектная модель) включает область **ExceptionHandlingScope**, которая позволяет веб-службе делегировать обработку исключений серверу SharePoint (см. статью [Использование области обработки исключений](http://msdn.microsoft.com/library/103619ef-1ba3-44e3-93e1-5e0685bc616e%28Office.15%29.aspx)). 

    Добавьте следующий код в блок **if** предыдущего фрагмента.
    
    ```C#
    ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext); 

    using (scope.StartScope()) 
    { 
        using (scope.StartTry()) 
        { 
        }         
        using (scope.StartCatch()) 
        {                                 
        } 
        using (scope.StartFinally()) 
        { 
        } 
    } 
    clientContext.ExecuteQuery();

    if (scope.HasException)
    {
        errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
            scope.ServerErrorTypeName, scope.ErrorMessage, 
            scope.ServerErrorDetails, scope.ServerErrorValue, 
            scope.ServerStackTrace, scope.ServerErrorCode);
    }
    ```

12. Предыдущий фрагмент содержит только один вызов SharePoint (**ExecuteQuery**), и этого недостаточно. Каждый объект, который будет указан в области исключений, необходимо сначала загрузить в клиент. 

    Добавьте следующий код *перед* конструктором **ExceptionHandlingScope**.
    
    ```C#
    ListCollection allLists = clientContext.Web.Lists;
    IEnumerable<List> matchingLists =
        clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
    clientContext.ExecuteQuery();

    var foundList = matchingLists.FirstOrDefault();
    List createdList = null;
    ```

13. Код для создания списка хост-сайтов добавляется в блок **StartTry**, но сначала код должен проверить, был ли этот список уже добавлен (как описывается в разделе [Включение логики отката и логики проверки выполненных действий в обработчики событий надстроек](handle-events-in-sharepoint-add-ins.md#Rollback)). Логику If-Then-Else можно делегировать серверу SharePoint с помощью класса **ConditionalScope** (см. статью [Использование условной области](http://msdn.microsoft.com/library/560112e9-c3ed-4b8f-9cd4-c8bc5d60d63c%28Office.15%29.aspx)). 

    Добавьте следующий код в блок **StartTry**.
    
    ```C#
    ConditionalScope condScope = new ConditionalScope(clientContext, 
            () => foundList.ServerObjectIsNull.Value == true, true);
    using (condScope.StartScope())
    {
        ListCreationInformation listInfo = new ListCreationInformation();
        listInfo.Title = listTitle;
        listInfo.TemplateType = (int)ListTemplateType.GenericList;
        listInfo.Url = listTitle;
        createdList = clientContext.Web.Lists.Add(listInfo);                                
    }
    ```

14. Блок **StartCatch** должен отменить создание списка, но для начала он должен проверить, создан ли список, так как исключение могло быть выдано в блоке **StartTry** до завершения создания списка. 

    Добавьте следующий код в блок **StartCatch**.
    
    ```C#
    ConditionalScope condScope = new ConditionalScope(clientContext, 
            () => createdList.ServerObjectIsNull.Value != true, true);
    using (condScope.StartScope())
    {
        createdList.DeleteObject();
    } 
    ```

    > [!TIP] 
    > **УСТРАНЕНИЕ НЕПОЛАДОК.** Чтобы проверить, вводится ли ваш блок **StartCatch**, когда положено, вам необходимо вызвать исключение среды выполнения на сервере SharePoint. Использование **throw** или деления на нуль не дадут нужного результата, поскольку они вызовут исключения *на стороне клиента*, прежде чем клиентская среда выполнения сможет упаковать код и отправить его на сервер (с помощью метода **ExecuteQuery**). 
    
    > Вместо этого добавьте в блок **StartTry** следующие строки. Среда выполнения на стороне клиента принимает этот код, но он приводит к исключению на стороне сервера, что вам и нужно. 
    
    > `List fakeList = clientContext.Web.Lists.GetByTitle("NoSuchList");`
    
    > `clientContext.Load(fakeList);`

Весь метод TryCreateList должен выглядеть следующим образом. (Блок **StartFinally** является обязательным, даже если он не используется.)
    
```C#
    private string TryCreateList(String listTitle, SPRemoteEventProperties properties)
    {    
        string errorMessage = String.Empty;  

        using (ClientContext clientContext = 
            TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
        {
            if (clientContext != null)
            {
                ListCollection allLists = clientContext.Web.Lists;
                IEnumerable<List> matchingLists = 
                    clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
                clientContext.ExecuteQuery();
                var foundList = matchingLists.FirstOrDefault();
                List createdList = null;

                ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext); 
                using (scope.StartScope()) 
                { 
                    using (scope.StartTry()) 
                    { 
                        ConditionalScope condScope = new ConditionalScope(clientContext, 
                                () => foundList.ServerObjectIsNull.Value == true, true);  
                        using (condScope.StartScope())
                        {
                            ListCreationInformation listInfo = new ListCreationInformation();
                            listInfo.Title = listTitle;
                            listInfo.TemplateType = (int)ListTemplateType.GenericList;
                            listInfo.Url = listTitle;
                            createdList = clientContext.Web.Lists.Add(listInfo);
                        }
                    } 
                    
                    using (scope.StartCatch()) 
                    { 
                        ConditionalScope condScope = new ConditionalScope(clientContext, 
                                () => createdList.ServerObjectIsNull.Value != true, true);
                        using (condScope.StartScope())
                        {
                            createdList.DeleteObject();
                        }    
                    } 

                    using (scope.StartFinally()) 
                    { 
                    } 
                } 
                clientContext.ExecuteQuery();

                if (scope.HasException)
                {
                        errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
                        scope.ServerErrorTypeName, scope.ErrorMessage, 
                        scope.ServerErrorDetails, scope.ServerErrorValue, 
                        scope.ServerStackTrace, scope.ServerErrorCode);
                }
            }
        }
        return errorMessage;
    }
```

<br/>

> [!TIP] 
> **ОТЛАДКА.** Независимо от того, используется ли стратегия делегирования обработчиков, при пошаговой отладке кода с помощью отладчика помните, что когда обработчик возвращает состояние отмены, SharePoint повторно вызывает обработчик еще три раза. Поэтому отладчик может проходить код до четырех раз.

> [!TIP] 
> **АРХИТЕКТУРА КОДА.** Поскольку вы можете устанавливать компоненты на сайте надстройки с описательной разметкой вне обработчика, вам вряд ли понадобится использовать 30 секунд, доступные обработчику для взаимодействия с сайтом надстройки. Но если это произойдет, помните, что коду требуется отдельный объект **ClientContext** для сайта надстройки. Это означает, что сайт надстройки и хост-сайт отличаются друг от друга так же, как база данных SQL Server отличается от каждого из этих компонентов. Таким образом, метод, который отправляет вызов на сайт надстройки, находится в блоке **try** блока **case** для события AppInstalled, как и метод TryCreateList в следующем примере. Однако обработчику *не* требуется отменять действия, выполненные на сайте надстройки. Если он обнаруживает ошибку, он просто отменяет событие, так как SharePoint удаляет весь сайт надстройки в случае отмены события.

## <a name="create-an-add-in-uninstalling-event-receiver"></a>Создание приемника событий удаления надстройки

1. Задайте для свойства **Управление удалением надстроек** проекта значение **True**. Инструменты *не* создают еще один файл веб-службы, если такой файл уже существует, но добавляют элемент **UninstallingEventEndpoint** в манифест надстройки.

2. Код в блоке **case** события AppUninstalling должен удалять элементы надстройки, в которых нет необходимости после удаления этой надстройки из второй корзины. Тем не менее, по мере возможности следует "прекращать использование" компонентов, а не полностью удалять их. Это связано с тем, что в случае отмены события удаления их потребуется восстановить. В этом случае надстройка останется во второй корзине, а пользователь сможет восстановить ее и использовать снова. Для восстановления работоспособности надстройки может быть достаточно заново создать удаленный компонент, но все данные и параметры конфигурации в компоненте будут потеряны.
    
    Эту стратегию относительно легко использовать для компонентов SharePoint, так как в SharePoint есть корзина, из которой можно восстанавливать объекты, а также существуют API-интерфейсы CSOM для доступа к ней. В следующих разделах показано, как это сделать. Для других платформ могут потребоваться другие методы. Например, если вам нужно удалить строку из таблицы SQL Server в обработчике удаления надстройки, хранимая процедура T-SQL в обработчике может добавить в таблицу столбец IsDeleted и присвоить ему значение **True** в этой строке. Если происходит ошибка, логика отката восстанавливает значение **False**. Если процедура завершается без ошибок, то непосредственно перед возвратом соответствующего флага она может задать таймер, чтобы удалить эту строку позже.
    
    Иногда требуется сохранить данные, например списки, даже после удаления надстройки; однако в качестве примера ниже представлен обработчик события, который удаляет список, созданный обработчиком события установки.

    ```C#
    case SPRemoteEventType.AppUninstalling:

    try
    {
        string error = TryRecycleList(listTitle, properties);
        if (error != String.Empty)
        {
            throw new Exception(error);
        }
    }
    catch (Exception e)
    {
        // Tell SharePoint to cancel the event.
        result.ErrorMessage = e.Message;
        result.Status = SPRemoteEventServiceStatus.CancelWithError;
    }
    break;
    ```

3. Добавьте вспомогательный метод для повторного использования списка. Обратите внимание на следующие особенности этого кода:
    
    - Код перемещает список в корзину, а не безвозвратно удаляет его. Это позволяет восстановить его, включая все данные, в случае сбоя события, что и делает блок **StartCatch**. Таким образом, если метод выполнится успешно, а событие завершится, то надстройка будет безвозвратно удалена со второго уровня корзины, но список останется на первом ее уровне.
    
    - Код проверяет наличие списка, прежде чем удалять его, поскольку пользователь уже мог удалить список с помощью пользовательского интерфейса SharePoint. Аналогичным образом, код отката проверяет наличие списка в корзине, прежде чем восстанавливать его, поскольку пользователь мог восстановить список или переместить его на второй уровень корзины. 
    
    - Есть две условные области, которые проверяют существование списка, определяя, имеет ли ссылка на него значение **null**. Но обе области содержат внутренний блок **if**, который повторно проверяет тот же объект на нулевое значение. Внешние проверки с блоками условных областей выполняются на сервере, но внутренние проверки на нулевое значение также необходимы. Это связано с тем, что среда выполнения клиента построчно просматривает код для создания XML-сообщения, которое метод **ExecuteQuery** отправит на сервер. По достижении ссылок на объекты **foundList** и **recycledList** одна из этих строк вызывает исключение Null Reference, если они не заключены во внутренние проверки на нулевые значения.
 
        ```C#
        private string TryRecycleList(String listTitle, SPRemoteEventProperties properties)
        {
            string errorMessage = String.Empty;

            using (ClientContext clientContext = 
                TokenHelper.CreateAppEventClientContext(properties, useAppWeb: false))
            {
                if (clientContext != null)
                {
                    ListCollection allLists = clientContext.Web.Lists;
                    IEnumerable<List> matchingLists = 
                        clientContext.LoadQuery(allLists.Where(list => list.Title == listTitle));
                    RecycleBinItemCollection bin = clientContext.Web.RecycleBin;
                    IEnumerable<RecycleBinItem> matchingRecycleBinItems = 
                        clientContext.LoadQuery(bin.Where(item => item.Title == listTitle));        
                    clientContext.ExecuteQuery();

                    List foundList = matchingLists.FirstOrDefault();
                    RecycleBinItem recycledList = matchingRecycleBinItems.FirstOrDefault();    

                    ExceptionHandlingScope scope = new ExceptionHandlingScope(clientContext);
                    using (scope.StartScope())
                    {
                        using (scope.StartTry())
                        {
                            ConditionalScope condScope = new ConditionalScope(clientContext, 
                                () => foundList.ServerObjectIsNull.Value == false, true);
                            using (condScope.StartScope())
                            {
                                if (foundList != null)
                                {
                                    foundList.Recycle();
                                }
                            }
                        }
                        using (scope.StartCatch())
                        {
                            ConditionalScope condScope = new ConditionalScope(clientContext, 
                                () => recycledList.ServerObjectIsNull.Value == false, true);
                            using (condScope.StartScope())
                            {
                                if (recycledList != null)
                                {
                                    recycledList.Restore(); 
                                }
                            }
                        }
                        using (scope.StartFinally())
                        {
                        }
                    }
                    clientContext.ExecuteQuery();

                    if (scope.HasException)
                    {
                        errorMessage = String.Format("{0}: {1}; {2}; {3}; {4}; {5}", 
                            scope.ServerErrorTypeName, scope.ErrorMessage, 
                            scope.ServerErrorDetails, scope.ServerErrorValue, 
                            scope.ServerStackTrace, scope.ServerErrorCode);
                    }
                }
            }
            return errorMessage;
        }
        ```


### <a name="to-debug-and-test-an-add-in-uninstalling-event-receiver"></a>Отладка и проверка приемника событий удаления надстройки

1. Откройте все перечисленные ниже страницы в отдельных окнах или вкладках.
    
    - Содержимое сайта.
    - Содержимое сайта — Корзина (_layouts/15/AdminRecycleBin.aspx?ql=1).
    - Корзина — Вторая корзина (_layouts/15/AdminRecycleBin.aspxView=2&amp;?ql=1).
    
 
2. Нажмите клавишу F5 и укажите, что необходимо доверять надстройке. Откроется начальная страница надстройки. Если вы собираетесь лишь протестировать обработчик удаления, окно браузера можно закрыть. *Но если вы отлаживаете обработчик, оставьте его открытым. При закрытии окна сеанс отладки завершится.* 
    
3. Обновите страницу "Содержимое сайта", а когда появится надстройка, удалите ее.

4. Обновите страницу "Параметры сайта — Корзина". Надстройка появится в начале списка. Установите флажок рядом с ней и выберите **Удалить выделенные объекты**.

5. Обновите страницу "Корзина — Вторая корзина". Надстройка появится в начале списка. Установите флажок рядом с ней и выберите **Удалить выделенные объекты**. SharePoint сразу вызовет обработчик удаления надстройки.
    

## <a name="create-an-add-in-updated-event-receiver"></a>Создание приемника событий обновления надстройки

Дополнительные сведения о создании обработчика для события обновления надстройки см. в [этой статье](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md).

## <a name="url-and-hosting-restrictions-on-production-add-in-event-receivers"></a>Ограничения в отношении URL-адреса и размещения производственных приемников событий надстройки

Удаленный приемник событий может быть размещен в облаке или на локальном сервере, который не используется в качестве сервера SharePoint. URL-адрес производственного приемника не может использовать определенный порт. Это значит, что вам необходимо использовать порт 443 для протокола HTTPS (рекомендовано) или порт 80 для HTTP. Если вы используете HTTPS, приемник размещен локально, а надстройка находится в SharePoint Online, сервер размещения должен иметь доверенный сертификат, выданный центром сертификации. (Самозаверяющий сертификат подходит, только если надстройка расположена в локальной ферме SharePoint.)
    
## <a name="see-also"></a>Дополнительные ресурсы

- [Обработка событий в надстройках SharePoint](handle-events-in-sharepoint-add-ins.md) 

