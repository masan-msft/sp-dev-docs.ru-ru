---
title: "Выполнение базовых операций с использованием конечных точек REST SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: cb954660d47ab7cf4c3b71921843f5826c3be14d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="complete-basic-operations-using-sharepoint-rest-endpoints"></a>Выполнение базовых операций с использованием конечных точек REST SharePoint
Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint.

## <a name="developing-with-the-sharepoint-client-apis-and-rest"></a>Разработка с помощью клиентских интерфейсов API и REST для SharePoint
<a name="ClientAPIs"> </a> Вы можете выполнять базовые операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса передачи репрезентативного состояния (REST), предоставляемого средой SharePoint. Интерфейс REST предоставляет доступ ко всем сущностям и операциям SharePoint, доступным в других клиентских API SharePoint. Одно из преимуществ использования REST состоит в том, что вам не требуется добавлять ссылки на библиотеки и клиентские сборки SharePoint. Вместо этого соответствующим конечным точкам отправляются HTTP-запросы на получение или обновление сущностей SharePoint, таких как веб-сайты, списки и элементы списков. Подробные сведения об интерфейсе REST SharePoint и его архитектуре см. в статье [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md).
 
Больше о работе с базовыми сущностями можно узнать в статьях SharePoint [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md) и [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md). С примерами выполнения многих из этих операций в контексте веб-приложения ASP.NET, написанного на C#, можно ознакомиться в репозитории  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations.md).
 
Дополнительные сведения о наборах API, доступных на платформе SharePoint, см. в статье [Выбор правильного набора API в SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx). Сведения о том, как использовать другие клиентские API, см. в статьях [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx), [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx) и [Создание приложений Windows Phone, обращающихся к SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163228.aspx).
 

## <a name="http-operations-in-sharepoint-rest-services"></a>Операции HTTP в службах REST SharePoint
<a name="HTTPOps"> </a> Конечные точки в службе REST SharePoint соответствуют типам и элементам клиентских объектных моделей SharePoint. С помощью HTTP-запросов вы можете использовать эти конечные точки REST для выполнения типичных операций CRUD (**Create**, **Read**, **Update** и **Delete**) с сущностями SharePoint, такими как списки и сайты. 
 
Как правило, конечные точки, представляющие операции **Read**, сопоставляются с HTTP-командами **GET**. Конечные точки, представляющие операции обновления, сопоставляются с HTTP-командами **POST**, а конечные точки, представляющие операции обновления или вставки, — с HTTP-командами **PUT**.
 
В SharePoint для создания таких сущностей, как списки и сайты, используется команда **POST**. Служба REST SharePoint поддерживает отправку команд **POST**, содержащих определения объектов для конечных точек, представляющих коллекции. Например, вы можете отправить команду **POST**, включающую определение нового объекта списка в формате ATOM, на следующий URL-адрес, чтобы создать список SharePoint:
 
 ```
 http://<site url>/_api/web/lists
 ```

В операциях **POST** для всех необязательных свойств заданы значения по умолчанию. При попытке задать в операции **POST** свойство, доступное только для чтения, служба возвращает исключение.
  
Для обновления существующих объектов SharePoint используйте операции **PUT** и **MERGE**. Все конечные точки службы, представляющие операцию **set** для свойства объекта, поддерживают как запросы **PUT**, так и запросы **MERGE**. Для запросов **MERGE** необязательно задавать свойства. Все свойства, не заданные явно, сохраняют текущие значения. Однако в командах **PUT** для всех свойств, не заданных явно, задаются значения по умолчанию. Кроме того, если указать не все обязательные свойства в операции обновления объекта при использовании HTTP-команд **PUT**, служба REST вернет исключение.
  
Используйте команду HTTP **DELETE** для URL-адреса определенной конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для повторно обрабатываемых объектов (например, списков, файлов и элементов списков) это приведет к выполнению операции **Recycle**.
 
