---
title: Поток кода авторизации OAuth для надстроек SharePoint
description: Узнайте о потоке авторизации OAuth для надстроек, запрашивающих разрешение на доступ к ресурсам SharePoint во время работы, а также об использовании страницы OAuthAuthorize.aspx и URI перенаправления SharePoint.
ms.date: 12/28/2017
ms.prod: sharepoint
ms.openlocfilehash: 9877eddc41472ea1ddc2ba7b576c4294d927869a
ms.sourcegitcommit: 215ba2e6c1eb40cc5a4e07f87d11ade98df4ffd2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2017
---
# <a name="authorization-code-oauth-flow-for-sharepoint-add-ins"></a>Поток кода авторизации OAuth для надстроек SharePoint

> [!NOTE] 
> В этой статье предполагается, что вы ознакомились со статьей [Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization.md) и основными понятиями и принципами протокола OAuth. Дополнительные сведения об OAuth см. на сайте [OAuth.net](http://oauth.net/) и в [описании протокола веб-авторизации (OAuth)](http://datatracker.ietf.org/doc/active/#oauth).

В некоторых случаях надстройка может запрашивать разрешение на доступ к ресурсам SharePoint во время работы (динамически), а не во время установки. Такие надстройки не обязательно запускать из среды SharePoint или даже устанавливать в ней. Например, надстройка может быть встроена в устройство, запущена с какого-либо веб-сайта или из приложения Office, и ей может требоваться доступ к ресурсам SharePoint во время выполнения.

> [!NOTE] 
> Этот тип надстройки может быть запущен только пользователями с разрешениями "Управление" на всех ресурсах, к которым надстройка запрашивает доступ. Например, если надстройка запрашивает у веб-сайта только разрешение на чтение, пользователь, у которого для веб-сайта есть права на "чтение", но не "управление", не может запускать надстройку.

Чтобы вызывать SharePoint, такая надстройка должна быть зарегистрирована на Панели мониторинга продаж или странице appregnew.aspx. Дополнительные сведения о регистрации надстроек на Панели мониторинга продаж и странице appregnew.aspx см. в статье [Регистрация надстроек SharePoint](register-sharepoint-add-ins.md).

После регистрации надстройка становится *субъектом безопасности*, у которого есть удостоверение, как у пользователей и групп. Это удостоверение называется субъектом надстройки. Как и у пользователей и групп, у субъекта надстройки есть определенные разрешения. Дополнительные сведения о субъектах надстроек см. в статье [Регистрация надстроек SharePoint](register-sharepoint-add-ins.md).

После регистрации надстройки вы получите идентификатор и секрет клиента, домен надстройки и URI перенаправления для субъекта надстройки. Эти сведения регистрируются на сервере авторизации — службе контроля доступа Microsoft Azure (ACS).
 
<a name="Flow"> </a>
 
## <a name="authorization-code-oauth-flow-for-add-ins-that-request-permissions-on-the-fly"></a>Поток OAuth кода авторизации для надстроек, запрашивающих разрешения во время выполнения

В этом разделе представлена сводка потока проверки подлинности и авторизации OAuth для надстроек SharePoint, запрашивающих разрешения во время работы. Этот поток называется **потоком кода аутентификации**. Эта последовательность иллюстрирует, как надстройка, запущенная не из SharePoint, может получать доступ к ресурсам в SharePoint.

> [!NOTE] 
> Поток включает ряд взаимодействий между надстройкой, SharePoint, сервером авторизации (ACS) и пользователем во время работы. Таким образом, в этом потоке необходима ферма SharePoint Online или SharePoint, подключенная к Интернету, для взаимодействия с ACS. На фермах SharePoint, не подключенных к Интернету, следует использовать [систему авторизации с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization.md).
 
Необходимы приложение или служба, размещенные отдельно от SharePoint. Даже если надстройка привязана к устройству, ей необходим URL-адрес веб-приложения или службы, который можно зарегистрировать в ACS, даже если веб-компонент не используется для других целей. 

Для простоты в этой статье предполагается, что надстройка представляет собой веб-приложение под названием Contoso.com. Приложение использует клиентскую объектную модель SharePoint (CSOM) или интерфейсы REST API SharePoint для отправки вызовов среде SharePoint. Когда приложение впервые пытается получить доступ к среде SharePoint, последняя запрашивает из ACS код авторизации, который можно отправить приложению Contoso.com. Затем приложение использует этот код авторизации, чтобы запросить маркер доступа из ACS. Получив маркер доступа, приложение Contoso.com включает его во все свои запросы к SharePoint.
 

<a name="Fly"> </a> 

### <a name="detailed-example-of-the-flow"></a>Подробный пример потока

Допустим, компания Contoso предоставляет услуги фотопечати в Интернете. Пользователю нужно распечатать фотографии. Для этого он должен предоставить службе Contoso разрешение на доступ к фотографиям из библиотек на сайте SharePoint Online `fabrikam.sharepoint.com` и их печать.

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_0.png)
 
