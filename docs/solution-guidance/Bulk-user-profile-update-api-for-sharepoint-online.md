---
title: Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online
ms.date: 11/03/2017
ms.openlocfilehash: f758e3aea35bf83519cf48059f33f9846ebc5cd9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a>Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online


_**Applies to:** SharePoint Online_

As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties. Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles. However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).

Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a>An Overview of the Bulk User Profile Update Process
<a name="sectionSection0"> </a>

![Bulk UPA update flow](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. User attributes are synchronized from the corporate Active Directory to the Azure Active Directory. You can select which attributes are replicated across on-premises and Azure.
2. A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365. Unlke on-premises SharePoint, these attributes cannot be customized.
3. A custom synchronization tool taking advantage of the new bulk update APIs. This tool uploads a JSON file to the Office 365 tenant and queues the import process. This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.
4. A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file. This could also be a combination of data from Active Directory and any external system. Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.
5. An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.
6. Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.

> [!NOTE] 
> The import only works for user profile properties which have **not** been set to be editable by end users. This is to prevent the user profile import process from overriding any information which an end user has already updated. Additionally, the import only allows custom properties that are not active directory core properties. These must be synchronized to Azure Active Directory. For the list of these core directory properties, see the table listed in the FAQ section below.

Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell. You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a>Import File Format
<a name="sectionSection1"> </a>

The import process uses a JSON file containing the properties and their values. Below is the expected structure of that file:   

```JSON
{
   "value": [
     {
       "<IdName>": "<UserIdValue_1>",
       "<AttributeName_1>": "<User1_AttributeValue_1>",
       "<AttributeName_2>": "<User1_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_2>",
       "<AttributeName_1>": "<User2_AttributeValue_1>",
       "<AttributeName_2>": "<User2_AttributeValue_2>",
     },
     {
       "<IdName>": "<UserIdValue_n>",
       "<AttributeName_1>": "<Usern_AttributeValue_1>",
       "<AttributeName_2>": "<Usern_AttributeValue_2>",
     }
   ]
}
```

Below is a simple example file using the format above:

```JSON
{
  "value": [
    {
      "IdName": "vesaj@contoso.com",
      "City": "Helsinki",
      "Office": "Viper"
    },
    {
      "IdName": "bjansen@contoso.com",
      "City": "Brussels",
      "Office": "Beetle"
    },
    {
      "IdName": "unknowperson@contoso.com",
      "City": "None",
      "Office": ""
    },
    {
      "IdName": "erwin@contoso.com",
      "City": "Stockholm",
      "Office": "Elite"
    }
  ]
}
```

In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`. The file contains information for four different accounts within the tenant. Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code. 

### <a name="source-data-file-restrictions"></a>Source Data File Restrictions
There are few restrictions on individual source data files:
- Maximum file size: 2GB
- Maximum number of properties: 500,000
- The source file must be uploaded to the same SharePoint Online tenant where the process is started


## <a name="user-profile-property-import-process"></a>User Profile Property Import Process
<a name="sectionSection2"> </a>

Here’s the full process:

1. Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it
     - When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.
2. Create any needed custom properties within the User Profile Service
     - Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).
     - Only user profile properties which are not “allowed to be edited by end users” can be imported. Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.
3. Create and upload the JSON file to the Office 365 tenant
     - You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.
     - In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.
     - Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API. You should consider the life cycle of these files within your implementation. These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.
4. Call the bulk UPA Import API for queuing the import job
     - Use the CSOM API to queue the import process. This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.
     - The method to queue the job requires property mapping information and the location of the data file. This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.
5. Check the status of the import job
     - You can also use remote APIs to check the status of a specific import job or all of the recent import jobs. To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.


## <a name="csom-api-for-the-bulk-import-process"></a>CSOM API for the Bulk Import Process
<a name="sectionSection3"> </a>

### <a name="queue-import"></a>Queue Import
You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object. This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later. Here’s the full signature of the method:

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a>Параметры

**Тип_идентификатора**:_[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_

The type of id to use when looking up the user profile. Possible values are `Email`, `CloudId`, and `PrincipalName`. Note that regardless of the type, the user must already exist in the User Profile Service for the import to work. It’s recommended to use the `CloudId` to ensure uniqueness.

Property mapping between ID Type and Azure AD property:

UPA Bulk Import ID Type | Azure Directory Attribute
--- | ---
CloudId | ObjectID
PrincipalName | userPrincipalName
Email | mail

**sourceDataIdProperty**: _`System.String`_

The name of the id property in the source data. The value of the property from the source data will be used to lookup the user. The User Profile Service property used for the lookup depends on the value of `idType`.

**propertyMap**: _`IDictionary<string, string>`_

A map from the source property name to the User Profile Service property name. Note that the User Profile Service properties must already exist. The key is the property name used in the source file, the value is the property name used in the User Profile Service.

**sourceUri**: _`System.String`_

The URI of the source data file to import. Файл не должен перемещен или удалить сразу, так как он не могут быть загружены в течение некоторого времени.

#### <a name="return-value"></a>Возвращаемое значение
A Guid that identifies the import job that has been queued.

#### <a name="example"></a>Пример
Below is an example using C# of how to start the process using the sample input file above:

```c#
// Create an instance of the Office 365 Tenant object. Loading this object is not technically needed for this operation. 
Office365Tenant tenant = new Office365Tenant(ctx);
ctx.Load(tenant);
ctx.ExecuteQuery();

// Type of user identifier ["PrincipalName", "Email", "CloudId"] in the 
// User Profile Service. In this case, we use Email as the identifier at the UPA storage
ImportProfilePropertiesUserIdType userIdType = 
      ImportProfilePropertiesUserIdType.Email;

// Name of the user identifier property within the JSON file
var userLookupKey = "IdName";

var propertyMap = new System.Collections.Generic.Dictionary<string, string>();

// The key is the property in the JSON file, 
// The value is the user profile property Name in the User Profile Service
// Notice that we have 2 custom properties in UPA called 'City' and 'OfficeCode'
propertyMap.Add("City", "City");
propertyMap.Add("Office", "OfficeCode");

// Returns a GUID which can be used to check the status of the execution and the end results
var workItemId = tenant.QueueImportProfileProperties(
      userIdType, userLookupKey, propertyMap, fileUrl
      );

ctx.ExecuteQuery();
```

### <a name="check-the-status-of-an-import-job"></a>Check the Status of an Import Job
Вы также можете проверить состояние задания импорта службы профилей пользователей с помощью новых интерфейсов API CSOM. Существует два метода новой базы данных для объекта клиента.

You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object. You will need to have the unique identifier of a specific import job provided as a parameter to this method. Ниже приведен полный подпись метода.

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a>Параметры
**jobID**: _`System.Guid`_

The id of the job for which to get the high-level status.

#### <a name="return-value"></a>Возвращаемое значение

[`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Объект с высокого уровня сведений о указанного задания.

#### <a name="example"></a>Пример
Ниже пример использует C# для получение сведений о состоянии с помощью сохраненных идентификатор задания определенных импорта:

```c#
// Check the status of a specific request based on the job id received when we queued the job
Office365Tenant tenant = new Office365Tenant(ctx);
var job = tenant.GetImportProfilePropertyJob(workItemId);
ctx.Load(job);
ctx.ExecuteQuery();
```

Можно проверить состояние всех заданий импорта с помощью [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) метод находится в объекте [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) . Ниже приведен полный подпись метода.

```c#
public ImportProfilePropertiesJobStatusCollection GetImportProfilePropertyJobs(); 
```

#### <a name="return-value"></a>Возвращаемое значение
[`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) Объект, который представляет собой коллекцию из [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) объекты с высокого уровня состояния сведения о каждом из заданий.

#### <a name="example"></a>Пример
Ниже пример использует C# для получения состояния всех заданий импорта, в настоящее время сохранены в клиентов. Это может быть уже обработан или в очереди заданий:

```c#
// Load all import jobs – old and queued ones
Office365Tenant tenant = new Office365Tenant(ctx);
var jobs = tenant.GetImportProfilePropertyJobs();
ctx.Load(jobs);
ctx.ExecuteQuery();
foreach (var item in jobs)
{
   // Check whatever properties needed
   var state = item.State;
}
```

[`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Объект, возвращенный с сведения о состоянии импорта имеет следующие свойства. 

**JobId**:_`System.Guid`_

Идентификатор задания импорта

**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_

Перечисление с помощью следующих значений:
- `Unknown`-Мы не может определить состояние задания
- `Submitted`-Задания отправки в систему
- `Processing`-Обрабатывается задание
- `Queued`-Заданием прошел проверку и в очередь для импорта для однозначного соответствия
- `Succeeded`-Задание завершена без ошибок
- `Error`-Задание завершено с ошибкой

**SourceUri**:_`System.String`_

URI файл источника данных

**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_

Перечисление, представляющее возможные ошибки:
- `NoError`-Ошибка не найден
- `InternalError`-Ошибки, возникающие при сбоя в службе
- `DataFileNotExist`-Не удалось найти файл источника данных
- `DataFileNotInTenant`-Файл источника данных принадлежит же клиента
- `DataFileTooBig`— Размер файла данных слишком велико
- `InvalidDataFile`-Файл источника данных не прошли проверку (может быть Дополнительные сведения в файле журнала)
- `ImportCompleteWithError`-Импорт данных, но произошла ошибка возникала

**Сообщение об ошибке**:_`System.String`_

The error message

**LogFileUri**:_`System.String`_

Uri в папку, где были записаны журналы

## <a name="calling-the-import-api-from-powershell"></a>Вызов API импорта из PowerShell
<a name="sectionSection4"> </a>

Вы можете воспользоваться преимуществами API импорта массового службы профилей пользователей с помощью PowerShell. Это означает, что вы будете использовать в коде CSOM непосредственно в сценарий PowerShell, используя необходимые параметры. Для этого необходимо, что обновленные распространяемый пакет CSOM был установлен на компьютере, где выполняется скрипт.

С помощью PowerShell, нет необходимости для компиляции кода в Visual Studio, которые могут быть более подходящим модели для некоторых клиентов.

### <a name="sample-powershell-script"></a>Образец сценария PowerShell
Ниже приведен образец сценария PowerShell, который выполняет те же действия, как приведенный выше код: 

```Powershell
# Get needed information from the end user
$adminUrl = Read-Host -Prompt 'Enter the admin URL of your tenant'
$userName = Read-Host -Prompt 'Enter your user name'
$pwd = Read-Host -Prompt 'Enter your password' -AsSecureString
$importFileUrl = Read-Host -Prompt 'Enter the URL to the file located in your tenant'

# Get instances to the Office 365 tenant using CSOM
$uri = New-Object System.Uri -ArgumentList $adminUrl
$context = New-Object Microsoft.SharePoint.Client.ClientContext($uri)

$context.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($userName, $pwd)
$o365 = New-Object Microsoft.Online.SharePoint.TenantManagement.Office365Tenant($context)
$context.Load($o365)

# Type of user identifier ["Email", "CloudId", "PrincipalName"] in the User Profile Service
$userIdType=[Microsoft.Online.SharePoint.TenantManagement.ImportProfilePropertiesUserIdType]::Email

# Name of user identifier property in the JSON
$userLookupKey="idName"

# Create property mapping between the source file property name and the O365 property name
# Notice that we have here 2 custom properties in UPA called 'City' and 'OfficeCode'
$propertyMap = New-Object -type 'System.Collections.Generic.Dictionary[String,String]'
$propertyMap.Add("City", "City")
$propertyMap.Add("Office", "OfficeCode")

# Call to queue UPA property import 
$workItemId = $o365.QueueImportProfileProperties($userIdType, $userLookupKey, $propertyMap, $importFileUrl);

# Execute the CSOM command for queuing the import job
$context.ExecuteQuery();

# Output the unique identifier of the job
Write-Host "Import job created with the following identifier:" $workItemId.Value 
```

## <a name="handling-exceptions"></a>Обработка исключений
<a name="sectionSection5"></a> Существует два уровня проверки при использовании этот интерфейс API. При запуске процесса импорта с помощью CSOM будет начальной уровень проверки указанные значения. Этот компонент включает подтверждения существование отмеченными сопоставление свойств в службе профилей пользователей и, что эти свойства недоступны для редактирования конечным пользователем. При вызове API очереди применяется только начальной уровень проверки и ее реального выполнения задания импорта выполняется последний проверка предоставлена информация.

Если во время выполнения задания импорта сведения о любых исключениях, в ту же библиотеку документов, где был задан Импорт файла создается файл ведения журнала с дополнительными сведениями. Будут сохранены файлы журналов для задания определенных импорта sub папки с именами с помощью уникальный идентификатор задания определенных импорта.

Ниже приведен пример результаты выполнения задания импорта. На рисунке ниже можно увидеть две вложенные папки для двух различных выполнений, создаваемых в библиотеке документов, где хранится файл импорта:

![Задание исключение вложенные папки](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-folders.png)

Файл журнала сохраняется в папке sub и для подробного анализа, который можно загрузить из Office 365:

![Задание файла журнала исключений](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-LogFile.png)

### <a name="common-exceptions"></a>Общие исключения

Следующая таблица содержит типичные исключения, которые могут возникнуть при запуске с помощью API массового службы профилей пользователей.

Пример исключений | Сведения
--- | ---
_Имена свойств [AboutMe] становятся недоступны для изменения пользователем._ | Это может быть создано с помощью CSOM API, при вызове `ExecuteQuery` метод при отправке задания к клиенту. API-Интерфейс будет проверять, что все свойства, которые в настоящий момент сопоставленные не редактируемое пользователем. Исключение будет отметить свойство, которое не может использоваться. В этом примере мы попытались сопоставление свойства JSON для `AboutMe` свойство в свойствах службы профилей пользователей, но это не допускается с момента `AboutMe` — это редактируемых свойств пользователя.
_InvalidProperty - vesaj@contoso.com свойство «AboutMe» не связан с любого свойства в приложение профилей пользователей._ | Файл данных JSON содержатся свойства, которое не сопоставлен свойства службы профилей пользователей в SharePoint Online. Это означает, что файл источника данных содержит свойства, для которых не заданы сопоставления в `propertyMap` параметр. Необходимо будет иметь определения сопоставления для каждого свойства объекта данных JSON.
_MissingIdentity - идентификатор отсутствует для объекта пользователя_ | Свойство identity не найден в объекте пользователя. Возможная причина в том, что `sourceDataIdProperty` неправильно имеет атрибут `QueueImportProfileProperties` метод. Убедитесь, имеют свойство right в исходном файле JSON и код или сценарий является назначение соответствующим образом этого атрибута.
_Не удалось разрешить IdentityNotResolvable unknown@contoso.com удостоверения пользователя_ | Файл данных содержится удостоверение, которое не удалось разрешить или не существует в службе профилей пользователей. В этом случае профилей пользователей с помощью электронной почты из _unknown@contoso.com_ не удается найти в службе профилей пользователей.
_DataFileNotJson - JsonToken EndObject не является допустимым для закрытия JsonType массива. Путь «значение», строка 8, поместите 10._ | В качестве формата формат файла импорта, не является допустимым JSON и не соответствует ожидаемому формату. 

## <a name="frequently-asked-questions"></a>Frequently Asked Questions
<a name="sectionSection6"> </a>

**Может выполнять код, использующий разрешения только для приложения только/надстройки**

Да, необходимо зарегистрировать идентификатор клиента и секрет должны иметь возможность выполнять интерфейсов API. Так как фактический импорт файла не синхронно с идентификатором вызывающего абонента, это работает без ошибок.

**Этот интерфейс API обновление свойств в службе профилей пользователей, но как я создаст этих свойств в клиента?**

Нет удаленного интерфейса API для создания настраиваемого пользовательского свойства профиля программным способом, поэтому это вручную операция, которой следует выполнить один раз в заданном клиента. Можно найти [в этой статье](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) представлены инструкции по созданию этих настраиваемых свойств.

**Эта возможность доступна в локальном SharePoint?**

К сожалению эта возможность в настоящее время используется только для SharePoint Online. В локальном SharePoint эта возможность будет полезен, но не как критические с момента его можно изменить сопоставление атрибутов в приложении-службе профилей пользователей в локальной. Также можно воспользоваться преимуществами Импорт атрибутов профиля пользователя, с помощью службы Business Connectivity (BCS) в SharePoint 2013. Тем не менее этот параметр недоступен в 2016 SharePoint, которая означает, что SharePoint 2016 только параметр в настоящее время для реализации настроек, которые воспользоваться преимуществами пользователя веб-службы профилей.

**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**
Да, локального развертывания SharePoint можно использовать так же, как и любой другой системе источника. Необходимо экспортировать значения профиля пользователя из локального SharePoint в формате JSON и затем процесс будет точно совпадает с Импорт значения из другой системе.

**Can I import string based, multi-value properties?**
No, this is not currently supported with this API.

**What permissions are required for executing this API??**
You will need to have Global Admin permissions currently. Недостаточно администрирования SharePoint.

**Можно импортировать на основе таксономии**
Нет, это не поддерживается в настоящее время этот интерфейс API.

**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**
If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties. If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.

**Что делать, если я необходима для обновления настраиваемых свойств, выходящим за пределы ограничения размера этот интерфейс API массового (то есть > файл 2 ГБ или > 500 000 свойств)?**
Необходимо пакетных заданий соответствующим образом, запуск нескольких заданий в последовательности (то есть завершения одно задание за раз с максимальное ограничение на этот интерфейс API). You should expect these high bandwidth imports will take a long time to complete. Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.

**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**
See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.

Атрибут Azure каталога  | SharePoint Online Profile Property
---------|----------
ObjectSid | SPS-SavedSID
msonline-UserPrincipalName | UserName
msonline-UserPrincipalName | AccountName
msonline-UserPrincipalName | SPS-ClaimID
msonline-UserPrincipalName | SPS-UserPrincipalName
GivenName | FirstName
sn | LastName
Manager | Manager
DisplayName | PreferredName
telephoneNumber | WorkPhone
proxyAddresses | WorkEmail
proxyAddresses | SPS-SIPAddress
PhysicalDeliveryOfficeName | Office
Заголовок | Заголовок
Заголовок | SPS-JobTitle
Department | Department
Department | SPS-Department
ObjectGuid | ADGuid
WWWHomePage | PublicSiteRedirect
DistinguishedName | SPS-DistinguishedName
msOnline-ObjectId | msOnline-ObjectId
PreferredLanguage | SPS-MUILanguages
msExchHideFromAddressList | SPS-HideFromAddressLists
msExchRecipientTypeDetails | SPS-RecipientTypeDetails
msonline-groupType | IsUnifiedGroup
msOnline-IsPublic | IsPublic
msOnline-ObjectId | msOnline-ObjectId
msOnline-UserType | SPS-UserType
GroupType | GroupType
SPO-IsSharePointOnlineObject | SPO-IsSPO

