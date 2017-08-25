
# <a name="replace-an-expiring-client-secret-in-a-sharepoint-add-in"></a><span data-ttu-id="a6f20-101">Замена секрета клиента с истекающим сроком действия в надстройке SharePoint</span><span class="sxs-lookup"><span data-stu-id="a6f20-101">Replace an expiring client secret in a SharePoint Add-in</span></span>
<span data-ttu-id="a6f20-102">Узнайте, как добавить новый секрет клиента для надстройки SharePoint, зарегистрированной на странице AppRegNew.aspx.</span><span class="sxs-lookup"><span data-stu-id="a6f20-102">Learn how to add a new client secret for a spappsing that is registered with AppRegNew.aspx.</span></span>
 

 <span data-ttu-id="a6f20-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="a6f20-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 

<span data-ttu-id="a6f20-p102">Срок действия секретов клиента для надстроек SharePoint, зарегистрированных на странице AppRegNew.aspx, завершается через год. В этой статье описано, как добавить новый секрет клиента для надстройки, а также как создать секрет клиента, действительный в течение трех лет.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p102">Client secrets for spappplural that are registered using the AppRegNew.aspx page expire after one year. This article explains how to add a new secret for the add-in, as well as how to create a new client secret that is valid for three years.</span></span>
 

 <span data-ttu-id="a6f20-p103">**Примечание.** Эта статья посвящена надстройкам SharePoint, распространяемым через каталог организации и зарегистрированным на странице AppRegNew.aspx. Если для регистрации приложения использовалась Панель мониторинга продаж, см. раздел [Создание или обновление идентификаторов и секретов клиентов на Панели мониторинга продаж](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).</span><span class="sxs-lookup"><span data-stu-id="a6f20-p103">**Note** This article is about SharePoint Add-ins that are distributed through an organization catalog and registered with the AppRegNew.aspx page. If the add-in is registered on the Seller Dashboard, see  [Create or update client IDs and secrets in the Seller Dashboard](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).</span></span>
 


## <a name="prerequisites-for-refreshing-a-client-secret"></a><span data-ttu-id="a6f20-110">Необходимые условия для обновления секрета клиента</span><span class="sxs-lookup"><span data-stu-id="a6f20-110">Prerequisites for refreshing a client secret</span></span>

<span data-ttu-id="a6f20-111">Убедитесь в следующем перед началом работы:</span><span class="sxs-lookup"><span data-stu-id="a6f20-111">Ensure the following before you begin:</span></span>
 

 

