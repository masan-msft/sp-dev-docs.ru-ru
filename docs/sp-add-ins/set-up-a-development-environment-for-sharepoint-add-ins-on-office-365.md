---
title: Настройка среды разработки надстроек SharePoint в Office 365
description: Установите Visual Studio и получите подписку разработчика Office 365.
ms.date: 03/14/2018
ms.prod: sharepoint
ms.openlocfilehash: 47fa3a86561f77094029995569d0b8f62a89bf89
ms.sourcegitcommit: ad9b18a3fc81d9561383413644120e7255d31d61
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/17/2018
---
# <a name="set-up-a-development-environment-for-sharepoint-add-ins-on-office-365"></a><span data-ttu-id="d5260-103">Настройка среды разработки надстроек SharePoint в Office 365</span><span class="sxs-lookup"><span data-stu-id="d5260-103">Set up a development environment for SharePoint Add-ins on Office 365</span></span>

<span data-ttu-id="d5260-104">Чтобы получить представление о доступных вариантах, прежде чем выполнять описанные в этой статье действия, см. статью [Средства и среды для разработки надстроек SharePoint](tools-and-environments-for-developing-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="d5260-104">To get an understanding of your options before you carry out any procedures in this article, see [Tools and environments for developing SharePoint Add-ins](tools-and-environments-for-developing-sharepoint-add-ins.md).</span></span> 

<span data-ttu-id="d5260-105">Если вы не уверены, какие надстройки SharePoint требуется создавать, см. статью [Надстройки SharePoint](sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="d5260-105">If you are not sure what kinds of SharePoint Add-ins you want to create, see [SharePoint Add-ins](sharepoint-add-ins.md).</span></span>
 
<span data-ttu-id="d5260-106"><a name="devenv_vs"> </a></span><span class="sxs-lookup"><span data-stu-id="d5260-106"><a name="devenv_vs"> </a></span></span>

## <a name="install-visual-studio-and-tools-on-your-computer"></a><span data-ttu-id="d5260-107">Установка Visual Studio и инструментов на компьютере</span><span class="sxs-lookup"><span data-stu-id="d5260-107">Install Visual Studio and tools on your computer</span></span>

- <span data-ttu-id="d5260-108">Если вы еще не установили **Visual Studio** 2013 или более поздней версии, сделайте это, следуя инструкциям из статьи [Установка Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="d5260-108">If you don't already have **Visual Studio** 2013 or later installed, install it by using the instructions at [Install Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="d5260-109">Рекомендуем использовать [последнюю версию из Центра загрузки Майкрософт](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="d5260-109">We recommend using the [latest version from the Microsoft Download Center](https://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span>
 
- <span data-ttu-id="d5260-110">Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d5260-110">Visual Studio includes the **Microsoft Office Developer Tools for Visual Studio**.</span></span> <span data-ttu-id="d5260-111">Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5260-111">Sometimes a version of the tools is released between updates of Visual Studio.</span></span> <span data-ttu-id="d5260-112">Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015).</span><span class="sxs-lookup"><span data-stu-id="d5260-112">To be sure that you have the latest version of the tools, run the [installer for Office Developer Tools for Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013), or the [installer for Office Developer Tools for Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).</span></span> 

<span data-ttu-id="d5260-113">Сверяйтесь с [более ранними версиями Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) или другой [документацией по Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/).</span><span class="sxs-lookup"><span data-stu-id="d5260-113">Reference [earlier versions of Visual Studio](http://msdn.microsoft.com/library/da049020-cfda-40d7-8ff4-7492772b620f.aspx) or other [Visual Studio documentation](https://docs.microsoft.com/ru-RU/visualstudio/).</span></span> 

### <a name="verbose-logging-in-visual-studio"></a><span data-ttu-id="d5260-114">Подробное ведение журнала в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5260-114">Verbose logging in Visual Studio</span></span>

<span data-ttu-id="d5260-115">Выполните указанные ниже действия, чтобы включить подробное ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="d5260-115">Follow these steps if you want to turn on verbose logging:</span></span>

1. <span data-ttu-id="d5260-116">Откройте реестр и перейдите к разделу **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, где _nn.n_ — это номер версии Visual Studio, например 12.0 или 14.0.</span><span class="sxs-lookup"><span data-stu-id="d5260-116">Open the registry, and go to **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\ _nn.n_\SharePointTools**, where _nn.n_ is the version of Visual Studio, such as 12.0 or 14.0.</span></span>

2. <span data-ttu-id="d5260-117">Добавьте ключ DWORD под названием **EnableDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="d5260-117">Add a DWORD key named **EnableDiagnostics**.</span></span>

3. <span data-ttu-id="d5260-118">Присвойте ключу значение **1**.</span><span class="sxs-lookup"><span data-stu-id="d5260-118">Give the key the value **1**.</span></span>

<span data-ttu-id="d5260-119">Путь реестра в будущих версиях Visual Studio изменится.</span><span class="sxs-lookup"><span data-stu-id="d5260-119">The registry path will change in future versions of Visual Studio.</span></span>


<span data-ttu-id="d5260-120"><a name="o365_signup"> </a></span><span class="sxs-lookup"><span data-stu-id="d5260-120"></span></span>

## <a name="sign-up-for-an-office-365-developer-subscription"></a><span data-ttu-id="d5260-121">Получение подписки разработчика Office 365</span><span class="sxs-lookup"><span data-stu-id="d5260-121">Sign up for an Office 365 Developer Subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5260-122">Возможно, у вас уже есть доступ к подписке разработчика Office 365:</span><span class="sxs-lookup"><span data-stu-id="d5260-122">You might already have access to an Office 365 Developer Site:</span></span> 
> - <span data-ttu-id="d5260-123">**У вас есть подписка на Visual Studio (MSDN)?**</span><span class="sxs-lookup"><span data-stu-id="d5260-123">**Are you a Visual Studio (MSDN) subscriber?**</span></span> <span data-ttu-id="d5260-124">Подписчики Visual Studio Ultimate и Visual Studio Premium с MSDN получают подписку разработчика Office 365 бесплатно.</span><span class="sxs-lookup"><span data-stu-id="d5260-124">Are you an MSDN subscriber? Visual Studio Ultimate and Visual Studio Premium with MSDN subscribers receive an Office 365 Developer Subscription as a benefit. Redeem your benefit today.</span></span> <span data-ttu-id="d5260-125">[Воспользуйтесь этим преимуществом сегодня](https://msdn.microsoft.com/subscriptions/manage/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5260-125"> Redeem your benefit today. https://msdn.microsoft.com/subscriptions/manage/default.aspx </span></span> 
> - <span data-ttu-id="d5260-126">**У вас есть один из указанных ниже планов подписки на Office 365?**</span><span class="sxs-lookup"><span data-stu-id="d5260-126">**Do you have one of the following Office 365 subscription plans?**</span></span> <span data-ttu-id="d5260-127">[Создайте сайт разработчика, используя имеющуюся подписку на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="d5260-127">For more information, see [Create a developer site on an existing Office 365 subscription](create-a-developer-site-on-an-existing-office-365-subscription.md).</span></span> 

<span data-ttu-id="d5260-128">Чтобы получить план Office 365:</span><span class="sxs-lookup"><span data-stu-id="d5260-128">Two ways to get an Office 365 plan.</span></span> 

- <span data-ttu-id="d5260-129">[Зарегистрируйтесь в программе для разработчиков Office 365](https://developer.microsoft.com/ru-RU/office/dev-program).</span><span class="sxs-lookup"><span data-stu-id="d5260-129">Sign up for a one-year Office 365 developer account through the Office 365 Developer Program.</span></span>

- <span data-ttu-id="d5260-130">Пошаговые инструкции для принятия участия в этой программе, регистрации и настройки подписки см. в [документации по программе для разработчиков приложений для Office 365](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="d5260-130">See the [Office 365 Developer Program documentation](https://docs.microsoft.com/ru-RU/office/developer-program/office-365-developer-program) for step-by-step instructions about how to join the Office 365 Developer Program and sign up and configure your subscription.</span></span> 

### <a name="open-your-developer-site"></a><span data-ttu-id="d5260-131">Открытие сайта разработчика</span><span class="sxs-lookup"><span data-stu-id="d5260-131">Open your developer site</span></span> 
 
<span data-ttu-id="d5260-132">Перейдите по ссылке **Создание надстроек** в левом верхнем углу страницы, чтобы открыть сайт разработчика.</span><span class="sxs-lookup"><span data-stu-id="d5260-132">Select the **Build Add-ins** link in the upper-left corner of the page to open your Developer Site.</span></span> <span data-ttu-id="d5260-133">Открывшийся сайт должен выглядеть так, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="d5260-133">You should see a site that looks like the one in Figure 3.</span></span> <span data-ttu-id="d5260-134">Наличие на странице списка **Тестируемые надстройки** подтверждает, что веб-сайт был создан с помощью шаблона "Сайт разработчика" SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d5260-134">The **Add-ins in Testing** list on the page confirms that the website was made with the SharePoint Developer Site template.</span></span> <span data-ttu-id="d5260-135">Если вместо этого отображается обычный сайт группы, подождите несколько минут и перезагрузите сайт.</span><span class="sxs-lookup"><span data-stu-id="d5260-135">If you see a regular team site instead, wait a few minutes and then restart your site.</span></span>
    
> [!NOTE]
> <span data-ttu-id="d5260-136">Запишите URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5260-136">Make a note of the site's URL; it's used when you create SharePoint Add-ins projects in Visual Studio.</span></span>

<span data-ttu-id="d5260-137">**Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**</span><span class="sxs-lookup"><span data-stu-id="d5260-137">**Figure 3. Your Developer Site home page with the Add-ins in Testing list**</span></span>

![Снимок экрана: домашняя страница сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)
 

## <a name="see-also"></a><span data-ttu-id="d5260-139">См. также</span><span class="sxs-lookup"><span data-stu-id="d5260-139">See also</span></span>
<span data-ttu-id="d5260-140"><a name="SP15SetupSPO365_bk_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d5260-140"></span></span>

- [<span data-ttu-id="d5260-141">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5260-141">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)
- [<span data-ttu-id="d5260-142">Знакомство с созданием надстроек SharePoint с размещением у поставщика</span><span class="sxs-lookup"><span data-stu-id="d5260-142">Get started creating provider-hosted SharePoint Add-ins</span></span>](get-started-creating-provider-hosted-sharepoint-add-ins.md)
- [<span data-ttu-id="d5260-143">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5260-143">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md) 

    
 
