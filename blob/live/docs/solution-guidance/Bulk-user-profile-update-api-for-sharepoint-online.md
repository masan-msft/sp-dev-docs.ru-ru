---
title: "Общие сведения об API для массового обновления настраиваемых свойств профиля для SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: 1742bdc985fa133bb6866803ce37aac74c419e17
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="introducing-the-api-for-bulk-updating-custom-user-profile-properties-for-sharepoint-online"></a><span data-ttu-id="dddd2-102">Общие сведения об API для массового обновления настраиваемых свойств профиля для SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="dddd2-102">Introducing the API for Bulk Updating Custom User Profile Properties for SharePoint Online</span></span>


<span data-ttu-id="dddd2-103">_**Применимо к:** SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="dddd2-103">_**Applies to:** SharePoint Online_</span></span>

<span data-ttu-id="dddd2-104">Как часть из нового клиента со стороны объектную модель (CSOM) версия (4622.1208 или более поздней версии) SharePoint, может выполнить массовый импорт настраиваемых свойств профиля.</span><span class="sxs-lookup"><span data-stu-id="dddd2-104">As part of the new Client Side Object Model (CSOM) version (4622.1208 or newer), SharePoint has the ability to bulk import custom user profile properties.</span></span> <span data-ttu-id="dddd2-105">В предыдущих версиях единственным вариантом было воспользоваться преимуществами пользователя профилей CSOM операций для обновления определенных свойств профилей отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-105">Prior to this release, your only option was to take advantage of the user profile CSOM operations for updating specific properties for individual user profiles.</span></span> <span data-ttu-id="dddd2-106">Тем не менее этот подход неэффективны и слишком много времени (особенно при работе с тысячами профили).</span><span class="sxs-lookup"><span data-stu-id="dddd2-106">However, this approach is inefficient and too time consuming (especially when dealing with thousands of profiles).</span></span>

<span data-ttu-id="dddd2-107">Многие предприятия необходимо воспроизвести настраиваемые атрибуты для службы профилей пользователей SharePoint и поэтому было освобождено дополнительные массового API профилей высокой производительностью пользователя.</span><span class="sxs-lookup"><span data-stu-id="dddd2-107">Many enterprises need to replicate custom attributes to the SharePoint user profile service and so a more performant user profile bulk API has been released.</span></span>

## <a name="an-overview-of-the-bulk-user-profile-update-process"></a><span data-ttu-id="dddd2-108">Обзор процесса обновления массового профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="dddd2-108">An Overview of the Bulk User Profile Update Process</span></span>
<span data-ttu-id="dddd2-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="dddd2-109"></span></span>

![Массовое обновление поток UPA](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess.png)

1. <span data-ttu-id="dddd2-111">Атрибуты пользователя синхронизируются из корпоративного Active Directory для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dddd2-111">User attributes are synchronized from the corporate Active Directory to the Azure Active Directory.</span></span> <span data-ttu-id="dddd2-112">Вы можете выбрать, какие атрибуты реплицируются между локальной и Azure.</span><span class="sxs-lookup"><span data-stu-id="dddd2-112">You can select which attributes are replicated across on-premises and Azure.</span></span>
2. <span data-ttu-id="dddd2-113">Типовой набор атрибутов, реплицируются из Azure Active Directory в хранилище профилей пользователя SharePoint Online в Office 365.</span><span class="sxs-lookup"><span data-stu-id="dddd2-113">A standardized set of attributes are replicated from Azure Active Directory to the SharePoint Online User Profile Store within Office 365.</span></span> <span data-ttu-id="dddd2-114">Unlke локальной SharePoint, не могут настраивать эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="dddd2-114">Unlke on-premises SharePoint, these attributes cannot be customized.</span></span>
3. <span data-ttu-id="dddd2-115">Воспользуйтесь преимуществами новых массового обновления API-интерфейсы средство синхронизации.</span><span class="sxs-lookup"><span data-stu-id="dddd2-115">A custom synchronization tool taking advantage of the new bulk update APIs.</span></span> <span data-ttu-id="dddd2-116">Это средство отправляет файл JSON для клиента Office 365 и ставит в очередь процесс импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-116">This tool uploads a JSON file to the Office 365 tenant and queues the import process.</span></span> <span data-ttu-id="dddd2-117">Это средство может осуществляться с помощью управляемого кода (.NET) или как PowerShell использовать при написании скриптов с помощью новых интерфейсов API CSOM.</span><span class="sxs-lookup"><span data-stu-id="dddd2-117">This tool can be implemented using managed code (.NET) or as a PowerShell script using the new CSOM APIs.</span></span>
4. <span data-ttu-id="dddd2-118">Строка из БИЗНЕС-системы, или любой внешней системы, который является источником данных в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="dddd2-118">A Line of Business (LOB) system, or any external system, which is the source of the information in the JSON file.</span></span> <span data-ttu-id="dddd2-119">Это может быть сочетание данных из Active Directory и все внешние системы.</span><span class="sxs-lookup"><span data-stu-id="dddd2-119">This could also be a combination of data from Active Directory and any external system.</span></span> <span data-ttu-id="dddd2-120">Обратите внимание на то, что с точки зрения API бизнес-системы может быть SharePoint 2013 в локальной или 2016 фермы.</span><span class="sxs-lookup"><span data-stu-id="dddd2-120">Notice that from an API perspective, the LOB system could even be an on-premises SharePoint 2013 or 2016 farm.</span></span>
5. <span data-ttu-id="dddd2-121">Сообщение о поле server со стороны запущено задание таймера в SharePoint online которого выполняется поиск в очередь запросы на импорт и будет выполнять операцию импорта на основе вызовов API и сведений о в файле отмеченными JSON.</span><span class="sxs-lookup"><span data-stu-id="dddd2-121">An out of the box server side timer job running in SharePoint online which checks for queued import requests and will perform the actual import operation based on the API calls and the information within the provided JSON file.</span></span>
6. <span data-ttu-id="dddd2-122">Сведения о профилях пользователей расширенного доступен в профили пользователей и может использоваться для каких-либо вне поля или пользовательские функциональные возможности в SharePoint online.</span><span class="sxs-lookup"><span data-stu-id="dddd2-122">Extended user profile information is available within user profiles and can be used for any out of the box or custom functionality in SharePoint online.</span></span>

><span data-ttu-id="dddd2-123">**Примечание**: импорт работает только для свойств профиля пользователя которого **не** были задайте значение будет изменять в конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-123">**Note**: The import only works for user profile properties which have **not** been set to be editable by end users.</span></span> <span data-ttu-id="dddd2-124">Это запрет на переопределение все сведения, которые конечный пользователь уже обновлен процесс импорта профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-124">This is to prevent the user profile import process from overriding any information which an end user has already updated.</span></span> <span data-ttu-id="dddd2-125">Кроме того Импорт позволяет только настраиваемые свойства, которые не являются основных свойств active directory.</span><span class="sxs-lookup"><span data-stu-id="dddd2-125">Additionally, the import only allows custom properties that are not active directory core properties.</span></span> <span data-ttu-id="dddd2-126">Они должны быть синхронизированы для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dddd2-126">These must be synchronized to Azure Active Directory.</span></span> <span data-ttu-id="dddd2-127">Список этих основных свойств каталога представлен в таблице в представленном ниже разделе вопросы и ответы.</span><span class="sxs-lookup"><span data-stu-id="dddd2-127">For the list of these core directory properties, see the table listed in the FAQ section below.</span></span>

<span data-ttu-id="dddd2-128">Ниже приведен короткий видеоролик, демонстрирующий использование нового интерфейса API CSOM из обоих управляемого кода (.NET) и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dddd2-128">Below is a brief video that demonstrates using the new CSOM API from both managed code (.NET) and from PowerShell.</span></span> <span data-ttu-id="dddd2-129">Можно найти в примере кода используется, включая сценарий PowerShell в [Коллекции кодов PnP разработчиков Office](http://dev.office.com/patterns-and-practices-detail/7202).</span><span class="sxs-lookup"><span data-stu-id="dddd2-129">You can find the sample code used, including the sample PowerShell script, in the [Office Dev PnP Code Gallery](http://dev.office.com/patterns-and-practices-detail/7202).</span></span>

