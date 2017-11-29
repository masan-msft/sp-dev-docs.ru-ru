---
title: "Подготовка пример консольного приложения"
ms.date: 11/03/2017
ms.openlocfilehash: 29d14151ccea3bebec3c7e1a899bdf8067321193
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="provisioning-console-application-sample"></a><span data-ttu-id="17cfa-102">Подготовка пример консольного приложения</span><span class="sxs-lookup"><span data-stu-id="17cfa-102">Provisioning console application sample</span></span>

<span data-ttu-id="17cfa-103">Изучение основ с помощью PnP модуля подготовки для создания и сохранения, а затем применять подготовки шаблонов для новых семейств сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="17cfa-103">Learn the fundamentals of using the PnP provisioning engine to create and persist, and then apply provisioning templates to new SharePoint site collections.</span></span>

<span data-ttu-id="17cfa-104">Для поддержки новой модели надстройки (PnP) программы Office 365 для разработчиков шаблоны и рекомендации представила подготовки структуру, которая позволяет пользователям создавать настраиваемые шаблоны сайтов, просто навести указатель мыши на узел модели, сохранение модели как шаблон подготовки а затем применять настраиваемый шаблон для новой или существующей семейств сайтов, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="17cfa-104">To support the new add-in model, the Office 365 Developer Patterns and Practices program (PnP) has introduced a provisioning framework that allows users to create custom site templates by simply pointing at a site model, persist the model as a provisioning template, and then apply the custom template to new or existing site collections as needed.</span></span>

<span data-ttu-id="17cfa-105">В этом примере мы создание простого консольного приложения, который реализует классы из подготовки PnP основной библиотеки для включения PnP модуля подготовки для выполнения этих основных задач подготовки:</span><span class="sxs-lookup"><span data-stu-id="17cfa-105">In this sample, we create a basic console application that implements classes in the provisioning PnP Core library to enable the PnP provisioning engine to complete these essential provisioning tasks:</span></span> 

- <span data-ttu-id="17cfa-106">Проектирование и модель настройки сайта.</span><span class="sxs-lookup"><span data-stu-id="17cfa-106">Design and model your site customization.</span></span> <span data-ttu-id="17cfa-107">Это может быть новый сайт проекта, или можно последовательно к существующему сайту и сохранить его как шаблон подготовки.</span><span class="sxs-lookup"><span data-stu-id="17cfa-107">This can be a new site design, or you can point to an existing site and save it as a provisioning template.</span></span>
    
- <span data-ttu-id="17cfa-108">Сохраните и сохранения модели сайта как шаблона подготовки, чтобы его можно повторно использовать.</span><span class="sxs-lookup"><span data-stu-id="17cfa-108">Save and persist the site model as a provisioning template so that you can reuse it.</span></span>
    
- <span data-ttu-id="17cfa-109">Применение шаблона подготовки к семейства нового или существующего веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="17cfa-109">Apply the provisioning template to a new or existing site collection.</span></span>
    
