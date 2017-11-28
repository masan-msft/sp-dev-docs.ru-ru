---
title: "Настраивать несколькими географически примера приложения"
ms.date: 11/03/2017
ms.openlocfilehash: 3151ffe7353aff021bc4a4113f0738ec7f21d5ee
ms.sourcegitcommit: 26a4fb9cfe1ffcd266313c16f2afabfc841fdb71
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2017
---
# <a name="set-up-your-multi-geo-sample-applications"></a><span data-ttu-id="30a27-102">Настраивать несколькими географически примера приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-102">Set up your Multi-Geo sample applications</span></span>

> <span data-ttu-id="30a27-103">**Важные:** OneDrive и SharePoint Online Multi-Geo в данный момент в предварительной версии и может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="30a27-103">**Important:** OneDrive and SharePoint Online Multi-Geo is currently in preview and is subject to change.</span></span>

<span data-ttu-id="30a27-104">При разработке для клиента несколькими географически важно понять модель безопасности и к счастью используется модель для клиента несколькими географически не отличаются в зависимости от модели, используемые для регулярного клиента.</span><span class="sxs-lookup"><span data-stu-id="30a27-104">When developing for a Multi-Geo tenant it's important to understand the security model and luckily the used model for a Multi-Geo tenant does not differ from the model used for a regular tenant.</span></span> <span data-ttu-id="30a27-105">В этой статье показано, как настроить примеров приложений.</span><span class="sxs-lookup"><span data-stu-id="30a27-105">This article shows you how to configure the sample applications.</span></span>

## <a name="my-application-needs-to-be-able-to-readupdate-profiles-for-all-users"></a><span data-ttu-id="30a27-106">Мое приложение должно иметь возможность чтения или изменение профилей для всех пользователей</span><span class="sxs-lookup"><span data-stu-id="30a27-106">My application needs to be able to read/update profiles for all users</span></span>
### <a name="im-using-the-microsoft-graph-api"></a><span data-ttu-id="30a27-107">Я использую Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="30a27-107">I'm using the Microsoft Graph API</span></span>
<span data-ttu-id="30a27-108">Как описано в статье [Профилей взаимодействие с пользователем несколькими географически](multigeo-userprofileexperience.md) предпочитаемый модели для чтения или изменение свойств профилей пользователей — с помощью API графике.</span><span class="sxs-lookup"><span data-stu-id="30a27-108">As explained in the [Multi-geo User Profile Experience](multigeo-userprofileexperience.md) article the preferred model to read/update user profile properties is by using the Graph API.</span></span> <span data-ttu-id="30a27-109">В этой главе объясняется, какие разрешения необходимо предоставить в приложение для реализации операций чтения профиля пользователя широкий клиента и обновлений.</span><span class="sxs-lookup"><span data-stu-id="30a27-109">This chapter explains which permissions you'll need to grant to your application to realize tenant wide user profile reads and updates.</span></span> <span data-ttu-id="30a27-110">Существует [длинный список возможных разрешений](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) можно предоставить приложение, определенных в Azure AD, что для управления профилями можно ограничить разрешения для:</span><span class="sxs-lookup"><span data-stu-id="30a27-110">There [a long list of possible permissions](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) that you can grant to an application defined in Azure AD, but for manipulating profiles you can limit permissions to:</span></span>