<iframe id="ytplayer" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/-X_2T0SRUBk?autoplay=0&origin=https://msdn.microsoft.com" frameborder="0"></iframe>

## <a name="import-file-format"></a><span data-ttu-id="dddd2-130">Формат файла импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-130">Import File Format</span></span>
<span data-ttu-id="dddd2-131"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="dddd2-131"></span></span>

<span data-ttu-id="dddd2-132">Процесс импорта использует файл JSON, содержащий свойства и их значения.</span><span class="sxs-lookup"><span data-stu-id="dddd2-132">The import process uses a JSON file containing the properties and their values.</span></span> <span data-ttu-id="dddd2-133">Ниже приведена структура ожидаемых, файл:</span><span class="sxs-lookup"><span data-stu-id="dddd2-133">Below is the expected structure of that file:</span></span>   

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

<span data-ttu-id="dddd2-134">Ниже — это простой пример файла в формате выше:</span><span class="sxs-lookup"><span data-stu-id="dddd2-134">Below is a simple example file using the format above:</span></span>

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

<span data-ttu-id="dddd2-135">В приведенном выше примере на основе разрешение идентификаторов `IdName` свойства и имеется два свойства, которые обновляются называется `City` и `Office`.</span><span class="sxs-lookup"><span data-stu-id="dddd2-135">In the example above, identity resolution is based on the `IdName` property and there are two properties which are being updated called `City` and `Office`.</span></span> <span data-ttu-id="dddd2-136">Файл содержит сведения о четыре различные учетные записи в рамках клиента.</span><span class="sxs-lookup"><span data-stu-id="dddd2-136">The file contains information for four different accounts within the tenant.</span></span> <span data-ttu-id="dddd2-137">Имена свойств, используемых в этом исходный файл не обязательно то же, что имена, используемые в службе SharePoint Online пользовательского профиля с момента сопоставления правильные свойства предоставляются в пределах нашего кода.</span><span class="sxs-lookup"><span data-stu-id="dddd2-137">Property names used in this source file are not necessarily the same as the names used within the SharePoint Online User Profile Service since we will provide correct property mapping within our code.</span></span> 

### <a name="source-data-file-restrictions"></a><span data-ttu-id="dddd2-138">Ограничения файлов источника данных</span><span class="sxs-lookup"><span data-stu-id="dddd2-138">Source Data File Restrictions</span></span>
<span data-ttu-id="dddd2-139">Существует несколько ограничений на отдельные исходные файлы данных.</span><span class="sxs-lookup"><span data-stu-id="dddd2-139">There are few restrictions on individual source data files:</span></span>
- <span data-ttu-id="dddd2-140">Максимальный размер файла: 2 ГБ</span><span class="sxs-lookup"><span data-stu-id="dddd2-140">Maximum file size: 2GB</span></span>
- <span data-ttu-id="dddd2-141">Максимальное число свойств: 500 000</span><span class="sxs-lookup"><span data-stu-id="dddd2-141">Maximum number of properties: 500,000</span></span>
- <span data-ttu-id="dddd2-142">Исходный файл необходимо загрузить же владельцу SharePoint Online, где запущен процесс</span><span class="sxs-lookup"><span data-stu-id="dddd2-142">The source file must be uploaded to the same SharePoint Online tenant where the process is started</span></span>


## <a name="user-profile-property-import-process"></a><span data-ttu-id="dddd2-143">Процесс импорта свойств профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="dddd2-143">User Profile Property Import Process</span></span>
<span data-ttu-id="dddd2-144"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="dddd2-144"></span></span>

<span data-ttu-id="dddd2-145">Ниже приведен полный процесс:</span><span class="sxs-lookup"><span data-stu-id="dddd2-145">Here’s the full process:</span></span>

1. <span data-ttu-id="dddd2-146">Создание и синхронизация пользователей в Office 365 для клиентов или Azure AD, связанная с ним</span><span class="sxs-lookup"><span data-stu-id="dddd2-146">Create or synchronize users in an Office 365 tenant or to the Azure AD associated to it</span></span>
     - <span data-ttu-id="dddd2-147">Пользователи синхронизируются с Azure AD, он будет синхронизировать типовой набор атрибутов в службу SharePoint Online пользовательского профиля.</span><span class="sxs-lookup"><span data-stu-id="dddd2-147">When users are synchronized to Azure AD, it will also synchronize a standardized set of attributes to the SharePoint Online User Profile Service.</span></span>
2. <span data-ttu-id="dddd2-148">Создать любые необходимые пользовательские свойства в рамках службы профилей пользователей</span><span class="sxs-lookup"><span data-stu-id="dddd2-148">Create any needed custom properties within the User Profile Service</span></span>
     - <span data-ttu-id="dddd2-149">Так как для создания настраиваемых свойств в службе профилей пользователей не удаленных интерфейсов API, это действие необходимо выполнить вручную для каждого из клиентов там, где необходимо настраиваемых свойств профиля (это действие необходимо выполнить один раз на клиента).</span><span class="sxs-lookup"><span data-stu-id="dddd2-149">Since there’s no remote APIs for creating custom properties in the User Profile Service, this step must be performed manually for each of the tenants where custom user profile properties are needed (this only needs to be done once per tenant).</span></span>
     - <span data-ttu-id="dddd2-150">Можно импортировать только свойства профиля пользователя недопустимые «редактировать конечные пользователи».</span><span class="sxs-lookup"><span data-stu-id="dddd2-150">Only user profile properties which are not “allowed to be edited by end users” can be imported.</span></span> <span data-ttu-id="dddd2-151">Попытка импорта JSON свойства объекта значение свойства профиля пользователя, помеченные как «редактируемого конечными пользователями» приведет к исключение при вызове CSOM API.</span><span class="sxs-lookup"><span data-stu-id="dddd2-151">Trying to import a JSON object property to a user profile property which is marked as “editable by end users” will result in an exception when the CSOM API is called.</span></span>
3. <span data-ttu-id="dddd2-152">Создание и отправка файла JSON для клиента Office 365</span><span class="sxs-lookup"><span data-stu-id="dddd2-152">Create and upload the JSON file to the Office 365 tenant</span></span>
     - <span data-ttu-id="dddd2-153">Необходимо отправить файл данных JSON, содержащий данные, которые следует обновить до клиента Office 365.</span><span class="sxs-lookup"><span data-stu-id="dddd2-153">You’ll need to upload the JSON data file containing the information to be updated to the Office 365 tenant.</span></span>
     - <span data-ttu-id="dddd2-154">В случае любого исключения во время импорта SharePoint будет предоставлять дополнительных сведений в журналах сохраняются в ту же библиотеку документов, где файл существовал в новую папку sub.</span><span class="sxs-lookup"><span data-stu-id="dddd2-154">In the case of any exception during the import process, SharePoint will provide additional logging information saved in the same document library where the file existed within a new sub folder.</span></span>
     - <span data-ttu-id="dddd2-155">Удаление файлов журнала и JSON файлы не происходит автоматически и несет ответственность за пользовательских решений с помощью API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="dddd2-155">Cleaning of the log files and JSON files are not done automatically and is the responsibility of the custom solution using the API.</span></span> <span data-ttu-id="dddd2-156">Жизненный цикл этих файлов необходимо учитывать в реализации.</span><span class="sxs-lookup"><span data-stu-id="dddd2-156">You should consider the life cycle of these files within your implementation.</span></span> <span data-ttu-id="dddd2-157">Эти файлы хранятся в библиотеках документов, их использование часть назначенный хранилища для семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="dddd2-157">These files are stored in document libraries so they will be consuming a portion of the assigned storage for the site collection.</span></span>
4. <span data-ttu-id="dddd2-158">Вызов массового UPA Импорт API для очереди задание импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-158">Call the bulk UPA Import API for queuing the import job</span></span>
     - <span data-ttu-id="dddd2-159">Использование CSOM API в очередь процесс импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-159">Use the CSOM API to queue the import process.</span></span> <span data-ttu-id="dddd2-160">Это можно сделать с помощью CSOM кода с помощью управляемого кода (.NET) или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dddd2-160">This can be achieved by executing CSOM code using either managed code (.NET) or PowerShell.</span></span>
     - <span data-ttu-id="dddd2-161">Метод в очередь задания требует сведения о сопоставлении свойств и расположение файла данных.</span><span class="sxs-lookup"><span data-stu-id="dddd2-161">The method to queue the job requires property mapping information and the location of the data file.</span></span> <span data-ttu-id="dddd2-162">Этот метод выполняется быстро, так как он просто ставит в очередь фактического процесса импорта, который будет выполняться более поздней версии в ходе процесса серверного компонента в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="dddd2-162">This method will quickly execute because it just queues the actual import process, which will later be executed as part of a back end process in SharePoint Online.</span></span>
