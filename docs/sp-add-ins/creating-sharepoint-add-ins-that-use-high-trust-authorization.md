# <a name="creating-sharepoint-add-ins-that-use-high-trust-authorization"></a><span data-ttu-id="f74b3-101">Создание надстроек SharePoint, использующих авторизацию с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="f74b3-101">Creating SharePoint Add-ins that use high-trust authorization</span></span>
<span data-ttu-id="f74b3-102">В этой статье рассказывается о надстройках SharePoint с высоким уровнем доверия, в которых используются цифровые сертификаты для создания доверия между SharePoint и удаленными компонентами, получающими доступ к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-102">Learn about high-trust SharePoint Add-ins, which use digital certificates to establish trust between SharePoint and the remote components that access SharePoint. Provided by:</span></span>
 

 <span data-ttu-id="f74b3-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="f74b3-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

 <span data-ttu-id="f74b3-106">**Авторы:**</span><span class="sxs-lookup"><span data-stu-id="f74b3-106">**Provided by:**</span></span>
 
<span data-ttu-id="f74b3-107">Стив Пешка (Steve Peschka), Корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f74b3-107">Steve Peschka, Microsoft Corporation</span></span>

<span data-ttu-id="f74b3-108">Сью Муа Хор (Siew Moi Khor), Корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="f74b3-108">Siew Moi Khor, Microsoft Corporation</span></span>
 

## <a name="overview-of-high-trust-sharepoint-add-ins"></a><span data-ttu-id="f74b3-109">Общие сведения о надстройках SharePoint с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="f74b3-109">Overview of high-trust SharePoint Add-ins</span></span>
<span data-ttu-id="f74b3-110"><a name="Overview"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-110"></span></span>

<span data-ttu-id="f74b3-p102">Надстройка с высоким уровнем доверия это Надстройка SharePoint, которая устанавливается в локальной ферме SharePoint. Ее нельзя установить в Microsoft SharePoint Online или продавать в Магазин Office. Надстройка с высоким уровнем доверия использует для создания отношения доверия сертификат, а не маркер контекста.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p102">A high-trust add-in is a provider-hosted SharePoint Add-in that is installed to an on-premises SharePoint farm. It cannot be installed to Microsoft SharePoint Online or marketed through the Office Store. A high-trust add-in uses a certificate instead of a context token to establish trust.</span></span>
 

 

 <span data-ttu-id="f74b3-p103">**Примечание.** В этой статье рассказывается о системе авторизации с высоким уровнем доверия для надстроек SharePoint. Практические сведения о создании и развертывании надстроек с высоким уровнем доверия см. в следующих статьях: [Создание надстроек SharePoint с высоким уровнем доверия](create-high-trust-sharepoint-add-ins) и [Упаковка и публикация надстроек SharePoint с высоким уровнем доверия](package-and-publish-high-trust-sharepoint-add-ins).</span><span class="sxs-lookup"><span data-stu-id="f74b3-p103">**Note** This topic helps you understand the high-trust authorization system for SharePoint Add-ins. For practical information about creating and deploying high-trust add-ins, see the following topics:>  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins) [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins)</span></span>
 

<span data-ttu-id="f74b3-p104">В SharePoint служба маркеров безопасности предоставляет маркеры доступа для проверки подлинности между серверами. Эти временные маркеры обеспечивают доступ к другим службам надстройки, например Exchange 2013, Lync 2013 и Надстройки SharePoint. Администратор фермы создает отношение доверия между SharePoint и другой надстройкой с помощью командлетов Windows PowerShell и сертификата. Каждый используемый сертификат необходимо сделать доверенным для SharePoint с помощью командлетов  `New-SPTrustedRootAuthority`. Кроме того, каждый сертификат должен быть зарегистрирован в SharePoint как издатель маркеров с помощью командлета  `New-SPTrustedSecurityTokenIssuer`.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p104">In SharePoint, the security token service (STS) provides access tokens for server-to-server authentication. The STS enables temporary access tokens to access other application services such as Exchange 2013, Lync 2013, and SharePoint Add-ins. A farm administrator establishes trust between SharePoint and the other application or add-in by using Windows PowerShell cmdlets and a certificate. Each certificate that is used must be trusted by SharePoint using the  `New-SPTrustedRootAuthority` cmdlet. Also each certificate must be registered with SharePoint as a token issuer using the `New-SPTrustedSecurityTokenIssuer` cmdlet.</span></span>
 

 

 <span data-ttu-id="f74b3-p105">**Примечание.** Служба маркеров безопасности не предназначена для проверки подлинности пользователей. Поэтому ее нет на странице входа для пользователей, в разделе **Поставщик проверки подлинности** в центре администрирования или в средстве выбора людей в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p105">**Note** The STS isn't intended for user authentication. So, you won't see the STS listed on the user sign-in page, in the **Authentication Provider** section in Central Administration, or in the People Picker in SharePoint.</span></span>
 


