---
title: "Использование Microsoft Azure WebJobs с Office 365"
ms.date: 11/03/2017
ms.openlocfilehash: 0b3eb304efb291dfa4c0bb7c0809f2c5b044d28f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-microsoft-azure-webjobs-with-office-365"></a><span data-ttu-id="7d274-102">Использование Microsoft Azure WebJobs с Office 365</span><span class="sxs-lookup"><span data-stu-id="7d274-102">Use Microsoft Azure WebJobs with Office 365</span></span>

<span data-ttu-id="7d274-103">Используйте Azure WebJobs для реализации заданий таймера, можно получить доступ к SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="7d274-103">Use Azure WebJobs to implement timer jobs that can access SharePoint Online.</span></span>

<span data-ttu-id="7d274-104">_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="7d274-104">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="7d274-105">**Автор:** Zimmergren Тобиаса</span><span class="sxs-lookup"><span data-stu-id="7d274-105">**Provided by:** Tobias Zimmergren</span></span>

<span data-ttu-id="7d274-106">Реализуйте функциональные возможности задания таймера с помощью [Microsoft Azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) или планировщиком заданий Windows для выполнения задач в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="7d274-106">Implement timer job functionality using  [Microsoft Azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/) or Windows Task Scheduler to perform tasks in SharePoint Online.</span></span> <span data-ttu-id="7d274-107">Задание таймера: повторяющихся, запланированного, фонового процесса, который выполняется в SharePoint для выполнения некоторых задач.</span><span class="sxs-lookup"><span data-stu-id="7d274-107">A timer job is a repetitive, scheduled, background process that runs in SharePoint to perform certain tasks.</span></span> <span data-ttu-id="7d274-108">Например вы можете задания таймера для копирования данных, введенных в список SharePoint с базой данных.</span><span class="sxs-lookup"><span data-stu-id="7d274-108">For example, you may want a timer job to copy data entered in a SharePoint list to a database.</span></span> <span data-ttu-id="7d274-109">В SharePoint Online нельзя развернуть решений фермы, являющийся развертыванию заданий таймера в прошлом.</span><span class="sxs-lookup"><span data-stu-id="7d274-109">In SharePoint Online, you cannot deploy farm solutions, which is how timer jobs were deployed in the past.</span></span> <span data-ttu-id="7d274-110">Чтобы реализовать аналогичные функциональные возможности задания таймера в SharePoint Online, необходимо для запуска консольного приложения в качестве WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-110">To implement similar timer job functionality in SharePoint Online, you need to run a console application as an Azure WebJob.</span></span> <span data-ttu-id="7d274-111">Консольное приложение получает доступ к SharePoint Online с помощью клиентской объектной модели (CSOM).</span><span class="sxs-lookup"><span data-stu-id="7d274-111">The console application accesses SharePoint Online using the client-side object model (CSOM).</span></span> <span data-ttu-id="7d274-112">В этой статье рассматриваются основные понятия, участвующих в развертывании консольные приложения как WebJobs Azure для запуска и получить доступ к SharePoint Online сайтов и контента.</span><span class="sxs-lookup"><span data-stu-id="7d274-112">This article presents the basic concepts involved in deploying console applications as Azure WebJobs to run and access your SharePoint Online sites and content.</span></span>

## <a name="create-and-run-a-console-application-as-an-azure-webjob"></a><span data-ttu-id="7d274-113">Создание и запуск консольного приложения в качестве WebJob Azure</span><span class="sxs-lookup"><span data-stu-id="7d274-113">Create and run a console application as an Azure WebJob</span></span>
<span data-ttu-id="7d274-114"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-114"></span></span>

<span data-ttu-id="7d274-115">Чтобы настроить консольного приложения для запуска в качестве WebJob Azure, необходимо:</span><span class="sxs-lookup"><span data-stu-id="7d274-115">To set up your console application to run as an Azure WebJob, you need to:</span></span>

1. <span data-ttu-id="7d274-116">Создание учетной записи организации для WebJob Azure для получения доступа к сайтов SharePoint и содержимого.</span><span class="sxs-lookup"><span data-stu-id="7d274-116">Create an organization account for the Azure WebJob to use to access your SharePoint sites and content.</span></span>
    
