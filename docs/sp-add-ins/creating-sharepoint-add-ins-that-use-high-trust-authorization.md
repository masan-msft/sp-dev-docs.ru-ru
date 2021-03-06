# <a name="creating-sharepoint-add-ins-that-use-high-trust-authorization"></a>Создание надстроек SharePoint, использующих авторизацию с высоким уровнем доверия
В этой статье рассказывается о надстройках SharePoint с высоким уровнем доверия, в которых используются цифровые сертификаты для создания доверия между SharePoint и удаленными компонентами, получающими доступ к SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

 **Авторы:**
 
Стив Пешка (Steve Peschka), Корпорация Майкрософт

Сью Муа Хор (Siew Moi Khor), Корпорация Майкрософт
 

## <a name="overview-of-high-trust-sharepoint-add-ins"></a>Общие сведения о надстройках SharePoint с высоким уровнем доверия
<a name="Overview"> </a>

Надстройка с высоким уровнем доверия это Надстройка SharePoint, которая устанавливается в локальной ферме SharePoint. Ее нельзя установить в Microsoft SharePoint Online или продавать в Магазин Office. Надстройка с высоким уровнем доверия использует для создания отношения доверия сертификат, а не маркер контекста.
 

 

 **Примечание.** В этой статье рассказывается о системе авторизации с высоким уровнем доверия для надстроек SharePoint. Практические сведения о создании и развертывании надстроек с высоким уровнем доверия см. в следующих статьях: [Создание надстроек SharePoint с высоким уровнем доверия](create-high-trust-sharepoint-add-ins) и [Упаковка и публикация надстроек SharePoint с высоким уровнем доверия](package-and-publish-high-trust-sharepoint-add-ins).
 

В SharePoint служба маркеров безопасности предоставляет маркеры доступа для проверки подлинности между серверами. Эти временные маркеры обеспечивают доступ к другим службам надстройки, например Exchange 2013, Lync 2013 и Надстройки SharePoint. Администратор фермы создает отношение доверия между SharePoint и другой надстройкой с помощью командлетов Windows PowerShell и сертификата. Каждый используемый сертификат необходимо сделать доверенным для SharePoint с помощью командлетов  `New-SPTrustedRootAuthority`. Кроме того, каждый сертификат должен быть зарегистрирован в SharePoint как издатель маркеров с помощью командлета  `New-SPTrustedSecurityTokenIssuer`.
 

 

 **Примечание.** Служба маркеров безопасности не предназначена для проверки подлинности пользователей. Поэтому ее нет на странице входа для пользователей, в разделе **Поставщик проверки подлинности** в центре администрирования или в средстве выбора людей в SharePoint.
 


## <a name="two-kinds-of-token-issuers"></a>Два вида издателей маркеров
<a name="TwoKindsOfIssuers"> </a>

Удаленное веб-приложение Надстройка SharePoint с высоким уровнем доверия привязано к цифровому сертификату. (Сведения о том, как это сделать, см. в двух разделах, указанных выше.) Удаленное веб-приложение использует сертификат для подписи маркеров доступа, которые добавляются во все запросы к SharePoint. Веб-приложение подписывает маркер закрытым ключом сертификата, а SharePoint проверяет его с помощью открытого ключа сертификата. Сертификат должен быть зарегистрирован как доверенный издатель маркеров, чтобы SharePoint доверял выдаваемым маркерам. Существует два типа издателей маркеров, некоторые из них могут выдавать маркеры только для определенного Надстройка SharePoint, а другие, которые называют посредниками доверия, могут выдавать маркеры нескольким Надстройки SharePoint.
 

 
Администраторы SharePoint определяют тип создаваемого издателя маркеров с помощью переключателей и параметров командлета  `New-SPTrustedSecurityTokenIssuer`. Для создания издателя маркеров, являющегося посредником доверия, добавьте переключатель  `-IsTrustBroker` в командную строку и используйте уникальное значение, отличное от кода клиента надстройки, для параметра `-Name`. Далее приводится измененный пример.
 

 



```
New-SPTrustedSecurityTokenIssuer -IsTrustBroker -RegisteredIssuerName "<full_token_issuer_name> " --other parameters omitted--
```

Переключатель  `-IsTrustBroker` не используется для создания издателя маркеров, не являющегося посредником доверия. Существует и другое отличие. Значение параметра `-RegisteredIssuerName` всегда представлено в форме двух идентификаторов GUID, разделенных символом "@"; _GUID_@ _GUID_. GUID в правой части всегда представляет идентификатор области проверки подлинности фермы SharePoint (или подписки сайта). GUID слева всегда представляет определенный идентификатор для издателя маркеров. Этот GUID произвольный, если создается  *посредник доверия*  . Но если создается другой тип издателя маркеров, указанный GUID издателя должен совпадать с GUID, который используется как код клиента Надстройка SharePoint. Данный параметр не только предоставляет имя издателя, но и сообщает SharePoint, какое Надстройка SharePoint является единственным приложением, для которого сертификат может выдавать маркеры. Далее представлен частичный пример:
 

 



