---
title: "Работа с профилями пользователей в SharePoint несколькими-географически клиентов"
ms.date: 11/03/2017
ms.openlocfilehash: 75880f9811d299cd14a66467fac73439aefa1818
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="work-with-user-profiles-in-a-sharepoint-multi-geo-tenant"></a>Работа с профилями пользователей в SharePoint несколькими-географически клиентов

> **Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.

В географически несколькими клиента можно определить расположение предпочитаемый данных для пользователя. В этой статье также описывает, как найти сайта OneDrive пользователя, а также для чтения и обновления по умолчанию и настраиваемых свойств профиля.

## <a name="where-are-user-profiles-located-in-a-multi-geo-tenant"></a>Где находятся профили пользователей в географически нескольких клиентов?
В географически нескольких клиентов, диапазон пользователей SharePoint, расположения различных географически — например, некоторые пользователи — это в Северной Америке некоторые, в Европе и т. д. Эта модель также распространяется на учетные записи пользователей и личные сайты (OneDrive для бизнеса). В идеальном варианте пользователей и их учетных записей пользователей и сайтов, в том же месте географически. Чтобы это, прежде чем создавать личные сайты, расположение пользователя предпочтительный данных значение их географического расположения. 

В примере показано на следующем рисунке vesa@contoso.onmicrosoft.com пользователя живущих в Европе и имеет равной **ЕВРО**предпочитаемый данных расположения. Таким образом:
 
- По умолчанию копию профиль пользователя находится в папке географически Европе.
- Личного сайта пользователя создается в папке географически Европе.

Bert@contoso.onmicrosoft.com пользователь имеет свой расположение предпочитаемый данных, задайте значение **им**. Так как он был личного сайта, размещенного в Европе, перед его расположение предпочитаемый данных было задано, свой профиль остается в Европе. 

![Настройка карты World, показывающая расположение по умолчанию geo в Северной Америке и вспомогательные расположений в Европе и Азии, с пользователями, географического расположения и расположения предпочитаемый данных](media/multigeo/multigeouserprofiles_intro.png)

Профили пользователей и личные сайты, в том же месте географически. Для пользователей, у которых нет личного сайта:

- Если они расположение предпочитаемый данных, свой профиль расположен в эту папку географически.
- Если они не заданы расположение предпочитаемый данных, свой профиль находится в каталоге географически по умолчанию.

Программными средствами обнаруживать расположение профиля пользователя, выполните одно из следующих действий.

- Использование профилей пользователей SharePoint API. Мы рекомендуем этот подход, так как это работает во всех сценариях. 
- С помощью Microsoft Graph. Это работает для пользователей, имеющих личные сайты, но не для пользователей, у которых нет личных сайтов.

### <a name="use-the-sharepoint-user-profile-api-to-detect-the-profile-location"></a>Использование API профилей пользователей SharePoint для определения расположения профилей
Можно вызвать API профилей пользователей SharePoint с помощью REST или CSOM, чтобы получить URL-адрес узла личного сайта для указанной учетной записи. Этот URL-адрес содержит размещения личного сайта для личного сайта пользователя, независимо от того, создан ли личного сайта. В следующем примере показано вызова REST.

```
GET https://contoso.sharepoint.com/_api/SP.UserProfiles.PeopleManager/GetPropertiesFor(accountName=@v)/personalsitehosturl?%40v=%27i%3A0%23.f%7Cmembership%7Cbert%40contoso.onmicrosoft.com%27
```

Если вы используете C#, CSOM, как показано в следующем примере, простой в использовании.

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

При наличии URL-адрес узла личного сайта, который можно использовать для получения URL-адрес сайта администрирования клиента для географического расположения, на котором размещается в профиле пользователя наряду со сведениями о [несколькими географически обнаружения](multigeo-discovery.md) .

Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

