
# <a name="troubleshooting-high-trust-sharepoint-add-ins"></a><span data-ttu-id="0a87c-101">Устранение неполадок надстроек SharePoint с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="0a87c-101">Troubleshooting high-trust SharePoint Add-ins</span></span>
<span data-ttu-id="0a87c-102">Описание решений некоторых проблем, возникающих при разработке надстроек SharePoint с высоким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="0a87c-102">Get some help with problems developing high-trust spappplural.</span></span>
 

 <span data-ttu-id="0a87c-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="0a87c-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="0a87c-106">В этой статье описывается средство Fiddler, а также представлены рекомендации по устранению некоторых конкретных проблем.</span><span class="sxs-lookup"><span data-stu-id="0a87c-106">This article describes the Fiddler tool and also provides some guidance for resolving some specific issues.</span></span>
 

## <a name="use-the-fiddler-tool"></a><span data-ttu-id="0a87c-107">Использование средства Fiddler</span><span class="sxs-lookup"><span data-stu-id="0a87c-107">Use the Fiddler tool</span></span>

<span data-ttu-id="0a87c-p102">С помощью бесплатного  [средства Fiddler](http://www.telerik.com/fiddler) можно захватывать HTTP-запросы, отправляемые удаленным компонентом вашей надстройки в SharePoint. Для этого [средства есть бесплатное расширение](https://github.com/andrewconnell/SPOAuthFiddlerExt), которое автоматически декодирует маркеры доступа в запросах.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p102">The free  [Fiddler tool](http://www.telerik.com/fiddler) can be used to capture the HTTP Requests sent by the remote component of your add-in to SharePoint. There is a [free extension to the tool](https://github.com/andrewconnell/SPOAuthFiddlerExt) that automatically decodes the access tokens in the requests.</span></span>
 

 
<span data-ttu-id="0a87c-p103">Установив Fiddler на сервере веб-приложений, добавьте в файл web.config следующую разметку, чтобы запросы удаленного веб-приложения проходили через данный прокси-сервер. Таким образом вы сможете отследить трассировку Fiddler и целиком увидеть отклик SharePoint при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p103">After you have installed Fiddler on the web application server, add the following markup to your web.config file to make requests from your remote web app go through this proxy. This way, you can capture a Fiddler trace and see the full response from SharePoint when you get an error.</span></span>
 

 

 <span data-ttu-id="0a87c-p104">**Примечание.** Если вы не используете Fiddler, обязательно удалите эту разметку. В противном случае ваша надстройка не сможет выполнять HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p104">**Note** Ensure that you remove this markup if you are not running Fiddler. If you don't remove the markup, your add-in won't be able to make HTTP requests.</span></span>
 




```XML
<system.net>
  <defaultProxy>
    <proxy usesystemdefault="False" bypassonlocal="False" proxyaddress="http://127.0.0.1:8888" />
  </defaultProxy>
</system.net>

```

<span data-ttu-id="0a87c-p105">Установив Fiddler, вы можете проверить заголовки ответов от SharePoint, включая GUID запроса. Данный GUID запроса идентификатор корреляции, с помощью которого можно находить в журналах ошибки, связанные с этим запросом.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p105">After you have Fiddler installed, you can also check the response headers from SharePoint, which will include a request GUID. This request GUID is a correlation ID you can look up in the logs to find any log errors associated with that request.</span></span>
 

 

## <a name="401-unauthorized-error"></a><span data-ttu-id="0a87c-116">Ошибка "401 - Не санкционировано"</span><span class="sxs-lookup"><span data-stu-id="0a87c-116">401 Unauthorized error</span></span>
<span data-ttu-id="0a87c-117"><a name="UnauthorizedException"> </a></span><span class="sxs-lookup"><span data-stu-id="0a87c-117"></span></span>

<span data-ttu-id="0a87c-p106">Ошибка авторизации **401 - Не санкционировано** может возникать по нескольким причинам, когда надстройка с высоким уровнем доверия впервые обращается к SharePoint. Если вы используете клиентскую объектную модель (CSOM), ошибка выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="0a87c-p106">Several things can cause a **401 Unauthorized** error when the high-trust add-in first accesses SharePoint. If you are using the Client-side Object Model (CSOM), the error looks something like the following:</span></span>
 

 

```C#
[WebException: The remote server returned an error: (401) Unauthorized.]
   System.Net.HttpWebRequest.GetResponse() +8515936
   Microsoft.SharePoint.Client.SPWebRequestExecutor.Execute() +178
   Microsoft.SharePoint.Client.ClientRequest.ExecuteQueryToServer(ChunkStringBuilder sb) +1427
   Microsoft.SharePoint.Client.ClientRequest.ExecuteQuery() +270
   Microsoft.SharePoint.Client.ClientRuntimeContext.ExecuteQuery() +146
   Microsoft.SharePoint.Client.ClientContext.ExecuteQuery() +666
   S2STestWeb.Default.Page_Load(Object sender, EventArgs e) in c:\MyFiles\HightrustTest\HightrustTestWeb\Default.aspx.cs:28
   System.Web.UI.Control.LoadRecursive() +71
   System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint) +3178
```

<span data-ttu-id="0a87c-120">При использовании файла TokenHelper и удостоверения Windows код, вызывающий исключение, выглядит так:</span><span class="sxs-lookup"><span data-stu-id="0a87c-120">If you are using the TokenHelper file and Windows identity, the code that triggers the exception looks like the following:</span></span>
 

 



```C#
ClientContext clientContext = 
    TokenHelper.GetS2SClientContextWithWindowsIdentity(sharepointUrl, Request.LogonUserIdentity); 
clientContext.Load(clientContext.Web);
clientContext.ExecuteQuery();
```

<span data-ttu-id="0a87c-p107">Чтобы устранить эту проблему, в первую очередь необходимо с помощью отладчика Visual Studio проверить, успешно ли созданы маркер доступа и объект **ClientContext**. Если это так, необходимо проверить описанные ниже возможности.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p107">Your first step in troubleshooting the issue is to use the Visual Studio debugger to verify that the access token and the **ClientContext** object are constructed successfully. If they are, investigate the following possibilities:</span></span>
 

 
 <span data-ttu-id="0a87c-123">**Возможные проблемы и способы их решения.**</span><span class="sxs-lookup"><span data-stu-id="0a87c-123">**Possible issues and resolution:**</span></span>
 

 

- <span data-ttu-id="0a87c-p108">Для пользователя, обращающегося к удаленному веб-приложению, не создан профиль. Создайте профиль пользователя.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p108">There is no user profile created for the user who is accessing the remote web application. Create the user profile.</span></span>
    
 
- <span data-ttu-id="0a87c-p109">У вашей надстройки отсутствует разрешение на ресурсы, к которым вы собираетесь получить доступ. Откройте Командная консоль SharePoint и запустите следующий командлет Windows PowerShell. Переменная  `$web` представляет веб-сайт SharePoint, к которому вы пытаетесь получить доступ, а `$appPrincipal` идентификатор надстройки. Дополнительные сведения см. в статье [Set-SPAppPrincipalPermission](http://technet.microsoft.com/en-us/library/jj219714%28v=office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a87c-p109">Your add-in does not have permission to the resource you are trying to access. Open the SharePoint Management Shell and run that the following Windows PowerShell cmdlet. The variable  `$web` is the SharePoint website you are trying to get access to and `$appPrincipal`) is the add-in ID. For more information, see  [Set-SPAppPrincipalPermission](http://technet.microsoft.com/en-us/library/jj219714%28v=office.15%29.aspx).</span></span>
    
```
  Set-SPAppPrincipalPermission -Site $web -AppPrincipal $appPrincipal -Scope Site -Right FullControl
```

- <span data-ttu-id="0a87c-p110">Ваше веб-приложение принимает анонимные запросы. Это значит, что в маркере доступа нет действительного удостоверения пользователя. Убедитесь, что в службах IIS для корневого каталога вашего удаленного веб-приложения отключен анонимный доступ. Это также можно проверить, выполнив отладку удаленного веб-приложения и проверив значение **Request.LogonUserIdentity** в файле default.aspx (с расширением CS или VB), чтобы убедиться, что пользователь не является анонимным.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p110">Your web application is accepting anonymous requests. This means there is not a real user identity in the access token. Ensure that anonymous access has been disabled in IIS for the root directory of your remote web application. You can also check this by debugging your remote web application, and checking the value of **Request.LogonUserIdentity** in the default.aspx.cs (or .vb) file to ensure that it's not an anonymous user.</span></span>
    
 
- <span data-ttu-id="0a87c-p111">Цифровой сертификат не был добавлен в хранилище доверенных сертификатов. Обязательно выполните процедуры, описанные в статье  [Упаковка и публикация надстроек с высоким уровнем доверия для SharePoint](package-and-publish-high-trust-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="0a87c-p111">Your digital certificate was not added to the trusted certificate store. Be sure you have followed the procedures in  [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins).</span></span>
    
 

## <a name="miscellaneous-ssl-and-domain-related-authorization-errors"></a><span data-ttu-id="0a87c-136">Прочие ошибки авторизации, связанные с протоколом SSL и доменами</span><span class="sxs-lookup"><span data-stu-id="0a87c-136">Miscellaneous SSL and domain-related authorization errors</span></span>
<span data-ttu-id="0a87c-137"><a name="DomainRelatedErrors"> </a></span><span class="sxs-lookup"><span data-stu-id="0a87c-137"></span></span>

<span data-ttu-id="0a87c-p112">Авторизации может препятствовать несовпадение доменных имен в файлах конфигурации и регистрационных формах. Следующие четыре значения должны полностью совпадать:</span><span class="sxs-lookup"><span data-stu-id="0a87c-p112">A mismatch of domain names in configuration files and registration forms can prevent authorization. The following four values have to be exactly the same:</span></span>
 

 

- <span data-ttu-id="0a87c-140">**Домен надстройки**, который указывается при регистрации надстройки SharePoint на странице AppRegNew.aspx.</span><span class="sxs-lookup"><span data-stu-id="0a87c-140">The **Add-in Domain** that is specified when the SharePoint Add-in is registered on AppRegNew.aspx.</span></span>
    
 
- <span data-ttu-id="0a87c-141">Домен, на котором зарегистрирован сертификат безопасности удаленного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0a87c-141">The domain under which the remote web application's security certificate is registered.</span></span>
    
 
- <span data-ttu-id="0a87c-142">Доменная часть значения **StartPage** в файле AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="0a87c-142">The domain part of the **StartPage** value in the AppManifest.xml file.</span></span>
    
 
- <span data-ttu-id="0a87c-143">Доменная часть URL-адресов всех приемников событий, указанных в файле AppManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="0a87c-143">The domain part of the URLs of any event receivers specified in the AppManifest.xml.</span></span>
    
 
<span data-ttu-id="0a87c-144">В связи с этим учтите указанные ниже особенности.</span><span class="sxs-lookup"><span data-stu-id="0a87c-144">In connection with this point, note the following:</span></span>
 

 

- <span data-ttu-id="0a87c-p113">Если ваше Надстройка SharePoint содержит удаленный компонент, использующий какой-либо другой порт, чем 443, вам необходимо явным образом включить порт как часть домена во всех четырех местах, например  `MarketingServer:3333`. (Необходимо использовать протокол HTTPS, порт по умолчанию для которого 443.)</span><span class="sxs-lookup"><span data-stu-id="0a87c-p113">If the remote component of your SharePoint Add-in is using any port other than 443, you must explicitly include the port as part of the domain in all four places; for example,  `MarketingServer:3333`. (You must use the HTTPS protocol for which the default port is 443.)</span></span>
    
 
- <span data-ttu-id="0a87c-p114">Домен должен быть жестко задан с помощью значения **StartPage** (и URL-адресе каждого приемника событий) в файле AppManifest.xml до упаковки надстройки. Если для упаковки надстройки используется мастер **публикации** в Visual Studio, вам будет предложено указать домен, а Инструменты разработчика Office для Visual Studio автоматически вставят его в значение **StartPage** (вместо маркера `~remoteWebUrl`, который используется при отладке). Но если вы не используете мастер **публикации**, вам потребуется вручную заменить маркер на домен (и протокол), например `https://MarketingServer` или `https://MarketingServer:3333`.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p114">The domain needs to be hardcoded in the **StartPage** value (and any event receiver URLs) of the AppManifest.xml file before the add-in is packaged. If you use the **Publish** wizard in Visual Studio to package the add-in, you will be prompted for the domain and the Office Developer Tools for Visual Studio will insert it into the **StartPage** value for you (in place of the `~remoteWebUrl` token that is used during debugging. But if you are not using the **Publish** wizard you must manually replace the token with the domain (and protocol); for example `https://MarketingServer` or `https://MarketingServer:3333`.</span></span>
    
 

## <a name="runtime-error-saying-that-theres-no-certificate-with-that-serial-number"></a><span data-ttu-id="0a87c-150">Ошибка выполнения с сообщением об отсутствии сертификата с этим серийным номером</span><span class="sxs-lookup"><span data-stu-id="0a87c-150">Runtime error saying that there's no certificate with that serial number</span></span>
<span data-ttu-id="0a87c-151"><a name="DomainRelatedErrors"> </a></span><span class="sxs-lookup"><span data-stu-id="0a87c-151"></span></span>

<span data-ttu-id="0a87c-p115">Если вы уверены в правильности серийного номера сертификата в файле web.config, а сертификат отображается в **хранилище сертификатов Windows**, то, скорее всего, в серийном номере из файла web.config есть дополнительный скрытый символ. Такое бывает, если серийный номер скопирован и вставлен из **консоли управления (MMC)**. Полностью удалите значение серийного номера из файла web.config и повторно введите его *вручную*.</span><span class="sxs-lookup"><span data-stu-id="0a87c-p115">If you are sure you have the correct certificate serial number in the web.config and you can see the certificate in the **Windows Certificate Store**, then there may be a hidden extra character in the serial number in the web.config. This will happen if the serial number is copy'n'pasted from the **Microsoft Management Console**. Delete the entire serial number value from the web.config and *manually*  retype it.</span></span>
 

 

