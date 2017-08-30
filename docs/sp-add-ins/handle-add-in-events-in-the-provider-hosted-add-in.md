# <a name="handle-add-in-events-in-the-provider-hosted-add-in"></a><span data-ttu-id="61208-101">Обработка событий надстройки, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="61208-101">Handle add-in events in the provider-hosted add-in</span></span>
<span data-ttu-id="61208-102">Узнайте, как настроить установку надстройки SharePoint, размещаемой у поставщика.</span><span class="sxs-lookup"><span data-stu-id="61208-102">Learn how to customize the installation of a provider-hosted spappsing.</span></span>
 

 <span data-ttu-id="61208-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="61208-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="61208-p102">Это седьмая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="61208-p102">Learn how to customize the installation of a provider-hosted SharePoint Add-in. This is the seventh in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 

-  [<span data-ttu-id="61208-108">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="61208-108">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="61208-109">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="61208-109">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel)
    
 
-  [<span data-ttu-id="61208-110">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="61208-110">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="61208-111">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="61208-111">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model)
    
 
-  [<span data-ttu-id="61208-112">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="61208-112">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in)
    
 
-  [<span data-ttu-id="61208-113">Добавление веб-части надстройки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="61208-113">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in)
    
 

 <span data-ttu-id="61208-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeAdd-inEventHandlers.sln.</span><span class="sxs-lookup"><span data-stu-id="61208-p103">**Note** If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeAdd-inEventHandlers.sln file.</span></span>
 

<span data-ttu-id="61208-p104">В данной статье мы настроим в SharePoint обработку событий, называемых событиями надстройки. Точнее мы создадим обработчики событий установки и удаления надстройки. Кроме того, настраиваемые обработчики можно использовать и для событий списка и элементов списка. О таких обработчиках вы узнаете в одной из следующих статей этой серии. Все эти события создаются в SharePoint, но пользовательский код, обрабатывающий каждое событие, находится в вашем удаленном веб-приложении. Вы настроите SharePoint, чтобы он вызывал настраиваемый обработчик, зарегистрировав URL-адрес обработчика для события SharePoint.</span><span class="sxs-lookup"><span data-stu-id="61208-p104">In this article, we will customize the handling of a kind of event in SharePoint, called add-in events. Specifically, we will create handlers for the add-in installation and uninstallation events. There are also list and list item events that can get custom handling. You'll learn about these in a later article in this series. All of these events are triggered in SharePoint, but your custom code that handles each event is in your remote web application. You configure SharePoint to call your custom handler by registering the handler's URL with the SharePoint event.</span></span>
 

## <a name="two-places-to-programmatically-deploy-sharepoint-components"></a><span data-ttu-id="61208-122">Два способа развертывания компонентов SharePoint программным путем</span><span class="sxs-lookup"><span data-stu-id="61208-122">Two places to programmatically deploy SharePoint components</span></span>

<span data-ttu-id="61208-p105">Мы хотим, чтобы наша надстройка "Сеть магазинов" автоматически создавала и развертывала списки **Местные сотрудники** и **Ожидаемые отгрузки**. Надстройка может в любое время развертывать компоненты SharePoint, например настраиваемые списки. Однако если надстройка зависит от определенного компонента, например настраиваемого списка, этот компонент необходимо развернуть *до того*, как пользователи начнут работать с надстройкой. Для таких критически важных компонентов пользовательский код, выполняющий развертывание, можно разместить в двух местах:</span><span class="sxs-lookup"><span data-stu-id="61208-p105">We want our Chain Store add-in to create and deploy the **Local Employees** and **Expected Shipments** lists automatically. An add-in can deploy SharePoint components, such as a custom list, any time. But when an add-in depends on a specific component, such as a custom list, then the component really should be deployed *before*  users start working with the add-in. For such vital components, there are two places where the custom deployment logic can go:</span></span>
 

 

