
# <a name="update-sharepoint-add-ins"></a><span data-ttu-id="e0a80-101">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-101">Update SharePoint Add-ins</span></span>
<span data-ttu-id="e0a80-102">Узнайте, как создать и развернуть обновление надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e0a80-102">Learn how to create and deploy an update for a spappsing.</span></span>
 

 <span data-ttu-id="e0a80-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="e0a80-p102">Вы можете обновить свою надстройку SharePoint, используя встроенные в SharePoint средства поддержки обновлений. В течение 24 часов после того, как вы отправите обновленную версию надстройки в каталог надстроек организации или она будет принята в Магазин Office, рядом с надстройкой на странице **Содержимое сайта** каждого веб-сайта, на котором она установлена, появится уведомление о доступном обновлении. Как видно на рисунке 1, пользователям предоставляется ссылка для мгновенной установки обновления.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p102">Learn how to create and deploy an update for a SharePoint Add-in. You can update your SharePoint Add-in by using the updating support built into SharePoint. Within 24 hours after you upload an updated version of the add-in to the organization's add-in catalog or the add-in is accepted at the Office Store, a notification that an update is available appears next to the add-in on **Site Contents** page of every website where it is installed. As you can see in Figure 1, a link is provided for users to immediately install the update.</span></span>
 

<span data-ttu-id="e0a80-109">**Рис. 1. Процесс обновления надстройки SharePoint**</span><span class="sxs-lookup"><span data-stu-id="e0a80-109">**Figure 1. Add-in for SharePoint update process**</span></span>

 

 
![Руководство по обновлению приложения в пользовательском интерфейсе](../../images/UpdatingApp_AppTileUpdateNotice.png)
 