```
$fullIssuerIdentifier = "<client_ID_of_SP_app> " + "@" + "<realm_GUID> "
New-SPTrustedSecurityTokenIssuer -RegisteredIssuerName $fullIssuerIdentifier --other parameters omitted--
```

Обычно командлет  `New-SPTrustedSecurityTokenIssuer` используется в сценарии, который выполняет другие задачи настройки SharePoint для надстроек с высоким уровнем доверия. Дополнительные сведения о таких сценариях и полные примеры применения командлета `New-SPTrustedSecurityTokenIssuer` см. в статье [Скрипты настройки высокого уровня доверия для SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).
 

 

## <a name="deciding-between-using-one-certificate-or-many-for-high-trust-sharepoint-add-ins"></a>Выбор между использованием одного или нескольких сертификатов для надстроек SharePoint с высоким уровнем доверия
<a name="Deciding"> </a>

При получении сертификатов, предназначенных для надстроек SharePoint с высоким уровнем доверия, и управлении ими администратор SharePoint и сети может выбрать одну из двух следующих основных стратегий:
 

 

- использование одного сертификата для нескольких Надстройки SharePoint;
    
 
- использование отдельных сертификатов для каждого Надстройка SharePoint.
    
 
В этом разделе обсуждаются преимущества и недостатки каждой стратегии.
 

 
Преимущество использования одного сертификата для нескольких Надстройки SharePoint состоит в том, что администратору для настройки доверия и управления приходится иметь дело с меньшим количеством сертификатов. Недостаток этого подхода состоит в том, что при необходимости разорвать доверительное отношение с определенным Надстройка SharePoint администратору потребуется удалить сертификат в качестве издателя маркеров или корневого центра сертификации. Но при удалении сертификата также разрывается доверительное отношение со всеми другими Надстройки SharePoint, использующими этот же сертификат, из-за чего все они перестанут работать.
 

 
Чтобы заслуживающие доверия Надстройки SharePoint опять начали работать, администратору потребуется создать объект `New-SPTrustedSecurityTokenIssuer`, *используя новый сертификат*, и указать флаг `-IsTrustBroker`. Новый сертификат необходимо зарегистрировать на каждом сервере, на котором размещаются доверенные надстройки. Все эти надстройки требуется связать с новым сертификатом.
 

 
Преимущество использования одного сертификата для каждой надстройки состоит в том, что упрощается разрыв доверия с определенной надстройкой, так как сертификаты, используемые заслуживающими доверия надстройками, не затрагиваются, когда администратор разрывает отношение доверия с сертификатом одной надстройки. Недостаток этой стратегии заключается в том, что администратору необходимо получить множество сертификатов, а SharePoint следует настроить для каждого из них, что можно сделать с помощью сценария, как показано в статье  [Скрипты настройки высокого уровня доверия для SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).
 

 

## <a name="certificates-are-root-authorities-in-sharepoint"></a>Сертификаты — это корневые центры в SharePoint
<a name="RootAuthorities"> </a>

Как было вскользь упомянуто в начале статьи, сертификат или удаленное веб-приложение в надстройке с высоким уровнем доверия администраторы фермы SharePoint должны сделать доверенным корневым центром сертификации в SharePoint, а также доверенным издателем маркеров. К слову, если за сертификатом веб-приложения стоит иерархия издателей сертификатов, то все сертификаты в цепочке необходимо добавить в список доверенных корневых центров сертификации SharePoint.
 

 
Каждый сертификат в цепочке добавляется в список доверенных корневых центров сертификации SharePoint с помощью командлета  `New-SPTrustedRootAuthority`. Например, предположим, что сертификат веб-приложения это сертификат домена, выданный корпоративным доменным центром сертификации в локальной сети, и что его сертификат в свою очередь был выдан автономным центром сертификации верхнего уровня в локальной сети. В этом сценарии сертификаты ЦС верхнего уровня, промежуточного ЦС и веб-приложения следует добавить в список доверенных корневых центров сертификации SharePoint. Это можно сделать с помощью следующего кода Windows PowerShell.
 

 



```
$rootCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("<path_to_top-level_CA's_cer_file>")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $rootCA

$intermediateCA = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_intermediate_CA's_cer_file")
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $intermediateCA

$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2("path_to_web_application's_cer_file") 
New-SPTrustedRootAuthority -Name "<name_of_certificate>" -Certificate $certificate 

```

