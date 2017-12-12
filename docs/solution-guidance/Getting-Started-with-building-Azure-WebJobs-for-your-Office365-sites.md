---
title: "Начало работы с azure WebJobs («задания таймера») для сайтов Office 365 #"
ms.date: 11/03/2017
ms.openlocfilehash: ec290dea670cdb0915b1f10dfc3e9a9698eb35fd
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="getting-started-with-azure-webjobs-timer-jobs-for-your-office-365-sites"></a><span data-ttu-id="6a545-102">Начало работы с azure WebJobs («задания таймера») для сайтов Office 365</span><span class="sxs-lookup"><span data-stu-id="6a545-102">Getting Started with azure WebJobs ("timer jobs") for your Office 365 Sites</span></span> #

### <a name="summary"></a><span data-ttu-id="6a545-103">Summary</span><span class="sxs-lookup"><span data-stu-id="6a545-103">Summary</span></span> ###
<span data-ttu-id="6a545-104">В этой записи будет говорить о как можно создавать WebJob Azure в качестве запланированного задания для Office 365 (или на prem должны продолжать) установки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a545-104">In this post I’ll talk about how you can build an Azure WebJob to act as a scheduled job for your Office 365 (or on-prem, should you like) SharePoint installation.</span></span> <span data-ttu-id="6a545-105">В Office 365 при запуске и использовании службы SharePoint Online, вам потребуется повторно думаете способ запуска вещей, которые используются для *задания таймера* в вашей традиционные решения фермы.</span><span class="sxs-lookup"><span data-stu-id="6a545-105">With Office 365, if you’re running and utilizing the SharePoint Online service, you’ll need to re-think the way you run the things that used to be *timer jobs* in your traditional Farm-solutions.</span></span> <span data-ttu-id="6a545-106">Понаблюдайте, пока будут рассмотрены основные понятия начало работы по построению настраиваемых заданий для сайтов Office 365.</span><span class="sxs-lookup"><span data-stu-id="6a545-106">Follow along while we walk through the basic concepts of getting started with building custom jobs for Office 365 sites.</span></span>

