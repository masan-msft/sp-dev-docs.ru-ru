---
title: Отправка запросов удаленной службе с помощью веб-прокси в SharePoint
description: Доступ к данным в удаленном домене со страницы, размещенной в SharePoint, с помощью веб-прокси.
ms.date: 12/22/2017
ms.prod: sharepoint
ms.openlocfilehash: 4a1a8516ad4496b977f4191608946bb25b31d9dc
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="query-a-remote-service-using-the-web-proxy-in-sharepoint"></a>Запрос данных в удаленной службе с помощью веб-прокси в SharePoint

При создании надстроек SharePoint обычно необходимо объединять данные из различных источников. Из соображений безопасности связь между доменами блокируется. Если вы используете веб-прокси, веб-страницам в надстройке доступны данные на удаленном домене и домене SharePoint.

Разработчики могут использовать веб-прокси, предоставляемый в клиентских объектных моделях JavaScript и .NET. При использовании веб-прокси вы передаете запрос инициализации в SharePoint. SharePoint в свою очередь запрашивает данные в определенной конечной точке и передает ответ обратно на вашу страницу.

Используйте веб-прокси, если нужно, чтобы связь осуществлялась на уровне сервера. Дополнительные сведения см. в статье [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md).

**Веб-прокси SharePoint — это посредник между вашим кодом и внешним источником данных**

![Символы "ваш код", "веб-прокси SharePoint" и "источник данных", показывающие, что запросы данных проходят через веб-прокси.](../images/3fbdcfae-6af9-452b-9a07-48575de7e86a.png)

<a name="SP15Queryremoteservice_Prereq"> </a>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье

Для выполнения действий, описанных в этом примере, вам потребуется следующее:

