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
# <a name="high-trust-configuration-scripts-for-sharepoint"></a><span data-ttu-id="79283-102">Скрипты настройки для SharePoint с высоким уровнем доверия</span><span class="sxs-lookup"><span data-stu-id="79283-102">High-trust configuration scripts for SharePoint</span></span>
<span data-ttu-id="79283-103">Получение настраиваемых скриптов Windows PowerShell для настройки фермы Microsoft SharePoint на использование надстройки SharePoint с высоким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="79283-103">Get customizable Windows PowerShell scripts that configure a Microsoft SharePoint farm to use a high-trust SharePoint Add-in.</span></span>
 

 <span data-ttu-id="79283-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="79283-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="how-to-use-the-scripts"></a><span data-ttu-id="79283-107">Как использовать скрипты</span><span class="sxs-lookup"><span data-stu-id="79283-107">How to use the scripts</span></span>
<span data-ttu-id="79283-108"><a name="Usage"> </a></span><span class="sxs-lookup"><span data-stu-id="79283-108"></span></span>

<span data-ttu-id="79283-p102">Указанные ниже скрипты используются для обозначения одного или нескольких цифровых сертификатов X.509 в качестве доверенных издателей маркеров доступа в промежуточной или производственной ферме Microsoft SharePoint. (Скрипт, который больше подходит для среды разработки Надстройки SharePoint, см. в статье  [Создание надстроек с высоким уровнем доверия для SharePoint](create-high-trust-sharepoint-add-ins.md).) Ни один набор скриптов не сможет работать в каждой ферме SharePoint, так как существует слишком много способов получения и хранения сертификатов. Поэтому обратите внимание на указанные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="79283-p102">The scripts below are used to designate one or more X.509 digital certificates as trusted issuers of access tokens in a staging or production Microsoft SharePoint farm. (For a script that is more appropriate for an SharePoint Add-ins development environment, see  [Create high-trust SharePoint Add-ins](create-high-trust-sharepoint-add-ins.md).) No single set of scripts can work for every SharePoint farm because there are too many different ways that the certificates can be acquired and stored. For that reason, please note the following:</span></span>
 

 

