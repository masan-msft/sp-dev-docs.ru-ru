---
title: "Использование удаленных приемников событий в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 713e1b42682a315626e2d121710931c64e86961e
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-remote-event-receivers-in-sharepoint"></a><span data-ttu-id="85b13-102">Использование удаленных приемников событий в SharePoint</span><span class="sxs-lookup"><span data-stu-id="85b13-102">Use remote event receivers in SharePoint</span></span>

<span data-ttu-id="85b13-103">Использование удаленных приемников событий для обработки событий в объектная модель SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85b13-103">Use remote event receivers to handle events in the SharePoint add-in model.</span></span> <span data-ttu-id="85b13-104">Используйте для установки или удаления объектов SharePoint и другие приемников событий, добавьте в необходимые события AppInstalled и AppUninstalling.</span><span class="sxs-lookup"><span data-stu-id="85b13-104">Use AppInstalled and AppUninstalling events to set up or remove SharePoint objects and other event receivers your add-in needs.</span></span>

<span data-ttu-id="85b13-105">_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="85b13-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

><span data-ttu-id="85b13-106">**Важные** По состоянию на январь 2017 SharePoint Online поддерживает webhooks списка, который можно использовать вместо «-ed» удаленные приемники событий.</span><span class="sxs-lookup"><span data-stu-id="85b13-106">**Important** As of January 2017 SharePoint Online does support list webhooks which you can use instead of "-ed" remote event receivers.</span></span> <span data-ttu-id="85b13-107">Извлечение [webhooks Общие сведения о SharePoint](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) для получения дополнительных сведений о webhooks.</span><span class="sxs-lookup"><span data-stu-id="85b13-107">Checkout [Overview of SharePoint webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) to learn more about webhooks.</span></span> <span data-ttu-id="85b13-108">Обратите внимание, что несколько примеров webhook доступны из репозитория репозиториев [sp dev примеры](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) .</span><span class="sxs-lookup"><span data-stu-id="85b13-108">Also note that several webhook samples are available from the [sp-dev-samples](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) GitHub repository.</span></span>

<span data-ttu-id="85b13-109">Пример [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) показано, как использовать размещение у поставщика в надстройке с удаленного приемника событий для обработки событий AppInstalled и AppUninstalling.</span><span class="sxs-lookup"><span data-stu-id="85b13-109">The  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample shows how to use a provider-hosted add-in with a remote event receiver to handle the AppInstalled and AppUninstalling events.</span></span> <span data-ttu-id="85b13-110">События AppInstalled и AppUninstalling Установка и удаление объектов SharePoint, которые используются надстройки при запуске.</span><span class="sxs-lookup"><span data-stu-id="85b13-110">The AppInstalled and AppUninstalling events set up and remove SharePoint objects that the add-in uses when it runs.</span></span> <span data-ttu-id="85b13-111">Кроме того обработчик событий AppInstalled добавляет обработчик событий ItemAdded со списком.</span><span class="sxs-lookup"><span data-stu-id="85b13-111">Additionally, the AppInstalled event handler adds the ItemAdded event handler to a list.</span></span> <span data-ttu-id="85b13-112">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="85b13-112">Use this solution if you want to:</span></span>

- <span data-ttu-id="85b13-113">Настройка надстройки на, сначала запустите с помощью события AppInstalled для настройки различных объектов SharePoint или приемников событий, надстройка для работы с.</span><span class="sxs-lookup"><span data-stu-id="85b13-113">Configure your add-in on first run using the AppInstalled event to set up various SharePoint objects or additional event receivers that your add-in works with.</span></span>
    
- <span data-ttu-id="85b13-114">Замените приемников событий создана с использованием решения с полным доверием кодом.</span><span class="sxs-lookup"><span data-stu-id="85b13-114">Replace event receivers implemented using fully trusted code solutions.</span></span> <span data-ttu-id="85b13-115">В полностью доверенной кода решения можно запустить приемников событий на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85b13-115">In fully trusted code solutions, you can run event receivers on the SharePoint server.</span></span> <span data-ttu-id="85b13-116">В новой надстройки модели SharePoint так как не удается запустить приемник событий на сервере SharePoint необходимо реализовать удаленного приемника событий на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="85b13-116">In the new SharePoint add-in model, because you cannot run the event receiver on the SharePoint server, you need to implement a remote event receiver on a web server.</span></span>
    