# <a name="introduction-to-azure-webjob-as-a-timer-job-for-your-office-365-sites"></a><span data-ttu-id="6a545-107">Общие сведения о WebJob Azure как задания таймера для сайтов Office 365</span><span class="sxs-lookup"><span data-stu-id="6a545-107">Introduction to Azure WebJob as a Timer Job for your Office 365 sites</span></span> #
<span data-ttu-id="6a545-108">В традиционных разработки SharePoint у нас есть [Задания таймера](http://tz.nu/1DNtqH8), который выполняет запланированные в фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a545-108">In traditional SharePoint development we have [Timer Jobs](http://tz.nu/1DNtqH8), which performs scheduled tasks in your SharePoint farms.</span></span> <span data-ttu-id="6a545-109">Часто используемый способ — для разработки настраиваемых задания; чтобы постоянно или несколько раз выполнять определенные задачи в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="6a545-109">A commonly used technique is to develop custom timer jobs in order to continuously or iteratively perform certain tasks in your environment.</span></span>

<span data-ttu-id="6a545-110">С помощью Office 365 и SharePoint Online у вас нет себе позволить развертывание решений фермы, которой — это обычно проживания задания таймера традиционное письмо.</span><span class="sxs-lookup"><span data-stu-id="6a545-110">With Office 365 and SharePoint Online, you don’t have the luxury to deploy your farm solutions, which is where your traditional timer jobs normally live.</span></span> <span data-ttu-id="6a545-111">Вместо этого нужно найти другой способ планирования наших задач — это приводит к концепцию [Azure WebJob](http://tz.nu/1ueFvMZ).</span><span class="sxs-lookup"><span data-stu-id="6a545-111">Instead, we have to find another way to schedule our tasks – this brings us to the concept of an [Azure WebJob](http://tz.nu/1ueFvMZ).</span></span>

## <a name="steps-for-building-the-webjob-using-visual-studio-2015-preview"></a><span data-ttu-id="6a545-112">Шаги по сборке WebJob, с помощью Visual Studio 2015 (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="6a545-112">Steps for building the WebJob using Visual Studio 2015 (Preview)</span></span>  ##
<span data-ttu-id="6a545-113">Для создания нового WebJob «с нуля», все, что для этого необходимо — создайте новое консольное приложение и убедитесь, что мы добавьте необходимые сборки в проект.</span><span class="sxs-lookup"><span data-stu-id="6a545-113">In order to build a new WebJob from scratch, all we need to do is create a new console application and make sure we add the required assemblies to the project.</span></span> <span data-ttu-id="6a545-114">В этом примере используется [Visual Studio 2015 (Предварительная версия)](http://tz.nu/1CagngX), как и предполагает его имя в настоящий момент находится в бета-версии.</span><span class="sxs-lookup"><span data-stu-id="6a545-114">In this sample I’ll use [Visual Studio 2015 (preview)](http://tz.nu/1CagngX), which as its name implies is currently in a beta release.</span></span>

### <a name="step-1-create-your-console-application"></a><span data-ttu-id="6a545-115">Шаг 1: Создание консольного приложения</span><span class="sxs-lookup"><span data-stu-id="6a545-115">Step 1: Create your console application</span></span> ###
<span data-ttu-id="6a545-116">Сначала необходимо создать новый проект и убедитесь в том, что выбран шаблон «**Консольное приложение**».</span><span class="sxs-lookup"><span data-stu-id="6a545-116">Start by creating a new project and make sure you’ve selected the "**Console Application**" template.</span></span> <span data-ttu-id="6a545-117">Кроме того и это важно, убедитесь, что вы выбрали **.NET Framework 4.5**.</span><span class="sxs-lookup"><span data-stu-id="6a545-117">Also, and this is important, make sure you've chosen **.NET Framework 4.5**!</span></span>

![Диалоговое окно Новый проект, задать создание консольного приложения, используя нотацию net Framework 4.5](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/1.Create-Console-Application.png)

### <a name="step-2-add-the-sharepoint-specific-assemblies-from-nuget"></a><span data-ttu-id="6a545-119">Шаг 2: Добавление сборки SharePoint из NuGet</span><span class="sxs-lookup"><span data-stu-id="6a545-119">Step 2: Add the SharePoint-specific assemblies from NuGet</span></span> ###
<span data-ttu-id="6a545-120">Если вы используете Visual Studio 2015 образом, диалоговое окно Диспетчер пакетов NuGet будет выглядеть незначительно отличается от предыдущих версий Visual Studio, но концепцию 's же.</span><span class="sxs-lookup"><span data-stu-id="6a545-120">If you’re using Visual Studio 2015 as I’m doing, the NuGet package manager dialog will look slightly different from earlier versions of Visual Studio, but the concept’s the same.</span></span>

 - <span data-ttu-id="6a545-121">Перейдите на «**Сервис**«->»**Диспетчер пакетов NuGet**«->»**Управление пакетами NuGet для решения...**»</span><span class="sxs-lookup"><span data-stu-id="6a545-121">Go to "**Tools**" -> "**NuGet Package Manager**" -> "**Manage NuGet Packages for Solution…**"</span></span>
 - <span data-ttu-id="6a545-122">Поиск для «**приложения для SharePoint**»</span><span class="sxs-lookup"><span data-stu-id="6a545-122">Search for "**App for SharePoint**"</span></span>
 - <span data-ttu-id="6a545-123">Установка пакета, называется «**AppForSharePointWebToolkit**» которого будет установить необходимые вспомогательные классы для работы с клиентской объектной модели SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a545-123">Install the package called "**AppForSharePointWebToolkit**" which will install the required helper classes for working with the SharePoint Client Object Model.</span></span>

<span data-ttu-id="6a545-124">![Диспетчер пакетов NuGet диалоговое окно, отображающее условия поиска, приложение для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a545-124">![The NuGet Package Manager dialog showing the search term, App for SharePoint.</span></span> <span data-ttu-id="6a545-125">Приложения для SharePoint Web Toolkit выделяется и кнопка установить готова к нажата.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/2.Add-App-For-SharePoint-Web-Toolkit-from-Nuget.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-125">App For SharePoint Web Toolkit is highlighted and the Install button is ready to be clicked.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/2.Add-App-For-SharePoint-Web-Toolkit-from-Nuget.png)</span></span>
<span data-ttu-id="6a545-126">Убедитесь, что пакет NuGet работал, проверяя, есть эти два новых классов в проект консольного приложения: ![в обозревателе решений отображается только что добавленный классы контекста точка совместный доступ и вспомогательный.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/3.Project-Overview-With-Added-Files.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-126">Make sure the NuGet package worked by making sure there’s these two new classes in your console application project: ![The Solution Explorer shows the newly added classes, Share Point Context and Token Helper.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/3.Project-Overview-With-Added-Files.png)</span></span>

### <a name="step-3-add-the-required-code-to-execute-the-job-on-your-office-365-site"></a><span data-ttu-id="6a545-127">Шаг 3: Добавление необходимых кода для выполнения задания на сайте Office 365</span><span class="sxs-lookup"><span data-stu-id="6a545-127">Step 3: Add the required code to execute the job on your Office 365 site</span></span> ###
<span data-ttu-id="6a545-128">На этом этапе мы создали наших консольного приложения и мы добавили необходимые сборки, которые легко для нас для взаимодействия с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a545-128">At this point we’ve created our Console Application and we’ve added the required assemblies that will make it easy for us to communicate with SharePoint.</span></span> <span data-ttu-id="6a545-129">Следующие действия, чтобы использовать эти классы модуля поддержки для выполнения команд в нашей среде SharePoint посредством наших консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="6a545-129">Next steps are to make use of these helper classes in order to execute commands in our SharePoint environment through our Console Application.</span></span> <span data-ttu-id="6a545-130">Установка метки.</span><span class="sxs-lookup"><span data-stu-id="6a545-130">Tag along.</span></span>

> [!NOTE] 
> <span data-ttu-id="6a545-131">В образце по завершении работы будет использоваться учетная запись + пароль подход (например, учетная запись службы).</span><span class="sxs-lookup"><span data-stu-id="6a545-131">In the finished sample I’ll be using an account+password approach (like a service account).</span></span> <span data-ttu-id="6a545-132">Мы обсудим проверки подлинности, параметры, расположенным ниже в статье извлечения и возврата ссылки на другие возможности.</span><span class="sxs-lookup"><span data-stu-id="6a545-132">We’ll discuss authentication options further down in the article and check out links to other alternatives.</span></span>

#### <a name="wire-up-the-calls-to-the-sharepoint-online-site-collection"></a><span data-ttu-id="6a545-133">Подключить вызовы семейства сайтов SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="6a545-133">Wire up the calls to the SharePoint Online site collection</span></span> ####

<span data-ttu-id="6a545-134">Следующий код демонстрирует легко подключить звонок на свой сайт, теперь, когда мы добавили вспомогательные классы из пакета наших NuGet.</span><span class="sxs-lookup"><span data-stu-id="6a545-134">The following code demonstrates how to wire up the call to your site quite easily now that we’ve added the helper classes from our NuGet package.</span></span>

```C#
 static void Main(string[] args)
  {
      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
          // Use default authentication mode
          context.AuthenticationMode = ClientAuthenticationMode.Default;
          // Specify the credentials for the account that will execute the request
          context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

          // TODO: Add your logic here!
      }
  }
 
 
  private static SecureString GetSPOSecureStringPassword()
  {
      try
      {
          Console.WriteLine(" --> Entered GetSPOSecureStringPassword()");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine(" --> Constructed the secure password");
 
          return secureString;
      }
      catch
      {
          throw;
      }
  }
 
  private static string GetSPOAccountName()
  {
      try
      {
          Console.WriteLine(" --> Entered GetSPOAccountName()");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
   }
``` 

<span data-ttu-id="6a545-135">В моем примере приложения видно, что я добавил два вспомогательных метода на извлечение имя учетной записи и пароль для учетной записи в файле app.config.</span><span class="sxs-lookup"><span data-stu-id="6a545-135">You can see in my sample application that I’ve added two helper methods for fetching the Account Name and Account Password from the app.config file.</span></span> <span data-ttu-id="6a545-136">Они рассматриваются в разделе тип проверки подлинности ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6a545-136">These are explained in the authentication-section further down in this article.</span></span>

<span data-ttu-id="6a545-137">Для метода главного это все мы потребуется подключить действия до нашей портала.</span><span class="sxs-lookup"><span data-stu-id="6a545-137">As for the main method, that’s all we need to wire things up to our portal.</span></span> <span data-ttu-id="6a545-138">Прежде чем мы узнать подробнее как можно управлять SharePoint из кода, давайте рассмотрим параметры проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6a545-138">Before we dig deeper into how we can manipulate SharePoint from our code, let’s discuss options for authentication.</span></span>

## <a name="authentication-considerations"></a><span data-ttu-id="6a545-139">Сведения о выполнении проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="6a545-139">Authentication considerations</span></span> ##
<span data-ttu-id="6a545-140">Мы будем извлечь два варианта проверки подлинности и посмотрите, их отличий.</span><span class="sxs-lookup"><span data-stu-id="6a545-140">We’ll check out two options for authentication and see how they differ.</span></span> <span data-ttu-id="6a545-141">Могут возникать и другие параметры проверки подлинности в будущем, но ниже приведены два часто используемые подхода.</span><span class="sxs-lookup"><span data-stu-id="6a545-141">There may be other options for authentication down the road, but here are two commonly used approaches.</span></span>

### <a name="option-1-use-a-service-account-username--password"></a><span data-ttu-id="6a545-142">Вариант 1: Использование учетной записи службы (имя пользователя + пароль)</span><span class="sxs-lookup"><span data-stu-id="6a545-142">Option 1: Use a Service Account (Username + Password)</span></span> ###
<span data-ttu-id="6a545-143">Этот подход довольно прост и позволяет просто введите учетную запись и пароль в клиент Office 365 и затем использовать для примера CSOM для выполнения кода на веб-узлы.</span><span class="sxs-lookup"><span data-stu-id="6a545-143">This approach is pretty straight forward and enables you to simply enter an account and password to your Office 365 tenant and then use for example CSOM to execute code on your sites.</span></span> <span data-ttu-id="6a545-144">Это, отображаемые в примере кода выше также.</span><span class="sxs-lookup"><span data-stu-id="6a545-144">This is what you see in my sample code above as well.</span></span>

#### <a name="create-a-new-service-account-in-office-365"></a><span data-ttu-id="6a545-145">Создание новой учетной записи службы в Office 365</span><span class="sxs-lookup"><span data-stu-id="6a545-145">Create a new Service Account in Office 365</span></span> ####
<span data-ttu-id="6a545-146">В порядке для работы конкретной учетной записи должен быть создан, который выступает в качестве учетной записи службы — для этого конкретного приложения или универсальные приложения учетную запись, можно использовать все задачи и службы.</span><span class="sxs-lookup"><span data-stu-id="6a545-146">In order for this to work a specific account should be created that acts as a service account – either for this specific application or a generic service application account that all your jobs and services can use.</span></span>

<span data-ttu-id="6a545-147">Для этой демонстрации я создал новую учетную запись, называется «**SP WebJob**»: ![панель мониторинга показывает только что созданная учетная запись WebJob пакета обновления.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/4.Service-Account-Overview.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-147">For the sake of this demo, I’ve created a new account called "**SP WebJob**": ![The dashboard shows the newly created SP WebJob account.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/4.Service-Account-Overview.png)</span></span>

<span data-ttu-id="6a545-148">В зависимости от разрешений задание должно иметь, необходимо изменить разрешения учетной записи при его создании.</span><span class="sxs-lookup"><span data-stu-id="6a545-148">Depending on what permissions the job should have, you will have to edit the permissions of the account when you set it up.</span></span>

#### <a name="store-credentials-in-your-appconfig"></a><span data-ttu-id="6a545-149">Хранение учетных данных в файле app.config</span><span class="sxs-lookup"><span data-stu-id="6a545-149">Store credentials in your app.config</span></span> ####
<span data-ttu-id="6a545-150">В файле app.config проекта можно указать учетные данные, они будут легко fetchable из исполняемый файл программы.</span><span class="sxs-lookup"><span data-stu-id="6a545-150">Within your project’s app.config file you can specify the credentials so they’re easily fetchable from the code executable.</span></span> <span data-ttu-id="6a545-151">Это выглядит как Мои app.config:</span><span class="sxs-lookup"><span data-stu-id="6a545-151">This is what my app.config looks like:</span></span>
```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
 <startup> 
   <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
 </startup>
 <appSettings>
   <add key="SPOAccount" value="spwebjob@redacted.onmicrosoft.com"/>
   <add key="SPOPassword" value="redacted"/>
 </appSettings>
</configuration>

```
<span data-ttu-id="6a545-152">Можно просмотреть два параметра в файле App.config:</span><span class="sxs-lookup"><span data-stu-id="6a545-152">You can see the two settings in the App.config:</span></span>

 - <span data-ttu-id="6a545-153">SPOAccount</span><span class="sxs-lookup"><span data-stu-id="6a545-153">SPOAccount</span></span>
 - <span data-ttu-id="6a545-154">SPOPassword</span><span class="sxs-lookup"><span data-stu-id="6a545-154">SPOPassword</span></span>

<span data-ttu-id="6a545-155">При просмотре в первом фрагменте кода я извлечение эти параметры в файле app.config.</span><span class="sxs-lookup"><span data-stu-id="6a545-155">If you review the first code snippet, I’m fetching these settings from the app.config file.</span></span> <span data-ttu-id="6a545-156">Имейте в виду, что это означает, что хранения имя учетной записи и пароль в виде простого текста в файле app.config. Необходимо принять решение в проекты как и место для хранения и защиты паролей, следует выбрать этот подход.</span><span class="sxs-lookup"><span data-stu-id="6a545-156">Just keep in mind that this means storing the account name and password in clear text in your app.config. You need to make a decision in your own projects for how and where to store and protect your passwords, should you choose this approach.</span></span>

#### <a name="the-job-runs-under-the-specified-account"></a><span data-ttu-id="6a545-157">Задание выполняется от имени указанной учетной записи</span><span class="sxs-lookup"><span data-stu-id="6a545-157">The job runs under the specified account</span></span> ####
<span data-ttu-id="6a545-158">Когда приложение запускается, вы увидите, что он выполняется с помощью учетной записи, указанной в конструкторе SharePointOnlineCredentials():</span><span class="sxs-lookup"><span data-stu-id="6a545-158">Once the application runs, you will see that it runs using the account specified in the SharePointOnlineCredentials() constructor:</span></span>

![В журнале автоматического перевода отображаются четыре атрибутами, WebJob (SP2) для перевода текста.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/5.Running-Job-Overview.png)

<span data-ttu-id="6a545-160">В моем примере выше я отображение WebJob, выполняемого действия для настраиваемого списка в одной из личных сайтов, размещенных в SharePoint Online семейство личных сайтов.</span><span class="sxs-lookup"><span data-stu-id="6a545-160">In my sample above I’m showing a WebJob that is executing actions on a custom list in one of my sites hosted in my SharePoint Online site collection.</span></span>

<span data-ttu-id="6a545-161">Таким образом можно получить хорошее отслеживания изменений в портал, выполняемой наших учетной записи службы.</span><span class="sxs-lookup"><span data-stu-id="6a545-161">Because of this, we can get a pretty good traceability of changes in the portal performed by our service account.</span></span> <span data-ttu-id="6a545-162">Поэтому важно нужен серьезный подход — имя учетной записи все будут знать, что изменения были автоматически производится наша служба просто, посмотрев метаданных изменены создан.</span><span class="sxs-lookup"><span data-stu-id="6a545-162">This is why its important to name the account wisely – everyone will know that the modifications were done automatically by our service simply by looking at the modified/created metadata.</span></span>

### <a name="option-2-use-oauth-and-include-authentication-tokens-in-your-requests-to-avoid-specifying-accountpassword"></a><span data-ttu-id="6a545-163">Вариант 2: Использование OAuth и включить маркеры проверки подлинности в запросов не следует использовать учетную запись и пароль</span><span class="sxs-lookup"><span data-stu-id="6a545-163">Option 2: Use OAuth and include authentication tokens in your requests to avoid specifying account/password</span></span> ###
<span data-ttu-id="6a545-164">Это были подробно описаны в эффективной, мой друг [Кирк Петров](http://blogs.msdn.com/b/kaevans/) в корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="6a545-164">This has been explained in great detail by my friend [Kirk Evans](http://blogs.msdn.com/b/kaevans/) at Microsoft.</span></span>

<span data-ttu-id="6a545-165">В его учет называемое «[построение надстройки SharePoint как задания таймера](http://tz.nu/1xBA76K)» он объясняется, как можно использовать и проход по access маркеры во избежание настройки имя пользователя и пароль, как я описанного выше, в случае, если вы не хотите хранить пароли и учетные данные в ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="6a545-165">In his post called "[Building a SharePoint Add-in as a Timer Job](http://tz.nu/1xBA76K)" he explains how you can utilize and pass along the access tokens in order to avoid username/password setups like I explained above, in case you don't want to store the passwords and credentials in your application.</span></span>

## <a name="extending-the-code-with-some-csom-magic"></a><span data-ttu-id="6a545-166">Расширение кода некоторые снег CSOM</span><span class="sxs-lookup"><span data-stu-id="6a545-166">Extending the code with some CSOM magic</span></span> ##
<span data-ttu-id="6a545-167">На этом этапе мы иметь рабочее консольного приложения, который может выполнять проверку подлинности и выполнения запросов к сайтам Office 365.</span><span class="sxs-lookup"><span data-stu-id="6a545-167">At this point we have a working Console Application which can authenticate and execute requests to your Office 365 sites.</span></span> <span data-ttu-id="6a545-168">Фигурном ничего не выполнено в коде, поэтому здесь приводится фрагмент для сбора некоторые данные из списка называется «Автоматическое переводы», создавшего я и логики кода будут видеть, есть ли все элементы списка, которые еще не были переведены и затем оно будет выполнения вызова службы перевода и перевода текста для требуемого языка.</span><span class="sxs-lookup"><span data-stu-id="6a545-168">Nothing fancy has been done in the code yet, so here’s a sample snippet for pulling out some information from a list called "Automatic Translations" that I have created, and the code logic will see if there’s any items in the list that haven’t been translated and then it’ll execute a call to a translation-service and translate the text to the desired output language.</span></span>
```C#
static void Main(string[] args)
{
   try
   {
      Console.WriteLine("Initiating Main()");

      using (ClientContext context = new ClientContext("https://redacted.sharepoint.com"))
      {
         Console.WriteLine("New ClientContext('https://redacted.sharepoint.com') opened. ");

         context.AuthenticationMode = ClientAuthenticationMode.Default;
         context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());

         Console.WriteLine("Authentication Mode and Credentials configured");

         List translationlist = context.Web.Lists.GetByTitle("Automatic Translations");
         context.Load(translationlist);
         context.ExecuteQuery();

         Console.WriteLine("TranslationList fetched, loaded and ExecuteQuery'ed");

         if (translationlist != null && translationlist.ItemCount > 0)
         {
             Console.WriteLine("The list exist, let's do some magic");

             CamlQuery camlQuery = new CamlQuery();
             camlQuery.ViewXml =
             @"<View>  
             <Query> 
                 <Where><Eq><FieldRef Name='IsTranslated' /><Value Type='Boolean'>0</Value></Eq></Where> 
             </Query> 
         </View>";

             ListItemCollection listItems = translationlist.GetItems(camlQuery);
             context.Load(listItems);
             context.ExecuteQuery();

             Console.WriteLine("Query for listItems executed.");

             foreach (ListItem item in listItems)
             {
                 item["Output"] = TranslatorHelper.GetTranslation(item["Title"], item["Target Language"], item["Original Language"]);
                 item["IsTranslated"] = true;
                 item.Update();
             }


             context.ExecuteQuery();
             Console.WriteLine("Updated all the list items we found. Carry on...");
         }
      }
   }
   catch (Exception ex)
   {
       Console.WriteLine("ERROR: " + ex.Message);
       Console.WriteLine("ERROR: " + ex.Source);
       Console.WriteLine("ERROR: " + ex.StackTrace);
       Console.WriteLine("ERROR: " + ex.InnerException);
   }
}

```
<span data-ttu-id="6a545-169">Класс **TranslatorHelper** является также вспомогательным классом, который вызывает пользовательский перевода API, но он не обсуждаются подробно в этой записи поскольку это довольно далеко не из области действия.</span><span class="sxs-lookup"><span data-stu-id="6a545-169">The **TranslatorHelper** class is a helper class which calls a custom translation API but it will not be discussed in detail in this post since it's pretty far outside of the scope.</span></span>

> [!NOTE] 
> <span data-ttu-id="6a545-170">По результатам из кода, это демонстрационный ролик, определенно не для рабочей среды, пожалуйста, измените его и корректировка по безопасности и стандартов программирования принципы.</span><span class="sxs-lookup"><span data-stu-id="6a545-170">As seen from the code this is a demo and definitely not for production use, please revise it and adjust according to your coding standards and security principles.</span></span> <span data-ttu-id="6a545-171">Однако все дополнения Console.WriteLine добавляются в порядке для "мне нравится" для просмотра выполнение заданий легко из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="6a545-171">However all the Console.WriteLine additions are added in order for us to review the execution of the jobs easily from the Azure Portal.</span></span> <span data-ttu-id="6a545-172">Дополнительные сведения о регистрации и мониторинга ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6a545-172">More on logging and monitoring further down in this article.</span></span>

## <a name="publishing-your-webjob-to-azure"></a><span data-ttu-id="6a545-173">Публикация вашего WebJob в Azure</span><span class="sxs-lookup"><span data-stu-id="6a545-173">Publishing your WebJob to Azure</span></span> ##
<span data-ttu-id="6a545-174">Когда вы разработали вашей WebJob и вы готовы к развертыванию в среде Azure (развертывание на веб-сайт Azure), у вас есть две основные параметры как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="6a545-174">When you’ve developed your WebJob and you’re ready to deploy it to your Azure environment (deploys to an Azure WebSite), you have two main options as described below.</span></span>

### <a name="option-1-upload-a-zip-file-with-the-webjob-binaries-to-your-azure-portal"></a><span data-ttu-id="6a545-175">Вариант 1: Загрузите ZIP-файл с двоичными файлами WebJob в портал Azure</span><span class="sxs-lookup"><span data-stu-id="6a545-175">Option 1: Upload a zip file with the WebJob binaries to your Azure Portal</span></span> ###
<span data-ttu-id="6a545-176">Использование портала Azure, где все вашей awesomeness хранить в Azure, можно будет загрузить zip файл, содержащий выходные данные построения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a545-176">Using the Azure Portal where you keep all of your awesomeness in Azure, you can upload a zip-file containing the output from Visual Studio’s build.</span></span> <span data-ttu-id="6a545-177">Это удобный способ компиляции и доставки кода другому человеку пользователей, которые будут выполнять развертывание для вас.</span><span class="sxs-lookup"><span data-stu-id="6a545-177">This is an easy way for compiling and shipping your code to someone else who will do the deployment for you.</span></span>

#### <a name="create-the-zip-file"></a><span data-ttu-id="6a545-178">Создание ZIP-файла</span><span class="sxs-lookup"><span data-stu-id="6a545-178">Create the zip file</span></span> ####
<span data-ttu-id="6a545-179">Просто скопировать все, что построение выходные файлы из Visual Studio (обычно в папке bin/Debug или bin/Release):</span><span class="sxs-lookup"><span data-stu-id="6a545-179">Simply grab all the output files from your Visual Studio build (normally in your bin/Debug or bin/Release folder):</span></span>

<span data-ttu-id="6a545-180">![Откроется представление проводника Windows из папки bin/Debug.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/6.Zip-File-Overview.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-180">![A Windows Explorer view of the bin/Debug folder is displayed.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/6.Zip-File-Overview.png)</span></span>
<span data-ttu-id="6a545-181">Сжать их, поэтому вы получите замечательно ZIP-файл для задания web:</span><span class="sxs-lookup"><span data-stu-id="6a545-181">Compress them so you’ll get a nice Zip file for your web job:</span></span>

![Откроется представление проводника Windows из завершенных ZIP-файл.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/7.Zip-File-Created.png)

#### <a name="find-a-web-site-where-the-job-should-be-deployed"></a><span data-ttu-id="6a545-183">Найдите веб-сайт, где должны развертываться задания</span><span class="sxs-lookup"><span data-stu-id="6a545-183">Find a web site where the job should be deployed</span></span> ####

<span data-ttu-id="6a545-184">Итак, теперь у вас есть пакет.</span><span class="sxs-lookup"><span data-stu-id="6a545-184">Okay, so you’ve got your package.</span></span> <span data-ttu-id="6a545-185">Это довольно легко.</span><span class="sxs-lookup"><span data-stu-id="6a545-185">That’s easy enough.</span></span> <span data-ttu-id="6a545-186">Следующим шагом является заголовок вход в систему https://portal.azure.com и входа в систему на портале Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="6a545-186">Next step is to head on to https://portal.azure.com and login to your Windows Azure Portal.</span></span> <span data-ttu-id="6a545-187">Отсюда вам потребуется создать новый веб-сайт или использовать существующее — этот веб-сайт будет узла для нашего web задания.</span><span class="sxs-lookup"><span data-stu-id="6a545-187">From there you’ll need to either create a new web site, or use an existing one – this website will be the host for our web job.</span></span>

<span data-ttu-id="6a545-188">В моем случае у меня уже есть веб-сайта Azure для некоторых демонстрационных Мой Office 365 так просто используете его.</span><span class="sxs-lookup"><span data-stu-id="6a545-188">In my case, I already have an Azure WebSite for some of my Office 365 demos so I’ll just use that one.</span></span>

<span data-ttu-id="6a545-189">Прокрутите вниз в области Параметры для веб-сайта можно найти так называемых «**WebJobs**» в разделе «**операции**» заголовок:</span><span class="sxs-lookup"><span data-stu-id="6a545-189">If you scroll down in the settings pane for your website, you’ll find a something called "**WebJobs**" under the "**Operations**" header:</span></span>

<span data-ttu-id="6a545-190">![Портал Azure автора отображается со стрелкой WebJobs. ](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/8.Find-WebJobs-in-Azure-Portal.png)
 **Click, где стрелка!**</span><span class="sxs-lookup"><span data-stu-id="6a545-190">![The author's Azure Portal is displayed, with an arrow pointing to WebJobs.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/8.Find-WebJobs-in-Azure-Portal.png)
**Click where the arrow points!**</span></span>

#### <a name="upload-your-webjob"></a><span data-ttu-id="6a545-191">Отправка ваше WebJob</span><span class="sxs-lookup"><span data-stu-id="6a545-191">Upload your WebJob</span></span> ####

<span data-ttu-id="6a545-192">Загрузите свою работу в web, нажав кнопку входа **[+ Добавить]** :</span><span class="sxs-lookup"><span data-stu-id="6a545-192">Upload your web job by clicking the **[+ Add]** sign:</span></span>

![Портал WebJobs Azure отображается со стрелкой добавить.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/9.Upload-Azure-WebJob-from-Azure-Portal.png)

<span data-ttu-id="6a545-194">Выберите имя, как выполняется задание и фактических ZIP-файла:</span><span class="sxs-lookup"><span data-stu-id="6a545-194">Choose a Name, how the job should run and the actual zip file:</span></span>

![Откроется диалоговое окно Добавление WebJob.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/10.Configure-Name-of-Uploaded-WebJob.png)

> [!IMPORTANT] 
> <span data-ttu-id="6a545-197">На этом этапе альтернатива «Для выполнения» только обеспечивает «По требованию» или «Продолжить», но скоро будет поддержка «Расписание» также – которого — это действительно необходимо.</span><span class="sxs-lookup"><span data-stu-id="6a545-197">The "How To Run" alternative only offers "On Demand" or "Continuous" at this point, but soon there will be support for "Scheduled" as well – which is what we really want.</span></span>

<span data-ttu-id="6a545-198">*(Подсказка: В следующем разделе для публикации на самом Azure, можно запланировать его из внутри VS).*</span><span class="sxs-lookup"><span data-stu-id="6a545-198">*(Hint: In the next section for publishing directly from Azure, you can schedule it from inside VS).*</span></span>

<span data-ttu-id="6a545-199">Да выполнить – теперь можно запустить вашей webjob через портал Azure:</span><span class="sxs-lookup"><span data-stu-id="6a545-199">Okay, done – you can now run your webjob from your Azure Portal:</span></span>

![Портал WebJobs Azure отображается со списком новых заданий.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/11.Run-WebJob-from-Azure-Portal.png)

<span data-ttu-id="6a545-202">Хотя это все нормально и замечательно, поскольку портала отсутствуют диалоговые окна для поддержки планирования пока — я бы настоятельно рекомендуется извлечь как опубликовать из внутри Visual Studio 2015 вместо (или 2013, если это ваш выбор).</span><span class="sxs-lookup"><span data-stu-id="6a545-202">While this is all fine and dandy, since the portal doesn’t have the dialogs for supporting scheduling just yet – I would urge you to check out how to publish from inside Visual Studio 2015 instead (or 2013, if that’s your choice).</span></span>

### <a name="option-2-publish-directly-to-azure-from-visual-studio"></a><span data-ttu-id="6a545-203">Вариант 2: Публикация непосредственно в Azure из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6a545-203">Option 2: Publish directly to Azure from Visual Studio</span></span> ###
<span data-ttu-id="6a545-204">Это Мои избранные один на этом этапе так, как я могу использовать инструментарий в Visual Studio для быстро публиковать все изменения непосредственно в моей размещенной службы.</span><span class="sxs-lookup"><span data-stu-id="6a545-204">This is my favorite one at this point because I can use the tooling in Visual Studio to quickly publish any changes directly to my hosted service.</span></span> <span data-ttu-id="6a545-205">Другие преимущество станет снимите флажок ближайшее время, как можно планировать задания точно способ для выполнения непосредственно из диалоговых окон в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a545-205">The other benefit will become clear soon, as you can also schedule the job exactly how you want it to execute directly from the dialogs in Visual Studio.</span></span>

#### <a name="choose-to-publish-the-webjob-from-visual-studio-2015"></a><span data-ttu-id="6a545-206">Выберите публикация WebJob из Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="6a545-206">Choose to publish the WebJob from Visual Studio 2015</span></span> ####

> [!NOTE] 
> <span data-ttu-id="6a545-207">Эти диалоговые окна может немного отличаться, если вы используете более ранней версии Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a545-207">These dialogs may differ slightly if you’re running an earlier version of Visual Studio.</span></span> <span data-ttu-id="6a545-208">Кроме того я уже вошел, если вы выполняете это в первый раз появляется диалоговое окно входа для входа в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6a545-208">Also, I am already logged in so if you’re doing this for the first time you may get a login-dialog in order to sign in to your Azure account.</span></span> <span data-ttu-id="6a545-209">Это связано с подготовкой.</span><span class="sxs-lookup"><span data-stu-id="6a545-209">That’s a pre-requisite.</span></span>

<span data-ttu-id="6a545-210">Просто щелкните правой кнопкой мыши проект и выберите пункт «**Публикация Azure WebJob...**»:</span><span class="sxs-lookup"><span data-stu-id="6a545-210">Simply right-click your project and select "**Publish as an Azure WebJob…**":</span></span>

![В контекстном меню в окне Обозреватель решений будет отображаться с публикация Azure WebJob выделенным параметром.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/12.Publish-WebJob-from-Visual-Studio-2015.png)

#### <a name="add-azure-webjob"></a><span data-ttu-id="6a545-212">Добавление Azure WebJob</span><span class="sxs-lookup"><span data-stu-id="6a545-212">Add Azure WebJob</span></span> ####
<span data-ttu-id="6a545-213">Откроется в диалоговом окне нового там, где можно настроить задания, а так как мы хотели повторяющегося задания, которое должно выполняться по расписанию (в моем случае один раз каждую ночь) можно настроить расписание непосредственно из диалоговых окон: ![displ — это диалоговое окно Добавление WebJob Azure ayed.</span><span class="sxs-lookup"><span data-stu-id="6a545-213">This will bring you to a new dialog where you can configure the job, and since we want a recurring job that should be executed on a schedule (in my case once every night) you can configure the schedule directly from the dialogs: ![The Add Azure WebJob dialog is displayed.</span></span> <span data-ttu-id="6a545-214">В поле имя WebJob содержит текст Zimmergren O365 WebJobSample, в поле режим запуска WebJob содержит параметр выполнения по расписанию, повторяющееся поле содержит задания типовой параметр и установлен флажок Нет даты окончания, повторять каждое поле установлено значение 1 дня , а начальную дату — 9 Januari 2015.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/13.Add-Azure-WebJob-Dialog.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-214">The WebJob name field contains the text Zimmergren-O365-WebJobSample, the WebJob run mode field contains the option Run on a Schedule, the Recurrence field contains the option Recurring job and the check box No end date is checked, the Recur every field is set to 1 days, and the Starting on date is 9 Januari 2015.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/13.Add-Azure-WebJob-Dialog.png)</span></span>

 - <span data-ttu-id="6a545-215">Убедитесь, что имя является понятное веб-сайт</span><span class="sxs-lookup"><span data-stu-id="6a545-215">Make sure the name is web friendly</span></span>
 - <span data-ttu-id="6a545-216">Режим выполнения, я на «Запуск расписание», так как требуется, чтобы оно только на определенное время каждый день</span><span class="sxs-lookup"><span data-stu-id="6a545-216">Select your run mode, I’m on "Run on a Schedule" because we want to have it occur on a specific time every day</span></span>
 - <span data-ttu-id="6a545-217">Задание должно быть повторяющееся задание или разовое задание?</span><span class="sxs-lookup"><span data-stu-id="6a545-217">Should the job be a recurring job or a one-time job?</span></span> <span data-ttu-id="6a545-218">Поскольку необходимо моделирования задания таймера, он должен быть повторяющаяся, и в моем случае без любая Дата завершения, так как она будет запущена каждую ночь</span><span class="sxs-lookup"><span data-stu-id="6a545-218">Since we want to simulate a Timer Job it needs to be recurring, and in my case without any end date since it’ll be running every night</span></span>
 - <span data-ttu-id="6a545-219">Вы хотите, можно планировать повторения вниз до каждую минуту.</span><span class="sxs-lookup"><span data-stu-id="6a545-219">You can schedule the recurrence down to every minute, should you want.</span></span>
 - <span data-ttu-id="6a545-220">Когда нужно начинать?</span><span class="sxs-lookup"><span data-stu-id="6a545-220">When do we start?</span></span> <span data-ttu-id="6a545-221">:-)</span><span class="sxs-lookup"><span data-stu-id="6a545-221"></span></span>

<span data-ttu-id="6a545-222">Счетчик **ОК** и вы увидите, что Visual Studio уменьшится сообщение «**Установка WebJobs публикации NuGet пакет**».</span><span class="sxs-lookup"><span data-stu-id="6a545-222">Hit **OK** and you’ll see that Visual Studio will drop you a message saying "**Installing WebJobs Publishing NuGet Package**".</span></span>

#### <a name="visual-studio-added-webjobs-publishing-nuget-package"></a><span data-ttu-id="6a545-223">Visual Studio добавлены WebJobs публикации NuGet-пакет</span><span class="sxs-lookup"><span data-stu-id="6a545-223">Visual Studio added WebJobs Publishing NuGet Package</span></span> ####
![Отображается диалоговое окно WebJobs NuGet пакет установки, которое отображает счетчик и текст, установка WebJobs публикации NuGet пакета.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/14.WebJobs-NuGet-Package-Install.png)

<span data-ttu-id="6a545-225">Это фактически добавляет новый файл с именем «**Публикация settings.json webjob**» для проектов, содержащий конфигурации для задания.</span><span class="sxs-lookup"><span data-stu-id="6a545-225">This actually adds a new file called "**webjob-publish-settings.json**" to our project, containing the configuration for the job.</span></span>

<span data-ttu-id="6a545-226">Файл выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6a545-226">The file looks like this:</span></span>
```json
{
  "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
  "webJobName": "Zimmergren-O365-WebJobSample",
  "startTime": "2015-01-09T01:00:00+01:00",
  "endTime": null,
  "jobRecurrenceFrequency": "Day",
  "interval": 1,
  "runMode": "Scheduled"
}
```
<span data-ttu-id="6a545-227">Права не требуется беспокоить с помощью данного файла в данный момент, поскольку уже предназначена планирования с помощью диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="6a545-227">Right, we don’t need to bother with this file at the moment since we already designed the scheduling using the dialogs.</span></span>

#### <a name="select-publishingdeployment-target"></a><span data-ttu-id="6a545-228">Выбор целевого публикации и развертывание</span><span class="sxs-lookup"><span data-stu-id="6a545-228">Select publishing/deployment target</span></span> ####
<span data-ttu-id="6a545-229">Следующим шагом в диалоговом окне будет места публикации/развертывания вашей WebJob.</span><span class="sxs-lookup"><span data-stu-id="6a545-229">The next step in the dialog will be where to publish/deploy your WebJob.</span></span> <span data-ttu-id="6a545-230">Можно импортировать профиль публикации или выберите веб-узлов Microsoft Azure для проверки подлинности и выберите один из существующих сайтов.</span><span class="sxs-lookup"><span data-stu-id="6a545-230">You can either import a publishing profile or select Microsoft Azure WebSites in order to authenticate and select one of your existing sites.</span></span>

<span data-ttu-id="6a545-231">Поскольку у меня правило всегда загрузка Мои публикации профили из портала личных Azure я будет пойти дальше и выберите «**Импорт**» и просто указать публикации файла профиля, который я загружен из личных веб-сайта Azure:</span><span class="sxs-lookup"><span data-stu-id="6a545-231">Since I’ve got a habit of always downloading my publishing profiles from my Azure Portal, I’ll go ahead and select "**Import**" and simply specify the publishing profile file that I’ve downloaded from my Azure website:</span></span>

![На вкладке подключения к видимым отображается диалоговое окно Публикация веб-сайта.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/15.Publish-Web-Dialog.png)

<span data-ttu-id="6a545-233">После этого все, что для этого необходимо — нажмите кнопку «Опубликовать».</span><span class="sxs-lookup"><span data-stu-id="6a545-233">With that done, all we need to do is click the button called "Publish".</span></span> <span data-ttu-id="6a545-234">Не следует бояться, оно не байтового.</span><span class="sxs-lookup"><span data-stu-id="6a545-234">Don’t be afraid, it wont bite.</span></span> <span data-ttu-id="6a545-235">Я думаю.</span><span class="sxs-lookup"><span data-stu-id="6a545-235">I think.</span></span>

#### <a name="publish"></a><span data-ttu-id="6a545-236">Публикация</span><span class="sxs-lookup"><span data-stu-id="6a545-236">Publish</span></span> ####
<span data-ttu-id="6a545-237">После нажатия кнопки Опубликовать диалоговое окно Публикация веб-трафик будет отображать ход выполнения задания Web развертывания: ![диалоговое окно, отображается действие опубликовать Web.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/16.Publish-Progress-Visual-Studio-2015.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-237">Once you hit Publish, the Web Publish Activity dialog will display the progress of your Web Job deployment: ![The dialog Web Publish Activity is displayed.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/16.Publish-Progress-Visual-Studio-2015.png)</span></span>

<span data-ttu-id="6a545-238">После завершения, вы должны увидеть WebJob в портал Azure: ![портала Azure отображается Zimmergren O365 WebJobSample в списке WebJobs в состоянии, завершения 2 минут назад.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/17.Web-Job-Published-as-seen-in-Azure-Portal.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-238">Once it’s done, you should see the WebJob in your Azure Portal: ![The Azure Portal shows Zimmergren-O365-WebJobSample in the list of WebJobs with the status of, Completed 2 min ago.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/17.Web-Job-Published-as-seen-in-Azure-Portal.png)</span></span>

<span data-ttu-id="6a545-239">Состояние WebJob теперь отображается как завершено.</span><span class="sxs-lookup"><span data-stu-id="6a545-239">The WebJob status is now displayed as Completed.</span></span> <span data-ttu-id="6a545-240">Он будет сказать сбоев и сообщений об ошибках, если он будет любой необработанное исключение или для предоставления неработоспособные поведение.</span><span class="sxs-lookup"><span data-stu-id="6a545-240">It would say failure/error if it would throw any unhandled exceptions or otherwise provide unhealthy behavior.</span></span>

<span data-ttu-id="6a545-241">По-прежнему написано «По запросу», но это задание выполняется один раз каждый час теперь.</span><span class="sxs-lookup"><span data-stu-id="6a545-241">It still says "On Demand", but this job actually runs once every hour now.</span></span>

## <a name="monitoring-the-job-and-reviewing-logs"></a><span data-ttu-id="6a545-242">Мониторинг задания и просмотра журналов</span><span class="sxs-lookup"><span data-stu-id="6a545-242">Monitoring the job and reviewing logs</span></span> ##
<span data-ttu-id="6a545-243">Если вы сделали все предыдущие действия, у вас работают как запланированная задача в облаке, задание для выполнения действий к вашей сайтов Office 365.</span><span class="sxs-lookup"><span data-stu-id="6a545-243">If you’ve done all the previous steps, you’ve got a job working for you as a scheduled task in the cloud, performing actions toward your Office 365 site(s).</span></span>

### <a name="view-all-job-executions-and-status"></a><span data-ttu-id="6a545-244">Просмотр всех заданий выполнений и состояния</span><span class="sxs-lookup"><span data-stu-id="6a545-244">View all job executions and status</span></span> ###
<span data-ttu-id="6a545-245">Если вы хотите просмотреть после последнего запуска задания, что результат каждого выполнения задания был или просмотрите, что происходит во время выполнения задания, можно нажать ссылку в разделе «Журналы», когда вы находитесь в обзоре WebJobs: ![WebJobs диалогового окна , со стрелкой на ссылку журналы.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/18.View-All-WebJobs-and-status-of-execution.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-245">If you want to review when the job last ran, what the outcome of every execution of the job was or review what happened during execution of the job, you can click on the link under "Logs" when you’re in the WebJobs overview: ![The WebJobs dialog, with an arrow pointing to the Logs link.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/18.View-All-WebJobs-and-status-of-execution.png)</span></span>

<span data-ttu-id="6a545-246">Это позволит получить общие сведения о всех выполнений выбранные задания, включая /outcome состояние:</span><span class="sxs-lookup"><span data-stu-id="6a545-246">This will give you an overview of all the executions of the selected jobs, including the status /outcome:</span></span>

![Сведения о WebJob, включая последние задание выполняется.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/19.WebJob-Details-Overview.png)

<span data-ttu-id="6a545-248">Щелкнув выделенную ссылку, можно пойти в выполнении конкретного просмотрите журналы задания и гарантировать правильность выглядеть нормально.</span><span class="sxs-lookup"><span data-stu-id="6a545-248">By clicking the highlighted link, you can dig down into a specific execution to review the logs of the job and make sure things look okay.</span></span> <span data-ttu-id="6a545-249">Это возможно, являются более качественных, если задания в действительности вызывает ошибку, и требуется проверить, что случилось, или если результата задания неправильные или не соответствует ожидаемому.</span><span class="sxs-lookup"><span data-stu-id="6a545-249">This is probably more relevant if the job actually caused an error and you needed to investigate what went wrong, or if the outcome of the job is incorrect or not as expected.</span></span>

<span data-ttu-id="6a545-250">Также можно увидеть, что операторы Console.WriteLine, поэтому хорошо использованные в Мои консольного приложения для этой демонстрации теперь отображается в журнале выполнения задания:</span><span class="sxs-lookup"><span data-stu-id="6a545-250">You can also see that the Console.WriteLine statements that I so nicely used in my Console Application for this demo now shows up in the job execution log:</span></span>

![Сведения о WebJob, отображение строки в файл журнала.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/20.Review-Logs-and-Monitor-WebJob-Execution.png)

## <a name="tips--tricks"></a><span data-ttu-id="6a545-252">Советы и рекомендации</span><span class="sxs-lookup"><span data-stu-id="6a545-252">Tips & Tricks</span></span> ##
<span data-ttu-id="6a545-253">Хотя все этого с более ранними версиями Visual Studio, сделанные все работает с помощью Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6a545-253">While this can all be done with earlier versions of Visual Studio, I made everything work with Visual Studio 2015.</span></span> <span data-ttu-id="6a545-254">Но попутно, которые были некоторые проблемы, добавляемых их здесь в случае, если приводят к одинаковые значения.</span><span class="sxs-lookup"><span data-stu-id="6a545-254">But along the way there were some gotchas, I’m adding them here in case you bump into the same thing.</span></span>

### <a name="exit-code--2146232576-problem-when-running-the-job"></a><span data-ttu-id="6a545-255">Выйдите из кода-2146232576 проблема при запуске задания</span><span class="sxs-lookup"><span data-stu-id="6a545-255">Exit code -2146232576 problem when running the job</span></span> ###
<span data-ttu-id="6a545-256">Я начала проекта Visual Studio 2015 (Предварительная версия), запуска проекта как на основании **.NET Framework 4.5.3**консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="6a545-256">Since I started a Visual Studio 2015 (Preview) project, it started the project up as a Console Application based on **.NET Framework 4.5.3**.</span></span>

<span data-ttu-id="6a545-257">Локально выполнения задания работает, так как .NET Framework 4.5.3 существует на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="6a545-257">Running the job locally works fine, since .NET Framework 4.5.3 exist on my dev machine.</span></span> <span data-ttu-id="6a545-258">Тем не менее после я развертывания задание для личных Windows Azure веб-сайта как WebJob сбой «**выйти из кода-2146232576**».</span><span class="sxs-lookup"><span data-stu-id="6a545-258">However, once I deployed the job to My Windows Azure Web Site as a WebJob, it failed with "**exit code -2146232576**".</span></span>

#### <a name="solution-make-sure-youre-on-the-correct-net-version"></a><span data-ttu-id="6a545-259">Решение: Убедитесь, что вы находитесь на правильную версию .NET</span><span class="sxs-lookup"><span data-stu-id="6a545-259">Solution: Make sure you’re on the correct .NET version</span></span> ####
<span data-ttu-id="6a545-260">Прежде чем я реализованные Azure нравится .NET Framework, версия 4.5.3, что при изменении для **.NET Framework 4.5**это работает потребовалось некоторое время.</span><span class="sxs-lookup"><span data-stu-id="6a545-260">It took a while before I realized that Azure didn’t like .NET Framework version 4.5.3, but when I changed to **.NET Framework 4.5**, it works.</span></span>

<span data-ttu-id="6a545-261">Если приводят к эту проблему, просто убедитесь, что задание выполняется в разделе правильную версию .NET framework.</span><span class="sxs-lookup"><span data-stu-id="6a545-261">If you bump into that problem, just make sure your job is executing under the correct .NET framework version.</span></span>
<span data-ttu-id="6a545-262">![Отображает страницу свойств проекта Visual Studio, вкладка приложения, отражающая конечного framework раскрывающегося списка, выделение точка NET Framework 4.5.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/21.Change-NET-Framework-In-Visual-Studio-2015.png)</span><span class="sxs-lookup"><span data-stu-id="6a545-262">![Displays the Visual Studio Project Properties page, Application tab, showing the Target framework drop down, highlighting dot NET Framework 4.5.](media/Getting-Started-with-building-Azure-WebJobs-for-your-Office365-sites/21.Change-NET-Framework-In-Visual-Studio-2015.png)</span></span>

# <a name="summary"></a><span data-ttu-id="6a545-263">Summary</span><span class="sxs-lookup"><span data-stu-id="6a545-263">Summary</span></span> #
<span data-ttu-id="6a545-264">Пока не очень большой объем к построению WebJob Azure, чтобы обеспечить их весьма сложным.</span><span class="sxs-lookup"><span data-stu-id="6a545-264">While there’s not very much to building an Azure WebJob, you can make them quite complex.</span></span> <span data-ttu-id="6a545-265">Общие концепции прост очень –, но затем как со всех сложных проектов, поступающие решения для проверки подлинности, стабильность кода и надежности, сценарии высокой доступности, обслуживания и т. д.</span><span class="sxs-lookup"><span data-stu-id="6a545-265">The overall concept is very straight forward – but then as with all complex projects comes the decisions around authentication, code stability and reliability, high availability scenarios, maintainability and so on.</span></span> <span data-ttu-id="6a545-266">Эти переменные, уникальных для каждого проекта и следует тщательно учесть перед «только что развертывание» задание для Azure.</span><span class="sxs-lookup"><span data-stu-id="6a545-266">These are variables unique to each project and should be carefully considered before "just deploying" a job to Azure.</span></span>

### <a name="related-links"></a><span data-ttu-id="6a545-267">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="6a545-267">Related links</span></span> ###
-  <span data-ttu-id="6a545-268">Для [исходного запись в блоге на Azure WebJobs](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites) Zimmergren Тобиаса</span><span class="sxs-lookup"><span data-stu-id="6a545-268">[Original blog post on Azure WebJobs](http://zimmergren.net/technical/getting-started-with-building-azure-webjobs-timer-jobs-for-your-office-365-sites) by Tobias Zimmergren</span></span>
-  [<span data-ttu-id="6a545-269">Рекомендуемые ресурсы для Azure WebJobs</span><span class="sxs-lookup"><span data-stu-id="6a545-269">Recommended Resources for Azure WebJobs</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-webjobs-resources/)
-  [<span data-ttu-id="6a545-270">Загрузить Visual Studio 2015 (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="6a545-270">Visual Studio 2015 (Preview) Download</span></span>](http://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx)
-  <span data-ttu-id="6a545-271">[Создание надстройки SharePoint как задания таймера](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx) с Кирк Петров</span><span class="sxs-lookup"><span data-stu-id="6a545-271">[Building a SharePoint Add-in as a Timer Job](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx) by Kirk Evans</span></span>
-  [<span data-ttu-id="6a545-272">Процесс развертывания Azure WebJobs на веб-сайтов Azure</span><span class="sxs-lookup"><span data-stu-id="6a545-272">How to Deploy Azure WebJobs to Azure Websites</span></span>](http://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-deploy-webjobs/)
-  <span data-ttu-id="6a545-273">[Простой удаленного таймер, который взаимодействует со службой SharePoint Online](http://channel9.msdn.com/Blogs/Office-365-Dev/Simple-remote-timer-job-that-interacts-with-SharePoint-Online-Office-365-Developer-Patterns-and-Prac) с (Andrew Connell) на Channel9</span><span class="sxs-lookup"><span data-stu-id="6a545-273">[Simple remote timer job that interacts with SharePoint Online](http://channel9.msdn.com/Blogs/Office-365-Dev/Simple-remote-timer-job-that-interacts-with-SharePoint-Online-Office-365-Developer-Patterns-and-Prac) by Andrew Connell on Channel9</span></span>

### <a name="applies-to"></a><span data-ttu-id="6a545-274">Применимо к</span><span class="sxs-lookup"><span data-stu-id="6a545-274">Applies to</span></span> ###
-  <span data-ttu-id="6a545-275">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="6a545-275">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="6a545-276">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="6a545-276">Office 365 Dedicated (D)</span></span>
-  <span data-ttu-id="6a545-277">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="6a545-277">SharePoint 2013 on-premises</span></span> 
