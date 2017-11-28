---
title: "Подготовка веб-сайтов «современный» групп программными средствами"
description: "Подготовка сайта группы из пользовательского интерфейса или с помощью PnP основных CSOM или PnP PowerShell."
ms.date: 11/08/2017
ms.openlocfilehash: 65b9637167045b4fa92728ab3266c336fdfe6ad2
ms.sourcegitcommit: 4ea7e9cb1efb53f89da236282002956739d77418
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/09/2017
---
# <a name="provisioning-modern-team-sites-programmatically"></a><span data-ttu-id="8616c-103">Подготовка веб-сайтов «современный» групп программными средствами</span><span class="sxs-lookup"><span data-stu-id="8616c-103">Provisioning "modern" team sites programmatically</span></span>

<span data-ttu-id="8616c-104">«Современный» веб-сайтов групп были представлены в SharePoint Online в 2016 и использовать их можно управлять на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="8616c-104">"Modern" team sites were introduced in SharePoint Online in 2016, and the option to use them can be controlled at the tenant level.</span></span> <span data-ttu-id="8616c-105">В этой статье обсуждаются различные параметры и рекомендации для подготовки веб-сайтов «современный» групп в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8616c-105">This article discusses the different options and considerations for provisioning "modern" team sites in SharePoint Online.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8616c-106">Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».</span><span class="sxs-lookup"><span data-stu-id="8616c-106">We're not deprecating the "classic" experience; both "classic" and "modern" will coexist.</span></span>

## <a name="provisioning-a-modern-team-site-from-the-user-interface"></a><span data-ttu-id="8616c-107">Подготовка сайта «современный» группы из пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="8616c-107">Provisioning a "modern" team site from the user interface</span></span>

<span data-ttu-id="8616c-108">Существует множество маршрутов для сайта группы «современный» для получения подготовить к работе.</span><span class="sxs-lookup"><span data-stu-id="8616c-108">There are numerous routes for a "modern" team site to get provisioned.</span></span> <span data-ttu-id="8616c-109">Можно начать подготовки непосредственно с сайта SharePoint Online, или в качестве альтернативы подготовить группу Office 365 из других местоположений (например, от Outlook), который затем также запускает подготовки сайта группы «современный».</span><span class="sxs-lookup"><span data-stu-id="8616c-109">You can start the provisioning directly from the SharePoint Online site, or alternatively provision an Office 365 group from other locations (for example, from Outlook), which then also triggers the provisioning of a "modern" team site.</span></span> 

- <span data-ttu-id="8616c-110">Если администратор включен веб-сайтов «современный» групп клиента, можно создать веб-сайтов групп «современный» на домашней странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8616c-110">If your administrator enabled "modern" team sites in your tenant, you can create "modern" team sites from the SharePoint home page.</span></span>

- <span data-ttu-id="8616c-111">Также можно создать группу Office 365 с Office 365 Outlook, и при доступе к вкладке сайта эту группу land на сайте «современный» группы.</span><span class="sxs-lookup"><span data-stu-id="8616c-111">You can also create an Office 365 group from Office 365 Outlook, and when you access the site tab of that group, you land on a "modern" team site.</span></span> 

### <a name="control-default-provisioning-flow"></a><span data-ttu-id="8616c-112">Элемент управления по умолчанию подготовки потока</span><span class="sxs-lookup"><span data-stu-id="8616c-112">Control default provisioning flow</span></span>

<span data-ttu-id="8616c-113">Можно управлять процедуры создания сайтов SharePoint с параметрами администрирования SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8616c-113">You can control the SharePoint site creation process from the SharePoint Online Admin settings.</span></span> <span data-ttu-id="8616c-114">Вы можете, если «современный» взаимодействия для конечных пользователей или если вы хотите продолжить использование «классический» качества.</span><span class="sxs-lookup"><span data-stu-id="8616c-114">You can choose if the "modern" experience is available for your end users, or if you'd like to continue using the "classic" experience.</span></span> <span data-ttu-id="8616c-115">Дополнительные сведения см [Управление создания сайтов в SharePoint Online](https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9).</span><span class="sxs-lookup"><span data-stu-id="8616c-115">For details, see [Manage site creation in SharePoint Online](https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9).</span></span>

<span data-ttu-id="8616c-116">*На рисунке 1. Параметры создания веб-сайтов из SharePoint Online*</span><span class="sxs-lookup"><span data-stu-id="8616c-116">*Figure 1. Site creation options from SharePoint Online*</span></span>

![Параметры создания веб-сайтов в пользовательском Интерфейсе администрирования SharePoint Online](media/modern-experiences/site-creation-options-admin-ui.png)