- <span data-ttu-id="61208-127">в обработчике события установки для надстройки;</span><span class="sxs-lookup"><span data-stu-id="61208-127">In a handler for the add-in installation event.</span></span>
    
 
- <span data-ttu-id="61208-128">в коде, выполняемом при первом запуске надстройки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="61208-128">In "first run" logic that executes the first time the add-in is launched in SharePoint.</span></span>
    
 
<span data-ttu-id="61208-p106">Описание процесса принятия решения о том, какой способ лучше подходит для конкретной надстройки, выходит за рамки данной статьи. В нашей статье мы приведем только несколько соображений, оказывающих влияние на выбор.</span><span class="sxs-lookup"><span data-stu-id="61208-p106">Deciding which is best for a given add-in is an advanced topic. In this article, we can only mention a few points of comparison:</span></span>
 

 

- <span data-ttu-id="61208-p107">Работа пользовательского обработчика установки должна завершиться в течение 30 секунд. Время работы логики первого запуска не ограничено.</span><span class="sxs-lookup"><span data-stu-id="61208-p107">A custom installation handler has to complete in 30 seconds. There is no limit to how long first-run logic can take.</span></span>
    
 
- <span data-ttu-id="61208-p108">Если в процессе установки надстройки что-то пойдет не так, SharePoint отменит все действия, которые он выполнил в ходе установки. Настраиваемый обработчик события установки запускается  *после*  того как SharePoint выполнит все действия, необходимые для установки надстройки, поэтому обработчик может принять участие в работе этой системы. Например, если ваш пользовательский код создал исключение, вы можете сообщить SharePoint, что необходимо полностью отменить установку надстройки. Если же что-то пойдет не так в пользовательском коде, выполняемом при первом запуске, надстройка останется установленной и, возможно, будет работать неправильно.</span><span class="sxs-lookup"><span data-stu-id="61208-p108">If anything goes wrong during an add-in installation, SharePoint will roll back everything it has done as part of the installation. A custom installation handler runs  *after*  SharePoint has done everything its going to do to install the add-in, so a custom handler can participate in this system. For example, if your custom logic throws an exception, you can tell SharePoint to roll back the entire add-in installation. If something goes wrong in custom first-run logic, however, the add-in remains installed and presumably won't work properly.</span></span>
    
 
- <span data-ttu-id="61208-p109">Если SharePoint придется отменить установку надстройки, он не "успокоится" на этом. Он сразу же попытается установить надстройку еще раз. Он совершает до 4 попыток (на каждую попытку выделяется 30 секунд). При каждой повторной попытке настраиваемый обработчик события установки запускается  *с самого начала*  . Если обработчик установил, например, список, прежде чем были отменены все действия по установке, то он будет пытаться установить этот же список при каждой новой попытке установки надстройки. Чтобы не допустить этого, необходимо написать код обработчика события установки так, чтобы он не выполнял никаких действий (например, развертывание компонента), прежде чем проверит, не было ли выполнено это действие ранее. Из-за этого код обработчика события установки сложнее кода, выполняемого при первом запуске, так как последний не выполняется повторно (если, конечно, вы намеренно не запрограммируете повторное выполнение). Кроме того, для проверки того, не развернут ли какой-либо компонент, необходимо выполнить затратный по времени вызов через Интернет от удаленного обработчика к SharePoint. После этого понадобится выполнить второй вызов для развертывания компонента (если он не был развернут ранее).</span><span class="sxs-lookup"><span data-stu-id="61208-p109">SharePoint doesn't give up if it has to roll back an add-in installation. It will immediately try the installation again. It makes up to 4 attempts (The 30 second time limit applies on each attempt.) Each time it retries, the custom installation handler runs again,  *from the beginning*  . If the handler managed to install, say, a list, before the roll back, it will try to install the same list again on the retry. To prevent this from happening, code in an installation handler has to be written so that it won't take any action (such as, deploy a component) unless if first checks to see if that action has already been done. This makes the logic of an installation handler more complex than first-run logic, since first-run logic won't retry (unless you specifically code it to do so). Also, checking to see if a component has already been deployed usually requires a time-consuming call over the internet from the remote handler to SharePoint. And then a second call is needed to actually deploy the component (if it turns not to have already been deployed).</span></span>
    
 
<span data-ttu-id="61208-p110">В надстройке Chain Store мы объединим эти стратегии. В данной статье вы создадите обработчик события установки, который будет регистрировать хост-сайт в качестве клиента в корпоративной базе данных, а затем задавать сигнал о том, была ли уже запущена надстройка на хост-сайте. В одной из следующих статей серии вы добавите код, выполняемый при первом запуске, в метод **Page_Load** начальной страницы надстройки. Этот код будет развертывать два настраиваемых списка и выполнять ряд других действий.</span><span class="sxs-lookup"><span data-stu-id="61208-p110">For the Chain Store add-in, we'll combine these strategies. In this article, you'll create an installation handler that will register the host web as a tenant in the corporate database and then set a signal that specifies whether the add-in has been run yet on the host web. In a later article in this series, you'll put first-run logic in the **Page_Load** method of the add-ins start page. This logic will deploy the two custom lists and do some other things too.</span></span>
 

 

