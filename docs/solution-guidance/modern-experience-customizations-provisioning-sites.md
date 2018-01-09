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
# <a name="provisioning-modern-team-sites-programmatically"></a>Подготовка веб-сайтов «современный» групп программными средствами

«Современный» сайты были представлены в SharePoint Online во время осени 2016 и использовать их можно управлять на уровне клиента. В этой статье обсуждаются различные параметры и рекомендации для подготовки «современный» сайтов в SharePoint Online. В частности в статье описаны способы создания веб-сайтов групп «современный» и «современный» связи сайтов.

> [!IMPORTANT]
> Мы в случае неподдерживаемые взаимодействия «классический»; будет сосуществовать «классический» и «современный».

## <a name="comparing-modern-team-sites-and-modern-communication-sites"></a>Сравнение веб-сайтов групп «современный» и «современный» связи сайтов
Прежде чем детали более подробно о том, как подготовить «современный» сайты, давайте рассмотрим немного о двух основных типов доступных: сайты рабочих групп и связи сайтов.

Сайт группы «современный» — это место, где группа людей могут работать вместе, совместной работы, совместное использование документов и сообщений. Каждый сайт группы «современный» имеет резервного группы Office 365, чтобы улучшить работу в общей совместной работы. На самом деле благодаря группы Office 365, участники группы смогут извлечь пользу из службы, такие как планировщик работы, общий календарь, общих OneDrive для бизнеса хранилища, настраиваемых соединителей Office 365, и т.д. На сайте «современный» группы обычно члены могут способствовать контента (чтение/запись). Кроме того группа Office 365, резервного сайта группы «современный» может быть частный или общедоступный и по умолчанию является открытым.

Сайт «современный» связи — это место, где можно обмениваться новости, демонстрирующие статьи, широковещательные сообщения. Представление о связи сайтов является несколько редакторов, создание и обслуживание содержимого и большой аудитории, в котором используется, что содержимое. Сайт связи не имеет резервного группы Office 365. Пользователям целевом сайте обмена данными с хорошо известных набор разрешений из других сайтов SharePoint и по умолчанию каждый сайт связи закрытый.

Таким образом Если для создания сайта для совместной работы группы, вероятнее всего сайта группы «современный» — это правильный выбор. С другой стороны Если вы хотите общаться что-то широкий набор людей, вероятно, сайт связи является лучшим выбором.

## <a name="provisioning-modern-team-sites"></a>Подготовка веб-сайтов «современный» групп


Теперь в этом разделе вы узнаете, как для подготовки сайта группы «современный», и доступные параметры для этого.

### <a name="provisioning-a-modern-team-site-from-the-user-interface"></a>Подготовка сайта «современный» группы из пользовательского интерфейса

Существует множество маршрутов для сайта группы «современный» для получения подготовить к работе. Можно начать подготовки непосредственно с сайта SharePoint Online, или в качестве альтернативы подготовить группу Office 365 из других местоположений (например, от Outlook), который затем также запускает подготовки сайта группы «современный». 

- Если администратор включен веб-сайтов «современный» групп клиента, можно создать веб-сайтов групп «современный» на домашней странице SharePoint.

- Также можно создать группу Office 365 с Office 365 Outlook, и при доступе к вкладке сайта эту группу land на сайте «современный» группы. 

### <a name="how-to-control-default-provisioning-flow"></a>Способы управления подготовки поток по умолчанию

Можно управлять процедуры создания сайтов SharePoint в параметрах администрирования SharePoint Online. Вы можете, если «современный» взаимодействия для конечных пользователей или если вы хотите продолжить использование «классический» качества.

![Параметры создания веб-сайтов из пользовательского интерфейса SharePoint Online администратора](media/modern-experiences/site-creation-options-admin-ui.png)

В следующей статье поддержка по Office для получения дополнительных сведений:
- Управление создания сайтов в SharePoint Online: https://support.office.com/en-US/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9

### <a name="provisioning-a-modern-team-site-programmatically-via-sharepoint-online-rest-api"></a>Подготовка сайта группы «современный» программным путем с помощью SharePoint Online API-Интерфейс REST

«Современный» веб-сайтов групп можно создать программным путем с помощью интерфейса API REST, предоставляемая SharePoint Online и используемые создать сайт пользовательского интерфейса из SharePoint Online, слишком.

#### <a name="provisioning-a-modern-team-site-using-the-pnp-csom-core-component"></a>Подготовка сайта «современный» группы с помощью компонент основной PnP CSOM