## <a name="two-kinds-of-token-issuers"></a><span data-ttu-id="f74b3-123">Два вида издателей маркеров</span><span class="sxs-lookup"><span data-stu-id="f74b3-123">Two kinds of token issuers</span></span>
<span data-ttu-id="f74b3-124"><a name="TwoKindsOfIssuers"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-124"></span></span>

<span data-ttu-id="f74b3-p106">Удаленное веб-приложение Надстройка SharePoint с высоким уровнем доверия привязано к цифровому сертификату. (Сведения о том, как это сделать, см. в двух разделах, указанных выше.) Удаленное веб-приложение использует сертификат для подписи маркеров доступа, которые добавляются во все запросы к SharePoint. Веб-приложение подписывает маркер закрытым ключом сертификата, а SharePoint проверяет его с помощью открытого ключа сертификата. Сертификат должен быть зарегистрирован как доверенный издатель маркеров, чтобы SharePoint доверял выдаваемым маркерам. Существует два типа издателей маркеров, некоторые из них могут выдавать маркеры только для определенного Надстройка SharePoint, а другие, которые называют посредниками доверия, могут выдавать маркеры нескольким Надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p106">The remote web application of a high-trust SharePoint Add-in is bound to a digital certificate. (For information about how this is done, see the two topics linked-to above.) The certificate is used by the remote web application to sign the access tokens that it includes in all its requests to SharePoint. The web application signs the token with the private key of the certificate and SharePoint validates it with the public key of the certificate. The certificate has to be registered as a trusted token issuer before SharePoint will trust the tokens that it issues. There are two kinds of token issuers: some can only issue tokens for a particular SharePoint Add-in; others, called trust brokers, can issue tokens for multiple SharePoint Add-ins.</span></span>
 

 
<span data-ttu-id="f74b3-p107">Администраторы SharePoint определяют тип создаваемого издателя маркеров с помощью переключателей и параметров командлета  `New-SPTrustedSecurityTokenIssuer`. Для создания издателя маркеров, являющегося посредником доверия, добавьте переключатель  `-IsTrustBroker` в командную строку и используйте уникальное значение, отличное от кода клиента надстройки, для параметра `-Name`. Далее приводится измененный пример.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p107">As a practical matter, SharePoint farm administrators determine which type of token issuer is created by the switches and parameter values they use with the  `New-SPTrustedSecurityTokenIssuer` cmdlet. To create a token issuer that is a trust broker, add the `-IsTrustBroker` switch to the command line and use a unique value, other than an add-in's client ID, for the `-Name` parameter. The following is an edited example.</span></span>
 

 



```
New-SPTrustedSecurityTokenIssuer -IsTrustBroker -RegisteredIssuerName "<full_token_issuer_name> " --other parameters omitted--
```