## <a name="configure-the-solution-for-event-receiver-debugging"></a><span data-ttu-id="61208-149">Настройка решения для отладки приемника событий</span><span class="sxs-lookup"><span data-stu-id="61208-149">Configure the solution for event receiver debugging</span></span>
<span data-ttu-id="61208-150"><a name="RERDebug"> </a></span><span class="sxs-lookup"><span data-stu-id="61208-150"></span></span>

<span data-ttu-id="61208-p111">Для отладки приемников событий необходимо использовать шину обслуживания Azure. Следуйте инструкциям в статье  [Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in). Так как в качестве тестового сайта вы используете веб-сайт SharePoint Online, не забудьте выполнить эти инструкции на удаленном тестовом сайте. В следующих статьях серии подразумевается, что вы успешно настроили среду отладки.</span><span class="sxs-lookup"><span data-stu-id="61208-p111">Debugging of event receivers requires the use of the Azure Service Bus. Follow the instructions at  [Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in). Since you are using a SharePoint Online website as your test site, be sure carry out the instructions for a remote test site. The remainder of this series will assume you have configured debugging successfully.</span></span> 
 

 

## <a name="create-the-installation-handler"></a><span data-ttu-id="61208-155">Создание обработчика установки</span><span class="sxs-lookup"><span data-stu-id="61208-155">Create the installation handler</span></span>
<span data-ttu-id="61208-156"><a name="RERDebug"> </a></span><span class="sxs-lookup"><span data-stu-id="61208-156"></span></span>


 

 

 <span data-ttu-id="61208-p112">**Примечание.** Параметры запускаемых проектов в Visual Studio обычно возвращаются к значениям по умолчанию каждый раз, когда вы заново открываете решение. Открывая пример решения, рассматриваемый в этой серии статей, всегда выполняйте следующие действия: щелкните правой кнопкой мыши узел решения в **обозревателе решений** и выберите пункт **Назначить запускаемые проекты**, а затем убедитесь, что для всех трех проектов в столбце **Действие** задано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="61208-p112">**Note**   The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles: Right-click the solution node at the top of **Solution Explorer** and select **Set startup projects**.  Make sure all three projects are set to **Start** in the **Action** column.</span></span>
 


