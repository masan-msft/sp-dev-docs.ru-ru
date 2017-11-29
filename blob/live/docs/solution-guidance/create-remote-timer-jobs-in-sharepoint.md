---
title: "Создание задания таймера удаленные в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 12f4abd507328afd19da562c8dbb569118bc91a9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="create-remote-timer-jobs-in-sharepoint"></a><span data-ttu-id="c4b05-102">Создание задания таймера удаленные в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4b05-102">Create remote timer jobs in SharePoint</span></span>

<span data-ttu-id="c4b05-103">Создание задания таймера удаленного в SharePoint для выполнения задач фон для управления и управляющие среды.</span><span class="sxs-lookup"><span data-stu-id="c4b05-103">Create remote timer jobs in SharePoint to perform background tasks to manage or govern your environment.</span></span>

<span data-ttu-id="c4b05-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="c4b05-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="c4b05-105">Создание задания таймера удаленного управления SharePoint, мониторинга и выполняют действия с данными SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c4b05-105">Create remote timer jobs to manage SharePoint by monitoring and taking action on SharePoint data.</span></span> <span data-ttu-id="c4b05-106">Не выполняйте задания таймера удаленного на SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="c4b05-106">Remote timer jobs do not run on your SharePoint server.</span></span> <span data-ttu-id="c4b05-107">Вместо этого задания таймера удаленного, назначенные задания, которые запускаются на другой сервер.</span><span class="sxs-lookup"><span data-stu-id="c4b05-107">Instead remote timer jobs are scheduled tasks that run on another server.</span></span> <span data-ttu-id="c4b05-108">Примеры использования задания таймера:</span><span class="sxs-lookup"><span data-stu-id="c4b05-108">Examples of how timer jobs are used include:</span></span>

- <span data-ttu-id="c4b05-109">Для выполнения задач управления, например отображения сообщения на сайте, определенным условиям не выполняются или применение политики хранения.</span><span class="sxs-lookup"><span data-stu-id="c4b05-109">Performing governance tasks, such as displaying a message on the site when certain criteria are not met, or enforcing retention policies.</span></span>
    
- <span data-ttu-id="c4b05-110">Выполнение запланированного процессов, которые являются процессор.</span><span class="sxs-lookup"><span data-stu-id="c4b05-110">Running scheduled processes that are processor intensive.</span></span>

## <a name="before-you-begin-to-create-a-remote-timer-job"></a><span data-ttu-id="c4b05-111">Прежде чем приступить к созданию задания таймера удаленного</span><span class="sxs-lookup"><span data-stu-id="c4b05-111">Before you begin to create a remote timer job</span></span>

