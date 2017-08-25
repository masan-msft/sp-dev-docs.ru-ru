# <a name="create-a-developer-site-on-an-existing-office-365-subscription"></a><span data-ttu-id="246db-101">Создание сайта разработчика с использованием существующей подписки на Office 365</span><span class="sxs-lookup"><span data-stu-id="246db-101">Create a developer site on an existing Office 365 subscription</span></span>
<span data-ttu-id="246db-p101">На Сайте разработчика Office 365 можно быстро и просто выполнить настройку и начать создавать, тестировать и развертывать надстройки Office и SharePoint. Во многих подписках Office 365 бизнес, Office 365 корпоративный, Office 365 для образования и Office 365 для государственных организаций имеется шаблон сайта, который вы можете использовать для создания Сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-p101">An Office 365 Developer Site makes it easier to get set up and start creating, testing, and deploying your Office and SharePoint Add-ins more quickly. Many Office 365 Business, Enterprise, Education, and Government subscriptions include a site template you can use to create a Developer Site. Before you start</span></span>
 

 <span data-ttu-id="246db-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="246db-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

 <span data-ttu-id="246db-107">**Перед началом работы**</span><span class="sxs-lookup"><span data-stu-id="246db-107">**Before you start**</span></span>
 

-  <span data-ttu-id="246db-p103">**Убедитесь, что ваша подписка на Office 365 поддерживает Сайт разработчика.** Если у вас есть один из указанных ниже планов подписки на Office 365, можно создать Сайт разработчиков, используя текущую подписку.</span><span class="sxs-lookup"><span data-stu-id="246db-p103">**Be sure you have an Office 365 subscription that supports a Developer Site.** If you have one of the following Office 365 subscription plans, you can create a Developer Site within your existing subscription:</span></span>
    
    - <span data-ttu-id="246db-110">Office 365 для среднего бизнеса.</span><span class="sxs-lookup"><span data-stu-id="246db-110">Office 365 Midsize Business</span></span>
    
 