2. <span data-ttu-id="7d274-117">Создание и настройка консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d274-117">Create and set up the console application.</span></span>
    
3. <span data-ttu-id="7d274-118">Добавьте код в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="7d274-118">Add code to the console application.</span></span>
    
4. <span data-ttu-id="7d274-119">Публикация консольное приложение, как WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-119">Publish your console application as an Azure WebJob.</span></span>
    
5. <span data-ttu-id="7d274-120">Запуск и проверьте вашей WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-120">Run and verify your Azure WebJob.</span></span>

## <a name="create-an-organization-account"></a><span data-ttu-id="7d274-121">Создание учетной записи организации</span><span class="sxs-lookup"><span data-stu-id="7d274-121">Create an organization account</span></span>
<span data-ttu-id="7d274-122"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-122"></span></span>

<span data-ttu-id="7d274-123">Необходимо создать учетную запись для WebJob Azure для использования при доступе к сайтов SharePoint и содержимого.</span><span class="sxs-lookup"><span data-stu-id="7d274-123">You need to create an account for the Azure WebJob to use when accessing SharePoint sites and content.</span></span> <span data-ttu-id="7d274-124">Для получения дополнительных сведений обратитесь к [справочной системе добавить пользователей по отдельности в администрирования Office 365](https://support.office.microsoft.com/article/Add-users-individually-to-Office-365---Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec).</span><span class="sxs-lookup"><span data-stu-id="7d274-124">For more information, see  [Add users individually to Office 365-Admin Help](https://support.office.microsoft.com/article/Add-users-individually-to-Office-365---Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec).</span></span> <span data-ttu-id="7d274-125">При выполнении Azure WebJob поле **Автор изменений** хранит и отображает значение, введенное в поле **отображаемое имя** учетной записи организации.</span><span class="sxs-lookup"><span data-stu-id="7d274-125">When the Azure WebJob runs, the  **Modified By** field stores and displays the value entered in **Display name** of the organization account.</span></span> <span data-ttu-id="7d274-126">Убедитесь, что выбрано отображаемое имя, которое пользователи могут легко определять как учетная запись, используемая Azure WebJob для доступа к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d274-126">Ensure you choose a display name that your users can easily identify as the account used by the Azure WebJob for accessing SharePoint.</span></span>

## <a name="create-and-set-up-the-console-application"></a><span data-ttu-id="7d274-127">Создание и настройка консольного приложения</span><span class="sxs-lookup"><span data-stu-id="7d274-127">Create and set up the console application</span></span>
<span data-ttu-id="7d274-128"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-128"></span></span>

<span data-ttu-id="7d274-129">Создание консольного приложения для запуска в качестве WebJob Azure, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="7d274-129">To create a console application to run as an Azure WebJob, perform the following steps:</span></span>

1. <span data-ttu-id="7d274-130">Создайте новый проект консольного приложения с:</span><span class="sxs-lookup"><span data-stu-id="7d274-130">Create a new console application project by:</span></span>
    
    1. <span data-ttu-id="7d274-131">Выберите **Новый проект**в Visual Studio > **Visual C#** > **Консольного приложения** > **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="7d274-131">In Visual Studio, choose  **New Project** > **Visual C#** > **Console Application** > **OK**.</span></span>
    
    2. <span data-ttu-id="7d274-132">После создания консольного приложения, выберите в меню **Сервис** > **Диспетчер пакетов NuGet** > **Управление пакетами NuGet для решения...**  >  **Online** > **все**.</span><span class="sxs-lookup"><span data-stu-id="7d274-132">After the console application is created, choose  **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution...** > **Online** > **All**.</span></span>
    
    3. <span data-ttu-id="7d274-133">Поиск **приложения для набора средств веб-сайта SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="7d274-133">Search for  **App for SharePoint Web Toolkit**.</span></span>
    
    4. <span data-ttu-id="7d274-134">Нажмите кнопку **установить**, а затем нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="7d274-134">Choose  **Install**, then choose  **OK**.</span></span>
    
    5. <span data-ttu-id="7d274-135">Нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="7d274-135">Choose  **Close**.</span></span>
    
    6. <span data-ttu-id="7d274-136">Убедитесь, что SharePointContext.cs и TokenHelper.cs были добавлены в проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="7d274-136">Verify that SharePointContext.cs and TokenHelper.cs were added to the console application project.</span></span>
    
2. <span data-ttu-id="7d274-137">Сохранение сведений об учетной записи в файле app.config, добавив элемент **appSettings** показано.</span><span class="sxs-lookup"><span data-stu-id="7d274-137">Save your account information in the app.config by adding the  **appSettings** element shown.</span></span> <span data-ttu-id="7d274-138">Измените **SPOAccount** и **SPOPassword** на имя пользователя и пароль для учетной записи организации, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="7d274-138">Change **SPOAccount** and **SPOPassword** to the user name and password of the organization account you created previously.</span></span>
    
    ```XML
    <?xml version="1.0" encoding="utf-8" ?>
     <configuration>
      <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
      </startup>
      <appSettings>
        <add key="SPOAccount" value="admin@contoso.onmicrosoft.com"/>
        <add key="SPOPassword" value="Contoso"/>
      </appSettings>
     </configuration>
    ```

    <span data-ttu-id="7d274-139">**Внимание!**  App.config хранит имя пользователя и пароль учетной записи организации в виде простого текста.</span><span class="sxs-lookup"><span data-stu-id="7d274-139">**Caution**  App.config stores the organization account's username and password in clear text.</span></span> <span data-ttu-id="7d274-140">Этот метод используется только в целях демонстрации и не должен использоваться в развертывании рабочей вашей WebJobs Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-140">This method is used for demonstration purposes only, and should not be used in your production deployment of your Azure WebJobs.</span></span> <span data-ttu-id="7d274-141">Мы рекомендуем шифровать пароль или проверка подлинности с помощью OAuth с помощью маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="7d274-141">We recommend encrypting the password, or authenticating using OAuth with access tokens.</span></span> <span data-ttu-id="7d274-142">Дополнительные сведения см в блоге Петров Кирк по [построению надстройки SharePoint как задания таймера](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d274-142">For more information, see Kirk Evans blog post on  [Building a SharePoint Add-in as a Timer Job](http://blogs.msdn.com/b/kaevans/archive/2014/03/02/building-a-sharepoint-app-as-a-timer-job.aspx).</span></span>

## <a name="add-code-to-the-console-application"></a><span data-ttu-id="7d274-143">Добавление кода для консольного приложения</span><span class="sxs-lookup"><span data-stu-id="7d274-143">Add code to the console application</span></span>
<span data-ttu-id="7d274-144"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-144"></span></span>

<span data-ttu-id="7d274-145">В файле Program.cs добавьте следующий код в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="7d274-145">In Program.cs, add the following code to the console application.</span></span>

<span data-ttu-id="7d274-146">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="7d274-146">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>


1. <span data-ttu-id="7d274-147">Добавьте операторы **using** .</span><span class="sxs-lookup"><span data-stu-id="7d274-147">Add  **using** statements.</span></span>
    
    ```C#
    using Microsoft.SharePoint.Client;
    using System.Security;
    using System.Configuration; 
    ```

2. <span data-ttu-id="7d274-148">Добавление класса следующих методов:</span><span class="sxs-lookup"><span data-stu-id="7d274-148">Add the following methods to your class:</span></span>
    
    -  <span data-ttu-id="7d274-149">**Основные** перейдете на сайт SharePoint, а затем использует CSOM для выполнения задач на сайте или контент.</span><span class="sxs-lookup"><span data-stu-id="7d274-149">**Main** signs into your SharePoint site, and then uses the CSOM to perform tasks on your site or content.</span></span> <span data-ttu-id="7d274-150">В этом образце кода используется CSOM поиск списка и общее число элементов, входящих в список в окне консоли выходные данные.</span><span class="sxs-lookup"><span data-stu-id="7d274-150">This code sample uses the CSOM to find a list and output the total number of items that are in the list to the console window.</span></span> <span data-ttu-id="7d274-151">При использовании Azure WebJobs, могут видеть выходные данные окна консоли в WebJob сведения о выполнении, обсуждаемой в [выполните и проверьте вашей WebJob Azure](Use-Microsoft-Azure-WebJobs-with-Office-365.md#runandverify).</span><span class="sxs-lookup"><span data-stu-id="7d274-151">When using Azure WebJobs, you can see the console window output in the WebJob Run Details, which is explained in [Run and verify your Azure WebJob](Use-Microsoft-Azure-WebJobs-with-Office-365.md#runandverify).</span></span>
    
  -  <span data-ttu-id="7d274-152">**GetSPOSecureStringPassword** считывает пароль из app.config.</span><span class="sxs-lookup"><span data-stu-id="7d274-152">**GetSPOSecureStringPassword** reads your password from app.config.</span></span>
    
  -  <span data-ttu-id="7d274-153">**GetSPOAccountName** считывает текущее имя пользователя из app.config.</span><span class="sxs-lookup"><span data-stu-id="7d274-153">**GetSPOAccountName** reads your username from app.config.</span></span>

    ```C#
    static void Main(string[] args)
        {
            using (ClientContext context = new ClientContext("https://contoso.sharepoint.com"))
            {
                // Use default authentication mode.
                context.AuthenticationMode = ClientAuthenticationMode.Default;                 
                context.Credentials = new SharePointOnlineCredentials(GetSPOAccountName(), GetSPOSecureStringPassword());
    
                // Add your CSOM code to perform tasks on your sites and content.
    
                try
                {
                    List objList = context.Web.Lists.GetByTitle("Docs");
                    context.Load(objList);
                    context.ExecuteQuery();
    
                    if (objList != null &amp;&amp; objList.ItemCount > 0)
                    {
                        Console.WriteLine(objList.Title.ToString() + " has " + objList.ItemCount + " items.");
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
                
        }
    
    private static SecureString GetSPOSecureStringPassword()
    {
      try
      {
          Console.WriteLine("Entered GetSPOSecureStringPassword.");
          var secureString = new SecureString();
          foreach (char c in ConfigurationManager.AppSettings["SPOPassword"])
          {
              secureString.AppendChar(c);
          }
          Console.WriteLine("Constructed the secure password.");
    
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
          Console.WriteLine("Entered GetSPOAccountName.");
          return ConfigurationManager.AppSettings["SPOAccount"];
      }
      catch
      {
          throw;
      }
    }
    
    ```

## <a name="publish-your-console-application-as-an-azure-webjob"></a><span data-ttu-id="7d274-154">Публикация консольное приложение, как WebJob Azure</span><span class="sxs-lookup"><span data-stu-id="7d274-154">Publish your console application as an Azure WebJob</span></span>
<span data-ttu-id="7d274-155"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-155"></span></span>

<span data-ttu-id="7d274-156">Завершив разработку консольное приложение, необходимо выполнить развертывание консольного приложения как WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-156">When you are finished developing your console application, you need to deploy the console application as an Azure WebJob.</span></span> <span data-ttu-id="7d274-157">Чтобы развернуть консольное приложение, как WebJob Azure, вы можете:</span><span class="sxs-lookup"><span data-stu-id="7d274-157">To deploy your console application as an Azure WebJob, you can:</span></span>

- <span data-ttu-id="7d274-158">Передача двоичных файлов Azure веб-приложения и создание WebJob Azure с использованием [Портала Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7d274-158">Upload your binaries to an Azure Web App, and create an Azure WebJob using the  [Microsoft Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7d274-159">Двоичные файлы для проекта Visual Studio можно найти в bin/Debug или bin/Release папки проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d274-159">The binaries for your Visual Studio project can be found in the bin/Debug or bin/Release folders of your Visual Studio project.</span></span> <span data-ttu-id="7d274-160">Для создания веб-приложения Azure и загрузки двоичных файлов, следуйте указаниям в разделе [Create веб-приложение ASP.NET в Azure приложения-службы](http://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="7d274-160">To create the Azure Web App and upload the binaries, follow the steps in  [Create an ASP.NET web app in Azure App Service](http://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span> <span data-ttu-id="7d274-161">Для создания по запросу, непрерывной или запланированного WebJob Azure видеть [Запуск фоновых задач с WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span><span class="sxs-lookup"><span data-stu-id="7d274-161">To create your on demand, continuous, or scheduled Azure WebJob, see  [Run Background tasks with WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span></span>
    
- <span data-ttu-id="7d274-162">Публикация вашего WebJob Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d274-162">Publish your Azure WebJob from Visual Studio.</span></span> <span data-ttu-id="7d274-163">Дополнительные сведения можно [Включить WebJobs развертывания без веб-проект](http://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="7d274-163">For more information, see  [Enable WebJobs deployment without a web project](http://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#convertnolink).</span></span>
    
## <a name="run-and-verify-your-azure-webjob"></a><span data-ttu-id="7d274-164">Запуск и проверка вашей WebJob Azure</span><span class="sxs-lookup"><span data-stu-id="7d274-164">Run and verify your Azure WebJob</span></span>
<span data-ttu-id="7d274-165"><a name="runandverify"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-165"></span></span>

<span data-ttu-id="7d274-166">После завершения всех предыдущих шагов, вашей WebJob Azure должен быть под управлением и выполнения задач в подписки Office 365.</span><span class="sxs-lookup"><span data-stu-id="7d274-166">After completing all the previous steps, your Azure WebJob should be running and performing tasks in your Office 365 subscription.</span></span> <span data-ttu-id="7d274-167">В некоторых случаях может потребоваться выполнение обслуживания и устранения неполадок вашей WebJobs Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-167">At times, you may need to perform maintenance or troubleshoot your Azure WebJobs.</span></span> <span data-ttu-id="7d274-168">Чтобы проверить, что ваше WebJob Azure работает:</span><span class="sxs-lookup"><span data-stu-id="7d274-168">To verify that your Azure WebJob is running:</span></span>

- <span data-ttu-id="7d274-169">Если ваше WebJob Azure обновление элемент SharePoint как элемент списка в поле **Автор изменений** отображается учетной записи организации, Azure WebJob для доступа к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7d274-169">If your Azure WebJob updated a SharePoint item, like a list item, the  **Modified By** field displays the organization account that the Azure WebJob used to access SharePoint.</span></span>
    
- <span data-ttu-id="7d274-170">Просмотр журналов на WebJob подробные сведения для вашей WebJob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d274-170">Review the WebJob Details logs for your Azure WebJob.</span></span> <span data-ttu-id="7d274-171">Запустите позволяет журналы WebJob сведений, просмотрите при выполнении задания, успешное или неудачное задания, вывод из WebJob (например, когда Console.WriteLine вызван) и другие сведения о запустите задание.</span><span class="sxs-lookup"><span data-stu-id="7d274-171">The WebJob Details logs lets you review when a job ran, the success or failure of a job run, any output from the WebJob (for example, when Console.WriteLine was called), and other details of the job run.</span></span> <span data-ttu-id="7d274-172">Для получения дополнительных сведений обратитесь к разделу Просмотр журнала заданий на [Запуск фоновых задач с WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span><span class="sxs-lookup"><span data-stu-id="7d274-172">For more information, see the section View the job history on  [Run Background tasks with WebJobs](http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d274-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7d274-173">Additional resources</span></span>
<span data-ttu-id="7d274-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7d274-174"></span></span>

-  <span data-ttu-id="7d274-175">[Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="7d274-175">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>
    
-  <span data-ttu-id="7d274-176">[Создание WebJob .NET в Azure приложения-службы](http://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span><span class="sxs-lookup"><span data-stu-id="7d274-176">[Create a .NET WebJob in Azure App Service](http://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span></span>
    
-  <span data-ttu-id="7d274-177">[Ресурсы azure WebJobs](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).</span><span class="sxs-lookup"><span data-stu-id="7d274-177">[Azure WebJobs resources](http://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).</span></span>
