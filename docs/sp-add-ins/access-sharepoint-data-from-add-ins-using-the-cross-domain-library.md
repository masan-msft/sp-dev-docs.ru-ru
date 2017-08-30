# <a name="access-sharepoint-data-from-add-ins-using-the-cross-domain-library"></a>Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки
Узнайте, как работать с данными на веб-сайте SharePoint из надстройки, используя междоменную библиотеку в SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". В процессе перехода с одного названия на другое в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

При создании надстроек SharePoint обычно необходимо объединять данные из различных источников. Но по [соображениям безопасности](http://msdn.microsoft.com/library/cc709423.aspx) используются механизмы блокировки, которые предотвращают одновременный обмен данными с несколькими доменами. Эти механизмы безопасности реализованы в большинстве браузеров, что усложняет или делает невозможным выполнение клиентских вызовов в разных доменах.
 

На рис. 1 показан заблокированный запрос для нескольких доменов.
 


**Рис. 1. Заблокированный запрос в нескольких доменах**

 
Когда пользователь запрашивает страницу из домена надстройки (1), коммуникации на стороне клиента привязаны только к этому домену. Надстройка может выполнять клиентские вызовы с этой страницы только для других ресурсов в том же домене. Однако надстройкам обычно требуются ресурсы из других доменов, например домена SharePoint, для реализации своих функций. В коде на странице можно попытаться отправить запрос домену SharePoint (2), который будет заблокирован браузером. Обычно появляется ошибка **Доступ запрещен**. Она не означает, что у вас нет разрешений для запрошенных ресурсов. Скорее всего, вы просто не можете отправлять запросы указанным ресурсам.
 
При использовании междоменной библиотеки веб-страницы надстройки могут получать доступ к данным в вашем домене надстройки и домене SharePoint. Междоменная библиотека — это клиентский вариант библиотеки в виде файла JavaScript (SP.RequestExecutor.js), расположенного на веб-сайте SharePoint, на который можно ссылаться в вашей удаленной надстройке. Она позволяет взаимодействовать с несколькими доменами на странице удаленной надстройки через прокси-сервер. Рекомендуем использовать библиотеку в том случае, если ваша надстройка выполняется на клиенте, а не на сервере, или при наличии таких барьеров, как брандмауэры, между SharePoint и вашей удаленной инфраструктурой. Вы можете получить доступ к данным на хост-сайте, например к спискам, с которыми взаимодействуют конечные пользователи, независимо от вашей надстройки, или к данным в веб-надстройке, таким как списки, настроенные для надстройки. Кроме того, вы можете получить доступ к другим семействам сайтов и веб-сайтам, если для надстройки настроены разрешения на уровне клиента и она развернута в пакетной установке с помощью каталога надстроек.
 

 **Примечание.** В этом разделе **домен надстройки** означает домен, в котором размещаются страницы надстройки. Это может быть домен удаленной веб-надстройки с размещением у поставщика. Но страницы надстройки также могут содержаться в SharePoint на сайте надстройки и отправлять запросы в домен хост-сайта. В последнем случае домен надстройки — это домен сайта надстройки.
 

В главном примере в данной статье показано, как создать надстройку, считывающую данные на сайте надстройки и отображающую их на веб-странице. В разделе  [Дальнейшие действия](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library#SP15Accessdatafromremoteapp_Next) показаны дополнительные сценарии, основанные на главном примере.
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье
<a name="SP15Accessdatafromremoteapp_Prereq"> </a>

Для выполнения примеров, описанных в этой статье, вам необходимо следующее:
 

 

-  [Visual Studio 2012](https://www.microsoft.com/en-us/download/details.aspx?id=30682)
    
 
-  [Инструменты разработчика Microsoft Office для Visual Studio 2012](https://msdn.microsoft.com/en-us/office/aa905340.aspx)
    
 
- Среда разработки SharePoint (для локальных сценариев необходима изоляция приложений)
    
 

## <a name="read-data-on-the-add-in-web-using-the-cross-domain-library"></a>Чтение данных с сайта надстройки с помощью междоменной библиотеки
<a name="SP15Accessdatafromremoteapp_Codeexample"> </a>

В этом примере за пределами SharePoint размещена простая страница, которая использует конечную точку REST, чтобы читать данные на веб-сайте SharePoint (сайте надстройки). Так как для междоменной библиотеки требуется сайт надстройки, имеет смысл начать с этого сценария.
 

 
Для чтения данных с сайта надстройки вы должны сделать следующее:
 

 

1. Создайте Надстройка SharePoint и веб-проекты.
    
 
2. Создайте элементы списка на сайте надстройки. Этот шаг также гарантирует, что сайт надстройки будет создан, когда пользователи развернут надстройку.
    
 
3. Создайте страницу надстройки, которая использует междоменную библиотеку для чтения элементов списка.
    
 
На рис. 2 показана веб-страница, на которой отображаются данные на сайте надстройки.
 

 

**Рис. 2. Веб-страница, на которой отображаются данные на сайте надстройки**

 

 
![Пример экрана с междоменными результатами чтения элементов](../../images/CrossDomainReadItemsResult.png)
 

### <a name="create-a-sharepoint-add-in-and-web-projects"></a>Создание надстройки SharePoint и веб-проектов


1. Откройте Visual Studio 2012 от имени администратора. Для этого щелкните правой кнопкой мыши значок Visual Studio 2012 в меню **Пуск** и выберите пункт **Запуск от имени администратора**.
    
 
2. Создайте новый проект с помощью шаблона **Надстройка для SharePoint**.
    
    Шаблон **Надстройка для SharePoint** в Visual Studio 2012 расположен в области **Шаблоны****>****Visual C#**, **Office SharePoint****>****Надстройки**.
    
 
3. Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.
    
 
4. Выберите для надстройки вариант размещения **Размещено у поставщика**.
    
     **Примечание.** Вы также можете использовать междоменную библиотеку в надстройке, размещаемой в SharePoint. Однако в такой надстройке ее страница уже находится на сайте надстройки, т. е. вам не нужна междоменная библиотека для чтения элементов списка. Пример такой надстройки, которая читает данные на хост-сайте, см. в статье, посвященной [использованию междоменной библиотеки в надстройке, размещаемой в SharePoint (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814), или в разделе [Доступ к данным на хост-сайте](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library#SP15Accessdatafromremoteapp_Hostweb) далее в этой статье.

### <a name="create-list-items-on-the-add-in-web"></a>Создание элементов списка на сайте надстройки


1. Щелкните правой кнопкой мыши проект надстройки SharePoint в **обозревателе решений**. Выберите **Добавить****>****Новый элемент…**
    
 
2. Выберите **Элементы Visual C#** **>** **Office/SharePoint** **>** **Список**. Введите для списка имя **Объявления**.
    
 
3. Дважды щелкните **Объявления** **>** **Elements.xml**. Вставьте следующие узлы XML как потомки элемента **ListInstance**.
    
```
  <Data>
    <Rows>
        <Row>
            <Field Name="Title">Lorem ipsum 1</Field>
            <Field Name="Body">Sed ut perspiciatis, unde omnis iste...</Field>
        </Row>
        <Row>
            <Field Name="Title">Lorem ipsum 2</Field>
            <Field Name="Body">Sed ut perspiciatis, unde omnis iste...</Field>
        </Row>
    </Rows>
</Data>
```


### <a name="to-add-a-new-page-that-uses-the-cross-domain-library"></a>Добавление новой страницы, которая использует междоменную библиотеку


1. Дважды щелкните файл **Default.aspx** в веб-проекте в **обозревателе решений**.
    
 
2. Скопируйте следующий код и вставьте его в файл Default.aspx. Этот код выполняет следующие задачи:
    
      - Загружает библиотеку jQuery из сети CDN Майкрософт.
    
 
  - Задает заполнитель для результатов.
    
 
  - Извлекает URL-адрес сайта надстройки из строки запроса.
    
 
  - Загружает междоменную библиотеку JavaScript с помощью функции **getScript** в jQuery.
    
    Функция загружает необходимые ресурсы и переходит к указанной функции, обеспечивая загрузку междоменной библиотеке и предоставляя к ней доступ последующему коду.
    
 
  - Создает экземпляр объекта **RequestExecutor**. По умолчанию RequestExecutor использует сайт надстройки как сайт контекста.
    
     **Примечание.** Вы можете изменить сайт контекста на сайты, отличные от сайта надстройки, с помощью конечной точки **AppContextSite** (REST) или объекта (JSOM). Дополнительные сведения об AppContextSite см. в разделе [Доступ к данным на хост-сайте](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library#SP15Accessdatafromremoteapp_Hostweb) далее в этой статье.
  - Выполняет REST-вызов к конечной точке элементов списка.
    
 
  - Обрабатывает успешное выполнение с отображением элементов списка на веб-странице.
    
 
  - Обрабатывает ошибки с отображением сообщения об ошибке на веб-странице.
    
 

```
  
<html>
    <head>
        <title>Cross-domain sample</title>
    </head>
    <body>
        <!-- This is the placeholder for the announcements -->
        <div id="renderAnnouncements"></div>
        <script 
            type="text/javascript" 
            src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
        </script>
        <script type="text/javascript">
          var hostweburl;
          var appweburl;

          // Load the required SharePoint libraries
          $(document).ready(function () {
            //Get the URI decoded URLs.
            hostweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPHostUrl")
            );
            appweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPAppWebUrl")
            );

            // resources are in URLs in the form:
            // web_url/_layouts/15/resource
            var scriptbase = hostweburl + "/_layouts/15/";

            // Load the js files and continue to the successHandler
            $.getScript(scriptbase + "SP.RequestExecutor.js", execCrossDomainRequest);
          });

          // Function to prepare and issue the request to get
          //  SharePoint data
          function execCrossDomainRequest() {
            // executor: The RequestExecutor object
            // Initialize the RequestExecutor with the add-in web URL.
            var executor = new SP.RequestExecutor(appweburl);

            // Issue the call against the add-in web.
            // To get the title using REST we can hit the endpoint:
            //      appweburl/_api/web/lists/getbytitle('listname')/items
            // The response formats the data in the JSON format.
            // The functions successHandler and errorHandler attend the
            //      sucess and error events respectively.
            executor.executeAsync(
                {
                  url:
                      appweburl +
                      "/_api/web/lists/getbytitle('Announcements')/items",
                  method: "GET",
                  headers: { "Accept": "application/json; odata=verbose" },
                  success: successHandler,
                  error: errorHandler
                }
            );
          }

          // Function to handle the success event.
          // Prints the data to the page.
          function successHandler(data) {
            var jsonObject = JSON.parse(data.body);
            var announcementsHTML = "";

            var results = jsonObject.d.results;
            for (var i = 0; i < results.length; i++) {
              announcementsHTML = announcementsHTML +
                  "<p><h1>" + results[i].Title +
                  "</h1>" + results[i].Body +
                  "</p><hr>";
            }

            document.getElementById("renderAnnouncements").innerHTML =
                announcementsHTML;
          }

          // Function to handle the error event.
          // Prints the error message to the page.
          function errorHandler(data, errorCode, errorMessage) {
            document.getElementById("renderAnnouncements").innerText =
                "Could not complete cross-domain call: " + errorMessage;
          }

          // Function to retrieve a query string value.
          // For production purposes you may want to use
          //  a library to handle the query string.
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
    </body>
</html>
```


### <a name="to-build-and-run-the-solution"></a>Создание и запуск решения


1. Нажмите клавишу F5.
    
     **Примечание.** Когда вы нажимаете клавишу F5, Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.
2. Нажмите кнопку **Доверять**.
    
 
3. Выберите значок надстройки на странице **Содержимое сайта**.
    
 
Если вы предпочитаете работать с загруженными примерами кода, этот пример можно скачать в коллекции исходных кодов. **Пример кода: получение элементов списка с помощью междоменной библиотеки** с использованием [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain) или [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain).
 

 

**Табл. 2. Поиск и устранение неполадок в решении**


|**Если вы видите...**|**Попробуйте...**|
|:-----|:-----|
|Сообщение об ошибке: "К сожалению, у нас возникли проблемы с доступом к сайту". К тому же, появляется кнопка, предназначенная для исправления ошибки, но она не устраняет проблему.|Возможно, вы столкнулись с проблемой с зонами безопасности в Internet Explorer, см. статью [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-zones-in-sharepoint-add-ins).|
|Сообщение об ошибке: требуемые функции не поддерживаются вашим браузером. Используйте IE 8 или более позднюю версию либо другой современный браузер. Метатег "X-UA-Compatible" должен быть равен "IE=8" или более высокому значению.|Для междоменной библиотеки требуется режим документа в **IE8** или более поздней версии. В ряде случаев он по умолчанию задан как **IE7**. Можно использовать средства разработчика Internet Explorer, чтобы определить или изменить режим документа для страницы. Дополнительные сведения см. в разделе [Определение совместимости документов](http://msdn.microsoft.com/library/cc288325.aspx).|
|Сообщение об ошибке: "Тип не определен". Кроме того, надстройка использует объектную модель JavaScript (JSOM).|JSOM использует метод **Type.registerNamespace** в библиотеке Microsoft Ajax для регистрации пространства имен **SP**. Используйте следующий код, чтобы добавить ссылку на библиотеку Microsoft Ajax на вашей странице: ```HTML<script  type="text/javascript"  src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js"></script>```.|

## <a name="next-steps"></a>Дальнейшие действия
<a name="SP15Accessdatafromremoteapp_Next"> </a>

В этой статье показано, как отправить запрос конечной точке REST для чтения данных с сайта надстройки с помощью страницы надстройки, не размещенной в SharePoint. Вы также можете изучить следующие сценарии и сведения о междоменной библиотеке.
 

 

### <a name="use-the-jsom-to-read-data-from-the-add-in-web"></a>Использование JSOM для чтения данных с сайта надстройки
<a name="SP15Accessdatafromremoteapp_JSOM"> </a>

В зависимости от ваших предпочтений вы можете использовать JSOM вместо REST для запроса данных с сайта надстройки. Чтобы использовать междоменную библиотеку с JSOM, необходимо выполнить дополнительные задачи:
 

 

- Добавить ссылку на SharePoint JSOM на страницу надстройки.
    
 
- Инициализировать объект **ProxyWebRequestExecutorFactory** и сделать его фабрикой объекта контекста.
    
 
- Получить доступ к объектам SharePoint для чтения данных из списка.
    
 
- Загрузить объекты в контекст и выполнить запрос.
    
 
Пример кода, в котором показано, как выполнить эти задачи, см. в репозитории  [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain). Дополнительные сведения об использовании JSOM см. в статье  [Использование объектной модели JavaScript (JSOM) в надстройках для SharePoint](http://blogs.msdn.com/b/officeapps/archive/2012/09/04/using-the-javascript-object-model-jsom-in-apps-for-sharepoint.aspx).
 

 

### <a name="access-data-from-the-host-web"></a>Доступ к данным на хост-сайте
<a name="SP15Accessdatafromremoteapp_Hostweb"> </a>

В примере на этой странице показано, как читать данные с сайта надстройки. Это хорошая начальная точка, так как междоменная библиотека изначально использует надстройку как сайт контекста. Однако существует множество сценариев, в которых необходимо получить доступ к данным на хост-сайте. Для этого требуется выполнить несколько задач: 
 

 

- Сделать хост-сайт сайтом контекста для междоменной библиотеки.
    
 
- Задать необходимые разрешения для надстройки.
    
 
Вы можете изменить сайт контекста с помощью конечной точки **AppContextSite** (REST) или объекта (JSOM). В следующем примере показано, как изменить сайт контекста с помощью конечной точки REST:
 

 



```
executor.executeAsync(
    {
        url:
            appweburl +
            "/_api/SP.AppContextSite(@target)/web/title?@target='" +
            hostweburl + "'",
        method: "GET",
        headers: { "Accept": "application/json; odata=verbose" },
        success: successHandler,
        error: errorHandler
    }
);
```

В следующем примере кода показано, как изменить сайт контекста с помощью JSOM:
 

 



```
context = new SP.ClientContext(appweburl);
factory = new SP.ProxyWebRequestExecutorFactory(appweburl);
context.set_webRequestExecutorFactory(factory);
appContextSite = new SP.AppContextSite(context, hostweburl);

this.web = appContextSite.get_web();
context.load(this.web);
```

По умолчанию у вашей надстройки есть разрешения для сайта надстройки, но не для хост-сайта. В следующем примере показан раздел манифеста, в котором объявляется запрос разрешений для чтения данных с хост-сайта:
 

 



```XML
<AppPermissionRequests>
    <AppPermissionRequest 
        Scope="http://sharepoint/content/sitecollection/web" 
        Right="Read" />
</AppPermissionRequests>
```

Создайте ресурс на сайте надстройки (например, пустую страницу или список), чтобы принудительно создать сайт надстройки, так как это необходимо для использования междоменной библиотеки.
 

 

### <a name="access-data-across-site-collections"></a>Доступ к данным на нескольких семействах веб-сайтов
<a name="SP15Accessdatafromremoteapp_TenantScope"> </a>

С помощью междоменной библиотеки можно получать доступ к данным на нескольких семействах веб-сайтов в одном клиенте. Для этого необходимо выполнить несколько задач:
 

 

- Добавить запрос разрешений для доступа к данным в клиенте.
    
 
- Заменить сайт контекста на семейства сайтов, к которым нужно выполнить запрос, в коде.
    
 
- Добавить надстройку в каталог надстроек.
    
 
- Развернуть надстройку с разрешениями на уровне клиента на веб-сайте. Пример см. в описании примера кода  [Использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).
    
 
Надстройке также требуются разрешения для доступа к данным клиента. В следующем примере показан раздел манифеста, в котором объявляется запрос разрешений для чтения данных клиента:
 

 



```XML
<AppPermissionRequests>
  <AppPermissionRequest 
    Scope="http://sharepoint/content/tenant" 
    Right="Read" />
</AppPermissionRequests>
```

Чтобы заменить сайт контекста в коде, используйте конечную точку **AppContextSite** (REST) или объект (JSOM), как в разделе [Доступ к данным на хост-сайте](access-sharepoint-2013-data-from-add-ins-using-the-cross-domain-library#SP15Accessdatafromremoteapp_Hostweb). Вот напоминание о конечной точке REST: /_api/SP.AppContextSite(@target)/web/title?@target='weburl', а также пример того, как создать экземпляр объекта в JSOM: `appContextSite = new SP.AppContextSite(context, weburl);`.
 

 
Вы как разработчик можете развернуть только надстройки с разрешениями на уровне клиента из каталога надстроек. Можно настроить каталог надстроек для локальной среды или среды SharePoint Online. Отправить надстройку в каталог надстроек так же просто, как загрузить файл в библиотеку документов. Подробные инструкции см. в статье о  [добавлении настраиваемых надстроек на сайт каталога надстроек](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).
 

 
Из каталога надстроек вы сможете развернуть надстройку на одном или нескольких веб-сайтах в клиенте. Так как у надстройки есть разрешения для доступа к данным клиента, нужно развернуть её только на одном веб-сайте для доступа к всем данным клиента. Инструкции по развертыванию надстройки из каталога надстроек см. в статье  [Развертывание настраиваемой надстройки](http://office.microsoft.com/en-us/sharepoint-help/use-the-app-catalog-to-make-custom-business-apps-available-for-your-sharepoint-online-environment-HA102772362.aspx).
 

 
Сведения о том, как скачать пример кода, в котором показано, как получить доступ к данным на разных семействах веб-сайтов, см. в статье  [Использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).
 

 

### <a name="issuing-calls-across-different-security-zones"></a>Выполнение запросов для разных зон безопасности
<a name="SP15Accessdatafromremoteapp_IEZones"> </a>

Для взаимодействия междоменная библиотека использует страницу прокси-сервера, размещенную в **IFrame** на странице надстройки. Если страница надстройки и веб-сайт SharePoint находятся в разных зонах безопасности, отправка файлов cookie авторизации невозможна. Если эти файлы отсутствуют и элемент IFrame пытается загрузить прокси-страницу, он перенаправляется на страницу входа SharePoint. В целях безопасности страница входа SharePoint не может содержаться в элементе IFrame. В такой ситуации библиотека не может загрузить прокси-страницу, и связь с SharePoint невозможна.
 

 
Однако для этих сценариев существует решение. Это **шаблон apphost**, который создает оболочку для страниц надстройки на странице, размещенной на сайте надстройки. Рекомендуем использовать шаблон apphost в надстройках, которые используют междоменную библиотеку, даже если очевидных границ безопасности нет. Дополнительные сведения см. в статье [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-zones-in-sharepoint-add-ins).
 

 

### <a name="access-data-from-an-additional-remote-host-in-a-sharepoint-hosted-add-in"></a>Доступ к данным на дополнительном удаленном узле в надстройках, размещаемых в SharePoint
<a name="SP15Accessdatafromremoteapp_SPhosted"> </a>

По умолчанию надстройке, размещаемой в SharePoint, разрешено выполнять междоменные вызовы для хост-сайта, если у нее есть необходимые разрешения. Однако такая надстройка также может указать удаленный узел в атрибуте **AllowedRemoteHostUrl**, принадлежащему **AppPrincipal**. Это позволяет эффективно выполнять междоменные вызовы из сайта надстройки и других узлов.
 

 
Сведения о том, как скачать пример Надстройки, размещаемые в SharePoint, использующего междоменную библиотеку, см. в статье  [Пример кода: использование междоменной библиотеки в надстройке, размещенной в SharePoint (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814).
 

 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Accessdatafromremoteapp_Addresources"> </a>


-  [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain)
    
 
-  [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain)
    
 
-  [Пример кода: запрос названия хост-сайта с помощью междоменной библиотеки (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Get-the-0ec36bb6)
    
 
-  [Пример кода: запрос названия хост-сайта с помощью междоменной библиотеки (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-2013-Get-the-563f2a3d)
    
 
-  [Пример кода: использование междоменной библиотеки в надстройке, размещаемой в SharePoint](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814)
    
 
-  [Пример кода: использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e)
    
 
-  [Пример кода: использование элемента управления хрома и междоменной библиотеки (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-a759e9f8)
    
 
-  [Пример кода: использование элемента управления хрома и междоменной библиотеки (JSOM)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-97c30a2e)
    
 
-  [Пример кода: использование дополнительных действий и междоменной библиотеки для заказа книг](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
    
 
-  [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins)
    
 
-  [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-zones-in-sharepoint-add-ins)
    
 
-  [Создание настраиваемой страницы прокси для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint-2013)
    
 
-  [Отправка запросов удаленной службе с помощью веб-прокси в SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint-2013)
    
 
-  [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
