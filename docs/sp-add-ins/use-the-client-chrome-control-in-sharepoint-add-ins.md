
# <a name="use-the-client-chrome-control-in-sharepoint-add-ins"></a>Использование клиентского элемента управления хрома в надстройках SharePoint
Узнайте, как использовать элемент управления хрома в надстройках в SharePoint.
 

 **Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

Элемент управления хрома в SharePoint позволяет использовать стили заголовков определенного сайта SharePoint в вашей надстройке без необходимости регистрировать серверную библиотеку или использовать специальные методы и средства. Чтобы использовать эту функцию, необходимо зарегистрировать библиотеку SharePoint JavaScript с помощью стандартного тега <script>. Вы можете использовать заполнитель с помощью HTML-элемента **div** и в дальнейшем настраивать этот элемент управления с использованием доступных параметров. Элемент управления наследует свой внешний вид от указанного веб-сайта SharePoint. 
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье
<a name="SP15Usechromecontrol_Prereq"> </a>

Для выполнения действий, описанных в этом примере, вам потребуется следующее:
 

 

- Visual Studio 2015;
    
 
- среда разработки для SharePoint (в случае локальных сценариев необходимо изолировать надстройку).
    
 
Руководство по настройке среды разработки согласно вашим потребностям см. в статье, посвященной [началу создания надстроек Office и SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).
 

 

### <a name="core-concepts-to-know-before-using-the-chrome-control"></a>Основные понятия, связанные с использованием элемента управления хрома

В приведенной ниже таблице перечислены полезные статьи, которые могут помочь вам ознакомиться с основными понятиями, связанными с использованием элемента управления хрома.
 

 

