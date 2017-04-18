# <a name="complete-basic-operations-using-sharepoint-rest-endpoints"></a>Выполнение базовых операций с использованием конечных точек REST SharePoint
Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint.

## <a name="developing-with-the-sharepoint-client-apis-and-rest"></a>Разработка с помощью клиентских интерфейсов API и REST для SharePoint
<a name="ClientAPIs"> </a> Вы можете выполнять базовые операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса передачи репрезентативного состояния (REST), предоставляемого средой SharePoint. Интерфейс REST предоставляет доступ ко всем сущностям и операциям SharePoint, доступным в других клиентских API SharePoint. Одно из преимуществ использования REST состоит в том, что вам не требуется добавлять ссылки на библиотеки и клиентские сборки SharePoint. Вместо этого соответствующим конечным точкам отправляются HTTP-запросы на получение или обновление сущностей SharePoint, таких как веб-сайты, списки и элементы списков. В статье [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md) представлено подробное введение в интерфейс REST SharePoint и его архитектуру.
 
В статьях [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md) и [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md) более подробно описывается работа с основными сущностями SharePoint. В примере [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations) показано, как выполнять многие из этих операций в контексте веб-приложения ASP.NET, написанного на языке C#.
 
Дополнительные сведения о наборах API, доступных на платформе SharePoint, см. в статье [Выбор правильного набора API в SharePoint 2013](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx). Сведения о том, как использовать другие клиентские интерфейсы API, см. в статьях [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx), [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx) и [Создание приложений для Windows Phone, обращающихся к SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163228.aspx).
 

## <a name="http-operations-in-sharepoint-rest-services"></a>Операции HTTP в службах REST SharePoint
<a name="HTTPOps"> </a> Конечные точки в службе REST SharePoint соответствуют типам и элементам клиентских объектных моделей SharePoint. С помощью HTTP-запросов вы можете использовать эти конечные точки REST для выполнения типичных операций CRUD (**Create**, **Read**, **Update** и **Delete**) с сущностями SharePoint, такими как списки и сайты. 
 
Как правило, конечные точки, представляющие операции **Read**, соответствуют командам HTTP **GET**. Конечные точки, представляющие операции обновления, соответствуют командам HTTP **POST**, а конечные точки для операций обновления и вставки — командам HTTP **PUT**.
 
В SharePoint с помощью команды **POST** можно создавать сущности, например списки и сайты. Служба REST SharePoint поддерживает отправку команд **POST**, включающих определения объектов, к конечным точкам, представляющим коллекции. Например, вы можете отправить команду **POST**, включающую определение нового объекта списка в формате ATOM, на следующий URL-адрес, чтобы создать список SharePoint:
 
 ```
 http://<site url>/_api/web/lists
 ```

В операциях **POST** для всех необязательных свойств задаются значения по умолчанию. При попытке задать доступное только для чтения свойство в рамках операции **POST** служба возвращает исключение.
  
С помощью операций **PUT** и **MERGE** можно обновлять существующие объекты SharePoint. Любая конечная точка службы, представляющая операцию **set** для свойств объектов, поддерживает как запросы **PUT**, так и запросы **MERGE**. В запросах **MERGE** задавать свойства необязательно. Все свойства, не заданные в явном виде, сохраняют свои текущие значения. Однако в командах **PUT** всем свойствам, не заданным в явном виде, присваиваются значения по умолчанию. Кроме того, если при обновлении объекта с помощью команды HTTP **PUT** указаны не все обязательные свойства, служба REST возвращает исключение.
  
Отправив команду HTTP **DELETE** на URL-адрес определенной конечной точки, вы можете удалить объект SharePoint, который представляет эта конечная точка. В случае объектов, поддерживающих повторное использование, например списков, файлов и элементов списков, при этом выполняется операция **Recycle**.
 
## <a name="reading-data-with-the-sharepoint-rest-interface"></a>Считывание данных с помощью интерфейса REST SharePoint
<a name="ReadingData"> </a> Чтобы использовать возможности REST, встроенные в SharePoint, необходимо создать HTTP-запрос RESTful, используя стандарт OData, соответствующий нужному API клиентской объектной модели. Каждая сущность SharePoint представляется в конечной точке на целевом сайте SharePoint, а ее метаданные представляются в формате XML или JSON. Вы можете выполнять HTTP-запросы на любом языке, в том числе JavaScript и C#.
 
