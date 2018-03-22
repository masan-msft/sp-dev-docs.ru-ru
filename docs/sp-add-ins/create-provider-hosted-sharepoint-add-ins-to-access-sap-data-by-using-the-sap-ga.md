---
title: Создание надстроек SharePoint, размещаемых у поставщика, для доступа к данным SAP
description: Узнайте, как создать надстройку SharePoint для получения авторизованного доступа к SAP с помощью шлюза SAP для Майкрософт.
ms.date: 12/27/2017
ms.prod: sharepoint
ms.openlocfilehash: da76de20f1e72d88d467c400d71fd03a279d7c31
ms.sourcegitcommit: 6bc4c8e43c260deabc60d41d633586bfa3e6024a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/28/2017
---
# <a name="create-provider-hosted-sharepoint-add-ins-to-access-sap-data-by-using-the-sap-gateway-for-microsoft"></a>Создание надстроек SharePoint, размещаемых у поставщика, для доступа к данным SAP с помощью шлюза SAP для Майкрософт

Вы можете создать надстройку SharePoint, которая считывает и записывает данные SAP, а при необходимости и данные SharePoint, с помощью шлюза SAP для Майкрософт и библиотеки аутентификации Azure Active Directory для .NET. В этой статье описано, как создать надстройку SharePoint для получения авторизованного доступа к SAP. 
 

## <a name="prerequisites"></a>Предварительные требования

Ниже перечислены компоненты, необходимые для выполнения процедур, описанных в этой статье.

- **Сайт разработчика Office 365** в домене Office 365, связанном с подпиской Microsoft Azure Active Directory (Azure AD). См. статью [Настройка среды разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) или [Создание сайта разработчика с использованием имеющейся подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).
    