- <span data-ttu-id="79283-112">Скрипты предназначены для запуска в командной консоли SharePoint на любом сервере SharePoint в ферме.</span><span class="sxs-lookup"><span data-stu-id="79283-112">The scripts are meant to be run in SharePoint Management Shell on any SharePoint server in the farm.</span></span>
    
 
- <span data-ttu-id="79283-113">Они представляют собой черновики, которые можно настраивать.</span><span class="sxs-lookup"><span data-stu-id="79283-113">These scripts should be thought of as drafts that may need to be customized.</span></span>
    
 
- <span data-ttu-id="79283-p103">Они используются, когда публикуется Надстройка SharePoint с высоким уровнем доверия. Их должен запускать только пользователь, изучивший статьи  [Создание надстроек для SharePoint, которые используют авторизацию с высоким уровнем доверия](creating-sharepoint-add-ins-that-use-high-trust-authorization.md) и [Упаковка и публикация надстроек с высоким уровнем доверия для SharePoint](package-and-publish-high-trust-sharepoint-add-ins.md), а также описанные в них необходимые условия.</span><span class="sxs-lookup"><span data-stu-id="79283-p103">They are used as part of the overall process of publishing a high-trust SharePoint Add-in. They should only be used by someone familiar with the topics  [Creating SharePoint Add-ins that use high-trust authorization](creating-sharepoint-add-ins-that-use-high-trust-authorization.md) and [Package and publish high-trust SharePoint Add-ins](package-and-publish-high-trust-sharepoint-add-ins.md) and the prerequisites listed in them.</span></span>
    
 
- <span data-ttu-id="79283-116">Кроме того, в случае необходимости эти скрипты должен просматривать и настраивать специалист, знакомый с политиками сертификата пользователя надстройки.</span><span class="sxs-lookup"><span data-stu-id="79283-116">They should also be reviewed and customized as needed by someone familiar with the add-in customer's certificate policies.</span></span>
    
 
- <span data-ttu-id="79283-117">В двух основных скриптах ниже, **HighTrustConfig-ForSharedCertificate.ps1** и **HighTrustConfig-ForSingleApp.ps1**, предполагается, что администратор получил сертификаты для компонента удаленного веб-приложения надстройки или надстроек и что администратор временно сохранил CER-файл сертификатов (без закрытого ключа) в папке, к которой у учетных записей пользователей для следующих пулов приложений IIS на серверах SharePoint есть доступ для чтения:</span><span class="sxs-lookup"><span data-stu-id="79283-117">The two major scripts below,  **HighTrustConfig-ForSharedCertificate.ps1** and **HighTrustConfig-ForSingleApp.ps1**, assume that an administrator has acquired a certificate for the remote web application component of the add-in or add-ins and that the administrator has temporarily stored a .cer version of the certificate (that does not contain the private key) in a folder to which the user accounts for the following IIS application pools on the SharePoint servers have Read access:</span></span>
    
      -  <span data-ttu-id="79283-118">**SecurityTokenServiceApplicationPool**</span><span class="sxs-lookup"><span data-stu-id="79283-118">**SecurityTokenServiceApplicationPool**</span></span>
    
 
  - <span data-ttu-id="79283-p104">Пул надстроек, обслуживающий веб-сайт IIS, на котором размещается родительское веб-приложение SharePoint для тестового веб-сайта SharePoint. Пул для веб-сайта IIS **SharePoint - 80** называется **OServerPortalAppPool**.</span><span class="sxs-lookup"><span data-stu-id="79283-p104">The add-in pool that serves the IIS web site that hosts the parent SharePoint web application for your test SharePoint website. For the  **SharePoint - 80** IIS website, the pool is called **OServerPortalAppPool**.</span></span>
    
 

    <span data-ttu-id="79283-p105">Чтобы найти учетную запись пользователя, которую применяет пул приложений, откройте диспетчер служб IIS на сервере SharePoint и дважды щелкните элемент **Пулы приложений** в области **Подключения**. В столбце **Удостоверение** в списке **Пулы приложений** отображаются пользователи пулов приложений.</span><span class="sxs-lookup"><span data-stu-id="79283-p105">To find the user account that an application pool is using, open IIS Manager on a SharePoint server and double-click  **Application Pools** in the **Connections** pane. The **Identity** column in the **Application Pools** list that opens shows the users for the application pools.</span></span>
    
 
