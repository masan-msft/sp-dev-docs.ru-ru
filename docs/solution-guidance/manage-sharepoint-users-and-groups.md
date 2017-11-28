---
title: "Управление SharePoint пользователями и группами"
ms.date: 11/03/2017
ms.openlocfilehash: 9f287515faede9c92aa172c947f6b1826efc0fa1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="manage-sharepoint-users-and-groups"></a><span data-ttu-id="2e18a-102">Управление SharePoint пользователями и группами</span><span class="sxs-lookup"><span data-stu-id="2e18a-102">Manage SharePoint users and groups</span></span>

<span data-ttu-id="2e18a-103">Управление пользователями, группами и разрешения в семействе сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e18a-103">Manage users, groups, and permissions within a SharePoint site collection.</span></span> 

<span data-ttu-id="2e18a-104">_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="2e18a-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="2e18a-105">В этой статье показано, как добавить или удалить групп и пользователей в рамках указанного семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="2e18a-105">This article shows you how to add or remove groups and users within a given site collection.</span></span> <span data-ttu-id="2e18a-106">Примеры кода в этой статье Добавление пользователей и групп и затем предоставьте им уровней разрешений доступа к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e18a-106">The code examples in this article add users and groups, and then give them permission levels of access to SharePoint.</span></span> <span data-ttu-id="2e18a-107">Этих пользователей и группы разрешений уровня действия реализуются с помощью методов расширения в образце PnP [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) .</span><span class="sxs-lookup"><span data-stu-id="2e18a-107">These user and group permission level actions are implemented via extension methods in the [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) PnP sample.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2e18a-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2e18a-108">Before you begin</span></span>

<span data-ttu-id="2e18a-109">Чтобы начать работу, загрузите пример надстройки [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="2e18a-109">To get started, download the [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="add-and-remove-groups-and-users"></a><span data-ttu-id="2e18a-110">Добавление и удаление пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="2e18a-110">Add and remove groups and users</span></span>

<span data-ttu-id="2e18a-111">Следующем примере показано, как добавлять группы и добавление пользователей в группу.</span><span class="sxs-lookup"><span data-stu-id="2e18a-111">The following example shows you how to add groups and add users to groups.</span></span>

<span data-ttu-id="2e18a-112">**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="2e18a-112">**Note:**  The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;

if (!cc.Web.GroupExists("Test"))
{
  Group group = cc.Web.AddGroup("Test", "Test group", true);
  cc.Web.AddUserToGroup("Test", currentUser.LoginName);
}
```

<span data-ttu-id="2e18a-113">Следующий пример удаляет группу.</span><span class="sxs-lookup"><span data-stu-id="2e18a-113">The next example removes a group.</span></span>

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemoveGroup("Test");
}
```

<span data-ttu-id="2e18a-114">Следующий пример удаляет пользователей из групп.</span><span class="sxs-lookup"><span data-stu-id="2e18a-114">The next example removes users from groups.</span></span>

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
if (cc.Web.GroupExists("Test"))
{
  if (cc.Web.IsUserInGroup("Test", currentUser.LoginName))
  {
    cc.Web.RemoveUserFromGroup("Test", currentUser.LoginName);
  }
}
```

## <a name="add-permission-level-to-group-or-user"></a><span data-ttu-id="2e18a-115">Добавление уровня разрешений для пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="2e18a-115">Add permission level to group or user</span></span>

<span data-ttu-id="2e18a-116">Следующий пример добавляет в группу уровня разрешений.</span><span class="sxs-lookup"><span data-stu-id="2e18a-116">The following example adds a permission level to a group.</span></span>

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.AddPermissionLevelToGroup("Test", RoleType.Contributor);
}
```

<span data-ttu-id="2e18a-117">Следующий пример добавляет уровень разрешений пользователя.</span><span class="sxs-lookup"><span data-stu-id="2e18a-117">The next example adds a permission level to a user.</span></span>

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.AddPermissionLevelToUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="remove-permission-level-from-group-or-user"></a><span data-ttu-id="2e18a-118">Удалить из группы или пользователи уровня разрешений</span><span class="sxs-lookup"><span data-stu-id="2e18a-118">Remove permission level from group or user</span></span>

<span data-ttu-id="2e18a-119">Следующий пример удаляет уровень разрешений из группы.</span><span class="sxs-lookup"><span data-stu-id="2e18a-119">The following example removes a permission level from a group.</span></span>

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemovePermissionLevelFromGroup("Test", RoleType.Reader);
}

```
<span data-ttu-id="2e18a-120">Следующий пример удаляет уровень разрешений пользователя.</span><span class="sxs-lookup"><span data-stu-id="2e18a-120">The next example removes a permission level from a user.</span></span>

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.RemovePermissionLevelFromUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="additional-resources"></a><span data-ttu-id="2e18a-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2e18a-121">Additional resources</span></span>
<span data-ttu-id="2e18a-122"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2e18a-122"></span></span>

- [<span data-ttu-id="2e18a-123">Решения по подготовке сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e18a-123">SharePoint site provisioning solutions</span></span>](sharepoint-site-provisioning-solutions.md)
    
- [<span data-ttu-id="2e18a-124">Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="2e18a-124">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
