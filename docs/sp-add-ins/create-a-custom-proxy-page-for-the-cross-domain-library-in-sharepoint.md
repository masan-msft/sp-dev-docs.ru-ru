---
title: Создание пользовательской страницы прокси для междоменной библиотеки в SharePoint
description: Создайте настраиваемую страницу прокси для доступа к данным в удаленной службе с веб-страницы SharePoint, используя междоменную библиотеку в SharePoint.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: da07fa22d0317199da1d1688adc644f98771a47c
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="create-a-custom-proxy-page-for-the-cross-domain-library-in-sharepoint"></a>Создание настраиваемой страницы прокси для междоменной библиотеки в SharePoint

В процессе создания создании надстроек SharePoint обычно приходится использовать данные из различных источников. При этом из соображений безопасности применяются механизмы блокировки, которые препятствуют обмену данными с более чем одним доменом одновременно.

Вы можете использовать междоменную библиотеку для доступа к данным в удаленной надстройке, если реализуете настраиваемую прокси-страницу, размещенную в инфраструктуре удаленной надстройки. Как разработчик вы отвечаете за реализацию настраиваемой прокси-страницы и пользовательской логики, например, за механизм проверки подлинности для удаленной надстройки. Используйте междоменную библиотеку с настраиваемой прокси-страницей, если необходимо, чтобы взаимодействие происходило на уровне клиента.
 
<a name="SP15Createcustomproxypage_Prereq"> </a>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье

Вам необходима среда разработки, описанная в статье [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).

### <a name="core-concepts-to-know-before-using-a-custom-proxy-page-with-sharepoint-add-ins"></a>Ключевые понятия, с которыми необходимо ознакомиться перед использованием настраиваемой страницы прокси вместе с надстройками SharePoint

Ниже перечислены полезные статьи, в которых описано, как запрашивать данные для надстроек SharePoint из удаленного домена.

