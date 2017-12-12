---
title: "Знакомство с созданием надстроек SharePoint с размещением в SharePoint"
description: "Узнайте, как настроить среду разработки и создать свою первую надстройку SharePoint с размещением в SharePoint."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: 7cf441bb18f0c4b6658a57be4e949eafce9a3260
ms.sourcegitcommit: 074f3a7983a7b253f56f8c670a0290c27bb7734b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="fcd5e-103">Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="fcd5e-103">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>

<span data-ttu-id="fcd5e-104">Надстройки с размещением в SharePoint — это один из двух основных типов надстроек SharePoint. Обзор надстроек SharePoint и этих основных типов см. в статье [Надстройки SharePoint](sharepoint-add-ins.md). Ниже представлен обзор надстроек с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-104">SharePoint-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see  [SharePoint Add-ins](sharepoint-add-ins.md). Here's a summary of SharePoint-hosted add-ins:</span></span>

- <span data-ttu-id="fcd5e-105">Они содержат списки SharePoint, веб-части, рабочие процессы, пользовательские страницы и другие компоненты, каждый из которых установлен на дочернем сайте (сайте надстройки) того веб-сайта SharePoint, на котором установлена надстройка.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-105">They contain SharePoint lists, Web Parts, workflows, custom pages, and other components, all of which are installed on a subweb, called the add-in web, of the SharePoint website where the add-in is installed.</span></span>

- <span data-ttu-id="fcd5e-106">Единственный код, который они содержат, — JavaScript пользовательских страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-106">The only code they have is JavaScript on custom SharePoint pages.</span></span>

- <span data-ttu-id="fcd5e-107">Этап 1. Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="fcd5e-107">Step 1 - Set up your dev environment</span></span> 

- <span data-ttu-id="fcd5e-108">Этап 2. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="fcd5e-108">Step 2 - Create the app project</span></span> 

- <span data-ttu-id="fcd5e-109">Этап 3. Написание кода приложения</span><span class="sxs-lookup"><span data-stu-id="fcd5e-109">Step 3 - Code your app</span></span>

<span data-ttu-id="fcd5e-110"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="fcd5e-110"></span></span>
## <a name="set-up-your-dev-environment"></a><span data-ttu-id="fcd5e-111">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="fcd5e-111">Set up your dev environment</span></span>

<span data-ttu-id="fcd5e-112">Существует множество способов настройки среды разработки для надстроек SharePoint. Здесь приведен самый простой из них.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-112">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way. For alternatives, see  Additional resources.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="fcd5e-113">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="fcd5e-113">Get the tools</span></span>

