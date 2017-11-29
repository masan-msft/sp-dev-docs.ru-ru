---
title: "Задания таймера удаленного в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: edd7747655afb18aee647a17e7c4e47d7af0b394
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="remote-timer-jobs-in-the-sharepoint-add-in-model"></a><span data-ttu-id="5a0ba-102">Задания таймера удаленного в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="5a0ba-102">Remote timer jobs in the SharePoint add-in model</span></span>
================================================

<a name="summary"></a><span data-ttu-id="5a0ba-103">Summary</span><span class="sxs-lookup"><span data-stu-id="5a0ba-103">Summary</span></span>
-------

<span data-ttu-id="5a0ba-104">Подхода, можно реализовать задания таймера отличается в новой модели надстройки SharePoint не был с кодом полного доверия.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-104">The approach you take to implement timer jobs is different in the new SharePoint Add-in model than it was with Full Trust Code.</span></span>  <span data-ttu-id="5a0ba-105">В типичных полного доверия кода (FTC) / сценарий решения фермы, задания таймера SharePoint были созданы с помощью объектной модели SharePoint Server со стороны кода, развернутые с помощью решений фермы и управления в веб-сайта центра администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-105">In a typical Full Trust Code (FTC) / Farm Solution scenario, SharePoint Timer Jobs were created with the SharePoint Server Side Object Model code, deployed via Farm Solutions and managed in the SharePoint Central Administration web site.</span></span> <span data-ttu-id="5a0ba-106">SharePoint обрабатывает планирование и выполнение задания таймера в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-106">SharePoint handles both the scheduling and the execution of the timer job in this scenario.</span></span> 

<span data-ttu-id="5a0ba-107">В сценарии модели надстройки SharePoint задания таймера создаются и вне SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-107">In the SharePoint Add-in model scenario, timer jobs are created and scheduled outside of SharePoint.</span></span>  <span data-ttu-id="5a0ba-108">SharePoint не отвечает за планирование и выполнение задания таймера в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-108">SharePoint is not responsible for the scheduling or the execution of the timer job in this scenario.</span></span>

<a name="high-level-guidelines"></a><span data-ttu-id="5a0ba-109">Рекомендации по высокого уровня</span><span class="sxs-lookup"><span data-stu-id="5a0ba-109">High-Level Guidelines</span></span>
---------------------

<span data-ttu-id="5a0ba-110">Как правило эскиз мы предлагаем обеспечивает следующие рекомендации высокого уровня для создания задания таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-110">As a rule of a thumb, we would like to provide the following high-level guidelines for creating timer jobs.</span></span>

- <span data-ttu-id="5a0ba-111">Задания таймера должен быть реализован за пределами SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-111">Timer jobs should be implemented outside of SharePoint.</span></span>
- <span data-ttu-id="5a0ba-112">Планирование заданий таймера должен быть реализован за пределами SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-112">Scheduling timer jobs should be implemented outside of SharePoint.</span></span>
- <span data-ttu-id="5a0ba-113">Задания таймера должны проходить проверку подлинности с помощью учетной записи службы или OAuth.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-113">Timer jobs should authenticate via a service account or OAuth.</span></span>

<a name="challenges-creating-timer-jobs"></a><span data-ttu-id="5a0ba-114">Проблемы, связанные с создание заданий таймера</span><span class="sxs-lookup"><span data-stu-id="5a0ba-114">Challenges creating timer jobs</span></span>
------------------------------

<span data-ttu-id="5a0ba-115">Самой сложной задачей, связанные с созданием задания таймера в Office 365 клиенты — того факта, что нельзя развертывание фермы областью действия решений для клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-115">The biggest challenge associated with creating timer jobs in Office 365 tenancies is the fact that you cannot deploy farm scoped solutions to an Office 365 tenancy.</span></span> <span data-ttu-id="5a0ba-116">Без решения уровня фермы нельзя развернуть задания таймера SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-116">Without a farm scoped solution, you cannot deploy a SharePoint timer job.</span></span>

<span data-ttu-id="5a0ba-117">Новый способ создания задания таймера — для построения за пределами SharePoint и обработка планирование за пределами SharePoint также.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-117">The new way to create a timer job is to build it outside of SharePoint and to handle the scheduling outside of SharePoint as well.</span></span> <span data-ttu-id="5a0ba-118">Необходимо учитывайте следующие факторы, связанные с заданиями таймера SharePoint для локальной среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-118">Consider the following factors associated with SharePoint timer jobs for an on-premises SharePoint environment.</span></span>

