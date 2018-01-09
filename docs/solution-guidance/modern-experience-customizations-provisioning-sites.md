---
title: "Подготовка веб-сайтов «современный» групп программными средствами"
description: "Подготовка сайта группы из пользовательского интерфейса или с помощью PnP основных CSOM или PnP PowerShell."
ms.date: 12/19/2017
ms.openlocfilehash: 138b18ccea000bb75ac9bbe7e45f5df5cff2c8a0
ms.sourcegitcommit: 7b6ce94b477d9b587beaa059eb9aa7cd6235efde
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="provisioning-modern-team-sites-programmatically"></a><span data-ttu-id="f4046-103">Подготовка веб-сайтов «современный» групп программными средствами</span><span class="sxs-lookup"><span data-stu-id="f4046-103">Provisioning "modern" team sites programmatically</span></span>

<span data-ttu-id="f4046-104">«Современный» сайты были представлены в SharePoint Online во время осени 2016 и использовать их можно управлять на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="f4046-104">"Modern" sites were introduced in SharePoint Online during the autumn of 2016 and the option to use them can be controlled at the tenant level.</span></span> <span data-ttu-id="f4046-105">В этой статье обсуждаются различные параметры и рекомендации для подготовки «современный» сайтов в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="f4046-105">This article discusses the different options and considerations for provisioning "modern" sites in SharePoint Online.</span></span> <span data-ttu-id="f4046-106">В частности в статье описаны способы создания веб-сайтов групп «современный» и «современный» связи сайтов.</span><span class="sxs-lookup"><span data-stu-id="f4046-106">In particular, the article covers how to create both "modern" team sites, and "modern" communication sites.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4046-107">Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».</span><span class="sxs-lookup"><span data-stu-id="f4046-107">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

## <a name="comparing-modern-team-sites-and-modern-communication-sites"></a><span data-ttu-id="f4046-108">Сравнение веб-сайтов групп «современный» и «современный» связи сайтов</span><span class="sxs-lookup"><span data-stu-id="f4046-108">Comparing "modern" team sites and "modern" communication sites</span></span>
<span data-ttu-id="f4046-109">Прежде чем детали более подробно о том, как подготовить «современный» сайты, давайте рассмотрим немного о двух основных типов доступных: сайты рабочих групп и связи сайтов.</span><span class="sxs-lookup"><span data-stu-id="f4046-109">Before digging into the details about how to provision "modern" sites, let's discuss a little bit about the two main flavors available: team sites, and communication sites.</span></span>

<span data-ttu-id="f4046-110">Сайт группы «современный» — это место, где группа людей могут работать вместе, совместной работы, совместное использование документов и сообщений.</span><span class="sxs-lookup"><span data-stu-id="f4046-110">A "modern" team site is a place where a group of people can work together, collaborate, share documents and messages.</span></span> <span data-ttu-id="f4046-111">Каждый сайт группы «современный» имеет резервного группы Office 365, чтобы улучшить работу в общей совместной работы.</span><span class="sxs-lookup"><span data-stu-id="f4046-111">Every "modern" team site has a backing Office 365 Group, in order to improve the overall collaboration experience.</span></span> <span data-ttu-id="f4046-112">На самом деле благодаря группы Office 365, участники группы смогут извлечь пользу из службы, такие как планировщик работы, общий календарь, общих OneDrive для бизнеса хранилища, настраиваемых соединителей Office 365, и т.д. На сайте «современный» группы обычно члены могут способствовать контента (чтение/запись).</span><span class="sxs-lookup"><span data-stu-id="f4046-112">In fact, thanks to the Office 365 Group, members of the team can benefit of services like Planner, a shared Calendar, a shared OneDrive for Business storage, custom Office 365 connectors, etc. In a "modern" team site, typically the members can contribute to the content (read/write).</span></span> <span data-ttu-id="f4046-113">Кроме того группа Office 365, резервного сайта группы «современный» может быть частный или общедоступный и по умолчанию является открытым.</span><span class="sxs-lookup"><span data-stu-id="f4046-113">Moreover, the Office 365 Group backing a "modern" team site can be private or public, and by default it is public.</span></span>