<span data-ttu-id="c4b05-112">Чтобы начать работу, загрузите пример надстройки [Core.TimerJobs.Samples](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="c4b05-112">To get started, download the [Core.TimerJobs.Samples ](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="c4b05-113">Чтобы начать использование Core.TimerJobs.Samples решения, необходимо выбрать запускаемый проект, например проект SimpleJob, откройте контекстное меню (щелкнув правой кнопкой мыши) **Core.TimerJobs.Samples.SimpleJob**, а затем выбрать **задаются в виде Запускаемый проект**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-113">To start using the Core.TimerJobs.Samples solution, you need to select a startup project, for example the SimpleJob project, by opening the shortcut menu for (right-clicking) the  **Core.TimerJobs.Samples.SimpleJob**, and then choosing  **Set as StartUp Project**.</span></span>

<span data-ttu-id="c4b05-114">**Примечание:**  При создании нового проекта в Visual Studio для создания вашего нового задания таймера удаленного, добавьте в проект пакетов NuGet **OfficeDevPnP.Core** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-114">**Note:**  When you create a new project in Visual Studio, to start building your new remote timer job, add the  **OfficeDevPnP.Core** NuGet package to your project.</span></span> <span data-ttu-id="c4b05-115">В Visual Studio выберите в меню **Сервис** > **Диспетчер пакетов NuGet** > **Управление пакетами NuGet для решения**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-115">In Visual Studio, choose **TOOLS** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span>

## <a name="schedule-your-remote-timer-job"></a><span data-ttu-id="c4b05-116">Задания таймера удаленного</span><span class="sxs-lookup"><span data-stu-id="c4b05-116">Schedule your remote timer job</span></span>

<span data-ttu-id="c4b05-117">Задания таймера можно запланировать один раз выполнить или может быть повторяющегося задания.</span><span class="sxs-lookup"><span data-stu-id="c4b05-117">A timer job can be scheduled to run once or can be a recurring job.</span></span> <span data-ttu-id="c4b05-118">Для задания таймера удаленного в рабочей среде, требуется для компиляции кода в .exe-файл, а затем запустите файл .exe, с помощью планировщиком заданий Windows или WebJob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b05-118">To schedule your remote timer job in your production environment, you need to compile your code into an .exe file, and then run the .exe file using Windows Task Scheduler or an Microsoft Azure WebJob.</span></span> <span data-ttu-id="c4b05-119">Дополнительные сведения по [развертыванию параметры задания таймера](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#timer-job-deployment-options).</span><span class="sxs-lookup"><span data-stu-id="c4b05-119">You can learn more at [Timer job deployment options](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#timer-job-deployment-options).</span></span>

## <a name="use-the-coretimerjobssamplessimplejob-add-in"></a><span data-ttu-id="c4b05-120">Использовать надстройки Core.TimerJobs.Samples.SimpleJob</span><span class="sxs-lookup"><span data-stu-id="c4b05-120">Use the Core.TimerJobs.Samples.SimpleJob add-in</span></span>

<span data-ttu-id="c4b05-121">В Core.TimerJobs.Samples.SimpleJob, **Main** в файле Program.cs необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c4b05-121">In Core.TimerJobs.Samples.SimpleJob,  **Main** in Program.cs performs the following steps:</span></span>

1. <span data-ttu-id="c4b05-122">Создает объект SimpleJob, который наследуется из базового класса [OfficeDevPnP.Core.Framework.TimerJobs.TimerJob](https://github.com/SharePoint/PnP/blob/dev/OfficeDevPnP.Core/OfficeDevPnP.Core/Framework/TimerJobs/TimerJob.cs) .</span><span class="sxs-lookup"><span data-stu-id="c4b05-122">Creates a SimpleJob object, which inherits from the [OfficeDevPnP.Core.Framework.TimerJobs.TimerJob](https://github.com/SharePoint/PnP/blob/dev/OfficeDevPnP.Core/OfficeDevPnP.Core/Framework/TimerJobs/TimerJob.cs) base class.</span></span>
    
2. <span data-ttu-id="c4b05-123">Задает учетные данные пользователя Office 365 для использования при запуске задания таймера с помощью **TimerJob.UseOffice365Authentication**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-123">Sets the Office 365 user credentials to use when running the timer job using  **TimerJob.UseOffice365Authentication**.</span></span> <span data-ttu-id="c4b05-124">Учетные данные пользователя необходимы соответствующие права доступа для семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="c4b05-124">The user credentials must have appropriate access to the site collections.</span></span> <span data-ttu-id="c4b05-125">Дополнительные сведения по [проверки подлинности](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="c4b05-125">You can learn more at [Authentication](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#authentication).</span></span>
    
3. <span data-ttu-id="c4b05-126">Добавление сайтов, что задание таймера на использование **TimerJob.AddSite**следует выполнить задачи.</span><span class="sxs-lookup"><span data-stu-id="c4b05-126">Adds sites that the timer job should perform tasks on using  **TimerJob.AddSite**.</span></span> <span data-ttu-id="c4b05-127">При необходимости можно Повторите инструкцию **TimerJob.AddSite** , чтобы добавить несколько узлов или добавление всех сайтов в разделе определенного URL-адреса с помощью подстановочный знак *. Например, http://contoso.sharepoint.com/sites/* задание таймера, которое будет выполняться на всех сайтах в разделе управляемый путь **sites** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-127">Optionally, you can repeat the **TimerJob.AddSite** statement to add more than one site, or add all sites under a particular URL using the wildcard character *. For example, http://contoso.sharepoint.com/sites/* will run the timer job on all sites under the **sites** managed path.</span></span>
    
4. <span data-ttu-id="c4b05-128">Выводит сведения о задания таймера и запускается задание таймера с помощью **PrintJobSettingsAndRunJob**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-128">Prints timer job information and runs the timer job using  **PrintJobSettingsAndRunJob**.</span></span>

<span data-ttu-id="c4b05-129">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="c4b05-129">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
 static void Main(string[] args)
        {
            SimpleJob simpleJob = new SimpleJob();
            
            // The user credentials must have access to the site collections you supply.
            simpleJob.UseOffice365Authentication(User, Password);

            // Use the following code if you are using SharePoint Server 2013 on-premises. 
            //simpleJob.UseNetworkCredentialsAuthentication(User, Password, Domain);
            
            // Add one or more sites that the timer job should work with.
            simpleJob.AddSite("https://contoso.sharepoint.com/sites/dev");
            
            // Prints timer job information and then calls Run().
            PrintJobSettingsAndRunJob(simpleJob);
        }
```

<span data-ttu-id="c4b05-130">При создании объекта **simpleJob** , конструктор **SimpleJob** :</span><span class="sxs-lookup"><span data-stu-id="c4b05-130">When the  **simpleJob** object is instantiated, the **SimpleJob** constructor:</span></span>

1. <span data-ttu-id="c4b05-131">Вызывает конструктор базового класса задания таймера.</span><span class="sxs-lookup"><span data-stu-id="c4b05-131">Calls the TimerJob base class constructor.</span></span> 
    
2. <span data-ttu-id="c4b05-132">Назначает **SimpleJob_TimerJobRun** обработчика событий для обработки событий **TimerJobRun** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-132">Assigns the  **SimpleJob_TimerJobRun** event handler to handle the **TimerJobRun** events.</span></span> <span data-ttu-id="c4b05-133">**SimpleJob_TimerJobRun** запускается при вызове **TimerJob.Run**, которое описывается более подробно далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c4b05-133">**SimpleJob_TimerJobRun** runs when a call is made to **TimerJob.Run**, which is described in more detail later in this article.</span></span>

```C#
public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }
```

<span data-ttu-id="c4b05-134">При выполнении **PrintJobSettingsAndRunJob** выходные данные задания таймера, записывается в окне консоли, а затем, называется **TimerJob.Run** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-134">When  **PrintJobSettingsAndRunJob** runs, output from the TimerJob is written to the console window, and then **TimerJob.Run** is called.</span></span>

```C#
 private static void PrintJobSettingsAndRunJob(TimerJob job)
        {
            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("************************************************");
            Console.WriteLine("Job name: {0}", job.Name);
            Console.WriteLine("Job version: {0}", job.Version);
            Console.WriteLine("Use threading: {0}", job.UseThreading);
            Console.WriteLine("Maximum threads: {0}", job.MaximumThreads);
            Console.WriteLine("Expand sub sites: {0}", job.ExpandSubSites);
            Console.WriteLine("Authentication type: {0}", job.AuthenticationType);
            Console.WriteLine("Manage state: {0}", job.ManageState);
            Console.WriteLine("SharePoint version: {0}", job.SharePointVersion);
            Console.WriteLine("************************************************");
            Console.ForegroundColor = ConsoleColor.Gray;

            // Run job.
            job.Run();
        }
```

<span data-ttu-id="c4b05-135">**TimerJob.Run** вызывает события **TimerJobRun** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-135">**TimerJob.Run** raises **TimerJobRun** events.</span></span> <span data-ttu-id="c4b05-136">**TimerJob.Run** вызывает **SimpleJob_TimerJobRun** SimpleJob.cs, которое было задано как обработчик событий для обработки событий **TimerJobRun** в конструкторе **SimpleJob**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-136">**TimerJob.Run** calls **SimpleJob_TimerJobRun** in SimpleJob.cs, which you set as the event handler to handle **TimerJobRun** events in the constructor of **SimpleJob**.</span></span> <span data-ttu-id="c4b05-137">В **SimpleJob_TimerJobRun**можно добавить пользовательский код, который будет вашего задания таймера для выполнения при запуске задания таймера.</span><span class="sxs-lookup"><span data-stu-id="c4b05-137">In **SimpleJob_TimerJobRun**, you can add your custom code that you want your timer job to perform when the timer job runs.</span></span> <span data-ttu-id="c4b05-138">**SimpleJob_TimerJobRun** запускает свой код на веб-сайтах, добавленную с помощью **TimerJob.AddSite** в файле Program.cs.</span><span class="sxs-lookup"><span data-stu-id="c4b05-138">**SimpleJob_TimerJobRun** runs your custom code on the sites you added using **TimerJob.AddSite** in Program.cs.</span></span> <span data-ttu-id="c4b05-139">В этом примере кода **SimpleJob_TimerJobRun** используется **ClientContext** из **задания таймера** для записи заголовок сайта в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="c4b05-139">In this code sample, **SimpleJob_TimerJobRun** uses the **ClientContext** from the **TimerJob** to write the title of the site to the console window.</span></span> <span data-ttu-id="c4b05-140">Если несколько сайтов были добавлены с помощью **TimerJob.AddSite** , **SimpleJob_TimerJobRun** вызывается для каждого сайта.</span><span class="sxs-lookup"><span data-stu-id="c4b05-140">If multiple sites were added using **TimerJob.AddSite** , **SimpleJob_TimerJobRun** is called for each site.</span></span>

```C#
 void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
```

## <a name="example-content-type-retention-enforcement-timer-job"></a><span data-ttu-id="c4b05-141">Пример: Задание таймера принудительное применение хранения типа контента</span><span class="sxs-lookup"><span data-stu-id="c4b05-141">Example: Content type retention enforcement timer job</span></span>

<span data-ttu-id="c4b05-142">Проект Core.TimerJobs.Samples.ContentTypeRetentionEnforcementJob показано, как можно использовать задания таймера SharePoint для применения политики хранения для типов контента.</span><span class="sxs-lookup"><span data-stu-id="c4b05-142">The Core.TimerJobs.Samples.ContentTypeRetentionEnforcementJob project shows how you can use SharePoint timer jobs to enforce retention policies on content types.</span></span> <span data-ttu-id="c4b05-143">С помощью элемента **ContentTypeRetentionPolicyPeriod** в файле app.config, укажите:</span><span class="sxs-lookup"><span data-stu-id="c4b05-143">Using the  **ContentTypeRetentionPolicyPeriod** element in app.config, specify:</span></span>

-  <span data-ttu-id="c4b05-144">**ключ**, который является идентификатор типа контента, которое применяется период хранения для типа контента.</span><span class="sxs-lookup"><span data-stu-id="c4b05-144">**key**, which is the content type ID of the content type that the retention period applies to.</span></span>
    
-  <span data-ttu-id="c4b05-145">**значение**, которое срок хранения в днях.</span><span class="sxs-lookup"><span data-stu-id="c4b05-145">**value**, which is the retention period in days.</span></span> <span data-ttu-id="c4b05-146">Период хранения будет применяться ко всем элементам списка, созданные с помощью типа контента, указанного в **ключ**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-146">The retention period will be applied to all list items created using the content type specified in **key**.</span></span>

```XML
<ContentTypeRetentionPolicyPeriod>
    <!-- Key is the content type ID, and value is the retention period in days -->
    <!-- Specifies an audio content type should be kept for 183 days -->
    <add key="0x0101009148F5A04DDD49cbA7127AADA5FB792B006973ACD696DC4858A76371B2FB2F439A" value="183" />
    <!-- Specifies a document content type should be kept for 365 days -->   
    <add key="0x0101" value="365" />
</ContentTypeRetentionPolicyPeriod>
```

<span data-ttu-id="c4b05-147">**ContentTypeRetentionEnforcementJob_TimerJobRun** задано как обработчик событий для события **TimerJobRun** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-147">**ContentTypeRetentionEnforcementJob_TimerJobRun** is set as the event handler for the **TimerJobRun** event.</span></span> <span data-ttu-id="c4b05-148">При вызове **TimerJob.Run** в файле Program.cs на каждом сайте, который был добавлен с помощью **TimerJob.AddSite** в файле Program.cs **ContentTypeRetentionEnforcementJob_TimerJobRun** необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c4b05-148">When **TimerJob.Run** is called in Program.cs, **ContentTypeRetentionEnforcementJob_TimerJobRun** performs the following steps on each site that was added using **TimerJob.AddSite** in Program.cs:</span></span>


1. <span data-ttu-id="c4b05-149">Получает все библиотеки документов на сайте.</span><span class="sxs-lookup"><span data-stu-id="c4b05-149">Gets all document libraries on the site.</span></span>
    
2. <span data-ttu-id="c4b05-150">Для каждого документа библиотеки на сайте считывает сведения о конфигурации, указанное в **ContentTypeRetentionPolicyPeriod** в файле app.config. Для каждого типа контента идентификатор и хранения периода пары, считанный из app.config называется **ApplyRetentionPolicy** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-150">For each document library on the site, reads the configuration information specified in  **ContentTypeRetentionPolicyPeriod** in app.config. For each content type ID and retention period pair that was read from app.config, **ApplyRetentionPolicy** is called.</span></span>

```C#
 void ContentTypeRetentionEnforcementJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            try
            {
                Log.Info("ContentTypeRetentionEnforcementJob", "Scanning web {0}", e.Url);

                // Get all document libraries. Lists are excluded.
                var documentLibraries = GetAllDocumentLibrariesInWeb(e.WebClientContext, e.WebClientContext.Web);

                // Iterate through all document libraries.
                foreach (var documentLibrary in documentLibraries)
                {
                    Log.Info("ContentTypeRetentionEnforcementJob", "Scanning library {0}", documentLibrary.Title);

                    // Iterate through configured content type retention policies specified in app.config.
                    foreach (var contentTypeName in configContentTypeRetentionPolicyPeriods.Keys)
                    {
                        var retentionPeriods = configContentTypeRetentionPolicyPeriods.GetValues(contentTypeName as string);
                        if (retentionPeriods != null)
                        {
                            var retentionPeriod = int.Parse(retentionPeriods[0]);
                            ApplyRetentionPolicy(e.WebClientContext, documentLibrary, contentTypeName, retentionPeriod);
                        }
                    }
                }
            }
            catch(Exception ex)
            {
                Log.Error("ContentTypeRetentionEnforcementJob", "Exception processing site {0}. Exception is {1}", e.Url, ex.Message);
            }
        }
```

<span data-ttu-id="c4b05-151">**ApplyRetentionPolicy** принудительного применения политики хранения настраиваемых действий с:</span><span class="sxs-lookup"><span data-stu-id="c4b05-151">**ApplyRetentionPolicy** enforces your custom retention policy actions by:</span></span>

1. <span data-ttu-id="c4b05-152">Расчет **validationDate**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-152">Calculating  **validationDate**.</span></span> <span data-ttu-id="c4b05-153">Метод **ApplyRetentionPolicy** обеспечивает выполнение действия политики хранения на документы, измененные до **validationDate**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-153">The **ApplyRetentionPolicy** method enforces retention policy actions on documents modified before **validationDate**.</span></span> <span data-ttu-id="c4b05-154">Затем **validationDate** формате CAML даты и назначается **camlDate**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-154">Then **validationDate** is formatted as a CAML date and is assigned to **camlDate**.</span></span>
    
2. <span data-ttu-id="c4b05-155">Выполнение запроса CAML для фильтрации документов в библиотеку документов на основе кода типа контента, который был задан в файле app.config и где дата **Автор изменений** меньше, чем **camlDate**.</span><span class="sxs-lookup"><span data-stu-id="c4b05-155">Running a CAML query to filter documents in the document library based on the content type ID, which was specified in app.config, and where the  **Modified By** date is less than **camlDate**.</span></span>
    
3. <span data-ttu-id="c4b05-156">Для каждого элемента списка применение хранения настраиваемых действий, выполняемых над документами, с использованием пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="c4b05-156">For each list item, applying custom retention actions to perform on the documents using custom code.</span></span>

```C#
private void ApplyRetentionPolicy(ClientContext clientContext, List documentLibrary, object contentTypeId, int retentionPeriodDays)
        {
            // Calculate validation date. You need to enforce the retention policy on any document modified before validation date.
            var validationDate = DateTime.Now.AddDays(-retentionPeriodDays);
            var camlDate = validationDate.ToString("yyyy-MM-ddTHH:mm:ssZ");

            // Get old documents in the library that match the content type.
            if (documentLibrary.ItemCount > 0)
            {
                var camlQuery = new CamlQuery();
                
                camlQuery.ViewXml = String.Format(
                    @"<View>
                        <Query>
                            <Where><And>
                                <BeginsWith><FieldRef Name='ContentTypeId'/><Value Type='ContentTypeId'>{0}</Value></BeginsWith>
                                <Lt><FieldRef Name='Modified' /><Value Type='DateTime'>{1}</Value></Lt>
                            </And></Where>
                        </Query>
                    </View>", contentTypeId, camlDate);

                var listItems = documentLibrary.GetItems(camlQuery);
                clientContext.Load(listItems,
                    items => items.Include(
                        item => item.Id,
                        item => item.DisplayName,
                        item => item.ContentType));

                clientContext.ExecuteQueryRetry(); 

                foreach (var listItem in listItems)
                {
                    Log.Info("ContentTypeRetentionEnforcementJob", "Document '{0}' has been modified earlier than {1}. Retention policy will be applied.", listItem.DisplayName, validationDate);
                    Console.WriteLine("Document '{0}' has been modified earlier than {1}. Retention policy will be applied.", listItem.DisplayName, validationDate);
                    
                    // Apply your custom retention actions here. For example, archiving documents, or starting a disposition workflow.
                }
            }
        }
```

## <a name="example-governance-timer-job"></a><span data-ttu-id="c4b05-157">Пример: Задание таймера управления</span><span class="sxs-lookup"><span data-stu-id="c4b05-157">Example: Governance timer job</span></span>

<span data-ttu-id="c4b05-158">Проект Core.TimerJobs.Samples.GovernanceJob убедитесь, что назначается два администраторам семейств веб-сайтов с помощью заданий таймера и если это не так, отобразит уведомление на сайте.</span><span class="sxs-lookup"><span data-stu-id="c4b05-158">The Core.TimerJobs.Samples.GovernanceJob project uses timer jobs to ensure two administrators are assigned to your site collections, and if not, displays a notification message on the site.</span></span>

<span data-ttu-id="c4b05-159">**SiteGovernanceJob_TimerJobRun** задано как обработчик событий для события **TimerJobRun** .</span><span class="sxs-lookup"><span data-stu-id="c4b05-159">**SiteGovernanceJob_TimerJobRun** is set as the event handler for the **TimerJobRun** event.</span></span> <span data-ttu-id="c4b05-160">При вызове **TimerJob.Run** в файле Program.cs на каждого семейства веб-сайтов, который был добавлен с помощью **TimerJob.AddSite** в файле Program.cs **SiteGovernanceJob_TimerJobRun** необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c4b05-160">When **TimerJob.Run** is called in Program.cs, **SiteGovernanceJob_TimerJobRun** performs the following steps on each site collection that was added using **TimerJob.AddSite** in Program.cs:</span></span>

1. <span data-ttu-id="c4b05-161">Получает число администраторов, назначенных для семейства сайтов, с помощью метода расширения [GetAdministrators](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/SecurityExtensions.cs) , которая является частью [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span><span class="sxs-lookup"><span data-stu-id="c4b05-161">Gets the number of administrators assigned to the site collection using the extension method [GetAdministrators](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/SecurityExtensions.cs) which is part of [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span></span>
    
2. <span data-ttu-id="c4b05-162">Загружает файл JavaScript с помощью [UploadFile](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/FileFolderExtensions.cs), которая является частью [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core)списка SiteAssets или Библиотека стилей.</span><span class="sxs-lookup"><span data-stu-id="c4b05-162">Uploads the JavaScript file to the SiteAssets or Style Library list using [UploadFile](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/FileFolderExtensions.cs), which is part of [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).</span></span> 
    
3. <span data-ttu-id="c4b05-163">Если сайт должен меньше, чем два администратора, [AddJSLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs) добавляет сообщение уведомления на сайт с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c4b05-163">If the site has less than two administrators, [AddJSLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs) adds a notification message to a site using JavaScript.</span></span> <span data-ttu-id="c4b05-164">Дополнительные сведения по [Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span><span class="sxs-lookup"><span data-stu-id="c4b05-164">You can learn more at [Customize your SharePoint site UI by using JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).</span></span>
    
4. <span data-ttu-id="c4b05-165">Если сайт имеет два или более администраторов, сообщение уведомления удаляется при помощи [DeleteJsLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="c4b05-165">If the site has two or more administrators, the notification message is removed using [DeleteJsLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs).</span></span>

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
        {
            try
            {
                string library = "";

                // Get the number of administrators.
                var admins = e.WebClientContext.Web.GetAdministrators();

                Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

                // Get a reference to the list.
                library = "SiteAssets";
                List list = e.WebClientContext.Web.GetListByUrl(library);

                if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
                {
                    if (list == null)
                    {
                        // Get a reference to the list.
                        library = "Style%20Library";
                        list = e.WebClientContext.Web.GetListByUrl(library);
                    }

                    if (list != null)
                    {
                        // Upload js file to list.
                        list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                        e.SetProperty("ScriptFileVersion", "1.0");
                    }
                }

                if (admins.Count < 2)
                {
                    // Show notification message because you need at least two site collection administrators.
                    e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
                    Console.WriteLine("Site {0} marked as incompliant!", e.Url);
                    e.SetProperty("SiteCompliant", "false");
                }
                else
                {
                    // Remove the notification message because two administrators are assigned.
                    e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
                    Console.WriteLine("Site {0} is compliant", e.Url);
                    e.SetProperty("SiteCompliant", "true");
                }

                e.CurrentRunSuccessful = true;
                e.DeleteProperty("LastError");
            }
            catch(Exception ex)
            {
                Log.Error("SiteGovernanceJob", "Error while processing site {0}. Error = {1}", e.Url, ex.Message);
                e.CurrentRunSuccessful = false;
                e.SetProperty("LastError", ex.Message);
            }
        }
```

## <a name="additional-resources"></a><span data-ttu-id="c4b05-166">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c4b05-166">Additional resources</span></span>
<span data-ttu-id="c4b05-167"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c4b05-167"></span></span>

- [<span data-ttu-id="c4b05-168">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="c4b05-168">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [<span data-ttu-id="c4b05-169">Руководство по с помощью Framework задания таймера</span><span class="sxs-lookup"><span data-stu-id="c4b05-169">Guide to using the Timer Job Framework</span></span>](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md)
    
- [<span data-ttu-id="c4b05-170">Framework задания таймера</span><span class="sxs-lookup"><span data-stu-id="c4b05-170">Timer job framework</span></span>](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples)