Приложение для фотопечати зарегистрировано, поэтому у него есть идентификатор и секрет клиента, а также URI перенаправления. URI перенаправления, предоставленный компанией Contoso при регистрации надстройки, — `https://contoso.com/RedirectAccept.aspx`. Идентификатор и секрет клиента хранятся в файле web.config приложения для фотопечати. Ниже представлен пример того, как идентификатор и секрет клиента вводятся в файле web.config.

```XML
    <configuration>
    <appSettings>
        <add key="ClientId" value="c78d058c-7f82-44ca-a077-fba855e14d38 "/>
        <add key="ClientSecret" value="SbALAKghPXTjbBiLQZP+GnbmN+vrgeCMMvptbgk7T6w= "/>
    </appSettings>
    </configuration>
```

### <a name="authentication-code-flow-steps"></a>Этапы потока кода аутентификации

Ниже перечислены этапы потока кода аутентификации.
 
> [!TIP] 
> Следующие действия ссылаются на методы в файле TokenHelper.cs (или TokenHelper.vb). Этот управляемый код не компилируется, поэтому для него справочные разделы недоступны. Однако сам файл подробно прокомментирован с описанием каждого класса, параметра члена и возвращаемого значения. Вы можете открыть его копию для справки при чтении следующих инструкций.

#### <a name="step-1-client-opens-an-application-and-then-directs-it-to-a-sharepoint-site-for-data"></a>Этап 1. Клиент открывает приложение, а затем переходит на сайт SharePoint для получения данных

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_1.png)

Пользователь открывает веб-сайт фотопечати Contoso. В его пользовательском интерфейсе указывается, что пользователь может печатать фотографии, хранящиеся на любом сайте SharePoint Online.

В этом примере используется URL-адрес `https://contoso.com/print/home.aspx`.

Надстройка для фотопечати предлагает пользователю ввести URL-адрес коллекции фотографий. Пользователь вводит URL-адрес, указывающий на сайт SharePoint Online: `https://fabrikam.sharepoint.com/`.

<a name="FlowStep2"> </a> 

#### <a name="step-2-the-add-in-redirects-to-the-sharepoint-site-authorization-url"></a>Этап 2. Надстройка перенаправляется на URL-адрес авторизации сайта SharePoint

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_2.png)

Когда пользователь нажимает кнопку для получения фотографий, надстройка фотопечати Contoso перенаправляет браузер на URL-адрес `https://fabrikam.sharepoint.com/`. Это отклик HTTP 302 Redirect.

Если вы используете Microsoft .NET, **Response.Redirect** лишь один из нескольких способов перенаправления, которые можно использовать в коде. Используя файл TokenHelper (с расширением CS или VB) в проекте, ваш код может вызвать перегруженный метод **GetAuthorizationUrl** (используя перегрузку с тремя аргументами). Он создает URL-адрес перенаправления OAuthAuthorize.aspx автоматически. С помощью вашего кода также можно сформировать URL-адрес вручную. 