## <a name="reading-data-with-the-sharepoint-rest-interface"></a>Считывание данных с помощью интерфейса REST SharePoint
<a name="ReadingData"> </a> Чтобы использовать возможности REST, встроенные в SharePoint, необходимо создать HTTP-запрос RESTful, используя стандарт OData, соответствующий нужному API клиентской объектной модели. Каждая сущность SharePoint представляется в конечной точке на целевом сайте SharePoint, а ее метаданные представляются в формате XML или JSON. Вы можете выполнять HTTP-запросы на любом языке, в том числе JavaScript и C#.
 
Чтобы прочитать данные из конечной точки REST, необходимо знать URL-адрес конечной точки и представление OData сущности SharePoint, которая предоставляется в этой конечной точке. Например, чтобы получить все списки на определенном сайте SharePoint, нужно создать запрос **GET** для `http://<site url>/_api/web/lists`. Вы можете перейти к этому URL-адресу в браузере и посмотреть на полученный код XML. Создавая запрос в коде, вы можете указать, в каком формате вы будете получать списки OData: XML или JSON.
 
Приведенный ниже код на C# иллюстрирует создание запроса **GET**, который возвращает представление JSON для всех списков на сайте с помощью JQuery. Предполагается, что у вас есть действительный маркер доступа OAuth, хранящийся в переменной **accessToken**. Маркер доступа не нужен, если вы выполняете вызов с сайта надстройки, как в надстройке, размещенной в SharePoint. Обратите внимание, что невозможно получить маркер доступа из кода, который выполняется в браузерном клиенте. Маркер доступа необходимо получить из кода, выполняемого на сервере. В статьях [Поток маркеров контекста OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) и [Поток кода аутентификации OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) рассказывается, как получить маркер доступа.

```
HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", 
  "Bearer " + accessToken);
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();

```

Этот запрос будет выглядеть немного по-другому, если вы создаете надстройку на JavaScript, но с использованием междоменной библиотеки SharePoint. В этом случае предоставлять маркер доступа не нужно. Ниже показано, как выглядел бы запрос, если бы вы использовали междоменную библиотеку и хотели получить представление списков OData в формате XML, а не JSON. Так как по умолчанию отклик представлен в формате Atom, добавлять заголовок **Accept** необязательно. Дополнительные сведения об использовании междоменной библиотеки см. в статье [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx).
 
```javascript
var executor = new SP.RequestExecutor(appweburl);
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/lists?@target='" +
            hostweburl + "'",
        method: "GET",
        success: successHandler,
        error: errorHandler
    }
);
```

В следующем примере показано, как запросить представление JSON всех списков сайта, используя C#. Предполагается, что у вас есть маркер доступа OAuth, который вы храните в переменной  `accessToken`.

```
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();

```

### <a name="getting-properties-that-arent-returned-with-the-resource"></a>Получение свойств, не возвращаемых с ресурсом
<a name="NavigationProperties"> </a> Значения многих свойств возвращаются при получении ресурса, но для некоторых свойств необходимо отправить запрос **GET** непосредственно конечной точке свойства. Это типично для свойств, представляющих сущности SharePoint.
 
В приведенном ниже примере показано, как получить свойство, добавив его имя в конечную точку ресурса. В примере значение свойства **Author** получается от ресурса **File**.
 
 ```
 http:// _<site url>_/_api/web/getfilebyserverrelativeurl('/ _<folder name>_/ _<file name>_')/author
 ```

Чтобы получить результаты в формате JSON, включите в запрос заголовок **Accept** со значением `"application/json;odata=verbose"`.

## <a name="writing-data-by-using-the-rest-interface"></a>Запись данных с помощью интерфейса REST
<a name="WritingData"> </a>

Вы можете создавать и обновлять сущности SharePoint, создавая HTTP-запросы с поддержкой RESTful для соответствующих конечных точек, как и при чтении данных. Одно из ключевых отличий заключается в использовании запроса **POST**. При обновлении сущностей вы также передаете метод **PUT** или **MERGE** HTTP-запроса, добавляя один из этих терминов в заголовки запроса в качестве значения ключа **X-HTTP-Method**. Метод **MERGE** обновляет только указанные свойства сущности, в то время как метод **PUT** заменяет существующую сущность на новую, которая указана в тексте запроса **POST**. Для удаления объекта используйте метод **DELETE**. При создании или обновлении сущности необходимо указать ее представление OData в тексте HTTP-запроса.
 