Корневой и промежуточные сертификаты необходимо добавить в ферму SharePoint только один раз. Обычно сертификат веб-приложения добавляется в отдельном скрипте, который выполняет и другие задачи настройки, например вызывает командлет  `New-SPTrustedSecurityTokenIssuer`. Примеры см. в статье  [Скрипты настройки высокого уровня доверия для SharePoint](high-trust-configuration-scripts-for-sharepoint-2013).
 

 
Если сертификат веб-приложения является самозаверяющим, что возможно во время разработки и отладки надстройки, цепочки сертификатов не существует, и в список корневых центров сертификации нужно добавить только сертификат веб-приложения.
 

 
Дополнительные сведения см. в записи блога  [Ошибка в связи с отсутствием доверия к корню цепочки сертификатов при проверке подлинности на основе утверждений](http://blogs.technet.com/b/speschka/archive/2010/02/13/root-of-certificate-chain-not-trusted-error-with-claims-authentication.aspx). (Пропустите раздел об экспорте сертификата из служб федерации Active Directory (AD FS), если вы создали сертификат для надстроек с высоким уровнем доверия какими-либо другими средствами, например, используя коммерческий сертификат, выпущенный центром сертификации, самозаверяющий сертификат или сертификат, выпущенный для домена.)
 

 

## <a name="web-application-needs-to-know-that-it-is-a-token-issuer"></a>Веб-приложению необходимо знать, что это издатель маркеров
<a name="AppIsTokenIssuer"> </a>

Компонент удаленного веб-приложения надстройки SharePoint связан с ее сертификатом в службах IIS. Этого достаточно для традиционных целей использования сертификатов: надежной идентификации веб-приложения и кодирования HTTP-запросов и ответов. Тем не менее в надстройке SharePoint с высоким уровнем доверия сертификат также выполняет дополнительную задачу: он служит официальным "издателем" маркеров доступа, которые веб-приложение отправляет в SharePoint. Для этого веб-приложение должно знать код издателя сертификата, используемый при регистрации сертификата в качестве издателя маркеров в SharePoint. Веб-приложение получает этот код из раздела **appSettings** файла web.config, который содержит ключ **IssuerId**. Инструкции по настройке этого значения разработчиками надстроек и привязке сертификата к веб-приложению в службах IIS см. в статье [Упаковка и публикация надстроек SharePoint с высоким уровнем доверия](package-and-publish-high-trust-sharepoint-add-ins). Обратите внимание, что если пользователь применяет отдельный сертификат для каждой надстройки SharePoint с высоким уровнем доверия, значение **ClientId** также используется в качестве значения **IssuerId**. Этот подход отличается от подхода, используемого в сценарии, в котором несколько надстроек используют один и тот же сертификат, так как у каждой надстройки SharePoint должен быть собственный уникальный код клиента, а код издателя является идентификатором для объекта **SPTrustedSecurityTokenIssuer**.
 

 
Ниже приведен пример раздела **appSettings** для надстройки SharePoint с высоким уровнем доверия. В нем сертификат используется несколькими надстройками, поэтому значение **IssuerId** не совпадает со значением **ClientId**. Обратите внимание, что ключа **ClientSecret** в надстройке SharePoint с высоким уровнем доверия нет.
 

 



```XML
<appSettings>
  <add key="ClientId" value="6569a7e8-3670-4669-91ae-ec6819ab461" />
  <add key="ClientSigningCertificatePath" value="C:\MyCerts\HighTrustCert.pfx" />
  <add key="ClientSigningCertificatePassword" value="3VeryComplexPa$$word82" />
  <add key="IssuerId" value="e9134021-0180-4b05-9e7e-0a9e5a524965" />
</appSettings>

```


 **Примечание по безопасности.** В предыдущем примере предполагается, что сертификат хранится в файловой системе. Это приемлемо при разработке и отладке. В рабочей надстройке SharePoint с высоким уровнем доверия сертификат обычно размещается в хранилище сертификатов Windows, а ключи **ClientSigningCertificatePath** и **ClientSigningCertificatePassword** обычно заменяются ключом **ClientSigningCertificateSerialNumber**.
 


## <a name="it-staff-responsibilities-in-the-high-trust-system"></a>Обязанности сотрудников ИТ-подразделения в системе высоким уровнем доверия
<a name="ITPro"> </a>

Разработчикам необходимо понимать описанные выше требования к безопасности приложений, но ИТ-специалисты будут реализовывать инфраструктуру, необходимую для ее поддержки. Поэтому им необходимо планировать выполнение указанных ниже эксплуатационных требований.
 

 

- Создание или покупка одного или нескольких сертификатов, которые будут использоваться для доверенных Надстройки SharePoint.
    
 
- Убедитесь, сертификаты безопасно хранятся на серверах веб-приложений. Если используется ОС Windows, сертификаты размещаются в хранилище сертификатов Windows.
    
 
- Управление распределением этих сертификатов среди разработчиков, собирающих Надстройки SharePoint.
    
 
- Отслеживание распространения каждого сертификата как для надстроек, использующих его, так и для разработчиков, которые получили копию. Чтобы отозвать сертификат, ИТ-специалистам понадобится связаться с каждым разработчиком, чтобы договориться о переходе на новый сертификат.
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="AR"> </a>


-  [Создание надстроек SharePoint с высоким уровнем доверия](create-high-trust-sharepoint-add-ins)
    
 
-  [Упаковка и публикация надстроек SharePoint с высоким уровнем доверия](package-and-publish-high-trust-sharepoint-add-ins)
    
 
-  [Советы по устранению неполадок в надстройках с высоким уровнем доверия в SharePoint](http://blogs.technet.com/b/speschka/archive/2012/11/01/more-troubleshooting-tips-for-high-trust-apps-on-sharepoint-2013.aspx)
    
 
-  [Авторизация и проверка подлинности надстроек SharePoint](authorization-and-authentication-of-sharepoint-add-ins)
    
 

