---
title: "Работа со списками и элементами списков в службе REST"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ec63b7dcf294e4a6248ca5c6014b6807f116f655
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="working-with-lists-and-list-items-with-rest"></a>Работа со списками и элементами списков в службе REST
Узнайте, как выполнять базовые операции CRUD (создание, чтение, обновление и удаление) со списками и элементами списков с помощью интерфейса REST в SharePoint.
 
 **Совет.** Служба REST в SharePoint Online (а также в локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Создание пакетного запроса с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).
 
## <a name="prerequisites"></a>Необходимые условия
В этой статье предполагается, что вы уже знакомы с темами [Знакомство со службой REST для SharePoint](get-to-know-the-sharepoint-rest-service.md) и [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md). Здесь фрагменты кода не предоставлены.

## <a name="retrieving-lists-and-list-properties-with-rest"></a>Получение списков и свойств списков с помощью REST
<a name="RetrieveLists"> </a> В следующем примере показано, как **получить** определенный список, если вы знаете его GUID.

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
> [!NOTE]
> Укажите `application/json;odata=verbose` в заголовке `accept`, если хотите получить отклик в формате JSON. Укажите `application/atom+xml` в заголовке `accept`, если хотите получить отклик в формате Atom.
 
В следующем примере показано, как **получить** определенный список, если вы знаете его название.

```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```
Ниже показан пример свойств списка, которые возвращаются при запросе типа контента XML.

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
> Свойство **ListItemEntityTypeFullName** (в предыдущем примере — **SP.Data.ProjectPolicyItemListItem**) особенно важно, если вы хотите создать и обновить элементы списка. Это значение должно передаваться как свойство **type** в метаданных тела HTTP-запроса каждый раз, когда вы создаете и обновляете элементы списка.

## <a name="working-with-lists-by-using-rest"></a>Работа со списками с помощью REST
<a name="WorkLists"> </a> В следующем примере показано, как **создать** список.

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

В следующем примере показано, как **обновить** список, используя метод **MERGE**.

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
В следующем примере показано, как **создать** **настраиваемое поле** для списка.

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

В следующем примере показано, как **удалить** список.

```
url: http://site url/_api/web/lists(guid'list GUID')
method: POST
Headers: 
    Authorization: "Bearer " + accessToken
    X-RequestDigest: form digest value
    IF-MATCH: etag or "*"
    X-HTTP-Method: DELETE

```

## <a name="working-with-list-items-by-using-rest"></a>Работа с элементами списка с помощью REST
<a name="ListItems"> </a> В следующем примере показано, как **получить** все элементы списка.
 
> [!NOTE]
> Параметр запроса OData $skip не работает при запрашивании элементов списка. Вместо него в большинстве случаев можете использовать параметр [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx).

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

В следующем примере показано, как **получить** определенный элемент списка.

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

Ниже показан пример свойств элементов списка, которые возвращаются при запросе типа контента XML.
 
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

В следующем примере показано, как **создать** элемент списка.

> [!NOTE]
> Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в теле HTTP-запроса.

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

В следующем примере показано, как **обновить** элемент списка.

> [!NOTE]
> Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в теле HTTP-запроса.

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

В следующем примере показано, как **удалить** элемент списка.

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: POST
headers:
    Authorization: "Bearer " + accessToken
     X-RequestDigest: form digest value
    "IF-MATCH": etag or "*"
    "X-HTTP-Method":"DELETE"

```

## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a>Использование значений ETag для определения версий документов и элементов списков
<a name="Etag"> </a> Служба SharePoint REST, работающая по [стандарту OData](http://www.odata.org/developers/protocols/operations), использует [значения HTML ETag для управления версиями](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) списков SharePoint и их элементов. Чтобы проверить версию элемента при выполнении запроса **PUT**, **MERGE** или **DELETE**, укажите значение **ETag** в заголовке HTTP-запроса **If-Match**.
 
Если указанное значение **ETag** не соответствует значению **ETag** документа или элемента списка на сервере, служба REST возвращает исключение 412 согласно спецификации OData.
 
- Чтобы перезаписать элемент независимо от версии, установите значение **ETag** **"*"**.
    
- Если вы не укажете значение **ETag**, SharePoint перезапишет элемент независимо от версии.
    
В SharePoint значения ETag применяются только к спискам SharePoint и элементам списков.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md)
-  [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md)
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [SharePoint 2013: выполнение базовых операций с файлами и папками с помощью REST](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [Выполнение вызовов REST при помощи C# и JavaScript для SharePoint 2013](http://www.microsoft.com/resources/msdn/en-us/office/media/video/video.mdl?cid=sdc&amp;from=mscomsdc&amp;VideoID=4e4cc094-ff69-405b-852f-2ac7c41293c5)
-  [Протокол OData](http://www.odata.org/)
-  [OData: формат JSON](http://www.odata.org/documentation/odata-version-2-0/json-format/)