Еще одна важная особенность создания, обновления и удаления сущностей SharePoint заключается в том, что если вы не используете OAuth для авторизации своих запросов, то для выполнения этих операций потребуется передавать значение дайджеста формы запроса с сервера в качестве значения заголовка **X-RequestDigest**. Чтобы получить это значение, выполните запрос **POST** с пустым текстом к конечной точке `http://<site url>/_api/contextinfo` и извлеките значение узла `d:FormDigestValue` в XML-коде, возвращаемом конечной точкой **contextinfo**. В приведенном ниже примере показан HTTP-запрос к конечной точке **contextinfo**, написанный на C#.
 
```
HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/contextinfo");
endpointRequest.Method = "POST";
endpointRequest.Accept = "application/json;odata=verbose";
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();
  
```

Если вы используете поток проверки подлинности и авторизации, описанный в статье [Авторизация и проверка подлинности для надстроек в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp142384.aspx), вам не потребуется включать дайджест в запросы.
 
Если вы используете междоменную библиотеку JavaScript, объект SP.RequestExecutor обрабатывает получение и отправку значения дайджеста формы.
 
Если вы создаете Надстройка SharePoint, размещенное в SharePoint, то вам не придется выполнять отдельный HTTP-запрос для получения обработанного значения. Вместо этого вы можете получить значение в коде JavaScript со страницы SharePoint (если страница использует эталонную страницу по умолчанию), как показано в следующем примере, в котором используется JQuery и создается список.
 
```javascript
jQuery.ajax({
        url: "http://<site url>/_api/web/lists",
        type: "POST",
        data:  JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'AllowContentTypes': true,
 'BaseTemplate': 100, 'ContentTypesEnabled': true, 'Description': 'My list description', 'Title': 'Test' }
),
        headers: { 
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val()
        },
        success: doSuccess,
        error: doError
});
```

В следующем примере показано, как обновить список, созданный в предыдущем примере. В примере меняется название списка, используется JQuery и предполагается, что вы выполняете эту операцию в надстройке, размещенной в SharePoint.

```javascript
jQuery.ajax({
        url: "http://<site url>/_api/web/lists/GetByTitle('Test')",
        type: "POST",
        data: JSON.stringify({ '__metadata': { 'type': 'SP.List' }, 'Title': 'New title' }),
        headers: { 
            "X-HTTP-Method":"MERGE",
            "accept": "application/json;odata=verbose",
            "content-type": "application/json;odata=verbose",
            "content-length": <length of post body>,
            "X-RequestDigest": $("#__REQUESTDIGEST").val(),
            "IF-MATCH": "*"
        },
        success: doSuccess,
        error: doError
});

```

В ключе **IF-MATCH** в заголовках запроса указывается значение **etag** для списка или его элемента. Это значение применяется только для списков и их элементов и помогает избежать проблем с одновременной обработкой при обновлении этих сущностей. В предыдущем примере вместо этого значения используется звездочка (*). Вы можете использовать это значение, если у вас нет причин беспокоиться о проблемах с одновременной обработкой. В противном случае необходимо получить значение **etag** либо список или его элемент, выполнив запрос **GET**, который извлекает сущность. Заголовки полученного HTTP-запроса передают etag в качестве значения ключа **ETag**. Это значение также включено в метаданные сущности. В приведенном ниже примере показан открывающий тег `<entry>` для узла XML, который содержит данные списка. Свойство **m:etag** содержит значение **etag**.

```XML
<entry xml:base="http://site url/_api/" xmlns=http://www.w3.org/2005/Atom 
xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" 
xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:etag=""1"">
```

## <a name="creating-a-site-with-rest"></a>Создание сайта с помощью REST
<a name="bk_CreateSite"> </a>

В приведенном ниже примере показано, как создать сайт на JavaScript.