<span data-ttu-id="f74b3-p108">Переключатель  `-IsTrustBroker` не используется для создания издателя маркеров, не являющегося посредником доверия. Существует и другое отличие. Значение параметра `-RegisteredIssuerName` всегда представлено в форме двух идентификаторов GUID, разделенных символом "@"; _GUID_@ _GUID_. GUID в правой части всегда представляет идентификатор области проверки подлинности фермы SharePoint (или подписки сайта). GUID слева всегда представляет определенный идентификатор для издателя маркеров. Этот GUID произвольный, если создается  *посредник доверия*  . Но если создается другой тип издателя маркеров, указанный GUID издателя должен совпадать с GUID, который используется как код клиента Надстройка SharePoint. Данный параметр не только предоставляет имя издателя, но и сообщает SharePoint, какое Надстройка SharePoint является единственным приложением, для которого сертификат может выдавать маркеры. Далее представлен частичный пример:</span><span class="sxs-lookup"><span data-stu-id="f74b3-p108">To create a non-broker token issuer, the  `-IsTrustBroker` switch is not used. There is one other difference. The value of the `-RegisteredIssuerName` parameter is always in the form of two GUIDs separated by the "@" character; _GUID_@ _GUID_. The GUID on the right side is always the ID of the authentication realm of the SharePoint farm (or site subscription). The GUID on the left side is always a specific ID for a token issuer. It is a random GUID when a  *trust broker*  token issuer is being created. But when a non-broker token issuer is being created, the specific issuer GUID must be the same GUID that is used as the client ID of the SharePoint Add-in. This parameter provides a name for the issuer. It also tells SharePoint which SharePoint Add-in is the only one for which the certificate can issue tokens. The following is a partial example:</span></span>
 

 



```
$fullIssuerIdentifier = "<client_ID_of_SP_app> " + "@" + "<realm_GUID> "
New-SPTrustedSecurityTokenIssuer -RegisteredIssuerName $fullIssuerIdentifier --other parameters omitted--
```

