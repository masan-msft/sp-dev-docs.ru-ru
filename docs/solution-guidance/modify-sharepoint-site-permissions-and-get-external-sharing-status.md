---
title: "Изменить разрешения для сайта SharePoint и получить сведения о состоянии внешних общего доступа"
ms.date: 11/03/2017
ms.openlocfilehash: 664db2cc6d314b24be417f009cd8b464bfd0a5cc
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-site-permissions-and-get-external-sharing-status"></a>Изменить разрешения для сайта SharePoint и получить сведения о состоянии внешних общего доступа

Изменение свойств Администраторы семейства сайтов с помощью CSOM. Получите состояние внешних общего доступа и внешние пользователи семейства веб-сайтов или клиента.

_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

Пример [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) можно использовать для изменения администраторов семейства веб-сайтов на все семейства сайтов, включая OneDrive для бизнеса на клиентах службы Office 365. В этом примере также показано, как получить состояние внешних общего доступа для нескольких развертываний Office 365 установок.

С помощью консольного приложения, создайте объект **ClientContext** для получения разрешений для списка и/или изменение администраторов и получить сведения о состоянии внешних общего доступа. Можно также создать зарегистрированные надстройки с помощью маркеров OAuth.

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.SitePermissions](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.SitePermissions) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="work-with-site-collection-administrators"></a>Работа с Администраторы семейства сайтов

Для обновления администраторов семейства веб-сайтов, необходимо быть администратором семейства веб-сайтов. Первым шагом является создание объект **ClientContext** пользователем наличии соответствующих разрешений.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```C#
ClientContext cc = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password); 
```

Объект **ClientContext** можно получить список текущего сайта Администраторы семейства сайтов или обновите администраторы семейств сайтов, как показано в следующем примере.

```C#
List<UserEntity> admins = cc.Web.GetAdministrators();

List<UserEntity> adminsToAdd = new List<UserEntity>();
adminsToAdd.Add(new UserEntity() { LoginName = "i:0#.f|membership|user@domain" });

cc.Web.AddAdministrators(adminsToAdd);

UserEntity adminToRemove = new UserEntity() { LoginName = "i:0#.f|membership|user@domain" };
cc.Web.RemoveAdministrator(adminToRemove);
```

Можно задать сайта для семейств веб-сайтов администраторов которой вы не уже администратором семейства сайтов, создав объект **ClientContext** , с помощью зарегистрированные надстройки. Здесь объект **ClientContext** основано на маркер OAuth с разрешениями на уровне клиента.

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
После этого, можно использовать следующий код для получения объекта **ClientContext** для этой надстройки.

```C#
ClientContext cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext("https://tenantname-my.sharepoint.com/personal/user2", "<your tenant realm>", "<appID>", "<appsecret>");
```

## <a name="work-with-external-sharing-office-365-mt-only"></a>Работа с внешними общего доступа (только для Office 365 MT)

В этом сценарии показано, как получить сведения о внешних общего доступа состоянии семейства веб-сайтов и получить список внешних пользователей для определенного семейства сайтов или для всей клиента. Так как для этого необходимо библиотек CSOM клиента, вам необходимо создать **ClientContext** от семейства сайтов администрирования клиентов. Учетная запись должна быть учетной записью администратора клиента.

```C#
ClientContext ccTenant = new AuthenticationManager().GetSharePointOnlineAuthenticatedContextTenant(String.Format("https://{0}-admin.sharepoint.com/", tenantName), String.Format("{0}@{1}.onmicrosoft.com", userName, tenantName), password);
```

После **ClientContext** будет готов, чтобы получить состояние внешних общего доступа и список внешних пользователей можно использовать следующий код.

```C#
ccTenant.Web.GetSharingCapabilitiesTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)))

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersForSiteTenant(new Uri(String.Format("https://{0}.sharepoint.com/sites/{1}", tenantName, siteName)));

List<ExternalUserEntity> externalUsers = ccTenant.Web.GetExternalUsersTenant();

```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Решения по подготовке сайтов SharePoint](sharepoint-site-provisioning-solutions.md)
    
- [Пример Provisioning.Pages](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.Pages)
