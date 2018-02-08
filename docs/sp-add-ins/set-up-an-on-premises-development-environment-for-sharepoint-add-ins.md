---
title: "Настройка локальной среды разработки надстроек SharePoint"
description: "Установка операционной системы и необходимых компонентов, а также настройка служб и изолированного домена надстройки."
ms.date: 11/03/2017
ms.prod: sharepoint
ms.openlocfilehash: 9d5ed586e02b108ada842518f54a90df6513f1f7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-an-on-premises-development-environment-for-sharepoint-add-ins"></a><span data-ttu-id="c4f76-103">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-103">Set up an on-premises development environment for SharePoint Add-ins</span></span>

<span data-ttu-id="c4f76-104">По сравнению с требованиями к рабочей среде, требования к среде разработки менее строгие, а их выполнение менее затратно. Поэтому в инструкциях, приведенных в этом разделе, нет сведений об установке в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c4f76-104">The requirements for a development environment are less stringent and costly than the requirements for a production environment, and the guidelines described here do not support a production environment installation.</span></span> 

<span data-ttu-id="c4f76-105">Инструкции по настройке установки SharePoint в рабочей среде см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c4f76-105">For the instructions to set up a production environment installation of SharePoint, see:</span></span>

- [<span data-ttu-id="c4f76-106">Обзор установки и настройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-106">Overview of SharePoint installation and configuration</span></span>](http://technet.microsoft.com/ru-RU/library/ee667264%28v=office.15%29)
- [<span data-ttu-id="c4f76-107">Требования к оборудованию и программному обеспечению для SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-107">Hardware and software requirements for SharePoint</span></span>](http://technet.microsoft.com/ru-RU/library/cc262485%28v=office.15%29)
- [<span data-ttu-id="c4f76-108">Настройка среды для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-108">Configure an environment for SharePoint Add-ins</span></span>](http://technet.microsoft.com/ru-RU/library/fp161236%28office.15%29.aspx) 

<span data-ttu-id="c4f76-109"><a name="bk_installOS"> </a></span><span class="sxs-lookup"><span data-stu-id="c4f76-109"><a name="bk_installOS"> </a></span></span>
## <a name="install-the-operating-system-for-your-development-environment-for-sharepoint-add-ins"></a><span data-ttu-id="c4f76-110">Установка операционной системы для среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-110">Install the operating system for your development environment for SharePoint Add-ins</span></span>

<span data-ttu-id="c4f76-111">Во всех средах разработки для установки и запуска SharePoint необходимо использовать компьютер с ЦП, поддерживающим архитектуру x64, и с ОЗУ не менее, чем на 16 ГБ. Рекомендуется ОЗУ на 24 ГБ.</span><span class="sxs-lookup"><span data-stu-id="c4f76-111">In any development environment, you should use a computer with an x64-capable CPU, and at least 16 GB of RAM to install and run SharePoint; 24 GB of RAM is preferable.</span></span>

<span data-ttu-id="c4f76-112">В зависимости от конкретных требований и бюджета можно выбрать какой-либо из следующих вариантов.</span><span class="sxs-lookup"><span data-stu-id="c4f76-112">Depending on your specific requirements and budget, you can choose from the following options:</span></span>

- <span data-ttu-id="c4f76-113">Установка SharePoint на сервере с Windows Server 2008 R2 с пакетом обновления 1 (64-разрядной версии) или Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="c4f76-113">Install SharePoint on Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012.</span></span>
 
- <span data-ttu-id="c4f76-114">Использование Microsoft Hyper-V и установка SharePoint на виртуальной машине под управлением гостевой ОС Windows Server 2012 или Windows Server 2008 R2 64-разрядной версии с пакетом обновления 1.</span><span class="sxs-lookup"><span data-stu-id="c4f76-114">Use Microsoft Hyper-V and install SharePoint on a virtual machine running a Windows Server 2008 R2 Service Pack 1 x64 or a Windows Server 2012 guest operating system.</span></span> <span data-ttu-id="c4f76-115">Руководство по настройке виртуальной машины Microsoft Hyper-V для SharePoint см. в статье [Использование рекомендованных конфигураций для виртуальных машин SharePoint и среды Hyper-V](http://technet.microsoft.com/ru-RU/library/ff621103%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4f76-115">For guidance on setting up a Microsoft Hyper-V virtual machine for SharePoint, see [Use best practice configurations for the SharePoint virtual machines and Hyper-V environment](http://technet.microsoft.com/ru-RU/library/ff621103%28v=office.15%29.aspx).</span></span> 
    
> [!NOTE]
> <span data-ttu-id="c4f76-116">Установка SharePoint поддерживается только в Windows Server 2008 R2 64-разрядной версии с пакетом обновления 1 или в Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="c4f76-116">Installation of SharePoint is supported only on Windows Server 2008 R2 Service Pack 1 x64 or Windows Server 2012.</span></span> <span data-ttu-id="c4f76-117">Если вы хотите разрабатывать надстройки SharePoint для SharePoint в Windows 7 или Windows 8, можно получить доступ к Сайту разработчика Office 365 и разрабатывать надстройки удаленно.</span><span class="sxs-lookup"><span data-stu-id="c4f76-117">If you want to develop SharePoint Add-ins for SharePoint on Windows 7 or Windows 8, you can sign up for an Office 365 Developer Site and develop add-ins remotely.</span></span> 

<span data-ttu-id="c4f76-118"><a name="bk_prereqsOS"> </a></span><span class="sxs-lookup"><span data-stu-id="c4f76-118"><a name="bk_prereqsOS"> </a></span></span>
## <a name="install-the-prerequisites-for-the-operating-system-and-sharepoint"></a><span data-ttu-id="c4f76-119">Установка необходимых компонентов для операционной системы и SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-119">Install the prerequisites for the operating system and SharePoint</span></span>

1. <span data-ttu-id="c4f76-120">Запустите средство PrerequisiteInstaller.exe, включенное в установочные файлы.</span><span class="sxs-lookup"><span data-stu-id="c4f76-120">Run the PrerequisiteInstaller.exe tool that is included with your installation files.</span></span>

2. <span data-ttu-id="c4f76-121">Запустите средство Setup.exe, включенное в ваши установочные файлы.</span><span class="sxs-lookup"><span data-stu-id="c4f76-121">Run the Setup.exe tool that is included with your installation files.</span></span>

3. <span data-ttu-id="c4f76-122">Примите условия лицензионного соглашения на использование программного обеспечения корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c4f76-122">Accept the Microsoft Software License Terms.</span></span>

4. <span data-ttu-id="c4f76-123">На странице **Выберите нужный тип установки** выберите вариант **Изолированная**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-123">On the **Choose the installation you want** page, select **Stand-alone**.</span></span>
    
   <span data-ttu-id="c4f76-124">*Рис. 1. Выбор варианта установки*</span><span class="sxs-lookup"><span data-stu-id="c4f76-124">*Figure 1. Installation type choice*</span></span>

   ![Тип сервера установки SharePoint](../images/SP15_app_ServerType.gif)

5. <span data-ttu-id="c4f76-p103">Если во время установки возникают какие-либо ошибки, просмотрите файл журнала. Чтобы найти его, откройте окно командной строки и введите следующие команды. Ссылка на файл журнала появляется также после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="c4f76-p103">If any errors occur in the installation, review the log file. To find the log file, open a Command Prompt window, and then type the following commands at the command prompt. A link to the log file also appears when the installation is complete.</span></span>
    
   ```
     cd %temp%
   dir /od *.log
   ```

6. <span data-ttu-id="c4f76-129">После завершения установки вам будет предложено запустить мастер настройки продуктов и технологий SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c4f76-129">After the installation is complete, you're prompted to start the SharePoint Products and Technologies Configuration Wizard.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="c4f76-130">Если установка выполняется на компьютере, который подсоединен к домену, но не подключен к контроллеру домена, работа мастера настройки продуктов и технологий SharePoint может завершиться с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c4f76-130">The SharePoint Products and Technologies Configuration Wizard may fail if you're using a computer that is joined to a domain but that is not connected to a domain controller.</span></span> <span data-ttu-id="c4f76-131">В этом случае подключитесь к контроллеру домена напрямую или через виртуальную частную сеть (VPN) либо выполните вход, используя локальную учетную запись с правами администратора на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c4f76-131">If you see this failure, connect to a domain controller either directly or through a Virtual Private Network (VPN) connection, or sign in with a local account that has administrative privileges on the computer.</span></span>

7. <span data-ttu-id="c4f76-132">После завершения работы мастера откроется страница **Выбор шаблона** нового сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c4f76-132">After the configuration wizard is complete, you see the **Template Selection** page of the new SharePoint site.</span></span> <span data-ttu-id="c4f76-133">На этой странице выберите шаблон **Сайт разработчика**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-133">On this page, select the **Developer Site** template.</span></span> <span data-ttu-id="c4f76-134">Надстройки SharePoint можно развертывать на Сайте разработчика только с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4f76-134">You can only deploy SharePoint Add-ins from Visual Studio to a Developer Site.</span></span>
    
   <span data-ttu-id="c4f76-135">*Рис. 2. Страница выбора шаблона сайта*</span><span class="sxs-lookup"><span data-stu-id="c4f76-135">*Figure 2. Select the site template page*</span></span>

   ![Страница шаблонов сайта](../images/SP15_appChooseSiteTemplate.gif)

<span data-ttu-id="c4f76-137"><a name="Servertoserver"> </a></span><span class="sxs-lookup"><span data-stu-id="c4f76-137"><a name="Servertoserver"> </a></span></span>
## <a name="configure-services-in-sharepoint-for-server-to-server-add-in-use"></a><span data-ttu-id="c4f76-138">Настройка служб в SharePoint для межсерверного использования надстроек</span><span class="sxs-lookup"><span data-stu-id="c4f76-138">Configure services in SharePoint for server-to-server add-in use</span></span>

<span data-ttu-id="c4f76-139">На этом этапе службы в SharePoint настраиваются для межсерверного использования надстроек.</span><span class="sxs-lookup"><span data-stu-id="c4f76-139">In this step, you configure services in SharePoint for server-to-server add-in use.</span></span> <span data-ttu-id="c4f76-140">Это позволяет создавать размещаемые у поставщиков надстройки с высоким уровнем доверия в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="c4f76-140">These steps ensure that you will be able to create high trust provider-hosted add-ins with your installation.</span></span> <span data-ttu-id="c4f76-141">Дополнительные сведения о создании таких надстроек см. в статье [Создание надстроек с высоким уровнем доверия для SharePoint](create-high-trust-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="c4f76-141">For more information about creating this kind of add-in, see [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins.md).</span></span>

<span data-ttu-id="c4f76-142">Настройте службу управления приложениями и приложение профилей пользователей (такое название службы связано с тем, что изначально надстройки SharePoint назывались "приложениями для SharePoint").</span><span class="sxs-lookup"><span data-stu-id="c4f76-142">Ensure that the App Management Service and user profile application are configured (it is called "App Management Service" because SharePoint Add-ins were originally named "apps for SharePoint").</span></span> <span data-ttu-id="c4f76-143">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c4f76-143">The steps are as follows:</span></span>
    
1. <span data-ttu-id="c4f76-144">В **центре администрирования** выберите пункт **Управление приложениями-службами** в разделе **Управление приложениями**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-144">In **Central Administration**, under **Application Management**, select **Manage service applications**.</span></span>
   
2. <span data-ttu-id="c4f76-145">На странице **Приложения-службы** убедитесь в том, что запущены следующие службы:</span><span class="sxs-lookup"><span data-stu-id="c4f76-145">On the **Service Applications** page, ensure that the following services are started:</span></span>
   
   - <span data-ttu-id="c4f76-146">Приложение-служба профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="c4f76-146">User Profile Service Application</span></span>
   - <span data-ttu-id="c4f76-147">Служба управления приложениями</span><span class="sxs-lookup"><span data-stu-id="c4f76-147">App Management Service</span></span>
    
3. <span data-ttu-id="c4f76-148">В разделе **Управление приложениями** выберите пункт **Управление службами на сервере**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-148">Under **Application Management**, select **Manage services on server**.</span></span> 
   
4. <span data-ttu-id="c4f76-149">На странице **Службы на сервере** убедитесь в том, что запущены следующие службы:</span><span class="sxs-lookup"><span data-stu-id="c4f76-149">On the **Services on Server** page, ensure that the following services are started:</span></span>
    
   - <span data-ttu-id="c4f76-150">Служба профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="c4f76-150">User Profile Service</span></span> 

<span data-ttu-id="c4f76-p108">Убедитесь в том, что в **приложении-службе профилей пользователей** создан по крайней мере один профиль. Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="c4f76-p108">Ensure that at least one profile is created in the **User Profile Service Application**. The steps are as follows:</span></span>
    
1. <span data-ttu-id="c4f76-153">В **центре администрирования** в разделе **Управление приложениями** выберите пункт **Управление приложениями-службами**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-153">In **Central Administration**, under **Application Management**, select **Manage service applications**.</span></span>
    
2. <span data-ttu-id="c4f76-154">Затем выберите пункт **Приложение-служба профилей пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-154">Next, select **User Profile Service Application**.</span></span>
    
3. <span data-ttu-id="c4f76-155">На странице **Служба управления профилями: приложение-служба профилей пользователей** в разделе **Люди** выберите пункт **Управление профилями пользователей**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-155">On the **Manage Profile Service: User Profile Service Application** page, under **People**, select **Manage User Profiles**.</span></span>
    
4. <span data-ttu-id="c4f76-156">На странице **Управление профилями пользователей** нажмите кнопку **Создать профили**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-156">On the **Manage User Profiles** page, select **New Profiles**.</span></span>
    
5. <span data-ttu-id="c4f76-157">На странице **Добавление профиля пользователя** введите имя своей учетной записи и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c4f76-157">On the **Add User Profile** page, type your account name and email address.</span></span>
    
6. <span data-ttu-id="c4f76-158">Нажмите кнопку **Сохранить и закрыть**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-158">Select **Save and Close**.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="c4f76-159">Если появится сообщение о том, что профиль, который вы пытаетесь создать, уже существует, нажмите **Отменить и вернуться**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-159">If you get a message saying that the profile you are trying to create already exists, select **Cancel and Go Back**.</span></span>

7. <span data-ttu-id="c4f76-160">Когда вы вернетесь на страницу **Управление профилями пользователей**, должно отобразиться сообщение **Общее число профилей: 1**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-160">Back on the **Manage User Profiles** page, you should see **Total number of profiles: 1**.</span></span>
    

<span data-ttu-id="c4f76-161"><a name="SP15Appdevonprem_bk_installVS"> </a></span><span class="sxs-lookup"><span data-stu-id="c4f76-161"><a name="SP15Appdevonprem_bk_installVS"> </a></span></span> 
## <a name="install-visual-studio-and-office-developer-tools-for-visual-studio"></a><span data-ttu-id="c4f76-162">Установка Visual Studio и Инструментов разработчика Office для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4f76-162">Install Visual Studio and Office Developer Tools for Visual Studio</span></span>

- <span data-ttu-id="c4f76-163">Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это согласно инструкциям на странице [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="c4f76-163">If you don't already have **Visual Studio** 2013 or later installed, install it with the instructions at [Install Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="c4f76-164">Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="c4f76-164">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>

- <span data-ttu-id="c4f76-165">В состав Visual Studio входят **Инструменты разработчика Microsoft Office для Visual Studio**, но иногда выход новой версии инструментов не совпадает с выходом обновлений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c4f76-165">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**, but sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="c4f76-166">Чтобы убедиться, что вы используете последнюю версию инструментов, запустите [установщик Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [установщик Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="c4f76-166">To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) or the [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span>

### <a name="verbose-logging-in-visual-studio"></a><span data-ttu-id="c4f76-167">Подробное ведение журнала в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4f76-167">Verbose logging in Visual Studio</span></span>

<span data-ttu-id="c4f76-168">Выполните указанные ниже действия, чтобы включить подробное ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="c4f76-168">Follow these steps if you want to turn on verbose logging:</span></span>

1. <span data-ttu-id="c4f76-169">Откройте реестр и перейдите к разделу **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, где _nn.n_ — это номер версии Visual Studio, например 12.0 или 14.0.</span><span class="sxs-lookup"><span data-stu-id="c4f76-169">Open the registry, and go to **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, where _nn.n_ is the version of Visual Studio, such as 12.0 or 14.0.</span></span>

2. <span data-ttu-id="c4f76-170">Добавьте ключ DWORD под названием **EnableDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-170">Add a DWORD key named **EnableDiagnostics**.</span></span>

3. <span data-ttu-id="c4f76-171">Присвойте ключу значение **1**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-171">Give the key the value **1**.</span></span>

<span data-ttu-id="c4f76-172">Путь реестра в будущих версиях Visual Studio изменится.</span><span class="sxs-lookup"><span data-stu-id="c4f76-172">The registry path will change in future versions of Visual Studio.</span></span>

<span data-ttu-id="c4f76-173"><a name="SP15appdevonprem_bk_configure"> </a></span><span class="sxs-lookup"><span data-stu-id="c4f76-173"><a name="SP15appdevonprem_bk_configure"> </a></span></span>
## <a name="configure-an-isolated-add-in-domain-in-sharepoint"></a><span data-ttu-id="c4f76-174">Настройка изолированного домена надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-174">Configure an isolated add-in domain in SharePoint</span></span>

<span data-ttu-id="c4f76-175">Прежде чем выполнять процедуры, описанные в этом разделе, ознакомьтесь с информацией в статье [Хост-сайты, сайты надстроек и изолированный домен](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain).</span><span class="sxs-lookup"><span data-stu-id="c4f76-175">Before you carry out any procedures in this section, read [Host webs, add-in webs, and the isolated domain](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain).</span></span>

<span data-ttu-id="c4f76-p111">Требуется создать изолированный домен в вашей тестовой ферме SharePoint. Кроме того, для установки SharePoint требуется общий домен с заголовком узла с подстановочными знаками, где можно выполнять подготовку надстроек, размещаемых в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c4f76-p111">You must create an isolated domain in your test SharePoint farm. Also, your SharePoint installation needs a general wildcard host header domain where it can provision SharePoint-hosted add-ins.</span></span>

<span data-ttu-id="c4f76-p112">В целях разработки можно изменить свой файл Hosts при необходимости, чтобы сделать возможной маршрутизацию с компьютера разработки к тестовому экземпляру Надстройка SharePoint. Visual Studio изменяет файл Hosts автоматически при создании и развертывании надстройки.</span><span class="sxs-lookup"><span data-stu-id="c4f76-p112">For development purposes, you can modify your hosts file as you need to route your development computer to a test instance of a SharePoint Add-in. Visual Studio modifies your hosts file automatically when you build and deploy the add-in.</span></span> 
 
> [!NOTE]
> <span data-ttu-id="c4f76-180">Для рабочих ферм необходимо создать стратегию маршрутизации DNS в интрасети и, возможно, настроить брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="c4f76-180">For production farms, you would have to create a DNS routing strategy within your intranet and optionally configure your firewall.</span></span> <span data-ttu-id="c4f76-181">Дополнительные сведения о создании и настройке рабочей среды для надстроек SharePoint см. в статье [Установка надстроек SharePoint и управление ими](http://technet.microsoft.com/ru-RU/library/fp161232%28v=office.15%29).</span><span class="sxs-lookup"><span data-stu-id="c4f76-181">For more information about how to create and configure a production environment for SharePoint Add-ins, see [Install and Manage SharePoint Add-ins](http://technet.microsoft.com/ru-RU/library/fp161232%28v=office.15%29).</span></span>

<span data-ttu-id="c4f76-182">Выполните действия, описанные в следующем разделе, чтобы создать изолированный домен надстройки.</span><span class="sxs-lookup"><span data-stu-id="c4f76-182">Perform the steps in the following procedure to create an isolated add-in domain.</span></span>
 
> [!NOTE]
> <span data-ttu-id="c4f76-183">Все эти действия необходимо выполнять от имени администратора фермы, а командную строку и командную консоль SharePoint необходимо запускать от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="c4f76-183">You must perform all the steps in the following procedure while signed in as the farm administrator, and you must run the command prompt and the SharePoint Management Shell as an administrator.</span></span>

### <a name="create-an-isolated-add-in-domain-on-your-development-computer"></a><span data-ttu-id="c4f76-184">Создание изолированного домена надстройки на компьютере для разработки</span><span class="sxs-lookup"><span data-stu-id="c4f76-184">Create an isolated add-in domain on your development computer</span></span>

1. <span data-ttu-id="c4f76-185">Убедитесь, что запущены службы spadmin и sptimer. Для этого откройте командную строку и введите приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="c4f76-185">Ensure that the spadmin and sptimer services are running by opening a command prompt and entering the following commands:</span></span>
    
    ```
      net start spadminv4
      net start sptimerv4
    ```

2. <span data-ttu-id="c4f76-186">Создайте изолированный домен надстройки, запустив командную консоль SharePoint от имени администратора и выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c4f76-186">Create your isolated add-in domain by running the SharePoint Management Shell as an administrator and entering the following command.</span></span>

   <span data-ttu-id="c4f76-187">Замените _contosoaddins.com_ доменом вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="c4f76-187">Replace the  _contosoaddins.com_ with your add-in domain.</span></span> <span data-ttu-id="c4f76-188">Это *не* должен быть поддомен несущего домена SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c4f76-188">It should *not* be a subdomain of the host SharePoint domain.</span></span> <span data-ttu-id="c4f76-189">В противном случае будет утрачено большинство преимуществ безопасности изолированных доменов надстроек.</span><span class="sxs-lookup"><span data-stu-id="c4f76-189">Doing so largely defeats the security advantages of having isolated add-in domains.</span></span> <span data-ttu-id="c4f76-190">Например, если имя несущего домена — contoso.com, не используйте addins.contoso.com в качестве домена надстроек.</span><span class="sxs-lookup"><span data-stu-id="c4f76-190">For example, if the host domain is contoso.com, do not use addins.contoso.com as the add-in domain.</span></span>
    
    ```
      Set-SPAppDomain "contosoaddins.com"
    ```

3. <span data-ttu-id="c4f76-191">Убедитесь, что запущены службы SPSubscriptionSettingsService и AppManagementServiceInstance. Для этого введите в командной консоли SharePoint приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c4f76-191">Ensure that the SPSubscriptionSettingsService and AppManagementServiceInstance services are running by entering the following command in the SharePoint Management Shell:</span></span>
    
    ```
      Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"} | Start-SPServiceInstance
    ```

4. <span data-ttu-id="c4f76-192">Убедитесь, что запущены службы SPSubscriptionSettingsService и AppManagementServiceInstance. Для этого введите в командной консоли SharePoint приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c4f76-192">Verify that the SPSubscriptionSettingsService and AppManagementServiceInstance services are running by entering the following command in the SharePoint Management Shell.</span></span> <span data-ttu-id="c4f76-193">Результат выполнения команды покажет, подключена ли каждая служба.</span><span class="sxs-lookup"><span data-stu-id="c4f76-193">The output will indicate whether each service is online.</span></span>
    
    ```
      Get-SPServiceInstance | where{$_.GetType().Name -eq "AppManagementServiceInstance" -or $_.GetType().Name -eq "SPSubscriptionSettingsServiceInstance"}
    ```

5. <span data-ttu-id="c4f76-194">Необходимо указать учетную запись, в которой будут выполняться экземпляры служб SPSubscriptionService и AppManagementServiceInstance.</span><span class="sxs-lookup"><span data-stu-id="c4f76-194">You must specify an account under which the SPSubscriptionService and AppManagementServiceInstance service instances will run.</span></span> <span data-ttu-id="c4f76-195">Это должна быть учетная запись SPManagedAccount.</span><span class="sxs-lookup"><span data-stu-id="c4f76-195">This account must be an SPManagedAccount.</span></span> <span data-ttu-id="c4f76-196">Чтобы создать учетную запись SPManagedAccount, введите в командной консоли SharePoint приведенную ниже команду (вам будет предложено указать имя пользователя или домен учетной записи, а также пароль).</span><span class="sxs-lookup"><span data-stu-id="c4f76-196">You can create an SPManagedAccount by entering the following command in the SharePoint Management Shell (you'll be prompted for the account domain\user and password):</span></span>
    
    ```
      $account = New-SPManagedAccount
    ```

6. <span data-ttu-id="c4f76-p117">Укажите параметры учетной записи, пула приложений и базы данных для служб SPSubscriptionService и AppManagementServiceInstance, введя следующий код в командной консоли SharePoint. Если в предыдущем действии была создана учетная запись SPManagedAccount, используйте здесь ее имя.</span><span class="sxs-lookup"><span data-stu-id="c4f76-p117">Specify an account, application pool, and database settings for the SPSubscriptionService and AppManagementServiceInstance services by typing the following code in the SharePoint Management Shell. If you created a SPManagedAccount in the preceding step, use that account name here.</span></span>
    
    ```
     $account = Get-SPManagedAccount "domain\user" 
     $appPoolSubSvc = New-SPServiceApplicationPool -Name SettingsServiceAppPool -Account $account
     $appPoolAppSvc = New-SPServiceApplicationPool -Name AppServiceAppPool -Account $account
     $appSubSvc = New-SPSubscriptionSettingsServiceApplication -ApplicationPool $appPoolSubSvc -Name SettingsServiceApp -DatabaseName SettingsServiceDB 
     $proxySubSvc = New-SPSubscriptionSettingsServiceApplicationProxy -ServiceApplication $appSubSvc
     $appAppSvc = New-SPAppManagementServiceApplication -ApplicationPool $appPoolAppSvc -Name AppServiceApp -DatabaseName AppServiceDB
     $proxyAppSvc = New-SPAppManagementServiceApplicationProxy -ServiceApplication $appAppSvc

    ```

7. <span data-ttu-id="c4f76-199">Укажите префикс надстройки (см. статью [Хост-сайты, сайты надстроек и изолированный домен](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain)). Для этого введите приведенный ниже код в командной консоли SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c4f76-199">Specify your add-in prefix (see [Host webs, add-in webs, and the isolated domain](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md#IsolatedDomain)) by typing the following code in the SharePoint Management Shell:</span></span>
    
    ```
      Set-SPAppSiteSubscriptionName -Name "add-in" -Confirm:$false
    ```

<span data-ttu-id="c4f76-p118">**Выполните следующую процедуру, только если в вашей среде используется прокси-сервер.** После создания изолированного домена надстроек выполните действия, приведенные в следующей процедуре, чтобы добавить этот домен в список обхода в Internet Explorer. Это гарантирует, что вы сможете переходить к этому домену после развертывания надстройки, размещенной в SharePoint, или надстройки, размещенной у поставщика, которая содержит сайт надстройки.</span><span class="sxs-lookup"><span data-stu-id="c4f76-p118">**Carry out the following procedure only if your environment uses a proxy server.** After you create your isolated add-in domain, perform the steps in the following procedure to add that domain to your bypass list in Internet Explorer. This ensures that you can navigate to this domain after you deploy a SharePoint-hosted add-in or a provider-hosted add-in that includes an add-in web.</span></span>

### <a name="add-your-isolated-add-in-domain-to-your-bypass-list-in-internet-explorer"></a><span data-ttu-id="c4f76-203">Добавление изолированного домена надстройки в список обхода в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c4f76-203">Add your isolated add-in domain to your bypass list in Internet Explorer</span></span>

1. <span data-ttu-id="c4f76-204">В Internet Explorer откройте меню **Сервис**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-204">In Internet Explorer, go to **Tools**.</span></span>

2. <span data-ttu-id="c4f76-205">Выберите пункт **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-205">Select **Internet options**.</span></span>

3. <span data-ttu-id="c4f76-206">На вкладке **Подключения** нажмите кнопку **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-206">On the **Connections** tab, select the **LAN Settings** button.</span></span>

4. <span data-ttu-id="c4f76-207">Снимите флажок **Автоматическое определение параметров**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-207">Clear the **Automatically detect settings** check box.</span></span>

5. <span data-ttu-id="c4f76-208">Установите флажок **Использовать прокси-сервер для локальных подключений**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-208">Select the **Use a proxy server for your LAN** check box.</span></span>

6. <span data-ttu-id="c4f76-209">Нажмите кнопку **Дополнительно** и добавьте адрес \*.Ваш_домен_надстроек.com в список **Исключения**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-209">Select the **Advanced** button, and then add \*.YourAddinsDomain.com to the **Exceptions** list.</span></span>

7. <span data-ttu-id="c4f76-210">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-210">Select **OK**.</span></span>

8. <span data-ttu-id="c4f76-211">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Настройка параметров локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-211">Select **OK** to close the **Local Area Network (LAN) Settings** dialog box.</span></span>

9. <span data-ttu-id="c4f76-212">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="c4f76-212">Select **OK** to close the **Internet Options** dialog box.</span></span>
    
<span data-ttu-id="c4f76-213">Сведения о доступных вариантах развертывания надстроек см. в статье [Развертывание и установка надстроек SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span><span class="sxs-lookup"><span data-stu-id="c4f76-213">For information about your options for deploying your add-ins, see [Deploying and installing SharePoint Add-ins: methods and options](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).</span></span>
 
> [!TIP]
> <span data-ttu-id="c4f76-214">Когда вы развернете размещаемую в SharePoint надстройку в среде установки и попробуете запустить эту надстройку, вам может быть предложено войти со своими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="c4f76-214">After you deploy a SharePoint-hosted add-in to your installation, you may be prompted to sign in with your credentials when you try to launch it.</span></span> <span data-ttu-id="c4f76-215">Чтобы такие предложения больше не появлялись, отключите проверки замыкания на себя.</span><span class="sxs-lookup"><span data-stu-id="c4f76-215">You need to disable the loopback check to get rid of these prompts.</span></span> <span data-ttu-id="c4f76-216">Инструкции по отключению таких проверок см. в статье [При просмотре веб-сайта, использующего встроенную проверку подлинности и размещенного на сервере IIS 5.1 или более поздней версии, появляется сообщение об ошибке 401.1](http://support.microsoft.com/kb/896861).</span><span class="sxs-lookup"><span data-stu-id="c4f76-216">For instructions about how to disable the loopback check, see [You receive error 401.1 when you browse a Web site that uses Integrated Authentication and is hosted on IIS 5.1 or a later version](http://support.microsoft.com/kb/896861).</span></span>
 

## <a name="see-also"></a><span data-ttu-id="c4f76-217">См. также</span><span class="sxs-lookup"><span data-stu-id="c4f76-217">See also</span></span>
<span data-ttu-id="c4f76-218"><a name="SP15SetupSPO365_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="c4f76-218"><a name="SP15SetupSPO365_bk_addlresources"> </a></span></span>

- [<span data-ttu-id="c4f76-219">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-219">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
- [<span data-ttu-id="c4f76-220">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="c4f76-220">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
- [<span data-ttu-id="c4f76-221">Знакомство с созданием надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="c4f76-221">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
- [<span data-ttu-id="c4f76-222">Установка более ранних версий Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4f76-222">Install earlier versions of Visual Studio</span></span>](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx)
- [<span data-ttu-id="c4f76-223">Документация по Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4f76-223">Visual Studio documentation</span></span>](https://docs.microsoft.com/ru-RU/visualstudio/)    
 
