# <a name="get-user-identity-and-properties-in-sharepoint"></a>Получение свойств и удостоверения пользователя в SharePoint
Узнайте, как получить удостоверение пользователя и сведения о нем в SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Существуют разные способы получения удостоверения и сведений о пользователе, в зависимости от сведений, которые требуется получить. В этой статье рассматриваются некоторые способы, с помощью которых это можно сделать.
 

## <a name="prerequisites-for-retrieving-user-identity-and-properties"></a>Необходимые условия для получения свойств и удостоверения пользователя
<a name="Prereq"> </a>


- Подготовьте среду разработки надстроек, как описано в статье [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins).
    
 
- Установите Visual Studio.
    
 
- Установите последнюю версию [Инструментов разработчика Office для Visual Studio 2013](http://aka.ms/OfficeDevToolsForVS2013) или [Инструментов разработчика Office для Visual Studio 2015](http://aka.ms/OfficeDevToolsForVS2015).
    
 

 **Примечание.** Руководство по настройке среды разработки, соответствующей вашим потребностям, см. в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins).
 


### <a name="core-concepts-to-know-for-retrieving-user-identity-and-properties"></a>Основные понятия, связанные с получением свойств и удостоверения пользователя

В приведенной ниже таблице перечислены некоторые полезные статьи, которые помогут разобраться в понятиях, используемых при создании надстроек SharePoint.
 

 


|**Статья **|**Описание**|
|:-----|:-----|
| [Разрешения надстроек в SharePoint](add-in-permissions-in-sharepoint-2013)|Сведения о разрешениях надстроек SharePoint для работы с SharePoint, включая типы разрешений надстроек, уровни запроса разрешений и управление разрешениями. В этой статье также рассматриваются различия между правами разрешений надстройки и правами пользователя.|
| [Поток OAuth маркера контекста для надстроек SharePoint](context-token-oauth-flow-for-sharepoint-add-ins)|Сведения о потоке проверки подлинности и авторизации OAuth для надстроек, размещаемых в облаке.|
| [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins)|Узнайте, как создавать базовое размещенное у поставщика Надстройка SharePoint с помощью Инструменты разработчика Office для Visual Studio 2012, как взаимодействовать с сайтами Microsoft SharePoint с помощью CSOM (клиентской объектной модели) SharePoint, и как реализовать OAuth в Надстройка SharePoint.|

## <a name="retrieving-current-website-user-identity"></a>Получение удостоверения текущего пользователя веб-сайта
<a name="WebsiteUserID"> </a>

Получить удостоверение текущего пользователя веб-сайта легче всего через объект **Web**. С помощью файла TokenHelper.cs из проекта вы можете получить удостоверение текущего пользователя веб-сайта с помощью приведенного ниже фрагмента кода.
 

 

```C#
ClientContext clientContext =
                    TokenHelper.GetClientContextWithAccessToken(
                        sharepointUrl.ToString(), accessToken);
 
 
            //Load the properties for the Web object.
            Web web = clientContext.Web;
            clientContext.Load(web);
            clientContext.ExecuteQuery();
 
            //Get the site name.
            siteName = web.Title;
 
            //Get the current user.
            clientContext.Load(web.CurrentUser);
            clientContext.ExecuteQuery();
            currentUser = clientContext.Web.CurrentUser.LoginName;

```


- Если вы используете Office 365, полученное имя для входа будет примерно таким: `i:0#.f|membership|adam@contoso.com`.
    
 
- Если вы используете Microsoft SharePoint локально, и пользователь вошел как обычный пользователь с помощью NTLM, то полученное имя для входа будет аналогично следующему:  `i:0#.w|contoso\adam`.
    
 
- Если вы используете локальную среду SharePoint, а пользователь выполняет вход с помощью учетной записи фермы, то будет получено имя для входа `SHAREPOINT\System`.
    
 