Например, если вы вызываете метод **GetAuthorizationUrl** для создания URL-адреса OAuthAuthorize.aspx, используя файл TokenHelper.cs (или TokenHelper.vb) в проекте, код будет следующим: `Response.Redirect(TokenHelper.GetAuthorizationUrl(` `sharePointSiteUrl.ToString(), "Web.Read List.Write", "https://contoso.com/RedirectAccept.aspx"));`.

Взглянув на перегрузку метода **GetAuthorizationUrl** с тремя параметрами в файле TokenHelper.cs (или TokenHelper.vb), вы увидите, что второй параметр задает область разрешений — разделенный пробелами список разрешений, запрашиваемых надстройкой, в сокращенном формате. Дополнительные сведения об областях разрешений см. в разделе [Псевдонимы областей разрешений и использование страницы OAuthAuthorize.aspx](#Scope).

Третьим параметром должен быть тот же URI перенаправления, который использовался при регистрации надстройки. Дополнительные сведения о регистрации см. в статье [Регистрация надстроек SharePoint](register-sharepoint-add-ins.md). Возвращаемая строка представляет собой URL-адрес, включающий параметры строки запроса. При желании вы можете вручную составить URL-адрес перенаправления для страницы OAuthAuthorize.aspx. Например, надстройка для фотопечати Contoso перенаправляет пользователя на следующий URL-адрес: `https://fabrikam.sharepoint.com/_layouts/15/OAuthAuthorize.aspx?client_id=client_GUID&amp;scope=app_permissions_list&amp;response_type=code&amp;redirect_uri=redirect_uri`.

Как видно из примера, надстройка для фотопечати Contoso отправляет идентификатор клиента OAuth и URI перенаправления на сайт Fabrikam в качестве параметров строки запроса. Ниже представлен образец запроса GET с примерами значений в строке запроса. Для удобства добавлены разрывы строк. Фактический целевой URL-адрес представляет собой одну строку. `GET /authcode HTTP/1.1`  `Host: fabrikam.sharepoint.com`   `/oauthauthorize.aspx`  `?client_id= c78d058c-7f82-44ca-a077-fba855e14d38`  `&amp;scope=list.read`  `&amp;response_type=code`  `&amp;redirect_uri= https%3A%2F%2Fcontoso%2Ecom%2Fredirectaccept.aspx`

Чтобы использовать для подтверждения отдельное всплывающее диалоговое окно, можно добавить параметр запроса **IsDlg=1** в URL-адрес, как показано здесь: `/oauthauthorize.aspx?IsDlg=1&amp;client_id= c78d058c-7f82-44ca-a077-fba855e14d38&amp;scope=list.read&amp;response_type=code&amp;redirect_uri= https%3A%2F%2Fcontoso%2Ecom%2Fredirectaccept.aspx`.


#### <a name="step-3-sharepoint-displays-the-consent-page-so-the-user-can-grant-the-add-in-permissions"></a>Этап 3. В SharePoint отображается страница подтверждения для предоставления надстройке разрешений

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_3.png)

Если пользователь еще не вошел на сайт Fabrikam в SharePoint Online, ему предлагается сделать это. Если пользователь вошел, то в SharePoint отображается HTML-страница подтверждения. На странице согласия пользователю предлагается предоставить надстройке для фотопечати Contoso запрашиваемые разрешения (или отказать ей). В данном случае пользователь предоставляет надстройке доступ на чтение к библиотеке изображений пользователя на сайте Fabrikam.

#### <a name="step-4-sharepoint-requests-a-short-lived-authorization-code-from-acs"></a>Этап 4. SharePoint запрашивает временный код авторизации у службы контроля доступа

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_4.png)

