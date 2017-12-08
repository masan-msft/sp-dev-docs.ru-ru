---
title: "Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 779998ed1b8929a1b23537fc577f8be2a1cbb0ba
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="complete-basic-operations-using-javascript-library-code-in-sharepoint"></a>Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint
Узнайте, как писать код для выполнения базовых операций с помощью клиентской объектной модели JavaScript в SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 


 **Примечание.** Пример создания надстройки SharePoint "Hello World", использующей библиотеку JavaScript, см. в статье [Использование API JavaScript для SharePoint для работы с данными SharePoint](use-the-sharepoint-javascript-apis-to-work-with-sharepoint-data.md).
 


## <a name="sharepoint-client-apis"></a>Клиентские интерфейсы API SharePoint
<a name="ClientAPIs"> </a>

Вы можете использовать клиентскую объектную модель SharePoint для извлечения, обновления данных и управления ими в SharePoint. SharePoint предоставляет объектные модели в нескольких формах.
 

 

- Распространяемые сборки .NET Framework
    
 
- библиотека JavaScript;
    
 
- конечные точки REST и OData;
    
 
- Сборки Windows Phone
    
 
- Распространяемые сборки Silverlight
    
 
Дополнительные сведения о наборах API, доступных для SharePoint, см. в статье [Выбор правильного набора API в SharePoint](http://msdn.microsoft.com/library/f36645da-77c5-47f1-a2ca-13d4b62b320d%28Office.15%29.aspx). 
 

 
В этой статье описано, как выполнять базовые операции с помощью объектной модели JavaScript. Вы можете добавить ссылку на объектную модель, используя HTML-теги &lt;script&gt;. Сведения об использовании других клиентских API-интерфейсов см. в следующих статьях:
 

 

-  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [Построение приложений Windows Phone, обращающихся к SharePoint](http://msdn.microsoft.com/library/36681335-f772-4499-8445-f94481bc18e7%28Office.15%29.aspx)
    
 
-  [Использование объектной модели Silverlight](http://msdn.microsoft.com/library/cea7829d-f360-4052-8b76-91d90bcefd2a%28Office.15%29.aspx)
    
 

## <a name="perform-basic-tasks-in-sharepoint-using-the-javascript-client-object-model"></a>Выполнение основных задач в SharePoint с помощью клиентской объектной модели JavaScript
<a name="BasicOps_SPJSOMOps"> </a>

В следующих разделах описываются задачи, которые вы можете выполнять программным путем. Они включают примеры кода на языке JavaScript, в которых демонстрируются эти операции.
 

 
При создании облачной надстройки можно добавить ссылку на объектную модель с помощью HTML-тегов &lt;script&gt;. Рекомендуем создать ссылку на хост-сайт, так как сайт надстройки может существовать не в каждом сценарии работы с облачными надстройками. Вы можете получить URL-адрес хост-сайта из параметра строки запроса _SPHostUrl_, если используете токен **{StandardTokens}**. Вы также можете использовать специальный параметр строки запроса, если применяете токен **{HostUrl}**. После получения URL-адреса хост-сайта вам нужно с помощью кода JavaScript динамично создать ссылку на объектную модель.
 

 
В приведенном ниже примере кода выполняются такие задачи для добавления ссылки на объектную модель JavaScript:
 

 

- Создание ссылки на библиотеку AJAX из сети Microsoft Content Delivery Network (CDN).
    
 
- Создание ссылки на библиотеку jQuery из сети Microsoft CDN.
    
 
- Извлечение URL-адреса хост-сайта из строки запроса.
    
 
- Загрузка файлов SP.Runtime.js и SP.js с помощью функции **getScript** в jQuery. После загрузки файлов программа получает доступ к объектной модели JavaScript для SharePoint.
    
 
- Продолжение рабочего процесса функции **execOperation**.
    
 



```
<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script
    type="text/javascript"
    src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
</script>
<script type="text/javascript">
    var hostweburl;

    // Load the required SharePoint libraries.
    $(document).ready(function () {

        // Get the URI decoded URLs.
        hostweburl =
            decodeURIComponent(
                getQueryStringParameter("SPHostUrl")
        );

        // The js files are in a URL in the form:
        // web_url/_layouts/15/resource_file
        var scriptbase = hostweburl + "/_layouts/15/";

        // Load the js files and continue to
        // the execOperation function.
        $.getScript(scriptbase + "SP.Runtime.js",
            function () {
                $.getScript(scriptbase + "SP.js", execOperation);
            }
        );
    });

    // Function to execute basic operations.
    function execOperation() {

        // Continue your program flow here.

    }

    // Function to retrieve a query string value.
    // For production purposes you may want to use
    // a library to handle the query string.
    function getQueryStringParameter(paramToRetrieve) {
        var params =
            document.URL.split("?")[1].split("&amp;");
        var strParams = "";
        for (var i = 0; i < params.length; i = i + 1) {
            var singleParam = params[i].split("=");
            if (singleParam[0] == paramToRetrieve)
                return singleParam[1];
        }
    }
</script>

```

При создании надстройки, размещаемой в SharePoint, можно добавить ссылку на объектную модель с помощью HTML-тегов &lt;script&gt;. Сайт надстройки, размещаемой в SharePoint, позволяет ссылаться на обязательные файлы для использования в объектной модели JavaScript, указывая относительные пути.
 

 
Следующая разметка выполняет указанные далее задачи для добавления ссылки на объектную модель JavaScript:
 

 

- Создание ссылки на библиотеку AJAX из сети Microsoft CDN.
    
 
- Создание ссылки на файл SP.Runtime.js с использованием относительного URL-адреса сайта надстройки.
    
 
- Создание ссылки на файл SP.js с использованием относительного URL-адреса сайта надстройки.
    
 



```
<script 
    src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
    type="text/javascript">
</script>
<script 
    type="text/javascript" 
    src="/_layouts/15/sp.runtime.js">
</script>
<script 
    type="text/javascript" 
    src="/_layouts/15/sp.js">
</script>
<script type="text/javascript">

    // Continue your program flow here.

</script>
```


## <a name="sharepoint-website-tasks"></a>Задачи, связанные с веб-сайтом SharePoint
<a name="BasicOps_SPWebTasks"> </a>

Для работы с веб-сайтами с использованием JavaScript начните с использования конструктора **ClientContext(serverRelativeUrl)** и передачи URL-адреса или URI-кода для возврата определенного контекста запроса.
 

 

### <a name="retrieve-the-properties-of-a-website"></a>Получение свойств веб-сайта

Используйте веб-свойства класса **ClientContext**, чтобы указать свойства объекта веб-сайта, который размещен по указанному URL-адресу контекста. После загрузки объекта веб-сайта с помощью метода **load(clientObject)** и вызова **executeQueryAsync(succeededCallback, failedCallback)** можно получить доступ ко всем свойствам этого веб-сайта. В приведенном ниже примере отображается заголовок и описание указанного веб-сайта, хотя все другие возвращаемые свойства по умолчанию становятся доступными после загрузки объекта веб-сайта и выполнения запроса.
 

 

```

function retrieveWebSite(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    clientContext.load(this.oWebsite);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Description: ' + this.oWebsite.get_description());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="retrieve-only-selected-properties-of-a-website"></a>Получение определенных свойств веб-сайта

Для снижения объема передаваемых данных между клиентом и сервером можно получать только указанные свойства объекта веб-сайта, а не все свойства. В этом случае используйте запрос LINQ или синтаксис лямбда-выражений с методом **load(clientObject)** для определения того, какие свойства следует получать от сервера. В приведенном ниже примере после вызова запроса **executeQueryAsync(succeededCallback, failedCallback)** доступны только заголовок и дата создания объекта веб-сайта.
 

 

```
function retrieveWebSiteProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    clientContext.load(this.oWebsite, 'Title', 'Created');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Created: ' + this.oWebsite.get_created());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


 **Примечание.** Если вы попытаетесь обратиться к другим свойствам, код создаст исключение, так как они недоступны.
 


### <a name="write-to-a-websites-properties"></a>Запись значений для свойств веб-сайта

Для изменения веб-сайта следует задать его свойства и вызвать метод **update()** аналогично применению серверной объектной модели. Однако в клиентской объектной модели следует вызвать **executeQueryAsync(succeededCallback, failedCallback)** для запроса пакетной обработки всех указанных команд. В приведенном ниже примере изменяется заголовок и описание указанного веб-сайта.
 

 

```
function updateWebSite(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    this.oWebsite = clientContext.get_web();

    this.oWebsite.set_title('Updated Web Site');
    this.oWebsite.set_description('This is an updated Web site.');
    this.oWebsite.update();

    clientContext.load(this.oWebsite, 'Title', 'Description');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    alert('Title: ' + this.oWebsite.get_title() + 
        ' Description: ' + this.oWebsite.get_description());
}
    
function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


## <a name="sharepoint-list-tasks"></a>Задачи по работе со списками SharePoint
<a name="BasicOps_SPListTasks"> </a>

Работа с объектами списков с использованием JavaScript похожа на работу с объектами веб-сайтов. Начинайте работу с использования конструктора **ClientContext(serverRelativeUrl)** и передачи URL-адреса или URI-кода для возврата определенного контекста запроса. После этого можно использовать свойство **lists** класса **Web** для получения коллекции списков на веб-сайте.
 

 

### <a name="retrieve-all-properties-of-all-lists-in-a-website"></a>Извлечение всех свойств всех списков на веб-сайте

Для возврата всех списков веб-сайта загрузите коллекцию списков с помощью метода **load(clientObject)**, а затем вызовите **executeQueryAsync(succeededCallback, failedCallback)**. В приведенном ниже примере представлен URL-адрес веб-сайта, а также дата и время создания списка.
 

 

```
function retrieveAllListProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.collList = oWebsite.get_lists();
    clientContext.load(collList);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';
    var listEnumerator = collList.getEnumerator();

    while (listEnumerator.moveNext()) {
        var oList = listEnumerator.get_current();
        listInfo += 'Title: ' + oList.get_title() + ' Created: ' + 
            oList.get_created().toString() + '\n';
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="retrieve-only-specified-properties-of-lists"></a>Извлечение только заданных свойств списков

В предыдущем примере выполнялся возврат всех свойств списков на веб-сайте. Для уменьшения ненужных данных, передаваемых между клиентом и сервером, можно использовать выражения запросов LINQ, чтобы указать возвращаемые свойства. В JavaScript следует указать **Include** как часть строки запроса, которая передается в метод **load(clientObject)** для указания возвращаемых свойств. В приведенном ниже примере этот подход используется для возврата только заголовка и идентификатора каждого из списков в коллекции.
 

 

```
function retrieveSpecificListProperties(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.collList = oWebsite.get_lists();

    clientContext.load(collList, 'Include(Title, Id)');
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';
    var listEnumerator = collList.getEnumerator();

    while (listEnumerator.moveNext()) {
        var oList = listEnumerator.get_current();
        listInfo += 'Title: ' + oList.get_title() + 
            ' ID: ' + oList.get_id().toString() + '\n';
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```


### <a name="store-retrieved-lists-in-a-collection"></a>Хранение полученных списков в коллекции

Как показывает следующий пример, вы можете использовать метод **loadQuery(clientObjectCollection, exp)** вместо метода **load(clientObject)** для хранения возвращаемого значения в другой коллекции вместо того, чтобы хранить его в свойстве списков.
 

 

```
function retrieveSpecificListPropertiesToCollection(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    var collList = oWebsite.get_lists();

    this.listInfoCollection = clientContext.loadQuery(collList, 'Include(Title, Id)');
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';

    for (var i = 0; i < this.listInfoCollection.length; i++) {
        var oList = this.listInfoCollection[i];
        listInfo += 'Title: ' + oList.get_title() + 
            ' ID: ' + oList.get_id().toString();
    }
    alert(listInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="apply-filters-to-list-retrieval"></a>Применение фильтров для извлечения списков

Как показано в приведенном ниже примере, операторы **Include** можно вкладывать в запрос JavaScript, чтобы возвратить метаданные как для списка, так и для его полей. В примере возвращаются все поля из всех списков на веб-сайте, а также отображаются заголовок и внутреннее имя всех полей, чье внутреннее имя содержит строку "name".
 

 

```
function retrieveAllListsAllFields(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    var collList = oWebsite.get_lists();

    this.listInfoArray = clientContext.loadQuery(collList, 
        'Include(Title,Fields.Include(Title,InternalName))');

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this._onQueryFailed)
    );
}

function onQuerySucceeded() {
    var listInfo = '';

    for (var i = 0; i < this.listInfoArray.length; i++) {
        var oList = this.listInfoArray[i];
        var collField = oList.get_fields();
        var fieldEnumerator = collField.getEnumerator();
            
        while (fieldEnumerator.moveNext()) {
            var oField = fieldEnumerator.get_current();
            var regEx = new RegExp('name', 'ig');
            
            if (regEx.test(oField.get_internalName())) {
                listInfo += '\nList: ' + oList.get_title() + 
                    '\n\tField Title: ' + oField.get_title() + 
                    '\n\tField Name: ' + oField.get_internalName();
            }
        }
    }
    alert(listInfo);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```


## <a name="create-update-and-delete-lists"></a>Создание, обновление и удаление списков
<a name="BasicOps_SPListCRUD"> </a>

Создание, обновление и удаление списков с использованием клиентской объектной модели аналогично выполнению этих операций с помощью клиентской объектной модели .NET, хотя клиентские операции не будут завершены до вызова функции **executeQueryAsync(succeededCallback, failedCallback)**.
 

 

### <a name="create-and-update-a-list"></a>Создание и обновление списка

Для создания объекта списка с помощью JavaScript используйте объект **ListCreationInformation**, чтобы определить его свойства, и передайте объект в функцию **add(parameters)** объекта **ListCollection**. В приведенном ниже примере создается новый список объявлений.
 

 

```
function createList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    
    var listCreationInfo = new SP.ListCreationInformation();
    listCreationInfo.set_title('My Announcements List');
    listCreationInfo.set_templateType(SP.ListTemplateType.announcements);

    this.oList = oWebsite.get_lists().add(listCreationInfo);

    clientContext.load(oList);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = oList.get_title() + ' created.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

Если нужно обновить список после его создания, можно задать свойства списка и вызвать функцию **update()** перед вызовом **executeQueryAsync(succeededCallback, failedCallback)**, как показано далее в измененном примере.
 

 



```
.
.
.
.
this.oList = oWebsite.get_lists().add(listCreationInfo);

oList.set_description('New Announcements List');
oList.update();

clientContext.load(oList);
clientContext.executeQueryAsync(
    Function.createDelegate(this, this.onQuerySucceeded), 
    Function.createDelegate(this, this.onQueryFailed)
);
```


### <a name="add-a-field-to-a-list"></a>Добавление поля в список

Используйте функцию **add(field)** или **addFieldAsXml(schemaXml, addToDefaultView, options)** объекта **FieldCollection** для добавления поля в коллекцию полей списка. В приведенном ниже примере создается поле, которое затем обновляется перед вызовом **executeQueryAsync(succeededCallback, failedCallback)**.
 

 

```
function addFieldToList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);

    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    this.oField = oList.get_fields().addFieldAsXml(
        '<Field DisplayName=\'MyField\' Type=\'Number\' />', 
        true, 
        SP.AddFieldOptions.defaultValue
    );

    var fieldNumber = clientContext.castTo(oField,SP.FieldNumber);
    fieldNumber.set_maximumValue(100);
    fieldNumber.set_minimumValue(35);
    fieldNumber.update();

    clientContext.load(oField);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = oField.get_title() + ' added.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="delete-a-list"></a>Удаление списка

Чтобы удалить список, вызовите функцию **deleteObject()** объекта списка, как показано в приведенном ниже примере.
 

 

```
function deleteList(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oWebsite = clientContext.get_web();
    this.listTitle = 'My Announcements List';

    this.oList = oWebsite.get_lists().getByTitle(listTitle);
    oList.deleteObject();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    var result = listTitle + ' deleted.';
    alert(result);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


## <a name="create-update-and-delete-folders"></a>Создание, обновление и удаление папок
<a name="BasicOps_FolderTasks"> </a>

Вы можете работать с папками, упорядочивая контент, с помощью объектной модели JavaScript. В следующих разделах рассказывается об основных операциях с папками.
 

 

### <a name="create-a-folder-in-a-document-library"></a>Создание папки в библиотеке документов

Чтобы создать папку, нужно использовать объект **ListItemCreationInformation**, задав базовый тип объекта как **SP.FileSystemObjectType.folder**, и передать его в виде параметра в функцию **addItem(parameters)** объекта **List**. Задайте свойства объекта элемента списка, возвращенного этим методом, и вызовите функцию **update()**, как показано в приведенном ниже примере.
 

 

```
function createFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var itemCreateInfo;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    itemCreateInfo = new SP.ListItemCreationInformation();
    itemCreateInfo.set_underlyingObjectType(SP.FileSystemObjectType.folder);
    itemCreateInfo.set_leafName("My new folder!");
    this.oListItem = oList.addItem(itemCreateInfo);
    this.oListItem.set_item("Title", "My new folder!");
    this.oListItem.update();

    clientContext.load(this.oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your new folder.";
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="update-a-folder-in-a-document-library"></a>Обновление папки в библиотеке документов

Чтобы обновить имя папки, вы можете записать его в свойство **FileLeafRef** и вызвать функцию **update()**, чтобы изменения вступили в силу при вызове метода **executeQueryAsync**.
 

 

```
function updateFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    this.oListItem = oList.getItemById(1);
    this.oListItem.set_item("FileLeafRef", "My updated folder");
    this.oListItem.update();

    clientContext.load(this.oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your updated folder.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="delete-a-folder-in-a-document-library"></a>Удаление папки в библиотеке документов

Чтобы удалить папку, следует вызвать функцию **deleteObject()** объекта. В приведенном ниже примере метод **getFolderByServerRelativeUrl** используется для извлечения папки из библиотеки документов и удаления элемента.
 

 

```
function deleteFolder(resultpanel) {
    var clientContext;
    var oWebsite;
    var folderUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        folderUrl = oWebsite.get_serverRelativeUrl() + "/Lists/Shared Documents/Folder1";
        this.folderToDelete = oWebsite.getFolderByServerRelativeUrl(folderUrl);
        this.folderToDelete.deleteObject();

        clientContext.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
    }, errorHandler);

    function successHandler() {
        resultpanel.innerHTML = "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to make sure the folder is no longer there.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


## <a name="create-read-update-and-delete-files"></a>Создание, чтение, обновление и удаление файлов
<a name="BasicOps_FileTasks"> </a>

Вы можете работать с файлами с помощью объектной модели JavaScript. В приведенных ниже разделах рассказывается об основных операциях с файлами.
 

 

 **Примечание.** С помощью объектной модели JavaScript можно работать только с файлами размером до 1,5 МБ. Чтобы отправлять более крупные файлы, используйте REST. Дополнительные сведения см. в разделе [](complete-basic-operations-using-sharepoint-rest-endpoints.md#LargeFiles).
 


### <a name="create-a-file-in-a-document-library"></a>Создание файла в библиотеке документов

Для создания файлов используйте объект **FileCreationInformation**, задав атрибут URL и добавив содержимое в виде байтового массива в кодировке Base64, как показано в приведенном ниже примере.
 

 

```
function createFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var fileCreateInfo;
    var fileContent;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    fileCreateInfo = new SP.FileCreationInformation();
    fileCreateInfo.set_url("my new file.txt");
    fileCreateInfo.set_content(new SP.Base64EncodedByteArray());
    fileContent = "The content of my new file";

    for (var i = 0; i < fileContent.length; i++) {
        
        fileCreateInfo.get_content().append(fileContent.charCodeAt(i));
    }

    this.newFile = oList.get_rootFolder().get_files().add(fileCreateInfo);

    clientContext.load(this.newFile);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see your new file.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="read-a-file-in-a-document-library"></a>Чтение файла в библиотеке документов

Для чтения содержимого файла используйте операцию **GET** с URL-адресом файла, как показано в приведенном ниже примере.
 

 

```
function readFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var fileUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        fileUrl = oWebsite.get_serverRelativeUrl() +
            "/Lists/Shared Documents/TextFile1.txt";
        $.ajax({
            url: fileUrl,
            type: "GET"
        })
            .done(Function.createDelegate(this, successHandler))
            .error(Function.createDelegate(this, errorHandler));
    }, errorHandler);

    function successHandler(data) {
        resultpanel.innerHTML =
            "The content of file \"TextFile1.txt\": " + data
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[2];
    }
}
```


### <a name="update-a-file-in-a-document-library"></a>Обновление файла в библиотеке документов

Чтобы обновить содержимое файла, используйте объект **FileCreationInformation** и задайте атрибуту перезаписи значение "true" с помощью метода **set_overwrite()**, как показано в приведенном ниже примере.
 

 

```
function updateFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var oList;
    var fileCreateInfo;
    var fileContent;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();
    oList = oWebsite.get_lists().getByTitle("Shared Documents");

    fileCreateInfo = new SP.FileCreationInformation();
    fileCreateInfo.set_url("TextFile1.txt");
    fileCreateInfo.set_content(new SP.Base64EncodedByteArray());
    fileCreateInfo.set_overwrite(true);
    fileContent = "The updated content of my file";

    for (var i = 0; i < fileContent.length; i++) {

        fileCreateInfo.get_content().append(fileContent.charCodeAt(i));
    }

    this.existingFile = oList.get_rootFolder().get_files().add(fileCreateInfo);

    clientContext.load(this.existingFile);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, successHandler),
        Function.createDelegate(this, errorHandler)
    );

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to see the updated \"TextFile1.txt\" file.";
    }

    function errorHandler() {
        resultpanel.innerHTML =
            "Request failed: " + arguments[1].get_message();
    }
}
```


### <a name="delete-a-file-in-a-document-library"></a>Удаление файла в библиотеке документов

Чтобы удалить файл, следует вызвать функцию **deleteObject()** объекта. В приведенном ниже примере метод **getFileByServerRelativeUrl** используется для извлечения файла из библиотеки документов и удаления этого элемента.
 

 

```
function deleteFile(resultpanel) {
    var clientContext;
    var oWebsite;
    var fileUrl;

    clientContext = new SP.ClientContext.get_current();
    oWebsite = clientContext.get_web();

    clientContext.load(oWebsite);
    clientContext.executeQueryAsync(function () {
        fileUrl = oWebsite.get_serverRelativeUrl() +
            "/Lists/Shared Documents/TextFile1.txt";
        this.fileToDelete = oWebsite.getFileByServerRelativeUrl(fileUrl);
        this.fileToDelete.deleteObject();

        clientContext.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
    }, errorHandler);

    function successHandler() {
        resultpanel.innerHTML =
            "Go to the " +
            "<a href='../Lists/Shared Documents'>document library</a> " +
            "to confirm that the \"TextFile1.txt\" file has been deleted.";
    }

    function errorHandler() {
        resultpanel.innerHTML = "Request failed: " + arguments[1].get_message();
    }
}
```


## <a name="sharepoint-list-item-tasks"></a>Задачи, связанные с элементами списков SharePoint
<a name="BasicOps_SPListItemTasks"> </a>

Для получения элементов из списка с помощью JavaScript используйте функцию **getItemById(id)** для возврата одного элемента или функцию **getItems(query)** для извлечения нескольких элементов. Затем можно использовать функцию **load(clientObject)**, чтобы получить объекты, представляющие элементы списка.
 

 

### <a name="retrieve-items-from-a-list"></a>Получение элементов из списка

Функция **getItems(query)** позволяет задавать запрос на языке CAML, который определяет возвращаемые элементы. Вы можете передать неопределенный объект **CamlQuery** для возврата всех элементов из списка или использовать функцию **set_viewXml** для определения запроса CAML и возврата элементов, которые отвечают определенным критериям. В приведенном ниже примере отображается идентификатор (помимо значений столбцов Title и Body) первых 100 элементов списка объявлений, начиная с элементов списка, идентификатор коллекции которых больше 10.
 

 

```
function retrieveListItems(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
        
    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml(
        '<View><Query><Where><Geq><FieldRef Name=\'ID\'/>' + 
        '<Value Type=\'Number\'>1</Value></Geq></Where></Query>' + 
        '<RowLimit>10</RowLimit></View>'
    );
    this.collListItem = oList.getItems(camlQuery);
        
    clientContext.load(collListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    ); 
}

function onQuerySucceeded(sender, args) {
    var listItemInfo = '';
    var listItemEnumerator = collListItem.getEnumerator();
        
    while (listItemEnumerator.moveNext()) {
        var oListItem = listItemEnumerator.get_current();
        listItemInfo += '\nID: ' + oListItem.get_id() + 
            '\nTitle: ' + oListItem.get_item('Title') + 
            '\nBody: ' + oListItem.get_item('Body');
    }

    alert(listItemInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="use-the-include-method-to-access-properties-of-listitem-objects"></a>Используйте метод Include для доступа к свойствам объектов ListItem

Четыре свойства объектов **ListItem** недоступны по умолчанию при возврате элементов списка: **displayName**, **effectiveBasePermissions**, **hasUniqueRoleAssignments** и **roleAssignments**. В предыдущем примере, если попытаться получить доступ к одному из этих свойств, возвращается исключение **PropertyOrFieldNotInitializedException**. Для доступа к этим свойствам используйте метод **Include** как часть строки запроса, как показано в приведенном ниже примере.
 

 

 **Примечание.** При создании запросов для клиентской объектной модели с помощью LINQ применяется поставщик [LINQ to Objects](http://msdn.microsoft.com/library/bb397919), а не [LINQ to SharePoint](http://msdn.microsoft.com/library/ee535491), который можно использовать только при написании кода для серверной объектной модели.
 


```
function retrieveListItemsInclude(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');

    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml('<View><RowLimit>100</RowLimit></View>');
    this.collListItem = oList.getItems(camlQuery);

    clientContext.load(
        collListItem, 
        'Include(Id, DisplayName, HasUniqueRoleAssignments)'
    );
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded(sender, args) {
    var listItemInfo = '';
    var listItemEnumerator = collListItem.getEnumerator();
        
    while (listItemEnumerator.moveNext()) {
        var oListItem = listItemEnumerator.get_current();
        listItemInfo += '\nID: ' + oListItem.get_id() + 
            '\nDisplay name: ' + oListItem.get_displayName() + 
            '\nUnique role assignments: ' + 
            oListItem.get_hasUniqueRoleAssignments();
    }

    alert(listItemInfo.toString());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}

```

Так как в этом примере используется **Include**, после выполнения запроса доступны только указанные свойства. Поэтому возвращается исключение **PropertyOrFieldNotInitializedException** при попытке доступа к другим свойствам помимо указанных. Кроме того, эта ошибка возникает, если вы пытаетесь использовать такие функции как **get_contentType** или **get_parentList** для получения доступа к объектам, которые они содержат.
 

 

### <a name="restrictions-on-retrieving-items"></a>Ограничения на получение элементов

Метод **loadQuery(clientObjectCollection, exp)** объектной модели JavaScript в SharePoint Foundation 2010 не поддерживает методы и операторы LINQ, которые используются в управляемой объектной модели.
 

 

## <a name="create-update-and-delete-list-items"></a>Создание, обновление и удаление элементов списков
<a name="BasicOps_SPListItemCRUD"> </a>

Создание, обновление и удаление элементов списка с помощью клиентской объектной модели работает аналогично выполнению этих задач с помощью серверной объектной модели. Можно создать объект элемента списка, установить его свойства, а затем обновить этот объект. Чтобы изменить или удалить объект элемента списка, необходимо вернуть этот объект с помощью функции **getById(id)** объекта **ListItemCollection**, а затем либо установить свойства и вызвать обновление в объекте, возвращенном методом, либо вызвать собственный метод объекта для удаления. В отличие от серверной объектной модели, каждая из этих операций в клиентской объектной модели должна завершаться вызовом метода **to executeQueryAsync(succeededCallback, failedCallback)**, чтобы изменения вступили в силу на сервере.
 

 

### <a name="create-a-list-item"></a>Создание элемента списка

Чтобы создать элементы списка, следует создать объект **ListItemCreationInformation**, установить его свойства и передать его как параметр в функцию **addItem(parameters)** объекта **List**. Затем устанавливаются свойства элемента списка, который возвращает этот метод, и вызывается функция **update()**, как показано в приведенном ниже примере.
 

 

```
function createListItem(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
        
    var itemCreateInfo = new SP.ListItemCreationInformation();
    this.oListItem = oList.addItem(itemCreateInfo);
    oListItem.set_item('Title', 'My New Item!');
    oListItem.set_item('Body', 'Hello World!');
    oListItem.update();

    clientContext.load(oListItem);
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item created: ' + oListItem.get_id());
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="update-a-list-item"></a>Обновление элемента списка

Для установки большинства свойств элемента списка можно с помощью индексатора столбца создать назначение, а затем вызвать функцию **update()**, чтобы изменения вступили в силу при вызове **executeQueryAsync(succeededCallback, failedCallback)**. В приведенном ниже примере устанавливается заголовок третьего элемента списка "Announcements".
 

 

```
function updateListItem(siteUrl) {
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');

    this.oListItem = oList.getItemById(3);
    oListItem.set_item('Title', 'My Updated Title');
    oListItem.update();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item updated!');
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


### <a name="delete-a-list-item"></a>Удаление элемента списка

Чтобы удалить элемент списка, следует вызвать функцию **deleteObject()** объекта. В приведенном ниже примере используется функция **getItemById(id)** для возврата второго элемента списка, а затем выполняется удаление элемента. SharePoint обслуживает целочисленные идентификаторы элементов в коллекциях, даже если эти элементы удаляются. Поэтому, например, второй элемент списка должен иметь идентификатор, отличный от 2. **ServerException** возвращается, если функция **deleteObject()** вызывается для несуществующего элемента.
 

 

```
function deleteListItem(siteUrl) {
    this.itemId = 2;
    var clientContext = new SP.ClientContext(siteUrl);
    var oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    this.oListItem = oList.getItemById(itemId);
    oListItem.deleteObject();

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.onQuerySucceeded), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function onQuerySucceeded() {
    alert('Item deleted: ' + itemId);
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```

Если, например, требуется получить новое количество элементов, появившееся в результате операции удаления, следует включить вызов метода update(), чтобы обновить список. Кроме того, перед выполнением запроса необходимо загрузить либо сам объект списка, либо его свойство **itemCount**. Если требуется получить как исходное, так и итоговое количество элементов списка, то необходимо выполнить два запроса и получить число элементов дважды, как показано ниже.
 

 



```
function deleteListItemDisplayCount(siteUrl) {
    this.clientContext = new SP.ClientContext(siteUrl);
    this.oList = clientContext.get_web().get_lists().getByTitle('Announcements');
    clientContext.load(oList);

    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.deleteItem), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function deleteItem() {
    this.itemId = 58;
    this.startCount = oList.get_itemCount();
    this.oListItem = oList.getItemById(itemId);
    oListItem.deleteObject();

    oList.update();
    clientContext.load(oList);
        
    clientContext.executeQueryAsync(
        Function.createDelegate(this, this.displayCount), 
        Function.createDelegate(this, this.onQueryFailed)
    );
}

function displayCount() {
    var endCount = oList.get_itemCount();
    var listItemInfo = 'Item deleted: ' + itemId + 
        '\nStart Count: ' +  startCount + 
        ' End Count: ' + endCount;
        
    alert(listItemInfo)
}

function onQueryFailed(sender, args) {
    alert('Request failed. ' + args.get_message() + 
        '\n' + args.get_stackTrace());
}
```


## <a name="access-objects-in-the-host-web"></a>Доступ к объектам на хост-сайте
<a name="BasicOps_AccessHostweb"> </a>

При разработке надстройки может потребоваться доступ к хост-сайту для работы с элементами на нем. Используйте объект **AppContextSite** для ссылки на хост-сайт или другие сайты SharePoint, как показано в приведенном ниже примере. Полный пример кода см. в разделе [Получение названия хост-сайта с помощью междоменной библиотеки (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-Get-the-563f2a3d).
 

 

```
function execCrossDomainRequest(appweburl, hostweburl) {
    // context: The ClientContext object provides access to
    //      the web and lists objects.
    // factory: Initialize the factory object with the
    //      add-in web URL.
    var context;
    var factory;
    var appContextSite;

    context = new SP.ClientContext(appweburl);
    factory = new SP.ProxyWebRequestExecutorFactory(appweburl);
    context.set_webRequestExecutorFactory(factory);
    appContextSite = new SP.AppContextSite(context, hostweburl);

    this.web = appContextSite.get_web();
    context.load(this.web);

    // Execute the query with all the previous 
    //  options and parameters.
    context.executeQueryAsync(
        Function.createDelegate(this, successHandler), 
        Function.createDelegate(this, errorHandler)
    );

    // Function to handle the success event.
    // Prints the host web's title to the page.
    function successHandler() {
        alert(this.web.get_title());
    }

    // Function to handle the error event.
    // Prints the error message to the page.
    function errorHandler(data, errorCode, errorMessage) {
        alert("Could not complete cross-domain call: " + errorMessage);
    }
}
```

В предыдущем примере для доступа к хост-сайту используется междоменная библиотека в SharePoint. Дополнительные сведения см. в разделе  [Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки](access-sharepoint-data-from-add-ins-using-the-cross-domain-library.md).
 

 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="BasicOps_AddRes"> </a>


-  [Выполнение базовых операций с использованием кода клиентской библиотеки в SharePoint](complete-basic-operations-using-sharepoint-client-library-code.md)
    
 
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](complete-basic-operations-using-sharepoint-rest-endpoints.md)
    
 
-  [Разработка надстроек SharePoint](develop-sharepoint-add-ins.md)
    
 
-  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)
    
 
-  [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint.md)
    
 