5. <span data-ttu-id="dddd2-163">Проверка состояния задания импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-163">Check the status of the import job</span></span>
     - <span data-ttu-id="dddd2-164">Можно также использовать API удаленного для проверки состояния задания определенных импорта или все последние задания импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-164">You can also use remote APIs to check the status of a specific import job or all of the recent import jobs.</span></span> <span data-ttu-id="dddd2-165">Чтобы можно было проверить состояние выполнения определенного вызова, следует хранить идентификатор задания уникальный, полученных как возвращаемое значение, когда в очереди заданий.</span><span class="sxs-lookup"><span data-stu-id="dddd2-165">To be able to check the status of a specific call, you should store the unique job identifier received as a return value when the job is queued.</span></span>


## <a name="csom-api-for-the-bulk-import-process"></a><span data-ttu-id="dddd2-166">CSOM API для группового импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-166">CSOM API for the Bulk Import Process</span></span>
<span data-ttu-id="dddd2-167"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="dddd2-167"></span></span>

### <a name="queue-import"></a><span data-ttu-id="dddd2-168">Импорт очереди</span><span class="sxs-lookup"><span data-stu-id="dddd2-168">Queue Import</span></span>
<span data-ttu-id="dddd2-169">Можно поместить в очередь процесс импорта, вызвав [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) метод находится в [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) объекта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-169">You can queue the import process by calling the [`QueueImportProfileProperties`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.queueimportprofileproperties.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="dddd2-170">Это асинхронный вызов, в том, что она не загрузить исходных данных или выполняется импорт, просто добавляет рабочий элемент в очередь для этого более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="dddd2-170">This is an asynchronous call in that it doesn’t download the source data or perform the import, it simply adds a work item to the queue for doing this later.</span></span> <span data-ttu-id="dddd2-171">Ниже приведен полный подпись метода.</span><span class="sxs-lookup"><span data-stu-id="dddd2-171">Here’s the full signature of the method:</span></span>

```c#
public ClientResult<Guid> QueueImportProfileProperties(
                          ImportProfilePropertiesUserIdType idType, 
                          string sourceDataIdProperty, 
                          IDictionary<string, string> propertyMap, 
                          string sourceUri);
```

#### <a name="parameters"></a><span data-ttu-id="dddd2-172">Параметры</span><span class="sxs-lookup"><span data-stu-id="dddd2-172">Parameters</span></span>

