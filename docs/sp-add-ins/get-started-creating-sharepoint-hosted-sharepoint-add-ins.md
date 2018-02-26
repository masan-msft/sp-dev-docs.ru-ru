---
title: "Знакомство с созданием надстроек SharePoint с размещением в SharePoint"
description: "Узнайте, как настроить среду разработки и создать свою первую надстройку SharePoint с размещением в SharePoint."
ms.date: 12/04/2017
ms.prod: sharepoint
ms.openlocfilehash: 35610e3d95841efa0d50c27e7b3751ff4f654bdf
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="get-started-creating-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="3a8d7-103">Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-103">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>

<span data-ttu-id="3a8d7-104">Надстройки с размещением в SharePoint — это один из двух основных типов надстроек SharePoint. Обзор надстроек SharePoint и этих основных типов см. в статье [Надстройки SharePoint](sharepoint-add-ins.md). Ниже представлен обзор надстроек с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-104">SharePoint-hosted add-ins are one of the two major types of SharePoint Add-ins. For an overview of SharePoint Add-ins and the two different types, see [SharePoint Add-ins](sharepoint-add-ins.md). Here's a summary of SharePoint-hosted add-ins:</span></span>

- <span data-ttu-id="3a8d7-105">Они содержат списки SharePoint, веб-части, рабочие процессы, пользовательские страницы и другие компоненты, каждый из которых установлен на дочернем сайте (сайте надстройки) того веб-сайта SharePoint, на котором установлена надстройка.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-105">They contain SharePoint lists, Web Parts, workflows, custom pages, and other components, all of which are installed on a subweb, called the add-in web, of the SharePoint website where the add-in is installed.</span></span>
- <span data-ttu-id="3a8d7-106">Единственный код, который они содержат, — JavaScript пользовательских страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-106">The only code they have is JavaScript on custom SharePoint pages.</span></span>

<span data-ttu-id="3a8d7-107">В этой статье описываются перечисленные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-107">In this article, you'll complete the following steps:</span></span>

- <span data-ttu-id="3a8d7-108">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-108">Set up your dev environment</span></span>
- <span data-ttu-id="3a8d7-109">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-109">Create the add-in project</span></span>
- <span data-ttu-id="3a8d7-110">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-110">Code your add-in</span></span>
- <span data-ttu-id="3a8d7-111">Запуск надстройки и тестирование списка</span><span class="sxs-lookup"><span data-stu-id="3a8d7-111">Run the add-in and test the list</span></span>

<span data-ttu-id="3a8d7-112"><a name="Setup"> </a></span><span class="sxs-lookup"><span data-stu-id="3a8d7-112"><a name="Setup"> </a></span></span>
## <a name="set-up-your-dev-environment"></a><span data-ttu-id="3a8d7-113">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-113">Set up your dev environment</span></span>

<span data-ttu-id="3a8d7-114">Существует множество способов настройки среды разработки для надстроек SharePoint. Здесь приведен самый простой из них.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-114">There are many ways to set up a development environment for SharePoint Add-ins. This section explains the simplest way.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="3a8d7-115">Получение инструментов</span><span class="sxs-lookup"><span data-stu-id="3a8d7-115">Get the tools</span></span>