<span data-ttu-id="f4046-114">Сайт «современный» связи — это место, где можно обмениваться новости, демонстрирующие статьи, широковещательные сообщения.</span><span class="sxs-lookup"><span data-stu-id="f4046-114">A "modern" communication site is a place where you can share news, showcase a story, broadcast a message.</span></span> <span data-ttu-id="f4046-115">Представление о связи сайтов является несколько редакторов, создание и обслуживание содержимого и большой аудитории, в котором используется, что содержимое.</span><span class="sxs-lookup"><span data-stu-id="f4046-115">The idea of a communication site is to have few editors that create and maintain the content, and a wide audience that consumes that content.</span></span> <span data-ttu-id="f4046-116">Сайт связи не имеет резервного группы Office 365.</span><span class="sxs-lookup"><span data-stu-id="f4046-116">However, a communication site does not have a backing Office 365 Group.</span></span> <span data-ttu-id="f4046-117">Пользователям целевом сайте обмена данными с хорошо известных набор разрешений из других сайтов SharePoint и по умолчанию каждый сайт связи закрытый.</span><span class="sxs-lookup"><span data-stu-id="f4046-117">Users can access the target communication site with the well-known set of permissions of any other SharePoint site, and by default every communication site is private.</span></span>

<span data-ttu-id="f4046-118">Таким образом Если для создания сайта для совместной работы группы, вероятнее всего сайта группы «современный» — это правильный выбор.</span><span class="sxs-lookup"><span data-stu-id="f4046-118">Thus, if you have to create a site for team collaboration, most likely the "modern" team site is the right choice.</span></span> <span data-ttu-id="f4046-119">С другой стороны Если вы хотите общаться что-то широкий набор людей, вероятно, сайт связи является лучшим выбором.</span><span class="sxs-lookup"><span data-stu-id="f4046-119">On the contrary, if you want to communicate something to a broad set of people, probably the communication site is your best choice.</span></span>

## <a name="provisioning-modern-team-sites"></a><span data-ttu-id="f4046-120">Подготовка веб-сайтов «современный» групп</span><span class="sxs-lookup"><span data-stu-id="f4046-120">Provisioning "modern" team sites</span></span>


<span data-ttu-id="f4046-121">Теперь в этом разделе вы узнаете, как для подготовки сайта группы «современный», и доступные параметры для этого.</span><span class="sxs-lookup"><span data-stu-id="f4046-121">Now in this section you will learn how to provision a "modern" team site, and what are the available options to do that.</span></span>

### <a name="provisioning-a-modern-team-site-from-the-user-interface"></a><span data-ttu-id="f4046-122">Подготовка сайта «современный» группы из пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f4046-122">Provisioning a "modern" team site from the user interface</span></span>

<span data-ttu-id="f4046-123">Существует множество маршрутов для сайта группы «современный» для получения подготовить к работе.</span><span class="sxs-lookup"><span data-stu-id="f4046-123">There are numerous routes for a "modern" team site to get provisioned.</span></span> <span data-ttu-id="f4046-124">Можно начать подготовки непосредственно с сайта SharePoint Online, или в качестве альтернативы подготовить группу Office 365 из других местоположений (например, от Outlook), который затем также запускает подготовки сайта группы «современный».</span><span class="sxs-lookup"><span data-stu-id="f4046-124">You can start the provisioning directly from the SharePoint Online site, or alternatively provision an Office 365 group from other locations (for example, from Outlook), which then also triggers the provisioning of a "modern" team site.</span></span> 

- <span data-ttu-id="f4046-125">Если администратор включен веб-сайтов «современный» групп клиента, можно создать веб-сайтов групп «современный» на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f4046-125">If your administrator enabled "modern" team sites in your tenant, you can create "modern" team sites from the SharePoint home page.</span></span>

- <span data-ttu-id="f4046-126">Также можно создать группу Office 365 с Office 365 Outlook, и при доступе к вкладке сайта эту группу land на сайте «современный» группы.</span><span class="sxs-lookup"><span data-stu-id="f4046-126">You can also create an Office 365 group from Office 365 Outlook, and when you access the site tab of that group, you land on a "modern" team site.</span></span> 

### <a name="how-to-control-default-provisioning-flow"></a><span data-ttu-id="f4046-127">Способы управления подготовки поток по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f4046-127">How to control default provisioning flow</span></span>