<span data-ttu-id="f74b3-p109">Обычно командлет  `New-SPTrustedSecurityTokenIssuer` используется в сценарии, который выполняет другие задачи настройки SharePoint для надстроек с высоким уровнем доверия. Дополнительные сведения о таких сценариях и полные примеры применения командлета `New-SPTrustedSecurityTokenIssuer` см. в статье [Скрипты настройки высокого уровня доверия для SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="f74b3-p109">Typically, the  `New-SPTrustedSecurityTokenIssuer` cmdlet is used in a script that performs other tasks to configure SharePoint for high-trust add-ins. For more information about such scripts and complete examples of the `New-SPTrustedSecurityTokenIssuer` cmdlet, see [High-trust configuration scripts for SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).</span></span>
 

 

## <a name="deciding-between-using-one-certificate-or-many-for-high-trust-sharepoint-add-ins"></a><span data-ttu-id="f74b3-145">Выбор между использованием одного или нескольких сертификатов для надстроек SharePoint с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="f74b3-145">Deciding between using one certificate or many for high-trust SharePoint Add-ins</span></span>
<span data-ttu-id="f74b3-146"><a name="Deciding"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-146"></span></span>

<span data-ttu-id="f74b3-147">При получении сертификатов, предназначенных для надстроек SharePoint с высоким уровнем доверия, и управлении ими администратор SharePoint и сети может выбрать одну из двух следующих основных стратегий:</span><span class="sxs-lookup"><span data-stu-id="f74b3-147">SharePoint and network administrator have two basic strategies to choose from when obtaining and managing certificates for use by high-trust SharePoint Add-ins:</span></span>
 

 

- <span data-ttu-id="f74b3-148">использование одного сертификата для нескольких Надстройки SharePoint;</span><span class="sxs-lookup"><span data-stu-id="f74b3-148">Use the same certificate for multiple SharePoint Add-ins.</span></span>
    
 
- <span data-ttu-id="f74b3-149">использование отдельных сертификатов для каждого Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-149">Use a separate certificate for each SharePoint Add-in.</span></span>
    
 
<span data-ttu-id="f74b3-150">В этом разделе обсуждаются преимущества и недостатки каждой стратегии.</span><span class="sxs-lookup"><span data-stu-id="f74b3-150">This section discusses the pros and cons for each strategy.</span></span>
 

 
<span data-ttu-id="f74b3-p110">Преимущество использования одного сертификата для нескольких Надстройки SharePoint состоит в том, что администратору для настройки доверия и управления приходится иметь дело с меньшим количеством сертификатов. Недостаток этого подхода состоит в том, что при необходимости разорвать доверительное отношение с определенным Надстройка SharePoint администратору потребуется удалить сертификат в качестве издателя маркеров или корневого центра сертификации. Но при удалении сертификата также разрывается доверительное отношение со всеми другими Надстройки SharePoint, использующими этот же сертификат, из-за чего все они перестанут работать.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p110">The benefit of using the same certificate for multiple SharePoint Add-ins is that an administrator has fewer certificates to trust and manage. The disadvantage in this approach is that, when you encounter a situation where you want to break trust with a particular SharePoint Add-in, the only way the administrator can break trust is by removing the certificate as a token issuer or as a root authority. But removing the certificate also breaks trust with all other SharePoint Add-ins that use the same certificate, which causes them all to stop working.</span></span>
 

 
<span data-ttu-id="f74b3-p111">Чтобы заслуживающие доверия Надстройки SharePoint опять начали работать, администратору потребуется создать объект `New-SPTrustedSecurityTokenIssuer`, *используя новый сертификат*, и указать флаг `-IsTrustBroker`. Новый сертификат необходимо зарегистрировать на каждом сервере, на котором размещаются доверенные надстройки. Все эти надстройки требуется связать с новым сертификатом.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p111">To get the still trustworthy SharePoint Add-ins working again, the administrator would need to create a  `New-SPTrustedSecurityTokenIssuer` object *using a new certificate*  and include the `-IsTrustBroker` flag. Then the new certificate would have to be registered with each server that hosts any of the trustworthy add-ins and each of those add-ins would have to be bound to the new certificate.</span></span>
 

 
<span data-ttu-id="f74b3-p112">Преимущество использования одного сертификата для каждой надстройки состоит в том, что упрощается разрыв доверия с определенной надстройкой, так как сертификаты, используемые заслуживающими доверия надстройками, не затрагиваются, когда администратор разрывает отношение доверия с сертификатом одной надстройки. Недостаток этой стратегии заключается в том, что администратору необходимо получить множество сертификатов, а SharePoint следует настроить для каждого из них, что можно сделать с помощью сценария, как показано в статье  [Скрипты настройки высокого уровня доверия для SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="f74b3-p112">The benefit of using one certificate per add-in is that it makes it easier to break trust with a particular add-in, because the certificates that are used by the still trustworthy add-ins are not affected when the administrator breaks trust with the certificate of the one add-in. The disadvantage in this strategy is that an administrator has more certificates to acquire and SharePoint must be configured to use each of them, which can be done with a reusable script as shown in  [High-trust configuration scripts for SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).</span></span>
 

 

## <a name="certificates-are-root-authorities-in-sharepoint"></a><span data-ttu-id="f74b3-158">Сертификаты — это корневые центры в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f74b3-158">Certificates are root authorities in SharePoint</span></span>
<span data-ttu-id="f74b3-159"><a name="RootAuthorities"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-159"></span></span>

<span data-ttu-id="f74b3-p113">Как было вскользь упомянуто в начале статьи, сертификат или удаленное веб-приложение в надстройке с высоким уровнем доверия администраторы фермы SharePoint должны сделать доверенным корневым центром сертификации в SharePoint, а также доверенным издателем маркеров. К слову, если за сертификатом веб-приложения стоит иерархия издателей сертификатов, то все сертификаты в цепочке необходимо добавить в список доверенных корневых центров сертификации SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p113">As mentioned briefly at the top of this article, SharePoint farm administrators have to make the certificate, of the remote web application in the high-trust add-in, a trusted root authority in SharePoint as well as a trusted token issuer. In fact, when there is a hierarchy of certificate issuing authorities behind the web application's certificate, all the certificates in the chain must be added to SharePoint's list of trusted root authorities.</span></span>
 

 
<span data-ttu-id="f74b3-p114">Каждый сертификат в цепочке добавляется в список доверенных корневых центров сертификации SharePoint с помощью командлета  `New-SPTrustedRootAuthority`. Например, предположим, что сертификат веб-приложения это сертификат домена, выданный корпоративным доменным центром сертификации в локальной сети, и что его сертификат в свою очередь был выдан автономным центром сертификации верхнего уровня в локальной сети. В этом сценарии сертификаты ЦС верхнего уровня, промежуточного ЦС и веб-приложения следует добавить в список доверенных корневых центров сертификации SharePoint. Это можно сделать с помощью следующего кода Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p114">Each certificate in the chain is added to SharePoint's list of trusted root authorities with a call of the  `New-SPTrustedRootAuthority` cmdlet. For example, suppose that the web application's certificate is a domain certificate that is issued by an enterprise domain certificate authority on the LAN, and suppose that its certificate, in turn, was issued by a standalone, top-level certificate authority on the LAN. In this scenario, the certificates of the top-level CA, the intermediate CA, and the web application all have to be added to SharePoint's list of trusted root authorities. The following Windows PowerShell code would accomplish this.</span></span>
 

 



```
$rootCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("<path_to_top-level_CA's_cer_file>")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $rootCA

$intermediateCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_intermediate_CA's_cer_file")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $intermediateCA

$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_web_application's_cer_file") 
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $certificate 

```

<span data-ttu-id="f74b3-p115">Корневой и промежуточные сертификаты необходимо добавить в ферму SharePoint только один раз. Обычно сертификат веб-приложения добавляется в отдельном скрипте, который выполняет и другие задачи настройки, например вызывает командлет  `New-SPTrustedSecurityTokenIssuer`. Примеры см. в статье  [Скрипты настройки высокого уровня доверия для SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).</span><span class="sxs-lookup"><span data-stu-id="f74b3-p115">The root and intermediate certificates should be added only once on a SharePoint farm. Typically, the web application's certificate is added in a separate script that does other configuration too, such as the call to  `New-SPTrustedSecurityTokenIssuer`. For examples, see  [High-trust configuration scripts for SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).</span></span>
 

 
<span data-ttu-id="f74b3-169">Если сертификат веб-приложения является самозаверяющим, что возможно во время разработки и отладки надстройки, цепочки сертификатов не существует, и в список корневых центров сертификации нужно добавить только сертификат веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f74b3-169">If the web application's certificate is self-signed, as might be the case when the add-in is being developed and debugged, then there is no certificate chain and only the web application's certificate needs to be added to the list of root authorities.</span></span>
 

 
<span data-ttu-id="f74b3-p116">Дополнительные сведения см. в записи блога  [Ошибка в связи с отсутствием доверия к корню цепочки сертификатов при проверке подлинности на основе утверждений](http://blogs.technet.com/b/speschka/archive/2010/02/13/root-of-certificate-chain-not-trusted-error-with-claims-authentication.aspx). (Пропустите раздел об экспорте сертификата из служб федерации Active Directory (AD FS), если вы создали сертификат для надстроек с высоким уровнем доверия какими-либо другими средствами, например, используя коммерческий сертификат, выпущенный центром сертификации, самозаверяющий сертификат или сертификат, выпущенный для домена.)</span><span class="sxs-lookup"><span data-stu-id="f74b3-p116">For more information, see the blog post  [Root of certificate chain not trusted error with claims authentication](http://blogs.technet.com/b/speschka/archive/2010/02/13/root-of-certificate-chain-not-trusted-error-with-claims-authentication.aspx). (Scroll past the section about exporting the certificate from Active Directory Federation Services (AD FS), assuming you created your certificate for your high-trust add-ins via some other means; for example, by using a commercial certificate issued by a Certificate Authority, a self-signed certificate, or a domain-issued certificate.)</span></span>
 

 

## <a name="web-application-needs-to-know-that-it-is-a-token-issuer"></a><span data-ttu-id="f74b3-172">Веб-приложению необходимо знать, что это издатель маркеров</span><span class="sxs-lookup"><span data-stu-id="f74b3-172">Web application needs to know that it is a token issuer</span></span>
<span data-ttu-id="f74b3-173"><a name="AppIsTokenIssuer"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-173"></span></span>

<span data-ttu-id="f74b3-p117">Компонент удаленного веб-приложения надстройки SharePoint связан с ее сертификатом в службах IIS. Этого достаточно для традиционных целей использования сертификатов: надежной идентификации веб-приложения и кодирования HTTP-запросов и ответов. Тем не менее в надстройке SharePoint с высоким уровнем доверия сертификат также выполняет дополнительную задачу: он служит официальным "издателем" маркеров доступа, которые веб-приложение отправляет в SharePoint. Для этого веб-приложение должно знать код издателя сертификата, используемый при регистрации сертификата в качестве издателя маркеров в SharePoint. Веб-приложение получает этот код из раздела **appSettings** файла web.config, который содержит ключ **IssuerId**. Инструкции по настройке этого значения разработчиками надстроек и привязке сертификата к веб-приложению в службах IIS см. в статье [Упаковка и публикация надстроек SharePoint с высоким уровнем доверия](package-and-publish-high-trust-sharepoint-add-ins). Обратите внимание, что если пользователь применяет отдельный сертификат для каждой надстройки SharePoint с высоким уровнем доверия, значение **ClientId** также используется в качестве значения **IssuerId**. Этот подход отличается от подхода, используемого в сценарии, в котором несколько надстроек используют один и тот же сертификат, так как у каждой надстройки SharePoint должен быть собственный уникальный код клиента, а код издателя является идентификатором для объекта **SPTrustedSecurityTokenIssuer**.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p117">The remote web application component of the SharePoint Add-in is bound to its certificate in IIS. This is sufficient for the traditional purposes of certificates: securely identifying the web application and encoding the HTTP requests and responses. However, in a high-trust SharePoint Add-in, the certificate has the additional task of being the official "issuer" of the access tokens that the web application sends to SharePoint. For this purpose, web application has to know the issuer ID of the certificate that is used when registering the certificate as a token issuer with SharePoint. The web application gets this ID from the **appSettings** section of the web.config file, where there is a key named **IssuerId**. Instructions for how the add-in developer sets this value, and how the certificate is bound to the web application in IIS, are in  [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins). Note that if the customer is using the strategy of having a separate certificate for each high-trust SharePoint Add-in, then the **ClientId** value is also used as the **IssuerId** value. This is not the case when multiple add-ins share the same certificate, because each SharePoint Add-in must have its own unique client ID, but the issuer ID is the identifier for a **SPTrustedSecurityTokenIssuer** object.</span></span>
 

 
<span data-ttu-id="f74b3-p118">Ниже приведен пример раздела **appSettings** для надстройки SharePoint с высоким уровнем доверия. В нем сертификат используется несколькими надстройками, поэтому значение **IssuerId** не совпадает со значением **ClientId**. Обратите внимание, что ключа **ClientSecret** в надстройке SharePoint с высоким уровнем доверия нет.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p118">Following is an example of an **appSettings** section for a high-trust SharePoint Add-in. In this example, a certificate is being shared by multiple add-ins, so the **IssuerId** is not the same as the **ClientId**. Note that there is no **ClientSecret** key in a high-trust SharePoint Add-in.</span></span>
 

 



```XML
<appSettings>
  <add key="ClientId" value="6569a7e8-3670-4669-91ae-ec6819ab461" />
  <add key="ClientSigningCertificatePath" value="C:\MyCerts\HighTrustCert.pfx" />
  <add key="ClientSigningCertificatePassword" value="3VeryComplexPa$$word82" />
  <add key="IssuerId" value="e9134021-0180-4b05-9e7e-0a9e5a524965" />
</appSettings>

```


 <span data-ttu-id="f74b3-p119">**Примечание по безопасности.** В предыдущем примере предполагается, что сертификат хранится в файловой системе. Это приемлемо при разработке и отладке. В рабочей надстройке SharePoint с высоким уровнем доверия сертификат обычно размещается в хранилище сертификатов Windows, а ключи **ClientSigningCertificatePath** и **ClientSigningCertificatePassword** обычно заменяются ключом **ClientSigningCertificateSerialNumber**.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p119">**SECURITY NOTE** The preceding example assumes that the certificate is stored on the file system. This is acceptable for development and debugging. In a production high-trust SharePoint Add-in, the certificate is usually stored in the Windows Certificate Store, and the **ClientSigningCertificatePath** and **ClientSigningCertificatePassword** keys are typically replaced by a **ClientSigningCertificateSerialNumber** key.</span></span>
 


## <a name="it-staff-responsibilities-in-the-high-trust-system"></a><span data-ttu-id="f74b3-188">Обязанности сотрудников ИТ-подразделения в системе высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="f74b3-188">IT staff responsibilities in the high-trust system</span></span>
<span data-ttu-id="f74b3-189"><a name="ITPro"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-189"></span></span>

<span data-ttu-id="f74b3-p120">Разработчикам необходимо понимать описанные выше требования к безопасности приложений, но ИТ-специалисты будут реализовывать инфраструктуру, необходимую для ее поддержки. Поэтому им необходимо планировать выполнение указанных ниже эксплуатационных требований.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p120">Developers will have to understand the requirements for application security as described above, but IT Pros will be implementing the infrastructure required to support it. IT Pros must plan for the following operational requirements:</span></span>
 

 

- <span data-ttu-id="f74b3-192">Создание или покупка одного или нескольких сертификатов, которые будут использоваться для доверенных Надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-192">Create or purchase one or more certificates that will be used for trusted SharePoint Add-ins.</span></span>
    
 
- <span data-ttu-id="f74b3-p121">Убедитесь, сертификаты безопасно хранятся на серверах веб-приложений. Если используется ОС Windows, сертификаты размещаются в хранилище сертификатов Windows.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p121">Ensure that the certificates are securely stored on the web application servers. When Windows OS is being used, this means storing the certificates in the Windows Certificate Store.</span></span>
    
 
- <span data-ttu-id="f74b3-195">Управление распределением этих сертификатов среди разработчиков, собирающих Надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f74b3-195">Manage the distribution of those certificates to developers who are building SharePoint Add-ins.</span></span>
    
 
- <span data-ttu-id="f74b3-p122">Отслеживание распространения каждого сертификата как для надстроек, использующих его, так и для разработчиков, которые получили копию. Чтобы отозвать сертификат, ИТ-специалистам понадобится связаться с каждым разработчиком, чтобы договориться о переходе на новый сертификат.</span><span class="sxs-lookup"><span data-stu-id="f74b3-p122">Keep track where each certificate is distributed, for both the add-ins using it and the developers who have received a copy. If a certificate has to be revoked, the IT staff must work with each developer to arrange for a managed transition to a new certificate.</span></span>
    
 

## <a name="additional-resources"></a><span data-ttu-id="f74b3-198">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f74b3-198">Additional resources</span></span>
<span data-ttu-id="f74b3-199"><a name="AR"> </a></span><span class="sxs-lookup"><span data-stu-id="f74b3-199"></span></span>


-  [<span data-ttu-id="f74b3-200">Создание надстроек SharePoint с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="f74b3-200">Create high-trust SharePoint Add-ins</span></span>](create-high-trust-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f74b3-201">Упаковка и публикация надстроек SharePoint с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="f74b3-201">Package and publish high-trust SharePoint Add-ins</span></span>](package-and-publish-high-trust-sharepoint-add-ins)
    
 
-  [<span data-ttu-id="f74b3-202">Советы по устранению неполадок в надстройках с высоким уровнем доверия в SharePoint</span><span class="sxs-lookup"><span data-stu-id="f74b3-202">Troubleshooting Tips for High Trust Add-ins on SharePoint</span></span>](http://blogs.technet.com/b/speschka/archive/2012/11/01/more-troubleshooting-tips-for-high-trust-apps-on-sharepoint-2013.aspx)
    
 
-  [<span data-ttu-id="f74b3-203">Авторизация и проверка подлинности надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="f74b3-203">Authorization and authentication of SharePoint Add-ins</span></span>](authorization-and-authentication-of-sharepoint-add-ins)
    
 

