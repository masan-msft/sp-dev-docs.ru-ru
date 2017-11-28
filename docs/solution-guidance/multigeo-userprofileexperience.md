---
title: "Работа с профилями пользователей в SharePoint несколькими-географически клиентов"
ms.date: 11/03/2017
ms.openlocfilehash: 85362f0bd67c1e148d8c75d691a67033e880c722
ms.sourcegitcommit: 4ea7e9cb1efb53f89da236282002956739d77418
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/09/2017
---
# <a name="work-with-user-profiles-in-a-sharepoint-multi-geo-tenant"></a><span data-ttu-id="a8835-102">Работа с профилями пользователей в SharePoint несколькими-географически клиентов</span><span class="sxs-lookup"><span data-stu-id="a8835-102">Work with user profiles in a SharePoint Multi-Geo tenant</span></span>

> <span data-ttu-id="a8835-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="a8835-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="a8835-104">В географически несколькими клиента можно определить расположение предпочитаемый данных для пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8835-104">In a Multi-Geo tenant, you can define a preferred data location for a user.</span></span> <span data-ttu-id="a8835-105">В этой статье также описывает, как найти сайта OneDrive пользователя, а также для чтения и обновления по умолчанию и настраиваемых свойств профиля.</span><span class="sxs-lookup"><span data-stu-id="a8835-105">This article also describes how to find a user's OneDrive site and how to read and update default and custom user profile properties.</span></span>

## <a name="where-are-user-profiles-located-in-a-multi-geo-tenant"></a><span data-ttu-id="a8835-106">Где находятся профили пользователей в географически нескольких клиентов?</span><span class="sxs-lookup"><span data-stu-id="a8835-106">Where are user profiles located in a Multi-Geo tenant?</span></span>
<span data-ttu-id="a8835-107">В географически нескольких клиентов, диапазон пользователей SharePoint, расположения различных географически — например, некоторые пользователи — это в Северной Америке некоторые, в Европе и т. д.</span><span class="sxs-lookup"><span data-stu-id="a8835-107">In a Multi-Geo tenant, SharePoint users span the different geo locations - for example, some users are in North America, some are in Europe, and so on.</span></span> <span data-ttu-id="a8835-108">Эта модель также распространяется на учетные записи пользователей и личные сайты (OneDrive для бизнеса).</span><span class="sxs-lookup"><span data-stu-id="a8835-108">This model also applies to user accounts and personal (OneDrive for Business) sites.</span></span> <span data-ttu-id="a8835-109">В идеальном варианте пользователей и их учетных записей пользователей и сайтов, в том же месте географически.</span><span class="sxs-lookup"><span data-stu-id="a8835-109">Ideally, the users and their user accounts and sites are in the same geo location.</span></span> <span data-ttu-id="a8835-110">Чтобы это, прежде чем создавать личные сайты, расположение пользователя предпочтительный данных значение их географического расположения.</span><span class="sxs-lookup"><span data-stu-id="a8835-110">To ensure this, before you create personal sites, you set the user's preferred data location to their geo location.</span></span> 

<span data-ttu-id="a8835-111">В примере показано на следующем рисунке vesa@contoso.onmicrosoft.com пользователя живущих в Европе и имеет равной **ЕВРО**предпочитаемый данных расположения.</span><span class="sxs-lookup"><span data-stu-id="a8835-111">In the example shown in the following image, user vesa@contoso.onmicrosoft.com is living in Europe and has a preferred data location set to **EUR**.</span></span> <span data-ttu-id="a8835-112">Таким образом:</span><span class="sxs-lookup"><span data-stu-id="a8835-112">As such:</span></span>
 
- <span data-ttu-id="a8835-113">По умолчанию копию профиль пользователя находится в папке географически Европе.</span><span class="sxs-lookup"><span data-stu-id="a8835-113">The default copy of the user's profile is in the Europe geo location.</span></span>
- <span data-ttu-id="a8835-114">Личного сайта пользователя создается в папке географически Европе.</span><span class="sxs-lookup"><span data-stu-id="a8835-114">The user's personal site is created in the Europe geo location.</span></span>