В компонент основной PnP SharePoint — с момента выпуска 2017 октября (v. 2.19.1710.1) - имеется новый метод расширения для типа CSOM _ClientContext_ . Имя метода расширения _CreateSiteAsync_ и позволяет создать сайт группы «современный» в нескольких несколько секунд. В следующем фрагменте кода можно узнать, как использовать этот метод.

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
> Дополнительно можно найти подробные сведения о аргумент _классификации_ [Официальная документация](https://msdn.microsoft.com/en-us/pnp_articles/modern-experience-site-classification)по.

Как вы видите, метод расширения создает новый сайт «современный» группы и возвращает новый объект _ClientContext_ непосредственно подключена к только что созданный сайт.

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a>Подготовка сайта «современный» группы с помощью PnP PowerShell

Можно также создать «современный» сайты, использующие [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases). Приведенный ниже сценарий будет создать сайт группы «современный» и верните фактический SharePoint URL-адрес сайта для дальнейшей обработки. Получив доступ к URL-адрес созданного сайта, можно использовать CSOM (с компонент основной PnP SharePoint) или SharePoint PnP PowerShell для автоматизации других операций на созданном веб-сайте.

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

### <a name="provisioning-an-office-365-group-programmatically"></a>Наполнение группы с Office 365 программными средствами

«Современный» веб-сайтов групп могут создаваться путем создания [группы Office 365](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/group) с помощью Microsoft Graph слишком программными средствами. На самом деле при создании группы с Office 365 сайта группы «современный» автоматически подготавливаться для группы. URI сайта «современный» группы будут основываться на параметр _mailNickname_ группы Office 365 и имеет следующую структуру по умолчанию. 

```
https://[tenant].sharepoint.com/sites/[mailNickname]
``` 

> [!NOTE]
> Подробное описание создания группы с помощью Microsoft Graph доступен на [официальные документы](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/group_post_groups).

#### <a name="provisioning-an-office-365-group-using-the-pnp-csom-core-component"></a>Подготовка группу Office 365, используя компонент основной PnP CSOM

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

#### <a name="provisioning-an-office-365-group-using-pnp-powershell"></a>Подготовка группу Office 365, с помощью PnP PowerShell

Кроме того, можно создать группу Office 365, с помощью [PnP PowerShell](https://github.com/SharePoint/PnP-PowerShell/releases), которые вы можете легко выполнять проверку подлинности с помощью Microsoft Graph, с помощью Azure Active Directory. Приведенный ниже сценарий создаст группу Office 365 вместе с сайта группы «современный» и возвращается фактическая SharePoint URL-адрес сайта для дальнейшей обработки. Получив доступ к URL-адрес созданного сайта, можно использовать CSOM (с компонент основной PnP SharePoint) или SharePoint PnP PowerShell для автоматизации других операций на созданном веб-сайте.

```PowerShell
# Connect to your SharePoint admin center, credentials will be asked
Connect-PnPOnline -Url https://contoso-admin.sharepoint.com

# Create a new modern team site
New-PnPSite -Type Team -Title "Awesome Group" -Description "Awesome Group" -Alias "awesome-group"
```

> [!NOTE]
> В настоящее время не поддерживается для подготовки веб-сайтов «современный» групп с помощью [Консоли SharePoint Online](https://www.microsoft.com/en-us/download/details.aspx?id=35588).

## <a name="provisioning-modern-communication-sites"></a>Подготовка «Современный» связи сайтов

В этом разделе вы узнаете, как для подготовки сайта «современный» связи, и какие параметры доступны для этого.

### <a name="provisioning-a-modern-communication-site-from-user-interface"></a>Подготовка сайта «современный» связи из пользовательского интерфейса

Для подготовки сайта «современный» обмена данными с помощью пользовательского интерфейса — Если администратор этот параметр включен веб-сайтов «современный» групп в клиент - можно начать непосредственно из SharePoint Online домашней страницы. Нажмите кнопку «Создать сайт», выберите для создания «Связи сайта» выберите проект для веб-узла, предоставить имя и описание и сайта будут создаваться в зависит от нескольких секунд.
Во время написания этой статьи приведены доступные разработки для связи сайтов:
* **Тема**: используйте этот конструктор, если у вас есть много информации для совместного использования, например, новости, события и другие материалы.
* **Демонстрация**: используйте этот конструктор для демонстрации продукта, группы или событие с помощью фотографий и изображений.
* **Пустой**: начать с пустого сайта и разработки поступают в жизнь быстро и легко.

### <a name="provisioning-a-modern-communication-site-programmatically"></a>Подготовка сайта «современный» обмена данными программными средствами

По желанию вместо можно создать узел «современный» связи программным путем с помощью любого из CSOM и PnP, или PowerShell.

#### <a name="provisioning-a-modern-communication-site-using-the-pnp-csom-core-component"></a>Подготовка сайта «современный» связи, с помощью компонент основной PnP CSOM

Компонент PnP основных CSOM как [пакет NuGet](https://www.nuget.org/packages/SharePointPnPCoreOnline)имеет упрощенный методы для обработки «современный» сайтов. 

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

Как вы видите, метод расширения создает новый сайт «современный» связи и возвращает новый объект _ClientContext_ непосредственно подключена к только что созданный сайт.

#### <a name="provisioning-a-modern-team-site-using-pnp-powershell"></a>Подготовка сайта «современный» группы с помощью PnP PowerShell

Приведенный ниже сценарий будет создавать сайт «современный» связи и верните фактический SharePoint URL-адрес сайта для дальнейшей обработки, нужным образом, как и в предыдущем примере с помощью веб-сайтов «современный» групп.

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

## <a name="additional-considerations"></a>Дополнительные сведения о выполнении

### <a name="sub-sites-use-classic-templates"></a>Сайты Sub использовать шаблоны «классический»

При предоставлении веб-узла в разделе корневого сайта семейства сайтов «современный» sub сайты будут использовать шаблоны «классический». Недоступны в настоящее время не шаблоны сайтов «современный» sub. «Классический» веб-узла на сайте «современный» команды можно изменять путем создания «современный» страницы на сайте и обновления странице Добро пожаловать на страницу только что созданный.  

Если не хотите разрешить пользователям создавать «классический» веб-узла в разделе семейства сайтов «современный», как администратор, перейдите в центр администрирования SharePoint, перейдите на страницу параметров и настройте параметр «Создание дочерних сайтов» для скрытия меню создания «дочерний сайт». На следующем рисунке отображена «Создание дочерних сайтов».

![Параметры создания дочернего сайта из пользовательского интерфейса SharePoint Online администратора](media/modern-experiences/subsite-creation-admin-setting.png)

### <a name="sites-are-not-listed-in-the-classic-sharepoint-admin-ui--tenant-api"></a>Сайты не указанные в пользовательском Интерфейсе администрирования классический SharePoint / API клиента

«Современный» веб-сайтов групп не отображаются в пользовательский Интерфейс администрирования SharePoint. Список веб-сайтов «современный» групп можно получить доступ с пользовательский интерфейс администрирования Office 365 группы в области портала администрирования Office 365. SharePoint Online пользовательский интерфейс администрирования только список «классический» сайты SharePoint. Это же ограничение не применяется к клиенту API: этот интерфейс API можно использовать для перечисления веб-сайтов групп «современный» вместе с веб-сайтов «классический» групп. Для получения списка только веб-сайтов групп «современный» можно также использовать конечных точек групп из Microsoft Graph API.

Имеется также предстоящие новые Admin пользовательского интерфейса SharePoint, которая поддерживает управление нового семейства сайтов «современный», вместе с «классический» из них.

## <a name="see-also"></a>См. также

- [Настройка "современных" интерфейсов в SharePoint Online](modern-experience-customizations.md)
- [Что такое на сайте группы SharePoint?](https://support.office.com/en-US/article/What-is-a-SharePoint-team-site-75545757-36c3-46a7-beed-0aaa74f0401e?ui=en-US&rs=en-US&ad=US)
- [Создание групп сайта в SharePoint Online](https://support.office.com/en-US/article/Create-a-team-site-in-SharePoint-Online-ef10c1e7-15f3-42a3-98aa-b5972711777d)
- [Управление создания сайтов в SharePoint Online](https://support.office.com/en-us/article/Manage-site-creation-in-SharePoint-Online-e72844a3-0171-47c9-befb-e98b23e2dcf9?ui=en-US&rs=en-US&ad=US)
- [Управление параметрами сайта группы разработчиков SharePoint](https://support.office.com/en-us/article/Manage-your-SharePoint-team-site-settings-8376034d-d0c7-446e-9178-6ab51c58df42?ui=en-US&rs=en-US&ad=US)