<span data-ttu-id="f4046-128">Можно управлять процедуры создания сайтов SharePoint в параметрах администрирования SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="f4046-128">You can control the SharePoint site creation process from the SharePoint Online admin settings.</span></span> <span data-ttu-id="f4046-129">Вы можете, если «современный» взаимодействия для конечных пользователей или если вы хотите продолжить использование «классический» качества.</span><span class="sxs-lookup"><span data-stu-id="f4046-129">You can choose if the "modern" experience is available for your end users or if you'd like to continue using the "classic" experience.</span></span>

![Параметры создания веб-сайтов из пользовательского интерфейса SharePoint Online администратора](media/modern-experiences/site-creation-options-admin-ui.png)

<span data-ttu-id="f4046-131">В следующей статье поддержка по Office для получения дополнительных сведений:</span><span class="sxs-lookup"><span data-stu-id="f4046-131">See the following Office Support article for details:</span></span>
- <span data-ttu-id="f4046-132">Управление создания сайтов в SharePoint Online: https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9</span><span class="sxs-lookup"><span data-stu-id="f4046-132">Manage site creation in SharePoint Online: https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9</span></span>

### <a name="provisioning-a-modern-team-site-programmatically-via-sharepoint-online-rest-api"></a><span data-ttu-id="f4046-133">Подготовка сайта группы «современный» программным путем с помощью SharePoint Online API-Интерфейс REST</span><span class="sxs-lookup"><span data-stu-id="f4046-133">Provisioning a "modern" team site programmatically via SharePoint Online REST API</span></span>

<span data-ttu-id="f4046-134">«Современный» веб-сайтов групп можно создать программным путем с помощью интерфейса API REST, предоставляемая SharePoint Online и используемые создать сайт пользовательского интерфейса из SharePoint Online, слишком.</span><span class="sxs-lookup"><span data-stu-id="f4046-134">"Modern" team sites can be created programmatically using a REST API provided by SharePoint Online, and used by the 'Create Site' UI of SharePoint Online, too.</span></span>

#### <a name="provisioning-a-modern-team-site-using-the-pnp-csom-core-component"></a><span data-ttu-id="f4046-135">Подготовка сайта «современный» группы с помощью компонент основной PnP CSOM</span><span class="sxs-lookup"><span data-stu-id="f4046-135">Provisioning a "modern" team site using the PnP CSOM core component</span></span>

<span data-ttu-id="f4046-136">В компонент основной PnP SharePoint — с момента выпуска 2017 октября (v.</span><span class="sxs-lookup"><span data-stu-id="f4046-136">In the SharePoint PnP Core component - since the October 2017 release (v.</span></span> <span data-ttu-id="f4046-137">2.19.1710.1) - имеется новый метод расширения для типа CSOM _ClientContext_ .</span><span class="sxs-lookup"><span data-stu-id="f4046-137">2.19.1710.1) - there is a new extension method for the CSOM _ClientContext_ type.</span></span> <span data-ttu-id="f4046-138">Имя метода расширения _CreateSiteAsync_ и позволяет создать сайт группы «современный» в нескольких несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="f4046-138">The extension method name is _CreateSiteAsync_ and allows you to create a "modern" team site in a matter of few seconds.</span></span> <span data-ttu-id="f4046-139">В следующем фрагменте кода можно узнать, как использовать этот метод.</span><span class="sxs-lookup"><span data-stu-id="f4046-139">In the following code snippet you can see how to use this technique.</span></span>

```C#
// Let's use the CreateSiteAsync extension method of PnP CSOM Core
// to create the "modern" team site

var targetTenantUrl = "https://[tenant].sharepoint.com/";

using (var context = new ClientContext(targetTenantUrl))
{
    context.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[Name-of-Your-Credentials]");

    // Create new "modern" team site at the url
    // https://[tenant].sharepoint.com/sites/mymodernteamsite
    var teamContext = await context.CreateSiteAsync(
        new TeamSiteCollectionCreationInformation
        {
            Alias = "mymodernteamsite", // Mandatory
            DisplayName = "displayName", // Mandatory
            Description = "description", // Optional
            Classification = "classification", // Optional
            IsPublic = true, // Optional, default true
        });
    teamContext.Load(teamContext.Web, w => w.Url);
    teamContext.ExecuteQueryRetry();
    Console.WriteLine(teamContext.Web.Url);
}
```

