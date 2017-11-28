---
title: "Управление SharePoint пользователями и группами"
ms.date: 11/03/2017
ms.openlocfilehash: 9f287515faede9c92aa172c947f6b1826efc0fa1
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="manage-sharepoint-users-and-groups"></a>Управление SharePoint пользователями и группами

Управление пользователями, группами и разрешения в семействе сайтов SharePoint. 

_**Применимо к:** Office 365 | SharePoint 2013 | Надстройки SharePoint | SharePoint Online_

В этой статье показано, как добавить или удалить групп и пользователей в рамках указанного семейства сайтов. Примеры кода в этой статье Добавление пользователей и групп и затем предоставьте им уровней разрешений доступа к SharePoint. Этих пользователей и группы разрешений уровня действия реализуются с помощью методов расширения в образце PnP [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) .

## <a name="before-you-begin"></a>Перед началом работы

Чтобы начать работу, загрузите пример надстройки [Core.GroupManagement](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.GroupManagement) из проекта [разработчика Office 365 шаблоны и рекомендации](https://github.com/SharePoint/PnP/tree/dev) на репозиториев.

## <a name="add-and-remove-groups-and-users"></a>Добавление и удаление пользователей и групп

Следующем примере показано, как добавлять группы и добавление пользователей в группу.

**Примечание:**  Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

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

Следующий пример удаляет группу.

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemoveGroup("Test");
}
```

Следующий пример удаляет пользователей из групп.

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

## <a name="add-permission-level-to-group-or-user"></a>Добавление уровня разрешений для пользователя или группы

Следующий пример добавляет в группу уровня разрешений.

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.AddPermissionLevelToGroup("Test", RoleType.Contributor);
}
```

Следующий пример добавляет уровень разрешений пользователя.

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.AddPermissionLevelToUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="remove-permission-level-from-group-or-user"></a>Удалить из группы или пользователи уровня разрешений

Следующий пример удаляет уровень разрешений из группы.

```C#
if (cc.Web.GroupExists("Test"))
{
  cc.Web.RemovePermissionLevelFromGroup("Test", RoleType.Reader);
}

```
Следующий пример удаляет уровень разрешений пользователя.

```C#
cc.Load(cc.Web, web => web.CurrentUser);
cc.ExecuteQuery();
Microsoft.SharePoint.Client.User currentUser = cc.Web.CurrentUser;
cc.Web.RemovePermissionLevelFromUser(currentUser.LoginName, RoleType.Reader);
```

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Решения по подготовке сайтов SharePoint](sharepoint-site-provisioning-solutions.md)
    
- [Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта](Branding-and-site-provisioning-solutions-for-SharePoint.md)
