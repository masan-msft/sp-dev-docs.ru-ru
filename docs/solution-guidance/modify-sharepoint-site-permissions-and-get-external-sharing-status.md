---
title: "Изменить разрешения для сайта SharePoint и получить сведения о состоянии внешних общего доступа"
ms.date: 11/03/2017
ms.openlocfilehash: 664db2cc6d314b24be417f009cd8b464bfd0a5cc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-site-permissions-and-get-external-sharing-status"></a><span data-ttu-id="f64a7-102">Изменить разрешения для сайта SharePoint и получить сведения о состоянии внешних общего доступа</span><span class="sxs-lookup"><span data-stu-id="f64a7-102">Modify SharePoint site permissions and get external sharing status</span></span>

<span data-ttu-id="f64a7-103">Изменение свойств Администраторы семейства сайтов с помощью CSOM.</span><span class="sxs-lookup"><span data-stu-id="f64a7-103">Modify properties of site collection administrators by using CSOM.</span></span> <span data-ttu-id="f64a7-104">Получите состояние внешних общего доступа и внешние пользователи семейства веб-сайтов или клиента.</span><span class="sxs-lookup"><span data-stu-id="f64a7-104">Get the external sharing status and external users of a site collection or tenant.</span></span>

<span data-ttu-id="f64a7-105">_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="f64a7-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="f64a7-106">Пример [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) можно использовать для изменения администраторов семейства веб-сайтов на все семейства сайтов, включая OneDrive для бизнеса на клиентах службы Office 365.</span><span class="sxs-lookup"><span data-stu-id="f64a7-106">You can use the [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) sample to modify the site collection administrators on any site collection, including those for OneDrive for Business on Office 365 tenants.</span></span> <span data-ttu-id="f64a7-107">В этом примере также показано, как получить состояние внешних общего доступа для нескольких развертываний Office 365 установок.</span><span class="sxs-lookup"><span data-stu-id="f64a7-107">This sample also shows you how to obtain external sharing status for Office 365 Multi-Tenant installations.</span></span>

<span data-ttu-id="f64a7-108">С помощью консольного приложения, создайте объект **ClientContext** для получения разрешений для списка и/или изменение администраторов и получить сведения о состоянии внешних общего доступа.</span><span class="sxs-lookup"><span data-stu-id="f64a7-108">Using a console application, you create a  **ClientContext** object to get permissions to list and/or modify administrators, and get external sharing status.</span></span> <span data-ttu-id="f64a7-109">Можно также создать зарегистрированные надстройки с помощью маркеров OAuth.</span><span class="sxs-lookup"><span data-stu-id="f64a7-109">You also create a registered add-in by using OAuth tokens.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f64a7-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f64a7-110">Before you begin</span></span>

