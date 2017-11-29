---
title: "Разработка с помощью клиента разрешения с помощью только для приложений в SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 7e4080cf1847a1dcf98d1dbb19149a4bbfa8edd5
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="developing-using-tenant-permissions-with-app-only-in-sharepoint-online"></a><span data-ttu-id="19db3-102">Разработка с помощью клиента разрешения с помощью только для приложений в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="19db3-102">Developing using Tenant permissions with App-Only in SharePoint Online</span></span>

<span data-ttu-id="19db3-103">Опыт разработки для SharePoint **Add-ins, размещаемые у поставщика** , который требуется **разрешение клиента в сочетании с только для приложений**, была изменена.</span><span class="sxs-lookup"><span data-stu-id="19db3-103">The developer experience has changed for SharePoint **Provider-hosted Add-ins** that require **Tenant permission in combination with app-only**.</span></span> <span data-ttu-id="19db3-104">В этой статье описываются новые возможности для разработки и отладки эти решения.</span><span class="sxs-lookup"><span data-stu-id="19db3-104">This article walks you through the new experience for developing and debugging these solutions.</span></span> 

<span data-ttu-id="19db3-105">_**Применимо к:** Поставщик Add-ins for SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="19db3-105">_**Applies to:** Provider Hosted Add-ins for SharePoint Online_</span></span>