Сайт SharePoint Online компании Fabrikam запрашивает у службы контроля доступа создание кратковременного (приблизительно 5 минут) кода авторизации, который является уникальным для этой комбинации пользователя и надстройки. ACS отправляет код авторизации на сайт Fabrikam.

#### <a name="step-5-the-sharepoint-online-site-redirects-to-the-apps-registered-redirect-uri-passing-the-authorization-code-to-the-add-in"></a>Этап 5. Сайт SharePoint Online перенаправляется на зарегистрированный URI перенаправления надстройки, передавая ей код авторизации

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_5.png)

Сайт Fabrikam в SharePoint Online перенаправляет браузер в надстройку Contoso с помощью отклика HTTP 302. URL-адрес для этого перенаправления создается с использованием URI перенаправления, указанного при регистрации надстройки для фотопечати. Он также содержит код авторизации в виде строки запроса.

URL-адрес перенаправления имеет следующую структуру: `https://contoso.com/RedirectAccept.aspx?code=<authcode>`.

#### <a name="step-6-the-add-in-uses-the-authorization-code-to-request-an-access-token-from-acs-which-validates-the-request-invalidates-the-authorization-code-and-then-sends-access-and-refresh-tokens-to-the-add-in"></a>Этап 6. Надстройка использует код авторизации, чтобы запросить маркер доступа у службы контроля доступа, которая проверяет запрос, прекращает действие кода авторизации и отправляет маркеры доступа и обновления надстройке

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_6.png)

Contoso получает код авторизации из параметра запроса и включает его вместе с идентификатором и секретом клиента в запрос маркера доступа, отправляемый службе контроля доступа.

Если вы используете управляемый код и SharePoint CSOM, файл TokenHelper.cs (или TokenHelper.vb), то отправлять запрос к ACS будет метод **GetClientContextWithAuthorizationCode**. В этом случае код выглядит примерно так (где `authCode` — это переменная, которой назначен код авторизации): `TokenHelper.GetClientContextWithAuthorizationCode(`  `"https://fabrikam.sharepoint.com/",`  `"00000003-0000-0ff1-ce00-000000000000",`  `authCode,`  `"1ee82b34-7c1b-471b-b27e-ff272accd564",`  `new Uri(Request.Url.GetLeftPart(UriPartial.Path)));`.

В файле TokenHelper.cs (или TokenHelper.vb) вторым параметром метода **GetClientContextWithAuthorizationCode** является `targetPrincipalName`. В надстройках, получающих доступ к SharePoint, его значение всегда равно `00000003-0000-0ff1-ce00-000000000000`. При трассировке иерархии вызовов из метода **GetClientContextWithAuthorizationCode** вы увидите, что он получает идентификатор и секрет клиента из файла web.config. 

ACS получает запрос от Contoso, а затем проверяет идентификатор и секрет клиента, URI перенаправления и код авторизации. Если они действительны, ACS делает код авторизации недействительным (его можно использовать только один раз) и создает маркеры обновления и доступа, а затем отправляет их надстройке Contoso. Приложение Contoso может кэшировать этот маркер доступа для использования в последующих запросах. По умолчанию срок действия маркеров доступа составляет около 12 часов.

Каждый маркер доступа связан с учетной записью, указанной в исходном запросе авторизации, и предоставляет доступ только к тем службам, которые указаны в этом запросе. Надстройка должна надежно хранить этот маркер доступа. Приложение Contoso также может кэшировать маркер обновления. По умолчанию срок действия маркеров обновления составляет 6 месяцев. По истечении срока действия старого маркера доступа от ACS вы можете получить новый с помощью маркера обновления. 

Дополнительные сведения о маркерах см. в статье [Обработка маркеров безопасности в надстройках SharePoint с низким уровнем доверия, размещенных у поставщика](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins.md).

#### <a name="step-7-the-add-in-can-now-use-the-access-token-to-request-data-from-the-sharepoint-site-which-it-can-display-to-the-user"></a>Этап 7. Теперь с помощью маркера доступа надстройка может запрашивать данные с сайта SharePoint, а затем показывать их пользователю

