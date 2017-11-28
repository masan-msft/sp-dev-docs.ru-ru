---
title: "Настройка SharePoint у поставщика надстроек для распределения"
ms.date: 11/03/2017
ms.openlocfilehash: 82a1c046063dda3a612f96f70e5583d58ca9a505
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a><span data-ttu-id="8bffa-102">Настройка SharePoint у поставщика надстроек для распределения</span><span class="sxs-lookup"><span data-stu-id="8bffa-102">Configure SharePoint Provider-Hosted Add-ins for Distribution</span></span>

### <a name="summary"></a><span data-ttu-id="8bffa-103">Summary</span><span class="sxs-lookup"><span data-stu-id="8bffa-103">Summary</span></span> ###

<span data-ttu-id="8bffa-104">На этой странице рассматриваются проблемы, которые могут возникнуть при совместном использовании SharePoint приложение с размещением у поставщика с другими разработчиками или при получении копии из системы управления версиями, такие как Team Foundation Server, Git или Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="8bffa-104">This page explains issues that may arise when sharing a SharePoint Provider-Hosted application with other developers or when obtaining a copy from a source control system such as Team Foundation Server, Git or Visual Studio Online.</span></span>

# <a name="configure-sharepoint-provider-hosted-add-ins-for-distribution"></a><span data-ttu-id="8bffa-105">Настройка SharePoint у поставщика надстроек для распределения</span><span class="sxs-lookup"><span data-stu-id="8bffa-105">Configure SharePoint Provider-Hosted Add-ins for Distribution</span></span>

<span data-ttu-id="8bffa-106">Все SharePoint у поставщика надстройки созданы с помощью Visual Studio 2013 включить NuGet пакет, который добавляет кода SharePoint и ссылки на веб-приложения, который выступает в качестве RemoteWeb для надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8bffa-106">All SharePoint Provider-Hosted add-ins created using Visual Studio 2013 include a NuGet package that adds SharePoint-specific code and references to the web application that serves as the RemoteWeb for the SharePoint add-in.</span></span> 

<span data-ttu-id="8bffa-107">Пакет NuGet, добавляемые в проект веб-приложения в средств разработчика Office в Visual Studio не установлена в реестре пакета NuGet и таким образом попыток выполнить восстановление пакетов NuGet завершится ошибкой, так как он не удается найти нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="8bffa-107">The NuGet package added to the web application project by the Office Developer Tools in Visual Studio is not present in the NuGet package registry and therefore attempts to perform a NuGet package restore will fail because it cannot find a matching package.</span></span>

## <a name="understanding-the-problem"></a><span data-ttu-id="8bffa-108">Общие сведения о проблемы</span><span class="sxs-lookup"><span data-stu-id="8bffa-108">Understanding the Problem</span></span> ##

<span data-ttu-id="8bffa-109">**Office Developer Tools для Visual Studio 2013**, версия 12.0.31105, добавляет пакет NuGet для веб-приложений создан как RemoteWeb для SharePoint у поставщика надстроек. Этот пакет **приложения для набора средств SharePoint Web**, добавляет следующих элементов в веб-проект:</span><span class="sxs-lookup"><span data-stu-id="8bffa-109">The **Office Developer Tools for Visual Studio 2013**, version 12.0.31105, adds a NuGet package to web applications created as the RemoteWeb for SharePoint Provider-Hosted add-ins. This package, the **App for SharePoint Web Toolkit**, adds the following things to the web project:</span></span>

- <span data-ttu-id="8bffa-110">Сборки и ссылки на сборки SharePoint со стороны клиента объектной модели (CSOM)</span><span class="sxs-lookup"><span data-stu-id="8bffa-110">Assemblies & references to the SharePoint Client-Side Object Model (CSOM) assemblies</span></span>
- <span data-ttu-id="8bffa-111">Файл кода `TokenHelper.cs` , которое поможет в процессе проверки подлинности для надстроек.</span><span class="sxs-lookup"><span data-stu-id="8bffa-111">A code file `TokenHelper.cs` that assists in the authentication process for add-ins.</span></span>
- <span data-ttu-id="8bffa-112">Файл кода `SharePointContext.cs` , приводятся рекомендации по созданию, обслуживанию контексте SharePoint в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8bffa-112">A code file `SharePointContext.cs` that helps in creating and maintaining a SharePoint context within the web application.</span></span>