- <span data-ttu-id="fcd5e-114">Если у вас еще не установлена среда **Visual Studio** 2013 или более поздней версии, установите ее согласно инструкциям на странице [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-114">If you don't already have  **Visual Studio** 2013 or later installed, install it using the instructions at [Install Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio). We recommend using the  latest version from the Microsoft Download Center.</span></span> <span data-ttu-id="fcd5e-115">Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-115">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>

- <span data-ttu-id="fcd5e-116">Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-116">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="fcd5e-117">Иногда выпуск новой версии инструментов не совпадает с выходом обновлений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-117">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="fcd5e-118">Чтобы убедиться, что у вас установлена последняя версия инструментов, запустите [установщик Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [установщик Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-118">Visual Studio includes the  Microsoft Office Developer Tools for Visual Studio. Sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 

<span data-ttu-id="fcd5e-119"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="fcd5e-119"></span></span>
### <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="fcd5e-120">Регистрация сайта разработчика для Office 365</span><span class="sxs-lookup"><span data-stu-id="fcd5e-120">Sign up for an Office 365 Developer Site</span></span>

> [!NOTE]
> <span data-ttu-id="fcd5e-121">Возможно, у вас уже есть доступ к сайту разработчика Office 365.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-121">Note You might already have access to an Office 365 Developer Site:</span></span>
> - <span data-ttu-id="fcd5e-p103">**Вы подписчик MSDN?** Visual Studio Ultimate и Visual Studio Premium с подпиской MSDN предоставляют льготное право на подписку разработчика приложений для Office 365. [Воспользуйтесь этим преимуществом прямо сегодня.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="fcd5e-p103">**Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span></span> 
> - <span data-ttu-id="fcd5e-125">**У вас есть один из указанных ниже планов подписки на Office 365?**</span><span class="sxs-lookup"><span data-stu-id="fcd5e-125">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="fcd5e-126">В таком случае администратор подписки на Office 365 может создать сайт разработчика с помощью [Центра администрирования Office 365](https://portal.microsoftonline.com/admin/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-126">If so, an administrator of the Office 365 subscription can create a Developer Site by using the [Office 365 admin center. For more information, see  Create a developer site on an existing Office 365 subscription](https://portal.microsoftonline.com/admin/default.aspx).</span></span> <span data-ttu-id="fcd5e-127">Дополнительные сведения см. в статье [Создание сайта разработчика с использованием имеющейся подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-127">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="fcd5e-128">Получить план Office 365 можно тремя способами:</span><span class="sxs-lookup"><span data-stu-id="fcd5e-128">There are three ways to get an Office 365 plan.</span></span> 

- <span data-ttu-id="fcd5e-129">Начните с [бесплатной 30-дневной пробной версии](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) с лицензией для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-129">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>

- <span data-ttu-id="fcd5e-130">Приобретите [подписку разработчика приложений для Office 365](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-130">Buy an  [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 

- <span data-ttu-id="fcd5e-131">Зарегистрируйте бесплатную учетную запись разработчика Office 365 на один год, приняв участие в программе для разработчиков приложений для Office 365.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-131">Sign up for a free, one-year Office 365 developer account through the Office 365 Developer Program.</span></span> <span data-ttu-id="fcd5e-132">[Ознакомьтесь с дополнительными сведениями](http://dev.office.com/devprogram) или перейдите непосредственно к [форме регистрации](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-132">[Get more information](http://dev.office.com/devprogram), or go straight to [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170).</span></span> <span data-ttu-id="fcd5e-133">После регистрации в программе для разработчиков вы получите электронное сообщение со ссылкой для регистрации учетной записи разработчика.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-133">You'll get an email after you sign up for the developer program with a link to sign up for the developer account.</span></span> <span data-ttu-id="fcd5e-134">Следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-134">Use the following instructions.</span></span>

> [!TIP]
> <span data-ttu-id="fcd5e-135">Откройте эти ссылки в новом окне или на новой вкладке, чтобы работать с ними было удобнее.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-135">Open these links in another window or tab in order to keep the following instructions handy.</span></span>

1. <span data-ttu-id="fcd5e-136">Первая страница регистрационной формы не требует объяснений. Укажите нужные сведения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-136">The first page (not shown) of the signup form is self-explanatory; supply the requested information and then choose  **Next**.</span></span>

2. <span data-ttu-id="fcd5e-137">На второй странице (рис. 1) укажите ИД администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-137">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
   
   <span data-ttu-id="fcd5e-138">*Рис. 1. Доменное имя сайта разработчика Office 365*</span><span class="sxs-lookup"><span data-stu-id="fcd5e-138">*Figure 1. Office 365 Developer Site domain name*</span></span>

   ![Страница 2 формы для регистрации учетной записи Office 365](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
   
3. <span data-ttu-id="fcd5e-140">Создайте поддомен **.onmicrosoft.com**, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-140">Create a subdomain of **.onmicrosoft.com**; for example, contoso.onmicrosoft.com.</span></span>
    
   <span data-ttu-id="fcd5e-141">После регистрации необходимо использовать полученные учетные данные (в формате *ИД_пользователя@ваш_домен.onmicrosoft.com*), чтобы войти на сайт портала Office 365, используемого для администрирования учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-141">After signup, you use the resulting credentials (in the format  *UserID*yourdomain.onmicrosoft.com) to sign in to your Office 365 portal site where you administer your account. Your SharePoint Online Developer Site is set up at your new domain:  http:// yourdomain.sharepoint.com.</span></span> <span data-ttu-id="fcd5e-142">Ваш сайт разработчика SharePoint Online будет установлен на новом домене: `http://yourdomain.sharepoint.com`.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-142">Your SharePoint Online Developer Site is set up at your new domain: `http://yourdomain.sharepoint.com`.</span></span>
    
4. <span data-ttu-id="fcd5e-143">Нажмите кнопку **Далее** и заполните последнюю страницу формы.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-143">Select **Next** and fill out the final page of the form.</span></span> <span data-ttu-id="fcd5e-144">Если вы хотите указать номер телефона, чтобы получить код подтверждения, можно ввести номер мобильного или стационарного телефона, но *не* номер VoIP.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-144">Choose  Next and fill out the final page of the form. If you choose to provide a telephone number to get a confirmation code, you can provide a mobile or landline number, but *not*  a VoIP (Voice over Internet Protocol) number.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="fcd5e-145">Если при попытке зарегистрировать учетную запись разработчика уже выполнен вход в другую учетную запись Майкрософт, может появиться сообщение "К сожалению, указанный вами ИД пользователя не работает.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-145">If you're signed in to another Microsoft account when you try to sign up for a developer account, you might see this message: "Sorry, that user ID you entered didn't work.</span></span> <span data-ttu-id="fcd5e-146">Похоже, он не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-146">It looks like it's not valid.</span></span> <span data-ttu-id="fcd5e-147">Обязательно укажите ИД пользователя, назначенный вам организацией.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-147">Be sure you enter the user ID that your organization assigned to you.</span></span> <span data-ttu-id="fcd5e-148">Как правило, ИД пользователя представлен в формате *proverka@example.com* или *proverka@example.onmicrosoft.com*".</span><span class="sxs-lookup"><span data-stu-id="fcd5e-148">Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*."</span></span> 

   > <span data-ttu-id="fcd5e-149">Если появится это сообщение, выйдите из используемой учетной записи Майкрософт и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-149">If you see that message, sign out of the Microsoft account you were using and try again.</span></span> <span data-ttu-id="fcd5e-150">Если сообщение по-прежнему появляется, очистите кэш браузера или переключитесь в режим **Просмотр InPrivate **, а затем заполните форму.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-150">If you see this message, log out of the Microsoft account you were using and try again. If you still get the message, clear your browser cache or switch to **InPrivate Browsing** and then fill out the form.</span></span>

   <span data-ttu-id="fcd5e-151">По завершении регистрации в браузере откроется страница установки Office 365.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-151">After you finish the signup process, your browser opens the Office 365 installation page. Choose the Admin icon to open the admin center page.</span></span> <span data-ttu-id="fcd5e-152">Щелкните значок администратора, чтобы открыть страницу центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-152">Select the Admin icon to open the admin center page.</span></span>

   <span data-ttu-id="fcd5e-153">*Рис. 2. Страница Центра администрирования Office 365*</span><span class="sxs-lookup"><span data-stu-id="fcd5e-153">*Figure 2. Office 365 admin center page*</span></span>

   ![Снимок экрана с изображением Центра администрирования Office 365.](../images/SP15_Office365AdminInset_border.png)
 
5. <span data-ttu-id="fcd5e-p111">Подождите, пока завершится настройка сайта разработчика. После этого обновите страницу центра администрирования в браузере.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-p111">Wait for your Developer Site to finish setting up. After provisioning is complete, refresh the admin center page in your browser.</span></span>

6. <span data-ttu-id="fcd5e-157">Перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-157">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="fcd5e-158">Открывшийся сайт должен выглядеть так, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-158">You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="fcd5e-159">Список **Тестируемые надстройки** на странице подтверждает, что веб-сайт был создан с помощью шаблона "Сайт разработчика" из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-159">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="fcd5e-160">Если вместо этого отображается обычный сайт группы, подождите несколько минут и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-160">If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>

7. <span data-ttu-id="fcd5e-161">Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-161">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>

   <span data-ttu-id="fcd5e-162">*Рис. 3. Домашняя страница сайта разработчика со списком "Тестируемые надстройки"*</span><span class="sxs-lookup"><span data-stu-id="fcd5e-162">*Figure 3. Your Developer Site home page with the Add-ins in Testing list*</span></span>

   ![Снимок экрана с изображением домашней страницы сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)

<span data-ttu-id="fcd5e-164"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="fcd5e-164"></span></span>
## <a name="create-the-add-in-project"></a><span data-ttu-id="fcd5e-165">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="fcd5e-165">Create the add-in project</span></span>

1. <span data-ttu-id="fcd5e-166">Запустите Visual Studio, выбрав команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-166">Start Visual Studio using the **Run as administrator** option.</span></span>

2. <span data-ttu-id="fcd5e-167">В Visual Studio выберите пункты **Файл** > **Создать** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-167">In Visual Studio, select **File** > **New** > **New Project**.</span></span>
 
3. <span data-ttu-id="fcd5e-168">В диалоговом окне **Новый проект** последовательно разверните узлы **Visual C#** и **Office/SharePoint**, а затем выберите элементы **Надстройки** > **Надстройка для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-168">In the  **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then choose **Add-ins** > **Add-in for SharePoint**.</span></span>

4. <span data-ttu-id="fcd5e-169">Присвойте проекту имя **EmployeeOrientation**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-169">Name the project EmployeeOrientation, and then choose  OK.</span></span>

5. <span data-ttu-id="fcd5e-170">В диалоговом окне **Настройка параметров надстроек SharePoint** укажите полный URL-адрес сайта SharePoint, который требуется использовать для отладки надстройки.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-170">In the first  **Specify the Add-in for SharePoint Settings** dialog box, provide the full URL of the SharePoint site that you want to use to debug your add-in. This is the URL of the Developer Site. (Use HTTPS, not HTTP in the URL.) Under How do you want to host your SharePoint Add-in, choose  SharePoint-hosted. Choose  Finish.</span></span> <span data-ttu-id="fcd5e-171">Это URL-адрес сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-171">This is the URL of the Developer Site.</span></span> <span data-ttu-id="fcd5e-172">Используйте в URL-адресе протокол HTTPS, а не HTTP. В разделе **Как требуется разместить надстройку SharePoint?**, выберите **Размещено в SharePoint**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-172">(Use HTTPS, not HTTP in the URL.) Under **How do you want to host your SharePoint Add-in**, select  **SharePoint-hosted**, and then select **Finish**.</span></span>

6. <span data-ttu-id="fcd5e-173">Вам может быть предложено войти на сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-173">You may be prompted to sign in to your Developer Site.</span></span> <span data-ttu-id="fcd5e-174">В таком случае используйте учетные данные администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-174">You may be prompted to login to your off365devsiteshort. If so, use your subscription administrator's credentials.</span></span>

7. <span data-ttu-id="fcd5e-175">После создания проекта откройте файл **/Pages/Default.aspx** из корневой папки проекта.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-175">After the project is created, open the file **/Pages/Default.aspx** from the root of the project.</span></span> <span data-ttu-id="fcd5e-176">Помимо прочего, этот созданный файл загружает один или оба сценария, размещенные в SharePoint: sp.runtime.js и sp.js.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-176">Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js.</span></span> <span data-ttu-id="fcd5e-177">Разметку для загрузки этих файлов можно найти в элементе управления **Content** в верхней части файла с идентификатором **PlaceHolderAdditionalPageHead**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-177">The markup for loading these files is in the **Content** control near the top of the file that has the ID **PlaceHolderAdditionalPageHead**.</span></span> <span data-ttu-id="fcd5e-178">Разметка зависит от используемой версии **Инструментов разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-178">The markup varies depending on the version of **Microsoft Office Developer Tools for Visual Studio** that you are using.</span></span> <span data-ttu-id="fcd5e-179">В руководствах из этой серии необходимо загружать оба файла с обычными HTML-тегами **\<script\>**, а не с тегами **\<SharePoint:ScriptLink\>**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-179">This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML **\<script\>** tags, not **\<SharePoint:ScriptLink\>** tags.</span></span> 

    <span data-ttu-id="fcd5e-180">Убедитесь, что указанные ниже строки присутствуют в элементе управления **PlaceHolderAdditionalPageHead** *над* строкой `<meta name="WebPartPageExpansion" content="full" />`.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-180">Ensure that the following lines are in the **PlaceHolderAdditionalPageHead** control, *just above*  the line `<meta name="WebPartPageExpansion" content="full" />`:</span></span>
    
    ```
      <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
      <script type="text/javascript" src="/_layouts/15/sp.js"></script> 
    ```

8. <span data-ttu-id="fcd5e-181">Проверьте файл на наличие другой разметки, загружающей один или оба файла сценариев, и удалите ее.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-181">Then search the file for any other markup that also loads one or the other of these files and remove the redundant markup. Save and close the file.</span></span> <span data-ttu-id="fcd5e-182">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-182">Save and close the file.</span></span>

<span data-ttu-id="fcd5e-183"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="fcd5e-183"></span></span>
## <a name="code-your-add-in"></a><span data-ttu-id="fcd5e-184">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="fcd5e-184">Code your add-in</span></span>

<span data-ttu-id="fcd5e-185">Для вашей первой надстройки SharePoint с размещением в SharePoint мы включим классическое расширение SharePoint: настраиваемый список и его экземпляр.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-185">For your first SharePoint-hosted SharePoint Add-in, we'll include the classic SharePoint extension: a custom list and list instance.</span></span>

1. <span data-ttu-id="fcd5e-186">В **обозревателе решений** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-186">In **Solution Explorer**, open the AppManifest.xml file.</span></span>

2. <span data-ttu-id="fcd5e-187">Когда откроется конструктор манифеста, измените значение в поле **Title**, на **Адаптация сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-187">When the manifest designer opens, add a space between the words in the Title field so that it reads Employee Orientation. (Do not change the Name field.)</span></span> <span data-ttu-id="fcd5e-188">*Не* меняйте значение в поле **Name**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-188">(Do  *not* change the **Name** field.)</span></span>

3. <span data-ttu-id="fcd5e-189">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-189">Save and close the file.</span></span>

4. <span data-ttu-id="fcd5e-190">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-190">Right-click the project in **Solution Explorer** and select **Add** > **New Folder**.</span></span> <span data-ttu-id="fcd5e-191">Назовите папку Lists.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-191">Name of the folder.</span></span>

5. <span data-ttu-id="fcd5e-192">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-192">Right-click the new folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="fcd5e-193">В узле **Office/SharePoint** откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-193">Right-click the new folder and choose  AddNew Item. The  **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>

6. <span data-ttu-id="fcd5e-194">Выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-194">Select **List**.</span></span> <span data-ttu-id="fcd5e-195">Задайте для него имя **NewEmployeeOrientation** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-195">Choose  **List**. Give it the name NewEmployeeOrientation, and then choose  **Add**.</span></span> 
 
7. <span data-ttu-id="fcd5e-196">На странице **Выберите параметры списка** в мастере настройки SharePoint оставьте заданное по умолчанию отображаемое имя списка **NewEmployeeOrientation**, нажмите кнопку **Создать настраиваемый шаблон списка и экземпляр списка на его основе** и в раскрывающемся списке выберите **По умолчанию (настраиваемый список)**. Затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-196">On the Choose List Settings page of the SharePoint Customization Wizard, leave the list display name at the default NewEmployeeOrientation, choose the Create a customizable list template and a list instance of it option button, and choose Default (Custom List) on the drop-down list. Then choose Finish.</span></span>

8. <span data-ttu-id="fcd5e-p121">Мастер создаст шаблон списка **NewEmployeeOrientation** с экземпляром дочернего списка под названием **NewEmployeeOrientationInstance**. При этом может открыться конструктор списков, который понадобится на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-p121">The wizard creates a **NewEmployeeOrientation** list template with a child list instance named **NewEmployeeOrientationInstance**. A list designer may open. It is used in a later step.</span></span>

9. <span data-ttu-id="fcd5e-200">Разверните узел **NewEmployeeOrientationInstance** в **обозревателе решений**, если вы еще не сделали этого, чтобы четко отличать файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка, от файла elements.xml, который представляет собой дочерний элемент *шаблона* списка.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-200">Expand the **NewEmployeeOrientationInstance** node in **Solution Explorer**, if it isn't already, so that you can clearly distinguish the elements.xml file that is a child of the list *instance* from the elements.xml file that is a child of the list *template*.</span></span>
    
    <span data-ttu-id="fcd5e-201">*Рис. 4. Узел списков в обозревателе решений*</span><span class="sxs-lookup"><span data-stu-id="fcd5e-201">*Lists node in Solution Explorer*</span></span>

    ![Содержимое папки с дочерним шаблоном NewEmployeeOrientation, у которого есть три дочерних элемента (NewEmployeeOrientationInstance, файл elements.xml и файл schema.xml). У экземпляра есть дочерний элемент elements.xml.](../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)

10. <span data-ttu-id="fcd5e-204">Откройте дочерний элемент elements.xml в шаблоне списка **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-204">Open the elements.xml child of the **NewEmployeeOrientation** list template.</span></span>

11. <span data-ttu-id="fcd5e-205">Измените значение атрибута **DisplayName** (не атрибута **Name**), чтобы имя стало более понятным: "Обучение новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="fcd5e-205">Add spaces to the DisplayName attribute (not the Name attribute) to make it friendlier: "New Employee Orientation".</span></span>

12. <span data-ttu-id="fcd5e-206">Задайте для атрибута **Description** значение "Сведения об адаптации новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="fcd5e-206">Set the **Description** attribute to "Orientation information about new employees."</span></span>

13. <span data-ttu-id="fcd5e-207">Оставьте для других атрибутов значения по умолчанию, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-207">Leave all other attributes at their default, save the file and close it.</span></span>

14. <span data-ttu-id="fcd5e-208">Если конструктор списков не открыт, выберите узел **NewEmployeeOrientation** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-208">If the list designer is not open, choose the  **NewEmployeeOrientation** node in **Solution Explorer**.</span></span>

15. <span data-ttu-id="fcd5e-209">Откройте вкладку **Список** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-209">Open the **List** tab of the designer.</span></span> <span data-ttu-id="fcd5e-210">Эта вкладка используется для установки определенных значений *экземпляра* (не *шаблона*) списка, но она содержит некоторые значения по умолчанию, унаследованные от шаблона.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-210">Open the  List tab of the designer. This tab is used to set certain values for the list *instance*  , not the list *template*  , but it has some default values that it inherited from the template.</span></span>

16. <span data-ttu-id="fcd5e-211">Замените значения на вкладке **Список** на следующие:</span><span class="sxs-lookup"><span data-stu-id="fcd5e-211">Change the values on this tab to the following:</span></span>
    
    -  <span data-ttu-id="fcd5e-212">**Заголовок**: "Новые сотрудники в Сиэтле".</span><span class="sxs-lookup"><span data-stu-id="fcd5e-212">**Title**: New Employees in Seattle</span></span>
    -  <span data-ttu-id="fcd5e-213">**URL-адрес списка**: Lists/NewEmployeesInSeattle.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-213">**List URL**: Lists/NewEmployeesInSeattle</span></span>
    -  <span data-ttu-id="fcd5e-214">**Описание**: "Новые сотрудники в Сиэтле".</span><span class="sxs-lookup"><span data-stu-id="fcd5e-214">**Description**: The new employees in Seattle.</span></span>

17. <span data-ttu-id="fcd5e-215">Оставьте установленные по умолчанию флажки и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-215">Leave the check boxes at their default status, save the file, and close the designer.</span></span>

18. <span data-ttu-id="fcd5e-216">В **обозревателе решений** может отображаться старое имя экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-216">The list instance may have its old name in **Solution Explorer**.</span></span> <span data-ttu-id="fcd5e-217">В таком случае откройте контекстное меню узла **NewEmployeeOrientationInstance**, выберите пункт **Переименовать** и измените имя на **NewEmployeesInSeattle**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-217">The list instance may have its old name in  **Solution Explorer**. If so, open the shortcut menu for  **NewEmployeeOrientationInstance**, choose  **Rename**, and change the name to NewEmployeesInSeattle.</span></span>

19. <span data-ttu-id="fcd5e-218">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-218">Open the schema.xml file.</span></span>

20. <span data-ttu-id="fcd5e-219">В элементе **View**, значение **BaseViewID** которого равно 0, замените имеющийся элемент **ViewFields** на приведенную ниже часть кода. Используйте именно этот GUID для параметра **FieldRef** с именем `Title`.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-219">In the  **View** element whose **BaseViewID** value is "0", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `Title`.)</span></span> <span data-ttu-id="fcd5e-220">В этом автоматически созданном файле schema.xml могут встречаться разрывы строк в странных местах.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-220">Line breaks may come at odd places in this autogenerated schema.xml file.</span></span> <span data-ttu-id="fcd5e-221">Убедитесь, что вы нашли соответствующие начальный и конечный теги элемента **ViewFields**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-221">Line breaks may come at odd places in this autogenerated schema.xml file. Be sure you have found the matching begin and end tags for the  **ViewFields** element. Add line breaks to improve readability.</span></span> <span data-ttu-id="fcd5e-222">Добавьте разрывы строк для удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-222">Add line breaks to improve readability.</span></span> 

    ```
      <ViewFields>
         <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
      </ViewFields>
    ```

21. <span data-ttu-id="fcd5e-223">Не закрывая файл schema.xml, в элементе **View**, значение **BaseViewID** которого равно 1, замените элемент **ViewFields** на приведенную ниже разметку. Используйте именно этот GUID для параметра **FieldRef** с именем `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-223">Still in the schema.xml file, in the  **View** element whose **BaseViewID** value is "1", replace the existing **ViewFields** element with the following markup. (Use exactly this GUID for the **FieldRef** named `LinkTitle`.)</span></span>
    
    ```
      <ViewFields>
         <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      </ViewFields>
    ```

22. <span data-ttu-id="fcd5e-224">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-224">Save and close the schema.xml file.</span></span>

23. <span data-ttu-id="fcd5e-225">Откройте файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка **NewEmployeesInSeattle** (а не *шаблона* списка **NewEmployeeOrientation**).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-225">Open the elements.xml file that is a child of the list  *instance* **NewEmployeesInSeattle** (not the elements.xml that is a child of the list *template* **NewEmployeeOrientation**).</span></span>

24. <span data-ttu-id="fcd5e-p126">В этом файле заполните список начальными данными. Для этого добавьте следующую разметку элемента **Data** в качестве дочернего элемента **ListInstance**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-p126">In this file, populate the list with some initial data. You do this by adding the following **Data** element markup as a child element of the **ListInstance** element.</span></span>
    
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

25. <span data-ttu-id="fcd5e-228">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-228">Save and close the file.</span></span>

26. <span data-ttu-id="fcd5e-229">В **обозревателе решений** дважды щелкните элемент **Компонент1**, чтобы открыть конструктор компонентов.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-229">In **Solution Explorer**, double-click **Feature1** to open the Feature designer.</span></span> <span data-ttu-id="fcd5e-230">В конструкторе задайте для параметра **Название** значение **Компоненты для адаптации новый сотрудников**, а для параметра **Описание** — значение **Списки и другие компоненты для адаптации сотрудников в компании**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-230">In Solution Explorer, double-click Feature1 to open the Feature designer. In the designer, set the Title to New Employee Orientation Components and set the Description to Lists and other components for getting employees oriented to the company. Save the file, and close the designer.</span></span> <span data-ttu-id="fcd5e-231">Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-231">Save the file and close the designer.</span></span>

27. <span data-ttu-id="fcd5e-232">Если элемент **Компонент1** в **обозревателе решений** не был переименован автоматически, откройте его контекстное меню, выберите пункт **Переименовать** и укажите имя **NewEmployeeOrientationComponents**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-232">If the  **Feature1** in **Solution Explorer** has not been automatically renamed, open its shortcut menu, choose **Rename**, and rename it NewEmployeeOrientationComponents.</span></span>

28. <span data-ttu-id="fcd5e-233">Откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-233">Open the Default.aspx file.</span></span>

29. <span data-ttu-id="fcd5e-234">Найдите элемент **Content** для ASP.NET с идентификатором **PlaceHolderPageTitleInTitleArea**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-234">Find the ASP.NET  **Content** element with the ID **PlaceHolderPageTitleInTitleArea**. Replace the default string "Page Title" with "New Employees by Location".</span></span> <span data-ttu-id="fcd5e-235">Замените стандартную строку **Заголовок страницы** на **Новые сотрудники по местонахождению**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-235">Replace the default string **Page Title** with **New Employees by Location**.</span></span>

30. <span data-ttu-id="fcd5e-236">Найдите элемент **Content** для ASP.NET с идентификатором **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-236">Find the ASP.NET **Content** element with the ID **PlaceHolderMain**.</span></span> <span data-ttu-id="fcd5e-237">*Замените* его содержимое на приведенную ниже разметку.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-237">*Replace* its contents with the following markup.</span></span> <span data-ttu-id="fcd5e-238">`_spPageContextInfo` — это объект JavaScript, который SharePoint автоматически включает на страницу.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-238">The `_spPageContextInfo` is a JavaScript object that SharePoint automatically includes on the page.</span></span> <span data-ttu-id="fcd5e-239">Его свойство `webAbsoluteUrl` возвращает URL-адрес сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-239">It's `webAbsoluteUrl` property returns the URL of the add-in web.</span></span>
    
    ```XML
        <p><asp:HyperLink runat="server" 
        NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="New Employees in Seattle" /></p>
    ```

<span data-ttu-id="fcd5e-240"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="fcd5e-240"></span></span>
## <a name="run-the-add-in-and-test-the-list"></a><span data-ttu-id="fcd5e-241">Запуск надстройки и тестирование списка</span><span class="sxs-lookup"><span data-stu-id="fcd5e-241">Run the add-in and test the list</span></span>

1. <span data-ttu-id="fcd5e-242">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-242">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="fcd5e-243">Visual Studio временно устанавливает надстройку на тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-243">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="fcd5e-244">Сведения о том, как пользователи запускают установленную надстройку SharePoint, см. в разделе [Дальнейшие действия](#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-244">(To find out how end users run an installed SharePoint Add-in, see [Next Steps](#Nextsteps).)</span></span>

2. <span data-ttu-id="fcd5e-245">Когда откроется страница надстройки по умолчанию, перейдите по ссылке **Новые сотрудники в Сиэтле**, чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-245">When the add-in's default page opens, choose the  **New Employees in Seattle** link to open the custom list instance.</span></span>
    
    <span data-ttu-id="fcd5e-246">*Рис. 5. Страница по умолчанию и страница представления списка*</span><span class="sxs-lookup"><span data-stu-id="fcd5e-246">*Default page and list view page*</span></span>

    ![Отображается страница по умолчанию надстройки, озаглавленная "Новые сотрудники по расположению". Ссылка "Новые сотрудники в Сиэтле". Стрелка от этой ссылки указывает на страницу списка. Она называется "Новые сотрудники в Сиэтле", список приведен ниже.](../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)

3. <span data-ttu-id="fcd5e-251">Добавьте и удалите элементы в списке.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-251">Add and delete items from the list.</span></span>

4. <span data-ttu-id="fcd5e-p132">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-p132">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

5. <span data-ttu-id="fcd5e-254">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-254">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="fcd5e-255">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-255">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fcd5e-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fcd5e-256">Additional resources</span></span>

- [<span data-ttu-id="fcd5e-257">Установка более ранних версий Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fcd5e-257">Install earlier versions of Visual Studio</span></span>](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx)
- [<span data-ttu-id="fcd5e-258">Документация по Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fcd5e-258">Visual Studio documentation</span></span>](https://docs.microsoft.com/ru-RU/visualstudio/)

## <a name="next-steps"></a><span data-ttu-id="fcd5e-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcd5e-259">Next steps</span></span>
<span data-ttu-id="fcd5e-260"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="fcd5e-260"></span></span>

<span data-ttu-id="fcd5e-261">На данный момент в списке мало сведений для адаптации сотрудников.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-261">So far, there isn't much orientation information in the list.</span></span> <span data-ttu-id="fcd5e-262">Мы добавим их в дальнейших статьях этой серии.</span><span class="sxs-lookup"><span data-stu-id="fcd5e-262">We'll add some in later articles in this series.</span></span> <span data-ttu-id="fcd5e-263">Но для начала ненадолго отвлечемся от написания кода, чтобы научиться развертывать надстройки SharePoint в статье [Развертывание и установка надстроек, размещаемых в SharePoint](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="fcd5e-263">So far, there isn't much orientation information in the list. We'll add some in later articles in this series. But first, take a brief break from coding to learn about deploying SharePoint Add-ins in  [Deploy and install a SharePoint-hosted SharePoint Add-in](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md).</span></span>
 
