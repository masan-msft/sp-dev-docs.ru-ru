---
title: "Выполнение базовых операций с использованием конечных точек REST SharePoint"
description: "Узнайте, как выполнять операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST SharePoint."
ms.date: 12/13/2017
ms.prod: sharepoint
ms.openlocfilehash: 66256c58591218c9c10d6553b7d7e01fd1c3870d
ms.sourcegitcommit: 4e65e89f3ad8ef1d953e2fdd04d7ab5c0e7df174
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="complete-basic-operations-using-sharepoint-rest-endpoints"></a>Выполнение базовых операций с использованием конечных точек REST SharePoint

Вы можете выполнять базовые операции CRUD (создание, чтение, обновление, удаление) с помощью интерфейса REST, предоставляемого средой SharePoint. Интерфейс REST предоставляет доступ ко всем сущностям и операциям SharePoint, доступным в других клиентских API SharePoint. Одно из преимуществ использования REST состоит в том, что вам не требуется добавлять ссылки на библиотеки и клиентские сборки SharePoint. Вместо этого соответствующим конечным точкам отправляются HTTP-запросы на получение или обновление сущностей SharePoint, таких как веб-сайты, списки и элементы списков. 

Общие сведения об интерфейсе SharePoint REST и его архитектуре см. в статье [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md). 

Сведения о том, как работать с основными сущностями SharePoint см. в статьях [Работа со списками и элементами списков в службе REST](working-with-lists-and-list-items-with-rest.md) и [Работа с папками и файлами в службе REST](working-with-folders-and-files-with-rest.md). 

В примере [SharePoint-Add-in-REST-OData-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-BasicDataOperations.md) показано, как выполнять многие из этих операций в контексте веб-приложения ASP.NET, написанного на языке C#. 

Дополнительные сведения о наборах API, доступных на платформе SharePoint, см. в статье [Выбор правильного набора API в SharePoint](../general-development/choose-the-right-api-set-in-sharepoint.md). 

Сведения об использовании других клиентских API см. в статье

- [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](complete-basic-operations-using-javascript-library-code-in-sharepoint.md)- [Выполнение базовых операций с использованием кода клиентской библиотеки SharePoint](complete-basic-operations-using-sharepoint-client-library-code.md).
- [Создание приложений Windows Phone с доступом к SharePoint](../general-development/build-windows-phone-apps-that-access-sharepoint.md)

<a name="HTTPOps"> </a>

## <a name="http-operations-in-sharepoint-rest-services"></a>Операции HTTP в службах REST SharePoint

Конечные точки в службе REST SharePoint соответствуют типам и элементам клиентских объектных моделей SharePoint. С помощью HTTP-запросов вы можете использовать эти конечные точки REST для выполнения типичных операций CRUD (**Create**, **Read**, **Update** и **Delete**) с сущностями SharePoint, такими как списки и сайты. 

Как правило, конечные точки, представляющие операции **Read**, сопоставляются с HTTP-командами **GET**. Конечные точки, представляющие операции обновления, сопоставляются с HTTP-командами **POST**, а конечные точки, представляющие операции обновления или вставки, — с HTTP-командами **PUT**.
 
В SharePoint для создания сущностей, например списков и сайтов, используется команда **POST**. Служба REST SharePoint поддерживает отправку команд **POST**, включающих описания объектов для конечных точек, представляющих коллекции. Например, можно отправить команду **POST**, включающую новое описание объекта списка в ATOM, на следующий URL-адрес, чтобы создать список SharePoint.
 
`http://<site url>/_api/web/lists`

Для операций **POST** любые свойства, которые не являются необходимыми, имеют значения по умолчанию. Если попытаться задать свойство, предназначенное только для чтения, в операции **POST**, служба возвращает исключение.