### <a name="use-microsoft-graph-to-detect-the-users-personal-site-url"></a>Использование Microsoft Graph для определения URL-адреса личного сайта пользователя
Для обнаружения URL-адреса личного сайта пользователя в географически нескольких клиентов, можно использовать при следующем вызове Microsoft Graph:

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=mySite
```

При наличии URL-адрес узла личного сайта, который можно использовать для получения URL-адрес сайта администрирования клиента для географического расположения, на котором размещается в профиле пользователя наряду со сведениями о [несколькими географически обнаружения](multigeo-discovery.md) .

> [!NOTE] 
> Если у пользователя нет личного сайта, этот способ не работает. Вместо этого следует использовать API профилей пользователей SharePoint.

Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

## <a name="updating-user-profile-properties"></a>Обновление свойств профиля пользователя
Предоставление доступа к массового обновления для свойств профилей пользователей — это распространенные сценарии для предприятий. Процесса для использования в зависимости от типа свойства профиля пользователя, который требуется обновить.

### <a name="updating-default-user-profile-properties"></a>Обновление свойств профиля пользователя по умолчанию
Некоторых свойств профиля пользователя, которые доступны по умолчанию; например **отдел**, **AboutMe**и **PreferredDataLocation**. Мы рекомендуем использовать Microsoft Graph API обновляет эти свойства, так как Microsoft Graph принять во внимание географически. Следующем примере показано, как обновить свойство **AboutMe** для bert@contoso.onmicrosoft.com пользователя.

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=aboutme
```

Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

#### <a name="updating-the-preferred-data-location-property"></a>Обновление свойства расположение предпочитаемый данных
Расположение предпочитаемый данных пользователя (свойство**preferredDataLocation** ) указывает расположение предпочитаемый географически для пользователя. Это влияет на следующие:

- Географического расположения, где был подготовлен личного сайта пользователя
- Географически расположение, где создаются сайты группы пользователя 

Так как расположение предпочитаемый данных является свойством по умолчанию, мы рекомендуем использовать Microsoft Graph API для настройки, как показано в следующем примере. 

```
GET https://graph.microsoft.com/v1.0/users/bert@contoso.onmicrosoft.com?$select=preferredDataLocation

PATCH https://graph.microsoft.com/beta/users/bert@contoso.onmicrosoft.com

JSON payload:
{
    "preferredDataLocation" : "eur"
}

```

Для получения дополнительных сведений см [MultiGeo.UserPreferredDataLocation](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserPreferredDataLocation) .

### <a name="custom-sharepoint-user-profile-properties"></a>Настраиваемые свойства профилей пользователей SharePoint
Свойства профиля пользователя конкретной компании можно добавить к профилям пользователей в SharePoint. Для клиентов SharePoint несколькими-географически следующие соображения.

- Свойства профиля пользователя создаются на уровне географического расположения. Это свойство недоступен в в других местах, географически при создании свойства в расположение географически Европе. Рекомендуется создание настраиваемого пользовательского свойства профиля в все географического расположения. Это снижает вероятность, что данные будут потеряны при перемещении пользователей в географически подразделениях.
- Необходимо прочитать и обновление свойств профиля пользователя на уровне географического расположения. При создании настраиваемых свойств в все географического расположения, необходимо итерации по географического расположения и обновите свойство для всех пользователей.

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

Для получения дополнительных сведений см [MultiGeo.UserProfileUpdates](https://github.com/SharePoint/PnP/tree/dev/Samples/MultiGeo.UserProfileUpdates) .

### <a name="using-the-bulk-user-profile-update-api"></a>С помощью массового обновления профиля пользователя API
[Профиль пользователя массового обновления API](https://msdn.microsoft.com/en-us/pnp_articles/bulk-user-profile-update-api-for-sharepoint-online) можно использовать для выполнения массового обновления настраиваемых свойств профиля в географически нескольких клиентов. Обратите внимание на следующее:

- Этот интерфейс API работает на уровне географического расположения и не Multi-географически принять во внимание. К примеру при использовании API в расположении географически Европа обновляются только учетные записи в Европе.
- При указании Импорт файла с учетными записями в разных географического расположения, API будет обновлять только свойства для пользователей в эту папку географически.


## <a name="see-also"></a>См. также

- [Общие сведения об API для массового обновления настраиваемых свойств профиля для SharePoint Online](bulk-user-profile-update-api-for-sharepoint-online.md)
- [Пример API пакета обновления профиля пользователя](https://github.com/SharePoint/PnP/tree/master/Samples/UserProfile.BatchUpdate.API)


