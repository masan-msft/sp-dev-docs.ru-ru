---
title: "Настройка клиента Office 365"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 77de8b0b91c0c67cb9149bd5bbc38b21c1e432f9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-your-office-365-tenant"></a><span data-ttu-id="64d88-102">Настройка клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="64d88-102">Set up your Office 365 tenant</span></span>

<span data-ttu-id="64d88-103">Для создания и развертывания клиентских веб-частей с помощью предварительного выпуска платформы SharePoint Framework необходим обычный клиент Office 365.</span><span class="sxs-lookup"><span data-stu-id="64d88-103">To build and deploy client-side web parts using the preview release of the SharePoint Framework, you will need a normal Office 365 tenant.</span></span> 

## <a name="sign-up-for-an-office-365-tenant"></a><span data-ttu-id="64d88-104">Регистрация клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="64d88-104">Sign up for an Office 365 tenant</span></span>
<span data-ttu-id="64d88-105">Если у вас уже есть клиент Office 365, переходите к разделу [Создание сайта каталога приложений](#create-app-catalog-site).</span><span class="sxs-lookup"><span data-stu-id="64d88-105">If you already have an Office 365 tenant, see [create your app catalog site](#create-app-catalog-site).</span></span>

<span data-ttu-id="64d88-106">В противном случае вы можете создать клиент пробной версии или принять участие в [программе для разработчиков Office](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=7a6e3d71-b057-49cc-b2aa-158ff23432f3&lcid=1033&culture=en-us&dir=LTR).</span><span class="sxs-lookup"><span data-stu-id="64d88-106">If you don't have one, you can create a trial tenant or for example sign up for the [Office Developer Program](https://profile.microsoft.com/RegSysProfileCenter/wizardnp.aspx?wizid=7a6e3d71-b057-49cc-b2aa-158ff23432f3&lcid=1033&culture=en-us&dir=LTR).</span></span> <span data-ttu-id="64d88-107">Вам будет отправлено письмо со ссылкой, позволяющей получить клиент Office 365 для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="64d88-107">You will receive a welcome mail with a link to sign up for an Office 365 Developer Tenant.</span></span> 

> [!NOTE] 
> <span data-ttu-id="64d88-108">Перед регистрацией убедитесь, что вы вышли из всех имеющихся клиентов Office 365.</span><span class="sxs-lookup"><span data-stu-id="64d88-108">Note: Make sure that you are signed out of any existing Office 365 tenants before you sign up.</span></span>

## <a name="create-app-catalog-site"></a><span data-ttu-id="64d88-109">Создание сайта каталога приложений</span><span class="sxs-lookup"><span data-stu-id="64d88-109">Create app catalog site</span></span>
<span data-ttu-id="64d88-110">Для отправки и развертывания веб-частей необходим каталог приложений.</span><span class="sxs-lookup"><span data-stu-id="64d88-110">You will need an app catalog to upload and deploy web parts.</span></span> <span data-ttu-id="64d88-111">Если вы уже настроили каталог приложений, переходите к разделу [Создание коллекции сайтов разработчиков](#create-a-new-developer-site-collection).</span><span class="sxs-lookup"><span data-stu-id="64d88-111">If you've already set up an app catalog, see [create a new Developer Site collection](#create-a-new-developer-site-collection).</span></span>  

<span data-ttu-id="64d88-112">Откройте **Центр администрирования SharePoint**, указав в браузере приведенный ниже URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="64d88-112">Go to the **SharePoint Admin Center** by entering the following URL in your browser.</span></span> <span data-ttu-id="64d88-113">Замените **yourtenantprefix** префиксом клиента разработчика приложений для Office 365.</span><span class="sxs-lookup"><span data-stu-id="64d88-113">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
<span data-ttu-id="64d88-114">На боковой панели слева выберите пункт меню **Приложения**, а затем — **Каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="64d88-114">In the left sidebar, choose the **apps** menu item and then choose **App Catalog**.</span></span>

<span data-ttu-id="64d88-115">Нажмите кнопку **ОК**, чтобы создать сайт каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="64d88-115">Choose **OK** to create a new app catalog site.</span></span>

<span data-ttu-id="64d88-116">На следующей странице введите указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="64d88-116">In the next page, enter the following details:</span></span>

* <span data-ttu-id="64d88-117">**Название**: введите **Каталог приложений**.</span><span class="sxs-lookup"><span data-stu-id="64d88-117">**Title**: Enter **App Catalog**.</span></span>
* <span data-ttu-id="64d88-118">**_Суффикс_ адреса веб-сайта**: введите предпочитаемый суффикс каталога приложений, например **apps**.</span><span class="sxs-lookup"><span data-stu-id="64d88-118">**Web Site Address _suffix_**: Enter your preferred suffix for the app catalog; for example: **apps**.</span></span>
* <span data-ttu-id="64d88-119">**Администратор**: введите имя пользователя и нажмите кнопку **Разрешить**, чтобы разрешить его.</span><span class="sxs-lookup"><span data-stu-id="64d88-119">**Administrator**: Enter your username and choose the **resolve** button to resolve the username.</span></span>

<span data-ttu-id="64d88-120">Нажмите кнопку **ОК**, чтобы создать сайт каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="64d88-120">Choose **OK** to create the app catalog site.</span></span>

<span data-ttu-id="64d88-121">SharePoint создаст сайт каталога приложений, а вы сможете наблюдать за ходом создания в Центре администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="64d88-121">SharePoint will create the app catalog site and you will be able to see its progress in the SharePoint admin center.</span></span>

## <a name="create-a-new-developer-site-collection"></a><span data-ttu-id="64d88-122">Создание семейства сайтов разработчиков</span><span class="sxs-lookup"><span data-stu-id="64d88-122">Create a new Developer Site collection</span></span>
<span data-ttu-id="64d88-123">Для тестирования также понадобится семейство веб-сайтов и сайт.</span><span class="sxs-lookup"><span data-stu-id="64d88-123">You also need a site collection and a site for your testing.</span></span> <span data-ttu-id="64d88-124">Семейство веб-сайтов можно создать с помощью любого из доступных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="64d88-124">You can create a new site collection using any of the available templates.</span></span> <span data-ttu-id="64d88-125">Мы можете использовать **семейство сайтов разработчиков**, но это излишне, так как базовое тестирование и тестирование в рабочей области можно выполнять на любом сайте.</span><span class="sxs-lookup"><span data-stu-id="64d88-125">You may chose to use **developer site collection**, but that does not really add additional value, since workbench and basic testing can be performed under any site.</span></span>

<span data-ttu-id="64d88-126">Ниже приведены шаги, позволяющие создать семейство сайтов разработчиков.</span><span class="sxs-lookup"><span data-stu-id="64d88-126">Here are steps for creating new developer site collection.</span></span>

 <span data-ttu-id="64d88-127">Откройте **Центр администрирования SharePoint**, указав в браузере приведенный ниже URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="64d88-127">Go to the **SharePoint Admin Center** by entering the following URL in your browser.</span></span> <span data-ttu-id="64d88-128">Замените **yourtenantprefix** префиксом клиента разработчика приложений для Office 365.</span><span class="sxs-lookup"><span data-stu-id="64d88-128">Replace **yourtenantprefix** with your Office 365 Developer Tenant prefix.</span></span>
    
```
https://yourtenantprefix-admin.sharepoint.com
```
    
<span data-ttu-id="64d88-129">На ленте SharePoint выберите **Создать** -> **Частное семейство веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="64d88-129">In the SharePoint ribbon, choose **New** -> **Private Site Collection**.</span></span>

<span data-ttu-id="64d88-130">В диалоговом окне введите указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="64d88-130">In the dialog box, enter the following details:</span></span>

* <span data-ttu-id="64d88-131">**Название**: введите название семейства сайтов разработчиков, например **Сайт разработчика**.</span><span class="sxs-lookup"><span data-stu-id="64d88-131">**Title**: Enter a title for your developer site collection; for example: **Developer Site**.</span></span>
* <span data-ttu-id="64d88-132">**_Суффикс_ адреса веб-сайта**: введите суффикс семейства сайтов разработчиков, например **dev**.</span><span class="sxs-lookup"><span data-stu-id="64d88-132">**Web Site Address _suffix_**: Enter a suffix for your developer site collection; for example: **dev**.</span></span>
* <span data-ttu-id="64d88-133">**Выбор шаблона**: выберите для семейства веб-сайтов шаблон **Сайт разработчика**.</span><span class="sxs-lookup"><span data-stu-id="64d88-133">**Template Selection**: Select **Developer Site** as the site collection template.</span></span>
* <span data-ttu-id="64d88-134">**Администратор**: введите имя пользователя и нажмите кнопку **Разрешить**, чтобы разрешить его.</span><span class="sxs-lookup"><span data-stu-id="64d88-134">**Administrator**: Enter your username and choose the **resolve** button to resolve the username.</span></span>

<span data-ttu-id="64d88-135">Нажмите кнопку **ОК**, чтобы создать семейство веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="64d88-135">Choose **OK** to create the site collection.</span></span>

<span data-ttu-id="64d88-p106">SharePoint создаст сайт разработчика, а вы сможете наблюдать за ходом создания в Центре администрирования SharePoint. После создания сайта вы можете перейти к семейству сайтов разработчиков.</span><span class="sxs-lookup"><span data-stu-id="64d88-p106">SharePoint will create the developer site and you will be able to see its progress in the SharePoint admin center. After the site is created, you can browse to your developer site collection.</span></span>

## <a name="sharepoint-workbench"></a><span data-ttu-id="64d88-138">SharePoint Workbench</span><span class="sxs-lookup"><span data-stu-id="64d88-138">SharePoint Workbench</span></span>
<span data-ttu-id="64d88-p107">SharePoint Workbench — это рабочая область конструирования для разработчиков, которая позволяет быстро просматривать и проверять веб-части, не развертывая их в SharePoint. Цепочка инструментов для разработчиков, доступная в SharePoint Framework, включает локальную версию рабочей области, позволяющую быстро протестировать и проверить создаваемые решения. Эта область размещается также в области клиентов, чтобы вы могли просматривать и проверять локальные веб-части, которые находятся в разработке. Получить доступ к SharePoint Workbench можно на любом сайте SharePoint в своей области клиентов, перейдя по такому URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="64d88-p107">SharePoint Workbench is a developer design surface that enables you to quickly preview and test web parts without deploying them in SharePoint. SharePoint Framework developer toolchain contains a version of the Workbench that works locally and helps you quickly test and validate solutions you are building. It is also hosted in your tenancy to preview and test your local web parts in development. You can access the SharePoint Workbench from any SharePoint site in your tenancy by browsing to the following URL:</span></span>

```
https://your-sharepoint-site/_layouts/workbench.aspx
```

## <a name="next-steps"></a><span data-ttu-id="64d88-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64d88-143">Next steps</span></span>
<span data-ttu-id="64d88-144">Теперь, когда вы настроили клиент SharePoint, [настройте среду разработки](./set-up-your-development-environment.md) для сборки клиентских веб-частей.</span><span class="sxs-lookup"><span data-stu-id="64d88-144">Now that you have configured your SharePoint tenant, [set up your development environment](./set-up-your-development-environment.md) to build client-side web parts.</span></span>