## <a name="provisioning-a-modern-team-site-programmatically"></a><span data-ttu-id="8616c-118">Подготовка сайта группы «современный» программными средствами</span><span class="sxs-lookup"><span data-stu-id="8616c-118">Provisioning a "modern" team site programmatically</span></span>

<span data-ttu-id="8616c-119">«Современный» веб-сайтов групп создаются путем создания [группы Office 365](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/group) с помощью Microsoft Graph программными средствами.</span><span class="sxs-lookup"><span data-stu-id="8616c-119">"Modern" team sites are created programmatically by creating an [Office 365 group](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/group) using Microsoft Graph.</span></span> <span data-ttu-id="8616c-120">При создании группы с Office 365 сайта группы «современный» автоматически подготавливаться для группы.</span><span class="sxs-lookup"><span data-stu-id="8616c-120">When you create an Office 365 group, a "modern" team site is automatically provisioned for the group.</span></span> <span data-ttu-id="8616c-121">URI сайта «современный» team основано на параметр **mailNickname** группы Office 365 и имеет следующую структуру по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8616c-121">The "modern" team site URI is based on the **mailNickname** parameter of the Office 365 group and has the following default structure.</span></span> 

```
https://[tenant].sharepoint.com/sites/[mailNickname]]
``` 

> [!NOTE]
> <span data-ttu-id="8616c-122">Подробное описание создания группы с помощью Microsoft Graph доступен на [официальные документы](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/api/group_post_groups).</span><span class="sxs-lookup"><span data-stu-id="8616c-122">A detailed description of group creation using Microsoft Graph is available from the [official documentation](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/api/group_post_groups).</span></span>

### <a name="provision-a-modern-team-site-using-the-pnp-csom-core-component"></a><span data-ttu-id="8616c-123">Подготовка сайта «современный» группы с помощью компонента PnP основные CSOM</span><span class="sxs-lookup"><span data-stu-id="8616c-123">Provision a "modern" team site using the PnP CSOM Core component</span></span>

