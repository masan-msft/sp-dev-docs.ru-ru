---
title: "Развертывание Office 365 сайты разработки в Microsoft Azure #"
ms.date: 11/03/2017
ms.openlocfilehash: c7e975f54da33125d6e8261efa1b525ba525747d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="deploying-development-office-365-sites-to-microsoft-azure"></a><span data-ttu-id="1ee28-102">Развертывание Office 365 сайты разработки в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1ee28-102">Deploying Development Office 365 Sites to Microsoft Azure</span></span> #

### <a name="summary"></a><span data-ttu-id="1ee28-103">Summary</span><span class="sxs-lookup"><span data-stu-id="1ee28-103">Summary</span></span> ###

<span data-ttu-id="1ee28-104">При разработке любой тип веб-приложения, разработка для большинства выполняется локально с помощью http://localhost.</span><span class="sxs-lookup"><span data-stu-id="1ee28-104">When developing any type a web application, most development is done locally using http://localhost.</span></span> <span data-ttu-id="1ee28-105">Некоторые проекты использовать локальные ресурсы или сочетание локальных и удаленных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1ee28-105">Some projects use local resources or a mix of local and remote resources.</span></span> <span data-ttu-id="1ee28-106">Использование таких проектов из среды разработки локального включает в себя небольшое количество задачи, выполняемые как изменение строки подключения базы данных, URL-адреса, конфигурации, и т.д.</span><span class="sxs-lookup"><span data-stu-id="1ee28-106">Taking these projects from local development environments involves a handful of tasks to perform like changing database connection strings, URLs, configurations, etc.</span></span>

<span data-ttu-id="1ee28-107">Веб-проектов, использующих возможности API-интерфейсы Office 365, практически не отличаются.</span><span class="sxs-lookup"><span data-stu-id="1ee28-107">Web projects that leverage the Office 365 APIs are no different.</span></span> <span data-ttu-id="1ee28-108">Эти проекты используют службы Azure AD корпорации Майкрософт для проверки подлинности приложений и получения маркера доступа OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="1ee28-108">These projects leverage Microsoft's Azure AD service to authenticate the applications and obtain OAuth 2.0 access tokens.</span></span> <span data-ttu-id="1ee28-109">Эти маркеры используются веб-приложений для проверки подлинности с помощью интерфейсов API Office 365.</span><span class="sxs-lookup"><span data-stu-id="1ee28-109">These tokens are used by the web applications to authenticate with the Office 365 APIs.</span></span>

