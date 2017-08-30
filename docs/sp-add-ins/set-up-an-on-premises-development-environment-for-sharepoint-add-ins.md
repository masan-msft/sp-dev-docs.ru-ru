
# <a name="set-up-an-on-premises-development-environment-for-sharepoint-add-ins"></a><span data-ttu-id="2f202-101">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f202-101">Set up an on-premises development environment for SharePoint Add-ins</span></span>
<span data-ttu-id="2f202-102">Узнайте, как настроить специальную среду разработки надстроек SharePoint с локальной установкой SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f202-102">Learn how to set up a development environment that is specifically suited to developing SharePoint Add-ins with an on-premises installation of SharePoint.</span></span>
 

 <span data-ttu-id="2f202-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="2f202-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 


## <a name="install-the-operating-system-for-your-development-environment-for-sharepoint-add-ins"></a><span data-ttu-id="2f202-106">Установка операционной системы для среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f202-106">Install the operating system for your development environment for SharePoint Add-ins</span></span>
<span data-ttu-id="2f202-107"><a name="bk_installOS"> </a></span><span class="sxs-lookup"><span data-stu-id="2f202-107"></span></span>

<span data-ttu-id="2f202-p102">По сравнению с требованиями к рабочей среде, требования к среде разработки менее строгие, а их выполнение менее затратно. Поэтому в инструкциях, приведенных в этом разделе, нет сведений об установке рабочей среды. В статьях  [Обзор установки и настройки SharePoint](http://technet.microsoft.com/en-us/library/ee667264%28v=office.15%29),  [Требования к оборудованию и программному обеспечению для SharePoint](http://technet.microsoft.com/en-us/library/cc262485%28v=office.15%29) и [Настройка среды для надстроек SharePoint](http://technet.microsoft.com/en-us/library/fp161236%28office.15%29.aspx) можно найти инструкции по настройке рабочей среды для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f202-p102">The requirements for a development environment are less stringent and costly than the requirements for a production environment, and the guidelines described here do not support a production environment installation. See  [Overview of SharePoint installation and configuration](http://technet.microsoft.com/en-us/library/ee667264%28v=office.15%29),  [Hardware and software requirements for SharePoint](http://technet.microsoft.com/en-us/library/cc262485%28v=office.15%29), and  [Configure an environment for SharePoint Add-ins](http://technet.microsoft.com/en-us/library/fp161236%28office.15%29.aspx) for the instructions to set up a production environment installation of SharePoint.</span></span>
 

 
<span data-ttu-id="2f202-110">Во всех средах разработки для установки и запуска SharePoint необходимо использовать компьютер с ЦП, поддерживающим архитектуру x64, и с ОЗУ не менее, чем на 16 ГБ. Рекомендуется ОЗУ на 24 ГБ.</span><span class="sxs-lookup"><span data-stu-id="2f202-110">In any development environment, you should use a computer with an x64-capable CPU, and at least 16 GB of RAM to install and run SharePoint; 24 GB of RAM is preferable.</span></span>
 

 
<span data-ttu-id="2f202-111">В зависимости от конкретных требований и бюджета можно выбрать какой-либо из следующих вариантов.</span><span class="sxs-lookup"><span data-stu-id="2f202-111">Depending on your specific requirements and budget, you can choose from the following options:</span></span>
 

 

- <span data-ttu-id="2f202-112">Установите SharePoint на сервере с Windows Server 2008 R2 с пакетом обновления 1 (64-разрядной версии) или Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="2f202-112">Install SharePoint on Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012.</span></span>
    
 
- <span data-ttu-id="2f202-p103">Использование Microsoft Hyper-V и установка SharePoint на виртуальной машине под управлением гостевой ОС Windows Server 2008 R2 64-разрядной версии с пакетом обновления 1 или Windows Server 2012. Руководство по настройке виртуальной машины Microsoft Hyper-V для SharePoint см. в статье  [Использование рекомендованных конфигураций виртуальных машин SharePoint и среды Hyper-V](http://technet.microsoft.com/en-US/library/ff621103%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f202-p103">Use Microsoft Hyper-V and install SharePoint on a virtual machine running a Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012 guest operating system. See  [Use best practice configurations for the SharePoint virtual machines and Hyper-V environment](http://technet.microsoft.com/en-US/library/ff621103%28v=office.15%29.aspx) for guidance on setting up a Microsoft Hyper-V virtual machine for SharePoint.</span></span>
    
 

 <span data-ttu-id="2f202-p104">**Примечание.** Установка SharePoint поддерживается только в ОС Windows Server 2008 R2 64-разрядной версии с пакетом обновления 1 или в Windows Server 2012. Если вы хотите разрабатывать надстройки SharePoint для SharePoint в Windows 7 или Windows 8, можно зарегистрировать Сайт разработчика Office 365 и разрабатывать надстройки удаленно.</span><span class="sxs-lookup"><span data-stu-id="2f202-p104">**Note** Installation of SharePoint is supported only on Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012. If you want to develop SharePoint Add-ins for SharePoint on Windows 7 or Windows 8, you can sign up for an Office 365 Developer Site and develop add-ins remotely.</span></span> 
 


## <a name="install-the-prerequisites-for-the-operating-system-and-sharepoint"></a><span data-ttu-id="2f202-117">Установка необходимых компонентов для операционной системы и SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f202-117">Install the prerequisites for the operating system and SharePoint</span></span>
<span data-ttu-id="2f202-118"><a name="bk_prereqsOS"> </a></span><span class="sxs-lookup"><span data-stu-id="2f202-118"></span></span>


1. <span data-ttu-id="2f202-119">Запустите средство PrerequisiteInstaller.exe, входящее в состав установочных файлов.</span><span class="sxs-lookup"><span data-stu-id="2f202-119">Run the PrerequisiteInstaller.exe tool that is included with your installation files.</span></span>
    
 
2. <span data-ttu-id="2f202-120">Запустите средство Setup.exe, включенное в ваши установочные файлы.</span><span class="sxs-lookup"><span data-stu-id="2f202-120">Run the Setup.exe tool that is included with your installation files.</span></span>
    
 
3. <span data-ttu-id="2f202-121">Примите условия лицензионного соглашения на использование программного обеспечения Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2f202-121">Accept the Microsoft Software License Terms.</span></span>
    
 
4. <span data-ttu-id="2f202-122">На странице **выбора варианта установки** выберите вариант **Автономная**.</span><span class="sxs-lookup"><span data-stu-id="2f202-122">On the **Choose the installation you want** page, choose **Stand-alone**.</span></span>
    
    <span data-ttu-id="2f202-123">**Рис. 1. Выбор типа установки**</span><span class="sxs-lookup"><span data-stu-id="2f202-123">**Figure 1. Installation type choice**</span></span>

 

  ![Тип сервера установки SharePoint](../../images/SP15_app_ServerType.gif)
 

 

 
5. <span data-ttu-id="2f202-p105">Если во время установки возникают какие-либо ошибки, просмотрите файл журнала. Чтобы найти его, откройте окно командной строки и введите следующие команды. Ссылка на файл журнала появляется также после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="2f202-p105">If any errors occur in the installation, review the log file. To find the log file, open a Command Prompt window, and then type the following commands at the command prompt. A link to the log file also appears when the installation is complete.</span></span>
    
```
  cd %temp%
dir /od *.log
```

6. <span data-ttu-id="2f202-128">После завершения установки вам будет предложено запустить мастер настройки продуктов и технологий SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f202-128">After the installation is complete, you're prompted to start the SharePoint Products and Technologies Configuration Wizard.</span></span>
    
     <span data-ttu-id="2f202-p106">**Примечание.** Если установка выполняется на компьютере, который присоединен к домену, но не подключен к контроллеру домена, работа мастера настройки продуктов и технологий SharePoint может завершиться с ошибкой. В этом случае подключитесь к контроллеру домена напрямую или с помощью VPN-подключения либо выполните вход с помощью локальной учетной записи с правами администратора на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2f202-p106">**Note** The SharePoint Products and Technologies Configuration Wizard may fail if you're using a computer that is joined to a domain but that is not connected to a domain controller. If you see this failure, connect to a domain controller either directly or through a Virtual Private Network (VPN) connection, or sign in with a local account that has administrative privileges on the computer.</span></span>
7. <span data-ttu-id="2f202-p107">После завершения работы мастера настройки откроется страница **Выбор шаблона** для нового сайта SharePoint. На этой странице выберите шаблон **Сайт разработчика**. Надстройки SharePoint можно разворачивать с помощью Visual Studio только на Сайте разработчика.</span><span class="sxs-lookup"><span data-stu-id="2f202-p107">After the configuration wizard is complete, you see the **Template Selection** page of the new SharePoint site. On this page, choose the **Developer Site** template. You can only deploy SharePoint Add-ins from Visual Studio to a Developer Site.</span></span>
    
    <span data-ttu-id="2f202-134">**Рис. 2. Страница выбора шаблона сайта**</span><span class="sxs-lookup"><span data-stu-id="2f202-134">**Figure 2. Choose the site template page**</span></span>

 

  ![Страница шаблонов сайта](../../images/SP15_appChooseSiteTemplate.gif)
 

 

 

## <a name="configure-services-in-sharepoint-for-server-to-server-add-in-use"></a><span data-ttu-id="2f202-136">Настройка служб в SharePoint для межсерверного использования надстроек</span><span class="sxs-lookup"><span data-stu-id="2f202-136">Configure services in SharePoint for server-to-server add-in use</span></span>
<span data-ttu-id="2f202-137"><a name="Servertoserver"> </a></span><span class="sxs-lookup"><span data-stu-id="2f202-137"></span></span>

<span data-ttu-id="2f202-p108">На этом этапе службы в SharePoint настраиваются для межсерверного использования надстроек. Это позволяет создавать размещаемые у поставщиков надстройки с высоким уровнем доверия в вашей среде. Дополнительные сведения о создании таких надстроек см. в статье  [Создание надстроек с высоким уровнем доверия для SharePoint](create-high-trust-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="2f202-p108">In this step, you configure services in SharePoint for server-to-server add-in use. These steps ensure that you will be able to create high trust provider-hosted add-ins with your installation. See  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins) for more information about creating this kind of add-in.</span></span>
 

 

1. <span data-ttu-id="2f202-p109">Убедитесь, что настроены служба управления приложениями и приложение профилей пользователей (эта служба называется службой управления приложениями, так как изначально Надстройки SharePoint назывались "приложениями для SharePoint"). Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2f202-p109">Ensure that the App Management Service and user profile application are configured. (It is called "App Management Service" because SharePoint Add-ins were originally named "apps for SharePoint".) The steps are as follows:</span></span>
    
      1. <span data-ttu-id="2f202-143">В **центре администрирования** выберите в разделе **Управление приложениями** элемент **Управление приложениями-службами**.</span><span class="sxs-lookup"><span data-stu-id="2f202-143">In **Central Administration**, under **Application Management**, select **Manage service applications**.</span></span>
    
 
  2. <span data-ttu-id="2f202-144">На странице **Приложения-службы** убедитесь, что запущены следующие службы:</span><span class="sxs-lookup"><span data-stu-id="2f202-144">On the **Service Applications** page, ensure that the following services are started:</span></span>
    
      - <span data-ttu-id="2f202-145">Приложение-служба профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="2f202-145">User Profile Service Application</span></span>
    
 
  - <span data-ttu-id="2f202-146">Служба управления приложениями</span><span class="sxs-lookup"><span data-stu-id="2f202-146">App Management Service</span></span>
    
 
  3. <span data-ttu-id="2f202-147">В разделе **Управление приложениями** выберите пункт **Управление службами на сервере**.</span><span class="sxs-lookup"><span data-stu-id="2f202-147">Under **Application Management**, select **Manage services on server**.</span></span> 
    
 
  4. <span data-ttu-id="2f202-148">На странице **Службы на сервере** убедитесь, что запущены следующие службы:</span><span class="sxs-lookup"><span data-stu-id="2f202-148">On the **Services on Server** page, ensure that the following services are started:</span></span>
    
      - <span data-ttu-id="2f202-149">Служба профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="2f202-149">User Profile Service</span></span> 
    
 
2. <span data-ttu-id="2f202-p110">Убедитесь, что в **приложении-службе профилей пользователей** создан по крайней мере один профиль. Для этого выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="2f202-p110">Ensure that at least one profile is created in the **User Profile Service Application**. The steps are as follows:</span></span>
    
      1. <span data-ttu-id="2f202-152">В **центре администрирования** выберите в разделе **Управление приложениями** элемент **Управление приложениями-службами**.</span><span class="sxs-lookup"><span data-stu-id="2f202-152">In **Central Administration**, under **Application Management**, select **Manage service applications**.</span></span>
    
 
  2. <span data-ttu-id="2f202-153">Затем выберите пункт **Приложение-служба профилей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2f202-153">Next, select **User Profile Service Application**.</span></span>
    
 
  3. <span data-ttu-id="2f202-154">На странице **Служба управления профилями: приложение-служба профилей пользователей** выберите в разделе **Люди** пункт **Управление профилями пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2f202-154">On the **Manage Profile Service: User Profile Service Application** page, under **People**, select **Manage User Profiles**.</span></span>
    
 
  4. <span data-ttu-id="2f202-155">На странице **Управление профилями пользователей** нажмите кнопку **Создать профили**.</span><span class="sxs-lookup"><span data-stu-id="2f202-155">On the **Manage User Profiles** page, select **New Profiles**.</span></span>
    
 
  5. <span data-ttu-id="2f202-156">На странице **Добавление профиля пользователя** укажите имя своей учетной записи и электронный адрес.</span><span class="sxs-lookup"><span data-stu-id="2f202-156">On the **Add User Profile** page, type your account name and email address.</span></span>
    
 
  6. <span data-ttu-id="2f202-157">Нажмите кнопку **Сохранить и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="2f202-157">Select **Save and Close**.</span></span>
    
     <span data-ttu-id="2f202-158">**Примечание.** Если появится сообщение о том, что профиль, который вы пытаетесь создать, уже существует, нажмите **Отменить и вернуться**.</span><span class="sxs-lookup"><span data-stu-id="2f202-158">**Note** If you get a message saying that the profile you are trying to create already exists, select **Cancel and Go Back**.</span></span>
  7. <span data-ttu-id="2f202-159">Вернувшись на страницу **Управление профилями пользователей**, вы должны увидеть сообщение **Общее число профилей: 1**.</span><span class="sxs-lookup"><span data-stu-id="2f202-159">Back on the **Manage User Profiles** page, you should see **Total number of profiles: 1**.</span></span>
    
 

## <a name="install-visual-studio-and-office-developer-tools-for-visual-studio"></a><span data-ttu-id="2f202-160">Установка Visual Studio и Инструментов разработчика Office для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f202-160">Install Visual Studio and Office Developer Tools for Visual Studio</span></span>
<span data-ttu-id="2f202-161"><a name="SP15Appdevonprem_bk_installVS"> </a></span><span class="sxs-lookup"><span data-stu-id="2f202-161"></span></span>


- <span data-ttu-id="2f202-p111">Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это согласно инструкциям на странице [Установка Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="2f202-p111">If you don't already have **Visual Studio** 2013 or later installed, install it with the instructions at [Install Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx). We recommend using the  [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
    
 
- <span data-ttu-id="2f202-p112">В состав Visual Studio входят **Инструменты разработчика Microsoft Office для Visual Studio**, но иногда выход новой версии инструментов не совпадает с выходом обновлений Visual Studio. Чтобы убедиться, что вы используете последнюю версию инструментов, запустите [установщик Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [установщик Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="2f202-p112">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**, but sometimes a version of the tools is released between updates of Visual Studio. To be sure that you have the latest version of the tools use run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or  [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>
    
 

### <a name="verbose-logging-in-visual-studio"></a><span data-ttu-id="2f202-166">Подробное ведение журнала в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f202-166">Verbose logging in Visual Studio</span></span>

<span data-ttu-id="2f202-167">Выполните указанные ниже действия, чтобы включить подробное ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="2f202-167">Follow these steps if you want to turn on verbose logging:</span></span>
 

 

1. <span data-ttu-id="2f202-168">Откройте реестр и перейдите к разделу **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, где _nn.n_ — это номер версии Visual Studio, например 12.0 или 14.0.</span><span class="sxs-lookup"><span data-stu-id="2f202-168">Open the registry, and navigate to HKEY_CURRENT_USERSoftwareMicrosoft**VisualStudio_nn.n_SharePointTools**, where _nn.n_ is the version of Visual Studio, such as 12.0 or 14.0.</span></span>
    
 
2. <span data-ttu-id="2f202-169">Добавьте ключ DWORD под названием **EnableDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="2f202-169">Add a DWORD key named **EnableDiagnostics**.</span></span>
    
 
3. <span data-ttu-id="2f202-170">Присвойте ключу значение **1**.</span><span class="sxs-lookup"><span data-stu-id="2f202-170">Give the key the value **1**.</span></span>
    
 
<span data-ttu-id="2f202-171">Путь реестра в будущих версиях Visual Studio изменится.</span><span class="sxs-lookup"><span data-stu-id="2f202-171">The registry path will change in future versions of Visual Studio.</span></span>
 

 

## <a name="configure-an-isolated-add-in-domain-in-sharepoint"></a><span data-ttu-id="2f202-172">Настройка изолированного домена надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f202-172">Configure an isolated add-in domain in SharePoint</span></span>
<span data-ttu-id="2f202-173"><a name="SP15appdevonprem_bk_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="2f202-173"></span></span>

<span data-ttu-id="2f202-174">Прежде чем выполнять процедуры, описанные в этом разделе, см. раздел [Хост-сайты, сайты надстроек и изолированный домен](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#IsolatedDomain).</span><span class="sxs-lookup"><span data-stu-id="2f202-174">Please read  [Host webs, add-in webs, and the isolated domain](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#IsolatedDomain) before you carry out any procedures in this section.</span></span>
 

 
<span data-ttu-id="2f202-p113">Требуется создать изолированный домен в вашей тестовой ферме SharePoint. Кроме того, для установки SharePoint требуется общий домен с заголовком узла с подстановочными знаками, где можно выполнять подготовку надстроек, размещаемых в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f202-p113">You must create an isolated domain in your test SharePoint farm. Also, your SharePoint installation needs a general wildcard host header domain where it can provision SharePoint-hosted add-ins.</span></span>
 

 
<span data-ttu-id="2f202-p114">В целях разработки можно изменить свой файл Hosts при необходимости, чтобы сделать возможной маршрутизацию с компьютера разработки к тестовому экземпляру Надстройка SharePoint. Visual Studio изменяет файл Hosts автоматически при создании и развертывании надстройки.</span><span class="sxs-lookup"><span data-stu-id="2f202-p114">For development purposes, you can modify your hosts file as you need to route your development computer to a test instance of a SharePoint Add-in. Visual Studio modifies your hosts file automatically when you build and deploy the add-in.</span></span> 
 

 

 <span data-ttu-id="2f202-p115">**Примечание.** Для рабочих ферм необходимо создать стратегию маршрутизации DNS в интрасети и, возможно, настроить брандмауэр. Дополнительные сведения о создании и настройке рабочей среды для надстроек SharePoint см. в статье [Установка надстроек SharePoint и управление ими](http://technet.microsoft.com/en-us/library/fp161232%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="2f202-p115">**Note** For production farms, you would have to create a DNS routing strategy within your intranet and optionally configure your firewall. See  [Install and Manage SharePoint Add-ins](http://technet.microsoft.com/en-us/library/fp161232%28v=office.15%29) for more information about how to create and configure a production environment for SharePoint Add-ins.</span></span>
 

<span data-ttu-id="2f202-181">Выполните действия, описанные в следующем разделе, чтобы создать изолированный домен надстройки.</span><span class="sxs-lookup"><span data-stu-id="2f202-181">Perform the steps in the following procedure to create an isolated add-in domain.</span></span>
 

 

 <span data-ttu-id="2f202-182">**Примечание.** Все эти действия необходимо выполнять от имени администратора фермы, а командную строку и командную консоль SharePoint необходимо запускать от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="2f202-182">**Note** You must perform all of the steps in the following procedure while logged in as the farm administrator, and you must run the command prompt and the SharePoint Management Shell as an administrator.</span></span>
 


### <a name="create-an-isolated-add-in-domain-on-your-development-computer"></a><span data-ttu-id="2f202-183">Создание изолированного домена надстройки на компьютере для разработки</span><span class="sxs-lookup"><span data-stu-id="2f202-183">Create an isolated add-in domain on your development computer</span></span>


1. <span data-ttu-id="2f202-184">Убедитесь, что запущены службы spadmin и sptimer. Для этого откройте командную строку и введите приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="2f202-184">Ensure that the spadmin and sptimer services are running by opening a command prompt and typing the following commands.</span></span>
    
```
  net start spadminv4
net start sptimerv4
```

2. <span data-ttu-id="2f202-p116">Создайте изолированный домен надстройки, запустив командную консоль SharePoint от имени администратора и выполнив следующую команду. Замените  _contosoaddins.com_ доменом вашей надстройки. Это *не*  должен быть поддомен ведущего домена SharePoint. В противном случае потеряется большинство преимуществ безопасности изолированных доменов надстроек. Например, если имя несущего домена contoso.com, не используйте addins.contoso.com в качестве домена надстроек.</span><span class="sxs-lookup"><span data-stu-id="2f202-p116">Create your isolated add-in domain by running the SharePoint Management Shell as an administrator and typing the following command. Replace the  _contosoaddins.com_ with your add-in domain. It should *not*  be a subdomain of the host SharePoint domain. Doing so largely defeats the security advantages of having isolated add-in domains. For example, if the host domain is contoso.com, do not use addins.contoso.com as the add-in domain.</span></span>
    
```
  Set-SPAppDomain "contosoaddins.com"
```

3. <span data-ttu-id="2f202-190">Убедитесь, что запущены службы SPSubscriptionSettingsService и AppManagementServiceInstance. Для этого введите в командной консоли SharePoint приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="2f202-190">Ensure that the SPSubscriptionSettingsService and AppManagementServiceInstance services are running by typing the following command in the SharePoint Management Shell.</span></span>
    
```
  Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"} | Start-SPServiceInstance
```

4. <span data-ttu-id="2f202-p117">Убедитесь, что службы SPSubscriptionSettingsService и AppManagementServiceInstance работают, введя в командной консоли SharePoint следующую команду. Результат выполнения команды покажет, подключена ли каждая служба.</span><span class="sxs-lookup"><span data-stu-id="2f202-p117">Verify that the SPSubscriptionSettingsService and AppManagementServiceInstance services are running by typing the following command in the SharePoint Management Shell. The output will indicate whether each service is online.</span></span>
    
```
  Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"}
```

5. <span data-ttu-id="2f202-p118">Необходимо указать учетную запись, в которой будут выполняться экземпляры служб SPSubscriptionService и AppManagementServiceInstance. Это должна быть учетная запись SPManagedAccount. Чтобы создать учетную запись SPManagedAccount, введите в командной консоли SharePoint приведенную ниже команду (вам будет предложено указать имя пользователя и домен учетной записи, а также пароль).</span><span class="sxs-lookup"><span data-stu-id="2f202-p118">You must specify an account under which the SPSubscriptionService and AppManagementServiceInstance service instances will run. This account must be an SPManagedAccount. You can create an SPManagedAccount by typing the following command in the SharePoint Management Shell. (You'll be prompted for the account domainuser and password.)</span></span>
    
```
  $account = New-SPManagedAccount
```

6. <span data-ttu-id="2f202-p119">Укажите параметры учетной записи, пула приложений и базы данных для служб SPSubscriptionService и AppManagementServiceInstance, введя следующий код в командной консоли SharePoint. Если в предыдущем действии была создана учетная запись SPManagedAccount, используйте здесь ее имя.</span><span class="sxs-lookup"><span data-stu-id="2f202-p119">Specify an account, application pool, and database settings for the SPSubscriptionService and AppManagementServiceInstance services by typing the following code in the SharePoint Management Shell. If you created a SPManagedAccount in the preceding step, use that account name here.</span></span>
    
```
  $account = Get-SPManagedAccount "domain\user" 
$appPoolSubSvc = New-SPServiceApplicationPool -Name SettingsServiceAppPool -Account $account
$appPoolAppSvc = New-SPServiceApplicationPool -Name AppServiceAppPool -Account $account
$appSubSvc = New-SPSubscriptionSettingsServiceApplication -ApplicationPool $appPoolSubSvc -Name SettingsServiceApp -DatabaseName SettingsServiceDB 
$proxySubSvc = New-SPSubscriptionSettingsServiceApplicationProxy -ServiceApplication $appSubSvc
$appAppSvc = New-SPAppManagementServiceApplication -ApplicationPool $appPoolAppSvc -Name AppServiceApp -DatabaseName AppServiceDB
$proxyAppSvc = New-SPAppManagementServiceApplicationProxy -ServiceApplication $appAppSvc

```

7. <span data-ttu-id="2f202-199">Укажите префикс надстройки (см. раздел [Хост-сайты, сайты надстроек и изолированный домен](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#IsolatedDomain)). Для этого введите приведенный ниже код в командной консоли SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2f202-199">Specify your add-in prefix (see  [Host webs, add-in webs, and the isolated domain](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013#IsolatedDomain)) by typing the following code in the SharePoint Management Shell.</span></span>
    
```
  Set-SPAppSiteSubscriptionName -Name "add-in" -Confirm:$false
```

 <span data-ttu-id="2f202-p120">**Выполните следующую процедуру, только если в вашей среде используется прокси-сервер.** После создания изолированного домена надстроек выполните действия, приведенные в следующей процедуре, чтобы добавить этот домен в список обхода в Internet Explorer. Это гарантирует, что вы сможете переходить к этому домену после развертывания надстройки, размещенной в SharePoint, или надстройки, размещенной у поставщика, которая содержит сайт надстройки.</span><span class="sxs-lookup"><span data-stu-id="2f202-p120">**Carry out the following procedure only if your environment uses a proxy server.** After you create your isolated add-in domain, perform the steps in the following procedure to add that domain to your bypass list in Internet Explorer. This ensures that you can navigate to this domain after you deploy a SharePoint-hosted add-in or a provider-hosted add-in that includes an add-in web.</span></span>
 

 

### <a name="add-your-isolated-add-in-domain-to-your-bypass-list-in-internet-explorer"></a><span data-ttu-id="2f202-203">Добавление изолированного домена надстройки в список обхода в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="2f202-203">Add your isolated add-in domain to your bypass list in Internet Explorer</span></span>


1. <span data-ttu-id="2f202-204">В Internet Explorer откройте меню **Сервис**.</span><span class="sxs-lookup"><span data-stu-id="2f202-204">In Internet Explorer, go to **Tools**.</span></span>
    
 
2. <span data-ttu-id="2f202-205">Выберите пункт **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="2f202-205">Choose **Internet options**.</span></span>
    
 
3. <span data-ttu-id="2f202-206">На вкладке **Подключения** нажмите кнопку **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="2f202-206">On the **Connections** tab, choose the **LAN Settings** button.</span></span>
    
 
4. <span data-ttu-id="2f202-207">Снимите флажок **Автоматическое определение параметров**.</span><span class="sxs-lookup"><span data-stu-id="2f202-207">Clear the **Automatically detect settings** check box.</span></span>
    
 
5. <span data-ttu-id="2f202-208">Установите флажок **Использовать прокси-сервер для локальных подключений**.</span><span class="sxs-lookup"><span data-stu-id="2f202-208">Select the **Use a proxy server for your LAN** check box.</span></span>
    
 
6. <span data-ttu-id="2f202-209">Нажмите кнопку **Дополнительно** и добавьте адрес *.Ваш_домен_надстроек.com в список **Исключения**.</span><span class="sxs-lookup"><span data-stu-id="2f202-209">Choose the Advanced button, and then add *.YourAddinsDomain.com to the Exceptions list.</span></span>
    
 
7. <span data-ttu-id="2f202-210">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2f202-210">Choose the **OK** button.</span></span>
    
 
8. <span data-ttu-id="2f202-211">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Настройка параметров локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="2f202-211">Choose the **OK** button to close the **Local Area Network (LAN) Settings** dialog box.</span></span>
    
 
9. <span data-ttu-id="2f202-212">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="2f202-212">Choose the **OK** button to close the **Internet Options** dialog box.</span></span>
    
 
<span data-ttu-id="2f202-213">Сведения о доступных вариантах развертывания надстроек см. в статье [Развертывание и установка надстроек SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options).</span><span class="sxs-lookup"><span data-stu-id="2f202-213">See  [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options) for information about your options for deploying your add-ins.</span></span>
 

 

 <span data-ttu-id="2f202-p121">**Совет.** После того, как вы развернете размещаемую в SharePoint надстройку в вашей установке, при попытке запуска этого приложения вам может предлагаться войти со своими учетными данными. Чтобы такие предложения больше не появлялись, выполните действия, описанные в статье [При просмотре веб-сайта, использующего встроенную проверку подлинности и размещенного на сервере IIS 5.1 или более поздней версии, появляется сообщение об ошибке 401.1](http://support.microsoft.com/kb/896861).</span><span class="sxs-lookup"><span data-stu-id="2f202-p121">**TIP** After you deploy a SharePoint-hosted add-in to your installation, you may be prompted to log in with your credentials when you try to launch it. You will need to disable the loopback check to get rid of these prompts. See  [You receive error 401.1 when you browse a Web site that uses Integrated Authentication and is hosted on IIS 5.1 or a later version](http://support.microsoft.com/kb/896861) for instructions on how to disable the loopback check.</span></span>
 


## <a name="additional-resources"></a><span data-ttu-id="2f202-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2f202-217">Additional resources</span></span>
<span data-ttu-id="2f202-218"><a name="SP15SetupSPO365_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2f202-218"></span></span>


-  [<span data-ttu-id="2f202-219">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f202-219">SharePoint Add-ins</span></span>](sharepoint-add-ins)
    
 
-  [<span data-ttu-id="2f202-220">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="2f202-220">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="2f202-221">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f202-221">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
    
 

 

 

