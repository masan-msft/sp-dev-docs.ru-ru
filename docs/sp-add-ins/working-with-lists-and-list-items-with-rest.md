---
title: "Работа со списками и элементами списков в службе REST"
description: "Выполнение основных операций по созданию, чтению, обновлению и удалению списков и элементов списков с помощью интерфейса REST SharePoint."
ms.date: 12/13/2017
ms.prod: sharepoint
ms.openlocfilehash: ed2f377af03bb1e27173447f01250d7819359387
ms.sourcegitcommit: bd167bbbcae67b7f1c6a40366183781a80337bc2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2018
---
# <a name="working-with-lists-and-list-items-with-rest"></a><span data-ttu-id="52a75-103">Работа со списками и элементами списков с использованием REST</span><span class="sxs-lookup"><span data-stu-id="52a75-103">Working with lists and list items with REST</span></span>

> [!TIP] 
> <span data-ttu-id="52a75-104">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData `$batch`.</span><span class="sxs-lookup"><span data-stu-id="52a75-104">The SharePoint Online (and on-premises SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData `$batch` query option.</span></span> <span data-ttu-id="52a75-105">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="52a75-105">For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52a75-106">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="52a75-106">Prerequisites</span></span>

<span data-ttu-id="52a75-107">В этой статье предполагается, что вы уже ознакомились со статьями [Знакомство со службой REST для SharePoint](get-to-know-the-sharepoint-rest-service.md) и [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="52a75-107">This topic assumes that you are already familiar with the topics Get to know the SharePoint REST service and Complete basic operations using SharePoint REST endpoints.</span></span> <span data-ttu-id="52a75-108">Здесь не представлены фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="52a75-108">It does not provide code snippets.</span></span>
 

<span data-ttu-id="52a75-109"><a name="RetrieveLists"> </a></span><span class="sxs-lookup"><span data-stu-id="52a75-109"></span></span> 

## <a name="retrieving-lists-and-list-properties-with-rest"></a><span data-ttu-id="52a75-110">Получение списков и свойств списков с помощью REST</span><span class="sxs-lookup"><span data-stu-id="52a75-110">Retrieving lists and list properties with REST</span></span>

<span data-ttu-id="52a75-111">В следующем примере показано, как **получить** определенный список, если вы знаете его GUID.</span><span class="sxs-lookup"><span data-stu-id="52a75-111">The following example shows how to **retrieve** a specific list if you know its GUID.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```


> [!NOTE] 
> <span data-ttu-id="52a75-112">Если вы хотите получить отклик в формате JSON, укажите `application/json;odata=verbose` в заголовке `accept`.</span><span class="sxs-lookup"><span data-stu-id="52a75-112">If you want the response in JSON, use `application/json;odata=verbose` in the `accept` header .</span></span> 

> <span data-ttu-id="52a75-113">Если вы хотите получить отклик в формате Atom, укажите `application/atom+xml` в заголовке `accept`.</span><span class="sxs-lookup"><span data-stu-id="52a75-113">If you want the response in Atom format, use `application/atom+xml` in the `accept` header.</span></span>
 
<br/>

<span data-ttu-id="52a75-114">В следующем примере показано, как **получить** определенный список, если вы знаете его название.</span><span class="sxs-lookup"><span data-stu-id="52a75-114">The following example shows how to  **retrieve** a specific list if you know its title.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="52a75-115">Ниже показан пример свойств списка, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="52a75-115">The following XML shows an example of the list properties that are returned when you request the XML content type.</span></span>

```XML
  <content type="application/xml">
  <m:properties>
  <d:AllowContentTypes m:type="Edm.Boolean">true</d:AllowContentTypes> 
  <d:BaseTemplate m:type="Edm.Int32">100</d:BaseTemplate> 
  <d:BaseType m:type="Edm.Int32">0</d:BaseType> 
  <d:ContentTypesEnabled m:type="Edm.Boolean">false</d:ContentTypesEnabled> 
  <d:Created m:type="Edm.DateTime">2012-06-26T23:15:58Z</d:Created> 
  <d:DefaultContentApprovalWorkflowId m:type="Edm.Guid">00000000-0000-0000-0000-000000000000</d:DefaultContentApprovalWorkflowId> 
  <d:Description>A list created by Project Based Retention used to store Project Policy Items.</d:Description> 
  <d:Direction>none</d:Direction> 
  <d:DocumentTemplateUrl m:null="true" /> 
  <d:DraftVersionVisibility m:type="Edm.Int32">0</d:DraftVersionVisibility> 
  <d:EnableAttachments m:type="Edm.Boolean">true</d:EnableAttachments> 
  <d:EnableFolderCreation m:type="Edm.Boolean">false</d:EnableFolderCreation> 
  <d:EnableMinorVersions m:type="Edm.Boolean">false</d:EnableMinorVersions> 
  <d:EnableModeration m:type="Edm.Boolean">false</d:EnableModeration> 
  <d:EnableVersioning m:type="Edm.Boolean">false</d:EnableVersioning> 
  <d:EntityTypeName>ProjectPolicyItemList</d:EntityTypeName> 
  <d:ForceCheckout m:type="Edm.Boolean">false</d:ForceCheckout> 
  <d:HasExternalDataSource m:type="Edm.Boolean">false</d:HasExternalDataSource> 
  <d:Hidden m:type="Edm.Boolean">true</d:Hidden> 
  <d:Id m:type="Edm.Guid">74de3ff3-029c-42f9-bd2a-1e9463def69d</d:Id> 
  <d:ImageUrl>/_layouts/15/images/itgen.gif</d:ImageUrl> 
  <d:IrmEnabled m:type="Edm.Boolean">false</d:IrmEnabled> 
  <d:IrmExpire m:type="Edm.Boolean">false</d:IrmExpire> 
  <d:IrmReject m:type="Edm.Boolean">false</d:IrmReject> 
  <d:IsApplicationList m:type="Edm.Boolean">false</d:IsApplicationList> 
  <d:IsCatalog m:type="Edm.Boolean">false</d:IsCatalog> 
  <d:IsPrivate m:type="Edm.Boolean">false</d:IsPrivate> 
  <d:ItemCount m:type="Edm.Int32">0</d:ItemCount> 
  <d:LastItemDeletedDate m:type="Edm.DateTime">2012-06-26T23:15:58Z</d:LastItemDeletedDate> 
  <d:LastItemModifiedDate m:type="Edm.DateTime">2012-06-26T23:15:59Z</d:LastItemModifiedDate> 
  <d:ListItemEntityTypeFullName>SP.Data.ProjectPolicyItemListItem</d:ListItemEntityTypeFullName> 
  <d:MultipleDataList m:type="Edm.Boolean">false</d:MultipleDataList> 
  <d:NoCrawl m:type="Edm.Boolean">true</d:NoCrawl> 
  <d:ParentWebUrl>/</d:ParentWebUrl> 
  <d:ServerTemplateCanCreateFolders m:type="Edm.Boolean">true</d:ServerTemplateCanCreateFolders> 
  <d:TemplateFeatureId m:type="Edm.Guid">00bfea71-de22-43b2-a848-c05709900100</d:TemplateFeatureId> 
  <d:Title>Project Policy Item List</d:Title> 
  </m:properties>
  </content>
```


> [!NOTE] 
> <span data-ttu-id="52a75-116">Свойство **ListItemEntityTypeFullName** (в предыдущем примере — **SP.Data.ProjectPolicyItemListItem**) особенно важно, если вы хотите создать и обновить элементы списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-116">The **ListItemEntityTypeFullName** property (**SP.Data.ProjectPolicyItemListItem** in the previous example) is especially important if you want to create and update list items.</span></span> <span data-ttu-id="52a75-117">Это значение должно передаваться в виде свойства **type** в тексте HTTP-запроса каждый раз, когда вы создаете и обновляете элементы списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-117">The  ListItemEntityTypeFullName property ( SP.Data.ProjectPolicyItemListItem in the previous example) is especially important if you want to create and update list items. This value must be passed as the **type** property in the metadata that you pass in the body of the HTTP request whenever you create and update list items.</span></span>
 
<br/>

<span data-ttu-id="52a75-118"><a name="WorkLists"> </a></span><span class="sxs-lookup"><span data-stu-id="52a75-118"></span></span>

## <a name="working-with-lists-by-using-rest"></a><span data-ttu-id="52a75-119">Работа со списками с помощью REST</span><span class="sxs-lookup"><span data-stu-id="52a75-119">Working with lists by using REST</span></span>

<span data-ttu-id="52a75-120">В приведенном ниже примере показано, как **создать** список.</span><span class="sxs-lookup"><span data-stu-id="52a75-120">The following example shows how to  **create** a list.</span></span>

```
url: http://site url/_api/web/lists
method: POST
body: { '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true, 'BaseTemplate': 100,
 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<br/>

<span data-ttu-id="52a75-121">В приведенном ниже примере показано, как **обновить** список, используя метод **MERGE**.</span><span class="sxs-lookup"><span data-stu-id="52a75-121">The following example shows how to **update** a list by using the **MERGE** method.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
body: { '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH": etag or "*"
    X-HTTP-Method: MERGE,
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<br/>

<span data-ttu-id="52a75-122">В следующем примере показывается, как **создать** **настраиваемое поле** для списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-122">The following example shows how to **create** a **custom field** for a list.</span></span>

```
Url: url: http://site url/_api/web/lists(guid'list GUID')/Fields
Method:POST
Body: { '__metadata': { 'type': 'SP.Field' }, 'Title': 'field title', 'FieldTypeKind': FieldType value,'Required': 'true/false', 'EnforceUniqueValues': 'true/false','StaticName': 'field name'}
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<br/>

<span data-ttu-id="52a75-123">В приведенном ниже примере показано, как **удалить** список.</span><span class="sxs-lookup"><span data-stu-id="52a75-123">The following example shows how to **delete** a list.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method: DELETE

```

<br/>

<span data-ttu-id="52a75-124"><a name="ListItems"> </a></span><span class="sxs-lookup"><span data-stu-id="52a75-124"></span></span>

## <a name="working-with-list-items-by-using-rest"></a><span data-ttu-id="52a75-125">Работа с элементами списка с помощью REST</span><span class="sxs-lookup"><span data-stu-id="52a75-125">Working with list items by using REST</span></span>

<span data-ttu-id="52a75-126">В приведенном ниже примере показано, как **получить** все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-126">The following example shows how to **retrieve** all of a list's items.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="52a75-127">Параметр запроса OData $skip не работает при запрашивании элементов списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-127">The OData $skip query option does not work when querying list items. In may situations, you can use the  $skiptoken option instead.</span></span> <span data-ttu-id="52a75-128">Обычно вместо него можно использовать параметр [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx).</span><span class="sxs-lookup"><span data-stu-id="52a75-128">Note The OData $skip query option does not work when querying list items. In may situations, you can use the  [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx) option instead.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="52a75-129">В приведенном ниже примере показано, как **получить** определенный элемент списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-129">The following example shows how to **retrieve** a specific list item.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="52a75-130">Ниже показан пример свойств элементов списка, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="52a75-130">The following XML shows an example of the list item properties that are returned when you request the XML content type.</span></span>

```XML
<content type="application/xml">
<m:properties> 
<d:FileSystemObjectType m:type="Edm.Int32">0</d:FileSystemObjectType>
<d:Id m:type="Edm.Int32">1</d:Id>
<d:ID m:type="Edm.Int32">1</d:ID>
<d:ContentTypeId>0x010049564F321A0F0543BA8C6303316C8C0F</d:ContentTypeId>
<d:Title>an item</d:Title>
<d:Modified m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Modified>
<d:Created m:type="Edm.DateTime">2012-07-24T22:47:26Z</d:Created>
<d:AuthorId m:type="Edm.Int32">11</d:AuthorId>
<d:EditorId m:type="Edm.Int32">11</d:EditorId>
<d:OData__UIVersionString>1.0</d:OData__UIVersionString>
<d:Attachments m:type="Edm.Boolean">false</d:Attachments>
<d:GUID m:type="Edm.Guid">eb6850c5-9a30-4636-b282-234eda8b1057</d:GUID>
</m:properties>
</content>
```

<br/>

<span data-ttu-id="52a75-131">В следующем примере показывается, как **создать** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-131">The following example shows how to **create** a list item.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="52a75-132">[!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="52a75-132">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>
 
```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'Test'}
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<br/>

<span data-ttu-id="52a75-133">В следующем примере показывается, как **обновить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-133">The following example shows how to **update** a list item.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="52a75-134">[!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="52a75-134">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
body: { '__metadata': { 'type': 'SP.Data.TestListItem' }, 'Title': 'TestUpdated'}
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"MERGE",
    accept: "application/json;odata=verbose"
    content-type: "application/json;odata=verbose"
    content-length:length of post body
```

<br/>

<span data-ttu-id="52a75-135">В приведенном ниже примере показано, как **удалить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="52a75-135">The following example shows how to **delete** a list item.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

<br/>

<span data-ttu-id="52a75-136"><a name="Etag"> </a></span><span class="sxs-lookup"><span data-stu-id="52a75-136"></span></span>

## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a><span data-ttu-id="52a75-137">Использование значений ETag для определения версий документов и элементов списков</span><span class="sxs-lookup"><span data-stu-id="52a75-137">Using ETag values to determine document and list item versioning</span></span>

<span data-ttu-id="52a75-138">Служба SharePoint REST, работающая по [стандарту OData](http://www.odata.org/developers/protocols/operations), использует [значения HTML ETag для управления версиями](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) списков SharePoint и их элементов.</span><span class="sxs-lookup"><span data-stu-id="52a75-138"> The SharePoint REST service, which follows the  [OData standard](http://www.odata.org/developers/protocols/operations), uses  [HTML ETags for concurrency control](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) of SharePoint lists and list items.</span></span> <span data-ttu-id="52a75-139">Чтобы проверить версию элемента при выполнении запроса **PUT**, **MERGE** или **DELETE**, укажите значение **ETag** в заголовке HTTP-запроса **If-Match**.</span><span class="sxs-lookup"><span data-stu-id="52a75-139">To check on an item's version when you perform a **PUT**,  **MERGE**, or  **DELETE** request, specify an **ETag** in the **If-Match** HTTP request header.</span></span>

<span data-ttu-id="52a75-140">Если **ETag**, который вы указываете в вашем запросе, не соответствует **ETag** документа или элемента списка на сервере, служба REST возвращает исключение 412 с помощью спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="52a75-140">If the **ETag** you specify in your request does not match the **ETag** of the document or list item on the server, the REST service returns a 412 exception, per the OData specification.</span></span>

- <span data-ttu-id="52a75-141">Чтобы принудительно переписать элемент независимо от версии, задайте **ETag** значение **"\*"**.</span><span class="sxs-lookup"><span data-stu-id="52a75-141">To force an overwrite of the item regardless of version, set the **ETag** value to **"**"\*.</span></span>
    
- <span data-ttu-id="52a75-142">Если не указать **ETag**, SharePoint переписывает элемент независимо от версии.</span><span class="sxs-lookup"><span data-stu-id="52a75-142">If you do not specify an **ETag**, SharePoint overwrites the item regardless of version.</span></span>
    
 
<span data-ttu-id="52a75-143">В SharePoint значения ETag применяются только к спискам SharePoint и элементам списков.</span><span class="sxs-lookup"><span data-stu-id="52a75-143">Within SharePoint, ETags apply only to SharePoint lists and list items.</span></span>
 
## <a name="see-also"></a><span data-ttu-id="52a75-144">См. также</span><span class="sxs-lookup"><span data-stu-id="52a75-144">See also</span></span>
<span data-ttu-id="52a75-145"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="52a75-145"></span></span>

- [<span data-ttu-id="52a75-146">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="52a75-146">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="52a75-147">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="52a75-147">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
- [<span data-ttu-id="52a75-148">SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST</span><span class="sxs-lookup"><span data-stu-id="52a75-148">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](https://docs.microsoft.com/ru-RU/sharepoint/dev/sp-add-ins/working-with-folders-and-files-with-rest)
- [<span data-ttu-id="52a75-149">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="52a75-149">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [<span data-ttu-id="52a75-150">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="52a75-150">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
- [<span data-ttu-id="52a75-151">Справочные материалы по REST API и примеры</span><span class="sxs-lookup"><span data-stu-id="52a75-151">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="52a75-152">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="52a75-152">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)  
- [<span data-ttu-id="52a75-153">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="52a75-153">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md) 

 

 