- <span data-ttu-id="3a8d7-116">Если у вас еще не установлена среда **Visual Studio** 2013 или более поздней версии, установите ее согласно инструкциям на странице [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-116">If you don't already have **Visual Studio** 2013 or later installed, install it using the instructions at [Install Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="3a8d7-117">Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-117">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>

- <span data-ttu-id="3a8d7-118">Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-118">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="3a8d7-119">Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-119">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="3a8d7-120">Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-120">To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>

<span data-ttu-id="3a8d7-121">Сверяйтесь с [более ранними версиями Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) или другой [документацией по Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-121">Reference [earlier versions of Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) or other [Visual Studio documentation](https://docs.microsoft.com/ru-RU/visualstudio/).</span></span>

<span data-ttu-id="3a8d7-122"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="3a8d7-122"><a name="o365_signup"> </a></span></span>
### <a name="sign-up-for-an-office-365-developer-site"></a><span data-ttu-id="3a8d7-123">Получение шаблона "Сайт разработчика" для Office 365</span><span class="sxs-lookup"><span data-stu-id="3a8d7-123">Sign up for an Office 365 Developer Site</span></span>

> [!NOTE]
> <span data-ttu-id="3a8d7-124">Возможно, у вас уже есть доступ к шаблону "Сайт разработчика" для Office 365.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-124">You might already have access to an Office 365 Developer Site:</span></span>
> - <span data-ttu-id="3a8d7-p103">**Вы подписчик MSDN?** Visual Studio Ultimate и Visual Studio Premium с подпиской MSDN предоставляют льготное право на подписку разработчика приложений для Office 365. [Воспользуйтесь этим преимуществом прямо сегодня.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="3a8d7-p103">**Are you an MSDN subscriber?** Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. [Redeem your benefit today.](https://msdn.microsoft.com/subscriptions/manage/default.aspx)</span></span> 
> - <span data-ttu-id="3a8d7-128">**У вас есть один из указанных ниже планов подписки на Office 365?**</span><span class="sxs-lookup"><span data-stu-id="3a8d7-128">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="3a8d7-129">Если есть, администратор подписки на Office 365 может создать шаблон "Сайт разработчика" с помощью [Центра администрирования Office 365](https://portal.microsoftonline.com/admin/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-129">If so, an administrator of the Office 365 subscription can create a Developer Site by using the [Office 365 admin center](https://portal.microsoftonline.com/admin/default.aspx).</span></span> <span data-ttu-id="3a8d7-130">Дополнительные сведения см. в статье [Создание шаблона "Сайт разработчика" для существующей подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-130">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="3a8d7-131">Получить план Office 365 можно тремя способами:</span><span class="sxs-lookup"><span data-stu-id="3a8d7-131">There are three ways to get an Office 365 plan:</span></span> 

- <span data-ttu-id="3a8d7-132">Начните с [бесплатной 30-дневной пробной версии](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) с лицензией для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-132">Start with a  [free 30-day trial](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) with one user license.</span></span>

- <span data-ttu-id="3a8d7-133">Приобретите [подписку разработчика приложений для Office 365](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-133">Buy an [Office 365 developer subscription](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK).</span></span> 

- <span data-ttu-id="3a8d7-134">Зарегистрируйте учетную запись разработчика на один год по специальной программе для разработчиков Office 365.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-134">Sign up for a free, one-year Office 365 developer account through the Office 365 Developer Program.</span></span> <span data-ttu-id="3a8d7-135">Вы можете [узнать больше](http://dev.office.com/devprogram) или сразу заполнить [регистрационную форму](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-135">[Get more information](http://dev.office.com/devprogram), or go straight to [the sign-up form](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=14b845d0-938c-45af-b061-f798fbb4d170).</span></span> <span data-ttu-id="3a8d7-136">После регистрации в программе для разработчиков вы получите электронное сообщение со ссылкой для регистрации учетной записи разработчика.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-136">You'll get an email after you sign up for the developer program with a link to sign up for the developer account.</span></span> <span data-ttu-id="3a8d7-137">Следуйте приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-137">Use the following instructions.</span></span>

> [!TIP]
> <span data-ttu-id="3a8d7-138">Откройте страницы, на которые указывают эти ссылки, в новом окне или на новой вкладке, чтобы работать с ними было удобнее.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-138">Open these links in another window or tab to keep the following instructions handy.</span></span>

1. <span data-ttu-id="3a8d7-139">Первая страница регистрационной формы не требует объяснений. Укажите нужные сведения и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-139">The first page of the sign-up form is self-explanatory; supply the requested information, and then select **Next**.</span></span>

2. <span data-ttu-id="3a8d7-140">На второй странице (рис. 1) укажите ИД пользователя, принадлежащий администратору подписки.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-140">On the second page, shown in Figure 1, specify a user ID for the administrator of the subscription.</span></span>
   
   <span data-ttu-id="3a8d7-141">*Рис. 1. Доменное имя шаблона "Сайт разработчика" для Office 365*</span><span class="sxs-lookup"><span data-stu-id="3a8d7-141">*Figure 1. Office 365 Developer Site domain name*</span></span>

   ![Страница 2 формы для регистрации учетной записи Office 365](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
   
3. <span data-ttu-id="3a8d7-143">Создайте поддомен **.onmicrosoft.com**, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-143">Create a subdomain of **.onmicrosoft.com**; for example, contoso.onmicrosoft.com.</span></span>
    
   <span data-ttu-id="3a8d7-144">После регистрации необходимо войти на сайт портала Office 365, используемого для администрирования учетной записи, указав полученные учетные данные (в формате *ИД_пользователя@ваш_домен.onmicrosoft.com*).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-144">After you sign up, you use the resulting credentials (in the format *UserID@yourdomain.onmicrosoft.com*) to sign in to your Office 365 portal site where you administer your account.</span></span> <span data-ttu-id="3a8d7-145">Ваш "Сайт разработчика" для SharePoint Online будет настроен в новом домене — `http://yourdomain.sharepoint.com`.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-145">Your SharePoint Online Developer Site is set up at your new domain: `http://yourdomain.sharepoint.com`.</span></span>
    
4. <span data-ttu-id="3a8d7-146">Нажмите кнопку **Далее** и заполните последнюю страницу формы.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-146">Select **Next** and fill out the final page of the form.</span></span> <span data-ttu-id="3a8d7-147">Если вы хотите указать номер телефона, чтобы получить код подтверждения, можно ввести номер мобильного или стационарного телефона, но *не* номер VoIP.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-147">If you choose to provide a telephone number to get a confirmation code, you can provide a mobile or landline number, but *not* a VoIP (Voice over Internet Protocol) number.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="3a8d7-148">Если при попытке зарегистрировать учетную запись разработчика уже выполнен вход в другую учетную запись Майкрософт, может появиться сообщение "К сожалению, указанный вами ИД пользователя не работает.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-148">If you're signed in to another Microsoft account when you try to sign up for a developer account, you might see this message: "Sorry, that user ID you entered didn't work.</span></span> <span data-ttu-id="3a8d7-149">Возможно, он недействителен.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-149">It looks like it's not valid.</span></span> <span data-ttu-id="3a8d7-150">Убедитесь, что вы вводите ИД пользователя, назначенный вам организацией.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-150">Be sure you enter the user ID that your organization assigned to you.</span></span> <span data-ttu-id="3a8d7-151">Как правило, ИД пользователя представлен в формате *proverka@example.com* или *proverka@example.onmicrosoft.com*".</span><span class="sxs-lookup"><span data-stu-id="3a8d7-151">Your user ID usually looks like *someone@example.com* or *someone@example.onmicrosoft.com*."</span></span> 

   > <span data-ttu-id="3a8d7-152">Если появляется это сообщение, выйдите из используемой учетной записи Майкрософт и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-152">If you see that message, sign out of the Microsoft account you were using and try again.</span></span> <span data-ttu-id="3a8d7-153">Если сообщение продолжает отображаться, очистите кэш браузера или переключитесь в режим **просмотра InPrivate**, а затем заполните форму.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-153">If you still get the message, clear your browser cache or switch to **InPrivate Browsing** and then fill out the form.</span></span>

   <span data-ttu-id="3a8d7-154">По завершении регистрации в браузере откроется страница установки Office 365.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-154">After you finish the sign-up process, your browser opens the Office 365 installation page.</span></span> <span data-ttu-id="3a8d7-155">Щелкните значок администратора, чтобы открыть страницу центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-155">Select the Admin icon to open the admin center page.</span></span>

   <span data-ttu-id="3a8d7-156">*Рис. 2. Страница Центра администрирования Office 365*</span><span class="sxs-lookup"><span data-stu-id="3a8d7-156">*Figure 2. Office 365 admin center page*</span></span>

   ![Снимок экрана с изображением Центра администрирования Office 365.](../images/SP15_Office365AdminInset_border.png)
 
5. <span data-ttu-id="3a8d7-p111">Подождите, пока завершится настройка шаблона "Сайт разработчика". После этого обновите страницу центра администрирования в браузере.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-p111">Wait for your Developer Site to finish setting up. After provisioning is complete, refresh the admin center page in your browser.</span></span>

6. <span data-ttu-id="3a8d7-160">Перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть "Сайт разработчика".</span><span class="sxs-lookup"><span data-stu-id="3a8d7-160">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="3a8d7-161">Открывшийся сайт должен выглядеть так, как показано на рис. 3.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-161">You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="3a8d7-162">Наличие на странице списка **Тестируемые надстройки** подтверждает, что веб-сайт был создан с помощью шаблона "Сайт разработчика" SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-162">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="3a8d7-163">Если вместо этого отображается обычный сайт группы, подождите несколько минут и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-163">If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>

7. <span data-ttu-id="3a8d7-164">Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-164">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>

   <span data-ttu-id="3a8d7-165">*Рис. 3. Домашняя страница сайта разработчика со списком "Тестируемые надстройки"*</span><span class="sxs-lookup"><span data-stu-id="3a8d7-165">*Figure 3. Your Developer Site home page with the Add-ins in Testing list*</span></span>

   ![Снимок экрана с изображением домашней страницы шаблона "Сайт разработчика".](../images/SP15_DeveloperSiteHome_border.png)

<span data-ttu-id="3a8d7-167"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="3a8d7-167"><a name="Create"> </a></span></span>
## <a name="create-the-add-in-project"></a><span data-ttu-id="3a8d7-168">Создание проекта надстройки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-168">Create the add-in project</span></span>

1. <span data-ttu-id="3a8d7-169">Запустите Visual Studio, выбрав команду **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-169">Start Visual Studio by using the **Run as administrator** option.</span></span>

2. <span data-ttu-id="3a8d7-170">В Visual Studio выберите пункты **Файл** > **Создать** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-170">In Visual Studio, select **File** > **New** > **New Project**.</span></span>
 
3. <span data-ttu-id="3a8d7-171">В диалоговом окне **Новый проект** последовательно разверните узлы **Visual C#** и **Office/SharePoint**, а затем выберите элементы **Надстройки** > **Надстройка для SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-171">In the **New Project** dialog box, expand the **Visual C#** node, expand the **Office/SharePoint** node, and then select **Add-ins** > **Add-in for SharePoint**.</span></span>

4. <span data-ttu-id="3a8d7-172">Присвойте проекту имя **EmployeeOrientation**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-172">Name the project **EmployeeOrientation**, and then select **OK**.</span></span>

5. <span data-ttu-id="3a8d7-173">В диалоговом окне **Настройка параметров надстроек SharePoint** укажите полный URL-адрес сайта SharePoint, который требуется использовать для отладки надстройки.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-173">In the **Specify the Add-in for SharePoint Settings** dialog box, provide the full URL of the SharePoint site that you want to use to debug your add-in.</span></span> <span data-ttu-id="3a8d7-174">Это URL-адрес сайта разработчика.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-174">This is the URL of the Developer Site.</span></span> <span data-ttu-id="3a8d7-175">Используйте в URL-адресе протокол HTTPS, а не HTTP. В разделе **Как требуется разместить надстройку SharePoint?**, выберите **Размещено в SharePoint**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-175">(Use HTTPS, not HTTP in the URL.) Under **How do you want to host your SharePoint Add-in**, select  **SharePoint-hosted**, and then select **Finish**.</span></span>

6. <span data-ttu-id="3a8d7-176">Вам может быть предложено войти на сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-176">You may be prompted to sign in to your Developer Site.</span></span> <span data-ttu-id="3a8d7-177">В таком случае используйте учетные данные администратора подписки.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-177">If so, use your subscription administrator's credentials.</span></span>

7. <span data-ttu-id="3a8d7-178">После создания проекта откройте файл **/Pages/Default.aspx** из корневой папки проекта.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-178">After the project is created, open the file **/Pages/Default.aspx** from the root of the project.</span></span> <span data-ttu-id="3a8d7-179">Помимо прочего, этот созданный файл загружает один или оба сценария, размещенные в SharePoint: sp.runtime.js и sp.js.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-179">Among other things, this generated file loads one or both of two scripts that are hosted on SharePoint: sp.runtime.js and sp.js.</span></span> <span data-ttu-id="3a8d7-180">Разметку для загрузки этих файлов можно найти в элементе управления **Content** в верхней части файла с идентификатором **PlaceHolderAdditionalPageHead**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-180">The markup for loading these files is in the **Content** control near the top of the file that has the ID **PlaceHolderAdditionalPageHead**.</span></span> <span data-ttu-id="3a8d7-181">Разметка зависит от используемой версии **Инструментов разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-181">The markup varies depending on the version of **Microsoft Office Developer Tools for Visual Studio** that you are using.</span></span> <span data-ttu-id="3a8d7-182">В руководствах из этой серии необходимо загружать оба файла с обычными HTML-тегами **\<script\>**, а не с тегами **\<SharePoint:ScriptLink\>**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-182">This series of tutorials requires that both files be loaded and that they be loaded with ordinary HTML **\<script\>** tags, not **\<SharePoint:ScriptLink\>** tags.</span></span> 

    <span data-ttu-id="3a8d7-183">Убедитесь, что указанные ниже строки присутствуют в элементе управления **PlaceHolderAdditionalPageHead** *над* строкой `<meta name="WebPartPageExpansion" content="full" />`.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-183">Ensure that the following lines are in the **PlaceHolderAdditionalPageHead** control, *just above*  the line `<meta name="WebPartPageExpansion" content="full" />`:</span></span>
    
    ```
      <script type="text/javascript" src="/_layouts/15/sp.runtime.js"></script> 
      <script type="text/javascript" src="/_layouts/15/sp.js"></script> 
    ```

8. <span data-ttu-id="3a8d7-184">Проверьте файл на наличие другой разметки, загружающей один или оба файла сценариев, и удалите ее.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-184">Search the file for any other markup that also loads one or the other of these files and remove the redundant markup.</span></span> <span data-ttu-id="3a8d7-185">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-185">Save and close the file.</span></span>

<span data-ttu-id="3a8d7-186"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="3a8d7-186"><a name="Code"> </a></span></span>
## <a name="code-your-add-in"></a><span data-ttu-id="3a8d7-187">Написание кода надстройки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-187">Code your add-in</span></span>

<span data-ttu-id="3a8d7-188">Для вашей первой надстройки SharePoint с размещением в SharePoint мы включим классическое расширение SharePoint: настраиваемый список и его экземпляр.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-188">For your first SharePoint-hosted SharePoint Add-in, we'll include the classic SharePoint extension: a custom list and list instance.</span></span>

1. <span data-ttu-id="3a8d7-189">В **обозревателе решений** откройте файл AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-189">In **Solution Explorer**, open the AppManifest.xml file.</span></span>

2. <span data-ttu-id="3a8d7-190">Когда откроется конструктор манифеста, измените значение в поле **Title**, на **Адаптация сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-190">When the manifest designer opens, add a space between the words in the **Title** field so that it reads **Employee Orientation**.</span></span> <span data-ttu-id="3a8d7-191">*Не* меняйте значение в поле **Name**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-191">(Do  *not* change the **Name** field.)</span></span>

3. <span data-ttu-id="3a8d7-192">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-192">Save and close the file.</span></span>

4. <span data-ttu-id="3a8d7-193">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункты **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-193">Right-click the project in **Solution Explorer** and select **Add** > **New Folder**.</span></span> <span data-ttu-id="3a8d7-194">Назовите папку Lists.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-194">Name the folder Lists.</span></span>

5. <span data-ttu-id="3a8d7-195">Щелкните новую папку правой кнопкой мыши и выберите пункты **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-195">Right-click the new folder and select **Add** > **New Item**.</span></span> <span data-ttu-id="3a8d7-196">В узле **Office/SharePoint** откроется диалоговое окно **Добавление нового элемента**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-196">The **Add New Item** dialog opens to the **Office/SharePoint** node.</span></span>

6. <span data-ttu-id="3a8d7-197">Выберите **Список**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-197">Select **List**.</span></span> <span data-ttu-id="3a8d7-198">Задайте для него имя **NewEmployeeOrientation** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-198">Give it the name **NewEmployeeOrientation**, and then select **Add**.</span></span> 
 
7. <span data-ttu-id="3a8d7-199">На странице **Выберите параметры списка** в мастере настройки SharePoint оставьте заданное по умолчанию отображаемое имя списка **NewEmployeeOrientation**, нажмите кнопку **Создать настраиваемый шаблон списка и экземпляр списка на его основе** и в раскрывающемся списке выберите **По умолчанию (настраиваемый список)**. Затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-199">On the **Choose List Settings** page of the SharePoint Customization Wizard, leave the list display name at the default **NewEmployeeOrientation**, select the **Create a customizable list template and a list instance of it** option button, select **Default (Custom List)** on the drop-down list, and then select **Finish**.</span></span>

8. <span data-ttu-id="3a8d7-p121">Мастер создаст шаблон списка **NewEmployeeOrientation** с экземпляром дочернего списка под названием **NewEmployeeOrientationInstance**. При этом может открыться конструктор списков, который понадобится на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-p121">The wizard creates a **NewEmployeeOrientation** list template with a child list instance named **NewEmployeeOrientationInstance**. A list designer may open. It is used in a later step.</span></span>

9. <span data-ttu-id="3a8d7-203">Разверните узел **NewEmployeeOrientationInstance** в **обозревателе решений**, если вы еще не сделали этого, чтобы четко отличать файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка, от файла elements.xml, который представляет собой дочерний элемент *шаблона* списка.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-203">Expand the **NewEmployeeOrientationInstance** node in **Solution Explorer**, if it isn't already, so that you can clearly distinguish the elements.xml file that is a child of the list *instance* from the elements.xml file that is a child of the list *template*.</span></span>
    
    <span data-ttu-id="3a8d7-204">*Рис. 4. Узел списков в обозревателе решений*</span><span class="sxs-lookup"><span data-stu-id="3a8d7-204">*Figure 4. Lists node in Solution Explorer*</span></span>

    ![Содержимое папки с дочерним шаблоном NewEmployeeOrientation, у которого есть три дочерних элемента (NewEmployeeOrientationInstance, файл elements.xml и файл schema.xml). У экземпляра есть дочерний элемент elements.xml.](../images/10e5d116-d24b-4a44-bfff-cfbf2f971b1e.PNG)

10. <span data-ttu-id="3a8d7-207">Откройте дочерний элемент elements.xml в шаблоне списка **NewEmployeeOrientation**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-207">Open the elements.xml child of the **NewEmployeeOrientation** list template.</span></span>

11. <span data-ttu-id="3a8d7-208">Измените значение атрибута **DisplayName** (не атрибута **Name**), чтобы имя стало более понятным: "Обучение новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="3a8d7-208">Add spaces to the **DisplayName** attribute (not the **Name** attribute) to make it friendlier: "New Employee Orientation."</span></span>

12. <span data-ttu-id="3a8d7-209">Задайте для атрибута **Description** значение "Сведения об адаптации новых сотрудников".</span><span class="sxs-lookup"><span data-stu-id="3a8d7-209">Set the **Description** attribute to "Orientation information about new employees."</span></span>

13. <span data-ttu-id="3a8d7-210">Оставьте для других атрибутов значения по умолчанию, а затем сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-210">Leave all other attributes at their default, save the file, and close it.</span></span>

14. <span data-ttu-id="3a8d7-211">Если конструктор списков не открыт, выберите узел **NewEmployeeOrientation** в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-211">If the list designer is not open, select the **NewEmployeeOrientation** node in **Solution Explorer**.</span></span>

15. <span data-ttu-id="3a8d7-212">Откройте вкладку **Список** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-212">Open the **List** tab of the designer.</span></span> <span data-ttu-id="3a8d7-213">Эта вкладка используется для установки определенных значений *экземпляра* (не *шаблона*) списка, но она содержит некоторые значения по умолчанию, унаследованные от шаблона.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-213">This tab is used to set certain values for the list *instance*, not the list *template*, but it has some default values that it inherited from the template.</span></span>

16. <span data-ttu-id="3a8d7-214">Замените значения на вкладке **Список** на следующие:</span><span class="sxs-lookup"><span data-stu-id="3a8d7-214">Change the values on the **List** tab to the following:</span></span>
    
    -  <span data-ttu-id="3a8d7-215">**Заголовок**: "Новые сотрудники в Сиэтле".</span><span class="sxs-lookup"><span data-stu-id="3a8d7-215">**Title**: New Employees in Seattle</span></span>
    -  <span data-ttu-id="3a8d7-216">**URL-адрес списка**: Lists/NewEmployeesInSeattle.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-216">**List URL**: Lists/NewEmployeesInSeattle</span></span>
    -  <span data-ttu-id="3a8d7-217">**Описание**: "Новые сотрудники в Сиэтле".</span><span class="sxs-lookup"><span data-stu-id="3a8d7-217">**Description**: The new employees in Seattle</span></span>

17. <span data-ttu-id="3a8d7-218">Оставьте установленные по умолчанию флажки и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-218">Leave the check boxes at their default status, save the file, and then close the designer.</span></span>

18. <span data-ttu-id="3a8d7-219">В **обозревателе решений** может отображаться старое имя экземпляра списка.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-219">The list instance may have its old name in **Solution Explorer**.</span></span> <span data-ttu-id="3a8d7-220">В таком случае откройте контекстное меню узла **NewEmployeeOrientationInstance**, выберите пункт **Переименовать** и измените имя на **NewEmployeesInSeattle**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-220">If so, open the shortcut menu for **NewEmployeeOrientationInstance**, select **Rename**, and change the name to **NewEmployeesInSeattle**.</span></span>

19. <span data-ttu-id="3a8d7-221">Откройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-221">Open the schema.xml file.</span></span>

20. <span data-ttu-id="3a8d7-222">В элементе **View**, значение **BaseViewID** которого равно 0, замените имеющийся элемент **ViewFields** на приведенную ниже часть кода. Используйте именно этот GUID для параметра **FieldRef** с именем `Title`.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-222">In the **View** element whose **BaseViewID** value is "0", replace the existing **ViewFields** element with the following markup (use exactly this GUID for the **FieldRef** named `Title`).</span></span> <span data-ttu-id="3a8d7-223">В этом автоматически созданном файле schema.xml могут встречаться разрывы строк в странных местах.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-223">Line breaks may come at odd places in this autogenerated schema.xml file.</span></span> <span data-ttu-id="3a8d7-224">Убедитесь, что вы нашли соответствующие начальный и конечный теги элемента **ViewFields**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-224">Be sure you have found the matching begin and end tags for the **ViewFields** element.</span></span> <span data-ttu-id="3a8d7-225">Добавьте разрывы строк для удобочитаемости.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-225">Add line breaks to improve readability.</span></span> 

    ```
      <ViewFields>
         <FieldRef Name="Title" ID="{fa564e0f-0c70-4ab9-b863-0177e6ddd247}" DisplayName="Employee" />
      </ViewFields>
    ```

21. <span data-ttu-id="3a8d7-226">Не закрывая файл schema.xml, в элементе **View**, значение **BaseViewID** которого равно 1, замените элемент **ViewFields** на приведенную ниже разметку. Используйте именно этот GUID для параметра **FieldRef** с именем `LinkTitle`.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-226">Still in the schema.xml file, in the **View** element whose **BaseViewID** value is "1", replace the existing **ViewFields** element with the following markup (use exactly this GUID for the **FieldRef** named `LinkTitle`).</span></span>
    
    ```
      <ViewFields>
         <FieldRef Name="LinkTitle" ID="{82642ec8-ef9b-478f-acf9-31f7d45fbc31}" DisplayName="Employee" />
      </ViewFields>
    ```

22. <span data-ttu-id="3a8d7-227">Сохраните и закройте файл schema.xml.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-227">Save and close the schema.xml file.</span></span>

23. <span data-ttu-id="3a8d7-228">Откройте файл elements.xml, который представляет собой дочерний элемент *экземпляра* списка **NewEmployeesInSeattle** (а не *шаблона* списка **NewEmployeeOrientation**).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-228">Open the elements.xml file that is a child of the list *instance* **NewEmployeesInSeattle** (not the elements.xml that is a child of the list *template* **NewEmployeeOrientation**).</span></span>

24. <span data-ttu-id="3a8d7-p126">В этом файле заполните список начальными данными. Для этого добавьте следующую разметку элемента **Data** в качестве дочернего элемента **ListInstance**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-p126">In this file, populate the list with some initial data. You do this by adding the following **Data** element markup as a child element of the **ListInstance** element.</span></span>
    
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

25. <span data-ttu-id="3a8d7-231">Сохраните и закройте файл.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-231">Save and close the file.</span></span>

26. <span data-ttu-id="3a8d7-232">В **обозревателе решений** дважды щелкните элемент **Компонент1**, чтобы открыть конструктор компонентов.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-232">In **Solution Explorer**, double-click **Feature1** to open the Feature designer.</span></span> <span data-ttu-id="3a8d7-233">В конструкторе задайте для параметра **Название** значение **Компоненты для адаптации новый сотрудников**, а для параметра **Описание** — значение **Списки и другие компоненты для адаптации сотрудников в компании**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-233">In the designer, set the **Title** to **New Employee Orientation Components** and set the **Description** to **Lists and other components for getting employees oriented to the company**.</span></span> <span data-ttu-id="3a8d7-234">Сохраните файл и закройте конструктор.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-234">Save the file, and then close the designer.</span></span>

27. <span data-ttu-id="3a8d7-235">Если элемент **Компонент1** в **обозревателе решений** не был переименован автоматически, откройте его контекстное меню, выберите пункт **Переименовать** и укажите имя **NewEmployeeOrientationComponents**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-235">If the **Feature1** in **Solution Explorer** has not been automatically renamed, open its shortcut menu, select **Rename**, and rename it to **NewEmployeeOrientationComponents**.</span></span>

28. <span data-ttu-id="3a8d7-236">Откройте файл Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-236">Open the Default.aspx file.</span></span>

29. <span data-ttu-id="3a8d7-237">Найдите элемент **Content** для ASP.NET с идентификатором **PlaceHolderPageTitleInTitleArea**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-237">Find the ASP.NET **Content** element with the ID **PlaceHolderPageTitleInTitleArea**.</span></span> <span data-ttu-id="3a8d7-238">Замените стандартную строку **Заголовок страницы** на **Новые сотрудники по местонахождению**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-238">Replace the default string **Page Title** with **New Employees by Location**.</span></span>

30. <span data-ttu-id="3a8d7-239">Найдите элемент **Content** для ASP.NET с идентификатором **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-239">Find the ASP.NET **Content** element with the ID **PlaceHolderMain**.</span></span> <span data-ttu-id="3a8d7-240">*Замените* его содержимое на приведенную ниже разметку.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-240">*Replace* its contents with the following markup.</span></span> <span data-ttu-id="3a8d7-241">`_spPageContextInfo` — это объект JavaScript, который SharePoint автоматически включает на страницу.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-241">The `_spPageContextInfo` is a JavaScript object that SharePoint automatically includes on the page.</span></span> <span data-ttu-id="3a8d7-242">Его свойство `webAbsoluteUrl` возвращает URL-адрес сайта надстройки.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-242">It's `webAbsoluteUrl` property returns the URL of the add-in web.</span></span>
    
    ```XML
        <p><asp:HyperLink runat="server" 
        NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="New Employees in Seattle" /></p>
    ```

<span data-ttu-id="3a8d7-243"><a name="Code"> </a></span><span class="sxs-lookup"><span data-stu-id="3a8d7-243"><a name="Code"> </a></span></span>
## <a name="run-the-add-in-and-test-the-list"></a><span data-ttu-id="3a8d7-244">Запуск надстройки и тестирование списка</span><span class="sxs-lookup"><span data-stu-id="3a8d7-244">Run the add-in and test the list</span></span>

1. <span data-ttu-id="3a8d7-245">Нажмите клавишу F5, чтобы развернуть и запустить надстройку.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-245">Use the F5 key to deploy and run your add-in.</span></span> <span data-ttu-id="3a8d7-246">Visual Studio временно устанавливает надстройку на тестовом сайте SharePoint и сразу же запускает ее.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-246">Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> <span data-ttu-id="3a8d7-247">Сведения о том, как пользователи запускают установленную надстройку SharePoint, см. в разделе [Дальнейшие действия](#Nextsteps).</span><span class="sxs-lookup"><span data-stu-id="3a8d7-247">(To find out how end users run an installed SharePoint Add-in, see [Next Steps](#Nextsteps).)</span></span>

2. <span data-ttu-id="3a8d7-248">Когда откроется страница надстройки по умолчанию, перейдите по ссылке **Новые сотрудники в Сиэтле**, чтобы открыть экземпляр настраиваемого списка.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-248">When the add-in's default page opens, select the **New Employees in Seattle** link to open the custom list instance.</span></span>
    
    <span data-ttu-id="3a8d7-249">*Рис. 5. Страница по умолчанию и страница представления списка*</span><span class="sxs-lookup"><span data-stu-id="3a8d7-249">*Figure 5. Default page and list view page*</span></span>

    ![Отображается страница по умолчанию надстройки, озаглавленная "Новые сотрудники по расположению". Ссылка "Новые сотрудники в Сиэтле". Стрелка от этой ссылки указывает на страницу списка. Она называется "Новые сотрудники в Сиэтле", список приведен ниже.](../images/9dc5cefe-083a-4807-bee6-473001f23db9.png)

3. <span data-ttu-id="3a8d7-254">Добавьте и удалите элементы в списке.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-254">Add and delete items from the list.</span></span>

4. <span data-ttu-id="3a8d7-p132">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-p132">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>

5. <span data-ttu-id="3a8d7-257">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуем отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-257">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are finished working with it for a while.</span></span> <span data-ttu-id="3a8d7-258">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-258">Right-click the project in **Solution Explorer**, and select **Retract**.</span></span>

<span data-ttu-id="3a8d7-259"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="3a8d7-259"><a name="Nextsteps"> </a></span></span>
## <a name="next-steps"></a><span data-ttu-id="3a8d7-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a8d7-260">Next steps</span></span>

<span data-ttu-id="3a8d7-261">Чтобы создавать надстройки, выполняйте перечисленные ниже действия в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="3a8d7-261">To create your add-ins, walk through the following steps in this order:</span></span>

1.  [<span data-ttu-id="3a8d7-262">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-262">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
2.  [<span data-ttu-id="3a8d7-263">Добавление настраиваемых столбцов в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-263">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
3.  [<span data-ttu-id="3a8d7-264">Добавление настраиваемого типа контента в надстройку с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-264">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)
4.  [<span data-ttu-id="3a8d7-265">Добавление веб-части на страницу в надстройке SharePoint, размещаемой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-265">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
5.  [<span data-ttu-id="3a8d7-266">Добавление рабочего процесса в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-266">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
6.  [<span data-ttu-id="3a8d7-267">Добавление настраиваемой страницы и стиля для надстройки с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-267">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)
7.  [<span data-ttu-id="3a8d7-268">Добавление настраиваемой функции отрисовки в клиенте в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-268">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in.md)
8.  [<span data-ttu-id="3a8d7-269">Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-269">Create a custom ribbon button in the host web of a SharePoint Add-in</span></span>](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md)
9.  [<span data-ttu-id="3a8d7-270">Использование API JavaScript для SharePoint для работы с данными SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a8d7-270">Use the SharePoint JavaScript APIs to work with SharePoint data</span></span>](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md)
10. [<span data-ttu-id="3a8d7-271">Работа с данными хост-сайта из JavaScript на сайте надстройки</span><span class="sxs-lookup"><span data-stu-id="3a8d7-271">Work with host web data from JavaScript in the add-in web</span></span>](work-with-host-web-data-from-javascript-in-the-add-in-web.md)


