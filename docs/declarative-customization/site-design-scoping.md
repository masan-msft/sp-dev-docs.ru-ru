---
title: "Определение областей доступа к макетам сайтов SharePoint"
description: "Узнайте, как задавать области для макетов сайтов SharePoint, чтобы управлять тем, кто может просматривать и использовать их."
ms.date: 12/14/2017
ms.openlocfilehash: b7a29bbbd28f097e92364d9ab73d16d896ad3446
ms.sourcegitcommit: 31f793b42ec75679f01e1a024d0375a2bc7b5ec7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="scoping-access-to-site-designs"></a>Определение областей доступа к макетам сайтов

> [!NOTE]
> Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены. Сейчас они не поддерживаются для использования в рабочих средах.

По умолчанию макеты сайтов доступны всем. Однако вы можете определять область их действия, чтобы они были доступны только определенным пользователям или группам. Например, в отделе бухгалтерии могут использоваться специальные макеты, которые нет смысла делать общедоступными. В этой статье описывается, как управлять тем, каким пользователям и группам видны те или иные макеты сайтов.

## <a name="granting-rights-to-a-site-design"></a>Предоставление прав для макета сайта

Сразу после создания макет сайта доступен всем. Вы можете предоставлять права на **просмотр** макета. После предоставления прав доступ получают только указанные пользователи или группы (субъекты). Вы можете продолжать предоставлять права другим субъектам при последующих вызовах API.

## <a name="granting-rights-to-security-groups"></a>Предоставление прав группам безопасности

В приведенном ниже примере показано, как определить область имеющегося макета сайта, чтобы только члены поддерживающей почту группы безопасности **accounting** могли просматривать и использовать этот макет.

```powershell
Grant-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com") `
  -Rights View
```

Вы можете создать макет сайта и сразу предоставить права для него, как показано в приведенном ниже примере.

```powershell
Add-SPOSiteDesign `
  -Title "Scoped site design" `
  -Description "Scoped to only the accounting email security group" `
  -SiteScripts 256494cb-bd31-4f60-9eba-285308d7a863 `
  -WebTemplate 64 `
  -PreviewImageUrl "https://contoso.sharepoint.com/SiteAssets/scope-image.png" `
| Grant-SPOSiteDesignRights `
  -Principals ("accounting@contoso.com") `
  -Rights View
```

## <a name="granting-rights-to-users"></a>Предоставление прав пользователям

В приведенном ниже примере показано, как предоставить права для макета сайта пользователю Nestor (пользователю на вымышленном сайте Contoso).

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="viewing-rights-assigned-to-a-site-design"></a>Права на просмотр, назначенные макету сайта

Чтобы просматривать права, используйте командлет **Get-SPOSiteDesignRights**. В приведенном ниже примере показано, как использовать этот командлет, а также представлен отклик для случая, когда права на просмотр есть только у пользователя Nestor.

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="revoking-rights-from-a-site-design"></a>Отзыв прав для макета сайта

Вы можете отозвать права для любого субъекта. Если отозвать права для всех субъектов, макет сайта снова станет общедоступным.

В приведенном ниже примере показано, как отозвать доступ для поддерживающей почту группы безопасности accounting и пользователя Nestor.

```powershell
Revoke-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com","nestorw@spdfcontosodemo2.onmicrosoft.com") `
```
