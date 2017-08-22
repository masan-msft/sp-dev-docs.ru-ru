# <a name="set-up-a-development-environment-for-sharepoint-add-ins-on-office-365"></a><span data-ttu-id="45998-101">Настройка среды разработки надстроек SharePoint в Office 365</span><span class="sxs-lookup"><span data-stu-id="45998-101">Set up a development environment for SharePoint Add-ins on Office 365</span></span>
<span data-ttu-id="45998-102">Настройте среду разработки надстроек SharePoint на Сайте разработчика для Office 365.</span><span class="sxs-lookup"><span data-stu-id="45998-102">Set up a development environment for SharePoint Add-ins on an Office 365 Developer Site.</span></span>
 

 <span data-ttu-id="45998-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в статье [Название "приложения для Office и SharePoint" изменилось на "надстройки Office и SharePoint"](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="45998-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="45998-p102">Прежде чем выполнять действия, описанные в этой статье, прочтите статью [Средства и среды для разработки надстроек для SharePoint](tools-and-environments-for-developing-sharepoint-add-ins), чтобы ознакомиться с существующими возможностями. Если вы не знаете, какие надстройки SharePoint вам нужны, ознакомьтесь с материалами на странице [Надстройки SharePoint](sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="45998-p102">Set up a development environment for SharePoint Add-ins on an Office 365 Developer Site. Please read  [Tools and environments for developing SharePoint Add-ins](tools-and-environments-for-developing-sharepoint-add-ins) to get an understanding of your options before you carry out any procedures in this article. See [SharePoint Add-ins](sharepoint-add-ins) if you are not sure what kinds of SharePoint Add-ins you want to create.</span></span>
 

## <a name="install-visual-studio-and-tools-on-your-computer"></a><span data-ttu-id="45998-108">Установка Visual Studio и инструментов на компьютере</span><span class="sxs-lookup"><span data-stu-id="45998-108">Install Visual Studio and tools on your computer</span></span>
<span data-ttu-id="45998-109"><a name="devenv_vs"> </a></span><span class="sxs-lookup"><span data-stu-id="45998-109"></span></span>


- <span data-ttu-id="45998-p103">Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это согласно инструкциям на странице [Установка Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). Мы рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="45998-p103">If you don't already have **Visual Studio** 2013 or later installed, install it with the instructions at [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). We recommend using the  [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
    
 
- <span data-ttu-id="45998-p104">Visual Studio включает в себя **Инструменты разработчика Microsoft Office для Visual Studio**, но иногда выход новой версии инструментов не совпадает с выходом обновлений Visual Studio. Чтобы убедиться, что вы используете последнюю версию инструментов, запустите [установщик Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [установщик Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="45998-p104">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**, but sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools use run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 
    
 

### <a name="verbose-logging-in-visual-studio"></a><span data-ttu-id="45998-114">Подробное ведение журнала в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45998-114">Verbose logging in Visual Studio</span></span>

<span data-ttu-id="45998-115">Выполните указанные ниже действия, чтобы включить подробное ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="45998-115">Follow these steps if you want to turn on verbose logging:</span></span>
 

 

1. <span data-ttu-id="45998-116">Откройте реестр и перейдите к разделу **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, где _nn.n_ — это номер версии Visual Studio, например 12.0 или 14.0.</span><span class="sxs-lookup"><span data-stu-id="45998-116">Open the registry, and navigate to HKEY_CURRENT_USERSoftwareMicrosoft**VisualStudio_nn.n_SharePointTools**, where _nn.n_ is the version of Visual Studio, such as 12.0 or 14.0.</span></span>
    
 
2. <span data-ttu-id="45998-117">Добавьте ключ DWORD под названием **EnableDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="45998-117">Add a DWORD key named **EnableDiagnostics**.</span></span>
    
 
3. <span data-ttu-id="45998-118">Присвойте ключу значение **1**.</span><span class="sxs-lookup"><span data-stu-id="45998-118">Give the key the value **1**.</span></span>
    
 
<span data-ttu-id="45998-119">Путь реестра в будущих версиях Visual Studio изменится.</span><span class="sxs-lookup"><span data-stu-id="45998-119">The registry path will change in future versions of Visual Studio.</span></span>
 

 

## <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="45998-120">Регистрация на Сайте разработчика для Office 365</span><span class="sxs-lookup"><span data-stu-id="45998-120">Sign up for an Office 365 Developer Site</span></span>
<span data-ttu-id="45998-121"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="45998-121"></span></span>


 <span data-ttu-id="45998-p105">**Примечание.** Возможно, у вас уже есть доступ к Сайту разработчика для Office 365. **Вы являетесь подписчиком MSDN?** Visual Studio Enterprise с подпиской MSDN предоставляет льготное право на подписку разработчика приложений для Office 365. [Воспользуйтесь этим преимуществом прямо сегодня.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **У вас есть один из указанных ниже планов подписки на Office 365?** **В этом случае администратор подписки на Office 365 может создать Сайт разработчика, ** используя [Центр администрирования Office 365](https://portal.microsoftonline.com/admin/default.aspx). Дополнительные сведения см. в статье [Создание сайта разработчика для существующей подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription).</span><span class="sxs-lookup"><span data-stu-id="45998-p105">**Note**   You might already have access to an Office 365 Developer Site: **Are you an MSDN subscriber?** Visual Studio Enterprise with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **Do you have one of the following Office 365 subscription plans?** **If so, an administrator of the Office 365 subscription can create a Developer Site** by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx). For more information, see  [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription).</span></span> 
 

<span data-ttu-id="45998-128">Три способа получения плана Office 365:</span><span class="sxs-lookup"><span data-stu-id="45998-128">Three ways to get an Office 365 plan.</span></span> 
 

 

- <span data-ttu-id="45998-p106">Бесплатно зарегистрируйте учетную запись разработчика Office 365 через программу для разработчиков Office 365 сроком на один год.  [Узнайте больше на сайте программы ](http://dev.office.com/devprogram) или заполните [форму регистрации](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). После регистрации в программе для разработчиков вы получите сообщение электронной почты со ссылкой для входа в учетную запись разработчика. Затем следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="45998-p106">Sign up for a free, one year Office 365 developer account through the Office 365 Developer Program.  [Get more information](http://dev.office.com/devprogram), or go straight to  [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170). You'll get an e-mail after you sign up for the developer program with a link to sign up for the developer account. Use the instructions below.</span></span>
    
 
- <span data-ttu-id="45998-133">Начните с [бесплатной 30-дневной пробной версии](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) с лицензией для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="45998-133">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>
    
 
- <span data-ttu-id="45998-134">Приобретите [подписку разработчика приложений для Office 365](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="45998-134">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 
    
 

 <span data-ttu-id="45998-135">**Совет.** Откройте эти ссылки в новом окне или на новой вкладке, чтобы работать с ними было удобнее.</span><span class="sxs-lookup"><span data-stu-id="45998-135">**TIP** Open these links in another window or tab in order to keep the following instructions handy.</span></span>
 


<span data-ttu-id="45998-136">**Рис. 1. Доменное имя Сайта разработчика Office 365**</span><span class="sxs-lookup"><span data-stu-id="45998-136">**Figure 1. Office 365 Developer Site domain name**</span></span>

 

 
![Страница 2 регистрационной формы для учетной записи Office 365](../../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. <span data-ttu-id="45998-p107">Первая страница (не отображается) регистрационной формы не требует объяснений. Просто введите запрашиваемую информацию о себе и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="45998-p107">The first page (not shown) of the signup form is self-explanatory. Just supply the information about yourself that is requested and choose **Next**.</span></span>
    
 
2. <span data-ttu-id="45998-140">На второй странице (рис. 1) укажите ИД администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="45998-140">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
    
 
3. <span data-ttu-id="45998-141">Создайте поддомен **.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="45998-141">Create a subdomain of **.onmicrosoft.com**.</span></span> 
    
    <span data-ttu-id="45998-p108">После регистрации необходимо использовать полученные учетные данные (в формате _ИД_пользователя_@ _ваш_домен_.onmicrosoft.com) для входа на сайт портала Office 365, на котором администрируется ваша учетная запись. Ваш Сайт разработчика для SharePoint Online подготавливается к работе на новом домене: **http:// _ваш_домен_.sharepoint.com**.</span><span class="sxs-lookup"><span data-stu-id="45998-p108">After signup, you have to use the resulting credentials (in the format UserID@yourdomain.onmicrosoft.com) to sign in to your off365short portal site where you administer your account. Your sposhort Developer Site is provisioned at your new domain: http://yourdomain.sharepoint.com.</span></span>
    
 
4. <span data-ttu-id="45998-p109">Нажмите кнопку **Далее** и заполните последнюю страницу формы. Если вы хотите указать номер телефона, чтобы получить код подтверждения, можно ввести номер мобильного или стационарного телефона, но *не* номер VoIP.</span><span class="sxs-lookup"><span data-stu-id="45998-p109">Choose **Next** and fill out the final page of the form. If you choose to provide a telephone number to obtain a confirmation code, you can provide a mobile or land line telephone number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
 

    
 <span data-ttu-id="45998-p110">**Примечание.** Если при попытке зарегистрировать учетную запись разработчика вы входите в другую учетную запись Майкрософт, может отобразиться такое сообщение: "Введенный ИД пользователя неверный. Возможно, он недействителен. Убедитесь, что вы вводите свой ИД пользователя, назначенный вам организацией. Он должен выглядеть так: *proverka@example.com* или *proverka@example.onmicrosoft.com*". Если появляется такое сообщение, выйдите из учетной записи Майкрософт, которую использовали, и повторите попытку. Если сообщение продолжает отображаться, очистите кэш браузера или выберите режим **Просмотр InPrivate**, затем заполните форму.</span><span class="sxs-lookup"><span data-stu-id="45998-p110">**Note**  If you're logged on to another Microsoft account when you try to sign up for a developer account, you might get this message: "Sorry, that user ID you entered didn't work. It looks like it's not valid. Be sure you enter the user ID that your organization assigned to you. Your user ID usually looks like  *someone@example.com*  or *someone@example.onmicrosoft.com*  ."If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to  **InPrivate Browsing** and then fill out the form.</span></span>
 

<span data-ttu-id="45998-p111">По завершении регистрации в браузере откроется страница установки Office 365. Щелкните значок администратора, чтобы открыть страницу Центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="45998-p111">After you finish the signup process, your browser will opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span>
 

 

<span data-ttu-id="45998-153">**Рис. 2. Страница Центра администрирования Office 365**</span><span class="sxs-lookup"><span data-stu-id="45998-153">**Figure 2. Office 365 admin center page**</span></span>

 

 
![Снимок экрана с изображением центра администрирования Office 365.](../../images/SP15_Office365AdminInset_border.png)
 

 

1. <span data-ttu-id="45998-p112">Необходимо подождать, пока завершится подготовка к работе Сайта разработчика. После этого обновите страницу Центра администрирования в браузере.</span><span class="sxs-lookup"><span data-stu-id="45998-p112">You'll have to wait for your Developer Site to finish provisioning. After provisioning is complete, refresh the admin center page in your browser.</span></span>
    
 
2. <span data-ttu-id="45998-p113">Затем щелкните ссылку **Создание надстроек** в верхнем левом углу страницы, чтобы открыть Сайт разработчиков. Должен открыться сайт, который выглядит так, как показано на рис. 3. На странице размещен список **Тестируемые надстройки**. Это подтверждает, что веб-сайт был создан с помощью шаблона Сайта разработчика SharePoint. Если вместо него вы видите обычный сайт группы, подождите несколько минут и перезапустите сайт.</span><span class="sxs-lookup"><span data-stu-id="45998-p113">Then, choose the **Build Add-ins** link in the upper left corner of the page to open your Developer Site. You should see a site that looks like the one in Figure 3. There is an **Add-ins in Testing** list on the page. This confirms that the website was made with SharePoint's Developer Site template. If you see a regular team site instead, wait a few minutes and launch your site again.</span></span>
    
 
3. <span data-ttu-id="45998-p114">Обратите внимание на URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45998-p114">Make a note of the URL of the site. It is used when you create SharePoint Add-ins projects in Visual Studio.</span></span>
    
 

<span data-ttu-id="45998-164">**Рис. 3. Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**</span><span class="sxs-lookup"><span data-stu-id="45998-164">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

 

 
![Снимок экрана с изображением домашней страницы сайта разработчика.](../../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="additional-resources"></a><span data-ttu-id="45998-166">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="45998-166">Additional resources</span></span>
<span data-ttu-id="45998-167"><a name="SP15SetupSPO365_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="45998-167"></span></span>


-  [<span data-ttu-id="45998-168">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="45998-168">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="45998-169">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="45998-169">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="45998-170">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="45998-170">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

 

 