<span data-ttu-id="a8835-115">Bert@contoso.onmicrosoft.com пользователь имеет свой расположение предпочитаемый данных, задайте значение **им**.</span><span class="sxs-lookup"><span data-stu-id="a8835-115">User bert@contoso.onmicrosoft.com has his preferred data location set to **NAM**.</span></span> <span data-ttu-id="a8835-116">Так как он был личного сайта, размещенного в Европе, перед его расположение предпочитаемый данных было задано, свой профиль остается в Европе.</span><span class="sxs-lookup"><span data-stu-id="a8835-116">Because he  had a personal site hosted in Europe before his preferred data location was set, his profile stays in Europe.</span></span> 

![Настройка карты World, показывающая расположение по умолчанию geo в Северной Америке и вспомогательные расположений в Европе и Азии, с пользователями, географического расположения и расположения предпочитаемый данных](media/multigeo/multigeouserprofiles_intro.png)

<span data-ttu-id="a8835-118">Профили пользователей и личные сайты, в том же месте географически.</span><span class="sxs-lookup"><span data-stu-id="a8835-118">Users' profiles and personal sites are in the same geo location.</span></span> <span data-ttu-id="a8835-119">Для пользователей, у которых нет личного сайта:</span><span class="sxs-lookup"><span data-stu-id="a8835-119">For users who do not have a personal site:</span></span>

- <span data-ttu-id="a8835-120">Если они расположение предпочитаемый данных, свой профиль расположен в эту папку географически.</span><span class="sxs-lookup"><span data-stu-id="a8835-120">If they set a preferred data location, their profile is located in that geo location.</span></span>
- <span data-ttu-id="a8835-121">Если они не заданы расположение предпочитаемый данных, свой профиль находится в каталоге географически по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8835-121">If they have not set a preferred data location, their profile is located in the default geo location.</span></span>

<span data-ttu-id="a8835-122">Программными средствами обнаруживать расположение профиля пользователя, выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="a8835-122">To programmatically discover a user's profile location, you can do one of the following:</span></span>

- <span data-ttu-id="a8835-123">Использование профилей пользователей SharePoint API.</span><span class="sxs-lookup"><span data-stu-id="a8835-123">Use the SharePoint User Profile API.</span></span> <span data-ttu-id="a8835-124">Мы рекомендуем этот подход, так как это работает во всех сценариях.</span><span class="sxs-lookup"><span data-stu-id="a8835-124">We recommend this approach because it works in all scenarios.</span></span> 
- <span data-ttu-id="a8835-125">С помощью Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="a8835-125">Use Microsoft Graph.</span></span> <span data-ttu-id="a8835-126">Это работает для пользователей, имеющих личные сайты, но не для пользователей, у которых нет личных сайтов.</span><span class="sxs-lookup"><span data-stu-id="a8835-126">This works for users who also have personal sites, but not for users who don't have personal sites.</span></span>

### <a name="use-the-sharepoint-user-profile-api-to-detect-the-profile-location"></a><span data-ttu-id="a8835-127">Использование API профилей пользователей SharePoint для определения расположения профилей</span><span class="sxs-lookup"><span data-stu-id="a8835-127">Use the SharePoint User Profile API to detect the profile location</span></span>
<span data-ttu-id="a8835-128">Можно вызвать API профилей пользователей SharePoint с помощью REST или CSOM, чтобы получить URL-адрес узла личного сайта для указанной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a8835-128">You can call the SharePoint User Profile API via REST or CSOM to retrieve the personal site host URL for a given account.</span></span> <span data-ttu-id="a8835-129">Этот URL-адрес содержит размещения личного сайта для личного сайта пользователя, независимо от того, создан ли личного сайта.</span><span class="sxs-lookup"><span data-stu-id="a8835-129">This URL contains the personal site host for the user's personal site, regardless of whether the personal site has been created.</span></span> <span data-ttu-id="a8835-130">В следующем примере показано вызова REST.</span><span class="sxs-lookup"><span data-stu-id="a8835-130">The following example shows the REST call.</span></span>

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/personalsitehosturl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

<span data-ttu-id="a8835-131">Если вы используете C#, CSOM, как показано в следующем примере, простой в использовании.</span><span class="sxs-lookup"><span data-stu-id="a8835-131">If you're using C#, CSOM, as shown in the following example, is easier to use.</span></span>