<span data-ttu-id="8616c-124">Компонент PnP основных CSOM как [пакет NuGet](https://www.nuget.org/packages/SharePointPnPCoreOnline)упрощенный методы обработки «современный» группы.</span><span class="sxs-lookup"><span data-stu-id="8616c-124">The PnP CSOM Core component, available as a [NuGet package](https://www.nuget.org/packages/SharePointPnPCoreOnline), has simplified methods for the "modern" group handling.</span></span> 

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

### <a name="provision-a-modern-team-site-using-pnp-powershell"></a><span data-ttu-id="8616c-125">Подготовка сайта «современный» группы с помощью PnP PowerShell</span><span class="sxs-lookup"><span data-stu-id="8616c-125">Provision a "modern" team site using PnP PowerShell</span></span>

<span data-ttu-id="8616c-126">Также можно создать сайты «современный» с помощью [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), позволяющий легко выполнять проверку подлинности с помощью Microsoft Graph с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8616c-126">You can also create "modern" sites by using [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), which lets you easily authenticate with Microsoft Graph by using Azure Active Directory.</span></span> <span data-ttu-id="8616c-127">Приведенный ниже сценарий создает сайт группы «современный» и возвращает фактический SharePoint URL-адрес сайта для дальнейшей обработки.</span><span class="sxs-lookup"><span data-stu-id="8616c-127">The following script creates a "modern" team site and then returns the actual SharePoint site URL for further manipulation.</span></span> <span data-ttu-id="8616c-128">После у вас есть доступ к URL-адрес созданного сайта, можно использовать CSOM (с компонент основной PnP SharePoint) или SharePoint PnP PowerShell для автоматизации других операций на созданном веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="8616c-128">After you have access to the URL of the created site, you can use CSOM (with the SharePoint PnP Core component) or SharePoint PnP PowerShell to automate other operations on the created site.</span></span>

```PowerShell
# Connect to Azure AD and get back an OAuth 2.0 Access Token
# This command will prompt the sign-in UI to authenticate
Connect-PnPMicrosoftGraph -Scopes "Group.ReadWrite.All","User.Read.All"

# Store the Access Token in a local variable
# This is not really needed for next steps, but is available
$accessToken = Get-PnPAccessToken

# Create a new Office 365 Unified Group, together with the corresponding Modern Site in SPO
$group = New-PnPUnifiedGroup -DisplayName "Awesome Group" -Description "Awesome Group" `
         -MailNickname "awesome-group" -Members "admin@contoso.onmicrosoft.com", "dan@contoso.onmicrosoft.com" `
         -IsPrivate -GroupLogoPath .\logo.jpg

# Connect to the modern site using PnP PowerShell SP cmdlets
# Since we are connecting now to SP side, credentials will be asked
Connect-PnPOnline $group.SiteUrl 

# Now we have access on the SharePoint site for any operations
$context = Get-PnPContext
$web = Get-PnPWeb
$context.Load($web, $web.WebTemplate)
Execute-PnPQuery
$web.WebTemplate + "#" + $web.Configuration
```

> [!NOTE]
> <span data-ttu-id="8616c-129">В настоящее время не поддерживается для подготовки веб-сайтов «современный» групп с помощью [Консоли SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span><span class="sxs-lookup"><span data-stu-id="8616c-129">There is currently no support to provision "modern" team sites by using the [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="8616c-130">Дополнительные сведения о выполнении</span><span class="sxs-lookup"><span data-stu-id="8616c-130">Additional considerations</span></span>

### <a name="subsites-use-classic-templates"></a><span data-ttu-id="8616c-131">Дочерние сайты используйте «классический» шаблоны</span><span class="sxs-lookup"><span data-stu-id="8616c-131">Subsites use "classic" templates</span></span>

<span data-ttu-id="8616c-132">Если Подготовка дочернего сайта в разделе корневого сайта семейства «современный» веб-сайтов, дочерних сайтов будет использовать «классический» шаблоны.</span><span class="sxs-lookup"><span data-stu-id="8616c-132">If you provision a subsite under the root site of a "modern" site collection, subsites will use "classic" templates.</span></span> <span data-ttu-id="8616c-133">На данный момент нет «современный» дочерний сайт доступных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="8616c-133">Currently, no "modern" subsite templates are available.</span></span> <span data-ttu-id="8616c-134">«Классический» дочернего сайта для сайта группы «современный» можно изменять путем создания «современный» страницы на сайте и обновления странице Добро пожаловать на страницу только что созданный.</span><span class="sxs-lookup"><span data-stu-id="8616c-134">You can transform a "classic" subsite to a "modern" team site by creating a "modern" page on the site and updating the welcome page to the newly created page.</span></span>  

### <a name="sites-are-not-listed-in-the-sharepoint-admin-ui--tenant-api"></a><span data-ttu-id="8616c-135">Сайты не указанные в пользовательском Интерфейсе администрирования SharePoint и API клиента</span><span class="sxs-lookup"><span data-stu-id="8616c-135">Sites are not listed in the SharePoint Admin UI / Tenant API</span></span>

<span data-ttu-id="8616c-136">«Современный» веб-сайтов групп не отображаются в пользовательском Интерфейсе администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8616c-136">"Modern" team sites are not visible in the SharePoint Admin UI.</span></span> <span data-ttu-id="8616c-137">Список веб-сайтов «современный» групп можно получить доступ с Office 365 Admin групп пользовательского интерфейса на портал администрирования Office 365.</span><span class="sxs-lookup"><span data-stu-id="8616c-137">You can access the list of "modern" team sites from the Office 365 groups Admin user interface under the Office 365 Admin portal.</span></span> <span data-ttu-id="8616c-138">Интерфейс пользователя SharePoint Online администрирования только приведены «классический» сайты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8616c-138">The SharePoint Online Admin user interface only lists "classic" SharePoint sites.</span></span> <span data-ttu-id="8616c-139">Это же ограничение не применяется к клиенту API; Этот интерфейс API можно использовать для перечисления веб-сайтов групп «современный» вместе с веб-сайтов «классический» групп.</span><span class="sxs-lookup"><span data-stu-id="8616c-139">This same limitation does not apply to the tenant API; you can use this API to enumerate "modern" team sites together with "classic" team sites.</span></span> <span data-ttu-id="8616c-140">Для получения списка только веб-сайтов «современный» групп, можно использовать группы конечную точку из Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="8616c-140">To obtain a list of only "modern" team sites, you can use the Groups end point from the Microsoft Graph API.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8616c-141">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8616c-141">Additional resources</span></span>

- [<span data-ttu-id="8616c-142">Настройка "современных" интерфейсов в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8616c-142">Customizing the "modern" experiences in SharePoint Online</span></span>](modern-experience-customizations.md)
- [<span data-ttu-id="8616c-143">Что такое на сайте группы SharePoint?</span><span class="sxs-lookup"><span data-stu-id="8616c-143">What is a SharePoint team site?</span></span>](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="8616c-144">Создание групп сайта в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8616c-144">Create a team site in SharePoint Online</span></span>](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [<span data-ttu-id="8616c-145">Управление создания сайтов в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8616c-145">Manage site creation in SharePoint Online</span></span>](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [<span data-ttu-id="8616c-146">Управление параметрами сайта группы разработчиков SharePoint</span><span class="sxs-lookup"><span data-stu-id="8616c-146">Manage your SharePoint team site settings</span></span>](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