- Приложение **Visual Studio 2013 c обновлением 2** или более поздней версии, которое вы можете получить на веб-странице [Вас приветствует Visual Studio](https://msdn.microsoft.com/library/dd831853.aspx).

- **Инструменты разработчика Microsoft Office для Visual Studio**. Версия, включенная в обновление 2 для Visual Studio 2013 или более поздней версии.
    
- **Шлюз SAP Gateway для Майкрософт**, развернутый и настроенный в Azure. См. документацию по [шлюзу SAP для Майкрософт](https://help.sap.com/saphelp_nwgwpam_1/helpdata/en/b5/74d3ad2f33428193a32c09c351e0b3/frameset.htm).
    
- **Учетная запись организации в Azure**. См. статью [Регистрация приложения API Office 365 в Azure AD](https://github.com/jasonjoh/office365-azure-guides/blob/master/RegisterAnAppInAzure.md).
    
    > [!NOTE] 
    > После создания учетной записи Office 365 (login.microsoftonline.com) войдите в нее и измените временный пароль.

- **Конечная точка OData для SAP** с примером данных. См. документацию к [шлюзу SAP для Майкрософт](https://help.sap.com/saphelp_nwgwpam_1/helpdata/en/b5/74d3ad2f33428193a32c09c351e0b3/frameset.htm).
    
- **Общее представление об Azure AD.** См. статью [Начало работы с Azure AD](https://docs.microsoft.com/ru-RU/azure/active-directory/get-started-azure-ad).
    
- **Общее представление о надстройках SharePoint.** См. статью [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).

- **Общее представление об OAuth 2.0 в Azure AD.** См. статью [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code) и связанные с ней статьи.
    
- **Пример кода.** [SharePoint: использование шлюза SAP для Майкрософт в надстройке SharePoint](https://code.msdn.microsoft.com/office/sharepoint-2013-using-the-0931abce)
 

<a name="AuthOverview"> </a> 

## <a name="understand-authentication-and-authorization-to-sap-gateway-for-microsoft-and-sharepoint"></a>Общие сведения о проверке подлинности и авторизации в шлюзе SAP для Майкрософт и SharePoint

С помощью OAuth 2.0 в Azure AD приложения могут получать доступ к нескольким ресурсам, размещаемым в Azure. В их число входит шлюз SAP для Майкрософт. В протоколе OAuth 2.0 субъектами безопасности являются не только пользователи, но и приложения. Субъектам приложений необходимы проверка подлинности и авторизация для защищенных ресурсов, а не только для пользователей (а иногда и вместо них). 

В этом процессе участвует поток OAuth, в котором приложение (например, надстройка SharePoint) получает маркеры доступа и обновления. Маркер доступа принимают все службы и приложения, размещенные в Azure и использующие Azure AD в качестве сервера авторизации OAuth 2.0. Этот процесс во многом аналогичен тому, как удаленные компоненты надстройки SharePoint, размещенной у поставщика, получают авторизацию для SharePoint (см. статью [Создание надстроек для SharePoint, использующих авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) и ее подразделы). Однако система авторизации для контроля доступа использует в качестве доверенного поставщика маркеров службу контроля доступа Azure (ACS), а не Azure AD.
 
> [!TIP] 
> Если надстройка SharePoint получает доступ не только к шлюзу SAP для Майкрософт, но и к SharePoint, то она должна использовать *обе* системы: Azure AD для получения маркера доступа к шлюзу SAP для Майкрософт и систему авторизации ACS для получения маркера доступа к SharePoint. Маркеры из этих двух источников не являются взаимозаменяемыми. Дополнительные сведения см. в разделе [Предоставление приложению ASP.NET доступа к SharePoint (необязательно)](#SharePoint).

Подробное описание и схему потока OAuth, используемого протоколом OAuth 2.0 в Azure AD, см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code). 

Подобное описание и схему потока для доступа к SharePoint см. в [руководстве по потоку токена контекста](context-token-oauth-flow-for-sharepoint-add-ins.md#OAuth_ProcessFlowSteps).


## <a name="create-the-sharepoint-add-in"></a>Создание надстройки SharePoint

### <a name="to-create-the-visual-studio-solution"></a>Создание решения Visual Studio


1. Создайте проект **надстройки SharePoint** в Visual Studio, выполнив указанные ниже действия. В примере из этой статьи используется язык C#, но вы также можете создать проект надстройки SharePoint с помощью раздела **Visual Basic** шаблонов нового проекта.
    
  1. В мастере создания надстройки SharePoint введите имя проекта и нажмите кнопку **ОК**. Для нашего примера укажите имя **SAP2SharePoint**.
      
  2. Укажите URL-адрес вашего сайта разработчика Office 365 (включая косую черту в конце) в качестве сайта отладки. Пример: `https://<O365_domain>.sharepoint.com/`. Выберите тип надстройки **Размещение у поставщика** и нажмите кнопку **Далее**.
      
  3. Выберите тип проекта. Для нашего примера выберите **Приложение веб-форм ASP.NET**. Вы также можете создавать приложения ASP.NET MVC, получающие доступ к шлюзу SAP для Майкрософт. Нажмите кнопку **Далее**.
      
  4. Выберите Azure ACS в качестве системы проверки подлинности. Надстройка SharePoint будет использовать эту систему для доступа к SharePoint. Эта система не используется при доступе к шлюзу SAP для Майкрософт. Нажмите кнопку **Готово**.
 
2. После создания проекта вам будет предложено войти в учетную запись Office 365. Используйте учетные данные администратора учетной записи, например `Bob@<O365_domain>.onmicrosoft.com`.
 
3. Решение Visual Studio включает два проекта: проект самой надстройки SharePoint и проект веб-форм ASP.NET. Добавьте пакет **библиотеки проверки подлинности Active Directory** (ADAL) к проекту ASP.NET, выполнив указанные ниже действия.
    
  1. Щелкните правой кнопкой мыши папку **Ссылки** проекта ASP.NET (в нашем примере он называется **SAP2SharePointWeb**) и выберите команду **Управление пакетами NuGet**. 
      
  2. В открывшемся диалоговом окне выберите **Сеть**. Введите **Microsoft.IdentityModel.Clients.ActiveDirectory** в поле поиска.
      
  3. Когда в результатах поиска появится библиотека ADAL, нажмите кнопку **Установить** и примите условия лицензионного соглашения.
    
4. Добавьте пакет Json.net в проект ASP.NET, выполнив указанные ниже действия.
    
  1. Введите **Json.net** в поле поиска. Если появится слишком много результатов, попробуйте выполнить поиск по запросу **Newtonsoft.json**.
      
  2. Когда в результатах поиска появится библиотека Json.net, нажмите кнопку **Установить**.
 
5. Нажмите кнопку **Закрыть**.
    

### <a name="to-register-your-web-application-with-azure-ad"></a>Регистрация веб-приложения в Azure AD

1. Войдите на [портал управления Azure](https://manage.windowsazure.com), используя учетную запись администратора Azure.
    
  > [!NOTE] 
  > Из соображений безопасности не рекомендуем использовать учетную запись администратора при разработке надстроек.

2. Выберите **Active Directory** в левой части страницы.    
 
3. Выберите каталог.     
 
4. Выберите **ПРИЛОЖЕНИЯ** (на верхней панели навигации).    
 
5. На панели инструментов в нижней части экрана нажмите кнопку **Добавить**.    
 
6. В открывшемся диалоговом окне выберите элемент **Добавить приложение, разрабатываемое моей организацией**.    
 
7. В диалоговом окне **ДОБАВЛЕНИЕ ПРИЛОЖЕНИЯ** введите имя приложения. Для нашего примера укажите имя **ContosoAutomobileCollection**.     
 
8. Выберите тип надстройки **Веб-надстройка или веб-API** и нажмите кнопку со стрелкой вправо.    
 
9. На второй странице диалогового окна укажите в поле **URL-адрес для входа** URL-адрес отладки SSL из проекта ASP.NET решения Visual Studio. Чтобы узнать этот URL-адрес, выполните указанные ниже действия. *Сначала необходимо зарегистрировать надстройку с URL-адресом отладки, чтобы иметь возможность запускать отладчик Visual Studio (F5). Когда надстройка будет готова к размещению, вы повторно зарегистрируете ее, используя URL-адрес веб-сайта Azure. См. раздел [Изменение надстройки и ее размещение в Azure и Office 365](#Stage).*
    
  1. Выделите проект ASP.NET в **обозревателе решений**. 

  2. В окне **Свойства** скопируйте значение свойства **URL-АДРЕС SSL**. Пример: `https://localhost:44300/`.
      
  3. Вставьте его в поле **URL-АДРЕС ДЛЯ ВХОДА** диалогового окна **ДОБАВЛЕНИЕ ПРИЛОЖЕНИЯ**.
    
10. В качестве **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ** укажите уникальный URI, например имя приложения, добавленное к URL-адресу SSL: `https://localhost:44300/ContosoAutomobileCollection`.    
 
11. Нажмите кнопку с галочкой. Откроется информационная панель Azure для приложения с сообщением об успешном выполнении операции.    
 
12. Выберите пункт **НАСТРОЙКА** в верхней части страницы.    
 
13. Найдите **КОД КЛИЕНТА** и скопируйте его. Он пригодится для дальнейших действий.    
 
14. В разделе **Ключи** создайте ключ. Он появится не сразу. Нажмите кнопку **СОХРАНИТЬ** в нижней части страницы, и ключ станет виден. Скопируйте его. Он понадобится вам позже.    
 
15. Прокрутите вниз до раздела **Разрешения для других приложений** и выберите свое приложение-службу шлюза SAP для Майкрософт.    
 
16. Откройте раскрывающийся список **Делегированные разрешения** и выберите разрешения службы шлюза SAP для Майкрософт, которые будет использовать ваша надстройка SharePoint.    
 
17. Нажмите кнопку **СОХРАНИТЬ** в нижней части экрана.
    
 

### <a name="to-configure-the-application-to-communicate-with-azure-ad"></a>Настройка приложения для взаимодействия с Azure AD

1. В Visual Studio откройте файл web.config проекта ASP.NET.    
 
2. В разделе `<appSettings>` в Инструментах разработчика Office для Visual Studio появились элементы **ClientID** и **ClientSecret** надстройки SharePoint. Они используются в системе авторизации Azure ACS, если приложение ASP.NET получает доступ к SharePoint. В нашем примере можно не обращать на них внимания, но не следует удалять их. Они необходимы в надстройках SharePoint, размещаемых у поставщика, даже если надстройка не получает доступ к данным SharePoint. Их значения меняются при каждом нажатии клавиши F5 в Visual Studio. 

  Добавьте в раздел два приведенных ниже элемента. Приложение использует их для проверки подлинности в Azure AD. Помните, что приложения, как и пользователи, являются субъектами безопасности в системах с проверкой подлинности и авторизацией на основе OAuth.
      
  ```
    <add key="ida:ClientID" value="" />
    <add key="ida:ClientKey" value="" />
  ```

3. Вставьте сохраненный ранее идентификатор клиента из каталога Azure AD в качестве значения ключа **ida:ClientID**. Оставьте регистр и пунктуацию без изменений. Будьте внимательны, чтобы не добавить пробел в начале или конце значения. В элементе **ida:ClientKey** укажите *ключ*, сохраненный из каталога. Опять-таки, не добавляйте пробелы и не меняйте значение каким-либо другим образом. Теперь раздел `<appSettings>` должен выглядеть примерно так (значением **ClientId** может быть GUID или пустая строка):
    
  ```
    <appSettings>
      <add key="ClientId" value="" />
      <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
      <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
      <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
    </appSettings>
  ```

  > [!NOTE] 
  > Azure AD идентифицирует приложение по URL-адресу localhost, который использовался для его регистрации. Идентификатор и ключ клиента сопоставлены с этим удостоверением. Когда вы будете готовы разместить приложение на веб-сайте Azure, вы повторно зарегистрируете его с новым URL-адресом.

4. Не покидая раздел **appSettings**, добавьте ключ **Authority** и укажите в качестве его значения домена Office 365 (*домен*.onmicrosoft.com) своей организационной учетной записи. В нашем примере используется организационная учетная запись `Bob@<O365_domain>.onmicrosoft.com`, поэтому указывается домен `<O365_domain>.onmicrosoft.com`. 
    
  ```
    <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
  ```

5. В разделе **appSettings** добавьте ключ **AppRedirectUrl** и укажите в качестве его значения страницу, на которую должен перенаправляться браузер пользователя, когда надстройка ASP.NET получит код авторизации от Azure AD. Как правило, это та же страница, которую просматривал пользователь на момент вызова Azure AD. В нашем примере используется значение URL-адреса SSL, к которому добавлена строка "/Pages/Default.aspx", как показано в следующем фрагменте кода (это еще одно значение, которое потребуется изменить для размещения):
    
  ```
    <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
  ```

6. Не покидая раздел **appSettings**, добавьте ключ **ResourceUrl** и задайте в качестве его значения URI идентификатора приложения шлюза SAP для Майкрософт, а *не* URI идентификатора приложения ASP.NET. Это значение можно узнать у администратора шлюза SAP для Майкрософт. Ниже приведен пример.
      
  ```
    <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
  ```

  Теперь раздел `<appSettings>` должен выглядеть примерно так:
    
  ```
    <appSettings>
      <add key="ClientId" value="06af1059-8916-4851-a271-2705e8cf53c6" />
      <add key="ClientSecret" value="LypZu2yVajlHfPLRn5J2hBrwCk5aBOHxE4PtKCjIQkk=" />
      <add key="ida:ClientID" value="4da99afe-08b5-4bce-bc66-5356482ec2df" />
      <add key="ida:ClientKey" value="URwh/oiPay/b5jJWYHgkVdoE/x7gq3zZdtcl/cG14ss=" />
      <add key="Authority" value="<O365_domain>.onmicrosoft.com" />
      <add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />
      <add key="ResourceUrl" value="http://<SAP_gateway_domain>.cloudapp.net/" />
    </appSettings>
  ```

7. Сохраните и закройте файл web.config.
    
  > [!TIP] 
  > Запуская отладчик Visual Studio (F5), не оставляйте файл web.config открытым. Инструменты разработчика Office для Visual Studio меняют значение **ClientId** (а не **ida:ClientID**) при каждом нажатии клавиши F5. При этом вам нужно отреагировать на предложение заново загрузить файл web.config (если он открыт) перед отладкой.


### <a name="to-add-a-helper-class-to-authenticate-to-azure-ad"></a>Добавление вспомогательного класса для проверки подлинности в Azure AD

1. Щелкните проект ASP.NET правой кнопкой мыши и следуйте процессу добавления элемента Visual Studio, чтобы добавить к проекту новый файл класса с именем **AADAuthHelper.cs**.

2. Добавьте в файл приведенные ниже операторы **using**.
    
  ```
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Configuration;
    using System.Web.UI;
  ```

3. Измените ключевое слово доступа с **public** на **internal** и добавьте ключевое слово **static** к объявлению класса.
    
  ```
    internal static class AADAuthHelper
  ```

4. Добавьте в класс приведенные ниже поля. В этих полях хранятся сведения, с помощью которых приложение ASP.NET получает маркеры доступа из Azure AD.
    
  ```
    private static readonly string _authority = ConfigurationManager.AppSettings["Authority"];
    private static readonly string _appRedirectUrl = ConfigurationManager.AppSettings["AppRedirectUrl"];
    private static readonly string _resourceUrl = ConfigurationManager.AppSettings["ResourceUrl"];     
    private static readonly string _clientId = ConfigurationManager.AppSettings["ida:ClientID"];        
    private static readonly ClientCredential _clientCredential = new ClientCredential(
                              ConfigurationManager.AppSettings["ida:ClientID"],
                              ConfigurationManager.AppSettings["ida:ClientKey"]);

    private static readonly AuthenticationContext _authenticationContext = 
                new AuthenticationContext("https://login.windows.net/common/" + 
                                          ConfigurationManager.AppSettings["Authority"]);
  ```

5. Добавьте в класс приведенное ниже свойство. Это свойство содержит URL-адрес экрана входа в Azure AD.
    
  ```
      private static string AuthorizeUrl
    {
        get
        {
            return string.Format("https://login.windows.net/{0}/oauth2/authorize?response_type=code&amp;redirect_uri={1}&amp;client_id={2}&amp;state={3}",
                _authority,
                _appRedirectUrl,
                _clientId,
                Guid.NewGuid().ToString());
        }
    }
  ```

6. Добавьте в класс приведенные ниже свойства. Они кэшируют маркеры доступа и обновления, а также проверяют, действительны ли они.
    
  ```
      public static Tuple<string, DateTimeOffset> AccessToken
    {
        get { return HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] 
          as Tuple<string, DateTimeOffset>;
        }

        set { HttpContext.Current.Session["AccessTokenWithExpireTime-" + _resourceUrl] = value; }
    }

    private static bool IsAccessTokenValid
    {
      get { 
          return AccessToken != null &amp;&amp;
          !string.IsNullOrEmpty(AccessToken.Item1) &amp;&amp;
          AccessToken.Item2 > DateTimeOffset.UtcNow;
      }
    }

    private static string RefreshToken
    {
        get { return HttpContext.Current.Session["RefreshToken" + _resourceUrl] as string; }
        set { HttpContext.Current.Session["RefreshToken-" + _resourceUrl] = value; }
    }

    private static bool IsRefreshTokenValid
    {
        get { return !string.IsNullOrEmpty(RefreshToken); }
    }

  ```

7. Добавьте к классу следующие методы. Они используются для проверки кода аутентификации и получения маркера доступа из Azure AD с помощью кода авторизации или маркера обновления.
    
  ```
    private static bool IsAuthorizationCodeNotNull(string authCode)
    {
        return !string.IsNullOrEmpty(authCode);
    }

    private static Tuple<Tuple<string,DateTimeOffset>,string> AcquireTokensUsingAuthCode(string authCode)
    {
        var authResult = _authenticationContext.AcquireTokenByAuthorizationCode(
                    authCode,
                    new Uri(_appRedirectUrl),
                    _clientCredential,
                    _resourceUrl);

        return new Tuple<Tuple<string, DateTimeOffset>, string>(
                    new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn), 
                    authResult.RefreshToken);
    }

    private static Tuple<string, DateTimeOffset> RenewAccessTokenUsingRefreshToken()
    {
        var authResult = _authenticationContext.AcquireTokenByRefreshToken(
                            RefreshToken,
                            _clientCredential.OwnerId,
                            _clientCredential,
                            _resourceUrl);

        return new Tuple<string, DateTimeOffset>(authResult.AccessToken, authResult.ExpiresOn);
    }

  ```

8. Добавьте в класс приведенный ниже метод. Он вызывается из кода ASP.NET для получения маркера доступа перед отправкой запроса данных SAP через шлюз SAP для Майкрософт.
    
  ```
      internal static void EnsureValidAccessToken(Page page)
    {
        if (IsAccessTokenValid) 
        {
            return;
        }
        else if (IsRefreshTokenValid) 
        {
            AccessToken = RenewAccessTokenUsingRefreshToken();
            return;
        }
        else if (IsAuthorizationCodeNotNull(page.Request.QueryString["code"]))
        {
            Tuple<Tuple<string, DateTimeOffset>, string> tokens = null;
            try
            {
                tokens = AcquireTokensUsingAuthCode(page.Request.QueryString["code"]);
            }
            catch 
            {
                page.Response.Redirect(AuthorizeUrl);
            }
            AccessToken = tokens.Item1;
            RefreshToken = tokens.Item2;
            return;
        }
        else
        {
            page.Response.Redirect(AuthorizeUrl);
        }
    }
  ```


> [!TIP] 
> В классе AADAuthHelper реализован минимум действий по обработке ошибок. Чтобы создать надежную надстройку SharePoint для использования в рабочей среде, добавьте обработку ошибок, как описано в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://docs.microsoft.com/ru-RU/azure/active-directory/develop/active-directory-protocols-oauth-code) на сайте MSDN.


### <a name="to-create-data-model-classes"></a>Создание классов модели данных

1. Создайте один или несколько классов для моделирования данных, которые надстройка получает из SAP. В нашем примере используется только один класс модели данных. Щелкните проект ASP.NET правой кнопкой мыши и следуйте процессу добавления элемента Visual Studio, чтобы добавить к проекту новый файл класса с именем **Automobile.cs**.

2. Добавьте в текст класса следующий код:
    
  ```
    public string Price;
    public string Brand;
    public string Model;
    public int Year;
    public string Engine;
    public int MaxPower;
    public string BodyStyle;
    public string Transmission;
  ```


### <a name="to-add-code-behind-to-get-data-from-sap-via-the-sap-gateway-for-microsoft"></a>Добавление кода для получения данных из SAP через шлюз SAP для Майкрософт

1. Откройте файл Default.aspx.cs и добавьте приведенные ниже операторы **using**.
    
  ```
    using System.Net;
    using Newtonsoft.Json.Linq;
  ```

2. Добавьте объявление **const** к классу Default, указав в качестве значения URL-адрес конечной точки OData SAP, которую будет использовать надстройку. Вот пример такого объявления:
    
  ```
      private const string SAP_ODATA_URL = @"https://<SAP_gateway_domain>.cloudapp.net:8081/perf/sap/opu/odata/sap/ZCAR_POC_SRV/";
  ```

3. В Инструментах разработчика Office для Visual Studio появились методы **Page\_PreInit** и **Page\_Load**. Раскомментируйте код метода **Page\_Load** и весь метод **Page\_Init**. Этот код не используется в нашем примере. Если ваша надстройка SharePoint будет получать доступ к SharePoint, восстановите этот код. См. раздел [Предоставление приложению ASP.NET доступа к SharePoint (необязательно)](#SharePoint).

4. Добавьте приведенную ниже строку в начале метода **Page_Load**. Это упрощает отладку, так как приложение ASP.NET связывается со шлюзом SAP для Майкрософт с помощью протокола SSL (HTTPS), но сервер "localhost:порт" все еще не настроен на доверие сертификату шлюза SAP для Майкрософт. Без этой строки кода перед открытием файла Default.aspx появлялось бы предупреждение о недействительном сертификате. В одних браузерах можно пропустить эту ошибку, а в других открыть файл Default.aspx будет невозможно.
    
  ```
    ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;
  ```

  > [!IMPORTANT] 
  > Удалите эту строку, когда вы будете готовы к развертыванию приложения ASP.NET для его размещения. См. раздел [Изменение и размещение надстройки в Azure и Office 365](#Stage).

5. Добавьте приведенный ниже код в метод **Page_Load**. Строка, передаваемая методу `GetSAPData`, — это запрос OData.
    
  ```
    if (!IsPostBack)
  {
      GetSAPData("DataCollection?$top=3");
  }
  ```

6. Добавьте следующий метод к классу Default. Этот метод сначала обеспечивает наличие в кэше действительного маркера доступа, полученного из Azure AD, а затем создает HTTP-запрос **GET**, который включает маркер доступа и отправляет его конечной точке OData SAP. Возвращаемый результат является объектом JSON, преобразованным в объект .NET **List**. В массиве, связанном с **DataListView**, используются три свойства элементов.
    
  ```
      private void GetSAPData(string oDataQuery)
    {
        AADAuthHelper.EnsureValidAccessToken(this);

        using (WebClient client = new WebClient())
        {
            client.Headers[HttpRequestHeader.Accept] = "application/json";
            client.Headers[HttpRequestHeader.Authorization] = "Bearer " + AADAuthHelper.AccessToken.Item1;
            var jsonString = client.DownloadString(SAP_ODATA_URL + oDataQuery);
            var jsonValue = JObject.Parse(jsonString)["d"]["results"];
            var dataCol = jsonValue.ToObject<List<Automobile>>();

            var dataList = dataCol.Select((item) => {
                return item.Brand + " " + item.Model + " " + item.Price;
                }).ToArray();

            DataListView.DataSource = dataList;
            DataListView.DataBind();
        }
    }

  ```


### <a name="to-create-the-user-interface"></a>Создание пользовательского интерфейса


1. Откройте файл Default.aspx и добавьте следующую разметку к объекту **form**:
    
    ```
      <div>
      <h3>Data from SAP via SAP Gateway for Microsoft</h3>

      <asp:ListView runat="server" ID="DataListView">
        <ItemTemplate>
          <tr runat="server">
            <td runat="server">
              <asp:Label ID="DataLabel" runat="server"
                Text="<%# Container.DataItem.ToString()%>" /><br />
            </td>
          </tr>
        </ItemTemplate>
      </asp:ListView>
    </div>
    ```

2. При желании вы можете придать веб-странице внешний вид страницы SharePoint с помощью [элемента управления хрома](use-the-client-chrome-control-in-sharepoint-add-ins.md) SharePoint и [таблицы стилей веб-сайта SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).
    
 
### <a name="to-test-the-add-in-with-f5-in-visual-studio"></a>Тестирование надстройки с помощью клавиши F5 в Visual Studio

1. Нажмите клавишу F5 в Visual Studio.   
 
2. После первого нажатия клавиши F5 вам может быть предложено войти на используемый сайт разработчика. Используйте учетные данные администратора. В нашем примере это учетная запись `Bob@<O365_domain>.onmicrosoft.com`.    
 
3. При первом нажатии клавиши F5 вам будет предложено предоставить надстройке разрешения. Нажмите кнопку **Доверять**.    
 
4. После краткой задержки для получения маркера доступа открывается страница Default.aspx. Убедитесь, что на ней отображаются данные SAP.
    

<a name="SharePoint"> </a> 

## <a name="add-sharepoint-access-to-the-aspnet-application-optional"></a>Предоставление приложению ASP.NET доступа к SharePoint (необязательно)

Конечно, надстройка SharePoint может не только выводить данные SAP на веб-странице, открытой из SharePoint. Она также может выполнять операции CRUD (создание, чтение, обновление и удаление) с данными из SharePoint. Для этого в коде можно использовать либо клиентскую объектную модель SharePoint (CSOM), либо интерфейсы REST API для SharePoint. CSOM развертывается в виде пары сборок, которые Инструменты разработчика Office для Visual Studio автоматически включают в проект ASP.NET, задавая параметр **Копировать локально** в Visual Studio, чтобы они добавлялись в пакет приложения ASP.NET. 

Общие сведения о CSOM см. в статье [Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint](complete-basic-operations-using-sharepoint-client-library-code.md). Общие сведения об использовании интерфейсов REST API см. в статье [Знакомство с REST-интерфейсом SharePoint 2013 и его использование](https://msdn.microsoft.com/ru-RU/magazine/dn198245.aspx). 

Независимо от того, используется ли CSOM или REST API для доступа к SharePoint, приложение ASP.NET должно получить маркер доступа к SharePoint, как и в случае шлюза SAP для Майкрософт. См. раздел [Общие сведения о проверке подлинности и авторизации в шлюзе SAP для Майкрософт и SharePoint](#AuthOverview) ранее в этой статье. 

Ниже представлены основные инструкции по выполнению этой задачи, но для начала рекомендуем ознакомиться со следующими статьями:

-  [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md)
-  [Авторизация и проверка подлинности для надстроек в SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)
-  [Три системы авторизации для надстроек SharePoint](three-authorization-systems-for-sharepoint-add-ins.md)   
-  [Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)    
-  [Поток OAuth токена контекста для надстроек SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md)   
 
### <a name="to-add-sharepoint-access-to-the-aspnet-application"></a>Предоставление приложению ASP.NET доступа к SharePoint

1. Откройте файл Default.aspx.cs и раскомментируйте метод **Page\_PreInit**. Кроме того, раскомментируйте код, который Инструменты разработчика Office для Visual Studio добавили к методу **Page\_Load**.

2. Если надстройка SharePoint будет получать доступ к данным SharePoint, необходимо кэшировать токен контекста SharePoint, отправляемый странице Default.aspx с помощью запроса POST при запуске надстройки в SharePoint. Это гарантирует, что токен контекста SharePoint не будет потерян при перенаправлении браузера после проверки подлинности в Azure AD. Кэшировать этот контекст можно несколькими способами. Инструменты разработчика Office для Visual Studio добавляют к проекту ASP.NET файл SharePointContext.cs, выполняющий большую часть работы. Чтобы использовать кэш сеанса, просто добавьте приведенный ниже код в блок `if (!IsPostBack)` *перед* кодом, который вызывает шлюз SAP для Майкрософт.
      
  ```
      if (HttpContext.Current.Session["SharePointContext"] == null) 
    {
        HttpContext.Current.Session["SharePointContext"]
            = SharePointContextProvider.Current.GetSharePointContext(Context);
    }
  ```

3. Файл SharePointContext.cs отправляет вызовы другому файлу, который Инструменты разработчика Office для Visual Studio добавляет к проекту: TokenHelper.cs. Этот файл содержит большую часть кода, необходимого для получения и использования маркеров доступа для SharePoint. Тем не менее, в нем отсутствует код для продления срока действия устаревшего маркера доступа или маркера обновления. Кроме того, в нем нет кода для кэширования маркеров. Если вы создаете профессиональную надстройку SharePoint, добавить этот код необходимо. Примером может служить логика кэширования из предыдущего этапа. Ваш код также должен кэшировать маркер доступа и продолжать использовать его до истечения срока действия. По истечении срока действия маркера код должен получить новый маркер доступа с помощью маркера обновления.
 
4. Добавьте вызовы данных из SharePoint с помощью CSOM или REST. Приведенный ниже пример представляет собой измененный код CSOM, который Инструменты разработчика Office для Visual Studio добавляют к методу **Page_Load**. В этом примере код был перемещен в отдельный метод и начинается с получения кэшированного токена контекста.
    
  ```
      private void GetSharePointTitle()
    {
        var spContext = HttpContext.Current.Session["SharePointContext"] as SharePointContext;
        using (var clientContext = spContext.CreateUserClientContextForSPHost())
        {
            clientContext.Load(clientContext.Web, web => web.Title);
            clientContext.ExecuteQuery();
            SharePointTitle.Text = "SharePoint web site title is: " + clientContext.Web.Title;
        }
    }
  ```

5. Добавьте элементы пользовательского интерфейса для отрисовки данных SharePoint. Ниже показан элемент управления HTML, на который ссылается предыдущий метод.
    
  ```HTML
    <h3>SharePoint title</h3><asp:Label ID="SharePointTitle" runat="server"></asp:Label><br />
  ```

  > [!NOTE] 
  > Во время отладки надстройки SharePoint Инструменты разработчика Office для Visual Studio заново регистрируют ее в Azure ACS при каждом нажатии клавиши F5 в Visual Studio. При размещении надстройки SharePoint необходимо выполнить долгосрочную регистрацию. См. раздел [Изменение и размещение надстройки в Azure и Office 365](#Stage).
 

<a name="Stage"> </a>

## <a name="modify-the-add-in-and-stage-it-to-azure-and-office-365"></a>Изменение и размещение надстройки в Azure и Office 365

Закончив отлаживать надстройку SharePoint с помощью клавиши F5 в Visual Studio, необходимо выполнить развертывание приложения ASP.NET в Веб-сайт Azure.

### <a name="to-create-the-azure-web-site"></a>Создание веб-сайта Azure

1. На портале Microsoft Azure выберите **ВЕБ-САЙТЫ** в левой области навигации.
    
2. Нажмите **СОЗДАТЬ** в нижней части страницы, а в диалоговом окне **СОЗДАНИЕ** выберите команды **ВЕБ-САЙТ** |**БЫСТРОЕ СОЗДАНИЕ**.
    
3. Введите доменное имя и нажмите кнопку **СОЗДАТЬ ВЕБ-САЙТ**. Скопируйте URL-адрес нового сайта. Он представлен в формате `my_domain.azurewebsites.net`.
    
 

### <a name="to-modify-the-code-and-markup-in-the-application"></a>Изменение кода и разметки в приложении

1. В Visual Studio удалите строку `ServicePointManager.ServerCertificateValidationCallback = (s, cert, chain, errors) => true;` из файла Default.aspx.cs.    
 
2. Откройте файл web.config проекта ASP.NET и замените доменную часть значения ключа **AppRedirectUrl** в разделе **appSettings** на домен Веб-сайт Azure. Например, замените `<add key="AppRedirectUrl" value="https://localhost:44322/Pages/Default.aspx" />` на `<add key="AppRedirectUrl" value="https://my_domain.azurewebsites.net/Pages/Default.aspx" />`.    
 
3. Щелкните правой кнопкой мыши файл AppManifest.xml в проекте надстройки SharePoint и выберите команду **Перейти к коду**.    
 
4. В значении **StartPage** замените строку `~remoteAppUrl` на полный домен веб-сайта Azure, включая протокол. Пример: `https://my_domain.azurewebsites.net`. Теперь полное значение **StartPage** должно выглядеть так: `https://my_domain.azurewebsites.net/Pages/Default.aspx` (как правило, значение **StartPage** полностью совпадает со значением ключа **AppRedirectUrl** в файле web.config).
    
 

### <a name="to-modify-the-azure-ad-registration-and-register-the-add-in-with-acs"></a>Изменение регистрационных данных в Azure AD и регистрация надстройки в службе контроля доступа

1. Войдите на [портал управления Azure](https://manage.windowsazure.com), используя учетную запись администратора Azure.    
 
2. Выберите **Active Directory** в левой части страницы.    
 
3. Выберите каталог.    
 
4. Выберите **ПРИЛОЖЕНИЯ** (на верхней панели навигации).    
 
5. Откройте созданное приложение. В нашем примере используется имя **ContosoAutomobileCollection**.    
 
6. В каждом из следующих значений замените фрагмент "localhost: *порт*" на значение домена нового веб-сайта Azure:
    
  - **URL-АДРЕС ДЛЯ ВХОДА**
      
  - **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ**
      
  - **URL-АДРЕС ОТВЕТА**
    
  Например, если для **URI ИДЕНТИФИКАТОРА ПРИЛОЖЕНИЯ** задано значение `https://localhost:44304/ContosoAutomobileCollection`, замените его на `https://<my_domain>.azurewebsites.net/ContosoAutomobileCollection`.
    
7. Нажмите кнопку **СОХРАНИТЬ** в нижней части экрана.
    
8. Зарегистрируйте надстройку в Azure ACS. Это необходимо сделать, даже если надстройка не получает доступ к SharePoint и не использует токены из ACS, так как в ходе этого процесса надстройка также регистрируется в службе управления надстройками для подписки на Office 365, что является обязательным условием. (Название "служба управления надстройками" связано с тем, что изначально надстройки SharePoint назывались "приложениями для SharePoint".) 

  Регистрация выполняется на странице AppRegNew.aspx любого веб-сайта SharePoint в подписке на Office 365. Подробные сведения см. в статье [Регистрация надстроек SharePoint](register-sharepoint-add-ins.md). 
  
  В рамках этого процесса вы получаете новые идентификатор и секрет клиента. Вставьте эти значения в файле web.config для ключей **ClientId** (не **ida:ClientID**) и **ClientSecret**.
    
  > [!WARNING] 
  > Если по той или иной причине вы нажмете клавишу F5 после внесения этого изменения, то Инструменты разработчика Office для Visual Studio заменят одно из этих значений или оба. По этой причине следует записывать значения, полученные на странице AppRegNew.aspx, и всегда проверять значения в файле web.config непосредственно перед публикацией приложения ASP.NET. 

### <a name="publish-the-aspnet-application-to-azure-and-install-the-add-in-to-sharepoint"></a>Публикация приложения ASP.NET в Azure и установка надстройки в SharePoint

1. Опубликовать приложение ASP.NET на веб-сайте Azure можно несколькими способами. Дополнительные сведения см. в статье [Развертывание локального репозитория Git в службе приложений Azure](https://docs.microsoft.com/ru-RU/azure/app-service/app-service-deploy-local-git).
    
2. В Visual Studio щелкните правой кнопкой мыши проект SharePoint и выберите команду **Упаковать**. На открывшейся странице **Публикация надстройки** нажмите **Упаковать надстройку**. Откроется проводник с папкой, содержащей пакет надстройки.    
 
3. Войдите в Office 365 от имени глобального администратора и перейдите к семейству веб-сайтов с каталогом надстроек организации. (Если такого семейства нет, создайте его. См. статью [Использование каталога приложений для развертывания пользовательских бизнес-приложений в среде SharePoint Online](https://support.office.com/en-us/article/Use-the-App-Catalog-to-make-custom-business-apps-available-for-your-SharePoint-Online-environment-0b6ab336-8b83-423f-a06b-bcc52861cba0?CorrelationId=40e9dc6b-213e-4496-8c5f-40ca27922fa1&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA102772362).)    
 
4. Отправьте пакет надстройки в каталог надстроек.    
 
5. Откройте на любом сайте подписки страницу **Контент сайта** и нажмите **Добавить надстройку**.    
 
6. На странице **Надстройки** найдите раздел **Надстройки, которые вы можете добавить** и выберите значок вашей надстройки.    
 
7. После установки надстройки щелкните ее значок на странице **Контент сайта**, чтобы запустить надстройку.    
 
Дополнительные сведения об установке надстроек SharePoint см. в статье [Развертывание и установка надстроек SharePoint: методы и параметры](deploying-and-installing-sharepoint-add-ins-methods-and-options.md).
 

## <a name="deploy-the-add-in-to-production"></a>Развертывание надстройки в рабочей среде

Завершив тестирование, вы можете развернуть надстройку в рабочей среде. Для этого может потребоваться внести некоторые изменения.

1. Если рабочий домен приложения ASP.NET отличается от промежуточного домена, необходимо изменить значение **AppRedirectUrl** в файле web.config и значение **StartPage** в файле AppManifest.xml, а затем заново упаковать надстройку SharePoint. См. раздел [Изменение кода и разметки в приложении](#to-modify-the-code-and-markup-in-the-application) ранее в этой статье.    
 
2. При изменении домена также необходимо изменить регистрационные данные надстроек в Azure AD. См. раздел [Изменение регистрационных данных в Azure AD и регистрация надстройки в службе контроля доступа](#to-modify-the-azure-ad-registration-and-register-the-add-in-with-acs) ранее в этой статье.    
 
3. Как упоминается в том же разделе, при изменении домена также требуется повторная регистрация надстройки в ACS (и службе управления надстройками для подписки). *Изменить* регистрационные данные надстройки в ACS невозможно. Однако создавать новые идентификатор и секрет клиента на странице AppRegNew.aspx необязательно. Вы можете скопировать исходные значения ключей **ClientId** (не **ida:ClientID**) и **ClientSecret** из файла web.config в новую форму AppRegNew. *Если вы все же создаете новые значения, обязательно скопируйте их в ключи в файле web.config.* 
    
 
## <a name="see-also"></a>См. также

- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)