```C#
public string GetUserPersonalSiteHostUrlCSOM(string userPrincipalName)
{
    string result = null;

    PeopleManager peopleManager = new PeopleManager(this.clientContext);
    var userProperties = peopleManager.GetPropertiesFor($"i:0#.f|membership|{userPrincipalName}");
    this.clientContext.Load(userProperties);
    this.clientContext.ExecuteQuery();
    result = userProperties.PersonalSiteHostUrl;

    return result;
}
```

<span data-ttu-id="a8835-132">При наличии URL-адрес узла личного сайта, который можно использовать для получения URL-адрес сайта администрирования клиента для географического расположения, на котором размещается в профиле пользователя наряду со сведениями о [несколькими географически обнаружения](multigeo-discovery.md) .</span><span class="sxs-lookup"><span data-stu-id="a8835-132">When you have the personal site host URL, you can use that along with the [Multi-Geo discovery](multigeo-discovery.md) information to get the tenant admin site URL for the geo location that hosts the user's profile.</span></span>

<span data-ttu-id="a8835-133">Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="a8835-133">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

### <a name="use-microsoft-graph-to-detect-the-users-personal-site-url"></a><span data-ttu-id="a8835-134">Использование Microsoft Graph для определения URL-адреса личного сайта пользователя</span><span class="sxs-lookup"><span data-stu-id="a8835-134">Use Microsoft Graph to detect the user's personal site URL</span></span>
<span data-ttu-id="a8835-135">Для обнаружения URL-адреса личного сайта пользователя в географически нескольких клиентов, можно использовать при следующем вызове Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="a8835-135">To discover a user's personal site URL in a Multi-Geo tenant, you can use the following Microsoft Graph call:</span></span>

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=mySite
```

<span data-ttu-id="a8835-136">При наличии URL-адрес узла личного сайта, который можно использовать для получения URL-адрес сайта администрирования клиента для географического расположения, на котором размещается в профиле пользователя наряду со сведениями о [несколькими географически обнаружения](multigeo-discovery.md) .</span><span class="sxs-lookup"><span data-stu-id="a8835-136">When you have the personal site host URL, you can use that along with the [Multi-Geo discovery](multigeo-discovery.md) information to get the tenant admin site URL for the geo location that hosts the user's profile.</span></span>

><span data-ttu-id="a8835-137">**Примечание:** Если у пользователя нет личного сайта, этот способ не работает.</span><span class="sxs-lookup"><span data-stu-id="a8835-137">**Note:** If the user doesn't have a personal site, this approach will not work.</span></span> <span data-ttu-id="a8835-138">Вместо этого следует использовать API профилей пользователей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8835-138">Instead, you should use the SharePoint User Profile API.</span></span>

<span data-ttu-id="a8835-139">Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="a8835-139">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

## <a name="updating-user-profile-properties"></a><span data-ttu-id="a8835-140">Обновление свойств профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="a8835-140">Updating user profile properties</span></span>
<span data-ttu-id="a8835-141">Предоставление доступа к массового обновления для свойств профилей пользователей — это распространенные сценарии для предприятий.</span><span class="sxs-lookup"><span data-stu-id="a8835-141">Making bulk updates to user profile properties is a common scenario for enterprise customers.</span></span> <span data-ttu-id="a8835-142">Процесса для использования в зависимости от типа свойства профиля пользователя, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="a8835-142">The process to use varies based on the type of user profile property you want to update.</span></span>

### <a name="updating-default-user-profile-properties"></a><span data-ttu-id="a8835-143">Обновление свойств профиля пользователя по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a8835-143">Updating default user profile properties</span></span>
<span data-ttu-id="a8835-144">Некоторых свойств профиля пользователя, которые доступны по умолчанию; например **отдел**, **AboutMe**и **PreferredDataLocation**.</span><span class="sxs-lookup"><span data-stu-id="a8835-144">Some user profile properties are available by default; for example, **Department**, **AboutMe**, and **PreferredDataLocation**.</span></span> <span data-ttu-id="a8835-145">Мы рекомендуем использовать Microsoft Graph API обновляет эти свойства, так как Microsoft Graph принять во внимание географически.</span><span class="sxs-lookup"><span data-stu-id="a8835-145">We recommend that you use the Microsoft Graph API to update these properties, because Microsoft Graph is geo-aware.</span></span> <span data-ttu-id="a8835-146">Следующем примере показано, как обновить свойство **AboutMe** для bert@contoso.onmicrosoft.com пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8835-146">The following example shows how to update the **AboutMe** property for the user bert@contoso.onmicrosoft.com.</span></span>

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=aboutme
```

