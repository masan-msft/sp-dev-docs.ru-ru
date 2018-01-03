---
title: "Определение областей доступа к макетам сайтов SharePoint"
description: "Узнайте, как задавать области для макетов сайтов SharePoint, чтобы управлять тем, кто может просматривать и использовать их."
ms.date: 12/14/2017
ms.openlocfilehash: d6181e92cd76af2e16e847219bb7aaa129ddebb7
ms.sourcegitcommit: 8e63066ad9591e51bbda419b1b9527452111081b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="scoping-access-to-site-designs"></a><span data-ttu-id="1c61d-103">Определение областей доступа к макетам сайтов</span><span class="sxs-lookup"><span data-stu-id="1c61d-103">Scoping access to site designs</span></span>

> [!NOTE]
> <span data-ttu-id="1c61d-104">Макеты и скрипты сайтов в настоящий момент пересматриваются и могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="1c61d-104">Site designs and site scripts are currently in preview and are subject to change.</span></span> <span data-ttu-id="1c61d-105">Сейчас они не поддерживаются для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="1c61d-105">They are currently not supported for use in production environments.</span></span>

<span data-ttu-id="1c61d-106">По умолчанию макеты сайтов доступны всем.</span><span class="sxs-lookup"><span data-stu-id="1c61d-106">Site designs are available to everyone by default.</span></span> <span data-ttu-id="1c61d-107">Однако вы можете определять область их действия, чтобы они были доступны только определенным пользователям или группам.</span><span class="sxs-lookup"><span data-stu-id="1c61d-107">But you can scope site designs so that they are only available to specific users or groups.</span></span> <span data-ttu-id="1c61d-108">Например, в отделе бухгалтерии могут использоваться специальные макеты, которые нет смысла делать общедоступными.</span><span class="sxs-lookup"><span data-stu-id="1c61d-108">For example, the accounting apartment may have specific site designs they use, but it may not make sense to share those site designs with everyone.</span></span> <span data-ttu-id="1c61d-109">В этой статье описывается, как управлять тем, каким пользователям и группам видны те или иные макеты сайтов.</span><span class="sxs-lookup"><span data-stu-id="1c61d-109">This article will explain how you can control which users and groups can see specific site designs.</span></span>

## <a name="granting-rights-to-a-site-design"></a><span data-ttu-id="1c61d-110">Предоставление прав для макета сайта</span><span class="sxs-lookup"><span data-stu-id="1c61d-110">Granting rights to a site design</span></span>

<span data-ttu-id="1c61d-111">Сразу после создания макет сайта доступен всем.</span><span class="sxs-lookup"><span data-stu-id="1c61d-111">When a site design is first created it is available to everyone.</span></span> <span data-ttu-id="1c61d-112">Вы можете предоставлять права на **просмотр** макета.</span><span class="sxs-lookup"><span data-stu-id="1c61d-112">You can grant **View** rights to the site design.</span></span> <span data-ttu-id="1c61d-113">После предоставления прав доступ получают только указанные пользователи или группы (субъекты).</span><span class="sxs-lookup"><span data-stu-id="1c61d-113">Once rights are granted, only the users or groups (principals) specified have access.</span></span> <span data-ttu-id="1c61d-114">Вы можете продолжать предоставлять права другим субъектам при последующих вызовах API.</span><span class="sxs-lookup"><span data-stu-id="1c61d-114">You can continue granting rights to more principals with subsequent API calls.</span></span>

## <a name="granting-rights-to-security-groups"></a><span data-ttu-id="1c61d-115">Предоставление прав группам безопасности</span><span class="sxs-lookup"><span data-stu-id="1c61d-115">Granting rights to security groups</span></span>

<span data-ttu-id="1c61d-116">В приведенном ниже примере показано, как определить область имеющегося макета сайта, чтобы только члены поддерживающей почту группы безопасности **accounting** могли просматривать и использовать этот макет.</span><span class="sxs-lookup"><span data-stu-id="1c61d-116">Here's an example of how to scope an existing site design so that only the mail-enabled security group **accounting** can view and use the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com") `
  -Rights View
```

<span data-ttu-id="1c61d-117">Вы можете создать макет сайта и сразу предоставить права для него, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="1c61d-117">You may want to create a new site design and grant rights at the same time as shown in the next example.</span></span>

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

## <a name="granting-rights-to-users"></a><span data-ttu-id="1c61d-118">Предоставление прав пользователям</span><span class="sxs-lookup"><span data-stu-id="1c61d-118">Granting permission to users</span></span>

<span data-ttu-id="1c61d-119">В приведенном ниже примере показано, как предоставить права для макета сайта пользователю Nestor (пользователю на вымышленном сайте Contoso).</span><span class="sxs-lookup"><span data-stu-id="1c61d-119">Here's an example of how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.sharepoint.com" `
         -Rights View
```

## <a name="viewing-rights-assigned-to-a-site-design"></a><span data-ttu-id="1c61d-120">Права на просмотр, назначенные макету сайта</span><span class="sxs-lookup"><span data-stu-id="1c61d-120">Viewing rights assigned to a site design</span></span>

<span data-ttu-id="1c61d-121">Чтобы просматривать права, используйте командлет **Get-SPOSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="1c61d-121">To view rights, use the **Get-SPOSiteDesignRights** cmdlet.</span></span> <span data-ttu-id="1c61d-122">В приведенном ниже примере показано, как использовать этот командлет, а также представлен отклик для случая, когда права на просмотр есть только у пользователя Nestor.</span><span class="sxs-lookup"><span data-stu-id="1c61d-122">The following example shows how to use this cmdlet and a response in the case where only Nestor has view rights.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.sharepoint.com   View
```

## <a name="revoking-rights-from-a-site-design"></a><span data-ttu-id="1c61d-123">Отзыв прав для макета сайта</span><span class="sxs-lookup"><span data-stu-id="1c61d-123">Revoking rights from a site design</span></span>

<span data-ttu-id="1c61d-124">Вы можете отозвать права для любого субъекта.</span><span class="sxs-lookup"><span data-stu-id="1c61d-124">You can revoke rights for any principal.</span></span> <span data-ttu-id="1c61d-125">Если отозвать права для всех субъектов, макет сайта снова станет общедоступным.</span><span class="sxs-lookup"><span data-stu-id="1c61d-125">If you revoke view rights for all principles, then the site design will again be available to everyone.</span></span>

<span data-ttu-id="1c61d-126">В приведенном ниже примере показано, как отозвать доступ для поддерживающей почту группы безопасности accounting и пользователя Nestor.</span><span class="sxs-lookup"><span data-stu-id="1c61d-126">Here's an example of revoking access for the accounting mail-enabled security group and Nestor.</span></span>

```powershell
Revoke-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com","nestorw@spdfcontosodemo2.onmicrosoft.com") `
```
