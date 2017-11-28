# <a name="granting-access-using-sharepoint-app-only"></a>Предоставление доступа с помощью SharePoint только для приложений
Только для приложений SharePoint — модель старых, но по-прежнему очень соответствующие настройки участников приложения. Эта модель работает для обоих SharePoint Online и локальной SharePoint 2013/2016 и идеально подходит для подготовки приложений для переноса из SharePoint в локальной в SharePoint online. Шаги, описанные ниже показано, как настройка субъект приложения с правами полного доступа клиентов, но очевидно, что может также предоставить разрешения на только что чтение этим способом.

## <a name="setting-up-an-app-only-principal-with-tenant-permissions"></a>Настройка субъект только для приложений с разрешениями клиента
Перейдите на сайт вашего клиента (например, https://contoso.sharepoint.com), а затем вызвать страницы appregnew.aspx (например, https://contoso.sharepoint.com/_layouts/15/appregnew.aspx). В этой страницы нажмите кнопку на кнопку Создать, чтобы создать идентификатор клиента и секрет клиента и заполнить остальные сведения, как показано в-снимке экрана ниже.

![с помощью appregnew.aspx](media/apponly/sharepointapponly1.png)

> [!IMPORTANT]
> Хранятся полученные данные (идентификатор клиента и секрет клиента), так как это понадобится на следующем этапе!

Следующим шагом предоставление разрешений для только что созданный субъекта. Поскольку мы требуется предоставить разрешения клиентов с областью действия в этом предоставление может выполняться только через appinv.aspx страницу на сайте администрирования клиентов. Можно получить доступ к этой сайта с помощью https://contoso-admin.sharepoint.com/_layouts/15/appinv.aspx. После загрузки страницы добавьте идентификатором клиента и найти созданный участника:

![с помощью appregnew.aspx](media/apponly/sharepointapponly2.png)

Чтобы предоставить разрешения, необходимые для предоставления разрешения на XML, описывающий необходимые разрешения. После этого приложения должна быть возможность доступа ко всем сайтам + также использует поиска с помощью только для приложений должен перечисленных ниже разрешений:

```
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/tenant" Right="FullControl" />
</AppPermissionRequests>
```

При нажатии кнопки на создание появится диалоговое окно подтверждения разрешений. Клавиши, доверие для предоставления разрешений:

![с помощью appregnew.aspx](media/apponly/sharepointapponly3.png)

> [!IMPORTANT]
> Пожалуйста защищают комбинацию идентификатор и секрет созданный клиента как может быть учетная запись администратора. С помощью этой идентификатор и секрет клиента один можно чтение/обновление всех данных в среде SharePoint Online!

С помощью подготовительных обратитесь к разделу следующей главе, в котором показано, как можно использовать субъекта созданного приложения с помощью его идентификатор клиента и секрета сочетание.

## <a name="using-this-principal-in-your-application-using-the-sharepoint-pnp-sites-core-library"></a>Использование участника в приложении с помощью библиотеки PnP основных сайтах SharePoint
На первом шаге, добавьте пакет nuget библиотеки PnP основных сайтов SharePoint: https://www.nuget.org/packages/SharePointPnPCoreOnline. После этого можно использовать ниже конструкцию кода:

```C#
string siteUrl = "https://contoso.sharepoint.com/sites/demo";
using (var cc = new AuthenticationManager().GetAppOnlyAuthenticatedContext(siteUrl, "[Your Client ID]", "[Your Client Secret]"))
{
    cc.Load(cc.Web, p => p.Title);
    cc.ExecuteQuery();
    Console.WriteLine(cc.Web.Title);
};
```

## <a name="using-this-principal-in-your-application-without-using-the-pnp-sites-core-library"></a>Использование участника в приложении без использования библиотеки PnP основных узлов
После субъекта создается и согласие для запроса доступа можно использовать идентификатор и секрет участника. Класс TokenHelper.cs будет скопировать идентификатор и секрет из файла конфигурации приложения.
с помощью Microsoft.SharePoint.Client; Использование системы;

```C#
namespace AzureACSAuth
{
    class Program
    {
        static void Main(string[] args)
        {
            string siteUrl = "https://contoso.sharepoint.com/sites/demo";

            //Get the realm for the URL
            string realm = TokenHelper.GetRealmFromTargetUrl(new Uri(siteUrl));

            //Get the access token for the URL.  
            string accessToken = TokenHelper.GetAppOnlyAccessToken(TokenHelper.SharePointPrincipal, new Uri(siteUrl).Authority, realm).AccessToken;

            //Create a client context object based on the retrieved access token
            using (ClientContext cc = TokenHelper.GetClientContextWithAccessToken(siteUrl, accessToken))
            {
                cc.Load(cc.Web, p => p.Title);
                cc.ExecuteQuery();
                Console.WriteLine(cc.Web.Title);
            }
        }
    }
}
```

Пример app.config выглядит следующим образом:

```XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <appSettings>
    <!-- Use AppRegNew.aspx and AppInv.aspx to register client id with secret -->
    <add key="ClientId" value="[Your Client ID]" />
    <add key="ClientSecret" value="[Your Client Secret]" />
  </appSettings>
</configuration>
```

> [!NOTE]
> Можно легко вставить класс TokenHelper.cs в вашем проекте, добавив пакет AppForSharePointOnlineWebToolkit nuget для решения.