<span data-ttu-id="17cfa-110">**Примечание:**  В этом пошаговом руководстве пример является companion для примера, в настоящее время недоступен на репозиториев: [Приступая к работе с PnP модуля подготовки](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Framework.Console).</span><span class="sxs-lookup"><span data-stu-id="17cfa-110">**Note:**  This sample walkthrough is a companion to a sample currently available on GitHub: [Getting Started with the PnP Provisioning Engine](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Framework.Console).</span></span> <span data-ttu-id="17cfa-111">Код (Program.cs) и файлы решений для примера доступны для загрузки.</span><span class="sxs-lookup"><span data-stu-id="17cfa-111">The code (Program.cs) and solution files for the sample are available for download.</span></span> <span data-ttu-id="17cfa-112">Также имеется 20-минутный видео презентации этого процесса (с кодом немного отличаться) на сайте Microsoft канала 9: [Приступая к работе с PnP модуля подготовки](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).</span><span class="sxs-lookup"><span data-stu-id="17cfa-112">There also is a 20-minute video presentation of this process (with slightly different code) available on the Microsoft Channel 9 site: [Getting Started with the PnP Provisioning Engine](https://channel9.msdn.com/blogs/OfficeDevPnP/Getting-Started-with-PnP-Provisioning-Engine).</span></span>

## <a name="remote-provisioning-walkthrough"></a><span data-ttu-id="17cfa-113">Удаленный подготовки Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="17cfa-113">Remote provisioning walkthrough</span></span>

<span data-ttu-id="17cfa-114">Чтобы начать, создайте проект Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17cfa-114">To begin, create a Visual Studio project.</span></span> <span data-ttu-id="17cfa-115">В этом примере для простоты мы создание простого консольного приложения, который реализует PnP модуля подготовки с помощью библиотеки PnP основных подготовки структуры.</span><span class="sxs-lookup"><span data-stu-id="17cfa-115">In this sample, for simplicity, we create a basic console application that implements the PnP provisioning engine by using the PnP Core library of the provisioning framework.</span></span> <span data-ttu-id="17cfa-116">Чтобы обеспечить поддержку примера решения, тем не менее, мы необходимо загрузить и установить подготовки PnP основной библиотеки framework.</span><span class="sxs-lookup"><span data-stu-id="17cfa-116">To support the sample solution, however, we must download and install the provisioning framework PnP Core library.</span></span> <span data-ttu-id="17cfa-117">Следуйте инструкциям для этого.</span><span class="sxs-lookup"><span data-stu-id="17cfa-117">Instructions for doing so follow.</span></span>

### <a name="create-and-prepare-a-visual-studio-project"></a><span data-ttu-id="17cfa-118">Создание и Подготовка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17cfa-118">Create and prepare a Visual Studio project</span></span>

1. <span data-ttu-id="17cfa-119">Запустите Visual Studio, а затем выберите **файл** > **New** > **проекта**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-119">Launch Visual Studio, and then choose  **File** > **New** > **Project**.</span></span>
    
2. <span data-ttu-id="17cfa-120">В мастере **Создания проекта** выберите **Visual C#**, а затем выберите пункт **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-120">In the  **New Project** wizard, choose **Visual C#**, then choose  **Console Application**.</span></span>
    
3. <span data-ttu-id="17cfa-121">Назовите проект «Программы» и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-121">Name the project "Program," and then click  **OK**.</span></span> <span data-ttu-id="17cfa-122">(Вы можете назовите проект что-либо как, но помните, что в этом пошаговом руководстве ссылаются на имя проекта как «программа».)</span><span class="sxs-lookup"><span data-stu-id="17cfa-122">(You can name the project anything you like, but be mindful that this walkthrough will reference the project name as "program.")</span></span>
    
4. <span data-ttu-id="17cfa-123">Загрузка и установка PnP основной библиотеки, доступные в виде пакета NuGet: [OfficeDevPnP.Core пакетов](https://www.nuget.org/profiles/officedevpnp).</span><span class="sxs-lookup"><span data-stu-id="17cfa-123">Download and install the PnP Core library that is available as a NuGet package here: [OfficeDevPnP.Core packages](https://www.nuget.org/profiles/officedevpnp).</span></span>
    
    <span data-ttu-id="17cfa-124">**Примечание:**  Существует две версии основной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="17cfa-124">**Note:**  There are two versions of the core library.</span></span> <span data-ttu-id="17cfa-125">Одна версия — это библиотека **OfficeDevPnP.Core** , которая относится SharePoint Online и Office 365.</span><span class="sxs-lookup"><span data-stu-id="17cfa-125">One version is the **OfficeDevPnP.Core** library, which targets SharePoint Online and Office 365.</span></span> <span data-ttu-id="17cfa-126">Второй версии — **OfficeDevPnP.Core (локально)**, который предназначен для SharePoint 2013 в локальной.</span><span class="sxs-lookup"><span data-stu-id="17cfa-126">The second version is **OfficeDevPnP.Core (on-premises)**, which targets SharePoint 2013 on-premises.</span></span> <span data-ttu-id="17cfa-127">Вот снимок из доступных вариантов.</span><span class="sxs-lookup"><span data-stu-id="17cfa-127">Here is a screenshot of the available options.</span></span>

    ![Два варианта загрузки библиотеки ядра](media/provisioning-console-application-sample/5b1adb8d-52e5-4c67-8792-6ef0ae41d655.png)

<span data-ttu-id="17cfa-129">В этом пошаговом руководстве пример используется первый вариант, чтобы целевой SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="17cfa-129">In this sample walkthrough, we're using the first option to target SharePoint Online.</span></span>

1. <span data-ttu-id="17cfa-130">Во-первых установите клиент NuGet, перейдя на [установщик клиента NuGet](http://docs.nuget.org/consume/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="17cfa-130">First, install the NuGet client by going to the [NuGet client installer](http://docs.nuget.org/consume/installing-nuget).</span></span>

2. <span data-ttu-id="17cfa-131">После NuGet установлен клиент, запустите **Диспетчер пакетов NuGet**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-131">After the NuGet client is installed, run the  **NuGet Package manager**.</span></span> <span data-ttu-id="17cfa-132">Щелкните правой кнопкой мыши узел **ссылки** в **Обозревателе решений**Visual Studio и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-132">Right-click the  **References** node in the Visual Studio **Solution Explorer**, and then select  **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="17cfa-133">Диспетчер пакетов, выберите **сети**, затем **EntityFramework**, а затем введите условие поиска разработчик офисных «решений» для предоставления библиотеки OfficeDevPnP.Core.</span><span class="sxs-lookup"><span data-stu-id="17cfa-133">In the Package Manager, choose **Online**, then  **EntityFramework**, and then enter the search term "OfficeDev" to expose the OfficeDevPnP.Core library.</span></span>

4. <span data-ttu-id="17cfa-134">Следуйте инструкциям, чтобы загрузить и установить библиотеки **OfficeDevPnP.Core** , выполнив указания данного.</span><span class="sxs-lookup"><span data-stu-id="17cfa-134">Follow directions to download and install the  **OfficeDevPnP.Core** library, following the given directions.</span></span>

   <span data-ttu-id="17cfa-135">После ссылки на библиотеку PnP основных в проекте Visual Studio, все члены библиотеки доступны как [методы расширения](https://msdn.microsoft.com/en-us/library/bb383977.aspx) на существующие экземпляры объекта, для примера, **веб-** серверы и **список** экземпляров.</span><span class="sxs-lookup"><span data-stu-id="17cfa-135">After the PnP Core library is referenced in your Visual Studio project, all library members are available to you as [extension methods](https://msdn.microsoft.com/en-us/library/bb383977.aspx) on existing object instances, for example, **web** and **list** instances.</span></span>

5. <span data-ttu-id="17cfa-136">Убедитесь, что файл Program.cs содержит все следующие `using` операторов.</span><span class="sxs-lookup"><span data-stu-id="17cfa-136">Ensure that your Program.cs file contains all of the following  `using` statements.</span></span>

    ```c#
    using Microsoft.SharePoint.Client;
    using OfficeDevPnP.Core.Framework.Provisioning.Connectors;
    using OfficeDevPnP.Core.Framework.Provisioning.Model;
    using OfficeDevPnP.Core.Framework.Provisioning.ObjectHandlers;
    using OfficeDevPnP.Core.Framework.Provisioning.Providers.Xml;
    using System;
    using System.Net;
    using System.Security;
    using System.Threading;
    ```

<span data-ttu-id="17cfa-137">**Один раз мы были заданы в проект**</span><span class="sxs-lookup"><span data-stu-id="17cfa-137">**Once we have set up your project**</span></span>

<span data-ttu-id="17cfa-138">После настройки проекта можно создать настройки сайта.</span><span class="sxs-lookup"><span data-stu-id="17cfa-138">Once your project is set up, you can create your site customizations.</span></span> <span data-ttu-id="17cfa-139">Это можно сделать вручную или, указав на сайт, макет которого вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="17cfa-139">You can do this by hand or by pointing to a site whose design you wish to use.</span></span> <span data-ttu-id="17cfa-140">Просто сохраните проект выбранного сайта в качестве шаблона подготовки.</span><span class="sxs-lookup"><span data-stu-id="17cfa-140">Simply save the chosen site design as a provisioning template.</span></span> <span data-ttu-id="17cfa-141">Или можно использовать сочетание оба подхода.</span><span class="sxs-lookup"><span data-stu-id="17cfa-141">Or, you can use a mix of both approaches.</span></span> <span data-ttu-id="17cfa-142">В данном примере мы просто укажет на существующий сайт и сохранить его вариант оформления и артефактов сайта (но не его содержимое) как шаблон подготовки.</span><span class="sxs-lookup"><span data-stu-id="17cfa-142">For the purpose of this sample, we will simply point to an existing site and save its composed look and site artifacts (but not its content) as a provisioning template.</span></span>

<span data-ttu-id="17cfa-143">Чтобы приступить к работе, необходимо подключение к сайту, мы желаем для моделирования как наш подготовки шаблон.</span><span class="sxs-lookup"><span data-stu-id="17cfa-143">To begin, we need to connect to the site that we wish to model as our provisioning template.</span></span> <span data-ttu-id="17cfa-144">Начнем с собирает сведения о подключении, включая имя пользователя, пароль и исходный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="17cfa-144">Let's start by gathering connection information, including user name, password, and the source URL.</span></span>

### <a name="create-and-extract-and-persist-the-provisioning-template"></a><span data-ttu-id="17cfa-145">Создание и извлечение и сохранение подготовки шаблона</span><span class="sxs-lookup"><span data-stu-id="17cfa-145">Create and extract and persist the provisioning template</span></span>

1. <span data-ttu-id="17cfa-146">Собирает сведения о подключении у пользователя.</span><span class="sxs-lookup"><span data-stu-id="17cfa-146">Collect connection information from the user.</span></span> <span data-ttu-id="17cfa-147">Обратите внимание, что в программе `Main` процедуры, мы выполнить три простых действия: собирать сведения о подключении и подготовки шаблона, а также ПРИМЕНЯЮТСЯ подготовки шаблона.</span><span class="sxs-lookup"><span data-stu-id="17cfa-147">Note that in the program's  `Main` routine, we do three simple things: collect connection information, GET the provisioning template, and APPLY the provisioning template.</span></span> <span data-ttu-id="17cfa-148">Сложных задач выполняется с помощью методов **GetProvisioningTemplate** и **ApplyProvisioningTemplate** , которые мы определяют ниже.</span><span class="sxs-lookup"><span data-stu-id="17cfa-148">The heavy lifting is done by the **GetProvisioningTemplate** and **ApplyProvisioningTemplate** methods that we define below.</span></span>
    
    ```C#
    static void Main(string[] args)
        {
            ConsoleColor defaultForeground = Console.ForegroundColor;
    
            // Collect information 
            string templateWebUrl = GetInput("Enter the URL of the template site: ", false, defaultForeground);
            string targetWebUrl = GetInput("Enter the URL of the target site: ", false, defaultForeground);
            string userName = GetInput("Enter your user name:", false, defaultForeground);
            string pwdS = GetInput("Enter your password:", true, defaultForeground);
            SecureString pwd = new SecureString();
            foreach (char c in pwdS.ToCharArray()) pwd.AppendChar(c);
    
            // GET the template from existing site and serialize
            // Serializing the template for later reuse is optional
            ProvisioningTemplate template = GetProvisioningTemplate(defaultForeground, templateWebUrl, userName, pwd);
    
            // APPLY the template to new site from 
            ApplyProvisioningTemplate(defaultForeground, targetWebUrl, userName, pwd, template);
    
            // Pause and modify the UI to indicate that the operation is complete
            Console.ForegroundColor = ConsoleColor.White;
            Console.WriteLine("We're done. Press Enter to continue.");
            Console.ReadLine();
        }
    ```

2. <span data-ttu-id="17cfa-149">Создайте и используйте закрытый метод **GetInput** для получения учетных данных пользователей.</span><span class="sxs-lookup"><span data-stu-id="17cfa-149">Create and use a private  **GetInput** method to obtain the required user credentials.</span></span>
    
    ```c#
    private static string GetInput(string label, bool isPassword, ConsoleColor defaultForeground)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("{0} : ", label);
            Console.ForegroundColor = defaultForeground;
    
            string value = "";
    
            for (ConsoleKeyInfo keyInfo = Console.ReadKey(true); keyInfo.Key != ConsoleKey.Enter; keyInfo = Console.ReadKey(true))
            {
                if (keyInfo.Key == ConsoleKey.Backspace)
                {
                    if (value.Length > 0)
                    {
                        value = value.Remove(value.Length - 1);
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                        Console.Write(" ");
                        Console.SetCursorPosition(Console.CursorLeft - 1, Console.CursorTop);
                    }
                }
                else if (keyInfo.Key != ConsoleKey.Enter)
                {
                    if (isPassword)
                    {
                        Console.Write("*");
                    }
                    else
                    {
                        Console.Write(keyInfo.KeyChar);
                    }
                    value += keyInfo.KeyChar;
    
                }
    
            }
            Console.WriteLine("");
    
            return value;
        }
    ```

3. <span data-ttu-id="17cfa-150">Выберите сайт, который является модель для нашего шаблона, подготовки.</span><span class="sxs-lookup"><span data-stu-id="17cfa-150">Point to the site that's the model for our provisioning template.</span></span> <span data-ttu-id="17cfa-151">Во время выполнения GET на исходного веб-сайта с помощью одной строки кода, рассмотрим `GetProvisioningTemplate()`, мы определили метод GET.</span><span class="sxs-lookup"><span data-stu-id="17cfa-151">While doing the GET on the source site with a single line of code, look at  `GetProvisioningTemplate()`, the GET method we defined.</span></span> 
    
    ```c#
    private static ProvisioningTemplate GetProvisioningTemplate(ConsoleColor defaultForeground, string webUrl, string userName, SecureString pwd)
        {
            using (var ctx = new ClientContext(webUrl))
            {
                // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    
                // Just to output the site details
                Web web = ctx.Web;
                ctx.Load(web, w => w.Title);
                ctx.ExecuteQueryRetry();
    
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine("Your site title is:" + ctx.Web.Title);
                Console.ForegroundColor = defaultForeground;
    
                ProvisioningTemplateCreationInformation ptci
                        = new ProvisioningTemplateCreationInformation(ctx.Web);
    
                // Create FileSystemConnector to store a temporary copy of the template 
                ptci.FileConnector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                ptci.PersistComposedLookFiles = true;
                ptci.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    // Only to output progress for console UI
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    
                // Execute actual extraction of the template
                ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);
    
                // We can serialize this template to save and reuse it
                // Optional step 
                XMLTemplateProvider provider =
                        new XMLFileSystemTemplateProvider(@"c:\temp\pnpprovisioningdemo", "");
                provider.SaveAs(template, "PnPProvisioningDemo.xml");
    
                return template;
            }
        }
    ```

    <span data-ttu-id="17cfa-152">В приведенном выше фрагменте кода мы также определены переменной, **ProvisioningTemplateCreationInformation** **pcti**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-152">In the above code snippet, we also defined a  **ProvisioningTemplateCreationInformation** variable, **pcti**.</span></span> <span data-ttu-id="17cfa-153">Переменная дает возможность хранения сведений о артефакты, которые можно сохранить вместе с шаблоном.</span><span class="sxs-lookup"><span data-stu-id="17cfa-153">The variable gives us the option to store information about artifacts that we can save along with the template.</span></span>
    
4. <span data-ttu-id="17cfa-154">Создание объекта файловой системы соединителя, чтобы сохранить копию временной подготовки шаблона, который мы собираемся для применения к другой сайт.</span><span class="sxs-lookup"><span data-stu-id="17cfa-154">Create a file system connector object so that we can store a temporary copy of the provisioning template that we're going to apply to another site.</span></span>
    
    <span data-ttu-id="17cfa-155">**Примечание:**  Этот шаг является необязательным.</span><span class="sxs-lookup"><span data-stu-id="17cfa-155">**Note:**  This step is optional.</span></span> <span data-ttu-id="17cfa-156">Это не является обязательным, сериализации подготовки шаблон XML.</span><span class="sxs-lookup"><span data-stu-id="17cfa-156">It's not required that you serialize the provisioning template to XML.</span></span> <span data-ttu-id="17cfa-157">На этом этапе шаблон — это просто кода C#.</span><span class="sxs-lookup"><span data-stu-id="17cfa-157">At this stage, the template is simply C# code.</span></span> <span data-ttu-id="17cfa-158">Не только сериализация является необязательным, но также можно использовать любой формат сериализации, вам следует.</span><span class="sxs-lookup"><span data-stu-id="17cfa-158">Not only is serialization optional, but you also can use whatever serialization format you wish.</span></span>

5. <span data-ttu-id="17cfa-159">Выполнение извлечения подготовки шаблона с помощью этой одной строки кода.</span><span class="sxs-lookup"><span data-stu-id="17cfa-159">Execute the extraction of the provisioning template by using just this single line of code.</span></span>      `ProvisioningTemplate template = ctx.Web.GetProvisioningTemplate(ptci);`
    
6. <span data-ttu-id="17cfa-160">(Необязательно) Сохранить и сохраните сериализованных версия подготовки шаблона, чтобы его можно повторно использовать.</span><span class="sxs-lookup"><span data-stu-id="17cfa-160">(Optional) Save and store a serialized version of the provisioning template so that you can reuse it.</span></span> <span data-ttu-id="17cfa-161">Можно выполнить сериализацию подготовки шаблона в формате, независимо от выбранного вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="17cfa-161">You can serialize the provisioning template in whichever format you prefer.</span></span> <span data-ttu-id="17cfa-162">В этом примере мы сериализованным в XML-файл с именем **PnPProvisioningDemo.xml**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-162">In this sample, we've serialized to an XML file named  **PnPProvisioningDemo.xml**.</span></span> <span data-ttu-id="17cfa-163">Сам файл является объектом **XMLFileSystemTemplateProvider** , для которого мы подготовили папку файловой системы.</span><span class="sxs-lookup"><span data-stu-id="17cfa-163">The file itself is an **XMLFileSystemTemplateProvider** object for which we've provided a file system location.</span></span>
    
<span data-ttu-id="17cfa-164">**Один раз мы извлечения, сохранить и сохранение подготовки шаблона**</span><span class="sxs-lookup"><span data-stu-id="17cfa-164">**Once we extract, save and persist the provisioning template**</span></span>

<span data-ttu-id="17cfa-165">Мы извлечения, сохранить и сохранение подготовки шаблона следующий и последний шаг после для применения подготовки шаблон для нового семейства сайтов SharePoint с помощью метода **ApplyProvisioningTemplate** .</span><span class="sxs-lookup"><span data-stu-id="17cfa-165">Once we extract, save, and persist the provisioning template, the next and final step is to apply the provisioning template to a new SharePoint site collection by using the  **ApplyProvisioningTemplate** method.</span></span>

### <a name="apply-the-provisioning-template-to-a-new-or-existing-site"></a><span data-ttu-id="17cfa-166">Применение шаблона подготовки нового или существующего сайта</span><span class="sxs-lookup"><span data-stu-id="17cfa-166">Apply the provisioning template to a new or existing site</span></span>

1. <span data-ttu-id="17cfa-167">Получите учетную запись для целевого сайта.</span><span class="sxs-lookup"><span data-stu-id="17cfa-167">Obtain credentials to the target site.</span></span>
    
    ```c#
    // ctx.Credentials = new NetworkCredentials(userName, pwd);
                ctx.Credentials = new SharePointOnlineCredentials(userName, pwd);
                ctx.RequestTimeout = Timeout.Infinite;
    ```

2. <span data-ttu-id="17cfa-168">Capture артефактов сайта, которые были сохранены с помощью метода **ProvisioningTemplateCreationInformation** с помощью метода companion **ProvisioningTemplateApplyingInformation**.</span><span class="sxs-lookup"><span data-stu-id="17cfa-168">Capture site artifacts that were stored using the  **ProvisioningTemplateCreationInformation** method by using the companion method, **ProvisioningTemplateApplyingInformation**.</span></span>
    
    ```c#
    ProvisioningTemplateApplyingInformation ptai
                        = new ProvisioningTemplateApplyingInformation();
                ptai.ProgressDelegate = delegate(String message, Int32 progress, Int32 total)
                {
                    Console.WriteLine("{0:00}/{1:00} - {2}", progress, total, message);
                };
    ```

3. <span data-ttu-id="17cfa-169">Получите связь с соединителя файла для активов.</span><span class="sxs-lookup"><span data-stu-id="17cfa-169">Get an association to the file connector for the assets.</span></span>
    
    ```c#
    // Associate file connector for assets
                FileSystemConnector connector = new FileSystemConnector(@"c:\temp\pnpprovisioningdemo", "");
                template.Connector = connector;
    
    ```

4. <span data-ttu-id="17cfa-170">(Необязательно) Из-за подготовки шаблона экземпляра объекта, можно написать код для настройки артефактов сайта во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="17cfa-170">(Optional) Because the provisioning template is an object instance, we can write code to customize site artifacts on the fly.</span></span> <span data-ttu-id="17cfa-171">В этом случае мы добавили новый список «контакт».</span><span class="sxs-lookup"><span data-stu-id="17cfa-171">In this instance, we're adding a new "contact" list.</span></span>
    
    ```c#
    // Since template is actual object, we can modify this using code as needed
                template.Lists.Add(new ListInstance()
                {
                    Title = "PnP Sample Contacts",
                    Url = "lists/PnPContacts",
                    TemplateType = (Int32)ListTemplateType.Contacts,
                    EnableAttachments = true
                });
    ```

5.  <span data-ttu-id="17cfa-172">Применение подготовки шаблона в новый сайт еще раз с помощью одной строки кода.</span><span class="sxs-lookup"><span data-stu-id="17cfa-172">Apply the provisioning template to the new site, again using one line of code.</span></span>
    
    ```c#
        web.ApplyProvisioningTemplate(template, ptai);
    ```

## <a name="additional-resources"></a><span data-ttu-id="17cfa-173">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="17cfa-173">Additional resources</span></span>
<span data-ttu-id="17cfa-174"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="17cfa-174"></span></span>

- [<span data-ttu-id="17cfa-175">PnP подготовки framework</span><span class="sxs-lookup"><span data-stu-id="17cfa-175">PnP provisioning framework</span></span>](pnp-provisioning-framework.md)
    
- [<span data-ttu-id="17cfa-176">Библиотека базовых и PnP модуля подготовки</span><span class="sxs-lookup"><span data-stu-id="17cfa-176">PnP provisioning engine and the core library</span></span>](pnp-provisioning-engine-and-the-core-library.md)