<span data-ttu-id="f64a7-111">Чтобы начать работу, загрузите пример надстройки [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="f64a7-111">To get started, download the [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="work-with-site-collection-administrators"></a><span data-ttu-id="f64a7-112">Работа с Администраторы семейства сайтов</span><span class="sxs-lookup"><span data-stu-id="f64a7-112">Work with site collection administrators</span></span>

<span data-ttu-id="f64a7-113">Для обновления администраторов семейства веб-сайтов, необходимо быть администратором семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f64a7-113">To update the administrators of a site collection, you must be an administrator for the site collection.</span></span> <span data-ttu-id="f64a7-114">Первым шагом является создание объект **ClientContext** пользователем наличии соответствующих разрешений.</span><span class="sxs-lookup"><span data-stu-id="f64a7-114">The first step is to create a  **ClientContext** object by a user with the right permissions.</span></span>

> [!NOTE] 
> <span data-ttu-id="f64a7-115">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="f64a7-115">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
ClientContext cc = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password); 
```

<span data-ttu-id="f64a7-116">Объект **ClientContext** можно получить список текущего сайта Администраторы семейства сайтов или обновите администраторы семейств сайтов, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f64a7-116">Using the  **ClientContext** object, you can get a list of the current site collection administrators or update the site collection administrators, as shown in the following example.</span></span>

```C#
List<UserEntity> admins = cc.Web.GetAdministrators();

List<UserEntity> adminsToAdd = new List<UserEntity>();
adminsToAdd.Add(new UserEntity() { LoginName = "i:0#.f|membership|user@domain" });

cc.Web.AddAdministrators(adminsToAdd);

UserEntity adminToRemove = new UserEntity() { LoginName = "i:0#.f|membership|user@domain" };
cc.Web.RemoveAdministrator(adminToRemove);
```

<span data-ttu-id="f64a7-117">Можно задать сайта для семейств веб-сайтов администраторов которой вы не уже администратором семейства сайтов, создав объект **ClientContext** , с помощью зарегистрированные надстройки.</span><span class="sxs-lookup"><span data-stu-id="f64a7-117">You can set the site collection administrators for site collections where you're not already a site collection administrator by creating a  **ClientContext** object using a registered add-in.</span></span> <span data-ttu-id="f64a7-118">Здесь объект **ClientContext** основано на маркер OAuth с разрешениями на уровне клиента.</span><span class="sxs-lookup"><span data-stu-id="f64a7-118">Here, the **ClientContext** object is based on an OAuth token with tenant-level permissions.</span></span>

```C#
// Use (Get-MsolCompanyInformation).ObjectID to obtain Target/Tenant realm: <guid>
//
// Manually register an add-in via the appregnew.aspx page and generate an add-in ID and 
// add-in secret. The add-in title and add-in domain can be a simple string like "MyAddin".
//
// Update the add-in ID in your worker role settings.
//
// Add the add-in secret in your worker role settings. 
//
// Manually set the permission XML for you add-in via the appinv.aspx page:
// 1. Look up your add-in via its add-in ID.
// 2. Paste the permission XML and choose create.
//
// Sample permission XML:
// <AppPermissionRequests AllowAppOnlyPolicy="true">
//   <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
// </AppPermissionRequests>
//
// Because you're granting tenant-wide full control to an add-in, the add-in secret is as important
// as the password from your SharePoint administration account.
```
<span data-ttu-id="f64a7-119">После этого, можно использовать следующий код для получения объекта **ClientContext** для этой надстройки.</span><span class="sxs-lookup"><span data-stu-id="f64a7-119">After you've done that, you can use the following code to obtain a  **ClientContext** object for this add-in.</span></span>

```C#
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext("https://tenantname-my.sharepoint.com/personal/user2", "<your tenant realm>", "<appID>", "<appsecret>");
```

## <a name="work-with-external-sharing-office-365-mt-only"></a><span data-ttu-id="f64a7-120">Работа с внешними общего доступа (только для Office 365 MT)</span><span class="sxs-lookup"><span data-stu-id="f64a7-120">Work with external sharing (Office 365 MT only)</span></span>

<span data-ttu-id="f64a7-121">В этом сценарии показано, как получить сведения о внешних общего доступа состоянии семейства веб-сайтов и получить список внешних пользователей для определенного семейства сайтов или для всей клиента.</span><span class="sxs-lookup"><span data-stu-id="f64a7-121">This scenario shows how to get the external sharing status of a site collection, and get a list of external users for a specific site collection or for the whole tenant.</span></span> <span data-ttu-id="f64a7-122">Так как для этого необходимо библиотек CSOM клиента, вам необходимо создать **ClientContext** от семейства сайтов администрирования клиентов.</span><span class="sxs-lookup"><span data-stu-id="f64a7-122">Because this requires the tenant CSOM libraries, you need to create a  **ClientContext** against the tenant admin site collection.</span></span> <span data-ttu-id="f64a7-123">Учетная запись должна быть учетной записью администратора клиента.</span><span class="sxs-lookup"><span data-stu-id="f64a7-123">The user account has to be a tenant administrator account.</span></span>

```C#
ClientContext ccTenant = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}-admin.sharepoint.com/", tenantName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password);
```

<span data-ttu-id="f64a7-124">После **ClientContext** будет готов, чтобы получить состояние внешних общего доступа и список внешних пользователей можно использовать следующий код.</span><span class="sxs-lookup"><span data-stu-id="f64a7-124">After the  **ClientContext** is ready, you can use the following code to get the external sharing status and a list of external users.</span></span>

```C#
ccTenant.Web.GetSharingCapabilitiesTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)))

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersForSiteTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)));

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersTenant();

```

## <a name="see-also"></a><span data-ttu-id="f64a7-125">См. также</span><span class="sxs-lookup"><span data-stu-id="f64a7-125">See also</span></span>
<span data-ttu-id="f64a7-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f64a7-126"></span></span>

- [<span data-ttu-id="f64a7-127">Решения по подготовке сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="f64a7-127">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="f64a7-128">Пример Provisioning.Pages</span><span class="sxs-lookup"><span data-stu-id="f64a7-128">Provisioning.Pages sample</span></span>](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.Pages)