Чтобы считывать сведения из конечной точки REST, вам потребуются URL-адрес конечной точки и представление OData соответствующей сущности SharePoint. Например, чтобы получить все списки на определенном сайте SharePoint, необходимо отправить запрос **GET** по адресу `http://<site url>/_api/web/lists`. Вы можете перейти по этому URL-адресу в браузере и просмотреть возвращаемый код XML. Совершая запрос в коде, вы можете указать, в каком формате нужно получить представление OData списков: XML или JSON.
 
В приведенном ниже коде на языке C# показано, как совершить запрос **GET**, который возвращает представление всех списков на сайте в формате JSON с помощью JQuery. Кроме того, предполагается, что у вас есть допустимый маркер доступа OAuth, хранящийся в переменной **accessToken**. Этот маркер доступа не требуется, если вы совершаете вызов с сайта надстройки, как в надстройках с размещением в SharePoint. Обратите внимание, что маркер доступа невозможно получить из кода, выполняемого в браузерном клиенте. Маркер доступа необходимо получить из кода, выполняемого на сервере. В статьях [Поток маркеров контекста OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) и [Поток кода аутентификации OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) описывается получение маркера доступа.

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

Если вы создаете надстройку на JavaScript, но используете междоменную библиотеку SharePoint, этот запрос будет выглядеть немного по-другому. В этом случае нет необходимости предоставлять маркер доступа. В приведенном ниже коде показано, как будет выглядеть этот запрос, если вы используете междоменную библиотеку и хотите получить представление OData списков в формате XML, а не JSON. (Так как по умолчанию для отклика используется формат Atom, включать заголовок **Accept** не требуется.) Дополнительные сведения об использовании междоменной библиотеки см. в статье [Обращение к данным SharePoint 2013 из надстроек с помощью междоменной библиотеки](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx).
 
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

В приведенном ниже примере кода показано, как запросить представление в формате JSON для всех списков на сайте с помощью C#. Предполагается, что у вас есть маркер доступа OAuth, хранящийся в переменной `accessToken`.

```
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();

```

### <a name="getting-properties-that-arent-returned-with-the-resource"></a>Получение свойств, не возвращаемых с ресурсом
<a name="NavigationProperties"> </a> Значения многих свойств возвращаются при получении ресурса, но для некоторых свойств необходимо отправить запрос **GET** непосредственно конечной точке свойства. Это типично для свойств, представляющих сущности SharePoint.
 
В приведенном ниже примере показано, как получить свойство, добавив его имя к конечной точке ресурса. В этом примере считывается значение свойства **Author** из ресурса **File**.
 
 ```
 http:// _<site url>_/_api/web/getfilebyserverrelativeurl('/ _<folder name>_/ _<file name>_')/author
 ```

Чтобы получить результаты в формате JSON, включите в запрос заголовок **Accept** со значением `"application/json;odata=verbose"`.

## <a name="writing-data-by-using-the-rest-interface"></a>Запись данных с помощью интерфейса REST
<a name="WritingData"> </a>

Вы можете создавать и обновлять сущности SharePoint, создавая HTTP-запросы RESTful к соответствующим конечным точкам, как и при считывании данных. Однако есть одно ключевое отличие — используется запрос **POST**. При обновлении сущностей также передается метод HTTP-запроса **PUT** или **MERGE** путем добавления одного из этих терминов в заголовки запроса в качестве значения ключа **X-HTTP-Method**. Метод **MERGE** обновляет только свойства указанной сущности, в то время как метод **PUT** заменяет существующую сущность новой, указанной в тексте запроса **POST**. Для удаления сущности используется метод **DELETE**. При создании или обновлении сущности необходимо указать представление OData нужной сущности в тексте HTTP-запроса.
 
