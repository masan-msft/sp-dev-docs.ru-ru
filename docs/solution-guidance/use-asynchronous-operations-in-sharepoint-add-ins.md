---
title: "Использование асинхронной операции в SharePoint надстройки"
ms.date: 11/03/2017
ms.openlocfilehash: 3bf311c7084c6dba5e4faecb2ebfbd9edd6e4f86
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-asynchronous-operations-in-sharepoint-add-ins"></a><span data-ttu-id="6a068-102">Использование асинхронной операции в SharePoint надстройки</span><span class="sxs-lookup"><span data-stu-id="6a068-102">Use asynchronous operations in SharePoint Add-ins</span></span>

<span data-ttu-id="6a068-103">Реализация асинхронной операции в SharePoint надстройки с помощью Microsoft Azure WebJobs.</span><span class="sxs-lookup"><span data-stu-id="6a068-103">Implement asynchronous operations in SharePoint Add-ins by using Microsoft Azure WebJobs.</span></span>

<span data-ttu-id="6a068-104">_**Применимо к:** SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="6a068-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="6a068-105">В примере [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) показано, как для создания и выполнения асинхронной операции с помощью провайдера надстройки и Azure WebJobs в Office 365.</span><span class="sxs-lookup"><span data-stu-id="6a068-105">The [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) sample shows you how to create and run asynchronous operations by using provider-hosted add-ins and Azure WebJobs in Office 365.</span></span>

<span data-ttu-id="6a068-106">Используйте для этого решения:</span><span class="sxs-lookup"><span data-stu-id="6a068-106">Use this solution to:</span></span>

- <span data-ttu-id="6a068-107">Повысить производительность вашего удаленных приемников событий.</span><span class="sxs-lookup"><span data-stu-id="6a068-107">Improve performance of your remote event receivers.</span></span>
    
- <span data-ttu-id="6a068-108">Перенос в SharePoint Online и реализации той же функциональности задания таймера, вы имели в локальной среде SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a068-108">Migrate to SharePoint Online and implement the same timer job functionality that you had in your SharePoint on-premises environment.</span></span> 
    
