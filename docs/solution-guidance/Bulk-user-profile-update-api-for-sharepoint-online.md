---
title: "Общие сведения об API для массового обновления настраиваемых свойств профиля для SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 1742bdc985fa133bb6866803ce37aac74c419e17
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a>Общие сведения об API для массового обновления настраиваемых свойств профиля для SharePoint Online


_**Применимо к:** SharePoint Online_

Как часть из нового клиента со стороны объектную модель (CSOM) версия (4622.1208 или более поздней версии) SharePoint, может выполнить массовый импорт настраиваемых свойств профиля. В предыдущих версиях единственным вариантом было воспользоваться преимуществами пользователя профилей CSOM операций для обновления определенных свойств профилей отдельных пользователей. Тем не менее этот подход неэффективны и слишком много времени (особенно при работе с тысячами профили).

Многие предприятия необходимо воспроизвести настраиваемые атрибуты для службы профилей пользователей SharePoint и поэтому было освобождено дополнительные массового API профилей высокой производительностью пользователя.

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a>Обзор процесса обновления массового профиля пользователя
<a name="sectionSection0"> </a>

![Массовое обновление поток UPA](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. Атрибуты пользователя синхронизируются из корпоративного Active Directory для Azure Active Directory. Вы можете выбрать, какие атрибуты реплицируются между локальной и Azure.
2. Типовой набор атрибутов, реплицируются из Azure Active Directory в хранилище профилей пользователя SharePoint Online в Office 365. Unlke локальной SharePoint, не могут настраивать эти атрибуты.
3. Воспользуйтесь преимуществами новых массового обновления API-интерфейсы средство синхронизации. Это средство отправляет файл JSON для клиента Office 365 и ставит в очередь процесс импорта. Это средство может осуществляться с помощью управляемого кода (.NET) или как PowerShell использовать при написании скриптов с помощью новых интерфейсов API CSOM.
4. Строка из БИЗНЕС-системы, или любой внешней системы, который является источником данных в файле JSON. Это может быть сочетание данных из Active Directory и все внешние системы. Обратите внимание на то, что с точки зрения API бизнес-системы может быть SharePoint 2013 в локальной или 2016 фермы.
5. Сообщение о поле server со стороны запущено задание таймера в SharePoint online которого выполняется поиск в очередь запросы на импорт и будет выполнять операцию импорта на основе вызовов API и сведений о в файле отмеченными JSON.
6. Сведения о профилях пользователей расширенного доступен в профили пользователей и может использоваться для каких-либо вне поля или пользовательские функциональные возможности в SharePoint online.

>**Примечание**: импорт работает только для свойств профиля пользователя которого **не** были задайте значение будет изменять в конечных пользователей. Это запрет на переопределение все сведения, которые конечный пользователь уже обновлен процесс импорта профилей пользователей. Кроме того Импорт позволяет только настраиваемые свойства, которые не являются основных свойств active directory. Они должны быть синхронизированы для Azure Active Directory. Список этих основных свойств каталога представлен в таблице в представленном ниже разделе вопросы и ответы.

Ниже приведен короткий видеоролик, демонстрирующий использование нового интерфейса API CSOM из обоих управляемого кода (.NET) и PowerShell. Можно найти в примере кода используется, включая сценарий PowerShell в [Коллекции кодов PnP разработчиков Office](http://dev.office.com/patterns-and-practices-detail/7202).

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a>Формат файла импорта
<a name="sectionSection1"> </a>

Процесс импорта использует файл JSON, содержащий свойства и их значения. Ниже приведена структура ожидаемых, файл:   

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

Ниже — это простой пример файла в формате выше:

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

В приведенном выше примере на основе разрешение идентификаторов `IdName` свойства и имеется два свойства, которые обновляются называется `City` и `Office`. Файл содержит сведения о четыре различные учетные записи в рамках клиента. Имена свойств, используемых в этом исходный файл не обязательно то же, что имена, используемые в службе SharePoint Online пользовательского профиля с момента сопоставления правильные свойства предоставляются в пределах нашего кода. 

### <a name="source-data-file-restrictions"></a>Ограничения файлов источника данных
Существует несколько ограничений на отдельные исходные файлы данных.
- Максимальный размер файла: 2 ГБ
- Максимальное число свойств: 500 000
- Исходный файл необходимо загрузить же владельцу SharePoint Online, где запущен процесс


## <a name="user-profile-property-import-process"></a>Процесс импорта свойств профиля пользователя
<a name="sectionSection2"> </a>

Ниже приведен полный процесс:

1. Создание и синхронизация пользователей в Office 365 для клиентов или Azure AD, связанная с ним
     - Пользователи синхронизируются с Azure AD, он будет синхронизировать типовой набор атрибутов в службу SharePoint Online пользовательского профиля.
2. Создать любые необходимые пользовательские свойства в рамках службы профилей пользователей
     - Так как для создания настраиваемых свойств в службе профилей пользователей не удаленных интерфейсов API, это действие необходимо выполнить вручную для каждого из клиентов там, где необходимо настраиваемых свойств профиля (это действие необходимо выполнить один раз на клиента).
     - Можно импортировать только свойства профиля пользователя недопустимые «редактировать конечные пользователи». Попытка импорта JSON свойства объекта значение свойства профиля пользователя, помеченные как «редактируемого конечными пользователями» приведет к исключение при вызове CSOM API.
3. Создание и отправка файла JSON для клиента Office 365
     - Необходимо отправить файл данных JSON, содержащий данные, которые следует обновить до клиента Office 365.
     - В случае любого исключения во время импорта SharePoint будет предоставлять дополнительных сведений в журналах сохраняются в ту же библиотеку документов, где файл существовал в новую папку sub.
     - Удаление файлов журнала и JSON файлы не происходит автоматически и несет ответственность за пользовательских решений с помощью API-интерфейса. Жизненный цикл этих файлов необходимо учитывать в реализации. Эти файлы хранятся в библиотеках документов, их использование часть назначенный хранилища для семейства веб-сайтов.
4. Вызов массового UPA Импорт API для очереди задание импорта
     - Использование CSOM API в очередь процесс импорта. Это можно сделать с помощью CSOM кода с помощью управляемого кода (.NET) или PowerShell.
     - Метод в очередь задания требует сведения о сопоставлении свойств и расположение файла данных. Этот метод выполняется быстро, так как он просто ставит в очередь фактического процесса импорта, который будет выполняться более поздней версии в ходе процесса серверного компонента в SharePoint Online.
5. Проверка состояния задания импорта
     - Можно также использовать API удаленного для проверки состояния задания определенных импорта или все последние задания импорта. Чтобы можно было проверить состояние выполнения определенного вызова, следует хранить идентификатор задания уникальный, полученных как возвращаемое значение, когда в очереди заданий.


## <a name="csom-api-for-the-bulk-import-process"></a>CSOM API для группового импорта
<a name="sectionSection3"> </a>

### <a name="queue-import"></a>Импорт очереди
Можно поместить в очередь процесс импорта, вызвав [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) метод находится в [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) объекта. Это асинхронный вызов, в том, что она не загрузить исходных данных или выполняется импорт, просто добавляет рабочий элемент в очередь для этого более поздней версии. Ниже приведен полный подпись метода.

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a>Параметры

**Тип_идентификатора**:_[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_

Тип идентификатора для использования при поиске профилей пользователей. Возможные значения: `Email`, `CloudId`, и `PrincipalName`. Обратите внимание, что независимо от типа, пользователь должен существовать в службе профилей пользователей для импорта для работы. Рекомендуется использовать `CloudId` для обеспечения уникальности.

Сопоставление свойств между тип идентификатора и свойство Azure AD:

Идентификатор типа UPA массового импорта | Атрибут Azure каталога
--- | ---
CloudId | ObjectID
PrincipalName | userPrincipalName
Email | mail

**sourceDataIdProperty**:_`System.String`_

Имя свойства id в источнике данных. Значение свойства из источника данных будет использоваться для поиска пользователя. Свойства службы профилей пользователей, используемые для поиска зависит от значения `idType`.

**propertyMap**:_`IDictionary<string, string>`_

Сопоставление имени свойства источника имени свойства службы профилей пользователей. Обратите внимание, что свойства службы профилей пользователей должен существовать. Ключ — это имя свойства, используемые в исходном файле, значение — это имя свойства, используемые в службе профилей пользователей.

**sourceUri**:_`System.String`_

URI исходного файла данных для импорта. Файл не должен перемещен или удалить сразу, так как он не могут быть загружены в течение некоторого времени.

#### <a name="return-value"></a>Возвращаемое значение
Guid, идентифицирующий задание импорта, который находится в очереди.

#### <a name="example"></a>Пример
Ниже приведен пример с помощью C#, необходимых начать процесс, с помощью выше пример входного файла.

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

### <a name="check-the-status-of-an-import-job"></a>Проверка состояния задания импорта
Вы также можете проверить состояние задания импорта службы профилей пользователей с помощью новых интерфейсов API CSOM. Существует два метода новой базы данных для объекта клиента.

Можно проверить состояние задания отдельных импорта с помощью [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) метод находится в [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) объекта. Необходимо будет иметь уникальный идентификатор определенного задания, представленные в качестве параметра этого метода импорта. Ниже приведен полный подпись метода.

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a>Параметры
**jobID**:_`System.Guid`_

Идентификатор задания, для которого необходимо получить сведения о состоянии высокого уровня.

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

**Состояние**:_[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_

Перечисление с помощью следующих значений:
- `Unknown`-Мы не может определить состояние задания
- `Submitted`-Задания отправки в систему
- `Processing`-Обрабатывается задание
- `Queued`-Заданием прошел проверку и в очередь для импорта для однозначного соответствия
- `Succeeded`-Задание завершена без ошибок
- `Error`-Задание завершено с ошибкой

**SourceUri**:_`System.String`_

URI файл источника данных

**Ошибка**:_[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_

Перечисление, представляющее возможные ошибки:
- `NoError`-Ошибка не найден
- `InternalError`-Ошибки, возникающие при сбоя в службе
- `DataFileNotExist`-Не удалось найти файл источника данных
- `DataFileNotInTenant`-Файл источника данных принадлежит же клиента
- `DataFileTooBig`— Размер файла данных слишком велико
- `InvalidDataFile`-Файл источника данных не прошли проверку (может быть Дополнительные сведения в файле журнала)
- `ImportCompleteWithError`-Импорт данных, но произошла ошибка возникала

**Сообщение об ошибке**:_`System.String`_

Сообщение об ошибке

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

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы
<a name="sectionSection6"> </a>

**Может выполнять код, использующий разрешения только для приложения только/надстройки**

Да, необходимо зарегистрировать идентификатор клиента и секрет должны иметь возможность выполнять интерфейсов API. Так как фактический импорт файла не синхронно с идентификатором вызывающего абонента, это работает без ошибок.

**Этот интерфейс API обновление свойств в службе профилей пользователей, но как я создаст этих свойств в клиента?**

Нет удаленного интерфейса API для создания настраиваемого пользовательского свойства профиля программным способом, поэтому это вручную операция, которой следует выполнить один раз в заданном клиента. Можно найти [в этой статье](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) представлены инструкции по созданию этих настраиваемых свойств.

**Эта возможность доступна в локальном SharePoint?**

К сожалению эта возможность в настоящее время используется только для SharePoint Online. В локальном SharePoint эта возможность будет полезен, но не как критические с момента его можно изменить сопоставление атрибутов в приложении-службе профилей пользователей в локальной. Также можно воспользоваться преимуществами Импорт атрибутов профиля пользователя, с помощью службы Business Connectivity (BCS) в SharePoint 2013. Тем не менее этот параметр недоступен в 2016 SharePoint, которая означает, что SharePoint 2016 только параметр в настоящее время для реализации настроек, которые воспользоваться преимуществами пользователя веб-службы профилей.

**Может использовать этот интерфейс API для синхронизации значений свойств профиля пользователя из личных SharePoint 2013 в локальной или 2016 farm(s) в SharePoint Online?**
Да, локального развертывания SharePoint можно использовать так же, как и любой другой системе источника. Необходимо экспортировать значения профиля пользователя из локального SharePoint в формате JSON и затем процесс будет точно совпадает с Импорт значения из другой системе.

**Можно импортировать на основе, строка многозначного свойства**
Нет, это не поддерживается в настоящее время этот интерфейс API.

**Какие разрешения необходимы для выполнения этой API??**
Необходимо иметь разрешения глобального администратора в настоящее время. Недостаточно администрирования SharePoint.

**Можно импортировать на основе таксономии**
Нет, это не поддерживается в настоящее время этот интерфейс API.

**Что делать, если я определить сопоставление в коде, который не используется или настроены параметры в файле JSON, не отнесенные?**
Если код или сценарий определяет сопоставление, который не используется или файл данных не содержит свойства для этого сопоставления, выполнение продолжается без все исключения и импорт будет применяться на основании сопоставленных свойств. Если, тем не менее, свойство в файле JSON, который не связан, процесс импорта будет отменена, и сведения об исключении будет предоставляться в файле журнала для выполнения определенного задания.

**Что делать, если я необходима для обновления настраиваемых свойств, выходящим за пределы ограничения размера этот интерфейс API массового (то есть > файл 2 ГБ или > 500 000 свойств)?**
Необходимо пакетных заданий соответствующим образом, запуск нескольких заданий в последовательности (то есть завершения одно задание за раз с максимальное ограничение на этот интерфейс API). Следует ожидать эти imports высокой пропускной способностью будет уйти много времени выполнения. Кроме того следует оптимизировать задания импорта только для дельта изменения пользовательских свойств профилей, а не полный набор значений в все задания импорта.

**Какие атрибуты Azure Active Directory выполняется синхронизация были вынуждены SharePoint Online профиля пользователя по умолчанию?**
Обратитесь к таблице ниже официальная список синхронизированных атрибуты и их сопоставление между Azure Active Directory и службы Online профилей пользователей SharePoint.

Атрибут Azure каталога  | Свойство SharePoint Online профиля
---------|----------
ObjectSid | SPS SavedSID
msonline UserPrincipalName | Имя пользователя
msonline UserPrincipalName | Имя учетной записи
msonline UserPrincipalName | SPS ClaimID
msonline UserPrincipalName | SPS UserPrincipalName
GivenName | FirstName
Sn | Фамилия
Руководитель | Руководитель
Отображаемое имя | PreferredName
telephoneNumber | WorkPhone
proxyAddresses. | WorkEmail
proxyAddresses. | SPS SIPAddress
PhysicalDeliveryOfficeName | Office
Заголовок | Заголовок
Заголовок | Название должности SPS
Отдел | Отдел
Отдел | Отдел SPS
ObjectGuid | ADGuid
WWWHomePage | PublicSiteRedirect
DistinguishedName | SPS DistinguishedName
msOnline ObjectId | msOnline ObjectId
PreferredLanguage | SPS MUILanguages
msExchHideFromAddressList | SPS HideFromAddressLists
msExchRecipientTypeDetails | SPS RecipientTypeDetails
msonline groupType | IsUnifiedGroup
msOnline IsPublic | IsPublic
msOnline ObjectId | msOnline ObjectId
msOnline UserType | SPS UserType
GroupType | GroupType
SPO IsSharePointOnlineObject | SPO IsSPO

