# <a name="granting-access-via-azure-ad-app-only"></a><span data-ttu-id="4df8f-101">Предоставление доступа с помощью Azure AD только для приложений</span><span class="sxs-lookup"><span data-stu-id="4df8f-101">Granting access via Azure AD App-Only</span></span>
<span data-ttu-id="4df8f-102">При использовании SharePoint Online можно определять приложения в Azure AD и эти приложения могут быть предоставлены разрешения для SharePoint, но и для всех других служб в Office 365.</span><span class="sxs-lookup"><span data-stu-id="4df8f-102">When using SharePoint Online you can define applications in Azure AD and these applications can be granted permissions to SharePoint, but also to all the other services in Office 365.</span></span> <span data-ttu-id="4df8f-103">Эта модель является предпочтительным в случае, если вы используете SharePoint Online, если вы используете SharePoint необходимо использовать модель SharePoint только через локальную основе Azure ACS описанные [здесь](security-apponly-azureacs.md "ссылка на статью только приложения Azure ACS").</span><span class="sxs-lookup"><span data-stu-id="4df8f-103">This model is the preferred model in case you’re using SharePoint Online, if you’re using SharePoint on-premises you have to use the SharePoint Only model via based Azure ACS as described in [here](security-apponly-azureacs.md "link to Azure ACS app only article").</span></span>

## <a name="setting-up-an-azure-ad-app-for-app-only-access"></a><span data-ttu-id="4df8f-104">Настройка приложения Azure AD для доступа только для приложений</span><span class="sxs-lookup"><span data-stu-id="4df8f-104">Setting up an Azure AD app for app-only access</span></span>
<span data-ttu-id="4df8f-105">В Azure AD при выполнении только приложения обычно используется сертификат для запроса доступа: отправляя сертификата и его закрытого ключа можно использовать приложение и разрешения для приложения.</span><span class="sxs-lookup"><span data-stu-id="4df8f-105">In Azure AD when doing app-only you typically use a certificate to request access: anyone having the certificate and its private key can use the app and the permissions granted to the app.</span></span> <span data-ttu-id="4df8f-106">Шаги, описанные ниже описывают настройки этой модели.</span><span class="sxs-lookup"><span data-stu-id="4df8f-106">Below steps walk you through the setup of this model.</span></span>

<span data-ttu-id="4df8f-107">Теперь все готово для настройки приложения Azure AD для вызова SharePoint Online с маркером только приложения.</span><span class="sxs-lookup"><span data-stu-id="4df8f-107">You are now ready to configure the Azure AD Application for invoking SharePoint Online with an App Only access token.</span></span> <span data-ttu-id="4df8f-108">Для этого необходимо создать и настроить самозаверяющий сертификат X.509, который будет использоваться для проверки подлинности приложения с Azure AD, во время разрешения на запрос маркера доступа приложения только.</span><span class="sxs-lookup"><span data-stu-id="4df8f-108">To do that, you have to create and configure a self-signed X.509 certificate, which will be used to authenticate your Application against Azure AD, while requesting the App Only access token.</span></span> <span data-ttu-id="4df8f-109">Сначала необходимо создать самозаверяющий сертификат X.509, который может быть создан с помощью средства makecert.exe, доступные в пакете SDK Windows или с помощью предоставленного сценарий PowerShell, которые не имеют зависимости makecert.</span><span class="sxs-lookup"><span data-stu-id="4df8f-109">First you must create the self-signed X.509 Certificate, which can be created using the makecert.exe tool that is available in the Windows SDK or through a provided PowerShell script which does not have a dependency to makecert.</span></span> <span data-ttu-id="4df8f-110">С помощью скрипта PowerShell является предпочтительным и описываются в данной главе.</span><span class="sxs-lookup"><span data-stu-id="4df8f-110">Using the PowerShell script is the preferred method and is explained in this chapter.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4df8f-111">Важно выполнить ниже сценарии с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4df8f-111">It's important that you run the below scripts with Administrator privileges.</span></span>

