---
title: "Настраивать несколькими географически примера приложения"
ms.date: 11/03/2017
ms.openlocfilehash: 5974998440e13f99fb7b025d1dcd70d84c2edd06
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="set-up-your-multi-geo-sample-applications"></a>Настраивать несколькими географически примера приложения

> **Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.

При разработке для клиента несколькими географически важно понять модель безопасности и к счастью используется модель для клиента несколькими географически не отличаются в зависимости от модели, используемые для регулярного клиента. В этой статье показано, как настроить примеров приложений.

## <a name="my-application-needs-to-be-able-to-readupdate-profiles-for-all-users"></a>Мое приложение должно иметь возможность чтения или изменение профилей для всех пользователей
### <a name="im-using-the-microsoft-graph-api"></a>Я использую Microsoft Graph API
Как описано в статье [Профилей взаимодействие с пользователем несколькими географически](multigeo-userprofileexperience.md) предпочитаемый модели для чтения или изменение свойств профилей пользователей — с помощью API графике. В этой главе объясняется, какие разрешения необходимо предоставить в приложение для реализации операций чтения профиля пользователя широкий клиента и обновлений. Существует [длинный список возможных разрешений](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) можно предоставить приложение, определенных в Azure AD, что для управления профилями можно ограничить разрешения для:

