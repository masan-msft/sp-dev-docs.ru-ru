---
title: "Настройка проектов API для Office 365 для рассылки"
ms.date: 11/03/2017
ms.openlocfilehash: 4dde15a519cd313b26b07e11b2bde7d8bb349f45
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="configure-office-365-api-projects-for-distribution"></a><span data-ttu-id="8f9ef-102">Настройка проектов API для Office 365 для рассылки</span><span class="sxs-lookup"><span data-stu-id="8f9ef-102">Configure Office 365 API Projects for Distribution</span></span>

### <a name="summary"></a><span data-ttu-id="8f9ef-103">Summary</span><span class="sxs-lookup"><span data-stu-id="8f9ef-103">Summary</span></span> ###
<span data-ttu-id="8f9ef-104">На этой странице объясняется, что некоторые действия разработчикам следует рассмотреть возможность на свои проекты, использующие API-интерфейсы Office 365 перед их распространения с другими разработчиками клиентами, или для системы управления версиями, такие как Team Foundation Server, Git или Visual Studio Онлайн.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-104">This page explains some steps developers should consider taking on their projects that leverage the Office 365 APIs prior to distributing them to other developers, their customers, or to source control systems such as Team Foundation Server, Git or Visual Studio Online.</span></span>

<span data-ttu-id="8f9ef-105">А именно на этой странице будет выглядеть в два этапа:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-105">Specifically this page will look at two steps:</span></span>