![OAuth](../images/SharePoint_appsForSharePoint_3LeggedOauthFlow_7.png)

Contoso включает маркер доступа для вызова REST API или запроса CSOM к SharePoint, передавая маркер доступа OAuth в заголовке HTTP **Authorization**. SharePoint возвращает сведения, запрашиваемые надстройкой Contoso. 

Дополнительные сведения о том, как отправляется этот запрос, см. в статье [Обработка маркеров безопасности в надстройках SharePoint с низким уровнем доверия, размещенных у поставщика](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins.md).



<a name="Scope"> </a>

## <a name="permission-scope-aliases-and-the-oauthauthorizeaspx-page"></a>Псевдонимы областей разрешений и страница OAuthAuthorize.aspx

В этом разделе предполагается, что вы уже ознакомились со статьей [Разрешения надстроек в SharePoint](add-in-permissions-in-sharepoint.md). В таблице 1 показаны URI областей запросов разрешений для надстроек, описанные в этой статье, а также дополнительный столбец (**Псевдоним области**). Право FullControl недоступно в столбце **Доступные права**, так как надстройка, запрашивающая разрешение на доступ к ресурсам SharePoint во время выполнения, не может запросить право на полный доступ.

Значения, указанные в столбце **Псевдоним области**, представляют собой сокращенные версии их аналогов из столбца **URI области**. Псевдонимами могут пользоваться только надстройки, запрашивающие разрешение на доступ к ресурсам SharePoint во время выполнения. Значение URI областей используются в манифестах надстроек, запускаемых из SharePoint. Такие надстройки запрашивают разрешения во время установки.