- <span data-ttu-id="5a0ba-119">SharePoint поставляется с сотни заданий таймера ожидания введите, планировщик SharePoint недостаток справиться с.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-119">SharePoint ships with hundreds of out-of-the-box timer jobs that the SharePoint scheduler struggles to keep up with.</span></span>  
<span data-ttu-id="5a0ba-120">можно сократить объем памяти и мощность процессора ОК-требуется на сервере SharePoint путем перемещения реализация кода в Azure или другой среде.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-120">ok- You can reduce the amount of memory and processor power needed on your SharePoint server by moving the implementation code to Azure or another environment.</span></span>
- <span data-ttu-id="5a0ba-121">Планирование и реализацию код, связанный с задания таймера на другой сервер при перемещении SharePoint server легче масштабируются и с достаточно постоянным как результат.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-121">Moving the scheduling and implementation code associated with timer jobs to another server makes your SharePoint server more scalable and stable as a result.</span></span>

<a name="options-to-schedule-timer-jobs"></a><span data-ttu-id="5a0ba-122">Параметры для планирования заданий таймера</span><span class="sxs-lookup"><span data-stu-id="5a0ba-122">Options to schedule timer jobs</span></span>
----------------------------

<span data-ttu-id="5a0ba-123">У вас есть две возможности для реализации планирования для задания таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-123">You have a couple of options to implement the scheduling for a timer job.</span></span>

- <span data-ttu-id="5a0ba-124">Планировщик Windows</span><span class="sxs-lookup"><span data-stu-id="5a0ba-124">Windows Scheduler</span></span>
    + <span data-ttu-id="5a0ba-125">Службы Windows</span><span class="sxs-lookup"><span data-stu-id="5a0ba-125">Windows Service</span></span>
- <span data-ttu-id="5a0ba-126">Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="5a0ba-126">Azure WebJob</span></span>
    + <span data-ttu-id="5a0ba-127">Azure рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="5a0ba-127">Azure worker process</span></span>

<a name="windows-scheduler"></a><span data-ttu-id="5a0ba-128">Планировщик Windows</span><span class="sxs-lookup"><span data-stu-id="5a0ba-128">Windows Scheduler</span></span>
-----------------
<span data-ttu-id="5a0ba-129">В этом шаблоне планировщик Windows обрабатывает аспекты планирования, связанные с задания таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-129">In this pattern, the Windows Scheduler handles the scheduling aspects associated with a timer job.</span></span>  <span data-ttu-id="5a0ba-130">Код реализации может быть консольное приложение или сценарий PowerShell или другой код, который можно было вызвать планировщик Windows.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-130">Implementation code can be a console application or a PowerShell script or any other code that the Windows Scheduler can invoke.</span></span>

<span data-ttu-id="5a0ba-131">**Параметр Sub обновления Windows** Службы Windows имеет те же характеристики, что планировщик Windows.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-131">**Windows Service Sub Option** A Windows Service has the same characteristics as the Windows Scheduler.</span></span> <span data-ttu-id="5a0ba-132">Не рекомендуется этому шаблону, но это упомянуть, так как она используется часто.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-132">Microsoft does not recommend this pattern but it is worth mentioning because it is commonly used.</span></span>

<span data-ttu-id="5a0ba-133">**При планировщик Windows подходит?**</span><span class="sxs-lookup"><span data-stu-id="5a0ba-133">**When is Windows Scheduler a good fit?**</span></span>

<span data-ttu-id="5a0ba-134">При отсутствии доступа к Azure подписки для планирования заданий таймера с помощью Azure WebJobs использование планировщика Windows является хорошим выбором, поскольку этот параметр может быть реализован на любом компьютере с операционной системой Windows.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-134">When you do not have access to an Azure subscription to schedule timer jobs with Azure WebJobs, Using a Windows Scheduler is a good option because this option may be implemented on any machine with the Windows operating system.</span></span>

- <span data-ttu-id="5a0ba-135">Требуется дополнительное оборудование для запуска планировщик Windows.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-135">Requires additional hardware to run the Windows Scheduler.</span></span>
- <span data-ttu-id="5a0ba-136">Требуется дополнительное оборудование выполнение задания таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-136">Requires additional hardware to run the timer job code.</span></span>

<span data-ttu-id="5a0ba-137">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="5a0ba-137">**Getting Started**</span></span>

