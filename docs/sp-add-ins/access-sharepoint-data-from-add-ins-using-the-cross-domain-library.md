---
title: "Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки"
description: "Узнайте, как получать доступ к данным на веб-сайте SharePoint из надстройки с помощью междоменной библиотеки в SharePoint."
ms.date: 12/29/2017
ms.prod: sharepoint
ms.openlocfilehash: 5854d179511e15eee96e87e22efe185c391ad8a1
ms.sourcegitcommit: e157d51378190ddfed6394ba154ce66141c8ca33
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/19/2018
---
# <a name="access-sharepoint-data-from-add-ins-using-the-cross-domain-library"></a>Обращение к данным SharePoint из надстроек с помощью междоменной библиотеки

При создании надстроек SharePoint обычно требуется внедрять данные из различных источников. Однако из [соображений безопасности](https://msdn.microsoft.com/library/cc709423.aspx) защитные механизмы блокируют одновременный обмен данными с несколькими доменами. Такие механизмы реализованы в большинстве браузеров, что затрудняет или делает невозможным вызов ресурсов в разных доменах.

Когда пользователь запрашивает страницу из домена надстройки, обмен данными на стороне клиента привязывается к этому домену. Надстройка может вызывать со страницы только другие ресурсы в том же домене. Однако для выполнения своих функций надстройкам обычно необходимы ресурсы из других доменов, например домена SharePoint. Запросы ресурсов в домене SharePoint, реализованные в коде страницы, блокируются браузером. Как правило, при этом возникает ошибка **Отказано в доступе**. Она не означает, что у вас нет разрешений на запрашиваемые ресурсы. Скорее всего, вы просто не можете их запрашивать.
 
При использовании междоменной библиотеки веб-страницы надстройки могут получать доступ к данным на доменах надстройки и SharePoint. Междоменная библиотека — это клиентская альтернатива в форме файла JavaScript (SP.RequestExecutor.js), размещенного на веб-сайте SharePoint, на который вы можете ссылаться в своей удаленной надстройке. Междоменная библиотека позволяет взаимодействовать с несколькими доменами на удаленной странице надстройки через прокси-сервер. Это отличный вариант, если вы предпочитаете, чтобы код надстройки выполнялся в клиенте, а не на сервере, или если между SharePoint и удаленной инфраструктурой существуют препятствия для подключения, такие как брандмауэры. 

Вы можете получать доступ к данным на хост-сайте, например спискам, с которыми пользователи работают вне надстройки. Вы также можете получать доступ к данным на сайте надстройки, например специально подготовленным для нее спискам. Надстройки также могут получать доступ к другим сайтам и семействам веб-сайтов при наличии разрешения на уровне клиента и развертывании путем пакетной установки с помощью каталога надстроек.
 
> [!NOTE] 
> В этой статье под **доменом надстройки** подразумевается домен, на котором размещаются страницы надстройки. Это может быть домен удаленного веб-приложения в надстройке с размещением у поставщика, но страницы надстройки также могут находиться в SharePoint на сайте надстройки и вызывать домен хост-сайта. В последнем случае доменом надстройки будет домен ее сайта.

В главном примере из этой статьи показано, как создать надстройку, которая считывает данные с сайта надстройки и отображает их на веб-странице. В разделе [Дальнейшие действия](#SP15Accessdatafromremoteapp_Next) показаны другие сценарии, которые основываются на главном примере.
 

<a name="SP15Accessdatafromremoteapp_Prereq"> </a>

## <a name="prerequisites"></a>Необходимые компоненты

Чтобы воспользоваться примерами, приведенными в этой статье, вам потребуется следующее:

- Среда [Visual Studio](https://docs.microsoft.com/ru-RU/visualstudio/install/install-visual-studio), установленная либо удаленно, либо на одном компьютере с SharePoint.
    
- Visual Studio включает **Инструменты разработчика Microsoft Office для Visual Studio**. Иногда выпуск новой версии этих инструментов не совпадает с выходом обновлений Visual Studio. Чтобы убедиться, что у вас установлена последняя версия этих инструментов, запустите [установщик набора "Инструменты разработчика Office для Visual Studio 2013"](http://aka.ms/OfficeDevToolsForVS2013) или [установщик набора "Инструменты разработчика Office для Visual Studio 2015"](http://aka.ms/OfficeDevToolsForVS2015).  
    
- Локальная среда разработки SharePoint. [Как настроить](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)


<a name="SP15Accessdatafromremoteapp_Codeexample"> </a>

## <a name="read-data-on-the-add-in-web-using-the-cross-domain-library"></a>Чтение данных с сайта надстройки с помощью междоменной библиотеки

В этом примере за пределами SharePoint размещена простая страница, которая использует конечную точку REST для чтения данных на веб-сайте SharePoint (сайте надстройки). Так как междоменной библиотеке необходим сайт надстройки, будет логично начать с этого сценария.

Для чтения данных с сайта надстройки вы должны сделать следующее:

1. Создайте надстройку SharePoint и веб-проекты.

2. Создайте элементы списка на сайте надстройки. Этот шаг также гарантирует создание сайта при развертывании надстройки.

3. Создайте страницу надстройки, которая использует междоменную библиотеку для чтения элементов списка.
    
Ниже показана веб-страница, на которой отображаются данные с сайта надстройки.

![Экран с результатами чтения элементов из разных доменов](../images/CrossDomainReadItemsResult.png)
 

### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a>Создание надстройки SharePoint и веб-проектов

1. Откройте Visual Studio от имени администратора. Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.
    
2. Создайте новый проект с помощью шаблона **Надстройка для SharePoint**. Шаблон **Надстройка для SharePoint** в Visual Studio находится в области **Шаблоны** > **Visual C#** > **Office SharePoint** > **Надстройки**.
     
3. Укажите URL-адрес веб-сайта SharePoint, который требуется использовать для отладки.   
 
4. Выберите для надстройки вариант размещения **Размещено у поставщика**.
    
    > [!NOTE] 
    > Вы также можете использовать междоменную библиотеку в надстройке с размещением в SharePoint. Однако страница надстройки с размещением в SharePoint уже находится на ее сайте, то есть для чтения элементов списка не нужна междоменная библиотека. Пример надстройки с размещением в SharePoint, считывающей данные с хост-сайта, см. на странице [Использование междоменной библиотеки в надстройке с размещением в SharePoint (REST)](https://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814) или в разделе [Доступ к данным с хост-сайта](#SP15Accessdatafromremoteapp_Hostweb) далее в этой статье.


### <a name="to-create-list-items-on-the-add-in-web"></a>Создание элементов списка на сайте надстройки

1. Щелкните правой кнопкой мыши проект надстройки SharePoint в **обозревателе решений**. Выберите **Добавить** > **Новый элемент**.    
 
2. Выберите **Элементы Visual C#** > **Office/SharePoint** > **Список**. Укажите имя списка **Объявления**.

3. Дважды щелкните узлы **Объявления** > **Elements.xml**. Вставьте приведенные ниже узлы XML в качестве дочерних объектов элемента **ListInstance**.
        
    ```XML
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


### <a name="to-create-an-add-in-page-that-uses-the-cross-domain-library"></a>Создание страницы надстройки, использующей междоменную библиотеку

1. Дважды щелкните файл **Default.aspx** в веб-проекте в **обозревателе решений**.
    
2. Скопируйте следующий код и вставьте его в файл Default.aspx. Этот код выполняет следующие задачи.
    
    - Загружает библиотеку jQuery из сети CDN Майкрософт.
        
    - Задает заполнитель для результатов.
        
    - Извлекает URL-адрес сайта надстройки из строки запроса.
        
    - Загружает междоменную библиотеку JavaScript с помощью функции **getScript** в jQuery.
        
        Функция загружает необходимые ресурсы и переходит к указанной функции, обеспечивая загрузку междоменной библиотеке и предоставляя к ней доступ последующему коду.
        
    - Создает экземпляр объекта **RequestExecutor**. По умолчанию RequestExecutor использует сайт надстройки как сайт контекста.
        
        > [!NOTE] 
        > (REST) или объект (JSOM). Дополнительные сведения об AppContextSite см. в разделе [Доступ к данным с хост-сайта](#SP15Accessdatafromremoteapp_Hostweb) далее в этой статье.

    - Вызывает конечную точку REST с элементами списка.
        
    - Обрабатывает успешное выполнение с отображением элементов списка на веб-странице.   
    
    - Обрабатывает ошибки с отображением сообщения об ошибке на веб-странице.
    
 

```HTML
  
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

<br/>

### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения

1. Нажмите клавишу F5.
    
    > [!NOTE] 
    > При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.

2. Нажмите кнопку **Доверять**.    
 
3. Выберите значок надстройки на странице **Содержимое сайта**.
    
Вы можете скачать примеры кода по теме на следующих страницах:

- [SharePoint-Add-in-REST-OData-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-REST-OData-CrossDomain)
- [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain).
 

#### <a name="troubleshooting-the-solution"></a>Устранение неполадок в решении


|**Сообщение об ошибке**|**Возможное решение**|
|:-----|:-----|
|"К сожалению, у нас возникли проблемы с доступом к сайту". Кроме того, появляется кнопка, предназначенная для исправления ошибки, но она не устраняет проблему.|Возможно, вы столкнулись с проблемой с зонами безопасности в Internet Explorer. См. статью [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).|
|"Ваш браузер не поддерживает необходимые функциональные возможности. Вам следует использовать IE 8 или более поздней версии либо другой современный браузер. Убедитесь в том, что для мета-тега X-UA-Compatible установлено значение IE=8 или выше".|Для использования междоменной библиотеке необходим режим документов **IE8** или более поздней версии. В некоторых случаях по умолчанию выбран режим документов **IE7**. Вы можете использовать средства разработчика Internet Explorer, чтобы определить и изменить режим документов страницы. Дополнительные сведения см. в статье [Определение совместимости документов](https://msdn.microsoft.com/library/cc288325.aspx).|
|"Поле Type не определено. Кроме того, ваша надстройка использует объектную модель JavaScript (JSOM)". |JSOM использует метод **Type.registerNamespace** в библиотеке Microsoft Ajax для регистрации пространства имен **SP**. Используйте следующий код, чтобы добавить ссылку на библиотеку Microsoft Ajax на вашей странице: <br/><br/>```HTML <script  type="text/javascript"  src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js"></script>```|


<a name="SP15Accessdatafromremoteapp_Next"> </a>

## <a name="next-steps-more-cross-domain-library-scenarios"></a>Дальнейшие действия: другие сценарии с использованием междоменной библиотеки

В этой статье показано, как отправить запрос конечной точке REST для чтения данных с сайта надстройки с помощью страницы надстройки, не размещенной в SharePoint. Вы также можете изучить следующие сценарии и сведения о междоменной библиотеке.
 
<a name="SP15Accessdatafromremoteapp_JSOM"> </a>
 
### <a name="use-the-jsom-to-read-data-from-the-add-in-web"></a>Использование JSOM для чтения данных с сайта надстройки

В зависимости от ваших предпочтений вы можете использовать JSOM вместо REST для запроса данных с сайта надстройки. Чтобы использовать междоменную библиотеку с JSOM, необходимо выполнить дополнительные задачи:

- Добавить ссылку на SharePoint JSOM на страницу надстройки.

- Инициализировать объект **ProxyWebRequestExecutorFactory** и сделать его фабрикой объекта контекста.

- Получить доступ к объектам SharePoint для чтения данных из списка.

- Загрузить объекты в контекст и выполнить запрос.

Пример кода, иллюстрирующий выполнение этих задач: [SharePoint-Add-in-JSOM-CrossDomain](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-CrossDomain). 

Дополнительные сведения об использовании модели JSOM в надстройках SharePoint см. в [этой статье](https://blogs.msdn.microsoft.com/officeapps/2012/09/04/using-the-javascript-object-model-jsom-in-apps-for-sharepoint/).
 

<a name="SP15Accessdatafromremoteapp_Hostweb"> </a> 

### <a name="access-data-from-the-host-web"></a>Доступ к данным с хост-сайта

В примере на этой странице показано, как считывать данные с сайта надстройки. Он подходит в качестве отправной точки, так как междоменная библиотека изначально использует надстройку в качестве сайта контекста. Однако во многих случаях требуется получить доступ к данным на хост-сайте. Для этого необходимо выполнить несколько задач. 

- Сделать хост-сайт сайтом контекста для междоменной библиотеки.

- Задать необходимые разрешения для надстройки.

Вы можете изменить сайт контекста, используя конечную точку **AppContextSite** (REST) или объект (JSOM). В следующем примере показано, как изменить сайт контекста с помощью конечной точки REST:

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

```js
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

Создайте ресурс на сайте надстройки (например, пустую страницу или список), чтобы принудительно подготовить сайт надстройки, так как это необходимо для использования междоменной библиотеки.
 

<a name="SP15Accessdatafromremoteapp_TenantScope"> </a> 

### <a name="access-data-across-site-collections"></a>Доступ к данным на нескольких семействах веб-сайтов

С помощью междоменной библиотеки можно получать доступ к данным на нескольких семействах веб-сайтов в одном клиенте. Для этого необходимо выполнить несколько задач:

- Добавить запрос разрешений для доступа к данным в клиенте.

- Заменить сайт контекста на семейства сайтов, к которым нужно выполнить запрос, в коде.

- Добавить надстройку в каталог надстроек.

- Развернуть надстройку на веб-сайте, предоставив ей разрешения на уровне клиента. Пример развертывания надстройки с разрешениями на уровне клиента представлен в описании образца кода [Использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).

Надстройке также требуются разрешения для доступа к данным клиента. В следующем примере показан раздел манифеста, в котором объявляется запрос разрешений для чтения данных клиента:

```XML
<AppPermissionRequests>
  <AppPermissionRequest 
    Scope="http://sharepoint/content/tenant" 
    Right="Read" />
</AppPermissionRequests>
```

Чтобы заменить сайт контекста в коде, используйте конечную точку **AppContextSite** (REST) или объект (JSOM), как в разделе [Доступ к данным с хост-сайта](#SP15Accessdatafromremoteapp_Hostweb). 

Напоминание о конечной точке REST: /_api/SP.AppContextSite(@target)/web/title?@target='weburl'. Пример создания экземпляра объекта в JSOM: `appContextSite = new SP.AppContextSite(context, weburl);`.
 
Как разработчик, вы можете развертывать надстройки с разрешениями на уровне клиента только из каталога надстроек. Вы можете подготовить к работе каталог надстроек в локальной среде или SharePoint Online. Отправить надстройку в каталог так же просто, как загрузить файл в библиотеку документов. Подробные инструкции см. в статье [Использование каталога приложений для развертывания пользовательских бизнес-приложений в среде SharePoint Online](https://support.office.com/en-us/article/Use-the-App-Catalog-to-make-custom-business-apps-available-for-your-SharePoint-Online-environment-0b6ab336-8b83-423f-a06b-bcc52861cba0?CorrelationId=94979966-ff7b-4e00-985a-5c9e614b35c9&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA102772362).

Из каталога надстроек вы можете развернуть надстройку на одном или нескольких веб-сайтах в клиенте. Так как у надстройки есть разрешения на доступ к данным в клиенте, развертывание на одном веб-сайте обеспечивает доступ к данным со всего клиента. Инструкции по развертыванию надстройки из каталога надстроек см. в [этой статье](https://support.office.com/en-us/article/Use-the-App-Catalog-to-make-custom-business-apps-available-for-your-SharePoint-Online-environment-0b6ab336-8b83-423f-a06b-bcc52861cba0?CorrelationId=94979966-ff7b-4e00-985a-5c9e614b35c9&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA102772362) 

Скачать пример кода, в котором показано, как получить доступ к данным на разных семействах веб-сайтов, можно на странице [Использование междоменной библиотеки в надстройке с разрешениями на уровне клиента (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-6b3e4c1e).
 

<a name="SP15Accessdatafromremoteapp_IEZones"> </a> 

### <a name="issuing-calls-across-different-security-zones"></a>Отправка вызовов в разные зоны безопасности

Для обмена данными междоменная библиотека использует прокси-страницу, размещаемую в объекте **IFrame** на странице надстройки. Если страница надстройки и веб-сайт SharePoint находятся в разных зонах безопасности, то отправлять cookie-файлы авторизации невозможно. Если cookie-файлов авторизации нет, а элемент IFrame пытается загрузить прокси-страницу, он перенаправляется на страницу входа в SharePoint. Из соображений безопасности страницу входа в SharePoint невозможно заключить в объект IFrame. В таких случаях библиотека не может загрузить прокси-страницу, и обмен данными с SharePoint невозможен.

Однако для этих сценариев существует решение. Это **шаблон apphost**, который создает оболочку для страниц надстройки на странице, размещенной на сайте надстройки. Рекомендуется использовать шаблон apphost в надстройках, которые используют междоменную библиотеку, даже если очевидных границ безопасности нет. Дополнительные сведения см. в статье [Работа с междоменной библиотекой в различных зонах безопасности Internet Explorer в надстройках SharePoint](work-with-the-cross-domain-library-across-different-internet-explorer-security-z.md).
 
<a name="SP15Accessdatafromremoteapp_SPhosted"> </a> 

### <a name="access-data-from-an-additional-remote-host-in-a-sharepoint-hosted-add-in"></a>Доступ к данным на дополнительном удаленном узле в надстройках с размещением в SharePoint

По умолчанию Надстройки, размещаемые в SharePoint разрешено выполнять междоменные вызовы для хост-сайта, если у него есть необходимые разрешения. Однако Надстройки, размещаемые в SharePoint также может указать удаленный узел в атрибуте **AllowedRemoteHostUrl****AppPrincipal**. Это позволяет эффективно выполнять междоменные вызовы из сайта надстройки и других узлов.

Скачать пример надстройки с размещением в SharePoint, использующей междоменную библиотеку, можно [здесь](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-00c37814).

## <a name="see-also"></a>См. также
<a name="SP15Accessdatafromremoteapp_Addresources"> </a>

- [Пример кода: запрос названия хост-сайта с помощью междоменной библиотеки (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Get-the-0ec36bb6)
- [Пример кода: запрос названия хост-сайта с помощью междоменной библиотеки (JSOM)](http://code.msdn.microsoft.com/office/SharePoint-2013-Get-the-563f2a3d)
- [Пример кода: использование элемента управления хрома и междоменной библиотеки (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-a759e9f8)
- [Пример кода: использование элемента управления хрома и междоменной библиотеки (JSOM)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-97c30a2e)
- [Пример кода: использование дополнительных действий и междоменной библиотеки для заказа книг](http://code.msdn.microsoft.com/SharePoint-2013-Open-a-36d1598d)
- [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md) 
- [Создание пользовательской страницы прокси для междоменной библиотеки в SharePoint](create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint.md)
- [Отправка запросов удаленной службе с помощью веб-прокси в SharePoint](query-a-remote-service-using-the-web-proxy-in-sharepoint.md)
- [Создание надстроек SharePoint, использующих междоменную библиотеку](creating-sharepoint-add-ins-that-use-the-cross-domain-library.md)
- [Авторизация и аутентификация надстроек SharePoint](authorization-and-authentication-of-sharepoint-add-ins.md)
