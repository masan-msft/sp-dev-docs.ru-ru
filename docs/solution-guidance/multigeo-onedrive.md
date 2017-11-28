---
title: "С помощью OneDrive для бизнеса в географически нескольких клиентов"
ms.date: 11/03/2017
ms.openlocfilehash: 4373f4073a36326d250317bf05f4dd82cd19a84f
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="using-onedrive-for-business-in-a-multi-geo-tenant"></a><span data-ttu-id="c1954-102">С помощью OneDrive для бизнеса в географически нескольких клиентов</span><span class="sxs-lookup"><span data-stu-id="c1954-102">Using OneDrive for Business in a Multi-Geo tenant</span></span>

> <span data-ttu-id="c1954-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="c1954-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="c1954-104">Доступ к пользователя OneDrive для бизнеса сайта, также известной как личный сайт или личных сайтов — это типично для пользовательских приложений.</span><span class="sxs-lookup"><span data-stu-id="c1954-104">Accessing a user's OneDrive for Business site, also known as personal site or my site, is a common scenario in custom applications.</span></span> <span data-ttu-id="c1954-105">В этой статье описывается, как для работы со службой OneDrive для бизнеса сайтов в географически нескольких клиентов.</span><span class="sxs-lookup"><span data-stu-id="c1954-105">This article describes how to work with OneDrive for Business sites in a Multi-Geo tenant.</span></span>

<span data-ttu-id="c1954-106">Можно использовать один из несколько интерфейсов API для доступа к службе OneDrive для бизнеса сайта:</span><span class="sxs-lookup"><span data-stu-id="c1954-106">You can use one of several APIs to access a OneDrive for Business site:</span></span>

- <span data-ttu-id="c1954-107">Microsoft Graph (рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="c1954-107">Microsoft Graph (preferred)</span></span>
- <span data-ttu-id="c1954-108">SharePoint CSOM</span><span class="sxs-lookup"><span data-stu-id="c1954-108">SharePoint CSOM</span></span> 
- <span data-ttu-id="c1954-109">API-Интерфейс REST SharePoint</span><span class="sxs-lookup"><span data-stu-id="c1954-109">SharePoint REST API</span></span>


## <a name="read-onedrive-for-business-files-using-microsoft-graph"></a><span data-ttu-id="c1954-110">Чтение файлы OneDrive для бизнеса с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c1954-110">Read OneDrive for Business files using Microsoft Graph</span></span>
<span data-ttu-id="c1954-111">При использовании Microsoft Graph для чтения OneDrive для бизнеса файла не нужно знать, где расположен сайт OneDrive пользователя.</span><span class="sxs-lookup"><span data-stu-id="c1954-111">When you use Microsoft Graph to read a OneDrive for Business file, you don't have to know where a user's OneDrive site is located.</span></span> <span data-ttu-id="c1954-112">При запросе диске, как показано в следующих примерах, вы получите необходимые файлы.</span><span class="sxs-lookup"><span data-stu-id="c1954-112">When you request the drive, as shown in the following examples, you'll get the files you need.</span></span> 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com/drive/root/children


GET https://graph.microsoft.com/v1.0/users/me/drive/root/children
```

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-microsoft-graph"></a><span data-ttu-id="c1954-113">Получение расположения пользователя OneDrive для бизнеса сайта с помощью Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c1954-113">Get the location of a user's OneDrive for Business site using Microsoft Graph</span></span>
<span data-ttu-id="c1954-114">В приведенных ниже примерах показано, как получить расположение OneDrive для бизнеса сайта с помощью API-Интерфейс Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="c1954-114">The following examples show how to get the location of a OneDrive for Business site using the Microsoft Graph API.</span></span>

```
GET https://graph.microsoft.com/v1.0/users/admin@a830edad9050849524e17052212.onmicrosoft.com/mySite


GET https://graph.microsoft.com/v1.0/users/me/mySite
```

<span data-ttu-id="c1954-115">Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="c1954-115">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

## <a name="get-the-location-of-a-users-onedrive-for-business-site-using-csom-and-rest"></a><span data-ttu-id="c1954-116">Получение расположения пользователя OneDrive для бизнеса сайта с помощью CSOM и REST</span><span class="sxs-lookup"><span data-stu-id="c1954-116">Get the location of a user's OneDrive for Business site using CSOM and REST</span></span>
<span data-ttu-id="c1954-117">В следующем примере показано запросов на основе REST для получения местоположения OneDrive для бизнеса сайта.</span><span class="sxs-lookup"><span data-stu-id="c1954-117">The following example shows a REST-based query to get the location of an OneDrive for Business site.</span></span>

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/PersonalUrl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

<span data-ttu-id="c1954-118">Если вы используете C#, CSOM можно использовать для получения местоположения OneDrive для бизнеса сайта.</span><span class="sxs-lookup"><span data-stu-id="c1954-118">If you're using C#, you can use CSOM to get the location of an OneDrive for Business site.</span></span>

```C#
public string GetUserPersonalUrlCSOM(ClientContext ctx, string userPrincipalName)
{
    string result = null;

    PeopleManager peopleManager = new PeopleManager(ctx);
    var userProperties = peopleManager.GetPropertiesFor(userPrincipalName);
    this.clientContext.ExecuteQuery();
    result = userProperties.PersonalUrl;

    return result;
}
```

## <a name="read-onedrive-for-business-files-using-csom-and-rest"></a><span data-ttu-id="c1954-119">Чтение файлы OneDrive для бизнеса с помощью CSOM и REST</span><span class="sxs-lookup"><span data-stu-id="c1954-119">Read OneDrive for Business files using CSOM and REST</span></span>

<span data-ttu-id="c1954-120">Чтение файлов с помощью CSOM идентична чтение файлов в других семействах сайтов, OneDrive для бизнеса сайта является регулярное семейства сайтов SharePoint с библиотекой документов, где хранятся файлы.</span><span class="sxs-lookup"><span data-stu-id="c1954-120">Reading files using CSOM is identical to reading files on other site collections, a OneDrive for Business site is a regular SharePoint site collection with a document library containing files.</span></span> <span data-ttu-id="c1954-121">В разделе ресурсы для примеров на использование CSOM и REST для загрузки файлов.</span><span class="sxs-lookup"><span data-stu-id="c1954-121">See the resources section for samples on using CSOM and REST to upload files.</span></span>

## <a name="see-also"></a><span data-ttu-id="c1954-122">См. также</span><span class="sxs-lookup"><span data-stu-id="c1954-122">See also</span></span>

- [<span data-ttu-id="c1954-123">Чтение файлов с помощью API-Интерфейс Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c1954-123">Reading files using the Microsoft Graph API</span></span>](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/api/item_list_children)
- [<span data-ttu-id="c1954-124">Передача файлов с помощью REST</span><span class="sxs-lookup"><span data-stu-id="c1954-124">Uploading files using REST</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.RestFileUpload)
- [<span data-ttu-id="c1954-125">Файл загрузки надстройки CSOM SharePoint</span><span class="sxs-lookup"><span data-stu-id="c1954-125">File Upload CSOM SharePoint Add-in</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.FileUpload)
- [<span data-ttu-id="c1954-126">Загрузка больших файлов с помощью CSOM</span><span class="sxs-lookup"><span data-stu-id="c1954-126">Large file upload with CSOM</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Core.LargeFileUpload)


