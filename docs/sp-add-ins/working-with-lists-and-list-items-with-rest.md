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
# <a name="working-with-lists-and-list-items-with-rest"></a>Работа со списками и элементами списков с использованием REST

> [!TIP] 
> Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).

## <a name="prerequisites"></a>Необходимые компоненты

В этой статье предполагается, что вы уже ознакомились со статьями [Знакомство со службой REST для SharePoint](get-to-know-the-sharepoint-rest-service.md) и [Выполнение базовых операций с использованием конечных точек REST в SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md). Здесь не представлены фрагменты кода.
 

<a name="RetrieveLists"> </a> 

## <a name="retrieving-lists-and-list-properties-with-rest"></a>Получение списков и свойств списков с помощью REST

В следующем примере показано, как **получить** определенный список, если вы знаете его GUID.

```
url: http://site url/_api/web/lists(guid'list GUID'),
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```


> [!NOTE] 
> Если вы хотите получить отклик в формате JSON, укажите `application/json;odata=verbose` в заголовке `accept`. 

> Если вы хотите получить отклик в формате Atom, укажите `application/atom+xml` в заголовке `accept`.
 
<br/>

В следующем примере показано, как **получить** определенный список, если вы знаете его название.

```
url: http://site url/_api/web/lists/GetByTitle('Test')
method: GET
Headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

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
> Свойство **ListItemEntityTypeFullName** (в предыдущем примере — **SP.Data.ProjectPolicyItemListItem**) особенно важно, если вы хотите создать и обновить элементы списка. Это значение должно передаваться в виде свойства **type** в тексте HTTP-запроса каждый раз, когда вы создаете и обновляете элементы списка.
 
<br/>

<a name="WorkLists"> </a>

## <a name="working-with-lists-by-using-rest"></a>Работа со списками с помощью REST

В приведенном ниже примере показано, как **создать** список.

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

В приведенном ниже примере показано, как **обновить** список, используя метод **MERGE**.

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

В следующем примере показывается, как **создать** **настраиваемое поле** для списка.

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

В приведенном ниже примере показано, как **удалить** список.

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

<a name="ListItems"> </a>

## <a name="working-with-list-items-by-using-rest"></a>Работа с элементами списка с помощью REST

### <a name="retrieve-all-list-items"></a>Получение всех элементов списка

Ниже показано, как **получить** все элементы списка.
 
> [!NOTE] 
> Параметр запроса OData $skip не работает при запрашивании элементов списка. Обычно вместо него можно использовать параметр [$skiptoken](http://msdn.microsoft.com/library/4dda9434-c2c5-4577-8e01-7bf9e822d90a.aspx).

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

### <a name="retrieve-specific-list-item"></a>Получение определенного элемента списка

Ниже показано, как **получить** определенный элемент списка.

```
url: http://site url/_api/web/lists/GetByTitle('Test')/items(item id)
method: GET
headers:
    Authorization: "Bearer " + accessToken
    accept: "application/json;odata=verbose" or "application/atom+xml"

```

<br/>

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

### <a name="create-list-item"></a>Создание элемента списка

Ниже показано, как **создать** элемент списка.
 
> [!NOTE] 
> [!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.
 
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

### <a name="create-list-item-in-a-folder"></a>Создание элемента списка в папке

Создайте элемент списка в папке.

```text
POST /_api/web/lists/GetByTitle('Test')/AddValidateUpdateItemUsingPath
```

#### <a name="uri-parameters"></a>Параметры URI

Нет

#### <a name="request-headers"></a>Заголовки запроса

| Заголовок | Значение |
|--------|-------|
|Accept|application/json;odata=nometadata|
|Content-Type|application/json;odata=nometadata|
|x-requestdigest|Подходящий дайджест для текущего сайта|

#### <a name="request-body"></a>Тело запроса

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

| Свойство | Описание |
|----------|-------|
|listItemCreateInfo|Информация о списке и папке, где необходимо создать элемент|
|listItemCreateInfo.FolderPath.DecodedUrl|Абсолютный URL-адрес папки, где необходимо создать элемент|
|listItemCreateInfo.UnderlyingObjectType|Тип элемента, который необходимо создать. Дополнительные сведения см. в разделе [https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.filesystemobjecttype(v=office.14).aspx](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.client.filesystemobjecttype(v=office.14).aspx).|
|formValues|Массив имен полей и значений, которые необходимо присвоить новому элементу|
|bNewDocumentUpdate|Установите значение `false`, чтобы создать элемент списка|

#### <a name="responses"></a>Ответы

| Имя   | Тип    |Описание|
|--------|---------|-----------|
|200 OK  | Boolean |Успешно    |

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

Свойство `value` содержит список свойств, заданных при создании элемента списка.

### <a name="update-list-item"></a>Обновление элемента списка

Ниже показано, как **обновить** элемент списка.
 
> [!NOTE] 
> [!Примечание] Для выполнения этой операции вам необходимо знать свойство **ListItemEntityTypeFullName** списка и передать его как значение **type** в тексте запроса HTTP.

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

### <a name="delete-list-item"></a>Удаление элемента списка

Ниже показано, как **удалить** элемент списка.

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

<a name="Etag"> </a>

## <a name="using-etag-values-to-determine-document-and-list-item-versioning"></a>Использование значений ETag для определения версий документов и элементов списков

Служба SharePoint REST, работающая по [стандарту OData](http://www.odata.org/developers/protocols/operations), использует [значения HTML ETag для управления версиями](http://www.odata.org/developers/protocols/operations#ConcurrencycontrolandETags) списков SharePoint и их элементов. Чтобы проверить версию элемента при выполнении запроса **PUT**, **MERGE** или **DELETE**, укажите значение **ETag** в заголовке HTTP-запроса **If-Match**.

Если **ETag**, который вы указываете в вашем запросе, не соответствует **ETag** документа или элемента списка на сервере, служба REST возвращает исключение 412 с помощью спецификации OData.

- Чтобы принудительно переписать элемент независимо от версии, задайте **ETag** значение **"*"**.
    
- Если не указать **ETag**, SharePoint переписывает элемент независимо от версии.
    
 
В SharePoint значения ETag применяются только к спискам SharePoint и элементам списков.
 
## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
- [SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST](https://docs.microsoft.com/ru-RU/sharepoint/dev/sp-add-ins/working-with-folders-and-files-with-rest)
- [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint.md)
- [Справочные материалы по REST API и примеры](https://msdn.microsoft.com/library)
- [Материалы по OData](get-to-know-the-sharepoint-rest-service.md#odata-resources)  
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md) 

 

 

