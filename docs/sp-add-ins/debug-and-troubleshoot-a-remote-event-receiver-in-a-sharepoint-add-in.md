---
title: Устранение неполадок и отладка удаленного приемника событий в надстройке для SharePoint
description: Настройка среды разработки для отладки удаленных событий с помощью Visual Studio.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: b6b34bef859eaaaa50361741220276a13c32d29e
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="debug-and-troubleshoot-a-remote-event-receiver-in-a-sharepoint-add-in"></a><span data-ttu-id="60f15-103">Устранение неполадок и отладка удаленного приемника событий в надстройке SharePoint</span><span class="sxs-lookup"><span data-stu-id="60f15-103">Debug and troubleshoot a remote event receiver in a SharePoint Add-in</span></span>

## <a name="configure-debugging-for-a-remote-sharepoint-test-site"></a><span data-ttu-id="60f15-104">Настройка отладки для удаленного тестового сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="60f15-104">Configure debugging for a remote SharePoint test site</span></span>

> [!NOTE] 
> <span data-ttu-id="60f15-105">Описанные в этом разделе действия применимы, только если Visual Studio и тестовый сайт SharePoint развернуты на разных компьютерах или если в качестве тестового сайта используется сайт разработчика SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="60f15-105">Note  The procedures in this section apply only when your test SharePoint site is on a different computer from Visual Studio or you are using an SharePoint Online Developer Site as your test site. If SharePoint and Visual Studio are on the same computer, skip this section.</span></span> <span data-ttu-id="60f15-106">Если SharePoint и Visual Studio развернуты на одном компьютере, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="60f15-106">If SharePoint and Visual Studio are on the same computer, skip this section.</span></span>