Для обновления существующих объектов SharePoint используйте операции **PUT** и **MERGE**. Любые конечные точки службы, представляющие операцию **set** свойства объекта, поддерживают как запросы **PUT**, так и запросы **MERGE**. Для запросов **MERGE** необязательно задавать свойства. Любые свойства, не заданные явно, сохраняют текущие значения. Однако для команд **PUT** любое свойство, не заданное явно, будет иметь значение по умолчанию. Кроме того, если не указать все обязательные свойства в обновлении объекта при использовании HTTP-команд **PUT**, служба REST вернет исключение.

Используйте HTTP-команду **DELETE** для определенного URL-адреса конечной точки, чтобы удалить объект SharePoint, представленный этой конечной точкой. Для повторно обрабатываемых объектов (например, списков, файлов и элементов списков) это приведет к выполнению операции **Recycle**.
 
<a name="ReadingData"> </a>
 
## <a name="reading-data-with-the-sharepoint-rest-interface"></a>Считывание данных с помощью интерфейса REST SharePoint

Для использования возможностей REST, которые встроены в SharePoint, вы создаете HTTP-запрос с поддержкой REST, используя стандарт OData, что соответствует клиентской объектной модели API, которую вы хотите использовать. Каждый объект SharePoint предоставляется в конечной точке на странице SharePoint, на которую вы ориентируетесь, а метаданные представлены в формате XML или JSON. Вы можете создавать HTTP-запросы на любом языке, в том числе на JavaScript, C# и многих других.

Чтобы считывать сведения из конечной точки REST, вам потребуются URL-адрес конечной точки и представление OData соответствующей сущности SharePoint. Например, чтобы получить все списки на определенном сайте SharePoint, необходимо отправить запрос **GET** по адресу `http://<site url>/_api/web/lists`. Вы можете перейти по этому URL-адресу в браузере и просмотреть возвращаемый код XML. Совершая запрос в коде, вы можете указать, в каком формате нужно получить представление OData списков — XML или JSON.

В приведенном ниже коде на языке C# показано, как совершить запрос **GET**, который возвращает представление всех списков на сайте в формате JSON с помощью JQuery. Кроме того, предполагается, что у вас есть допустимый маркер доступа OAuth, хранящийся в переменной **accessToken**. Этот маркер доступа не требуется, если вы совершаете вызов с сайта надстройки, как в надстройках с размещением в SharePoint. Обратите внимание, что маркер доступа невозможно получить из кода, выполняемого в браузерном клиенте. Маркер доступа необходимо получить из кода, выполняемого на сервере. 

Дополнительные сведения о том, как получить маркер доступа, см. в статьях [Поток маркеров контекста OAuth для надстроек SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md) и [Поток кода авторизации OAuth для надстроек SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md).

```C#

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

<br/>

Если вы создаете надстройку на JavaScript, но используете междоменную библиотеку SharePoint, этот запрос будет выглядеть немного по-другому. В этом случае нет необходимости предоставлять маркер доступа. 

В приведенном ниже коде показано, как будет выглядеть этот запрос, если вы используете междоменную библиотеку и хотите получить представление OData списков в формате XML, а не JSON. Так как формат отклика Atom используется по умолчанию, включать заголовок **Accept** необязательно. Дополнительные сведения об использовании междоменной библиотеки см. в статье [Доступ к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).

```
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

<br/>

В приведенном ниже примере кода показано, как запросить представление в формате JSON для всех списков на сайте с помощью C#. Предполагается, что у вас есть маркер доступа OAuth, хранящийся в переменной `accessToken`.

```C#
HttpWebRequest endpointRequest = (HttpWebRequest)HttpWebRequest.Create(sharepointUrl.ToString() + "/_api/web/lists");
endpointRequest.Method = "GET";
endpointRequest.Accept = "application/json;odata=verbose";
endpointRequest.Headers.Add("Authorization", "Bearer " + accessToken);
HttpWebResponse endpointResponse = (HttpWebResponse)endpointRequest.GetResponse();

```

<br/>

<a name="NavigationProperties"> </a>

### <a name="getting-properties-that-arent-returned-with-the-resource"></a>Получение свойств, не возвращаемых с ресурсом