<span data-ttu-id="8bffa-113">Способ работы Visual Studio является, что или addins, обычно содержат локальную копию пакетов NuGet, разработчики не всегда имеют подключение к Интернету для загрузки пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="8bffa-113">The way Visual Studio works is that it, or addins, typically contain a local copy of the NuGet package so developers do not always have to be connected to the internet to download the NuGet packages.</span></span> <span data-ttu-id="8bffa-114">Устанавливаемый пакет средства включают имеет идентификатор **AppForSharePoint16WebToolkit**.</span><span class="sxs-lookup"><span data-stu-id="8bffa-114">The package that the tools include has an ID of **AppForSharePoint16WebToolkit**.</span></span>

<span data-ttu-id="8bffa-115">Когда проекты фиксируются в системе управления версиями, обычно пакеты не включены как часть фиксации, так как они могут добавлять много требования пространства дополнительного хранилища и без необходимости увеличьте размер пакета при обмена с другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="8bffa-115">When projects are committed to source control, typically the packages are not included as part of the commit because they can add a lot of extra storage space demands and unnecessarily increase the size of a package when sharing it with other developers.</span></span> <span data-ttu-id="8bffa-116">Таким образом один из первой задачи разработчиков выполните действия после получения копии проекта из системы управления версиями — выполнить [Восстановление пакетов NuGet](http://docs.nuget.org/docs/reference/package-restore).</span><span class="sxs-lookup"><span data-stu-id="8bffa-116">Therefore one of the first tasks developers do after getting a copy of the project from source control is to run [NuGet package restore](http://docs.nuget.org/docs/reference/package-restore).</span></span>

<span data-ttu-id="8bffa-117">Проблема в том, что пакет с таким же Идентификатором не существует в реестре пакета NuGet; не найден пакет с Идентификатором **AppForSharePoint16WebToolkit**.</span><span class="sxs-lookup"><span data-stu-id="8bffa-117">The challenge is that a package with the same ID does not exist in the NuGet package registry; there is no package with an ID of **AppForSharePoint16WebToolkit**.</span></span> <span data-ttu-id="8bffa-118">Вместо этого точное того же пакета был добавлен в реестр пакетов NuGet как **AppForSharePointWebToolkit** ([http://www.nuget.org/packages/AppForSharePointWebToolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit)) ** (*Обратите внимание на то нехватка "16" идентификатор*).</span><span class="sxs-lookup"><span data-stu-id="8bffa-118">Instead the exact same package was added to the NuGet package registry as **AppForSharePointWebToolkit** ([http://www.nuget.org/packages/AppForSharePointWebToolkit](http://www.nuget.org/packages/AppForSharePointWebToolkit))** (*notice the lack of the '16' in the ID*).</span></span>

## <a name="preparing-a-sharepoint-provider-hosted-add-in-project-for-source-control--distribution"></a><span data-ttu-id="8bffa-119">Подготовка размещением у поставщика добавьте в проект SharePoint для системы управления версиями и рассылки</span><span class="sxs-lookup"><span data-stu-id="8bffa-119">Preparing a SharePoint Provider-Hosted Add-in Project for Source Control / Distribution</span></span> ##

<span data-ttu-id="8bffa-120">До обновления Office Developer Tools для Visual Studio 2013 для устранения этой проблемы рекомендуется для изменения проекта перед внесением системы управления версиями, независимо от того, при использовании сервера Team Foundation Server, Visual Studio Online, Git или любой другой решение.</span><span class="sxs-lookup"><span data-stu-id="8bffa-120">Until the Office Developer Tools for Visual Studio 2013 are updated to fix this issue, it is recommended to alter the project prior to committing to your source control system, regardless if you are using Team Foundation Server, Visual Studio Online, Git or any other solution.</span></span>

<span data-ttu-id="8bffa-121">После создания проекта, поиск в рамках проекта `packages.config` файл и выполните поиск пакета с Идентификатором **AppForSharePoint16WebToolkit**.</span><span class="sxs-lookup"><span data-stu-id="8bffa-121">After creating the project, look within the project's `packages.config` file and search for a package with an ID of **AppForSharePoint16WebToolkit**.</span></span> <span data-ttu-id="8bffa-122">Удаление и повторная установка пакета — безопасный способ обновления проекта.</span><span class="sxs-lookup"><span data-stu-id="8bffa-122">The safest way to update the project is to uninstall & then reinstall the package.</span></span>

<span data-ttu-id="8bffa-123">Откройте **Консоль диспетчера пакетов** в Visual Studio и введите следующую команду для удаления пакета:</span><span class="sxs-lookup"><span data-stu-id="8bffa-123">Open the **Package Manager Console** in Visual Studio and enter the following to uninstall the package:</span></span>

  ````powershell
  PM> Uninstall-Package -Id AppForSharePoint16WebToolkit
  ````

  > <span data-ttu-id="8bffa-124">Если удалить создает ошибка, не удалось найти пакет, просто удалите ссылку пакета из `packages.config` файл вручную и сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="8bffa-124">If the uninstall throws an error about not finding the package, simply remove the package reference from the `packages.config` file manually & save your changes.</span></span>

<span data-ttu-id="8bffa-125">Теперь установите общедоступной версии пакета же NuGet из открытого реестра:</span><span class="sxs-lookup"><span data-stu-id="8bffa-125">Now, install the public version of the same NuGet package from the public registry:</span></span>

  ````powershell
  PM> Install-Package -Id AppForSharePointWebToolkit
  ````

----------

### <a name="related-links"></a><span data-ttu-id="8bffa-126">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="8bffa-126">Related links</span></span> ###
- [<span data-ttu-id="8bffa-127">NuGet: Приложения для набора средств веб-сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="8bffa-127">NuGet: App for SharePoint Web Toolkit</span></span>](http://www.nuget.org/packages/AppForSharePointWebToolkit)
- [<span data-ttu-id="8bffa-128">NuGet: Восстановление пакетов</span><span class="sxs-lookup"><span data-stu-id="8bffa-128">NuGet: Package Restore</span></span>](http://docs.nuget.org/docs/reference/package-restore)

### <a name="applies-to"></a><span data-ttu-id="8bffa-129">Применимо к</span><span class="sxs-lookup"><span data-stu-id="8bffa-129">Applies to</span></span> ###
-  <span data-ttu-id="8bffa-130">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="8bffa-130">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="8bffa-131">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="8bffa-131">Office 365 Dedicated (D)</span></span>
-  <span data-ttu-id="8bffa-132">SharePoint 2013 в локальной</span><span class="sxs-lookup"><span data-stu-id="8bffa-132">SharePoint 2013 on-premises</span></span>

### <a name="author"></a><span data-ttu-id="8bffa-133">Автор</span><span class="sxs-lookup"><span data-stu-id="8bffa-133">Author</span></span>
<span data-ttu-id="8bffa-134">Эндрю Коннелл - [@andrewconnell](https://twitter.com/andrewconnell)</span><span class="sxs-lookup"><span data-stu-id="8bffa-134">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span></span>

### <a name="version-history"></a><span data-ttu-id="8bffa-135">История изменений</span><span class="sxs-lookup"><span data-stu-id="8bffa-135">Version history</span></span> ###
<span data-ttu-id="8bffa-136">Версия</span><span class="sxs-lookup"><span data-stu-id="8bffa-136">Version</span></span>  | <span data-ttu-id="8bffa-137">Date</span><span class="sxs-lookup"><span data-stu-id="8bffa-137">Date</span></span> | <span data-ttu-id="8bffa-138">Примечания</span><span class="sxs-lookup"><span data-stu-id="8bffa-138">Comments</span></span>
---------| -----| --------
<span data-ttu-id="8bffa-139">0,1</span><span class="sxs-lookup"><span data-stu-id="8bffa-139">0.1</span></span>  | <span data-ttu-id="8bffa-140">31 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="8bffa-140">December 31, 2014</span></span> | <span data-ttu-id="8bffa-141">Первый черновик</span><span class="sxs-lookup"><span data-stu-id="8bffa-141">First draft</span></span>
