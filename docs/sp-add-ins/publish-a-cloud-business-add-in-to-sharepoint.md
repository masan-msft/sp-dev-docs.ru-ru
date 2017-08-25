
# <a name="publish-a-cloud-business-add-in-to-sharepoint"></a><span data-ttu-id="b93fe-101">Публикация облачной бизнес-надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b93fe-101">Publish a cloud business add-in to SharePoint</span></span>
<span data-ttu-id="b93fe-p101">Вы можете опубликовать свою облачную бизнес-надстройку как надстройку для SharePoint с размещением у поставщика. Используя такой тип надстроек, вы сможете гибко развертывать свое веб-приложение и базу данных в локальном сайте SharePoint, Microsoft Azure или на стороннем сайте размещения. После того как вы опубликуете надстройку, другие люди смогут запускать ее из SharePoint на своих компьютерах и мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="b93fe-p101">You can publish your cloud business add-in as a provider-hosted SharePoint add-in. A provider-hosted add-in gives you the flexibility of deploying your web app and database to an on-premise SharePoint site, to Microsoft Azure, or to a third-party hosting site. After you publish your add-in, others can run it from SharePoint on their computers and mobile devices.</span></span>
 
<span data-ttu-id="b93fe-105">Вы можете опубликовать свою надстройку прямо на сайте, используя WebDeploy, или создать для нее пакет, который можно развертывать на многочисленных серверах.</span><span class="sxs-lookup"><span data-stu-id="b93fe-105">You can publish your add-in directly to a site using WebDeploy, or you can create a package for your add-in that can be deployed to multiple servers.</span></span>
 

 <span data-ttu-id="b93fe-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b93fe-p102">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="to-publish-an-add-in"></a><span data-ttu-id="b93fe-109">Публикация надстройки</span><span class="sxs-lookup"><span data-stu-id="b93fe-109">To publish an add-in</span></span>
<span data-ttu-id="b93fe-110"><a name="publish"> </a></span><span class="sxs-lookup"><span data-stu-id="b93fe-110"></span></span>


1. <span data-ttu-id="b93fe-111">В **обозревателе решений** откройте контекстное меню для узла приложения верхнего уровня, как показано на рисунке 1, а затем выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-111">In **Solution Explorer**, open the shortcut menu for the top-level application node as shown in Figure 1, and then choose **Publish**.</span></span>
    
    <span data-ttu-id="b93fe-112">**Рис. 1. Узел верхнего уровня**</span><span class="sxs-lookup"><span data-stu-id="b93fe-112">**Figure 1. The top-level node**</span></span>

 

  ![Узел IncidentManager](../../images/CBA_IM_18.PNG)
 

 

 
2. <span data-ttu-id="b93fe-114">На странице **Параметры SharePoint** мастера публикации приложений LightSwitch выберите переключатель **Размещение у поставщика**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-114">In the LightSwitch Publish Application Wizard, on the **SharePoint Options** page, choose the **Provider-hosted** option button, and then choose **Next**.</span></span>
    
 
3. <span data-ttu-id="b93fe-115">На странице **Конфигурация сервера приложений** выберите переключатель **Сервер IIS** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-115">On the **Application Server Configuration** page, choose the **IIS Server** option button, and then choose **Next**.</span></span>
    
     <span data-ttu-id="b93fe-p103">**Примечание.** Если у вас есть файл параметров публикации (PUBLISHSETTINGS или PUBXML), созданный для другой надстройки, то с его помощью вы можете предоставить остальные сведения, необходимые для публикации. В таком случае нажмите в мастере кнопку **Параметры импорта**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-p103">**Note** If you have a publish settings (.publishsettings or .pubxml) file that was created for another add-in, you can use that file to provide the rest of the information that you need for publishing. If so, choose the **Import Settings** button in the wizard.</span></span>