|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins.md)|Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.|
| [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)|Узнайте о параметрах доступа к данным в Надстройки SharePoint. В этой статье представлена информация об альтернативах высокого уровня при работе с данными в надстройке.|
| [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включить в Надстройка SharePoint, какие компоненты можно развернуть на хост-сайтах, а какие на сайтах надстроек, а также узнайте, как развертывать сайты надстроек в изолированном домене.|
| [Междоменная безопасность на стороне клиента](http://msdn.microsoft.com/ru-RU/library/cc709423%28v=vs.85%29.aspx)|Изучите междоменные угрозы и примеры использования, а также принципы безопасности для междоменных запросов, и оцените риски разработчиков, связанные с улучшением междоменного доступа из веб-приложений, которые запускаются в браузере.|

<a name="SP15Createcustomproxypage_Codeexample"> </a>

## <a name="code-example-access-remote-data-using-a-custom-proxy-page-for-the-cross-domain-library"></a>Пример кода. Доступ к удаленным данным с помощью настраиваемой страницы прокси для междоменной библиотеки

Чтобы прочесть данные из удаленной службы, выполните указанные ниже действия. 

1. Создайте проект надстройки для SharePoint.
    
2. Измените манифест надстройки, чтобы разрешить связь с удаленной надстройкой.

3. Создать настраиваемую прокси-страницу и страницу контента в веб-проекте.

4. Создать страницу, которая использует междоменную библиотеку в проекте Надстройка SharePoint.

### <a name="to-create-the-sharepoint-add-in-project"></a>Создание проекта надстройки SharePoint

1. Откройте Visual Studio от имени администратора. (Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.)
    
2. Создайте надстройку SharePoint с размещением у поставщика, как описано в [этой статье](get-started-creating-provider-hosted-sharepoint-add-ins.md), и назовите ее **ProxyPageApp**. 
    
### <a name="to-edit-the-add-in-manifest-file"></a>Изменение файла манифеста надстройки

1. В **обозревателе решений** щелкните правой кнопкой мыши файл **AppManifest.xml** и выберите **Просмотреть код**.
    
2. Замените весь элемент **AppPrincipal** указанным ниже фрагментом.
    
    ```XML
    <AppPrincipal>
        <Internal AllowedRemoteHostUrl="~remoteAppUrl"/>
    </AppPrincipal>
    ```

> [!NOTE] 
> Атрибут **AllowedRemoteHostUrl** используется для указания удаленного домена. **~remoteAppUrl** принимает значение URL-адреса удаленной надстройки. Дополнительные сведения о маркерах см. в статье [Изучение структуры манифеста приложения и пакета надстройки SharePoint](explore-the-app-manifest-structure-and-the-package-of-a-sharepoint-add-in.md).

### <a name="to-create-a-custom-proxy-page"></a>Создание настраиваемой страницы прокси

1. После создания решения Visual Studio щелкните правой кнопкой мыши проект веб-приложения (не проект надстройки SharePoint) и выберите **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**, чтобы добавить новую веб-форму. Присвойте форме имя **Proxy.aspx**.
 
2. В файле Proxy.aspx замените весь HTML-элемент и его дочерние элементы следующим HTML-кодом. Оставьте всю разметку над HTML-элементом без изменений. HTML-код содержит разметку и скрипт JavaScript, который выполняет следующие задачи:
    
    - Предоставляет заполнитель для файла междоменной библиотеки JavaScript.

    - Извлекает URL-адрес сайта надстройки из источника ссылки.
 
    - Динамически загружает файл JavaScript междоменной библиотеки в заполнитель.

    - Предоставляет параметры для объекта **RequestExecutorMessageProcessor**.

    - Инициализирует объект **RequestExecutorMessageProcessor**.

    ```HTML
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <meta http-equiv="X-UA-Compatible" content="IE=8" /> 
        <title>Custom Proxy Host Page</title>
        <script 
            src="http://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js" 
            type="text/javascript">
        </script>
        <script 
            type="text/javascript" 
            src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js">
        </script>

        <!-- Script to load the cross-domain library js file -->
        <script type="text/javascript">
            var hostweburl;

            $(document).ready(function(){
                //Get the URI decoded host web URL.
                hostweburl =
                    decodeURIComponent(
                        getQueryStringParameter("SPHostUrl")
                );

                // The cross-domain js file is in a URL in the form:
                // host_web_url/_layouts/15/SP.RequestExecutor.js
                var scriptbase = hostweburl + "/_layouts/15/";

                // Load the js file 
                $.getScript(scriptbase + "SP.RequestExecutor.js", initCustomProxy);
            });

            //Function to initialize the custom proxy page
            //  must set the appropriate settings and implement
            //  proper authentication mechanism
            function initCustomProxy() {
                var settings =
                {
                    originAuthorityValidator: function (messageOriginAuthority) {
                        // This page must implement the authentication for the
                        //   remote add-in.
                        // You should validate if messageOriginAuthority is
                        //  an approved domain to receive calls from.
                        return true;
                    }
                };
                SP.RequestExecutorMessageProcessor.init(settings);
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
    <body>
        
    </body>
    </html>
    ```

<br/>

> [!IMPORTANT] 
> В производственной надстройке SharePoint необходимо предоставить логику авторизации и вернуть соответствующее значение в объект **originAuthorityValidator** в параметрах.

### <a name="to-create-a-content-page"></a>Создание страницы содержимого

1. Щелкните правой кнопкой мыши проект веб-приложения в **обозревателе решений** и выберите **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**, чтобы добавить новую веб-форму. Присвойте форме имя **Content.aspx**.

2. Скопируйте указанный ниже код и вставьте его в метод **Page_Load** в файле с выделенным кодом. Этот код выполняет следующие задачи.
    
    - Устанавливает для **content-type** значение **text/plain**.

    - Записывает контент в выходной буфер.

    - Завершает подключение.

    ```C#
    string content;
    content = "Just some text.";
    Response.ContentType="text/plain";
    Response.Write(content);
    Response.End();

    ```

<br/>

### <a name="to-create-a-sharepoint-webpage-that-uses-the-cross-domain-library"></a>Создание веб-страницы SharePoint, использующей междоменную библиотеку

1. Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Модуль**.

2. Присвойте модулю имя **Pages** и нажмите **Добавить**.

3. Щелкните папку Pages правой кнопкой мыши и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Страница**. 

4. Задайте для страницы имя **Home.aspx** и нажмите кнопку **Добавить**.

5. Если страница Home.aspx не открылась автоматически, откройте ее.

6. Скопируйте указанный ниже код и вставьте его в тег содержимого **PlaceHolderMain**.
        
    ```js
    <!-- The page dynamically loads the cross-domain library's
        js file, rescript acts as the placeholder. -->
    <script 
        type="text/javascript"
        id="rescript"
        src="../_layouts/15/SP.RequestExecutor.js">
    </script>
        Data from the remote domain: <span id="TextData"></span>

        <!-- Main script to retrieve the host web's title -->
        <script type="text/javascript">
        (function () {
            var executor;
            var hostweburl;
            var remotedomain;

            remotedomain = "<your_remote_add-in_domain>";

            //Get the URI decoded host web URL.
            hostweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPHostUrl")
            );

            // Initialize the RequestExecutor with the custom proxy URL.
            executor = new SP.RequestExecutor(remotedomain);
            executor.iFrameSourceUrl = "Proxy.aspx?SPHostUrl=" + hostweburl;

            // Issue the call against the remote endpoint.
            // The response formats the data in plain text.
            // The functions successHandler and errorHandler attend the
            //      sucess and error events respectively.
            executor.executeAsync(
                {
                    url:
                        remotedomain + "Content.aspx",
                    method: "GET",
                    headers: { "Accept": "text/plain" },
                    success: successHandler,
                    error: errorHandler
                }
            );
        })();

        // Function to handle the success event.
        // Prints the data to the placeholder.
        function successHandler(data) {
            document.getElementById("TextData").innerText =
                data.body;
        }

        // Function to handle the error event.
        // Prints the error message to the page.
        function errorHandler(data, errorCode, errorMessage) {
            document.getElementById("TextData").innerText =
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

    ```

    <br/>

7. В ранее вставленном вами фрагменте кода найдите строку `remotedomain = "<your_remote_add-in_domain>";` и замените заполнитель _<домен_вашей_удаленной_надстройки>_ URL-адресом "localhost", который ваше веб-приложение использует, когда вы запускаете надстройку клавишей F5 в Visual Studio. Чтобы найти это значение, выберите проект веб-приложения в **обозревателе решений**. Свойство **URL** находится на панели **Свойства**. Используйте это значение целиком, включая протокол, порт и закрывающий символ косой черты, например `http://localhost:45072`.
    
8. Сохраните и закройте файл.
    
9. Откройте файл appmanifest.xml и задайте для параметра **Начальная страница** значение **ProxyPageApp/Pages/Home.aspx**.
    
### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения

1. Убедитесь, что проект надстройки SharePoint выбран как запускаемый проект.

2. Нажмите клавишу F5.
    
    > [!NOTE] 
    > При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.

3. Нажмите кнопку **Доверять**.
    
    Откроется домашняя страница, которая должна выглядеть следующим образом. Может потребоваться несколько секунд, чтобы появилась фраза "Just some text", так как она извлекается со страницы Content.aspx удаленного домена.
 
    ![Страница SharePoint с данными из удаленной службы](../images/CustomProxy_result.jpg)

#### <a name="troubleshooting-the-solution"></a>Устранение неполадок в решении

|**Проблема**|**Решение**|
|:-----|:-----|
|Visual Studio не открывает браузер после нажатия клавиши F5.|Сделайте проект надстройки SharePoint запускаемым.|
|Необработанное исключение **SP не определен**.|Убедитесь, что у вас есть доступ к файлу SP.RequestExecutor.js в окне браузера.|

## <a name="see-also"></a>Дополнительные ресурсы
<a name="SP15Createcustomproxypage_Addresources"> </a>

- [Пример кода. Получение данных с помощью страницы прокси для междоменной библиотеки](https://code.msdn.microsoft.com/SharePoint-2013-Get-data-10039ff1)
- [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint.md)

    
 