## <a name="understanding-the-problem"></a><span data-ttu-id="19db3-106">Общие сведения о проблемы</span><span class="sxs-lookup"><span data-stu-id="19db3-106">Understanding the Problem</span></span>
<span data-ttu-id="19db3-107">В Visual Studio выберите пункты отладка, начать отладку и сообщение об ошибке, «**Администратор клиента должен одобрить это приложение**» как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="19db3-107">In Visual Studio, you navigate to Debug, start debugging and receive a message that "**Your tenant administrator has to approve this app**" as depicted below.</span></span>
<span data-ttu-id="19db3-108">![](http://i.imgur.com/oFH9oqb.png).</span><span class="sxs-lookup"><span data-stu-id="19db3-108"></span></span> 

<span data-ttu-id="19db3-109">Причина, почему не удается щелкните **доверенным** том, что работы Visual Studio для разработчиков семейства веб-сайтов, указанный в параметры проекта, тогда как разрешения на уровне клиента с помощью только приложения могут быть предоставлены только через [доверие для вашего клиента сайт администрирования](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online).</span><span class="sxs-lookup"><span data-stu-id="19db3-109">The reason why you can't click **trust it** is because Visual Studio is working against the dev site collection you've specified in your project settings whereas tenant level permissions with app-only can only be granted via [trusting it against your tenant administration site](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online).</span></span>

## <a name="walkthrough"></a><span data-ttu-id="19db3-110">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="19db3-110">Walkthrough</span></span>
### <a name="step-1-create-a-new-service-principal"></a><span data-ttu-id="19db3-111">Шаг 1: Создание новых участников служб</span><span class="sxs-lookup"><span data-stu-id="19db3-111">Step 1: Create a new service principal</span></span>
<span data-ttu-id="19db3-112">Перейдите к семейству сайтов клиента и создание нового идентификатора клиента и секрет.</span><span class="sxs-lookup"><span data-stu-id="19db3-112">Navigate to a site collection in your tenant and generate a new client Id and Secret.</span></span> <span data-ttu-id="19db3-113">(Например, https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span><span class="sxs-lookup"><span data-stu-id="19db3-113">(E.g., https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span></span> <span data-ttu-id="19db3-114">На этой странице щелкните **Создать** для обоих **Идентификатор клиента**, **Секрет клиента** полей и предоставить оставшиеся поля.</span><span class="sxs-lookup"><span data-stu-id="19db3-114">In this page click **Generate** for both the **Client Id**, **Client Secret** Fields and supply the remaining fields.</span></span> <span data-ttu-id="19db3-115">При разработке надстройки убедитесь, что использование localhost.com, включая порт, что домен приложения.</span><span class="sxs-lookup"><span data-stu-id="19db3-115">While you are developing the add-in ensure you use localhost.com including the port as the App Domain.</span></span> <span data-ttu-id="19db3-116">Вы должны что-то вроде как ниже.</span><span class="sxs-lookup"><span data-stu-id="19db3-116">You should have something similar as below.</span></span>

![](http://i.imgur.com/5CfHgFD.png)

### <a name="step-2-grant-tenant-permissions"></a><span data-ttu-id="19db3-117">Шаг 2: Клиента предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="19db3-117">Step 2: Grant Tenant Permissions</span></span>
<span data-ttu-id="19db3-118">Чтобы выполнить это действие, необходимо быть администратором SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="19db3-118">In order to perform this step, you must be a SharePoint Online Administrator.</span></span> 

<span data-ttu-id="19db3-119">Перейдите в центр администрирования SharePoint (например, https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx) и предоставить разрешения клиента![](http://i.imgur.com/EGuJG3a.png)</span><span class="sxs-lookup"><span data-stu-id="19db3-119">Navigate to the SharePoint Admin Center (E.g., https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx) and grant the tenant permissions ![](http://i.imgur.com/EGuJG3a.png)</span></span>

![](http://i.imgur.com/dst9ZdP.png)


### <a name="step-3-update-your-manifest-and-webconfig"></a><span data-ttu-id="19db3-120">Шаг 3: Обновление манифеста и файла web.config</span><span class="sxs-lookup"><span data-stu-id="19db3-120">Step 3: Update your manifest and web.config</span></span>
<span data-ttu-id="19db3-121">В решении Visual Studio; обновление манифеста и файла web.config с идентификатором клиента, созданной на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="19db3-121">In the Visual Studio solution; update the manifest and web.config with the client id created in step 1.</span></span>
![](http://i.imgur.com/fKkLIde.png)


### <a name="step-4-package-the-app-and-add-the-app-file-to-the-app-catalog"></a><span data-ttu-id="19db3-122">Шаг 4: Упаковка приложения и добавьте App-файл в каталог приложений</span><span class="sxs-lookup"><span data-stu-id="19db3-122">Step 4: Package the app and add the .app file to the App catalog</span></span>
<span data-ttu-id="19db3-123">Щелкните правой кнопкой мыши проект надстройки SharePoint и нажмите кнопку Опубликовать.</span><span class="sxs-lookup"><span data-stu-id="19db3-123">Right click on the SharePoint Add-in project and click publish.</span></span>

<span data-ttu-id="19db3-124">Укажите **Идентификатор клиента** и ** секрет клиента ** создан в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="19db3-124">Supply the **Client ID** and **Client Secret **created in Step 1.</span></span>

![](http://i.imgur.com/XpM9rwb.png)

<span data-ttu-id="19db3-125">Так как необходимо выполнить отладку надстройки, убедитесь, что вы задаете https://localhost.com включая номер порта, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="19db3-125">Since you want to debug the add-in, ensure that you supply https://localhost.com including the port as depicted below.</span></span>
![](http://i.imgur.com/nQmSbPC.png)

<span data-ttu-id="19db3-126">Теперь развертывание надстройки на сайте каталога приложений.</span><span class="sxs-lookup"><span data-stu-id="19db3-126">Now deploy the add-in in the App Catalog site.</span></span>

### <a name="step-5-install-your-add-in-in-your-developer-site-collection"></a><span data-ttu-id="19db3-127">Шаг 5: Установка надстройки в в семействе веб-сайтов для разработчиков</span><span class="sxs-lookup"><span data-stu-id="19db3-127">Step 5: Install your add-in in your developer site collection</span></span>

<span data-ttu-id="19db3-128">Перейдите на сайт разработчика и добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="19db3-128">Navigate to the developer site and add the app.</span></span> <span data-ttu-id="19db3-129">Выберите команду **сведения о приложении**.</span><span class="sxs-lookup"><span data-stu-id="19db3-129">Click on **App Details**.</span></span>
![](http://i.imgur.com/Aihr4r7.png)

<span data-ttu-id="19db3-130">Если вы выбрали на Плитка приложения, необходимо выберите команду «**Узнайте, почему**» и запросить вашего приложения![](http://i.imgur.com/DwWUkG0.png)</span><span class="sxs-lookup"><span data-stu-id="19db3-130">If you clicked on the app tile, you will have to click on "**Find out why**" and request your app ![](http://i.imgur.com/DwWUkG0.png)</span></span>

<span data-ttu-id="19db3-131">После отправки запроса состояния будет в состоянии ожидания, пока администратор SharePoint или администратор каталога приложения одобряет запрос.</span><span class="sxs-lookup"><span data-stu-id="19db3-131">Once the request has been submitted the status will be in a pending state until the SharePoint Administrator or the App Catalog Administrator approves the request.</span></span> <span data-ttu-id="19db3-132">Утверждение запроса, перейдите в каталог приложений, запросы приложений и утвердить запрос.</span><span class="sxs-lookup"><span data-stu-id="19db3-132">To approve the request, navigate to the app catalog, App Requests and approve the request.</span></span>

![](http://i.imgur.com/yZ8vNEc.png)

<span data-ttu-id="19db3-133">После запроса утвержден надстройки могут теперь установить.</span><span class="sxs-lookup"><span data-stu-id="19db3-133">Once the request has been approved the add-in may now be installed.</span></span>

![](http://i.imgur.com/PMitOEY.png)

### <a name="step-6-debug-your-add-in"></a><span data-ttu-id="19db3-134">Шаг 6: Отладка надстройки</span><span class="sxs-lookup"><span data-stu-id="19db3-134">Step 6: Debug your Add-in</span></span>
<span data-ttu-id="19db3-135">В Visual Studio щелкните правой кнопкой мыши веб-проект и выберите новый экземпляр начальном **отладки** .</span><span class="sxs-lookup"><span data-stu-id="19db3-135">In Visual Studio right click your web project and select **Debug** Start new instance.</span></span> <span data-ttu-id="19db3-136">После запуска перейдите на свой сайт и запустите надстройку.</span><span class="sxs-lookup"><span data-stu-id="19db3-136">Once started, navigate to your site and launch the add-in.</span></span>

![](http://i.imgur.com/Y5vAlDr.png)

><span data-ttu-id="19db3-137">**Примечание**</span><span class="sxs-lookup"><span data-stu-id="19db3-137">**Note**</span></span>
> - <span data-ttu-id="19db3-138">Если для какой-либо причине приложение упаковать файл изменений необходимо снова развернуть ее в каталог приложений и повторно установить для семейства веб-сайтов разработки</span><span class="sxs-lookup"><span data-stu-id="19db3-138">If for some reason your app package file changes you'll need to redeploy it to the app catalog and re-install it to your development site collection</span></span>
> - <span data-ttu-id="19db3-139">Если вы надстройки имеет приемника событий appinstalled, необходимо убедиться, что вы сделали шаг 6, прежде чем шаг 5</span><span class="sxs-lookup"><span data-stu-id="19db3-139">If you're add-in has an appinstalled event receiver you'll need to ensure that you've done step 6 before you do step 5</span></span>


## <a name="additional-resources"></a><span data-ttu-id="19db3-140">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="19db3-140">Additional resources</span></span>
<span data-ttu-id="19db3-141"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="19db3-141"></span></span>
- [<span data-ttu-id="19db3-142">Надстройка только клиента административные разрешения для приложений в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="19db3-142">Add-in app only tenant administrative permissions in SharePoint Online</span></span>](https://msdn.microsoft.com/en-us/pnp_articles/how-to-provide-add-in-app-only-tenant-administrative-permissions-in-sharepoint-online)
- [<span data-ttu-id="19db3-143">Разрешения для надстроек в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="19db3-143">Add-in permissions in SharePoint 2013</span></span>](https://msdn.microsoft.com/en-us/library/office/fp142383.aspx)
- [<span data-ttu-id="19db3-144">Изучите структуру манифеста надстройки и пакет надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="19db3-144">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](https://msdn.microsoft.com/en-us/library/office/fp179918.aspx)

