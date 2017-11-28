---
title: "Публикация надстроек SharePoint с помощью Visual Studio"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 7215ae000b40436c64b2a4b566948a88f20b9533
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="publish-sharepoint-add-ins-by-using-visual-studio"></a><span data-ttu-id="f8f97-102">Публикация надстроек SharePoint с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f8f97-102">Publish SharePoint Add-ins by using Visual Studio</span></span>
<span data-ttu-id="f8f97-p101">Узнайте, как опубликовать Надстройка SharePoint с помощью Microsoft Visual Studio 2013 или Visual Studio 2012. Если с надстройкой связано веб-приложение, то сначала необходимо развернуть его. Затем, как и для всех Надстройки SharePoint, необходимо упаковать Надстройка SharePoint и опубликовать его. Кроме того, можно отправить надстройку для ее включения в Магазин Office.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p101">Learn how to publish your SharePoint Add-in by using Microsoft Visual Studio 2013 or Visual Studio 2012. If the add-in has an associated web application, you deploy it first. Then, as for all SharePoint Add-ins, you package the SharePoint Add-in and then publish it. You can also optionally choose to submit your add-in for inclusion on the Office Store.</span></span>
 

 <span data-ttu-id="f8f97-p102">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p102">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="f8f97-110">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="f8f97-110">Prerequisites</span></span>
<span data-ttu-id="f8f97-111"><a name="Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="f8f97-111"></span></span>


 

 

