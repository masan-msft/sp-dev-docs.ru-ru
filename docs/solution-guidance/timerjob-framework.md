---
title: "Платформа задания таймера #"
ms.date: 11/03/2017
ms.openlocfilehash: d6db7e8e9eb50006d8abb6d02ccfd9a0d12b736c
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="the-timer-job-framework"></a><span data-ttu-id="0d453-102">Платформа задания таймера</span><span class="sxs-lookup"><span data-stu-id="0d453-102">The Timer Job Framework</span></span> #

<span data-ttu-id="0d453-103">PnP Framework задания таймера представляют собой набор классов, предназначенных для упрощения создания фоновых процессах, которые используются для сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0d453-103">The PnP Timer Job Framework is a set of classes designed to ease the creation of background processes that operate against SharePoint sites.</span></span> <span data-ttu-id="0d453-104">Платформа задания таймера похож на код полного доверия локальной задания таймера (`SPJobDefinition`).</span><span class="sxs-lookup"><span data-stu-id="0d453-104">The Timer Job Framework is similar to on-premises full trust code Timer Jobs (`SPJobDefinition`).</span></span> <span data-ttu-id="0d453-105">С основным различием между Framework задания таймера и кода полного доверия задание таймера только в том, что Framework задания таймера с помощью API-интерфейсы на стороне клиента и таким образом можно и следует выполнять вне SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0d453-105">The primary difference with between the Timer Job Framework and the full trust code Timer Job is that the Timer Job Framework only uses client side APIs and therefore can (and should) be run outside of SharePoint.</span></span> <span data-ttu-id="0d453-106">Framework задания таймера позволяет создавать задания таймера, работают в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="0d453-106">The Timer Job Framework makes it possible to build Timer Jobs that operate against SharePoint Online.</span></span>

<span data-ttu-id="0d453-107">После задания таймера был создан, его необходимо планирования и выполнения.</span><span class="sxs-lookup"><span data-stu-id="0d453-107">Once a Timer Job has been created it needs to be scheduled and executed.</span></span> <span data-ttu-id="0d453-108">Две основные параметры являются:</span><span class="sxs-lookup"><span data-stu-id="0d453-108">The two most common options are:</span></span>

- <span data-ttu-id="0d453-109">Когда **Microsoft Azure** платформы размещения, задания таймера можно развернуть и запуска в качестве **Azure WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="0d453-109">When **Microsoft Azure** is the hosting platform, Timer Jobs can be deployed and run as **Azure WebJobs**.</span></span>
- <span data-ttu-id="0d453-110">**Windows Server** — размещения задания таймера платформы (например, для локального развертывания SharePoint) можно развернуть и запустить в **Планировщик Windows**.</span><span class="sxs-lookup"><span data-stu-id="0d453-110">When **Windows Server** is the hosting platform (e.g. for on-premises SharePoint) Timer Jobs can be deployed and run in **Windows scheduler**.</span></span>