<span data-ttu-id="e0a80-p103">Пользователь может установить обновление, не удаляя предыдущую версию. Инфраструктура обновления проверяет установку обновления и выполняет ее откат в случае каких-либо ошибок.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p103">A user can install the update without first uninstalling the earlier version. The update infrastructure tests the update installation and rolls it back if there are any errors.</span></span>
 

    
 <span data-ttu-id="e0a80-p104">**Важно!** С помощью системы обновления невозможно изменить *тип надстройки*. Например, надстройку с размещением в SharePoint невозможно преобразовать в размещенную у поставщика с помощью обновления. Чтобы изменить тип, необходимо [выполнить миграцию из старой надстройки в новую](sharepoint-add-ins-update-process#Major). В частности, следует помнить, что так как [ознакомительная программа для автоматически размещаемых надстроек была закрыта](http://blogs.office.com/2014/05/16/update-on-autohosted-apps-preview-program/), автоматически размещаемую надстройку невозможно обновить до размещаемой у поставщика. Потребуется преобразовать надстройку согласно инструкциям из статьи [Преобразование автоматически размещаемой надстройки SharePoint в надстройку с размещением у поставщика](convert-an-autohosted-sharepoint-add-in-to-a-provider-hosted-add-in).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p104">You cannot change the add-in type using the update system. For example, you cannot change an add-in from SharePoint-hosted to provider-hosted with an update. To make a change of type, you need to migrate from an old add-in to a new one. In particular, since  the preview program for autohosted add-ins has been closed http://blogs.office.com/2014/05/16/update-on-autohosted-apps-preview-program/ , you should be aware that you cannot update an autohosted add-in to a provider-hosted add-in. You have to convert the add-in as explained in How to: Convert an autohosted SharePoint Add-in to a provider-hosted add-in.</span></span>
 


## <a name="prerequisites-for-updating-a-sharepoint-add-in"></a><span data-ttu-id="e0a80-118">Необходимые условия для обновления надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-118">Prerequisites for updating a SharePoint Add-in</span></span>
<span data-ttu-id="e0a80-119"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-119"></span></span>


 

 

- <span data-ttu-id="e0a80-p105">Тестовая установка SharePoint, которая поддерживает изоляцию. Указания по настройке Сайт разработчиков Office 365 см. в статье  [Настройка среды для разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p105">A test SharePoint installation that is configured for add-in isolation. See  [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365) for instructions on how to set up an Office 365 Developer Site.</span></span>
    
 
- <span data-ttu-id="e0a80-p106">Средства, используемые при создании Надстройка SharePoint, обычно также используются для его обновления. Например, многие разработчики используют Visual Studio и Инструменты разработчика Microsoft Office для Visual Studio для создания Надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p106">Tools that are used in creating a SharePoint Add-in are usually also used in updating it. For example, most developers use Visual Studio and Microsoft Office Developer Tools for Visual Studio to create SharePoint Add-ins.</span></span>
    
 

### <a name="core-concepts-to-know-to-update-a-sharepoint-add-in"></a><span data-ttu-id="e0a80-124">Основные понятия, которые необходимо знать при обновлении надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-124">Core concepts to know to update a SharePoint Add-in</span></span>


 

 

<span data-ttu-id="e0a80-125">**Таблица 1. Основные понятия, связанные с обновлением надстроек SharePoint**</span><span class="sxs-lookup"><span data-stu-id="e0a80-125">**Table 1. Core concepts for updating a SharePoint Add-in**</span></span>


|<span data-ttu-id="e0a80-126">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="e0a80-126">**Article title**</span></span>|<span data-ttu-id="e0a80-127">**Описание**</span><span class="sxs-lookup"><span data-stu-id="e0a80-127">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="e0a80-128">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-128">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in)|<span data-ttu-id="e0a80-p107">Сведения о различных типах надстроек SharePoint. Процесс обновления для разных типов отличается.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p107">Learn about the different types of SharePoint Add-ins. The updating process varies depending on the type.</span></span>|
| [<span data-ttu-id="e0a80-131">Процесс обновления надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-131">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process)|<span data-ttu-id="e0a80-132">Описание процесса обновления надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e0a80-132">Learn about the process for updating SharePoint Add-ins.</span></span>|
| [<span data-ttu-id="e0a80-133">Обновление компонентов</span><span class="sxs-lookup"><span data-stu-id="e0a80-133">Upgrading Features</span></span>](http://msdn.microsoft.com/library/e917f709-6491-4d50-adbe-2ab8f35da990%28Office.15%29.aspx)|<span data-ttu-id="e0a80-134">Узнайте, как обновлять компоненты (пакет SDK SharePoint 2010).</span><span class="sxs-lookup"><span data-stu-id="e0a80-134">Learn how to update Features (SharePoint 2010 SDK).</span></span>|
| [<span data-ttu-id="e0a80-135">Развертывание и установка надстроек SharePoint: методы и параметры</span><span class="sxs-lookup"><span data-stu-id="e0a80-135">Deploying and installing SharePoint Add-ins: methods and options</span></span>](deploying-and-installing-sharepoint-add-ins-methods-and-options)|<span data-ttu-id="e0a80-136">Сведения о методах публикации, установки и удаления надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e0a80-136">Learn about the methods for publishing, installing, and uninstalling a SharePoint Add-in.</span></span>|
| [<span data-ttu-id="e0a80-137">Обработка событий в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-137">Handle events in SharePoint Add-ins</span></span>](handle-events-in-sharepoint-add-ins)|<span data-ttu-id="e0a80-138">Сведения о приемниках удаленных событий в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e0a80-138">Learn about remote event receivers in SharePoint.</span></span>|

## <a name="major-steps-in-updating-an-add-in"></a><span data-ttu-id="e0a80-139">Основные действия при обновлении надстройки</span><span class="sxs-lookup"><span data-stu-id="e0a80-139">Major steps in updating an add-in</span></span>
<span data-ttu-id="e0a80-140"><a name="MajorAppUpgradeSteps"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-140"></span></span>

<span data-ttu-id="e0a80-p108">Ниже описаны основные действия, которые могут быть необходимы при создании обновления для надстройки SharePoint. Каждое действие подробно рассматривается в разделах статьи, на которые можно перейти по ссылкам. Не все они являются обязательными в каждом проекте обновления. Необходимые действия зависят от того, какие компоненты уже содержатся в надстройке и какие необходимо добавить. Обязательными являются только элементы, отмеченные знаком *****.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p108">The following are the major steps that may be needed when you create an update for a SharePoint Add-in. Each step is discussed in detail in linked sections or articles. Not all the steps are required in every update project. What you must do depends on what components are already in your add-in and what components you are adding. Only the items marked with ***** are always required.</span></span>
 

 

- <span data-ttu-id="e0a80-146">Обновите манифест надстройки.</span><span class="sxs-lookup"><span data-stu-id="e0a80-146">Update the add-in manifest.</span></span>
    
      -  <span data-ttu-id="e0a80-p109">***** Увеличьте номер **Version** в элементе [App](http://msdn.microsoft.com/library/d5f30dfe-7500-5f85-0f08-f4f220c0c692%28Office.15%29.aspx) файла appmanifest.xml. (В первоначальном выпуске схемы надстройки назывались "приложениями".) *Не*  изменяйте номер **ProductID**.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p109">***** Raise the **Version** number in the [App](http://msdn.microsoft.com/library/d5f30dfe-7500-5f85-0f08-f4f220c0c692%28Office.15%29.aspx) element of the appmanifest.xml file. (Add-ins were called "apps" when the schema was first released.) Do *not*  change the **ProductID** number.</span></span>
    
 
  - <span data-ttu-id="e0a80-149">Измените раздел [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx) файла appmanifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e0a80-149">Change the  [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx) section of the appmanifest.xml file.</span></span>
    
 
  - <span data-ttu-id="e0a80-150">Измените раздел [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx) файла appmanifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e0a80-150">Change the  [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx) section of the appmanifest.xml file.</span></span>
    
 

    <span data-ttu-id="e0a80-151">Дополнительные сведения см. в разделе [Обновление версии надстройки, запросов разрешений и необходимых условий](#UpdateManifest).</span><span class="sxs-lookup"><span data-stu-id="e0a80-151">For more information, see  [Update the add-in version, permission requests, and prerequisites](#UpdateManifest).</span></span>
    
 
- <span data-ttu-id="e0a80-p110">Добавьте или обновите часть кода для компонентов сайта надстройки. Дополнительные сведения см. в статье [Обновление компонентов сайта надстройки в SharePoint](update-add-in-web-components-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p110">Add or update the markup for add-in web components. For more information, see  [Update add-in web components in SharePoint](update-add-in-web-components-in-sharepoint-2013).</span></span>
    
 
- <span data-ttu-id="e0a80-p111">Добавьте или обновите часть кода для компонентов хост-сайта. Дополнительные сведения см. в статье [Обновление компонентов хост-сайта в SharePoint](update-host-web-components-in-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p111">Add or update the markup for host web components. For more information, see  [Update host web components in SharePoint](update-host-web-components-in-sharepoint-2013).</span></span>
    
 
- <span data-ttu-id="e0a80-p112">Добавьте настраиваемую логику в  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) и зарегистрируйте ее в файле appmanifest.xml. Подробнее см. в статье [Создание обработчика для события обновления в надстройках для SharePoint](create-a-handler-for-the-update-event-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p112">Add custom logic to an  [UpgradedEventEndpoint](http://msdn.microsoft.com/library/09a93d44-d295-47bb-f91c-d243178b0f53%28Office.15%29.aspx) and register it in the appmanifest.xml file. For more information, see [Create a handler for the update event in SharePoint Add-ins](create-a-handler-for-the-update-event-in-sharepoint-add-ins).</span></span>
    
 
- <span data-ttu-id="e0a80-158">Обновите удаленные компоненты.</span><span class="sxs-lookup"><span data-stu-id="e0a80-158">Update the remote components:</span></span>
    
      - <span data-ttu-id="e0a80-159">Для надстройки, размещаемой у поставщика, обновите удаленные компоненты с помощью методов, соответствующих платформам, используемым для размещения.</span><span class="sxs-lookup"><span data-stu-id="e0a80-159">For a provider-hosted add-in, update the remote components using the techniques appropriate for the hosting platform stack.</span></span>
    
 

    <span data-ttu-id="e0a80-160">Дополнительные сведения см. в статье [Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="e0a80-160">For more information, see  [Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins).</span></span>
    
 
-  <span data-ttu-id="e0a80-161">***** Отправьте пакет надстройки в Магазин Office или каталог надстроек организации.</span><span class="sxs-lookup"><span data-stu-id="e0a80-161">***** Upload the add-in package to the Office Store or the organization's add-in catalog.</span></span>
    
 

## <a name="best-practices-for-add-in-updates"></a><span data-ttu-id="e0a80-162">Рекомендации по обновлению надстроек</span><span class="sxs-lookup"><span data-stu-id="e0a80-162">Best practices for add-in updates</span></span>
<span data-ttu-id="e0a80-163"><a name="BestUpdatePractices"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-163"></span></span>

<span data-ttu-id="e0a80-164">В следующих разделах рассматриваются процедуры, которым нужно следовать, и важные вопросы, на которые следует обратить внимание при планировании обновления.</span><span class="sxs-lookup"><span data-stu-id="e0a80-164">The following sections discuss practices you should follow and important points to consider as you are planning an update.</span></span>
 

 

### <a name="decide-whether-you-really-have-to-update"></a><span data-ttu-id="e0a80-165">Определение необходимости обновления</span><span class="sxs-lookup"><span data-stu-id="e0a80-165">Decide whether you really have to update</span></span>

<span data-ttu-id="e0a80-p113">Улучшить Надстройка SharePoint с размещением у поставщика можно и без ее обновления. Если изменения касаются только удаленных компонентов и не должны отражаться на компонентах SharePoint, можно изменить удаленные компоненты, не обновляя надстройку. Если не изменяются URL-адреса и строки подключения, используемые компонентами SharePoint для доступа к удаленным компонентам, Надстройка SharePoint будет продолжать работать. Допустим, вы добавили кнопку в удаленное веб-приложение, которое читает столбец из списка SharePoint, который ранее не был прочтен веб-приложением. Если столбец уже существует в списке, вам не нужно ничего менять в SharePoint. Вы можете загрузить измененную веб-страницу, измененный код или JavaScript в удаленное веб-приложение. Новые функции мгновенно станут доступны пользователям при запуске Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p113">For a provider-hosted SharePoint Add-in, improvements to the add-in do not necessarily require updating the add-in. If all the changes are to remote components, and those changes don't have to be reflected in SharePoint components, you can change the remote components without updating the add-in. As long as the URLs and connection strings that the SharePoint components use to access the remote components do not change, the SharePoint Add-in continues to work. For example, suppose that you add a button to a remote web application that reads a column from a SharePoint list that the web application did not previously read. If the column already exists on the list, you do not have to change anything in SharePoint. You can upload the revised webpage, and the revised code behind or JavaScript, to the remote web application. The new functionality is immediately available to users when they start the SharePoint Add-in.</span></span>
 

 

### <a name="remember-that-updating-is-optional-for-users"></a><span data-ttu-id="e0a80-173">Необязательное обновление для пользователей</span><span class="sxs-lookup"><span data-stu-id="e0a80-173">Remember that updating is optional for users</span></span>

<span data-ttu-id="e0a80-p114">Когда новая версия надстройки SharePoint становится доступна в Магазин Office или каталоге надстроек организации, на плитке надстройки на странице **Содержимое сайта** пользователи видят сообщение о доступном обновлении. Оно появляется в течение 24 часов. Но инфраструктура SharePoint не принуждает пользователей к обновлению. Поэтому изменения, которые вы вносите в удаленные компоненты, не должны нарушать работу предыдущих версий надстройки. Общее, но не универсальное, правило гласит, что следует *добавлять* новое в удаленные компоненты, но избегать удаления, переименования, перемещения или изменения схемы, строки подключения или URL-адреса существующих компонентов.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p114">When a new version of your SharePoint Add-in becomes available in the Office Store or the organization's add-in catalog, a message appears on the add-in's tile on the **Site Contents** page informing users that an update is available. It takes no more than 24 hours for this message to appear. But nothing in the SharePoint infrastructure forces users to update. So changes that you make to remote components must not break the older versions of the add-in. A general, but not quite universal, rule is that you should *add*  things to remote components, but avoid deleting, renaming, moving, or changing the schema, connection string, or URL of any existing component.</span></span>
 

 
<span data-ttu-id="e0a80-p115">Если удаленному компоненту необходимо знать версию экземпляра надстройки, который его вызывает, вы можете отправить эти сведения из SharePoint. Например, можно добавить версию надстройки как параметр запроса в URL-адресе  [начальной страницы](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx) приложения.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p115">If a remote component needs to know the version of the add-in instance that is calling it, you can pass this information from SharePoint. For example, you can add the add-in version as a query parameter on the  [StartPage](http://msdn.microsoft.com/library/3092674c-a6c3-9021-3d7e-e716562a4a4f%28Office.15%29.aspx) URL of the add-in.</span></span>
 

 

### <a name="create-and-debug-the-new-version-as-if-it-were-a-brand-new-add-in"></a><span data-ttu-id="e0a80-181">Создание и отладка новой версии в качестве новой надстройки</span><span class="sxs-lookup"><span data-stu-id="e0a80-181">Create and debug the new version as if it were a brand new add-in</span></span>
<span data-ttu-id="e0a80-182"><a name="DebugFirst"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-182"></span></span>

<span data-ttu-id="e0a80-p116">Следует отделять разработку и отладку новой версии надстройки от отладки разметки и логики обновления. Для этого удалите предыдущую версию надстройки из тестового сайта SharePoint для разработки. Сохраните резервную копию файла пакета надстройки для предыдущей версии. Необходимым образом добавьте и измените компоненты надстройки, а затем проверьте и отладьте их с использованием тестового сайта, как будто это новая надстройка, созданная с нуля.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p116">You should separate the development and debugging of the new version of the add-in from the debugging of the update markup and logic. To do this, uninstall the earlier version of the add-in from your development test SharePoint site. Save a backup copy of the add-in package file for the earlier version. Add and change components of the add-in as needed, and then test and debug them against the test site as if it is a brand new add-in you are creating from scratch.</span></span>
 

 

### <a name="test-the-update-with-each-earlier-version-of-the-add-in"></a><span data-ttu-id="e0a80-187">Тестирование обновления с каждой предыдущей версией надстройки</span><span class="sxs-lookup"><span data-stu-id="e0a80-187">Test the update with each earlier version of the add-in</span></span>
<span data-ttu-id="e0a80-188"><a name="DebugFirst"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-188"></span></span>

<span data-ttu-id="e0a80-p117">Когда вы убедитесь, что новая версия надстройки правильно работает в качестве новой надстройки, измените код и разметку таким образом, чтобы проект являлся обновлением старой надстройки. Например, увеличьте номер версии надстройки, как указано в статье  [Основные действия при обновлении надстройки](#MajorAppUpgradeSteps). Дополнительные сведения о преобразовании проекта в обновление см. в разделах этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p117">When the new version of the add-in is functioning correctly as a "new" add-in, restructure the code and markup so that the project is an update of the old add-in. For example, increment the add-in version number as indicated in  [Major steps in updating an add-in](#MajorAppUpgradeSteps). For more information about turning the project into an update, see the child topics of this topic.</span></span>
 

 
<span data-ttu-id="e0a80-p118">Когда вы будете готовы проверить свое обновление, отзовите новую версию из тестового сайта и повторно разверните предыдущую версию, чтобы иметь возможность проверить логику обновления. Если вы предоставили много предыдущих версий надстройки, установите каждую предыдущую версию на отдельный дочерний сайт тестового сайта. Затем передайте последнюю версию надстройки в каталог надстроек тестового сайта и обновите каждый экземпляр надстройки. Убедитесь, что каждый из них имеет последний номер версии надстройки и версии всех компонентов. Если в надстройке используется сайт надстройки, убедитесь, что его компоненты развернуты соответственно процедуре, описанной в статье  [Проверка развертывания компонентов сайта надстройки](update-add-in-web-components-in-sharepoint-2013#VerifyDeployAppWebComp).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p118">When you are ready to test your update, retract the new version from the test site and redeploy the earlier version so you can test update logic. If you have shipped multiple previous versions of the add-in, install each earlier version on a different subweb of your test site. Then upload the latest version of the add-in to your test site's add-in catalog and update every instance of the add-in. Verify that each has the latest add-in version number and the latest version of all components. If there is an add-in web in the add-in, verify that the add-in web components have been deployed using the procedure in  [Verify deployment of add-in web components](update-add-in-web-components-in-sharepoint-2013#VerifyDeployAppWebComp).</span></span>
 

 

### <a name="update-an-add-in-without-waiting-24-hours"></a><span data-ttu-id="e0a80-197">Обновление надстройки без необходимости ожидать 24 часа</span><span class="sxs-lookup"><span data-stu-id="e0a80-197">Update an add-in without waiting 24 hours</span></span>
<span data-ttu-id="e0a80-198"><a name="ImmediateUpdateNotice"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-198"></span></span>

<span data-ttu-id="e0a80-p119">При разработке обновления для надстройки на тестовом сайте SharePoint нет смысла ждать 24 часа между обновлениями. Вы (и пользователи производственного сайта SharePoint) можете обновить надстройку мгновенно после ее отправки в Магазин Office или каталог надстроек организации, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p119">When developing an update for an add-in on your SharePoint test site, it is impractical to wait 24 hours between updates. You (and users on a production SharePoint site) can update an add-in immediately after it is uploaded to the Office Store or the organization's add-in catalog with these steps:</span></span>
 

 

### <a name="to-immediately-update-an-add-in"></a><span data-ttu-id="e0a80-201">Мгновенное обновление надстройки</span><span class="sxs-lookup"><span data-stu-id="e0a80-201">To immediately update an add-in</span></span>


1. <span data-ttu-id="e0a80-202">После того как последнее обновление будет отправлено в каталог надстроек, откройте страницу **Содержимое сайта** на веб-сайте, на котором установлена надстройка, и нажмите кнопку **…** на плитке надстройки.</span><span class="sxs-lookup"><span data-stu-id="e0a80-202">After the latest update is uploaded to the add-in catalog, open the **Site Contents** page on the website where the add-in is installed and choose the **...** button on the add-in's tile.</span></span>
    
 
2. <span data-ttu-id="e0a80-p120">В появившейся выноске выберите вкладку **О программе**. На открывшейся странице **О программе** вы увидите сообщение о доступности новой версии.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p120">On the callout that opens, choose the **About** tab. On the **About** page that opens, there is a notice that a new version is available.</span></span>
    
 
3. <span data-ttu-id="e0a80-p121">Нажмите кнопку **Получить**. Снова откроется страница **Содержимое сайта**, и на плитке надстройки появится сообщение о выполнении обновления.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p121">Choose the **Get It** button. The **Site Contents** page reopens, and there is a notice on the add-in's tile that the add-in is being updated.</span></span>
    
 
<span data-ttu-id="e0a80-207">На рис. 2 показаны эти действия.</span><span class="sxs-lookup"><span data-stu-id="e0a80-207">Figure 2 illustrates these steps.</span></span>
 

 

<span data-ttu-id="e0a80-208">**Рис. 2. Процесс мгновенного обновления надстройки SharePoint**</span><span class="sxs-lookup"><span data-stu-id="e0a80-208">**Figure 2. Process of immediately updating a SharePoint Add-in**</span></span>

 

 
![Процесс мгновенного обновления приложения](../../images/UpdatingApp_ImmediateUpgradeProcess.png)
 

    
 <span data-ttu-id="e0a80-210">**Примечание.** Чтобы сообщение о доступности обновления на плитке надстройки отображалось чаще, чем каждые 24 часа, вы можете использовать метод, описанный в статье [Процесс обновления надстройки SharePoint](sharepoint-add-ins-update-process#Minor), чтобы оно появлялось мгновенно.</span><span class="sxs-lookup"><span data-stu-id="e0a80-210">**Note** If you need to see the "update available" notice on the add-in's tile more frequently than every 24 hours, you can use the method described in  [Update process for a SharePoint Add-in](sharepoint-add-ins-update-process#Minor) to make the notice appear immediately.</span></span>
 


## <a name="update-the-add-in-version-permission-requests-and-prerequisites"></a><span data-ttu-id="e0a80-211">Обновление версии надстройки, запросов разрешений и необходимых условий</span><span class="sxs-lookup"><span data-stu-id="e0a80-211">Update the add-in version, permission requests, and prerequisites</span></span>
<span data-ttu-id="e0a80-212"><a name="UpdateManifest"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-212"></span></span>

<span data-ttu-id="e0a80-p122">Создав резервную копию папки проекта Visual Studio, откройте проект надстройки. Откройте манифест надстройки и на вкладке **Общие** конструктора манифеста увеличьте номер версии.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p122">After making a backup copy of the Visual Studio project folder, open the add-in project. Open add-in manifest and raise the version number on the **General** tab of the manifest designer.</span></span>
 

 
<span data-ttu-id="e0a80-p123">Если обновленной версии надстройки требуется больше (или меньше) разрешений для компонентов хост-сайта, внесите необходимые изменения в раздел надстройки  [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx). В Visual Studio используйте вкладку **Разрешения** конструктора манифеста. После обновления надстройки пользователь будет видеть подсказки с предложением предоставить разрешения, независимо от того, изменились ли разрешения по сравнению с предыдущей версией. Если в новой версии требуется *меньше*  разрешений по сравнению с предыдущей, дополнительные разрешения, имеющиеся в предыдущей версии, *не отзываются*  . Чтобы использовать в надстройке только те разрешения, которые предусмотрены в последней версии, необходимо после обновления надстройки перейти на страницу *{SharePointDomain}*  `/_layouts/15/appinv.aspx`, а затем вручную задать разрешения, соответствующие схеме  [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0a80-p123">If the updated version of the add-in needs more (or fewer) permissions to components of the host web, make changes as needed to the  [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx) section of the add-in. In Visual Studio, use the **Permissions** tab of the manifest designer. When an add-in is updated, the user is always prompted to grant permissions, whether the permissions have changed or not since the previous version. If the new version requests *fewer*  permissions than the preceding version, the additional permissions of the preceding version *are not revoked*  . The only way to restrict the add-in to the permissions that the latest version needs, is for a user to open the page *{SharePointDomain}*  `/_layouts/15/appinv.aspx` after the add-in has been updated, and then manually enter permission markup that conforms to the [AppPermissionRequests](http://msdn.microsoft.com/library/4e617622-78d3-3d23-677d-9957eb1fb107%28Office.15%29.aspx) schema.</span></span>
 

 
<span data-ttu-id="e0a80-p124">Если обновленной версии надстройки требуются определенные компоненты, которых не было в предыдущей версии (или отсутствуют компоненты, которые использовались в предыдущей версии), внесите необходимые изменения в раздел надстройки  [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx). В Visual Studio откройте вкладку **Необходимые компоненты** в конструкторе манифеста.</span><span class="sxs-lookup"><span data-stu-id="e0a80-p124">If the updated version of the add-in has prerequisites that the earlier versions did not have (or no longer has some prerequisites that earlier versions had), make changes as needed to the  [AppPrerequisites](http://msdn.microsoft.com/library/7622b55f-01a1-2c39-9daa-7cfb1a3c890f%28Office.15%29.aspx) section of the add-in. In Visual Studio, use the **Prerequisites** tab of the manifest designer.</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="e0a80-222">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0a80-222">Next steps</span></span>
<span data-ttu-id="e0a80-223"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-223"></span></span>

<span data-ttu-id="e0a80-224">Перейдите к следующему пункту раздела [Основные действия при обновлении надстройки](#MajorAppUpgradeSteps) или непосредственно к одной из следующих статей:</span><span class="sxs-lookup"><span data-stu-id="e0a80-224">Continue with the next bullet in the section  [Major steps in updating an add-in](#MajorAppUpgradeSteps) or go directly to one of the following articles:</span></span>
 

 

-  [<span data-ttu-id="e0a80-225">Обновление компонентов сайта надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-225">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="e0a80-226">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-226">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint-2013)
    
 
-  [<span data-ttu-id="e0a80-227">Создание обработчика событий обновления в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-227">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins)
    
 
-  <span data-ttu-id="e0a80-228">[Обновление удаленных компонентов в надстройках SharePoint](update-remote-components-in-sharepoint-add-ins) </span><span class="sxs-lookup"><span data-stu-id="e0a80-228">[Update remote components in SharePoint Add-ins](update-remote-components-in-sharepoint-add-ins)</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="e0a80-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e0a80-229">Additional resources</span></span>
<span data-ttu-id="e0a80-230"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e0a80-230"></span></span>


-  [<span data-ttu-id="e0a80-231">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-231">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="e0a80-232">Процесс обновления надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="e0a80-232">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process)
    
 

