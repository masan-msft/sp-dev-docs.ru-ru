---
title: "Настройка клиента Office 365"
description: "Настройте клиент Office 365, чтобы создавать и развертывать клиентские веб-части, используя SharePoint Framework."
ms.date: 01/08/2018
ms.prod: sharepoint
ms.openlocfilehash: ca2dc88c013458f79b7e27402f60d53b08261bac
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="a151a-103">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="a151a-103">Set up your Office 365 tenant</span></span>

<span data-ttu-id="a151a-104">Чтобы создавать и развертывать клиентские веб-части, используя SharePoint Framework, необходимо настроить клиент Office 365.</span><span class="sxs-lookup"><span data-stu-id="a151a-104">To build and deploy client-side web parts using the SharePoint Framework, you need an Office 365 tenant.</span></span> 

<span data-ttu-id="a151a-105">Если у вас уже есть клиент Office 365, переходите к разделу [Создание сайта каталога приложений](#create-app-catalog-site).</span><span class="sxs-lookup"><span data-stu-id="a151a-105">If you already have an Office 365 tenant, see [create app catalog site](#create-app-catalog-site).</span></span>

<span data-ttu-id="a151a-106">Если у вас нет клиента, создайте подписку или зарегистрируйтесь в [программе для разработчиков приложений для Microsoft Office 365](https://dev.office.com/devprogram).</span><span class="sxs-lookup"><span data-stu-id="a151a-106">If you don't have one, you can create a trial tenant or sign up for the [Microsoft Office 365 Developer Program](https://dev.office.com/devprogram).</span></span>  

> [!NOTE] 
> <span data-ttu-id="a151a-107">Перед регистрацией убедитесь, что вы вышли из всех имеющихся клиентов Office 365.</span><span class="sxs-lookup"><span data-stu-id="a151a-107">Make sure that you are signed out of any existing Office 365 tenants before you sign up.</span></span>

## <a name="create-app-catalog-site"></a><span data-ttu-id="a151a-108">Создание сайта каталога приложений</span><span class="sxs-lookup"><span data-stu-id="a151a-108">Create app catalog site</span></span>

<span data-ttu-id="a151a-109">Для отправки и развертывания веб-частей необходим каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="a151a-109">You need an app catalog to upload and deploy web parts.</span></span> <span data-ttu-id="a151a-110">Если вы уже настроили каталог приложений, переходите к разделу [Создание семейства веб-сайтов разработчика](#create-a-new-developer-site-collection).</span><span class="sxs-lookup"><span data-stu-id="a151a-110">If you've already set up an app catalog, see [create a new developer site collection](#create-a-new-developer-site-collection).</span></span>  

### <a name="to-create-an-app-catalog-site"></a><span data-ttu-id="a151a-111">Создание сайта каталога приложений</span><span class="sxs-lookup"><span data-stu-id="a151a-111">To create an app catalog site</span></span>

1. <span data-ttu-id="a151a-112">Откройте **Центр администрирования SharePoint**, указав в браузере приведенный ниже URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a151a-112">Go to the **SharePoint Admin Center** by entering the following URL in your browser.</span></span> <span data-ttu-id="a151a-113">Замените **yourtenantprefix** префиксом клиента разработчика приложений для Office 365.</span><span class="sxs-lookup"><span data-stu-id="a151a-113">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
    ```
    https://yourtenantprefix-admin.sharepoint.com
    ```
    
2. <span data-ttu-id="a151a-114">На боковой панели слева выберите пункт меню **Приложения**, а затем выберите **Каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="a151a-114">In the left sidebar, select the **apps** menu item, and then select **App Catalog**.</span></span>

3. <span data-ttu-id="a151a-115">Нажмите кнопку **ОК**, чтобы создать сайт каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="a151a-115">Select **OK** to create a new app catalog site.</span></span>

4. <span data-ttu-id="a151a-116">На следующей странице введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a151a-116">On the next page, enter the following details:</span></span>

    - <span data-ttu-id="a151a-117">**Название**. Введите **Каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="a151a-117">**Title**: Enter **App Catalog**.</span></span>
    - <span data-ttu-id="a151a-118">**_Суффикс_ адреса веб-сайта**: введите предпочитаемый суффикс каталога приложений, например **apps**.</span><span class="sxs-lookup"><span data-stu-id="a151a-118">**Web Site Address _suffix_**: Enter your preferred suffix for the app catalog; for example: **apps**.</span></span>
    - <span data-ttu-id="a151a-119">**Администратор**: введите имя пользователя и нажмите кнопку **Разрешить**, чтобы разрешить его.</span><span class="sxs-lookup"><span data-stu-id="a151a-119">**Administrator**: Enter your username, and then select the **resolve** button to resolve the username.</span></span>

5. <span data-ttu-id="a151a-120">Нажмите кнопку **ОК**, чтобы создать сайт каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="a151a-120">Select **OK** to create the app catalog site.</span></span>

<span data-ttu-id="a151a-121">SharePoint создаст сайт каталога приложений. Вы можете наблюдать за ходом его создания в Центре администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a151a-121">SharePoint creates the app catalog site, and you are able to see its progress in the SharePoint admin center.</span></span>

## <a name="create-a-new-developer-site-collection"></a><span data-ttu-id="a151a-122">Создание семейства веб-сайтов разработчика</span><span class="sxs-lookup"><span data-stu-id="a151a-122">Create a new developer site collection</span></span>

<span data-ttu-id="a151a-123">Для тестирования также понадобится семейство веб-сайтов и сайт.</span><span class="sxs-lookup"><span data-stu-id="a151a-123">You also need a site collection and a site for your testing.</span></span> <span data-ttu-id="a151a-124">Семейство веб-сайтов можно создать, используя любой из доступных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a151a-124">You can create a new site collection by using any of the available templates.</span></span> <span data-ttu-id="a151a-125">Мы можете использовать **семейство веб-сайтов разработчика**, но это излишне, так как базовое тестирование и тестирование в рабочей области можно выполнять на любом сайте.</span><span class="sxs-lookup"><span data-stu-id="a151a-125">You may choose to use **developer site collection**, but that does not really add additional value because workbench and basic testing can be performed under any site.</span></span>

### <a name="to-create-a-new-developer-site-collection"></a><span data-ttu-id="a151a-126">Создание семейства веб-сайтов разработчика</span><span class="sxs-lookup"><span data-stu-id="a151a-126">To create a new developer site collection</span></span>

1. <span data-ttu-id="a151a-127">Откройте **Центр администрирования SharePoint**, указав в браузере приведенный ниже URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="a151a-127">Go to the **SharePoint Admin Center** by entering the following URL in your browser.</span></span> <span data-ttu-id="a151a-128">Замените **yourtenantprefix** префиксом клиента разработчика приложений для Office 365.</span><span class="sxs-lookup"><span data-stu-id="a151a-128">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
    ```
    https://yourtenantprefix-admin.sharepoint.com
    ```
    
2. <span data-ttu-id="a151a-129">На ленте SharePoint выберите **Создать** > **Частное семейство веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="a151a-129">On the SharePoint ribbon, select **New** > **Private Site Collection**.</span></span>

3. <span data-ttu-id="a151a-130">В диалоговом окне введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a151a-130">In the dialog box, enter the following details:</span></span>

    - <span data-ttu-id="a151a-131">**Название**: введите название семейства сайтов разработчиков, например **Сайт разработчика**.</span><span class="sxs-lookup"><span data-stu-id="a151a-131">**Title**: Enter a title for your developer site collection; for example: **Developer Site**.</span></span>
    - <span data-ttu-id="a151a-132">**_Суффикс_ адреса веб-сайта**: введите суффикс семейства сайтов разработчиков, например **dev**.</span><span class="sxs-lookup"><span data-stu-id="a151a-132">**Web Site Address _suffix_**: Enter a suffix for your developer site collection; for example: **dev**.</span></span>
    - <span data-ttu-id="a151a-133">**Выбор шаблона**: выберите для семейства веб-сайтов шаблон **Сайт разработчика**.</span><span class="sxs-lookup"><span data-stu-id="a151a-133">**Template Selection**: Select **Developer Site** as the site collection template.</span></span>
    - <span data-ttu-id="a151a-134">**Администратор**: введите имя пользователя и нажмите кнопку **Разрешить**, чтобы разрешить его.</span><span class="sxs-lookup"><span data-stu-id="a151a-134">**Administrator**: Enter your username, and then select the **resolve** button to resolve the username.</span></span>

4. <span data-ttu-id="a151a-135">Нажмите кнопку **ОК**, чтобы создать семейство веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a151a-135">Select **OK** to create the site collection.</span></span>

<span data-ttu-id="a151a-136">SharePoint создаст сайт разработчика. Вы можете наблюдать за ходом его создания в Центре администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a151a-136">SharePoint creates the developer site and you are able to see its progress in the SharePoint admin center.</span></span> <span data-ttu-id="a151a-137">После создания сайта вы можете перейти к семейству веб-сайтов разработчика.</span><span class="sxs-lookup"><span data-stu-id="a151a-137">After the site is created, you can browse to your developer site collection.</span></span>

## <a name="sharepoint-workbench"></a><span data-ttu-id="a151a-138">SharePoint Workbench</span><span class="sxs-lookup"><span data-stu-id="a151a-138">SharePoint Workbench</span></span>

<span data-ttu-id="a151a-139">SharePoint Workbench — это рабочая область конструирования для разработчиков, которая позволяет быстро просматривать и проверять веб-части, не развертывая их в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a151a-139">SharePoint Workbench is a developer design surface that enables you to quickly preview and test web parts without deploying them in SharePoint.</span></span> <span data-ttu-id="a151a-140">Цепочка инструментов для разработчиков, доступная в SharePoint Framework, включает локальную версию Workbench, позволяющую быстро протестировать и проверить создаваемые решения.</span><span class="sxs-lookup"><span data-stu-id="a151a-140">SharePoint Framework developer toolchain contains a version of the Workbench that works locally and helps you quickly test and validate solutions that you are building.</span></span> <span data-ttu-id="a151a-141">Эта область размещается также в области клиентов, чтобы вы могли просматривать и проверять локальные веб-части, которые находятся в разработке.</span><span class="sxs-lookup"><span data-stu-id="a151a-141">It is also hosted in your tenancy to preview and test your local web parts in development.</span></span> <span data-ttu-id="a151a-142">Получить доступ к SharePoint Workbench можно на любом сайте SharePoint в своей области клиентов, перейдя по такому URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="a151a-142">You can access the SharePoint Workbench from any SharePoint site in your tenancy by browsing to the following URL:</span></span>

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a><span data-ttu-id="a151a-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a151a-143">Next steps</span></span>

<span data-ttu-id="a151a-144">Теперь, когда вы настроили клиент SharePoint, [настройте среду разработки](./set-up-your-development-environment.md) для сборки клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="a151a-144">Now that you have configured your SharePoint tenant, [set up your development environment](./set-up-your-development-environment.md) to build client-side web parts.</span></span>
