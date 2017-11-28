---
title: "Использование асинхронной операции в SharePoint надстройки"
ms.date: 11/03/2017
ms.openlocfilehash: 3bf311c7084c6dba5e4faecb2ebfbd9edd6e4f86
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-asynchronous-operations-in-sharepoint-add-ins"></a>Использование асинхронной операции в SharePoint надстройки

Реализация асинхронной операции в SharePoint надстройки с помощью Microsoft Azure WebJobs.

_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

В примере [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) показано, как для создания и выполнения асинхронной операции с помощью провайдера надстройки и Azure WebJobs в Office 365.

Используйте для этого решения:

- Повысить производительность вашего удаленных приемников событий.
    
- Перенос в SharePoint Online и реализации той же функциональности задания таймера, вы имели в локальной среде SharePoint. 
    
- Реализация длительных операций, которые будут выполняться для среды SharePoint. Например:
    
    -  События **AppInstalled** , на которых выполняется больше, чем интервал времени ожидания 30 секунд. Есть асинхронных процессы в обработчиках событий надстройки. Дополнительные сведения можно [обрабатывать события в SharePoint надстройки](http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx) и [Создание приемника событий надстройки в SharePoint надстройки](http://msdn.microsoft.com/library/f40c910f-12a2-4caa-8e91-c7a61ae540db%28Office.15%29.aspx).
    
    - Подготовки настраиваемого сайта семейства сайтов.
    
    - Операции, которые синхронизации данных между локальными системами и Office 365.
    
    - Операции, которые выполняют сложные вычисления.
    
На следующей схеме показана высокоуровневая архитектура необходимые компоненты и поток обработки среди этих компонентов при выполнении асинхронной операции.

![Диаграмма, показывающая поток асинхронной операции. Надстройка SharePoint вызывает у поставщика надстройки, который добавляет сообщение в очередь хранилища Azure. WebJob Azure обрабатывает сообщение и начинает действовать на сайте SharePoint.](media/use-asynchronous-operations-in-sharepoint-add-ins/a4abdcc1-504c-46d7-9f6d-ea209d994605.png)

Для реализации асинхронной операции в надстройка размещением у поставщика с помощью Azure WebJobs:

1. Пользователям запускать надстройки, развернутые в SharePoint Online.
    
2. Надстройка размещением у поставщика дает входные параметры, необходимые для Azure WebJob и затем добавляет нового сообщения в очереди хранилища Azure.
    
3. Очереди Azure хранилища инициирует событие в постоянно работает WebJob Azure, чтобы начать обработку нового сообщения.
    
4. Azure WebJob запускает настраиваемых бизнес-логики на веб-узле SharePoint Online. 
    
**Примечание:**  Добавление сообщения в очередь хранилища Azure использует процесс отличается от процесса, на котором выполняется Azure WebJob. Таким образом надстройка можно реализовать асинхронной операции путем добавления новых сообщений в очередь с использованием одного процесса, а затем с помощью Azure WebJob для обработки этих сообщений в другом процессе. 

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузить пример надстройки [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев и затем создание учетной записи Azure, добавить сведения для этой учетной записи и убедитесь, что запущен Azure WebJob.

Создание учетной записи хранилища Azure для доступа к очереди Azure хранения:

1. Вход на портал Microsoft [портала управления Azure](https://manage.windowsazure.com).
    
2. Выберите команду **Создать** > **Data Services** > **хранения** > **Быстрое создание**.
    
3. В **URL-адрес**введите имя домена. Например введите **contoso**. 
    
4. **РАСПОЛОЖЕНИЕ/СХОДСТВА группы**и выберите нужное место.
    
5. В **репликации**выберите **Географически избыточных**. 
    
6. Выберите **Создать учетную запись ХРАНИЛИЩА**.
    
Добавление сведений учетной записи только что созданный хранения:

1. При создании учетной записи хранилища Azure, выберите пункт **УПРАВЛЕНИЕ ключи доступа**.
    
2. В области **Управления ключами доступа**скопируйте **Имя учетной записи ХРАНИЛИЩА** и **Первичный ключ доступа**.
    
3. Применение идентификатор клиента, секрет клиента и сведений об учетной записи хранилища Azure в несколько файлов конфигурации. 
    
4. В Project\Core.QueueWebJobUsage.Console.SendMessage вспомогательных откройте Program.cs и введите URL-адрес сайта в поле **siteUrl** .
    
5. В окне **Свойства** на Core.QueueWebJobUsage.Job значение **Локальной копии** **значение True** для ссылки на **Microsoft.SharePoint.Client** и **Microsoft.SharePoint.Client.Runtime** . Установка для **Локальной копии** копий **значение True,** на который указывает ссылка сборки в Azure, чтобы Azure WebJob можно разрешить ссылки на следующие сборки.
    
6. Развертывание Azure WebJob. Дополнительные сведения можно [Развернуть WebJobs проекта](https://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#deploy). 
    
Чтобы проверить, что ваше WebJob Azure работает:

1. Вход на портал [портала управления Azure](https://manage.windowsazure.com).
    
2. Выберите **веб-приложений**и выберите веб-сайты Microsoft Azure, выполнен вход. 
    
3. Выберите **WEBJOBS**.
    
4. Убедитесь, что вашей WebJob Azure появится в списке, и этот **ГРАФИК** имеет значение **работает непрерывно**.
    
5. Нажмите кнопку **Настройка**.
    
6. В разделе **параметры надстроек**создание новых параметров надстройки для **ClientId** и **ClientSecret**. Копирование файла Core.QueueWebJobUsage.Job\app.config пары ключ значение **ClientId** и **ClientSecret** .
    
7. В **строках подключения**создайте новые строки подключения для **AzureWebJobsDashboard** и **AzureWebJobsStorage**. Скопируйте **AzureWebJobsDashboard** и **AzureWebJobsStorage** ключ (имя) и пары "значение" из файла Core.QueueWebJobUsage.Job\app.config, а затем установите тип **настраиваемого**.
    
8. Выберите команду **Сохранить**.

### <a name="apply-configuration-settings"></a>Применение параметров конфигурации

Используйте сведения в следующей таблице для применения параметров конфигурации для решения Core.QueueWebJobUsage Visual Studio.

|**Расположение файлов**|**Ключ для обновления**|**Сведения о значение для обновления**|
|:-----|:-----|:-----|
|Вспомогательные Project\Core.QueueWebJobUsage.Console.SendMessage\app.config| **StorageConnectionString**| Замените **[имя вашей учетной записи]** имя учетной записи хранилища, скопированные из портала управления Azure.|
||| Замените **[Ключ учетной записи]** ключ основного доступа, скопированные из портала управления Azure.|
|Core.QueueWebJobUsageWeb\web.config| **StorageConnectionString**| Замените **[YourAccountName]** имя учетной записи хранилища, скопированные из портала управления Azure.|
||| Замените **[YourAccountKey]** с ключом доступа основной, скопированные из портала управления Azure.|
|Core.QueueWebJobUsage.Job\app.config| **StorageConnectionString**| Замените **[YourAccountName]** имя учетной записи хранилища, скопированные из портала управления Azure.|
||| Замените **[YourAccountKey]** с ключом доступа основной, скопированные из портала управления Azure.|
|| **ClientId**| Замените идентификатор клиента, скопированные из Core.QueueWebJobUsageWeb\web.config **[Добавить идентификатора]** .|
|| **ClientSecret**| Замените **[Add-in секрет]** секрета клиента, скопированные из Core.QueueWebJobUsageWeb\web.config.|
|| **AzureWebJobsDashboard**| Замените **[YourAccount]** имя учетной записи хранилища, скопированные из портала управления Azure.|
||| Замените **[YourKey]** с ключом доступа основной, скопированные из портала управления Azure.|
|| **AzureWebJobsStorage**| Замените **[YourAccount]** имя учетной записи хранилища, скопированные из портала управления Azure.|
||| Замените **[YourKey]** с ключом доступа основной, скопированные из портала управления Azure.|

**Примечание:**  Если **ClientId** и **ClientSecret** в Core.QueueWebJobUsageWeb обновляется, например, при увеличить номер версии файла AppManifest.XML, убедитесь, что обновление **ClientId** и **ClientSecret** в Core.QueueWebJobUsage.Job\app.config.

## <a name="using-the-corequeuewebjobusage-add-in"></a>С помощью надстройки Core.QueueWebJobUsage

В следующей таблице описываются все проекты Visual Studio в решении Core.QueueWebJobUsage.

|**Проект Visual Studio**|**Описание**|
|:-----|:-----|
|Core.QueueWebJobUsage|Проект надстройки SharePoint. Необходимы следующие разрешения:<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>AllowAppOnlyPolicy</p></li><li><p>Разрешения на полный доступ в Интернете.</p></li></ul>|
|Core.QueueWebJobUsage.Common|Содержит бизнес-объекты и код бизнес-логики &mdash; например методов для добавления сообщений в очередь хранилища &mdash; для этого решения. Этот проект включен для совместного использования бизнес-объекты и бизнес-логики от разных проектов. Это не может потребоваться в реализации.|
|Core.QueueWebJobUsage.Job|WebJob Azure, на котором выполняется при добавлении новых сообщений в очередь хранилища Azure. Этот проект содержит код вашей настраиваемых бизнес-логики. |
|Core.QueueWebJobUsageWeb|Размещение у поставщика надстройки, которая содержит пользовательский Интерфейс для проекта Core.QueueWebJobUsage. |
|Вспомогательные Project\Core.QueueWebJobUsage.Console.SendMessage|Проект модуля поддержки, который может использоваться для проверки сведений об учетной записи хранилища и процесс создания очередей и отправлять сообщения в очередь для обработки без настройки всего решения, описанного в данной статье. |

При запуске примера кода Core.QueueWebJobUsage надстройки размещением у поставщика отображается и отображаются две кнопки: **синхронный режим** и **асинхронной операции**. При выборе **синхронный режим** **btnSync_Click** в Pages\Default.aspx моделирует синхронный процесс длительным. В этом примере кода **btnSync_Click** помещает текущего потока в спящий режим на 10 секунд, а затем создает библиотеки документов. При выборе **асинхронной операции** **btnAsync_Click** в Pages\Default.aspx выполняет следующие действия:

1. Получает текущего пользователя.
    
2. Создает объект business **SiteModifyRequest** , в которой хранятся данные для включения в сообщения, отправляемые в очередь хранилища Azure. В этом примере кода отправляемых данных включает в себя имя текущего пользователя и URL-адрес текущего сайта.
    
3. Вызывает **SiteManager(). AddAsyncOperationRequestToQueue** для добавления сообщения в очередь хранилища Azure.
    
**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
protected void btnAsync_Click(object sender, EventArgs e)
        {

            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);

            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                // Get the current user.
                var currUser = clientContext.Web.CurrentUser;
                clientContext.Load(currUser);
                clientContext.ExecuteQuery();

                // Create business object, and then add the request to the queue.
                SiteModifyRequest request = new SiteModifyRequest() { RequestorName = currUser.Title, SiteUrl = Page.Request["SPHostUrl"] };
                new SiteManager().AddAsyncOperationRequestToQueue(request,
                                                                  ConfigurationManager.AppSettings["StorageConnectionString"]);

                processViews.ActiveViewIndex = 1;
                lblStatus.Text = "Asynchronous operation to create document library started.";
            }
        }
```

В Core.QueueWebJobUsage.Common в SiteManager.cs **AddAsyncOperationRequestToQueue** выполняет следующие действия:

1. Создает объект [CloudStorageAccount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx) с помощью **AccountName** и **AccountKey** сведений о конфигурации в файле Core.QueueWebJobUsageWeb\web.config.
    
2. Создает клиент обмена хранилища Azure очереди с помощью [CloudStorageAccount.CreateCloudQueueClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.createcloudqueueclient.aspx).
    
3. Использует [CloudQueueClient.GetQueueReference](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueueclient.getqueuereference.aspx) для получения ссылки на хранилища Azure очередь с именем, равное значению **SiteManager.StorageQueueName** , константу.
    
4. [CloudQueue.CreateIfNotExists](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.createifnotexists.aspx) используется для создания очереди хранилища Azure, если не существует.
    
5. Использует [CloudQueue.AddMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) для добавления новых сообщений в очередь хранилища Azure. Бизнес-объект **modifyRequest** преобразуется в объект [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) , который добавляется в очередь хранилища Azure.

```C#
public void AddAsyncOperationRequestToQueue(SiteModifyRequest modifyRequest, 
                                                    string storageConnectionString)
        {
            CloudStorageAccount storageAccount =
                                CloudStorageAccount.Parse(storageConnectionString);

            // Get queue or create a new one if one does not exist.
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
            CloudQueue queue = queueClient.GetQueueReference(SiteManager.StorageQueueName);
            queue.CreateIfNotExists();

            // Add a message to queue.
            queue.AddMessage(new CloudQueueMessage(JsonConvert.SerializeObject(modifyRequest)));
        }
```

После добавления сообщения в очередь хранилища Azure постоянно работает WebJob Azure ожидает и затем обрабатывает нового сообщения. Azure WebJob определяется в Core.QueueWebJobUsage.Job. При выполнении Azure WebJob Main в Core.QueueWebJobUsage.Job\Program.cs создает новый **JobHost**, а затем вызывает **RunAndBlock**. Вызовы методов **JobHost** координаты помечается атрибутом **QueueTrigger** и контрольные значения для сообщений в определенной очереди. **RunAndBlock** гарантирует, что Azure WebJob работает постоянно и вызывает **ProcessQueueMessage**, то есть метод запуск при добавлении нового сообщения в очередь хранилища Azure. Пакет SDK для Azure WebJobs связывает **основной** поток с **ProcessQueueMessage**. Для получения дополнительных сведений см. [Создание WebJob .NET в Azure службы надстройки](https://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).

```C#
static void Main()
        {
            var host = new JobHost();
            // The following code ensures that the WebJob will run continuously.
            host.RunAndBlock();
        }
```

**ProcessQueueMessage** обрабатывает новые сообщения, которые добавлены в хранилище Azure очередь с:

1. С помощью атрибута **QueueTrigger** выполнять запуск **ProcessQueueMessage** при записи в очередь с именем равно значению **SiteManager.StorageQueueName**нового сообщения.
    
2. Запись в журнал для Azure WebJob с помощью переменной **журнала** , переданный в качестве параметра **ProcessQueueMessage**.
    
3. Вызов **SiteManager(). PerformSiteModification** для выполнения бизнес-процесса длительным на сайте. В этом примере кода поток помещается в спящий режим на 10 секунд, а затем создается библиотеки документов.

```C#
public static void ProcessQueueMessage(
            [QueueTrigger(SiteManager.StorageQueueName)] 
            SiteModifyRequest modifyRequest, TextWriter log)
        {
            log.WriteLine(string.Format("{0} '{1}' {2} '{3}'.",
                            "Received new site modification request with URL", 
                            modifyRequest.SiteUrl, 
                            "from person named as ", 
                            modifyRequest.RequestorName));
            
            try
            {
                Uri targetSite = new Uri(modifyRequest.SiteUrl);
                
                // Get the realm for the URL.
                string realm = TokenHelper.GetRealmFromTargetUrl(targetSite);

                // Get the access token for the URL.  
                // Requires this add-in to be registered with the tenant.
                string accessToken = TokenHelper.GetAppOnlyAccessToken(
                                                    TokenHelper.SharePointPrincipal,
                                                    targetSite.Authority, realm).AccessToken;

                // Get client context with access token.
                using (var ctx =
                    TokenHelper.GetClientContextWithAccessToken(
                                                    targetSite.ToString(), accessToken))
                {
                    // Call business logic code.
                    new SiteManager().PerformSiteModification(ctx, modifyRequest);
                }
            }
            catch (Exception ex)
            {
                log.WriteLine(string.Format("Site modification to URL {0} failed with following details.", modifyRequest.SiteUrl));
                log.WriteLine(ex.ToString());
                throw;
            }
        }
```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).
    
- [Использование удаленных приемников событий в SharePoint](Use-remote-event-receivers-in-SharePoint.md)
    
- [Журнал изменений запросов SharePoint с ChangeQuery и маркер изменения](query-sharepoint-change-log-with-changequery-and-changeToken.md)
