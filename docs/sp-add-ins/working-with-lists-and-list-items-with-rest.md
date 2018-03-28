---
title: Работа со списками и элементами списков в службе REST
description: Выполнение основных операций по созданию, чтению, обновлению и удалению списков и элементов списков с помощью интерфейса REST SharePoint.
ms.date: 12/13/2017
ms.prod: sharepoint
ms.openlocfilehash: 6e61e000e9fc375c14810c6da12e451b286dd8ce
ms.sourcegitcommit: 895d31071e73aa23e62593c9ffa46b38701ba801
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/19/2018
---
# <a name="working-with-lists-and-list-items-with-rest"></a><span data-ttu-id="7f1a0-103">Работа со списками и элементами списков с использованием REST</span><span class="sxs-lookup"><span data-stu-id="7f1a0-103">Working with lists and list items with REST</span></span>

> [!TIP] 
> <span data-ttu-id="7f1a0-104">Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData `$batch`.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-104">The SharePoint Online (and on-premises SharePoint 2016 and later) REST service supports combining multiple requests into a single call to the service by using the OData `$batch` query option.</span></span> <span data-ttu-id="7f1a0-105">Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="7f1a0-105">For details and links to code samples, see [Make batch requests with the REST APIs](make-batch-requests-with-the-rest-apis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f1a0-106">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="7f1a0-106">Prerequisites</span></span>