```javascript
jQuery.ajax({
    url: "http://<site url>/_api/web/webinfos/add",
    type: "POST",
    data: JSON.stringify(
        {'parameters': {
            '__metadata':  {'type': 'SP.WebInfoCreationInformation' },
            'Url': 'RestSubWeb',
            'Title': 'RestSubWeb',
            'Description': 'REST created web',
            'Language':1033,
            'WebTemplate':'sts',
            'UseUniquePermissions':false}
        }
    ),
    headers: { 
        "accept": "application/json; odata=verbose", 
        "content-type":"application/json;odata=verbose",
        "content-length": <length of post body>,
        "X-RequestDigest": $("#__REQUESTDIGEST").val() 
    },
    success: doSuccess,
    error: doError
});
```

## <a name="how-rest-requests-differ-by-environment"></a>Отличия между запросами REST в разных средах
<a name="bk_HowRequestsDiffer"> </a>

Методы составления и отправки HTTP-запросов могут различаться в зависимости от языка, библиотеки и типа надстройки, поэтому при переводе запроса из одной среды в другую часто требуется менять один или несколько его компонентов. Например, в запросах jQuery AJAX текст и тип запроса указываются с помощью параметров **data** и **type**, а в запросах к междоменной библиотеке — с помощью параметров **body** и **method**.
 
В следующих разделах описываются другие распространенные отличия между средами.

### <a name="the-way-you-get-and-send-the-form-digest-value-depends-on-the-add-in"></a>Способ получения и отправки значение дайджеста формы зависит от надстройки
<a name="FormDigest"> </a>

При отправке запроса POST в его заголовке **X-RequestDigest** должно быть указано значение дайджеста формы. Однако способ получения и отправки значения зависит от надстройки.
 
- В надстройках с размещением в SharePoint можно передавать следующий заголовок: 
 
 `X-RequestDigest": $("#__REQUESTDIGEST").val()`
    
- В надстройках с размещением в облаке, использующих OAuth, для начала необходимо получить значение дайджеста формы, отправив запрос конечной точке **contextinfo**, а затем добавить его в запросы, как показано в разделе [Запись данных с помощью интерфейса REST](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData).
    
- В надстройках с размещением в облаке, которые используют междоменную библиотеку JavaScript, не требуется указывать значение дайджеста формы. По умолчанию SP.RequestExecutor делает это автоматически. (Метод также обрабатывает значение content-length.)

### <a name="add-ins-that-use-oauth-must-pass-access-tokens-in-requests"></a>Надстройки, использующие OAuth, должны передавать маркеры доступа в запросах
<a name="OAuthTokens"> </a>

Чтобы авторизовать доступ к данным в SharePoint, надстройки с размещением в облаке используют OAuth или междоменную библиотеку. Компоненты надстроек с кодом, выполняемым на удаленном веб-сервере, должны использовать OAuth для авторизации доступа к данным в SharePoint. В этом случае необходимо включить заголовок **Authorization** для отправки маркера доступа. Пример добавления заголовка авторизации к объекту **HTTPWebRequest** см. в разделе [Чтение данных с помощью интерфейса SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData).
 
 **Примечание.** Компоненты надстроек с размещением в облаке, написанные на JavaScript, должны использовать объект **SP.RequestExecutor** из междоменной библиотеки для доступа к данным SharePoint. В запросы к междоменной библиотеке не обязательно включать маркер доступа.
 
Дополнительные сведения о маркерах доступа OAuth и их получении см. в статьях [Поток маркеров контекста OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) и [Поток кода аутентификации OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).
 
### <a name="endpoint-uris-in-cross-domain-requests-use-spappcontextsite-to-change-the-context"></a>URI конечных точек в междоменных запросах используют объект SP.AppContextSite для изменения контекста
<a name="AppContextSite"> </a>

Запросы отправляются конечной точке ресурсов, указанной в свойстве **url** запроса. URI конечных точек представляются в следующем формате:
 
 `_<site url>_/_api/ _<context>_/ _<resource>_ (example, https://contoso.com/_api/web/lists)`
 