-  <span data-ttu-id="a6f20-112">[Помощник по входу в Microsoft Online Services](http://www.microsoft.com/download/details.aspx?id=39267) установлен на компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="a6f20-112">[Microsoft Online Services Sign-In Assistant](http://www.microsoft.com/download/details.aspx?id=39267) is installed on the development computer.</span></span>
    
 
- <span data-ttu-id="a6f20-113">Модуль PowerShell для Microsoft Online Services ( [32-разрядный](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-разрядный](http://go.microsoft.com/fwlink/p/?linkid=236297)) установлен на компьютере для разработки.</span><span class="sxs-lookup"><span data-stu-id="a6f20-113">Microsoft Online Services PowerShell Module ( [32-bit](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-bit](http://go.microsoft.com/fwlink/p/?linkid=236297)) is installed on the development computer.</span></span>
    
 
- <span data-ttu-id="a6f20-114">Вы администратор фермы или клиента Office 365, для которого зарегистрирована надстройка на странице AppRegNew.aspx.</span><span class="sxs-lookup"><span data-stu-id="a6f20-114">You are a tenant administrator for the Office 365 tenant (or a farm administrator on the farm) where the add-in was registered with the AppRegNew.aspx page.</span></span>
    
 

## <a name="find-out-the-expiration-dates-of-the-sharepoint-add-ins-installed-to-the-office-365-tenancy"></a><span data-ttu-id="a6f20-115">Просмотр дат истечения срока Надстройки SharePoint, установленных на клиенте Office 365</span><span class="sxs-lookup"><span data-stu-id="a6f20-115">Find out the expiration dates of the SharePoint Add-ins installed to the Office 365 tenancy</span></span>


 

 

1. <span data-ttu-id="a6f20-116">Откройте Windows PowerShell и запустите следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="a6f20-116">Open Windows PowerShell and run the following cmdlet:</span></span>
    
```
  Connect-MsolService

```

2. <span data-ttu-id="a6f20-117">При появлении запроса введите учетные данные администратора клиента или администратора фермы для области клиента Office 365 или фермы, где надстройка зарегистрирована с использованием AppRegNew.aspx.</span><span class="sxs-lookup"><span data-stu-id="a6f20-117">At the login prompt, enter tenant-administrator (or farm administrator) credentials for the Office 365 tenancy or farm where the add-in was registered with AppRegNew.aspx.</span></span>
    
 
3. <span data-ttu-id="a6f20-p104">Создайте отчет со списком всех надстроек и датами истечения срока действия их секретов с помощью указанных ниже строк. Обратите внимание на особенности этого кода:</span><span class="sxs-lookup"><span data-stu-id="a6f20-p104">Generate a report that lists each add-in and the date that its secret expires with the following lines. Note the following about this code:</span></span>
    
      - <span data-ttu-id="a6f20-120">Сначала он применяет фильтр к приложениям Майкрософт, надстройкам в процессе разработки, а также нерекомендуемым надстройкам — автоматически размещенным.</span><span class="sxs-lookup"><span data-stu-id="a6f20-120">It first filters out Microsoft's own applications, add-ins still under development (and a now-deprecated type of add-in that was called autohosted).</span></span>
    
 
  - <span data-ttu-id="a6f20-121">Из оставшихся результатов он исключает надстройки не для SharePoint и надстройки с использованием асимметричных ключей, например рабочие процессы.</span><span class="sxs-lookup"><span data-stu-id="a6f20-121">From the remainder, it filters out non-SharePoint add-ins and add-ins that use asymmetric keys, like workflows.</span></span>
    
 

```
  $applist = Get-MsolServicePrincipal -all  |Where-Object -FilterScript { ($_.DisplayName -notlike "*Microsoft*") -and ($_.DisplayName -notlike "autohost*") -and  ($_.ServicePrincipalNames -notlike "*localhost*") }

foreach ($appentry in $applist)
{
    $principalId = $appentry.AppPrincipalId
    $principalName = $appentry.DisplayName
    
    Get-MsolServicePrincipalCredential -AppPrincipalId $principalId -ReturnKeyValues $false | Where-Object { ($_.Type -ne "Other") -and ($_.Type -ne "Asymmetric") }
    
     $date = get-date
     Write-Host "$principalName;$principalId;$appentry.KeyId;$appentry.type;$date;$appentry.Usage"

}  > c:\temp\appsec.txt
```

4. <span data-ttu-id="a6f20-p105">Откройте файл C:\temp\appsec.txt, чтобы просмотреть отчет. Не закрывайте окно Windows PowerShell для выполнения следующей процедуры, если скоро истекает срок действия какого-либо секрета.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p105">Open the file C:tempappsec.txt to see the report. Leave the Windows PowerShell window open for the next procedure, if any of the secrets is near to expiration.</span></span>
    
 

## <a name="generate-a-new-secret"></a><span data-ttu-id="a6f20-124">Создание секрета клиента</span><span class="sxs-lookup"><span data-stu-id="a6f20-124">Generate a new secret</span></span>


 

 

1. <span data-ttu-id="a6f20-125">Создайте переменную ИД клиента со следующем строкой, используя ИД клиента, которое имеет Надстройка SharePoint, в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="a6f20-125">Create a client ID variable with the following line, using the client ID of the SharePoint Add-in as the parameter.</span></span>
    
```
  $clientId = 'client id of the add-in'

```

2. <span data-ttu-id="a6f20-126">Создайте новый секрет клиента со следующими строками:</span><span class="sxs-lookup"><span data-stu-id="a6f20-126">Generate a new client secret with the following lines:</span></span>
    
```
  $bytes = New-Object Byte[] 32
$rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
$rand.GetBytes($bytes)
$rand.Dispose()
$newClientSecret = [System.Convert]::ToBase64String($bytes)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Sign -Value $newClientSecret
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Verify -Value $newClientSecret
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Password -Usage Verify -Value $newClientSecret
$newClientSecret
```

3. <span data-ttu-id="a6f20-p106">Новый секрет клиента появится в консоли Windows PowerShell. Скопируйте его в текстовый файл, он будет нужен для следующей процедуры.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p106">The new client secret will appear on the Windows PowerShell console. Copy it to a text file. You use it in the next procedure.</span></span>
    
 

 <span data-ttu-id="a6f20-p107">**Совет.** По умолчанию срок действия надстройки составляет один год. Вы можете сократить или увеличить его (до 3 лет) с помощью параметра **-EndDate** в трех вызовах командлета **New-MsolServicePrincipalCredential**. Значением этого параметра должен быть объект [DateTime](http://msdn2.microsoft.com/EN-US/library/03ybds8y), превышающий значение **DateTime.Now** не более чем на 3 года.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p107">**TIP** By default, the add-in secret lasts one year. You can set this to a shorter or longer (up to 3 years maximum) by using the **-EndDate** parameter on the three calls of the **New-MsolServicePrincipalCredential** cmdlet. The value of the parameter must be a [DateTime](http://msdn2.microsoft.com/EN-US/library/03ybds8y) object set to no longer than 3 years from **DateTime.Now**.</span></span>
 


## <a name="update-the-remote-web-application-in-visual-studio-to-use-the-new-secret"></a><span data-ttu-id="a6f20-133">Обновление удаленного веб-приложения в Visual Studio для использования нового секрета</span><span class="sxs-lookup"><span data-stu-id="a6f20-133">Update the remote web application in Visual Studio to use the new secret</span></span>


 <span data-ttu-id="a6f20-p108">**Важно!** Если ваша надстройка изначально создана с помощью предварительного выпуска Инструментов разработчика Microsoft Office для Visual Studio, она может содержать устаревшую версию файла TokenHelper (с расширением CS или VB). Если файл не содержит строку secondaryClientSecret, то это устаревшая версия, которую следует заменить, прежде чем обновлять веб-приложение для использования нового секрета. Чтобы получить копию файла финальной версии, необходима среда Visual Studio 2012 или более поздней версии. Создайте проект надстройки SharePoint в Visual Studio. Скопируйте файл TokenHelper из него в проект веб-приложения своей надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p108">**Important** If your add-in was originally created with a prerelease version the Microsoft Office Developer Tools for Visual Studio, it may contain an out-of-date version of the TokenHelper.cs (or .vb) file. If the file does not contain the string "secondaryClientSecret", it is out-of-date and it must be replaced before you can update the web application with a new secret. To obtain a copy of a release version of the file, you need Visual Studio 2012 or later. Create a new SharePoint Add-in project in Visual Studio. Copy the TokenHelper file from it to the web application project of your SharePoint Add-in.</span></span> 
 


1. <span data-ttu-id="a6f20-p109">Откройте проект надстройки SharePoint в Visual Studio, а затем откройте файл web.config из проекта веб-приложения. В разделе **appSettings** указаны ключи для идентификатора и секрета клиента. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p109">Open the SharePoint Add-in project in Visual Studio, and open the web.config file for the web application project. In the **appSettings** section, there are keys for the client ID and client secret. The following is an example:</span></span>
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>

```

2. <span data-ttu-id="a6f20-142">Измените имя ключа **ClientSecret** на SecondaryClientSecret, как показано в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="a6f20-142">Change the name of the **ClientSecret** key to "SecondaryClientSecret" as shown in the following example:</span></span>
    
```XML
  <add key="SecondaryClientSecret" value="your old secret here" />
```

> <span data-ttu-id="a6f20-p110">**Примечание.** Если вы впервые выполняете эту процедуру, то в этой части файла конфигурации не будет записи свойства **SecondaryClientSecret**. Но если процедура выполняется для последующего (второго или третьего) секрета клиента, то свойство **SecondaryClientSecret** уже присутствует и содержит исходный или уже просроченный секрет. В этом случае необходимо удалить свойство **SecondaryClientSecret**, прежде чем переименовывать ключ **ClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p110">**Note** If you are performing this procedure for the first time there will be no **SecondaryClientSecret** property entry at this point in the configuration file. However if you are performing the procedure for a subsequent client secret expiration (second or third) the property **SecondaryClientSecret** is already present and containing the initial or already longer time ago expired old secret. In this case delete the **SecondaryClientSecret** property first before renaming **ClientSecret**.</span></span>

3. <span data-ttu-id="a6f20-p111">Добавьте новый ключ **ClientSecret** и включите в него новый секрет клиента. Результат должен выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="a6f20-p111">Add a new **ClientSecret** key and give it your new client secret. Your markup should now look like the following:</span></span>
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your new secret here" />
  <add key="SecondaryClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>
```

4. <span data-ttu-id="a6f20-148">Если вы использовали новый файл TokenHelper, выполните повторную сборку проекта.</span><span class="sxs-lookup"><span data-stu-id="a6f20-148">If you changed to a new TokenHelper file, rebuild the project.</span></span>
    
 
5. <span data-ttu-id="a6f20-149">Опубликуйте веб-приложение повторно.</span><span class="sxs-lookup"><span data-stu-id="a6f20-149">Republish the web application.</span></span>
    
 

## <a name="create-a-client-secret-that-is-valid-for-three-years"></a><span data-ttu-id="a6f20-150">Создание секрета клиента, действительного на протяжении трех лет</span><span class="sxs-lookup"><span data-stu-id="a6f20-150">Create a client secret that is valid for three years</span></span>

<span data-ttu-id="a6f20-p112">Если срок действия секретов клиента истек, сначала удалите все просроченные секреты с заданным значением **clientId**. После этого создайте новые с помощью PowerShell для Microsoft Office, подождите хотя бы 24 часа, а затем протестируйте приложение с использованием нового значения **clientId** и ключа **ClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p112">For expired client secrets, first you must delete all of the expired secrets for a given **clientId**. Then you create a new one with MSO PowerShell, wait at least 24 hours, and test the app with the new **clientId** and **ClientSecret** key.</span></span>
 

 

1. <span data-ttu-id="a6f20-153">Подключитесь к Microsoft Office Online от имени администратора клиента с помощью приведенной ниже разметки, используя Windows PowerShell для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a6f20-153">Connect to MSOnline using the tenant admin user with the below markup using SharePoint Windows PowerShell.</span></span>
    
```
  import-module MSOnline
$msolcred = get-credential
connect-msolservice -credential $msolcred

```

2. <span data-ttu-id="a6f20-p113">Получите **ServicePrincipals** и ключи. При использовании параметра **$keys** возвращаются три записи. Замените каждое значение **KeyId** в *KeyId1*, *KeyId2* и *KeyId3*. Вы также увидите значение **EndDate** для каждого ключа. Убедитесь, что там отображается просроченный ключ.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p113">Get **ServicePrincipals** and keys. Printing **$keys** returns three records. Replace each **KeyId** in *KeyId1*  , *KeyId2*  and *KeyId3*  . You will also see the **EndDate** of each key. Confirm whether your expired key appers there.</span></span>
    
     <span data-ttu-id="a6f20-p114">**Примечание.** Значение **clientId** должно совпадать с просроченным **clientId**. Рекомендуется удалить все ключи (как просроченные, так и действительные) для этого идентификатора **clientId**.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p114">**Note:** The **clientId** needs to match your expired **clientId**. It's recommended to delete all keys, both expired and unexpired, for this **clientId**.</span></span>
    


```
  $clientId = "27c5b286-62a6-45c7-beda-abbaea6eecf2"
$keys = Get-MsolServicePrincipalCredential -AppPrincipalId $clientId
Remove-MsolServicePrincipalCredential -KeyIds @("KeyId1"," KeyId2"," KeyId3") -AppPrincipalId $clientId 

```

3. <span data-ttu-id="a6f20-p115">Создайте новое значение **ClientSecret** для этого идентификатора **clientID**. Для него используется то же значение **clientId**, что и на предыдущем этапе. Новое значение **ClientSecret** действительно в течение 3 лет.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p115">Generate a new **ClientSecret** for this **clientID**. It uses the same **clientId** as set in the above step. The new **ClientSecret** is valid for 3 years.</span></span>
    
```
  $bytes = New-Object Byte[] 32
$rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
$rand.GetBytes($bytes)
$rand.Dispose()
$newClientSecret = [System.Convert]::ToBase64String($bytes)
$dtStart = [System.DateTime]::Now
$dtEnd = $dtStart.AddYears(3)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Sign -Value $newClientSecret -StartDate $dtStart  -EndDate $dtEnd
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Verify -Value $newClientSecret   -StartDate $dtStart  -EndDate $dtEnd
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Password -Usage Verify -Value $newClientSecret   -StartDate $dtStart  -EndDate $dtEnd
$newClientSecret

```

4. <span data-ttu-id="a6f20-164">Скопируйте выходные данные **$newClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="a6f20-164">Copy the output of **$newClientSecret**.</span></span>
    
 
5. <span data-ttu-id="a6f20-p116">Замените **Web.config** на эти значения **ClientId** и **ClientSecret**. Вам не потребуются параметры приложения **SecondaryClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="a6f20-p116">Replace the **Web.config** with this **ClientId** and **ClientSecret**. You don't need **SecondaryClientSecret** app settings.</span></span>
    
 
6. <span data-ttu-id="a6f20-167">Подождите хотя бы 24 часа, чтобы ключ **ClientSecret** распространился в SharePoint Online (SPO).</span><span class="sxs-lookup"><span data-stu-id="a6f20-167">Wait at least 24 hours to propagate **ClientSecret** to SharePoint Office (SPO).</span></span>
    
 

## <a name="see-also"></a><span data-ttu-id="a6f20-168">См. также</span><span class="sxs-lookup"><span data-stu-id="a6f20-168">See also</span></span>


#### <a name="other-resources"></a><span data-ttu-id="a6f20-169">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="a6f20-169">Other resources</span></span>


 
 [<span data-ttu-id="a6f20-170">Размещенное у поставщика приложение не работает в SPO</span><span class="sxs-lookup"><span data-stu-id="a6f20-170">Provider Hosted App fails on SPO</span></span>](http://blogs.technet.com/b/sharepointdevelopersupport/archive/2015/03/11/provider-hosted-app-fails-on-spo.aspx)