- <span data-ttu-id="246db-111">Office 365 корпоративный E1, E3, E4, E5 или K1.</span><span class="sxs-lookup"><span data-stu-id="246db-111">Office 365 Enterprise E1, E3, E4, E5, or K1</span></span>
    
 
- <span data-ttu-id="246db-112">Office 365 для образовательных учреждений A2, A3 или A4.</span><span class="sxs-lookup"><span data-stu-id="246db-112">Office 365 Education A2, A3, or A4</span></span>
    
 
- <span data-ttu-id="246db-113">Office 365 для государственных учреждений G1, G3, G4 или K1.</span><span class="sxs-lookup"><span data-stu-id="246db-113">Office 365 Government G1, G3, G4, or K1</span></span>
    
 
-  <span data-ttu-id="246db-p104">**Если у вас есть подписка на Office 365 для малого бизнеса,** она поддерживает только одно семейство веб-сайтов, поэтому невозможно создать семейство Сайта разработчика. Узнать больше о планах Office 365 для своей компании можно в статье [SharePoint Online: ограничения, связанные с программным обеспечением, и пороговые значения](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/sharepoint-online-software-boundaries-and-limits-HA102694293.aspx).</span><span class="sxs-lookup"><span data-stu-id="246db-p104">**If you have an Office 365 Small Business subscription,** it supports only a single site collection, and so you can't create a Developer Site collection. If you would like to learn more about Office 365 plans for your business, see [SharePoint Online: software boundaries and limits](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/sharepoint-online-software-boundaries-and-limits-HA102694293.aspx).</span></span>
    
 
- <span data-ttu-id="246db-116">Дополнительные сведения о подписках на Office 365 корпоративный см. на веб-странице [тарифных планов и цен](http://products.office.com/en-us/business/office-365-enterprise-e1-business-software ).</span><span class="sxs-lookup"><span data-stu-id="246db-116">For more information about the Office 365 Enterprise offerings, see  Plans & Pricing http://products.office.com/en-us/business/office-365-enterprise-e1-business-software  .</span></span>
    
 

## <a name="create-a-developer-site"></a><span data-ttu-id="246db-117">Создание Сайта разработчика</span><span class="sxs-lookup"><span data-stu-id="246db-117">Create a Developer Site</span></span>
<span data-ttu-id="246db-118"><a name="bk_createdevsite"> </a></span><span class="sxs-lookup"><span data-stu-id="246db-118"></span></span>


1. <span data-ttu-id="246db-119">Войдите в Office 365 в качестве глобального администратора или администратора SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="246db-119">Sign in to Office 365 as a Global or SharePoint Online admin.</span></span>
    
     <span data-ttu-id="246db-p105">**Необходимо войти как глобальный администратор или администратор SharePoint Online, чтобы создавать новые семейства веб-сайтов,** например Сайт разработчиков. Только администраторы могут видеть раздел "Администратор" при входе в Office 365. Если вы не администратор, свяжитесь с администратором своей организации и попросите его сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="246db-p105">**You must sign in as a Global or SharePoint Online admin to create new site collections,** such as a Developer Site. Only admins can see Admin options when signing into Office 365. If you're not an admin, contact an admin in your company and have them do one of the following:</span></span>
    
      - <span data-ttu-id="246db-123">Предоставить вам права администратора, чтобы вы могли самостоятельно создать Сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-123">Grant you admin rights, so you can create the Developer Site yourself.</span></span>
    
 
  - <span data-ttu-id="246db-124">Создать Сайт разработчиков и указать вас как администратора семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="246db-124">Create the Developer Site for you, and specify you as an admin for the site collection.</span></span>
    
 
2. <span data-ttu-id="246db-125">Нажмите кнопку средства запуска приложений в дальней левой части панели навигации вверху страницы.</span><span class="sxs-lookup"><span data-stu-id="246db-125">Click the App Launcher button on the far left of the navigation bar at top.</span></span>
    
 
3. <span data-ttu-id="246db-126">Щелкните плитку **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="246db-126">Click the **Admin** tile.</span></span>
    
 
4. <span data-ttu-id="246db-127">В дереве переходов слева разверните раздел **Администратор** и выберите пункт **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="246db-127">In the navigation tree on the left, expand **Admin**, and select **SharePoint**.</span></span>
    
 
5. <span data-ttu-id="246db-128">В **Центре администрирования SharePoint** на вкладке **Семейства веб-сайтов** щелкните **Создать > Частное семейство веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="246db-128">In the **SharePoint admin center**, on the **Site Collections** tab, click **New > Private Site Collection**.</span></span>
    
  ![Пункт создания семейства веб-сайтов в Центре администрирования SharePoint](../../images/SPAdminCenter_newSiteCollection.png)
 

 

 
6. <span data-ttu-id="246db-130">В диалоговом окне **Создание семейства веб-сайтов** укажите сведения о своем Сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-130">In the **New Site Collection** dialog box, provide information about your Developer Site.</span></span>
    
|<span data-ttu-id="246db-131">**Поле**</span><span class="sxs-lookup"><span data-stu-id="246db-131">**Field**</span></span>|<span data-ttu-id="246db-132">**Значение**</span><span class="sxs-lookup"><span data-stu-id="246db-132">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="246db-133">**Название**</span><span class="sxs-lookup"><span data-stu-id="246db-133">**Title**</span></span>|<span data-ttu-id="246db-134">Название, которое вы собираетесь присвоить своему Сайту разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-134">The name you want to give your Developer Site.</span></span>|
|<span data-ttu-id="246db-135">Список **Адрес общедоступного веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="246db-135">**Public Website Address** list</span></span>|<span data-ttu-id="246db-136">Укажите доменное имя и URL-путь (**/sites/** или **/teams/**), а затем введите URL-имя семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="246db-136">A domain name and a URL path—either **/sites/** or **/teams/**—and then type a URL name for the site collection.</span></span>|
|<span data-ttu-id="246db-137">Список **Выберите язык** в разделе **Выбор шаблона**</span><span class="sxs-lookup"><span data-stu-id="246db-137">**Select a language** list in the **Template Selection** section</span></span>|<span data-ttu-id="246db-p106">Основной язык для вашего Сайта разработчика. **Выберите правильный язык для семейства веб-сайтов Сайта разработчика, так как после выбора языка вы не сможете его изменить.** Выбор языка для Сайта разработчика не влияет на перечень языков, которые можно сделать доступными в ваших надстройках Office и SharePoint. Вы можете включить многоязычный интерфейс SharePoint на своих сайтах, но основным языком для семейства веб-сайтов будет тот язык, который вы выберете здесь.</span><span class="sxs-lookup"><span data-stu-id="246db-p106">A primary language to use for your Developer Site. **Be sure to select the appropriate language for the Developer Site site collection, because once you choose it, it can't be changed.**Selecting a language for your Developer Site does not affect the languages you can make available in your Office and SharePoint Add-ins.You can enable the SharePoint multiple language interface on your sites, but the primary language for the site collection is the one you choose here.</span></span>|
|<span data-ttu-id="246db-140">Вкладка **Совместная работа** в подразделе **Выберите шаблон** раздела **Выбор шаблона**</span><span class="sxs-lookup"><span data-stu-id="246db-140">**Template Selection** section, on the **Collaboration** tab under **Select a template**</span></span>|<span data-ttu-id="246db-141">Выберите **Сайт разработчика**.</span><span class="sxs-lookup"><span data-stu-id="246db-141">Choose **Developer Site.**</span></span>|
|<span data-ttu-id="246db-142">**Часовой пояс**</span><span class="sxs-lookup"><span data-stu-id="246db-142">**Time Zone**</span></span>|<span data-ttu-id="246db-143">Часовой пояс, который соответствует локали вашего Сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-143">Time zone that's appropriate for the locale of your Developer Site.</span></span>|
|<span data-ttu-id="246db-144">**Администратор**</span><span class="sxs-lookup"><span data-stu-id="246db-144">**Administrator**</span></span>|<span data-ttu-id="246db-145">Имя пользователя администратора вашего семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="246db-145">The user name of your site collection administrator.</span></span>|
|<span data-ttu-id="246db-146">**Квота хранилища**</span><span class="sxs-lookup"><span data-stu-id="246db-146">**Storage Quota**</span></span>|<span data-ttu-id="246db-147">Место в мегабайтах (МБ), которое вы хотите выделить для этого семейства веб-сайтов Сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-147">Number of megabytes (MB) you want to allocate to this Developer Site site collection.</span></span>|
|<span data-ttu-id="246db-148">**Квота ресурсов сервера**</span><span class="sxs-lookup"><span data-stu-id="246db-148">**Server Resource Quota**</span></span>|<span data-ttu-id="246db-p107">Количество ресурсов, которые необходимо выделить для семейства веб-сайтов. Это значение объединяет в себе метрики производительности (например, загруженность процессора и необработанные исключения), относящиеся к коду в изолированных решениях. Если указанный уровень превышает дневную квоту, песочница для этого семейства веб-сайтов будет отключена.</span><span class="sxs-lookup"><span data-stu-id="246db-p107">This number is a combination of performance metrics (such as processor time and unhandled exceptions) that pertain to code in sandboxed solutions. When the level exceeds a daily quota, the sandbox is turned off for this site collection.</span></span>|
7. <span data-ttu-id="246db-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="246db-152">Click **OK**.</span></span>
    
    <span data-ttu-id="246db-p108">URL-адрес нового Сайта разработчика отобразится в списке **Семейства веб-сайтов**. По завершении создания сайта вы сможете перейти по этому URL-адресу и открыть свой Сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="246db-p108">You'll see the new developer site URL in the **Site Collections** list. When the site creation is finished, you can navigate to the URL to open your Developer Site.</span></span>
    
  ![Подготовка нового семейства веб-сайтов](../../images/SPAdminCenter_newSiteCollection_provisioning.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="246db-156">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="246db-156">Additional resources</span></span>
<span data-ttu-id="246db-157"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="246db-157"></span></span>


-  [<span data-ttu-id="246db-158">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="246db-158">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="246db-159">Создание и удаление семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="246db-159">Create or delete a site collection</span></span>](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/create-or-delete-a-site-collection-HA102772354.aspx?CTT=1)
    
 