- <span data-ttu-id="79283-p106">В инструкциях для двух основных скриптов также предполагается, что сертификаты установлены в службах IIS на серверах, на которых размещаются удаленные веб-приложения. Указания см. в разделе  [Настройка удаленного веб-сервера с помощью сертификата](package-and-publish-high-trust-sharepoint-add-ins.md#ConfigureRemote).</span><span class="sxs-lookup"><span data-stu-id="79283-p106">The instructions for the two major scripts also assume that the certificate(s) have been installed to IIS on server(s) that host the remote web application(s). For instructions, see  [Configure the remote web server with the certificate](package-and-publish-high-trust-sharepoint-add-ins.md#ConfigureRemote).</span></span>
    
 
<span data-ttu-id="79283-125">Рекомендации по использованию скриптов приводятся в разделах ниже.</span><span class="sxs-lookup"><span data-stu-id="79283-125">See specific usage notes for each script in the sections below.</span></span>
 

 

## <a name="addsprootauthorityps1"></a><span data-ttu-id="79283-126">AddSPRootAuthority.ps1</span><span class="sxs-lookup"><span data-stu-id="79283-126">AddSPRootAuthority.ps1</span></span>
<span data-ttu-id="79283-127"><a name="RootScript"> </a></span><span class="sxs-lookup"><span data-stu-id="79283-127"></span></span>

<span data-ttu-id="79283-p107">Сертификат компонента удаленного веб-приложения Надстройка SharePoint выдает коммерческий центр сертификации (ЦС) или ЦС домена. В обоих случаях сертификат это самое нижнее звено в цепочке сертификатов, где каждый сертификат доверяют стоящему выше сертификату. При этом данный сертификат получен от корневого ЦС (коммерческого или доменного). SharePoint требует, чтобы  *все*  сертификаты в цепочке были добавлены в список доверенных корневых ЦС SharePoint. Скрипт, представленный далее, можно использовать, чтобы добавить каждый сертификат из цепочки ( *кроме самого нижнего*  ) в список. Самый нижний сертификат в цепочке, который напрямую привязан к удаленному веб-приложению, добавляется в корневые ЦС в одном из основных скриптов, описанных в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="79283-p107">The certificate of the remote web application component of the high-trust SharePoint Add-in is obtained from either a commercial Certificate Authority (CA) or a domain CA. In either case, the certificate is the lowest link in a chain of certificates, each trusting the one above it, which originates with a root CA (commercial or domain). SharePoint requires that  *all*  the certificates in the chain be added to SharePoint's list of trusted root authorities. The script below can be used to add each certificate in the chain *except the lowest one*  to the list. The lowest certificate in the chain, the certificate that is directly bound to the remote web application, is added to the root authorities in one of the major scripts described in later sections.</span></span>
 

 
<span data-ttu-id="79283-133">Ниже перечислены параметры скрипта.</span><span class="sxs-lookup"><span data-stu-id="79283-133">The parameters for the script are the following:</span></span>
 

 


|<span data-ttu-id="79283-134">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="79283-134">**Parameter**</span></span>|<span data-ttu-id="79283-135">**Значение**</span><span class="sxs-lookup"><span data-stu-id="79283-135">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="79283-136">-CertPath</span><span class="sxs-lookup"><span data-stu-id="79283-136">-CertPath</span></span>|<span data-ttu-id="79283-137">Полный путь и имя файла сертификата (CER-файла).</span><span class="sxs-lookup"><span data-stu-id="79283-137">The full path and filename of the certificate (the .cer file).</span></span>|
|<span data-ttu-id="79283-138">-CertName</span><span class="sxs-lookup"><span data-stu-id="79283-138">-CertName</span></span>|<span data-ttu-id="79283-p108">Имя сертификата. Его можно найти в свойствах сертификата.</span><span class="sxs-lookup"><span data-stu-id="79283-p108">The name of the certificate. To find the name, view the properties of the certificate.</span></span>|
<span data-ttu-id="79283-p109">Например, в распространенном сценарии, когда сертификат веб-приложения выдан промежуточным сервером ЦС (который также называют "корпоративным), сертификат которого, в свою очередь, выдан корневым сервером ЦС (который также называют "автономным"), скрипт следует выполнить один раз для каждого сертификата двух серверов ЦС. Далее показан пример:</span><span class="sxs-lookup"><span data-stu-id="79283-p109">For example, in the common scenario where the web application's certificate is issued by an intermediate (also called 'enterprise') CA server and its certificate, in turn, is issued by a root (also called 'standalone') CA server, the script should be run once for each of the certificates of the two CA servers. The following shows this:</span></span>
 

 



```
./AddSPRootAuthority.ps1 -CertPath "\\CertStorage\RootCA.cer" -CertName "Contoso Root CA"

./AddSPRootAuthority.ps1 -CertPath "C:\RegionalCerts\NorthRegion.cer" -CertName "North Region Intermediate CA"

```

<span data-ttu-id="79283-143">Если все сертификаты Надстройки SharePoint с высоким уровнем доверия клиента получены из одной цепочки сертификатов, что встречается довольно часто, этот скрипт больше не используется.</span><span class="sxs-lookup"><span data-stu-id="79283-143">If all of certificates of the customer's high-trust SharePoint Add-ins come from the same chain of certificates, as would typically be the case, then this script is never used again.</span></span>
 

 
<span data-ttu-id="79283-p110">Далее представлен код скрипта. Просто вставьте его в любой текстовый редактор или редактор PowerShell (IPowerShell ISE) и сохраните его как AddSPRootAuthority.ps1.</span><span class="sxs-lookup"><span data-stu-id="79283-p110">The following is the code for the script. Simply paste it into any text editor or the PowerShell editor (IPowerShell ISE) and save it as AddSPRootAuthority.ps1.</span></span>
 

 

 <span data-ttu-id="79283-p111">**Примечание** Файл необходимо сохранить в формате ANSI, а не UTF-8. При выполнении файла в формате, отличном от ANSI, в PowerShell могут возникать ошибки синтаксиса. По умолчанию приложение Блокнот и редактор PowerShell сохраняют файлы в формате ANSI. Если для сохранения файла используется другой редактор, обязательно выберите формат ANSI.</span><span class="sxs-lookup"><span data-stu-id="79283-p111">**Note**  The file has to be saved as ANSI format, not UTF-8. PowerShell may give syntax errors when it runs a file with a non-ANSI format. NotePad and the PowerShell editor will default to saving it as ANSI. If you use any other editor to save the file, be sure you are saving it as ANSI.</span></span>
 




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


## <a name="hightrustconfig-forsharedcertificateps1"></a><span data-ttu-id="79283-150">HighTrustConfig-ForSharedCertificate.ps1</span><span class="sxs-lookup"><span data-stu-id="79283-150">HighTrustConfig-ForSharedCertificate.ps1</span></span>
<span data-ttu-id="79283-151"><a name="MultipleAppScript"> </a></span><span class="sxs-lookup"><span data-stu-id="79283-151"></span></span>

<span data-ttu-id="79283-p112">Основная задача этого скрипта регистрация общего сертификата компонентов удаленного веб-приложения в нескольких Надстройки SharePoint с высоким уровнем доверия в SharePoint в качестве корневого ЦС и в качестве доверенного издателя маркеров доступа. Этот скрипт не используется, если клиент применяет отдельные сертификаты для каждого Надстройка SharePoint с высоким уровнем доверия. Для этого сценария см. скрипт  [HighTrustConfig-ForSingleApp.ps1](#SingleAppScript) ниже. Если все надстройки используют один сертификат, то этот скрипт будет выполнен всего один раз. Если некоторые наборы надстроек используют отличающиеся сертификаты из других наборов, то этот скрипт будет выполнен по одному разу для каждого набора.</span><span class="sxs-lookup"><span data-stu-id="79283-p112">The primary tasks of this script are to register the shared certificate of the remote web application components in multiple high-trust SharePoint Add-ins with SharePoint as both a root authority and as a trusted access token issuer. This script is not used if the customer is using separate certificates with each high-trust SharePoint Add-in. For that scenario, see  [HighTrustConfig-ForSingleApp.ps1](#SingleAppScript) below. If all of the add-ins use the same certificate, then this script is run only once. If some sets of add-ins use a different certificate from other sets, then this script is run once for each set.</span></span>
 

 
<span data-ttu-id="79283-p113">В таблице ниже представлены параметры скрипта. В процессе настройки скрипта может потребоваться внесение изменений в эту таблицу.</span><span class="sxs-lookup"><span data-stu-id="79283-p113">The following table describes the parameters and switches for the script. Customization of the script may require changes to this table.</span></span>
 

 


|<span data-ttu-id="79283-159">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="79283-159">**Parameter**</span></span>|<span data-ttu-id="79283-160">**Значение**</span><span class="sxs-lookup"><span data-stu-id="79283-160">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="79283-161">-CertPath (обязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-161">-CertPath (required)</span></span>|<span data-ttu-id="79283-162">Полный путь к общему CER-файлу.</span><span class="sxs-lookup"><span data-stu-id="79283-162">The full path to the shared *.cer file.</span></span>|
|<span data-ttu-id="79283-163">-CertName (обязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-163">-CertName (required)</span></span>|<span data-ttu-id="79283-p114">Имя общего сертификата. Чтобы найти его, откройте диспетчер служб IIS на удаленном веб-сервере, на котором размещено удаленное веб-приложение. Выделите узел  _имя сервера_ и дважды щелкните элемент **Сертификаты**. После этого появится имя сертификата.  </span><span class="sxs-lookup"><span data-stu-id="79283-p114">The name of the shared certificate. To find the name, open IIS on the remote web server that hosts the remote web application. Highlight the  _server name_ node and double-click **Certificates**. The certificate will be listed by its name.</span></span>|
|<span data-ttu-id="79283-168">-TokenIssuerFriendlyName (необязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-168">-TokenIssuerFriendlyName (optional)</span></span>|<span data-ttu-id="79283-p115">Уникальное понятное имя издателя маркеров длиной до 50 символов. Это может быть удобно при отладке проблем, связанных с издателями маркеров. Имя должно быть уникальным. Чтобы обеспечить это, можно использовать GUID, но он использует 32 из 50 символов, поэтому GUID можно преобразовать в строку Base 64, а затем сократить эту строку до 22 символов. Если этот параметр не применяется, сценарий использует имя "High-Trust Add-ins _<base64 version of issuer GUID>_".</span><span class="sxs-lookup"><span data-stu-id="79283-p115">A unique friendly name for the token issuer, up to 50 characters. This can be helpful if you are debugging issues with token issuers. The name must be unique. Including a GUID would ensure that it is, but a GUID uses up 32 of the 50 characters, consider converting a GUID to a Base 64 string which can be reduced to 22 characters. If this parameter is not used, the script uses the name "High-Trust Add-ins  _<base64 version of issuer GUID>_".</span></span>|
<span data-ttu-id="79283-174">Ниже приведен пример выполнения этого скрипта.</span><span class="sxs-lookup"><span data-stu-id="79283-174">The following is an example of running this script.</span></span>
 

 
 `./HighTrustConfig-ForSharedCertificate.ps1 -CertPath "C:\Certs\MyCert.cer" -CertName "My Cert" -TokenIssuerFriendlyName "SharePoint High-Trust Add-ins Token Issuer"`
 

 

 <span data-ttu-id="79283-p116">**Важно!** Регистрация сертификата в качестве поставщика маркера не вступает в силу немедленно. Может потребоваться до 24 часов, пока все серверы SharePoint не получат сведения о новом поставщике. Если выполнить команду iisreset на всех серверах SharePoint, поставщик будет зарегистрирован немедленно (используйте этот метод, если вы уверены, что работа пользователей SharePoint не будет нарушена).</span><span class="sxs-lookup"><span data-stu-id="79283-p116">**Important**  The registration of the certificate as a token issuer is not effective immediately. It may take as long as 24 hours before all the SharePoint servers recognize the new token issuer. Running an iisreset on all the SharePoint servers would cause them to immediately recognize the issuer, if you can do that without disturbing SharePoint users.</span></span>
 

<span data-ttu-id="79283-p117">Создайте файл в текстовом редакторе или редакторе PowerShell, скопируйте в него следующий код и сохраните файл как HighTrustConfig-ForSharedCertificate.ps1. Используйте формат ANSI, а не UTF-8.</span><span class="sxs-lookup"><span data-stu-id="79283-p117">Start a new file in a text editor, or the PowerShell editor, and copy the following into a text file and save it as HighTrustConfig-ForSharedCertificate.ps1. Use ANSI format, not UTF-8.</span></span>
 

 



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


 <span data-ttu-id="79283-p118">**Совет.** Если после успешного выполнения строки `New-SPTrustedRootAuthority` скрипта возникает ошибка, скрипт не удастся выполнить повторно, пока не будет удален этот объект. Используйте для этого командлет `Remove-SPTrustedRootAuthority -Identity <certificate name>`, где для параметра `-Identity` укажите то же значение, которое было задано для параметра `-CertName` в скрипте. Если по какой-либо причине необходимо удалить поставщик маркеров, это можно сделать с помощью командлета `Remove-SPTrustedSecurityTokenIssuer -Identity <issuer name>`. Если используется параметр `-TokenIssuerFriendlyName`, укажите для параметра `-Identity` то же значение. Если параметр `-TokenIssuerFriendlyName`не используется, случайный GUID является частью имени издателя. Чтобы получить значение, которое требуется для параметра `-Identity`, запустите командлет `Get-SPTrustedSecurityTokenIssuer | Out-File -FilePath "TokenIssuers.txt"`. Затем откройте возвращенный файл TokenIssuers.txt и найдите поставщик с именем "High-Trust Add-ins _<base64 version of issuer GUID>_". Для параметра `-Identity` укажите это имя полностью.</span><span class="sxs-lookup"><span data-stu-id="79283-p118">**Tip**  If the script throws an error after the  `New-SPTrustedRootAuthority` line has run successfully, the script cannot be rerun until that object has been removed. Use the following cmdlet, where the value of the `-Identity` parameter is the same as was used for the `-CertName` parameter in the script. `Remove-SPTrustedRootAuthority -Identity <certificate name>`If the token issuer needs to be removed for any reason, use the following cmdlet: `Remove-SPTrustedSecurityTokenIssuer -Identity <issuer name>`If the  `-TokenIssuerFriendlyName` parameter was used, then use the same value for `-Identity`. If the  `-TokenIssuerFriendlyName` parameter was not used, then a random GUID is part of the issuer name. To obtain value needed for `-Identity`, run the following cmdlet. Then open the TokenIssuers.txt file that is produced and find the issuer whose name is "High-Trust Add-ins  _<base64 version of issuer GUID>_". Use that entire name for  `-Identity`.  `Get-SPTrustedSecurityTokenIssuer | Out-File -FilePath "TokenIssuers.txt"`</span></span>
 


## <a name="hightrustconfig-forsingleappps1"></a><span data-ttu-id="79283-187">HighTrustConfig-ForSingleApp.ps1</span><span class="sxs-lookup"><span data-stu-id="79283-187">HighTrustConfig-ForSingleApp.ps1</span></span>
<span data-ttu-id="79283-188"><a name="SingleAppScript"> </a></span><span class="sxs-lookup"><span data-stu-id="79283-188"></span></span>

<span data-ttu-id="79283-p119">Основная цель этого скрипта регистрация сертификата удаленного веб-приложения в Надстройка SharePoint с высоким уровнем доверия в SharePoint в качестве корневого ЦС и как доверенного поставщика маркеров доступа. Этот скрипт не используется, если клиент применяет один сертификат для нескольких Надстройки SharePoint. В этом случае см. раздел  [HighTrustConfig-ForSharedCertificate.ps1](#MultipleAppScript) выше. Этот скрипт выполняется для всех Надстройка SharePoint с высоким уровнем доверия.</span><span class="sxs-lookup"><span data-stu-id="79283-p119">The primary tasks of this script are to register the certificate of the remote web application in a high-trust SharePoint Add-in with SharePoint as both a root authority and as a trusted access token issuer. This script is not used if the customer is using a single certificate for multiple SharePoint Add-ins. For that scenario, see  [HighTrustConfig-ForSharedCertificate.ps1](#MultipleAppScript) above. This script is run for each high-trust SharePoint Add-in.</span></span>
 

 
<span data-ttu-id="79283-p120">В таблице ниже представлены параметры скрипта. В процессе настройки скрипта может потребоваться внесение изменений в эту таблицу.</span><span class="sxs-lookup"><span data-stu-id="79283-p120">The following table describes the parameters and switches for the script. Customization of the script may require changes to this table.</span></span>
 

 


|<span data-ttu-id="79283-194">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="79283-194">**Parameter**</span></span>|<span data-ttu-id="79283-195">**Значение**</span><span class="sxs-lookup"><span data-stu-id="79283-195">**Value**</span></span>|
|:-----|:-----|
|<span data-ttu-id="79283-196">-CertPath (обязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-196">-CertPath (required)</span></span>|<span data-ttu-id="79283-197">Полный путь к общему CER-файлу.</span><span class="sxs-lookup"><span data-stu-id="79283-197">The full path to the shared *.cer file.</span></span>|
|<span data-ttu-id="79283-198">-CertName (обязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-198">-CertName (required)</span></span>|<span data-ttu-id="79283-p121">Имя общего сертификата. Чтобы найти его, откройте диспетчер служб IIS на удаленном веб-сервере, на котором размещено удаленное веб-приложение. Выделите узел  _имя сервера_ и дважды щелкните элемент **Сертификаты**. После этого появится имя сертификата.  </span><span class="sxs-lookup"><span data-stu-id="79283-p121">The name of the shared certificate. To find the name, open IIS on the remote web server that hosts the remote web application. Highlight the  _server name_ node and double-click **Certificates**. The certificate will be listed by its name.</span></span>|
|<span data-ttu-id="79283-203">-SPAppClientID (обязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-203">-SPAppClientID (required)</span></span>|<span data-ttu-id="79283-p122">Идентификатор клиента (GUID), который использовался при регистрации Надстройка SharePoint в appregnew.aspx. Он применяется как идентификатор поставщика маркеров. Скрипт проверяет, что в идентификаторе используются только строчные буквы, что является обязательным для идентификаторов поставщиков.</span><span class="sxs-lookup"><span data-stu-id="79283-p122">The client ID (a GUID) that was used when the SharePoint Add-in was registered on appregnew.aspx. This is used as the issuer ID for the token issuer. The script ensures that it is lower-case, which is a requirement for issuer IDs.</span></span>|
|<span data-ttu-id="79283-207">-TokenIssuerFriendlyName (необязательный)</span><span class="sxs-lookup"><span data-stu-id="79283-207">-TokenIssuerFriendlyName (optional)</span></span>|<span data-ttu-id="79283-p123">Понятное имя поставщика маркеров длиной до 50 символов. Оно может быть полезно при отладке проблем с поставщиками маркеров. Имя должно быть уникальным. Вы можете использовать имя Надстройка SharePoint. Если этот параметр не используется, скрипт применяет в качестве имени значение  `-SPAppClientID`.</span><span class="sxs-lookup"><span data-stu-id="79283-p123">A unique friendly name for the token issuer, up to 50 characters. This can be helpful if you are debugging issues with token issuers. The name must be unique. Consider using the name of the SharePoint Add-in. If this parameter is not used, the script uses the value of  `-SPAppClientID` as the name.</span></span>|
<span data-ttu-id="79283-213">Далее показан пример вызова скрипта:</span><span class="sxs-lookup"><span data-stu-id="79283-213">The following is an example of calling the script:</span></span>
 

 
 `./HighTrustConfig-ForSingleApp.ps1 -CertPath "\\MyServer\Certs\MyCert.cer" -CertName "My Cert" -SPAppClientID "afe332f4-1f87-4c31-89b8-9c343ad7f24e" -TokenIssuerFriendlyName "Payroll add-in"`
 

 

 <span data-ttu-id="79283-p124">**Важно!** Регистрация сертификата в качестве поставщика маркера не вступает в силу немедленно. Может потребоваться до 24 часов, пока все серверы SharePoint не получат сведения о новом поставщике. Если выполнить команду iisreset на всех серверах SharePoint, поставщик будет зарегистрирован немедленно (используйте этот метод, если вы уверены, что работа пользователей SharePoint не будет нарушена).</span><span class="sxs-lookup"><span data-stu-id="79283-p124">**Important**  The registration of the certificate as a token issuer is not effective immediately. It may take as long as 24 hours before all the SharePoint servers recognize the new token issuer. Running an iisreset on all the SharePoint servers would cause them to immediately recognize the issuer, if you can do that without disturbing SharePoint users.</span></span>
 

<span data-ttu-id="79283-p125">Создайте файл в текстовом редакторе или редакторе PowerShell, скопируйте в него следующий код и сохраните файл как HighTrustConfig-ForSingleApp.ps1. Используйте формат ANSI, а не UTF-8.</span><span class="sxs-lookup"><span data-stu-id="79283-p125">Start a new file in a text editor, or the PowerShell editor, and copy the following into a text file and save it as HighTrustConfig-ForSingleApp.ps1. Use ANSI format, not UTF-8.</span></span>
 

 



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


 <span data-ttu-id="79283-219">**Совет.** Советы, указанные в конце предыдущего раздела, применимы и здесь, но в качестве значения параметра `-Identity` командлета `Remove-SPTrustedSecurityTokenIssuer` используйте идентификатор клиента, если параметр `-TokenIssuerFriendlyName` не применялся для сценария HighTrustConfig-ForSingleApp.ps1.</span><span class="sxs-lookup"><span data-stu-id="79283-219">**Tip**  The tips at the end of the preceding section apply here as well, but for the  `-Identity` parameter of the `Remove-SPTrustedSecurityTokenIssuer` cmdlet, use the client ID if the `-TokenIssuerFriendlyName` parameter was not used with HighTrustConfig-ForSingleApp.ps1.</span></span>
 


## <a name="modifications-needed-for-site-subscriptions"></a><span data-ttu-id="79283-220">Изменения, которые необходимо внести в подписки на сайт</span><span class="sxs-lookup"><span data-stu-id="79283-220">Modifications needed for site subscriptions</span></span>
<span data-ttu-id="79283-221"><a name="SiteSubscriptions"> </a></span><span class="sxs-lookup"><span data-stu-id="79283-221"></span></span>

<span data-ttu-id="79283-p126">Подписка сайта, которую иногда называют областью клиентов, это подмножество семейств веб-сайтов в ферме SharePoint. Подписки сайта обычно создаются в размещенных фермах SharePoint. Если клиент Надстройка SharePoint с высоким уровнем доверия хочет установить надстройку в ферме, которая настроена для подписок сайта, необходимо изменить используемый скрипт HighTrustConfig-*.ps1. У каждой подписки сайта есть собственный идентификатор области, но строка  `$realm = Get-SPAuthenticationRealm` в скриптах всегда возвращает область фермы. SharePoint считает маркеры доступа, выданные издателем маркеров, допустимыми только для области, указанной после символа @ в полном идентификаторе издателя. Чтобы получить правильную область для веб-сайта, на котором будет установлена надстройка, скрипт должен использовать параметр `-ServiceContext` в вызове командлета `Get-SPAuthenticationRealm`. Объект контекста службы, в свою очередь, создается на основе родительского семейства веб-сайтов целевого веб-сайта. Далее представлен пример, в котором  `$WebURL` это строковая переменная с полным URL-адресом веб-сайта SharePoint, например http://marketing.contoso.com/sites/northteam/july. Этот код позволяет запускать надстройку с высоким уровнем доверия не только на указанном веб-сайте, но и на любом сайте в рамках одной подписки сайта.</span><span class="sxs-lookup"><span data-stu-id="79283-p126">A site subscription, sometimes called a tenancy, is a subset of the site collections on a SharePoint farm. Site subscriptions are typically created on hosted SharePoint farms. If the customer of the high-trust SharePoint Add-in wants to install the add-in on a farm that has been configured for site subscriptions, then whichever of the two HighTrustConfig-*.ps1 scripts is being used needs to be modified. Each site subscription has its own realm ID, but the line  `$realm = Get-SPAuthenticationRealm` in the scripts always returns the realm of the farm. The access tokens issued by a token issuer are only regarded as valid by SharePoint for the realm that is specified after the "@" character in the full issuer ID. To get the correct realm for the website where the add-in is going to be installed, the script has to use the `-ServiceContext` parameter in the call to `Get-SPAuthenticationRealm`. The service context object, in turn, is created from the parent site collection of the of the target website. The following is an example, where  `$WebURL` is a string variable with the full URL of a SharePoint website, such as "http://marketing.contoso.com/sites/northteam/july." This code enables the high-trust add-in to be run, not just on the website specified, but on every website within the same site subscription.</span></span>
 

 

```
$Web = Get-SPWeb $WebURL
$sc = Get-SPServiceContext -Site $Web.Site
$realm = Get-SPAuthenticationRealm -ServiceContext $sc
```

<span data-ttu-id="79283-231">Чтобы завершить изменение сертификата, добавьте обязательный параметр  `$WebURL` в список параметров в начале файла следующим образом:</span><span class="sxs-lookup"><span data-stu-id="79283-231">To complete the modification of the script, add an additional required parameter  `$WebURL` to the param list at the top of the file, like this:</span></span>
 

 



```
param (
    # other parameters omitted 
    [Parameter()][String] $WebURL
)
```

<span data-ttu-id="79283-p127">Не забудьте добавить запятую после параметра перед новым параметром. Разверните пример Usage в верхней строке, чтобы учесть новый параметр. Пример:  `-WebURL <full URL where SP add-in will be installed>`.</span><span class="sxs-lookup"><span data-stu-id="79283-p127">Be sure to add a comma after the parameter that precedes the new one. And expand the "Usage" example on the top line to take into account the new parameter with something like this:  `-WebURL <full URL where SP add-in will be installed>`.</span></span>
 

 
<span data-ttu-id="79283-p128">Чтобы Надстройка SharePoint было доверенным для каждой подписки сайта, получите ссылку на ферму с помощью командлета  `Get-SPFarm`, а затем выполните перебор по свойству **SiteSubscriptions**. Передайте каждый объект **SPSiteSubscription** командлету `Get-SPServiceContext` как значение параметра `-SiteSubscription`. Далее представлен пример.</span><span class="sxs-lookup"><span data-stu-id="79283-p128">To make the SharePoint Add-in trusted on every site subscription, get a reference to the farm with the  `Get-SPFarm` cmdlet, and then iterate through its **SiteSubscriptions** property. Pass each **SPSiteSubscription** object to the `Get-SPServiceContext` cmdlet as the value of the `-SiteSubscription` parameter. The following is an example.</span></span>
 

 



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