<span data-ttu-id="7f1a0-107">В этой статье предполагается, что вы уже ознакомились со статьями [Знакомство со службой REST для SharePoint](get-to-know-the-sharepoint-rest-service.md) и [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="7f1a0-107">This topic assumes that you are already familiar with the topics [Get to know the SharePoint REST service](get-to-know-the-sharepoint-rest-service.md) and [Complete basic operations using SharePoint REST endpoints](complete-basic-operations-using-sharepoint-rest-endpoints.md).</span></span> <span data-ttu-id="7f1a0-108">Здесь не представлены фрагменты кода.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-108">It does not provide code snippets.</span></span>
 

<span data-ttu-id="7f1a0-109"><a name="RetrieveLists"> </a></span><span class="sxs-lookup"><span data-stu-id="7f1a0-109"><a name="RetrieveLists"> </a></span></span> 

## <a name="retrieving-lists-and-list-properties-with-rest"></a><span data-ttu-id="7f1a0-110">Получение списков и свойств списков с помощью REST</span><span class="sxs-lookup"><span data-stu-id="7f1a0-110">Retrieving lists and list properties with REST</span></span>

<span data-ttu-id="7f1a0-111">В следующем примере показано, как **получить** определенный список, если вы знаете его GUID.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-111">The following example shows how to **retrieve** a specific list if you know its GUID.</span></span>

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```


> [!NOTE] 
> <span data-ttu-id="7f1a0-112">Если вы хотите получить отклик в формате JSON, укажите `application/json;odata=verbose` в заголовке `accept`.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-112">If you want the response in JSON, use `application/json;odata=verbose` in the `accept` header .</span></span> 

> <span data-ttu-id="7f1a0-113">Если вы хотите получить отклик в формате Atom, укажите `application/atom+xml` в заголовке `accept`.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-113">If you want the response in Atom format, use `application/atom+xml` in the `accept` header.</span></span>
 
<br/>

<span data-ttu-id="7f1a0-114">В следующем примере показано, как **получить** определенный список, если вы знаете его название.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-114">The following example shows how to  **retrieve** a specific list if you know its title.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="7f1a0-115">Ниже показан пример свойств списка, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-115">The following XML shows an example of the list properties that are returned when you request the XML content type.</span></span>

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
> <span data-ttu-id="7f1a0-116">Свойство **ListItemEntityTypeFullName** (в предыдущем примере — **SP.Data.ProjectPolicyItemListItem**) особенно важно, если вы хотите создать и обновить элементы списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-116">The **ListItemEntityTypeFullName** property (**SP.Data.ProjectPolicyItemListItem** in the previous example) is especially important if you want to create and update list items.</span></span> <span data-ttu-id="7f1a0-117">Это значение должно передаваться в виде свойства **type** в тексте HTTP-запроса каждый раз, когда вы создаете и обновляете элементы списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-117">This value must be passed as the **type** property in the metadata that you pass in the body of the HTTP request whenever you create and update list items.</span></span>
 
<br/>

<span data-ttu-id="7f1a0-118"><a name="WorkLists"> </a></span><span class="sxs-lookup"><span data-stu-id="7f1a0-118"><a name="WorkLists"> </a></span></span>

## <a name="working-with-lists-by-using-rest"></a><span data-ttu-id="7f1a0-119">Работа со списками с помощью REST</span><span class="sxs-lookup"><span data-stu-id="7f1a0-119">Working with lists by using REST</span></span>

<span data-ttu-id="7f1a0-120">В приведенном ниже примере показано, как **создать** список.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-120">The following example shows how to  **create** a list.</span></span>

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

<span data-ttu-id="7f1a0-121">В приведенном ниже примере показано, как **обновить** список, используя метод **MERGE**.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-121">The following example shows how to **update** a list by using the **MERGE** method.</span></span>

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

<span data-ttu-id="7f1a0-122">В следующем примере показывается, как **создать** **настраиваемое поле** для списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-122">The following example shows how to **create** a **custom field** for a list.</span></span>

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

<span data-ttu-id="7f1a0-123">В приведенном ниже примере показано, как **удалить** список.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-123">The following example shows how to **delete** a list.</span></span>

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

<span data-ttu-id="7f1a0-124"><a name="ListItems"> </a></span><span class="sxs-lookup"><span data-stu-id="7f1a0-124"><a name="ListItems"> </a></span></span>

## <a name="working-with-list-items-by-using-rest"></a><span data-ttu-id="7f1a0-125">Работа с элементами списка с помощью REST</span><span class="sxs-lookup"><span data-stu-id="7f1a0-125">Working with list items by using REST</span></span>

### <a name="retrieve-all-list-items"></a><span data-ttu-id="7f1a0-126">Получение всех элементов списка</span><span class="sxs-lookup"><span data-stu-id="7f1a0-126">Retrieve all list items</span></span>

<span data-ttu-id="7f1a0-127">Ниже показано, как **получить** все элементы списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-127">The following example shows how to **retrieve** all of a list's items.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="7f1a0-128">Параметр запроса OData $skip не работает при запрашивании элементов списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-128">The OData $skip query option does not work when querying list items.</span></span> <span data-ttu-id="7f1a0-129">Обычно вместо него можно использовать параметр [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f1a0-129">In may situations, you can use the [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx) option instead.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

### <a name="retrieve-specific-list-item"></a><span data-ttu-id="7f1a0-130">Получение определенного элемента списка</span><span class="sxs-lookup"><span data-stu-id="7f1a0-130">Retrieve specific list item</span></span>

<span data-ttu-id="7f1a0-131">Ниже показано, как **получить** определенный элемент списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-131">The following example shows how to **retrieve** a specific list item.</span></span>

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

<span data-ttu-id="7f1a0-132">Ниже показан пример свойств элементов списка, которые возвращаются при запросе типа контента XML.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-132">The following XML shows an example of the list item properties that are returned when you request the XML content type.</span></span>

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

### <a name="create-list-item"></a><span data-ttu-id="7f1a0-133">Создание элемента списка</span><span class="sxs-lookup"><span data-stu-id="7f1a0-133">Create list item</span></span>

<span data-ttu-id="7f1a0-134">Ниже показано, как **создать** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-134">The following example shows how to **create** a list item.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="7f1a0-135">[!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-135">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>
 
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

### <a name="create-list-item-in-a-folder"></a><span data-ttu-id="7f1a0-136">Создание элемента списка в папке</span><span class="sxs-lookup"><span data-stu-id="7f1a0-136">Create list item in a folder</span></span>

<span data-ttu-id="7f1a0-137">Создайте элемент списка в папке.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-137">Create list item in a folder.</span></span>

```text
POST /_api/web/lists/GetByTitle('Test')/AddValidateUpdateItemUsingPath
```

#### <a name="uri-parameters"></a><span data-ttu-id="7f1a0-138">Параметры URI</span><span class="sxs-lookup"><span data-stu-id="7f1a0-138">URI Parameters</span></span>

<span data-ttu-id="7f1a0-139">Нет</span><span class="sxs-lookup"><span data-stu-id="7f1a0-139">None</span></span>

#### <a name="request-headers"></a><span data-ttu-id="7f1a0-140">Заголовки запроса</span><span class="sxs-lookup"><span data-stu-id="7f1a0-140">Request headers</span></span>

| <span data-ttu-id="7f1a0-141">Заголовок</span><span class="sxs-lookup"><span data-stu-id="7f1a0-141">Header</span></span> | <span data-ttu-id="7f1a0-142">Значение</span><span class="sxs-lookup"><span data-stu-id="7f1a0-142">Value</span></span> |
|--------|-------|
|<span data-ttu-id="7f1a0-143">Accept</span><span class="sxs-lookup"><span data-stu-id="7f1a0-143">Accept</span></span>|<span data-ttu-id="7f1a0-144">application/json;odata=nometadata</span><span class="sxs-lookup"><span data-stu-id="7f1a0-144">Accept > application/json;odata=nometadata</span></span>|
|<span data-ttu-id="7f1a0-145">Content-Type</span><span class="sxs-lookup"><span data-stu-id="7f1a0-145">Content-Type</span></span>|<span data-ttu-id="7f1a0-146">application/json;odata=nometadata</span><span class="sxs-lookup"><span data-stu-id="7f1a0-146">Accept > application/json;odata=nometadata</span></span>|
|<span data-ttu-id="7f1a0-147">x-requestdigest</span><span class="sxs-lookup"><span data-stu-id="7f1a0-147">x-requestdigest</span></span>|<span data-ttu-id="7f1a0-148">Подходящий дайджест для текущего сайта</span><span class="sxs-lookup"><span data-stu-id="7f1a0-148">The appropriate digest for current site</span></span>|

#### <a name="request-body"></a><span data-ttu-id="7f1a0-149">Тело запроса</span><span class="sxs-lookup"><span data-stu-id="7f1a0-149">Request body</span></span>

```json
{
    "listItemCreateInfo": {
        "FolderPath":  { "DecodedUrl": "https://contoso.sharepoint.com/lists/Test/Folder/SubFolder" },
        "UnderlyingObjectType": 0
    },
    "formValues": [
        {
            "FieldName": "Title",
            "FieldValue": "Item"
        }
    ],
    "bNewDocumentUpdate": false
}
```

| <span data-ttu-id="7f1a0-150">Свойство</span><span class="sxs-lookup"><span data-stu-id="7f1a0-150">Property</span></span> | <span data-ttu-id="7f1a0-151">Описание</span><span class="sxs-lookup"><span data-stu-id="7f1a0-151">Description</span></span> |
|----------|-------|
|<span data-ttu-id="7f1a0-152">listItemCreateInfo</span><span class="sxs-lookup"><span data-stu-id="7f1a0-152">listItemCreateInfo</span></span>|<span data-ttu-id="7f1a0-153">Информация о списке и папке, где необходимо создать элемент</span><span class="sxs-lookup"><span data-stu-id="7f1a0-153">Information about the list and folder where the item should be created</span></span>|
|<span data-ttu-id="7f1a0-154">listItemCreateInfo.FolderPath.DecodedUrl</span><span class="sxs-lookup"><span data-stu-id="7f1a0-154">listItemCreateInfo.FolderPath.DecodedUrl</span></span>|<span data-ttu-id="7f1a0-155">Абсолютный URL-адрес папки, где необходимо создать элемент</span><span class="sxs-lookup"><span data-stu-id="7f1a0-155">Absolute URL of the folder where the item should be created</span></span>|
|<span data-ttu-id="7f1a0-156">listItemCreateInfo.UnderlyingObjectType</span><span class="sxs-lookup"><span data-stu-id="7f1a0-156">listItemCreateInfo.UnderlyingObjectType</span></span>|<span data-ttu-id="7f1a0-157">Тип элемента, который необходимо создать.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-157">Type of item to create.</span></span> <span data-ttu-id="7f1a0-158">Дополнительные сведения см. в разделе [https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.filesystemobjecttype(v=office.14).aspx](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.filesystemobjecttype(v=office.14).aspx).</span><span class="sxs-lookup"><span data-stu-id="7f1a0-158">For more information, see:</span></span>|
|<span data-ttu-id="7f1a0-159">formValues</span><span class="sxs-lookup"><span data-stu-id="7f1a0-159">formValues</span></span>|<span data-ttu-id="7f1a0-160">Массив имен полей и значений, которые необходимо присвоить новому элементу</span><span class="sxs-lookup"><span data-stu-id="7f1a0-160">Array of field names and values to set on the newly created item</span></span>|
|<span data-ttu-id="7f1a0-161">bNewDocumentUpdate</span><span class="sxs-lookup"><span data-stu-id="7f1a0-161">bNewDocumentUpdate</span></span>|<span data-ttu-id="7f1a0-162">Установите значение `false`, чтобы создать элемент списка</span><span class="sxs-lookup"><span data-stu-id="7f1a0-162">Set to `false` to create a list item</span></span>|

#### <a name="responses"></a><span data-ttu-id="7f1a0-163">Ответы</span><span class="sxs-lookup"><span data-stu-id="7f1a0-163">Error Responses</span></span>

| <span data-ttu-id="7f1a0-164">Имя</span><span class="sxs-lookup"><span data-stu-id="7f1a0-164">Name</span></span>   | <span data-ttu-id="7f1a0-165">Тип</span><span class="sxs-lookup"><span data-stu-id="7f1a0-165">Type</span></span>    |<span data-ttu-id="7f1a0-166">Описание</span><span class="sxs-lookup"><span data-stu-id="7f1a0-166">Description</span></span>|
|--------|---------|-----------|
|<span data-ttu-id="7f1a0-167">200 OK</span><span class="sxs-lookup"><span data-stu-id="7f1a0-167">200 OK</span></span>  | <span data-ttu-id="7f1a0-168">Boolean</span><span class="sxs-lookup"><span data-stu-id="7f1a0-168">Boolean</span></span> |<span data-ttu-id="7f1a0-169">Успешно</span><span class="sxs-lookup"><span data-stu-id="7f1a0-169">Success</span></span>    |

```json
{
  "value": [
    {
      "ErrorMessage": null,
      "FieldName": "Title",
      "FieldValue": "Item",
      "HasException": false,
      "ItemId": 0
    },
    {
      "ErrorMessage": null,
      "FieldName": "Id",
      "FieldValue": "1",
      "HasException": false,
      "ItemId": 0
    }
  ]
}
```

<span data-ttu-id="7f1a0-170">Свойство `value` содержит список свойств, заданных при создании элемента списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-170">The `value` property contains the list of properties that have been set when creating the list item.</span></span>

### <a name="update-list-item"></a><span data-ttu-id="7f1a0-171">Обновление элемента списка</span><span class="sxs-lookup"><span data-stu-id="7f1a0-171">Update list item</span></span>

<span data-ttu-id="7f1a0-172">Ниже показано, как **обновить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-172">The following example shows how to **update** a list item.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="7f1a0-173">[!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-173">To do this operation, you must know the **ListItemEntityTypeFullName** property of the list and pass that as the value of **type** in the HTTP request body.</span></span>

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

### <a name="delete-list-item"></a><span data-ttu-id="7f1a0-174">Удаление элемента списка</span><span class="sxs-lookup"><span data-stu-id="7f1a0-174">Delete list item</span></span>

<span data-ttu-id="7f1a0-175">Ниже показано, как **удалить** элемент списка.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-175">The following example shows how to **delete** a list item.</span></span>

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

<span data-ttu-id="7f1a0-176"><a name="Etag"> </a></span><span class="sxs-lookup"><span data-stu-id="7f1a0-176"></span></span>

## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a><span data-ttu-id="7f1a0-177">Использование значений ETag для определения версий документов и элементов списков</span><span class="sxs-lookup"><span data-stu-id="7f1a0-177">Using ETag values to determine document and list item versioning</span></span>

<span data-ttu-id="7f1a0-178">Служба SharePoint REST, работающая по [стандарту OData](http://www.odata.org/developers/protocols/operations), использует [значения HTML ETag для управления версиями](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) списков SharePoint и их элементов.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-178">The SharePoint REST service, which follows the [OData standard](http://www.odata.org/developers/protocols/operations), uses [HTML ETags for concurrency control](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) of SharePoint lists and list items.</span></span> <span data-ttu-id="7f1a0-179">Чтобы проверить версию элемента при выполнении запроса **PUT**, **MERGE** или **DELETE**, укажите значение **ETag** в заголовке HTTP-запроса **If-Match**.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-179">To check on an item's version when you perform a **PUT**, **MERGE**, or **DELETE** request, specify an **ETag** in the **If-Match** HTTP request header.</span></span>

<span data-ttu-id="7f1a0-180">Если **ETag**, который вы указываете в вашем запросе, не соответствует **ETag** документа или элемента списка на сервере, служба REST возвращает исключение 412 с помощью спецификации OData.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-180">If the **ETag** you specify in your request does not match the **ETag** of the document or list item on the server, the REST service returns a 412 exception, per the OData specification.</span></span>

- <span data-ttu-id="7f1a0-181">Чтобы принудительно переписать элемент независимо от версии, задайте **ETag** значение **"\*"**.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-181">To force an overwrite of the item regardless of version, set the **ETag** value to **"\*"**.</span></span>
    
- <span data-ttu-id="7f1a0-182">Если не указать **ETag**, SharePoint переписывает элемент независимо от версии.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-182">If you do not specify an **ETag**, SharePoint overwrites the item regardless of version.</span></span>
    
 
<span data-ttu-id="7f1a0-183">В SharePoint значения ETag применяются только к спискам SharePoint и элементам списков.</span><span class="sxs-lookup"><span data-stu-id="7f1a0-183">Within SharePoint, ETags apply only to SharePoint lists and list items.</span></span>
 
## <a name="see-also"></a><span data-ttu-id="7f1a0-184">См. также</span><span class="sxs-lookup"><span data-stu-id="7f1a0-184">See also</span></span>
<span data-ttu-id="7f1a0-185"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7f1a0-185"></span></span>

- [<span data-ttu-id="7f1a0-186">Знакомство со службой REST в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f1a0-186">Get to know the SharePoint REST service</span></span>](get-to-know-the-sharepoint-rest-service.md)
- [<span data-ttu-id="7f1a0-187">SharePoint-Add-in-REST-OData-BasicDataOperations</span><span class="sxs-lookup"><span data-stu-id="7f1a0-187">SharePoint-Add-in-REST-OData-BasicDataOperations</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
- [<span data-ttu-id="7f1a0-188">SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST</span><span class="sxs-lookup"><span data-stu-id="7f1a0-188">SharePoint: Perform basic data access operations on files and folders by using REST</span></span>](https://docs.microsoft.com/ru-RU/sharepoint/dev/sp-add-ins/working-with-folders-and-files-with-rest)
- [<span data-ttu-id="7f1a0-189">Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f1a0-189">Secure data access and client object models for SharePoint Add-ins</span></span>](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [<span data-ttu-id="7f1a0-190">Работа с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f1a0-190">Work with external data in SharePoint</span></span>](work-with-external-data-in-sharepoint.md)
- [<span data-ttu-id="7f1a0-191">Справочные материалы по REST API и примеры</span><span class="sxs-lookup"><span data-stu-id="7f1a0-191">REST API reference and samples</span></span>](https://msdn.microsoft.com/library)
- [<span data-ttu-id="7f1a0-192">Материалы по OData</span><span class="sxs-lookup"><span data-stu-id="7f1a0-192">OData resources</span></span>](get-to-know-the-sharepoint-rest-service.md#odata-resources)  
- [<span data-ttu-id="7f1a0-193">Разработка надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="7f1a0-193">Develop SharePoint Add-ins</span></span>](develop-sharepoint-add-ins.md) 

 

 