Многие значения свойств возвращаются, когда вы получаете ресурс, но для некоторых свойств необходимо отправить запрос **GET** непосредственно в конечную точку свойства. Это типично для свойств, представляющих объекты SharePoint.

В следующем примере показывается, как получить свойство, добавив его имя в конечную точку ресурса. В примере значение свойства **Author** получено от ресурса **File**.
 
`http://<site url>/_api/web/getfilebyserverrelativeurl('/<folder name>/<file name>')/author`

Чтобы получить результаты в формате JSON, включите набор заголовков **Accept** в `"application/json;odata=verbose"`.
 

<a name="WritingData"> </a> 

## <a name="writing-data-by-using-the-rest-interface"></a>Запись данных с помощью интерфейса REST

Вы можете создавать и обновлять объекты SharePoint, создавая HTTP-запросы с поддержкой REST для соответствующих конечных точек, так же, как это происходит при чтении данных. Одно из ключевых отличий заключается в том, что вы используете запрос **POST**. При обновлении объектов вы также передаете HTTP-запрос **PUT** или **MERGE**, добавляя один из этих операторов в заголовки запроса в качестве значения ключа **X-HTTP-Method**. Метод **MERGE** обновляет только те свойства объекта, которые вы укажете, в то время как метод **PUT** заменяет существующий объект на новый, который вы указываете в теле **POST**. Используйте метод **DELETE** для удаления объекта. При создании или обновлении объекта необходимо указать представление OData для объекта, который вы хотите создать или изменить, в теле HTTP-запроса.

Еще одним важным фактором при создании, обновлении и удалении объектов SharePoint является то, что если вы не используете OAuth для авторизации своих запросов, для выполнения этих операций потребуется передавать значение дайджеста формы запроса сервера в качестве значения заголовка **X-RequestDigest**. Чтобы получить это значение, выполните запрос **POST** с пустым телом для `http://<site url>/_api/contextinfo` и извлеките значение сайта `d:FormDigestValue` в XML-коде, возвращаемом конечной точкой **contextinfo**. В следующем примере показан HTTP-запрос к конечной точке **contextinfo**, написанный на C#.

```C#

HttpWebRequest endpointRequest =
  (HttpWebRequest)HttpWebRequest.Create(
  "http://<site url>/_api/contextinfo");
endpointRequest.Method = "POST";
endpointRequest.Accept = "application/json;odata=verbose";
HttpWebResponse endpointResponse =
  (HttpWebResponse)endpointRequest.GetResponse();

```

<br/>

Если вы используете поток проверки подлинности и авторизации, описанный в статье [Авторизация и проверка подлинности для надстроек SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md), вам не потребуется включать дайджест в запросы.

Если вы используете междоменную библиотеку JavaScript, объект SP.RequestExecutor обрабатывает получение и отправку значения дайджеста формы.

При создании надстройки, размещаемой в SharePoint, вам не понадобится отправлять отдельный HTTP-запрос, чтобы получить значение дайджеста формы. Вместо этого вы можете получить значение в коде JavaScript со страницы SharePoint (если в ней используется эталонная страница по умолчанию), как показано в приведенном ниже примере, где используется JQuery и создается список.


```
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

<br/>

В следующем примере показано, как обновить список, созданный в предыдущем примере. В примере меняется название списка, используется JQuery и предполагается, что вы выполняете эту операцию в надстройке, размещенной в SharePoint.

```
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

<br/>

Значение ключа **IF-MATCH** в заголовках запросов должно содержать значение **etag** списка или его элемента. Это конкретное значение применимо только к спискам и их элементам. Оно призвано помочь вам избежать проблем с параллелизмом при обновлении этих сущностей. В предыдущем примере вместо этого значения используется звездочка (*). Так можно делать, когда нет причин волноваться о проблемах с параллелизмом. В противном случае необходимо получить значение **etag** списка или его элемента, выполнив запрос **GET** на получение сущности. В заголовках полученного HTTP-отклика значение etag передается в качестве значения ключа **ETag**. Это значение также входит в состав метаданных сущности. 

