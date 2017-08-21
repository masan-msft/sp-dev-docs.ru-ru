
# <a name="tools-and-environments-for-developing-sharepoint-add-ins"></a><span data-ttu-id="f6cc9-101">Средства и среды для разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6cc9-101">Tools and environments for developing SharePoint Add-ins</span></span>
<span data-ttu-id="f6cc9-102">Узнайте о вариантах создания среды для разработки надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f6cc9-102">Learn your options for creating a development environment for SharePoint Add-ins. There are two basic patterns for development environments for SharePoint Add-ins:</span></span>
 

 <span data-ttu-id="f6cc9-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f6cc9-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="f6cc9-106">Существует два основных шаблона для сред разработки надстроек SharePoint:</span><span class="sxs-lookup"><span data-stu-id="f6cc9-106">Learn your options for creating a development environment for SharePoint Add-ins. There are two basic patterns for development environments for SharePoint Add-ins:</span></span>
 

-  <span data-ttu-id="f6cc9-p102">**Веб-сайт SharePoint для тестирования и отладки включен в веб-сайт SharePoint Online подписки на Office 365.** Обычно Visual Studio устанавливается на локальный компьютер, но можно использовать и облачную версию Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f6cc9-p102">**The test and debugging SharePoint website is in a SharePoint Online website in an Office 365 subscription.** Typically, Visual Studio is installed to a local computer, but a cloud-based Visual Studio is also an option.</span></span>
    
 
-  <span data-ttu-id="f6cc9-p103">**Тестирование и отладка веб-сайта SharePoint выполняются в локальной односерверной ферме SharePoint.** Visual Studio устанавливается на том же компьютере.</span><span class="sxs-lookup"><span data-stu-id="f6cc9-p103">**The test and debugging SharePoint website is on an on-premise, one-server SharePoint farm.** Visual Studio is installed on the same computer.</span></span>
    
 
<span data-ttu-id="f6cc9-111">Примите во внимание следующее:</span><span class="sxs-lookup"><span data-stu-id="f6cc9-111">Consider the following:</span></span>
 

- <span data-ttu-id="f6cc9-p104">Практически любую созданную надстройку можно развернуть в SharePoint Online или на локальных фермах SharePoint, независимо от типа используемой среды. Как правило, надстройки, в SharePoint Online невозможно развернуть те надстройки, которые там невозможно создать. К таким надстройкам могут относиться те, для которых требуются  [разрешения на полный доступ](add-in-permissions-in-sharepoint-2013), или те, которые используют  [систему авторизации с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization).</span><span class="sxs-lookup"><span data-stu-id="f6cc9-p104">Almost any add-in you create can be deployed to either SharePoint Online or to on-premise SharePoint farms, regardless of which type of environment you use. As a general rule, add-ins that cannot be deployed to SharePoint Online also cannot be developed with it. Examples: add-ins that require  [Full Control permissions](add-in-permissions-in-sharepoint-2013) and add-ins that use the [high-trust authorization system](creating-sharepoint-add-ins-that-use-high-trust-authorization).</span></span>
    
 
- <span data-ttu-id="f6cc9-115">Вы можете разрабатывать надстройки, размещаемые как в SharePoint, так и у поставщика, независимо от типа используемой среды.</span><span class="sxs-lookup"><span data-stu-id="f6cc9-115">You can develop both SharePoint-hosted and provider-hosted SharePoint Add-ins, regardless of which type of environment you use.</span></span>
    
 
- <span data-ttu-id="f6cc9-116">У вас могут быть как локальные тестовые сайты, так и тестовые сайты SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="f6cc9-116">You can have both on-premise and SharePoint Online test sites.</span></span>
    
 
- <span data-ttu-id="f6cc9-117">Учитывая все вышеизложенное, можно считать оба варианта одинаково простыми в настройке.</span><span class="sxs-lookup"><span data-stu-id="f6cc9-117">All things considered, the two options are equally easy to set up.</span></span>
    
 
 <span data-ttu-id="f6cc9-118">**Руководство по созданию среды SharePoint Online** с помощью подписки SharePoint Online, которую можно использовать для разработки, см. в статье [Создание сайта разработчика с использованием актуальной подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription).</span><span class="sxs-lookup"><span data-stu-id="f6cc9-118">**To create the SharePoint Online environment** using an SharePoint Online subscription that you can use for development, see [Create a developer site on an existing Office 365 subscription. To create the on-premise environment, see Set up an on-premises development environment for SharePoint Add-ins](create-a-developer-site-on-an-existing-office-365-subscription).</span></span>
 
 <span data-ttu-id="f6cc9-119">**Руководство по созданию локальной среды** см. в статье [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="f6cc9-119">**To create the on-premise environment**, see [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span></span>
 

 <span data-ttu-id="f6cc9-p105">**Примечание.** Эта статья посвящена только средам разработки надстроек SharePoint. Если вы планируете разрабатывать решения для ферм, см. статью [Настройка общей среды разработки для SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). Если вы планируете разрабатывать решения обоих типов, начните с последней статьи, а затем ознакомьтесь с дополнительными указаниями по разработке надстроек SharePoint, описанными в статье [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="f6cc9-p105">**Note** This topic is only concerned with environments for developing SharePoint Add-ins. If you plan to develop farm solutions, see  [Set up a general development environment for SharePoint](http://msdn.microsoft.com/library/08e4e4e1-d960-43fa-85df-f3c279ed6927%28Office.15%29.aspx). If you plan to do both kinds of development, start with the latter article, and then see  [Set up an on-premises development environment for SharePoint Add-ins](set-up-an-on-premises-development-environment-for-sharepoint-add-ins) for additional steps you need to develop SharePoint Add-ins.</span></span>
 


## <a name="other-tooling-information"></a><span data-ttu-id="f6cc9-123">Сведения о других средствах</span><span class="sxs-lookup"><span data-stu-id="f6cc9-123">Other tooling information</span></span>

 
-  [<span data-ttu-id="f6cc9-124">Создание надстроек SharePoint в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6cc9-124">Create SharePoint Add-ins in Visual Studio</span></span>](create-sharepoint-add-ins-in-visual-studio)
    
 

## <a name="additional-resources"></a><span data-ttu-id="f6cc9-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f6cc9-125">Additional resources</span></span>
<span data-ttu-id="f6cc9-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f6cc9-126"></span></span>


-  [<span data-ttu-id="f6cc9-127">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6cc9-127">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 