При создании, обновлении и удалении сущностей SharePoint также следует учитывать, что для этих операций необходимо указать значение дайджеста формы запроса в заголовке **X-RequestDigest**, если для авторизации запросов не используется OAuth. Вы можете извлечь это значение, отправив запрос **POST** с пустым текстом по адресу `http://<site url>/_api/contextinfo` и получив значение узла `d:FormDigestValue` в формате XML, возвращаемое конечной точкой **contextinfo**. В приведенном ниже примере показан HTTP-запрос к конечной точке **contextinfo** на языке C#.
 
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
 
При создании надстройки, размещаемой в SharePoint, вам не понадобится отправлять отдельный HTTP-запрос, чтобы получить значение дайджеста формы. Вместо этого вы можете получить значение в коде JavaScript со страницы SharePoint (если в ней используется эталонная страница по умолчанию), как показано в приведенном ниже примере, где используется JQuery и создается список.
 
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

В приведенном ниже примере показано, как обновить список, созданный в предыдущем примере. В этом примере изменяется заголовок списка, используется JQuery и предполагается, что операция выполняется в надстройке, размещенной в SharePoint.

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

Значение ключа **IF-MATCH** в заголовках запросов должно содержать значение **etag** списка или его элемента. Это конкретное значение применимо только к спискам и их элементам. Оно призвано помочь вам избежать проблем с параллелизмом при обновлении этих сущностей. В предыдущем примере вместо этого значения используется звездочка (*). Так можно делать, когда нет причин волноваться о проблемах с параллелизмом. В противном случае необходимо получить значение **etag** списка или его элемента, выполнив запрос **GET** на получение сущности. В заголовках полученного HTTP-отклика значение etag передается в качестве значения ключа **ETag**. Это значение также входит в состав метаданных сущности. В приведенном ниже примере показан открывающий тег `<entry>` узла XML, содержащий данные списка. Свойство **m:etag** содержит значение **etag**.

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

Процесс создания и отправки HTTP-запроса зависит от языка, библиотеки и типа надстройки, поэтому при переносе запроса из одной среды в другую часто требуется изменить один или несколько компонентов. Например, в запросах jQuery AJAX текст и тип запроса задаются с помощью параметров **data** и **type**, но в запросах междоменной библиотеки эти значения задаются с помощью параметров **body** и **method**.
 
В следующих разделах описаны другие распространенные отличия между средами.

### <a name="the-way-you-get-and-send-the-form-digest-value-depends-on-the-add-in"></a>Способ получения и отправки значение дайджеста формы зависит от надстройки
<a name="FormDigest"> </a>

Отправляемый запрос POST должен включать значение дайджеста формы в заголовке **X-RequestDigest**. Однако способ получения и отправки значения зависит от конкретной надстройки:
 
- В надстройках с размещением в SharePoint можно передавать следующий заголовок: 
 
 `X-RequestDigest": $("#__REQUESTDIGEST").val()`
    
- В надстройках с размещением в облаке, использующих OAuth, для начала необходимо получить значение дайджеста формы, отправив запрос конечной точке **contextinfo**, а затем добавить его в запросы, как показано в разделе [Запись данных с помощью интерфейса REST](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData).
    
- В надстройках с размещением в облаке, использующих междоменную библиотеку JavaScript, не требуется указывать значение дайджеста формы. По умолчанию это автоматически делает объект SP.RequestExecutor. (Кроме того, он обрабатывает значение Content-Length.)

### <a name="add-ins-that-use-oauth-must-pass-access-tokens-in-requests"></a>Надстройки, использующие OAuth, должны передавать маркеры доступа в запросах
<a name="OAuthTokens"> </a>

Надстройки с размещением в облаке используют OAuth или междоменную библиотеку для авторизации доступа к данным SharePoint. Компоненты надстроек с кодом, выполняющимся на удаленном веб-сервере, должны использовать OAuth для авторизации доступа к данным SharePoint. В этом случае необходимо включить в запрос заголовок **Authorization** для отправки маркера доступа. В разделе [Считывание данных с помощью интерфейса REST SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData) представлен пример добавления заголовка авторизации к объекту **HTTPWebRequest**.
 
 **Примечание.** Компоненты надстроек с размещением в облаке, написанные на JavaScript, должны использовать объект **SP.RequestExecutor** из междоменной библиотеки для доступа к данным SharePoint. В запросы к междоменной библиотеке не обязательно включать маркер доступа.
 