В приведенном ниже примере показан открывающий тег `<entry>` узла XML, содержащий данные списка. Свойство **m:etag** содержит значение **etag**.

```XML
<entry xml:base="http://site url/_api/" xmlns=http://www.w3.org/2005/Atom 
xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" 
xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns:georss="http://www.georss.org/georss" xmlns:gml="http://www.opengis.net/gml" m:etag=""1"">
```

<br/>

<a name="bk_CreateSite"> </a>

## <a name="creating-a-site-with-rest"></a>Создание сайта с помощью REST

В приведенном ниже примере показано, как создать сайт на JavaScript.

```
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
> [!NOTE] 
> Если задать для свойства **WebTemplate** значение "sts", будет создана современная домашняя страница. Чтобы создать классическую домашнюю страницу, задайте для свойства **WebTemplate** значение "sts#0". 
<br/>

<a name="bk_HowRequestsDiffer"> </a>

## <a name="how-rest-requests-differ-by-environment"></a>Отличия между запросами REST в разных средах

Методы составления и отправки HTTP-запросов могут различаться в зависимости от языка, библиотеки и типа надстройки, поэтому при переводе запроса из одной среды в другую часто требуется изменять один или несколько компонентов запросов. Например, запросы jQuery AJAX используют параметры **data** и **type**, чтобы указывать тело и тип запроса, в то время как запросы междоменных библиотек используют параметры **body** и **method**.

В приведенных ниже разделах описаны другие распространенные отличия между средами.

<a name="FormDigest"> </a> 

### <a name="the-way-you-get-and-send-the-form-digest-value-depends-on-the-add-in"></a>Способ получения и отправки значения дайджеста формы зависит от надстройки

При отправке запроса POST в его заголовке **X-RequestDigest** должно быть указано значение дайджеста формы. Однако способ получения и отправки значения зависит от надстройки:

- В надстройках с размещением в SharePoint можно передавать следующий заголовок: 
 
    `"X-RequestDigest": $("#__REQUESTDIGEST").val()`

- Надстройки с размещением в облаке, использующие OAuth, сначала получают значение дайджеста формы, отправляя запрос к конечной точке **contextinfo**, а затем добавляя его в запросы, как показано в разделе  [Запись данных с помощью интерфейса REST](complete-basic-operations-using-sharepoint-rest-endpoints.md#WritingData).

- В надстройках с размещением в облаке, которые используют междоменную библиотеку JavaScript, не требуется указывать значение дайджеста формы. По умолчанию SP.RequestExecutor делает это автоматически. (Метод также обрабатывает значение content-length.)
    
<a name="OAuthTokens"> </a> 

### <a name="add-ins-that-use-oauth-must-pass-access-tokens-in-requests"></a>Надстройки, использующие OAuth, должны передавать маркеры доступа в запросах

Надстройки с размещением в облаке используют OAuth или междоменную библиотеку для авторизации доступа к данным SharePoint. Компоненты надстроек с кодом, выполняющимся на удаленном веб-сервере, должны использовать OAuth для авторизации доступа к данным SharePoint. В этом случае необходимо включить в запрос заголовок **Authorization** для отправки маркера доступа. Пример добавления заголовка авторизации к объекту **HTTPWebRequest** см. в разделе [Считывание данных с помощью интерфейса REST SharePoint](complete-basic-operations-using-sharepoint-rest-endpoints.md#ReadingData).
 
> [!NOTE] 
> Компоненты надстроек с размещением в облаке, написанные на JavaScript, должны использовать объект **SP.RequestExecutor** из междоменной библиотеки для доступа к данным SharePoint. В запросы к междоменной библиотеке не обязательно включать маркер доступа.

Дополнительные сведения о маркерах доступа OAuth и их получении см. в статьях [Поток маркеров контекста OAuth для надстроек в SharePoint](context-token-oauth-flow-for-sharepoint-add-ins.md) и [Поток кода авторизации OAuth для надстроек в SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md). 

<a name="AppContextSite"> </a> 

### <a name="endpoint-uris-in-cross-domain-requests-use-spappcontextsite-to-change-the-context"></a>URI конечных точек в междоменных запросах используют объект SP.AppContextSite для изменения контекста

Запросы отправляются к конечной точке ресурсов, указанной в свойстве **url** запроса. URI конечных точек имеют следующий формат:
 
`<site url>/_api/<context>/<resource>` (например, https://contoso.com/_api/web/lists)

Запросы к междоменным библиотекам имеют такой формат при доступе к данным на сайте надстройки, стандартном контексте запросов к междоменным библиотекам. Тем не менее, для доступа к данным на сайте надстройки или в другом семействе веб-сайтов запросам необходимо инициализировать хост-сайт или другое семейство веб-сайтов в качестве контекста. Для этого они используют конечную точку **SP.AppContextSite** из URI, как показано в таблице 1. В примерах URI из таблицы 1 используется псевдоним **@target** для отправки целевого URL-адреса в строке запроса, так как URL-адрес содержит специальный символ (":").
 
> [!NOTE] 
> Для доступа к данным SharePoint при использовании междоменной библиотеки надстройке с размещением в облаке необходим экземпляр сайта надстройки.

**Таблица 1. Изменение контекста запроса с помощью конечной точки SP.AppContextSite**

|**Тип надстройки**|**Сценарий междоменного доступа к данным**|**Пример URI конечной точки**|
|:-----|:-----|:-----|
|С размещением в облаке|Компонент надстройки JavaScript получает доступ к данным хост-сайта с помощью междоменной библиотеки|`<app web url>/_api/SP.AppContextSite(@target)/web/lists?@target='<host web url>'`|
|Размещение в облаке|Компонент надстройки JavaScript получает доступ к данным в семействе веб-сайтов, не включающем хост-сайт, с помощью междоменной библиотеки (только для надстроек с разрешениями на уровне клиента)|`<app web url>/_api/SP.AppContextSite(@target)/web/title?@target='<target site url>'`|
|Размещение в SharePoint|Компонент сайта надстройки получает доступ к данным в другом семействе веб-сайтов (только для надстроек с разрешениями на уровне клиента)|`<app web url>/_api/SP.AppContextSite(@target)/web/title?@target='<target site url>'`|

> [!NOTE] 
> Для доступа к данным между доменами надстройке также необходимы соответствующие разрешения. Дополнительные сведения см. в разделах [Доступ к данным на хост-сайте](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_Hostweb) и [Доступ к данным в нескольких семействах веб-сайтов](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md#SP15Accessdatafromremoteapp_TenantScope).
 
Надстройки SharePoint могут получать URL-адреса сайта надстройки и хост-сайта из строки запроса на странице надстройки, как показано в приведенном ниже примере кода. В этом примере также показано, как ссылаться на междоменную библиотеку, определенную в файле SP.RequestExecutor.js на хост-сайте. В этом примере предполагается, что надстройка запускается из SharePoint. Рекомендации по правильной настройке контекста SharePoint в том случае, если надстройка не запускается из SharePoint, см. в статье [Поток кода авторизации OAuth для надстроек SharePoint](authorization-code-oauth-flow-for-sharepoint-add-ins.md). 

```
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
??? // success and error callback functions
```

<br/>

<a name="bk_requestElements"> </a>

## <a name="properties-used-in-rest-requests"></a>Свойства, используемые в запросах REST

В таблице 2 показаны свойства, которые часто используются в HTTP-запросах для службы REST SharePoint.

**Таблица 2. Использование свойств запроса REST в HTTP-запросах**

|**Свойства**|**Когда требуется**|**Описание**|
|:-----|:-----|:-----|
|**url**|Все запросы|URL-адрес конечной точки ресурса REST. Например:  `http://<site url>/_api/web/lists`|
|**method** (или **type**)|Все запросы|Метод HTTP-запроса: **GET** для операций чтения и **POST** для операций записи. Запросы **POST** могут выполнять операции обновления или удаления, используя команду **DELETE**, **MERGE** или **PUT** в заголовке **X-HTTP-Method**.  |
|**body** (или **data**)|Запросы **POST**, которые отправляют данные в тексте запроса|Тело запроса POST. Отправляет данные (например, сложные типы), которые нельзя передать в URI конечной точки. Используется с заголовком **content-length**.|
|Заголовок **Authentication**|Удаленные надстройки, которые используют OAuth для проверки подлинности пользователей. Не применяется при использовании JavaScript или междоменной библиотеки. |Отправляет маркер доступа (полученный от сервера токенов безопасности для службы контроля доступа Microsoft Azure), который используется для проверки подлинности пользователя для запроса. Например:  `"Authorization": "Bearer " + accessToken`, где  `accessToken` представляет переменную, которая сохраняет маркер. Маркеры должны загружаться с использованием кода на стороне сервера. |
|Заголовок **X-RequestDigest**|Запросы **POST** (кроме запросов SP.RequestExecutor)|Удаленные надстройки, использующие протокол OAuth, могут получить значение дайджеста формы от конечной точки  `http://<site url>/_api/contextinfo`. Надстройки, размещенные в SharePoint, могут получить это значение от элемента управления страницей **#__REQUESTDIGEST**, если он доступен на странице SharePoint. См. раздел  [Запись данных с помощью интерфейса REST](#WritingData).  |
|Заголовок **accept**|Запросы, которые возвращают метаданные SharePoint|Указывает формат данных ответа от сервера. Форматом по умолчанию является  `application/atom+xml`, например:  `"accept":"application/json;odata=verbose"`|
|Заголовок **content-type**|Запросы **POST**, которые отправляют данные в тексте запроса|Указывает формат данных, которые клиент отправляет серверу. Форматом по умолчанию является  `application/atom+xml`, например:  `"content-type":"application/json;odata=verbose"`|
|Заголовок **content-length**|Запросы **POST**, которые отправляют данные в тексте запроса (кроме запросов SP.RequestExecutor)|Указывает длину содержимого, например:  `"content-length":requestBody.length`|
|Заголовок **IF-MATCH**|Запросы **POST** для операций **DELETE**, **MERGE** и **PUT** (в первую очередь для изменения списков и библиотек). |Предоставляет способ проверки того, что изменяемый объект не менялся с момента его последней загрузки. Или позволяет включить перезапись любых изменений, как показано в следующем примере:  `"IF-MATCH":"*"`|
|Заголовок **X-HTTP-Method**|**POST** запрашивает операции **DELETE**, **MERGE** или **PUT**|Указывает, что запрос выполняет операцию обновления или удаления. Пример: `"X-HTTP-Method":"PUT"`|
|**binaryStringRequestBody**|Запросы **POST**, которые отправляют двоичные данные в теле запроса|Указывает, является ли текст запроса двоичной строкой. **Boolean**.|
|**binaryStringResponseBody**|Запросы SP.RequestExecutor, возвращающие двоичные данные|Указывает, является ли ответ двоичной строкой. **Boolean**.|

<br/>

<a name="batch"> </a>

## <a name="batch-job-support"></a>Поддержка пакетных заданий

Служба REST в SharePoint Online (а также локальной среде SharePoint 2016 или более поздней версии) поддерживает объединение нескольких запросов в один вызов службы с помощью параметра запроса OData `$batch`. Подробные сведения и ссылки на примеры кода см. в статье [Отправка пакетных запросов с помощью интерфейсов REST API](make-batch-requests-with-the-rest-apis.md).

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Знакомство со службой REST в SharePoint](get-to-know-the-sharepoint-rest-service.md)
- [SharePoint: выполнение основных операций доступа к данным в файлах и папках с помощью REST](http://code.msdn.microsoft.com/SharePoint-Perform-ab9c4ae5)
- [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
- [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint.md)
- [Материалы по OData](get-to-know-the-sharepoint-rest-service.md#odata-resources)
- [Назначение настраиваемых разрешений для списка с помощью интерфейса REST](set-custom-permissions-on-a-list-by-using-the-rest-interface.md) 
- [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)

 

 

