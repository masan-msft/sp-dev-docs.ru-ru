# <a name="determine-sharepoint-rest-service-endpoint-uris"></a>Как определить URI конечных точек службы REST в SharePoint
В этой статье представлены общие рекомендации по определению URI конечных точек REST в SharePoint с помощью подписей соответствующих API клиентской объектной модели.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

 **Перед началом работы**
 

-  [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [Навигация по структуре данных SharePoint, представленной в службе REST](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
**Дальнейшие действия**
 

-  [Использование операций запросов OData в запросах REST SharePoint](use-odata-query-operations-in-sharepoint-rest-requests)
    
 

## <a name="sharepoint-rest-endpoint-uri-structure"></a>Структура URI конечной точки REST в SharePoint

Чтобы иметь возможность доступа к ресурсу SharePoint с помощью службы REST, сначала необходимо определить конечную точку URI, которая указывает на этот ресурс. Когда возможно, URI для этих конечных точек REST близко имитирует подпись API ресурса в клиентской объектной модели SharePoint. Пример:
 

 
 *Метод клиентской объектной модели:* 
 

 
List.GetByTitle(listname).GetItems()
 

 
 *Конечная точка REST:* 
 

 
 `http://server/site/_api/lists/getbytitle('listname')/items`
 

 
Но в некоторых случаях URI конечной точки отличается от соответствующей подписи клиентской объектной модели для соответствия соглашениям REST или OData.
 

 
На приведенном ниже рисунке показана общая структура синтаксиса для URI конечных точек REST в SharePoint. 
 

 

**Структура синтаксиса URI REST в SharePoint**

 

 
![Синтаксис запроса REST SharePoint](../../images/SPF15Con_REST_OverallSyntax.png)
 
Синтаксис некоторых конечных точек для ресурсов SharePoint не соответствует этой структуре:
 

 

 

- Методы, в качестве параметров которых требуются сложные типы. 
    
    Если соответствующий метод клиентской объектной модели требует, чтобы в качестве параметров передавались сложные типы, конечная точка REST может отклоняться от этой структуры синтаксиса в связи с ограничениями REST.
    
 
- Статические методы и свойства. 
    
    Синтаксис конечных точек REST отличается от структуры синтаксиса для URI, представляющих статические методы и свойства.
    
 

## <a name="determine-sharepoint-rest-service-endpoints"></a>Как определить конечные точки службы REST в SharePoint

Чтобы создать конечную точку REST для ресурса SharePoint, выполните указанные ниже действия.
 

 

1. Начните со ссылки на службу REST:
    
     `http://server/site/_api`
    
 
2. Укажите соответствующую точку входа. Например:
    
     `http://server/site/_api/web`
    
 
3. Перейдите от точки входа к конкретным ресурсам, к которым нужно получить доступ. Это включает указание параметров для конечных точек, которые соответствуют методам в клиентской объектной модели. Например:
    
     `http://server/site/_api/web/lists/getbytitle('listname')`
    
 

### <a name="reference-the-sharepoint-rest-service-in-your-endpoint-uri"></a>Ссылка на службу REST SharePoint в URI конечной точки

Используйте `_api`, чтобы указать ссылку на службу REST SharePoint в URI конечной точки. Служба REST входит в состав веб-службы client.svc. Но чтобы упростить создание URI REST и сократить базовый путь к URI REST, служба REST использует `_api`, избавляя от необходимости явно ссылаться на веб-службу client.svc. Служба REST по-прежнему распознает и принимает URI, которые ссылаются на веб-службу client.svc. Например, вы можете использовать `http://server/site/_vti_bin/client.svc/web/lists` вместо `http://server/site/_api/web/lists`. Однако предпочтительней использовать `_api`. Максимальная длина URL-адреса составляет 256 символов, а `_api` сокращает базовый URI, оставляя в запасе больше символов для составления URL-адреса.
 

 

### <a name="specify-entry-points-for-the-sharepoint-rest-service"></a>Указание точек входа для службы REST SharePoint

Основные точки входа для службы REST представляют семейство веб-сайтов и сайт указанного контекста. Таким образом, эти точки входа соответствуют свойствам **ClientContext.Site** и **ClientContext.Web** клиентских объектных моделей.
 

 
Для доступа к определенному семейству веб-сайтов используйте следующую конструкцию:
 

 
 `http://server/site/_api/site`
 

 
Для доступа к определенному сайту используйте следующую конструкцию:
 

 
 `http://server/site/_api/web`
 

 
В этих примерах *server* представляет имя сервера, а *site* — имя определенного сайта или путь к нему.
 

 
Помимо `/site` и `/web`, служба REST включает несколько других точек доступа, которые позволяют разработчикам переходить к определенным компонентам. В приведенной ниже таблице перечислены эти точки доступа.
 

 


|**Область функций**|**Точка доступа**|
|:-----|:-----|
|Сайт|http:// _server/site_/_api/site|
|Интернет|http:// _server/site_/_api/web|
|Профили пользователей|http:// _server/site_/_api/SP.UserProfiles.PeopleManager|
|Поиск|http:// _server/site_/_api/search|

### <a name="navigate-to-the-specific-resources-you-want-to-access"></a>Переход к определенным ресурсам, к которым требуется получить доступ

С этой точки можно создавать более конкретные конечные точки REST, ''обходя" объектную модель, с использованием имен API клиентской объектной модели, разделенных знаком косой черты (/). В таблице ниже показаны примеры вызовов клиентских объектных моделей и эквивалентные им конечные точки. 
 

 


|**API клиентской объектной модели**|**Конечная точка REST**|
|:-----|:-----|
|ClientContext.Web.Lists|http:// _server_/ _site_/_api/web/lists|
|ClientContext.Web.Lists[guid]|http:// _server_/ _site_/_api/web/lists('_guid_')|
|ClientContext.Web.Lists.GetByTitle("Title")|http:// _server_/ _site_/_api/web/lists/getbytitle('_Title_')|
URI конечных точек указываются с учетом регистра. В примере из предыдущей таблицы используется метод `/getbytitle` — аналог метода **GetByTitle()** в службе REST.
 

 

## <a name="specify-parameters-in-rest-endpoint-uris"></a>Как указать параметры в URI конечных точек REST

SharePoint расширяет спецификацию OData, позволяя использовать скобки для указания параметров метода и значений индекса. Это предотвращает потенциальные проблемы из-за неоднозначности в URI, содержащих несколько параметров с одинаковым именем. Например, два следующих URI содержат параметры с одинаковым именем:
 

 
 `http://server/site/_api/web/lists/getByTitle('Announcements')/fields/getByTitle('Description')`
 

 
 `http://server/site/_api/web/lists('<guid>')/fields/getById('<guid>')`
 

 
Чтобы указать несколько параметров, включите параметр в формате "значение-имя" и разделите параметры запятыми. Например:
 

 
 `http://server/site/_api/web/getAvailableWebTemplates(lcid=1033, includeCrossLanguage=true)`
 

 
На приведенном ниже рисунке показан синтаксис параметров службы REST в SharePoint.
 

 

**Синтаксис параметров службы REST в SharePoint**

 

 
![Синтаксис параметров метода службы REST в SharePoint](../../images/SPF15Con_REST_parameterSyntax.png)
 

### <a name="complex-types-as-parameters-for-the-rest-service"></a>Сложные типы в качестве параметров для службы REST

Некоторые методы клиентской объектной модели принимают полезные данные больших размеров в качестве параметра. Для обеспечения паритета функциональности между конечными точками REST и соответствующими API клиентской объектной модели необходимо, чтобы конечные точки принимали параметр сложного типа. В таких случаях служба REST расширяет существующий протокол OData, позволяя этим конечным точкам REST принимать один параметр сложного типа. Это относится только к операциям **POST**, а сложный тип необходимо передавать в формате [Atom](http://www.odata.org/developers/protocols/atom-format#RepresentingComplexTypesProperties) или [JSON](http://www.odata.org/developers/protocols/json-format#RepresentingComplexTypeProperties) согласно стандартам OData.
 

 
Например, метод **ListCollection.Add** принимает в качестве параметра объект **Microsoft.SharePoint.Client.ListCreationInformation**. Чтобы добавить список на указанный сайт, создайте соответствующую конечную точку REST следующим образом:
 

 
 `http://server/site/_api/web/lists/add`
 

 
Затем передайте в тексте запроса сложный тип, отформатированный здесь с помощью JSON.
 

 



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


### <a name="using-parameter-aliases-in-rest-service-calls"></a>Использование псевдонимов параметров в вызовах службы REST

В OData можно передавать параметры в конечную точку SharePoint REST с помощью семантики псевдонимов параметров. При таком подходе значение параметра идентифицируется с псевдонимом в вызове параметра и в строке запроса URI указывается фактическое значение. Это позволяет поддерживать больше типов символов и единообразное форматирование, используя строку запроса.
 

 
Например, два приведенных ниже URI REST эквивалентны. 
 

 
 *Непосредственное указание значения параметра:* 
 

 
 `http://server/site/_api/web/applyWebTemplate("STS#0")`
 

 
 *Использование псевдонима параметра и указание фактического значения параметра в строке запроса URI:* 
 

 
 `http://server/site/_api/web/applyWebTemplate(title=@template)?@template="STS#0"`
 

 
Однако служба SharePoint REST не поддерживает передачу комплексных типов через псевдонимы параметров. Например, следующий URI, содержащий комплексный тип в качестве параметра, не поддерживается:
 

 
 `http://server/site/_api/userProfiles/People(7)/GetWorkplace(@address)?@address={"__metadata":{"type: "ODataDemo.Address"},"Street":"NE 228th", "City":"Sammamish","State":"WA","ZipCode":"98074","Country": "USA"}`
 

 

**Синтаксис присвоения псевдонима параметру службы REST в SharePoint**

 

 
![Синтаксис присвоения псевдонима параметру службы REST в SharePoint](../../images/SPF15Con_REST_parameterAliasSyntax.png)
 

 

 

### <a name="specifying-dictionaries-as-parameter-values"></a>Указание словарей в качестве значений параметров

Для конечных точек REST, которые соответствуют методам, принимающим в качестве параметров словари `Dictionary<String, String>`, словарь следует передавать в строке запроса в формате разделенных запятыми пар "имя-значение".
 

 

**Синтаксис службы REST для параметров словаря**

 

 
![Синтаксис службы REST для параметров словаря](../../images/SPF15Con_REST_parameterDictionarySyntax.png)
 
Словарь `Dictionary<String, object>` представлен как многозначный объект с именем KeyedPropertyValue, содержащий следующие строковые свойства:
 

 

 

-  **Key**. Ключ многозначного объекта.
    
 
-  **Value**. Значение объекта.
    
 
-  **ValueType**. Тип значения объекта. Для простых типов, которые соответствуют существующим типам модели данных с использованием сущностей (EDM), служба REST возвращает соответствующую строку типа EDM, например "Edm.String". В противном случае служба REST возвращает тип значения, возвращенный функцией **Type.ToString**.
    
 

### <a name="specifying-parameter-values-in-the-query-string"></a>Указание значений параметров в строке запроса

Если URI REST завершается вызовом метода, с помощью синтаксиса строки запроса можно указать значения параметров метода. Например:
 

 
 `http://<server>/<site>/_api/web/applyWebTemplate?template="STS#0"`
 

 
На приведенном ниже рисунке показан синтаксис службы REST для параметров в строке запроса.
 

 

**Синтаксис службы REST для параметров в строке запроса**

 

 
![Синтаксис службы REST для параметров в строке запроса](../../images/SPF15Con_REST_parameterQuerySyntax.png)
 

 

 

## <a name="specifying-static-methods-and-properties-as-rest-service-uris"></a>Указание статических методов и свойств в качестве URI службы REST

Для создания URI, соответствующих статическим методам или свойствам, используйте имя соответствующего API из объектной модели ECMAScript, начиная с объявления пространства имен и использования точечной нотации. Например, [SP.Utilities.Utility.getImageUrl(imageName)](http://msdn.microsoft.com/ru-ru/library/ee658947.aspx) в клиентской объектной модели ECMAScript имеет следующий аналог в службе REST:
 

 
 `http://server/site/_api/SP.Utilities.Utility.getImageUrl('imageName')`
 

 
Однако к статическим свойствам возможен только прямой доступ, и их не разрешается указывать в составе более длинных URI. Например, прямой доступ к методу **SP.Utility.AssetsLibrary** в REST можно получить следующим образом:
 

 
 `http://server/site/_api/SP.Utility.assetsLibrary/id`
 

 
При этом не допускается использовать расположение ресурса в качестве параметра для более сложного URI, как показано в следующем примере:
 

 
 `http://server/site/_api/getList(~SP.Utility/assetsLibrary/id)`
 

 
На приведенном ниже рисунке показан синтаксис статического элемента для службы REST в SharePoint.
 

 

**Синтаксис статического элемента для службы REST в SharePoint**

 

 
![Синтаксис службы REST для параметров в строке запроса](../../images/SPF15Con_REST_parameterQuerySyntax.png)
 

 

 

## <a name="next-steps"></a>Дальнейшие действия

Служба SharePoint REST поддерживает широкий набор операторов строки запроса OData, позволяющих выбирать, фильтровать и упорядочивать данные, запрошенные у конечной точки. 
 

 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-2013-rest-service)
    
 
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-2013-rest-endpoints)
    
 
-  [Работа со списками и элементами списков в интерфейсе REST](working-with-lists-and-list-items-with-rest)
    
 
-  [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest)
    
 
-  [Навигация по структуре данных SharePoint, представленной в службе REST](navigate-the-sharepoint-data-structure-represented-in-the-rest-service)
    
 
-  [Использование операций запросов OData в запросах REST SharePoint](use-odata-query-operations-in-sharepoint-rest-requests)
    
 
-  [Справочные материалы и примеры по REST API](http://msdn.microsoft.com/library/rest-api-reference-and-samples%28Office.15%29.aspx)
    
 
-  [Синхронизация элементов SharePoint с помощью службы REST](synchronize-sharepoint-items-using-the-rest-service)
    
 
-  [Получение версий элементов списков и документов с помощью значений ETag в службе REST](http://msdn.microsoft.com/library/5f7e0579-46b7-44ab-b3b4-cdbc622dcd98%28Office.15%29.aspx)
    
 

 

 

