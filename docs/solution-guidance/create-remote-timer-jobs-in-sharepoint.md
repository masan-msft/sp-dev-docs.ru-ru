---
title: "Создание задания таймера удаленные в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: e9cf373ef4ba81b66c9bfa340b650dd71548f006
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-remote-timer-jobs-in-sharepoint"></a>Создание задания таймера удаленные в SharePoint

Создание задания таймера удаленного в SharePoint для выполнения задач фон для управления и управляющие среды.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Создание задания таймера удаленного управления SharePoint, мониторинга и выполняют действия с данными SharePoint. Не выполняйте задания таймера удаленного на SharePoint server. Вместо этого задания таймера удаленного, назначенные задания, которые запускаются на другой сервер. Примеры использования задания таймера:

- Для выполнения задач управления, например отображения сообщения на сайте, определенным условиям не выполняются или применение политики хранения.
    
- Выполнение запланированного процессов, которые являются процессор.

## <a name="before-you-begin-to-create-a-remote-timer-job"></a>Прежде чем приступить к созданию задания таймера удаленного

Чтобы начать работу, загрузите пример надстройки [Core.TimerJobs.Samples](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

Чтобы начать использование Core.TimerJobs.Samples решения, необходимо выбрать запускаемый проект, например проект SimpleJob, откройте контекстное меню (щелкнув правой кнопкой мыши) **Core.TimerJobs.Samples.SimpleJob**, а затем выбрать **задаются в виде Запускаемый проект**.

> [!NOTE] 
> При создании нового проекта в Visual Studio для создания вашего нового задания таймера удаленного, добавьте в проект пакетов NuGet **OfficeDevPnP.Core** . В Visual Studio выберите в меню **Сервис** > **Диспетчер пакетов NuGet** > **Управление пакетами NuGet для решения**.

## <a name="schedule-your-remote-timer-job"></a>Задания таймера удаленного

Задания таймера можно запланировать один раз выполнить или может быть повторяющегося задания. Для задания таймера удаленного в рабочей среде, требуется для компиляции кода в .exe-файл, а затем запустите файл .exe, с помощью планировщиком заданий Windows или WebJob Microsoft Azure. Дополнительные сведения по [развертыванию параметры задания таймера](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#timer-job-deployment-options).

## <a name="use-the-coretimerjobssamplessimplejob-add-in"></a>Использовать надстройки Core.TimerJobs.Samples.SimpleJob

В Core.TimerJobs.Samples.SimpleJob, **Main** в файле Program.cs необходимо выполнить следующие действия:

1. Создает объект SimpleJob, который наследуется из базового класса [OfficeDevPnP.Core.Framework.TimerJobs.TimerJob](https://github.com/SharePoint/PnP/blob/dev/OfficeDevPnP.Core/OfficeDevPnP.Core/Framework/TimerJobs/TimerJob.cs) .
    
2. Задает учетные данные пользователя Office 365 для использования при запуске задания таймера с помощью **TimerJob.UseOffice365Authentication**. Учетные данные пользователя необходимы соответствующие права доступа для семейств веб-сайтов. Дополнительные сведения по [проверки подлинности](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md#authentication).
    
3. Добавление сайтов, что задание таймера на использование **TimerJob.AddSite**следует выполнить задачи. При необходимости можно Повторите инструкцию **TimerJob.AddSite** , чтобы добавить несколько узлов или добавление всех сайтов в разделе определенного URL-адреса с помощью подстановочный знак *. Например, http://contoso.sharepoint.com/sites/* задание таймера, которое будет выполняться на всех сайтах в разделе управляемый путь **sites** .
    
4. Выводит сведения о задания таймера и запускается задание таймера с помощью **PrintJobSettingsAndRunJob**.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

При создании объекта **simpleJob** , конструктор **SimpleJob** :

1. Вызывает конструктор базового класса задания таймера. 
    
2. Назначает **SimpleJob_TimerJobRun** обработчика событий для обработки событий **TimerJobRun** . **SimpleJob_TimerJobRun** запускается при вызове **TimerJob.Run**, которое описывается более подробно далее в этой статье.

```C#
public SimpleJob() : base("SimpleJob")
        {
            TimerJobRun += SimpleJob_TimerJobRun;
        }
```

При выполнении **PrintJobSettingsAndRunJob** выходные данные задания таймера, записывается в окне консоли, а затем, называется **TimerJob.Run** .

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

**TimerJob.Run** вызывает события **TimerJobRun** . **TimerJob.Run** вызывает **SimpleJob_TimerJobRun** SimpleJob.cs, которое было задано как обработчик событий для обработки событий **TimerJobRun** в конструкторе **SimpleJob**. В **SimpleJob_TimerJobRun**можно добавить пользовательский код, который будет вашего задания таймера для выполнения при запуске задания таймера. **SimpleJob_TimerJobRun** запускает свой код на веб-сайтах, добавленную с помощью **TimerJob.AddSite** в файле Program.cs. В этом примере кода **SimpleJob_TimerJobRun** используется **ClientContext** из **задания таймера** для записи заголовок сайта в окне консоли. Если несколько сайтов были добавлены с помощью **TimerJob.AddSite** , **SimpleJob_TimerJobRun** вызывается для каждого сайта.

```C#
 void SimpleJob_TimerJobRun(object sender, TimerJobRunEventArgs e)
        {
            e.WebClientContext.Load(e.WebClientContext.Web, p => p.Title);
            e.WebClientContext.ExecuteQueryRetry();
            Console.WriteLine("Site {0} has title {1}", e.Url, e.WebClientContext.Web.Title);
        }
```

## <a name="example-content-type-retention-enforcement-timer-job"></a>Пример: Задание таймера принудительное применение хранения типа контента

Проект Core.TimerJobs.Samples.ContentTypeRetentionEnforcementJob показано, как можно использовать задания таймера SharePoint для применения политики хранения для типов контента. С помощью элемента **ContentTypeRetentionPolicyPeriod** в файле app.config, укажите:

-  **ключ**, который является идентификатор типа контента, которое применяется период хранения для типа контента.
    
-  **значение**, которое срок хранения в днях. Период хранения будет применяться ко всем элементам списка, созданные с помощью типа контента, указанного в **ключ**.

```XML
<ContentTypeRetentionPolicyPeriod>
    <!-- Key is the content type ID, and value is the retention period in days -->
    <!-- Specifies an audio content type should be kept for 183 days -->
    <add key="0x0101009148F5A04DDD49cbA7127AADA5FB792B006973ACD696DC4858A76371B2FB2F439A" value="183" />
    <!-- Specifies a document content type should be kept for 365 days -->   
    <add key="0x0101" value="365" />
</ContentTypeRetentionPolicyPeriod>
```

**ContentTypeRetentionEnforcementJob_TimerJobRun** задано как обработчик событий для события **TimerJobRun** . При вызове **TimerJob.Run** в файле Program.cs на каждом сайте, который был добавлен с помощью **TimerJob.AddSite** в файле Program.cs **ContentTypeRetentionEnforcementJob_TimerJobRun** необходимо выполнить следующие действия:


1. Получает все библиотеки документов на сайте.
    
2. Для каждого документа библиотеки на сайте считывает сведения о конфигурации, указанное в **ContentTypeRetentionPolicyPeriod** в файле app.config. Для каждого типа контента идентификатор и хранения периода пары, считанный из app.config называется **ApplyRetentionPolicy** .

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

**ApplyRetentionPolicy** принудительного применения политики хранения настраиваемых действий с:

1. Расчет **validationDate**. Метод **ApplyRetentionPolicy** обеспечивает выполнение действия политики хранения на документы, измененные до **validationDate**. Затем **validationDate** формате CAML даты и назначается **camlDate**.
    
2. Выполнение запроса CAML для фильтрации документов в библиотеку документов на основе кода типа контента, который был задан в файле app.config и где дата **Автор изменений** меньше, чем **camlDate**.
    
3. Для каждого элемента списка применение хранения настраиваемых действий, выполняемых над документами, с использованием пользовательского кода.

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

## <a name="example-governance-timer-job"></a>Пример: Задание таймера управления

Проект Core.TimerJobs.Samples.GovernanceJob убедитесь, что назначается два администраторам семейств веб-сайтов с помощью заданий таймера и если это не так, отобразит уведомление на сайте.

**SiteGovernanceJob_TimerJobRun** задано как обработчик событий для события **TimerJobRun** . При вызове **TimerJob.Run** в файле Program.cs на каждого семейства веб-сайтов, который был добавлен с помощью **TimerJob.AddSite** в файле Program.cs **SiteGovernanceJob_TimerJobRun** необходимо выполнить следующие действия:

1. Получает число администраторов, назначенных для семейства сайтов, с помощью метода расширения [GetAdministrators](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/SecurityExtensions.cs) , которая является частью [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core).
    
2. Загружает файл JavaScript с помощью [UploadFile](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/FileFolderExtensions.cs), которая является частью [OfficeDevPnP.Core](https://github.com/SharePoint/PnP/tree/master/OfficeDevPnP.Core)списка SiteAssets или Библиотека стилей. 
    
3. Если сайт должен меньше, чем два администратора, [AddJSLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs) добавляет сообщение уведомления на сайт с помощью JavaScript. Дополнительные сведения по [Настройка сайта SharePoint пользовательского интерфейса с помощью JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md).
    
4. Если сайт имеет два или более администраторов, сообщение уведомления удаляется при помощи [DeleteJsLink](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/OfficeDevPnP.Core/AppModelExtensions/JavaScriptExtensions.cs).

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Шаблоны и рекомендации решений разработки Office 365](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [Руководство по с помощью Framework задания таймера](https://github.com/SharePoint/PnP/blob/master/OfficeDevPnP.Core/TimerJob%20Framework.md)
    
- [Framework задания таймера](https://github.com/SharePoint/PnP/tree/dev/Solutions/Core.TimerJobs.Samples)