1. <span data-ttu-id="61208-160">В **обозревателе решений** выберите проект **ChainStore**, чтобы его свойства появились в области **Свойства** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61208-160">In **Solution Explorer**, select the **ChainStore** project, so its properties appear in the **Properties** pane of Visual Studio.</span></span>
    
 
2. <span data-ttu-id="61208-p113">Задайте для параметра **Управление установленными надстройками** значение **True** (этот параметр может по-прежнему называться **Управление установленными приложениями**). При этом выполняется два указанных ниже действия.</span><span class="sxs-lookup"><span data-stu-id="61208-p113">Set the value of **Handle Add-in Installed** to **True**. (It may still be called **Handle App Installed**.) This does two things:</span></span>
    
      - <span data-ttu-id="61208-p114">В проекте **ChainStoreWeb** (но не в проекте **ChainStore**) создается папка **Службы**, в которую добавляются два файла: файл AppEventReceiver.svc и его файл кода программной части AppEventReceiver.svc.cs. Имена файлов начинаются со строки App, так как ранее надстройки назывались приложениями. *Не переименовывайте эти файлы.* Для правильной работы Инструментов разработчика Office для Visual Studio необходимо, чтобы у файлов были именно такие имена.</span><span class="sxs-lookup"><span data-stu-id="61208-p114">A folder called **Services** is created in the **ChainStoreWeb** project (not the **ChainStore** project) and two files are added to it: a AppEventReceiver.svc file and its code behind AppEventReceiver.svc.cs file. (The file names begin with the string "App", because add-ins used to be called "apps". *Don't rename these files.*  The Office Developer Tools for Visual Studio assume the files will keep these names. )</span></span>
    
 
  - <span data-ttu-id="61208-p115">URL-адрес обработчика регистрируется в манифесте надстройки. Эта часть не отображается в конструкторе манифеста. Чтобы увидеть ее, щелкните правой кнопкой мыши файл AppManifest.xml и выберите пункт **Перейти к коду**. Там вы увидите новый дочерний объект элемента **Properties**, представленный ниже. Эта часть кода сообщает SharePoint, что по завершении установки надстройки необходимо будет вызвать метод **ProcessEvent** этой службы. Настраиваемый обработчик — это последний компонент, запускаемый в процессе установки. Строка `~remoteAppUrl` — это заполнитель, который Инструменты разработчика Office для Visual Studio заменят на URL-адрес узла службы. При отладке в качестве этого адреса используется URL-адрес служебной шины Azure. Соответственно, при создании пакета для развертывания в рабочей среде используется URL-адрес рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="61208-p115">The handler URL is registered in the add-in manifest. This part of the manifest is not visible in the manifest designer. To see it, right-click the AppManifest.xml file and select **View Code**. There is a new child of the **Properties** element that looks like the following. This markup tells SharePoint to call the **ProcessEvent** method of this service when it has finished doing all of its own work related to installing the add-in. The custom handler is the last thing that runs as part of the installation. The string `~remoteAppUrl` is a placeholder that the Office Developer Tools for Visual Studio will replace with the service host URL. When you are debugging, it is an Azure Service Bus URL. When you create the package for deployment to production, it is the production URL.</span></span>
    
```XML
  <InstalledEventEndpoint>~remoteAppUrl/Services/AppEventReceiver.svc</InstalledEventEndpoint>
```

3. <span data-ttu-id="61208-177">Откройте файл AppEventReceiver.svc.cs.</span><span class="sxs-lookup"><span data-stu-id="61208-177">Open the AppEventReceiver.svc.cs file.</span></span>
    
 
4. <span data-ttu-id="61208-p116">Вы увидите, что Инструменты разработчика Office для Visual Studio создали пример реализации метода **ProcessEvent**. Все реализации этого метода начинаются с инициализации объекта **SPRemoteEventResult** и заканчиваются возвращением этого объекта в SharePoint. Помимо прочего, этот объект сообщает среде SharePoint, следует ли откатить событие из-за сбоя кода настраиваемого обработчика. Кроме того, возможно, что инструменты включили в этот метод блок **using**, который создает объект **ClientContext**. Настраиваемый обработчик в надстройке "Сеть магазинов" не будет отправлять обратный вызов в SharePoint, поэтому удалите этот блок. Теперь этот метод должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="61208-p116">You'll see that the Office Developer Tools for Visual Studio have created a sample implementation of the **ProcessEvent** method. All implementations of this method begin by initializing a **SPRemoteEventResult** object and they all end by returning that object to SharePoint. Among other things, this object tells SharePoint whether or not it should roll back the event because the custom handling logic has failed. The tools may also have included a **using** block in this method that creates a **ClientContext** object. The custom handler in the Chain Store add-in isn't going to call back into SharePoint, so delete this block. The method should now look like the following.</span></span>
    
```C#
  public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
{
    SPRemoteEventResult result = new SPRemoteEventResult();


    return result;
}
```

5. <span data-ttu-id="61208-p117">Приемник событий можно вызвать с помощью любого из трех возможных событий надстройки, поэтому добавьте приведенную ниже структуру **switch** в метод **ProcessEvent** между строками, в которых создается и возвращается объект `result`. В именах событий имеется строка App (Приложение), так как ранее надстройки назывались приложениями.</span><span class="sxs-lookup"><span data-stu-id="61208-p117">The event receiver could be called by any of three possible add-in events, so add the following **switch** structure to the **ProcessEvent** method in between the lines that create and return the `result` object. The event names have the string "App" in them because add-ins used to be called "apps".</span></span>
    
```C#
  switch (properties.EventType)
{
    case SPRemoteEventType.AppInstalled:

        // TODO2: Custom installation logic goes here.

        break;
    case SPRemoteEventType.AppUpgraded:
        // This sample does not implement an add-in upgrade handler.
        break;
    case SPRemoteEventType.AppUninstalling:

        // TODO3: Custom uninstallation logic goes here.         
         
        break;
}
```

6. <span data-ttu-id="61208-p118">Для регистрации магазина в Гонконге в качестве клиента в удаленном веб-приложении наш код, выполняемый во время установки, должен вызывать хранимую процедуру SQL. Очень важно, чтобы в случае сбоя процесса обработчик сообщал SharePoint, что необходимо откатить установку надстройки. Поэтому добавьте приведенные ниже блоки **try/catch** вместо `TODO2`. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="61208-p118">Our installation logic is going to call an SQL stored procedure to register the Hong Kong store as a tenant in the remote web application. It is very important that, if this process fails, the handler signals SharePoint to roll back the installation of the add-in, so add the following **try/catch** blocks in place of `TODO2`. Note the following about this code:</span></span>
    
      - <span data-ttu-id="61208-189">Мы создадим объект `tenantName` и метод `CreateTenant` на последующем этапе.</span><span class="sxs-lookup"><span data-stu-id="61208-189">You will create the  `tenantName` object and `CreateTenant` method in a later step.</span></span>
    
 
  - <span data-ttu-id="61208-p119">Свойство **Status** объекта **SPRemoteEventResult** может принимать одно из трех следующих значений: **Continue** (используется по умолчанию), **CancelNoError** и **CancelWithError**. Два последних значения сообщают SharePoint, что необходимо откатить событие.</span><span class="sxs-lookup"><span data-stu-id="61208-p119">The **Status** property of the **SPRemoteEventResult** object can have three possible values: **Continue** (the default), **CancelNoError**, and **CancelWithError**. Either of the latter two tell SharePoint to roll back the event.</span></span>
    
 

```C#
  try
{
    CreateTenant(tenantName);
 }
catch (Exception e)
{
     // Tell SharePoint to cancel and roll back the event.
    result.ErrorMessage = e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;
}
```

7. <span data-ttu-id="61208-p120">URL-адрес хост-сайта, представляющий собой дискриминатор клиента в примере, включается в сведения, которые SharePoint передает приемнику в параметре **SPRemoteEventProperties**. Добавьте приведенную ниже строку в метод **ProcessEvent** сразу же после блока инициализации объекта **SPRemoteEventResult**.</span><span class="sxs-lookup"><span data-stu-id="61208-p120">The host web URL, which is the sample's tenant discriminator, is part of the information that SharePoint passes to the receiver in the **SPRemoteEventProperties** parameter. Add the following line to the **ProcessEvent** method on line that is just below the initialization of the **SPRemoteEventResult** object.</span></span>
    
```C#
  string tenantName = properties.AppEventProperties.HostWebFullUrl.ToString();
```

8. <span data-ttu-id="61208-p121">Теперь в нашем коде придется учесть небольшую особенность свойства **AppEventProperties.HostWebFullUrl**. В большинстве других контекстов SharePoint добавляет закрывающий символ косой черты "/" в конце URL-адреса хост-сайта, поэтому в нашем примере кода предполагается, что этот символ присутствует. Но SharePoint добавляет этот символ в конце значения **HostWebFullUrl** только в том случае, если хост-сайт является корневым в семействе веб-сайтов. Так как наш веб-сайт магазина в Гонконге является дочерним в семействе веб-сайтов, то нам потребуется добавить этот символ, чтобы во всем примере использовалось одно и то же имя клиента. Добавьте приведенный ниже код сразу после блока инициализации объекта `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="61208-p121">Now our code has to deal with a little quirk of the **AppEventProperties.HostWebFullUrl** property. In most other contexts, SharePoint includes a closing "/" character at the end of the host web URL, so the logic of our sample code assumes that this character is present. But SharePoint adds this character at the end of the **HostWebFullUrl** value if, and only if, the host web is the root web of a site collection. Since our Hong Kong website is a subweb in the site collection, we need to add this character to ensure that the same tenant name string is used throughout the sample. Add the following code below the initialization of the `tenantName` object.</span></span>
    
```C#
  if (!tenantName.EndsWith("/"))
{
    tenantName += "/";
}
```

9. <span data-ttu-id="61208-199">Добавьте приведенные ниже операторы **using** в начале файла.</span><span class="sxs-lookup"><span data-stu-id="61208-199">Add the following **using** statements to the top of the file.</span></span>
    
```
  using System.Data.SqlClient;
using System.Data;
using ChainStoreWeb.Utilities;
```

10. <span data-ttu-id="61208-p122">Добавьте указанный ниже метод в класс  `AppEventReceiver`. Мы не будем подробно рассматривать его, так как цель этой серии статей научить вас программированию надстроек SharePoint, а не программированию для SQL Server или Azure.</span><span class="sxs-lookup"><span data-stu-id="61208-p122">Add the following method to the  `AppEventReceiver` class. We don't discuss this in detail because the purpose of this series of articles is to teach SharePoint Add-in programming, not SQL Server/Azure programming.</span></span>
    
    <span data-ttu-id="61208-p123">Этот метод будет создавать строку в таблице **Tenants** (Клиенты) базы данных. Помимо столбца **Name** (Имя), в таблице имеется столбец **Version** (Версия) со значением 0000.0000.0000.0000, используемым по умолчанию. В одной из следующих статей этой серии описывается создание кода, выполняемого во время первого запуска, который будет использовать это значение, чтобы проверить, установлена ли надстройка на хост-сайте. Если номер версии равен 0000.0000.0000.0000, то ваш код развернет списки **Местные сотрудники** и **Ожидаемые поставки**, а затем увеличит номер версии.</span><span class="sxs-lookup"><span data-stu-id="61208-p123">This method is going to create a row in a database table called **Tenants**. In addition to the **Name** column, the table also has a **Version** column with a default value set to0000.0000.0000.0000. In a later article in this series, you will create first-run logic that looks at this value to determine whether or not the add-in has already been installed on the host web. If the version is 0000.0000.0000.0000, your code will deploy the **Local Employees** and **Expected Shipments** lists, and then raise the version number.</span></span>
    


```C#
  private void CreateTenant(string tenantName)
{
    // Do not catch exceptions. Allow them to bubble up and trigger roll back
    // of installation.

    using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
    using (SqlCommand cmd = conn.CreateCommand())
    {
        conn.Open();
        cmd.CommandText = "AddTenant";
        cmd.CommandType = CommandType.StoredProcedure;
        SqlParameter name = cmd.Parameters.Add("@Name", SqlDbType.NVarChar);
        name.Value = tenantName;
        cmd.ExecuteNonQuery();
    }//dispose conn and cmd
}
```


## <a name="create-the-uninstallation-handler"></a><span data-ttu-id="61208-206">Создание обработчика удаления</span><span class="sxs-lookup"><span data-stu-id="61208-206">Create the uninstallation handler</span></span>
<span data-ttu-id="61208-207"><a name="RERDebug"> </a></span><span class="sxs-lookup"><span data-stu-id="61208-207"></span></span>

<span data-ttu-id="61208-p124">В случаях, когда обрабатывается событие установки, обычно рекомендуется обрабатывать и событие удаления. Основная причина этого состоит в том, что обработчик события удаления должен перемещать в корзину или удалять объекты, установленные обработчиком события установки. Тем не менее существует много исключений, поэтому вам необходимо хорошо понимать варианты использования вашей надстройки. Например, в списке, который был развернут и заполнен надстройкой, могут остаться значения даже после ее удаления, при этом вам может быть потребоваться, чтобы обработчик события удаления не удалял этот список.</span><span class="sxs-lookup"><span data-stu-id="61208-p124">It is usually good practice to handle the uninstalling event whenever you are handling the installed event. The basic idea is that the uninstalling handler deletes or recycles things that the installed handler deployed. There are, however, many exceptions, so you really need to understand the use cases of your add-in. For example, a list that is deployed with an add-in and populated with the add-in might still have value even after the add-in itself is uninstalled in which case you wouldn't want to uninstall the list in the uninstalling event handler.</span></span> 
 

 
<span data-ttu-id="61208-p125">Если пользователь удаляет надстройку со страницы **Содержимое сайта**, то событие удаления не создается, как того можно было ожидать. В этом случае надстройка лишь перемещается в корзину веб-сайта. Пользователь может восстановить ее, но при восстановлении обработчик события установки не запускается повторно, поэтому необходимо, чтобы по-прежнему существовали все объекты, развернутые обработчиком события установки. Компоненты SharePoint можно перемещать из корзины во вторую корзину. Событие удаления будет создано только при удалении надстройки из второй корзины. Если пользователь сделает это, то надстройка будет безвозвратно удалена, поэтому в этот момент нам необходимо будет удалить клиент магазина в Гонконге из корпоративной базы данных.</span><span class="sxs-lookup"><span data-stu-id="61208-p125">The uninstallation event does not run, as you might expect, when a user removes the add-in from the **Site Contents** page. Doing so only moves the add-in to the website's Recycle Bin. A user could restore it, but restoring does not rerun the installed even handler, so you'd want anything that was deployed with the installed event handler to still exist if the add-in is restored. SharePoint components can be moved from the Recycle Bin to the second-stage Recycle Bin. It is only when an add-in is deleted from the second-stage that the uninstalling event happens; and when a user does that, the add-in is unrestorable anyway, so we want the Hong Kong store's tenancy to be removed from the corporate database at that point.</span></span>
 

 

1. <span data-ttu-id="61208-p126">Задайте для параметра **Управление удалением надстроек** значение **True** (этот параметр может по-прежнему называться **Управление удалением приложений**). При этом обработчик будет зарегистрирован в файле AppManifest.xml точно так же, как ранее был зарегистрирован обработчик события установки. Взглянув на содержимое файла, вы увидите, что их URL-адреса полностью совпадают. Инструменты разработчика Office для Visual Studio предполагают, что вы используете один и тот же SVC-файл. Мы делаем это в данном примере, и это является стандартной рекомендацией.</span><span class="sxs-lookup"><span data-stu-id="61208-p126">Set the value of **Handle Add-in Uninstalling** to **True**. (It may still be called **Handle App Uninstalling**.) This registers the handler in the AppManifest.xml file just as you earlier registered the installation handler. If you look at the file, you'll see that they have exactly the same URL. The Office Developer Tools for Visual Studio assume that you are using the same *.svc file. We are doing that in this sample, and it is a standard practice.</span></span> 
    
 
2. <span data-ttu-id="61208-p127">Добавьте приведенный ниже код вместо заполнителя `TODO3` в файле AppEventReceiver.svc.cs. Обратите внимание на указанные ниже особенности этого кода.</span><span class="sxs-lookup"><span data-stu-id="61208-p127">Add the following code in place of  `TODO3` in the AppEventReceiver.svc.cs file. Note the following about this code:</span></span>
    
      - <span data-ttu-id="61208-224">Метод `DeleteTenant` будет добавлен на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="61208-224">The  `DeleteTenant` method is added in the next step.</span></span>
    
 
  - <span data-ttu-id="61208-225">При откате удаления надстройка останется во второй корзине, из которой ее все еще можно восстановить.</span><span class="sxs-lookup"><span data-stu-id="61208-225">Rolling back the uninstallation of the add-in would leave it in the second-stage Recycle Bin, from which it could still be restored.</span></span>
    
 

```C#
  try
{
    DeleteTenant(tenantName);
 }
catch (Exception e)
{
     // Tell SharePoint to cancel and roll back the event.
    result.ErrorMessage = e.Message;
    result.Status = SPRemoteEventServiceStatus.CancelWithError;
}
```

3. <span data-ttu-id="61208-226">Добавьте приведенный ниже метод в класс `AppEventReceiver`.</span><span class="sxs-lookup"><span data-stu-id="61208-226">Add the following method to the  `AppEventReceiver` class.</span></span>
    
```C#
  private void DeleteTenant(string tenantName)
{
    // Do not catch exceptions. Allow them to bubble up and trigger roll back
    // of un-installation (removal from 2nd level Recycle Bin).

    using (SqlConnection conn = SQLAzureUtilities.GetActiveSqlConnection())
    using (SqlCommand cmd = conn.CreateCommand())
    {
        conn.Open();
        cmd.CommandText = "RemoveTenant";
        cmd.CommandType = CommandType.StoredProcedure;
        SqlParameter name = cmd.Parameters.Add("@Name", SqlDbType.NVarChar);
        name.Value = tenantName;
        cmd.ExecuteNonQuery();                
    }//dispose conn and cmd
}
```


 <span data-ttu-id="61208-p128">**Примечание.** В предыдущей статье этой серии вы настроили проект так, чтобы при каждом нажатии клавиши F5 перестраивалась корпоративная база данных. При этом выполняется очистка таблицы **Tenants** (Клиенты).</span><span class="sxs-lookup"><span data-stu-id="61208-p128">**Note** In an earlier article in this series, you configured the project to rebuild the corporate database each time you press F5. This empties the **Tenants** table.</span></span>
 


## <a name="run-the-add-in-and-test-the-installation-handler"></a><span data-ttu-id="61208-229">Запуск надстройки и тестирование обработчика установки</span><span class="sxs-lookup"><span data-stu-id="61208-229">Run the add-in and test the installation handler</span></span>
<span data-ttu-id="61208-230"><a name="RERDebug"> </a></span><span class="sxs-lookup"><span data-stu-id="61208-230"></span></span>


1. <span data-ttu-id="61208-p129">Нажмите клавишу F5, чтобы развернуть и запустить вашу надстройку. Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL в SQL Express. Кроме того, он создает временную установку надстройки на вашем тестовом сайте SharePoint, запускает обработчик события установки и немедленно запускает надстройку. Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="61208-p129">Use the F5 key to deploy and run your add-in. Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in a SQL Express. It also makes a temporary installation of the add-in on your test SharePoint site and, runs the installation event handler, and immediately runs the add-in. You are prompted to grant permissions to the add-in before it's start page opens.</span></span> 
    
 
2. <span data-ttu-id="61208-235">Когда откроется начальная страница надстройки, нажмите значок с изображением шестеренки на расположенном вверху элементе управления хрома и выберите **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="61208-235">When the add-in's start page opens, press the gear icon on the chrome control at the top, and select **Account settings**.</span></span>
    
 
3. <span data-ttu-id="61208-p130">На странице **Учетные записи** нажмите кнопку **Показать версию надстройки**. Появится номер версии 0000.0000.0000.0000.</span><span class="sxs-lookup"><span data-stu-id="61208-p130">On the **Accounts** page, press the **Show Add-in Version** button. The version shows as0000.0000.0000.0000.</span></span>
    
  ![Страница "Учетные записи" с заголовком "Параметры учетной записи". Под кнопкой "Показать версию надстройки" находится строка "Зарегистрированная версия: ноль ноль ноль ноль точка ноль ноль ноль ноль точка ноль ноль ноль ноль точка ноль ноль ноль ноль".](../../images/2a905b7d-89c7-456a-8456-21a9b7e9efc5.PNG)
 

 

 
4. <span data-ttu-id="61208-p132">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="61208-p132">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
5. <span data-ttu-id="61208-p133">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="61208-p133">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="61208-244"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="61208-244"></span></span>

 <span data-ttu-id="61208-245">В следующей статье этой серии вы добавите в надстройку код, выполняемый при первом запуске, для автоматического развертывания списка **Local Employees** (Местные сотрудники) и настраиваемой кнопки ленты: [Добавление кода, выполняемого при первом запуске, в надстройку, размещаемую у поставщика](add-first-run-logic-to-the-provider-hosted-add-in).</span><span class="sxs-lookup"><span data-stu-id="61208-245">In the next article of the series, you will add first-run logic to the add-in that will programmatically deploy the **Local Employees** list and the custom ribbon button: [Add first-run logic to the provider-hosted add-in](add-first-run-logic-to-the-provider-hosted-add-in)</span></span>
 

 

