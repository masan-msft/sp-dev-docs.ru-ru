---
title: "Скрипты настройки для SharePoint с высоким уровнем доверия"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 24dd5cb063c9d1119b692496210bacbb47e075c2
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="high-trust-configuration-scripts-for-sharepoint"></a>Скрипты настройки для SharePoint с высоким уровнем доверия
Получение настраиваемых скриптов Windows PowerShell для настройки фермы Microsoft SharePoint на использование надстройки SharePoint с высоким уровнем доверия.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 


## <a name="how-to-use-the-scripts"></a>Как использовать скрипты
<a name="Usage"> </a>

Указанные ниже скрипты используются для обозначения одного или нескольких цифровых сертификатов X.509 в качестве доверенных издателей маркеров доступа в промежуточной или производственной ферме Microsoft SharePoint. (Скрипт, который больше подходит для среды разработки Надстройки SharePoint, см. в статье  [Создание надстроек с высоким уровнем доверия для SharePoint](create-high-trust-sharepoint-add-ins.md).) Ни один набор скриптов не сможет работать в каждой ферме SharePoint, так как существует слишком много способов получения и хранения сертификатов. Поэтому обратите внимание на указанные ниже сведения.
 

 

- Скрипты предназначены для запуска в командной консоли SharePoint на любом сервере SharePoint в ферме.
    
 
- Они представляют собой черновики, которые можно настраивать.
    
 
- Они используются, когда публикуется Надстройка SharePoint с высоким уровнем доверия. Их должен запускать только пользователь, изучивший статьи  [Создание надстроек для SharePoint, которые используют авторизацию с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization.md) и [Упаковка и публикация надстроек с высоким уровнем доверия для SharePoint](package-and-publish-high-trust-sharepoint-add-ins.md), а также описанные в них необходимые условия.
    
 
- Кроме того, в случае необходимости эти скрипты должен просматривать и настраивать специалист, знакомый с политиками сертификата пользователя надстройки.
    
 
- В двух основных скриптах ниже, **HighTrustConfig-ForSharedCertificate.ps1** и **HighTrustConfig-ForSingleApp.ps1**, предполагается, что администратор получил сертификаты для компонента удаленного веб-приложения надстройки или надстроек и что администратор временно сохранил CER-файл сертификатов (без закрытого ключа) в папке, к которой у учетных записей пользователей для следующих пулов приложений IIS на серверах SharePoint есть доступ для чтения:
    
      -  **SecurityTokenServiceApplicationPool**
    
 
  - Пул надстроек, обслуживающий веб-сайт IIS, на котором размещается родительское веб-приложение SharePoint для тестового веб-сайта SharePoint. Пул для веб-сайта IIS **SharePoint - 80** называется **OServerPortalAppPool**.
    
 

    Чтобы найти учетную запись пользователя, которую применяет пул приложений, откройте диспетчер служб IIS на сервере SharePoint и дважды щелкните элемент **Пулы приложений** в области **Подключения**. В столбце **Удостоверение** в списке **Пулы приложений** отображаются пользователи пулов приложений.
    
 