- [<span data-ttu-id="8f9ef-106">Справочник по NuGet пакета клиентских графике AD Azure исправление (en)</span><span class="sxs-lookup"><span data-stu-id="8f9ef-106">Fixup Azure AD Graph Client NuGet Package Reference</span></span>](#fixup-azure-ad-graph-client-nuget-package-reference)
- [<span data-ttu-id="8f9ef-107">Очистка `web.config` для получения дополнительных сведений конкретного приложения</span><span class="sxs-lookup"><span data-stu-id="8f9ef-107">Cleaning the `web.config` for app-specific details</span></span>](#cleaning-the-webconfig-for-app-specific-details)

# <a name="fixup-azure-ad-graph-client-nuget-package-reference"></a><span data-ttu-id="8f9ef-108">Справочник по NuGet пакета клиентских графике AD Azure исправление (en)</span><span class="sxs-lookup"><span data-stu-id="8f9ef-108">Fixup Azure AD Graph Client NuGet Package Reference</span></span>

<span data-ttu-id="8f9ef-109">Все проекты, использующих возможности SDK API Office 365 путем получения добавление подключенной службы содержат NuGet пакета, который добавляет Office 365 и Azure AD ссылок в проект, созданный в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-109">All projects that leverage the Office 365 API SDKs by way of adding a connected service include a NuGet package that adds Office 365 & Azure AD references to the project created in Visual Studio.</span></span> 

<span data-ttu-id="8f9ef-110">Пакет NuGet добавлен в проект в **Office 365 API средств** в Visual Studio не установлена в реестре пакета NuGet и таким образом попыток выполнить восстановление пакетов NuGet завершится ошибкой, так как он не удается найти нужный пакет.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-110">The NuGet package added to the project by the **Office 365 API Tools** in Visual Studio is not present in the NuGet package registry and therefore attempts to perform a NuGet package restore will fail because it cannot find a matching package.</span></span>

## <a name="understanding-the-problem"></a><span data-ttu-id="8f9ef-111">Общие сведения о проблемы</span><span class="sxs-lookup"><span data-stu-id="8f9ef-111">Understanding the Problem</span></span> ##

<span data-ttu-id="8f9ef-112">**Office 365 API Tools для Visual Studio 2013**, версия 1.3.41104.1, добавляет несколько пакетов NuGet проекты в процессе завершения работы мастера добавления подключения службы.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-112">The **Office 365 API Tools for Visual Studio 2013**, version 1.3.41104.1, adds multiple NuGet packages to projects as part of completing the Add Connected Service wizard.</span></span> <span data-ttu-id="8f9ef-113">В частности одним пакетом представляет сложную задачу: **Клиентская библиотека Microsoft Azure Active Directory графике**.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-113">One package in particular presents a challenge: **Microsoft Azure Active Directory Graph Client Library**.</span></span>

<span data-ttu-id="8f9ef-114">Способ работы Visual Studio является, что или addins, обычно содержат локальную копию пакетов NuGet, разработчики не всегда имеют подключение к Интернету для загрузки пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-114">The way Visual Studio works is that it, or addins, typically contain a local copy of the NuGet package so developers do not always have to be connected to the internet to download the NuGet packages.</span></span> <span data-ttu-id="8f9ef-115">Устанавливаемый пакет средства включают имеет идентификатор **Microsoft.Azure.ActiveDirectory.GraphClient** & версии **1.0.22**.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-115">The package that the tools include has an ID of **Microsoft.Azure.ActiveDirectory.GraphClient** & a version of **1.0.22**.</span></span>

<span data-ttu-id="8f9ef-116">Когда проекты фиксируются в системе управления версиями, обычно пакеты не включены как часть фиксации, так как они могут добавлять много требования пространства дополнительного хранилища и без необходимости увеличьте размер пакета при обмена с другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-116">When projects are committed to source control, typically the packages are not included as part of the commit because they can add a lot of extra storage space demands and unnecessarily increase the size of a package when sharing it with other developers.</span></span> <span data-ttu-id="8f9ef-117">Таким образом один из первой задачи разработчиков выполните действия после получения копии проекта из системы управления версиями — выполнить [Восстановление пакетов NuGet](http://docs.nuget.org/docs/reference/package-restore).</span><span class="sxs-lookup"><span data-stu-id="8f9ef-117">Therefore one of the first tasks developers do after getting a copy of the project from source control is to run [NuGet package restore](http://docs.nuget.org/docs/reference/package-restore).</span></span>

<span data-ttu-id="8f9ef-118">Проблема в том, что пакет с таким же Идентификатором & версии отсутствует в реестре пакета NuGet; не найден пакет с Идентификатором **Microsoft.Azure.ActiveDirectory.GraphClient** & версии **1.0.22**.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-118">The challenge is that a package with the same ID & version does not exist in the NuGet package registry; there is no package with an ID of **Microsoft.Azure.ActiveDirectory.GraphClient** & a version of **1.0.22**.</span></span> <span data-ttu-id="8f9ef-119">Пакет существует в реестре пакета NuGet **[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)**, но в разных версиях.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-119">The package does exist in the NuGet package registry, **[Microsoft.Azure.ActiveDirectory.GraphClient](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient)**, but under different versions.</span></span>

## <a name="fixing-the-azure-ad-graph-client-nuget-package-reference"></a><span data-ttu-id="8f9ef-120">Устранение ссылку Azure AD графике клиента NuGet-пакет</span><span class="sxs-lookup"><span data-stu-id="8f9ef-120">Fixing the Azure AD Graph Client NuGet Package Reference</span></span> ##

<span data-ttu-id="8f9ef-121">До обновления средства Office 365 API для Visual Studio 2013 для устранения этой проблемы рекомендуется для изменения проекта перед внесением системы управления версиями, независимо от того, при использовании сервера Team Foundation Server, Visual Studio Online, Git или любой другой решение.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-121">Until the Office 365 API Tools for Visual Studio 2013 are updated to fix this issue, it is recommended to alter the project prior to committing to your source control system, regardless if you are using Team Foundation Server, Visual Studio Online, Git or any other solution.</span></span>

<span data-ttu-id="8f9ef-122">После создания проекта, поиск в рамках проекта `packages.config` файл и выполните поиск пакета с Идентификатором **Microsoft.Azure.ActiveDirectory.GraphClient** & версии **1.0.22**.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-122">After creating the project, look within the project's `packages.config` file and search for a package with an ID of **Microsoft.Azure.ActiveDirectory.GraphClient** & version of **1.0.22**.</span></span> <span data-ttu-id="8f9ef-123">Удаление и повторная установка пакета — безопасный способ обновления проекта.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-123">The safest way to update the project is to uninstall & then reinstall the package.</span></span>

<span data-ttu-id="8f9ef-124">Откройте **Консоль диспетчера пакетов** в Visual Studio и введите следующую команду для удаления пакета:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-124">Open the **Package Manager Console** in Visual Studio and enter the following to uninstall the package:</span></span>

  ````powershell
  PM> Uninstall-Package -Id Microsoft.Azure.ActiveDirectory.GraphClient
  ````

  > <span data-ttu-id="8f9ef-125">Если удалить создает ошибка, не удалось найти пакет, просто удалите ссылку пакета из `packages.config` файл вручную и сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-125">If the uninstall throws an error about not finding the package, simply remove the package reference from the `packages.config` file manually & save your changes.</span></span>

<span data-ttu-id="8f9ef-126">Теперь установите общедоступной версии пакета же NuGet из открытого реестра:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-126">Now, install the public version of the same NuGet package from the public registry:</span></span>

  ````powershell
  PM> Install-Package -Id Microsoft.Azure.ActiveDirectory.GraphClient -Version 2.0.2
  ````

  > <span data-ttu-id="8f9ef-127">Вышеприведенный пример ссылается на определенной версии клиента графике Azure AD, известные для работы с помощью интерфейсов API Office 365.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-127">The above example references a specific version of the Azure AD graph client that is known to work with the Office 365 APIs.</span></span> <span data-ttu-id="8f9ef-128">Будущих версий могут работать так пропуск `-Version` аргумент является необязательным.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-128">Future versions may work so omitting the `-Version` argument is optional.</span></span>

[<span data-ttu-id="8f9ef-129">в начало</span><span class="sxs-lookup"><span data-stu-id="8f9ef-129">back to top</span></span>](#configure-office-365-api-projects-for-distribution)

# <a name="cleaning-the-webconfig-for-app-specific-details"></a><span data-ttu-id="8f9ef-130">Очистка `web.config` для получения дополнительных сведений конкретного приложения</span><span class="sxs-lookup"><span data-stu-id="8f9ef-130">Cleaning the `web.config` for App-Specific Details</span></span>

<span data-ttu-id="8f9ef-131">**Office 365 API Tools** для Visual Studio добавьте возможность создания нового приложения Azure AD с необходимыми разрешениями для API-интерфейсы Office 365 с помощью мастера **Подключения службы** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-131">The **Office 365 API Tools** for Visual Studio add the ability to create a new Azure AD application with the necessary permissions for the Office 365 APIs using the **Connected Service** wizard in Visual Studio.</span></span> <span data-ttu-id="8f9ef-132">После завершения работы мастера, несколько записей и настройки выполняются в проект `web.config` файла.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-132">When completing the wizard, multiple entries and customizations are made to the project's `web.config` file.</span></span>

<span data-ttu-id="8f9ef-133">Эти изменения включают следующие параметры надстройки:</span><span class="sxs-lookup"><span data-stu-id="8f9ef-133">These modifications include the following add-in settings:</span></span>

- <span data-ttu-id="8f9ef-134">**ida: ClientID**: Уникальный идентификатор приложения, созданного в клиент Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-134">**ida:ClientID**: The unique ID of the application created in your Azure AD tenant.</span></span>
- <span data-ttu-id="8f9ef-135">**IDA: пароль**: ключ приложения Azure AD, созданный с помощью мастера подключения службы.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-135">**ida:Password**: The Azure AD application's key that was generated by the Connected Service wizard.</span></span>
- <span data-ttu-id="8f9ef-136">**ida: AuthorizationUri**: конечная точка для проверки подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-136">**ida:AuthorizationUri**: The endpoint used to authenticate with Azure AD.</span></span>

<span data-ttu-id="8f9ef-137">**ida: ClientID** и **Ida: пароль** являются уникальными для приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-137">The **ida:ClientID** and **ida:Password** are unique to the Azure AD app.</span></span> <span data-ttu-id="8f9ef-138">Некоторые группы разработчиков может выбрать для каждого разработчика для кода с использованием собственные приложения, аналогичное как разработчики работают собственные базе данных и локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-138">Some development teams may elect for each developer to code against their own app, similar to how developers work against their own local development database.</span></span> <span data-ttu-id="8f9ef-139">Таким образом можно представить **ida: ClientID** и **Ida: пароль** аналогичную строки подключения базы данных.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-139">Therefore you can think of the the **ida:ClientID** and **ida:Password** similar to database connection strings.</span></span> 

<span data-ttu-id="8f9ef-140">Следующий раз разработчик использует мастер подключения службы для создания нового приложения Azure AD проекта мастера будет обнаруживать **ida: CliendID** и попытайтесь подключиться к приложению в текущий пользователь Azure AD для клиентов.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-140">The next time a developer uses the Connected Service wizard to create a new Azure AD application of the project, the wizard will detect the **ida:CliendID** and try to connect to an application in the current user's Azure AD tenant.</span></span> <span data-ttu-id="8f9ef-141">Если совпадение не найдено, мастер подключения службы возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-141">If a match is not found, the Connected Service wizard will throw an error.</span></span>

<span data-ttu-id="8f9ef-142">Поэтому перед внесением в проект системы управления версиями или до обмена с другими разработчиками, рекомендуется выполнить удалите значения из **ida: ClientID** & ida: надстройка параметров**Паролей** в `web.config`.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-142">Therefore, prior to committing the project to source control or before sharing with other developers, it is recommended to remove the values from the **ida:ClientID** & **ida:Password** add-in settings in the `web.config`.</span></span>

[<span data-ttu-id="8f9ef-143">в начало</span><span class="sxs-lookup"><span data-stu-id="8f9ef-143">back to top</span></span>](#configure-office-365-api-projects-for-distribution)

----------

### <a name="related-links"></a><span data-ttu-id="8f9ef-144">Ссылки по теме</span><span class="sxs-lookup"><span data-stu-id="8f9ef-144">Related links</span></span> ###
- [<span data-ttu-id="8f9ef-145">NuGet: Приложения для набора средств веб-сайта SharePoint</span><span class="sxs-lookup"><span data-stu-id="8f9ef-145">NuGet: App for SharePoint Web Toolkit</span></span>](http://www.nuget.org/packages/AppForSharePointWebToolkit)
- [<span data-ttu-id="8f9ef-146">NuGet: Восстановление пакетов</span><span class="sxs-lookup"><span data-stu-id="8f9ef-146">NuGet: Package Restore</span></span>](http://docs.nuget.org/docs/reference/package-restore)
- [<span data-ttu-id="8f9ef-147">MSDN: Пакетами NuGet библиотека API клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="8f9ef-147">MSDN: Office 365 API Client Library NuGet Packages</span></span>](http://msdn.microsoft.com/office/office365/HowTo/adding-service-to-your-Visual-Studio-project#O365NuGets)

### <a name="applies-to"></a><span data-ttu-id="8f9ef-148">Применимо к</span><span class="sxs-lookup"><span data-stu-id="8f9ef-148">Applies to</span></span> ###
-  <span data-ttu-id="8f9ef-149">Office 365 нескольких клиентов (MT)</span><span class="sxs-lookup"><span data-stu-id="8f9ef-149">Office 365 Multi Tenant (MT)</span></span>
-  <span data-ttu-id="8f9ef-150">Office 365 выделенных (D)</span><span class="sxs-lookup"><span data-stu-id="8f9ef-150">Office 365 Dedicated (D)</span></span>

### <a name="author"></a><span data-ttu-id="8f9ef-151">Автор</span><span class="sxs-lookup"><span data-stu-id="8f9ef-151">Author</span></span>
<span data-ttu-id="8f9ef-152">Эндрю Коннелл - [@andrewconnell](https://twitter.com/andrewconnell)</span><span class="sxs-lookup"><span data-stu-id="8f9ef-152">Andrew Connell - [@andrewconnell](https://twitter.com/andrewconnell)</span></span>

### <a name="version-history"></a><span data-ttu-id="8f9ef-153">История изменений</span><span class="sxs-lookup"><span data-stu-id="8f9ef-153">Version history</span></span> ###
<span data-ttu-id="8f9ef-154">Версия</span><span class="sxs-lookup"><span data-stu-id="8f9ef-154">Version</span></span>  | <span data-ttu-id="8f9ef-155">Date</span><span class="sxs-lookup"><span data-stu-id="8f9ef-155">Date</span></span> | <span data-ttu-id="8f9ef-156">Примечания</span><span class="sxs-lookup"><span data-stu-id="8f9ef-156">Comments</span></span>
---------| -----| --------
<span data-ttu-id="8f9ef-157">0,1</span><span class="sxs-lookup"><span data-stu-id="8f9ef-157">0.1</span></span>  | <span data-ttu-id="8f9ef-158">31 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="8f9ef-158">December 31, 2014</span></span> | <span data-ttu-id="8f9ef-159">Первый черновик</span><span class="sxs-lookup"><span data-stu-id="8f9ef-159">First draft</span></span>