<span data-ttu-id="4df8f-112">Чтобы создать самостоятельно подпись сертификата с помощью этого сценария:</span><span class="sxs-lookup"><span data-stu-id="4df8f-112">To create a self signed certificate with this script:</span></span>

```powershell
.\Create-SelfSignedCertificate.ps1 -CommonName "MyCompanyName" -StartDate 2017-10-01 -EndDate 2019-10-01
```

> [!NOTE]
> <span data-ttu-id="4df8f-113">Даты приведены в формат даты США: гггг-мм дд</span><span class="sxs-lookup"><span data-stu-id="4df8f-113">The dates are provided in US date format: YYYY-MM-dd</span></span>

<span data-ttu-id="4df8f-114">Здесь можно скопировать сценарий:</span><span class="sxs-lookup"><span data-stu-id="4df8f-114">The actual script can be copied from here:</span></span>

```powershell
#Requires -RunAsAdministrator
<#
.SYNOPSIS
Creates a Self Signed Certificate for use in server to server authentication
.DESCRIPTION
.EXAMPLE
PS C:\> .\Create-SelfSignedCertificate.ps1 -CommonName "MyCert" -StartDate 2015-11-21 -EndDate 2017-11-21
This will create a new self signed certificate with the common name "CN=MyCert". During creation you will be asked to provide a password to protect the private key.
.EXAMPLE
PS C:\> .\Create-SelfSignedCertificate.ps1 -CommonName "MyCert" -StartDate 2015-11-21 -EndDate 2017-11-21 -Password (ConvertTo-SecureString -String "MyPassword" -AsPlainText -Force)
This will create a new self signed certificate with the common name "CN=MyCert". The password as specified in the Password parameter will be used to protect the private key
.EXAMPLE
PS C:\> .\Create-SelfSignedCertificate.ps1 -CommonName "MyCert" -StartDate 2015-11-21 -EndDate 2017-11-21 -Force
This will create a new self signed certificate with the common name "CN=MyCert". During creation you will be asked to provide a password to protect the private key. If there is already a certificate with the common name you specified, it will be removed first.
#>
Param(

   [Parameter(Mandatory=$true)]
   [string]$CommonName,

   [Parameter(Mandatory=$true)]
   [DateTime]$StartDate,
   
   [Parameter(Mandatory=$true)]
   [DateTime]$EndDate,

   [Parameter(Mandatory=$false, HelpMessage="Will overwrite existing certificates")]
   [Switch]$Force,

   [Parameter(Mandatory=$false)]
   [SecureString]$Password
)

# DO NOT MODIFY BELOW

function CreateSelfSignedCertificate(){
    
    #Remove and existing certificates with the same common name from personal and root stores
    #Need to be very wary of this as could break something
    if($CommonName.ToLower().StartsWith("cn="))
    {
        # Remove CN from common name
        $CommonName = $CommonName.Substring(3)
    }
    $certs = Get-ChildItem -Path Cert:\LocalMachine\my | Where-Object{$_.Subject -eq "CN=$CommonName"}
    if($certs -ne $null -and $certs.Length -gt 0)
    {
        if($Force)
        {
        
            foreach($c in $certs)
            {
                remove-item $c.PSPath
            }
        } else {
            Write-Host -ForegroundColor Red "One or more certificates with the same common name (CN=$CommonName) are already located in the local certificate store. Use -Force to remove them";
            return $false
        }
    }

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=$CommonName", 0)

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
    $key.KeySpec = 1
    $key.Length = 2048 
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"
    $key.MachineContext = 1
    $key.ExportPolicy = 1 # This is required to allow the private key to be exported
    $key.Create()

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1") # Server Authentication
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"
    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = $StartDate
    $cert.NotAfter = $EndDate
    $cert.X509Extensions.Add($ekuext)
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")
    return $true
}

function ExportPFXFile()
{
    if($CommonName.ToLower().StartsWith("cn="))
    {
        # Remove CN from common name
        $CommonName = $CommonName.Substring(3)
    }
    if($Password -eq $null)
    {
        $Password = Read-Host -Prompt "Enter Password to protect private key" -AsSecureString
    }
    $cert = Get-ChildItem -Path Cert:\LocalMachine\my | where-object{$_.Subject -eq "CN=$CommonName"}
    
    Export-PfxCertificate -Cert $cert -Password $Password -FilePath "$($CommonName).pfx"
    Export-Certificate -Cert $cert -Type CERT -FilePath "$CommonName.cer"
}

function RemoveCertsFromStore()
{
    # Once the certificates have been been exported we can safely remove them from the store
    if($CommonName.ToLower().StartsWith("cn="))
    {
        # Remove CN from common name
        $CommonName = $CommonName.Substring(3)
    }
    $certs = Get-ChildItem -Path Cert:\LocalMachine\my | Where-Object{$_.Subject -eq "CN=$CommonName"}
    foreach($c in $certs)
    {
        remove-item $c.PSPath
    }
}

if(CreateSelfSignedCertificate)
{
    ExportPFXFile
    RemoveCertsFromStore
}
```