- В инструкциях для двух основных скриптов также предполагается, что сертификаты установлены в службах IIS на серверах, на которых размещаются удаленные веб-приложения. Указания см. в разделе  [Настройка удаленного веб-сервера с помощью сертификата](package-and-publish-high-trust-sharepoint-add-ins.md#ConfigureRemote).
    
 
Рекомендации по использованию скриптов приводятся в разделах ниже.
 

 

## <a name="addsprootauthorityps1"></a>AddSPRootAuthority.ps1
<a name="RootScript"> </a>

Сертификат компонента удаленного веб-приложения Надстройка SharePoint выдает коммерческий центр сертификации (ЦС) или ЦС домена. В обоих случаях сертификат это самое нижнее звено в цепочке сертификатов, где каждый сертификат доверяют стоящему выше сертификату. При этом данный сертификат получен от корневого ЦС (коммерческого или доменного). SharePoint требует, чтобы  *все*  сертификаты в цепочке были добавлены в список доверенных корневых ЦС SharePoint. Скрипт, представленный далее, можно использовать, чтобы добавить каждый сертификат из цепочки ( *кроме самого нижнего*  ) в список. Самый нижний сертификат в цепочке, который напрямую привязан к удаленному веб-приложению, добавляется в корневые ЦС в одном из основных скриптов, описанных в следующих разделах.
 

 
Ниже перечислены параметры скрипта.
 

 


|**Параметр**|**Значение**|
|:-----|:-----|
|-CertPath|Полный путь и имя файла сертификата (CER-файла).|
|-CertName|Имя сертификата. Его можно найти в свойствах сертификата.|
Например, в распространенном сценарии, когда сертификат веб-приложения выдан промежуточным сервером ЦС (который также называют "корпоративным), сертификат которого, в свою очередь, выдан корневым сервером ЦС (который также называют "автономным"), скрипт следует выполнить один раз для каждого сертификата двух серверов ЦС. Далее показан пример:
 

 



```
./AddSPRootAuthority.ps1 -CertPath "\\CertStorage\RootCA.cer" -CertName "Contoso Root CA"

./AddSPRootAuthority.ps1 -CertPath "C:\RegionalCerts\NorthRegion.cer" -CertName "North Region Intermediate CA"

```

Если все сертификаты Надстройки SharePoint с высоким уровнем доверия клиента получены из одной цепочки сертификатов, что встречается довольно часто, этот скрипт больше не используется.
 

 
Далее представлен код скрипта. Просто вставьте его в любой текстовый редактор или редактор PowerShell (IPowerShell ISE) и сохраните его как AddSPRootAuthority.ps1.
 

 

 **Примечание** Файл необходимо сохранить в формате ANSI, а не UTF-8. При выполнении файла в формате, отличном от ANSI, в PowerShell могут возникать ошибки синтаксиса. По умолчанию приложение Блокнот и редактор PowerShell сохраняют файлы в формате ANSI. Если для сохранения файла используется другой редактор, обязательно выберите формат ANSI.
 




```
param(
    [Parameter(Mandatory)][String] $CertName = $(throw "Usage: AddSPRootAuthority.ps1 -CertPath <full path to .cer file> -CertName <name of certificate>"),
    [Parameter(Mandatory)][String] $CertPath
)
# Stop if there's an error
$ErrorActionPreference = "Stop"

# Make the certificate a trusted root authority in SharePoint
$cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($CertPath)
New-SPTrustedRootAuthority -Name $CertName -Certificate $cert

```


## <a name="hightrustconfig-forsharedcertificateps1"></a>HighTrustConfig-ForSharedCertificate.ps1
<a name="MultipleAppScript"> </a>

Основная задача этого скрипта регистрация общего сертификата компонентов удаленного веб-приложения в нескольких Надстройки SharePoint с высоким уровнем доверия в SharePoint в качестве корневого ЦС и в качестве доверенного издателя маркеров доступа. Этот скрипт не используется, если клиент применяет отдельные сертификаты для каждого Надстройка SharePoint с высоким уровнем доверия. Для этого сценария см. скрипт  [HighTrustConfig-ForSingleApp.ps1](#SingleAppScript) ниже. Если все надстройки используют один сертификат, то этот скрипт будет выполнен всего один раз. Если некоторые наборы надстроек используют отличающиеся сертификаты из других наборов, то этот скрипт будет выполнен по одному разу для каждого набора.
 

 
В таблице ниже представлены параметры скрипта. В процессе настройки скрипта может потребоваться внесение изменений в эту таблицу.
 

 


|**Параметр**|**Значение**|
|:-----|:-----|
|-CertPath (обязательный)|Полный путь к общему CER-файлу.|
|-CertName (обязательный)|Имя общего сертификата. Чтобы найти его, откройте диспетчер служб IIS на удаленном веб-сервере, на котором размещено удаленное веб-приложение. Выделите узел  _имя сервера_ и дважды щелкните элемент **Сертификаты**. После этого появится имя сертификата.  |
|-TokenIssuerFriendlyName (необязательный)|Уникальное понятное имя издателя маркеров длиной до 50 символов. Это может быть удобно при отладке проблем, связанных с издателями маркеров. Имя должно быть уникальным. Чтобы обеспечить это, можно использовать GUID, но он использует 32 из 50 символов, поэтому GUID можно преобразовать в строку Base 64, а затем сократить эту строку до 22 символов. Если этот параметр не применяется, сценарий использует имя "High-Trust Add-ins _<base64 version of issuer GUID>_".|
Ниже приведен пример выполнения этого скрипта.
 

 
 `./HighTrustConfig-ForSharedCertificate.ps1 -CertPath "C:\Certs\MyCert.cer" -CertName "My Cert" -TokenIssuerFriendlyName "SharePoint High-Trust Add-ins Token Issuer"`
 

 

 **Важно!** Регистрация сертификата в качестве поставщика маркера не вступает в силу немедленно. Может потребоваться до 24 часов, пока все серверы SharePoint не получат сведения о новом поставщике. Если выполнить команду iisreset на всех серверах SharePoint, поставщик будет зарегистрирован немедленно (используйте этот метод, если вы уверены, что работа пользователей SharePoint не будет нарушена).
 

Создайте файл в текстовом редакторе или редакторе PowerShell, скопируйте в него следующий код и сохраните файл как HighTrustConfig-ForSharedCertificate.ps1. Используйте формат ANSI, а не UTF-8.
 

 



```
param(
    [Parameter(Mandatory)][String] $CertPath = $(throw "Usage: HighTrustConfig-ForSharedCertificate.ps1 -CertPath <full path to .cer file> -CertName <name of certificate> [-TokenIssuerFriendlyName <friendly name>]"),
    [Parameter(Mandatory)][String] $CertName,
    [Parameter()][String] $TokenIssuerFriendlyName
) 
# Stop if there's an error
$ErrorActionPreference = "Stop"

# Ensure friendly name is short enough
if ($TokenIssuerFriendlyName.Length -gt 50)
{
    throw "-TokenIssuerFriendlyName must be unique name of no more than 50 characters."
} 

# Get the certificate
$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($CertPath)

# Make the certificate a trusted root authority in SharePoint
New-SPTrustedRootAuthority -Name $CertName -Certificate $certificate 

# Get the GUID of the authentication realm
$realm = Get-SPAuthenticationRealm

# Generate a unique specific issuer ID
$specificIssuerId = [System.Guid]::NewGuid().ToString()

# Create full issuer ID in the required format
$fullIssuerIdentifier = $specificIssuerId + '@' + $realm 

# Create issuer name
if ($TokenIssuerFriendlyName.Length -ne 0)
{
    $tokenIssuerName = $TokenIssuerFriendlyName
}
else
{
    $tokenIssuerName = "High-Trust Add-ins " + [System.Convert]::ToBase64String($specificIssuerId.ToByteArray()).TrimEnd('=') 
}

# Register the token issuer
New-SPTrustedSecurityTokenIssuer -Name $tokenIssuerName -Certificate $certificate -RegisteredIssuerName $fullIssuerIdentifier -IsTrustBroker

# Output the specific issuer ID to a file in the same folder as this script. The file should be given to the developer of the high-trust SharePoint Add-in.
$specificIssuerId | select * | Out-File -FilePath "SecureTokenIssuerID.txt"
```


 **Совет.** Если после успешного выполнения строки `New-SPTrustedRootAuthority` скрипта возникает ошибка, скрипт не удастся выполнить повторно, пока не будет удален этот объект. Используйте для этого командлет `Remove-SPTrustedRootAuthority -Identity <certificate name>`, где для параметра `-Identity` укажите то же значение, которое было задано для параметра `-CertName` в скрипте. Если по какой-либо причине необходимо удалить поставщик маркеров, это можно сделать с помощью командлета `Remove-SPTrustedSecurityTokenIssuer -Identity <issuer name>`. Если используется параметр `-TokenIssuerFriendlyName`, укажите для параметра `-Identity` то же значение. Если параметр `-TokenIssuerFriendlyName`не используется, случайный GUID является частью имени издателя. Чтобы получить значение, которое требуется для параметра `-Identity`, запустите командлет `Get-SPTrustedSecurityTokenIssuer | Out-File -FilePath "TokenIssuers.txt"`. Затем откройте возвращенный файл TokenIssuers.txt и найдите поставщик с именем "High-Trust Add-ins _<base64 version of issuer GUID>_". Для параметра `-Identity` укажите это имя полностью.
 


## <a name="hightrustconfig-forsingleappps1"></a>HighTrustConfig-ForSingleApp.ps1
<a name="SingleAppScript"> </a>

Основная цель этого скрипта регистрация сертификата удаленного веб-приложения в Надстройка SharePoint с высоким уровнем доверия в SharePoint в качестве корневого ЦС и как доверенного поставщика маркеров доступа. Этот скрипт не используется, если клиент применяет один сертификат для нескольких Надстройки SharePoint. В этом случае см. раздел  [HighTrustConfig-ForSharedCertificate.ps1](#MultipleAppScript) выше. Этот скрипт выполняется для всех Надстройка SharePoint с высоким уровнем доверия.
 

 
В таблице ниже представлены параметры скрипта. В процессе настройки скрипта может потребоваться внесение изменений в эту таблицу.
 

 


|**Параметр**|**Значение**|
|:-----|:-----|
|-CertPath (обязательный)|Полный путь к общему CER-файлу.|
|-CertName (обязательный)|Имя общего сертификата. Чтобы найти его, откройте диспетчер служб IIS на удаленном веб-сервере, на котором размещено удаленное веб-приложение. Выделите узел  _имя сервера_ и дважды щелкните элемент **Сертификаты**. После этого появится имя сертификата.  |
|-SPAppClientID (обязательный)|Идентификатор клиента (GUID), который использовался при регистрации Надстройка SharePoint в appregnew.aspx. Он применяется как идентификатор поставщика маркеров. Скрипт проверяет, что в идентификаторе используются только строчные буквы, что является обязательным для идентификаторов поставщиков.|
|-TokenIssuerFriendlyName (необязательный)|Понятное имя поставщика маркеров длиной до 50 символов. Оно может быть полезно при отладке проблем с поставщиками маркеров. Имя должно быть уникальным. Вы можете использовать имя Надстройка SharePoint. Если этот параметр не используется, скрипт применяет в качестве имени значение  `-SPAppClientID`.|
Далее показан пример вызова скрипта:
 

 
 `./HighTrustConfig-ForSingleApp.ps1 -CertPath "\\MyServer\Certs\MyCert.cer" -CertName "My Cert" -SPAppClientID "afe332f4-1f87-4c31-89b8-9c343ad7f24e" -TokenIssuerFriendlyName "Payroll add-in"`
 

 

 **Важно!** Регистрация сертификата в качестве поставщика маркера не вступает в силу немедленно. Может потребоваться до 24 часов, пока все серверы SharePoint не получат сведения о новом поставщике. Если выполнить команду iisreset на всех серверах SharePoint, поставщик будет зарегистрирован немедленно (используйте этот метод, если вы уверены, что работа пользователей SharePoint не будет нарушена).
 

Создайте файл в текстовом редакторе или редакторе PowerShell, скопируйте в него следующий код и сохраните файл как HighTrustConfig-ForSingleApp.ps1. Используйте формат ANSI, а не UTF-8.
 

 



```
param(
    [Parameter(Mandatory)][String] $CertPath = $(throw "Usage: HighTrustConfig-ForSingleApp.ps1 -CertPath <full path to .cer file> -CertName <name of certificate> [-SPAppClientID <client ID of SharePoint add-in>] [-TokenIssuerFriendlyName <friendly name>]"),
    [Parameter(Mandatory)][String] $CertName,
    [Parameter(Mandatory)][String] $SPAppClientID,
    [Parameter()][String] $TokenIssuerFriendlyName
) 
# Stop if there's an error
$ErrorActionPreference = "Stop"

# Ensure friendly name is short enough
if ($TokenIssuerFriendlyName.Length -gt 50)
{
    throw "-TokenIssuerFriendlyName must be unique name of no more than 50 characters."
} 

# Get the certificate
$certificate = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($CertPath)

# Make the certificate a trusted root authority in SharePoint
New-SPTrustedRootAuthority -Name $CertName -Certificate $certificate 

# Get the GUID of the authentication realm
$realm = Get-SPAuthenticationRealm

# Must use the client ID as the specific issuer ID. Must be lower-case!
$specificIssuerId = New-Object System.String($SPAppClientID).ToLower()

# Create full issuer ID in the required format
$fullIssuerIdentifier = $specificIssuerId + '@' + $realm 

# Create issuer name
if ($TokenIssuerFriendlyName.Length -ne 0)
{
    $tokenIssuerName = $TokenIssuerFriendlyName
}
else
{
    $tokenIssuerName = $specificIssuerId 
}

# Register the token issuer
New-SPTrustedSecurityTokenIssuer -Name $tokenIssuerName -Certificate $certificate -RegisteredIssuerName $fullIssuerIdentifier

```


 **Совет.** Советы, указанные в конце предыдущего раздела, применимы и здесь, но в качестве значения параметра `-Identity` командлета `Remove-SPTrustedSecurityTokenIssuer` используйте идентификатор клиента, если параметр `-TokenIssuerFriendlyName` не применялся для сценария HighTrustConfig-ForSingleApp.ps1.
 


## <a name="modifications-needed-for-site-subscriptions"></a>Изменения, которые необходимо внести в подписки на сайт
<a name="SiteSubscriptions"> </a>

Подписка сайта, которую иногда называют областью клиентов, это подмножество семейств веб-сайтов в ферме SharePoint. Подписки сайта обычно создаются в размещенных фермах SharePoint. Если клиент Надстройка SharePoint с высоким уровнем доверия хочет установить надстройку в ферме, которая настроена для подписок сайта, необходимо изменить используемый скрипт HighTrustConfig-*.ps1. У каждой подписки сайта есть собственный идентификатор области, но строка  `$realm = Get-SPAuthenticationRealm` в скриптах всегда возвращает область фермы. SharePoint считает маркеры доступа, выданные издателем маркеров, допустимыми только для области, указанной после символа @ в полном идентификаторе издателя. Чтобы получить правильную область для веб-сайта, на котором будет установлена надстройка, скрипт должен использовать параметр `-ServiceContext` в вызове командлета `Get-SPAuthenticationRealm`. Объект контекста службы, в свою очередь, создается на основе родительского семейства веб-сайтов целевого веб-сайта. Далее представлен пример, в котором  `$WebURL` это строковая переменная с полным URL-адресом веб-сайта SharePoint, например http://marketing.contoso.com/sites/northteam/july. Этот код позволяет запускать надстройку с высоким уровнем доверия не только на указанном веб-сайте, но и на любом сайте в рамках одной подписки сайта.
 

 

```
$Web = Get-SPWeb $WebURL
$sc = Get-SPServiceContext -Site $Web.Site
$realm = Get-SPAuthenticationRealm -ServiceContext $sc
```

Чтобы завершить изменение сертификата, добавьте обязательный параметр  `$WebURL` в список параметров в начале файла следующим образом:
 

 



```
param (
    # other parameters omitted 
    [Parameter()][String] $WebURL
)
```

Не забудьте добавить запятую после параметра перед новым параметром. Разверните пример Usage в верхней строке, чтобы учесть новый параметр. Пример:  `-WebURL <full URL where SP add-in will be installed>`.
 

 
Чтобы Надстройка SharePoint было доверенным для каждой подписки сайта, получите ссылку на ферму с помощью командлета  `Get-SPFarm`, а затем выполните перебор по свойству **SiteSubscriptions**. Передайте каждый объект **SPSiteSubscription** командлету `Get-SPServiceContext` как значение параметра `-SiteSubscription`. Далее представлен пример.
 

 



```
$Farm = Get-SPFarm
foreach ($ss in $Farm.SiteSubscriptions)
{
    $sc = Get-SPServiceContext -SiteSubscription $ss
    $realm = Get-SPAuthenticationRealm -ServiceContext $sc

    # All of the lines from the draft script below the call to 
    # Get-SPAuthenticationRealm are inserted here inside the loop.
}
# end of script
```