<span data-ttu-id="dddd2-173">**Тип_идентификатора**:_[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span><span class="sxs-lookup"><span data-stu-id="dddd2-173">**idType**: _[`ImportProfilePropertiesUserIdType`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesuseridtype.aspx)_</span></span>

<span data-ttu-id="dddd2-174">Тип идентификатора для использования при поиске профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-174">The type of id to use when looking up the user profile.</span></span> <span data-ttu-id="dddd2-175">Возможные значения: `Email`, `CloudId`, и `PrincipalName`.</span><span class="sxs-lookup"><span data-stu-id="dddd2-175">Possible values are `Email`, `CloudId`, and `PrincipalName`.</span></span> <span data-ttu-id="dddd2-176">Обратите внимание, что независимо от типа, пользователь должен существовать в службе профилей пользователей для импорта для работы.</span><span class="sxs-lookup"><span data-stu-id="dddd2-176">Note that regardless of the type, the user must already exist in the User Profile Service for the import to work.</span></span> <span data-ttu-id="dddd2-177">Рекомендуется использовать `CloudId` для обеспечения уникальности.</span><span class="sxs-lookup"><span data-stu-id="dddd2-177">It’s recommended to use the `CloudId` to ensure uniqueness.</span></span>

<span data-ttu-id="dddd2-178">Сопоставление свойств между тип идентификатора и свойство Azure AD:</span><span class="sxs-lookup"><span data-stu-id="dddd2-178">Property mapping between ID Type and Azure AD property:</span></span>

<span data-ttu-id="dddd2-179">Идентификатор типа UPA массового импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-179">UPA Bulk Import ID Type</span></span> | <span data-ttu-id="dddd2-180">Атрибут Azure каталога</span><span class="sxs-lookup"><span data-stu-id="dddd2-180">Azure Directory Attribute</span></span>
--- | ---
<span data-ttu-id="dddd2-181">CloudId</span><span class="sxs-lookup"><span data-stu-id="dddd2-181">CloudId</span></span> | <span data-ttu-id="dddd2-182">ObjectID</span><span class="sxs-lookup"><span data-stu-id="dddd2-182">ObjectID</span></span>
<span data-ttu-id="dddd2-183">PrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-183">PrincipalName</span></span> | <span data-ttu-id="dddd2-184">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-184">userPrincipalName</span></span>
<span data-ttu-id="dddd2-185">Email</span><span class="sxs-lookup"><span data-stu-id="dddd2-185">Email</span></span> | <span data-ttu-id="dddd2-186">mail</span><span class="sxs-lookup"><span data-stu-id="dddd2-186">mail</span></span>

<span data-ttu-id="dddd2-187">**sourceDataIdProperty**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-187">**sourceDataIdProperty**: _`System.String`_</span></span>

<span data-ttu-id="dddd2-188">Имя свойства id в источнике данных.</span><span class="sxs-lookup"><span data-stu-id="dddd2-188">The name of the id property in the source data.</span></span> <span data-ttu-id="dddd2-189">Значение свойства из источника данных будет использоваться для поиска пользователя.</span><span class="sxs-lookup"><span data-stu-id="dddd2-189">The value of the property from the source data will be used to lookup the user.</span></span> <span data-ttu-id="dddd2-190">Свойства службы профилей пользователей, используемые для поиска зависит от значения `idType`.</span><span class="sxs-lookup"><span data-stu-id="dddd2-190">The User Profile Service property used for the lookup depends on the value of `idType`.</span></span>

<span data-ttu-id="dddd2-191">**propertyMap**:_`IDictionary<string, string>`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-191">**propertyMap**: _`IDictionary<string, string>`_</span></span>

<span data-ttu-id="dddd2-192">Сопоставление имени свойства источника имени свойства службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-192">A map from the source property name to the User Profile Service property name.</span></span> <span data-ttu-id="dddd2-193">Обратите внимание, что свойства службы профилей пользователей должен существовать.</span><span class="sxs-lookup"><span data-stu-id="dddd2-193">Note that the User Profile Service properties must already exist.</span></span> <span data-ttu-id="dddd2-194">Ключ — это имя свойства, используемые в исходном файле, значение — это имя свойства, используемые в службе профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-194">The key is the property name used in the source file, the value is the property name used in the User Profile Service.</span></span>

<span data-ttu-id="dddd2-195">**sourceUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-195">**sourceUri**: _`System.String`_</span></span>

<span data-ttu-id="dddd2-196">URI исходного файла данных для импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-196">The URI of the source data file to import.</span></span> <span data-ttu-id="dddd2-197">Файл не должен перемещен или удалить сразу, так как он не могут быть загружены в течение некоторого времени.</span><span class="sxs-lookup"><span data-stu-id="dddd2-197">The file should not be moved or deleted right away as it may not be downloaded for some time.</span></span>

#### <a name="return-value"></a><span data-ttu-id="dddd2-198">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dddd2-198">Return value</span></span>
<span data-ttu-id="dddd2-199">Guid, идентифицирующий задание импорта, который находится в очереди.</span><span class="sxs-lookup"><span data-stu-id="dddd2-199">A Guid that identifies the import job that has been queued.</span></span>

#### <a name="example"></a><span data-ttu-id="dddd2-200">Пример</span><span class="sxs-lookup"><span data-stu-id="dddd2-200">Example</span></span>
<span data-ttu-id="dddd2-201">Ниже приведен пример с помощью C#, необходимых начать процесс, с помощью выше пример входного файла.</span><span class="sxs-lookup"><span data-stu-id="dddd2-201">Below is an example using C# of how to start the process using the sample input file above:</span></span>

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

### <a name="check-the-status-of-an-import-job"></a><span data-ttu-id="dddd2-202">Проверка состояния задания импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-202">Check the Status of an Import Job</span></span>
<span data-ttu-id="dddd2-203">Вы также можете проверить состояние задания импорта службы профилей пользователей с помощью новых интерфейсов API CSOM.</span><span class="sxs-lookup"><span data-stu-id="dddd2-203">You can also check the status of the User Profile Service import jobs by using the new CSOM APIs.</span></span> <span data-ttu-id="dddd2-204">Существует два метода новой базы данных для объекта клиента.</span><span class="sxs-lookup"><span data-stu-id="dddd2-204">There are two new methods for this in the Tenant object.</span></span>

<span data-ttu-id="dddd2-205">Можно проверить состояние задания отдельных импорта с помощью [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) метод находится в [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) объекта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-205">You can check status of an individual import job by using the [`GetImportProfilePropertyJob`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjob.aspx) method located in the [`Office365Tenant`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="dddd2-206">Необходимо будет иметь уникальный идентификатор определенного задания, представленные в качестве параметра этого метода импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-206">You will need to have the unique identifier of a specific import job provided as a parameter to this method.</span></span> <span data-ttu-id="dddd2-207">Ниже приведен полный подпись метода.</span><span class="sxs-lookup"><span data-stu-id="dddd2-207">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobInfo GetImportProfilePropertyJob(Guid jobId);
```

#### <a name="parameters"></a><span data-ttu-id="dddd2-208">Параметры</span><span class="sxs-lookup"><span data-stu-id="dddd2-208">Parameters</span></span>
<span data-ttu-id="dddd2-209">**jobID**:_`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-209">**jobID**: _`System.Guid`_</span></span>

<span data-ttu-id="dddd2-210">Идентификатор задания, для которого необходимо получить сведения о состоянии высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="dddd2-210">The id of the job for which to get the high-level status.</span></span>

#### <a name="return-value"></a><span data-ttu-id="dddd2-211">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dddd2-211">Return value</span></span>

<span data-ttu-id="dddd2-212">[`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Объект с высокого уровня сведений о указанного задания.</span><span class="sxs-lookup"><span data-stu-id="dddd2-212">An [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object with high level status information about the specified job.</span></span>

#### <a name="example"></a><span data-ttu-id="dddd2-213">Пример</span><span class="sxs-lookup"><span data-stu-id="dddd2-213">Example</span></span>
<span data-ttu-id="dddd2-214">Ниже пример использует C# для получение сведений о состоянии с помощью сохраненных идентификатор задания определенных импорта:</span><span class="sxs-lookup"><span data-stu-id="dddd2-214">Below is an example using C# of retrieving the status of a specific import job using a stored identifier:</span></span>

```c#
// Check the status of a specific request based on the job id received when we queued the job
Office365Tenant tenant = new Office365Tenant(ctx);
var job = tenant.GetImportProfilePropertyJob(workItemId);
ctx.Load(job);
ctx.ExecuteQuery();
```

<span data-ttu-id="dddd2-215">Можно проверить состояние всех заданий импорта с помощью [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) метод находится в объекте [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) .</span><span class="sxs-lookup"><span data-stu-id="dddd2-215">You can check the status of all import jobs by using the [`GetImportProfilePropertyJobs`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.getimportprofilepropertyjobs.aspx) method located in the [Office365Tenant](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.office365tenant.aspx) object.</span></span> <span data-ttu-id="dddd2-216">Ниже приведен полный подпись метода.</span><span class="sxs-lookup"><span data-stu-id="dddd2-216">Here’s the full signature of the method:</span></span>

```c#
public ImportProfilePropertiesJobStatusCollection GetImportProfilePropertyJobs(); 
```

#### <a name="return-value"></a><span data-ttu-id="dddd2-217">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="dddd2-217">Return value</span></span>
<span data-ttu-id="dddd2-218">[`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) Объект, который представляет собой коллекцию из [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) объекты с высокого уровня состояния сведения о каждом из заданий.</span><span class="sxs-lookup"><span data-stu-id="dddd2-218">An [`ImportProfilePropertiesJobStatusCollection`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstatuscollection.aspx) object which is a collection of [`ImportProfilePropertiesJobStatus`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) objects with high level status information about each of the jobs.</span></span>

#### <a name="example"></a><span data-ttu-id="dddd2-219">Пример</span><span class="sxs-lookup"><span data-stu-id="dddd2-219">Example</span></span>
<span data-ttu-id="dddd2-220">Ниже пример использует C# для получения состояния всех заданий импорта, в настоящее время сохранены в клиентов.</span><span class="sxs-lookup"><span data-stu-id="dddd2-220">Below is an example using C# of getting the status of all import jobs currently saved in the tenant.</span></span> <span data-ttu-id="dddd2-221">Это может быть уже обработан или в очереди заданий:</span><span class="sxs-lookup"><span data-stu-id="dddd2-221">These could be already processed or queued jobs:</span></span>

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

<span data-ttu-id="dddd2-222">[`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) Объект, возвращенный с сведения о состоянии импорта имеет следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="dddd2-222">An [`ImportProfilePropertiesJobInfo`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobinfo.aspx) object returned with the import status information has the following properties.</span></span> 

<span data-ttu-id="dddd2-223">**JobId**:_`System.Guid`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-223">**JobId**: _`System.Guid`_</span></span>

<span data-ttu-id="dddd2-224">Идентификатор задания импорта</span><span class="sxs-lookup"><span data-stu-id="dddd2-224">The Id of the import job</span></span>

<span data-ttu-id="dddd2-225">**Состояние**:_[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span><span class="sxs-lookup"><span data-stu-id="dddd2-225">**State**: _[`ImportProfilePropertiesJobState`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjobstate.aspx)_</span></span>

<span data-ttu-id="dddd2-226">Перечисление с помощью следующих значений:</span><span class="sxs-lookup"><span data-stu-id="dddd2-226">An enum with following values:</span></span>
- <span data-ttu-id="dddd2-227">`Unknown`-Мы не может определить состояние задания</span><span class="sxs-lookup"><span data-stu-id="dddd2-227">`Unknown` - We cannot determine the state of the job</span></span>
- <span data-ttu-id="dddd2-228">`Submitted`-Задания отправки в систему</span><span class="sxs-lookup"><span data-stu-id="dddd2-228">`Submitted` - The job has been submitted to the system</span></span>
- <span data-ttu-id="dddd2-229">`Processing`-Обрабатывается задание</span><span class="sxs-lookup"><span data-stu-id="dddd2-229">`Processing` - The job is being processed</span></span>
- <span data-ttu-id="dddd2-230">`Queued`-Заданием прошел проверку и в очередь для импорта для однозначного соответствия</span><span class="sxs-lookup"><span data-stu-id="dddd2-230">`Queued` - The job has passed validation and queued for import to UPA</span></span>
- <span data-ttu-id="dddd2-231">`Succeeded`-Задание завершена без ошибок</span><span class="sxs-lookup"><span data-stu-id="dddd2-231">`Succeeded` - The job completed with no error</span></span>
- <span data-ttu-id="dddd2-232">`Error`-Задание завершено с ошибкой</span><span class="sxs-lookup"><span data-stu-id="dddd2-232">`Error` - The job completed with error</span></span>

<span data-ttu-id="dddd2-233">**SourceUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-233">**SourceUri**: _`System.String`_</span></span>

<span data-ttu-id="dddd2-234">URI файл источника данных</span><span class="sxs-lookup"><span data-stu-id="dddd2-234">The URI to the data source file</span></span>

<span data-ttu-id="dddd2-235">**Ошибка**:_[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span><span class="sxs-lookup"><span data-stu-id="dddd2-235">**Error**: _[`ImportProfilePropertiesJobError`](https://msdn.microsoft.com/en-us/library/office/microsoft.online.sharepoint.tenantmanagement.importprofilepropertiesjoberror.aspx)_</span></span>

<span data-ttu-id="dddd2-236">Перечисление, представляющее возможные ошибки:</span><span class="sxs-lookup"><span data-stu-id="dddd2-236">An enum representing the possible error:</span></span>
- <span data-ttu-id="dddd2-237">`NoError`-Ошибка не найден</span><span class="sxs-lookup"><span data-stu-id="dddd2-237">`NoError` - No error found</span></span>
- <span data-ttu-id="dddd2-238">`InternalError`-Ошибки, возникающие при сбоя в службе</span><span class="sxs-lookup"><span data-stu-id="dddd2-238">`InternalError` - The error was caused by a failure in the service</span></span>
- <span data-ttu-id="dddd2-239">`DataFileNotExist`-Не удалось найти файл источника данных</span><span class="sxs-lookup"><span data-stu-id="dddd2-239">`DataFileNotExist` - The data source file could not be found</span></span>
- <span data-ttu-id="dddd2-240">`DataFileNotInTenant`-Файл источника данных принадлежит же клиента</span><span class="sxs-lookup"><span data-stu-id="dddd2-240">`DataFileNotInTenant` - The data source file did not belong to the same tenant</span></span>
- <span data-ttu-id="dddd2-241">`DataFileTooBig`— Размер файла данных слишком велико</span><span class="sxs-lookup"><span data-stu-id="dddd2-241">`DataFileTooBig` - The size of the data file was too big</span></span>
- <span data-ttu-id="dddd2-242">`InvalidDataFile`-Файл источника данных не прошли проверку (может быть Дополнительные сведения в файле журнала)</span><span class="sxs-lookup"><span data-stu-id="dddd2-242">`InvalidDataFile` - The data source file did not pass validation (There may be additional details in the log file)</span></span>
- <span data-ttu-id="dddd2-243">`ImportCompleteWithError`-Импорт данных, но произошла ошибка возникала</span><span class="sxs-lookup"><span data-stu-id="dddd2-243">`ImportCompleteWithError` - The data has been imported, but there was an error encountered</span></span>

<span data-ttu-id="dddd2-244">**Сообщение об ошибке**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-244">**ErrorMessage**: _`System.String`_</span></span>

<span data-ttu-id="dddd2-245">Сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="dddd2-245">The error message</span></span>

<span data-ttu-id="dddd2-246">**LogFileUri**:_`System.String`_</span><span class="sxs-lookup"><span data-stu-id="dddd2-246">**LogFileUri**: _`System.String`_</span></span>

<span data-ttu-id="dddd2-247">Uri в папку, где были записаны журналы</span><span class="sxs-lookup"><span data-stu-id="dddd2-247">The Uri to the folder where the logs have been written</span></span>

## <a name="calling-the-import-api-from-powershell"></a><span data-ttu-id="dddd2-248">Вызов API импорта из PowerShell</span><span class="sxs-lookup"><span data-stu-id="dddd2-248">Calling the Import API from PowerShell</span></span>
<span data-ttu-id="dddd2-249"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="dddd2-249"></span></span>

<span data-ttu-id="dddd2-250">Вы можете воспользоваться преимуществами API импорта массового службы профилей пользователей с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dddd2-250">You can take advantage of the User Profile Service bulk import API with PowerShell.</span></span> <span data-ttu-id="dddd2-251">Это означает, что вы будете использовать в коде CSOM непосредственно в сценарий PowerShell, используя необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="dddd2-251">This means that you’ll use the CSOM code directly in a PowerShell script using the necessary parameters.</span></span> <span data-ttu-id="dddd2-252">Для этого необходимо, что обновленные распространяемый пакет CSOM был установлен на компьютере, где выполняется скрипт.</span><span class="sxs-lookup"><span data-stu-id="dddd2-252">This requires that the updated CSOM redistributable package has been installed on the computer where the script is executed.</span></span>

<span data-ttu-id="dddd2-253">С помощью PowerShell, нет необходимости для компиляции кода в Visual Studio, которые могут быть более подходящим модели для некоторых клиентов.</span><span class="sxs-lookup"><span data-stu-id="dddd2-253">By using PowerShell, you do not need to compile your code within Visual Studio, which may be a more suitable model for some customers.</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="dddd2-254">Образец сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="dddd2-254">Sample PowerShell Script</span></span>
<span data-ttu-id="dddd2-255">Ниже приведен образец сценария PowerShell, который выполняет те же действия, как приведенный выше код:</span><span class="sxs-lookup"><span data-stu-id="dddd2-255">Below is a sample PowerShell script which performs the same operations as the code above:</span></span> 

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

## <a name="handling-exceptions"></a><span data-ttu-id="dddd2-256">Обработка исключений</span><span class="sxs-lookup"><span data-stu-id="dddd2-256">Handling Exceptions</span></span>
<span data-ttu-id="dddd2-257"><a name="sectionSection5"></a> Существует два уровня проверки при использовании этот интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="dddd2-257"><a name="sectionSection5"> </a> There are two levels of validation when this API is used.</span></span> <span data-ttu-id="dddd2-258">При запуске процесса импорта с помощью CSOM будет начальной уровень проверки указанные значения.</span><span class="sxs-lookup"><span data-stu-id="dddd2-258">When you queue the import process with CSOM there will be an initial level of validation of the provided values.</span></span> <span data-ttu-id="dddd2-259">Этот компонент включает подтверждения существование отмеченными сопоставление свойств в службе профилей пользователей и, что эти свойства недоступны для редактирования конечным пользователем.</span><span class="sxs-lookup"><span data-stu-id="dddd2-259">This includes confirmation that the provided mapping properties exist in the User Profile Service and that these properties are not editable by the end user.</span></span> <span data-ttu-id="dddd2-260">При вызове API очереди применяется только начальной уровень проверки и ее реального выполнения задания импорта выполняется последний проверка предоставлена информация.</span><span class="sxs-lookup"><span data-stu-id="dddd2-260">When the queue API is called, only an initial level of validation is applied and final validation of the provided information is performed when the import job is actually executed.</span></span>

<span data-ttu-id="dddd2-261">Если во время выполнения задания импорта сведения о любых исключениях, в ту же библиотеку документов, где был задан Импорт файла создается файл ведения журнала с дополнительными сведениями.</span><span class="sxs-lookup"><span data-stu-id="dddd2-261">If there are any exceptions during the actual import job execution, a logging file with additional details is generated in the same document library where the import file was located.</span></span> <span data-ttu-id="dddd2-262">Будут сохранены файлы журналов для задания определенных импорта sub папки с именами с помощью уникальный идентификатор задания определенных импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-262">Log files for specific import jobs are saved to sub folders named using the unique identifier of the specific import job.</span></span>

<span data-ttu-id="dddd2-263">Ниже приведен пример результаты выполнения задания импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-263">Below is an example of the results of running an import job.</span></span> <span data-ttu-id="dddd2-264">На рисунке ниже можно увидеть две вложенные папки для двух различных выполнений, создаваемых в библиотеке документов, где хранится файл импорта:</span><span class="sxs-lookup"><span data-stu-id="dddd2-264">In the picture below, you can see two sub folders for two different executions created in the document library where the import file is stored:</span></span>

![Задание исключение вложенные папки](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-folders.png)

<span data-ttu-id="dddd2-266">Файл журнала сохраняется в папке sub и для подробного анализа, который можно загрузить из Office 365:</span><span class="sxs-lookup"><span data-stu-id="dddd2-266">The actual log file is saved in the sub folder and you can download that from Office 365 for detailed analysis:</span></span>

![Задание файла журнала исключений](media/bulkuserprofileupdateapi/UserProfileBulkAPIProcess-LogFile.png)

### <a name="common-exceptions"></a><span data-ttu-id="dddd2-268">Общие исключения</span><span class="sxs-lookup"><span data-stu-id="dddd2-268">Common Exceptions</span></span>

<span data-ttu-id="dddd2-269">Следующая таблица содержит типичные исключения, которые могут возникнуть при запуске с помощью API массового службы профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-269">Following table contains typical exceptions which you could encounter when you start using the User Profile Service bulk API.</span></span>

<span data-ttu-id="dddd2-270">Пример исключений</span><span class="sxs-lookup"><span data-stu-id="dddd2-270">Example Exception</span></span> | <span data-ttu-id="dddd2-271">Сведения</span><span class="sxs-lookup"><span data-stu-id="dddd2-271">Details</span></span>
--- | ---
<span data-ttu-id="dddd2-272">_Имена свойств [AboutMe] становятся недоступны для изменения пользователем._</span><span class="sxs-lookup"><span data-stu-id="dddd2-272">_Property Names [AboutMe] are editable by user._</span></span> | <span data-ttu-id="dddd2-273">Это может быть создано с помощью CSOM API, при вызове `ExecuteQuery` метод при отправке задания к клиенту.</span><span class="sxs-lookup"><span data-stu-id="dddd2-273">This would be thrown by the CSOM API when you call the `ExecuteQuery` method when submitting the job to your tenant.</span></span> <span data-ttu-id="dddd2-274">API-Интерфейс будет проверять, что все свойства, которые в настоящий момент сопоставленные не редактируемое пользователем.</span><span class="sxs-lookup"><span data-stu-id="dddd2-274">The API will validate that all properties currently being mapped are NOT user editable.</span></span> <span data-ttu-id="dddd2-275">Исключение будет отметить свойство, которое не может использоваться.</span><span class="sxs-lookup"><span data-stu-id="dddd2-275">The exception will point out the property which cannot be used.</span></span> <span data-ttu-id="dddd2-276">В этом примере мы попытались сопоставление свойства JSON для `AboutMe` свойство в свойствах службы профилей пользователей, но это не допускается с момента `AboutMe` — это редактируемых свойств пользователя.</span><span class="sxs-lookup"><span data-stu-id="dddd2-276">In this example, we have tried to map a JSON property to the `AboutMe` property in the User Profile Service properties, but this is not allowed since `AboutMe` is a user editable property.</span></span>
<span data-ttu-id="dddd2-277">_InvalidProperty - vesaj@contoso.com свойство «AboutMe» не связан с любого свойства в приложение профилей пользователей._</span><span class="sxs-lookup"><span data-stu-id="dddd2-277">_InvalidProperty - vesaj@contoso.com Property 'AboutMe' is not mapped to any property in the user profile application._</span></span> | <span data-ttu-id="dddd2-278">Файл данных JSON содержатся свойства, которое не сопоставлен свойства службы профилей пользователей в SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="dddd2-278">The JSON data file contained a property which has not been mapped to the User Profile Service property in SharePoint Online.</span></span> <span data-ttu-id="dddd2-279">Это означает, что файл источника данных содержит свойства, для которых не заданы сопоставления в `propertyMap` параметр.</span><span class="sxs-lookup"><span data-stu-id="dddd2-279">This means that the source data file contains properties for which you have not provided a mapping in the `propertyMap` parameter.</span></span> <span data-ttu-id="dddd2-280">Необходимо будет иметь определения сопоставления для каждого свойства объекта данных JSON.</span><span class="sxs-lookup"><span data-stu-id="dddd2-280">You will need to have a mapping definition for each of the properties in the JSON data object.</span></span>
<span data-ttu-id="dddd2-281">_MissingIdentity - идентификатор отсутствует для объекта пользователя_</span><span class="sxs-lookup"><span data-stu-id="dddd2-281">_MissingIdentity - The identity is missing for the user object_</span></span> | <span data-ttu-id="dddd2-282">Свойство identity не найден в объекте пользователя.</span><span class="sxs-lookup"><span data-stu-id="dddd2-282">The identity property could not be found in the user object.</span></span> <span data-ttu-id="dddd2-283">Возможная причина в том, что `sourceDataIdProperty` неправильно имеет атрибут `QueueImportProfileProperties` метод.</span><span class="sxs-lookup"><span data-stu-id="dddd2-283">The most likely cause is that the `sourceDataIdProperty` attribute is wrongly set for the `QueueImportProfileProperties` method.</span></span> <span data-ttu-id="dddd2-284">Убедитесь, имеют свойство right в исходном файле JSON и код или сценарий является назначение соответствующим образом этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="dddd2-284">Ensure that you have the right property in the JSON source file and that your code/script is assigning this attribute accordingly.</span></span>
<span data-ttu-id="dddd2-285">_Не удалось разрешить IdentityNotResolvable unknown@contoso.com удостоверения пользователя_</span><span class="sxs-lookup"><span data-stu-id="dddd2-285">_IdentityNotResolvable unknown@contoso.com User identity cannot be resolved_</span></span> | <span data-ttu-id="dddd2-286">Файл данных содержится удостоверение, которое не удалось разрешить или не существует в службе профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-286">The data file contained an identity, which could not be resolved or was not present in the User Profile Service.</span></span> <span data-ttu-id="dddd2-287">В этом случае профилей пользователей с помощью электронной почты из _unknown@contoso.com_ не удается найти в службе профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-287">In this case, the user profile with email of _unknown@contoso.com_ could not be located in the User Profile Service.</span></span>
<span data-ttu-id="dddd2-288">_DataFileNotJson - JsonToken EndObject не является допустимым для закрытия JsonType массива. Путь «значение», строка 8, поместите 10._</span><span class="sxs-lookup"><span data-stu-id="dddd2-288">_DataFileNotJson - JsonToken EndObject is not valid for closing JsonType Array. Path 'value', line 8, position 10._</span></span> | <span data-ttu-id="dddd2-289">В качестве формата формат файла импорта, не является допустимым JSON и не соответствует ожидаемому формату.</span><span class="sxs-lookup"><span data-stu-id="dddd2-289">Your import file format is not valid JSON and does not match the expected format.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="dddd2-290">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="dddd2-290">Frequently Asked Questions</span></span>
<span data-ttu-id="dddd2-291"><a name="sectionSection6"> </a></span><span class="sxs-lookup"><span data-stu-id="dddd2-291"></span></span>

<span data-ttu-id="dddd2-292">**Может выполнять код, использующий разрешения только для приложения только/надстройки**</span><span class="sxs-lookup"><span data-stu-id="dddd2-292">**Can I execute the code using app-only/add-in only permissions?**</span></span>

<span data-ttu-id="dddd2-293">Да, необходимо зарегистрировать идентификатор клиента и секрет должны иметь возможность выполнять интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="dddd2-293">Yes, you’ll need to register the client id and secret to be able to execute the APIs.</span></span> <span data-ttu-id="dddd2-294">Так как фактический импорт файла не синхронно с идентификатором вызывающего абонента, это работает без ошибок.</span><span class="sxs-lookup"><span data-stu-id="dddd2-294">Since the actual import of the file does not occur synchronously with the identity of the caller, this works without any issues.</span></span>

<span data-ttu-id="dddd2-295">**Этот интерфейс API обновление свойств в службе профилей пользователей, но как я создаст этих свойств в клиента?**</span><span class="sxs-lookup"><span data-stu-id="dddd2-295">**This API is updating properties in the User Profile Service, but how would I create those properties in the tenant?**</span></span>

<span data-ttu-id="dddd2-296">Нет удаленного интерфейса API для создания настраиваемого пользовательского свойства профиля программным способом, поэтому это вручную операция, которой следует выполнить один раз в заданном клиента.</span><span class="sxs-lookup"><span data-stu-id="dddd2-296">There’s no remote API to create custom user profile properties programmatically, so this is manual operation which needs to be completed once per given tenant.</span></span> <span data-ttu-id="dddd2-297">Можно найти [в этой статье](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) представлены инструкции по созданию этих настраиваемых свойств.</span><span class="sxs-lookup"><span data-stu-id="dddd2-297">You can refer to [this article](https://support.office.com/en-us/article/Add-and-edit-user-profile-properties-85091402-737F-4BB9-99A7-BC5F194502A8) for instructions on how to create these custom properties.</span></span>

<span data-ttu-id="dddd2-298">**Эта возможность доступна в локальном SharePoint?**</span><span class="sxs-lookup"><span data-stu-id="dddd2-298">**Is this capability available in on-premises SharePoint?**</span></span>

<span data-ttu-id="dddd2-299">К сожалению эта возможность в настоящее время используется только для SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="dddd2-299">Unfortunately, this capability is currently only for SharePoint Online.</span></span> <span data-ttu-id="dddd2-300">В локальном SharePoint эта возможность будет полезен, но не как критические с момента его можно изменить сопоставление атрибутов в приложении-службе профилей пользователей в локальной.</span><span class="sxs-lookup"><span data-stu-id="dddd2-300">In on-premises SharePoint this capability would be useful but not as critical since you can modify the attribute mapping in the on-premises User Profile Service Application.</span></span> <span data-ttu-id="dddd2-301">Также можно воспользоваться преимуществами Импорт атрибутов профиля пользователя, с помощью службы Business Connectivity (BCS) в SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="dddd2-301">You can also take advantage of importing user profile attributes using the Business Connectivity Service (BCS) in SharePoint 2013.</span></span> <span data-ttu-id="dddd2-302">Тем не менее этот параметр недоступен в 2016 SharePoint, которая означает, что SharePoint 2016 только параметр в настоящее время для реализации настроек, которые воспользоваться преимуществами пользователя веб-службы профилей.</span><span class="sxs-lookup"><span data-stu-id="dddd2-302">However, this option is not available in SharePoint 2016, which means that for SharePoint 2016 the only option currently is to implement customizations which take advantage of the user profile web services.</span></span>

<span data-ttu-id="dddd2-303">**Может использовать этот интерфейс API для синхронизации значений свойств профиля пользователя из личных SharePoint 2013 в локальной или 2016 farm(s) в SharePoint Online?**</span><span class="sxs-lookup"><span data-stu-id="dddd2-303">**Could I use this API for synchronizing user profile property values from my on-premises SharePoint 2013 or 2016 farm(s) to SharePoint Online?**</span></span>
<span data-ttu-id="dddd2-304">Да, локального развертывания SharePoint можно использовать так же, как и любой другой системе источника.</span><span class="sxs-lookup"><span data-stu-id="dddd2-304">Yes, on-premises SharePoint can be used just like any other source system.</span></span> <span data-ttu-id="dddd2-305">Необходимо экспортировать значения профиля пользователя из локального SharePoint в формате JSON и затем процесс будет точно совпадает с Импорт значения из другой системе.</span><span class="sxs-lookup"><span data-stu-id="dddd2-305">You'll need to export the user profile values from your on-premises SharePoint to the JSON file format and then the process would be exactly the same as importing values from any other system.</span></span>

<span data-ttu-id="dddd2-306">**Можно импортировать на основе, строка многозначного свойства**</span><span class="sxs-lookup"><span data-stu-id="dddd2-306">**Can I import string based, multi-value properties?**</span></span>
<span data-ttu-id="dddd2-307">Нет, это не поддерживается в настоящее время этот интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="dddd2-307">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="dddd2-308">**Какие разрешения необходимы для выполнения этой API??**</span><span class="sxs-lookup"><span data-stu-id="dddd2-308">**What permissions are required for executing this API??**</span></span>
<span data-ttu-id="dddd2-309">Необходимо иметь разрешения глобального администратора в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="dddd2-309">You will need to have Global Admin permissions currently.</span></span> <span data-ttu-id="dddd2-310">Недостаточно администрирования SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dddd2-310">SharePoint Admin is not sufficient.</span></span>

<span data-ttu-id="dddd2-311">**Можно импортировать на основе таксономии**</span><span class="sxs-lookup"><span data-stu-id="dddd2-311">**Can I import taxonomy based properties?**</span></span>
<span data-ttu-id="dddd2-312">Нет, это не поддерживается в настоящее время этот интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="dddd2-312">No, this is not currently supported with this API.</span></span>

<span data-ttu-id="dddd2-313">**Что делать, если я определить сопоставление в коде, который не используется или настроены параметры в файле JSON, не отнесенные?**</span><span class="sxs-lookup"><span data-stu-id="dddd2-313">**What if I define a mapping in the code which is not used or have properties in the JSON file which are not mapped?**</span></span>
<span data-ttu-id="dddd2-314">Если код или сценарий определяет сопоставление, который не используется или файл данных не содержит свойства для этого сопоставления, выполнение продолжается без все исключения и импорт будет применяться на основании сопоставленных свойств.</span><span class="sxs-lookup"><span data-stu-id="dddd2-314">If your code/script defines a mapping which is not used or the data file does not contain properties for that mapping, execution will continue without any exceptions and the import will be applied based on the mapped properties.</span></span> <span data-ttu-id="dddd2-315">Если, тем не менее, свойство в файле JSON, который не связан, процесс импорта будет отменена, и сведения об исключении будет предоставляться в файле журнала для выполнения определенного задания.</span><span class="sxs-lookup"><span data-stu-id="dddd2-315">If you, however, have a property in the JSON file which is not mapped, the import process will be aborted and exception details will be provided in the log file for the specific job execution.</span></span>

<span data-ttu-id="dddd2-316">**Что делать, если я необходима для обновления настраиваемых свойств, выходящим за пределы ограничения размера этот интерфейс API массового (то есть > файл 2 ГБ или > 500 000 свойств)?**</span><span class="sxs-lookup"><span data-stu-id="dddd2-316">**What if I have a need to update custom properties that are beyond the size limitations of this bulk API (i.e. >2 GB file or >500,000 properties)?**</span></span>
<span data-ttu-id="dddd2-317">Необходимо пакетных заданий соответствующим образом, запуск нескольких заданий в последовательности (то есть завершения одно задание за раз с максимальное ограничение на этот интерфейс API).</span><span class="sxs-lookup"><span data-stu-id="dddd2-317">You would need to batch your jobs accordingly by triggering multiple jobs in sequence (i.e. finishing one job at a time with the maximum limit on this API).</span></span> <span data-ttu-id="dddd2-318">Следует ожидать эти imports высокой пропускной способностью будет уйти много времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="dddd2-318">You should expect these high bandwidth imports will take a long time to complete.</span></span> <span data-ttu-id="dddd2-319">Кроме того следует оптимизировать задания импорта только для дельта изменения пользовательских свойств профилей, а не полный набор значений в все задания импорта.</span><span class="sxs-lookup"><span data-stu-id="dddd2-319">Also, you should optimize the import jobs only for delta changes in custom profile properties rather than importing a full set of values in all jobs.</span></span>

<span data-ttu-id="dddd2-320">**Какие атрибуты Azure Active Directory выполняется синхронизация были вынуждены SharePoint Online профиля пользователя по умолчанию?**</span><span class="sxs-lookup"><span data-stu-id="dddd2-320">**Which Azure Active Directory attributes are being sync’d to SharePoint Online user profile by default?**</span></span>
<span data-ttu-id="dddd2-321">Обратитесь к таблице ниже официальная список синхронизированных атрибуты и их сопоставление между Azure Active Directory и службы Online профилей пользователей SharePoint.</span><span class="sxs-lookup"><span data-stu-id="dddd2-321">See the following table for the official list of synchronized attributes and their mapping between Azure Active Directory and the SharePoint Online User Profile Service.</span></span>

<span data-ttu-id="dddd2-322">Атрибут Azure каталога</span><span class="sxs-lookup"><span data-stu-id="dddd2-322">Azure Directory Attribute</span></span>  | <span data-ttu-id="dddd2-323">Свойство SharePoint Online профиля</span><span class="sxs-lookup"><span data-stu-id="dddd2-323">SharePoint Online Profile Property</span></span>
---------|----------
<span data-ttu-id="dddd2-324">ObjectSid</span><span class="sxs-lookup"><span data-stu-id="dddd2-324">ObjectSid</span></span> | <span data-ttu-id="dddd2-325">SPS SavedSID</span><span class="sxs-lookup"><span data-stu-id="dddd2-325">SPS-SavedSID</span></span>
<span data-ttu-id="dddd2-326">msonline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-326">msonline-UserPrincipalName</span></span> | <span data-ttu-id="dddd2-327">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="dddd2-327">UserName</span></span>
<span data-ttu-id="dddd2-328">msonline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-328">msonline-UserPrincipalName</span></span> | <span data-ttu-id="dddd2-329">Имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="dddd2-329">AccountName</span></span>
<span data-ttu-id="dddd2-330">msonline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-330">msonline-UserPrincipalName</span></span> | <span data-ttu-id="dddd2-331">SPS ClaimID</span><span class="sxs-lookup"><span data-stu-id="dddd2-331">SPS-ClaimID</span></span>
<span data-ttu-id="dddd2-332">msonline UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-332">msonline-UserPrincipalName</span></span> | <span data-ttu-id="dddd2-333">SPS UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="dddd2-333">SPS-UserPrincipalName</span></span>
<span data-ttu-id="dddd2-334">GivenName</span><span class="sxs-lookup"><span data-stu-id="dddd2-334">GivenName</span></span> | <span data-ttu-id="dddd2-335">FirstName</span><span class="sxs-lookup"><span data-stu-id="dddd2-335">FirstName</span></span>
<span data-ttu-id="dddd2-336">Sn</span><span class="sxs-lookup"><span data-stu-id="dddd2-336">sn</span></span> | <span data-ttu-id="dddd2-337">Фамилия</span><span class="sxs-lookup"><span data-stu-id="dddd2-337">LastName</span></span>
<span data-ttu-id="dddd2-338">Руководитель</span><span class="sxs-lookup"><span data-stu-id="dddd2-338">Manager</span></span> | <span data-ttu-id="dddd2-339">Руководитель</span><span class="sxs-lookup"><span data-stu-id="dddd2-339">Manager</span></span>
<span data-ttu-id="dddd2-340">Отображаемое имя</span><span class="sxs-lookup"><span data-stu-id="dddd2-340">DisplayName</span></span> | <span data-ttu-id="dddd2-341">PreferredName</span><span class="sxs-lookup"><span data-stu-id="dddd2-341">PreferredName</span></span>
<span data-ttu-id="dddd2-342">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="dddd2-342">telephoneNumber</span></span> | <span data-ttu-id="dddd2-343">WorkPhone</span><span class="sxs-lookup"><span data-stu-id="dddd2-343">WorkPhone</span></span>
<span data-ttu-id="dddd2-344">proxyAddresses.</span><span class="sxs-lookup"><span data-stu-id="dddd2-344">proxyAddresses</span></span> | <span data-ttu-id="dddd2-345">WorkEmail</span><span class="sxs-lookup"><span data-stu-id="dddd2-345">WorkEmail</span></span>
<span data-ttu-id="dddd2-346">proxyAddresses.</span><span class="sxs-lookup"><span data-stu-id="dddd2-346">proxyAddresses</span></span> | <span data-ttu-id="dddd2-347">SPS SIPAddress</span><span class="sxs-lookup"><span data-stu-id="dddd2-347">SPS-SIPAddress</span></span>
<span data-ttu-id="dddd2-348">PhysicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="dddd2-348">PhysicalDeliveryOfficeName</span></span> | <span data-ttu-id="dddd2-349">Office</span><span class="sxs-lookup"><span data-stu-id="dddd2-349">Office</span></span>
<span data-ttu-id="dddd2-350">Заголовок</span><span class="sxs-lookup"><span data-stu-id="dddd2-350">Title</span></span> | <span data-ttu-id="dddd2-351">Заголовок</span><span class="sxs-lookup"><span data-stu-id="dddd2-351">Title</span></span>
<span data-ttu-id="dddd2-352">Заголовок</span><span class="sxs-lookup"><span data-stu-id="dddd2-352">Title</span></span> | <span data-ttu-id="dddd2-353">Название должности SPS</span><span class="sxs-lookup"><span data-stu-id="dddd2-353">SPS-JobTitle</span></span>
<span data-ttu-id="dddd2-354">Отдел</span><span class="sxs-lookup"><span data-stu-id="dddd2-354">Department</span></span> | <span data-ttu-id="dddd2-355">Отдел</span><span class="sxs-lookup"><span data-stu-id="dddd2-355">Department</span></span>
<span data-ttu-id="dddd2-356">Отдел</span><span class="sxs-lookup"><span data-stu-id="dddd2-356">Department</span></span> | <span data-ttu-id="dddd2-357">Отдел SPS</span><span class="sxs-lookup"><span data-stu-id="dddd2-357">SPS-Department</span></span>
<span data-ttu-id="dddd2-358">ObjectGuid</span><span class="sxs-lookup"><span data-stu-id="dddd2-358">ObjectGuid</span></span> | <span data-ttu-id="dddd2-359">ADGuid</span><span class="sxs-lookup"><span data-stu-id="dddd2-359">ADGuid</span></span>
<span data-ttu-id="dddd2-360">WWWHomePage</span><span class="sxs-lookup"><span data-stu-id="dddd2-360">WWWHomePage</span></span> | <span data-ttu-id="dddd2-361">PublicSiteRedirect</span><span class="sxs-lookup"><span data-stu-id="dddd2-361">PublicSiteRedirect</span></span>
<span data-ttu-id="dddd2-362">DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="dddd2-362">DistinguishedName</span></span> | <span data-ttu-id="dddd2-363">SPS DistinguishedName</span><span class="sxs-lookup"><span data-stu-id="dddd2-363">SPS-DistinguishedName</span></span>
<span data-ttu-id="dddd2-364">msOnline ObjectId</span><span class="sxs-lookup"><span data-stu-id="dddd2-364">msOnline-ObjectId</span></span> | <span data-ttu-id="dddd2-365">msOnline ObjectId</span><span class="sxs-lookup"><span data-stu-id="dddd2-365">msOnline-ObjectId</span></span>
<span data-ttu-id="dddd2-366">PreferredLanguage</span><span class="sxs-lookup"><span data-stu-id="dddd2-366">PreferredLanguage</span></span> | <span data-ttu-id="dddd2-367">SPS MUILanguages</span><span class="sxs-lookup"><span data-stu-id="dddd2-367">SPS-MUILanguages</span></span>
<span data-ttu-id="dddd2-368">msExchHideFromAddressList</span><span class="sxs-lookup"><span data-stu-id="dddd2-368">msExchHideFromAddressList</span></span> | <span data-ttu-id="dddd2-369">SPS HideFromAddressLists</span><span class="sxs-lookup"><span data-stu-id="dddd2-369">SPS-HideFromAddressLists</span></span>
<span data-ttu-id="dddd2-370">msExchRecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="dddd2-370">msExchRecipientTypeDetails</span></span> | <span data-ttu-id="dddd2-371">SPS RecipientTypeDetails</span><span class="sxs-lookup"><span data-stu-id="dddd2-371">SPS-RecipientTypeDetails</span></span>
<span data-ttu-id="dddd2-372">msonline groupType</span><span class="sxs-lookup"><span data-stu-id="dddd2-372">msonline-groupType</span></span> | <span data-ttu-id="dddd2-373">IsUnifiedGroup</span><span class="sxs-lookup"><span data-stu-id="dddd2-373">IsUnifiedGroup</span></span>
<span data-ttu-id="dddd2-374">msOnline IsPublic</span><span class="sxs-lookup"><span data-stu-id="dddd2-374">msOnline-IsPublic</span></span> | <span data-ttu-id="dddd2-375">IsPublic</span><span class="sxs-lookup"><span data-stu-id="dddd2-375">IsPublic</span></span>
<span data-ttu-id="dddd2-376">msOnline ObjectId</span><span class="sxs-lookup"><span data-stu-id="dddd2-376">msOnline-ObjectId</span></span> | <span data-ttu-id="dddd2-377">msOnline ObjectId</span><span class="sxs-lookup"><span data-stu-id="dddd2-377">msOnline-ObjectId</span></span>
<span data-ttu-id="dddd2-378">msOnline UserType</span><span class="sxs-lookup"><span data-stu-id="dddd2-378">msOnline-UserType</span></span> | <span data-ttu-id="dddd2-379">SPS UserType</span><span class="sxs-lookup"><span data-stu-id="dddd2-379">SPS-UserType</span></span>
<span data-ttu-id="dddd2-380">GroupType</span><span class="sxs-lookup"><span data-stu-id="dddd2-380">GroupType</span></span> | <span data-ttu-id="dddd2-381">GroupType</span><span class="sxs-lookup"><span data-stu-id="dddd2-381">GroupType</span></span>
<span data-ttu-id="dddd2-382">SPO IsSharePointOnlineObject</span><span class="sxs-lookup"><span data-stu-id="dddd2-382">SPO-IsSharePointOnlineObject</span></span> | <span data-ttu-id="dddd2-383">SPO IsSPO</span><span class="sxs-lookup"><span data-stu-id="dddd2-383">SPO-IsSPO</span></span>