> [!NOTE]
> <span data-ttu-id="f4046-140">Дополнительно можно найти подробные сведения о аргумент _классификации_ [Официальная документация](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-site-classification)по.</span><span class="sxs-lookup"><span data-stu-id="f4046-140">You can find further details about the _Classification_ argument in the [official documentation](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-site-classification).</span></span>

<span data-ttu-id="f4046-141">Как вы видите, метод расширения создает новый сайт «современный» группы и возвращает новый объект _ClientContext_ непосредственно подключена к только что созданный сайт.</span><span class="sxs-lookup"><span data-stu-id="f4046-141">As you can see, the extension method creates a new "modern" team site and returns a new _ClientContext_ object directly connected to the newly created site.</span></span>

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a><span data-ttu-id="f4046-142">Подготовка сайта «современный» группы с помощью PnP PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4046-142">Provisioning a "modern" team site using PnP PowerShell</span></span>

<span data-ttu-id="f4046-143">Можно также создать «современный» сайты, использующие [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases).</span><span class="sxs-lookup"><span data-stu-id="f4046-143">You can also create "modern" sites using [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases).</span></span> <span data-ttu-id="f4046-144">Приведенный ниже сценарий будет создать сайт группы «современный» и верните фактический SharePoint URL-адрес сайта для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="f4046-144">The following script will create a "modern" team site and then return the actual SharePoint site URL for further manipulation.</span></span> <span data-ttu-id="f4046-145">Получив доступ к URL-адрес созданного сайта, можно использовать CSOM (с компонент основной PnP SharePoint) или SharePoint PnP PowerShell для автоматизации других операций на созданном веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="f4046-145">Once you have access to the URL of the created site, you can use CSOM (with the SharePoint PnP Core component) or SharePoint PnP-PowerShell to automate other operations on the created site.</span></span>

```ps
# Connect to SharePoint Online
# This command will prompt the sign-in UI to authenticate
Connect-PnPOnline "https://[tenant].sharepoint.com/"

# Create the new "modern" team site
$teamSiteUrl = New-PnPSite -Type TeamSite -Title "displayName" -Alias "mymodernteamsite" -Description "description" -IsPublic -Classification "classification" 

# Connect to the modern site using PnP PowerShell SP cmdlets
# Since we are connecting now to SP side, credentials will be asked
Connect-PnPOnline $teamSiteUrl

# Now we have access on the SharePoint site for any operations
$context = Get-PnPContext
$web = Get-PnPWeb
$context.Load($web, $web.WebTemplate)
Execute-PnPQuery
$web.WebTemplate + "#" + $web.Configuration
```

### <a name="provisioning-an-office-365-group-programmatically"></a><span data-ttu-id="f4046-146">Наполнение группы с Office 365 программными средствами</span><span class="sxs-lookup"><span data-stu-id="f4046-146">Provisioning an Office 365 Group programmatically</span></span>

<span data-ttu-id="f4046-147">«Современный» веб-сайтов групп могут создаваться путем создания [группы Office 365](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/group) с помощью Microsoft Graph слишком программными средствами.</span><span class="sxs-lookup"><span data-stu-id="f4046-147">"Modern" team sites can be created programmatically by creating an [Office 365 group](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/group) using the Microsoft Graph, too.</span></span> <span data-ttu-id="f4046-148">На самом деле при создании группы с Office 365 сайта группы «современный» автоматически подготавливаться для группы.</span><span class="sxs-lookup"><span data-stu-id="f4046-148">In fact, when you create an Office 365 group a "modern" team site is automatically provisioned for the group.</span></span> <span data-ttu-id="f4046-149">URI сайта «современный» группы будут основываться на параметр _mailNickname_ группы Office 365 и имеет следующую структуру по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f4046-149">The "modern" team site URI will be based upon the _mailNickname_ parameter of the Office 365 group and has the following default structure.</span></span> 

```
https://[tenant].sharepoint.com/sites/[mailNickname]
``` 

> [!NOTE]
> <span data-ttu-id="f4046-150">Подробное описание создания группы с помощью Microsoft Graph доступен на [официальные документы](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_post_groups).</span><span class="sxs-lookup"><span data-stu-id="f4046-150">A detailed description of group creation using Microsoft Graph is available from the [official documentation](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_post_groups).</span></span>