|**Разрешение**|**Тип**|**Описание**| **Необходимые разрешения администратора**
|:-----|:-----|:-----|:-----|
|**[User.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)** | Разрешение приложения | Приложение сможет просматривать и записывать полный набор свойств профиля, данные о членстве в группах, сведения о подчиненных и руководителях других пользователей в организации без входа пользователя.  Также позволяет приложения для создания и удаления пользователей без прав администратора. Не разрешать сброс паролей пользователей. | Да
|**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)** | Разрешение приложения | Позволяет приложениям чтения и записи документов и элементов списка всех семейств веб-сайтов не выполнен вход пользователя. Это разрешение — это требуется только в том случае, когда приложение будет извлечение расположения личного сайта пользователя (например выберите https://graph.microsoft.com/v1.0/users/UserB@contoso.onmicrosoft.com?$ = mySite) | Да

Microsoft Graph, на основе нескольких географически примеры с помощью библиотеки проверки подлинности Microsoft (MSAL) с помощью Microsoft Graph на конечной версии 2. По сравнению с ADAL, который подключается с помощью конечной версии 1, MSAL позволяет подключения к Microsoft Graph с учетными записями Microsoft, Azure AD и Azure AD B2C. Ниже инструкциям поможет вам программы установки приложения для конечной версии 2, но вы также можете использовать «предыдущий» подход, на основе в конечных точках v1.

#### <a name="register-your-application"></a>Регистрация приложения
Чтобы использовать разрешения приложения Microsoft Graph, сначала необходимо зарегистрировать приложение. Для этого в https://apps.dev.microsoft.com. После входа нажмите кнопку добавьте новое приложение Converged, нажав кнопку Добавить приложение

![Регистрация приложения в Azure AD](media/multigeo/multigeopermissions_registerapp1.png)

Имя приложения и нажмите Создать приложение.

На экране настройки приложения настройте следующие параметры.
- Создать пароль и запишите его вместе с идентификатором приложения
- Нажмите кнопку «Добавить платформа» и выберите «Собственные приложения» в качестве целевой платформы как приложение не имеет целевая страница
- Добавьте нужные разрешения приложения. В этом примере приложения добавлена разрешения приложения User.ReadWrite.All и Sites.ReadWrite.All.
- Убедитесь, что снимите флажок «Пакет SDK Live для поддержки»
- Один раз настроены сохранить изменения.

![Настройка приложения в Azure AD, часть 1](media/multigeo/multigeopermissions_registerapp2.png)

![Настройка приложения в Azure AD часть 2](media/multigeo/multigeopermissions_registerapp3.png)


#### <a name="consent-to-the-application"></a>Разрешения для приложения
Этот пример User.ReadWrite.All и разрешения приложений, Sites.ReadWrite.All требуются разрешения администратора в клиент перед его можно использовать. Создайте URL-адрес согласия следующим образом:

```
https://login.microsoftonline.com/<tenant>/adminconsent?client_id=<clientid>&state=<something>
```

Использование идентификатор клиента из приложения зарегистрирован и соглашаетесь приложения из моих contoso.onmicrosoft.com клиента, URL-адрес выглядит следующим образом:

```
https://login.microsoftonline.com/contoso.onmicrosoft.com/adminconsent?client_id=6e4433ca-7011-4a11-85b6-1195b0114fea&state=12345
```

Просмотра для созданного URL-адреса и вход как администратор клиента и разрешения для приложения. Вы видите на экране подтверждения показывать имя приложения, а также области разрешений, которые вы настроили.

![Согласие клиента для приложения Azure AD](media/multigeo/multigeopermissions_registerapp4.png)

### <a name="im-using-the-csom-user-profile-api"></a>Я использую API профиля пользователя CSOM
Если с помощью CSOM API для управления свойствами профилей, вы сможете только сделать это для настраиваемых свойств созданного со времени ожидания введите свойства — это лучше обрабатывается с помощью Microsoft Graph API... в статье [Профиля несколькими географически пользовательского интерфейса](multigeo-userprofileexperience.md) для получения дополнительных сведений Подробные сведения. С точки зрения разрешений есть два режима:

#### <a name="using-user-credentials"></a>С помощью учетных данных пользователя
Это нуждается в настройке `ClientContext` объектов с помощью URL-адрес администрирования клиента и учетные данные администратора SharePoint Online. Поскольку существует только один экземпляр Azure AD, удерживая пользователей это также означает, что SharePoint Online администрирования является администратора все географического расположения.

```C#
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";

using (ClientContext cc = new ClientContext(tenantAdminSiteForMyGeoLocation))
{
    SecureString securePassword = GetSecurePassword("password");
    cc.Credentials = new SharePointOnlineCredentials("admin@contoso.onmicrosoft.com", securePassword);
    
    // user profile logic
}

static SecureString GetSecurePassword(string Password)
{
    SecureString sPassword = new SecureString();
    foreach (char c in Password.ToCharArray()) sPassword.AppendChar(c);
    return sPassword;
}
```

#### <a name="using-an-app-only-principal"></a>С помощью субъект только для приложений
При использовании только приложения вам потребуется предоставить участника созданное приложение **Полный доступ** для области разрешений [http://sharepoint/social/tenant](https://dev.office.com/sharepoint/docs/general-development/get-started-developing-with-social-features-in-sharepoint#bkmk_AppPerms) . Ниже инструкциям показано использование appregnew.aspx и appinv.aspx для зарегистрировать субъект приложения и соглашаетесь его.

##### <a name="create-the-principal"></a>Создание участника
Перейдите на сайт вашего клиента (например, https://contoso.sharepoint.com), а затем вызвать страницы appregnew.aspx (например, https://contoso.sharepoint.com/_layouts/15/appregnew.aspx). В этой страницы нажмите кнопку на кнопку Создать, чтобы создать идентификатор клиента и секрет клиента и заполнить остальные сведения, как показано в-снимке экрана ниже.

![Зарегистрируйте участника приложения ACS](media/multigeo/multigeopermissions_registerprincipal1.png)

> **Важные** Хранятся полученные данные (идентификатор клиента и секрет клиента), так как это понадобится на следующем этапе!

##### <a name="grant-permissions-to-the-created-principal"></a>Предоставление разрешений для созданного участника
Следующим шагом предоставление разрешений для только что созданный субъекта. Поскольку мы требуется предоставить разрешения клиентов с областью действия в этом предоставление может выполняться только через appinv.aspx страницу на сайте администрирования клиентов. Можно получить доступ к этой сайта с помощью https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx. После загрузки страницы добавьте идентификатором клиента и найти созданный участника:

![Предоставление разрешений для участника приложения](media/multigeo/multigeopermissions_registerprincipal2.png)

Для предоставления разрешений необходимо предоставить разрешение на XML, описывающий необходимые разрешения. Поскольку пользовательский Интерфейс взаимодействия сканера необходимо получить доступ ко всем сайтам + также использует поиска с помощью только приложения требуется перечисленных ниже разрешений:

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="FullControl" />
</AppPermissionRequests>
```

При нажатии кнопки на создание появится диалоговое окно подтверждения разрешений. Клавиши, доверие для предоставления разрешений:

![Разрешения субъекта приложения](media/multigeo/multigeopermissions_registerprincipal3.png)


##### <a name="use-the-principal-in-your-code"></a>Использование субъекта в коде
После субъекта создается и согласие для запроса доступа можно использовать идентификатор и секрет участника. `TokenHelper.cs` Класс будет скопировать идентификатор и секрет из файла конфигурации приложения.

```C#
string tenantAdminSiteForMyGeoLocation = "https://contoso-europe-admin.sharepoint.com";

//Get the realm for the URL
string realm = TokenHelper.GetRealmFromTargetUrl(siteUri);

//Get the access token for the URL.  
string accessToken = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, siteUri.Authority, realm).AccessToken;

//Create a client context object based on the retrieved access token
using (ClientContext cc = TokenHelper.GetClientContextWithAccessToken(tenantAdminSiteForMyGeoLocation, accessToken))
{
    // user profile logic
}
```

Пример app.config выглядит следующим образом:

```XML
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <!-- Use AppRegNew.aspx and AppInv.aspx to register client id with proper secret -->
    <add key="ClientId" value="[Your Client ID]" />
    <add key="ClientSecret" value="[Your Client Secret]" />
  </appSettings>
</configuration>
```


> [!NOTE] 
> Можно легко вставить `TokenHelper.cs` в проекте, добавив пакет **AppForSharePointOnlineWebToolkit** nuget для решения.

## <a name="my-application-needs-to-be-able-to-be-able-to-discover-the-multi-geo-configuration"></a>Мои приложение должно иметь возможность обнаруживать несколькими географически конфигурации
### <a name="im-using-the-microsoft-graph-api"></a>Я использую Microsoft Graph API
Только поддерживаемые API обнаружения географического расположения в географически нескольких клиентов — это с помощью API графике. В этой главе объясняется, какие разрешения необходимо предоставить в приложение для получения сведений о нескольких географически. Существует [длинный список возможных разрешений](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) можно предоставить приложение, определенных в Azure AD, что для чтения сведений о конфигурации клиента несколькими географически можно ограничить разрешения для:

|**Разрешение**|**Тип**|**Описание**| **Необходимые разрешения администратора**
|:-----|:-----|:-----|:-----|
|**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)** | Разрешение приложения | Позволяет приложениям чтения и записи документов и элементов списка всех семейств веб-сайтов не выполнен вход пользователя. | Да

Используйте этапы создания приложения Azure AD, как описано в главе «Мое приложение должно иметь возможность чтения или изменение профилей для всех пользователей».

## <a name="my-application-needs-to-be-able-to-createdelete-sites-collections-or-set-tenant-site-collection-properties"></a>Мое приложение необходимо иметь возможность создание и удаление семейства веб-сайтов или задать свойства семейства сайтов клиента
### <a name="im-using-the-microsoft-graph-api"></a>Я использую Microsoft Graph API
[Географическая ферма с несколькими сайтами](multigeo-sites.md) содержатся дополнительные сведения о том, как создавать сайты группы (или «Современный» сайты рабочих групп) с помощью Microsoft Graph API, в этом разделе мы только адресации разрешения. Приведенной ниже таблице перечислены необходимые разрешения

|**Разрешение**|**Тип**|**Описание**| **Необходимые разрешения администратора**
|:-----|:-----|:-----|:-----|
|**[Group.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#group-permissions)** | Разрешение приложения | Позволяет приложениям создавать группы, чтение и обновить членство в группах и удаление групп. Все эти операции могут выполняться с приложения без пользователь выполнил вход. Обратите внимание на то, что не все группы API поддерживает доступ с помощью разрешений только для приложений. | Да

Microsoft Graph, на основе нескольких географически примеры с помощью библиотеки проверки подлинности Microsoft (MSAL) с помощью Microsoft Graph на конечной версии 2. По сравнению с ADAL, который подключается с помощью конечной версии 1, MSAL позволяет подключения к Microsoft Graph с учетными записями Microsoft, Azure AD и Azure AD B2C. Используйте этапы создания приложения Azure AD, как описано в главе «Мое приложение должно иметь возможность чтения или изменение профилей для всех пользователей».

### <a name="im-using-the-csom-tenant-api"></a>Я использую API клиента CSOM
С помощью API клиента CSOM очень похож на уже было сказано CSOM руководства, в течение нескольких фактов идентичен рекомендации по использованию учетных данных пользователя. Для использования только субъект инструкциям такие же, но вам потребуется предоставить разные разрешения (клиент, полный доступ):

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```

## <a name="resources"></a>Resources
Под списком ресурсов полезны, если также дополнительные сведения о Microsoft Graph API и CSOM API:
- [Центр разработчиков Microsoft Graph](https://developer.microsoft.com/en-us/graph)
- [Получение маркера доступа для вызова API график](https://developer.microsoft.com/en-us/graph/docs/concepts/auth_overview)
- [Документация по Microsoft Graph](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [Графическое представление проводника](https://developer.microsoft.com/en-us/graph/graph-explorer)
- [Права только для приложений и с повышенными привилегиями в объектная модель SharePoint](app-only-elevated-privileges-sharepoint-add-in.md)
