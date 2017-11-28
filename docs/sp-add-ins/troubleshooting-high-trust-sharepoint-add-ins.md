---
title: "Устранение неполадок надстроек SharePoint с высоким уровнем доверия"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: f195d06c28eae988551d2bd4eb2add49007876dc
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="troubleshooting-high-trust-sharepoint-add-ins"></a>Устранение проблем с надстройками SharePoint с высоким уровнем доверия
Описание решений некоторых проблем, возникающих при разработке надстроек SharePoint с высоким уровнем доверия.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 

В этой статье описывается средство Fiddler, а также представлены рекомендации по устранению некоторых конкретных проблем.
 

## <a name="use-the-fiddler-tool"></a>Использование средства Fiddler

С помощью бесплатного  [средства Fiddler](http://www.telerik.com/fiddler) можно захватывать HTTP-запросы, отправляемые удаленным компонентом вашей надстройки в SharePoint. Для этого [средства есть бесплатное расширение](https://github.com/andrewconnell/SPOAuthFiddlerExt), которое автоматически декодирует маркеры доступа в запросах.
 

 
Установив Fiddler на сервере веб-приложений, добавьте в файл web.config следующую разметку, чтобы запросы удаленного веб-приложения проходили через данный прокси-сервер. Таким образом вы сможете отследить трассировку Fiddler и целиком увидеть отклик SharePoint при возникновении ошибки.
 

 

 **Примечание.** Если вы не используете Fiddler, обязательно удалите эту разметку. В противном случае ваша надстройка не сможет выполнять HTTP-запросы.
 




```XML
<system.net>
  <defaultProxy>
    <proxy usesystemdefault="False" bypassonlocal="False" proxyaddress="http://127.0.0.1:8888" />
  </defaultProxy>
</system.net>

```

Установив Fiddler, вы можете проверить заголовки ответов от SharePoint, включая GUID запроса. Данный GUID запроса идентификатор корреляции, с помощью которого можно находить в журналах ошибки, связанные с этим запросом.
 

 

## <a name="401-unauthorized-error"></a>Ошибка "401 - Не санкционировано"
<a name="UnauthorizedException"> </a>

Ошибка авторизации **401 - Не санкционировано** может возникать по нескольким причинам, когда надстройка с высоким уровнем доверия впервые обращается к SharePoint. Если вы используете клиентскую объектную модель (CSOM), ошибка выглядит примерно так:
 

 

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

При использовании файла TokenHelper и удостоверения Windows код, вызывающий исключение, выглядит так:
 

 



```C#
ClientContext clientContext = 
    TokenHelper.GetS2SClientContextWithWindowsIdentity(sharepointUrl, Request.LogonUserIdentity); 
clientContext.Load(clientContext.Web);
clientContext.ExecuteQuery();
```

Чтобы устранить эту проблему, в первую очередь необходимо с помощью отладчика Visual Studio проверить, успешно ли созданы маркер доступа и объект **ClientContext**. Если это так, необходимо проверить описанные ниже возможности.
 

 
 **Возможные проблемы и способы их решения.**
 

 

- Для пользователя, обращающегося к удаленному веб-приложению, не создан профиль. Создайте профиль пользователя.
    
 
- У вашей надстройки отсутствует разрешение на ресурсы, к которым вы собираетесь получить доступ. Откройте Командная консоль SharePoint и запустите следующий командлет Windows PowerShell. Переменная  `$web` представляет веб-сайт SharePoint, к которому вы пытаетесь получить доступ, а `$appPrincipal` идентификатор надстройки. Дополнительные сведения см. в статье [Set-SPAppPrincipalPermission](http://technet.microsoft.com/ru-RU/library/jj219714%28v=office.15%29.aspx).
    
```
  Set-SPAppPrincipalPermission -Site $web -AppPrincipal $appPrincipal -Scope Site -Right FullControl
```

- Ваше веб-приложение принимает анонимные запросы. Это значит, что в маркере доступа нет действительного удостоверения пользователя. Убедитесь, что в службах IIS для корневого каталога вашего удаленного веб-приложения отключен анонимный доступ. Это также можно проверить, выполнив отладку удаленного веб-приложения и проверив значение **Request.LogonUserIdentity** в файле default.aspx (с расширением CS или VB), чтобы убедиться, что пользователь не является анонимным.
    
 
- Цифровой сертификат не был добавлен в хранилище доверенных сертификатов. Обязательно выполните процедуры, описанные в статье  [Упаковка и публикация надстроек с высоким уровнем доверия для SharePoint](package-and-publish-high-trust-sharepoint-add-ins.md).
    
 

## <a name="miscellaneous-ssl-and-domain-related-authorization-errors"></a>Прочие ошибки авторизации, связанные с протоколом SSL и доменами
<a name="DomainRelatedErrors"> </a>

Авторизации может препятствовать несовпадение доменных имен в файлах конфигурации и регистрационных формах. Следующие четыре значения должны полностью совпадать:
 

 

- **Домен надстройки**, который указывается при регистрации надстройки SharePoint на странице AppRegNew.aspx.
    
 
- Домен, на котором зарегистрирован сертификат безопасности удаленного веб-приложения.
    
 
- Доменная часть значения **StartPage** в файле AppManifest.xml.
    
 
- Доменная часть URL-адресов всех приемников событий, указанных в файле AppManifest.xml.
    
 
В связи с этим учтите указанные ниже особенности.
 

 

- Если ваше Надстройка SharePoint содержит удаленный компонент, использующий какой-либо другой порт, чем 443, вам необходимо явным образом включить порт как часть домена во всех четырех местах, например  `MarketingServer:3333`. (Необходимо использовать протокол HTTPS, порт по умолчанию для которого 443.)
    
 
- Домен должен быть жестко задан с помощью значения **StartPage** (и URL-адресе каждого приемника событий) в файле AppManifest.xml до упаковки надстройки. Если для упаковки надстройки используется мастер **публикации** в Visual Studio, вам будет предложено указать домен, а Инструменты разработчика Office для Visual Studio автоматически вставят его в значение **StartPage** (вместо маркера `~remoteWebUrl`, который используется при отладке). Но если вы не используете мастер **публикации**, вам потребуется вручную заменить маркер на домен (и протокол), например `https://MarketingServer` или `https://MarketingServer:3333`.
    
 

## <a name="runtime-error-saying-that-theres-no-certificate-with-that-serial-number"></a>Ошибка выполнения с сообщением об отсутствии сертификата с этим серийным номером
<a name="DomainRelatedErrors"> </a>

Если вы уверены в правильности серийного номера сертификата в файле web.config, а сертификат отображается в **хранилище сертификатов Windows**, то, скорее всего, в серийном номере из файла web.config есть дополнительный скрытый символ. Такое бывает, если серийный номер скопирован и вставлен из **консоли управления (MMC)**. Полностью удалите значение серийного номера из файла web.config и повторно введите его *вручную*.
 

 

