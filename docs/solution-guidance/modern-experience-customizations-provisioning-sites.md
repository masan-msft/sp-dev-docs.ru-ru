---
title: "Подготовка веб-сайтов «современный» групп программными средствами"
description: "Подготовка сайта группы из пользовательского интерфейса или с помощью PnP основных CSOM или PnP PowerShell."
ms.date: 11/08/2017
ms.openlocfilehash: 137629c7d1e9aaf55ac7709b07c4ad478202bfdc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="provisioning-modern-team-sites-programmatically"></a>Подготовка веб-сайтов «современный» групп программными средствами

«Современный» веб-сайтов групп были представлены в SharePoint Online в 2016 и использовать их можно управлять на уровне клиента. В этой статье обсуждаются различные параметры и рекомендации для подготовки веб-сайтов «современный» групп в SharePoint Online.

> [!IMPORTANT]
> Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».

## <a name="provisioning-a-modern-team-site-from-the-user-interface"></a>Подготовка сайта «современный» группы из пользовательского интерфейса

Существует множество маршрутов для сайта группы «современный» для получения подготовить к работе. Можно начать подготовки непосредственно с сайта SharePoint Online, или в качестве альтернативы подготовить группу Office 365 из других местоположений (например, от Outlook), который затем также запускает подготовки сайта группы «современный». 

- Если администратор включен веб-сайтов «современный» групп клиента, можно создать веб-сайтов групп «современный» на домашней странице SharePoint.

- Также можно создать группу Office 365 с Office 365 Outlook, и при доступе к вкладке сайта эту группу land на сайте «современный» группы. 

### <a name="control-default-provisioning-flow"></a>Элемент управления по умолчанию подготовки потока

Можно управлять процедуры создания сайтов SharePoint с параметрами администрирования SharePoint Online. Вы можете, если «современный» взаимодействия для конечных пользователей или если вы хотите продолжить использование «классический» качества. Дополнительные сведения см [Управление создания сайтов в SharePoint Online](https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9).

*На рисунке 1. Параметры создания веб-сайтов из SharePoint Online*

![Параметры создания веб-сайтов в пользовательском Интерфейсе администрирования SharePoint Online](media/modern-experiences/site-creation-options-admin-ui.png)


## <a name="provisioning-a-modern-team-site-programmatically"></a>Подготовка сайта группы «современный» программными средствами

«Современный» веб-сайтов групп создаются путем создания [группы Office 365](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/group) с помощью Microsoft Graph программными средствами. При создании группы с Office 365 сайта группы «современный» автоматически подготавливаться для группы. URI сайта «современный» team основано на параметр **mailNickname** группы Office 365 и имеет следующую структуру по умолчанию. 

```
https://[tenant].sharepoint.com/sites/[mailNickname]]
``` 

> [!NOTE]
> Подробное описание создания группы с помощью Microsoft Graph доступен на [официальные документы](https://graph.microsoft.io/en-us/docs/api-reference/v1.0/api/group_post_groups).

### <a name="provision-a-modern-team-site-using-the-pnp-csom-core-component"></a>Подготовка сайта «современный» группы с помощью компонента PnP основные CSOM

Компонент PnP основных CSOM как [пакет NuGet](https://www.nuget.org/packages/SharePointPnPCoreOnline)упрощенный методы обработки «современный» группы. 

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

### <a name="provision-a-modern-team-site-using-pnp-powershell"></a>Подготовка сайта «современный» группы с помощью PnP PowerShell

Также можно создать сайты «современный» с помощью [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), позволяющий легко выполнять проверку подлинности с помощью Microsoft Graph с помощью Azure Active Directory. Приведенный ниже сценарий создает сайт группы «современный» и возвращает фактический SharePoint URL-адрес сайта для дальнейшей обработки. После у вас есть доступ к URL-адрес созданного сайта, можно использовать CSOM (с компонент основной PnP SharePoint) или SharePoint PnP PowerShell для автоматизации других операций на созданном веб-сайте.

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
> В настоящее время не поддерживается для подготовки веб-сайтов «современный» групп с помощью [Консоли SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).

## <a name="additional-considerations"></a>Дополнительные сведения о выполнении

### <a name="subsites-use-classic-templates"></a>Дочерние сайты используйте «классический» шаблоны

Если Подготовка дочернего сайта в разделе корневого сайта семейства «современный» веб-сайтов, дочерних сайтов будет использовать «классический» шаблоны. На данный момент нет «современный» дочерний сайт доступных шаблонов. «Классический» дочернего сайта для сайта группы «современный» можно изменять путем создания «современный» страницы на сайте и обновления странице Добро пожаловать на страницу только что созданный.  

### <a name="sites-are-not-listed-in-the-sharepoint-admin-ui--tenant-api"></a>Сайты не указанные в пользовательском Интерфейсе администрирования SharePoint и API клиента

«Современный» веб-сайтов групп не отображаются в пользовательском Интерфейсе администрирования SharePoint. Список веб-сайтов «современный» групп можно получить доступ с Office 365 Admin групп пользовательского интерфейса на портал администрирования Office 365. Интерфейс пользователя SharePoint Online администрирования только приведены «классический» сайты SharePoint. Это же ограничение не применяется к клиенту API; Этот интерфейс API можно использовать для перечисления веб-сайтов групп «современный» вместе с веб-сайтов «классический» групп. Для получения списка только веб-сайтов «современный» групп, можно использовать группы конечную точку из Microsoft Graph API.

## <a name="see-also"></a>См. также

- [Настройка "современных" интерфейсов в SharePoint Online](modern-experience-customizations.md)
- [Что такое на сайте группы SharePoint?](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [Создание групп сайта в SharePoint Online](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [Управление создания сайтов в SharePoint Online](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [Управление параметрами сайта группы разработчиков SharePoint](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