- <span data-ttu-id="6a068-109">Реализация длительных операций, которые будут выполняться для среды SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a068-109">Implement long-running operations that you want to run against your SharePoint environment.</span></span> <span data-ttu-id="6a068-110">Например:</span><span class="sxs-lookup"><span data-stu-id="6a068-110">For example:</span></span>
    
    -  <span data-ttu-id="6a068-111">События **AppInstalled** , на которых выполняется больше, чем интервал времени ожидания 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="6a068-111">**AppInstalled** events that run longer than the 30-second time-out interval.</span></span> <span data-ttu-id="6a068-112">Есть асинхронных процессы в обработчиках событий надстройки.</span><span class="sxs-lookup"><span data-stu-id="6a068-112">There are asynchronous processes in add-in event handlers.</span></span> <span data-ttu-id="6a068-113">Дополнительные сведения можно [обрабатывать события в SharePoint надстройки](http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx) и [Создание приемника событий надстройки в SharePoint надстройки](http://msdn.microsoft.com/library/f40c910f-12a2-4caa-8e91-c7a61ae540db%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a068-113">For more information, see [Handle events in SharePoint Add-ins](http://msdn.microsoft.com/library/c050d056-8548-4496-a053-016779d723d9%28Office.15%29.aspx) and [Create an add-in event receiver in SharePoint Add-ins](http://msdn.microsoft.com/library/f40c910f-12a2-4caa-8e91-c7a61ae540db%28Office.15%29.aspx).</span></span>
    
    - <span data-ttu-id="6a068-114">Подготовки настраиваемого сайта семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="6a068-114">Custom site collection provisioning.</span></span>
    
    - <span data-ttu-id="6a068-115">Операции, которые синхронизации данных между локальными системами и Office 365.</span><span class="sxs-lookup"><span data-stu-id="6a068-115">Operations that synchronize data between Office 365 and your on-premises systems.</span></span>
    
    - <span data-ttu-id="6a068-116">Операции, которые выполняют сложные вычисления.</span><span class="sxs-lookup"><span data-stu-id="6a068-116">Operations that perform complex calculations.</span></span>
    
<span data-ttu-id="6a068-117">На следующей схеме показана высокоуровневая архитектура необходимые компоненты и поток обработки среди этих компонентов при выполнении асинхронной операции.</span><span class="sxs-lookup"><span data-stu-id="6a068-117">The following diagram shows a high-level architecture of the required components, and the processing flow among those components when an asynchronous operation is performed.</span></span>

![Диаграмма, показывающая поток асинхронной операции.](media/use-asynchronous-operations-in-sharepoint-add-ins/a4abdcc1-504c-46d7-9f6d-ea209d994605.png)

<span data-ttu-id="6a068-121">Для реализации асинхронной операции в надстройка размещением у поставщика с помощью Azure WebJobs:</span><span class="sxs-lookup"><span data-stu-id="6a068-121">To implement asynchronous operations in your provider-hosted add-in by using Azure WebJobs:</span></span>

1. <span data-ttu-id="6a068-122">Пользователям запускать надстройки, развернутые в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="6a068-122">Users run the add-in deployed in SharePoint Online.</span></span>
    
2. <span data-ttu-id="6a068-123">Надстройка размещением у поставщика дает входные параметры, необходимые для Azure WebJob и затем добавляет нового сообщения в очереди хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-123">The provider-hosted add-in gives input parameters required by the Azure WebJob, and then adds a new message to the Azure Storage queue.</span></span>
    
3. <span data-ttu-id="6a068-124">Очереди Azure хранилища инициирует событие в постоянно работает WebJob Azure, чтобы начать обработку нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="6a068-124">The Azure Storage queue triggers an event in a continuously running Azure WebJob to start processing the new message.</span></span>
    
4. <span data-ttu-id="6a068-125">Azure WebJob запускает настраиваемых бизнес-логики на веб-узле SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="6a068-125">The Azure WebJob runs custom business logic against your SharePoint Online site.</span></span> 
    
<span data-ttu-id="6a068-126">**Примечание:**  Добавление сообщения в очередь хранилища Azure использует процесс отличается от процесса, на котором выполняется Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="6a068-126">**Note:**  Adding a message to the Azure Storage queue uses a different process from the process that runs the Azure WebJob.</span></span> <span data-ttu-id="6a068-127">Таким образом надстройка можно реализовать асинхронной операции путем добавления новых сообщений в очередь с использованием одного процесса, а затем с помощью Azure WebJob для обработки этих сообщений в другом процессе.</span><span class="sxs-lookup"><span data-stu-id="6a068-127">Therefore, your add-in can implement asynchronous operations by adding new messages to the queue using one process, and then by using the Azure WebJob to handle those messages in another process.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="6a068-128">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6a068-128">Before you begin</span></span>

<span data-ttu-id="6a068-129">Чтобы начать работу, загрузить пример надстройки [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев и затем создание учетной записи Azure, добавить сведения для этой учетной записи и убедитесь, что запущен Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="6a068-129">To get started, download the [Core.QueueWebJobUsage](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.QueueWebJobUsage) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub, and then create an Azure account, add details to that account, and verify that Azure WebJob is running.</span></span>

<span data-ttu-id="6a068-130">Создание учетной записи хранилища Azure для доступа к очереди Azure хранения:</span><span class="sxs-lookup"><span data-stu-id="6a068-130">To create an Azure Storage account to access the Azure storage queue:</span></span>

1. <span data-ttu-id="6a068-131">Вход на портал Microsoft [портала управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6a068-131">Sign in to your Microsoft [Azure Management Portal](https://manage.windowsazure.com).</span></span>
    
2. <span data-ttu-id="6a068-132">Выберите команду **Создать** > **Data Services** > **хранения** > **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="6a068-132">Choose  **New** > **Data Services** > **Storage** > **Quick Create**.</span></span>
    
3. <span data-ttu-id="6a068-133">В **URL-адрес**введите имя домена.</span><span class="sxs-lookup"><span data-stu-id="6a068-133">In  **URL**, enter your domain name.</span></span> <span data-ttu-id="6a068-134">Например введите **contoso**.</span><span class="sxs-lookup"><span data-stu-id="6a068-134">For example, enter  **contoso**.</span></span> 
    
4. <span data-ttu-id="6a068-135">**РАСПОЛОЖЕНИЕ/СХОДСТВА группы**и выберите нужное место.</span><span class="sxs-lookup"><span data-stu-id="6a068-135">In  **LOCATION/AFFINITY GROUP**, choose an appropriate location.</span></span>
    
5. <span data-ttu-id="6a068-136">В **репликации**выберите **Географически избыточных**.</span><span class="sxs-lookup"><span data-stu-id="6a068-136">In  **REPLICATION**, choose  **Geo-Redundant**.</span></span> 
    
6. <span data-ttu-id="6a068-137">Выберите **Создать учетную запись ХРАНИЛИЩА**.</span><span class="sxs-lookup"><span data-stu-id="6a068-137">Choose  **CREATE STORAGE ACCOUNT**.</span></span>
    
<span data-ttu-id="6a068-138">Добавление сведений учетной записи только что созданный хранения:</span><span class="sxs-lookup"><span data-stu-id="6a068-138">To add details to your newly created storage account:</span></span>

1. <span data-ttu-id="6a068-139">При создании учетной записи хранилища Azure, выберите пункт **УПРАВЛЕНИЕ ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="6a068-139">When the Azure Storage account is created, choose  **MANAGE ACCESS KEYS**.</span></span>
    
2. <span data-ttu-id="6a068-140">В области **Управления ключами доступа**скопируйте **Имя учетной записи ХРАНИЛИЩА** и **Первичный ключ доступа**.</span><span class="sxs-lookup"><span data-stu-id="6a068-140">In  **Manage Access Keys**, copy the  **STORAGE ACCOUNT NAME** and **PRIMARY ACCESS KEY**.</span></span>
    
3. <span data-ttu-id="6a068-141">Применение идентификатор клиента, секрет клиента и сведений об учетной записи хранилища Azure в несколько файлов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6a068-141">Apply the client ID, client secret, and your Azure Storage account information to several of the configuration files.</span></span> 
    
4. <span data-ttu-id="6a068-142">В Project\Core.QueueWebJobUsage.Console.SendMessage вспомогательных откройте Program.cs и введите URL-адрес сайта в поле **siteUrl** .</span><span class="sxs-lookup"><span data-stu-id="6a068-142">In Helper Project\Core.QueueWebJobUsage.Console.SendMessage, open Program.cs and enter the URL of your site in the  **siteUrl** box.</span></span>
    
5. <span data-ttu-id="6a068-143">В окне **Свойства** на Core.QueueWebJobUsage.Job значение **Локальной копии** **значение True** для ссылки на **Microsoft.SharePoint.Client** и **Microsoft.SharePoint.Client.Runtime** .</span><span class="sxs-lookup"><span data-stu-id="6a068-143">In  **Properties** on the Core.QueueWebJobUsage.Job, set **Copy Local** to **True** on the **Microsoft.SharePoint.Client** and **Microsoft.SharePoint.Client.Runtime** references.</span></span> <span data-ttu-id="6a068-144">Установка для **Локальной копии** копий **значение True,** на который указывает ссылка сборки в Azure, чтобы Azure WebJob можно разрешить ссылки на следующие сборки.</span><span class="sxs-lookup"><span data-stu-id="6a068-144">Setting **Copy Local** to **True** copies the referenced assemblies to Azure so that the Azure WebJob can resolve the references to these assemblies.</span></span>
    
6. <span data-ttu-id="6a068-145">Развертывание Azure WebJob.</span><span class="sxs-lookup"><span data-stu-id="6a068-145">Deploy the Azure WebJob.</span></span> <span data-ttu-id="6a068-146">Дополнительные сведения можно [Развернуть WebJobs проекта](https://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#deploy).</span><span class="sxs-lookup"><span data-stu-id="6a068-146">For more information, see [Deploy a WebJobs project](https://azure.microsoft.com/documentation/articles/websites-dotnet-deploy-webjobs/#deploy).</span></span> 
    
<span data-ttu-id="6a068-147">Чтобы проверить, что ваше WebJob Azure работает:</span><span class="sxs-lookup"><span data-stu-id="6a068-147">To verify that your Azure WebJob is running:</span></span>

1. <span data-ttu-id="6a068-148">Вход на портал [портала управления Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="6a068-148">Sign in to your [Azure Management Portal](https://manage.windowsazure.com).</span></span>
    
2. <span data-ttu-id="6a068-149">Выберите **веб-приложений**и выберите веб-сайты Microsoft Azure, выполнен вход.</span><span class="sxs-lookup"><span data-stu-id="6a068-149">Choose  **web apps**, and then choose the Microsoft Azure Websites you entered.</span></span> 
    
3. <span data-ttu-id="6a068-150">Выберите **WEBJOBS**.</span><span class="sxs-lookup"><span data-stu-id="6a068-150">Choose  **WEBJOBS**.</span></span>
    
4. <span data-ttu-id="6a068-151">Убедитесь, что вашей WebJob Azure появится в списке, и этот **ГРАФИК** имеет значение **работает непрерывно**.</span><span class="sxs-lookup"><span data-stu-id="6a068-151">Verify that your Azure WebJob appears in the list, and that  **SCHEDULE** is set to **Runs continuously**.</span></span>
    
5. <span data-ttu-id="6a068-152">Нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="6a068-152">Choose  **CONFIGURE**.</span></span>
    
6. <span data-ttu-id="6a068-153">В разделе **параметры надстроек**создание новых параметров надстройки для **ClientId** и **ClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="6a068-153">In  **add-in settings**, create new add-in settings for  **ClientId** and **ClientSecret**.</span></span> <span data-ttu-id="6a068-154">Копирование файла Core.QueueWebJobUsage.Job\app.config пары ключ значение **ClientId** и **ClientSecret** .</span><span class="sxs-lookup"><span data-stu-id="6a068-154">Copy the **ClientId** and **ClientSecret** key-value pairs from the Core.QueueWebJobUsage.Job\app.config file.</span></span>
    
7. <span data-ttu-id="6a068-155">В **строках подключения**создайте новые строки подключения для **AzureWebJobsDashboard** и **AzureWebJobsStorage**.</span><span class="sxs-lookup"><span data-stu-id="6a068-155">In  **connection strings**, create new connection strings for  **AzureWebJobsDashboard** and **AzureWebJobsStorage**.</span></span> <span data-ttu-id="6a068-156">Скопируйте **AzureWebJobsDashboard** и **AzureWebJobsStorage** ключ (имя) и пары "значение" из файла Core.QueueWebJobUsage.Job\app.config, а затем установите тип **настраиваемого**.</span><span class="sxs-lookup"><span data-stu-id="6a068-156">Copy the **AzureWebJobsDashboard** and **AzureWebJobsStorage** key (name) and value pairs from the Core.QueueWebJobUsage.Job\app.config file, and then set the type to **Custom**.</span></span>
    
8. <span data-ttu-id="6a068-157">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6a068-157">Choose  **Save**.</span></span>

### <a name="apply-configuration-settings"></a><span data-ttu-id="6a068-158">Применение параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="6a068-158">Apply configuration settings</span></span>

<span data-ttu-id="6a068-159">Используйте сведения в следующей таблице для применения параметров конфигурации для решения Core.QueueWebJobUsage Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a068-159">Use the information in the following table to apply configuration settings to the Core.QueueWebJobUsage Visual Studio solution.</span></span>

|<span data-ttu-id="6a068-160">**Расположение файлов**</span><span class="sxs-lookup"><span data-stu-id="6a068-160">**File location**</span></span>|<span data-ttu-id="6a068-161">**Ключ для обновления**</span><span class="sxs-lookup"><span data-stu-id="6a068-161">**Key to update**</span></span>|<span data-ttu-id="6a068-162">**Сведения о значение для обновления**</span><span class="sxs-lookup"><span data-stu-id="6a068-162">**Value information to update**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="6a068-163">Вспомогательные Project\Core.QueueWebJobUsage.Console.SendMessage\app.config</span><span class="sxs-lookup"><span data-stu-id="6a068-163">Helper Project\Core.QueueWebJobUsage.Console.SendMessage\app.config</span></span>| <span data-ttu-id="6a068-164">**StorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="6a068-164">**StorageConnectionString**</span></span>| <span data-ttu-id="6a068-165">Замените **[имя вашей учетной записи]** имя учетной записи хранилища, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-165">Replace **[Your Account name]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="6a068-166">Замените **[Ключ учетной записи]** ключ основного доступа, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-166">Replace **[Your Account Key]** with the primary access key copied from the Azure Management Portal.</span></span>|
|<span data-ttu-id="6a068-167">Core.QueueWebJobUsageWeb\web.config</span><span class="sxs-lookup"><span data-stu-id="6a068-167">Core.QueueWebJobUsageWeb\web.config</span></span>| <span data-ttu-id="6a068-168">**StorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="6a068-168">**StorageConnectionString**</span></span>| <span data-ttu-id="6a068-169">Замените **[YourAccountName]** имя учетной записи хранилища, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-169">Replace **[YourAccountName]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="6a068-170">Замените **[YourAccountKey]** с ключом доступа основной, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-170">Replace **[YourAccountKey]** with the primary access key copied from the Azure Management Portal.</span></span>|
|<span data-ttu-id="6a068-171">Core.QueueWebJobUsage.Job\app.config</span><span class="sxs-lookup"><span data-stu-id="6a068-171">Core.QueueWebJobUsage.Job\app.config</span></span>| <span data-ttu-id="6a068-172">**StorageConnectionString**</span><span class="sxs-lookup"><span data-stu-id="6a068-172">**StorageConnectionString**</span></span>| <span data-ttu-id="6a068-173">Замените **[YourAccountName]** имя учетной записи хранилища, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-173">Replace **[YourAccountName]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="6a068-174">Замените **[YourAccountKey]** с ключом доступа основной, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-174">Replace **[YourAccountKey]** with the primary access key copied from the Azure Management Portal.</span></span>|
|| <span data-ttu-id="6a068-175">**ClientId**</span><span class="sxs-lookup"><span data-stu-id="6a068-175">**ClientId**</span></span>| <span data-ttu-id="6a068-176">Замените идентификатор клиента, скопированные из Core.QueueWebJobUsageWeb\web.config **[Добавить идентификатора]** .</span><span class="sxs-lookup"><span data-stu-id="6a068-176">Replace **[Your Add-in ID]** with the client ID copied from the Core.QueueWebJobUsageWeb\web.config.</span></span>|
|| <span data-ttu-id="6a068-177">**ClientSecret**</span><span class="sxs-lookup"><span data-stu-id="6a068-177">**ClientSecret**</span></span>| <span data-ttu-id="6a068-178">Замените **[Add-in секрет]** секрета клиента, скопированные из Core.QueueWebJobUsageWeb\web.config.</span><span class="sxs-lookup"><span data-stu-id="6a068-178">Replace **[Your Add-in Secret]** with the client secret copied from the Core.QueueWebJobUsageWeb\web.config.</span></span>|
|| <span data-ttu-id="6a068-179">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="6a068-179">**AzureWebJobsDashboard**</span></span>| <span data-ttu-id="6a068-180">Замените **[YourAccount]** имя учетной записи хранилища, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-180">Replace **[YourAccount]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="6a068-181">Замените **[YourKey]** с ключом доступа основной, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-181">Replace **[YourKey]** with the primary access key copied from the Azure Management Portal.</span></span>|
|| <span data-ttu-id="6a068-182">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="6a068-182">**AzureWebJobsStorage**</span></span>| <span data-ttu-id="6a068-183">Замените **[YourAccount]** имя учетной записи хранилища, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-183">Replace **[YourAccount]** with the storage account name copied from the Azure Management Portal.</span></span>|
||| <span data-ttu-id="6a068-184">Замените **[YourKey]** с ключом доступа основной, скопированные из портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-184">Replace **[YourKey]** with the primary access key copied from the Azure Management Portal.</span></span>|

<span data-ttu-id="6a068-185">**Примечание:**  Если **ClientId** и **ClientSecret** в Core.QueueWebJobUsageWeb обновляется, например, при увеличить номер версии файла AppManifest.XML, убедитесь, что обновление **ClientId** и **ClientSecret** в Core.QueueWebJobUsage.Job\app.config.</span><span class="sxs-lookup"><span data-stu-id="6a068-185">**Note:**  If the  **ClientId** and the **ClientSecret** in Core.QueueWebJobUsageWeb gets updated, for example, when you increment the version number in the AppManifest.xml, make sure you update the **ClientId** and the **ClientSecret** in the Core.QueueWebJobUsage.Job\app.config.</span></span>

## <a name="using-the-corequeuewebjobusage-add-in"></a><span data-ttu-id="6a068-186">С помощью надстройки Core.QueueWebJobUsage</span><span class="sxs-lookup"><span data-stu-id="6a068-186">Using the Core.QueueWebJobUsage add-in</span></span>

<span data-ttu-id="6a068-187">В следующей таблице описываются все проекты Visual Studio в решении Core.QueueWebJobUsage.</span><span class="sxs-lookup"><span data-stu-id="6a068-187">The following table describes all the Visual Studio projects in the Core.QueueWebJobUsage solution.</span></span>

|<span data-ttu-id="6a068-188">**Проект Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="6a068-188">**Visual Studio project**</span></span>|<span data-ttu-id="6a068-189">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6a068-189">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6a068-190">Core.QueueWebJobUsage</span><span class="sxs-lookup"><span data-stu-id="6a068-190">Core.QueueWebJobUsage</span></span>|<span data-ttu-id="6a068-191">Проект надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="6a068-191">Your SharePoint Add-in project.</span></span> <span data-ttu-id="6a068-192">Необходимы следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="6a068-192">The following permissions are required:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="6a068-193">AllowAppOnlyPolicy</span><span class="sxs-lookup"><span data-stu-id="6a068-193">AllowAppOnlyPolicy</span></span></p></li><li><p><span data-ttu-id="6a068-194">Разрешения на полный доступ в Интернете.</span><span class="sxs-lookup"><span data-stu-id="6a068-194">FullControl permissions on the Web.</span></span></p></li></ul>|
|<span data-ttu-id="6a068-195">Core.QueueWebJobUsage.Common</span><span class="sxs-lookup"><span data-stu-id="6a068-195">Core.QueueWebJobUsage.Common</span></span>|<span data-ttu-id="6a068-196">Содержит бизнес-объекты и код бизнес-логики &mdash; например методов для добавления сообщений в очередь хранилища &mdash; для этого решения.</span><span class="sxs-lookup"><span data-stu-id="6a068-196">Contains the business objects and business logic code &mdash; such as the methods to add messages to the storage queue &mdash; for this solution.</span></span> <span data-ttu-id="6a068-197">Этот проект включен для совместного использования бизнес-объекты и бизнес-логики от разных проектов.</span><span class="sxs-lookup"><span data-stu-id="6a068-197">This project is included to share business objects and business logic between different projects.</span></span> <span data-ttu-id="6a068-198">Это не может потребоваться в реализации.</span><span class="sxs-lookup"><span data-stu-id="6a068-198">You may not need this in your implementation.</span></span>|
|<span data-ttu-id="6a068-199">Core.QueueWebJobUsage.Job</span><span class="sxs-lookup"><span data-stu-id="6a068-199">Core.QueueWebJobUsage.Job</span></span>|<span data-ttu-id="6a068-200">WebJob Azure, на котором выполняется при добавлении новых сообщений в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-200">The Azure WebJob that runs when a new message is added to the Azure Storage queue.</span></span> <span data-ttu-id="6a068-201">Этот проект содержит код вашей настраиваемых бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="6a068-201">This project contains your custom business logic code.</span></span> |
|<span data-ttu-id="6a068-202">Core.QueueWebJobUsageWeb</span><span class="sxs-lookup"><span data-stu-id="6a068-202">Core.QueueWebJobUsageWeb</span></span>|<span data-ttu-id="6a068-203">Размещение у поставщика надстройки, которая содержит пользовательский Интерфейс для проекта Core.QueueWebJobUsage.</span><span class="sxs-lookup"><span data-stu-id="6a068-203">The provider-hosted add-in that contains the UI for the Core.QueueWebJobUsage project.</span></span> |
|<span data-ttu-id="6a068-204">Вспомогательные Project\Core.QueueWebJobUsage.Console.SendMessage</span><span class="sxs-lookup"><span data-stu-id="6a068-204">Helper Project\Core.QueueWebJobUsage.Console.SendMessage</span></span>|<span data-ttu-id="6a068-205">Проект модуля поддержки, который может использоваться для проверки сведений об учетной записи хранилища и процесс создания очередей и отправлять сообщения в очередь для обработки без настройки всего решения, описанного в данной статье.</span><span class="sxs-lookup"><span data-stu-id="6a068-205">A helper project that can be used to validate the storage account information and queue creation process, and to send messages to the queue for processing without setting up the entire solution described in this article.</span></span> |

<span data-ttu-id="6a068-206">При запуске примера кода Core.QueueWebJobUsage надстройки размещением у поставщика отображается и отображаются две кнопки: **синхронный режим** и **асинхронной операции**.</span><span class="sxs-lookup"><span data-stu-id="6a068-206">When you run the Core.QueueWebJobUsage code sample, the provider-hosted add-in appears and displays two buttons:  **Synchronous operation** and **Asynchronous operation**.</span></span> <span data-ttu-id="6a068-207">При выборе **синхронный режим** **btnSync_Click** в Pages\Default.aspx моделирует синхронный процесс длительным.</span><span class="sxs-lookup"><span data-stu-id="6a068-207">When you choose  **Synchronous operation**,  **btnSync_Click** in Pages\Default.aspx simulates a long-running synchronous process.</span></span> <span data-ttu-id="6a068-208">В этом примере кода **btnSync_Click** помещает текущего потока в спящий режим на 10 секунд, а затем создает библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="6a068-208">In this code sample, **btnSync_Click** puts the current thread to sleep for 10 seconds, and then creates a document library.</span></span> <span data-ttu-id="6a068-209">При выборе **асинхронной операции** **btnAsync_Click** в Pages\Default.aspx выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6a068-209">When you choose **Asynchronous operation**,  **btnAsync_Click** in Pages\Default.aspx does the following:</span></span>

1. <span data-ttu-id="6a068-210">Получает текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6a068-210">Gets the current user.</span></span>
    
2. <span data-ttu-id="6a068-211">Создает объект business **SiteModifyRequest** , в которой хранятся данные для включения в сообщения, отправляемые в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-211">Creates a  **SiteModifyRequest** business object that stores the data to include in the message being sent to the Azure Storage queue.</span></span> <span data-ttu-id="6a068-212">В этом примере кода отправляемых данных включает в себя имя текущего пользователя и URL-адрес текущего сайта.</span><span class="sxs-lookup"><span data-stu-id="6a068-212">In this code sample, the data being sent includes the current user's name and the current site's URL.</span></span>
    
3. <span data-ttu-id="6a068-213">Вызывает **SiteManager(). AddAsyncOperationRequestToQueue** для добавления сообщения в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-213">Calls  **SiteManager().AddAsyncOperationRequestToQueue** to add the message to the Azure Storage queue.</span></span>
    
<span data-ttu-id="6a068-214">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="6a068-214">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="6a068-215">В Core.QueueWebJobUsage.Common в SiteManager.cs **AddAsyncOperationRequestToQueue** выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6a068-215">In Core.QueueWebJobUsage.Common, in SiteManager.cs,  **AddAsyncOperationRequestToQueue** does the following:</span></span>

1. <span data-ttu-id="6a068-216">Создает объект [CloudStorageAccount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx) с помощью **AccountName** и **AccountKey** сведений о конфигурации в файле Core.QueueWebJobUsageWeb\web.config.</span><span class="sxs-lookup"><span data-stu-id="6a068-216">Creates a [CloudStorageAccount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx) object by using the **AccountName** and **AccountKey** configuration information in the Core.QueueWebJobUsageWeb\web.config file.</span></span>
    
2. <span data-ttu-id="6a068-217">Создает клиент обмена хранилища Azure очереди с помощью [CloudStorageAccount.CreateCloudQueueClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.createcloudqueueclient.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a068-217">Creates an Azure Storage queue client by using [CloudStorageAccount.CreateCloudQueueClient](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.createcloudqueueclient.aspx).</span></span>
    
3. <span data-ttu-id="6a068-218">Использует [CloudQueueClient.GetQueueReference](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueueclient.getqueuereference.aspx) для получения ссылки на хранилища Azure очередь с именем, равное значению **SiteManager.StorageQueueName** , константу.</span><span class="sxs-lookup"><span data-stu-id="6a068-218">Uses [CloudQueueClient.GetQueueReference](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueueclient.getqueuereference.aspx) to get a reference to the Azure Storage queue with name equal to the value of the **SiteManager.StorageQueueName** constant.</span></span>
    
4. <span data-ttu-id="6a068-219">[CloudQueue.CreateIfNotExists](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.createifnotexists.aspx) используется для создания очереди хранилища Azure, если не существует.</span><span class="sxs-lookup"><span data-stu-id="6a068-219">Uses [CloudQueue.CreateIfNotExists](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.createifnotexists.aspx) to create the Azure Storage queue if it does not exist.</span></span>
    
5. <span data-ttu-id="6a068-220">Использует [CloudQueue.AddMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) для добавления новых сообщений в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-220">Uses [CloudQueue.AddMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) to add a new message to the Azure Storage queue.</span></span> <span data-ttu-id="6a068-221">Бизнес-объект **modifyRequest** преобразуется в объект [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) , который добавляется в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-221">The **modifyRequest** business object is serialized into a [CloudQueueMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.aspx) object, which is added to the Azure Storage queue.</span></span>

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

<span data-ttu-id="6a068-222">После добавления сообщения в очередь хранилища Azure постоянно работает WebJob Azure ожидает и затем обрабатывает нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="6a068-222">After the message is added to the Azure Storage Queue, a continuously running Azure WebJob waits for and then processes the new message.</span></span> <span data-ttu-id="6a068-223">Azure WebJob определяется в Core.QueueWebJobUsage.Job.</span><span class="sxs-lookup"><span data-stu-id="6a068-223">The Azure WebJob is defined in Core.QueueWebJobUsage.Job.</span></span> <span data-ttu-id="6a068-224">При выполнении Azure WebJob Main в Core.QueueWebJobUsage.Job\Program.cs создает новый **JobHost**, а затем вызывает **RunAndBlock**.</span><span class="sxs-lookup"><span data-stu-id="6a068-224">When the Azure WebJob runs, Main in Core.QueueWebJobUsage.Job\Program.cs creates a new  **JobHost**, and then calls **RunAndBlock**.</span></span> <span data-ttu-id="6a068-225">Вызовы методов **JobHost** координаты помечается атрибутом **QueueTrigger** и контрольные значения для сообщений в определенной очереди.</span><span class="sxs-lookup"><span data-stu-id="6a068-225">The **JobHost** coordinates calls to methods marked with the **QueueTrigger** attribute, and watches for messages on a specific queue.</span></span> <span data-ttu-id="6a068-226">**RunAndBlock** гарантирует, что Azure WebJob работает постоянно и вызывает **ProcessQueueMessage**, то есть метод запуск при добавлении нового сообщения в очередь хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6a068-226">**RunAndBlock** ensures that the Azure WebJob runs continuously and calls **ProcessQueueMessage**, which is the method to trigger when a new message is added to the Azure Storage Queue.</span></span> <span data-ttu-id="6a068-227">Пакет SDK для Azure WebJobs связывает **основной** поток с **ProcessQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="6a068-227">The Azure WebJobs SDK associates the **Main** thread with **ProcessQueueMessage**.</span></span> <span data-ttu-id="6a068-228">Для получения дополнительных сведений см. [Создание WebJob .NET в Azure службы надстройки](https://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span><span class="sxs-lookup"><span data-stu-id="6a068-228">For more information, see [Create a .NET WebJob in Azure Add-in Service](https://azure.microsoft.com/documentation/articles/websites-dotnet-webjobs-sdk-get-started/).</span></span>

```C#
static void Main()
        {
            var host = new JobHost();
            // The following code ensures that the WebJob will run continuously.
            host.RunAndBlock();
        }
```

<span data-ttu-id="6a068-229">**ProcessQueueMessage** обрабатывает новые сообщения, которые добавлены в хранилище Azure очередь с:</span><span class="sxs-lookup"><span data-stu-id="6a068-229">**ProcessQueueMessage** processes new messages that are added to the Azure Storage queue by:</span></span>

1. <span data-ttu-id="6a068-230">С помощью атрибута **QueueTrigger** выполнять запуск **ProcessQueueMessage** при записи в очередь с именем равно значению **SiteManager.StorageQueueName**нового сообщения.</span><span class="sxs-lookup"><span data-stu-id="6a068-230">Using the  **QueueTrigger** attribute to specify that **ProcessQueueMessage** should be triggered when a new message is written to the queue with name equal to the value of **SiteManager.StorageQueueName**.</span></span>
    
2. <span data-ttu-id="6a068-231">Запись в журнал для Azure WebJob с помощью переменной **журнала** , переданный в качестве параметра **ProcessQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="6a068-231">Writing to the log for the Azure WebJob by using the  **log** variable that was passed as a parameter to **ProcessQueueMessage**.</span></span>
    
3. <span data-ttu-id="6a068-232">Вызов **SiteManager(). PerformSiteModification** для выполнения бизнес-процесса длительным на сайте.</span><span class="sxs-lookup"><span data-stu-id="6a068-232">Calling  **SiteManager().PerformSiteModification** to perform a long-running business process on the site.</span></span> <span data-ttu-id="6a068-233">В этом примере кода поток помещается в спящий режим на 10 секунд, а затем создается библиотеки документов.</span><span class="sxs-lookup"><span data-stu-id="6a068-233">In this code sample, the thread is put to sleep for 10 seconds, and then a document library is created.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="6a068-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6a068-234">Additional resources</span></span>
<span data-ttu-id="6a068-235"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6a068-235"></span></span>

- <span data-ttu-id="6a068-236">[Office 365 development шаблоны и рекомендации руководство по решениям](Office-365-development-patterns-and-practices-solution-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="6a068-236">[Office 365 development patterns and practices solution guidance](Office-365-development-patterns-and-practices-solution-guidance.md).</span></span>
    
- [<span data-ttu-id="6a068-237">Использование удаленных приемников событий в SharePoint</span><span class="sxs-lookup"><span data-stu-id="6a068-237">Use remote event receivers in SharePoint</span></span>](Use-remote-event-receivers-in-SharePoint.md)
    
- [<span data-ttu-id="6a068-238">Журнал изменений запросов SharePoint с ChangeQuery и маркер изменения</span><span class="sxs-lookup"><span data-stu-id="6a068-238">Query SharePoint change log with ChangeQuery and ChangeToken</span></span>](query-sharepoint-change-log-with-changequery-and-changeToken.md)