Дополнительные сведения о маркерах доступа OAuth и их получении см. в статьях [Поток маркеров контекста OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/fp142382.aspx) и [Поток кода аутентификации OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx).
 
### <a name="endpoint-uris-in-cross-domain-requests-use-spappcontextsite-to-change-the-context"></a>URI конечных точек в междоменных запросах используют объект SP.AppContextSite для изменения контекста
<a name="AppContextSite"> </a>

Запросы отправляются конечной точке ресурса, указанной в свойстве **url** запроса. URI конечных точек должны быть представлены в следующем формате:
 
 `_<site url>_/_api/ _<context>_/ _<resource>_ (example, https://contoso.com/_api/web/lists)`
 
В запросах к междоменной библиотеке этот формат используется при доступе к данным на сайте надстройки (это стандартный контекст для таких запросов). Однако для доступа к данным на хост-сайте или в другом семействе веб-сайтов запросы должны инициализировать хост-сайт или другое семейство веб-сайтов в качестве контекста. Для этого используется конечная точка **SP.AppContextSite** в URI, как показано в таблице 1. Примеры URI в таблице 1 содержат псевдоним **@target** для отправки целевого URL-адреса в строке запроса, так как URL-адрес содержит специальный знак (":").

 **Примечание.** Для доступа к данным SharePoint при использовании междоменной библиотеки надстройке с размещением в облаке необходим экземпляр сайта надстройки.

**Таблица 1. Использование конечной точки SP.AppContextSite для изменения контекста запроса**