-  [<span data-ttu-id="f8f97-112">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f8f97-112">Microsoft Visual Studio 2013</span></span>](http://go.microsoft.com/fwlink/?LinkId=517284  )
    
    <span data-ttu-id="f8f97-113">-или-</span><span class="sxs-lookup"><span data-stu-id="f8f97-113">-or-</span></span>
    
     <span data-ttu-id="f8f97-p103">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) и Инструменты разработчика Office для Visual Studio. Чтобы скачать эти инструменты, см. раздел "Инструменты" на [странице загрузки](http://go.microsoft.com/fwlink/?LinkId=234393). (Новый диспетчер публикации недоступен в Visual Studio 2012 и более ранних версиях.)</span><span class="sxs-lookup"><span data-stu-id="f8f97-p103">[Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682) and the Office Developer Tools for Visual Studio. To download the tools, see "Tools" on the [Download page](http://go.microsoft.com/fwlink/?LinkId=234393). (The new Publish Manager is not available in Visual Studio 2012 or earlier versions.)</span></span>
    
 
- <span data-ttu-id="f8f97-117">Microsoft SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8f97-117">Microsoft SharePoint</span></span>
    
 

## <a name="publish-by-using-visual-studio-2013"></a><span data-ttu-id="f8f97-118">Публикация с помощью Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f8f97-118">Publish by using Visual Studio 2013</span></span>
<span data-ttu-id="f8f97-119"><a name="VS2013"> </a></span><span class="sxs-lookup"><span data-stu-id="f8f97-119"></span></span>

<span data-ttu-id="f8f97-p104">Если с размещаемым у поставщика Надстройка SharePoint связано веб-приложение, для начала разверните файлы для него. Затем, как и для всех Надстройки SharePoint, запакуйте Надстройка SharePoint и опубликуйте его.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p104">If your provider-hosted SharePoint Add-in has a web application, deploy the files for it first. You then, as for all SharePoint Add-ins, package the SharePoint Add-in and publish it.</span></span>
 

 

 <span data-ttu-id="f8f97-p105">**Важно!** Чтобы обеспечить публикацию значений идентификатора и секрета клиента SharePoint с веб-проектом, что позволит веб-содержимому получать доступ к данным SharePoint, опубликуйте проект надстройки SharePoint с помощью страницы **Публикация надстройки**. Чтобы открыть эту страницу, вызовите контекстное меню надстройки SharePoint (не веб-приложения) и выберите команду **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p105">**Important**  To ensure that your SharePoint Client ID and Client Secret values get published with your web project, which allows your web content to access SharePoint data, publish your SharePoint Add-in project from the  **Publish your add-in** page. You access this page by opening the shortcut menu for the SharePoint Add-in, not the shortcut menu for the web app, and then choosing the **Publish** command.</span></span>
 


### <a name="step-1-deploy-the-web-application"></a><span data-ttu-id="f8f97-124">Этап 1. Развертывание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f8f97-124">Step 1: Deploy the web application</span></span>

<span data-ttu-id="f8f97-p106">Обычно с Надстройка SharePoint связано ведущее веб-приложение, которое необходимо развернуть на веб-сервере. Подробнее об использовании мастера веб-публикации см. в статье  [Инструкции. Развертывание проекта веб-приложения с помощью публикации одним щелчком в Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p106">Your SharePoint Add-in typically has an associated host web application that you need to deploy to a web server. For more information about how to use the Publish Web wizard, see  [How to: Deploy a Web Project using On-Click Publishing in Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span></span>
 

 

### <a name="to-open-the-publish-your-add-in-page"></a><span data-ttu-id="f8f97-127">Открытие страницы публикации надстроек</span><span class="sxs-lookup"><span data-stu-id="f8f97-127">To open the Publish your add-in page</span></span>


- <span data-ttu-id="f8f97-128">В **обозревателе решений** откройте контекстное меню для проекта надстройки SharePoint и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-128">In  **Solution Explorer**, open the shortcut menu for the SharePoint Add-in project, and then choose  **Publish**.</span></span>
    
    <span data-ttu-id="f8f97-129">Откроется страница **Публикация надстройки**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-129">The  **Publish your add-in** page appears.</span></span>
    
 

### <a name="to-select-or-create-a-profile"></a><span data-ttu-id="f8f97-130">Выбор или создание профиля</span><span class="sxs-lookup"><span data-stu-id="f8f97-130">To select or create a profile</span></span>


- <span data-ttu-id="f8f97-131">В списке **Текущий профиль** выберите профиль для импорта или нажмите **<Создать…>**, чтобы создать профиль.</span><span class="sxs-lookup"><span data-stu-id="f8f97-131">In the  **Current profile** list, choose a profile to import, or choose **<New …>** to create a profile.</span></span>
    
    <span data-ttu-id="f8f97-p107">В профиле публикации указан сервер, на котором развертывается веб-приложение, учетные данные, необходимые для входа на сервер, развертываемые базы данных (если применимо) и другие параметры развертывания. Вы можете создавать различные профили публикации в соответствии с вашими потребностями. Например, можно создать один профиль для тестирования, а другой — для публикации.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p107">A publish profile specifies the server to which you're deploying the web app, the credentials that are needed to log on to the server, the databases to deploy (if applicable), and other deployment options. You can create different publish profiles to fit your needs. For example, you might create one profile for testing and another profile for publishing.</span></span>
    
    <span data-ttu-id="f8f97-p108">Если выбрать команду **<Создать…>**, откроется **мастер создания профиля публикации**. С помощью этого мастера можно импортировать профиль публикации от поставщика услуг размещения сайтов, например Azure, или создать новый профиль, а затем вручную добавить имя сервера, учетные данные и другие параметры. Если создать новый профиль, а не импортировать существующий, потребуется указать значения идентификатора и секрета клиента, как описано в статьях [Регистрация надстроек для SharePoint 2013](http://msdn.microsoft.com/library/jj687469.aspx) и [Создание или обновление идентификаторов и секретов клиентов на Панели мониторинга продаж](http://msdn.microsoft.com/library/office/jj220036.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p108">If you choose  **<New …>**, the  **Create publishing profile** wizard appears. You can use this wizard to import a publishing profile from a website hosting provider, such as Azure, or to create a profile and then manually add your server name, credentials, and other settings. If you created a new profile rather than imported an existing profile, you'll need to supply client Id and client secret values, as outlined in [Guidelines for registering SharePoint Add-ins 2013](http://msdn.microsoft.com/library/jj687469.aspx) and [How to: Create Client IDs and secrets in the Microsoft Seller Dashboard](http://msdn.microsoft.com/library/office/jj220036.aspx).</span></span>
    
    <span data-ttu-id="f8f97-p109">Если планируется отправить надстройку SharePoint в Магазин Office, то необходимо использовать значения идентификатора и секрета клиента, созданные на Панели мониторинга продаж. Во время разработки вы можете использовать идентификатор и секрет клиента, созданные с помощью страницы appregnew.aspx, но для надстроек, отправляемых в Магазин Office, необходимо использовать идентификаторы и секреты клиентов, полученные из Панели мониторинга продаж. Кроме того, необходимо создать профиль публикации на сайте Azure и импортировать его в Visual Studio, а не создавать профиль в мастере **создания профиля публикации**. При создании профиля в Azure все параметры на вкладке **Подключение** автоматически указываются в Visual Studio. Дополнительные сведения об импорте и создании профилей публикации см. в разделе [Создание профиля публикации](http://msdn.microsoft.com/library/dd465337.aspx#creating_a_profile).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p109">If you plan to submit your SharePoint Add-in to the Office Store, be sure to use client ID and client secret values that are created in the Seller Dashboard. You can use client IDs and client secret values that you generate by using the appregnew.aspx page during the development phase, but add-ins that you submit to the Office Store must use client IDs and client secrets that you get from the Seller Dashboard. Also, you should create the publishing profile on your Azure site and then import it into Visual Studio, rather than creating a profile in the  **Create publishing profile** wizard. When you create a profile in Azure, all of the settings on the **Connection** tab are provided for you in Visual Studio. For more information about how to import or create a publishing profile, see [Creating a Publish Profile](http://msdn.microsoft.com/library/dd465337.aspx#creating_a_profile).</span></span>
    
     <span data-ttu-id="f8f97-p110">**Совет.** Если не удается опубликовать веб-содержимое напрямую, вы можете создать пакет веб-развертывания, который администратор может развернуть на сайте. Чтобы создать пакет веб-развертывания, создайте новый профиль, откройте вкладку **Подключение** и выберите пункт **Пакет веб-развертывания** в списке **Метод публикации**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p110">**Tip**  If you can't publish web content directly, you can create a web deploy package that an administrator can deploy to the web for you. To create a web deploy package, create a new profile, choose the  **Connection** tab, and then choose **Web Deploy Package** in the **Publish method** list.</span></span>

### <a name="to-deploy-your-web-app-project"></a><span data-ttu-id="f8f97-145">Развертывание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f8f97-145">To deploy your web app project</span></span>


1. <span data-ttu-id="f8f97-146">На вкладке **Публикация надстройки** нажмите кнопку **Развернуть веб-проект**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-146">On the  **Publish your add-in** page, choose the **Deploy your web project** button.</span></span>
    
    <span data-ttu-id="f8f97-147">Откроется диалоговое окно **Публикация веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-147">The  **Publish Web** dialog box appears.</span></span>
    
 
2. <span data-ttu-id="f8f97-148">Укажите недостающие значения на вкладках **Подключение** и **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-148">On the  **Connection** and **Settings** tabs, fill in any missing values.</span></span>
    
    <span data-ttu-id="f8f97-149">Если требуется изменить способ публикации файлов для надстройки SharePoint или надстройка использует внешнюю базу данных, откройте вкладку **Параметры**. См. раздел "Настройка вкладки «Параметры»" статьи [Развертывание проекта веб-приложения с помощью публикации одним щелчком в Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f97-149">To change how the files for your SharePoint Add-in are published or if the add-in uses an external database, choose the  **Settings** tab. See the section "Configuring the Settings Tab" in [How to: Deploy a Web Project using On-Click Publishing in Visual Studio](http://msdn.microsoft.com/library/dd465337.aspx).</span></span>
    
 
3. <span data-ttu-id="f8f97-150">Чтобы узнать, какие элементы будут изменены при развертывании веб-приложения, нажмите кнопку **Начать просмотр** на вкладке **Предварительный просмотр**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-150">To review what items will change when the web app is deployed, choose the  **Start Preview** button on the **Preview** tab.</span></span>
    
 
4. <span data-ttu-id="f8f97-151">Нажмите кнопку **Опубликовать**, чтобы развернуть проект веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f8f97-151">Choose the  **Publish** button to deploy the web app project.</span></span>
    
 

### <a name="step-2-package-the-add-in"></a><span data-ttu-id="f8f97-152">Этап 2. Упаковка надстройки</span><span class="sxs-lookup"><span data-stu-id="f8f97-152">Step 2: Package the Add-in</span></span>


1. <span data-ttu-id="f8f97-153">На вкладке **Публикация надстройки** нажмите кнопку **Упаковать надстройку**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-153">On the  **Publish your add-in** page, choose the **Package the add-in** button.</span></span>
    
    <span data-ttu-id="f8f97-154">Откроется **мастер публикации надстроек Office и SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-154">The  **Publish Office and SharePoint Add-ins** wizard appears.</span></span>
    
 
2. <span data-ttu-id="f8f97-155">В текстовом поле **Где размещен ваш веб-сайт?** введите URL-адрес сайта, на котором будут размещены файлы надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8f97-155">In the  **Where is your website hosted?** text box, enter the URL of the website that will host the content files of your SharePoint Add-in.</span></span>
    
    <span data-ttu-id="f8f97-p111">Этот адрес должен начинаться с префикса https. См. раздел [Почему приложения и надстройки должны быть защищены с использованием SSL?](http://msdn.microsoft.com/library/jj591603#bk_q7).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p111">You must specify an address that starts with the "https" prefix. See  [Why do my add-ins have to be SSL-secured?](http://msdn.microsoft.com/library/jj591603#bk_q7).</span></span>
    
     <span data-ttu-id="f8f97-p112">**Примечание.** Веб-сайты Azure автоматически предоставляют конечную точку https. Если надстройка публикуется на сайте Магазина Office или в самом Магазине Office, то адрес должен начинаться с префикса https. Однако если надстройка публикуется на локальном сайте, необходимо использовать префикс http.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p112">**Note**  Azure web sites automatically provide an https endpoint. If you publish your add-in on an Office Store site or to the Office Store, the address must start with an https prefix. However, if you publish the add-in to an on-premises site, you can use an http prefix.</span></span>

    <span data-ttu-id="f8f97-161">В текстовом поле **Идентификатор клиента надстройки** уже должен появиться идентификатор клиента, указанный в профиле публикации.</span><span class="sxs-lookup"><span data-stu-id="f8f97-161">In the  **What is the add-in's client ID?** text box, the client ID that you entered in the publishing profile should already appear.</span></span>
    
    <span data-ttu-id="f8f97-p113">Если до этого момента использовалось замещающее значение идентификатора клиента, то теперь необходимо добавить фактический идентификатор клиента. Эти сведения встроены в APP-пакет и позволяют веб-содержимому связываться с SharePoint на динамическом сайте.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p113">If you've used a placeholder value for the client ID until this point, you must add an actual client ID now. This information is embedded in the .app package and enables your web content to communicate with SharePoint on the live site.</span></span>
    
 
3. <span data-ttu-id="f8f97-164">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-164">Choose the  **Finish** button.</span></span>
    
    <span data-ttu-id="f8f97-p114">Visual Studio создаст файлы, необходимые для публикации Надстройка SharePoint, а затем откроет конечную папку публикации. Сведения об установке надстроек см. в статье  [Установка надстроек SharePoint и управление ими](http://technet.microsoft.com/library/fp161232.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p114">Visual Studio generates the files that are needed to publish your SharePoint Add-in and then opens the publish output folder. For information about how to install the add-in, see  [Install and manage SharePoint Add-ins 2013](http://technet.microsoft.com/library/fp161232.aspx).</span></span>
    
 

### <a name="step-3-publish-your-sharepoint-add-in-on-the-office-store"></a><span data-ttu-id="f8f97-167">Этап 3. Публикация надстройки SharePoint в Магазине Office</span><span class="sxs-lookup"><span data-stu-id="f8f97-167">Step 3: Publish your SharePoint Add-in on the Office Store</span></span>

<span data-ttu-id="f8f97-168">Чтобы отправить надстройку SharePoint в Магазин Office, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f8f97-168">Perform the following procedure if you want to submit your SharePoint Add-in to the Office Store.</span></span>
 

 

1. <span data-ttu-id="f8f97-169">На странице **Публикация надстройки** нажмите кнопку **Посетить Панель мониторинга продаж** и войдите в свою учетную запись Панели мониторинга продаж Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f8f97-169">On the  **Publish your add-in** page, choose the **Visit the Seller Dashboard** button, and then sign in to your Microsoft Seller Dashboard account.</span></span>
    
    <span data-ttu-id="f8f97-170">См. статью [Отправка надстроек Office и SharePoint, а также веб-приложений для Office 365 в Магазин Office](http://msdn.microsoft.com/library/submit-office-and-sharepoint-add-ins-and-office-365-web-apps-to-the-office-store%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f97-170">See  [Submit Office and SharePoint Add-ins and Office 365 web apps to the Office Store](http://msdn.microsoft.com/library/submit-office-and-sharepoint-add-ins-and-office-365-web-apps-to-the-office-store%28Office.15%29.aspx).</span></span>
    
 
2. <span data-ttu-id="f8f97-p115">Нажмите **Добавить новое приложение**, укажите необходимые данные и отправьте надстройку в Магазин Office. Дополнительные сведения см. в статье [Отправка надстроек Office и SharePoint и приложений для Office 365 в Магазин Office с помощью Панели мониторинга продаж](http://msdn.microsoft.com/library/use-the-seller-dashboard-to-submit-office-and-sharepoint-add-ins-and-office-365-apps-to-the-office-store%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p115">Choose  **add a new app**, fill out the information, and then submit the add-in to the Office Store. For details, see  [Use the Seller Dashboard to submit Office and SharePoint Add-ins and Office 365 apps to the Office Store](http://msdn.microsoft.com/library/use-the-seller-dashboard-to-submit-office-and-sharepoint-add-ins-and-office-365-apps-to-the-office-store%28Office.15%29.aspx).</span></span>
    
 

## <a name="publish-by-using-visual-studio-2012"></a><span data-ttu-id="f8f97-173">Публикация с помощью Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f8f97-173">Publish by using Visual Studio 2012</span></span>
<span data-ttu-id="f8f97-174"><a name="VS2012"> </a></span><span class="sxs-lookup"><span data-stu-id="f8f97-174"></span></span>

<span data-ttu-id="f8f97-175">Когда надстройка SharePoint будет готова к упаковке, откройте мастер **публикации надстроек Office**, который подготовит файлы надстройки SharePoint к публикации.</span><span class="sxs-lookup"><span data-stu-id="f8f97-175">When you're ready to package your SharePoint Add-in, open the  **Publish Office Add-ins** wizard, which prepares the files in your SharePoint Add-in for publishing.</span></span>
 

 

### <a name="step-1-package-the-sharepoint-add-in"></a><span data-ttu-id="f8f97-176">Этап 1. Упаковка надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8f97-176">Step 1: Package the SharePoint Add-in</span></span>


1. <span data-ttu-id="f8f97-177">В **обозревателе решений** откройте контекстное меню для проекта надстройки SharePoint и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-177">In  **Solution Explorer**, open the shortcut menu for the SharePoint Add-in project, and then choose  **Publish**.</span></span>
    
    <span data-ttu-id="f8f97-p116">Запустится мастер **публикации надстроек Office**. Страницы мастера зависят от типа упаковываемой надстройки SharePoint. Для надстройки с размещением в SharePoint появляется только страница **Сводка**. Для надстройки, размещаемой у поставщика, также отображаются страницы **Профиль** и **Размещение**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p116">The  **Publish Office Add-ins** wizard appears. The type of SharePoint Add-in that you're packaging determines the pages that appear in the wizard. If your add-in will be SharePoint-hosted, only the **Summary** page appears. If your add-in will be provider-hosted, the **Profile** and **Hosting** pages also appear.</span></span>
    
 
2. <span data-ttu-id="f8f97-182">Если надстройка SharePoint размещается у поставщика, укажите имя профиля публикации в списке **Выбор профиля для публикации** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-182">If your SharePoint Add-in is provider-hosted, specify a publishing profile name in the  **Which profile do you wish to publish?** list, and then choose the **Next** button.</span></span>
    
    <span data-ttu-id="f8f97-183">В профиле публикации сохраняются сведения, указанные на странице **Размещение**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-183">The publishing profile saves the information that you enter in the  **Hosting** page.</span></span>
    
 
3. <span data-ttu-id="f8f97-184">В списке **Где размещен ваш веб-сайт?** укажите URL-адрес веб-приложения, в котором будет размещаться надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f8f97-184">In the  **Where is your website hosted?** list, specify the URL for the web application that will host your SharePoint Add-in.</span></span>
    
 
4. <span data-ttu-id="f8f97-185">В полях под заголовком **Удостоверение надстройки** укажите идентификатор и секрет клиента, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-185">In the boxes under  **What is the identity of your add-in?**, specify the client ID and client secret for your add-in, and then choose the  **Next** button.</span></span>
    
    <span data-ttu-id="f8f97-186">См. статью [Авторизация и проверка подлинности надстроек SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f8f97-186">See  [Authorization and authentication of SharePoint Add-ins](authorization-and-authentication-of-sharepoint-add-ins.md).</span></span>
    
 
5. <span data-ttu-id="f8f97-187">Для всех типов надстроек SharePoint установите флажок **Открыть папку выходных данных после успешной упаковки** (если он еще не установлен) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f8f97-187">For all types of SharePoint Add-ins, select the  **Open output folder after successful packaging** check box, if it isn't already selected, and then choose the **Finish** button.</span></span>
    
    <span data-ttu-id="f8f97-p117">Visual Studio создает все файлы, необходимые для публикации Надстройка SharePoint. Эти файлы находятся в подпапке  `app.Publish` в папке выходных данных проекта (например, `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`). В ней содержится APP-файл Надстройка SharePoint и несколько файлов веб-приложения (если Надстройка SharePoint размещается в облаке). Все Надстройки SharePoint включают APP-файл, представляющий собой манифест надстройки для публикации Надстройка SharePoint. Надстройки SharePoint с размещением у поставщика также включают файлы для публикации ведущего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p117">Visual Studio generates all of the files that you need to publish your SharePoint Add-in. You can find these files in the  `app.Publish` folder of your project output folder (for example, `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`). That folder will contain a .app file for your SharePoint Add-in and multiple files for the web application (if your SharePoint Add-in is cloud-based). All SharePoint Add-ins include a .app file, which is the add-in manifest to publish the SharePoint Add-in. Provider-hosted SharePoint Add-ins also include files for publishing the host web application.</span></span>
    
 

### <a name="step-2-publish-the-web-application"></a><span data-ttu-id="f8f97-193">Этап 2. Публикация веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f8f97-193">Step 2: Publish the web application</span></span>

<span data-ttu-id="f8f97-p118">Если Надстройка SharePoint размещается у поставщика, то с ним связано веб-приложение, которое необходимо опубликовать на веб-сервере. Visual Studio создает пакет развертывания и сценарий для выполнения этой задачи.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p118">If your SharePoint Add-in is provider-hosted, you'll typically have an associated host web application that you need to publish to a web server. Visual Studio generates a deployment package and a script to help you perform this task.</span></span>
 

 
<span data-ttu-id="f8f97-p119">Пакет развертывания для проекта веб-приложения содержится в сжатом файле (ZIP) в папке  `app.publish`. Помимо ZIP-файла, в папке  `app.publish` находятся следующие файлы.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p119">The deployment package of the web application project is contained in a compressed (.zip) file in the  `app.publish` folder. In addition to the .zip file, the `app.publish` folder contains the following files:</span></span>
 

 


|<span data-ttu-id="f8f97-198">**Файл**</span><span class="sxs-lookup"><span data-stu-id="f8f97-198">**File**</span></span>|<span data-ttu-id="f8f97-199">**Описание**</span><span class="sxs-lookup"><span data-stu-id="f8f97-199">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="f8f97-200">_Имя_проекта_.deploy.cmd</span><span class="sxs-lookup"><span data-stu-id="f8f97-200">_ProjectName_.deploy.cmd</span></span>|<span data-ttu-id="f8f97-201">Это пакетный файл командной строки, который вызывает средство веб-развертывания, что позволяет упростить установку пакета с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="f8f97-201">This file is a command-line batch file that invokes Web Deploy so that you can more easily install the package at a command prompt.</span></span>|
| <span data-ttu-id="f8f97-202">_Имя_проекта_.SetParameters.xml</span><span class="sxs-lookup"><span data-stu-id="f8f97-202">_ProjectName_.SetParameters.xml</span></span>|<span data-ttu-id="f8f97-p120">Этот файл содержит параметры, которые передаются в средство веб-развертывания при использовании файла deploy.cmd для установки пакета. Настройки пакета Visual Studio определяют значения по умолчанию для всех параметров. Вы можете изменить эти значения, например, если нужно установить веб-приложение на нескольких серверах и использовать разные параметры для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p120">This file contains parameters that are passed to Web Deploy when you use the deploy.cmd file to install the package. The Visual Studio package settings determine the default value that's specified for each parameter. You can change these values if, for example, you want to install the web application to multiple servers and use different settings for each server.</span></span>|
| <span data-ttu-id="f8f97-206">_Имя_проекта_.SourceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f8f97-206">_ProjectName_.SourceManifest.xml</span></span>|<span data-ttu-id="f8f97-p121">Этот файл содержит параметры, которые Visual Studio передает в средство веб-развертывания и которые это средство использует для создания веб-пакета. Этот файл требуется средству веб-развертывания только для создания пакета. Он не используется при установке пакета.</span><span class="sxs-lookup"><span data-stu-id="f8f97-p121">This file contains settings that Visual Studio passes to Web Deploy and that Web Deploy uses to create the web package. Web Deploy requires this file only to create the package. This file isn't used when the package is installed.</span></span>|
<span data-ttu-id="f8f97-210">Пошаговые инструкции см. в статье [Как установить пакет развертывания с помощью файла deploy.cmd, созданного в Visual Studio](http://go.microsoft.com/fwlink/?LinkID=254954).</span><span class="sxs-lookup"><span data-stu-id="f8f97-210">For step-by-step guidance, see  [How to: Install a Deployment Package Using the deploy.cmd File Created by Using Visual Studio](http://go.microsoft.com/fwlink/?LinkID=254954)</span></span>
 

 

### <a name="step-3-publish-your-sharepoint-add-in"></a><span data-ttu-id="f8f97-211">Этап 3. Публикация надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8f97-211">Step 3: Publish your SharePoint Add-in</span></span>
<span data-ttu-id="f8f97-212"><a name="Publish"> </a></span><span class="sxs-lookup"><span data-stu-id="f8f97-212"></span></span>

<span data-ttu-id="f8f97-p122">Чтобы опубликовать Надстройка SharePoint, отправьте файл манифеста надстройки (APP-файл) в Магазин Office, каталог надстроек Office, SharePoint, файловый ресурс или каталог Exchange. Манифест надстройки находится в папке  `app.publish`, например  `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`. Дополнительные сведения о публикации Надстройка SharePoint см. в статье  [Авторизация и проверка подлинности для надстроек в SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="f8f97-p122">To publish your SharePoint Add-in, upload the add-in manifest file (.app) of your add-in to the Office Store, the Office Add-ins catalog, SharePoint, a file share, or the Exchange catalog. The add-in manifest for your add-in is located in the  `app.publish` folder, such as `%UserProfile%\Documents\Visual Studio 2012\Projects\MyApp\bin\Debug\app.publish`. For more information about how to publish your SharePoint Add-in, see  [Authorization and authentication of SharePoint Add-ins](authorization-and-authentication-of-sharepoint-add-ins.md).</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="f8f97-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f8f97-216">Additional resources</span></span>
<span data-ttu-id="f8f97-217"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="f8f97-217"></span></span>


-  [<span data-ttu-id="f8f97-218">Публикация надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f8f97-218">Publish SharePoint Add-ins</span></span>](publish-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="f8f97-219">Публикация надстройки Office</span><span class="sxs-lookup"><span data-stu-id="f8f97-219">Publish your Office Add-in</span></span>](http://msdn.microsoft.com/library/7f3ae6a0-06e9-438c-8899-bd9f605e6d9e%28Office.15%29.aspx)
    
 