|<span data-ttu-id="30a27-111">**Разрешение**</span><span class="sxs-lookup"><span data-stu-id="30a27-111">**Permission**</span></span>|<span data-ttu-id="30a27-112">**Тип**</span><span class="sxs-lookup"><span data-stu-id="30a27-112">**Type**</span></span>|<span data-ttu-id="30a27-113">**Описание**</span><span class="sxs-lookup"><span data-stu-id="30a27-113">**Description**</span></span>| <span data-ttu-id="30a27-114">**Необходимые разрешения администратора**</span><span class="sxs-lookup"><span data-stu-id="30a27-114">**Admin consent needed**</span></span>
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="30a27-115">**[User.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span><span class="sxs-lookup"><span data-stu-id="30a27-115">**[User.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span></span> | <span data-ttu-id="30a27-116">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-116">Application permission</span></span> | <span data-ttu-id="30a27-117">Приложение сможет просматривать и записывать полный набор свойств профиля, данные о членстве в группах, сведения о подчиненных и руководителях других пользователей в организации без входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="30a27-117">Allows the app to read and write the full set of profile properties, group membership, reports and managers of other users in your organization, without a signed-in user.</span></span>  <span data-ttu-id="30a27-118">Также позволяет приложения для создания и удаления пользователей без прав администратора.</span><span class="sxs-lookup"><span data-stu-id="30a27-118">Also allows the app to create and delete non-administrative users.</span></span> <span data-ttu-id="30a27-119">Не разрешать сброс паролей пользователей.</span><span class="sxs-lookup"><span data-stu-id="30a27-119">Does not allow reset of user passwords.</span></span> | <span data-ttu-id="30a27-120">Да</span><span class="sxs-lookup"><span data-stu-id="30a27-120">Yes</span></span>
|<span data-ttu-id="30a27-121">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span><span class="sxs-lookup"><span data-stu-id="30a27-121">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span></span> | <span data-ttu-id="30a27-122">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-122">Application permission</span></span> | <span data-ttu-id="30a27-123">Позволяет приложениям чтения и записи документов и элементов списка всех семейств веб-сайтов не выполнен вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="30a27-123">Allows the app to read/write documents and list items in all site collections without a signed in user.</span></span> <span data-ttu-id="30a27-124">Это разрешение — это требуется только в том случае, когда приложение будет извлечение расположения личного сайта пользователя (например выберите https://graph.microsoft.com/v1.0/users/UserB@contoso.onmicrosoft.com?$ = mySite)</span><span class="sxs-lookup"><span data-stu-id="30a27-124">This permission is only needed if the application will be retrieving the user's personal site location (e.g. https://graph.microsoft.com/v1.0/users/UserB@contoso.onmicrosoft.com?$select=mySite)</span></span> | <span data-ttu-id="30a27-125">Да</span><span class="sxs-lookup"><span data-stu-id="30a27-125">Yes</span></span>

<span data-ttu-id="30a27-126">Microsoft Graph, на основе нескольких географически примеры с помощью библиотеки проверки подлинности Microsoft (MSAL) с помощью Microsoft Graph на конечной версии 2.</span><span class="sxs-lookup"><span data-stu-id="30a27-126">The Microsoft Graph based Multi-Geo samples are using the Microsoft Authentication Library (MSAL) to connect with the Microsoft Graph on the v2 endpoint.</span></span> <span data-ttu-id="30a27-127">По сравнению с ADAL, который подключается с помощью конечной версии 1, MSAL позволяет подключения к Microsoft Graph с учетными записями Microsoft, Azure AD и Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="30a27-127">Compared to ADAL which connects using the v1 endpoint, MSAL allows connection to the Microsoft Graph with Microsoft Accounts, Azure AD and Azure AD B2C.</span></span> <span data-ttu-id="30a27-128">Ниже инструкциям поможет вам программы установки приложения для конечной версии 2, но вы также можете использовать «предыдущий» подход, на основе в конечных точках v1.</span><span class="sxs-lookup"><span data-stu-id="30a27-128">Below instructions will help you setup your application for the v2 endpoint, but you can also use the "older" approach based on the v1 endpoints.</span></span>

#### <a name="register-your-application"></a><span data-ttu-id="30a27-129">Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-129">Register your application</span></span>
<span data-ttu-id="30a27-130">Чтобы использовать разрешения приложения Microsoft Graph, сначала необходимо зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="30a27-130">To use application permissions against the Microsoft Graph you first have to register your application.</span></span> <span data-ttu-id="30a27-131">Для этого в https://apps.dev.microsoft.com. После входа нажмите кнопку добавьте новое приложение Converged, нажав кнопку Добавить приложение</span><span class="sxs-lookup"><span data-stu-id="30a27-131">You do this at https://apps.dev.microsoft.com. Once logged in click add a new Converged application, by clicking Add an app</span></span>

![Регистрация приложения в Azure AD](media/multigeo/multigeopermissions_registerapp1.png)

<span data-ttu-id="30a27-133">Имя приложения и нажмите Создать приложение.</span><span class="sxs-lookup"><span data-stu-id="30a27-133">Give your application a name and hit Create application.</span></span>

<span data-ttu-id="30a27-134">На экране настройки приложения настройте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="30a27-134">In the application configuration screen configure the following:</span></span>
- <span data-ttu-id="30a27-135">Создать пароль и запишите его вместе с идентификатором приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-135">Generate a password and make a note of it together with the application id</span></span>
- <span data-ttu-id="30a27-136">Нажмите кнопку «Добавить платформа» и выберите «Собственные приложения» в качестве целевой платформы как приложение не имеет целевая страница</span><span class="sxs-lookup"><span data-stu-id="30a27-136">Click 'Add Platform' and select "Native application" as the platform target as the application does not have a landing page</span></span>
- <span data-ttu-id="30a27-137">Добавьте нужные разрешения приложения.</span><span class="sxs-lookup"><span data-stu-id="30a27-137">Add the necessary Application Permission.</span></span> <span data-ttu-id="30a27-138">В этом примере приложения добавлена разрешения приложения User.ReadWrite.All и Sites.ReadWrite.All.</span><span class="sxs-lookup"><span data-stu-id="30a27-138">In this sample app we have added the User.ReadWrite.All and Sites.ReadWrite.All application permissions.</span></span>
- <span data-ttu-id="30a27-139">Убедитесь, что снимите флажок «Пакет SDK Live для поддержки»</span><span class="sxs-lookup"><span data-stu-id="30a27-139">Make sure to uncheck 'Live SDK support'</span></span>
- <span data-ttu-id="30a27-140">Один раз настроены сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="30a27-140">Once configured save your changes.</span></span>

![Настройка приложения в Azure AD, часть 1](media/multigeo/multigeopermissions_registerapp2.png)

![Настройка приложения в Azure AD часть 2](media/multigeo/multigeopermissions_registerapp3.png)


#### <a name="consent-to-the-application"></a><span data-ttu-id="30a27-143">Разрешения для приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-143">Consent to the application</span></span>
<span data-ttu-id="30a27-144">Этот пример User.ReadWrite.All и разрешения приложений, Sites.ReadWrite.All требуются разрешения администратора в клиент перед его можно использовать.</span><span class="sxs-lookup"><span data-stu-id="30a27-144">In this sample the User.ReadWrite.All and Sites.ReadWrite.All application permissions require admin consent in a tenant before it can be used.</span></span> <span data-ttu-id="30a27-145">Создайте URL-адрес согласия следующим образом:</span><span class="sxs-lookup"><span data-stu-id="30a27-145">Create a consent URL like the following:</span></span>

```
https://login.microsoftonline.com/<tenant>/adminconsent?client_id=<clientid>&state=<something>
```

<span data-ttu-id="30a27-146">Использование идентификатор клиента из приложения зарегистрирован и соглашаетесь приложения из моих contoso.onmicrosoft.com клиента, URL-адрес выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="30a27-146">Using the client id from the app registered and consenting to the app from my tenant contoso.onmicrosoft.com, the URL looks like this:</span></span>

```
https://login.microsoftonline.com/contoso.onmicrosoft.com/adminconsent?client_id=6e4433ca-7011-4a11-85b6-1195b0114fea&state=12345
```

<span data-ttu-id="30a27-147">Просмотра для созданного URL-адреса и вход как администратор клиента и разрешения для приложения.</span><span class="sxs-lookup"><span data-stu-id="30a27-147">Browsing to the created URL and log in as a tenant admin, and consent to the application.</span></span> <span data-ttu-id="30a27-148">Вы видите на экране подтверждения показывать имя приложения, а также области разрешений, которые вы настроили.</span><span class="sxs-lookup"><span data-stu-id="30a27-148">You can see the consent screen show the name of your application as well as the permission scopes you configured.</span></span>

![Согласие клиента для приложения Azure AD](media/multigeo/multigeopermissions_registerapp4.png)

### <a name="im-using-the-csom-user-profile-api"></a><span data-ttu-id="30a27-150">Я использую API профиля пользователя CSOM</span><span class="sxs-lookup"><span data-stu-id="30a27-150">I'm using the CSOM User Profile API</span></span>
<span data-ttu-id="30a27-151">Если с помощью CSOM API для управления свойствами профилей, вы сможете только сделать это для настраиваемых свойств созданного со времени ожидания введите свойства — это лучше обрабатывается с помощью Microsoft Graph API... в статье [Профиля несколькими географически пользовательского интерфейса](multigeo-userprofileexperience.md) для получения дополнительных сведений Подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="30a27-151">When using the CSOM API to manipulate profile properties you'll only do this for the custom created properties since out-of-the-box properties are better handled via the Microsoft Graph API...see the [Multi-geo User Profile Experience](multigeo-userprofileexperience.md) article for more details.</span></span> <span data-ttu-id="30a27-152">С точки зрения разрешений есть два режима:</span><span class="sxs-lookup"><span data-stu-id="30a27-152">From a permission point of view there's two modes:</span></span>

#### <a name="using-user-credentials"></a><span data-ttu-id="30a27-153">С помощью учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="30a27-153">Using user credentials</span></span>
<span data-ttu-id="30a27-154">Это нуждается в настройке `ClientContext` объектов с помощью URL-адрес администрирования клиента и учетные данные администратора SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="30a27-154">This requires setting up a `ClientContext` object using the tenant admin url and using SharePoint Online admin credentials.</span></span> <span data-ttu-id="30a27-155">Поскольку существует только один экземпляр Azure AD, удерживая пользователей это также означает, что SharePoint Online администрирования является администратора все географического расположения.</span><span class="sxs-lookup"><span data-stu-id="30a27-155">Since there's only one Azure AD instance holding users this also implies that a SharePoint Online admin is admin for all the geo locations.</span></span>

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

#### <a name="using-an-app-only-principal"></a><span data-ttu-id="30a27-156">С помощью субъект только для приложений</span><span class="sxs-lookup"><span data-stu-id="30a27-156">Using an app-only principal</span></span>
<span data-ttu-id="30a27-157">При использовании только приложения вам потребуется предоставить участника созданное приложение **Полный доступ** для области разрешений [http://sharepoint/social/tenant](https://dev.office.com/sharepoint/docs/general-development/get-started-developing-with-social-features-in-sharepoint#bkmk_AppPerms) .</span><span class="sxs-lookup"><span data-stu-id="30a27-157">When using app-only you'll need to grant the created app principal **full control** for the [http://sharepoint/social/tenant](https://dev.office.com/sharepoint/docs/general-development/get-started-developing-with-social-features-in-sharepoint#bkmk_AppPerms) permission scope.</span></span> <span data-ttu-id="30a27-158">Ниже инструкциям показано использование appregnew.aspx и appinv.aspx для зарегистрировать субъект приложения и соглашаетесь его.</span><span class="sxs-lookup"><span data-stu-id="30a27-158">Below instructions show you to use appregnew.aspx and appinv.aspx to register an app principal and consent it.</span></span>

##### <a name="create-the-principal"></a><span data-ttu-id="30a27-159">Создание участника</span><span class="sxs-lookup"><span data-stu-id="30a27-159">Create the principal</span></span>
<span data-ttu-id="30a27-160">Перейдите на сайт вашего клиента (например, https://contoso.sharepoint.com), а затем вызвать страницы appregnew.aspx (например, https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span><span class="sxs-lookup"><span data-stu-id="30a27-160">Navigate to a site in your tenant (e.g. https://contoso.sharepoint.com) and then call the appregnew.aspx page (e.g. https://contoso.sharepoint.com/_layouts/15/appregnew.aspx).</span></span> <span data-ttu-id="30a27-161">В этой страницы нажмите кнопку на кнопку Создать, чтобы создать идентификатор клиента и секрет клиента и заполнить остальные сведения, как показано в-снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="30a27-161">In this page click on the Generate button to generate a client id and client secret and fill the remaining information like shown in the screen-shot below.</span></span>

![Зарегистрируйте участника приложения ACS](media/multigeo/multigeopermissions_registerprincipal1.png)

> <span data-ttu-id="30a27-163">**Важные** Хранятся полученные данные (идентификатор клиента и секрет клиента), так как это понадобится на следующем этапе!</span><span class="sxs-lookup"><span data-stu-id="30a27-163">**Important** Store the retrieved information (client id and client secret) since you'll need this in the next step!</span></span>

##### <a name="grant-permissions-to-the-created-principal"></a><span data-ttu-id="30a27-164">Предоставление разрешений для созданного участника</span><span class="sxs-lookup"><span data-stu-id="30a27-164">Grant permissions to the created principal</span></span>
<span data-ttu-id="30a27-165">Следующим шагом предоставление разрешений для только что созданный субъекта.</span><span class="sxs-lookup"><span data-stu-id="30a27-165">Next step is granting permissions to the newly created principal.</span></span> <span data-ttu-id="30a27-166">Поскольку мы требуется предоставить разрешения клиентов с областью действия в этом предоставление может выполняться только через appinv.aspx страницу на сайте администрирования клиентов.</span><span class="sxs-lookup"><span data-stu-id="30a27-166">Since we're granting tenant scoped permissions this granting can only be done via the appinv.aspx page on the tenant administration site.</span></span> <span data-ttu-id="30a27-167">Можно получить доступ к этой сайта с помощью https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx.</span><span class="sxs-lookup"><span data-stu-id="30a27-167">You can reach this site via https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx.</span></span> <span data-ttu-id="30a27-168">После загрузки страницы добавьте идентификатором клиента и найти созданный участника:</span><span class="sxs-lookup"><span data-stu-id="30a27-168">Once the page is loaded add your client id and look up the created principal:</span></span>

![Предоставление разрешений для участника приложения](media/multigeo/multigeopermissions_registerprincipal2.png)

<span data-ttu-id="30a27-170">Для предоставления разрешений необходимо предоставить разрешение на XML, описывающий необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="30a27-170">In order to grant permissions you'll need to provide the permission XML that describes the needed permissions.</span></span> <span data-ttu-id="30a27-171">Поскольку пользовательский Интерфейс взаимодействия сканера необходимо получить доступ ко всем сайтам + также использует поиска с помощью только приложения требуется перечисленных ниже разрешений:</span><span class="sxs-lookup"><span data-stu-id="30a27-171">Since the UI experience scanner needs to be able to access all sites + also uses search with app-only it requires below permissions:</span></span>

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/social/tenant" Right="FullControl" />
</AppPermissionRequests>
```

<span data-ttu-id="30a27-172">При нажатии кнопки на создание появится диалоговое окно подтверждения разрешений.</span><span class="sxs-lookup"><span data-stu-id="30a27-172">When you click on Create you'll be presented with a permission consent dialog.</span></span> <span data-ttu-id="30a27-173">Клавиши, доверие для предоставления разрешений:</span><span class="sxs-lookup"><span data-stu-id="30a27-173">Press Trust It to grant the permissions:</span></span>

![Разрешения субъекта приложения](media/multigeo/multigeopermissions_registerprincipal3.png)


##### <a name="use-the-principal-in-your-code"></a><span data-ttu-id="30a27-175">Использование субъекта в коде</span><span class="sxs-lookup"><span data-stu-id="30a27-175">Use the principal in your code</span></span>
<span data-ttu-id="30a27-176">После субъекта создается и согласие для запроса доступа можно использовать идентификатор и секрет участника.</span><span class="sxs-lookup"><span data-stu-id="30a27-176">Once the principal is created and consented you can use the principal's id and secret to request an access.</span></span> <span data-ttu-id="30a27-177">`TokenHelper.cs` Класс будет скопировать идентификатор и секрет из файла конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="30a27-177">The `TokenHelper.cs` class will grab the id and secret from the application's configuration file.</span></span>

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

<span data-ttu-id="30a27-178">Пример app.config выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="30a27-178">A sample app.config looks like this:</span></span>

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


><span data-ttu-id="30a27-179">**Примечание:** Можно легко вставить `TokenHelper.cs` в проекте, добавив пакет **AppForSharePointOnlineWebToolkit** nuget для решения.</span><span class="sxs-lookup"><span data-stu-id="30a27-179">**Note:** You can easily insert the `TokenHelper.cs` class in your project by adding the **AppForSharePointOnlineWebToolkit** nuget package to your solution.</span></span>

## <a name="my-application-needs-to-be-able-to-be-able-to-discover-the-multi-geo-configuration"></a><span data-ttu-id="30a27-180">Мои приложение должно иметь возможность обнаруживать несколькими географически конфигурации</span><span class="sxs-lookup"><span data-stu-id="30a27-180">My application needs to be able to be able to discover the Multi-Geo configuration</span></span>
### <a name="im-using-the-microsoft-graph-api"></a><span data-ttu-id="30a27-181">Я использую Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="30a27-181">I'm using the Microsoft Graph API</span></span>
<span data-ttu-id="30a27-182">Только поддерживаемые API обнаружения географического расположения в географически нескольких клиентов — это с помощью API графике.</span><span class="sxs-lookup"><span data-stu-id="30a27-182">The only supported API discover the geo locations in a Multi-Geo tenant is by using the Graph API.</span></span> <span data-ttu-id="30a27-183">В этой главе объясняется, какие разрешения необходимо предоставить в приложение для получения сведений о нескольких географически.</span><span class="sxs-lookup"><span data-stu-id="30a27-183">This chapter explains which permissions you'll need to grant to your application to discover Multi-Geo information.</span></span> <span data-ttu-id="30a27-184">Существует [длинный список возможных разрешений](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) можно предоставить приложение, определенных в Azure AD, что для чтения сведений о конфигурации клиента несколькими географически можно ограничить разрешения для:</span><span class="sxs-lookup"><span data-stu-id="30a27-184">There [a long list of possible permissions](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference) that you can grant to an application defined in Azure AD, but for reading Multi-Geo tenant configuration information you can limit permissions to:</span></span>

|<span data-ttu-id="30a27-185">**Разрешение**</span><span class="sxs-lookup"><span data-stu-id="30a27-185">**Permission**</span></span>|<span data-ttu-id="30a27-186">**Тип**</span><span class="sxs-lookup"><span data-stu-id="30a27-186">**Type**</span></span>|<span data-ttu-id="30a27-187">**Описание**</span><span class="sxs-lookup"><span data-stu-id="30a27-187">**Description**</span></span>| <span data-ttu-id="30a27-188">**Необходимые разрешения администратора**</span><span class="sxs-lookup"><span data-stu-id="30a27-188">**Admin consent needed**</span></span>
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="30a27-189">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span><span class="sxs-lookup"><span data-stu-id="30a27-189">**[Sites.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#user-permissions)**</span></span> | <span data-ttu-id="30a27-190">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-190">Application permission</span></span> | <span data-ttu-id="30a27-191">Позволяет приложениям чтения и записи документов и элементов списка всех семейств веб-сайтов не выполнен вход пользователя.</span><span class="sxs-lookup"><span data-stu-id="30a27-191">Allows the app to read/write documents and list items in all site collections without a signed in user.</span></span> | <span data-ttu-id="30a27-192">Да</span><span class="sxs-lookup"><span data-stu-id="30a27-192">Yes</span></span>

<span data-ttu-id="30a27-193">Используйте этапы создания приложения Azure AD, как описано в главе «Мое приложение должно иметь возможность чтения или изменение профилей для всех пользователей».</span><span class="sxs-lookup"><span data-stu-id="30a27-193">Use the Azure AD application creation steps as described in the "My application needs to be able to read/update profiles for all users" chapter.</span></span>

## <a name="my-application-needs-to-be-able-to-createdelete-sites-collections-or-set-tenant-site-collection-properties"></a><span data-ttu-id="30a27-194">Мое приложение необходимо иметь возможность создание и удаление семейства веб-сайтов или задать свойства семейства сайтов клиента</span><span class="sxs-lookup"><span data-stu-id="30a27-194">My application needs to be able to create/delete sites collections or set tenant site collection properties</span></span>
### <a name="im-using-the-microsoft-graph-api"></a><span data-ttu-id="30a27-195">Я использую Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="30a27-195">I'm using the Microsoft Graph API</span></span>
<span data-ttu-id="30a27-196">[Географическая ферма с несколькими сайтами](multigeo-sites.md) содержатся дополнительные сведения о том, как создавать сайты группы (или</span><span class="sxs-lookup"><span data-stu-id="30a27-196">The [Multi-Geo Sites](multigeo-sites.md) provides more details on how to create group sites (a.k.a.</span></span> <span data-ttu-id="30a27-197">«Современный» сайты рабочих групп) с помощью Microsoft Graph API, в этом разделе мы только адресации разрешения.</span><span class="sxs-lookup"><span data-stu-id="30a27-197">"modern" team sites) using the Microsoft Graph API, in this section we're only addressing the permissions.</span></span> <span data-ttu-id="30a27-198">Приведенной ниже таблице перечислены необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="30a27-198">Below table lists the needed permissions</span></span>

|<span data-ttu-id="30a27-199">**Разрешение**</span><span class="sxs-lookup"><span data-stu-id="30a27-199">**Permission**</span></span>|<span data-ttu-id="30a27-200">**Тип**</span><span class="sxs-lookup"><span data-stu-id="30a27-200">**Type**</span></span>|<span data-ttu-id="30a27-201">**Описание**</span><span class="sxs-lookup"><span data-stu-id="30a27-201">**Description**</span></span>| <span data-ttu-id="30a27-202">**Необходимые разрешения администратора**</span><span class="sxs-lookup"><span data-stu-id="30a27-202">**Admin consent needed**</span></span>
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="30a27-203">**[Group.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#group-permissions)**</span><span class="sxs-lookup"><span data-stu-id="30a27-203">**[Group.ReadWrite.All](https://developer.microsoft.com/en-us/graph/docs/concepts/permissions_reference#group-permissions)**</span></span> | <span data-ttu-id="30a27-204">Разрешение приложения</span><span class="sxs-lookup"><span data-stu-id="30a27-204">Application permission</span></span> | <span data-ttu-id="30a27-205">Позволяет приложениям создавать группы, чтение и обновить членство в группах и удаление групп.</span><span class="sxs-lookup"><span data-stu-id="30a27-205">Allows the app to create groups, read and update group memberships, and delete groups.</span></span> <span data-ttu-id="30a27-206">Все эти операции могут выполняться с приложения без пользователь выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="30a27-206">All of these operations can be performed by the app without a signed-in user.</span></span> <span data-ttu-id="30a27-207">Обратите внимание на то, что не все группы API поддерживает доступ с помощью разрешений только для приложений.</span><span class="sxs-lookup"><span data-stu-id="30a27-207">Note that not all group API supports access using app-only permissions.</span></span> | <span data-ttu-id="30a27-208">Да</span><span class="sxs-lookup"><span data-stu-id="30a27-208">Yes</span></span>

<span data-ttu-id="30a27-209">Microsoft Graph, на основе нескольких географически примеры с помощью библиотеки проверки подлинности Microsoft (MSAL) с помощью Microsoft Graph на конечной версии 2.</span><span class="sxs-lookup"><span data-stu-id="30a27-209">The Microsoft Graph based Multi-Geo samples are using the Microsoft Authentication Library (MSAL) to connect with the Microsoft Graph on the v2 endpoint.</span></span> <span data-ttu-id="30a27-210">По сравнению с ADAL, который подключается с помощью конечной версии 1, MSAL позволяет подключения к Microsoft Graph с учетными записями Microsoft, Azure AD и Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="30a27-210">Compared to ADAL which connects using the v1 endpoint, MSAL allows connection to the Microsoft Graph with Microsoft Accounts, Azure AD and Azure AD B2C.</span></span> <span data-ttu-id="30a27-211">Используйте этапы создания приложения Azure AD, как описано в главе «Мое приложение должно иметь возможность чтения или изменение профилей для всех пользователей».</span><span class="sxs-lookup"><span data-stu-id="30a27-211">Use the Azure AD application creation steps as described in the "My application needs to be able to read/update profiles for all users" chapter.</span></span>

### <a name="im-using-the-csom-tenant-api"></a><span data-ttu-id="30a27-212">Я использую API клиента CSOM</span><span class="sxs-lookup"><span data-stu-id="30a27-212">I'm using the CSOM Tenant API</span></span>
<span data-ttu-id="30a27-213">С помощью API клиента CSOM очень похож на уже было сказано CSOM руководства, в течение нескольких фактов идентичен рекомендации по использованию учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="30a27-213">Using the CSOM Tenant API is very similar to the previously described CSOM guidance, in a matter of fact the guidance for using user credentials is identical.</span></span> <span data-ttu-id="30a27-214">Для использования только субъект инструкциям такие же, но вам потребуется предоставить разные разрешения (клиент, полный доступ):</span><span class="sxs-lookup"><span data-stu-id="30a27-214">For using an app-only principal the instructions are the same but you'll need to grant different permissions (tenant, full control):</span></span>

```Xml
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```

## <a name="resources"></a><span data-ttu-id="30a27-215">Resources</span><span class="sxs-lookup"><span data-stu-id="30a27-215">Resources</span></span>
<span data-ttu-id="30a27-216">Под списком ресурсов полезны, если также дополнительные сведения о Microsoft Graph API и CSOM API:</span><span class="sxs-lookup"><span data-stu-id="30a27-216">Below list of resources are useful when you're learning more about the Microsoft Graph API and CSOM API's:</span></span>
- [<span data-ttu-id="30a27-217">Центр разработчиков Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="30a27-217">Microsoft Graph developer center</span></span>](https://developer.microsoft.com/en-us/graph)
- [<span data-ttu-id="30a27-218">Получение маркера доступа для вызова API график</span><span class="sxs-lookup"><span data-stu-id="30a27-218">Get access tokens to call the Graph API</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/auth_overview)
- [<span data-ttu-id="30a27-219">Документация по Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="30a27-219">Microsoft Graph documentation</span></span>](https://developer.microsoft.com/en-us/graph/docs/concepts/overview)
- [<span data-ttu-id="30a27-220">Графическое представление проводника</span><span class="sxs-lookup"><span data-stu-id="30a27-220">Graph Explorer</span></span>](https://developer.microsoft.com/en-us/graph/graph-explorer)
- [<span data-ttu-id="30a27-221">Права только для приложений и с повышенными привилегиями в объектная модель SharePoint</span><span class="sxs-lookup"><span data-stu-id="30a27-221">App-only and elevated privileges in the SharePoint add-in model</span></span>](app-only-elevated-privileges-sharepoint-add-in.md)