<span data-ttu-id="60f15-107">Если проект надстройки SharePoint в Visual Studio содержит удаленный приемник событий (RER) или приемник событий надстройки, то для отладки надстройки с помощью клавиши F5 нужно выполнить дополнительную быструю настройку свойств проекта.</span><span class="sxs-lookup"><span data-stu-id="60f15-107">When a SharePoint Add-in project in Visual Studio includes a remote event receiver (RER) or an add-in event receiver, you have to do some additional quick configuration in the project properties before you can debug the add-in with (F5).</span></span> <span data-ttu-id="60f15-108">А для этого, в свою очередь, требуется настроить Azure.</span><span class="sxs-lookup"><span data-stu-id="60f15-108">This configuration, in turn, requires that you do some Azure configuration.</span></span> <span data-ttu-id="60f15-109">Повторять настройку Azure для каждого проекта, который содержит удаленный приемник событий или событие надстройки, не требуется.</span><span class="sxs-lookup"><span data-stu-id="60f15-109">You do not have to repeat the Azure configuration for every project that has an RER or add-in event.</span></span> <span data-ttu-id="60f15-110">(Если надстройка содержит обработчик событий AppInstalled, она не запустится ни с помощью клавиши F5, ни с помощью клавиш CTRL+F5 [запуск без отладки], пока не будут выполнены настройки, описанные в этом разделе.)</span><span class="sxs-lookup"><span data-stu-id="60f15-110">(If the add-in includes an AppInstalled event handler, the add-in won't even run with either F5 or Ctrl+F5 [run without debugging] unless you carry out the configuration in this section.)</span></span>

### <a name="to-configure-azure"></a><span data-ttu-id="60f15-111">Настройка Azure</span><span class="sxs-lookup"><span data-stu-id="60f15-111">To configure Azure</span></span>

1. <span data-ttu-id="60f15-112">Если у вас еще нет подписки Microsoft Azure, приобретите ее.</span><span class="sxs-lookup"><span data-stu-id="60f15-112">If you don't already have one, get an Microsoft Azure subscription. One is included as a benefit with an  MSDN Subscription.</span></span> <span data-ttu-id="60f15-113">Она входит в состав [подписки на Visual Studio](http://azure.microsoft.com/ru-RU/pricing/member-offers/msdn-benefits/).</span><span class="sxs-lookup"><span data-stu-id="60f15-113">If you don't already have one, get an Microsoft Azure subscription. One is included as a benefit with an  [MSDN Subscription](http://azure.microsoft.com/ru-RU/pricing/member-offers/msdn-benefits/).</span></span>

2. <span data-ttu-id="60f15-114">Выполните действия, описанные в разделе [Создание пространства имен служебной шины](https://docs.microsoft.com/ru-RU/azure/service-bus-messaging/service-bus-resource-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="60f15-114">Carry out the instructions in  [How To: Create or Modify a Service Bus Service Namespace](https://docs.microsoft.com/ru-RU/azure/service-bus-messaging/service-bus-resource-manager-overview).</span></span>
    

### <a name="to-configure-the-sharepoint-add-in-project-in-visual-studio"></a><span data-ttu-id="60f15-115">Настройка проекта надстройки SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="60f15-115">To configure the SharePoint Add-in project in Visual Studio</span></span>

1. <span data-ttu-id="60f15-116">Вам потребуется последняя версия Инструментов разработчика Office для Visual Studio, поэтому [запустите установщик веб-платформы](http://aka.ms/OfficeDevToolsForVS2013) или [установщик Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="60f15-116">You should have the latest version of the Office Developer Tools for Visual Studio 2013, so  [run the WebPI installer here](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>

2. <span data-ttu-id="60f15-117">Добавив удаленный приемник событий или обработчик событий надстройки в проект надстройки SharePoint в Visual Studio, щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="60f15-117">After you add a RER or add-in event handler to a SharePoint Add-in project in Visual Studio, right-click the project in **Solution Explorer** and select **Properties**.</span></span>

3. <span data-ttu-id="60f15-118">На панели свойств откройте вкладку **SharePoint** и прокрутите вниз.</span><span class="sxs-lookup"><span data-stu-id="60f15-118">In the properties pane, open the **SharePoint** tab and scroll to the bottom.</span></span>

4. <span data-ttu-id="60f15-119">Установите флажок **Включить отладку через шину обслуживания Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="60f15-119">Select the check box for **Enable debugging via Microsoft Azure Service Bus**.</span></span>

5. <span data-ttu-id="60f15-p104">Укажите в текстовом поле полную строку подключения. Чтобы получить эту строку, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="60f15-p104">Enter the complete connection string in the text box provided. You obtain the string with these steps.</span></span>
    
    1. <span data-ttu-id="60f15-122">Войдите на портал Azure и откройте вкладку **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="60f15-122">Log in to the Azure portal and open the  **Service Bus** tab.</span></span>

    2. <span data-ttu-id="60f15-123">Откройте пространство имен, созданное для отладки удаленного приемника событий и перейдите к строкам подключения.</span><span class="sxs-lookup"><span data-stu-id="60f15-123">Open the namespace that you created for RER debugging and navigate to the connection strings. The Azure portal UI changes frequently. See  Azure portal help if you can't find the connection strings.</span></span> <span data-ttu-id="60f15-124">Пользовательский интерфейс портала Azure часто меняется.</span><span class="sxs-lookup"><span data-stu-id="60f15-124">The Azure portal UI changes frequently.</span></span> <span data-ttu-id="60f15-125">Если не удается найти строки подключения, см. [справку по порталу Azure](https://docs.microsoft.com/ru-RU/azure/).</span><span class="sxs-lookup"><span data-stu-id="60f15-125">If you can't find the connection strings, see [Azure portal help](https://docs.microsoft.com/ru-RU/azure/).</span></span>

    3. <span data-ttu-id="60f15-p106">Скопируйте строку подключения **SAS**. Это строка, которую вы указываете в свойствах проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="60f15-p106">Copy the **SAS** connection string. This is the string you enter in the Visual Studio project properties.</span></span>

<span data-ttu-id="60f15-128">В дальнейшем при создании проектов Надстройка SharePoint в Visual Studio эти сведения будут заполнены заранее, поэтому не потребуется каждый раз открывать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60f15-128">In the future, when you create SharePoint Add-in projects in Visual Studio, this information is prefilled, so you don't have to open the Azure portal each time.</span></span>


<span data-ttu-id="60f15-129"><a name="CreateRER"> </a></span><span class="sxs-lookup"><span data-stu-id="60f15-129"></span></span>

## <a name="test-the-configuration"></a><span data-ttu-id="60f15-130">Тестирование конфигурации</span><span class="sxs-lookup"><span data-stu-id="60f15-130">Test the configuration</span></span>

<span data-ttu-id="60f15-131">Чтобы убедиться, что вы можете выполнять отладку RER, выполните процедуры, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="60f15-131">Use the procedures in this section to verify that you can debug an RER.</span></span>

### <a name="to-create-a-remote-event-receiver-project"></a><span data-ttu-id="60f15-132">Создание проекта приемника удаленных событий</span><span class="sxs-lookup"><span data-stu-id="60f15-132">To create a remote event receiver project</span></span>

1. <span data-ttu-id="60f15-133">В Visual Studio создайте надстройку SharePoint с размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="60f15-133">In Visual Studio, create a provider-hosted SharePoint Add-in.</span></span> <span data-ttu-id="60f15-134">См. статью [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="60f15-134">See  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>

2. <span data-ttu-id="60f15-135">В **обозревателе решений** выберите узел проекта надстройки.</span><span class="sxs-lookup"><span data-stu-id="60f15-135">In  **Solution Explorer** select the add-in project's node.</span></span>

3. <span data-ttu-id="60f15-136">В строке меню выберите **Проект** > **Добавить новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="60f15-136">On the menu bar, select **Project** > **Add New Item**.</span></span>

4. <span data-ttu-id="60f15-137">На панели **Шаблоны** выберите шаблон **Список**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="60f15-137">In the  **Templates** pane, choose the **List** template, and then choose the **Add** button.</span></span>

5. <span data-ttu-id="60f15-138">Нажмите **Готово**, чтобы добавить настраиваемый список по умолчанию в проект надстройки.</span><span class="sxs-lookup"><span data-stu-id="60f15-138">Choose the  **Finish** button to add a default custom list to the add-in project.</span></span>

6. <span data-ttu-id="60f15-139">Добавьте еще один элемент в проект надстройки, выбрав шаблон **Удаленный приемник событий** на панели **Шаблоны**.</span><span class="sxs-lookup"><span data-stu-id="60f15-139">Add another item to the add-in project by, in the  **Templates** pane, choosing the **Remote Event Receiver** template.</span></span>

7. <span data-ttu-id="60f15-140">В поле **Имя** оставьте имя, заданное по умолчанию (RemoteEventReceiver1), и нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="60f15-140">In the  **Name** box, leave the default name (RemoteEventReceiver1), and then choose the  **Add** button.</span></span>

8. <span data-ttu-id="60f15-141">В списке **Тип приемника событий** выберите **События элемента списка**.</span><span class="sxs-lookup"><span data-stu-id="60f15-141">In the **What type of event receiver do you want?** list, choose **List Item Events**.</span></span> <span data-ttu-id="60f15-142">В качестве источника события оставьте **List1** — список, который вы добавили на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="60f15-142">Leave the event source as **List1**, the list that you added in the previous steps.</span></span>

9. <span data-ttu-id="60f15-143">В списке **Обработать следующие события** выберите **Добавляется элемент** и нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="60f15-143">In the **Handle the following events** list, choose **An item is being added**, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="60f15-p109">Веб-сервис будет добавлен в веб-приложение для управления удаленным событием, которое вы указали. Приемник удаленных событий будет добавлен в Надстройка SharePoint. Он будет ссылаться на веб-службы и события элемента списка в файле Elements.xml приемника событий.</span><span class="sxs-lookup"><span data-stu-id="60f15-p109">A web service is added to the web application to handle the remote event that you specified. A remote event receiver is added to the SharePoint Add-in. The receiver references the web service and the list item event in the event receiver's Elements.xml file.</span></span>

10. <span data-ttu-id="60f15-147">В проекте надстройки откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="60f15-147">In the add-in project, open AppManifest.xml.</span></span>

11. <span data-ttu-id="60f15-148">Укажите страницу списка в качестве начальной: _AddInProjectName_/Lists/List1.</span><span class="sxs-lookup"><span data-stu-id="60f15-148">Change the start page to the list's page:  _AddInProjectName_/Lists/List1.</span></span>

12. <span data-ttu-id="60f15-149">Замените _AddInProjectName_ именем проекта надстройки, например `SharePointAddIn4/Lists/List1`.</span><span class="sxs-lookup"><span data-stu-id="60f15-149">Replace _AddInProjectName_ with the name of your add-in project, such as `SharePointAddIn4/Lists/List1`.</span></span> <span data-ttu-id="60f15-150">В этом примере начальной страницей назначается страница списка.</span><span class="sxs-lookup"><span data-stu-id="60f15-150">For this example, we're setting the start page to the list's page.</span></span> <span data-ttu-id="60f15-151">Но в типичной надстройке ссылка, скорее всего, будет указывать на ваш собственный пользовательский интерфейс на странице веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="60f15-151">Replace  AddInProjectName with the name of your add-in project, such asSharePointAddIn4/Lists/List1. For this example, we're setting the start page to the list's page. However, in a typical add-in, you'd likely point to your own UI on the web project page.</span></span>
    
 

### <a name="to-run-and-test-event-handler-debugging"></a><span data-ttu-id="60f15-152">Запуск и тестирование отладки обработчика событий</span><span class="sxs-lookup"><span data-stu-id="60f15-152">To run and test event handler debugging</span></span>

1. <span data-ttu-id="60f15-153">Если вы еще не сделали этого, выполните действия, описанные ранее в разделе **Настройка проекта надстройки SharePoint в Visual Studio** этой статьи.</span><span class="sxs-lookup"><span data-stu-id="60f15-153">If you haven't done so already, complete the **To configure the SharePoint Add-in project in Visual Studio** procedure earlier in this article.</span></span>

2. <span data-ttu-id="60f15-154">В веб-проекте откройте службу удаленного приемника событий (RemoteEventReceiver1.svc), а затем добавьте точку останова в любую строку кода внутри метода `ProcessEvent()`.</span><span class="sxs-lookup"><span data-stu-id="60f15-154">In the web project, open the remote event receiver service (RemoteEventReceiver1.svc), and then add a breakpoint to any line of code inside the  `ProcessEvent()` method.</span></span>

3. <span data-ttu-id="60f15-155">Нажмите клавишу **F5** для запуска проекта.</span><span class="sxs-lookup"><span data-stu-id="60f15-155">Choose the  **F5** key to run the project.</span></span>

4. <span data-ttu-id="60f15-156">Нажмите кнопку **+ Новый элемент**, чтобы добавить элемент в список.</span><span class="sxs-lookup"><span data-stu-id="60f15-156">Choose the  **+ New item** button to add an item to the list.</span></span>

5. <span data-ttu-id="60f15-157">Укажите название элемента, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="60f15-157">Provide a title for the item, and then choose the  **Save** button.</span></span> <span data-ttu-id="60f15-158">Будет достигнута точка останова, добавленная к обработчику удаленных событий и указывающая, что выполняется отладка обработчика удаленных событий.</span><span class="sxs-lookup"><span data-stu-id="60f15-158">The breakpoint that you added to the remote event receiver is hit, verifying that you're debugging the remote event receiver.</span></span>

6. <span data-ttu-id="60f15-159">Нажмите клавишу **F5**, чтобы продолжить выполнение проекта, а по завершении его работы остановите отладку.</span><span class="sxs-lookup"><span data-stu-id="60f15-159">Choose the  **F5** key to continue to run the project, and then stop debugging when you're done.</span></span>


<span data-ttu-id="60f15-160"><a name="RER_TurnOnOffNotificationsinRER"> </a></span><span class="sxs-lookup"><span data-stu-id="60f15-160"></span></span>

## <a name="turn-onoff-the-notification-from-visual-studio-that-event-debugging-needs-to-be-configured"></a><span data-ttu-id="60f15-161">Включение и отключение уведомлений от Visual Studio о необходимости настроить отладку событий</span><span class="sxs-lookup"><span data-stu-id="60f15-161">Turn on/off the notification from Visual Studio that event debugging needs to be configured</span></span>

<span data-ttu-id="60f15-162">Если в проекте используется удаленное событие, а отладка удаленных событий не настроена, Visual Studio предлагает ее настроить (см. следующий рисунок).</span><span class="sxs-lookup"><span data-stu-id="60f15-162">If you have a remote event in your project and have not configured remote event debugging, Visual Studio prompts you to configure remote event debugging (see Figure 1). You can change this behavior by clearing the  Notify me if remote event debugging is not configured check box on the SharePoint tab.</span></span> <span data-ttu-id="60f15-163">Чтобы это уведомление не отображалось, снимите флажок **Уведомлять меня, если отладка удаленных событий не настроена** на вкладке **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="60f15-163">If you have a remote event in your project and have not configured remote event debugging, vsnv prompts you to configure remote event debugging (see Figure 1). You can change this behavior by clearing the **Notify me if remote event debugging is not configured** check box on the **SharePoint** tab.</span></span>

<span data-ttu-id="60f15-164">**Уведомление об отладке удаленных событий**</span><span class="sxs-lookup"><span data-stu-id="60f15-164">**Figure 1. Remote event debugging notification**</span></span>

![Уведомления в удаленных приемниках событий](../images/SP15Con_Remote_Event_Receivers_FAQ_fig3.png)

<span data-ttu-id="60f15-166"><a name="RER_HowDoIKnowWheteherMyServiceisHostedintheServiceBus"> </a></span><span class="sxs-lookup"><span data-stu-id="60f15-166"></span></span>

## <a name="verify-that-your-service-is-hosted-in-the-service-bus"></a><span data-ttu-id="60f15-167">Проверка размещения службы в служебной шине</span><span class="sxs-lookup"><span data-stu-id="60f15-167">Verify that your service is hosted in the Service Bus</span></span>

<span data-ttu-id="60f15-168">Нажав клавишу F5 и установив доверие, перейдите к пространству имен служебной шины в браузере, например `http://mynamespace.servicebus.windows.net`, и вы увидите конечную точку в виде числа.</span><span class="sxs-lookup"><span data-stu-id="60f15-168">After you press F5 and trust the add-in, go to the Service Bus namespace in your browser; for example http://mynamespace.servicebus.windows.net, and you should see your endpoint listed as a number. Figure 2 shows what the page looks like when a namespace is not listed; that is, before you press F5.</span></span> <span data-ttu-id="60f15-169">На следующем рисунке показано, как выглядит страница, когда пространство имен *не* указано (то есть до нажатия клавиши F5).</span><span class="sxs-lookup"><span data-stu-id="60f15-169">The following figure shows what the page looks like when a namespace is *not* listed; that is, before you select F5.</span></span>

<span data-ttu-id="60f15-170">**Просмотр пространства имен служебной шины**</span><span class="sxs-lookup"><span data-stu-id="60f15-170">**Browsing to the service bus namespace**</span></span>

![Просмотр пространства имен служебной шины](../images/SP15Con_Remote_Event_Receivers_FAQ_fig4.PNG)

<span data-ttu-id="60f15-172"><a name="RER_DoesNotHitTheBreakPoint"> </a></span><span class="sxs-lookup"><span data-stu-id="60f15-172"></span></span>

## <a name="rer-does-not-hit-the-breakpoint"></a><span data-ttu-id="60f15-173">Удаленный приемник событий не достигает точки останова</span><span class="sxs-lookup"><span data-stu-id="60f15-173">RER does not hit the breakpoint</span></span>

<span data-ttu-id="60f15-p114">Удаленные события бывают синхронными и асинхронными. Если событие асинхронное, то для активации точки останова может потребоваться несколько секунд или больше времени.</span><span class="sxs-lookup"><span data-stu-id="60f15-p114">Depending on the event, the remote event may be synchronous or asynchronous. It might take a few seconds or more to hit your breakpoint if it is asynchronous.</span></span>

## <a name="error-there-was-no-endpoint-listening"></a><span data-ttu-id="60f15-176">Ошибка: "Прослушивание не выполняла ни одна конечная точка"</span><span class="sxs-lookup"><span data-stu-id="60f15-176">Error: "There was no endpoint listening"</span></span>

<span data-ttu-id="60f15-177">При выполнении обработчика в рабочей среде возникает следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="60f15-177">You get the following error when your handler runs in production:</span></span>

<span data-ttu-id="60f15-178">*"Ошибка вызова приемника удаленных событий. Сведения: прослушивание на `https://{domain}:nnnnn/{path}/AppEventReceiver.svc` не выполняла ни одна конечная точка, которая могла бы принять сообщение. Это могло быть вызвано неправильным адресом или действием SOAP".*</span><span class="sxs-lookup"><span data-stu-id="60f15-178">"The remote event receiver callout failed. Details: There was no endpoint listening at https:// {domain}:     {path}/AppEventReceiver.svc that could accept the message. This is often caused by an incorrect address or SOAP action." where     is a port.</span></span> <span data-ttu-id="60f15-179">(При этом _nnnnn_ является портом.)</span><span class="sxs-lookup"><span data-stu-id="60f15-179">(where  _nnnnn_ is a port).</span></span>

<span data-ttu-id="60f15-p116">SharePoint требует отсутствия явного порта в URL-адресе обработчика в рабочей среде. Это означает, что вам необходимо использовать либо порт 443 для HTTPS, что мы и рекомендуем, либо порт 80 для HTTP.</span><span class="sxs-lookup"><span data-stu-id="60f15-p116">SharePoint requires that there be no explicit port in the URL of the handler in production. This means that you must use either port 443 for HTTPS, which we recommend, or port 80 for HTTP.</span></span> 

## <a name="error-could-not-establish-trust-relationship-for-the-ssltls-secure-channel-with-authority"></a><span data-ttu-id="60f15-182">Ошибка: "Не удалось установить доверительные отношения для защищенного канала SSL/TLS с полномочиями"</span><span class="sxs-lookup"><span data-stu-id="60f15-182">Error: "Could not establish trust relationship for the SSL/TLS secure channel with authority"</span></span>

<span data-ttu-id="60f15-183">При выполнении обработчика в рабочей среде возникает следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="60f15-183">You get the following error when your handler runs in production:</span></span>

<span data-ttu-id="60f15-184">*"Ошибка вызова приемника удаленных событий. Ошибка: Не удалось установить доверительные отношения для защищенного канала SSL/TLS с полномочиями".*</span><span class="sxs-lookup"><span data-stu-id="60f15-184">*"The remote event receiver callout failed. Details: Could not establish trust relationship for the SSL/TLS secure channel with authority"*</span></span>

<span data-ttu-id="60f15-185">Когда надстройка находится в SharePoint Online, но удаленный приемник событий расположен в локальной среде и использует HTTPS согласно нашим рекомендациям, сервер, на котором размещен приемник, не может использовать самозаверяющий сертификат в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="60f15-185">When the add-in is in Microsoft SharePoint Online, but the remote event receiver service is on-premise, and is using HTTPS as we recommend, the server that is hosting the receiver cannot use a self-signed certificate in production. The server must have a publicly accepted certificate from a certificate authority. If the add-in is in an on-premise SharePoint farm, self-signed certificates are acceptable.</span></span> <span data-ttu-id="60f15-186">Серверу необходим общепринятый сертификат от центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="60f15-186">The server must have a publicly accepted certificate from a certificate authority.</span></span> <span data-ttu-id="60f15-187">Если надстройка находится в локальной ферме SharePoint, можно использовать самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="60f15-187">If the add-in is on an on-premises SharePoint farm, self-signed certificates are acceptable.</span></span>

## <a name="see-also"></a><span data-ttu-id="60f15-188">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="60f15-188">See also</span></span>

-  [<span data-ttu-id="60f15-189">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="60f15-189">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins.md)
 