4. <span data-ttu-id="b93fe-118">На странице **Выходные данные публикации** выберите переключатель **Опубликовать непосредственно на сервере** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-118">On the **Publish Output** page, choose the **Publish directly to a server now** option button, and then choose **Next**.</span></span>
    
 
5. <span data-ttu-id="b93fe-119">На странице **Параметры публикации** в текстовом поле **URL-адрес службы** введите URL-адрес сервера, на котором вы хотите опубликовать свою надстройку.</span><span class="sxs-lookup"><span data-stu-id="b93fe-119">On the **Publish Settings** page, in the **Service URL** text box, enter the URL for the server where you want to publish your add-in.</span></span>
    
    <span data-ttu-id="b93fe-p104">При публикации у компании-поставщика услуг размещения, это значение должна предоставить компания. Оно может быть представлено в одном из следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="b93fe-p104">If you're publishing to a hosting company, the company provides this value. It can be in any of the following formats:</span></span>
    
      -  <span data-ttu-id="b93fe-122">_URL-адрес_поставщика_ (например, `contoso.com`);</span><span class="sxs-lookup"><span data-stu-id="b93fe-122">_HostingCompanyURL_ (for example, `contoso.com`)</span></span>
    
 
  -  <span data-ttu-id="b93fe-123">`https://` _URL-адрес_поставщика_ (например, `https://contoso.com`);</span><span class="sxs-lookup"><span data-stu-id="b93fe-123">`https://` _HostingCompanyURL_ (for example, `https://contoso.com`)</span></span>
    
 
  -  <span data-ttu-id="b93fe-124">`https://` _URL-адрес_поставщика_ `:8172/msdeploy.axd` (например, `https://contoso.com:8172/msdeploy.axd`).</span><span class="sxs-lookup"><span data-stu-id="b93fe-124">`https://` _HostingCompanyURL_ `:8172/msdeploy.axd` (for example, `https://contoso.com:8172/msdeploy.axd`)</span></span>
    
 

    <span data-ttu-id="b93fe-125">При публикации в службах IIS на собственном компьютере для тестирования укажите значение `localhost` или имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="b93fe-125">If you're publishing to Internet Information Services (IIS) on your own computer for testing, enter  `localhost` or the name of your computer.</span></span>
    
    <span data-ttu-id="b93fe-126">При публикации на сервере в собственной сети укажите один из следующих URL-адресов:</span><span class="sxs-lookup"><span data-stu-id="b93fe-126">If you're publishing to a server on your own network, enter one of these URLs:</span></span>
    
      -  <span data-ttu-id="b93fe-127">`http://` _Имя_сервера_</span><span class="sxs-lookup"><span data-stu-id="b93fe-127">`http://` _servername_</span></span>
    
 
  -  <span data-ttu-id="b93fe-128">`http://` _Имя_сервера_ `/msdeployagentservice`</span><span class="sxs-lookup"><span data-stu-id="b93fe-128">`http://` _servername_ `/msdeployagentservice`</span></span>
    
 

     <span data-ttu-id="b93fe-129">**Примечание.** В случае публикации через брандмауэр вам может потребоваться открыть порт 8172.</span><span class="sxs-lookup"><span data-stu-id="b93fe-129">**Note** If you're publishing through a firewall, you might have to open port 8172.</span></span>
6. <span data-ttu-id="b93fe-130">В текстовом поле **Сайт или приложение** введите имена веб-сайта IIS и вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="b93fe-130">In the **Site/application** text box, enter the names of the IIS website and your add-in.</span></span>
    
    <span data-ttu-id="b93fe-p105">В случае публикации на сервере компании по размещению веб-сайтов она предоставит вам это значение. Обычно оно представляет собой доменное имя (например,  `contoso.com`) или доменное имя и имя надстройки (например,  `contoso.com/MyApp`).</span><span class="sxs-lookup"><span data-stu-id="b93fe-p105">If you're publishing to a hosting company, the company provides this value. It's typically either a domain name (for example,  `contoso.com`) or a domain and add-in name (for example,  `contoso.com/MyApp`).</span></span>
    
    <span data-ttu-id="b93fe-p106">В случае тестовой публикации в службы IIS на своем компьютере или публикации на сервере в своей внутренней сети введите имя сайта и надстройки, которые отображаются в диспетчере IIS. Например, если вы публикуете надстройку MyApp на веб-сайте по умолчанию в службах IIS, введите Веб-сайт по умолчанию/MyApp.</span><span class="sxs-lookup"><span data-stu-id="b93fe-p106">If you're publishing to IIS on your own computer for testing, or you're publishing to a server on your internal network, enter the site and add-in name as they appear in IIS Manager. For example, if you're publishing the add-in MyApp to the default website in IIS, enter Default Web Site/MyApp.</span></span>
    
     <span data-ttu-id="b93fe-135">**Примечание.** Если вы публикуете приложение в существующей веб-папке и хотите удалить какое-либо имеющееся содержимое, установите флажок **Удалять дополнительные файлы в месте назначения**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-135">**Note** If you're publishing to an existing web folder and want to remove any existing content, select the **Remove additional files at destination** check box.</span></span>