Этот формат используется в запросах к междоменной библиотеке при доступе к данным на сайте надстройки — стандартном контексте таких запросов. Однако для доступа к данным на хост-сайте или в другом семействе веб-сайтов запросам необходимо инициализировать хост-сайт или другое семейство веб-сайтов в качестве контекста. Для этого они используют конечную точку **SP.AppContextSite** в URI, как показано в таблице 1. В примерах URI из таблицы 1 используется псевдоним **@target** для отправки целевого URL-адреса в строке запроса, так как URL-адрес содержит специальный символ (":").

 **Примечание.** Для доступа к данным SharePoint при использовании междоменной библиотеки надстройке с размещением в облаке необходим экземпляр сайта надстройки.

**Таблица 1. Изменение контекста запроса с помощью конечной точки SP.AppContextSite**


|**Тип надстройки**|**Сценарий междоменного доступа к данным**|**Пример URI конечной точки**|
|:-----|:-----|:-----|
|С размещением в облаке|Компонент надстройки JavaScript получает доступ к данным хост-сайта с помощью междоменной библиотеки| _<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'|
|Размещение в облаке|Компонент надстройки JavaScript получает доступ к данным в семействе веб-сайтов, не включающем хост-сайт, с помощью междоменной библиотеки (только для надстроек с разрешениями на уровне клиента)| _<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'|
|Размещение в SharePoint|Компонент сайта надстройки получает доступ к данным в другом семействе веб-сайтов (только для надстроек с разрешениями на уровне клиента)| _<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'|

 
  **Примечание.** Для междоменного доступа к данным также требуются соответствующие разрешения для надстроек. Дополнительные сведения см. в разделах [Доступ к данным на хост-сайте](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_Hostweb) и [Доступ к данным в нескольких семействах веб-сайтов](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_TenantScope).

Надстройки SharePoint могут получать URL-адреса сайта надстройки и хост-сайта из строки запроса страницы надстройки, как показано в следующем примере кода. Кроме того, в этом примере показывается, как ссылаться на междоменную библиотеку, определенную в файле SP.RequestExecutor.js на хост-сайте. Этот пример предполагает, что ваша надстройка запускается из SharePoint. Указания по правильной настройке контекста SharePoint, если надстройка запускается не из SharePoint, см. в статье  [Поток кода аутентификации OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).

```javascript
var hostweburl;
var appweburl;

// Get the URLs for the add-in web the host web URL from the query string.
$(document).ready(function () {
  //Get the URI decoded URLs.
  hostweburl = decodeURIComponent(getQueryStringParameter("SPHostUrl"));
  appweburl = decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));

  // Load the SP.RequestExecutor.js file.
  $.getScript(hostweburl + "/_layouts/15/SP.RequestExecutor.js", runCrossDomainRequest);
});

// Build and send the HTTP request.
function runCrossDomainRequest() {
  var executor = new SP.RequestExecutor(appweburl); 
  executor.executeAsync({
      url: appweburl + "/_api/SP.AppContextSite(@target)/web/lists?@target='" + hostweburl + "'",
      method: "GET", 
      headers: { "Accept": "application/json; odata=verbose" }, 
      success: successHandler, 
      error: errorHandler 
  });
}

// Get a query string value.
// For production add-ins, you may want to use a library to handle the query string.
function getQueryStringParameter(paramToRetrieve) {
  var params = document.URL.split("?")[1].split("&amp;");
  var strParams = "";
  for (var i = 0; i < params.length; i = i + 1) {
    var singleParam = params[i].split("=");
    if (singleParam[0] == paramToRetrieve) return singleParam[1];
  }
}
… // success and error callback functions
```

## <a name="properties-used-in-rest-requests"></a>Свойства, используемые в запросах REST
<a name="bk_requestElements"> </a>

В таблице 2 показаны свойства, которые часто используются в HTTP-запросах для службы REST SharePoint.
 
**Таблица 2. Использование свойств запроса REST в HTTP-запросах**

