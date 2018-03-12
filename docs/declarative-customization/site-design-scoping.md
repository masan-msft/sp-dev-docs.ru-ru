---
title: "Определение областей доступа к макетам сайтов SharePoint"
description: "Узнайте, как задавать области для макетов сайтов SharePoint, чтобы управлять тем, кто может просматривать и использовать их."
ms.date: 01/08/2018
ms.openlocfilehash: ec07c838ff993266cc9085be1fe3d79050f14ded
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="scoping-access-to-site-designs"></a><span data-ttu-id="a0164-103">Определение областей доступа к макетам сайтов</span><span class="sxs-lookup"><span data-stu-id="a0164-103">Scoping access to site designs</span></span>

<span data-ttu-id="a0164-104">По умолчанию макеты сайтов доступны всем.</span><span class="sxs-lookup"><span data-stu-id="a0164-104">Site designs are available to everyone by default.</span></span> <span data-ttu-id="a0164-105">Вы можете определять область их действия, чтобы они были доступны только определенным пользователям или группам.</span><span class="sxs-lookup"><span data-stu-id="a0164-105">You can also scope site designs so that they are only available to specific users or groups.</span></span> <span data-ttu-id="a0164-106">Например, в отделе бухгалтерии могут использоваться специальные макеты, которые нет смысла делать общедоступными.</span><span class="sxs-lookup"><span data-stu-id="a0164-106">For example, the accounting apartment may have specific site designs they use, but it may not make sense to share those site designs with everyone.</span></span> <span data-ttu-id="a0164-107">В этой статье описывается, как управлять тем, каким пользователям и группам видны те или иные макеты сайтов.</span><span class="sxs-lookup"><span data-stu-id="a0164-107">This article will explain how you can control which users and groups can see specific site designs.</span></span>

## <a name="granting-rights-to-a-site-design"></a><span data-ttu-id="a0164-108">Предоставление прав для макета сайта</span><span class="sxs-lookup"><span data-stu-id="a0164-108">Granting rights to a site design</span></span>

<span data-ttu-id="a0164-109">Сразу после создания макет сайта доступен всем.</span><span class="sxs-lookup"><span data-stu-id="a0164-109">When a site design is first created, it is available to everyone.</span></span> <span data-ttu-id="a0164-110">Вы можете предоставлять права на **просмотр** макета сайта.</span><span class="sxs-lookup"><span data-stu-id="a0164-110">You can grant **View** rights to the site design.</span></span> <span data-ttu-id="a0164-111">Когда права будут предоставлены, доступ будет только у указанных пользователей или групп (субъектов).</span><span class="sxs-lookup"><span data-stu-id="a0164-111">After rights are granted, only the users or groups (principals) specified have access.</span></span> <span data-ttu-id="a0164-112">Вы можете продолжать предоставлять права другим субъектам при последующих вызовах API.</span><span class="sxs-lookup"><span data-stu-id="a0164-112">You can continue granting rights to more principals with subsequent API calls.</span></span>

> [!NOTE]
> <span data-ttu-id="a0164-113">В настоящее время определение области доступно только для групп безопасности с включенной поддержкой почты и пользователей.</span><span class="sxs-lookup"><span data-stu-id="a0164-113">Scoping is currently only available for mail-enabled security groups and users.</span></span> <span data-ttu-id="a0164-114">В будущем планируется предоставление поддержки и для Групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="a0164-114">We are planning to provide support for Office 365 Groups in the future.</span></span>

## <a name="granting-rights-to-security-groups"></a><span data-ttu-id="a0164-115">Предоставление прав группам безопасности</span><span class="sxs-lookup"><span data-stu-id="a0164-115">Granting rights to security groups</span></span>

<span data-ttu-id="a0164-116">В приведенном ниже примере показано, как определить область действия имеющегося макета сайта, чтобы только члены поддерживающей почту группы безопасности **accounting** могли просматривать и использовать этот макет.</span><span class="sxs-lookup"><span data-stu-id="a0164-116">The following example shows how to scope an existing site design so that only the mail-enabled security group **accounting** can view and use the site design.</span></span>

```powershell
Grant-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com") `
  -Rights View
```

<span data-ttu-id="a0164-117">Вы можете создать макет сайта и сразу предоставить права для него, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="a0164-117">You might want to create a new site design and grant rights at the same time, as shown in the next example.</span></span>

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

## <a name="granting-rights-to-users"></a><span data-ttu-id="a0164-118">Предоставление прав пользователям</span><span class="sxs-lookup"><span data-stu-id="a0164-118">Granting rights to users</span></span>

<span data-ttu-id="a0164-119">Приведенный ниже пример кода предоставляет пользователю Nestor права на просмотр макета сайта (на вымышленном сайте Contoso).</span><span class="sxs-lookup"><span data-stu-id="a0164-119">The following example shows how to grant view rights on a site design to Nestor (a user at the fictional Contoso site).</span></span>

```powershell
PS C:\> Grant-SPOSiteDesignRights `
         -Identity 44252d09-62c4-4913-9eb0-a2a8b8d7f863 `
         -Principals "nestorw@contoso.onmicrosoft.com" `
         -Rights View
```

## <a name="viewing-rights-assigned-to-a-site-design"></a><span data-ttu-id="a0164-120">Права на просмотр, назначенные макету сайта</span><span class="sxs-lookup"><span data-stu-id="a0164-120">Viewing rights assigned to a site design</span></span>

<span data-ttu-id="a0164-121">Чтобы просматривать права, используйте командлет **Get-SPOSiteDesignRights**.</span><span class="sxs-lookup"><span data-stu-id="a0164-121">To view rights, use the **Get-SPOSiteDesignRights** cmdlet.</span></span> <span data-ttu-id="a0164-122">В приведенном ниже примере показано, как использовать этот командлет, а также представлен отклик для случая, когда права на просмотр есть только у пользователя Nestor.</span><span class="sxs-lookup"><span data-stu-id="a0164-122">The following example shows how to use this cmdlet and a response in the case where only Nestor has view rights.</span></span>

```powershell
PS C:\> Get-SPOSiteDesignRights 607aed52-6d61-490a-b692-c0f58a6981a1
```

```
DisplayName  PrincipalName                                      Rights
-----------  -------------                                      ------
Nestor Wilke i:0#.f|membership|nestorw@contoso.onmicrosoft.com   View
```

## <a name="revoking-rights-from-a-site-design"></a><span data-ttu-id="a0164-123">Отзыв прав для макета сайта</span><span class="sxs-lookup"><span data-stu-id="a0164-123">Revoking rights from a site design</span></span>

<span data-ttu-id="a0164-124">Вы можете отозвать права для любого субъекта.</span><span class="sxs-lookup"><span data-stu-id="a0164-124">You can revoke rights for any principal.</span></span> <span data-ttu-id="a0164-125">Если отозвать права на просмотр для всех субъектов, макет сайта снова станет общедоступным.</span><span class="sxs-lookup"><span data-stu-id="a0164-125">If you revoke view rights for all principles, the site design will again be available to everyone.</span></span>

<span data-ttu-id="a0164-126">Приведенный ниже пример кода отзывает права на доступ для группы безопасности accounting, поддерживающей почту, и пользователя Nestor.</span><span class="sxs-lookup"><span data-stu-id="a0164-126">The following example revokes access for the accounting mail-enabled security group and Nestor.</span></span>

```powershell
Revoke-SPOSiteDesignRights `
  -Identity db752673-18fd-44db-865a-aa3e0b28698e `
  -Principals ("accounting@contoso.sharepoint.com","nestorw@spdfcontosodemo2.onmicrosoft.com") `
```