7. <span data-ttu-id="b93fe-136">В текстовых полях **Имя пользователя** и **Пароль** укажите данные учетной записи, имеющей достаточные полномочия для выполнения задач развертывания на целевом веб-сервере, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-136">In the **User Name** and **Password** text boxes, enter credentials for an account that has sufficient authority to perform deployment tasks on the destination web server, and then choose **Next**.</span></span>
    
    <span data-ttu-id="b93fe-137">При публикации у поставщика услуг размещения эти значения предоставляет поставщик.</span><span class="sxs-lookup"><span data-stu-id="b93fe-137">If you're publishing to a hosting company, the company provides these values.</span></span>
    
 
8. <span data-ttu-id="b93fe-138">На странице **Параметры безопасности** выберите переключатель **Да, пользователи должны подключаться по HTTPS** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-138">On the **Security Settings** page, choose the **Yes, users must connect using HTTPS** option button, and then choose **Next**.</span></span>
    
 
9. <span data-ttu-id="b93fe-139">На странице **Подключения данных** на вкладке **Подключения к базам данных** введите строки подключения администратора и пользователя для сервера базы данных, на котором вы хотите опубликовать базу данных своей надстройки.</span><span class="sxs-lookup"><span data-stu-id="b93fe-139">On the **Data connections** page, on the **Database Connections** tab, enter the administrator and user connection strings for the database server where you want to publish your add-in's database.</span></span>
    
     <span data-ttu-id="b93fe-140">**Примечание.** База данных не обязательно должна находиться на сервере, на котором вы публикуете надстройку.</span><span class="sxs-lookup"><span data-stu-id="b93fe-140">**Note** The database doesn't have to be located on the server where you are publishing the add-in.</span></span>
10. <span data-ttu-id="b93fe-141">На вкладке **Подключенные источники данных** по мере необходимости измените строки всех дополнительных подключений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-141">On the **Attached Data Sources** tab, update the connection strings for any additional connections as needed, and then choose **Next**.</span></span>
    
 
11. <span data-ttu-id="b93fe-142">На странице **Размещение у поставщика** укажите полный URL-адрес своей надстройки в текстовом поле **Где размещается приложение LightSwitch**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-142">On the **Provider Hosting** page, in the **Where is your LightSwitch application hosted** text box, enter the full URL for your add-in.</span></span>
    
    <span data-ttu-id="b93fe-143">В большинстве случаев этот URL-адрес будет совпадать с указанными ранее значениями **URL-адрес службы** и **Сайт или приложение** (например, `https://contoso.com/MyApplication`).</span><span class="sxs-lookup"><span data-stu-id="b93fe-143">In most cases this URL will be the same as the **Service URL** and **Site/application** values that you entered earlier (for example `https://contoso.com/MyApplication`).</span></span>
    
 