|**Свойства**|**Когда требуется**|**Описание**|
|:-----|:-----|:-----|
|**url**|Все запросы|URL-адрес конечной точки ресурса REST. Например:  `http://<site url>/_api/web/lists`|
|**method** (или **type**)|Все запросы|Метод HTTP-запроса: **GET** для операций чтения и **POST** для операций записи. Запросы **POST** могут выполнять операции обновления или удаления с помощью команды **DELETE**, **MERGE** или **PUT** в заголовке **X-HTTP-Method**.|
|**body** (или **data**)|Запросы **POST**, которые отправляют данные в тексте запроса|Текст запроса POST. Отправляет данные (например, сложные типы), которые невозможно передать в URI конечной точки. Используется с заголовком **content-length**.|
|Заголовок **Authentication**|Удаленные надстройки, которые используют OAuth для проверки подлинности пользователей. Не применяется при использовании JavaScript или междоменной библиотеки.|Отправляет маркер доступа (полученный от сервера токенов безопасности для службы контроля доступа Microsoft Azure), который используется для проверки подлинности пользователя для запроса. Например:  `"Authorization": "Bearer " + accessToken`, где  `accessToken` представляет переменную, которая сохраняет маркер. Маркеры должны загружаться с использованием кода на стороне сервера. |
|Заголовок **X-RequestDigest**|Запросы **POST** (кроме запросов SP.RequestExecutor)|Удаленные надстройки, использующие протокол OAuth, могут получить значение дайджеста формы от конечной точки  `http://<site url>/_api/contextinfo`. Надстройки, размещенные в SharePoint, могут получить это значение от элемента управления страницей **#__REQUESTDIGEST**, если он доступен на странице SharePoint. См. раздел  [Запись данных с помощью интерфейса REST](#WritingData).  |
|Заголовок **accept**|Запросы, которые возвращают метаданные SharePoint|Указывает формат данных ответа от сервера. Форматом по умолчанию является  `application/atom+xml`, например:  `"accept":"application/json;odata=verbose"`|
|Заголовок **content-type**|Запросы **POST**, которые отправляют данные в тексте запроса|Указывает формат данных, которые клиент отправляет серверу. Форматом по умолчанию является  `application/atom+xml`, например:  `"content-type":"application/json;odata=verbose"`|
|Заголовок **content-length**|Запросы **POST**, которые отправляют данные в тексте запроса (кроме запросов SP.RequestExecutor)|Указывает длину содержимого, например:  `"content-length":requestBody.length`|
|Заголовок **IF-MATCH**|Запросы **POST** для операций **DELETE**, **MERGE** и **PUT**, в первую очередь для изменения списков и библиотек.|Предоставляет способ проверки того, что изменяемый объект не менялся с момента его последней загрузки. Или позволяет включить перезапись любых изменений, как показано в следующем примере:  `"IF-MATCH":"*"`|
|Заголовок **X-HTTP-Method**|Запросы **POST** для операций **DELETE**, **MERGE** и **PUT**|Указывает, что запрос выполняет операцию обновления или удаления. Пример: `"X-HTTP-Method":"PUT"`|
|**binaryStringRequestBody**|Запросы **POST** для SP.RequestExecutor, которые отправляют двоичные данные в тексте запроса|Указывает, является ли текст запроса двоичной строкой. **Boolean**.|
|**binaryStringResponseBody**|Запросы SP.RequestExecutor, возвращающие двоичные данные|Указывает, является ли отклик двоичной строкой. **Логическое значение**.|

## <a name="batch-job-support"></a>Поддержка пакетных заданий
<a name="batch"> </a> Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md)
-  [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md) 
-  [Справочные материалы по интерфейсу API службы REST и примеры](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [SharePoint 2013: выполнение базовых операций с файлами и папками с помощью REST](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  
  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx)
-  
  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx)
-  
  [Разработка надстроек для SharePoint](https://msdn.microsoft.com/en-us/library/office/jj163794.aspx)
-  
  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](https://msdn.microsoft.com/en-us/library/office/fp179897.aspx)
-  
  [Работа с внешними данными в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179893.aspx)
-  [Протокол OData](http://www.odata.org/)
-  [OData: формат нотации объектов JavaScript (JSON)](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
-  [Назначение настраиваемых разрешений для списка с помощью интерфейса REST](set-custom-permissions-on-a-list-by-using-the-rest-interface.md)