- <span data-ttu-id="85b13-117">Получайте уведомления о отмену изменения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85b13-117">Receive notifications of changes occuring in SharePoint.</span></span> <span data-ttu-id="85b13-118">К примеру при добавлении нового элемента в список, которую необходимо выполнить задачи.</span><span class="sxs-lookup"><span data-stu-id="85b13-118">For example, when a new item is added to a list, you want to perform a task.</span></span>

- <span data-ttu-id="85b13-119">Дополнение решения журнала изменений.</span><span class="sxs-lookup"><span data-stu-id="85b13-119">Complement your change log solution.</span></span> <span data-ttu-id="85b13-120">С использованием шаблона приемника удаленных событий с шаблоном журнал изменений содержит более надежная архитектура для обработки всех изменений баз данных контента, семейств веб-сайтов, сайтов или списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85b13-120">Using the remote event receiver pattern with a change log pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span></span> <span data-ttu-id="85b13-121">Принудительное выполнение удаленных приемников событий, но поскольку они выполняются на удаленном сервере, могут возникать ошибка связи.</span><span class="sxs-lookup"><span data-stu-id="85b13-121">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span></span> <span data-ttu-id="85b13-122">Шаблон журнала изменений гарантирует, что все изменения, доступны для обработки, но обычно обработки изменений приложение запускается по расписанию (например, задания таймера).</span><span class="sxs-lookup"><span data-stu-id="85b13-122">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span></span> <span data-ttu-id="85b13-123">Это означает, что изменения не обрабатываются немедленно.</span><span class="sxs-lookup"><span data-stu-id="85b13-123">This means that changes are not processed immediately.</span></span> <span data-ttu-id="85b13-124">При совместном использовании этих двух шаблонов убедитесь, что использовать механизм для предотвращения обработки такое же изменение дважды.</span><span class="sxs-lookup"><span data-stu-id="85b13-124">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span></span> <span data-ttu-id="85b13-125">Для получения дополнительных сведений см [SharePoint запрос изменения журнала с ChangeQuery и маркер изменения](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span><span class="sxs-lookup"><span data-stu-id="85b13-125">For more information, see [Query SharePoint change log with ChangeQuery and ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span></span>