-  [Visual Studio 2015 и Инструменты разработчика Microsoft Office последней версии](https://www.visualstudio.com/features/office-tools-vs.aspx)

- Среда разработки SharePoint (для локальных сценариев необходимо изолировать надстройку).

### <a name="core-concepts-to-know-before-using-the-web-proxy"></a>Ключевые понятия, с которыми необходимо ознакомиться до использования веб-прокси

Ниже перечислены полезные статьи, в которых описано, как запрашивать данные для надстроек SharePoint из удаленного домена.

|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins.md)|Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.|
| [Безопасный доступ к данным и клиентские объектные модели для надстроек SharePoint](secure-data-access-and-client-object-models-for-sharepoint-add-ins.md)|Узнайте о вариантах доступа к данным в надстройках SharePoint. В этой статье представлена информация о вариантах работы с данными в надстройке.|
| [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включить в Надстройка SharePoint, какие компоненты можно развернуть на хост-сайтах, а какие на сайтах надстроек, а также узнайте, как развертывать сайты надстроек в изолированном домене.|
| [Междоменная безопасность на стороне клиента](http://msdn.microsoft.com/ru-RU/library/cc709423%28v=vs.85%29.aspx)|Ознакомьтесь с междоменными угрозами, случаями использования и принципами безопасности для междоменных запросов, а также оцените риски для разработчиков, возникающие при расширении междоменного доступа из веб-приложений, которые запускаются в браузере.|

<a name="SP15Queryremoteservice_Codeexample"> </a>

## <a name="code-example-access-data-in-a-remote-service-using-the-web-proxy"></a>Пример кода. Доступ к данным в удаленной службе с помощью веб-прокси

Чтобы прочитать данные из удаленной службы, необходимо выполнить указанные ниже действия. 

1. Создайте проект надстройки для SharePoint.

2. Измените страницу **Default.aspx**, чтобы использовать веб-прокси для запроса удаленной службы.

3. Измените манифест надстройки, чтобы разрешить связь с удаленным доменом.

На следующем рисунке показано окно браузера с данными из удаленной службы на веб-странице SharePoint.

**Веб-страница SharePoint с данными из удаленной службы**

![Страница SharePoint с данными из удаленной службы](../images/WebProxy_result.png)
 

### <a name="to-create-the-sharepoint-add-in-project"></a>Создание проекта надстройки SharePoint

1. Откройте Visual Studio 2015 от имени администратора. Для этого щелкните правой кнопкой мыши значок Visual Studio 2015 в меню **Пуск** и выберите **Запуск от имени администратора**.
    
2. Создайте новый проект с помощью шаблона **Надстройка SharePoint**.
    
    На следующем рисунке показано расположение шаблона **Надстройка SharePoint** в 2015: **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки Office**.
    
    **Шаблон надстройки SharePoint в Visual Studio**

    ![Шаблон приложения для SharePoint в Visual Studio](../images/AppForSharePointVSTemplate.PNG)

    <br/>

3. Укажите URL-адрес веб-сайта SharePoint, который планируется использовать для отладки.
    
4. Выберите **SharePoint-hosted** (Размещение в SharePoint) в качестве варианта размещения надстройки.
    

### <a name="to-modify-the-defaultaspx-page-to-use-the-web-proxy-by-using-the-javascript-object-model"></a>Изменение страницы Default.aspx для использования веб-прокси с помощью объектной модели JavaScript

1. Дважды щелкните страницу **Default.aspx** в папке **Страницы**.
    
2. Скопируйте следующую разметку и вставьте ее в тег содержимого **PlaceHolderMain** страницы. Разметка выполняет следующие задачи:
    
    - Предоставление заполнителя для удаленных данных.
    
    - Создание ссылки на файлы JavaScript в SharePoint.
        
    - Подготовка запроса с объектом **WebRequestInfo**.
        
    - Подготовка заголовка запроса **Accept** для указания ответа в формате Нотация объектов JavaScript (JSON).
    
    - Отправка вызова удаленной конечной точке.
        
    - Обработка успешного выполнения с отображением удаленных данных на веб-странице SharePoint.
    
    - Обработка любых ошибок с отображением сообщения об ошибке на веб-странице SharePoint.
 
    ```js
    Categories from the Northwind database exposed as an OData service: 
        
    <!-- Placeholder for the remote content -->
    <span id="categories"></span>

    <!-- Add references to the JavaScript libraries. -->
    <script 
        type="text/javascript" 
        src="../_layouts/15/SP.Runtime.js">
    </script>
    <script 
        type="text/javascript" 
        src="../_layouts/15/SP.js">
    </script>
    <script type="text/javascript">
    (function () {
        "use strict";

        // Prepare the request to an OData source
        // using the GET verb.
        var context = SP.ClientContext.get_current();
        var request = new SP.WebRequestInfo();
        request.set_url(
            "http://services.odata.org/Northwind/Northwind.svc/Categories"
            );
        request.set_method("GET");

        // We need the response formatted as JSON.
        request.set_headers({ "Accept": "application/json;odata=verbose" });
        var response = SP.WebProxy.invoke(context, request);

        // Let users know that there is some
        // processing going on.
        document.getElementById("categories").innerHTML =
                    "<P>Loading categories...</P>";

        // Set the event handlers and invoke the request.
        context.executeQueryAsync(successHandler, errorHandler);

        // Event handler for the success event.
        // Get the totalResults node in the response.
        // Render the value in the placeholder.
        function successHandler() {

            // Check for status code == 200
            // Some other status codes, such as 302 redirect
            // do not trigger the errorHandler. 
            if (response.get_statusCode() == 200) {
                var categories;
                var output;

                // Load the OData source from the response.
                categories = JSON.parse(response.get_body());

                // Extract the CategoryName and Description
                // from each result in the response.
                // Build the output as a list.
                output = "<UL>";
                for (var i = 0; i < categories.d.results.length; i++) {
                    var categoryName;
                    var description;
                    categoryName = categories.d.results[i].CategoryName;
                    description = categories.d.results[i].Description;
                    output += "<LI>" + categoryName + ":&amp;nbsp;" +
                        description + "</LI>";
                }
                output += "</UL>";

                document.getElementById("categories").innerHTML = output;
            }
            else {
                var errordesc;

                errordesc = "<P>Status code: " +
                    response.get_statusCode() + "<br/>";
                errordesc += response.get_body();
                document.getElementById("categories").innerHTML = errordesc;
            }
        }

        // Event handler for the error event.
        // Render the response body in the placeholder.
        // The body includes the error message.
        function errorHandler() {
            document.getElementById("categories").innerHTML =
                response.get_body();
        }
    })();
    </script>
    ```

    <br/>


### <a name="optional-to-modify-the-defaultaspx-page-to-use-the-web-proxy-by-using-the-rest-endpoint"></a>(Необязательно) Изменение страницы Default.aspx для использования веб-прокси с помощью конечной точки REST

1. Дважды щелкните страницу **Default.aspx** в папке **Страницы**.
    
2. Скопируйте следующую разметку и вставьте ее в тег содержимого **PlaceHolderMain** страницы. Разметка выполняет следующие задачи:
    
    - Предоставление заполнителя для удаленных данных.
     
    - Обращение к библиотеке jQuery.
    
    - Подготовка запроса к конечной точке **SP.WebRequest.Invoke**.
    
    - Подготовка текста запроса с объектом **SP.WebrequestInfo**. Он включает заголовок **Accept** для указания ответа в формате Нотация объектов JavaScript (JSON).
    
    - Отправка вызова удаленной конечной точке.
    
    - Обработка успешного выполнения с отображением удаленных данных на веб-странице SharePoint.
    
    - Обработка любых ошибок с отображением сообщения об ошибке на веб-странице SharePoint.
    
    ```js
    Categories from the Northwind database exposed as an OData service: 
        
    <!-- Placeholder for the remote content -->
    <span id="categories"></span>

    <script 
        type="text/javascript" 
        src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js">
    </script>

    <script type="text/javascript">
    (function () {
        "use strict";

        // The Northwind categories endpoint.
        var url =
            "http://services.odata.org/Northwind/Northwind.svc/Categories";

        // Let users know that there is some
        // processing going on.
        document.getElementById("categories").innerHTML =
                    "<P>Loading categories...</P>";

        // Issue a POST request to the SP.WebProxy.Invoke endpoint.
        // The body has the information to issue a GET request
        // to the Northwind service.
        $.ajax({
            url: "../_api/SP.WebProxy.invoke",
            type: "POST",
            data: JSON.stringify(
                {
                    "requestInfo": {
                        "__metadata": { "type": "SP.WebRequestInfo" },
                        "Url": url,
                        "Method": "GET",
                        "Headers": {
                            "results": [{
                                "__metadata": { "type": "SP.KeyValue" },
                                "Key": "Accept",
                                "Value": "application/json;odata=verbose",
                                "ValueType": "Edm.String"
                            }]
                        }
                    }
                }),
            headers: {
                "Accept": "application/json;odata=verbose",
                "Content-Type": "application/json;odata=verbose",
                "X-RequestDigest": $("#__REQUESTDIGEST").val()
            },
            success: successHandler,
            error: errorHandler
        });

        // Event handler for the success event.
        // Get the totalResults node in the response.
        // Render the value in the placeholder.
        function successHandler(data) {
            // Check for status code == 200
            // Some other status codes, such as 302 redirect,
            // do not trigger the errorHandler. 
            if (data.d.Invoke.StatusCode == 200) {
                var categories;
                var output;

                // Load the OData source from the response.
                categories = JSON.parse(data.d.Invoke.Body);

                // Extract the CategoryName and Description
                // from each result in the response.
                // Build the output as a list
                output = "<UL>";
                for (var i = 0; i < categories.d.results.length; i++) {
                    var categoryName;
                    var description;
                    categoryName = categories.d.results[i].CategoryName;
                    description = categories.d.results[i].Description;
                    output += "<LI>" + categoryName + ":&amp;nbsp;" +
                        description + "</LI>";
                }
                output += "</UL>";

                document.getElementById("categories").innerHTML = output;
            }
            else {
                var errordesc;

                errordesc = "<P>Status code: " +
                    data.d.Invoke.StatusCode + "<br/>";
                errordesc += response.get_body();
                document.getElementById("categories").innerHTML = errordesc;
            }
        }

        // Event handler for the error event.
        // Render the response body in the placeholder.
        // The 2nd argument includes the error message.
        function errorHandler() {
            document.getElementById("categories").innerHTML =
                arguments[2];
        }
    })();
    </script>

    ```

<br/>

### <a name="to-edit-the-add-in-manifest-file"></a>Изменение файла манифеста надстройки

1. В **обозревателе решений** откройте контекстное меню файла **AppManifest.xml** и выберите **Просмотреть код**.
    
2. Скопируйте следующее определение **RemoteEndPoints** в качестве дочернего элемента узла **App**.
    
    ```XML
    <RemoteEndpoints>
        <RemoteEndpoint Url=" http://services.odata.org" />
    </RemoteEndpoints>
    ```

Элемент **RemoteEndpoint** используется для указания удаленного домена. Веб-прокси проверяет, объявлены ли запросы к удаленным доменам в манифесте надстройки. Вы можете создать до 20 записей в элементе **RemoteEndpoints**. Учитывается только часть источника;  `http://domain:port` и `http://domain:port/website` считаются одной и той же конечной точкой. Вы можете осуществлять вызовы множества различных конечных точек в одном домене с помощью одного определения **RemoteEndpoint**.

### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения

1. Нажмите клавишу F5.
    
    > [!NOTE] 
    > При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.

2. Нажмите кнопку **Доверять**.
 
3. Выберите значок надстройки на странице "Содержимое сайта".
    
    Ниже показаны удаленные данные на веб-странице SharePoint.
    
    **Удаленные данные на веб-странице SharePoint**

    ![Страница SharePoint с данными из удаленной службы](../images/WebProxy_result.png)
 

#### <a name="troubleshooting-the-solution"></a>Устранение неполадок в решении

|**Проблема**|**Решение**|
|:-----|:-----|
|Visual Studio не открывает браузер после нажатия клавиши F5.|Сделайте проект надстройки SharePoint запускаемым.|
|Необработанное исключение **SP не определен**.|Убедитесь, что вы можете получить доступ к файлу SP.RequestExecutor.js в окне браузера. Если в качестве среды разработки используется локальный сервер, необходимо отключить проверку обратной связи IIS. <br/><br/>Выполните следующую команду с помощью командной строки Windows PowerShell: `New-ItemProperty HKLM:\System\CurrentControlSet\Control\Lsa -Name "DisableLoopbackCheck" -value "1" -PropertyType dword`.<br/><br/>**Внимание!** Не рекомендуется отключать проверку обратной связи IIS в рабочей среде. |
|Размер ответа от удаленной конечной точки превышает заданный лимит.|Размер ответа для запросов веб-прокси не должен превышать 200 КБ.|
|Комбинация "схема-порт" не поддерживается.|Комбинация "схема-порт" вызова должна отвечать следующим критериям:<br/><br/>**Схема** - **порт**<br/>HTTP — 80<br/>HTTPS — 443<br/>HTTP или HTTPS — 7000–10000<br/><br/>**Важно!** Исходящие порты зависят от доступности брандмауэра узла. В частности, в SharePoint Online доступны только порты HTTP-80 и HTTPS-443. |


## <a name="see-also"></a>Дополнительные ресурсы
<a name="SP15Createcustomproxypage_Addresources"> </a>

- [Пример кода. Получение данных из удаленной службы с помощью веб-прокси](https://code.msdn.microsoft.com/office/SharePoint-2013-Get-data-705bdcd5)
- [Работа с внешними данными в SharePoint](work-with-external-data-in-sharepoint.md)