<span data-ttu-id="0d453-111">Для видео Общие сведения о задания таймера [в этом видео PnP](http://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-the-PnP-timer-job-framework) представляется Framework задания таймера и показано в примере простого задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-111">For a video introduction to Timer Jobs, [this PnP video](http://channel9.msdn.com/blogs/OfficeDevPnP/Introduction-to-the-PnP-timer-job-framework) introduces the Timer Job Framework and demonstrates the Simple Timer Job example.</span></span>

## <a name="simple-timer-job-example"></a><span data-ttu-id="0d453-112">Простой пример задания таймера</span><span class="sxs-lookup"><span data-stu-id="0d453-112">Simple Timer Job example</span></span> ##
<span data-ttu-id="0d453-113">В этой главе вы увидите, как создать простой задание таймера: задача в этом примере — предоставить средство чтения быстрого представления, более поздней версии для мы предлагаем более подробное описание Framework задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-113">In this chapter you'll see how to create a very simple Timer Job: the goal of this sample is to provide the reader a quick view, later on we'll provide a more detailed explanation of the Timer Job Framework.</span></span> 

<span data-ttu-id="0d453-114">**Примечание:** Расширенный PnP решение с десяти отдельных примеры задания таймера из примеры задания фактический истечения срока действия содержимого, «Hello world» в разделе https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples</span><span class="sxs-lookup"><span data-stu-id="0d453-114">**Note:** For a more extensive PnP solution with ten individual Timer Job examples, from "Hello world" samples to actual content expiration jobs, see https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples</span></span>

<span data-ttu-id="0d453-115">Ниже описывается, как создать простой задания таймера:</span><span class="sxs-lookup"><span data-stu-id="0d453-115">The following describes how to create a simple Timer Job:</span></span>

### <a name="step-1-create-a-console-project-and-reference-pnp-core"></a><span data-ttu-id="0d453-116">Этап 1: Создайте проект консольного и ссылаться PnP ядра</span><span class="sxs-lookup"><span data-stu-id="0d453-116">Step 1: Create a Console project and reference PnP Core</span></span> ###
<span data-ttu-id="0d453-117">На первом этапе создайте новый проект типа «консоли» и ссылки на библиотеку PnP core, выполнив одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="0d453-117">In this first step, create a new project of the type "console" and reference the PnP core library by doing one of the following:</span></span>

- <span data-ttu-id="0d453-118">Добавьте в проект пакетов Nuget основные рекомендации и шаблоны для разработчиков Office 365.</span><span class="sxs-lookup"><span data-stu-id="0d453-118">Add the Office 365 Developer Patterns and Practices Core Nuget package to your project.</span></span> <span data-ttu-id="0d453-119">Существует [пакетов nuget для v15 (локально), а также для v16 (Office 365)](https://www.nuget.org/packages?q=pnp).</span><span class="sxs-lookup"><span data-stu-id="0d453-119">There's a [nuget package for v15 (on-premises) and for v16 (Office 365)](https://www.nuget.org/packages?q=pnp).</span></span> <span data-ttu-id="0d453-120">Это является предпочтительным.</span><span class="sxs-lookup"><span data-stu-id="0d453-120">This is the preferred option.</span></span>
- <span data-ttu-id="0d453-121">Добавление существующего проекта PnP основных источника в проект.</span><span class="sxs-lookup"><span data-stu-id="0d453-121">Add the existing PnP Core source project to your project.</span></span> <span data-ttu-id="0d453-122">Это позволит выполнить пошагово код PnP основных при отладке.</span><span class="sxs-lookup"><span data-stu-id="0d453-122">This will allow you to step into the PnP core code when debugging.</span></span> <span data-ttu-id="0d453-123">**Примечание:** Ответственность за поддержание этот код, обновлены с последними изменениями, добавляемого PnP будет.</span><span class="sxs-lookup"><span data-stu-id="0d453-123">**Note:** You will be responsible for keeping this code updated with the latest changes added to PnP.</span></span>

### <a name="step-2-create-a-timer-job-class-and-add-your-timer-job-logic"></a><span data-ttu-id="0d453-124">Шаг 2: Создание задания таймера класса и добавьте логику задания таймера</span><span class="sxs-lookup"><span data-stu-id="0d453-124">Step 2: Create a Timer Job class and add your Timer Job logic</span></span> ###
1. <span data-ttu-id="0d453-125">Добавьте в класс для задания таймера с именем `SimpleJob`.</span><span class="sxs-lookup"><span data-stu-id="0d453-125">Add a class for the Timer Job named `SimpleJob`.</span></span>
2. <span data-ttu-id="0d453-126">Класс, наследуемый `TimerJob` абстрактный базовый класс.</span><span class="sxs-lookup"><span data-stu-id="0d453-126">Have the class inherit the `TimerJob` abstract base class.</span></span>
3. <span data-ttu-id="0d453-127">В конструкторе имя задания таймера (`base("SimpleJob")`) и подключение `TimerJobRun` обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="0d453-127">In the constructor give the Timer Job a name (`base("SimpleJob")`) and connect the `TimerJobRun` event handler.</span></span>
4. <span data-ttu-id="0d453-128">Добавьте логику задания таймера для `TimerJobRun` обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="0d453-128">Add your Timer Job logic to the `TimerJobRun` event handler.</span></span>

<span data-ttu-id="0d453-129">Результатом будет следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0d453-129">The result will be similar to the following:</span></span>
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.SharePoint.Client;
using OfficeDevPnP.Core.Framework.TimerJobs;

namespace Core.TimerJobs.Samples.SimpleJob
{
    public class SimpleJob: TimerJob
    {
        public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }

        void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
    }
}
```

### <a name="step-3-update-programcs-to-use-the-timer-job"></a><span data-ttu-id="0d453-130">Шаг 3: Обновление Program.cs использования задания таймера</span><span class="sxs-lookup"><span data-stu-id="0d453-130">Step 3: Update Program.cs to use the Timer Job</span></span> ###
<span data-ttu-id="0d453-131">По-прежнему требуется выполнение задания таймера, созданных на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="0d453-131">The Timer Job created in the previous step still needs to be executed.</span></span> <span data-ttu-id="0d453-132">Для этого обновления `Program.cs` , выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0d453-132">To do so, update `Program.cs` by using the following steps:</span></span>

1. <span data-ttu-id="0d453-133">Создайте экземпляр класса задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-133">Instantiate your Timer Job class.</span></span>
2. <span data-ttu-id="0d453-134">Введите сведения проверки подлинности для задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-134">Provide the authentication details for the Timer Job.</span></span> <span data-ttu-id="0d453-135">В этом примере используется имя пользователя и пароль для проверки подлинности SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="0d453-135">This example uses the user name and password to authenticate against SharePoint Online.</span></span>
3. <span data-ttu-id="0d453-136">Добавление одного или нескольких сайтов для программы задания таймера для доступа.</span><span class="sxs-lookup"><span data-stu-id="0d453-136">Add one or more sites for the Timer Job program to access.</span></span> <span data-ttu-id="0d453-137">В этом примере используется подстановочный знак в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0d453-137">This example uses a wild card character in the URL.</span></span> <span data-ttu-id="0d453-138">Задание таймера, которое будет выполняться на всех сайтах, которые соответствуют этот URL-адрес подстановочным знаком.</span><span class="sxs-lookup"><span data-stu-id="0d453-138">The Timer Job will run on all sites that match this wild card URL.</span></span>
4. <span data-ttu-id="0d453-139">Запуск задания таймера, вызвав `Run` метод.</span><span class="sxs-lookup"><span data-stu-id="0d453-139">Start the Timer Job by calling the `Run` method.</span></span>

```C#
static void Main(string[] args)
{
    // Instantiate the Timer Job class
    SimpleJob simpleJob = new SimpleJob();
    
    // The provided credentials need access to the site collections you want to use
    simpleJob.UseOffice365Authentication("user@tenant.onmicrosoft.com", "pwd");

    // Add one or more sites to operate on
    simpleJob.AddSite("https://<tenant>.sharepoint.com/sites/d*");
    
    // Run the job
    simpleJob.Run();
}
```

## <a name="timer-job-deployment-options"></a><span data-ttu-id="0d453-140">Параметры развертывания задания таймера</span><span class="sxs-lookup"><span data-stu-id="0d453-140">Timer Job deployment options</span></span> ##
<span data-ttu-id="0d453-141">Предыдущее действие демонстрируется простой задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-141">The previous step demonstrates a simple Timer Job.</span></span> <span data-ttu-id="0d453-142">Следующим шагом является развертывание задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-142">The next step is to deploy the Timer Job.</span></span>

<span data-ttu-id="0d453-143">Задание таймера: .exe файла, который необходимо запланировать на платформы размещения.</span><span class="sxs-lookup"><span data-stu-id="0d453-143">A Timer Job is an .exe file that must be scheduled on a hosting platform.</span></span> <span data-ttu-id="0d453-144">В зависимости от выбранной платформы размещения отличается развертывания.</span><span class="sxs-lookup"><span data-stu-id="0d453-144">Depending on the chosen hosting platform the deployment differs.</span></span> <span data-ttu-id="0d453-145">Варианты платформы размещения два наиболее распространенных в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="0d453-145">The following sections describe the two most common hosting platform options:</span></span>
- <span data-ttu-id="0d453-146">Использование Microsoft Azure в качестве платформы размещения</span><span class="sxs-lookup"><span data-stu-id="0d453-146">Using Microsoft Azure as the hosting platform</span></span>
- <span data-ttu-id="0d453-147">Использование Windows Server в качестве платформы размещения</span><span class="sxs-lookup"><span data-stu-id="0d453-147">Using Windows Server as the hosting platform</span></span>

### <a name="deploying-timer-jobs-to-microsoft-azure-using-azure-webjobs"></a><span data-ttu-id="0d453-148">Развертывание заданий таймера в Microsoft Azure с использованием Azure WebJobs</span><span class="sxs-lookup"><span data-stu-id="0d453-148">Deploying Timer Jobs to Microsoft Azure using Azure WebJobs</span></span> ###
<span data-ttu-id="0d453-149">Перед развертыванием задания таймера, убедитесь, что задание можно запустить без взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="0d453-149">Before deploying a Timer Job, ensure that the job can run without user interaction.</span></span> <span data-ttu-id="0d453-150">Примеры в этой статье предлагать пользователю указать пароль или clientsecret (Дополнительные возможности **проверки подлинности**) котором работает во время тестирования но не будут работать при развертывании.</span><span class="sxs-lookup"><span data-stu-id="0d453-150">The sample in this article prompts the user to provide a password or clientsecret (see more in **Authentication**) which works while testing but will not work when deployed.</span></span> <span data-ttu-id="0d453-151">Все существующие образцы разрешает пользователю указать пароль или clientsecret с помощью `app.config` файла:</span><span class="sxs-lookup"><span data-stu-id="0d453-151">The existing samples all allow the user to provide a password or clientsecret by using the `app.config` file:</span></span>

```XML
  <appSettings>
    <add key="user" value="user@tenant.onmicrosoft.com"/>
    <add key="password" value="your password goes here!"/>
    <add key="domain" value="Contoso"/>
    <add key="clientid" value="a4cdf20c-3385-4664-8302-5eab57ee6f14"/>
    <add key="clientsecret" value="your clientsecret goes here!"/>
  </appSettings>
```

<span data-ttu-id="0d453-152">После добавления этих изменений `app.config` файл, запустите задание таймера из Visual Studio, чтобы убедиться, что он работает без взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="0d453-152">After these changes are added to the `app.config` file, run the Timer Job from Visual Studio to confirm that it runs without user interaction.</span></span> 

<span data-ttu-id="0d453-153">Фактические развертывания в Azure основан на задания Web Azure.</span><span class="sxs-lookup"><span data-stu-id="0d453-153">The actual deployment to Azure is based on Azure Web Jobs.</span></span> <span data-ttu-id="0d453-154">Чтобы развернуть в этом примере задание таймера, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0d453-154">To deploy this Timer Job example, follow these steps:</span></span>

1. <span data-ttu-id="0d453-155">Щелкните правой кнопкой мыши проект в Visual Studio и выберите пункт **Опубликовать как Azure WebJob...**</span><span class="sxs-lookup"><span data-stu-id="0d453-155">Right click the project in Visual Studio and choose **Publish as Azure WebJob...**</span></span>
2. <span data-ttu-id="0d453-156">Укажите расписание для задания таймера и нажмите **кнопку ОК**</span><span class="sxs-lookup"><span data-stu-id="0d453-156">Provide a schedule for the Timer Job and click **OK**</span></span>
3. <span data-ttu-id="0d453-157">Выберите **Веб-сайты Microsoft Azure** в качестве назначения публикации.</span><span class="sxs-lookup"><span data-stu-id="0d453-157">Select **Microsoft Azure Websites** as a publish target.</span></span> <span data-ttu-id="0d453-158">Вам потребуется войти в систему в Azure и выберите веб-сайта Azure, используемом для задания таймера (можно также создать новый Если, который необходимо было)</span><span class="sxs-lookup"><span data-stu-id="0d453-158">You'll be asked to login to Azure and select the Azure Web Site that will host the Timer Job (you can also create a new one if that would be needed)</span></span>
4. <span data-ttu-id="0d453-159">Нажмите кнопку **Опубликовать** , чтобы push-WebJob в Azure</span><span class="sxs-lookup"><span data-stu-id="0d453-159">Press **Publish** to push the WebJob to Azure</span></span>
5. <span data-ttu-id="0d453-160">После публикации задания таймера можно запустить задание и проверьте выполнение задания из Visual Studio или [портала управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0d453-160">Once the Timer Job has been published you can trigger the job and check the job execution from Visual Studio or the [Azure management portal](https://manage.windowsazure.com).</span></span>

![Портала управления Azure](media/timerjob-framework/4xDUvXv.png)

<span data-ttu-id="0d453-162">Кроме того задания таймера можно выполнять с новой [Azure портала](https://portal.azure.com) , выберите задание и выберите **выполнить**.</span><span class="sxs-lookup"><span data-stu-id="0d453-162">Also, the timer job can be run from the new [Azure portal](https://portal.azure.com) by selecting the job and choosing **Run**.</span></span> <span data-ttu-id="0d453-163">Дополнительные сведения о том, как работать с WebJobs в новый портал можно найти в статье, [запустите фоновых задач с WebJobs](https://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).</span><span class="sxs-lookup"><span data-stu-id="0d453-163">More details about how to work with WebJobs from the new portal can be found in the article, [Run Background tasks with WebJobs](https://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).</span></span>

![Портал Azure](media/timerjob-framework/n4wGS5x.png)

<span data-ttu-id="0d453-165">**Примечание:** Подробная информация о развертывании WebJob Azure в разделе [Приступая к работе с azure WebJobs («задания таймера») для сайтов Office 365](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md).</span><span class="sxs-lookup"><span data-stu-id="0d453-165">**Note:** For in-depth guidance on deploying an Azure WebJob, see [Getting Started with azure WebJobs ("Timer Jobs") for your Office 365 Sites](https://github.com/SharePoint/PnP-Guidance/blob/master/articles/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites.md).</span></span> 

### <a name="deploying-timer-jobs-to-windows-server-using-the-windows-scheduler"></a><span data-ttu-id="0d453-166">Развертывание задания таймера для Windows Server с помощью планировщика заданий Windows</span><span class="sxs-lookup"><span data-stu-id="0d453-166">Deploying Timer Jobs to Windows Server using the Windows Scheduler</span></span> ###
<span data-ttu-id="0d453-167">При развертывании Windows Server, задание таймера, которое должно выполняться без взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="0d453-167">When deployed to Windows Server, the Timer Job must run without user interaction.</span></span> <span data-ttu-id="0d453-168">Изменение `app.config` файлов, как описано в **Развертывание заданий таймера в Microsoft Azure с использованием Azure WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="0d453-168">Modify the `app.config` file as described in **Deploying Timer Jobs to Microsoft Azure using Azure WebJobs**.</span></span> 

<span data-ttu-id="0d453-169">Скопируйте версии выпуска задания вы должны быть выполнены сервере.</span><span class="sxs-lookup"><span data-stu-id="0d453-169">Copy the release version of your job to the server you want it to run on.</span></span> <span data-ttu-id="0d453-170">**Важные:** Копирование всех соответствующих сборок, файлов .exe и config-файла убедитесь, что задание можно запустить на сервере без установки дополнительных файлов или программ на сервере.</span><span class="sxs-lookup"><span data-stu-id="0d453-170">**Important:** Copy all the relevant assemblies, the .exe file and the .config file to ensure the job can run on the server without installing any additional files or programs on the server.</span></span> 

<span data-ttu-id="0d453-171">Планирование выполнения задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-171">Schedule the execution of the Timer Job.</span></span> <span data-ttu-id="0d453-172">Рекомендуется использовать встроенный [Планировщик задач Windows](https://technet.microsoft.com/en-us/library/cc721871.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d453-172">It is recommended to use the built in [Windows Task Scheduler](https://technet.microsoft.com/en-us/library/cc721871.aspx).</span></span> <span data-ttu-id="0d453-173">Чтобы использовать планировщик задач Windows, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0d453-173">To use the Windows Task Scheduler, take the following steps:</span></span>

1. <span data-ttu-id="0d453-174">Откройте планировщик заданий (панель управления -> планировщик заданий).</span><span class="sxs-lookup"><span data-stu-id="0d453-174">Open the task scheduler (Control Panel -> Task Scheduler).</span></span>
2. <span data-ttu-id="0d453-175">Щелкните **Создать задачу** и укажите имя и учетную запись, которая будет выполнять задачи.</span><span class="sxs-lookup"><span data-stu-id="0d453-175">Click on **Create Task** and specify a name and an account that will execute the task.</span></span>
3. <span data-ttu-id="0d453-176">Щелкните **триггеры** и добавить новый триггер.</span><span class="sxs-lookup"><span data-stu-id="0d453-176">Click on **Triggers** and add a new trigger.</span></span> <span data-ttu-id="0d453-177">Укажите расписание, которое необходимо использовать для задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-177">Specify the schedule you want for the Timer Job.</span></span>
4. <span data-ttu-id="0d453-178">Нажмите кнопку **действия** и выберите действие «Запустите программу», выберите файл .exe задание таймера и укажите время начала в папке.</span><span class="sxs-lookup"><span data-stu-id="0d453-178">Click on **Actions** and choose action "Start a program", select the Timer Job .exe file and set the start in folder.</span></span>
5. <span data-ttu-id="0d453-179">Нажмите **кнопку ОК** , чтобы сохранить задачу.</span><span class="sxs-lookup"><span data-stu-id="0d453-179">Click on **OK** to save the task.</span></span>

![Планировщик заданий Windows](media/timerjob-framework/hkRc0Bo.png)

## <a name="timer-job-framework-in-depth"></a><span data-ttu-id="0d453-181">Подробные Framework задания таймера</span><span class="sxs-lookup"><span data-stu-id="0d453-181">Timer Job Framework in-depth</span></span> ##
<span data-ttu-id="0d453-182">В этом разделе сведения о том, как функции Framework задания таймера и как это работает.</span><span class="sxs-lookup"><span data-stu-id="0d453-182">This section details how the Timer Job Framework features and how it works.</span></span>

### <a name="structure"></a><span data-ttu-id="0d453-183">Структура</span><span class="sxs-lookup"><span data-stu-id="0d453-183">Structure</span></span> ###
<span data-ttu-id="0d453-184">`TimerJob` Класс — абстрактный базовый класс, который содержит следующие общие свойства, методы и события:</span><span class="sxs-lookup"><span data-stu-id="0d453-184">The `TimerJob` class is an abstract base class which contains the following public properties, methods and events:</span></span>

![Структура класса задания таймера](media/timerjob-framework/4XsZ1pN.png)

<span data-ttu-id="0d453-186">Большинство свойств и методов будет описано в следующих разделах более подробно.</span><span class="sxs-lookup"><span data-stu-id="0d453-186">Most properties and methods will be explained in more detail in the coming sections.</span></span> <span data-ttu-id="0d453-187">Остальные свойства и методы, описанные здесь:</span><span class="sxs-lookup"><span data-stu-id="0d453-187">The rest of the properties and methods are described here:</span></span>

- <span data-ttu-id="0d453-188">Свойство **IsRunning** : возвращает значение, указывающее, выполняется ли задание таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-188">**IsRunning** property: Gets a value indicating whether the Timer Job is executing.</span></span> <span data-ttu-id="0d453-189">Значение **true,** Если выполнение; **значение false,** Если не выполняется.</span><span class="sxs-lookup"><span data-stu-id="0d453-189">Value of **true** if executing; **false** if not executing.</span></span>
- <span data-ttu-id="0d453-190">Свойство **Name** : Возвращает имя задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-190">**Name** property: Gets the name of the Timer Job.</span></span> <span data-ttu-id="0d453-191">Имя изначально набора в конструкторе задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-191">The name is initially set in the Timer Job constructor.</span></span>
- <span data-ttu-id="0d453-192">Свойство **SharePointVersion** : Получает или задает версию SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0d453-192">**SharePointVersion** property: Gets or sets the SharePoint version.</span></span> <span data-ttu-id="0d453-193">Это свойство автоматически устанавливается на основе версии загруженных Microsoft.SharePoint.Client.dll и вообще не изменятся.</span><span class="sxs-lookup"><span data-stu-id="0d453-193">this property is automatically set based on the version of the loaded Microsoft.SharePoint.Client.dll and in general should not change.</span></span> <span data-ttu-id="0d453-194">Тем не менее, можно изменить это свойство, в случае, если требуется для примера использования библиотек CSOM v16 в v15 развертывания (локально).</span><span class="sxs-lookup"><span data-stu-id="0d453-194">You can, however, change this property in case you for example want to use the v16 CSOM libraries in a v15 (on-premises) deployment.</span></span>
- <span data-ttu-id="0d453-195">Свойство **Version** : Получает версию этого задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-195">**Version** property: Gets the version of this Timer Job.</span></span> <span data-ttu-id="0d453-196">Версия не задано в конструкторе задание таймера или параметры по умолчанию для версии 1.0, если не задано с помощью конструктора.</span><span class="sxs-lookup"><span data-stu-id="0d453-196">The version is initially set in the Timer Job constructor or defaults to 1.0 when not set via the constructor.</span></span>

<span data-ttu-id="0d453-197">Чтобы подготовить для задания таймера, вы запустите необходимо **настроить** первый его:</span><span class="sxs-lookup"><span data-stu-id="0d453-197">To prepare for a Timer Job run you must first **configure** it:</span></span>

1. <span data-ttu-id="0d453-198">Укажите параметры **проверки подлинности** .</span><span class="sxs-lookup"><span data-stu-id="0d453-198">Provide **authentication** settings.</span></span>
2. <span data-ttu-id="0d453-199">Укажите **область**, в которой приведен список сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-199">Provide a **scope**, which is a list of sites.</span></span>
3. <span data-ttu-id="0d453-200">При необходимости задайте значения **Задания таймера**.</span><span class="sxs-lookup"><span data-stu-id="0d453-200">Optionally set **Timer Job properties**.</span></span>

<span data-ttu-id="0d453-201">С точки зрения выполнения следующие общие действия, предпринимаемые при работы выполнения задания таймера:</span><span class="sxs-lookup"><span data-stu-id="0d453-201">From an execution perspective the following overall steps are taken when a Timer Job run is started:</span></span>

1. <span data-ttu-id="0d453-202">**Разрешения сайтов**: URL-адреса сайтов подстановочным знаком (например, https://tenant.sharepoint.com/sites/d *) заменяются на фактический список существующих сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-202">**Resolve sites**: Wild card site urls (for example, https://tenant.sharepoint.com/sites/d*) are resolved into an actual list of existing sites.</span></span> <span data-ttu-id="0d453-203">Если развертывание сайта sub был запрошен со всеми сайтами sub развернут в список разрешенных узлов.</span><span class="sxs-lookup"><span data-stu-id="0d453-203">If sub site expanding was requested then the resolved sites list is expanded with all sub sites.</span></span>
2. <span data-ttu-id="0d453-204">**Создание пакетов работы** на основе текущего treading параметров и создайте один поток в пакете.</span><span class="sxs-lookup"><span data-stu-id="0d453-204">**Create batches of work** based on the current treading settings and create one thread per batch.</span></span>
3. <span data-ttu-id="0d453-205">**Потоки выполнения работы пакетов** и вызова `TimerJobRun` событий для каждого сайта в списке.</span><span class="sxs-lookup"><span data-stu-id="0d453-205">The **threads execute work batches** and call the `TimerJobRun` event for each site in the list.</span></span>

<span data-ttu-id="0d453-206">Дополнительные сведения о каждом шаге можно найти ниже.</span><span class="sxs-lookup"><span data-stu-id="0d453-206">Further details on each step can be found below.</span></span>

### <a name="authentication"></a><span data-ttu-id="0d453-207">Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="0d453-207">Authentication</span></span> ###
<span data-ttu-id="0d453-208">Прежде чем можно будет использовать задания таймера задание таймера, которое необходимо знать, как выполнить проверку подлинности на SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0d453-208">Before a Timer Job can be used the Timer Job needs to know how to authenticate back to SharePoint.</span></span> <span data-ttu-id="0d453-209">Платформа в настоящее время поддерживает подходов в перечисления **AuthenticationType** . **Office 365**, **NetworkCredentials** и **AppOnly**.</span><span class="sxs-lookup"><span data-stu-id="0d453-209">The framework currently supports the approaches in the **AuthenticationType** enum; **Office365**, **NetworkCredentials** and **AppOnly**.</span></span> <span data-ttu-id="0d453-210">С помощью методов ниже иллюстрируется автоматически устанавливает свойство **AuthenticationType** соответствующее значение **Office 365**, **NetworkCredentials** и **AppOnly**.</span><span class="sxs-lookup"><span data-stu-id="0d453-210">Using the methods illustrated below also automatically sets the **AuthenticationType** property to the appropriate value of **Office365**, **NetworkCredentials** and **AppOnly**.</span></span> <span data-ttu-id="0d453-211">Блок-схема ниже показаны шаги.</span><span class="sxs-lookup"><span data-stu-id="0d453-211">The flowchart below shows the steps to take.</span></span> <span data-ttu-id="0d453-212">Подробное объяснение на каждый подход находятся ниже.</span><span class="sxs-lookup"><span data-stu-id="0d453-212">Detailed explanations on each approach are found below.</span></span>

![Блок-схема шаги проверки подлинности](media/timerjob-framework/rt4dZa3.png)

#### <a name="user-credentials"></a><span data-ttu-id="0d453-214">Учетные данные пользователя</span><span class="sxs-lookup"><span data-stu-id="0d453-214">User credentials</span></span> ####
<span data-ttu-id="0d453-215">Чтобы указать учетные данные пользователя для работы с **Office 365** можно использовать эти методы 2:</span><span class="sxs-lookup"><span data-stu-id="0d453-215">To specify user credentials for running against **Office 365** you can use these 2 methods:</span></span>
```C#
public void UseOffice365Authentication(string userUPN, string password)
public void UseOffice365Authentication(string credentialName)
```

<span data-ttu-id="0d453-216">Первый метод просто принимает имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="0d453-216">The first method simply accepts a user name and password.</span></span> <span data-ttu-id="0d453-217">Второй позволяет указать универсальный учетные данные, хранящиеся в диспетчере учетных данных Windows.</span><span class="sxs-lookup"><span data-stu-id="0d453-217">The second one allows you to specify a generic credential stored in the Windows Credential Manager.</span></span> <span data-ttu-id="0d453-218">Снимок экрана ниже показано `bertonline` универсальный учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0d453-218">The screen shot below shows the `bertonline` generic credential.</span></span> <span data-ttu-id="0d453-219">Чтобы использовать ее для проверки подлинности задание таймера, предоставляют «bertonline» в качестве параметра метода второй.</span><span class="sxs-lookup"><span data-stu-id="0d453-219">To use that to authenticate the Timer Job, provide "bertonline" as the parameter of the second method.</span></span>

![Диспетчер учетных данных Windows](media/timerjob-framework/HdqvsHy.png)

<span data-ttu-id="0d453-221">Существует аналогичные методы для работы с **SharePoint локально**.</span><span class="sxs-lookup"><span data-stu-id="0d453-221">There are similar methods for running against **SharePoint on-premises**:</span></span>
```C#
public void UseNetworkCredentialsAuthentication(string samAccountName, string password, string domain)
public void UseNetworkCredentialsAuthentication(string credentialName)
```

#### <a name="app-only"></a><span data-ttu-id="0d453-222">Только приложения</span><span class="sxs-lookup"><span data-stu-id="0d453-222">App Only</span></span> ####
<span data-ttu-id="0d453-223">Приложение только — **предпочтительный способ** как может предоставить разрешения уровня клиента.</span><span class="sxs-lookup"><span data-stu-id="0d453-223">App only is the **preferred method** as you can grant tenant scoped permissions.</span></span> <span data-ttu-id="0d453-224">Учетные данные пользователя для учетной записи пользователя должны быть необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="0d453-224">For user credentials the user account must have the needed permissions.</span></span> 

<span data-ttu-id="0d453-225">**Примечание:** Определенные веб-сайтов разрешения логику не работы с проверкой подлинности только для приложений.</span><span class="sxs-lookup"><span data-stu-id="0d453-225">**Note:** Certain site resolving logic wont work with App-only authentication.</span></span> <span data-ttu-id="0d453-226">Подробные сведения можно найти в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="0d453-226">Details can be found in the next section.</span></span> 

<span data-ttu-id="0d453-227">Чтобы настроить задание для проверки подлинности только для приложений, используйте один из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="0d453-227">To configure the job for app-only authentication, use one of the following methods:</span></span>
```C#
public void UseAppOnlyAuthentication(string clientId, string clientSecret)
public void UseAzureADAppOnlyAuthentication(string clientId, string clientSecret)
```

<span data-ttu-id="0d453-228">Тот же метод можно использовать для Office 365 или SharePoint локальных что делает задания таймера с помощью только проверки подлинности легко портативных между средами.</span><span class="sxs-lookup"><span data-stu-id="0d453-228">The same method can be used for either Office 365 or SharePoint on-premises which makes Timer Jobs using app-only authentication easily transportable between environments.</span></span>

<span data-ttu-id="0d453-229">**Примечание:** При использовании только логику задание таймера не удается при использовании API-интерфейсы, которые не работают с **AuthenticationType.AppOnly**.</span><span class="sxs-lookup"><span data-stu-id="0d453-229">**Note:** When you use app-only your Timer Job logic will fail when APIs are used that do not work with **AuthenticationType.AppOnly**.</span></span> <span data-ttu-id="0d453-230">Типичные примеры — это API поиска, записи в хранилище данных таксономии и с помощью API профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="0d453-230">Typical samples are the Search API, writing to the taxonomy store, and using the user profile API.</span></span>

### <a name="sites-to-operate-on"></a><span data-ttu-id="0d453-231">Сайты для работы с</span><span class="sxs-lookup"><span data-stu-id="0d453-231">Sites to operate on</span></span> ###
<span data-ttu-id="0d453-232">После запуска задания таймера должно одного или нескольких сайтов должно выполняться.</span><span class="sxs-lookup"><span data-stu-id="0d453-232">When a Timer Job runs it needs one or more sites to run against.</span></span> <span data-ttu-id="0d453-233">Чтобы добавить сайты задания таймера, используйте ниже набор методов.</span><span class="sxs-lookup"><span data-stu-id="0d453-233">To add sites to a Timer Job, use the below set of methods.</span></span>

```C#
public void AddSite(string site)
public void ClearAddedSites()
```

<span data-ttu-id="0d453-234">Чтобы добавить сайт, укажите полный URL-адрес (например, https://tenant.sharepoint.com/sites/dev) или URL-адрес подстановочным знаком.</span><span class="sxs-lookup"><span data-stu-id="0d453-234">To add a site, specify either a fully qualified URL (for example, https://tenant.sharepoint.com/sites/dev) or a wild card URL.</span></span> <span data-ttu-id="0d453-235">URL-адрес подстановочным знаком — это URL-адрес, который заканчивается на * (только один одним * может должно являться последнего символа, URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="0d453-235">A wild card URL is a URL that ends with a * (only one single * is allowed and it must be the last character of the url).</span></span> <span data-ttu-id="0d453-236">— Это URL-адрес примера подстановочных https://tenant.sharepoint.com/sites/ *, которая возвращает **все** семейства веб-сайтов под управляемый путь из этого сайта.</span><span class="sxs-lookup"><span data-stu-id="0d453-236">A sample wild card URL is https://tenant.sharepoint.com/sites/* which will return **all** the site collections underneath the managed path of that site.</span></span> <span data-ttu-id="0d453-237">Другой пример https://tenant.sharepoint.com/sites/dev * возвращает все семейства сайтов которых содержит URL-адрес «dev».</span><span class="sxs-lookup"><span data-stu-id="0d453-237">For another example, https://tenant.sharepoint.com/sites/dev* will return all site collections where the URL contains "dev".</span></span>

<span data-ttu-id="0d453-238">Обычно сайты добавляются по программам, создает экземпляр объекта задания таймера, но при необходимости задание таймера, которое может принимать контроль над переданный список сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-238">Typically the sites are added by the program that instantiates the Timer Job object, but if needed the Timer Job can take control over the passed list of sites.</span></span> <span data-ttu-id="0d453-239">Это можно сделать, добавив переопределение метода для `UpdateAddedSites`виртуальный метод, как показано в примере ниже:</span><span class="sxs-lookup"><span data-stu-id="0d453-239">Do this by adding a method override for the `UpdateAddedSites`virtual method as shown in sample below:</span></span>

```C#
public override List<string> UpdateAddedSites(List<string> addedSites)
{
    // Let's assume we're not happy with the provided list of sites, so first clear it
    addedSites.Clear();

    // Manually adding a new wildcard Url, without an added URL the Timer Job will do...nothing
    addedSites.Add("https://bertonline.sharepoint.com/sites/d*");

    // Return the updated list of sites
    return addedSites;
}
```

<span data-ttu-id="0d453-240">После добавления подстановочных URL-адрес и параметры проверки подлинности только для приложений, укажите учетные данные перечисление.</span><span class="sxs-lookup"><span data-stu-id="0d453-240">After adding a wild card URL and setting authentication to app-only, specify the enumeration credentials.</span></span> <span data-ttu-id="0d453-241">Чтобы получить список семейств веб-сайтов, используемые в алгоритм сопоставления сайта для возврата реальных список сайтов используются учетные данные перечисление.</span><span class="sxs-lookup"><span data-stu-id="0d453-241">Enumeration credentials are used to fetch a list of site collections which are used in the site matching algorithm to return a real list of sites.</span></span> <span data-ttu-id="0d453-242">Для получения списка семейств веб-сайтов framework таймера будет отличаться от Office 365 (v16) и локальной (v15):</span><span class="sxs-lookup"><span data-stu-id="0d453-242">To acquire a list of site collections the timer framework will behave differently between Office 365 (v16) and on-premises (v15):</span></span>
- <span data-ttu-id="0d453-243">Office 365: `Tenant.GetSiteProperties` метод используется для чтения «периодически» семейств, API поиска используется для чтения OneDrive для бизнеса семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-243">Office 365: The `Tenant.GetSiteProperties` method is used to read the 'regular' site collections, the search API is used to read the OneDrive for Business site collections.</span></span>
- <span data-ttu-id="0d453-244">Локальные: API поиска используется для чтения всех семейств веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-244">On-Premises: The search API is used to read all site collections.</span></span>

<span data-ttu-id="0d453-245">API поиска не работает с помощью контекста пользователя, что задание таймера, которое будет использоваться учетные данные указанного перечисления.</span><span class="sxs-lookup"><span data-stu-id="0d453-245">Given that the search API doesn't work with a user context, the Timer Job falls back to the specified enumeration credentials.</span></span> 

<span data-ttu-id="0d453-246">Чтобы указать учетные данные пользователя для работы с **Office 365** можно использовать эти методы 2:</span><span class="sxs-lookup"><span data-stu-id="0d453-246">To specify user credentials for running against **Office 365** you can use these 2 methods:</span></span>
```C#
public void SetEnumerationCredentials(string userUPN, string password)
public void SetEnumerationCredentials(string credentialName)
```

<span data-ttu-id="0d453-247">Существует аналогичные методы для работы с **SharePoint локально**.</span><span class="sxs-lookup"><span data-stu-id="0d453-247">There are similar methods for running against **SharePoint on-premises**:</span></span>
```C#
public void SetEnumerationCredentials(string samAccountName, string password, string domain)
public void SetEnumerationCredentials(string credentialName)
```

<span data-ttu-id="0d453-248">Первый метод просто принимает имя пользователя, пароль и при необходимости домена (в локальном).</span><span class="sxs-lookup"><span data-stu-id="0d453-248">The first method simply accepts a user name, password and optionally domain (when in on-premises).</span></span> <span data-ttu-id="0d453-249">Второй — задает универсальный учетные данные, хранящиеся в диспетчере учетных данных Windows.</span><span class="sxs-lookup"><span data-stu-id="0d453-249">The second specifies a generic credential stored in the Windows Credential Manager.</span></span> <span data-ttu-id="0d453-250">Обратитесь к главе **проверки подлинности** для получения дополнительных сведений о диспетчере учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0d453-250">See the **Authentication** chapter to learn more about the Credential Manager.</span></span>

#### <a name="sub-site-expanding"></a><span data-ttu-id="0d453-251">Развертывание веб-узла</span><span class="sxs-lookup"><span data-stu-id="0d453-251">Sub site expanding</span></span> ####
<span data-ttu-id="0d453-252">Часто требуется код задания таймера для выполнения корневого сайта семейства веб-сайтов и всех вложенных сайтов этого семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-252">Often you want the Timer Job code to be executed against the root site of the site collection and against all the sub sites of that site collection.</span></span> <span data-ttu-id="0d453-253">Чтобы сделать это, присвойте свойству **ExpandSubSites** значение **true**.</span><span class="sxs-lookup"><span data-stu-id="0d453-253">To do this, set the **ExpandSubSites** property to **true**.</span></span> <span data-ttu-id="0d453-254">Это приведет к задания таймера для разверните узел сайты sub как часть узла, разрешение шаг.</span><span class="sxs-lookup"><span data-stu-id="0d453-254">This will cause the Timer Job to expand the sub sites as part of the site resolving step.</span></span>

#### <a name="override-resolved-andor-expanded-sites"></a><span data-ttu-id="0d453-255">Переопределение разрешения и/или расширенное сайтов</span><span class="sxs-lookup"><span data-stu-id="0d453-255">Override resolved and/or expanded sites</span></span> ####
<span data-ttu-id="0d453-256">Framework таймера обрабатывает шаблонами сайтов и при необходимости разворачивает сайты sub, следующий шаг после обработки в список сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-256">Once the timer framework resolves the wild card sites, and optionally expands the sub sites, the next step is to process the list of sites.</span></span> <span data-ttu-id="0d453-257">До начала обработки в список сайтов, может возникнуть необходимость изменить список сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-257">Prior to processing the list of sites, you might want to modify the list of sites.</span></span> <span data-ttu-id="0d453-258">Например может потребоваться удаление определенных сайтов или добавить несколько узлов в список.</span><span class="sxs-lookup"><span data-stu-id="0d453-258">For example, you may want to remove specific sites or add more sites to the list.</span></span> <span data-ttu-id="0d453-259">Это можно сделать путем переопределения `ResolveAddedSites` виртуальный метод.</span><span class="sxs-lookup"><span data-stu-id="0d453-259">This can be accomplished by overriding the `ResolveAddedSites` virtual method.</span></span> <span data-ttu-id="0d453-260">В этом примере показано, как переопределить `ResolveAddedSites` метод для удаления одного сайта из списка.</span><span class="sxs-lookup"><span data-stu-id="0d453-260">The sample below shows how to override the `ResolveAddedSites` method to remove one site from the list.</span></span> 

```C#
public override List<string> ResolveAddedSites(List<string> addedSites)
{
    // Use default TimerJob base class site resolving
    addedSites = base.ResolveAddedSites(addedSites);

    //Delete the first one from the list...simple change. A real life case could be reading the site scope 
    //from a SQL (Azure) DB to prevent the whole site resolving. 
    addedSites.RemoveAt(0);

    // return the updated list of resolved sites...this list will be processed by the Timer Job
    return addedSites;
}
```

### <a name="timerjobrun-event"></a><span data-ttu-id="0d453-261">Событие TimerJobRun</span><span class="sxs-lookup"><span data-stu-id="0d453-261">TimerJobRun event</span></span> ###
<span data-ttu-id="0d453-262">Список сайтов разделяет Framework задания таймера на рабочих пакетов.</span><span class="sxs-lookup"><span data-stu-id="0d453-262">The Timer Job Framework splits the list of sites into work batches.</span></span> <span data-ttu-id="0d453-263">Каждый пакет сайтов будет выполняться в отдельном потоке.</span><span class="sxs-lookup"><span data-stu-id="0d453-263">Each batch of sites will be run on its own thread.</span></span> <span data-ttu-id="0d453-264">По умолчанию платформа будет создавать пять пакетов и пять потоков для запуска этих пять пакетов.</span><span class="sxs-lookup"><span data-stu-id="0d453-264">By default, the framework will create five batches and five threads to run those five batches.</span></span> <span data-ttu-id="0d453-265">Чтобы узнать больше о threading параметры задания таймера в разделе **работы с потоками** .</span><span class="sxs-lookup"><span data-stu-id="0d453-265">See the **Threading** section to learn more about Timer Job threading options.</span></span> <span data-ttu-id="0d453-266">Когда поток обрабатывает пакет `TimerJobRun` событие инициируется framework таймера и будет предоставлять все необходимые сведения для выполнения задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-266">When a thread processes a batch the `TimerJobRun` event is triggered by the timer framework and will provide all the necessary information to run the Timer Job.</span></span> <span data-ttu-id="0d453-267">Задания таймера выполняются как события, поэтому код необходимо подключить обработчик событий для `TimerJobRun` событий:</span><span class="sxs-lookup"><span data-stu-id="0d453-267">Timer Jobs are run as events, so the code must connect an event handler to the `TimerJobRun` event:</span></span>

```C#
public SimpleJob() : base("SimpleJob")
{
    TimerJobRun += SimpleJob_TimerJobRun;
}

void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
{
    // your Timer Job logic goes here
}
```

<span data-ttu-id="0d453-268">Альтернативный подход с помощью делегата встроенного как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="0d453-268">An alternative approach is using an inline delegate as shown here:</span></span>

```C#
public SimpleJob() : base("SimpleJob")
{
    // Inline delegate
    TimerJobRun += delegate(object sender, TimerJobRunEventArgs e)
    {
        // your Timer Job logic goes here
    };
}
```

<span data-ttu-id="0d453-269">При `TimerJobRun` вызывает событие, вы получаете `TimerJobRunEventArgs` объект, который предоставляет сведения, необходимые для запись логику задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-269">When the `TimerJobRun` event fires you receive a `TimerJobRunEventArgs` object which provides the necessary information to write the Timer Job logic.</span></span> <span data-ttu-id="0d453-270">В этом классе доступны следующие атрибуты и методы:</span><span class="sxs-lookup"><span data-stu-id="0d453-270">The following attributes and methods are available in this class:</span></span>

![Структура класса TimerJobRunEventArgs](media/timerjob-framework/CRFBdwS.png)

<span data-ttu-id="0d453-272">Некоторые свойства и все методы, используемых в функции управления необязательно состояний, которая будет описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="0d453-272">Several of the properties and all of the methods are used in the optional state management feature which will be discussed in the next section.</span></span> <span data-ttu-id="0d453-273">Тем не менее следующие свойства всегда будут доступны в все события, вне зависимости от конфигурации:</span><span class="sxs-lookup"><span data-stu-id="0d453-273">However the following properties will always be available in every event, regardless of the used configuration:</span></span>
- <span data-ttu-id="0d453-274">Свойство **URL-адрес** : Получает или задает URL-адрес сайта для задания таймера для работы.</span><span class="sxs-lookup"><span data-stu-id="0d453-274">**Url** property: Gets or sets the URL of the site for the Timer Job to operate against.</span></span> <span data-ttu-id="0d453-275">Это может быть корневого сайта семейства веб-сайтов, но это может быть веб-узла в случае, если развертывание сайта было сделано.</span><span class="sxs-lookup"><span data-stu-id="0d453-275">This can be the root site of the site collection, but it can also be a sub site in case site expanding was done.</span></span>
- <span data-ttu-id="0d453-276">Свойство **ConfigurationData** : Получает или задает данные конфигурации задания таймера дополнительных (не обязательно).</span><span class="sxs-lookup"><span data-stu-id="0d453-276">**ConfigurationData** property: Gets or sets additional timer job configuration data (optional).</span></span> <span data-ttu-id="0d453-277">Эти данные конфигурации передается как часть `TimerJobRunEventArgs` объекта.</span><span class="sxs-lookup"><span data-stu-id="0d453-277">This configuration data is passed along as part of the `TimerJobRunEventArgs` object.</span></span>
- <span data-ttu-id="0d453-278">Свойство **WebClientContext** : Получает или задает `ClientContext` объекта для текущего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="0d453-278">**WebClientContext** property: Gets or sets the `ClientContext` object for the current URL.</span></span> <span data-ttu-id="0d453-279">Это свойство соответствует `ClientContext` объекта для сайта, определенного в свойстве *URL-адрес* .</span><span class="sxs-lookup"><span data-stu-id="0d453-279">This property is a `ClientContext` object for the site defined in the *Url* property.</span></span> <span data-ttu-id="0d453-280">Обычно это `ClientContext` объект, который можно использовать в коде задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-280">This is typically the `ClientContext` object that you would use in your Timer Job code.</span></span>
- <span data-ttu-id="0d453-281">Свойство **SiteClientContext** : Получает или задает `ClientContext` объект для корневого сайта семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-281">**SiteClientContext** property: Gets or sets the `ClientContext` object for the root site of the site collection.</span></span> <span data-ttu-id="0d453-282">Это свойство предоставляет доступ к корневому сайту задание таймера, которое требуется доступ к нему.</span><span class="sxs-lookup"><span data-stu-id="0d453-282">This property provides access to the root site should the Timer Job require access to it.</span></span> <span data-ttu-id="0d453-283">Например задание таймера, которое можно добавить в макет страниц в коллекции главных страниц, с помощью свойства *SiteClientContext* .</span><span class="sxs-lookup"><span data-stu-id="0d453-283">For example, the Timer Job can add a page layout to the master page gallery using the *SiteClientContext* property.</span></span>
- <span data-ttu-id="0d453-284">Свойство **TenantClientContext** : Получает или задает `ClientContext` объекта для работы с API клиента.</span><span class="sxs-lookup"><span data-stu-id="0d453-284">**TenantClientContext** property: Gets or sets the `ClientContext` object to work with the Tenant API.</span></span> <span data-ttu-id="0d453-285">Это свойство предоставляет `ClientContext`объект, созданный с помощью URL-адрес сайта администрирования клиентов.</span><span class="sxs-lookup"><span data-stu-id="0d453-285">This property provides a `ClientContext`object constructed by using the tenant admin site URL.</span></span> <span data-ttu-id="0d453-286">Для использования `Tenant` API в задание таймера `TimerJobRun` обработчик события создания нового `Tenant` объектов с помощью этого свойства TenantClientContext.</span><span class="sxs-lookup"><span data-stu-id="0d453-286">To use the `Tenant` API in the Timer Job `TimerJobRun` event handler, create a new `Tenant` object by using this TenantClientContext property.</span></span>

<span data-ttu-id="0d453-287">Все `ClientContext`объекты используют данные проверки подлинности, описанных в разделе **тип проверки подлинности** .</span><span class="sxs-lookup"><span data-stu-id="0d453-287">All `ClientContext`objects use the authentication information described in the **Authentication** section.</span></span> <span data-ttu-id="0d453-288">Если вы удалили учетных данных пользователя Убедитесь, что используется учетная запись имеет необходимые разрешения для работы указанные веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="0d453-288">If you've opted for user credentials please ensure that the used account has the needed permissions to operate against the specified sites.</span></span> <span data-ttu-id="0d453-289">При использовании только для приложений, рекомендуется задать разрешения на уровне клиента участнику только для приложений.</span><span class="sxs-lookup"><span data-stu-id="0d453-289">When using app-only, it is best to set tenant-scoped permissions to the app-only principal.</span></span>

### <a name="state-management"></a><span data-ttu-id="0d453-290">Управление состоянием</span><span class="sxs-lookup"><span data-stu-id="0d453-290">State management</span></span> ###
<span data-ttu-id="0d453-291">При создании задания таймера логики часто требуется сохранить состояние.</span><span class="sxs-lookup"><span data-stu-id="0d453-291">When you write Timer Job logic you often need to persist state.</span></span> <span data-ttu-id="0d453-292">Например, для записи при последней обработки сайта или для хранения данных для поддержки бизнес-логикой. Задание таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-292">For example, to record when a site was last processed, or to store data to support your Timer Job business logic.</span></span> <span data-ttu-id="0d453-293">По этой причине Framework задания таймера имеет возможности управления состояние.</span><span class="sxs-lookup"><span data-stu-id="0d453-293">For this reason, the Timer Job Framework has state management capabilities.</span></span> <span data-ttu-id="0d453-294">Управление состоянием хранит и получает набор стандартных и пользовательских свойств виде строки JSON сериализованным в контейнере свойств web обработанные узла (имя = имя задания таймера + «_Properties»).</span><span class="sxs-lookup"><span data-stu-id="0d453-294">State management stores and retrieves a set of standard and custom properties as a JSON serialized string in the web property bag of the processed site (name = Timer Job name + "_Properties").</span></span> <span data-ttu-id="0d453-295">Ниже перечислены свойства по умолчанию `TimerJobRunEventArgs`объектов:</span><span class="sxs-lookup"><span data-stu-id="0d453-295">The following are the default properties of the `TimerJobRunEventArgs`object:</span></span>
- <span data-ttu-id="0d453-296">Свойство **PreviousRun** : Получает или задает дату и время предыдущей процедуры.</span><span class="sxs-lookup"><span data-stu-id="0d453-296">**PreviousRun** property: Gets or sets the date and time of the previous run.</span></span>
- <span data-ttu-id="0d453-297">Свойство **PreviousRunSuccessful** : Получает или задает значение, указывающее, успешно ли предыдущего запуска.</span><span class="sxs-lookup"><span data-stu-id="0d453-297">**PreviousRunSuccessful** property: Gets or sets a value indicating whether the previous run was successful.</span></span> <span data-ttu-id="0d453-298">Обратите внимание на то, что задание таймера автора несет ответственность за Пометка задания, как успешно завершиться, задав свойство **CurrentRunSuccessful** как часть задания таймера внедрения</span><span class="sxs-lookup"><span data-stu-id="0d453-298">Note that the Timer Job author is responsible for flagging a job run as successful by setting the **CurrentRunSuccessful** property as part of your Timer Job implementation</span></span>
- <span data-ttu-id="0d453-299">Свойство **PreviousRunVersion** : Получает или задает версию предыдущего запуска задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-299">**PreviousRunVersion** property: Gets or sets the Timer Job version of the previous run.</span></span>

<span data-ttu-id="0d453-300">Рядом с пунктом эти стандартными свойствами имеется также параметр, чтобы указать свои собственные свойства путем добавления ключевого слова - пары значение `Properties` коллекцию `TimerJobRunEventArgs`объекта.</span><span class="sxs-lookup"><span data-stu-id="0d453-300">Next to these standard properties you also have the option to specify your own properties by adding keyword - value pairs to the `Properties` collection of the `TimerJobRunEventArgs`object.</span></span> <span data-ttu-id="0d453-301">Чтобы облегчить существует три способа, которые помогут вам:</span><span class="sxs-lookup"><span data-stu-id="0d453-301">To make this easier there are three methods to help you:</span></span>
- <span data-ttu-id="0d453-302">**SetProperty** добавляет или обновляет свойство.</span><span class="sxs-lookup"><span data-stu-id="0d453-302">**SetProperty** adds or updates a property.</span></span>
- <span data-ttu-id="0d453-303">**GetProperty** возвращает значение свойства.</span><span class="sxs-lookup"><span data-stu-id="0d453-303">**GetProperty** returns the value of a property.</span></span>
- <span data-ttu-id="0d453-304">**DeleteProperty** Удаляет свойство из коллекции свойств.</span><span class="sxs-lookup"><span data-stu-id="0d453-304">**DeleteProperty** removes a property from the property collection.</span></span>

<span data-ttu-id="0d453-305">В следующем коде показано, как можно использовать управление состоянием:</span><span class="sxs-lookup"><span data-stu-id="0d453-305">The following code shows how state management can be used:</span></span>

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // grab reference to list
        library = "SiteAssets";
        List list = e.WebClientContext.Web.GetListByUrl(library);

        if (!e.GetProperty("ScriptFileVersion").Equals("1.0", StringComparison.InvariantCultureIgnoreCase))
        {
            if (list == null)
            {
                // grab reference to list
                library = "Style%20Library";
                list = e.WebClientContext.Web.GetListByUrl(library);
            }

            if (list != null)
            {
                // upload js file to list
                list.RootFolder.UploadFile("sitegovernance.js", "sitegovernance.js", true);

                e.SetProperty("ScriptFileVersion", "1.0");
            }
        }

        if (admins.Count < 2)
        {
            // Oops, we need at least 2 site collection administrators
            e.WebClientContext.Site.AddJsLink(SiteGovernanceJobKey, BuildJavaScriptUrl(e.Url, library));
            Console.WriteLine("Site {0} marked as incompliant!", e.Url);
            e.SetProperty("SiteCompliant", "false");
        }
        else
        {
            // We're all good...let's remove the notification
            e.WebClientContext.Site.DeleteJsLink(SiteGovernanceJobKey);
            Console.WriteLine("Site {0} is compliant", e.Url);
            e.SetProperty("SiteCompliant", "true");
        }

        e.CurrentRunSuccessful = true;
        e.DeleteProperty("LastError");
    }
    catch(Exception ex)
    {
        e.CurrentRunSuccessful = false;
        e.SetProperty("LastError", ex.Message);
    }
}
```

<span data-ttu-id="0d453-306">Состояние хранятся как одного JSON сериализованным свойство означает его можно использовать, а также другие настройки.</span><span class="sxs-lookup"><span data-stu-id="0d453-306">The state is stored as a single JSON serialized property which means it can be used by other customizations as well.</span></span> <span data-ttu-id="0d453-307">Например, если создавал записи состояния задания таймера «SiteCompliant = false», JavaScript подпрограммы может предложить пользователю действовать, так как задание таймера, которое определено, что сайт был incompliant.</span><span class="sxs-lookup"><span data-stu-id="0d453-307">For example, if the Timer Job wrote the state entry "SiteCompliant=false", a JavaScript routine could prompt the user to act because the Timer Job determined that the site was incompliant.</span></span>

### <a name="threading"></a><span data-ttu-id="0d453-308">Работа с потоками</span><span class="sxs-lookup"><span data-stu-id="0d453-308">Threading</span></span> ###
<span data-ttu-id="0d453-309">Framework задания таймера по умолчанию используется для параллельного выполнения рабочих потоков.</span><span class="sxs-lookup"><span data-stu-id="0d453-309">The Timer Job Framework by default uses threads to parallelize work.</span></span> <span data-ttu-id="0d453-310">Threading служит для обоих sub сайта расширения (по запросу), а также для выполнения фактических логики задания таймера (`TimerJobRun` события) для каждого сайта.</span><span class="sxs-lookup"><span data-stu-id="0d453-310">Threading is used for both the sub site expansion (when requested) and for the running the actual Timer Job logic (`TimerJobRun` event) for each site.</span></span> <span data-ttu-id="0d453-311">Следующие свойства могут быть использованы для управления реализация потоков:</span><span class="sxs-lookup"><span data-stu-id="0d453-311">The following properties can be used to control the threading implementation:</span></span>
- <span data-ttu-id="0d453-312">Свойство **UseThreading** : Получает или задает значение, указывающее, является ли threading будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="0d453-312">**UseThreading** property: Gets or sets a value indicating whether threading will be used.</span></span> <span data-ttu-id="0d453-313">По умолчанию используется значение **true**.</span><span class="sxs-lookup"><span data-stu-id="0d453-313">Defaults to **true**.</span></span>  <span data-ttu-id="0d453-314">Установите значение **false** , чтобы выполнить все действия с помощью основной поток приложения.</span><span class="sxs-lookup"><span data-stu-id="0d453-314">Set to **false** to perform all actions by using the main application thread.</span></span>
- <span data-ttu-id="0d453-315">Свойство **MaximumThreads** : Получает или задает число потоков, используемых для этого задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-315">**MaximumThreads** property: Gets or sets the number of threads to use for this Timer Job.</span></span> <span data-ttu-id="0d453-316">Допустимые значения: 2 до 100.</span><span class="sxs-lookup"><span data-stu-id="0d453-316">Valid values are 2 to 100.</span></span> <span data-ttu-id="0d453-317">Значение по умолчанию равно 5.</span><span class="sxs-lookup"><span data-stu-id="0d453-317">The default is 5.</span></span> <span data-ttu-id="0d453-318">Наличие большое количество потоков не обязательно быстрее, а затем всего несколько потоков.</span><span class="sxs-lookup"><span data-stu-id="0d453-318">Having lots of threads is not necessarily faster then having just few threads.</span></span> <span data-ttu-id="0d453-319">Оптимальное число должна быть получена посредством тестирования с использованием различных число потоков.</span><span class="sxs-lookup"><span data-stu-id="0d453-319">The optimal number should be acquired via testing using a variety of thread counts.</span></span> <span data-ttu-id="0d453-320">По умолчанию 5 потоков обнаружило значительно повысить производительность в большинстве случаев.</span><span class="sxs-lookup"><span data-stu-id="0d453-320">The default of 5 threads has been found to significantly boost performance in most scenarios.</span></span> 

#### <a name="throttling"></a><span data-ttu-id="0d453-321">Регулирование</span><span class="sxs-lookup"><span data-stu-id="0d453-321">Throttling</span></span> ####
<span data-ttu-id="0d453-322">Так как задание таймера с помощью threading и операции задания таймера, обычно выполняются операции связано со значительными затратами ресурсов, может регулирование выполнения задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-322">Because Timer Job uses threading and Timer Job operations are typically resource intensive operations, a Timer Job run could be throttled.</span></span> <span data-ttu-id="0d453-323">Чтобы правильно иметь дело с регулирование Framework задания таймера и целые использует PnP основных `ExecuteQueryRetry` метод вместо по умолчанию `ExecuteQuery`метод.</span><span class="sxs-lookup"><span data-stu-id="0d453-323">In order to correctly deal with throttling the Timer Job Framework and the whole of PnP Core uses the `ExecuteQueryRetry` method instead of the default `ExecuteQuery`method.</span></span>

<span data-ttu-id="0d453-324">**Примечание:** Необходимо использовать `ExecuteQueryRetry` в коде реализации задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-324">**Note:** It is important to use `ExecuteQueryRetry` in your Timer Job implementation code.</span></span>

#### <a name="concurrency-issues---process-all-sub-sites-of-a-site-collection-in-the-same-thread"></a><span data-ttu-id="0d453-325">Проблемы параллелизма — обрабатывать все сайты sub семейства веб-сайтов в том же потоке</span><span class="sxs-lookup"><span data-stu-id="0d453-325">Concurrency issues - process all sub sites of a site collection in the same thread</span></span> ####

<span data-ttu-id="0d453-326">Задания таймера могут возникнуть проблемы параллелизма при использовании нескольких потоков для обработки вложенных сайтов.</span><span class="sxs-lookup"><span data-stu-id="0d453-326">Timer Jobs may have concurrency issues when using multiple threads to process sub sites.</span></span> <span data-ttu-id="0d453-327">Выполните в этом примере: поток A обрабатывает первого набора sub сайты из семейства веб-сайтов 1 и поток B обрабатывает rest sub сайты из семейства веб-сайтов 1.</span><span class="sxs-lookup"><span data-stu-id="0d453-327">Take this example: Thread A processes the first set of sub sites from site collection 1, and thread B processes the rest of the sub sites from site collection 1.</span></span> <span data-ttu-id="0d453-328">Если задание таймера, которое обрабатывает веб-узла и корневого сайта (с помощью `SiteClientContext` объект), начиная с оба потока A может быть проблема параллелизма и поток B обрабатывать корневого сайта.</span><span class="sxs-lookup"><span data-stu-id="0d453-328">If the Timer Job processes the sub site and the root site (by using the `SiteClientContext` object), there could be a concurrency issue since both thread A and thread B process the root site.</span></span> <span data-ttu-id="0d453-329">Чтобы предотвратить использование параллельного проблему (без запуска задания таймера в один поток) `GetAllSubSites` метод задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-329">To avoid the concurrency issue (without running the Timer Jobs in a single thread) use the `GetAllSubSites` method within the Timer Job.</span></span>

<span data-ttu-id="0d453-330">Следующий код демонстрирует использование `GetAllSubSites` метод в рамках задания таймера:</span><span class="sxs-lookup"><span data-stu-id="0d453-330">The following code shows how to use the `GetAllSubSites` method within a Timer Job:</span></span>

```C#
public class SiteCollectionScopedJob: TimerJob
{
    public SiteCollectionScopedJob() : base("SiteCollectionScopedJob")
    {
        // ExpandSites *must* be false as we'll deal with that at TimerJobEvent level
        ExpandSubSites = false;
        TimerJobRun += SiteCollectionScopedJob_TimerJobRun;
    }

    void SiteCollectionScopedJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
    {
        // Get all the sub sites in the site we're processing
        IEnumerable<string> expandedSites = GetAllSubSites(e.SiteClientContext.Site);

        // Manually iterate over the content
        foreach (string site in expandedSites)
        {
            // Clone the existing ClientContext for the sub web
            using (ClientContext ccWeb = e.SiteClientContext.Clone(site))
            {
                // Here's the Timer Job logic, but now a single site collection is handled in a single thread which 
                // allows for further optimization or prevents race conditions
                ccWeb.Load(ccWeb.Web, s => s.Title);
                ccWeb.ExecuteQueryRetry();
                Console.WriteLine("Here: {0} - {1}", site, ccWeb.Web.Title);
            }
        }
    }
}
```

### <a name="logging"></a><span data-ttu-id="0d453-331">Ведение журнала</span><span class="sxs-lookup"><span data-stu-id="0d453-331">Logging</span></span> ###
<span data-ttu-id="0d453-332">Framework задание таймера используется ведения журнала PnP основных компонентов в его составе PnP основной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="0d453-332">The Timer Job Framework uses the PnP Core logging components as it's part of the PnP Core library.</span></span> <span data-ttu-id="0d453-333">Для активации встроенных PnP основных ведения журнала, настройте его с помощью файла соответствующие конфигурации (app.config или web.config).</span><span class="sxs-lookup"><span data-stu-id="0d453-333">To activate the built-in PnP Core logging, configure it using the appropriate config file (app.config or web.config).</span></span> <span data-ttu-id="0d453-334">В следующем примере показано требуется следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="0d453-334">The following example shows the required syntax:</span></span>

```XML
  <system.diagnostics>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="DebugListenter" type="System.Diagnostics.TextWriterTraceListener" initializeData="trace.log" />
        <!--<add name="consoleListener" type="System.Diagnostics.ConsoleTraceListener" />-->
      </listeners>
    </trace>
  </system.diagnostics>
```

<span data-ttu-id="0d453-335">С помощью выше файла конфигурации Framework задание таймера будет использовать `System.Diagnostics.TextWriterTraceListener` для записи журналов в файл с именем trace.log в ту же папку .exe задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-335">Using the above configuration file the Timer Job Framework will use the `System.Diagnostics.TextWriterTraceListener` to write logs to a file called trace.log in the same folder as the Timer Job .exe.</span></span> <span data-ttu-id="0d453-336">Например, доступны другие слушателям трассировки:</span><span class="sxs-lookup"><span data-stu-id="0d453-336">Other trace listeners are available such as:</span></span>
- <span data-ttu-id="0d453-337">**ConsoleTraceListener** записывает журналы на консоль.</span><span class="sxs-lookup"><span data-stu-id="0d453-337">**ConsoleTraceListener** writes logs to the console.</span></span>
- <span data-ttu-id="0d453-338">Способов, описанных в [Облаке Диагностика - вступили в элемент управления из ведения журналов и трассировки в Windows Azure](https://msdn.microsoft.com/en-us/magazine/ff714589.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d453-338">The method described in [Cloud Diagnostics - Take Control of Logging and Tracing in Windows Azure](https://msdn.microsoft.com/en-us/magazine/ff714589.aspx).</span></span> <span data-ttu-id="0d453-339">Этот метод используется Microsoft.WindowsAzure.Diagnostics. **DiagnosticMonitorTraceListener**.</span><span class="sxs-lookup"><span data-stu-id="0d453-339">This method uses Microsoft.WindowsAzure.Diagnostics.**DiagnosticMonitorTraceListener**.</span></span> <span data-ttu-id="0d453-340">Здесь можно найти дополнительные ресурсы Azure:</span><span class="sxs-lookup"><span data-stu-id="0d453-340">Additional Azure resources can be found here:</span></span>
    - [<span data-ttu-id="0d453-341">Включение сбора данных диагностики для веб-сайтов Azure</span><span class="sxs-lookup"><span data-stu-id="0d453-341">Enable diagnostic logging for Azure Websites</span></span>](http://azure.microsoft.com/en-us/documentation/articles/web-sites-enable-diagnostic-log/)
    - [<span data-ttu-id="0d453-342">Устранение неполадок в Azure веб-сайтов в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0d453-342">Troubleshooting Azure Websites in Visual Studio</span></span>](http://azure.microsoft.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<span data-ttu-id="0d453-343">Настоятельно рекомендуется использовать такой же подход ведения журнала для свой код задания таймера, как для Framework задания таймера.</span><span class="sxs-lookup"><span data-stu-id="0d453-343">It is strongly advised to use the same logging approach for your custom Timer Job code as you do for the Timer Job Framework.</span></span> <span data-ttu-id="0d453-344">В код задания таймера можно использовать PnP основных `Log` классов:</span><span class="sxs-lookup"><span data-stu-id="0d453-344">In your Timer Job code you can use the PnP Core `Log` class:</span></span>

```C#
void SiteGovernanceJob_TimerJobRun(object o, TimerJobRunEventArgs e)
{
    try
    {
        string library = "";

        // Get the number of admins
        var admins = e.WebClientContext.Web.GetAdministrators();

        Log.Info("SiteGovernanceJob", "ThreadID = {2} | Site {0} has {1} administrators.", e.Url, admins.Count, Thread.CurrentThread.ManagedThreadId);

        // Additional Timer Job logic...

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
