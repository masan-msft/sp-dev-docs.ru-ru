---
title: "Замена секрета клиента с истекающим сроком действия в надстройке SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 4c5295ea0cd345f01264f86c6d84230029c6ace8
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="replace-an-expiring-client-secret-in-a-sharepoint-add-in"></a>Замена секрета клиента с истекающим сроком действия в надстройке SharePoint
Узнайте, как добавить новый секрет клиента для надстройки SharePoint, зарегистрированной на странице AppRegNew.aspx.
 

> [!NOTE]
> Название "приложения для SharePoint" меняется на "надстройки SharePoint". В переходный период в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средствах Visual Studio по-прежнему может использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Срок действия секретов клиента для надстроек SharePoint, зарегистрированных на странице AppRegNew.aspx, завершается через год. В этой статье описано, как добавить новый секрет клиента для надстройки, а также как создать секрет клиента, действительный в течение трех лет.
 

> [!NOTE]
> Эта статья посвящена надстройкам SharePoint, распространяемым через каталог организации и зарегистрированным на странице AppRegNew.aspx. Если для регистрации надстройки использовалась Панель мониторинга продаж, см. статью [Создание или обновление идентификаторов и секретов клиентов на Панели мониторинга продаж](https://dev.office.com/officestore/docs/create-or-update-client-ids-and-secrets#bk_update).
 


## <a name="prerequisites-for-refreshing-a-client-secret"></a>Необходимые условия для обновления секрета клиента

Убедитесь в следующем перед началом работы:
 

 

-  [Помощник по входу в Microsoft Online Services](http://www.microsoft.com/download/details.aspx?id=39267) установлен на компьютере разработчика.
    
 
- Модуль PowerShell для Microsoft Online Services ( [32-разрядный](http://go.microsoft.com/fwlink/p/?linkid=236298);  [64-разрядный](http://go.microsoft.com/fwlink/p/?linkid=236297)) установлен на компьютере для разработки.
    
 
- Вы администратор фермы или клиента Office 365, для которого зарегистрирована надстройка на странице AppRegNew.aspx.
    
 

## <a name="find-out-the-expiration-dates-of-the-sharepoint-add-ins-installed-to-the-office-365-tenancy"></a>Просмотр дат истечения срока Надстройки SharePoint, установленных на клиенте Office 365


 

 

1. Откройте Windows PowerShell и запустите следующий командлет:
    
```
  Connect-MsolService

```

2. При появлении запроса введите учетные данные администратора клиента или администратора фермы для области клиента Office 365 или фермы, где надстройка зарегистрирована с использованием AppRegNew.aspx.
    
 
3. Создайте отчет со списком всех надстроек и датами истечения срока действия их секретов с помощью указанных ниже строк. Обратите внимание на особенности этого кода:
    
      - Сначала он применяет фильтр к приложениям Майкрософт, надстройкам в процессе разработки, а также нерекомендуемым надстройкам — автоматически размещенным.
    
 
  - Из оставшихся результатов он исключает надстройки не для SharePoint и надстройки с использованием асимметричных ключей, например рабочие процессы.
    
 

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

4. Откройте файл C:\temp\appsec.txt, чтобы просмотреть отчет. Не закрывайте окно Windows PowerShell для выполнения следующей процедуры, если скоро истекает срок действия какого-либо секрета.
    
 

## <a name="generate-a-new-secret"></a>Создание секрета клиента


 

 

1. Создайте переменную ИД клиента со следующем строкой, используя ИД клиента, которое имеет Надстройка SharePoint, в качестве параметра.
    
```
  $clientId = 'client id of the add-in'

```

2. Создайте новый секрет клиента со следующими строками:
    
```
  $bytes = New-Object Byte[] 32
$rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
$rand.GetBytes($bytes)
$rand.Dispose()
$newClientSecret = [System.Convert]::ToBase64String($bytes)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Sign -Value $newClientSecret -StartDate (Get-Date) -EndDate (Get-Date).AddYears(1)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Symmetric -Usage Verify -Value $newClientSecret -StartDate (Get-Date) -EndDate (Get-Date).AddYears(1)
New-MsolServicePrincipalCredential -AppPrincipalId $clientId -Type Password -Usage Verify -Value $newClientSecret -StartDate (Get-Date) -EndDate (Get-Date).AddYears(1)
$newClientSecret
```

3. Новый секрет клиента появится в консоли Windows PowerShell. Скопируйте его в текстовый файл, он будет нужен для следующей процедуры.
    
 

> [!TIP]
> По умолчанию срок действия секрета надстройки составляет один год. Вы можете сократить или увеличить его (до 3 лет) с помощью параметра **-EndDate**, трижды вызвав командлет **New-MsolServicePrincipalCredential**. Значением этого параметра должен быть объект [DateTime](http://msdn2.microsoft.com/EN-US/library/03ybds8y), превышающий значение **DateTime.Now** не более чем на 3 года.
 
## <a name="update-the-remote-web-application-in-visual-studio-to-use-the-new-secret"></a>Обновление удаленного веб-приложения в Visual Studio для использования нового секрета


> [!IMPORTANT]
>  Если ваша надстройка изначально создана с помощью предварительного выпуска Инструментов разработчика Microsoft Office для Visual Studio, она может содержать устаревшую версию файла TokenHelper (с расширением CS или VB). Если файл не содержит строку "secondaryClientSecret", то это устаревшая версия, которую следует заменить, прежде чем обновлять веб-приложение для использования нового секрета. Чтобы можно было получить копию файла финальной версии, требуется Visual Studio 2012 или более поздней версии. Создайте проект надстройки SharePoint в Visual Studio. Скопируйте файл TokenHelper из него в проект веб-приложения своей надстройки SharePoint. 
 


1. Откройте проект надстройки SharePoint в Visual Studio, а затем откройте файл web.config из проекта веб-приложения. В разделе **appSettings** указаны ключи для идентификатора и секрета клиента. Ниже приведен пример.
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>

```

2. Измените имя ключа **ClientSecret** на SecondaryClientSecret, как показано в приведенном ниже примере.
    
```XML
  <add key="SecondaryClientSecret" value="your old secret here" />
```

> [!NOTE]
> Если вы впервые выполняете эту процедуру, в файле конфигурации не будет записи свойства **SecondaryClientSecret**. Но если процедура выполняется для последующего (второго или третьего) секрета клиента, то свойство **SecondaryClientSecret** уже присутствует и содержит исходный или другой просроченный секрет. В этом случае необходимо удалить свойство **SecondaryClientSecret**, прежде чем переименовывать **ClientSecret**.

3. Добавьте новый ключ **ClientSecret** и включите в него новый секрет клиента. Результат должен выглядеть так:
    
```XML
  <appSettings>
  <add key="ClientId" value="your client id here" />
  <add key="ClientSecret" value="your new secret here" />
  <add key="SecondaryClientSecret" value="your old secret here" />
     ... other settings may be here ...
</appSettings>
```

> [!IMPORTANT]
> Вы не сможете использовать новый секрет клиента, который создали, пока не истечет срок действия текущего. Если вы замените ключ ClientId новым секретом клиента, когда отсутствует ключ SecondaryClientSecret, нужного результата не будет. Необходимо выполнить инструкции из этой статьи и подождать, пока не истечет срок действия предыдущего секрета клиента. После этого можно будет при необходимости удалить SecondaryClientSecret.

4. Если вы использовали новый файл TokenHelper, выполните повторную сборку проекта.
    
 
5. Опубликуйте веб-приложение повторно.
    
 

## <a name="create-a-client-secret-that-is-valid-for-three-years"></a>Создание секрета клиента, действительного на протяжении трех лет

Если срок действия секретов клиента истек, сначала удалите все просроченные секреты с заданным значением **clientId**. После этого создайте новые с помощью PowerShell для Microsoft Office, подождите хотя бы 24 часа, а затем протестируйте приложение с использованием нового значения **clientId** и ключа **ClientSecret**.
 

 

1. Подключитесь к Microsoft Office Online от имени администратора клиента с помощью приведенной ниже разметки, используя Windows PowerShell для SharePoint.
    
```
  import-module MSOnline
$msolcred = get-credential
connect-msolservice -credential $msolcred

```

2. Получите **ServicePrincipals** и ключи. При использовании параметра **$keys** возвращаются три записи. Замените каждое значение **KeyId** в *KeyId1*, *KeyId2* и *KeyId3*. Вы также увидите значение **EndDate** для каждого ключа. Убедитесь, что там отображается просроченный ключ.
    
     >**Примечание.** Значение **clientId** должно совпадать с просроченным **clientId**. Рекомендуется удалить все ключи (как просроченные, так и действительные) для этого идентификатора **clientId**.
    


```
  $clientId = "27c5b286-62a6-45c7-beda-abbaea6eecf2"
$keys = Get-MsolServicePrincipalCredential -AppPrincipalId $clientId
Remove-MsolServicePrincipalCredential -KeyIds @("KeyId1"," KeyId2"," KeyId3") -AppPrincipalId $clientId 

```

3. Создайте новое значение **ClientSecret** для этого идентификатора **clientID**. Для него используется то же значение **clientId**, что и на предыдущем этапе. Новое значение **ClientSecret** действительно в течение 3 лет.
    
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

4. Скопируйте выходные данные **$newClientSecret**.
    
 
5. Замените **Web.config** на эти значения **ClientId** и **ClientSecret**. Вам не потребуются параметры приложения **SecondaryClientSecret**.
    
 
6. Подождите хотя бы 24 часа, чтобы ключ **ClientSecret** распространился в SharePoint Online (SPO).
    
 

## <a name="see-also"></a>См. также

[Размещаемое у поставщика приложение не работает в SPO](http://blogs.technet.com/b/sharepointdevelopersupport/archive/2015/03/11/provider-hosted-app-fails-on-spo.aspx)