<span data-ttu-id="4df8f-115">Будет предложено предоставить пароль для шифрования закрытого ключа и другое. PFX-файл и. CER-файл экспортируется в текущую папку.</span><span class="sxs-lookup"><span data-stu-id="4df8f-115">You will be asked to give a password to encrypt your private key, and both the .PFX file and .CER file will be exported to the current folder.</span></span> 

<span data-ttu-id="4df8f-116">Следующим шагом Регистрация приложения Azure AD в Azure Active Directory для клиентов, связанного с клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="4df8f-116">Next step is registering an Azure AD application in the Azure Active Directory tenant that is linked to your Office 365 tenant.</span></span> <span data-ttu-id="4df8f-117">Для этого откройте центра администрирования Office 365 (https://portal.office.com) с помощью учетной записи пользователя члена группы «Администраторы» глобального клиента.</span><span class="sxs-lookup"><span data-stu-id="4df8f-117">To do that, open the Office 365 Admin Center (https://portal.office.com) using the account of a user member of the Tenant Global Admins group.</span></span> <span data-ttu-id="4df8f-118">Щелкните ссылку «Azure AD», который доступен в группе «Центра администрирования» в левой части treeview центра администрирования Office 365.</span><span class="sxs-lookup"><span data-stu-id="4df8f-118">Click on the "Azure AD" link that is available under the "Admin centers" group in the left-side treeview of the Office 365 Admin Center.</span></span> <span data-ttu-id="4df8f-119">На вкладке новый браузер, который будет открыт вы найдете портала управления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4df8f-119">In the new browser's tab that will be opened you will find the Microsoft Azure Management Portal.</span></span> <span data-ttu-id="4df8f-120">Если он установлен в первый раз, доступ к портала управления Azure с помощью учетной записи, необходимо зарегистрировать новую подписку Azure, предоставляя сведения и данные о банковской карте для применения оплаты.</span><span class="sxs-lookup"><span data-stu-id="4df8f-120">If it is the first time that you access the Azure Management Portal with your account, you will have to register a new Azure subscription, providing some information and a credit card for any payment need.</span></span> <span data-ttu-id="4df8f-121">Но не выполнения для воспроизведения с Azure AD и для регистрации приложения Office 365 будет не что-либо оплаты.</span><span class="sxs-lookup"><span data-stu-id="4df8f-121">But don't worry, in order to play with Azure AD and to register an Office 365 Application you will not pay anything.</span></span> <span data-ttu-id="4df8f-122">На самом деле это бесплатное возможности.</span><span class="sxs-lookup"><span data-stu-id="4df8f-122">In fact, those are free capabilities.</span></span> <span data-ttu-id="4df8f-123">Один раз возможность доступа к портала управления Azure, выберите в разделе «Active Directory» и выберите параметр «Регистрации приложения».</span><span class="sxs-lookup"><span data-stu-id="4df8f-123">Once having access to the Azure Management Portal, select the "Active Directory" section and choose the option "App Registrations".</span></span> <span data-ttu-id="4df8f-124">В разделе ниже для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="4df8f-124">See the next figure for further details.</span></span>

![Показывает портала azure ad](media/apponly/azureadapponly1.png)

<span data-ttu-id="4df8f-126">На вкладке «Регистрации приложения» вы найдете список Azure AD приложения, зарегистрированные в вашего клиента.</span><span class="sxs-lookup"><span data-stu-id="4df8f-126">In the "App Registrations" tab you will find the list of Azure AD applications registered in your tenant.</span></span> <span data-ttu-id="4df8f-127">Нажмите кнопку «Новый регистрации приложения» в левой верхней части blade.</span><span class="sxs-lookup"><span data-stu-id="4df8f-127">Click the "New application registration" button in the upper left part of the blade.</span></span> <span data-ttu-id="4df8f-128">После этого укажите имя для вашего приложения, выберите параметр «веб-приложение / API» и заполните поля в «Входа URL-адрес» URL-адрес (не существует, например https://www.pnp.com).</span><span class="sxs-lookup"><span data-stu-id="4df8f-128">Next, provide a name for your application, select the option "Web app / API", and fill in the "Sign-on URL" with a URL (does not have to exist, e.g. https://www.pnp.com).</span></span> <span data-ttu-id="4df8f-129">Щелкните «Создать», чтобы создать приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4df8f-129">Click on “Create” to create the Azure AD application.</span></span>

![Создает новое приложение azure ad](media/apponly/azureadapponly2.png)

<span data-ttu-id="4df8f-131">Один раз созданные необходимо выполнять поиск еще раз приложения Azure AD и откройте его:</span><span class="sxs-lookup"><span data-stu-id="4df8f-131">Once created you need to look up your Azure AD application again and open it:</span></span>

![Откроется новое приложение azure ad из портала](media/apponly/azureadapponly3.png)

> [!IMPORTANT]
> <span data-ttu-id="4df8f-133">После открытия приложения скопируйте код приложения, как он потребуется позже.</span><span class="sxs-lookup"><span data-stu-id="4df8f-133">Once the application has been opened copy the application ID as you’ll need it later.</span></span>

<span data-ttu-id="4df8f-134">Теперь щелкните «Необходимые разрешения» и нажмите кнопку «Добавить» будет отображаться новые blade.</span><span class="sxs-lookup"><span data-stu-id="4df8f-134">Now click on "Required Permissions", and click on the "Add" button, a new blade will appear.</span></span> <span data-ttu-id="4df8f-135">Необходимо настроить следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="4df8f-135">You need to configure the following permissions:</span></span>
 - <span data-ttu-id="4df8f-136">Office 365 SharePoint Online (разрешений приложения)</span><span class="sxs-lookup"><span data-stu-id="4df8f-136">Office 365 SharePoint Online (Application Permission)</span></span>
     - <span data-ttu-id="4df8f-137">Чтение и запись управляемых метаданных</span><span class="sxs-lookup"><span data-stu-id="4df8f-137">Read and write managed metadata</span></span>
     - <span data-ttu-id="4df8f-138">Полный доступ все семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="4df8f-138">Have full control of all site collection</span></span>

<span data-ttu-id="4df8f-139">Приложение» разрешения «— это списки предоставленных приложению при запуске приложения только.</span><span class="sxs-lookup"><span data-stu-id="4df8f-139">The "Application Permissions" are those granted to the application when running as App Only.</span></span>

![Предоставление разрешений приложению azure ad](media/apponly/azureadapponly4.png)

<span data-ttu-id="4df8f-141">Последний этап «подключение» сертификат, созданный ранее в приложение.</span><span class="sxs-lookup"><span data-stu-id="4df8f-141">Final step is “connecting” the certificate we created earlier to the application.</span></span> <span data-ttu-id="4df8f-142">Необходимо выполнить сценарий Get-SelfSignedCertificateInformation.ps1.</span><span class="sxs-lookup"><span data-stu-id="4df8f-142">You need to execute the Get-SelfSignedCertificateInformation.ps1 script.</span></span> 

```powershell
.\Get-SelfSignedCertificateInformation.ps1 | clip
```

<span data-ttu-id="4df8f-143">Здесь можно скопировать сценарий:</span><span class="sxs-lookup"><span data-stu-id="4df8f-143">The actual script can be copied from here:</span></span>

```powershell
$certPath = Read-Host "Enter certificate path (.cer)"
$cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$cert.Import($certPath)
$rawCert = $cert.GetRawCertData()
$base64Cert = [System.Convert]::ToBase64String($rawCert)
$rawCertHash = $cert.GetCertHash()
$base64CertHash = [System.Convert]::ToBase64String($rawCertHash)
$KeyId = [System.Guid]::NewGuid().ToString()

$keyCredentials = 
'"keyCredentials": [
    {
      "customKeyIdentifier": "'+ $base64CertHash + '",
      "keyId": "' + $KeyId + '",
      "type": "AsymmetricX509Cert",
      "usage": "Verify",
      "value":  "' + $base64Cert + '"
     }
  ],'
$keyCredentials

Write-Host "Certificate Thumbprint:" $cert.Thumbprint
```

<span data-ttu-id="4df8f-144">Будет необходимо указать полный путь. Файл CER, созданный при создании сертификата для конфигурации AppOnly контекста.</span><span class="sxs-lookup"><span data-stu-id="4df8f-144">You will have to provide the full qualified path of the .CER file that you created when you created the certificate for the AppOnly context configuration.</span></span> <span data-ttu-id="4df8f-145">Команда будет копировать в буфер обмена фрагмент JSON, который будет использоваться в Предстоящие действия.</span><span class="sxs-lookup"><span data-stu-id="4df8f-145">The command will copy into the clipboard a JSON snippet that you will use in the upcoming steps.</span></span> <span data-ttu-id="4df8f-146">Вставка содержимого буфера обмена в надежном месте (например, новым новый файл "Блокнот").</span><span class="sxs-lookup"><span data-stu-id="4df8f-146">Paste the content of the clipboard in a safe place (like a fresh new notepad file).</span></span>

<span data-ttu-id="4df8f-147">Вернитесь в Azure AD приложение, созданное на предыдущем шаге и нажмите кнопку «Манифест» в верхней части blade, а затем нажмите кнопку Изменить ".</span><span class="sxs-lookup"><span data-stu-id="4df8f-147">Go back to the Azure AD Application that you created in the previous step and click the "Manifest" button at the top of the blade, then click Edit'.</span></span> <span data-ttu-id="4df8f-148">Поиск свойства **keyCredentials** и замените фрагмент, созданный перед, это может быть следующим:</span><span class="sxs-lookup"><span data-stu-id="4df8f-148">Search for the **keyCredentials** property and replace it with the snippet you generated before, this will be like:</span></span>

```JSON
  "keyCredentials": [
    {
      "customKeyIdentifier": "<$base64CertHash>",
      "keyId": "<$KeyId>",
      "type": "AsymmetricX509Cert",
      "usage": "Verify",
      "value":  "<$base64Cert>"
     }
  ],
```

<span data-ttu-id="4df8f-149">После завершения этого шага нажмите кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="4df8f-149">Click Save when you complete this step.</span></span>

<span data-ttu-id="4df8f-150">В этом примере разрешения приложения Sites.FullControl.All требуются разрешения администратора в клиент перед его можно использовать.</span><span class="sxs-lookup"><span data-stu-id="4df8f-150">In this sample the Sites.FullControl.All application permission require admin consent in a tenant before it can be used.</span></span> <span data-ttu-id="4df8f-151">Создайте URL-адрес согласия следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4df8f-151">Create a consent URL like the following:</span></span>

```
https://login.microsoftonline.com/<tenant>/adminconsent?client_id=<application id>&state=<something>
```

<span data-ttu-id="4df8f-152">С помощью идентификатора приложения из Мое приложение Azure AD и соглашаетесь приложения из моих contoso.onmicrosoft.com клиента, URL-адрес выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4df8f-152">Using the application id from my Azure AD app and consenting to the app from my tenant contoso.onmicrosoft.com, the URL looks like this:</span></span>

```
https://login.microsoftonline.com/contoso.onmicrosoft.com/adminconsent?client_id=6e4433ca-7011-4a11-85b6-1195b0114fea&state=12345
```

<span data-ttu-id="4df8f-153">Просмотра для созданного URL-адреса и вход как администратор клиента и разрешения для приложения.</span><span class="sxs-lookup"><span data-stu-id="4df8f-153">Browsing to the created URL and log in as a tenant admin, and consent to the application.</span></span> <span data-ttu-id="4df8f-154">Вы видите на экране подтверждения показывать имя приложения, а также области разрешений, которые вы настроили.</span><span class="sxs-lookup"><span data-stu-id="4df8f-154">You can see the consent screen show the name of your application as well as the permission scopes you configured.</span></span>

![Предоставление разрешений приложению azure ad](media/apponly/azureadapponly5.png)

> [!NOTE]
> <span data-ttu-id="4df8f-156">После нажатия кнопки «Accept» будет перенаправлен на вход URL-адрес указан более ранних (https://www.pnp.com в нашем случае).. .if, недопустимый URL-адрес перенаправления завершится с ошибкой, но предоставление было выполнено успешно, поэтому nothing заниматься.</span><span class="sxs-lookup"><span data-stu-id="4df8f-156">After clicking “Accept” you’re redirected to the sign-in URL you specified earlier (https://www.pnp.com in our case) …if that URL is not valid the redirect will fail but the grant was done successful, so nothing to worry about.</span></span>


## <a name="using-this-principal-in-your-application-using-the-sharepoint-pnp-sites-core-library"></a><span data-ttu-id="4df8f-157">Использование участника в приложении с помощью библиотеки PnP основных сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="4df8f-157">Using this principal in your application using the SharePoint PnP Sites Core library</span></span>
<span data-ttu-id="4df8f-158">На первом шаге, добавьте пакет nuget библиотеки SharePointPnPCoreOnline: https://www.nuget.org/packages/SharePointPnPCoreOnline.</span><span class="sxs-lookup"><span data-stu-id="4df8f-158">In a first step, you add the SharePointPnPCoreOnline library nuget package: https://www.nuget.org/packages/SharePointPnPCoreOnline.</span></span> <span data-ttu-id="4df8f-159">После этого можно использовать ниже конструкцию кода:</span><span class="sxs-lookup"><span data-stu-id="4df8f-159">Once that’s done you can use below code construct:</span></span>

```C#
using OfficeDevPnP.Core;
using System;

namespace AzureADCertAuth
{
    class Program
    {
        static void Main(string[] args)
        {
            string siteUrl = "https://contoso.sharepoint.com/sites/demo";
            using (var cc = new AuthenticationManager().GetAzureADAppOnlyAuthenticatedContext(siteUrl, "<application id>", "contoso.onmicrosoft.com", @"C:\BertOnlineAzureADAppOnly.pfx", "<password>"))
            {
                cc.Load(cc.Web, p => p.Title);
                cc.ExecuteQuery();
                Console.WriteLine(cc.Web.Title);
            };
        }
    }
}
```

## <a name="faq"></a><span data-ttu-id="4df8f-160">Вопросы и ответы</span><span class="sxs-lookup"><span data-stu-id="4df8f-160">FAQ</span></span>
### <a name="can-i-use-other-means-besides-certificates-for-realizing-app-only-access-for-my-azure-ad-app"></a><span data-ttu-id="4df8f-161">Можно использовать другие означает, что помимо сертификаты для реализации доступ только для приложений для приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="4df8f-161">Can I use other means besides certificates for realizing app-only access for my Azure AD app?</span></span>
<span data-ttu-id="4df8f-162">Нет, все другие параметры блокируемые по SharePoint Online и приведет к сообщение об отказе в доступе.</span><span class="sxs-lookup"><span data-stu-id="4df8f-162">No, all other options are blocked by SharePoint Online and will result in an Access Denied message.</span></span>

