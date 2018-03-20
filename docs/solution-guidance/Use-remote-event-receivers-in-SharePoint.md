---
title: "Использование удаленных приемников событий в SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d6c2026aa9ae377601a42662fa5aebbb688011a7
ms.sourcegitcommit: 895d31071e73aa23e62593c9ffa46b38701ba801
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2018
---
# <a name="use-remote-event-receivers-in-sharepoint"></a><span data-ttu-id="0a4a3-102">Использование удаленных приемников событий в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a4a3-102">Use remote event receivers in SharePoint</span></span>

<span data-ttu-id="0a4a3-103">Использование удаленных приемников событий для обработки событий в объектная модель SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-103">Use remote event receivers to handle events in the SharePoint add-in model.</span></span> <span data-ttu-id="0a4a3-104">Используйте для установки или удаления объектов SharePoint и другие приемников событий, добавьте в необходимые события AppInstalled и AppUninstalling.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-104">Use AppInstalled and AppUninstalling events to set up or remove SharePoint objects and other event receivers your add-in needs.</span></span>

<span data-ttu-id="0a4a3-105">_**Применимо к:** надстройки для SharePoint | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="0a4a3-105">_**Applies to:** add-ins for SharePoint | SharePoint 2013 | SharePoint Online_</span></span>

><span data-ttu-id="0a4a3-106">**Важные** По состоянию на январь 2017 SharePoint Online поддерживает webhooks списка, который можно использовать вместо «-ed» удаленные приемники событий.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-106">**Important** As of January 2017 SharePoint Online does support list webhooks which you can use instead of "-ed" remote event receivers.</span></span> <span data-ttu-id="0a4a3-107">Извлечение [webhooks Общие сведения о SharePoint](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) для получения дополнительных сведений о webhooks.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-107">Checkout [Overview of SharePoint webhooks](https://dev.office.com/sharepoint/docs/apis/webhooks/overview-sharepoint-webhooks) to learn more about webhooks.</span></span> <span data-ttu-id="0a4a3-108">Обратите внимание, что несколько примеров webhook доступны из репозитория репозиториев [sp dev примеры](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-108">Also note that several webhook samples are available from the [sp-dev-samples](https://github.com/SharePoint/sp-dev-samples/tree/master/Samples) GitHub repository.</span></span>

<span data-ttu-id="0a4a3-109">Пример [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) показано, как использовать размещение у поставщика в надстройке с удаленного приемника событий для обработки событий AppInstalled и AppUninstalling.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-109">The  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample shows how to use a provider-hosted add-in with a remote event receiver to handle the AppInstalled and AppUninstalling events.</span></span> <span data-ttu-id="0a4a3-110">События AppInstalled и AppUninstalling Установка и удаление объектов SharePoint, которые используются надстройки при запуске.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-110">The AppInstalled and AppUninstalling events set up and remove SharePoint objects that the add-in uses when it runs.</span></span> <span data-ttu-id="0a4a3-111">Кроме того обработчик событий AppInstalled добавляет обработчик событий ItemAdded со списком.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-111">Additionally, the AppInstalled event handler adds the ItemAdded event handler to a list.</span></span> <span data-ttu-id="0a4a3-112">Если вы хотите используйте этого решения:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-112">Use this solution if you want to:</span></span>

- <span data-ttu-id="0a4a3-113">Настройка надстройки на, сначала запустите с помощью события AppInstalled для настройки различных объектов SharePoint или приемников событий, надстройка для работы с.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-113">Configure your add-in on first run using the AppInstalled event to set up various SharePoint objects or additional event receivers that your add-in works with.</span></span>
    
- <span data-ttu-id="0a4a3-114">Замените приемников событий создана с использованием решения с полным доверием кодом.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-114">Replace event receivers implemented using fully trusted code solutions.</span></span> <span data-ttu-id="0a4a3-115">В полностью доверенной кода решения можно запустить приемников событий на сервере SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-115">In fully trusted code solutions, you can run event receivers on the SharePoint server.</span></span> <span data-ttu-id="0a4a3-116">В новой надстройки модели SharePoint так как не удается запустить приемник событий на сервере SharePoint необходимо реализовать удаленного приемника событий на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-116">In the new SharePoint add-in model, because you cannot run the event receiver on the SharePoint server, you need to implement a remote event receiver on a web server.</span></span>
    
- <span data-ttu-id="0a4a3-117">Получайте уведомления о отмену изменения в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-117">Receive notifications of changes occuring in SharePoint.</span></span> <span data-ttu-id="0a4a3-118">К примеру при добавлении нового элемента в список, которую необходимо выполнить задачи.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-118">For example, when a new item is added to a list, you want to perform a task.</span></span>

- <span data-ttu-id="0a4a3-119">Дополнение решения журнала изменений.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-119">Complement your change log solution.</span></span> <span data-ttu-id="0a4a3-120">С использованием шаблона приемника удаленных событий с шаблоном журнал изменений содержит более надежная архитектура для обработки всех изменений баз данных контента, семейств веб-сайтов, сайтов или списков SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-120">Using the remote event receiver pattern with a change log pattern provides a more reliable architecture for handling all changes made to SharePoint content databases, site collections, sites, or lists.</span></span> <span data-ttu-id="0a4a3-121">Принудительное выполнение удаленных приемников событий, но поскольку они выполняются на удаленном сервере, могут возникать ошибка связи.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-121">Remote event receivers run immediately, but because they run on a remote server, you might encounter a communication failure.</span></span> <span data-ttu-id="0a4a3-122">Шаблон журнала изменений гарантирует, что все изменения, доступны для обработки, но обычно обработки изменений приложение запускается по расписанию (например, задания таймера).</span><span class="sxs-lookup"><span data-stu-id="0a4a3-122">The change log pattern ensures that all changes are available for processing, but the application processing the changes usually runs on a schedule (for example, a timer job).</span></span> <span data-ttu-id="0a4a3-123">Это означает, что изменения не обрабатываются немедленно.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-123">This means that changes are not processed immediately.</span></span> <span data-ttu-id="0a4a3-124">При совместном использовании этих двух шаблонов убедитесь, что использовать механизм для предотвращения обработки такое же изменение дважды.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-124">If you use these two patterns together, ensure you use a mechanism to prevent processing the same change twice.</span></span> <span data-ttu-id="0a4a3-125">Для получения дополнительных сведений см [SharePoint запрос изменения журнала с ChangeQuery и маркер изменения](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span><span class="sxs-lookup"><span data-stu-id="0a4a3-125">For more information, see [Query SharePoint change log with ChangeQuery and ChangeToken](query-sharepoint-change-log-with-changequery-and-changeToken.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="0a4a3-126">Размещение в SharePoint надстройки не поддерживают удаленных приемников событий.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-126">SharePoint-hosted add-ins do not support remote event receivers.</span></span> <span data-ttu-id="0a4a3-127">Чтобы использовать удаленные приемники событий, необходимо использовать размещение у поставщика в надстройке.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-127">To use remote event receivers, you need to use a provider-hosted add-in.</span></span> <span data-ttu-id="0a4a3-128">Не следует использовать удаленных приемников событий для синхронизации или долго выполняющихся процессов.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-128">You should not use remote event receivers for synchronization scenarios, or for long running processes.</span></span> <span data-ttu-id="0a4a3-129">Дополнительные сведения можно [как: Создание приемника событий надстройка](https://msdn.microsoft.com/library/office/jj220052.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a4a3-129">For more information, see  [How to: Create an add-in event receiver](https://msdn.microsoft.com/library/office/jj220052.aspx).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0a4a3-130">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0a4a3-130">Before you begin</span></span>
<span data-ttu-id="0a4a3-131"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="0a4a3-131"></span></span>

<span data-ttu-id="0a4a3-132">Чтобы начать работу, загрузите пример надстройки [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-132">To get started, download the  [Core.EventReceivers](https://github.com/SharePoint/PnP/tree/master/Samples/Core.EventReceivers) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

<span data-ttu-id="0a4a3-133">Прежде чем запускать эта надстройка, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-133">Before you run this add-in, do the following:</span></span>

1. <span data-ttu-id="0a4a3-134">В свойства проекта Core.EventReceivers убедитесь, что **Управление установленными приложениями** и **Обработка удаляемого приложения** имеет значение **True**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-134">In the properties on the Core.EventReceivers project, verify that  **Handle App Installed** and **Handle App Uninstalling** is set to **True**.</span></span> <span data-ttu-id="0a4a3-135">Установка **Управление установленными приложениями** и **Обработка удаляемого приложения** **значения True** создает службы WCF, который определяет обработчик событий для события **AppInstalled** и **AppUninstalling** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-135">Setting  **Handle App Installed** and **Handle App Uninstalling** to **True** creates a WCF service that defines the event handler for the **AppInstalled** and **AppUninstalling** event.</span></span> <span data-ttu-id="0a4a3-136">В Core.EventReceivers откройте контекстное меню (щелкните правой кнопкой мыши) на файл AppManifest.xml и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-136">In Core.EventReceivers, open the shortcut menu (right-click) on AppManifest.xml, and choose **Properties**.</span></span> <span data-ttu-id="0a4a3-137">**InstalledEventEndpoint** и **UninstallingEventEndpoint** указывают на удаленный приемник событий, который обрабатывает события **AppInstalled** и **AppUninstalling** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-137">The  **InstalledEventEndpoint** and **UninstallingEventEndpoint** point to the remote event receiver that handles the **AppInstalled** and **AppUninstalling** events.</span></span>
    
2. <span data-ttu-id="0a4a3-138">Присоединение удаленного приемника событий для объекта на хост-сайте обычно требуется разрешение **Управление** для только этот объект.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-138">Attaching a remote event receiver to an object in the host web usually requires  **Manage** permission for that object only.</span></span> <span data-ttu-id="0a4a3-139">Например при присоединении приемника событий в существующий список, надстройки требуется разрешение **Управление** в **список** только.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-139">For example, when attaching an event receiver to an existing list, the add-in requires **Manage** permission on the **List** only.</span></span> <span data-ttu-id="0a4a3-140">В этом примере кода требуются разрешения **Управление** **Web** , так как он добавляется список и активирует компонент на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-140">This code sample requires **Manage** permissions on the **Web** because it adds a list and activates a feature on the host web.</span></span> <span data-ttu-id="0a4a3-141">Чтобы задать управление разрешениями в Интернете:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-141">To set manage permissions on the web:</span></span>
    
    1. <span data-ttu-id="0a4a3-142">Дважды щелкните Core.EventReceivers\AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-142">Double click Core.EventReceivers\AppManifest.xml.</span></span>
    
    2. <span data-ttu-id="0a4a3-143">Выберите **разрешения**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-143">Choose  **Permissions**.</span></span>
    
    3. <span data-ttu-id="0a4a3-144">Убедитесь, что **область** имеет значение **Web**и набор **разрешений** на **Управление**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-144">Verify that  **Scope** is set to **Web**, and  **Permission** is set to **Manage**.</span></span>
    
3. <span data-ttu-id="0a4a3-145">Для запуска этого примера кода требуется Azure подписки.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-145">To run this code sample, you need an Azure subscription.</span></span> <span data-ttu-id="0a4a3-146">Чтобы подписаться на пробную версию, обратитесь к разделу [Бесплатная пробная версия на один месяц](http://azure.microsoft.com/en-us/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a4a3-146">To sign up for a trial, see [Free one-month trial](http://azure.microsoft.com/en-us/pricing/free-trial/).</span></span>
    
4. <span data-ttu-id="0a4a3-147">Создайте пространство имен шины Azure службы.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-147">Create an Azure Service Bus Namespace.</span></span>
    
    1. <span data-ttu-id="0a4a3-148">Выполните инструкции в разделе [Создание пространство имен служебной шины](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-create-namespace-portal).</span><span class="sxs-lookup"><span data-stu-id="0a4a3-148">Carry out the instructions in [Create a Service Bus namespace](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-create-namespace-portal).</span></span>

    2. <span data-ttu-id="0a4a3-149">Скопируйте **Основной строку подключения** с только что созданный пространства имен шины обслуживания</span><span class="sxs-lookup"><span data-stu-id="0a4a3-149">Copy **Primary Connection String** from the just created Service Bus Namespace</span></span>
    
    3. <span data-ttu-id="0a4a3-150">Вернуться в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-150">Return to Visual Studio.</span></span>
    
    4. <span data-ttu-id="0a4a3-151">Щелкните правой кнопкой мыши Core.EventReceivers > **Свойства** > **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-151">Right-click Core.EventReceivers >  **Properties** > **SharePoint**.</span></span>
    
    5. <span data-ttu-id="0a4a3-152">Установите флажок **Включить отладку через шину службы Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-152">Select  **Enable debugging via Microsoft Azure Service Bus**.</span></span>
    
    6. <span data-ttu-id="0a4a3-153">В поле **Строка подключения шины службы Microsoft Azure**вставьте строку подключения.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-153">In  **Microsoft Azure Service Bus connection string**, paste the Connection String.</span></span>
    
    7. <span data-ttu-id="0a4a3-154">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-154">Choose  **Save**.</span></span>
    
5. <span data-ttu-id="0a4a3-155">Выполнение примера кода и выполните следующие дополнительные действия:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-155">Run the code sample, and perform the following additional steps:</span></span>
    
    - <span data-ttu-id="0a4a3-156">Нажмите кнопку **Доверять** в окне **Предоставление разрешений для приложения** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-156">Click  **Trust It** in the **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="0a4a3-157">Закройте окно **Предоставление разрешений для приложения** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-157">Close the  **Grant permissions to the app** window.</span></span>
    
    - <span data-ttu-id="0a4a3-158">После завершения установки надстройки и службы WCF, откроется браузер.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-158">When installation of the add-in and WCF service is completed, your browser will open.</span></span>
    
    - <span data-ttu-id="0a4a3-159">Вход на сайт Office 365.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-159">Sign in to your Office 365 site.</span></span> <span data-ttu-id="0a4a3-160">Откроется страница start надстройки Core.EventReceivers.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-160">The start page of the Core.EventReceivers add-in is displayed.</span></span>

## <a name="use-the-coreeventreceivers-add-in"></a><span data-ttu-id="0a4a3-161">Использовать надстройки Core.EventReceivers</span><span class="sxs-lookup"><span data-stu-id="0a4a3-161">Use the Core.EventReceivers add-in</span></span>
<span data-ttu-id="0a4a3-162"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="0a4a3-162"></span></span>

<span data-ttu-id="0a4a3-163">Чтобы просмотреть демонстрационный пример кода Core.EventReceivers:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-163">To see a demo of the Core.EventReceivers code sample:</span></span>

1. <span data-ttu-id="0a4a3-164">Запуск образца и на странице "Запуск" выберите **веб-узел**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-164">Run the sample, and on the start page, choose  **Back to Site**.</span></span>
    
2. <span data-ttu-id="0a4a3-165">Выберите **элементы контент сайта**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-165">Choose  **Site Contents**.</span></span>
    
3. <span data-ttu-id="0a4a3-166">Выберите **задания приемника удаленных событий**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-166">Choose  **Remote Event Receiver Jobs**.</span></span>
    
4. <span data-ttu-id="0a4a3-167">Выберите **новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-167">Choose  **new item**.</span></span>
    
5. <span data-ttu-id="0a4a3-168">В поле **Название**введите **Contoso**и в **поле Описание** введите **Contoso тестирования**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-168">In  **Title**, enter  **Contoso**, and in  **Description** enter **Contoso test**.</span></span>
    
6. <span data-ttu-id="0a4a3-169">Вернуться к списку и обновить страницу.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-169">Return to the list and refresh the page.</span></span>
    
7. <span data-ttu-id="0a4a3-170">Убедитесь, что описание добавляемого элемента была обновлены для **тестирования Contoso обновлен с ReR 192336**, где **192336** — отметку времени.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-170">Verify that the description of the newly added item was updated to  **Contoso test Updated by ReR 192336**, where  **192336** is a timestamp.</span></span>
    
<span data-ttu-id="0a4a3-171">Services/AppEventReceiver.cs **AppEventReceiver** реализует интерфейс **IRemoteEventService** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-171">In Services/AppEventReceiver.cs,  **AppEventReceiver** implements the **IRemoteEventService** interface.</span></span> <span data-ttu-id="0a4a3-172">В этом примере кода предоставляет реализацию **методе ProcessEvent** , так как они используют синхронные события.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-172">This code sample provides an implementation for the **ProcessEvent** method because it uses synchronous events.</span></span> <span data-ttu-id="0a4a3-173">Если вы используете асинхронные события, необходимо предоставить реализацию метода **ProcessOneWayEvent** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-173">If you use asynchronous events, you need to provide an implementation for the **ProcessOneWayEvent** method.</span></span>

<span data-ttu-id="0a4a3-174">**ProcessEvent** обрабатывает следующие **SPRemoteEventType** удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-174">The  **ProcessEvent** handles the following **SPRemoteEventType** remote events:</span></span>

-  <span data-ttu-id="0a4a3-175">События **AppInstalled** при установке надстройки.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-175">**AppInstalled** events when installing the add-in.</span></span> <span data-ttu-id="0a4a3-176">При возникновении события **AppInstalled** **ProcessEvent** вызовов **HandleAppInstalled**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-176">When an **AppInstalled** event occurs, **ProcessEvent** calls **HandleAppInstalled**.</span></span>
    
-  <span data-ttu-id="0a4a3-177">События **AppUninstalling** при удалении надстройки.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-177">**AppUninstalling** events when uninstalling the add-in.</span></span> <span data-ttu-id="0a4a3-178">При возникновении события **AppUninstalling** **ProcessEvent** вызовов **HandleAppUninstalling**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-178">When an **AppUninstalling** event occurs, **ProcessEvent** calls **HandleAppUninstalling**.</span></span> <span data-ttu-id="0a4a3-179">Событие **AppUninstalling** выполняется только в том случае, когда пользователь полностью удаляет надстройку, удалив надстройки из корзины сайта (для конечных пользователей) или удаления надстройку из списка **тестирование приложений** (для разработчиков).</span><span class="sxs-lookup"><span data-stu-id="0a4a3-179">The  **AppUninstalling** event only runs when a user completely removes the add-in either by deleting the add-in from the site recycle bin (for end users) or by removing the add-in from the **Apps in testing** list (for developers).</span></span>
    
-  <span data-ttu-id="0a4a3-180">Событий **ItemAdded** при добавлении элемента в список.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-180">**ItemAdded** events when an item is added to a list.</span></span> <span data-ttu-id="0a4a3-181">Когда возникает событие **ItemAdded** вызовы **ProcessEvent** **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-181">When an **ItemAdded** event occurs, **ProcessEvent** calls **HandleItemAdded**.</span></span>

> [!NOTE] 
> <span data-ttu-id="0a4a3-182">В окне Свойства проекта Core.EventReceiver доступны только свойства, **Управление установленными приложениями** и **Обработка удаляемого приложения** .</span><span class="sxs-lookup"><span data-stu-id="0a4a3-182">In the Core.EventReceiver project properties, only  **Handle App Installed** and **Handle App Uninstalling** properties are available.</span></span> <span data-ttu-id="0a4a3-183">В этом примере кода показано, как добавить обработчик событий **ItemAdded** для списка на веб-сайт с помощью события **AppInstalled** во время установки надстройки.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-183">This code sample shows how you can add the **ItemAdded** event handler to a list on the host web by using the **AppInstalled** event during add-in installation.</span></span>

> [!NOTE] 
> <span data-ttu-id="0a4a3-184">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-184">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="0a4a3-185">**HandleAppInstalled** вызывает **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** RemoteEventReceiverManager.cs.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-185">**HandleAppInstalled** calls **RemoteEventReceiverManager.AssociateRemoteEventsToHostWeb** in RemoteEventReceiverManager.cs.</span></span>

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

<span data-ttu-id="0a4a3-186">**AssociateRemoteEventsToHostWeb** создает или позволяет различных объектов SharePoint, используемые надстройкой Core.EventReceivers.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-186">**AssociateRemoteEventsToHostWeb** creates or enables various SharePoint objects that the Core.EventReceivers add-in uses.</span></span> <span data-ttu-id="0a4a3-187">Ваши требования могут отличаться.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-187">Your requirements might differ.</span></span> <span data-ttu-id="0a4a3-188">**AssociateRemoteEventsToHostWeb** выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-188">**AssociateRemoteEventsToHostWeb** does the following:</span></span>

- <span data-ttu-id="0a4a3-189">Включает Push-уведомлений с помощью **Web.Features.Add**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-189">Enables the Push Notification feature by using  **Web.Features.Add**.</span></span>
    
- <span data-ttu-id="0a4a3-190">Использует объект **clientContext** для поиска для списка.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-190">Uses the  **clientContext** object to search for a list.</span></span> <span data-ttu-id="0a4a3-191">Если список не существует, **CreateJobsList** создает список.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-191">If the list does not exist, **CreateJobsList** creates the list.</span></span> <span data-ttu-id="0a4a3-192">Если список существует, **List.EventReceivers** используется для поиска существующего получателя событий, имя которого является **ItemAddedEvent**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-192">If the list exists, **List.EventReceivers** is used to search for an existing event receiver whose name is **ItemAddedEvent**.</span></span>
    
- <span data-ttu-id="0a4a3-193">Если не существует **ItemAddedEvent** приемника событий:</span><span class="sxs-lookup"><span data-stu-id="0a4a3-193">If the  **ItemAddedEvent** event receiver does not exist:</span></span>
    
    - <span data-ttu-id="0a4a3-194">Создает новый объект **EventReceiverDefinitionCreationInformation** для создания нового приемника удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-194">Instantiates a new  **EventReceiverDefinitionCreationInformation** object to create the new remote event receiver.</span></span> <span data-ttu-id="0a4a3-195">Тип приемника событий **ItemAdded** добавляется **EventReceiverDefinitionCreationInformation.EventType**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-195">The **ItemAdded** event receiver type is added to **EventReceiverDefinitionCreationInformation.EventType**.</span></span>
    
    - <span data-ttu-id="0a4a3-196">Задает **EventReceiverDefinitionCreationInformation.ReceiverURL** URL-адрес в **AppInstalled** удаленный приемник событий.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-196">Sets the  **EventReceiverDefinitionCreationInformation.ReceiverURL** to the URL of the **AppInstalled** remote event receiver.</span></span>
    
    - <span data-ttu-id="0a4a3-197">Добавляет новый приемника событий в список с помощью **List.EventReceivers.Add**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-197">Adds a new event receiver to the list using  **List.EventReceivers.Add**.</span></span>

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

<span data-ttu-id="0a4a3-198">При добавлении элемента в список **Заданий приемника удаленных событий** **ProcessEvent** в AppEventReceiver.svc.cs обрабатывает событие **ItemAdded** , а затем вызывает **HandleItemAdded**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-198">When an item is added to the  **Remote Event Receiver Jobs** list, **ProcessEvent** in AppEventReceiver.svc.cs handles the **ItemAdded** event, and then calls **HandleItemAdded**.</span></span>  <span data-ttu-id="0a4a3-199">**HandleItemAdded** вызывает **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-199">**HandleItemAdded** calls **RemoteEventReceiverManager.ItemAddedToListEventHandler**.</span></span>  <span data-ttu-id="0a4a3-200">**ItemAddedToListEventHandler** выбирает элемент списка, который был добавлен и добавляет строку **обновлен с ReR** описание элемента списка.</span><span class="sxs-lookup"><span data-stu-id="0a4a3-200">**ItemAddedToListEventHandler** fetches the list item that was added, and adds the string **Updated by ReR** to the list item's description.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="0a4a3-201">См. также</span><span class="sxs-lookup"><span data-stu-id="0a4a3-201">See also</span></span>
<span data-ttu-id="0a4a3-202"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0a4a3-202"></span></span>

-  [<span data-ttu-id="0a4a3-203">Шаблоны и рекомендации решений разработки Office 365</span><span class="sxs-lookup"><span data-stu-id="0a4a3-203">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
    
-  [<span data-ttu-id="0a4a3-204">Core.AppEvents.HandlerDelegation</span><span class="sxs-lookup"><span data-stu-id="0a4a3-204">Core.AppEvents.HandlerDelegation </span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.AppEvents.HandlerDelegation)
    