|**Тип надстройки**|**Сценарий междоменного доступа к данным**|**Пример URI конечной точки**|
|:-----|:-----|:-----|
|С размещением в облаке|Компонент надстройки JavaScript получает доступ к данным хост-сайта с помощью междоменной библиотеки| _<app web url>_/_api/SP.AppContextSite(@target)/web/lists?@target=' _<host web url>_'|
|С размещением в облаке|Компонент надстройки JavaScript получает доступ к данным в семействе веб-сайтов, не включающем хост-сайт, с помощью междоменной библиотеки (только для надстроек с разрешениями на уровне клиента)| _<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'|
|Размещено в SharePoint|Компонент сайта надстройки получает доступ к данным в другом семействе веб-сайтов (только для надстроек с разрешениями на уровне клиента)| _<app web url>_/_api/SP.AppContextSite(@target)/web/title?@target=' _<target site url>_'|

 
  **Примечание.** Для доступа к данным между доменами надстройке также необходимы соответствующие разрешения. Дополнительные сведения см. в разделах [Доступ к данным на хост-сайте](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_Hostweb) и [Доступ к данным на нескольких семействах веб-сайтов](https://msdn.microsoft.com/en-us/library/office/fp179927.aspx#SP15Accessdatafromremoteapp_TenantScope).

Надстройки SharePoint могут получать URL-адреса сайта надстройки и хост-сайта из строки запроса на странице надстройки, как показано в приведенном ниже примере кода. В этом примере также показано, как ссылаться на междоменную библиотеку, определенную в файле SP.RequestExecutor.js на хост-сайте. В этом примере предполагается, что надстройка запускается из SharePoint. В статье [Поток кода аутентификации OAuth для надстроек в SharePoint](https://msdn.microsoft.com/en-us/library/office/jj687470.aspx) рассказывается, как правильно задать контекст SharePoint, если надстройка не запускается из SharePoint.

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
 
**Таблица 2. Использование свойств запроса REST в HTTP-запросах**

|**Свойства**|**Когда требуется**|**Описание**|
|:-----|:-----|:-----|
|**url**|Все запросы|URL-адрес конечной точки ресурса REST. Пример: `http://<site url>/_api/web/lists`|
|**method** (или **type**)|Все запросы|Метод HTTP-запроса:  **GET** для операций чтения и **POST** для записи. Запросы **POST** могут выполнять операции обновления и удаления с помощью команд **DELETE**, **MERGE** и **PUT** в заголовке **X-HTTP-Method**.|
|**body** (или **data**)|Запросы **POST**, которые отправляют данные в тексте запроса|Текст запроса POST. Отправляет данные (например, сложные типы), которые невозможно отправлять в URI конечной точки. Используется с заголовком **content-length**.|
|Заголовок **Authentication**|Удаленные надстройки, использующие OAuth для проверки подлинности пользователей. Не применяется при использовании JavaScript или междоменной библиотеки.|Отправляет маркер доступа OAuth, полученный с сервера токенов безопасности в службе контроля доступа (ACS) и используемый для проверки подлинности пользователя в запросе. Пример: `"Authorization": "Bearer " + accessToken`, где `accessToken` представляет переменную, в которой хранится маркер. Маркеры необходимо получать с помощью серверного кода.|
|Заголовок **X-RequestDigest**|Запросы **POST** (кроме запросов SP.RequestExecutor)|Удаленные надстройки, использующие OAuth, могут получать значение дайджеста формы из конечной точки `http://<site url>/_api/contextinfo`. Надстройки с размещением в SharePoint могут получать значение от элемента управления страницей **#__REQUESTDIGEST**, если он доступен на странице SharePoint. См. раздел [Запись данных с помощью интерфейса REST](#WritingData).|
|Заголовок **accept**|Запросы, которые возвращают метаданные SharePoint|Задает формат данных для отклика сервера. Формат по умолчанию: `application/atom+xml`. Пример: `"accept":"application/json;odata=verbose"`|
|Заголовок **content-type**|Запросы **POST**, которые отправляют данные в тексте запроса|Указывает формат данных, которые клиент отправляет серверу. Формат по умолчанию: `application/atom+xml`. Пример: `"content-type":"application/json;odata=verbose"`|
|Заголовок **content-length**|Запросы **POST**, которые отправляют данные в тексте запроса (кроме запросов SP.RequestExecutor)|Указывает длину содержимого. Пример: `"content-length":requestBody.length`|
|Заголовок **IF-MATCH**|Запросы **POST** для операций **DELETE**, **MERGE** и **PUT**, в первую очередь для изменения списков и библиотек.|Позволяет убедиться, что изменяемый объект не был изменен с момента его последнего получения. Кроме того, с помощью этого заголовка можно переписать все изменения, как показано в следующем примере: `"IF-MATCH":"*"`|
|Заголовок **X-HTTP-Method**|Запросы **POST** для операций **DELETE**, **MERGE** и **PUT**|Указывает, что запрос выполняет операцию обновления или удаления. Пример: `"X-HTTP-Method":"PUT"`|
|**binaryStringRequestBody**|Запросы **POST**, которые отправляют двоичные данные в тексте запроса|Указывает, является ли текст запроса двоичной строкой.  **Логическое значение**.|
|**binaryStringResponseBody**|Запросы SP.RequestExecutor, возвращающие двоичные данные|Указывает, является ли отклик двоичной строкой.  **Логическое значение**.|

## <a name="batch-job-support"></a>Поддержка пакетных заданий
<a name="batch"> </a> Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Выполнение пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md)
-  [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md) 
-  [Справочные материалы по интерфейсу API службы REST и примеры](http://msdn.microsoft.com/library/02128c70-9d27-4388-9374-a11bce68fdb8%28Office.15%29.aspx)
-  [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations)
-  [SharePoint 2013: выполнение базовых операций доступа к данным файлов и папок с помощью REST](http://code.msdn.microsoft.com/SharePoint-2013-Perform-ab9c4ae5)
-  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179912.aspx)
-  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/jj163201.aspx)
-  [Разработка надстроек для SharePoint](https://msdn.microsoft.com/en-us/library/office/jj163794.aspx)
-  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](https://msdn.microsoft.com/en-us/library/office/fp179897.aspx)
-  [Работа с внешними данными в SharePoint 2013](https://msdn.microsoft.com/en-us/library/office/fp179893.aspx)
-  [Open Data Protocol](http://www.odata.org/)
-  [OData: формат нотации объектов JavaScript (JSON)](http://www.odata.org/documentation/odata-version-2-0/JSON-format/)
-  [Назначение настраиваемых разрешений для списка с помощью интерфейса REST](set-custom-permissions-on-a-list-by-using-the-rest-interface.md)