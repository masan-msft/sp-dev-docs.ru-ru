---
title: "Обработка событий в надстройке с размещением у поставщика"
description: "Настройка установки надстройки SharePoint, размещаемой у поставщика, путем конфигурирования решения для отладки приемника событий, создания обработчиков событий установки и удаления, запуска надстройки и тестирования этих обработчиков."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: bfbff7d0fb0a477eddfc5ba9d77b760195e85bae
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="handle-add-in-events-in-the-provider-hosted-add-in"></a><span data-ttu-id="4e3e8-103">Обработка событий в надстройке с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="4e3e8-103">Handle add-in events in the provider-hosted add-in</span></span>

<span data-ttu-id="4e3e8-104">Это седьмая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых у поставщика. Для начала вам следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-104">This is the seventh in a series of articles about the basics of developing provider-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>

-  [<span data-ttu-id="4e3e8-105">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="4e3e8-105">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="4e3e8-106">Настройка внешнего вида надстройки SharePoint, размещенной у поставщика</span><span class="sxs-lookup"><span data-stu-id="4e3e8-106">Give your provider-hosted add-in the SharePoint look-and-feel</span></span>](give-your-provider-hosted-add-in-the-sharepoint-look-and-feel.md)
-  [<span data-ttu-id="4e3e8-107">Добавление настраиваемой кнопки в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="4e3e8-107">Include a custom button in the provider-hosted add-in</span></span>](include-a-custom-button-in-the-provider-hosted-add-in.md)
-  [<span data-ttu-id="4e3e8-108">Краткий обзор объектной модели SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e3e8-108">Get a quick overview of the SharePoint object model</span></span>](get-a-quick-overview-of-the-sharepoint-object-model.md)
-  [<span data-ttu-id="4e3e8-109">Добавление операций записи SharePoint в надстройку, размещенную у поставщика</span><span class="sxs-lookup"><span data-stu-id="4e3e8-109">Add SharePoint write operations to the provider-hosted add-in</span></span>](add-sharepoint-write-operations-to-the-provider-hosted-add-in.md)
-  [<span data-ttu-id="4e3e8-110">Добавление веб-части надстройки в надстройку, размещаемую у поставщика</span><span class="sxs-lookup"><span data-stu-id="4e3e8-110">Include an add-in part in the provider-hosted add-in</span></span>](include-an-add-in-part-in-the-provider-hosted-add-in.md)

> [!NOTE]
> <span data-ttu-id="4e3e8-111">Если вы изучали предыдущие статьи из этой серии о надстройках, размещаемых у поставщика, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-111">Note  If you have been working through this series about provider-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_Provider-hosted_Add-Ins_Tutorials and open the BeforeRibbonButton.sln file.</span></span> <span data-ttu-id="4e3e8-112">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) и открыть файл BeforeAdd-inEventHandlers.sln.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-112">You can also download the repository at [SharePoint_Provider-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_Provider-hosted_Add-ins_Tutorials) and open the BeforeAdd-inEventHandlers.sln file.</span></span>

<span data-ttu-id="4e3e8-113">В данной статье мы настроим в SharePoint обработку событий, которые называются событиями надстройки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-113">In this article, we customize the handling of a kind of event in SharePoint called add-in events.</span></span> <span data-ttu-id="4e3e8-114">В частности, мы создадим обработчики событий установки и удаления надстройки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-114">Specifically, we create handlers for the add-in installation and uninstallation events.</span></span> <span data-ttu-id="4e3e8-115">Кроме того, настраиваемые обработчики можно использовать для событий списка и элементов списка. О таких обработчиках вы узнаете в одной из следующих статей этой серии.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-115">List and list item events can also get custom handling; you'll learn about these in a later article in this series.</span></span> <span data-ttu-id="4e3e8-116">Все эти события создаются в SharePoint, но настраиваемый код, обрабатывающий каждое событие, находится в вашем удаленном веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-116">All of these events are triggered in SharePoint, but your custom code that handles each event is in your remote web application.</span></span> <span data-ttu-id="4e3e8-117">Вы настроите SharePoint для вызова настраиваемого обработчика, зарегистрировав его URL-адрес для события SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-117">You configure SharePoint to call your custom handler by registering the handler's URL with the SharePoint event.</span></span>

## <a name="two-places-to-programmatically-deploy-sharepoint-components"></a><span data-ttu-id="4e3e8-118">Два места для программного развертывания компонентов SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e3e8-118">Two places to programmatically deploy SharePoint components</span></span>

<span data-ttu-id="4e3e8-119">Мы хотим, чтобы наша надстройка Chain Store автоматически создавала и развертывала списки **Local Employees** (Местные сотрудники) и **Expected Shipments** (Ожидаемые отгрузки).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-119">We want our Chain Store add-in to create and deploy the **Local Employees** and **Expected Shipments** lists automatically.</span></span> <span data-ttu-id="4e3e8-120">Надстройка может в любое время развертывать компоненты SharePoint, например настраиваемые списки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-120">An add-in can deploy SharePoint components, such as a custom list, any time.</span></span> <span data-ttu-id="4e3e8-121">Но если надстройка зависит от определенного компонента, например настраиваемого списка, этот компонент необходимо развернуть, *прежде чем* пользователи начнут работать с надстройкой.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-121">But when an add-in depends on a specific component such as a custom list, the component really should be deployed *before* users start working with the add-in.</span></span> <span data-ttu-id="4e3e8-122">Для таких критически важных компонентов настраиваемый код, выполняющий развертывание, можно разместить в двух местах:</span><span class="sxs-lookup"><span data-stu-id="4e3e8-122">For such vital components, there are two places where the custom deployment logic can go:</span></span>

- <span data-ttu-id="4e3e8-123">в обработчике события установки для надстройки;</span><span class="sxs-lookup"><span data-stu-id="4e3e8-123">In a handler for the add-in installation event.</span></span>
- <span data-ttu-id="4e3e8-124">в коде, выполняемом при первом запуске надстройки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-124">In "first run" logic that executes the first time the add-in is launched in SharePoint.</span></span>

<span data-ttu-id="4e3e8-p104">Описание процесса принятия решения о том, какой способ лучше подходит для конкретной надстройки, выходит за рамки данной статьи. В нашей статье мы приведем только несколько соображений, оказывающих влияние на выбор.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-p104">Deciding which is best for a given add-in is an advanced topic. In this article, we can only mention a few points of comparison:</span></span>

- <span data-ttu-id="4e3e8-p105">Работа настраиваемого обработчика установки должна завершиться в течение 30 секунд. Время работы кода, выполняемого при первом запуске, не ограничено.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-p105">A custom installation handler has to complete in 30 seconds. There is no limit to how long first-run logic can take.</span></span>

- <span data-ttu-id="4e3e8-129">Если в процессе установки надстройки что-то пойдет не так, SharePoint откатит все действия, которые он выполнил в ходе установки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-129">If anything goes wrong during an add-in installation, SharePoint rolls back everything it has done as part of the installation.</span></span> <span data-ttu-id="4e3e8-130">Настраиваемый обработчик события установки запускается *после* того как SharePoint выполнит все действия, необходимые для установки надстройки, поэтому обработчик может принять участие в работе этой системы.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-130">A custom installation handler runs *after* SharePoint has done everything it's going to do to install the add-in, so a custom handler can participate in this system.</span></span> 

   <span data-ttu-id="4e3e8-131">Например, если ваш настраиваемый код создал исключение, вы можете сообщить SharePoint, что необходимо полностью откатить установку надстройки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-131">For example, if your custom logic throws an exception, you can tell SharePoint to roll back the entire add-in installation.</span></span> <span data-ttu-id="4e3e8-132">Если же что-то пойдет не так в настраиваемом коде, выполняемом при первом запуске, надстройка останется установленной и, возможно, будет работать неправильно.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-132">If something goes wrong in custom first-run logic, however, the add-in remains installed and presumably won't work properly.</span></span>

- <span data-ttu-id="4e3e8-133">Если SharePoint придется откатить установку надстройки, он не "успокоится" на этом.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-133">SharePoint doesn't give up if it has to roll back an add-in installation.</span></span> <span data-ttu-id="4e3e8-134">Он сразу же попытается установить надстройку еще раз.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-134">It immediately tries the installation again.</span></span> <span data-ttu-id="4e3e8-135">Будет предпринято до 4 попыток (на каждую попытку выделяется 30 секунд).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-135">It makes up to four attempts (the 30-second time limit applies on each attempt).</span></span> <span data-ttu-id="4e3e8-136">При каждой повторной попытке настраиваемый обработчик события установки *запускается с самого начала*.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-136">Each time it retries, the custom installation handler runs again *from the beginning*.</span></span> <span data-ttu-id="4e3e8-137">Если обработчик установил, например, список, перед откатом всех действий, то он будет пытаться установить этот же список при каждой новой попытке установить надстройку.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-137">If the handler managed to install, say, a list, before the rollback, it tries to install the same list again on the retry.</span></span> 

   <span data-ttu-id="4e3e8-138">Чтобы не допустить этого, необходимо написать код обработчика события установки таким образом, чтобы он не выполнял никаких действий (например, развертывание компонента), прежде чем проверит, не выполнено ли это действие ранее.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-138">To prevent this from happening, code in an installation handler has to be written so that it won't take any action (such as deploy a component) unless it first checks to see if that action has already been done.</span></span> <span data-ttu-id="4e3e8-139">Из-за этого код обработчика события установки сложнее кода, выполняемого при первом запуске, так как последний не выполняется повторно (если, конечно, вы намеренно не запрограммируете повторное выполнение).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-139">This makes the logic of an installation handler more complex than first-run logic because first-run logic won't retry (unless you specifically code it to do so).</span></span> <span data-ttu-id="4e3e8-140">Кроме того, чтобы проверить, не развернут ли какой-либо компонент, необходимо выполнить затратный по времени вызов через Интернет от удаленного обработчика к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-140">Also, checking to see if a component has already been deployed usually requires a time-consuming call over the Internet from the remote handler to SharePoint.</span></span> <span data-ttu-id="4e3e8-141">После этого понадобится выполнить второй вызов для развертывания компонента (если он еще не развернут).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-141">A second call is also needed to actually deploy the component (if it has not already been deployed).</span></span>

<span data-ttu-id="4e3e8-142">В надстройке Chain Store мы объединим эти стратегии.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-142">For the Chain Store add-in, we combine these strategies.</span></span> <span data-ttu-id="4e3e8-143">В этой статье вы создадите обработчик события установки, который будет регистрировать хост-сайт в качестве клиента в корпоративной базе данных, а затем задавать сигнал о том, запущена ли уже надстройка на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-143">In this article, you create an installation handler that registers the host web as a tenant in the corporate database and then sets a signal that specifies whether the add-in has been run yet on the host web.</span></span> 

<span data-ttu-id="4e3e8-144">В одной из следующих статей этой серии вы добавите код, выполняемый при первом запуске, в метод **Page_Load** начальной страницы надстройки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-144">In a later article in this series, you'll put first-run logic in the **Page_Load** method of the add-ins start page.</span></span> <span data-ttu-id="4e3e8-145">Этот код будет развертывать два настраиваемых списка и выполнять ряд других действий.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-145">This logic deploys the two custom lists and does some other things, too.</span></span>

<span data-ttu-id="4e3e8-146"><a name="RERDebug"> </a></span><span class="sxs-lookup"><span data-stu-id="4e3e8-146"></span></span>
## <a name="configure-the-solution-for-event-receiver-debugging"></a><span data-ttu-id="4e3e8-147">Настройка решения для отладки приемника событий</span><span class="sxs-lookup"><span data-stu-id="4e3e8-147">Configure the solution for event receiver debugging</span></span>

<span data-ttu-id="4e3e8-148">Для отладки приемников событий необходимо использовать служебную шину Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-148">Debugging of event receivers requires the use of the Azure Service Bus.</span></span> <span data-ttu-id="4e3e8-149">Следуйте инструкциям в статье [Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-149">[Debug and troubleshoot a remote event receiver in a SharePoint Add-in](debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in.md)</span></span> <span data-ttu-id="4e3e8-150">Так как в качестве тестового сайта вы используете веб-сайт SharePoint Online, не забудьте выполнить эти инструкции на удаленном тестовом сайте.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-150">Because you are using a SharePoint Online website as your test site, ensure that you carry out the instructions for a remote test site.</span></span> <span data-ttu-id="4e3e8-151">В следующих статьях этой серии подразумевается, что вы успешно настроили среду отладки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-151">The remainder of this series assumes you have configured debugging successfully.</span></span> 

## <a name="create-the-installation-handler"></a><span data-ttu-id="4e3e8-152">Создание обработчика установки</span><span class="sxs-lookup"><span data-stu-id="4e3e8-152">Create the installation handler</span></span>

> [!NOTE]
> <span data-ttu-id="4e3e8-153">Когда решение открывается повторно, для параметров раздела "Запускаемые проекты" в Visual Studio обычно возвращаются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-153">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> <span data-ttu-id="4e3e8-154">Сразу же после повторного открытия примера решения согласно инструкциям из этой серии статей всегда делайте вот что:</span><span class="sxs-lookup"><span data-stu-id="4e3e8-154">Note  The settings for Startup Projects in Visual Studio tend to revert to defaults whenever the solution is reopened. Always take these steps immediately after reopening the sample solution in this series of articles:</span></span> 
> 1. <span data-ttu-id="4e3e8-155">В верхней части **обозревателя решений** щелкните узел решения правой кнопкой мыши и выберите пункт **Назначить запускаемые проекты**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-155">Right-click the solution node at the top of  **Solution Explorer** and select **Set startup projects**.</span></span>  
> 2. <span data-ttu-id="4e3e8-156">Убедитесь, что в столбце **Действие** для всех трех проектов указано значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-156">Make sure all three projects are set to  **Start** in the **Action** column.</span></span>

1. <span data-ttu-id="4e3e8-157">В **обозревателе решений** выберите проект **ChainStore**, чтобы его свойства отобразились в области **Свойства** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-157">In  **Solution Explorer**, select the  **ChainStore** project, so its properties appear in the **Properties** pane of Visual Studio.</span></span>

2. <span data-ttu-id="4e3e8-158">Задайте для параметра **Управление установленными надстройками** значение **True** (этот параметр может по-прежнему называться **Управление установленными приложениями**).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-158">Set the value of  **Handle Add-in Installed** to **True**. (It may still be called  **Handle App Installed**.) This does two things:</span></span> <span data-ttu-id="4e3e8-159">При этом выполняется два следующих действия:</span><span class="sxs-lookup"><span data-stu-id="4e3e8-159">This does two things:</span></span>
    
   - <span data-ttu-id="4e3e8-160">В проекте **ChainStoreWeb** (но не в проекте **ChainStore**) создается папка **Services** (Службы), в которую будут добавлены два файла: файл AppEventReceiver.svc и его файл кода программной части AppEventReceiver.svc.cs. (Имена файлов начинаются со строки App, так как ранее надстройки назывались приложениями. *Не переименовывайте эти файлы*. Для правильной работы пакета "Инструменты разработчика Office для Visual Studio" необходимо, чтобы файлы имели именно эти имена.)</span><span class="sxs-lookup"><span data-stu-id="4e3e8-160">A folder called  **Services** is created in the **ChainStoreWeb** project (not the **ChainStore** project) and two files are added to it: a AppEventReceiver.svc file and its code behind AppEventReceiver.svc.cs file. (The file names begin with the string "App", because add-ins used to be called "apps". *Don't rename these files.*  The Office Developer Tools for Visual Studio assume the files will keep these names. )</span></span>

   - <span data-ttu-id="4e3e8-161">URL-адрес обработчика регистрируется в манифесте надстройки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-161">The handler URL is registered in the add-in manifest.</span></span> <span data-ttu-id="4e3e8-162">Эта часть манифеста не отображается в конструкторе манифеста.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-162">This part of the manifest is not visible in the manifest designer.</span></span> <span data-ttu-id="4e3e8-163">Чтобы отобразить ее, щелкните правой кнопкой мыши файл AppManifest.xml и выберите пункт **Просмотр кода**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-163">To see it, right-click the AppManifest.xml file and select **View Code**.</span></span> <span data-ttu-id="4e3e8-164">Новый дочерний элемент элемента **Свойства** выглядит, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-164">A new child of the **Properties** element looks like the following.</span></span> 
   
      ```XML
        <InstalledEventEndpoint>~remoteAppUrl/Services/AppEventReceiver.svc</InstalledEventEndpoint>
      ``` 
   
     <span data-ttu-id="4e3e8-165">Эта разметка сообщает SharePoint, что когда он завершит всю работу по установке надстройки, необходимо будет вызвать метод **ProcessEvent** этой службы.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-165">This markup tells SharePoint to call the **ProcessEvent** method of this service when it has finished doing all of its own work related to installing the add-in.</span></span> <span data-ttu-id="4e3e8-166">Настраиваемый обработчик — это последний компонент, запускаемый в процессе установки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-166">The custom handler is the last thing that runs as part of the installation.</span></span> <span data-ttu-id="4e3e8-167">Строка `~remoteAppUrl` — это заполнитель, который пакет "Инструменты разработчика Office для Visual Studio" заменит URL-адресом узла службы.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-167">The string `~remoteAppUrl` is a placeholder that the Office Developer Tools for Visual Studio replaces with the service host URL.</span></span> <span data-ttu-id="4e3e8-168">При отладке в качестве этого URL-адреса используется URL-адрес служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-168">When you are debugging, it is an Azure Service Bus URL.</span></span> <span data-ttu-id="4e3e8-169">При создании пакета для развертывания в рабочей среде используется URL-адрес рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-169">When you create the package for deployment to production, it is the production URL.</span></span>

3. <span data-ttu-id="4e3e8-170">Откройте файл AppEventReceiver.svc.cs.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-170">Open the AppEventReceiver.svc.cs file.</span></span>
    
4. <span data-ttu-id="4e3e8-171">Вы увидите, что пакет "Инструменты разработчика Office для Visual Studio" создал пример реализации метода **ProcessEvent**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-171">You see that the Office Developer Tools for Visual Studio has created a sample implementation of the **ProcessEvent** method.</span></span> <span data-ttu-id="4e3e8-172">Все реализации этого метода начинаются с инициализации объекта **SPRemoteEventResult** и заканчиваются возвращением этого объекта в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-172">All implementations of this method begin by initializing an **SPRemoteEventResult** object, and they all end by returning that object to SharePoint.</span></span> <span data-ttu-id="4e3e8-173">Помимо прочего, этот объект сообщает SharePoint, следует ли откатить событие из-за сбоя кода настраиваемого обработчика.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-173">Among other things, this object tells SharePoint whether or not it should roll back the event because the custom handling logic has failed.</span></span> 

   <span data-ttu-id="4e3e8-174">Кроме того, возможно, пакет инструментов включил в этот метод блок **using**, который создает объект **ClientContext**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-174">The tools may also have included a **using** block in this method that creates a **ClientContext** object.</span></span> <span data-ttu-id="4e3e8-175">Настраиваемый обработчик в надстройке Chain Store не будет делать обратный вызов в SharePoint, поэтому удалите этот блок.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-175">The custom handler in the Chain Store add-in isn't going to call back into SharePoint, so delete this block.</span></span> <span data-ttu-id="4e3e8-176">Теперь метод должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="4e3e8-176">The method should now look like the following.</span></span>
    
    ```C#
       public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
     {
         SPRemoteEventResult result = new SPRemoteEventResult();

         return result;
     }
    ```

5. <span data-ttu-id="4e3e8-177">Приемник событий можно вызвать с помощью любого из трех возможных событий надстройки, поэтому добавьте приведенную ниже структуру **switch** в метод **ProcessEvent** между строками, в которых создается и возвращается объект `result`. Имена событий включают строку App (Приложение), так как ранее надстройки назывались приложениями.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-177">The event receiver could be called by any of three possible add-in events, so add the following  **switch** structure to the **ProcessEvent** method in between the lines that create and return the `result` object. The event names have the string "App" in them because add-ins used to be called "apps".</span></span>
    
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

6. <span data-ttu-id="4e3e8-178">Для регистрации магазина в Гонконге в качестве клиента в удаленном веб-приложении наш код, выполняемый во время установки, должен вызывать хранимую процедуру SQL.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-178">Our installation logic is going to call an SQL stored procedure to register the Hong Kong store as a tenant in the remote web application.</span></span> <span data-ttu-id="4e3e8-179">Очень важно, чтобы при сбое процесса обработчик сообщил SharePoint, что необходимо откатить установку надстройки. Поэтому добавьте указанные ниже блоки **try/catch** вместо `TODO2`.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-179">Our installation logic is going to call an SQL stored procedure to register the Hong Kong store as a tenant in the remote web application. It is very important that, if this process fails, the handler signals SharePoint to roll back the installation of the add-in, so add the following  **try/catch** blocks in place of `TODO2`. Note the following about this code:</span></span> 

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

   <span data-ttu-id="4e3e8-180">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="4e3e8-180">Note the following about this code:</span></span>

   - <span data-ttu-id="4e3e8-181">Вы создадите объект `tenantName` и метод `CreateTenant` на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-181">You will create the  `tenantName` object and `CreateTenant` method in a later step.</span></span>
   - <span data-ttu-id="4e3e8-p120">Свойство **Status** объекта **SPRemoteEventResult** может иметь три одно из трех следующих значений: **Continue** (используется по умолчанию), **CancelNoError** и **CancelWithError**. Два последних значения сообщают SharePoint, что необходимо откатить событие.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-p120">The **Status** property of the **SPRemoteEventResult** object can have three possible values: **Continue** (the default), **CancelNoError**, and **CancelWithError**. Either of the latter two tell SharePoint to roll back the event.</span></span>

7. <span data-ttu-id="4e3e8-184">URL-адрес хост-сайта, представляющий собой дискриминатор клиента в примере, включается в сведения, которые SharePoint передает в приемник в параметре **SPRemoteEventProperties**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-184">The host web URL, which is the sample's tenant discriminator, is part of the information that SharePoint passes to the receiver in the **SPRemoteEventProperties** parameter. Add the following line to the ProcessEvent method on line that is just below the initialization of the SPRemoteEventResult object.</span></span> <span data-ttu-id="4e3e8-185">Добавьте указанную ниже строку в метод **ProcessEvent** в строку сразу же после блока инициализации объекта **SPRemoteEventResult**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-185">Add the following line to the **ProcessEvent** method on the line that is just under the initialization of the **SPRemoteEventResult** object.</span></span>
    
    ```C#
      string tenantName = properties.AppEventProperties.HostWebFullUrl.ToString();
    ```

8. <span data-ttu-id="4e3e8-186">Теперь в нашем коде придется учесть небольшую особенность свойства **AppEventProperties.HostWebFullUrl**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-186">Now our code has to deal with a little quirk of the **AppEventProperties.HostWebFullUrl** property.</span></span> <span data-ttu-id="4e3e8-187">В большинстве других контекстов SharePoint добавляет закрывающий символ косой черты "`"/"`" в конец URL-адреса хост-сайта, поэтому в нашем примере кода предполагается, что этот символ присутствует.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-187">In most other contexts, SharePoint includes a closing `"/"` character at the end of the host web URL, so the logic of our sample code assumes that this character is present.</span></span> <span data-ttu-id="4e3e8-188">Но SharePoint добавляет этот символ в конец значения **HostWebFullUrl**, исключительно когда хост-сайт является корневым веб-сайтом семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-188">But SharePoint adds this character at the end of the **HostWebFullUrl** value if, and only if, the host web is the root web of a site collection.</span></span> <span data-ttu-id="4e3e8-189">Так как наш веб-сайт магазина в Гонконге представляет собой подсайт в семействе веб-сайтов, то нам потребуется добавить этот символ, чтобы во всем примере использовалось одно имя клиента.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-189">Because our Hong Kong website is a subweb in the site collection, we need to add this character to ensure that the same tenant name string is used throughout the sample.</span></span> 

   <span data-ttu-id="4e3e8-190">Добавьте указанный ниже код сразу после блока инициализации объекта `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-190">Add the following code under the initialization of the `tenantName` object.</span></span>
    
    ```C#
      if (!tenantName.EndsWith("/"))
    {
        tenantName += "/";
    }
    ```

9. <span data-ttu-id="4e3e8-191">Добавьте указанные ниже операторы **using** в начало файла.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-191">Add the following **using** statements to the top of the file.</span></span>
    
    ```C#
      using System.Data.SqlClient;
      using System.Data;
      using ChainStoreWeb.Utilities;
    ```

10. <span data-ttu-id="4e3e8-192">Добавьте указанный ниже метод в класс `AppEventReceiver`.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-192">Add the following method to the  `AppEventReceiver` class.</span></span> <span data-ttu-id="4e3e8-193">Мы не будем подробно рассматривать его, так как цель этой серии статей научить вас программированию надстроек SharePoint, а не программированию для SQL Server или Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-193">Add the following method to the   class. We don't discuss this in detail because the purpose of this series of articles is to teach SharePoint Add-in programming, not SQL Server/Azure programming.</span></span>

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

    <span data-ttu-id="4e3e8-194">Этот метод будет создавать строку в таблице **Tenants** (Клиенты) базы данных.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-194">This method creates a row in a database table called **Tenants**.</span></span> <span data-ttu-id="4e3e8-195">Кроме столбца **Name** (Имя), в таблице имеется столбец **Version** (Версия) со значением 0000.0000.0000.0000, используемым по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-195">In addition to the **Name** column, the table also has a **Version** column with a default value set to 0000.0000.0000.0000.</span></span> <span data-ttu-id="4e3e8-196">В одной из следующих статей этой серии вы создадите код, выполняемый во время первого запуска, который будет использовать это значение, чтобы определить, установлена ли надстройка на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-196">In a later article in this series, you will create first-run logic that looks at this value to determine whether the add-in has already been installed on the host web.</span></span> <span data-ttu-id="4e3e8-197">Если номер версии равен 0000.0000.0000.0000, то ваш код развернет списки **Local Employees** (Местные сотрудники) и **Expected Shipments** (Ожидаемые отгрузки), а затем увеличит номер версии.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-197">If the version is 0000.0000.0000.0000, your code deploys the **Local Employees** and **Expected Shipments** lists, and then raises the version number.</span></span>
    
## <a name="create-the-uninstallation-handler"></a><span data-ttu-id="4e3e8-198">Создание обработчика события удаления</span><span class="sxs-lookup"><span data-stu-id="4e3e8-198">Create the uninstallation handler</span></span>

<span data-ttu-id="4e3e8-199">При обработке события установки обычно рекомендуется обрабатывать и событие удаления.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-199">It is usually a good practice to handle the uninstalling event whenever you are handling the installed event.</span></span> <span data-ttu-id="4e3e8-200">Основная причина этого состоит в том, что обработчик события удаления должен перемещать в корзину или удалять объекты, установленные обработчиком события установки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-200">The basic idea is that the uninstalling handler deletes or recycles things that the installed handler deployed.</span></span> <span data-ttu-id="4e3e8-201">Тем не менее существует много исключений, поэтому вам необходимо хорошо понимать варианты использования вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-201">There are, however, many exceptions, so you really need to understand the use cases of your add-in.</span></span> <span data-ttu-id="4e3e8-202">Например, в списке, который развернут и заполнен надстройкой, могут остаться значения даже после ее удаления, поэтому вам может потребоваться, чтобы обработчик события удаления не удалял этот список.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-202">It is usually good practice to handle the uninstalling event whenever you are handling the installed event. The basic idea is that the uninstalling handler deletes or recycles things that the installed handler deployed. There are, however, many exceptions, so you really need to understand the use cases of your add-in. For example, a list that is deployed with an add-in and populated with the add-in might still have value even after the add-in itself is uninstalled in which case you wouldn't want to uninstall the list in the uninstalling event handler.</span></span> 

<span data-ttu-id="4e3e8-203">Если пользователь удаляет надстройку со страницы **Site Contents** (Содержание сайта), то событие удаления не запускается (как можно было бы ожидать).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-203">The uninstallation event does not run, as you might expect, when a user removes the add-in from the **Site Contents** page.</span></span> <span data-ttu-id="4e3e8-204">В этом случае надстройка только перемещается в корзину веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-204">Doing so only moves the add-in to the website's Recycle Bin.</span></span> <span data-ttu-id="4e3e8-205">Пользователь может восстановить ее, но при восстановлении не будет перезапущен обработчик события установки. Поэтому при восстановлении надстройки вам может потребоваться, чтобы по-прежнему существовали все объекты, развернутые обработчиком события установки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-205">A user could restore it, but restoring does not rerun the installed event handler, so you'd want anything that was deployed with the installed event handler to still exist if the add-in is restored.</span></span> <span data-ttu-id="4e3e8-206">Компоненты SharePoint можно переместить из корзины во вторую корзину.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-206">SharePoint components can be moved from the Recycle Bin to the second-stage Recycle Bin.</span></span> <span data-ttu-id="4e3e8-207">Событие удаления будет создано только после удаления надстройки из второй корзины. Если пользователь сделает это, то надстройка будет безвозвратно удалена, поэтому в этот момент нам понадобится удалить область клиента магазина в Гонконге из корпоративной базы данных.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-207">It is only when an add-in is deleted from the second-stage that the uninstalling event happens; when a user does that, the add-in is unrestorable anyway, so we want the Hong Kong store's tenancy to be removed from the corporate database at that point.</span></span>

1. <span data-ttu-id="4e3e8-208">Присвойте параметру **Управление удалением надстроек** значение **True** (этот параметр может по-прежнему называться **Управление удалением приложений**).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-208">Set the value of  **Handle Add-in Installed** to **True**. (It may still be called  **Handle App Installed**.) This does two things:</span></span> <span data-ttu-id="4e3e8-209">Благодаря этому обработчик будет зарегистрирован в файле AppManifest.xml точно так же, как ранее был зарегистрирован обработчик события установки.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-209">This registers the handler in the AppManifest.xml file just as you earlier registered the installation handler.</span></span> <span data-ttu-id="4e3e8-210">Если вы просмотрите содержимое файла, то увидите, что у них абсолютно одинаковые URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-210">If you look at the file, you see that they have exactly the same URL.</span></span> <span data-ttu-id="4e3e8-211">Пакет "Инструменты разработчика Office для Visual Studio" предполагает, что вы используете один и тот же файл \*.svc.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-211">The Office Developer Tools for Visual Studio assumes that you are using the same \*.svc file.</span></span> <span data-ttu-id="4e3e8-212">Мы делаем это в данном примере. Кроме того, это стандартная рекомендация.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-212">We are doing that in this sample, and it is a standard practice.</span></span> 

2. <span data-ttu-id="4e3e8-213">Добавьте приведенный ниже код вместо заполнителя `TODO3` в файле AppEventReceiver.svc.cs.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-213">Add the following code in place of  `TODO3` in the AppEventReceiver.svc.cs file. Note the following about this code:</span></span> 

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

   <span data-ttu-id="4e3e8-214">Обратите внимание на следующие особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="4e3e8-214">Note the following about this code:</span></span>

   - <span data-ttu-id="4e3e8-215">Метод `DeleteTenant` будет добавлен на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-215">The  `DeleteTenant` method is added in the next step.</span></span>
   - <span data-ttu-id="4e3e8-216">При откате удаления надстройка останется во второй корзине, из которой ее все еще можно восстановить.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-216">Rolling back the uninstallation of the add-in would leave it in the second-stage Recycle Bin, from which it could still be restored.</span></span>

3. <span data-ttu-id="4e3e8-217">Добавьте указанный ниже метод в класс `AppEventReceiver`.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-217">Add the following method to the  `AppEventReceiver` class.</span></span>
    
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
> <span data-ttu-id="4e3e8-218">В предыдущей статье этой серии вы настроили проект так, чтобы при каждом нажатии клавиши F5 выполнялась перестройка корпоративной базы данных.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-218">In an earlier article in this series, you configured the project to rebuild the corporate database each time you press F5. This empties the Tenants table.</span></span> <span data-ttu-id="4e3e8-219">Это приводит к очистке таблицы **Tenants** (Клиенты).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-219">This empties the **Tenants** table.</span></span>

## <a name="run-the-add-in-and-test-the-installation-handler"></a><span data-ttu-id="4e3e8-220">Запуск надстройки и тестирование обработчика установки</span><span class="sxs-lookup"><span data-stu-id="4e3e8-220">Run the add-in and test the installation handler</span></span>

1. <span data-ttu-id="4e3e8-221">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-221">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="4e3e8-222">Редактор Visual Studio размещает удаленное веб-приложение в IIS Express, а базу данных SQL — в SQL Express.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-222">Visual Studio hosts the remote web application in IIS Express and hosts the SQL database in SQL Express.</span></span> <span data-ttu-id="4e3e8-223">Кроме того, он временно устанавливает надстройку на вашем тестовом сайте SharePoint, запускает обработчик события установки и немедленно запускает надстройку.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-223">It also makes a temporary installation of the add-in on your test SharePoint site, runs the installation event handler, and immediately runs the add-in.</span></span> <span data-ttu-id="4e3e8-224">Прежде чем откроется начальная страница надстройки, вам будет предложено предоставить надстройке необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-224">You are prompted to grant permissions to the add-in before its start page opens.</span></span> 

2. <span data-ttu-id="4e3e8-225">Когда откроется начальная страница надстройки, щелкните значок с изображением шестеренки на расположенном вверху элементе управления хрома и выберите **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-225">When the add-in's start page opens, press the gear icon on the chrome control at the top, and select  **Account settings**.</span></span>

3. <span data-ttu-id="4e3e8-226">На странице **Учетные записи** нажмите кнопку **Показать версию надстройки**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-226">On the **Accounts settings** page, select the **Show Add-in Version** button.</span></span> <span data-ttu-id="4e3e8-227">Отобразится номер версии 0000.0000.0000.0000.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-227">On the Accounts page, press the Show Add-in Version button. The version shows as 0000.0000.0000.0000.</span></span>
    
   <span data-ttu-id="4e3e8-228">*Рис. 1. Страница "Параметры учетной записи"*</span><span class="sxs-lookup"><span data-stu-id="4e3e8-228">*Figure 1. Account settings page*</span></span>

   ![Страница "Параметры учетной записи" с заголовком "Параметры учетной записи", кнопкой "Показать версию надстройки" и строкой "Зарегистрированная версия: ноль ноль ноль ноль точка ноль ноль ноль ноль точка ноль ноль ноль ноль точка ноль ноль ноль ноль" под этой кнопкой.](../images/2a905b7d-89c7-456a-8456-21a9b7e9efc5.PNG)

4. <span data-ttu-id="4e3e8-230">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-230">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="4e3e8-231">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-231">Each time that you select F5, Visual Studio retracts the previous version of the add-in and installs the latest one.</span></span>

5. <span data-ttu-id="4e3e8-232">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-232">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="4e3e8-233">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="4e3e8-233">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e3e8-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e3e8-234">Next steps</span></span>
<span data-ttu-id="4e3e8-235"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="4e3e8-235"></span></span>

<span data-ttu-id="4e3e8-236">В следующей статье этой серии вы добавите в надстройку код, выполняемый при первом запуске, для автоматического развертывания списка **Local Employees** (Местные сотрудники) и настраиваемой кнопки ленты: [Добавление кода, выполняемого при первом запуске, в надстройку, размещаемую у поставщика](add-first-run-logic-to-the-provider-hosted-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="4e3e8-236">In the next article of the series, you will add first-run logic to the add-in that will programmatically deploy the **Local Employees** list and the custom ribbon button: [Add first-run logic to the provider-hosted add-in](add-first-run-logic-to-the-provider-hosted-add-in.md)</span></span>
 

 