Псевдонимы областей используются только в контексте страницы перенаправления OAuthAuthorize.aspx. Как показано на [этапе 2 потока OAuth](#FlowStep2), описанном в предыдущем разделе, если надстройка использует управляемый код, то псевдонимы используются при вызове метода **GetAuthorizationUrl** из файла TokenHelper.cs (или TokenHelper.vb) вашего проекта. Ниже представлен еще один пример. 

```C#
Response.Redirect(TokenHelper.GetAuthorizationUrl(
    sharePointSiteUrl.ToString(), 
    "Web.Read List.Write ", 
    "https://contoso.com/RedirectAccept.aspx "));
```

Значение параметра _scope_, `Web.Read List.Write`, представляет собой пример запроса разрешений с помощью псевдонимов областей. Параметр _scope_ — это разделенный пробелами набор, состоящий из области разрешений и запрашиваемых прав.

Если вы не используете управляемый код, в поле области URL-адреса перенаправления используются псевдонимы областей. Пример:

`https://fabrikam.sharepoint.com/_layout/15/OAuthAuthorize.aspx?client_id=c78d058c-7f82-44ca-a077-fba855e14d38&amp;scope=list.write&amp;response_type=code&amp;redirect_uri=https%3A%2F%2Fcontoso%2Ecom%2Fredirectaccept.aspx`

> [!NOTE] 
> Описание областей см. в статье [Разрешения надстроек в SharePoint](add-in-permissions-in-sharepoint.md).
 
<br/>

**Таблица 1. URI областей разрешений для надстроек SharePoint и соответствующие псевдонимы**

|**URI области**|**Псевдоним области**|**Доступные права**|
|:-----|:-----|:-----|
|http://sharepoint/content/sitecollection|Сайт|Чтение, запись, управление|
|http://sharepoint/content/sitecollection/web|Веб|Чтение, запись, управление|
|http://sharepoint/content/sitecollection/web/list|Перечисление|Чтение, запись, управление|
|http://sharepoint/content/tenant|AllSites|Чтение, запись, управление|
|http://sharepoint/bcs/connection|Нет (сейчас не поддерживается)|Чтение|
|http://sharepoint/search|Поиск|QueryAsUserIgnoreAppPrincipal|
|http://sharepoint/projectserver|ProjectAdmin |Управление|
|http://sharepoint/projectserver/projects|Проекты|Чтение, запись|
|http://sharepoint/projectserver/projects/project|Project |Чтение, запись|
|http://sharepoint/projectserver/enterpriseresources|ProjectResources|Чтение, запись|
|http://sharepoint/projectserver/statusing|ProjectStatusing|SubmitStatus|
|http://sharepoint/projectserver/reporting|ProjectReporting|Чтение|
|http://sharepoint/projectserver/workflow|ProjectWorkflow|Повышение прав|
|http://sharepoint/social/tenant|AllProfiles|Чтение, запись, управление|
|http://sharepoint/social/core|Сообщество|Чтение, запись, управление|
|http://sharepoint/social/microfeed|Microfeed|Чтение, запись, управление|
|http://sharepoint/taxonomy|TermStore|Чтение, запись|


<a name="RedirectURI"> </a>

## <a name="redirect-uris-and-a-sample-redirect-page"></a>URI перенаправления и пример страницы перенаправления

URI перенаправления, используемый надстройками, который запрашивают разрешения во время выполнения, — это URI, на который SharePoint перенаправляет браузер после предоставления согласия (с кодом авторизации в виде параметра запроса). На [этапе 2 потока OAuth](#FlowStep2) представлен пример жестко заданного URI в вызове метода **GetAuthorizationUrl**. Кроме того, надстройка ASP.NET также может хранить URI в файле web.config, как показано в следующем примере:

```XML
    <configuration>
        <appSettings>
            <add key="RedirectUri" value="https://contoso.com/RedirectAccept.aspx" />
        </appSettings>
    <configuration>
```

Это значение можно получить, вызвав метод `WebConfigurationManager.AppSettings.Get("RedirectUri")`.

Конечная точка, соответствующая URI перенаправления, получает код авторизации из параметра запроса и получает с его помощью маркер доступа, который затем можно использовать для доступа к SharePoint. Как правило, конечной точкой является та же страница (либо метод контроллера или веб-метод), которая изначально пыталась получить доступ к SharePoint. Однако это могут быть страница или метод, которые просто получают маркер авторизации, а затем выполняют перенаправление на другую страницу или в другой метод. Специальные страница или метод могут передать маркер авторизации или кэшировать его. Срок действия маркера составляет около 5 минут. Вы также можете использовать маркер авторизации, чтобы получить маркер доступа, который будет кэширован.

Ниже приведен пример кода такой страницы в приложении ASP.NET. Обратите внимание на следующие особенности этого кода:

- В нем используется файл TokenHelper.cs, который создают Инструменты разработчика Office для Visual Studio.

- В коде предполагается, что существует параметр запроса "code", содержащий код авторизации. Это безопасно, так как страницу вызывает только SharePoint и только при передаче кода авторизации.

- В нем используется клиентский объект контекста CSOM для доступа к SharePoint, но можно также просто кэшировать этот объект на сервере и перейти на другую страницу.

- Метод **GetClientContextWithAuthorizationCode** использует код авторизации, чтобы получить код доступа. Затем он создает объект контекста клиента SharePoint и меняет обработчик события **ExecutingWebRequest** в этом объекте, чтобы этот обработчик включал маркер доступа во все запросы к SharePoint. Маркер доступа, по сути, кэшируется в объекте.

- Метод **GetClientContextWithAuthorizationCode** отправляет службе контроля доступа URL-адрес перенаправления в параметре `rUrl`, но служба контроля доступа использует его для идентификации в случае кражи кода авторизации. Служба контроля доступа не использует его для повторного перенаправления, поэтому он не создает бесконечный цикл из-за перенаправления на себя.

- В коде не предусмотрена обработка просроченных маркеров доступа. Создав объект контекста клиента, он использует один и тот же маркер доступа. Маркер обновления не используется вообще. Это приемлемо для надстроек, продолжительность сеансов использования которых не превышает срок действия маркера доступа.

Более сложный пример использования маркера обновления для получения нового маркера доступа см. в следующем разделе.

```C#
public partial class RedirectAccept : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        string authCode = Request.QueryString["code"];
        Uri rUri = new Uri("https://contoso.com/RedirectAccept.aspx");

        using (ClientContext context = TokenHelper.GetClientContextWithAuthorizationCode(
            "https://fabrikam.sharepoint.com/", 
            "00000003-0000-0ff1-ce00-000000000000",
            authCode,
            "1ee82b34-7c1b-471b-b27e-ff272accd564".
            rUri))
       {
           context.Load(context.Web);
           context.ExecuteQuery();

           Response.Write("<p>" + context.Web.Title + "</p>");
       }
    }
}

```

<br/>

<a name="Default"> </a>

## <a name="sample-code-behind-for-a-page-that-accesses-sharepoint"></a>Пример кода страницы, получающей доступ к SharePoint

Ниже приведен код страницы Default.aspx. Эта страница рассчитана на сценарий, в котором страницей по умолчанию является начальная страница надстройки, которая также является зарегистрированным URL-адресом перенаправления для надстройки. Обратите внимание на следующие особенности этого кода:

- Метод **Page_Load** сначала проверяет наличие кода авторизации в строке запроса. Он существует, если браузер был перенаправлен на страницу средой SharePoint. Если код присутствует, с его помощью метод получает новый маркер обновления, который сохраняется в надежном кэше, рассчитанном на множество сеансов.

- Затем метод проверяет наличие маркера обновления в кэше. 
    
    - Если такого маркера нет, метод получает его, передавая SharePoint требуемые разрешения (разрешение на запись в области веб-сайтов) и запрашивая код авторизации у SharePoint. Пользователю предлагается предоставить разрешение. Если пользователь его предоставит, SharePoint получит код авторизации от службы контроля доступа и отправит его как параметр запроса в перенаправлении на эту же страницу.
    
    - При наличии кэшированного маркера обновления метод использует его, чтобы получить маркер доступа непосредственно из ACS. Как показано в примере в конце предыдущего раздела этой статьи, маркер доступа используется при создании объекта контекста клиента SharePoint. При использовании кэшированного маркера обновления для получения маркера доступа непосредственно из ACS отсутствует необходимость в дополнительном сетевом вызове SharePoint в начале сеанса. По этой причине, если повторно запустить надстройку, пока не истечет срок действия кэша с маркером обновления, то она запустится быстрее.

- Как и пример в конце предыдущего раздела, этот код не предусматривает обработку просроченного маркера доступа. Создав объект контекста клиента, он использует один и тот же маркер доступа. Один из способов защиты от просроченных маркеров доступа — кэшировать не только маркер обновления, но и маркер доступа. Затем следует изменить приведенный ниже код, чтобы он вызывал метод **GetAccessToken** только при отсутствии действительного маркера доступа к кэше. 
    
    Несмотря на то что маркер обновления можно кэшировать, к примеру, в файле cookie в клиенте, из соображений безопасности маркер доступа должен храниться исключительно в кэше на стороне сервера. Маркер обновления шифруется, и расшифровать его может только ACS. Однако маркер доступа только кодируется (в кодировке Base 64), и может быть легко раскодирован путем активного вмешательства в соединение.

- Ниже в этом разделе представлено определение класса **TokenCache**, на который ссылается этот код.

**Код страницы Default.aspx**

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Microsoft.SharePoint.Samples;
using Microsoft.SharePoint.Client;

namespace DynamicAppPermissionRequest
{
    public partial class Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            Uri sharePointSiteUrl = new Uri("https://fabrikam.sharpoint.com/print/");

            if (Request.QueryString["code"] != null)
            {
                TokenCache.UpdateCacheWithCode(Request, Response, sharePointSiteUrl);
            }

            if (!TokenCache.IsTokenInCache(Request.Cookies))
            {
                Response.Redirect(TokenHelper.GetAuthorizationUrl(sharePointSiteUrl.ToString(), 
                                                                  "Web.Write"));
            }
            else
            {
                string refreshToken = TokenCache.GetCachedRefreshToken(Request.Cookies);
                string accessToken = 
                TokenHelper.GetAccessToken(
                           refreshToken, 
                           "00000003-0000-0ff1-ce00-000000000000", 
                           sharePointSiteUrl.Authority, 
                           TokenHelper.GetRealmFromTargetUrl(sharePointSiteUrl)).AccessToken;

                using (ClientContext context = 
                       TokenHelper.GetClientContextWithAccessToken(sharePointSiteUrl.ToString(), 
                                                                   accessToken))
                {
                    context.Load(context.Web);
                    context.ExecuteQuery();

                    Response.Write("<p>" + context.Web.Title + "</p>");
                }
            }
        }
    }
}
```

<br/>

Ниже приведен пример кода для модуля кэширования маркера, вызываемого в предыдущем примере кода. Он использует файлы cookie в качестве кэша. Существуют и другие варианты кэширования. Дополнительные сведения см. в статье [Обработка маркеров безопасности в надстройках SharePoint с низким уровнем доверия, размещенных у поставщика](handle-security-tokens-in-provider-hosted-low-trust-sharepoint-add-ins.md).

**Пример кода для модуля кэширования маркера**

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using Microsoft.SharePoint.Samples;

namespace DynamicAppPermissionRequest
{
    public static class TokenCache
    {
        private const string REFRESH_TOKEN_COOKIE_NAME = "RefreshToken";

        public static void UpdateCacheWithCode(HttpRequest request, 
                                               HttpResponse response, 
                                               Uri targetUri)
        {
            string refreshToken = 
                TokenHelper.GetAccessToken(
                    request.QueryString["code"], 
                    "00000003-0000-0ff1-ce00-000000000000", 
                    targetUri.Authority, 
                    TokenHelper.GetRealmFromTargetUrl(targetUri), 
                    new Uri(request.Url.GetLeftPart(UriPartial.Path)))
                   .RefreshToken;
            SetRefreshTokenCookie(response.Cookies, refreshToken);
            SetRefreshTokenCookie(request.Cookies, refreshToken);
        }

        internal static string GetCachedRefreshToken(HttpCookieCollection requestCookies)
        {
            return GetRefreshTokenFromCookie(requestCookies);
        }

        internal static bool IsTokenInCache(HttpCookieCollection requestCookies)
        {
            return requestCookies[REFRESH_TOKEN_COOKIE_NAME] != null;
        }

        private static string GetRefreshTokenFromCookie(HttpCookieCollection cookies)
        {
            if (cookies[REFRESH_TOKEN_COOKIE_NAME] != null)
            {
                return cookies[REFRESH_TOKEN_COOKIE_NAME].Value;
            }
            else
            {
                return null;
            }
        }

        private static void SetRefreshTokenCookie(HttpCookieCollection cookies, 
                                                  string refreshToken)
        {
            if (cookies[REFRESH_TOKEN_COOKIE_NAME] != null)
            {
                cookies[REFRESH_TOKEN_COOKIE_NAME].Value = refreshToken;
            }
            else
            {
                HttpCookie cookie = new HttpCookie(REFRESH_TOKEN_COOKIE_NAME, 
                                                   refreshToken);
                cookie.Expires = DateTime.Now.AddDays(30);
                cookies.Add(cookie);
            }
        }
    }
}

```

<br/>

## <a name="see-also"></a>См. также

- [Настройка локальной среды разработки надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)
- [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md)
- [Создание надстроек SharePoint, использующих авторизацию с низким уровнем доверия](creating-sharepoint-add-ins-that-use-low-trust-authorization.md)
- [Авторизация и проверка подлинности для надстроек в SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)


    
 