12. <span data-ttu-id="b93fe-144">Укажите **идентификатор клиента** и **секрет клиента** для своей надстройки.</span><span class="sxs-lookup"><span data-stu-id="b93fe-144">Enter the **Client ID** and **Client Secret** values for your add-in.</span></span>
    
    <span data-ttu-id="b93fe-p107">Вы можете получить эти значения на странице **appregnew** сайта SharePoint или Панели мониторинга продаж. См. статью [Регистрация надстроек для SharePoint 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b93fe-p107">You can get these values from the **appregnew** page of your SharePoint site or from the Seller dashboard. See [Guidelines for registering SharePoint Add-ins 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span></span>
    
 
13. <span data-ttu-id="b93fe-147">Нажмите кнопку **Опубликовать**, чтобы опубликовать надстройку.</span><span class="sxs-lookup"><span data-stu-id="b93fe-147">Choose **Publish** to publish your add-in.</span></span>
    
    <span data-ttu-id="b93fe-148">Когда надстройка будет опубликована, откроется **проводник** с каталогом **Publish** для проекта.</span><span class="sxs-lookup"><span data-stu-id="b93fe-148">When your add-in is published, **File Explorer** opens and displays the **Publish** directory for your project.</span></span>
    
 

## <a name="to-package-an-add-in"></a><span data-ttu-id="b93fe-149">Упаковка надстройки</span><span class="sxs-lookup"><span data-stu-id="b93fe-149">To package an add-in</span></span>
<span data-ttu-id="b93fe-150"><a name="package"> </a></span><span class="sxs-lookup"><span data-stu-id="b93fe-150"></span></span>


1. <span data-ttu-id="b93fe-151">В **обозревателе решений** откройте контекстное меню для узла приложения верхнего уровня, как показано на рисунке 1, а затем выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-151">In **Solution Explorer**, open the shortcut menu for the top-level application node as shown in Figure 1, and then choose **Publish**.</span></span>
    
    <span data-ttu-id="b93fe-152">**Рис. 1. Узел верхнего уровня**</span><span class="sxs-lookup"><span data-stu-id="b93fe-152">**Figure 1. The top-level node**</span></span>

 

  ![Узел IncidentManager](../../images/CBA_IM_18.PNG)
 

    
    
 
2. <span data-ttu-id="b93fe-154">На странице **Параметры SharePoint** мастера публикации приложений LightSwitch выберите переключатель **Размещение у поставщика**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-154">In the LightSwitch Publish Application Wizard, on the **SharePoint Options** page, choose the **Provider-hosted** option button, and then choose **Next**.</span></span>
    
 
3. <span data-ttu-id="b93fe-155">На странице **Конфигурация сервера приложений** выберите переключатель **Сервер IIS** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-155">On the **Application Server Configuration** page, choose the **IIS Server** option button, and then choose **Next**.</span></span>
    
     <span data-ttu-id="b93fe-p108">**Примечание.** Если у вас есть файл параметров публикации (PUBLISHSETTINGS или PUBXML), созданный для другой надстройки, то с его помощью вы можете предоставить остальные сведения, необходимые для публикации. В таком случае нажмите в мастере кнопку **Параметры импорта**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-p108">**Note** If you have a publish settings (.publishsettings or .pubxml) file that was created for another add-in, you can use that file to provide the rest of the information that you need for publishing. If so, choose the **Import Settings** button in the wizard.</span></span>
4. <span data-ttu-id="b93fe-158">На странице **Выходные данные публикации** выберите переключатель **Создать пакет на диске** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-158">On the **Publish Output** page, choose the **Create a package on disk** option button, and then choose **Next**.</span></span>
    
 
5. <span data-ttu-id="b93fe-159">На странице **Параметры публикации** укажите имя сайта в текстовом поле **Как должен быть назван веб-сайт?**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-159">On the **Publish Settings** page, in the **What should the website be named?** text box, enter a name for the website.</span></span>
    
    <span data-ttu-id="b93fe-160">По умолчанию задано имя надстройки.</span><span class="sxs-lookup"><span data-stu-id="b93fe-160">The default name is the add-in name.</span></span>
    
 
6. <span data-ttu-id="b93fe-161">В текстовом поле **Где должен быть создан пакет?** введите путь к расположению, где требуется опубликовать выходные данные, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-161">In the **Where should the package be created?** text box, enter the path for the location where you want the output to be published, and then choose **Next**.</span></span>
    
    <span data-ttu-id="b93fe-162">По умолчанию используется подкаталог Publish каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="b93fe-162">The default location is the Publish subdirectory under your project directory.</span></span>
    
 
7. <span data-ttu-id="b93fe-163">На странице **Параметры безопасности** выберите переключатель **Да, пользователи должны подключаться по HTTPS** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-163">On the **Security Settings** page, choose the **Yes, users must connect using HTTPS** option button, and then choose **Next**.</span></span>
    
 
8. <span data-ttu-id="b93fe-164">На странице **Конфигурация базы данных** выберите переключатель **Создать новую базу данных** и введите имя своей надстройки в качестве имени базы данных.</span><span class="sxs-lookup"><span data-stu-id="b93fe-164">On the **Database Configuration** page, choose the **Generate a new database called** option button and enter your add-in's name as the database name.</span></span>
    
 
9. <span data-ttu-id="b93fe-165">Выберите вкладку **Подключенные источники данных** и по мере необходимости измените строки всех дополнительных подключений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-165">Choose the **Attached Data Sources** tab and update the connection strings for any additional connections as needed, and then choose **Next**.</span></span>
    
 
10. <span data-ttu-id="b93fe-166">На странице **Размещение у поставщика** укажите полный URL-адрес своей надстройки в текстовом поле **Где размещается приложение LightSwitch**.</span><span class="sxs-lookup"><span data-stu-id="b93fe-166">On the **Provider Hosting** page, in the **Where is your LightSwitch application hosted** text box, enter the full URL for your add-in.</span></span>
    
    <span data-ttu-id="b93fe-167">В большинстве случаев этот URL-адрес будет совпадать с указанными ранее значениями **URL-адрес службы** и **Сайт или приложение** (например, `https://contoso.com/MyApplication`).</span><span class="sxs-lookup"><span data-stu-id="b93fe-167">In most cases this URL will be the same as the **Service URL** and **Site/application** values that you entered earlier (for example `https://contoso.com/MyApplication`).</span></span>
    
 
11. <span data-ttu-id="b93fe-168">Введите **идентификатор клиента** и **секрет клиента** для надстройки.</span><span class="sxs-lookup"><span data-stu-id="b93fe-168">Enter the **Client ID** and **Client Secret** for your add-in.</span></span>
    
    <span data-ttu-id="b93fe-p109">Вы можете получить эти значения на странице **appregnew** сайта SharePoint или Панели мониторинга продаж. См. статью [Регистрация надстроек для SharePoint 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b93fe-p109">You can get these values from the **appregnew** page of your SharePoint site or from the Seller dashboard. See [Guidelines for registering SharePoint Add-ins 2013](http://msdn.microsoft.com/en-us/library/office/jj687469%28v=office.15%29.aspx).</span></span>
    
 
12. <span data-ttu-id="b93fe-171">Нажмите кнопку **Опубликовать**, чтобы опубликовать надстройку.</span><span class="sxs-lookup"><span data-stu-id="b93fe-171">Choose **Publish** to publish your add-in.</span></span>
    
    <span data-ttu-id="b93fe-p110">Когда ваша надстройка будет опубликована, файл ZIP с пакетом помещается в каталог, который вы указали на этапе 4. После создания этого пакета администратор сервера сможет с помощью средства MSDeploy развернуть вашу надстройку на серверах, на которых запущены службы IIS и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b93fe-p110">When your add-in is published, a .zip file that contains the package is placed in the directory that you specified in step 4. After this package has been created, a server administrator can use the MSDeploy tool to deploy your add-in to servers that are running IIS and SQL Server.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="b93fe-174">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b93fe-174">Additional resources</span></span>
<span data-ttu-id="b93fe-175"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b93fe-175"></span></span>


-  [<span data-ttu-id="b93fe-176">Регистрация надстроек SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="b93fe-176">Register SharePoint Add-ins 2013</span></span>](register-sharepoint-add-ins-2013)
    
 
-  [<span data-ttu-id="b93fe-177">Публикация облачных бизнес-надстроек</span><span class="sxs-lookup"><span data-stu-id="b93fe-177">Publish cloud business add-ins</span></span>](publish-cloud-business-add-ins)
    
 

