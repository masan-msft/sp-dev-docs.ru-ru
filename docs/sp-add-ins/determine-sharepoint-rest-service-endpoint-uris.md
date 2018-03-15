---
title: "Определение URI конечных точек службы REST в SharePoint"
description: "Рекомендации по определению URI конечных точек REST в SharePoint на основе подписей соответствующих API в клиентской объектной модели."
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 388f9dccfd1093b2db4ed81e53bedf6b38af778c
ms.sourcegitcommit: 202dd467c8e5b62c6469808226ad334061f70aa2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="determine-sharepoint-rest-service-endpoint-uris"></a>Определение URI конечных точек службы REST в SharePoint

**Перед началом работы**

- [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [Навигация по структуре данных SharePoint, представленной в службе REST](navigate-the-sharepoint-data-structure-represented-in-the-rest-service.md)

**Дальнейшие действия**

- [Использование операций запросов OData в запросах REST SharePoint](use-odata-query-operations-in-sharepoint-rest-requests.md)

## <a name="sharepoint-rest-endpoint-uri-structure"></a>Структура URI конечной точки REST в SharePoint

Чтобы иметь возможность доступа к ресурсу SharePoint с помощью службы REST, сначала необходимо определить конечную точку URI, которая указывает на этот ресурс. Когда возможно, URI для этих конечных точек REST близко имитирует подпись API ресурса в клиентской объектной модели SharePoint. Пример:

*Метод клиентской объектной модели:* 
 
`List.GetByTitle(listname).GetItems()`
 
*Конечная точка REST:* 
 
`http://server/site/_api/lists/getbytitle('listname')/items`
 
Но в некоторых случаях URI конечной точки отличается от соответствующей подписи клиентской объектной модели для соответствия соглашениям REST или OData.

На приведенном ниже рисунке показана общая структура синтаксиса для URI конечных точек REST в SharePoint. 

**Структура синтаксиса URI REST в SharePoint**

![Синтаксис запроса REST SharePoint](../images/SPF15Con_REST_OverallSyntax.png)

<br/>
 
Синтаксис некоторых конечных точек для ресурсов SharePoint не соответствует этой структуре:

- **Методы, параметры которых должны быть сложными типами.** Если соответствующий метод клиентской объектной модели требует, чтобы в качестве параметров передавались сложные типы, конечная точка REST может отклоняться от этой структуры синтаксиса в связи с ограничениями REST.
 
- **Статические методы и свойства.** Синтаксис конечных точек REST отличается от структуры синтаксиса для URI, представляющих статические методы и свойства.

## <a name="determine-sharepoint-rest-service-endpoints"></a>Как определить конечные точки службы REST в SharePoint

Чтобы создать конечную точку REST для ресурса SharePoint, выполните указанные ниже действия.

1. Начните со ссылки на службу REST:
    
     `http://server/site/_api`

2. Укажите соответствующую точку входа. Например:
    
     `http://server/site/_api/web`
 
3. Перейдите от точки входа к конкретным ресурсам, к которым нужно получить доступ. Это включает указание параметров для конечных точек, которые соответствуют методам в клиентской объектной модели. Например:
    
     `http://server/site/_api/web/lists/getbytitle('listname')`
    

### <a name="reference-the-sharepoint-rest-service-in-your-endpoint-uri"></a>Ссылка на службу REST SharePoint в URI конечной точки

Используйте `_api`, чтобы указать ссылку на службу REST SharePoint в URI конечной точки. Служба REST входит в состав веб-службы client.svc. Но чтобы упростить создание URI REST и сократить базовый путь к URI REST, служба REST использует `_api`, избавляя от необходимости явно ссылаться на веб-службу client.svc. 

Служба REST по-прежнему распознает и принимает URI, которые ссылаются на веб-службу client.svc. Например, вы можете использовать `http://server/site/_vti_bin/client.svc/web/lists` вместо `http://server/site/_api/web/lists`. Однако лучше использовать `_api`. Максимальная длина URL-адреса составляет 256 символов, а `_api` сокращает базовый URI, оставляя в запасе больше символов для составления URL-адреса.

### <a name="specify-entry-points-for-the-sharepoint-rest-service"></a>Указание точек входа для службы REST SharePoint

Основные точки входа для службы REST представляют семейство веб-сайтов и сайт указанного контекста. Таким образом, эти точки входа соответствуют свойствам **ClientContext.Site** и **ClientContext.Web** клиентских объектных моделей.

Для доступа к определенному семейству веб-сайтов используйте следующую конструкцию (*server* — имя сервера, а *site* — имя сайта или путь к нему):

`http://server/site/_api/site`

Для доступа к определенному сайту используйте следующую конструкцию:

`http://server/site/_api/web`

Помимо `/site` и `/web`, служба REST включает несколько других точек доступа, которые позволяют разработчикам переходить к определенным компонентам. В приведенной ниже таблице перечислены эти точки доступа.

|**Область функций**|**Точка доступа**|
|:-----|:-----|
|Сайт|`http://server/site/_api/site`|
|Интернет|`http://server/site/_api/web`|
|Профиль пользователя|`http://server/site/_api/SP.UserProfiles.PeopleManager`|
|Поиск|`http://server/site/_api/search`|

### <a name="navigate-to-the-specific-resources-you-want-to-access"></a>Переход к определенным ресурсам, к которым требуется получить доступ

Здесь вы можете создать более конкретные конечные точки REST, "обходя" объектную модель, с использованием имен API клиентской объектной модели, разделенных знаком косой черты (/). Ниже показаны примеры вызовов клиентской объектной модели и аналогичная конечная точка REST. 

|**API клиентской объектной модели**|**Конечная точка REST**|
|:-----|:-----|
|ClientContext.Web.Lists|`http://server/site/_api/web/lists`|
|ClientContext.Web.Lists[guid]|`http://server/site/_api/web/lists('<guid>')`|
|ClientContext.Web.Lists.GetByTitle("Title")|`http://server/site/_api/web/lists/getbytitle('<Title>')`|
URI конечных точек указываются с учетом регистра. В примере из предыдущей таблицы используется метод `/getbytitle`, который представляет собой аналог метода **GetByTitle()** в службе REST.

## <a name="specify-parameters-in-rest-endpoint-uris"></a>Указание параметров в URI конечных точек REST

SharePoint расширяет спецификацию OData, позволяя использовать скобки для указания параметров метода и значений индекса. Это предотвращает потенциальные проблемы из-за неоднозначности в URI, содержащих несколько параметров с одинаковым именем. Например, два следующих URI содержат параметры с одинаковым именем:

`http://server/site/_api/web/lists/getByTitle('Announcements')/fields/getByTitle('Description')`

`http://server/site/_api/web/lists('<guid>')/fields/getById('<guid>')`
 
<br/>
 
Чтобы указать несколько параметров, включите параметр в формате "значение-имя" и разделите параметры запятыми. Например:

`http://server/site/_api/web/getAvailableWebTemplates(lcid=1033, includeCrossLanguage=true)`
 
<br/>
 
На приведенном ниже рисунке показан синтаксис параметров службы REST в SharePoint.

**Синтаксис параметров службы REST в SharePoint**

![Синтаксис параметров метода службы REST в SharePoint](../images/SPF15Con_REST_parameterSyntax.png)

<br/>

### <a name="complex-types-as-parameters-for-the-rest-service"></a>Сложные типы в качестве параметров для службы REST

Некоторым методам в клиентской объектной модели в качестве параметра требуются большие полезные данные. Чтобы поддерживалось равенство функциональности конечных точек REST с соответствующими API клиентской объектной модели, конечные точки должны принимать в качестве параметра комплексный тип. В этих случаях служба REST расширяет существующий протокол OData, чтобы разрешить этим конечным точкам REST принимать единственный комплексный тип в качестве параметра. Это применяется только к операциям **POST**, и вам необходимо передать комплексный тип в формат  [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties) или [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties) соответственно стандартам OData.

Например, метод **ListCollection.Add** принимает в качестве параметра объект **Microsoft.SharePoint.Client.ListCreationInformation**. Чтобы добавить список на указанный сайт, создайте соответствующую конечную точку REST следующим образом:

`http://server/site/_api/web/lists/add`
 
После этого передайте в теле запроса сложный тип, отформатированный здесь с помощью JSON.

```
{ "d" : {
   "results": {
     "__metadata": {
       "type": "SP.ListCreationInformation"
     }, 
     "CustomSchemaXml": "…large payload…/", 
     "Description": "desc", 
     "DocumentTemplateType": "1", 
     "TemplateType": "101", 
     "Title": "Announcements"
   }
} 
}

```

<br/>

### <a name="using-parameter-aliases-in-rest-service-calls"></a>Использование псевдонимов параметров в вызовах службы REST

В OData можно передавать параметры в конечную точку SharePoint REST с помощью семантики псевдонимов параметров. При таком подходе значение параметра идентифицируется с псевдонимом в вызове параметра и в строке запроса URI указывается фактическое значение. Это позволяет поддерживать больше типов символов и единообразное форматирование, используя строку запроса.

Например, два приведенных ниже URI REST эквивалентны. 

*Непосредственное указание значения параметра:*<br/> 
`http://server/site/_api/web/applyWebTemplate("STS#0")`

*Использование псевдонима параметра и указание фактического значения параметра в строке запроса URI:*<br/> 
`http://server/site/_api/web/applyWebTemplate(title=@template)?@template="STS#0"`

Однако служба SharePoint REST не поддерживает передачу комплексных типов через псевдонимы параметров. Например, следующий URI, содержащий комплексный тип в качестве параметра, не поддерживается:

`http://server/site/_api/userProfiles/People(7)/GetWorkplace(@address)?@address={"__metadata":{"type: "ODataDemo.Address"},"Street":"NE 228th", "City":"Sammamish","State":"WA","ZipCode":"98074","Country": "USA"}`
 
**Синтаксис присвоения псевдонима параметру службы REST в SharePoint**

![Синтаксис присвоения псевдонима параметру службы REST в SharePoint](../images/SPF15Con_REST_parameterAliasSyntax.png)

<br/>

### <a name="specifying-dictionaries-as-parameter-values"></a>Указание словарей в качестве значений параметров

Для конечных точек REST, которые соответствуют методам, принимающим в качестве параметров словари `Dictionary<String, String>`, словарь следует передавать в строке запроса в формате разделенных запятыми пар "имя-значение".

**Синтаксис службы REST для параметров словаря**

![Синтаксис службы REST для параметров словаря](../images/SPF15Con_REST_parameterDictionarySyntax.png)

<br/>

Объект `Dictionary<String, object>` представлен как многозначный объект с именем KeyedPropertyValue, содержащий следующие строковые свойства:

- **Key**. Ключ многозначного объекта.
- **Value**. Значение объекта.
- **ValueType**. Тип значения объекта. Для простых типов, которые соответствуют существующим типам модели данных с использованием сущностей (EDM), служба REST возвращает соответствующую строку типа EDM, например "Edm.String". В противном случае служба REST возвращает тип значения, возвращенный функцией **Type.ToString**.

### <a name="specifying-parameter-values-in-the-query-string"></a>Указание значений параметров в строке запроса

Если URI REST завершается вызовом метода, с помощью синтаксиса строки запроса можно указать значения параметров метода. Например:

`http://server/site/_api/web/applyWebTemplate?template="STS#0"`
 
Ниже показан синтаксис службы REST для параметров в строке запроса.

**Синтаксис службы REST для параметров в строке запроса**

![Синтаксис службы REST для параметров в строке запроса](../images/SPF15Con_REST_parameterQuerySyntax.png)
 
<br/>

## <a name="specify-static-methods-and-properties-as-rest-service-uris"></a>Указание статических методов и свойств в виде URI службы REST

Для создания URI, соответствующих статическим методам или свойствам, используйте имя соответствующего API из объектной модели ECMAScript, начиная с объявления пространства имен и использования точечной нотации. Например, [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/ru-RU/library/ee658947.aspx) в клиентской объектной модели ECMAScript имеет следующий аналог в службе REST:

`http://server/site/_api/SP.Utilities.Utility.getImageUrl('imageName')`

Однако к статическим свойствам возможен только прямой доступ, и их нельзя указывать в составе более длинных URI. Например, прямой доступ к методу **SP.Utility.AssetsLibrary** в REST можно получить следующим образом:

`http://server/site/_api/SP.Utility.assetsLibrary/id`

При этом нельзя использовать расположение ресурса в качестве параметра для более сложного URI, как показано в примере ниже:

`http://server/site/_api/getList(~SP.Utility/assetsLibrary/id)`
 
Ниже показан синтаксис статического элемента для службы REST в SharePoint.

**Синтаксис статического элемента для службы REST в SharePoint**

![Синтаксис службы REST для параметров в строке запроса](../images/SPF15Con_REST_parameterQuerySyntax.png)
 
<br/>

Служба SharePoint REST поддерживает широкий набор операторов строки запроса OData, позволяющих выбирать, фильтровать и упорядочивать данные, запрошенные у конечной точки. Дополнительные сведения см. в статье [Использование операций запросов OData в запросах SharePoint REST](use-odata-query-operations-in-sharepoint-rest-requests.md).

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [Справочные материалы по REST API и примеры](https://msdn.microsoft.com/library)
- [Получение версий списков документов с помощью значений ETag в службе REST](working-with-lists-and-list-items-with-rest.md#using-etag-values-to-determine-document-and-list-item-versioning)  
- [Материалы по OData](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)
 

 