**Таблица 1. Основные понятия, связанные с использованием элемента управления хрома**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins)|Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать надстройки — небольшие и удобные в использовании решения для пользователей.|
| [Дизайн пользовательского интерфейса надстроек SharePoint](ux-design-for-sharepoint-add-ins)|Сведения о параметрах и вариантах построения пользовательского интерфейса при создании надстроек SharePoint.|
| [Хост-сайты, сайты надстроек и компоненты в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку SharePoint, какие компоненты развертываются на хост-сайте, а какие на сайте надстройки и как развертывается сайт надстройки в изолированном домене.|

## <a name="code-example-use-the-chrome-control-in-your-cloud-hosted-add-in"></a>Пример кода. Использование элемента управления хрома в надстройке, размещаемой в облаке
<a name="SP15Usechromecontrol_Codeexample"> </a>

Размещенная в облаке надстройка включает по крайней мере один удаленный компонент. Чтобы узнать больше, см.  [Выбор шаблонов для разработки и размещения надстройки SharePoint](choose-patterns-for-developing-and-hosting-your-sharepoint-add-in). Чтобы использовать элемент управления хрома в размещенной в облаке надстройке, сделайте следующее:
 

 

1. Создайте надстройку SharePoint и удаленные веб-проекты.
    
 
2. Отправьте параметры конфигурации по умолчанию в строке запроса.
    
 
3. Добавьте в веб-проект веб-страницу.
    
 
На рис. 1 показана удаленная веб-страница с элементом управления хрома.
 

 

**Рис. 1. Удаленная веб-страница с элементом управления хрома**

 

 
![Удаленная веб-страница с элементом управления хрома](../../images/ChromeControl_result.png)
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a>Создание надстройки SharePoint и удаленных веб-проектов


1. Откройте Visual Studio 2015 от имени администратора. Для этого щелкните правой кнопкой мыши значок Visual Studio 2015 в меню **Пуск** и выберите пункт **Запуск от имени администратора**.
    
 
2. Создайте проект, используя шаблон **Надстройка SharePoint**.
    
    На рис. 2 показано расположение шаблона **Надстройка SharePoint** в Visual Studio 2015: **Шаблоны**, **Visual C#**, **Office/SharePoint**, **Надстройки Office**.
    

    **Рис. 2. Шаблон надстройки SharePoint в Visual Studio**

 

  ![Шаблон приложения для SharePoint в Visual Studio](../../images/AppForSharePointVSTemplate.PNG)
 

 

 
3. Укажите URL-адрес веб-сайта SharePoint, который планируется использовать для отладки.
    
 
4. Выберите **Размещение у поставщика** в качестве варианта размещения надстройки. Пример кода с размещением в SharePoint: [SharePoint-Add-in-JSOM-BasicDataOperations](https://github.com/OfficeDev/SharePoint-Add-in-JSOM-BasicDataOperations).
    
    После завершения работы мастера в **обозревателе решений** появится структура, подобная представленной на рис. 3.
    

    **Рис. 3. Проекты надстроек SharePoint в обозревателе решений**

 

  ![Проекты надстроек SharePoint в обозревателе решений](../../images/AppVSTemplateSolutionExplorer.jpg)
 

 

 

### <a name="to-send-default-configuration-options-in-the-query-string"></a>Отправка параметров конфигурации по умолчанию в строке запроса


1. Откройте файл Appmanifest.xml в редакторе манифеста.
    
 
2. Добавьте в строку запроса маркер **{StandardTokens}** и дополнительный параметр _SPHostTitle_. На рис. 4 показан редактор манифеста с настроенными параметрами строки запроса.
    
    **Рис. 4. Редактор манифеста с параметрами строки запроса для элемента управления хрома**

 

  ![Редактор манифеста с параметрами строки запроса](../../images/ChromeControl_manifest.PNG)
 

    Элемент управления хрома автоматически принимает из строки запроса следующие значения:
    
 

      -  **SPHostUrl**;
    
 
  -  **SPHostTitle**;
    
 
  -  **SPAppWebUrl**;
    
 
  -  **SPLanguage**.
    
 

     Маркер **{StandardTokens}** включает маркеры **SPHostUrl** и **SPAppWebUrl**.
    
 

### <a name="to-add-a-page-that-uses-the-chrome-control-in-the-web-project"></a>Добавление в веб-проект страницы с элементом управления хрома


1. Щелкните правой кнопкой мыши веб-проект и добавьте новую веб-форму.
    
 
2. Скопируйте следующие исправления и вставьте их на страницу ASPX. Часть кода выполняет следующие действия:
    
      - загружает библиотеку AJAX из сети доставки содержимого Майкрософт (CDN);
    
 
  - загружает библиотеку jQuery из сети CDN корпорации Майкрософт;
    
 
  - загружает файл SP.UI.Controls.js с помощью функции jQuery **getScript**;
    
 
  - определяет функцию обратного вызова для события **onCssLoaded**;
    
 
  - подготавливает параметры для элемента управления хрома;
    
 
  - инициализирует элемент управления хрома.
    
 

```HTML
  <!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Chrome control host page</title>
    <script 
        src="//ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
        type="text/javascript">
    </script>
    <script 
        type="text/javascript" 
        src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
    </script>      
    <script 
        type="text/javascript"
        src="ChromeLoader.js">
    </script>
<script type="text/javascript">
"use strict";

var hostweburl;

//load the SharePoint resources
$(document).ready(function () {
    //Get the URI decoded URL.
    hostweburl =
        decodeURIComponent(
            getQueryStringParameter("SPHostUrl")
    );

    // The SharePoint js files URL are in the form:
    // web_url/_layouts/15/resource
    var scriptbase = hostweburl + "/_layouts/15/";

    // Load the js file and continue to the 
    //   success handler
    $.getScript(scriptbase + "SP.UI.Controls.js", renderChrome)
});

// Callback for the onCssLoaded event defined
//  in the options object of the chrome control
function chromeLoaded() {
    // When the page has loaded the required
    //  resources for the chrome control,
    //  display the page body.
    $("body").show();
}

//Function to prepare the options and render the control
function renderChrome() {
    // The Help, Account and Contact pages receive the 
    //   same query string parameters as the main page
    var options = {
        "appIconUrl": "siteicon.png",
        "appTitle": "Chrome control add-in",
        "appHelpPageUrl": "Help.html?"
            + document.URL.split("?")[1],
        // The onCssLoaded event allows you to 
        //  specify a callback to execute when the
        //  chrome resources have been loaded.
        "onCssLoaded": "chromeLoaded()",
        "settingsLinks": [
            {
                "linkUrl": "Account.html?"
                    + document.URL.split("?")[1],
                "displayName": "Account settings"
            },
            {
                "linkUrl": "Contact.html?"
                    + document.URL.split("?")[1],
                "displayName": "Contact us"
            }
        ]
    };

    var nav = new SP.UI.Controls.Navigation(
                            "chrome_ctrl_placeholder",
                            options
                        );
    nav.setVisible(true);
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
</head>

<!-- The body is initally hidden. 
     The onCssLoaded callback allows you to 
     display the content after the required
     resources for the chrome control have
     been loaded.  -->
<body style="display: none">

    <!-- Chrome control placeholder -->
    <div id="chrome_ctrl_placeholder"></div>

    <!-- The chrome control also makes the SharePoint
          Website stylesheet available to your page -->
    <h1 class="ms-accentText">Main content</h1>
    <h2 class="ms-accentText">The chrome control</h2>
    <div id="MainContent">
        This is the page's main content. 
        You can use the links in the header to go to the help, 
        account or contact pages.
    </div>
</body>
</html>
```

3. Элемент управления хрома также можно использовать декларативным способом. В следующем примере кода в разметке HTML элемент управления объявляется без использования кода JavaScript для его настройки и инициализации. Эта разметка выполняет следующие задачи:
    
      - предоставляет заполнитель для файла SP.UI.Controls.js JavaScript;
    
 
  - динамически загружает файл SP.UI.Controls.js;
    
 
  - предоставляет заполнитель для элемента управления хрома и задает его параметры.
    
 

```HTML
  <!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Chrome control host page</title>
    <script 
        src="http://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
        type="text/javascript">
    </script>
    <script 
        type="text/javascript" 
        src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
    </script>      
    <script type="text/javascript">
    var hostweburl;

    // Load the SharePoint resources.
    $(document).ready(function () {

        // Get the URI decoded add-in web URL.
        hostweburl =
            decodeURIComponent(
                getQueryStringParameter("SPHostUrl")
        );

        // The SharePoint js files URL are in the form:
        // web_url/_layouts/15/resource.js
        var scriptbase = hostweburl + "/_layouts/15/";

        // Load the js file and continue to the 
        // success handler.
        $.getScript(scriptbase + "SP.UI.Controls.js")
    });

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
</head>
<body>

    <!-- Chrome control placeholder 
           Options are declared inline.  -->
    <div 
        id="chrome_ctrl_container"
        data-ms-control="SP.UI.Controls.Navigation"  
        data-ms-options=
            '{  
                "appHelpPageUrl" : "Help.html",
                "appIconUrl" : "siteIcon.png",
                "appTitle" : "Chrome control add-in",
                "settingsLinks" : [
                    {
                        "linkUrl" : "Account.html",
                        "displayName" : "Account settings"
                    },
                    {
                        "linkUrl" : "Contact.html",
                        "displayName" : "Contact us"
                    }
                ]
             }'>
    </div>
    
    <!-- The chrome control also makes the SharePoint
          Website style sheet available to your page. -->
    <h1 class="ms-accentText">Main content</h1>
    <h2 class="ms-accentText">The chrome control</h2>
    <div id="MainContent">
        This is the page's main content. 
        You can use the links in the header to go to the help, 
        account or contact pages.
    </div>
</body>
</html>
```


    The SP.UI.Controls.js library automatically renders the control if it finds the  **data-ms-control="SP.UI.Controls.Navigation"** attribute in a **div** element.
    
 

### <a name="to-edit-the-startpage-element-in-the-add-in-manifest"></a>Изменение элемента StartPage в манифесте надстройки


1. Дважды щелкните файл **AppManifest.xml** в **обозревателе решений**.
    
 
2. В раскрывающемся меню **Начальная страница** выберите веб-страницу, на которой используется элемент управления хрома.
    
 

### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения


1. Убедитесь, что проект Надстройка SharePoint выбран как запускаемый проект.
    
 
2. Нажмите клавишу F5.
    
     **Примечание.** При нажатии клавиши F5 Visual Studio собирает решение, развертывает надстройку и открывает страницу ее разрешений.
3. Нажмите кнопку **Доверять**.
    
 
4. Нажмите значок надстройки **ChromeControlCloudhosted**.
    
 
5. При использовании элемента управления хрома на веб-страницах вы также можете использовать таблицу стилей веб-сайта SharePoint, как показано на рис. 4.
    
    **Рис. 5. Таблица стилей веб-сайта SharePoint на странице**

 

  ![Таблица стилей веб-сайта SharePoint на странице](../../images/ChromControl_stylesheet.png)
 

 

 

**Таблица 2. Устранение неполадок в решении**


|**Проблема**|**Решение**|
|:-----|:-----|
|Необработанное исключение **SP не определен**.|Убедитесь, что браузер загружает файл SP.UI.Controls.js.|
|Элемент управления хрома не выполняет обработку должным образом.|Элемент управления хрома поддерживает только режимы документов Internet Explorer 8 и более поздних версий. Убедитесь, что браузер отображает страницу в режиме документов Internet Explorer 8 и более поздних версий.|
|Ошибка сертификата.|Задайте для свойства **SSL включен** веб-проекта значение false. В проекте надстройки SharePoint задайте для свойства **Веб-проект** значение None, а затем снова укажите в нем имя веб-проекта.|

## <a name="next-steps"></a>Дальнейшие действия
<a name="SP15Usechromecontrol_Nextsteps"> </a>

В этой статье показано, как использовать элемент управления хрома в надстройке SharePoint. Далее вы можете узнать о других компонентах UX, доступных для надстроек SharePoint. Дополнительные сведения см. в следующих статьях:
 

 

-  [Пример кода. Использование элемента управления хрома в надстройке, размещаемой в облаке](http://code.msdn.microsoft.com/SharePoint-2013-Work-with-089ecc6f)
    
 
-  [Пример кода. Использование элемента управления хрома и междоменной библиотеки (CSOM)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-97c30a2e)
    
 
-  [Пример кода. Использование элемента управления хрома и междоменной библиотеки (REST)](http://code.msdn.microsoft.com/SharePoint-2013-Use-the-a759e9f8)
    
 
-  [Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [Создание дополнительных действий для развертывания с надстройками SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins)
    
 
-  [Создание веб-частей надстроек для установки вместе с надстройкой SharePoint](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Usechromecontrol_Addresources"> </a>


-  [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [Дизайн пользовательского интерфейса надстроек SharePoint](ux-design-for-sharepoint-add-ins)
    
 
-  [Рекомендации по проектированию пользовательского интерфейса надстроек SharePoint](sharepoint-add-ins-ux-design-guidelines)
    
 
-  [Создание компонентов пользовательского интерфейса в SharePoint](create-ux-components-in-sharepoint-2013)
    
 
-  [Три представления о вариантах разработки надстроек SharePoint](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [Важные аспекты архитектуры и разработки надстроек SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