<span data-ttu-id="a8835-147">Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="a8835-147">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

#### <a name="updating-the-preferred-data-location-property"></a><span data-ttu-id="a8835-148">Обновление свойства расположение предпочитаемый данных</span><span class="sxs-lookup"><span data-stu-id="a8835-148">Updating the preferred data location property</span></span>
<span data-ttu-id="a8835-149">Расположение предпочитаемый данных пользователя (свойство**preferredDataLocation** ) указывает расположение предпочитаемый географически для пользователя.</span><span class="sxs-lookup"><span data-stu-id="a8835-149">The user's preferred data location (**preferredDataLocation** property) indicates the preferred geo location for the user.</span></span> <span data-ttu-id="a8835-150">Это влияет на следующие:</span><span class="sxs-lookup"><span data-stu-id="a8835-150">This affects the following:</span></span>

- <span data-ttu-id="a8835-151">Географического расположения, где был подготовлен личного сайта пользователя</span><span class="sxs-lookup"><span data-stu-id="a8835-151">The geo location where the user's personal site is provisioned</span></span>
- <span data-ttu-id="a8835-152">Географически расположение, где создаются сайты группы пользователя</span><span class="sxs-lookup"><span data-stu-id="a8835-152">The geo location where the user's group sites are created</span></span> 

<span data-ttu-id="a8835-153">Так как расположение предпочитаемый данных является свойством по умолчанию, мы рекомендуем использовать Microsoft Graph API для настройки, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="a8835-153">Because the preferred data location is a default property, we recommend that you use the Microsoft Graph API  to configure it, as shown in the following example.</span></span> 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=preferredDataLocation

PATCH https://graph.microsoft.com/beta/users/bert@contoso.onmicrosoft.com

JSON payload:
{
    "preferredDataLocation" : "eur"
}

```

<span data-ttu-id="a8835-154">Для получения дополнительных сведений см [MultiGeo.UserPreferredDataLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserPreferredDataLocation) .</span><span class="sxs-lookup"><span data-stu-id="a8835-154">To learn more, see the [MultiGeo.UserPreferredDataLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserPreferredDataLocation) sample.</span></span>

### <a name="custom-sharepoint-user-profile-properties"></a><span data-ttu-id="a8835-155">Настраиваемые свойства профилей пользователей SharePoint</span><span class="sxs-lookup"><span data-stu-id="a8835-155">Custom SharePoint user profile properties</span></span>
<span data-ttu-id="a8835-156">Свойства профиля пользователя конкретной компании можно добавить к профилям пользователей в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a8835-156">You can add company-specific user profile properties to user profiles in SharePoint.</span></span> <span data-ttu-id="a8835-157">Для клиентов SharePoint несколькими-географически следующие соображения.</span><span class="sxs-lookup"><span data-stu-id="a8835-157">For SharePoint Multi-Geo tenants, the following considerations apply:</span></span>

- <span data-ttu-id="a8835-158">Свойства профиля пользователя создаются на уровне географического расположения.</span><span class="sxs-lookup"><span data-stu-id="a8835-158">Custom user profile properties are created at the geo location level.</span></span> <span data-ttu-id="a8835-159">Это свойство недоступен в в других местах, географически при создании свойства в расположение географически Европе.</span><span class="sxs-lookup"><span data-stu-id="a8835-159">If you create a property in the Europe geo location, that property is not available in the other geo locations.</span></span> <span data-ttu-id="a8835-160">Рекомендуется создание настраиваемого пользовательского свойства профиля в все географического расположения.</span><span class="sxs-lookup"><span data-stu-id="a8835-160">As a best practice, create custom user profile properties in all geo locations.</span></span> <span data-ttu-id="a8835-161">Это снижает вероятность, что данные будут потеряны при перемещении пользователей в географически подразделениях.</span><span class="sxs-lookup"><span data-stu-id="a8835-161">This reduces the risk that data will be lost when a user move across geo locations.</span></span>
- <span data-ttu-id="a8835-162">Необходимо прочитать и обновление свойств профиля пользователя на уровне географического расположения.</span><span class="sxs-lookup"><span data-stu-id="a8835-162">You must read and update custom user profile properties at the geo location level.</span></span> <span data-ttu-id="a8835-163">При создании настраиваемых свойств в все географического расположения, необходимо итерации по географического расположения и обновите свойство для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="a8835-163">If you created a custom property in all geo locations, you need to iterate over the geo locations and update the property for all  users.</span></span>

```C#
// For SharePoint Online custom properties, use the following approach.
string userPrincipalName = "bert@contoso.onmicrosoft.com";
string userAccountName = $"i:0#.f|membership|{userPrincipalName}";
PeopleManager peopleManager = new PeopleManager(tenantAdminContext);
var propsToRetrieve = new string[] { "CostCenter", "CustomProperty" };
var props = peopleManager.GetUserProfilePropertiesFor(new UserProfilePropertiesForUser(tenantAdminContext, userAccountName, propsToRetrieve));
tenantAdminContext.ExecuteQuery();