<span data-ttu-id="5a0ba-138">Следующие статьи использовать шаблон, планировщик Windows и предоставляют примеры кода для начала.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-138">The following articles use the Windows Scheduler pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="5a0ba-139">Core.SimpleTimerJob (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-139">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
    + <span data-ttu-id="5a0ba-140">Статья начала до конца об этом шаблоне с видеороликами.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-140">End-to-end article about this pattern with accompanying video.</span></span>
- [<span data-ttu-id="5a0ba-141">Core.TimerJobs.Samples (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-141">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="5a0ba-142">Примеры кода великолепную, включающая 10 различных примеров.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-142">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="5a0ba-143">*Примечание: Не все примеры десять кода могут быть применены шаблон планировщик Windows.*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-143">*Note: Not all ten code examples are applicable to the Windows Scheduler pattern.*</span></span>

<a name="azure-webjob"></a><span data-ttu-id="5a0ba-144">Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="5a0ba-144">Azure WebJob</span></span>
------------
<span data-ttu-id="5a0ba-145">В этом шаблоне Azure WebJob обрабатывает аспекты планирования, связанные с задания таймера, а также код реализации.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-145">In this pattern, the Azure WebJob handles the scheduling aspects associated with a timer job and includes the implementation code.</span></span>

- <span data-ttu-id="5a0ba-146">Не требуется дополнительное оборудование для запуска WebJob Azure (код планирования и реализации).</span><span class="sxs-lookup"><span data-stu-id="5a0ba-146">Does not require additional hardware to run the Azure WebJob (scheduling and implementation code).</span></span>
- <span data-ttu-id="5a0ba-147">Выгодно, так как они используют Azure WebJob для планирования и реализации кода, который позволяет легко управлять в одном месте.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-147">Advantageous because it uses the Azure WebJob for scheduling as well as the implementation code, which makes it easy to manage in one location.</span></span>

<span data-ttu-id="5a0ba-148">**Параметр Sub роль Azure работника** Рабочая роль Azure имеет те же характеристики, что WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-148">**Azure Worker Role Sub Option** An Azure Worker Role has the same characteristics as an Azure WebJob.</span></span> <span data-ttu-id="5a0ba-149">Не рекомендуется этому шаблону, но это упомянуть, так как она используется часто.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-149">Microsoft does not recommend this pattern but it is worth mentioning because it is commonly used.</span></span>

<span data-ttu-id="5a0ba-150">**При Azure WebJob подходит?**</span><span class="sxs-lookup"><span data-stu-id="5a0ba-150">**When is Azure WebJob a good fit?**</span></span>

<span data-ttu-id="5a0ba-151">При наличии доступа к Azure подписки для планирования заданий таймера с помощью Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-151">When you have access to an Azure subscription to schedule timer jobs with Azure WebJobs.</span></span>

<span data-ttu-id="5a0ba-152">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="5a0ba-152">**Getting Started**</span></span>

<span data-ttu-id="5a0ba-153">Следующие статьи описывается шаблон Azure WebJob и приводятся примеры кода для начала.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-153">The following articles describe the Azure WebJob pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="5a0ba-154">Начало работы с azure WebJobs («задания таймера») для сайтов Office 365 (O365 PnP статья)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-154">Getting Started with azure WebJobs ("timer jobs") for your Office 365 Sites (O365 PnP Article)</span></span>](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md)
    + <span data-ttu-id="5a0ba-155">Описывается создание WebJob Azure в качестве запланированного задания для Office 365 или локальной среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-155">Describes how to build an Azure WebJob to act as a scheduled job for your Office 365 or on-premises SharePoint environment.</span></span> <span data-ttu-id="5a0ba-156">Включает в себя публикации и отслеживания информации.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-156">Includes publishing and monitoring information.</span></span>
- [<span data-ttu-id="5a0ba-157">Core.SimpleTimerJob (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-157">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="5a0ba-158">Примеры кода великолепную, включающая 10 различных примеров.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-158">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="5a0ba-159">*Примечание: Не все примеры десять кода могут быть применены шаблон Azure WebJob.*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-159">*Note: Not all ten code examples are applicable to the Azure WebJob pattern.*</span></span>

<a name="authentication-options"></a><span data-ttu-id="5a0ba-160">Параметры проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="5a0ba-160">Authentication Options</span></span>
----------------------

<span data-ttu-id="5a0ba-161">В порядке для заданий таймера для взаимодействия с SharePoint они должны проходить проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-161">In order for your timer jobs to interact with SharePoint they must authenticate.</span></span> <span data-ttu-id="5a0ba-162">На данный момент существует два варианта, которые можно использовать для проверки подлинности задания таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-162">Currently, there are two patterns you may use to authenticate timer jobs.</span></span>

- <span data-ttu-id="5a0ba-163">Использование учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="5a0ba-163">Use a service account</span></span>
- <span data-ttu-id="5a0ba-164">Использование OAuth</span><span class="sxs-lookup"><span data-stu-id="5a0ba-164">Use OAuth</span></span>

<a name="use-a-service-account"></a><span data-ttu-id="5a0ba-165">Использование учетной записи службы</span><span class="sxs-lookup"><span data-stu-id="5a0ba-165">Use a service account</span></span>
---------------------
<span data-ttu-id="5a0ba-166">В этом шаблоне можно определить один или несколько учетных записей служб, используемый для проверки подлинности заданий таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-166">In this pattern, you define one or more service accounts used to authenticate timer jobs.</span></span>

- <span data-ttu-id="5a0ba-167">Учетные записи служб, определяются в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-167">Service accounts are defined in SharePoint.</span></span>
    + <span data-ttu-id="5a0ba-168">В клиента Office 365 в зависимости от функциональных возможностей у задания таймера, учетные записи служб может потребоваться лицензии Office 365, назначенные им.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-168">In an Office 365 tenancy, depending what functionality your timer jobs have, the service accounts may need an Office 365 license assigned to them.</span></span>
    + <span data-ttu-id="5a0ba-169">Можно создать учетные записи служб на отдельных основы задание таймера или использование одной учетной записи для всех заданий таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-169">You can create service accounts on a per timer job basis, or use a single account for all timer jobs.</span></span>
    + <span data-ttu-id="5a0ba-170">Создание понятными и описательными имен для учетных записей служб, можно легко отслеживать операций, выполняемых ими.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-170">Create clear and descriptive names for the service accounts so you can easily track the operations they perform.</span></span>
    
    <span data-ttu-id="5a0ba-171">Например: Если ваше задание таймера выполняется изменение элементов списка, в столбце Автор изменений для элементов списка отображаются имя учетной записи службы, связанные с задания таймера.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-171">For example: If your timer job modifies list items, the Modified By column for the list items will display the name of the service account associated with the timer job.</span></span>

- <span data-ttu-id="5a0ba-172">При проверке подлинности с помощью учетных записей служб, вы должны получить имя пользователя и пароль для учетной записи службы.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-172">When authenticating with service accounts, you must retrieve a user name and password for the service account.</span></span>
    + <span data-ttu-id="5a0ba-173">Приведенный ниже фрагмент кода иллюстрирует, используя имя пользователя и пароль для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-173">The code snippet below illustrates using a user name and password to authenticate.</span></span>
    + <span data-ttu-id="5a0ba-174">Будьте внимательны для хранения и извлечения имя пользователя и пароль безопасным образом.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-174">Take care to store and retrieve the user name and password in a secure fashion.</span></span>

    ```
    using (ClientContext context = new ClientContext("https://tenancy.sharepoint.com"))
    {   
        // Use default authentication mode
        context.AuthenticationMode = ClientAuthenticationMode.Default;  
        // Specify the credentials for the account that will execute the request
        context.Credentials = new SharePointOnlineCredentials("User Name", "Password");
    }
    ```

<span data-ttu-id="5a0ba-175">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="5a0ba-175">**Getting Started**</span></span>

<span data-ttu-id="5a0ba-176">В следующих статьях описываются как можно использовать шаблон службы учетной записи проверки подлинности и предоставляются примеры кода для начала.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-176">The following articles describe how to use a service account authentication pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="5a0ba-177">Построение приложений SharePoint как задания таймера (блог MSDN)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-177">Building a SharePoint App as a Timer Job (MSDN Blog)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx)
    + <span data-ttu-id="5a0ba-178">Статья начала до конца по этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-178">End-to-end article about this pattern.</span></span>
- [<span data-ttu-id="5a0ba-179">Core.SimpleTimerJob (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-179">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
    + <span data-ttu-id="5a0ba-180">Статья начала до конца об этом шаблоне с видеороликами.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-180">End-to-end article about this pattern with accompanying video.</span></span>
- [<span data-ttu-id="5a0ba-181">Core.TimerJobs.Samples (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-181">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="5a0ba-182">Примеры кода великолепную, включающая 10 различных примеров.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-182">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="5a0ba-183">*Примечание: Не все примеры десять кода могут быть применены к шаблону проверки подлинности учетной записи службы.*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-183">*Note: Not all ten code examples are applicable to the service account authentication pattern.*</span></span>

<a name="use-oauth"></a><span data-ttu-id="5a0ba-184">Использование OAuth</span><span class="sxs-lookup"><span data-stu-id="5a0ba-184">Use OAuth</span></span>
-----------
<span data-ttu-id="5a0ba-185">В этом шаблоне определение приложения в SharePoint или Azure Active Directory и использовании маркеры проверки подлинности, связанных с приложением для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-185">In this pattern, you define an application in SharePoint or Azure Active Directory and use the authentication tokens associated with the application to authenticate.</span></span>

- <span data-ttu-id="5a0ba-186">При использовании приложения SharePoint для проверки подлинности создания участника приложения и назначить ему разрешения.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-186">When using a SharePoint application to authenticate you create an app principal and assign permissions to it.</span></span>
    + <span data-ttu-id="5a0ba-187">В этом шаблоне задания таймера может реализовать с помощью Provider-hosted SharePoint Add-in или консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-187">In this pattern, timer jobs may be implemented via a Provider-hosted SharePoint Add-in or a console application.</span></span>
    + <span data-ttu-id="5a0ba-188">Чтобы зарегистрировать субъект приложения для Provider-hosted SharePoint надстройки или консольное приложение, используйте страницу AppRegNew в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-188">To register an app principal for the Provider-hosted SharePoint Add-in or console application, use the AppRegNew page in SharePoint.</span></span>
    
    <span data-ttu-id="5a0ba-189">На этой странице осуществляется на следующий URL-адрес http://<tenancy>/<site>/_layouts/AppRegNew.aspx</span><span class="sxs-lookup"><span data-stu-id="5a0ba-189">This page is accessed at the following URL  http://<tenancy>/<site>/_layouts/AppRegNew.aspx</span></span>

    + <span data-ttu-id="5a0ba-190">Чтобы предоставить разрешения на субъекта приложения, используйте страницу AppInv в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-190">To grant permissions to an app principal, use the AppInv page in SharePoint.</span></span>
    
    <span data-ttu-id="5a0ba-191">На этой странице осуществляется на следующий URL-адрес http://<tenancy>/<site>/_layouts/AppInv.aspx</span><span class="sxs-lookup"><span data-stu-id="5a0ba-191">This page is accessed at the following URL  http://<tenancy>/<site>/_layouts/AppInv.aspx</span></span>

- <span data-ttu-id="5a0ba-192">Задания таймера использовать приложение только разрешения, так как у них нет интерактивного пользователя, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-192">Timer jobs use App Only permissions because they do not have an interactive user associated with them.</span></span> 
    + <span data-ttu-id="5a0ba-193">Приведенный ниже фрагмент кода иллюстрирует получение маркер доступа и с помощью приложения только разрешения проходить проверку подлинности в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-193">The code snippet below illustrates obtaining an access token and using App Only permissions to authenticate to SharePoint.</span></span>

    ```
    string accessToken = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUri.Authority, realm).AccessToken;
    
    using(var clientContext = TokenHelper.GetClientContextWithAccessToken(siteUri.ToString(),accessToken))
    {
        //Implement timer job code
    }
    ```

- <span data-ttu-id="5a0ba-194">При использовании приложения Azure Active Directory для проверки подлинности, можно создать приложение Azure Active Directory в портала управления Azure и назначить ему разрешения.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-194">When using an Azure Active Directory application to authenticate, you create an Azure Active Directory application in the Azure Management Portal and assign permissions to it.</span></span>
    + <span data-ttu-id="5a0ba-195">В этом шаблоне задания таймера может реализовать с помощью Provider-hosted SharePoint Add-in или консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-195">In this pattern, timer jobs may be implemented via a Provider-hosted SharePoint Add-in or a console application.</span></span>
    + <span data-ttu-id="5a0ba-196">В этом шаблоне взаимодействия с библиотеке проверки подлинности Active Directory или Microsoft Graph API для получения маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-196">In this pattern, you interact with the Active Directory Authentication Library or the Microsoft Graph API to retrieve an access token.</span></span>
    + <span data-ttu-id="5a0ba-197">Маркер доступа используется для проверки подлинности в SharePoint (и, возможно, другие службы Office 365 в клиенте Office 365).</span><span class="sxs-lookup"><span data-stu-id="5a0ba-197">The access token is used to authenticate to SharePoint (and possibly other Office 365 services in an Office 365 tenancy).</span></span>

<span data-ttu-id="5a0ba-198">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="5a0ba-198">**Getting Started**</span></span>

<span data-ttu-id="5a0ba-199">Следующие статьи описывается шаблон проверки подлинности OAUth и приводятся примеры кода для начала.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-199">The following articles describe the OAUth authentication pattern and provide code samples to get you started.</span></span>

- [<span data-ttu-id="5a0ba-200">Построение приложений SharePoint как задания таймера (блог MSDN)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-200">Building a SharePoint App as a Timer Job (MSDN Blog)</span></span>](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx)
    + <span data-ttu-id="5a0ba-201">Статья начала до конца по этому шаблону.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-201">End-to-end article about this pattern.</span></span>
- [<span data-ttu-id="5a0ba-202">Core.TimerJobs.Samples (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-202">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
    + <span data-ttu-id="5a0ba-203">Примеры кода великолепную, включающая 10 различных примеров.</span><span class="sxs-lookup"><span data-stu-id="5a0ba-203">Excellent code samples encompassing 10 different examples.</span></span> <span data-ttu-id="5a0ba-204">*Примечание: Не все примеры десять кода могут быть применены к шаблону проверки подлинности OAUth.*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-204">*Note: Not all ten code examples are applicable to the OAUth authentication pattern.*</span></span>

<a name="related-links"></a><span data-ttu-id="5a0ba-205">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="5a0ba-205">Related links</span></span>
=============
- [<span data-ttu-id="5a0ba-206">Ресурсы Azure WebJob (Azure документации)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-206">Azure WebJob resources (Azure Documentation)</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
- [<span data-ttu-id="5a0ba-207">Развертывание WebJobs, с помощью Visual Studio (Azure документации)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-207">Deploy WebJobs using Visual Studio (Azure Documentation)</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
- <span data-ttu-id="5a0ba-208">Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")</span><span class="sxs-lookup"><span data-stu-id="5a0ba-208">Guidance articles at [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Guidance Articles")</span></span>
- <span data-ttu-id="5a0ba-209">Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")</span><span class="sxs-lookup"><span data-stu-id="5a0ba-209">References in MSDN at [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "References in MSDN")</span></span>
- <span data-ttu-id="5a0ba-210">Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")</span><span class="sxs-lookup"><span data-stu-id="5a0ba-210">Videos at [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "Videos")</span></span>

<a name="related-pnp-samples"></a><span data-ttu-id="5a0ba-211">Примеры связанных с ними PnP</span><span class="sxs-lookup"><span data-stu-id="5a0ba-211">Related PnP samples</span></span>
===================

- [<span data-ttu-id="5a0ba-212">Core.SimpleTimerJob (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-212">Core.SimpleTimerJob (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.SimpleTimerJob)
- [<span data-ttu-id="5a0ba-213">Core.TimerJobs.Samples (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-213">Core.TimerJobs.Samples (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Solutions/Core.TimerJobs.Samples)
- [<span data-ttu-id="5a0ba-214">Provisioning.Services.SiteManager (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-214">Provisioning.Services.SiteManager (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Services.SiteManager)
- [<span data-ttu-id="5a0ba-215">Provisioning.SiteCollectionCreation (O365 PnP образец)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-215">Provisioning.SiteCollectionCreation (O365 PnP Sample)</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.SiteCollectionCreation)
- <span data-ttu-id="5a0ba-216">Примеры и содержимое в https://github.com/SharePoint/PnP</span><span class="sxs-lookup"><span data-stu-id="5a0ba-216">Samples and content at https://github.com/SharePoint/PnP</span></span>

<a name="applies-to"></a><span data-ttu-id="5a0ba-217">Применимо к</span><span class="sxs-lookup"><span data-stu-id="5a0ba-217">Applies to</span></span>
==========
- <span data-ttu-id="5a0ba-218">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="5a0ba-218">Office 365 Multi Tenant (MT)</span></span>
- <span data-ttu-id="5a0ba-219">Office 365 выделенных (D) *частично*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-219">Office 365 Dedicated (D) *partly*</span></span>
- <span data-ttu-id="5a0ba-220">SharePoint 2013 в локальной — *частично*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-220">SharePoint 2013 on-premises – *partly*</span></span>

<span data-ttu-id="5a0ba-221">*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*</span><span class="sxs-lookup"><span data-stu-id="5a0ba-221">*Patterns for dedicated and on-premises are identical with SharePoint Add-in model techniques, but there are differences on the possible technologies that can be used.*</span></span>
