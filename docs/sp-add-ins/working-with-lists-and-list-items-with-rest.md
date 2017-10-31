---
title: "Работа со списками и элементами списков в службе REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a94a8e9863e6173e9036f02fd76696f6f796cfde
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="working-with-lists-and-list-items-with-rest"></a><span data-ttu-id="b9afa-102">Работа со списками и элементами списков в службе REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-102">Working with lists and list items with REST</span></span>
<span data-ttu-id="b9afa-103">Узнайте, как выполнять базовые операции CRUD (создание, чтение, обновление и удаление) со списками и элементами списков с помощью интерфейса REST в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b9afa-103">Learn how to perform basic create, read, update, and delete (CRUD) operations on lists and list items with the SharePoint REST interface.</span></span>
 

 <span data-ttu-id="b9afa-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="b9afa-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="b9afa-p102">**Совет.** Служба REST в SharePoint Online (а также в локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="b9afa-p102">**Tip**  The SharePoint Online (and on-premise SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData  `$batch` query option. For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>
 


## <a name="prerequisites"></a><span data-ttu-id="b9afa-109">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="b9afa-109">Prerequisites</span></span>

<span data-ttu-id="b9afa-p103">В этой статье предполагается, что вы уже знакомы с темами [Знакомство со службой REST для SharePoint](get-to-know-the-sharepoint-rest-service.md) и [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md). Здесь фрагменты кода не предоставлены.</span><span class="sxs-lookup"><span data-stu-id="b9afa-p103">This topic assumes that you are already familiar with the topics  [Get to know the SharePoint REST service](get-to-know-the-sharepoint-rest-service.md) and [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md). It does not provide code snippets.</span></span>
 

 

## <a name="retrieving-lists-and-list-properties-with-rest"></a><span data-ttu-id="b9afa-112">Получение списков и их свойств с помощью REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-112">Retrieving lists and list properties with REST</span></span>
<span data-ttu-id="b9afa-113"><a name="RetrieveLists"> </a></span><span class="sxs-lookup"><span data-stu-id="b9afa-113"><a name="RetrieveLists"> </a></span></span>

<span data-ttu-id="b9afa-114">В приведенном ниже примере показано, как **получить** определенный список, если вам известен его GUID.</span><span class="sxs-lookup"><span data-stu-id="b9afa-114">The following example shows how to  **retrieve** a specific list if you know its GUID.</span></span>
 

 

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```


 <span data-ttu-id="b9afa-p104">**Примечание.** Если вы хотите получить ответ в формате JSON, укажите `application/json;odata=verbose` в заголовке `accept`. Если вы хотите получить ответ в формате Atom, укажите `application/atom+xml` в заголовке `accept`.</span><span class="sxs-lookup"><span data-stu-id="b9afa-p104">**Note**  Use  `application/json;odata=verbose` in the `accept` header if you want the response in JSON. Use `application/atom+xml` in the `accept` header if you want the response in Atom format.</span></span>
 

<span data-ttu-id="b9afa-117">В следующем примере показано, как **получить** определенный список, если вы знаете его название.</span><span class="sxs-lookup"><span data-stu-id="b9afa-117">The following example shows how to  **retrieve** a specific list if you know its title.</span></span>
 

 



```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="b9afa-118">Ниже показан пример свойств списка, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="b9afa-118">The following XML shows an example of the list properties that are returned when you request the XML content type.</span></span>
 

 



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


 <span data-ttu-id="b9afa-p105">**Примечание.** Свойство **ListItemEntityTypeFullName** (в предыдущем примере — **SP.Data.ProjectPolicyItemListItem**) особенно важно, если вы хотите создать и обновить элементы списка. Это значение должно передаваться в виде свойства **type** в тексте HTTP-запроса каждый раз, когда вы создаете и обновляете элементы списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-p105">**Note**  The  **ListItemEntityTypeFullName** property ( **SP.Data.ProjectPolicyItemListItem** in the previous example) is especially important if you want to create and update list items. This value must be passed as the **type** property in the metadata that you pass in the body of the HTTP request whenever you create and update list items.</span></span>
 


## <a name="working-with-lists-by-using-rest"></a><span data-ttu-id="b9afa-121">Работа со списками с помощью REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-121">Working with lists by using REST</span></span>
<span data-ttu-id="b9afa-122"><a name="WorkLists"> </a></span><span class="sxs-lookup"><span data-stu-id="b9afa-122"><a name="WorkLists"> </a></span></span>

<span data-ttu-id="b9afa-123">В приведенном ниже примере показано, как **создать** список.</span><span class="sxs-lookup"><span data-stu-id="b9afa-123">The following example shows how to  **create** a list.</span></span>
 

 

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

<span data-ttu-id="b9afa-124">В приведенном ниже примере показано, как **обновить** список с помощью метода **MERGE**.</span><span class="sxs-lookup"><span data-stu-id="b9afa-124">The following example shows how to  **update** a list by using the **MERGE** method.</span></span>
 

 



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

<span data-ttu-id="b9afa-125">В следующем примере показано, как **создать** **настраиваемое поле** для списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-125">The following example shows how to  **create** a **custom field** for a list.</span></span>
 

 



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

<span data-ttu-id="b9afa-126">В следующем примере показано, как **удалить** список.</span><span class="sxs-lookup"><span data-stu-id="b9afa-126">The following example shows how to  **delete** a list.</span></span>
 

 



```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method: DELETE

```


## <a name="working-with-list-items-by-using-rest"></a><span data-ttu-id="b9afa-127">Работа с элементами списков с помощью REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-127">Working with list items by using REST</span></span>
<span data-ttu-id="b9afa-128"><a name="ListItems"> </a></span><span class="sxs-lookup"><span data-stu-id="b9afa-128"><a name="ListItems"> </a></span></span>

<span data-ttu-id="b9afa-129">В приведенном ниже примере показано, как **получить** все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-129">The following example shows how to  **retrieve** all of a list's items.</span></span>
 

 

 <span data-ttu-id="b9afa-p106">**Примечание.** Параметр запроса OData $skip не работает, когда вы запрашиваете элементы списка. Во многих случаях вместо него можно использовать параметр [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9afa-p106">**Note**  The OData $skip query option does not work when querying list items. In may situations, you can use the  [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx) option instead.</span></span>
 


```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="b9afa-132">В следующем примере показано, как **получить** определенный элемент списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-132">The following example shows how to  **retrieve** a specific list item.</span></span>
 

 



```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<span data-ttu-id="b9afa-133">Ниже показан пример свойств элементов списка, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="b9afa-133">The following XML shows an example of the list item properties that are returned when you request the XML content type.</span></span>
 

 



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

<span data-ttu-id="b9afa-134">В следующем примере показано, как **создать** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-134">The following example shows how to  **create** a list item.</span></span>
 

 

 <span data-ttu-id="b9afa-135">**Примечание.** Чтобы выполнить эту операцию, необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b9afa-135">**Note**  To do this operation, you must know the  **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>
 




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

<span data-ttu-id="b9afa-136">В следующем примере показано, как **обновить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-136">The following example shows how to  **update** a list item.</span></span>
 

 

 <span data-ttu-id="b9afa-137">**Примечание.** Чтобы выполнить эту операцию, необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="b9afa-137">**Note**  To do this operation, you must know the  **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>
 




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

<span data-ttu-id="b9afa-138">В следующем примере показано, как **удалить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="b9afa-138">The following example shows how to  **delete** a list item.</span></span>
 

 



```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```


## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a><span data-ttu-id="b9afa-139">Использование значений ETag для определения версий документов и элементов списков</span><span class="sxs-lookup"><span data-stu-id="b9afa-139">Using ETag values to determine document and list item versioning</span></span>
<span data-ttu-id="b9afa-140"><a name="Etag"> </a></span><span class="sxs-lookup"><span data-stu-id="b9afa-140"><a name="Etag"> </a></span></span>

<span data-ttu-id="b9afa-p107"> Служба SharePoint REST, работающая по [стандарту OData](http://www.odata.org/developers/protocols/operations), использует [значения HTML ETag для управления версиями](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) списков SharePoint и их элементов. Чтобы проверить версию элемента при выполнении запроса **PUT**, **MERGE** или **DELETE**, укажите значение **ETag** в заголовке HTTP-запроса **If-Match**</span><span class="sxs-lookup"><span data-stu-id="b9afa-p107">The SharePoint REST service, which follows the  [OData standard](http://www.odata.org/developers/protocols/operations), uses  [HTML ETags for concurrency control](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) of SharePoint lists and list items. To check on an item's version when you perform a **PUT**,  **MERGE**, or  **DELETE** request, specify an **ETag** in the **If-Match** HTTP request header.</span></span>
 

 
<span data-ttu-id="b9afa-143">Если указанное значение **ETag** не соответствует значению **ETag** документа или элемента списка на сервере, служба REST возвращает исключение 412 согласно спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="b9afa-143">If the  **ETag** you specify in your request does not match the **ETag** of the document or list item on the server, the REST service returns a 412 exception, per the OData specification.</span></span>
 

 

- <span data-ttu-id="b9afa-144">Чтобы перезаписать элемент независимо от версии, установите значение **ETag** **"*"**.</span><span class="sxs-lookup"><span data-stu-id="b9afa-144">To force an overwrite of the item regardless of version, set the  **ETag** value to **"*"**.</span></span>
    
 
- <span data-ttu-id="b9afa-145">Если вы не укажете значение **ETag**, SharePoint перезапишет элемент независимо от версии.</span><span class="sxs-lookup"><span data-stu-id="b9afa-145">If you do not specify an  **ETag**, SharePoint overwrites the item regardless of version.</span></span>
    
 
<span data-ttu-id="b9afa-146">В SharePoint значения ETag применяются только к спискам SharePoint и элементам списков.</span><span class="sxs-lookup"><span data-stu-id="b9afa-146">Within SharePoint, ETags apply only to SharePoint lists and list items.</span></span>
 

 

## <a name="additional-resources"></a><span data-ttu-id="b9afa-147">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b9afa-147">Additional resources</span></span>
<span data-ttu-id="b9afa-148"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b9afa-148"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="b9afa-149">Выполнение базовых операций с использованием конечных точек SharePoint REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-149">Complete basic operations using SharePoint REST endpoints</span></span>](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [<span data-ttu-id="b9afa-150">Работа с папками и файлами в службе REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-150">Working with folders and files with REST</span></span>](working-with-folders-and-files-with-rest.md)
    
 
-  [<span data-ttu-id="b9afa-151">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="b9afa-151">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
    
 
-  [<span data-ttu-id="b9afa-152">SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST</span><span class="sxs-lookup"><span data-stu-id="b9afa-152">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](http://code.msdn.microsoft.com/SharePoint-Perform-ab9c4ae5)
    
 
-  [<span data-ttu-id="b9afa-153">Выполнение вызовов REST при помощи C# и JavaScript для SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-153">Making REST calls with C# and JavaScript for SharePoint</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
    
 
-  [<span data-ttu-id="b9afa-154">Выполнение вызовов REST при помощи C# и JavaScript для демоверсии SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-154">Making REST calls with C# and JavaScript for SharePoint demo</span></span>](http://www.microsoft.com/resources/msdn/en-us/office/media/video/videol?cid=sdc&amp;from=mscomsdc&amp;VideoID=b1e7c9c5-0f62-4a78-bb7b-8e283c86145c)
    
 
-  [<span data-ttu-id="b9afa-155">Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-155">Complete basic operations using SharePoint client library code</span></span>](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [<span data-ttu-id="b9afa-156">Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-156">Complete basic operations using JavaScript library code in SharePoint</span></span>](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)
    
 
-  [<span data-ttu-id="b9afa-157">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-157">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="b9afa-158">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-158">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="b9afa-159">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b9afa-159">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
    
 
-  [<span data-ttu-id="b9afa-160">Протокол OData</span><span class="sxs-lookup"><span data-stu-id="b9afa-160">Open Data Protocol</span></span>](http://www.odata.org/)
    
 
-  [<span data-ttu-id="b9afa-161">OData: формат JSON</span><span class="sxs-lookup"><span data-stu-id="b9afa-161">OData: JavaScript Object Notation (JSON) Format</span></span>](http://www.odata.org/documentation/odata-version-2-0/json-format/)
    
 

 

 