## <a name="retrieving-user-identity-using-the-resolveprincipal-method"></a>Получение удостоверения пользователя с помощью метода ResolvePrincipal
<a name="ResolvePrincipal"> </a>

Далее приводится другой способ получения имени для входа пользователя. Если у вас есть адрес электронной почты или отображаемое имя пользователя, то для получения его имени для входа можно использовать метод  **ResolvePrincipal** .
 

 

 **Примечание.** API находятся в пространстве имен Microsoft.SharePoint.Client.Utilities в сборке [Microsoft.SharePoint.Client.dll](http://msdn.microsoft.com/ru-ru/library/microsoft.sharepoint.client.utilities.utility.resolveprincipal.aspx).
 

Ниже представлен пример кода, иллюстрирующей получение данных для входа пользователя.
 

 



```C#
ClientResult<Microsoft.SharePoint.Client.Utilities.PrincipalInfo> persons = Microsoft.SharePoint.Client.Utilities.Utility.ResolvePrincipal(clientContext, clientContext.Web, <email>, Microsoft.SharePoint.Client.Utilities.PrincipalType.User, Microsoft.SharePoint.Client.Utilities.PrincipalSource.All, null, true);
                    clientContext.ExecuteQuery();
                    Microsoft.SharePoint.Client.Utilities.PrincipalInfo person = persons.Value;

```

Значение **Person.LoginName** предоставляет сведения для входа.
 

 

## <a name="retrieving-user-identity-and-profile-properties"></a>Получение удостоверения пользователя и свойств профиля
<a name="Profile"> </a>

Если требуется получить удостоверение и свойства пользователя, можно использовать маркер OAuth и API социальных компонентов. Сначала получите маркер OAuth и установите его в контекст клиента. В следующем примере кода показывается, как получить свойства профиля пользователя.
 

 

```C#

ClientContext clientContext = new ClientContext(<sharepointurl>);
clientContext.AuthenticationMode = ClientAuthenticationMode.Anonymous;
clientContext.FormDigestHandlingEnabled = false;
clientContext.ExecutingWebRequest +=
delegate(object oSender, WebRequestEventArgs webRequestEventArgs)
{                      
    webRequestEventArgs.WebRequestExecutor.RequestHeaders["Authorization"] =
        "Bearer " + accessToken;
};

```

Затем используйте API **UserProfilesPeopleManager**, чтобы получить свойства пользователя надстройки.
 

 



```C#

PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties personDetails = peopleManager.GetMyProperties();
clientContext.Load(personDetails, personsD => personsD.AccountName, personsD => personsD.Email,  personsD => personsD.DisplayName);
                clientContext.ExecuteQuery();

```

Чтобы код работал, должны соблюдаться приведенные ниже условия.
 

 

- Необходимо настроить и синхронизировать общую службу профилей пользователей в SharePoint для пользователей.
    
 
- Необходимо добавить в манифест надстройки следующий уровень разрешений для социальных компонентов:
    
```XML
  <AppPermissionRequest Right="Read" Scope="http://sharepoint/social/tenant" />

```

API находятся в библиотеке Microsoft.SharePoint.Client.UserProfiles.dll.
 

 
Далее приводится еще один пример фрагмента кода, показывающий, как можно получить доступ к хранилищу профилей пользователей.
 

 



```C#

ClientContext clientContext; //Create this like you normally would.               
PeopleManager peopleManager = new PeopleManager(clientContext);
PersonProperties myProperties = peopleManager.GetMyProperties();
clientContext.Load(myProperties);
clientContext.ExecuteQuery();

```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="AdditionalResources"> </a>


-  [Разрешения надстроек в SharePoint](add-in-permissions-in-sharepoint-2013)
    
 
-  [Поток OAuth маркера контекста для надстроек SharePoint](context-token-oauth-flow-for-sharepoint-add-ins)
    
 
-  [Надстройки SharePoint](sharepoint-add-ins)
    
 
-  [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins)
    
 