<span data-ttu-id="1ee28-110">На этой странице Описание действий, необходимых для создания заметок в проект разработки Office 365 API и запуска его примеры размещенных полностью в Microsoft Azure с использованием [Office 365](http://products.office.com/en-us/business/explore-office-365-for-business), [Azure Active Directory](http://azure.microsoft.com/en-us/services/active-directory/) & [Azure веб-сайтов] (http:// Azure.Microsoft.com/en-US/Services/WebSites/.</span><span class="sxs-lookup"><span data-stu-id="1ee28-110">This page explains the steps involved in taking an Office 365 API development project and launching it to a working sample hosted entirely in Microsoft Azure using [Office 365](http://products.office.com/en-us/business/explore-office-365-for-business), [Azure Active Directory](http://azure.microsoft.com/en-us/services/active-directory/) & [Azure Websites](http://azure.microsoft.com/en-us/services/websites/.</span></span>

<span data-ttu-id="1ee28-111">Развертывание Office 365 API веб-приложения в Microsoft Azure из среды разработки локального требуются три основных действия нужно выполнить, как описано на этой странице:</span><span class="sxs-lookup"><span data-stu-id="1ee28-111">Deploying an Office 365 API web application to Microsoft Azure from a local development environment requires three high-level steps to be performed as outlined in this page:</span></span>

- [<span data-ttu-id="1ee28-112">Создание и настройка веб-сайта Azure</span><span class="sxs-lookup"><span data-stu-id="1ee28-112">Create and Configure an Azure Website</span></span>](#create-and-configure-an-azure-website)
- [<span data-ttu-id="1ee28-113">Настройка приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ee28-113">Configure the Azure AD Application</span></span>](#configure-the-azure-ad-application)
- [<span data-ttu-id="1ee28-114">Настройка проекта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ee28-114">Configure the ASP.NET Project</span></span>](#configure-the-aspnet-project)
- [<span data-ttu-id="1ee28-115">Развертывание Office 365 API веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ee28-115">Deploy the Office 365 API ASP.NET Web Application</span></span>](#deploy-the-office-365-api-aspnet-web-application)

> <span data-ttu-id="1ee28-116">На этой странице предполагается, что локальное приложение ASP.NET работа с использованием API Office 365.</span><span class="sxs-lookup"><span data-stu-id="1ee28-116">This page assumes that you have a local working ASP.NET application that uses the Office 365 APIs.</span></span> <span data-ttu-id="1ee28-117">Для ссылки он будет использовать project **[O365 WebApp SingleTenant](https://github.com/SharePoint/O365-WebApp-SingleTenant)** , обнаруженных в учетной записи **[разработчик офисных решений](https://github.com/SharePoint)** в репозиториев.</span><span class="sxs-lookup"><span data-stu-id="1ee28-117">For reference, it will use the **[O365-WebApp-SingleTenant](https://github.com/SharePoint/O365-WebApp-SingleTenant)** project found in the **[OfficeDev](https://github.com/SharePoint)** account in GitHub.</span></span>

# <a name="create-and-configure-an-azure-website"></a><span data-ttu-id="1ee28-118">Создание и настройка веб-сайта Azure</span><span class="sxs-lookup"><span data-stu-id="1ee28-118">Create and Configure an Azure Website</span></span>

<span data-ttu-id="1ee28-119">На этом этапе создается Azure веб-сайт, который будет использоваться для размещения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1ee28-119">In this step you will create an Azure website that will be used to host the web application.</span></span> 

1. <span data-ttu-id="1ee28-120">Перейдите к странице [Портала управления Azure](https://manage.windowsazure.com) и входа в систему с помощью учетной записи идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="1ee28-120">Navigate to the [Azure Management Portal](https://manage.windowsazure.com) and login using your Organization ID account.</span></span>
1. <span data-ttu-id="1ee28-121">После входа, в боковой панели навигации выберите **веб-САЙТОВ**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-121">After logging in, using the navigation sidebar, select **WEBSITES**.</span></span>
1. <span data-ttu-id="1ee28-122">На странице " **веб-сайтов** " щелкните ссылку **Создать** в нижнем колонтитуле, обнаруженных в левом нижнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="1ee28-122">On the **websites** page, click the **NEW** link in the footer found in the lower-left corner of the page.</span></span>
1. <span data-ttu-id="1ee28-123">В окне мастера выберите **Быстрое создание**, введите имя для сайта в поле **URL-адрес** , выберите **Размещение планирование Web** и **подписки**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-123">In the wizard that appears, select **Quick Create**, enter a name for the site in the **URL** field, select a **Web Hosting Plan** and **Subscription**.</span></span> 

  ![Параметры быстрого создания: поле URL-адрес имеет значение o365api-01, Web размещения планирование задано значение Default1 (Восточный США, стандартный) подписки задано значение Azure MSDN (основной).](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-01.png)

  > <span data-ttu-id="1ee28-125">Убедитесь, что хранить сообщения с именем веб-сайта, которые создаются как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="1ee28-125">Make sure to keep a note of the name of the website you create as it will be needed later.</span></span>

1. <span data-ttu-id="1ee28-126">И, наконец, щелкните ссылку **Создать веб-сайт** для создания сайта.</span><span class="sxs-lookup"><span data-stu-id="1ee28-126">Finally click the **Create Website** link to create the site.</span></span>

<span data-ttu-id="1ee28-127">Предоставление Azure в некоторое время для создания сайта.</span><span class="sxs-lookup"><span data-stu-id="1ee28-127">Give Azure a few moments to create the site.</span></span> <span data-ttu-id="1ee28-128">После создания сайта можно указать *Параметры приложения* с помощью веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1ee28-128">After creating the site you can specify *app settings* through the web interface.</span></span> <span data-ttu-id="1ee28-129">Это позволяет изменить любой `<appSettings>` в рамках проекта `web.config` файл в веб-интерфейсе администрирования для веб-сайта без развертывания веб-узла базы кода для простой `web.config` изменений.</span><span class="sxs-lookup"><span data-stu-id="1ee28-129">This allows you to override any `<appSettings>` within the project's `web.config` file through the web administration interface for the website without deploying your site codebase for simple `web.config` changes.</span></span>

1. <span data-ttu-id="1ee28-130">Выберите веб-сайт, который вы только что создали **Портала управления Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-130">Click the website that you just created within the **Azure Management Portal**.</span></span>
1. <span data-ttu-id="1ee28-131">Щелкните ссылку **НАСТРОИТЬ** в верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="1ee28-131">CLick the **CONFIGURE** link in the top navigation.</span></span>
1. <span data-ttu-id="1ee28-132">Прокрутите список вниз до раздела **Настройки приложения** и добавления трех новых записей:</span><span class="sxs-lookup"><span data-stu-id="1ee28-132">Scroll down to the **App Settings** section and add three new entries:</span></span>
  - <span data-ttu-id="1ee28-133">**IDA: ClientID**</span><span class="sxs-lookup"><span data-stu-id="1ee28-133">**ida:ClientID**</span></span>
  - <span data-ttu-id="1ee28-134">**IDA: пароль**</span><span class="sxs-lookup"><span data-stu-id="1ee28-134">**ida:Password**</span></span> 
  - <span data-ttu-id="1ee28-135">**IDA: TenantID**</span><span class="sxs-lookup"><span data-stu-id="1ee28-135">**ida:TenantID**</span></span> 
1. <span data-ttu-id="1ee28-136">Скопируйте соответствующие значения из проекта рабочего `web.config` эти значения параметров веб-сайта Azure как показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="1ee28-136">Copy the corresponding values from the working project's `web.config` to these settings values in your Azure website as shown in the following figure:</span></span>

  ![WEBSITE_NODE_DEFAULT_VERSION 0.10.32, ida: ClientID 92b1e137-c36f-4bfe-9e1c-01ef546ce4a9, ida: Password — Bns06N18ZiyYfMcyU9qUfGnZbnkBiPZfUptLDsU6cml, частично исправленный ida: TenantId.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-02.png)

1. <span data-ttu-id="1ee28-139">В нижнем колонтитуле нажмите кнопку **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="1ee28-139">In the footer, click the **SAVE** button to save your changes.</span></span>

<span data-ttu-id="1ee28-140">На этом этапе веб-сайта Azure — это программа установки и настройки для размещения веб-проекта Office 365 API для развертывания на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="1ee28-140">At this point the Azure website is setup and configured to host the Office 365 API web project that you will deploy in a later step.</span></span>

[<span data-ttu-id="1ee28-141">в начало</span><span class="sxs-lookup"><span data-stu-id="1ee28-141">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="configure-the-azure-ad-application"></a><span data-ttu-id="1ee28-142">Настройка приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ee28-142">Configure the Azure AD Application</span></span>

<span data-ttu-id="1ee28-143">На этом этапе будет изменять приложения Azure AD используется для разработки и тестирования приложения Office 365.</span><span class="sxs-lookup"><span data-stu-id="1ee28-143">In this step you will modify the Azure AD application used in the development & testing of the Office 365 application.</span></span>

1. <span data-ttu-id="1ee28-144">Перейдите к странице [Портала управления Azure](https://manage.windowsazure.com) и входа в систему с помощью учетной записи идентификатор организации.</span><span class="sxs-lookup"><span data-stu-id="1ee28-144">Navigate to the [Azure Management Portal](https://manage.windowsazure.com) and login using your Organization ID account.</span></span>
1. <span data-ttu-id="1ee28-145">После входа, с помощью боковой панели навигации, выберите пункт **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-145">After logging in, using the navigation sidebar, select **ACTIVE DIRECTORY**.</span></span>
1. <span data-ttu-id="1ee28-146">На странице " **active directory** " выберите каталог, который связан с клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="1ee28-146">On the **active directory** page, select the directory that is linked to your Office 365 tenant.</span></span>
1. <span data-ttu-id="1ee28-147">Выберите элемент **приложения** в верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="1ee28-147">Next, click the **APPLICATIONS** item in the top navigation.</span></span>
1. <span data-ttu-id="1ee28-148">В разделе **Свойства** обновление **SIGN-ON URL-адрес** для указания на URL-адрес по умолчанию созданного веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-148">Within the **Properties** section, update the **SIGN-ON URL** to point to the default URL of the Azure Website you created.</span></span> <span data-ttu-id="1ee28-149">Запомните использование конечную точку HTTPS, которая предоставляется со всех веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-149">Take note to use the HTTPS endpoint that is provided with all Azure websites.</span></span>

  ![Имя имеет значение O365 WebApp SingleTenant.Office365App, URL-адрес входа задано значение https://o365api-01.azurewebsites.net](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-03.png)

1. <span data-ttu-id="1ee28-151">В разделе **Единого входа** обновите **Приложения идентификатор URI** для использования в домен для веб-сайта Azure (как показано на следующем рисунке).</span><span class="sxs-lookup"><span data-stu-id="1ee28-151">Within the **Single Sign-On** section, update the **App ID URI** to use the domain for the Azure website (shown in the following figure).</span></span>
1. <span data-ttu-id="1ee28-152">Затем обновите **URL-адрес ОТВЕТА** , поэтому только URL-адреса из списка домашнюю страницу веб-сайта Azure:</span><span class="sxs-lookup"><span data-stu-id="1ee28-152">Next, update the **REPLY URL** so the only URL listed is the homepage of the Azure website:</span></span>

  ![Идентификатор URI приложения https://o365api-01.azurewebsites.net/O365-WebApp-SingleTenant, URL-адрес ответа https://o365api-01.azurewebsites.net/](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-04.png)

1. <span data-ttu-id="1ee28-154">В нижнем колонтитуле нажмите кнопку **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="1ee28-154">In the footer, click the **SAVE** button to save your changes.</span></span>

<span data-ttu-id="1ee28-155">На этом этапе приложение Azure AD, используемых в Office 365 API веб-проект был настроен для работы с новой веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-155">At this point, the Azure AD application used by the Office 365 API web project has been configured to work with the new Azure website.</span></span>

[<span data-ttu-id="1ee28-156">в начало</span><span class="sxs-lookup"><span data-stu-id="1ee28-156">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="configure-the-aspnet-project"></a><span data-ttu-id="1ee28-157">Настройка проекта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ee28-157">Configure the ASP.NET Project</span></span>

<span data-ttu-id="1ee28-158">На этом этапе вы настроите проекта ASP.NET в приложении для использования нового веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-158">In this step you will configure the ASP.NET project in your application to use the new Azure Website.</span></span>

<span data-ttu-id="1ee28-159">Для примера приложения, используемые в этом примере для данное руководство дополнительные действия не требуется.</span><span class="sxs-lookup"><span data-stu-id="1ee28-159">For the sample application used in the example for this guidance, no extra work is actually required.</span></span> <span data-ttu-id="1ee28-160">Тем не менее веб-приложения, содержащие настройки в `web.config` файла для приложения Azure AD и Azure AD клиента, который используется во время разработки.</span><span class="sxs-lookup"><span data-stu-id="1ee28-160">However the web application does contain the settings within the `web.config` file for the Azure AD application and Azure AD tenant used during development.</span></span> <span data-ttu-id="1ee28-161">Некоторые разработчики следующим шагом нужно использовать другой Azure AD приложений или даже другой Azure подписки для их разработку и производственные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="1ee28-161">Some developers may choose to use different Azure AD applications or even different Azure subscriptions for their development and production instances.</span></span>

<span data-ttu-id="1ee28-162">В предыдущем шаге, описанные на этой странице, при создании веб-сайта Azure задайте параметры надстройки для приложения, которое обычно находятся в `web.config`.</span><span class="sxs-lookup"><span data-stu-id="1ee28-162">In a previous step outlined in this page, when you created the Azure website you set the add-in settings for the application that are typically found in the `web.config`.</span></span> <span data-ttu-id="1ee28-163">Чтобы убедиться в веб-приложение получает эти значения из конфигурации веб-сайта Azure, рекомендуется заменить значения в пределах `web.config` с заполнитель со значениями вместо этого.</span><span class="sxs-lookup"><span data-stu-id="1ee28-163">To ensure the web application receives these values from the Azure website configuration, it's recommended you replace the values within the `web.config` with placeholder values instead.</span></span>

1. <span data-ttu-id="1ee28-164">Откройте проект `web.config` файла.</span><span class="sxs-lookup"><span data-stu-id="1ee28-164">Open the project's `web.config` file.</span></span>
1. <span data-ttu-id="1ee28-165">Найдите параметры надстройки для **ida: ClientID**, **Ida: пароль** и **ida: TenantId**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-165">Locate the add-in settings for the **ida:ClientID**, **ida:Password** and **ida:TenantId**.</span></span>
1. <span data-ttu-id="1ee28-166">Замените значение-заполнитель значения следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="1ee28-166">Replace the values of these settings with a placeholder value:</span></span>

  ````xml
  <add key="ida:TenantId" value="set-in-azure-website-config" />
  <add key="ida:ClientID" value="set-in-azure-website-config" />
  <add key="ida:Password" value="set-in-azure-website-config" />
  ````

1. <span data-ttu-id="1ee28-167">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="1ee28-167">Save your changes.</span></span>

<span data-ttu-id="1ee28-168">На этом этапе веб-приложения, веб-сайта Azure и приложения в Azure AD, все правильно настроены и готовы к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="1ee28-168">At this point the web application, Azure website & application in Azure AD are all configured correctly and ready to be deployed.</span></span>

[<span data-ttu-id="1ee28-169">в начало</span><span class="sxs-lookup"><span data-stu-id="1ee28-169">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

# <a name="deploy-the-office-365-api-aspnet-web-application"></a><span data-ttu-id="1ee28-170">Развертывание Office 365 API веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ee28-170">Deploy the Office 365 API ASP.NET Web Application</span></span>

<span data-ttu-id="1ee28-171">На этом этапе вы публикуете веб-приложения Office 365 API для веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-171">In this step you will publish the Office 365 API web application to the Azure website.</span></span> <span data-ttu-id="1ee28-172">После развертывания сайта можно проверить его, чтобы убедиться, что все работает, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="1ee28-172">Once the site has been deployed you will test it to ensure everything works as desired.</span></span>

> <span data-ttu-id="1ee28-173">На этом шаге предполагается, у вас есть он Microsoft [Azure SDK](http://azure.microsoft.com/en-us/downloads/), версии 2.0 или более поздней версии, установлены.</span><span class="sxs-lookup"><span data-stu-id="1ee28-173">This step assumes you have he Microsoft [Azure SDK](http://azure.microsoft.com/en-us/downloads/), version 2.0 or higher, installed.</span></span> 

## <a name="deploy-the-aspnet-web-application"></a><span data-ttu-id="1ee28-174">Развертывание веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ee28-174">Deploy the ASP.NET Web Application</span></span>

1. <span data-ttu-id="1ee28-175">Откройте веб-приложения Office 365 API в Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1ee28-175">Open your Office 365 API web application in Visual Studio 2013.</span></span>
1. <span data-ttu-id="1ee28-176">В окне Обозреватель решений средство щелкните правой кнопкой мыши проект и выберите **Опубликовать** запустить мастер **Публикация веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="1ee28-176">Within the Solution Explorer tool window, right-click the project and select **Publish** start the **Publish Web** wizard.</span></span>
1. <span data-ttu-id="1ee28-177">На вкладке **профиля** выберите **Веб-сайт Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-177">On the **Profile** tab, select **Microsoft Azure Website**.</span></span>

  <span data-ttu-id="1ee28-178">На этом этапе вам будет предложено входа в Azure подписки с помощью вашей организации по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="1ee28-178">At this point you will be prompted to login to your Azure subscription using your Organization ID.</span></span>

1. <span data-ttu-id="1ee28-179">После входа выберите веб-сайт, созданный в предыдущем шаге на этой странице и нажмите **кнопку ОК**.</span><span class="sxs-lookup"><span data-stu-id="1ee28-179">After logging in, select the website that you created in a previous step from this page and click **OK**.</span></span>

  ![Диалоговое окно выберите существующий веб-сайт показан набор существующих веб-сайтов для o365api-01.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-05.png)

1. <span data-ttu-id="1ee28-181">На вкладке **подключения** нажмите кнопку **Проверить подключение** , чтобы проверить профиль подключения был успешно загружен и применения.</span><span class="sxs-lookup"><span data-stu-id="1ee28-181">On the **Connection** tab, click the **Validate Connection** button to ensure the connection profile was successfully downloaded and applied.</span></span>

  ![Стрелка указывает на кнопку Проверить подключение около внизу диалогового окна с зеленая галочка рядом с кнопкой.](media/Move-O365Api-Project-from-Dev-To-Prod/Move-O365Api-Project-from-Dev-To-Prod-06.png)

1. <span data-ttu-id="1ee28-183">Публикация веб-приложения и веб-сайта Azure, нажмите кнопку **Опубликовать** .</span><span class="sxs-lookup"><span data-stu-id="1ee28-183">Click the **Publish** button to publish the web application to the Azure website.</span></span>

## <a name="test-the-aspnet-web-application"></a><span data-ttu-id="1ee28-184">Тестирование веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1ee28-184">Test the ASP.NET Web Application</span></span>

<span data-ttu-id="1ee28-185">После публикации веб-приложения и веб-сайта Azure, Visual Studio откройте браузер и перейдите на домашнюю страницу веб-узла.</span><span class="sxs-lookup"><span data-stu-id="1ee28-185">After publishing the web application to the Azure website, Visual Studio will open a browser and navigate to the site's homepage.</span></span> 

<span data-ttu-id="1ee28-186">По умолчанию это конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ee28-186">By default this is the HTTP endpoint.</span></span> <span data-ttu-id="1ee28-187">При настройке приложения Azure AD, задайте его на получение дополнительные модули входа из конечную точку HTTPS отозвать из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="1ee28-187">Recall from the previous step when you configured the Azure AD application that you set it to only accept sign ons from the HTTPS endpoint.</span></span> <span data-ttu-id="1ee28-188">Прежде чем использовать обновления приложения URL-адрес для указания на конечную точку HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1ee28-188">Before you use the application update the url to point to the HTTPS endpoint.</span></span>

1. <span data-ttu-id="1ee28-189">В браузере обновите URL-адрес, чтобы перейти на домашнюю страницу HTTPS для веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-189">In the browser, update the URL to go to the HTTPS homepage for the Azure website.</span></span> <span data-ttu-id="1ee28-190">В примере на этой странице, которая является https://o365api-01.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="1ee28-190">In the example in this page, that is https://o365api-01.azurewebsites.net.</span></span>
1. <span data-ttu-id="1ee28-191">Щелкните ссылку **Войти** в заголовок в верхней правой части страницы.</span><span class="sxs-lookup"><span data-stu-id="1ee28-191">Click the **Sign In** link in the header at the top-right of the page.</span></span> <span data-ttu-id="1ee28-192">Вы будете направлены на Azure AD входа на странице.</span><span class="sxs-lookup"><span data-stu-id="1ee28-192">This will redirect you to the Azure AD sign on page.</span></span>

  > <span data-ttu-id="1ee28-193">Если на этом этапе сообщение об ошибке, значит, вероятно проблема с тремя параметрами надстройки, созданной для веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="1ee28-193">If you get an error at this point, it's likely an issue with the three add-in settings you created for the Azure website.</span></span> <span data-ttu-id="1ee28-194">Вернитесь и убедитесь в том, что значения являются правильными значениями из клиента Azure AD и приложения.</span><span class="sxs-lookup"><span data-stu-id="1ee28-194">Go back and make sure the values are the correct values from the Azure AD tenant & application.</span></span> <span data-ttu-id="1ee28-195">Должно появиться URL-адрес, которая выглядит</span><span class="sxs-lookup"><span data-stu-id="1ee28-195">You should see a URL that looks</span></span> 

1. <span data-ttu-id="1ee28-196">После успешного входа будет перенаправлен обратно на домашнюю страницу веб-приложения веб-сайта Azure, которую вы создали.</span><span class="sxs-lookup"><span data-stu-id="1ee28-196">After successfully logging in, you will be redirected back to the homepage for the web application of the Azure website you created.</span></span>

<span data-ttu-id="1ee28-197">На этом этапе успешно развернута проекта Office 365 API веб-приложения для запуска в Azure веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1ee28-197">At this point you have successfully deployed your Office 365 API web application project to run in an Azure website.</span></span>

[<span data-ttu-id="1ee28-198">в начало</span><span class="sxs-lookup"><span data-stu-id="1ee28-198">back to top</span></span>](#deploying-development-office-365-sites-to-microsoft-azure)

----------

### <a name="related-links"></a><span data-ttu-id="1ee28-199">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="1ee28-199">Related links</span></span> ###
-  [<span data-ttu-id="1ee28-200">O365-WebApp-SingleTenant</span><span class="sxs-lookup"><span data-stu-id="1ee28-200">O365-WebApp-SingleTenant</span></span>](https://github.com/SharePoint/O365-WebApp-SingleTenant)

### <a name="applies-to"></a><span data-ttu-id="1ee28-201">Применимо к</span><span class="sxs-lookup"><span data-stu-id="1ee28-201">Applies to</span></span> ###
-  <span data-ttu-id="1ee28-202">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="1ee28-202">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="1ee28-203">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="1ee28-203">Office 365 Dedicated (D)</span></span>

### <a name="author"></a><span data-ttu-id="1ee28-204">Автор</span><span class="sxs-lookup"><span data-stu-id="1ee28-204">Author</span></span>
<span data-ttu-id="1ee28-205">Эндрю Коннелл - [@andrewconnell](https://twitter.com/andrewconnell)</span><span class="sxs-lookup"><span data-stu-id="1ee28-205">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span></span>

### <a name="version-history"></a><span data-ttu-id="1ee28-206">История изменений</span><span class="sxs-lookup"><span data-stu-id="1ee28-206">Version history</span></span> ###
<span data-ttu-id="1ee28-207">Версия</span><span class="sxs-lookup"><span data-stu-id="1ee28-207">Version</span></span>  | <span data-ttu-id="1ee28-208">Date</span><span class="sxs-lookup"><span data-stu-id="1ee28-208">Date</span></span> | <span data-ttu-id="1ee28-209">Примечания</span><span class="sxs-lookup"><span data-stu-id="1ee28-209">Comments</span></span>
---------| -----| --------
<span data-ttu-id="1ee28-210">0,1</span><span class="sxs-lookup"><span data-stu-id="1ee28-210">0.1</span></span>  | <span data-ttu-id="1ee28-211">2 января 2015</span><span class="sxs-lookup"><span data-stu-id="1ee28-211">January 2, 2015</span></span> | <span data-ttu-id="1ee28-212">Первый черновик</span><span class="sxs-lookup"><span data-stu-id="1ee28-212">First draft</span></span>


