---
title: "Обработка событий в надстройке с размещением у поставщика"
description: "Настройка установки надстройки SharePoint, размещаемой у поставщика, путем конфигурирования решения для отладки приемника событий, создания обработчиков событий установки и удаления, запуска надстройки и тестирования этих обработчиков."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 41f809a377fff222955696c34aafb60e102788a8
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="handle-add-in-events-in-the-provider-hosted-add-in"></a><span data-ttu-id="17515-103">Обработка событий в надстройке с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="17515-103">Handle add-in events in the provider-hosted add-in</span></span>

<span data-ttu-id="17515-104">Это седьмая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями этой серии, представленными в разделе [Знакомство с созданием надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md#SP15createprovider_nextsteps).</span><span class="sxs-lookup"><span data-stu-id="17515-104">This is the seventh in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span> 

> [!NOTE]
> <span data-ttu-id="17515-105">Если вы изучали предыдущие статьи этой серии о размещаемых у поставщика надстройках, то у вас уже есть решение Visual Studio, которое можно использовать для работы с данной статьей.</span><span class="sxs-lookup"><span data-stu-id="17515-105">If you have been working through this series about provider-hosted add-ins, you have a Visual Studio solution that you can use to continue with this topic.</span></span> <span data-ttu-id="17515-106">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeAdd-inEventHandlers.sln.</span><span class="sxs-lookup"><span data-stu-id="17515-106">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeAdd-inEventHandlers.sln file.</span></span>

<span data-ttu-id="17515-107">В данной статье мы настроим в SharePoint обработку событий, которые называются событиями надстройки.</span><span class="sxs-lookup"><span data-stu-id="17515-107">In this article, we customize the handling of a kind of event in SharePoint called add-in events.</span></span> <span data-ttu-id="17515-108">В частности, мы создадим обработчики событий установки и удаления надстройки.</span><span class="sxs-lookup"><span data-stu-id="17515-108">Specifically, we create handlers for the add-in installation and uninstallation events.</span></span> <span data-ttu-id="17515-109">Кроме того, настраиваемые обработчики можно использовать для событий списка и элементов списка. О таких обработчиках вы узнаете в одной из следующих статей этой серии.</span><span class="sxs-lookup"><span data-stu-id="17515-109">List and list item events can also get custom handling; you'll learn about these in a later article in this series.</span></span> <span data-ttu-id="17515-110">Все эти события создаются в SharePoint, но настраиваемый код, обрабатывающий каждое событие, находится в вашем удаленном веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="17515-110">All of these events are triggered in SharePoint, but your custom code that handles each event is in your remote web application.</span></span> <span data-ttu-id="17515-111">Вы настроите SharePoint для вызова настраиваемого обработчика, зарегистрировав его URL-адрес для события SharePoint.</span><span class="sxs-lookup"><span data-stu-id="17515-111">You configure SharePoint to call your custom handler by registering the handler's URL with the SharePoint event.</span></span>

## <a name="two-places-to-programmatically-deploy-sharepoint-components"></a><span data-ttu-id="17515-112">Два места для программного развертывания компонентов SharePoint</span><span class="sxs-lookup"><span data-stu-id="17515-112">Two places to programmatically deploy SharePoint components</span></span>

<span data-ttu-id="17515-113">Мы хотим, чтобы наша надстройка Chain Store автоматически создавала и развертывала списки **Local Employees** (Местные сотрудники) и **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="17515-113">We want our Chain Store add-in to create and deploy the **Local Employees** and **Expected Shipments** lists automatically.</span></span> <span data-ttu-id="17515-114">Надстройка может в любое время развертывать компоненты SharePoint, например настраиваемые списки.</span><span class="sxs-lookup"><span data-stu-id="17515-114">An add-in can deploy SharePoint components, such as a custom list, any time.</span></span> <span data-ttu-id="17515-115">Но если надстройка зависит от определенного компонента, например настраиваемого списка, этот компонент необходимо развернуть, *прежде чем* пользователи начнут работать с надстройкой.</span><span class="sxs-lookup"><span data-stu-id="17515-115">But when an add-in depends on a specific component such as a custom list, the component really should be deployed *before* users start working with the add-in.</span></span> <span data-ttu-id="17515-116">Для таких критически важных компонентов настраиваемый код, выполняющий развертывание, можно разместить в двух местах:</span><span class="sxs-lookup"><span data-stu-id="17515-116">For such vital components, there are two places where the custom deployment logic can go:</span></span>

- <span data-ttu-id="17515-117">в обработчике события установки для надстройки;</span><span class="sxs-lookup"><span data-stu-id="17515-117">In a handler for the add-in installation event.</span></span>
- <span data-ttu-id="17515-118">в коде, выполняемом при первом запуске надстройки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="17515-118">In "first run" logic that executes the first time the add-in is launched in SharePoint.</span></span>

<span data-ttu-id="17515-p104">Описание процесса принятия решения о том, какой способ лучше подходит для конкретной надстройки, выходит за рамки данной статьи. В нашей статье мы приведем только несколько соображений, оказывающих влияние на выбор.</span><span class="sxs-lookup"><span data-stu-id="17515-p104">Deciding which is best for a given add-in is an advanced topic. In this article, we can only mention a few points of comparison:</span></span>

- <span data-ttu-id="17515-p105">Работа настраиваемого обработчика установки должна завершиться в течение 30 секунд. Время работы кода, выполняемого при первом запуске, не ограничено.</span><span class="sxs-lookup"><span data-stu-id="17515-p105">A custom installation handler has to complete in 30 seconds. There is no limit to how long first-run logic can take.</span></span>

- <span data-ttu-id="17515-123">Если в процессе установки надстройки что-то пойдет не так, SharePoint откатит все действия, которые он выполнил в ходе установки.</span><span class="sxs-lookup"><span data-stu-id="17515-123">If anything goes wrong during an add-in installation, SharePoint rolls back everything it has done as part of the installation.</span></span> <span data-ttu-id="17515-124">Настраиваемый обработчик события установки запускается *после* того как SharePoint выполнит все действия, необходимые для установки надстройки, поэтому обработчик может принять участие в работе этой системы.</span><span class="sxs-lookup"><span data-stu-id="17515-124">A custom installation handler runs *after* SharePoint has done everything it's going to do to install the add-in, so a custom handler can participate in this system.</span></span> 

   <span data-ttu-id="17515-125">Например, если ваш настраиваемый код создал исключение, вы можете сообщить SharePoint, что необходимо полностью откатить установку надстройки.</span><span class="sxs-lookup"><span data-stu-id="17515-125">For example, if your custom logic throws an exception, you can tell SharePoint to roll back the entire add-in installation.</span></span> <span data-ttu-id="17515-126">Если же что-то пойдет не так в настраиваемом коде, выполняемом при первом запуске, надстройка останется установленной и, возможно, будет работать неправильно.</span><span class="sxs-lookup"><span data-stu-id="17515-126">If something goes wrong in custom first-run logic, however, the add-in remains installed and presumably won't work properly.</span></span>

- <span data-ttu-id="17515-127">Если SharePoint придется откатить установку надстройки, он не "успокоится" на этом.</span><span class="sxs-lookup"><span data-stu-id="17515-127">SharePoint doesn't give up if it has to roll back an add-in installation.</span></span> <span data-ttu-id="17515-128">Он сразу же попытается установить надстройку еще раз.</span><span class="sxs-lookup"><span data-stu-id="17515-128">It immediately tries the installation again.</span></span> <span data-ttu-id="17515-129">Будет предпринято до 4 попыток (на каждую попытку выделяется 30 секунд).</span><span class="sxs-lookup"><span data-stu-id="17515-129">It makes up to four attempts (the 30-second time limit applies on each attempt).</span></span> <span data-ttu-id="17515-130">При каждой повторной попытке настраиваемый обработчик события установки *запускается с самого начала*.</span><span class="sxs-lookup"><span data-stu-id="17515-130">Each time it retries, the custom installation handler runs again *from the beginning*.</span></span> <span data-ttu-id="17515-131">Если обработчик установил, например, список, перед откатом всех действий, то он будет пытаться установить этот же список при каждой новой попытке установить надстройку.</span><span class="sxs-lookup"><span data-stu-id="17515-131">If the handler managed to install, say, a list, before the rollback, it tries to install the same list again on the retry.</span></span> 

   <span data-ttu-id="17515-132">Чтобы не допустить этого, необходимо написать код обработчика события установки таким образом, чтобы он не выполнял никаких действий (например, развертывание компонента), прежде чем проверит, не выполнено ли это действие ранее.</span><span class="sxs-lookup"><span data-stu-id="17515-132">To prevent this from happening, code in an installation handler has to be written so that it won't take any action (such as deploy a component) unless it first checks to see if that action has already been done.</span></span> <span data-ttu-id="17515-133">Из-за этого код обработчика события установки сложнее кода, выполняемого при первом запуске, так как последний не выполняется повторно (если, конечно, вы намеренно не запрограммируете повторное выполнение).</span><span class="sxs-lookup"><span data-stu-id="17515-133">This makes the logic of an installation handler more complex than first-run logic because first-run logic won't retry (unless you specifically code it to do so).</span></span> <span data-ttu-id="17515-134">Кроме того, чтобы проверить, не развернут ли какой-либо компонент, необходимо выполнить затратный по времени вызов через Интернет от удаленного обработчика к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="17515-134">Also, checking to see if a component has already been deployed usually requires a time-consuming call over the Internet from the remote handler to SharePoint.</span></span> <span data-ttu-id="17515-135">После этого понадобится выполнить второй вызов для развертывания компонента (если он еще не развернут).</span><span class="sxs-lookup"><span data-stu-id="17515-135">A second call is also needed to actually deploy the component (if it has not already been deployed).</span></span>

<span data-ttu-id="17515-136">В надстройке Chain Store мы объединим эти стратегии.</span><span class="sxs-lookup"><span data-stu-id="17515-136">For the Chain Store add-in, we combine these strategies.</span></span> <span data-ttu-id="17515-137">В этой статье вы создадите обработчик события установки, который будет регистрировать хост-сайт в качестве клиента в корпоративной базе данных, а затем задавать сигнал о том, запущена ли уже надстройка на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="17515-137">In this article, you create an installation handler that registers the host web as a tenant in the corporate database and then sets a signal that specifies whether the add-in has been run yet on the host web.</span></span> 

<span data-ttu-id="17515-138">В одной из следующих статей этой серии вы добавите код, выполняемый при первом запуске, в метод **Page_Load** начальной страницы надстройки.</span><span class="sxs-lookup"><span data-stu-id="17515-138">In a later article in this series, you'll put first-run logic in the **Page_Load** method of the add-ins start page.</span></span> <span data-ttu-id="17515-139">Этот код будет развертывать два настраиваемых списка и выполнять ряд других действий.</span><span class="sxs-lookup"><span data-stu-id="17515-139">This logic deploys the two custom lists and does some other things, too.</span></span>

<span data-ttu-id="17515-140"><a name="RERDebug"> </a></span><span class="sxs-lookup"><span data-stu-id="17515-140"></span></span>
## <a name="configure-the-solution-for-event-receiver-debugging"></a><span data-ttu-id="17515-141">Настройка решения для отладки приемника событий</span><span class="sxs-lookup"><span data-stu-id="17515-141">Configure the solution for event receiver debugging</span></span>

<span data-ttu-id="17515-142">Для отладки приемников событий необходимо использовать служебную шину Azure.</span><span class="sxs-lookup"><span data-stu-id="17515-142">Debugging of event receivers requires the use of the Azure Service Bus.</span></span> <span data-ttu-id="17515-143">Следуйте инструкциям в статье [Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="17515-143">Follow the instructions at [Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span></span> <span data-ttu-id="17515-144">Так как в качестве тестового сайта вы используете веб-сайт SharePoint Online, не забудьте выполнить эти инструкции на удаленном тестовом сайте.</span><span class="sxs-lookup"><span data-stu-id="17515-144">Because you are using a SharePoint Online website as your test site, ensure that you carry out the instructions for a remote test site.</span></span> <span data-ttu-id="17515-145">В следующих статьях этой серии подразумевается, что вы успешно настроили среду отладки.</span><span class="sxs-lookup"><span data-stu-id="17515-145">The remainder of this series assumes you have configured debugging successfully.</span></span> 

## <a name="create-the-installation-handler"></a><span data-ttu-id="17515-146">Создание обработчика установки</span><span class="sxs-lookup"><span data-stu-id="17515-146">Create the installation handler</span></span>

> [!NOTE]
> <span data-ttu-id="17515-147">Когда решение открывается повторно, для параметров раздела "Запускаемые проекты" в Visual Studio обычно возвращаются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="17515-147">The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened.</span></span> <span data-ttu-id="17515-148">После повторного открытия примера решения, который рассматривается в этой серии статей, всегда выполняйте указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="17515-148">Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 
> 1. <span data-ttu-id="17515-149">В верхней части **обозревателя решений** щелкните узел решения правой кнопкой мыши и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="17515-149">Right-click the solution node at the top of **Solution Explorer**, and then select **Set startup projects**.</span></span>  
> 2. <span data-ttu-id="17515-150">Убедитесь, что в столбце **Действие** для всех трех проектов указано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="17515-150">Ensure that all three projects are set to **Start** in the **Action** column.</span></span>

1. <span data-ttu-id="17515-151">В **обозревателе решений** выберите проект **ChainStore**, чтобы его свойства отобразились в области **Свойства** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17515-151">In **Solution Explorer**, select the **ChainStore** project so that its properties appear in the **Properties** pane of Visual Studio.</span></span>

2. <span data-ttu-id="17515-152">Задайте для параметра **Управление установленными надстройками** значение **True** (этот параметр может по-прежнему называться **Управление установленными приложениями**).</span><span class="sxs-lookup"><span data-stu-id="17515-152">Set the value of **Handle Add-in Installed** to **True** (it may still be called **Handle App Installed**).</span></span> <span data-ttu-id="17515-153">При этом выполняется два следующих действия:</span><span class="sxs-lookup"><span data-stu-id="17515-153">This does two things:</span></span>
    
   - <span data-ttu-id="17515-154">В проекте **ChainStoreWeb** (но не в проекте **ChainStore**) создается папка **Services** (Службы), в которую будут добавлены два файла: файл AppEventReceiver.svc и его файл кода программной части AppEventReceiver.svc.cs. (Имена файлов начинаются со строки App, так как ранее надстройки назывались приложениями. *Не переименовывайте эти файлы*. Для правильной работы пакета "Инструменты разработчика Office для Visual Studio" необходимо, чтобы файлы имели именно эти имена.)</span><span class="sxs-lookup"><span data-stu-id="17515-154">A folder called **Services** is created in the **ChainStoreWeb** project (not the **ChainStore** project), and two files are added to it: an AppEventReceiver.svc file and its code-behind AppEventReceiver.svc.cs file (the file names begin with the string "App" because add-ins used to be called "apps"; *don't rename these files* because the Office Developer Tools for Visual Studio assumes that the files will keep these names).</span></span>

   - <span data-ttu-id="17515-155">URL-адрес обработчика регистрируется в манифесте надстройки.</span><span class="sxs-lookup"><span data-stu-id="17515-155">The handler URL is registered in the add-in manifest.</span></span> <span data-ttu-id="17515-156">Эта часть манифеста не отображается в конструкторе манифеста.</span><span class="sxs-lookup"><span data-stu-id="17515-156">This part of the manifest is not visible in the manifest designer.</span></span> <span data-ttu-id="17515-157">Чтобы отобразить ее, щелкните правой кнопкой мыши файл AppManifest.xml и выберите пункт **Просмотр кода**.</span><span class="sxs-lookup"><span data-stu-id="17515-157">To see it, right-click the AppManifest.xml file and select **View Code**.</span></span> <span data-ttu-id="17515-158">Новый дочерний элемент элемента **Свойства** выглядит, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="17515-158">A new child of the **Properties** element looks like the following.</span></span> 
   
      ```XML
        <InstalledEventEndpoint>~remoteAppUrl/Services/AppEventReceiver.svc</InstalledEventEndpoint>
      ``` 
   
     <span data-ttu-id="17515-159">Эта разметка сообщает SharePoint, что когда он завершит всю работу по установке надстройки, необходимо будет вызвать метод **ProcessEvent** этой службы.</span><span class="sxs-lookup"><span data-stu-id="17515-159">This markup tells SharePoint to call the **ProcessEvent** method of this service when it has finished doing all of its own work related to installing the add-in.</span></span> <span data-ttu-id="17515-160">Настраиваемый обработчик — это последний компонент, запускаемый в процессе установки.</span><span class="sxs-lookup"><span data-stu-id="17515-160">The custom handler is the last thing that runs as part of the installation.</span></span> <span data-ttu-id="17515-161">Строка `~remoteAppUrl` — это заполнитель, который пакет "Инструменты разработчика Office для Visual Studio" заменит URL-адресом узла службы.</span><span class="sxs-lookup"><span data-stu-id="17515-161">The string `~remoteAppUrl` is a placeholder that the Office Developer Tools for Visual Studio replaces with the service host URL.</span></span> <span data-ttu-id="17515-162">При отладке в качестве этого URL-адреса используется URL-адрес служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="17515-162">When you are debugging, it is an Azure Service Bus URL.</span></span> <span data-ttu-id="17515-163">При создании пакета для развертывания в рабочей среде используется URL-адрес рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="17515-163">When you create the package for deployment to production, it is the production URL.</span></span>

3. <span data-ttu-id="17515-164">Откройте файл AppEventReceiver.svc.cs.</span><span class="sxs-lookup"><span data-stu-id="17515-164">Open the AppEventReceiver.svc.cs file.</span></span>
    
4. <span data-ttu-id="17515-165">Вы увидите, что пакет "Инструменты разработчика Office для Visual Studio" создал пример реализации метода **ProcessEvent**.</span><span class="sxs-lookup"><span data-stu-id="17515-165">You see that the Office Developer Tools for Visual Studio has created a sample implementation of the **ProcessEvent** method.</span></span> <span data-ttu-id="17515-166">Все реализации этого метода начинаются с инициализации объекта **SPRemoteEventResult** и заканчиваются возвращением этого объекта в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="17515-166">All implementations of this method begin by initializing an **SPRemoteEventResult** object, and they all end by returning that object to SharePoint.</span></span> <span data-ttu-id="17515-167">Помимо прочего, этот объект сообщает SharePoint, следует ли откатить событие из-за сбоя кода настраиваемого обработчика.</span><span class="sxs-lookup"><span data-stu-id="17515-167">Among other things, this object tells SharePoint whether or not it should roll back the event because the custom handling logic has failed.</span></span> 

   <span data-ttu-id="17515-168">Кроме того, возможно, пакет инструментов включил в этот метод блок **using**, который создает объект **ClientContext**.</span><span class="sxs-lookup"><span data-stu-id="17515-168">The tools may also have included a **using** block in this method that creates a **ClientContext** object.</span></span> <span data-ttu-id="17515-169">Настраиваемый обработчик в надстройке Chain Store не будет делать обратный вызов в SharePoint, поэтому удалите этот блок.</span><span class="sxs-lookup"><span data-stu-id="17515-169">The custom handler in the Chain Store add-in isn't going to call back into SharePoint, so delete this block.</span></span> <span data-ttu-id="17515-170">Теперь метод должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="17515-170">The method should now look like the following.</span></span>
    
    ```C#
       public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
     {
         SPRemoteEventResult result = new SPRemoteEventResult();

         return result;
     }
    ```

5. <span data-ttu-id="17515-171">Приемник событий можно вызвать с помощью любого из трех возможных событий надстройки, поэтому добавьте приведенную ниже структуру **switch** в метод **ProcessEvent** между строками, в которых создается и возвращается объект `result`. Имена событий включают строку App (Приложение), так как ранее надстройки назывались приложениями.</span><span class="sxs-lookup"><span data-stu-id="17515-171">The event receiver could be called by any of three possible add-in events, so add the following **switch** structure to the **ProcessEvent** method in between the lines that create and return the `result` object (the event names have the string "App" in them because add-ins used to be called "apps").</span></span>
    
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

6. <span data-ttu-id="17515-172">Для регистрации магазина в Гонконге в качестве клиента в удаленном веб-приложении наш код, выполняемый во время установки, должен вызывать хранимую процедуру SQL.</span><span class="sxs-lookup"><span data-stu-id="17515-172">Our installation logic is going to call an SQL stored procedure to register the Hong Kong store as a tenant in the remote web application.</span></span> <span data-ttu-id="17515-173">Очень важно, чтобы при сбое процесса обработчик сообщил SharePoint, что необходимо откатить установку надстройки. Поэтому добавьте указанные ниже блоки **try/catch** вместо `TODO2`.</span><span class="sxs-lookup"><span data-stu-id="17515-173">It is very important that, if this process fails, the handler signals SharePoint to roll back the installation of the add-in, so add the following **try/catch** blocks in place of `TODO2`.</span></span> 

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

   <span data-ttu-id="17515-174">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="17515-174">Note the following about this code:</span></span>

   - <span data-ttu-id="17515-175">Вы создадите объект `tenantName` и метод `CreateTenant` на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="17515-175">You create the `tenantName` object and `CreateTenant` method in a later step.</span></span>
   - <span data-ttu-id="17515-p120">Свойство **Status** объекта **SPRemoteEventResult** может иметь три одно из трех следующих значений: **Continue** (используется по умолчанию), **CancelNoError** и **CancelWithError**. Два последних значения сообщают SharePoint, что необходимо откатить событие.</span><span class="sxs-lookup"><span data-stu-id="17515-p120">The **Status** property of the **SPRemoteEventResult** object can have three possible values: **Continue** (the default), **CancelNoError**, and **CancelWithError**. Either of the latter two tell SharePoint to roll back the event.</span></span>

7. <span data-ttu-id="17515-178">URL-адрес хост-сайта, представляющий собой дискриминатор клиента в примере, включается в сведения, которые SharePoint передает в приемник в параметре **SPRemoteEventProperties**.</span><span class="sxs-lookup"><span data-stu-id="17515-178">The host web URL, which is the sample's tenant discriminator, is part of the information that SharePoint passes to the receiver in the **SPRemoteEventProperties** parameter.</span></span> <span data-ttu-id="17515-179">Добавьте указанную ниже строку в метод **ProcessEvent** в строку сразу же после блока инициализации объекта **SPRemoteEventResult**.</span><span class="sxs-lookup"><span data-stu-id="17515-179">Add the following line to the **ProcessEvent** method on the line that is just under the initialization of the **SPRemoteEventResult** object.</span></span>
    
    ```C#
      string tenantName = properties.AppEventProperties.HostWebFullUrl.ToString();
    ```

8. <span data-ttu-id="17515-180">Теперь в нашем коде придется учесть небольшую особенность свойства **AppEventProperties.HostWebFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="17515-180">Now our code has to deal with a little quirk of the **AppEventProperties.HostWebFullUrl** property.</span></span> <span data-ttu-id="17515-181">В большинстве других контекстов SharePoint добавляет закрывающий символ косой черты "`"/"`" в конец URL-адреса хост-сайта, поэтому в нашем примере кода предполагается, что этот символ присутствует.</span><span class="sxs-lookup"><span data-stu-id="17515-181">In most other contexts, SharePoint includes a closing `"/"` character at the end of the host web URL, so the logic of our sample code assumes that this character is present.</span></span> <span data-ttu-id="17515-182">Но SharePoint добавляет этот символ в конец значения **HostWebFullUrl**, исключительно когда хост-сайт является корневым веб-сайтом семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="17515-182">But SharePoint adds this character at the end of the **HostWebFullUrl** value if, and only if, the host web is the root web of a site collection.</span></span> <span data-ttu-id="17515-183">Так как наш веб-сайт магазина в Гонконге представляет собой подсайт в семействе веб-сайтов, то нам потребуется добавить этот символ, чтобы во всем примере использовалось одно имя клиента.</span><span class="sxs-lookup"><span data-stu-id="17515-183">Because our Hong Kong website is a subweb in the site collection, we need to add this character to ensure that the same tenant name string is used throughout the sample.</span></span> 

   <span data-ttu-id="17515-184">Добавьте указанный ниже код сразу после блока инициализации объекта `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="17515-184">Add the following code under the initialization of the `tenantName` object.</span></span>
    
    ```C#
      if (!tenantName.EndsWith("/"))
    {
        tenantName += "/";
    }
    ```

9. <span data-ttu-id="17515-185">Добавьте указанные ниже операторы **using** в начало файла.</span><span class="sxs-lookup"><span data-stu-id="17515-185">Add the following **using** statements to the top of the file.</span></span>
    
    ```C#
      using System.Data.SqlClient;
      using System.Data;
      using ChainStoreWeb.Utilities;
    ```

10. <span data-ttu-id="17515-186">Добавьте указанный ниже метод в класс `AppEventReceiver`.</span><span class="sxs-lookup"><span data-stu-id="17515-186">Add the following method to the `AppEventReceiver` class.</span></span> <span data-ttu-id="17515-187">Мы не будем подробно рассматривать его, так как цель этой серии статей научить вас программированию надстроек SharePoint, а не программированию для SQL Server или Azure.</span><span class="sxs-lookup"><span data-stu-id="17515-187">We don't discuss this in detail because the purpose of this series of articles is to teach SharePoint Add-in programming, not SQL Server/Azure programming.</span></span>

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

    <span data-ttu-id="17515-188">Этот метод будет создавать строку в таблице **Tenants** (Клиенты) базы данных.</span><span class="sxs-lookup"><span data-stu-id="17515-188">This method creates a row in a database table called **Tenants**.</span></span> <span data-ttu-id="17515-189">Кроме столбца **Name** (Имя), в таблице имеется столбец **Version** (Версия) со значением 0000.0000.0000.0000, используемым по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="17515-189">In addition to the **Name** column, the table also has a **Version** column with a default value set to 0000.0000.0000.0000.</span></span> <span data-ttu-id="17515-190">В одной из следующих статей этой серии вы создадите код, выполняемый во время первого запуска, который будет использовать это значение, чтобы определить, установлена ли надстройка на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="17515-190">In a later article in this series, you will create first-run logic that looks at this value to determine whether the add-in has already been installed on the host web.</span></span> <span data-ttu-id="17515-191">Если номер версии равен 0000.0000.0000.0000, то ваш код развернет списки **Local Employees** (Местные сотрудники) и **Expected Shipments** (Ожидаемые отгрузки), а затем увеличит номер версии.</span><span class="sxs-lookup"><span data-stu-id="17515-191">If the version is 0000.0000.0000.0000, your code deploys the **Local Employees** and **Expected Shipments** lists, and then raises the version number.</span></span>
    
## <a name="create-the-uninstallation-handler"></a><span data-ttu-id="17515-192">Создание обработчика события удаления</span><span class="sxs-lookup"><span data-stu-id="17515-192">Create the uninstallation handler</span></span>

<span data-ttu-id="17515-193">При обработке события установки обычно рекомендуется обрабатывать и событие удаления.</span><span class="sxs-lookup"><span data-stu-id="17515-193">It is usually a good practice to handle the uninstalling event whenever you are handling the installed event.</span></span> <span data-ttu-id="17515-194">Основная причина этого состоит в том, что обработчик события удаления должен перемещать в корзину или удалять объекты, установленные обработчиком события установки.</span><span class="sxs-lookup"><span data-stu-id="17515-194">The basic idea is that the uninstalling handler deletes or recycles things that the installed handler deployed.</span></span> <span data-ttu-id="17515-195">Тем не менее существует много исключений, поэтому вам необходимо хорошо понимать варианты использования вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="17515-195">There are, however, many exceptions, so you really need to understand the use cases of your add-in.</span></span> <span data-ttu-id="17515-196">Например, в списке, который развернут и заполнен надстройкой, могут остаться значения даже после ее удаления, поэтому вам может потребоваться, чтобы обработчик события удаления не удалял этот список.</span><span class="sxs-lookup"><span data-stu-id="17515-196">For example, a list that is deployed with an add-in and populated with the add-in might still have value even after the add-in itself is uninstalled, in which case you wouldn't want to uninstall the list in the uninstalling event handler.</span></span> 

<span data-ttu-id="17515-197">Если пользователь удаляет надстройку со страницы **Site Contents** (Содержание сайта), то событие удаления не запускается (как можно было бы ожидать).</span><span class="sxs-lookup"><span data-stu-id="17515-197">The uninstallation event does not run, as you might expect, when a user removes the add-in from the **Site Contents** page.</span></span> <span data-ttu-id="17515-198">В этом случае надстройка только перемещается в корзину веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="17515-198">Doing so only moves the add-in to the website's Recycle Bin.</span></span> <span data-ttu-id="17515-199">Пользователь может восстановить ее, но при восстановлении не будет перезапущен обработчик события установки. Поэтому при восстановлении надстройки вам может потребоваться, чтобы по-прежнему существовали все объекты, развернутые обработчиком события установки.</span><span class="sxs-lookup"><span data-stu-id="17515-199">A user could restore it, but restoring does not rerun the installed event handler, so you'd want anything that was deployed with the installed event handler to still exist if the add-in is restored.</span></span> <span data-ttu-id="17515-200">Компоненты SharePoint можно переместить из корзины во вторую корзину.</span><span class="sxs-lookup"><span data-stu-id="17515-200">SharePoint components can be moved from the Recycle Bin to the second-stage Recycle Bin.</span></span> <span data-ttu-id="17515-201">Событие удаления будет создано только после удаления надстройки из второй корзины. Если пользователь сделает это, то надстройка будет безвозвратно удалена, поэтому в этот момент нам понадобится удалить область клиента магазина в Гонконге из корпоративной базы данных.</span><span class="sxs-lookup"><span data-stu-id="17515-201">It is only when an add-in is deleted from the second-stage that the uninstalling event happens; when a user does that, the add-in is unrestorable anyway, so we want the Hong Kong store's tenancy to be removed from the corporate database at that point.</span></span>

1. <span data-ttu-id="17515-202">Присвойте параметру **Управление удалением надстроек** значение **True** (этот параметр может по-прежнему называться **Управление удалением приложений**).</span><span class="sxs-lookup"><span data-stu-id="17515-202">Set the value of **Handle Add-in Uninstalling** to **True** (it may still be called **Handle App Uninstalling**).</span></span> <span data-ttu-id="17515-203">Благодаря этому обработчик будет зарегистрирован в файле AppManifest.xml точно так же, как ранее был зарегистрирован обработчик события установки.</span><span class="sxs-lookup"><span data-stu-id="17515-203">This registers the handler in the AppManifest.xml file just as you earlier registered the installation handler.</span></span> <span data-ttu-id="17515-204">Если вы просмотрите содержимое файла, то увидите, что у них абсолютно одинаковые URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="17515-204">If you look at the file, you see that they have exactly the same URL.</span></span> <span data-ttu-id="17515-205">Пакет "Инструменты разработчика Office для Visual Studio" предполагает, что вы используете один и тот же файл \*.svc.</span><span class="sxs-lookup"><span data-stu-id="17515-205">The Office Developer Tools for Visual Studio assumes that you are using the same \*.svc file.</span></span> <span data-ttu-id="17515-206">Мы делаем это в данном примере. Кроме того, это стандартная рекомендация.</span><span class="sxs-lookup"><span data-stu-id="17515-206">We are doing that in this sample, and it is a standard practice.</span></span> 

2. <span data-ttu-id="17515-207">Добавьте приведенный ниже код вместо заполнителя `TODO3` в файле AppEventReceiver.svc.cs.</span><span class="sxs-lookup"><span data-stu-id="17515-207">Add the following code in place of `TODO3` in the AppEventReceiver.svc.cs file.</span></span> 

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

   <span data-ttu-id="17515-208">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="17515-208">Note the following about this code:</span></span>

   - <span data-ttu-id="17515-209">Метод `DeleteTenant` будет добавлен на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="17515-209">The `DeleteTenant` method is added in the next step.</span></span>
   - <span data-ttu-id="17515-210">При откате удаления надстройка останется во второй корзине, из которой ее все еще можно восстановить.</span><span class="sxs-lookup"><span data-stu-id="17515-210">Rolling back the uninstallation of the add-in leaves it in the second-stage Recycle Bin, from which it could still be restored.</span></span>

3. <span data-ttu-id="17515-211">Добавьте указанный ниже метод в класс `AppEventReceiver`.</span><span class="sxs-lookup"><span data-stu-id="17515-211">Add the following method to the `AppEventReceiver` class.</span></span>
    
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

> [!NOTE]
> <span data-ttu-id="17515-212">В предыдущей статье этой серии вы настроили проект так, чтобы при каждом нажатии клавиши F5 выполнялась перестройка корпоративной базы данных.</span><span class="sxs-lookup"><span data-stu-id="17515-212">In an earlier article in this series, you configured the project to rebuild the corporate database each time you select F5.</span></span> <span data-ttu-id="17515-213">Это приводит к очистке таблицы **Tenants** (Клиенты).</span><span class="sxs-lookup"><span data-stu-id="17515-213">This empties the **Tenants** table.</span></span>

## <a name="run-the-add-in-and-test-the-installation-handler"></a><span data-ttu-id="17515-214">Запуск надстройки и тестирование обработчика установки</span><span class="sxs-lookup"><span data-stu-id="17515-214">Run the add-in and test the installation handler</span></span>

1. <span data-ttu-id="17515-215">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="17515-215">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="17515-216">Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express.</span><span class="sxs-lookup"><span data-stu-id="17515-216">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="17515-217">Кроме того, он временно устанавливает надстройку на вашем тестовом сайте SharePoint, запускает обработчик события установки и немедленно запускает надстройку.</span><span class="sxs-lookup"><span data-stu-id="17515-217">It also makes a temporary installation of the add-in on your test SharePoint site, runs the installation event handler, and immediately runs the add-in.</span></span> <span data-ttu-id="17515-218">Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="17515-218">You are prompted to grant permissions to the add-in before its start page opens.</span></span> 

2. <span data-ttu-id="17515-219">Когда откроется начальная страница надстройки, щелкните значок с изображением шестеренки на расположенном вверху элементе управления хрома и выберите **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="17515-219">When the add-in's start page opens, select the gear icon on the chrome control at the top, and then select **Account settings**.</span></span>

3. <span data-ttu-id="17515-220">На странице **Учетные записи** нажмите кнопку **Показать версию надстройки**.</span><span class="sxs-lookup"><span data-stu-id="17515-220">On the **Accounts settings** page, select the **Show Add-in Version** button.</span></span> <span data-ttu-id="17515-221">Отобразится номер версии 0000.0000.0000.0000.</span><span class="sxs-lookup"><span data-stu-id="17515-221">The version shows as 0000.0000.0000.0000.</span></span>
    
   <span data-ttu-id="17515-222">*Рис. 1. Страница "Параметры учетной записи"*</span><span class="sxs-lookup"><span data-stu-id="17515-222">*Figure 1. Account settings page*</span></span>

   ![Страница "Параметры учетной записи" с заголовком "Параметры учетной записи", кнопкой "Показать версию надстройки" и строкой "Зарегистрированная версия: ноль ноль ноль ноль точка ноль ноль ноль ноль точка ноль ноль ноль ноль точка ноль ноль ноль ноль" под этой кнопкой.](../images/2a905b7d-89c7-456a-8456-21a9b7e9efc5.PNG)

4. <span data-ttu-id="17515-224">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17515-224">To end the debugging session, close the browser window or stop debugging in Visual Studio.</span></span> <span data-ttu-id="17515-225">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="17515-225">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

5. <span data-ttu-id="17515-226">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="17515-226">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while.</span></span> <span data-ttu-id="17515-227">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="17515-227">Right-click the project in **Solution Explorer** and select **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17515-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17515-228">Next steps</span></span>
<span data-ttu-id="17515-229"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="17515-229"></span></span>

<span data-ttu-id="17515-230">В следующей статье этой серии вы добавите в надстройку код, выполняемый при первом запуске, для автоматического развертывания списка **Local Employees** (Местные сотрудники) и настраиваемой кнопки ленты: [Добавление кода, выполняемого при первом запуске, в надстройку, размещаемую у поставщика](add-first-run-logic-to-the-provider-hosted-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="17515-230">In the next article of the series, you will add first-run logic to the add-in that programmatically deploys the **Local Employees** list and the custom ribbon button: [Add first-run logic to the provider-hosted add-in](add-first-run-logic-to-the-provider-hosted-add-in.md).</span></span>
 

 