int i = 0;
foreach (var prop in props)
{
    Console.WriteLine($"Prop: {propsToRetrieve[i]} Value: {prop}");
    i++;
}

// Update user profile properties
peopleManager.SetSingleValueProfileProperty(userAccountName, "CostCenter", "89786879");
tenantAdminContext.ExecuteQuery();
```

<span data-ttu-id="a8835-164">Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .</span><span class="sxs-lookup"><span data-stu-id="a8835-164">To learn more, see the [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) sample.</span></span>

### <a name="using-the-bulk-user-profile-update-api"></a><span data-ttu-id="a8835-165">С помощью массового обновления профиля пользователя API</span><span class="sxs-lookup"><span data-stu-id="a8835-165">Using the bulk user profile update API</span></span>
<span data-ttu-id="a8835-166">[Профиль пользователя массового обновления API](https://msdn.microsoft.com/en-us/pnp_articles/bulk-user-profile-update-api-for-sharepoint-online) можно использовать для выполнения массового обновления настраиваемых свойств профиля в географически нескольких клиентов.</span><span class="sxs-lookup"><span data-stu-id="a8835-166">You can use the [bulk user profile update API](https://msdn.microsoft.com/en-us/pnp_articles/bulk-user-profile-update-api-for-sharepoint-online) to make bulk updates to custom user profile properties in a Multi-Geo tenant.</span></span> <span data-ttu-id="a8835-167">Обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="a8835-167">Note the following:</span></span>

- <span data-ttu-id="a8835-168">Этот интерфейс API работает на уровне географического расположения и не Multi-географически принять во внимание.</span><span class="sxs-lookup"><span data-stu-id="a8835-168">This API works at the geo location level and is not Multi-Geo aware.</span></span> <span data-ttu-id="a8835-169">К примеру при использовании API в расположении географически Европа обновляются только учетные записи в Европе.</span><span class="sxs-lookup"><span data-stu-id="a8835-169">For example, if you use the API in the Europe geo location, only accounts in Europe are updated.</span></span>
- <span data-ttu-id="a8835-170">При указании Импорт файла с учетными записями в разных географического расположения, API будет обновлять только свойства для пользователей в эту папку географически.</span><span class="sxs-lookup"><span data-stu-id="a8835-170">If you specify an import file with accounts in different geo locations, the API will only update the properties for the users in that geo location.</span></span>


## <a name="see-also"></a><span data-ttu-id="a8835-171">См. также</span><span class="sxs-lookup"><span data-stu-id="a8835-171">See also</span></span>

- [<span data-ttu-id="a8835-172">Общие сведения об API для массового обновления настраиваемых свойств профиля для SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a8835-172">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span></span>](bulk-user-profile-update-api-for-sharepoint-online.md)
- [<span data-ttu-id="a8835-173">Пример API пакета обновления профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="a8835-173">User Profile Batch Update API sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.BatchUpdate.API)