<span data-ttu-id="85b13-126">**Примечание**  Размещение в SharePoint надстройки не поддерживают удаленных приемников событий.</span><span class="sxs-lookup"><span data-stu-id="85b13-126">**Note**  SharePoint-hosted add-ins do not support remote event receivers.</span></span> <span data-ttu-id="85b13-127">Чтобы использовать удаленные приемники событий, необходимо использовать размещение у поставщика в надстройке.</span><span class="sxs-lookup"><span data-stu-id="85b13-127">To use remote event receivers, you need to use a provider-hosted add-in.</span></span> <span data-ttu-id="85b13-128">Не следует использовать удаленных приемников событий для синхронизации или долго выполняющихся процессов.</span><span class="sxs-lookup"><span data-stu-id="85b13-128">You should not use remote event receivers for synchronization scenarios, or for long running processes.</span></span> <span data-ttu-id="85b13-129">Дополнительные сведения можно [как: Создание приемника событий надстройка](https://msdn.microsoft.com/library/office/jj220052.aspx).</span><span class="sxs-lookup"><span data-stu-id="85b13-129">For more information, see  [How to: Create an add-in event receiver](https://msdn.microsoft.com/library/office/jj220052.aspx).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="85b13-130">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="85b13-130">Before you begin</span></span>
<span data-ttu-id="85b13-131"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="85b13-131"></span></span>

<span data-ttu-id="85b13-132">Чтобы начать работу, загрузите пример надстройки [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="85b13-132">To get started, download the  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="85b13-133">Прежде чем запускать эта надстройка, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="85b13-133">Before you run this add-in, do the following:</span></span>

1. <span data-ttu-id="85b13-134">В свойства проекта Core.EventReceivers убедитесь, что **Управление установленными приложениями** и **Обработка удаляемого приложения** имеет значение **True**.</span><span class="sxs-lookup"><span data-stu-id="85b13-134">In the properties on the Core.EventReceivers project, verify that  **Handle App Installed** and **Handle App Uninstalling** is set to **True**.</span></span> <span data-ttu-id="85b13-135">Установка **Управление установленными приложениями** и **Обработка удаляемого приложения** **значения True** создает службы WCF, который определяет обработчик событий для события **AppInstalled** и **AppUninstalling** .</span><span class="sxs-lookup"><span data-stu-id="85b13-135">Setting  **Handle App Installed** and **Handle App Uninstalling** to **True** creates a WCF service that defines the event handler for the **AppInstalled** and **AppUninstalling** event.</span></span> <span data-ttu-id="85b13-136">В Core.EventReceivers откройте контекстное меню (щелкните правой кнопкой мыши) на файл AppManifest.xml и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="85b13-136">In Core.EventReceivers, open the shortcut menu (right-click) on AppManifest.xml, and choose **Properties**.</span></span> <span data-ttu-id="85b13-137">**InstalledEventEndpoint** и **UninstallingEventEndpoint** указывают на удаленный приемник событий, который обрабатывает события **AppInstalled** и **AppUninstalling** .</span><span class="sxs-lookup"><span data-stu-id="85b13-137">The  **InstalledEventEndpoint** and **UninstallingEventEndpoint** point to the remote event receiver that handles the **AppInstalled** and **AppUninstalling** events.</span></span>
    
2. <span data-ttu-id="85b13-138">Присоединение удаленного приемника событий для объекта на хост-сайте обычно требуется разрешение **Управление** для только этот объект.</span><span class="sxs-lookup"><span data-stu-id="85b13-138">Attaching a remote event receiver to an object in the host web usually requires  **Manage** permission for that object only.</span></span> <span data-ttu-id="85b13-139">Например при присоединении приемника событий в существующий список, надстройки требуется разрешение **Управление** в **список** только.</span><span class="sxs-lookup"><span data-stu-id="85b13-139">For example, when attaching an event receiver to an existing list, the add-in requires **Manage** permission on the **List** only.</span></span> <span data-ttu-id="85b13-140">В этом примере кода требуются разрешения **Управление** **Web** , так как он добавляется список и активирует компонент на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="85b13-140">This code sample requires **Manage** permissions on the **Web** because it adds a list and activates a feature on the host web.</span></span> <span data-ttu-id="85b13-141">Чтобы задать управление разрешениями в Интернете:</span><span class="sxs-lookup"><span data-stu-id="85b13-141">To set manage permissions on the web:</span></span>
    
    1. <span data-ttu-id="85b13-142">Дважды щелкните Core.EventReceivers\AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="85b13-142">Double click Core.EventReceivers\AppManifest.xml.</span></span>
    
    2. <span data-ttu-id="85b13-143">Выберите **разрешения**.</span><span class="sxs-lookup"><span data-stu-id="85b13-143">Choose  **Permissions**.</span></span>
    
    3. <span data-ttu-id="85b13-144">Убедитесь, что **область** имеет значение **Web**и набор **разрешений** на **Управление**.</span><span class="sxs-lookup"><span data-stu-id="85b13-144">Verify that  **Scope** is set to **Web**, and  **Permission** is set to **Manage**.</span></span>
    
3. <span data-ttu-id="85b13-145">Для запуска этого примера кода требуется Azure подписки.</span><span class="sxs-lookup"><span data-stu-id="85b13-145">To run this code sample, you need an Azure subscription.</span></span> <span data-ttu-id="85b13-146">Чтобы подписаться на пробную версию, обратитесь к разделу [Бесплатная пробная версия на один месяц](http://azure.microsoft.com/en-us/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85b13-146">To sign up for a trial, see  [Free one-month trial](http://azure.microsoft.com/en-us/pricing/free-trial/).</span></span>
    
4. <span data-ttu-id="85b13-147">Создайте пространство имен шины Azure службы с поддержкой службы ACS.</span><span class="sxs-lookup"><span data-stu-id="85b13-147">Create an Azure Service Bus Namespace with ACS Support.</span></span>
    
    1. <span data-ttu-id="85b13-148">Установка Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85b13-148">Install Azure PowerShell.</span></span> <span data-ttu-id="85b13-149">Дополнительные сведения можно [как: Установка Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).</span><span class="sxs-lookup"><span data-stu-id="85b13-149">For more information, see  [How to: Install Azure PowerShell](http://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/#Install).</span></span>
    
    2. <span data-ttu-id="85b13-150">Запустите **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="85b13-150">Start  **Azure PowerShell**.</span></span>
    
    3. <span data-ttu-id="85b13-151">Введите **Добавить AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="85b13-151">Enter  **Add-AzureAccount**.</span></span>
    
    4. <span data-ttu-id="85b13-152">Введите свой адрес электронной почты в диалоговом окне **входа в Windows Azure** и нажмите кнопку **Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="85b13-152">Enter your email address in the  **Sign in to Windows Azure** dialog, and then choose **Continue**.</span></span>
    
    5. <span data-ttu-id="85b13-153">Введите свой пароль и нажмите кнопку **Вход**.</span><span class="sxs-lookup"><span data-stu-id="85b13-153">Enter your password, and then choose  **Sign in**.</span></span>
    
    6. <span data-ttu-id="85b13-154">Создайте новое пространство имен шины службы с помощью следующего командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="85b13-154">Create a new service bus namespace using the following PowerShell cmdlet.</span></span>
    
        ```powershell
        New-AzureSBNamespace NamespaceNameRegion -CreateACSNamespace $true -NamespaceType Messaging
        
        ```
    
       <span data-ttu-id="85b13-155">Где:</span><span class="sxs-lookup"><span data-stu-id="85b13-155">Where:</span></span>
    
       -  <span data-ttu-id="85b13-156">_Имя_пространства_имен_ — это имя пространства имен шины служб Azure.</span><span class="sxs-lookup"><span data-stu-id="85b13-156">_NamespaceName_ is the name of your Azure Service Bus namespace.</span></span>
    
       -  <span data-ttu-id="85b13-157">_Область_ — региона, ближайшего к вам.</span><span class="sxs-lookup"><span data-stu-id="85b13-157">_Region_ is the region closest to you.</span></span> <span data-ttu-id="85b13-158">Например можно указать **«Запад США»**.</span><span class="sxs-lookup"><span data-stu-id="85b13-158">For example, you may enter **"West US"**.</span></span> <span data-ttu-id="85b13-159">Необходимо включить имя регион в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="85b13-159">You must include the region name in double quotes.</span></span>
    
    7. <span data-ttu-id="85b13-160">Вернуться к вашей портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="85b13-160">Return to your Azure Management Portal.</span></span> <span data-ttu-id="85b13-161">Выберите **СЛУЖЕБНОЙ ШИНЫ**и нажмите кнопку введенное имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="85b13-161">Choose  **SERVICE BUS**, and then choose the namespace name you entered.</span></span>
    
    8. <span data-ttu-id="85b13-162">Выберите **Управление строки подключения**и нажмите кнопку Копировать в **СТРОКУ подключения службы ACS**.</span><span class="sxs-lookup"><span data-stu-id="85b13-162">Choose  **Manage Connection Strings**, and then in  **ACS CONNECTION STRING**, choose the copy button.</span></span>
    
    9. <span data-ttu-id="85b13-163">Вернуться в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85b13-163">Return to Visual Studio.</span></span>
    
    10. <span data-ttu-id="85b13-164">Щелкните правой кнопкой мыши Core.EventReceivers > **Свойства** > **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="85b13-164">Right-click Core.EventReceivers >  **Properties** > **SharePoint**.</span></span>
    
    11. <span data-ttu-id="85b13-165">Установите флажок **Включить отладку через шину службы Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="85b13-165">Select  **Enable debugging via Microsoft Azure Service Bus**.</span></span>
    
    12. <span data-ttu-id="85b13-166">В поле **Строка подключения шины службы Microsoft Azure**вставьте строку подключения службы ACS.</span><span class="sxs-lookup"><span data-stu-id="85b13-166">In  **Microsoft Azure Service Bus connection string**, paste the ACS Connection String.</span></span>
    
    13. <span data-ttu-id="85b13-167">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="85b13-167">Choose  **Save**.</span></span>
    
5. <span data-ttu-id="85b13-168">Выполнение примера кода и выполните следующие дополнительные действия:</span><span class="sxs-lookup"><span data-stu-id="85b13-168">Run the code sample, and perform the following additional steps:</span></span>
    
    - <span data-ttu-id="85b13-169">Нажмите кнопку **Доверять** в окне **Предоставление разрешений для приложения** .</span><span class="sxs-lookup"><span data-stu-id="85b13-169">Click  **Trust It** in the **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="85b13-170">Закройте окно **Предоставление разрешений для приложения** .</span><span class="sxs-lookup"><span data-stu-id="85b13-170">Close the  **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="85b13-171">После завершения установки надстройки и службы WCF, откроется браузер.</span><span class="sxs-lookup"><span data-stu-id="85b13-171">When installation of the add-in and WCF service is completed, your browser will open.</span></span>
    
    - <span data-ttu-id="85b13-172">Вход на сайт Office 365.</span><span class="sxs-lookup"><span data-stu-id="85b13-172">Sign in to your Office 365 site.</span></span> <span data-ttu-id="85b13-173">Откроется страница start надстройки Core.EventReceivers.</span><span class="sxs-lookup"><span data-stu-id="85b13-173">The start page of the Core.EventReceivers add-in is displayed.</span></span>

## <a name="use-the-coreeventreceivers-add-in"></a><span data-ttu-id="85b13-174">Использовать надстройки Core.EventReceivers</span><span class="sxs-lookup"><span data-stu-id="85b13-174">Use the Core.EventReceivers add-in</span></span>
<span data-ttu-id="85b13-175"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="85b13-175"></span></span>

<span data-ttu-id="85b13-176">Чтобы просмотреть демонстрационный пример кода Core.EventReceivers:</span><span class="sxs-lookup"><span data-stu-id="85b13-176">To see a demo of the Core.EventReceivers code sample:</span></span>

1. <span data-ttu-id="85b13-177">Запуск образца и на странице "Запуск" выберите **веб-узел**.</span><span class="sxs-lookup"><span data-stu-id="85b13-177">Run the sample, and on the start page, choose  **Back to Site**.</span></span>
    
2. <span data-ttu-id="85b13-178">Выберите **элементы контент сайта**.</span><span class="sxs-lookup"><span data-stu-id="85b13-178">Choose  **Site Contents**.</span></span>
    
3. <span data-ttu-id="85b13-179">Выберите **задания приемника удаленных событий**.</span><span class="sxs-lookup"><span data-stu-id="85b13-179">Choose  **Remote Event Receiver Jobs**.</span></span>
    
4. <span data-ttu-id="85b13-180">Выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="85b13-180">Choose  **new item**.</span></span>
    
5. <span data-ttu-id="85b13-181">В поле **Название**введите **Contoso**и в **поле Описание** введите **Contoso тестирования**.</span><span class="sxs-lookup"><span data-stu-id="85b13-181">In  **Title**, enter  **Contoso**, and in  **Description** enter **Contoso test**.</span></span>
    
6. <span data-ttu-id="85b13-182">Вернуться к списку и обновить страницу.</span><span class="sxs-lookup"><span data-stu-id="85b13-182">Return to the list and refresh the page.</span></span>
    
7. <span data-ttu-id="85b13-183">Убедитесь, что описание добавляемого элемента была обновлены для **тестирования Contoso обновлен с ReR 192336**, где **192336** — отметку времени.</span><span class="sxs-lookup"><span data-stu-id="85b13-183">Verify that the description of the newly added item was updated to  **Contoso test Updated by ReR 192336**, where  **192336** is a timestamp.</span></span>
    
<span data-ttu-id="85b13-184">Services/AppEventReceiver.cs **AppEventReceiver** реализует интерфейс **IRemoteEventService** .</span><span class="sxs-lookup"><span data-stu-id="85b13-184">In Services/AppEventReceiver.cs,  **AppEventReceiver** implements the **IRemoteEventService** interface.</span></span> <span data-ttu-id="85b13-185">В этом примере кода предоставляет реализацию **методе ProcessEvent** , так как они используют синхронные события.</span><span class="sxs-lookup"><span data-stu-id="85b13-185">This code sample provides an implementation for the **ProcessEvent** method because it uses synchronous events.</span></span> <span data-ttu-id="85b13-186">Если вы используете асинхронные события, необходимо предоставить реализацию метода **ProcessOneWayEvent** .</span><span class="sxs-lookup"><span data-stu-id="85b13-186">If you use asynchronous events, you need to provide an implementation for the **ProcessOneWayEvent** method.</span></span>

<span data-ttu-id="85b13-187">**ProcessEvent** обрабатывает следующие **SPRemoteEventType** удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="85b13-187">The  **ProcessEvent** handles the following **SPRemoteEventType** remote events:</span></span>

-  <span data-ttu-id="85b13-188">События **AppInstalled** при установке надстройки.</span><span class="sxs-lookup"><span data-stu-id="85b13-188">**AppInstalled** events when installing the add-in.</span></span> <span data-ttu-id="85b13-189">При возникновении события **AppInstalled** **ProcessEvent** вызовов **HandleAppInstalled**.</span><span class="sxs-lookup"><span data-stu-id="85b13-189">When an **AppInstalled** event occurs, **ProcessEvent** calls **HandleAppInstalled**.</span></span>
    
-  <span data-ttu-id="85b13-190">События **AppUninstalling** при удалении надстройки.</span><span class="sxs-lookup"><span data-stu-id="85b13-190">**AppUninstalling** events when uninstalling the add-in.</span></span> <span data-ttu-id="85b13-191">При возникновении события **AppUninstalling** **ProcessEvent** вызовов **HandleAppUninstalling**.</span><span class="sxs-lookup"><span data-stu-id="85b13-191">When an **AppUninstalling** event occurs, **ProcessEvent** calls **HandleAppUninstalling**.</span></span> <span data-ttu-id="85b13-192">Событие **AppUninstalling** выполняется только в том случае, когда пользователь полностью удаляет надстройку, удалив надстройки из корзины сайта (для конечных пользователей) или удаления надстройку из списка **тестирование приложений** (для разработчиков).</span><span class="sxs-lookup"><span data-stu-id="85b13-192">The  **AppUninstalling** event only runs when a user completely removes the add-in either by deleting the add-in from the site recycle bin (for end users) or by removing the add-in from the **Apps in testing** list (for developers).</span></span>
    
-  <span data-ttu-id="85b13-193">Событий **ItemAdded** при добавлении элемента в список.</span><span class="sxs-lookup"><span data-stu-id="85b13-193">**ItemAdded** events when an item is added to a list.</span></span> <span data-ttu-id="85b13-194">Когда возникает событие **ItemAdded** вызовы **ProcessEvent** **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="85b13-194">When an **ItemAdded** event occurs, **ProcessEvent** calls **HandleItemAdded**.</span></span>

<span data-ttu-id="85b13-195">**Примечание**  В окне Свойства проекта Core.EventReceiver доступны только свойства, **Управление установленными приложениями** и **Обработка удаляемого приложения** .</span><span class="sxs-lookup"><span data-stu-id="85b13-195">**Note**  In the Core.EventReceiver project properties, only  **Handle App Installed** and **Handle App Uninstalling** properties are available.</span></span> <span data-ttu-id="85b13-196">В этом примере кода показано, как добавить обработчик событий **ItemAdded** для списка на веб-сайт с помощью события **AppInstalled** во время установки надстройки.</span><span class="sxs-lookup"><span data-stu-id="85b13-196">This code sample shows how you can add the **ItemAdded** event handler to a list on the host web by using the **AppInstalled** event during add-in installation.</span></span>

<span data-ttu-id="85b13-197">**Примечание**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="85b13-197">**Note**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {

            SPRemoteEventResult result = new SPRemoteEventResult();

            switch (properties.EventType)
            {
                case SPRemoteEventType.AppInstalled:
                    HandleAppInstalled(properties);
                    break;
                case SPRemoteEventType.AppUninstalling:
                    HandleAppUninstalling(properties);
                    break;
                case SPRemoteEventType.ItemAdded:
                    HandleItemAdded(properties);
                    break;
            }


            return result;
        }
```

<span data-ttu-id="85b13-198">**HandleAppInstalled** вызывает **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** RemoteEventReceiverManager.cs.</span><span class="sxs-lookup"><span data-stu-id="85b13-198">**HandleAppInstalled** calls **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.</span></span>

```C#
 private void HandleAppInstalled(SPRemoteEventProperties properties)
        {
            using (ClientContext clientContext =
                TokenHelper.CreateAppEventClientContext(properties, false))
            {
                if (clientContext != null)
                {
                    new RemoteEventReceiverManager().AssociateRemoteEventsToHostWeb(clientContext);
                }
            }
        }
```

<span data-ttu-id="85b13-199">**AssociateRemoteEventsToHostWeb** создает или позволяет различных объектов SharePoint, используемые надстройкой Core.EventReceivers.</span><span class="sxs-lookup"><span data-stu-id="85b13-199">**AssociateRemoteEventsToHostWeb** creates or enables various SharePoint objects that the Core.EventReceivers add-in uses.</span></span> <span data-ttu-id="85b13-200">Ваши требования могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="85b13-200">Your requirements might differ.</span></span> <span data-ttu-id="85b13-201">**AssociateRemoteEventsToHostWeb** выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="85b13-201">**AssociateRemoteEventsToHostWeb** does the following:</span></span>

- <span data-ttu-id="85b13-202">Включает Push-уведомлений с помощью **Web.Features.Add**.</span><span class="sxs-lookup"><span data-stu-id="85b13-202">Enables the Push Notification feature by using  **Web.Features.Add**.</span></span>
    
- <span data-ttu-id="85b13-203">Использует объект **clientContext** для поиска для списка.</span><span class="sxs-lookup"><span data-stu-id="85b13-203">Uses the  **clientContext** object to search for a list.</span></span> <span data-ttu-id="85b13-204">Если список не существует, **CreateJobsList** создает список.</span><span class="sxs-lookup"><span data-stu-id="85b13-204">If the list does not exist, **CreateJobsList** creates the list.</span></span> <span data-ttu-id="85b13-205">Если список существует, **List.EventReceivers** используется для поиска существующего получателя событий, имя которого является **ItemAddedEvent**.</span><span class="sxs-lookup"><span data-stu-id="85b13-205">If the list exists, **List.EventReceivers** is used to search for an existing event receiver whose name is **ItemAddedEvent**.</span></span>
    
- <span data-ttu-id="85b13-206">Если не существует **ItemAddedEvent** приемника событий:</span><span class="sxs-lookup"><span data-stu-id="85b13-206">If the  **ItemAddedEvent** event receiver does not exist:</span></span>
    
    - <span data-ttu-id="85b13-207">Создает новый объект **EventReceiverDefinitionCreationInformation** для создания нового приемника удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="85b13-207">Instantiates a new  **EventReceiverDefinitionCreationInformation** object to create the new remote event receiver.</span></span> <span data-ttu-id="85b13-208">Тип приемника событий **ItemAdded** добавляется **EventReceiverDefinitionCreationInformation.EventType**.</span><span class="sxs-lookup"><span data-stu-id="85b13-208">The **ItemAdded** event receiver type is added to **EventReceiverDefinitionCreationInformation.EventType**.</span></span>
    
    - <span data-ttu-id="85b13-209">Задает **EventReceiverDefinitionCreationInformation.ReceiverURL** URL-адрес в **AppInstalled** удаленный приемник событий.</span><span class="sxs-lookup"><span data-stu-id="85b13-209">Sets the  **EventReceiverDefinitionCreationInformation.ReceiverURL** to the URL of the **AppInstalled** remote event receiver.</span></span>
    
    - <span data-ttu-id="85b13-210">Добавляет новый приемника событий в список с помощью **List.EventReceivers.Add**.</span><span class="sxs-lookup"><span data-stu-id="85b13-210">Adds a new event receiver to the list using  **List.EventReceivers.Add**.</span></span>

```C#
public void AssociateRemoteEventsToHostWeb(ClientContext clientContext)
        {
            // Add Push Notification feature to host web.
            // Not required but it is included here to show you
            // how to activate features.
            clientContext.Web.Features.Add(
                     new Guid("41e1d4bf-b1a2-47f7-ab80-d5d6cbba3092"),
                     true, FeatureDefinitionScope.None);


            // Get the Title and EventReceivers lists.
            clientContext.Load(clientContext.Web.Lists,
                lists => lists.Include(
                    list => list.Title,
                    list => list.EventReceivers).Where
                        (list => list.Title == LIST_TITLE));

            clientContext.ExecuteQuery();

            List jobsList = clientContext.Web.Lists.FirstOrDefault();

            bool rerExists = false;
            if (null == jobsList)
            {
                // List does not exist, create it. 
                jobsList = CreateJobsList(clientContext);

            }
            else
            {
                foreach (var rer in jobsList.EventReceivers)
                {
                    if (rer.ReceiverName == RECEIVER_NAME)
                    {
                        rerExists = true;
                        System.Diagnostics.Trace.WriteLine("Found existing ItemAdded receiver at "
                            + rer.ReceiverUrl);
                    }
                }
            }

            if (!rerExists)
            {
                EventReceiverDefinitionCreationInformation receiver =
                    new EventReceiverDefinitionCreationInformation();
                receiver.EventType = EventReceiverType.ItemAdded;
                
                // Get WCF URL where this message was handled.
                OperationContext op = OperationContext.Current;
                Message msg = op.RequestContext.RequestMessage;
                receiver.ReceiverUrl = msg.Headers.To.ToString();

                receiver.ReceiverName = RECEIVER_NAME;
                receiver.Synchronization = EventReceiverSynchronization.Synchronous;

                // Add the new event receiver to a list in the host web.
                jobsList.EventReceivers.Add(receiver);
                clientContext.ExecuteQuery();

                System.Diagnostics.Trace.WriteLine("Added ItemAdded receiver at " + receiver.ReceiverUrl);
            }
        }
```

<span data-ttu-id="85b13-211">При добавлении элемента в список **Заданий приемника удаленных событий** **ProcessEvent** в AppEventReceiver.svc.cs обрабатывает событие **ItemAdded** , а затем вызывает **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="85b13-211">When an item is added to the  **Remote Event Receiver Jobs** list, **ProcessEvent** in AppEventReceiver.svc.cs handles the **ItemAdded** event, and then calls **HandleItemAdded**.</span></span>  <span data-ttu-id="85b13-212">**HandleItemAdded** вызывает **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span><span class="sxs-lookup"><span data-stu-id="85b13-212">**HandleItemAdded** calls **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span></span>  <span data-ttu-id="85b13-213">**ItemAddedToListEventHandler** выбирает элемент списка, который был добавлен и добавляет строку **обновлен с ReR** описание элемента списка.</span><span class="sxs-lookup"><span data-stu-id="85b13-213">**ItemAddedToListEventHandler** fetches the list item that was added, and adds the string **Updated by ReR** to the list item's description.</span></span>

```C#
 public void ItemAddedToListEventHandler(ClientContext clientContext, Guid listId, int listItemId)
        {
            try
            {
                List photos = clientContext.Web.Lists.GetById(listId);
                ListItem item = photos.GetItemById(listItemId);
                clientContext.Load(item);
                clientContext.ExecuteQuery();

                item["Description"] += "\nUpdated by RER " +
                    System.DateTime.Now.ToLongTimeString();
                item.Update();
                clientContext.ExecuteQuery();
            }
            catch (Exception oops)
            {
                System.Diagnostics.Trace.WriteLine(oops.Message);
            }

        }
```

## <a name="additional-resources"></a><span data-ttu-id="85b13-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="85b13-214">Additional resources</span></span>
<span data-ttu-id="85b13-215"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="85b13-215"></span></span>

-  [<span data-ttu-id="85b13-216">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="85b13-216">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="85b13-217">Core.AppEvents.HandlerDelegation</span><span class="sxs-lookup"><span data-stu-id="85b13-217">Core.AppEvents.HandlerDelegation </span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    
