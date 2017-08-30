# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="d569e-101">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d569e-101">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>
<span data-ttu-id="d569e-102">Узнайте, как настроить среду разработки и создать свою первую надстройку SharePoint с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d569e-102">Set up a development environment and create your first SharePoint-hosted spappsing.</span></span>
 

 <span data-ttu-id="d569e-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="d569e-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="d569e-p102">Надстройки с размещением в SharePoint — это один из двух основных типов надстроек SharePoint. Обзор надстроек SharePoint и этих основных типов см. в статье [Надстройки SharePoint](sharepoint-add-ins). Ниже представлен обзор надстроек с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d569e-p102">Set up a development environment and create your first SharePoint-hosted SharePoint Add-in. SharePoint-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see  [SharePoint Add-ins](sharepoint-add-ins). Here's a summary of SharePoint-hosted add-ins:</span></span>
 

- <span data-ttu-id="d569e-109">Они содержат списки SharePoint, веб-части, рабочие процессы, пользовательские страницы и другие компоненты, каждый из которых установлен на дочернем сайте (сайте надстройки) того веб-сайта SharePoint, на котором установлена надстройка.</span><span class="sxs-lookup"><span data-stu-id="d569e-109">They contain SharePoint lists, Web Parts, workflows, custom pages, and other components, all of which are installed on a subweb, called the add-in web, of the SharePoint website where the add-in is installed.</span></span>
    
 
- <span data-ttu-id="d569e-110">Единственный код, который они содержат, — JavaScript пользовательских страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d569e-110">The only code they have is JavaScript on custom SharePoint pages.</span></span>
    
 
- [<span data-ttu-id="d569e-111">Этап 1. Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="d569e-111">Step 1 Set up your dev environment</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#Setup) 

- [<span data-ttu-id="d569e-112">Этап 2. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="d569e-112">Step 2 Create the app project</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#Create) 

- [<span data-ttu-id="d569e-113">Этап 3. Написание кода приложения</span><span class="sxs-lookup"><span data-stu-id="d569e-113">Step 3 Code your app</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins#Code)
 

## <a name="set-up-your-dev-environment"></a><span data-ttu-id="d569e-114">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="d569e-114">Set up your dev environment</span></span>
<span data-ttu-id="d569e-115"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="d569e-115"></span></span>

<span data-ttu-id="d569e-p103">Существует множество способов настройки среды разработки для Надстройки SharePoint. Здесь приведен самый простой способ. Остальные см. в разделе  [Дополнительные ресурсы](#bk_addresources).</span><span class="sxs-lookup"><span data-stu-id="d569e-p103">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way. For alternatives, see  [Additional Resources](#bk_addresources).</span></span>
 

 

### <a name="get-the-tools"></a><span data-ttu-id="d569e-119">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="d569e-119">Get the tools</span></span>


- <span data-ttu-id="d569e-p104">Если у вас еще не установлена среда **Visual Studio** 2013 или более поздней версии, установите ее, следуя инструкциям на странице [Установка Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="d569e-p104">If you don't already have **Visual Studio** 2013 or later installed, install it using the instructions at [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). We recommend using the  [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
    
 
- <span data-ttu-id="d569e-p105">В состав Visual Studio входят **Инструменты разработчика Microsoft Office для Visual Studio**. Иногда выпуск новой версии инструментов не совпадает с выходом обновлений Visual Studio. Чтобы убедиться, что у вас установлена последняя версия инструментов, запустите [установщик Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [установщик Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="d569e-p105">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**. Sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 
    
 

### <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="d569e-125">Получение Сайта разработчика для Office 365</span><span class="sxs-lookup"><span data-stu-id="d569e-125">Sign up for an Office 365 Developer Site</span></span>
<span data-ttu-id="d569e-126"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="d569e-126"></span></span>


 <span data-ttu-id="d569e-p106">**Примечание.** Возможно, у вас уже есть доступ к Сайту разработчика для Office 365. **Вы являетесь подписчиком MSDN?** Visual Studio Ultimate и Visual Studio Premium с подпиской на MSDN включают бесплатную подписку разработчика приложений для Office 365. [Воспользуйтесь этим преимуществом прямо сегодня.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **У вас есть один из указанных ниже планов подписки на Office 365?** **В этом случае администратор подписки на Office 365 может создать Сайт разработчика, ** используя [Центр администрирования Office 365](https://portal.microsoftonline.com/admin/default.aspx). Дополнительные сведения см. в статье [Создание сайта разработчика для существующей подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription).</span><span class="sxs-lookup"><span data-stu-id="d569e-p106">**Note**   You might already have access to an Office 365 Developer Site. **Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Do you have one of the following Office 365 subscription plans?** **If so, an administrator of the Office 365 subscription can create a Developer Site** by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx). For more info, see  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription).</span></span> 
 

<span data-ttu-id="d569e-134">Получить план Office 365 можно тремя способами.</span><span class="sxs-lookup"><span data-stu-id="d569e-134">There are three ways to get an Office 365 plan.</span></span> 
 

 

- <span data-ttu-id="d569e-p107">Бесплатно зарегистрируйте учетную запись разработчика Office 365 через программу для разработчиков Office 365 сроком на один год.  [Узнайте больше на сайте программы ](http://dev.office.com/devprogram) или заполните [форму регистрации](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). После регистрации в программе для разработчиков вы получите сообщение электронной почты со ссылкой для входа в учетную запись разработчика. Затем следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="d569e-p107">Sign up for a free, one year Office 365 developer account through the Office 365 Developer Program.  [Get more information](http://dev.office.com/devprogram), or go straight to  [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). You'll get an e-mail after you sign up for the developer program with a link to sign up for the developer account. Use the instructions below.</span></span>
    
 
- <span data-ttu-id="d569e-139">Начните с [бесплатной 30-дневной пробной версии](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) с лицензией для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="d569e-139">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>
    
 
- <span data-ttu-id="d569e-140">Приобретите [подписку разработчика приложений для Office 365](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="d569e-140">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 
    
 

 <span data-ttu-id="d569e-141">**Совет.** Откройте эти ссылки в новом окне или на новой вкладке, чтобы работать с ними было удобнее.</span><span class="sxs-lookup"><span data-stu-id="d569e-141">**TIP** Open these links in another window or tab in order to keep the following instructions handy.</span></span>
 


<span data-ttu-id="d569e-142">**Рис. 1. Доменное имя Сайта разработчика Office 365**</span><span class="sxs-lookup"><span data-stu-id="d569e-142">**Figure 1. Office 365 Developer Site domain name**</span></span>

 

 
![Страница 2 регистрационной формы для учетной записи Office 365](../../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. <span data-ttu-id="d569e-144">Первая страница (не показана) регистрационной формы не требует объяснений. Укажите нужные сведения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d569e-144">The first page (not shown) of the signup form is self-explanatory; supply the requested information and then choose **Next**.</span></span>
    
 
2. <span data-ttu-id="d569e-145">На второй странице (рис. 1) укажите ИД администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="d569e-145">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
 
3. <span data-ttu-id="d569e-146">Создайте поддомен **.onmicrosoft.com**, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d569e-146">Create a subdomain of **.onmicrosoft.com**; for example, contoso.onmicrosoft.com.</span></span>
    
    <span data-ttu-id="d569e-p108">После регистрации необходимо использовать полученные учетные данные (в формате _ИД_пользователя_@ _ваш_домен_.onmicrosoft.com) для входа на сайт портала Office 365, используемый для администрирования учетной записи. Сайт разработчика для SharePoint Online будет установлен на новом домене: **http:// _ваш_домен_.sharepoint.com**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p108">After signup, you use the resulting credentials (in the format UserID@yourdomain.onmicrosoft.com) to sign in to your off365short portal site where you administer your account. Your sposhort Developer Site is set up  at your new domain: http://yourdomain.sharepoint.com.</span></span>
    
 
4. <span data-ttu-id="d569e-p109">Нажмите кнопку **Далее** и заполните последнюю страницу формы. Если вы хотите указать номер телефона, чтобы получить код подтверждения, можно ввести номер мобильного или стационарного телефона, но *не* номер VoIP.</span><span class="sxs-lookup"><span data-stu-id="d569e-p109">Choose **Next** and fill out the final page of the form. If you choose to provide a telephone number to get a confirmation code, you can provide a mobile or landline number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
 

    
 <span data-ttu-id="d569e-p110">**Примечание.** Если при попытке зарегистрировать учетную запись разработчика выполнен вход в другую учетную запись Майкрософт, может появиться следующее сообщение: "Введен неправильный ИД пользователя. Возможно, он недействителен. Убедитесь, что вы вводите ИД пользователя, назначенный вам организацией. Он должен выглядеть так: *proverka@example.com* или *proverka@example.onmicrosoft.com*". Если появляется такое сообщение, выйдите из текущей учетной записи Майкрософт и повторите попытку. Если сообщение продолжает появляться, очистите кэш браузера или выберите режим **Просмотр InPrivate**, а затем заполните форму.</span><span class="sxs-lookup"><span data-stu-id="d569e-p110">**Note**  If you're logged on to another Microsoft account when you try to sign up for a developer account, you might see this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  *someone@example.com*  or *someone@example.onmicrosoft.com*  ."If you see that message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to  **InPrivate Browsing** and then fill out the form.</span></span>
 

<span data-ttu-id="d569e-p111">По завершении регистрации в браузере откроется страница установки Office 365. Щелкните значок администратора, чтобы открыть страницу Центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="d569e-p111">After you finish the signup process, your browser opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span>
 

 

<span data-ttu-id="d569e-158">**Рис. 2. Страница Центра администрирования Office 365**</span><span class="sxs-lookup"><span data-stu-id="d569e-158">**Figure 2. Office 365 admin center page**</span></span>

 

 
![Снимок экрана с изображением Центра администрирования Office 365.](../../images/SP15_Office365AdminInset_border.png)
 

 

1. <span data-ttu-id="d569e-p112">Подождите, пока завершится настройка Сайта разработчика. После этого обновите страницу центра администрирования в браузере.</span><span class="sxs-lookup"><span data-stu-id="d569e-p112">Wait for your Developer Site to finish setting up. After provisioning is complete, refresh the admin center page in your browser.</span></span>
    
 
2. <span data-ttu-id="d569e-p113">Затем перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть Сайт разработчика. Должен открыться сайт, показанный на рис. 3. На странице отображается список **Тестируемые надстройки**, подтверждающий, что веб-сайт был создан с помощью шаблона Сайта разработчика SharePoint. Если вместо него вы видите обычный сайт группы, подождите несколько минут и откройте сайт заново.</span><span class="sxs-lookup"><span data-stu-id="d569e-p113">Then, choose the **Build Add-ins** link in the upper left corner of the page to open your Developer Site. You should see a site that looks like the one in Figure 3. The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template. If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>
    
 
3. <span data-ttu-id="d569e-166">Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d569e-166">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
 

<span data-ttu-id="d569e-167">**Рис. 3. Домашняя страница Сайта разработчика со списком "Тестируемые надстройки"**</span><span class="sxs-lookup"><span data-stu-id="d569e-167">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

 

 
![Снимок экрана с изображением домашней страницы Сайта разработчика.](../../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="create-the-add-in-project"></a><span data-ttu-id="d569e-169">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="d569e-169">Create the add-in project</span></span>
<span data-ttu-id="d569e-170"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="d569e-170"></span></span>


1. <span data-ttu-id="d569e-171">Запустите Visual Studio, выбрав команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="d569e-171">Start Visual Studio using the **Run as administrator** option.</span></span>
    
 
2. <span data-ttu-id="d569e-172">Последовательно выберите элементы **Файл** > **Создать** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="d569e-172">Choose **File** > **New** > **New Project**.</span></span>
    
 
3. <span data-ttu-id="d569e-173">В диалоговом окне **Новый проект** последовательно разверните узлы **Visual C#** и **Office/SharePoint**, а затем выберите элементы **Надстройки** > **Надстройка для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="d569e-173">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then choose **Add-ins** > **Add-in for SharePoint**.</span></span>
    
 
4. <span data-ttu-id="d569e-174">Присвойте проекту имя EmployeeOrientation, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d569e-174">Name the project EmployeeOrientation, and then choose **OK**.</span></span>
    
 
5. <span data-ttu-id="d569e-p114">В первом диалоговом окне **Укажите параметры надстройки для SharePoint** введите полный URL-адрес сайта SharePoint, который вы собираетесь использовать для отладки надстройки. Это URL-адрес Сайта разработчика. Укажите в URL-адресе протокол HTTPS, а не HTTP. В диалоговом окне **Как требуется разместить надстройку SharePoint?** выберите вариант **Размещено в SharePoint** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p114">In the first **Specify the Add-in for SharePoint Settings** dialog box, provide the full URL of the SharePoint site that you want to use to debug your add-in. This is the URL of the Developer Site. (Use HTTPS, not HTTP in the URL.) Under **How do you want to host your SharePoint Add-in**, choose **SharePoint-hosted**. Choose **Finish**.</span></span>
    
 
6. <span data-ttu-id="d569e-p115">Вам может потребоваться войти на свой Сайт разработчика. В этом случае используйте учетные данные администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="d569e-p115">You may be prompted to login to your Developer Site. If so, use your subscription administrator's credentials.</span></span>
    
 
7. <span data-ttu-id="d569e-p116">После создания проекта откройте файл **/Pages/Default.aspx** из корневой папки проекта. Помимо прочего, этот созданный файл загружает один или оба сценария, размещенные в SharePoint: sp.runtime.js и sp.js. Часть кода для загрузки этих файлов можно найти в элементе управления **Content** в начале файла с идентификатором **PlaceHolderAdditionalPageHead**. Часть кода зависит от используемой версии **Инструментов разработчика Microsoft Office для Visual Studio**. Согласно руководствам из этой серии необходимо загрузить оба файла с обычными HTML-тегами **\<script\>**, а не с тегами **\<SharePoint:ScriptLink\>**. Убедитесь, что приведенные ниже строки присутствуют в элементе управления **PlaceHolderAdditionalPageHead** *над* строкой `<meta name="WebPartPageExpansion" content="full" />`.</span><span class="sxs-lookup"><span data-stu-id="d569e-p116">After the project is created, open the file /Pages/Default.aspx from the root of the project. Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js. The markup for loading these files is in the Content control near the top of the file that has the ID PlaceHolderAdditionalPageHead. The markup varies depending on the version of Microsoft Office Developer Tools for Visual Studio that you are using. This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML    tags, not <SharePoint:ScriptLink> tags. Ensure that the following lines are in the PlaceHolderAdditionalPageHead control, just above  the line :</span></span>
    
```
  <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
  <script type="text/javascript" src="/_layouts/15/sp.js"></script> 

```


<span data-ttu-id="d569e-p117">Проверьте файл на наличие другой разметки, загружающей один или оба файла сценария и удалите ее. Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="d569e-p117">Then search the file for any other markup that also loads one or the other of these files and remove the redundant markup. Save and close the file.</span></span>
    
 

## <a name="code-your-add-in"></a><span data-ttu-id="d569e-189">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="d569e-189">Code your add-in</span></span>
<span data-ttu-id="d569e-190"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="d569e-190"></span></span>

<span data-ttu-id="d569e-191">Для вашей первой надстройки SharePoint с размещением в SharePoint мы включим классическое расширение SharePoint: настраиваемый список и его экземпляр.</span><span class="sxs-lookup"><span data-stu-id="d569e-191">For your first SharePoint-hosted SharePoint Add-in, we'll include the classic SharePoint extension: a custom list and list instance.</span></span>
 

 

1. <span data-ttu-id="d569e-192">В **обозревателе решений** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="d569e-192">In **Solution Explorer**, open the AppManifest.xml file.</span></span>
    
 
2. <span data-ttu-id="d569e-p118">Когда откроется конструктор манифеста, измените значение в поле **Заголовок** на "Employee Orientation" (Обучение сотрудников). *Не* меняйте значение в поле **Имя** .</span><span class="sxs-lookup"><span data-stu-id="d569e-p118">When the manifest designer opens, add a space between the words in the **Title** field so that it readsEmployee Orientation. (Do  *not*  change the **Name** field.)</span></span>
    
 
3. <span data-ttu-id="d569e-195">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="d569e-195">Save and close the file.</span></span>
    
 
4. <span data-ttu-id="d569e-p119">Щелкните проект правой кнопкой мыши в **обозревателе решений** и выберите пункты **Добавить** > **Новая папка**. Укажите для папки имя "Lists" (Списки).</span><span class="sxs-lookup"><span data-stu-id="d569e-p119">Right-click the project in **Solution Explorer** and choose **Add** > **New Folder**. Name the folder Lists.</span></span>
    
 
5. <span data-ttu-id="d569e-p120">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Новый элемент**. Откроется диалоговое окно **Добавление нового элемента** для узла **Office/SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p120">Right-click the new folder and choose **Add** > **New Item**. The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>
    
 
6. <span data-ttu-id="d569e-p121">Выберите элемент **Список**. Задайте для него имя NewEmployeeOrientation и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p121">Choose **List**. Give it the name NewEmployeeOrientation, and then choose **Add**.</span></span> 
    
 
7. <span data-ttu-id="d569e-p122">На странице **Выберите параметры списка** в **мастере настройки SharePoint** оставьте заданное по умолчанию отображаемое имя списка **NewEmployeeOrientation**, нажмите кнопку **Создать настраиваемый шаблон списка и экземпляр списка на его основе** и в раскрывающемся списке выберите **По умолчанию (настраиваемый список)**. Затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p122">On the **Choose List Settings** page of the **SharePoint Customization Wizard**, leave the list display name at the default **NewEmployeeOrientation**, choose the **Create a customizable list template and a list instance of it** option button, and choose **Default (Custom List)** on the drop-down list. Then choose **Finish**.</span></span>
    
 
8. <span data-ttu-id="d569e-p123">Мастер создаст шаблон списка **NewEmployeeOrientation** с дочерним экземпляром списка под названием **NewEmployeeOrientationInstance**. При этом может открыться конструктор списков, который понадобится на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="d569e-p123">The wizard creates a **NewEmployeeOrientation** list template with a child list instance named **NewEmployeeOrientationInstance**. A list designer may open. It is used in a later step.</span></span>
    
 
9. <span data-ttu-id="d569e-207">Разверните узел **NewEmployeeOrientationInstance** в **обозревателе решений**, если вы еще не сделали этого, чтобы вам было легко отличать файл elements.xml, являющийся дочерним элементом *экземпляра* списка, от файла elements.xml, который представляет собой дочерний элемент *шаблона* списка.</span><span class="sxs-lookup"><span data-stu-id="d569e-207">Expand the **NewEmployeeOrientationInstance** node in **Solution Explorer**, if it isn't already, so that you can clearly distinguish the elements.xml file that is a child of the list  *instance*  from the elements.xml file that is a child of the list *template*  .</span></span>
    
    <span data-ttu-id="d569e-208">**Узел списков в обозревателе решений**</span><span class="sxs-lookup"><span data-stu-id="d569e-208">**Lists node in Solution Explorer**</span></span>

 

  ![Содержимое папки с дочерним шаблоном NewEmployeeOrientation, у которого есть три дочерних элемента (NewEmployeeOrientationInstance, файл elements.xml и файл schema.xml). У экземпляра есть дочерний элемент elements.xml.](../../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)
 

    
    
 
10. <span data-ttu-id="d569e-211">Откройте дочерний элемент elements.xml в шаблоне списка **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="d569e-211">Open the elements.xml child of the **NewEmployeeOrientation** list template.</span></span>
    
 
11. <span data-ttu-id="d569e-212">Измените значение атрибута **DisplayName** (не атрибута **Name**), чтобы имя стало более понятным: "Обучение новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="d569e-212">Add spaces to the **DisplayName** attribute (not the **Name** attribute) to make it friendlier:"New Employee Orientation".</span></span>
    
 
12. <span data-ttu-id="d569e-213">Задайте для атрибута **Description** значение "Orientation information about new employees" (Сведения об адаптации новых сотрудников).</span><span class="sxs-lookup"><span data-stu-id="d569e-213">Set the **Description** attribute to"Orientation information about new employees."</span></span>
    
 
13. <span data-ttu-id="d569e-214">Оставьте для других атрибутов значения по умолчанию, сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="d569e-214">Leave all other attributes at their default, save the file and close it.</span></span>
    
 
14. <span data-ttu-id="d569e-215">Если конструктор списков не открыт, выберите узел **NewEmployeeOrientation** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="d569e-215">If the list designer is not open, choose the **NewEmployeeOrientation** node in **Solution Explorer**.</span></span>
    
 
15. <span data-ttu-id="d569e-p125">Откройте вкладку **Список** конструктора. Эта вкладка используется для установки определенных значений *экземпляра* (не *шаблона*) списка, но она содержит некоторые значения по умолчанию, унаследованные от шаблона.</span><span class="sxs-lookup"><span data-stu-id="d569e-p125">Open the **List** tab of the designer. This tab is used to set certain values for the list *instance*  , not the list *template*  , but it has some default values that it inherited from the template.</span></span>
    
 
16. <span data-ttu-id="d569e-218">Замените значения на этой вкладке следующими:</span><span class="sxs-lookup"><span data-stu-id="d569e-218">Change the values on this tab to the following:</span></span>
    
      -  <span data-ttu-id="d569e-219">**Заголовок**: "New Employees in Seattle" (Новые сотрудники в Сиэтле).</span><span class="sxs-lookup"><span data-stu-id="d569e-219">**Title**: New Employees in Seattle</span></span>
    
 
  -  <span data-ttu-id="d569e-220">**URL-адрес списка**: Lists/NewEmployeesInSeattle.</span><span class="sxs-lookup"><span data-stu-id="d569e-220">**List URL**: Lists/NewEmployeesInSeattle</span></span>
    
 
  -  <span data-ttu-id="d569e-221">**Описание**: "New Employees in Seattle" (Новые сотрудники в Сиэтле).</span><span class="sxs-lookup"><span data-stu-id="d569e-221">**Description**: The new employees in Seattle.</span></span>
    
 

     <span data-ttu-id="d569e-222">Не меняя состояние флажков, сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="d569e-222">Leave the check boxes at their default status, save the file, and close the designer.</span></span>
    
 
17. <span data-ttu-id="d569e-p126">В **обозревателе решений** может отображаться старое имя экземпляра списка. В этом случае откройте контекстное меню узла **NewEmployeeOrientationInstance**, выберите пункт **Переименовать** и измените имя на NewEmployeesInSeattle.</span><span class="sxs-lookup"><span data-stu-id="d569e-p126">The list instance may have its old name in **Solution Explorer**. If so, open the shortcut menu for **NewEmployeeOrientationInstance**, choose **Rename**, and change the name to NewEmployeesInSeattle.</span></span>
    
 
18. <span data-ttu-id="d569e-225">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="d569e-225">Open the schema.xml file.</span></span>
    
 
19. <span data-ttu-id="d569e-p127">В элементе **View**, значение **BaseViewID** которого равно 0, замените имеющийся элемент **ViewFields** на приведенную ниже часть кода. Используйте именно этот GUID для параметра **FieldRef** с именем `Title`.</span><span class="sxs-lookup"><span data-stu-id="d569e-p127">In the **View** element whose **BaseViewID** value is "0", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `Title`.)</span></span>
    
     <span data-ttu-id="d569e-228">*В этом автоматически созданном файле schema.xml могут встречаться странные разрывы строк. Проверьте наличие соответствующих открывающих и закрывающих тегов для элемента **ViewFields**. Добавьте разрывы строк для удобочитаемости.*</span><span class="sxs-lookup"><span data-stu-id="d569e-228">*Line breaks may come at odd places in this autogenerated schema.xml file. Be sure you have found the matching begin and end tags for the **ViewFields** element. Add line breaks to improve readability.*</span></span> 
    


```
  <ViewFields>
  <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
  </ViewFields>
```

20. <span data-ttu-id="d569e-p128">Не закрывая файл schema.xml, в элементе **View**, значение **BaseViewID** которого равно 1, замените элемент **ViewFields** на приведенную ниже часть кода. Используйте именно этот GUID для параметра **FieldRef** с именем `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="d569e-p128">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
```
  <ViewFields>
  <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
  </ViewFields>
```

21. <span data-ttu-id="d569e-231">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="d569e-231">Save and close the schema.xml file.</span></span>
    
 
22. <span data-ttu-id="d569e-232">Откройте файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка **NewEmployeesInSeattle** (а не *шаблона* списка **NewEmployeeOrientation**).</span><span class="sxs-lookup"><span data-stu-id="d569e-232">Open the elements.xml file that is a child of the list  *instance*  **NewEmployeesInSeattle** (not the elements.xml that is a child of the list *template*  **NewEmployeeOrientation**).</span></span>
    
 
23. <span data-ttu-id="d569e-p129">В этом файле заполните список начальными данными. Для этого добавьте приведенную ниже часть кода с элементом **Data** в качестве дочернего элемента **ListInstance**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p129">In this file, populate the list with some initial data. You do this by adding the following **Data** element markup as a child element of the **ListInstance** element.</span></span>
    
```
  <Data>
  <Rows>
    <Row>
      <Field Name="Title">Tom Higginbotham</Field>
    </Row>
    <Row>
      <Field Name="Title">Satomi Hayakawa</Field>
    </Row>
    <Row>
      <Field Name="Title">Cassi Hicks</Field>
    </Row>
    <Row>
      <Field Name="Title">Lertchai Treetawatchaiwong</Field>
    </Row>
  </Rows>
</Data>
```

24. <span data-ttu-id="d569e-235">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="d569e-235">Save and close the file.</span></span>
    
 
25. <span data-ttu-id="d569e-p130"> В **обозревателе решений** дважды щелкните элемент **Компонент1**, чтобы открыть конструктор компонентов. В конструкторе укажите для параметра **Заголовок** значение "New Employee Orientation Components" (Компоненты для обучения новых сотрудников), а для параметра **Описание** — значение "Lists and other components for getting employees oriented to the company" (Списки и другие компоненты для обучения сотрудников в компании). Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="d569e-p130">In **Solution Explorer**, double-click **Feature1** to open the Feature designer. In the designer, set the **Title** toNew Employee Orientation Components and set the **Description** toLists and other components for getting employees oriented to the company. Save the file, and close the designer.</span></span>
    
 
26. <span data-ttu-id="d569e-239">Если элемент **Компонент1** в **обозревателе решений** не был переименован автоматически, откройте его контекстное меню, выберите пункт **Переименовать** и укажите имя NewEmployeeOrientationComponents.</span><span class="sxs-lookup"><span data-stu-id="d569e-239">If the **Feature1** in **Solution Explorer** has not been automatically renamed, open its shortcut menu, choose **Rename**, and rename it NewEmployeeOrientationComponents.</span></span>
    
 
27. <span data-ttu-id="d569e-240">Откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="d569e-240">Open the Default.aspx file.</span></span>
    
 
28. <span data-ttu-id="d569e-p131">Найдите элемент **Content** ASP.NET с идентификатором **PlaceHolderPageTitleInTitleArea**. Замените заданную по умолчанию строку "Page Title" (Заголовок страницы) на "New Employees by Location" (Новые сотрудники по месту работы).</span><span class="sxs-lookup"><span data-stu-id="d569e-p131">Find the ASP.NET **Content** element with the ID **PlaceHolderPageTitleInTitleArea**. Replace the default string "Page Title" with "New Employees by Location".</span></span>
    
 
29. <span data-ttu-id="d569e-p132">Найдите элемент **Content** ASP.NET с идентификатором **PlaceHolderMain**. *Замените* его содержимое на приведенную ниже часть кода. ` _spPageContextInfo` — это объект JavaScript, который SharePoint автоматически добавляет на страницу. Его свойство `webAbsoluteUrl` возвращает URL-адрес сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="d569e-p132">Find the ASP.NET **Content** element with the ID **PlaceHolderMain**.  *Replace*  its contents with the following markup. The ` _spPageContextInfo` is a JavaScript object that SharePoint automatically includes in the page. It's `webAbsoluteUrl` property returns the URL of the add-in web.</span></span>
    
```XML
    <p><asp:HyperLink runat="server" 
    NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
    Text="New Employees in Seattle" /></p>
```


## <a name="run-the-add-in-and-test-the-list"></a><span data-ttu-id="d569e-247">Запуск надстройки и тестирование списка</span><span class="sxs-lookup"><span data-stu-id="d569e-247">Run the add-in and test the list</span></span>
<span data-ttu-id="d569e-248"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="d569e-248"></span></span>


 

 

1. <span data-ttu-id="d569e-p133">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку и немедленный запуск надстройки на тестовом сайте SharePoint. (Сведения о том, как пользователи запускают установленное Надстройка SharePoint, см. в разделе  [Дальнейшие действия](#Nextsteps).)</span><span class="sxs-lookup"><span data-stu-id="d569e-p133">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in. (To find out how end users run an installed SharePoint Add-in, see  [Next Steps](#Nextsteps).)</span></span>
    
 
2. <span data-ttu-id="d569e-252">Когда откроется страница надстройки, используемая по умолчанию, перейдите по ссылке **New Employees in Seattle** (Новые сотрудники в Сиэтле), чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="d569e-252">When the add-in's default page opens, choose the **New Employees in Seattle** link to open the custom list instance.</span></span>
    
    <span data-ttu-id="d569e-253">**Страница по умолчанию и страница представления списка**</span><span class="sxs-lookup"><span data-stu-id="d569e-253">**Default page and list view page**</span></span>

 

  ![Отображается страница по умолчанию надстройки, озаглавленная "Новые сотрудники по расположению". Ссылка "Новые сотрудники в Сиэтле". Стрелка от этой ссылки указывает на страницу списка. Она называется "Новые сотрудники в Сиэтле", список приведен ниже.](../../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)
 

    
    
 
3. <span data-ttu-id="d569e-258">Добавьте и удалите элементы в списке.</span><span class="sxs-lookup"><span data-stu-id="d569e-258">Add and delete items from the list.</span></span>
    
 
4. <span data-ttu-id="d569e-p135">Для завершения сеанса отладки закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio отзовет предыдущую версию надстройки и установит самую последнюю.</span><span class="sxs-lookup"><span data-stu-id="d569e-p135">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
 
5. <span data-ttu-id="d569e-p136">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуется отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="d569e-p136">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>
    
 

## 
<span data-ttu-id="d569e-263"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="d569e-263"></span></span>

<span data-ttu-id="d569e-p137">Пока в списке указано немного сведений об адаптации. Мы добавим некоторые из них в новых статьях из этой серии. А пока отвлекитесь слегка от написания кода и почитайте о том, как развертывать Надстройки SharePoint, в статье  [Развертывание и установка надстроек для SharePoint](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in).</span><span class="sxs-lookup"><span data-stu-id="d569e-p137">So far, there isn't much orientation information in the list. We'll add some in later articles in this series. But first, take a brief break from coding to learn about deploying SharePoint Add-ins in  [Deploy and install a SharePoint-hosted SharePoint Add-in](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in).</span></span>
 

 