#### <a name="provisioning-an-office-365-group-using-the-pnp-csom-core-component"></a><span data-ttu-id="f4046-151">Подготовка группу Office 365, используя компонент основной PnP CSOM</span><span class="sxs-lookup"><span data-stu-id="f4046-151">Provisioning an Office 365 Group using the PnP CSOM core component</span></span>

<span data-ttu-id="f4046-152">Компонент PnP основных CSOM как [пакет NuGet](https://www.nuget.org/packages/SharePointPnPCoreOnline)упрощенный методы обработки «современный» группы.</span><span class="sxs-lookup"><span data-stu-id="f4046-152">The PnP CSOM Core component, available as a [NuGet package](https://www.nuget.org/packages/SharePointPnPCoreOnline), has simplified methods for the "modern" group handling.</span></span> 

```C#
/// <summary>
/// Let's use the UnifiedGroupsUtility class from PnP CSOM Core to simplify managed code operations for Office 365 groups
/// </summary>
/// <param name="accessToken">Azure AD Access token with Group.ReadWrite.All permission</param>
public static void ManipulateModernTeamSite(string accessToken)
{
    // Create new modern team site at the url https://[tenant].sharepoint.com/sites/mymodernteamsite
    Stream groupLogoStream = new FileStream("C:\\groupassets\\logo-original.png", 
                                            FileMode.Open, FileAccess.Read);
    var group = UnifiedGroupsUtility.CreateUnifiedGroup("displayName", "description", 
                            "mymodernteamsite", accessToken, groupLogo: groupLogoStream);
            
    // We received a group entity containing information about the group
    string url = group.SiteUrl;
    string groupId = group.GroupId;

    // Get group based on groupID
    var group2 = UnifiedGroupsUtility.GetUnifiedGroup(groupId, accessToken);
    // Get SharePoint site URL from group id
    var siteUrl = UnifiedGroupsUtility.GetUnifiedGroupSiteUrl(groupId, accessToken);

    // Get all groups in the tenant
    List<UnifiedGroupEntity> groups = UnifiedGroupsUtility.ListUnifiedGroups(accessToken);

    // Update description and group logo programatically
    groupLogoStream = new FileStream("C:\\groupassets\\logo-new.png", FileMode.Open, FileAccess.Read);
    UnifiedGroupsUtility.UpdateUnifiedGroup(groupId, accessToken, description: "Updated description", 
                                            groupLogo: groupLogoStream);

    // Delete group programatically
    UnifiedGroupsUtility.DeleteUnifiedGroup(groupId, accessToken);
}
```

#### <a name="provisioning-an-office-365-group-using-pnp-powershell"></a><span data-ttu-id="f4046-153">Подготовка группу Office 365, с помощью PnP PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4046-153">Provisioning an Office 365 Group using PnP PowerShell</span></span>

<span data-ttu-id="f4046-154">Кроме того, можно создать группу Office 365, с помощью [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), которые вы можете легко выполнять проверку подлинности с помощью Microsoft Graph, с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4046-154">You can also create an Office 365 Group using [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), which will let you easily authenticate with the Microsoft Graph using Azure Active Directory.</span></span> <span data-ttu-id="f4046-155">Приведенный ниже сценарий создаст группу Office 365 вместе с сайта группы «современный» и возвращается фактическая SharePoint URL-адрес сайта для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="f4046-155">The following script will create an Office 365 Group, together with a "modern" team site, and then return the actual SharePoint site URL for further manipulation.</span></span> <span data-ttu-id="f4046-156">Получив доступ к URL-адрес созданного сайта, можно использовать CSOM (с компонент основной PnP SharePoint) или SharePoint PnP PowerShell для автоматизации других операций на созданном веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="f4046-156">Once you have access to the URL of the created site, you can use CSOM (with the SharePoint PnP Core component) or SharePoint PnP-PowerShell to automate other operations on the created site.</span></span>

```PowerShell
# Connect to your SharePoint admin center, credentials will be asked
Connect-PnPOnline -Url https://contoso-admin.sharepoint.com

# Create a new modern team site
New-PnPSite -Type Team -Title "Awesome Group" -Description "Awesome Group" -Alias "awesome-group"
```

> [!NOTE]
> <span data-ttu-id="f4046-157">В настоящее время не поддерживается для подготовки веб-сайтов «современный» групп с помощью [Консоли SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="f4046-157">There is currently no support to provision "modern" team sites using [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

## <a name="provisioning-modern-communication-sites"></a><span data-ttu-id="f4046-158">Подготовка «Современный» связи сайтов</span><span class="sxs-lookup"><span data-stu-id="f4046-158">Provisioning "Modern" communication sites</span></span>

<span data-ttu-id="f4046-159">В этом разделе вы узнаете, как для подготовки сайта «современный» связи, и какие параметры доступны для этого.</span><span class="sxs-lookup"><span data-stu-id="f4046-159">In this section you will learn how to provision a "modern" communication site, and what are the available options to do that.</span></span>

### <a name="provisioning-a-modern-communication-site-from-user-interface"></a><span data-ttu-id="f4046-160">Подготовка сайта «современный» связи из пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f4046-160">Provisioning a "modern" communication site from user interface</span></span>

<span data-ttu-id="f4046-161">Для подготовки сайта «современный» обмена данными с помощью пользовательского интерфейса — Если администратор этот параметр включен веб-сайтов «современный» групп в клиент - можно начать непосредственно из SharePoint Online домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="f4046-161">To provision a "modern" communication site using the user interface - if your administrator enabled "modern" team sites in your tenant - you can start directly from the SharePoint Online home page.</span></span> <span data-ttu-id="f4046-162">Нажмите кнопку «Создать сайт», выберите для создания «Связи сайта» выберите проект для веб-узла, предоставить имя и описание и сайта будут создаваться в зависит от нескольких секунд.</span><span class="sxs-lookup"><span data-stu-id="f4046-162">Click the 'Create Site' button, select to create a 'Communication Site', choose a design for your site,  provide a name and a description, and the site will be created in a matter of few seconds.</span></span>
<span data-ttu-id="f4046-163">Во время написания этой статьи приведены доступные разработки для связи сайтов:</span><span class="sxs-lookup"><span data-stu-id="f4046-163">At the time of this writing the available designs for a communication site are:</span></span>
* <span data-ttu-id="f4046-164">**Тема**: используйте этот конструктор, если у вас есть много информации для совместного использования, например, новости, события и другие материалы.</span><span class="sxs-lookup"><span data-stu-id="f4046-164">**Topic**: use this design if you have a lot of information to share such as news, events, and other content.</span></span>
* <span data-ttu-id="f4046-165">**Демонстрация**: используйте этот конструктор для демонстрации продукта, группы или событие с помощью фотографий и изображений.</span><span class="sxs-lookup"><span data-stu-id="f4046-165">**Showcase**: use this design to showcase a product, team, or event using photos or images.</span></span>
* <span data-ttu-id="f4046-166">**Пустой**: начать с пустого сайта и разработки поступают в жизнь быстро и легко.</span><span class="sxs-lookup"><span data-stu-id="f4046-166">**Blank**: start with a blank site and make your design come to life quickly and easily.</span></span>

### <a name="provisioning-a-modern-communication-site-programmatically"></a><span data-ttu-id="f4046-167">Подготовка сайта «современный» обмена данными программными средствами</span><span class="sxs-lookup"><span data-stu-id="f4046-167">Provisioning a "modern" communication site programmatically</span></span>

<span data-ttu-id="f4046-168">По желанию вместо можно создать узел «современный» связи программным путем с помощью любого из CSOM и PnP, или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4046-168">If you rather prefer, you can create a "modern" communication site programmatically using either CSOM and PnP, or PowerShell.</span></span>

#### <a name="provisioning-a-modern-communication-site-using-the-pnp-csom-core-component"></a><span data-ttu-id="f4046-169">Подготовка сайта «современный» связи, с помощью компонент основной PnP CSOM</span><span class="sxs-lookup"><span data-stu-id="f4046-169">Provisioning a "modern" communication site using the PnP CSOM core component</span></span>

<span data-ttu-id="f4046-170">Компонент PnP основных CSOM как [пакет NuGet](https://www.nuget.org/packages/SharePointPnPCoreOnline)имеет упрощенный методы для обработки «современный» сайтов.</span><span class="sxs-lookup"><span data-stu-id="f4046-170">The PnP CSOM Core component, available as a [NuGet package](https://www.nuget.org/packages/SharePointPnPCoreOnline), has simplified methods for the "modern" sites handling.</span></span> 

```C#
// Let's use the CreateSiteAsync extension method of PnP CSOM Core
// to create the "modern" team site

var targetTenantUrl = "https://[tenant].sharepoint.com/";

using (var context = new ClientContext(targetTenantUrl))
{
    context.Credentials = OfficeDevPnP.Core.Utilities.CredentialManager.GetSharePointOnlineCredential("[Name-of-Your-Credentials]");

    // Create new "modern" communication site at the url https://[tenant].sharepoint.com/sites/mymoderncommunicationsite
    var communicationContext = await context.CreateSiteAsync(new CommunicationSiteCollectionCreationInformation {
        Title = "title", // Mandatory
        Description = "description", // Mandatory
        Lcid = 1033, // Mandatory
        AllowFileSharingForGuestUsers = false, // Optional
        Classification = "classification", // Optional
        SiteDesign = CommunicationSiteDesign.Topic, // Mandatory
        Url = "https://[tenant].sharepoint.com/sites/mymoderncommunicationsite", // Mandatory
    });
    communicationContext.Load(communicationContext.Web, w => w.Url);
    communicationContext.ExecuteQueryRetry();
    Console.WriteLine(communicationContext.Web.Url);
}
```

<span data-ttu-id="f4046-171">Как вы видите, метод расширения создает новый сайт «современный» связи и возвращает новый объект _ClientContext_ непосредственно подключена к только что созданный сайт.</span><span class="sxs-lookup"><span data-stu-id="f4046-171">As you can see, the extension method creates a new "modern" communication site and returns a new _ClientContext_ object directly connected to the newly created site.</span></span>

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a><span data-ttu-id="f4046-172">Подготовка сайта «современный» группы с помощью PnP PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4046-172">Provisioning a "modern" team site using PnP PowerShell</span></span>

<span data-ttu-id="f4046-173">Приведенный ниже сценарий будет создавать сайт «современный» связи и верните фактический SharePoint URL-адрес сайта для дальнейшей обработки, нужным образом, как и в предыдущем примере с помощью веб-сайтов «современный» групп.</span><span class="sxs-lookup"><span data-stu-id="f4046-173">The following script will create a "modern" communication site and then return the actual SharePoint site URL for further manipulation, as like as it was in the previous example with "modern" team sites.</span></span>

```ps
# Connect to SharePoint Online
# This command will prompt the sign-in UI to authenticate
Connect-PnPOnline "https://[tenant].sharepoint.com/"

# Create the new "modern" communication site
$communicationSiteUrl = New-PnPSite -Type CommunicationSite -Title "displayName" -Url "https://[tenant].sharepoint.com/sites/mymoderncommunicationsite" -Description "description" -Classification "classification" -SiteDesign Topic

# Connect to the modern site using PnP PowerShell SP cmdlets
# Since we are connecting now to SP side, credentials will be asked
Connect-PnPOnline $teamSiteUrl

# Now we have access on the SharePoint site for any operations
$context = Get-PnPContext
$web = Get-PnPWeb
$context.Load($web, $web.Title)
Execute-PnPQuery
$web.Title
```

## <a name="additional-considerations"></a><span data-ttu-id="f4046-174">Дополнительные сведения о выполнении</span><span class="sxs-lookup"><span data-stu-id="f4046-174">Additional Considerations</span></span>

### <a name="sub-sites-use-classic-templates"></a><span data-ttu-id="f4046-175">Сайты Sub использовать шаблоны «классический»</span><span class="sxs-lookup"><span data-stu-id="f4046-175">Sub sites use "classic" templates</span></span>

<span data-ttu-id="f4046-176">При предоставлении веб-узла в разделе корневого сайта семейства сайтов «современный» sub сайты будут использовать шаблоны «классический».</span><span class="sxs-lookup"><span data-stu-id="f4046-176">If you provision a sub site under the root site of a "modern" site collection, sub sites will use "classic" templates.</span></span> <span data-ttu-id="f4046-177">Недоступны в настоящее время не шаблоны сайтов «современный» sub.</span><span class="sxs-lookup"><span data-stu-id="f4046-177">There are currently no "modern" sub site templates available.</span></span> <span data-ttu-id="f4046-178">«Классический» веб-узла на сайте «современный» команды можно изменять путем создания «современный» страницы на сайте и обновления странице Добро пожаловать на страницу только что созданный.</span><span class="sxs-lookup"><span data-stu-id="f4046-178">You can transform a "classic" sub site to a "modern" team site by creating a "modern" page on the site and updating the welcome page to the newly created page.</span></span>  

<span data-ttu-id="f4046-179">Если не хотите разрешить пользователям создавать «классический» веб-узла в разделе семейства сайтов «современный», как администратор, перейдите в центр администрирования SharePoint, перейдите на страницу параметров и настройте параметр «Создание дочерних сайтов» для скрытия меню создания «дочерний сайт».</span><span class="sxs-lookup"><span data-stu-id="f4046-179">If you don't want to allow users to create a "classic" sub site under a "modern" site collection, as an admin you can go to the SharePoint Admin Center, select the Settings page and configure the option for "Subsite Creation" to hide the "subsite" creation menu.</span></span> <span data-ttu-id="f4046-180">На следующем рисунке отображена «Создание дочерних сайтов».</span><span class="sxs-lookup"><span data-stu-id="f4046-180">You can see the "Subsite Creation" option in the following image.</span></span>

![Параметры создания дочернего сайта из пользовательского интерфейса SharePoint Online администратора](media/modern-experiences/subsite-creation-admin-setting.png)

### <a name="sites-are-not-listed-in-the-classic-sharepoint-admin-ui--tenant-api"></a><span data-ttu-id="f4046-182">Сайты не указанные в пользовательском Интерфейсе администрирования классический SharePoint / API клиента</span><span class="sxs-lookup"><span data-stu-id="f4046-182">Sites are not listed in the classic SharePoint Admin UI / Tenant API</span></span>

<span data-ttu-id="f4046-183">«Современный» веб-сайтов групп не отображаются в пользовательский Интерфейс администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f4046-183">"Modern" team sites are not visible in the SharePoint admin UI.</span></span> <span data-ttu-id="f4046-184">Список веб-сайтов «современный» групп можно получить доступ с пользовательский интерфейс администрирования Office 365 группы в области портала администрирования Office 365.</span><span class="sxs-lookup"><span data-stu-id="f4046-184">You can access the list of "modern" team sites from the Office 365 Groups admin user interface under Office 365 admin portal.</span></span> <span data-ttu-id="f4046-185">SharePoint Online пользовательский интерфейс администрирования только список «классический» сайты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f4046-185">SharePoint Online admin user interface only list "classic" SharePoint sites.</span></span> <span data-ttu-id="f4046-186">Это же ограничение не применяется к клиенту API: этот интерфейс API можно использовать для перечисления веб-сайтов групп «современный» вместе с веб-сайтов «классический» групп.</span><span class="sxs-lookup"><span data-stu-id="f4046-186">This same limitation does not apply to the tenant API: you can use this API to enumerate "modern" team sites together with "classic" team sites.</span></span> <span data-ttu-id="f4046-187">Для получения списка только веб-сайтов групп «современный» можно также использовать конечных точек групп из Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="f4046-187">To obtain a list of only "modern" team sites you can also use the Groups endpoint from Microsoft Graph API.</span></span>

<span data-ttu-id="f4046-188">Имеется также предстоящие новые Admin пользовательского интерфейса SharePoint, которая поддерживает управление нового семейства сайтов «современный», вместе с «классический» из них.</span><span class="sxs-lookup"><span data-stu-id="f4046-188">There is also an upcoming new SharePoint Admin UI, which supports managing the new "modern" site collections, together with the "classic" ones.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4046-189">См. также</span><span class="sxs-lookup"><span data-stu-id="f4046-189">See also</span></span>

- [<span data-ttu-id="f4046-190">Настройка "современных" интерфейсов в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f4046-190">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="f4046-191">Что такое на сайте группы SharePoint?</span><span class="sxs-lookup"><span data-stu-id="f4046-191">What is a SharePoint team site?</span></span>](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="f4046-192">Создание групп сайта в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f4046-192">Create a team site in SharePoint Online</span></span>](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [<span data-ttu-id="f4046-193">Управление создания сайтов в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="f4046-193">Manage site creation in SharePoint Online</span></span>](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="f4046-194">Управление параметрами сайта группы разработчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="f4046-194">Manage your SharePoint team site settings</span></span>](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
