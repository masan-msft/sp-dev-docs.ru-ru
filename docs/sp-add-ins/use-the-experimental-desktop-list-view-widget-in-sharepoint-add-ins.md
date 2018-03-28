---
title: Использование экспериментального мини-приложения Desktop List View в надстройках SharePoint
description: Используйте мини-приложение Desktop List View в своих надстройках, чтобы показывать данные из списков, размещенных на сайте SharePoint.
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 0dbcff715dcaebb27878c2c23de8b4dbb6c5ff0a
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="use-the-experimental-desktop-list-view-widget-in-sharepoint-add-ins"></a>Использование экспериментального мини-приложения Desktop List View в надстройках SharePoint

Используйте мини-приложение Desktop List View на любой веб-странице, даже если она не размещена в SharePoint. Используйте мини-приложение List View в своих надстройках, чтобы показывать данные из списков, размещенных на сайте SharePoint.
 
> [!WARNING] 
> Экспериментальные мини-приложения Office для веб-страниц предоставляются только в целях исследования и сбора отзывов. Не следует использовать их в производственных сценариях. Поведение мини-приложений Office для веб-страниц может существенно измениться в будущих выпусках. Ознакомьтесь с [условиями лицензии на экспериментальные мини-приложения Office для веб-страниц](office-web-widgetsexperimental-license-terms.md).

С помощью мини-приложения "Представление списка" вы можете отображать данные в списке SharePoint подобно тому, как это делается с помощью обычного мини-приложения "Представление списка", но вы можете использовать его даже в тех надстройках и на веб-сайтах, которые не размещены в SharePoint.

<br/>

**Мини-приложение Desktop List View, в котором показаны данные в списке**

![Экспериментальный элемент управления Desktop List View на странице](../images/DesktopListView_basic.png)

<br/>

Вы можете указать в списке SharePoint представление, которое вы хотите использовать для отображения данных. Виджет "Представление списка" отображает столбцы и элементы в порядке, который указывает представление.

Мини-приложение List View использует междоменную библиотеку для получения данных списка, поэтому передача информации происходит на уровне клиента.
 
> [!NOTE] 
> Мини-приложение Desktop List View позволяет выполнять не все сценарии собственного представления списка.

В текущей версии мини-приложения не включены следующие сценарии:

- использование виджета в схемах проверки подлинности, неподдерживаемых междоменной библиотекой;
- использование виджета с другими источниками данных, кроме библиотек и списков SharePoint;
- привязка виджета к данным;
- представления с сенсорным управлением;
- встроенная правка пользователями;
- показ информации о присутствии;
- настраиваемые шаблоны отрисовки;
- локальные сценарии. В данный момент виджет работает только в SharePoint Online.


## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье

Для выполнения примеров, описанных в этой статье, вам необходимо следующее:

- Visual Studio 2013 или более поздней версии.

- Диспетчер пакетов NuGet. Дополнительные сведения см. в статье [Установка клиентских средств NuGet](https://docs.microsoft.com/ru-RU/nuget/guides/install-nuget).
    
- Среда разработки SharePoint (для локальных сценариев требуется изоляция приложений). 
    
- Пакет NuGet "Экспериментальные мини-приложения Office для веб-страниц". Дополнительные сведения об установке пакетов NuGet см. в статье [Пользовательский интерфейс диспетчера пакетов NuGet](https://docs.microsoft.com/ru-RU/nuget/tools/package-manager-ui). Вы также можете просмотреть [страницу коллекции NuGet](https://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).
    
## <a name="use-the-desktop-list-view-widget-in-a-provider-hosted-sharepoint-add-in"></a>Использование мини-приложения Desktop List View в надстройке SharePoint с размещением у поставщика

В этом примере показана простая страница, размещенная вне SharePoint, которая объявляет мини-приложение Desktop List View.

Чтобы использовать мини-приложение Desktop List View:

- Создайте надстройку SharePoint и веб-проекты.
    
- Создайте список на сайте надстройки. Этот шаг также гарантирует создание сайта надстройки при ее развертывании.
    
    > [!NOTE] 
    > Междоменная библиотека требует наличия сайта надстройки. Мини-приложение List View связывается с SharePoint с помощью междоменной библиотеки.

- Создайте страницу надстройки, которая объявляет экземпляр мини-приложения List View, используя разметку HTML.

### <a name="to-create-a-sharepoint-add-in-and-web-projects"></a>Создание надстройки SharePoint и веб-проектов

1. Откройте Visual Studio от имени администратора. (Для этого выберите значок Visual Studio в меню **Пуск** и пункт **Запуск от имени администратора**.)

2. Создайте проект, используя шаблон **Надстройка SharePoint**. Шаблон "Надстройка SharePoint" находится в разделе **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки**.

3. Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.

4. Выберите для надстройки вариант размещения **Размещено у поставщика**.
    
    > [!NOTE] 
    > Вы также можете использовать мини-приложение Desktop List View с другими вариантами размещения или даже с надстройками Office или собственным веб-сайтом.

5. Выберите **Приложение веб-форм ASP.NET** в качестве типа проекта веб-приложения.
 
6. Выберите **службу контроля доступа Windows Azure** в качестве способа проверки подлинности.
    
 

### <a name="to-create-a-list-on-the-add-in-web"></a>Создание списка на сайте надстройки

1. Выберите проект надстройки SharePoint в **обозревателе решений**, а затем — команду **Добавить** > **Создать элемент**.
    
2. Выберите **Элементы Visual C#** > **Office/SharePoint** > **Список**. Введите **Объявления** в текстовое поле **Имя** и нажмите кнопку **Добавить**.
 
3. Выберите **Создать экземпляр списка на основе существующего шаблона списка**. Выберите шаблон **Объявления** и нажмите кнопку **Готово**.
    
 

### <a name="to-add-a-new-page-that-uses-the-desktop-list-view-widget"></a>Добавление новой страницы, использующей мини-приложение Desktop List View


1. Выберите папку **Страницы** веб-проекта в **обозревателе решений**.
    
 
2. Скопируйте приведенный ниже код и вставьте его в **ASPX**-файл проекта. Код выполняет следующие задачи:
    
    - добавляет ссылки на необходимые библиотеки и ресурсы Office;

    - предоставляет заполнитель для виджета "Представление списка";

    - инициализирует среду выполнения элементов управления;

    - запускает метод **renderAll** среды выполнения для элементов управления Office.
        
    ```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <!-- IE9 or superior -->
        <meta http-equiv="x-ua-compatible" content="IE=10">
        <title>Desktop List View HTML Markup</title>

        <!-- Controls Specific CSS File -->
        <link rel="stylesheet" type="text/css" href="/Scripts/Office.Controls.css" />

        <!-- Ajax, jQuery, and utils -->
        <script 
            src=" https://ajax.aspnetcdn.com/ajax/4.0/1/MicrosoftAjax.js.js">
        </script>
        <script 
            src=" https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js">
        </script>
        <script type="text/javascript">

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

        <!-- Cross-Domain Library and Office controls runtime -->
        <script type="text/javascript">
            //Register namespace and variables used through the sample
            Type.registerNamespace("Office.Samples.ListViewBasic");
            //Retrieve context tokens from the querystring
            Office.Samples.ListViewBasic.appWebUrl =
                decodeURIComponent(getQueryStringParameter("SPAppWebUrl"));
            Office.Samples.ListViewBasic.hostWebUrl =
                decodeURIComponent(getQueryStringParameter("SPHostUrl"));
            Office.Samples.ListViewBasic.ctag =
                decodeURIComponent(getQueryStringParameter("SPClientTag"));

            //Pattern to dynamically load JSOM and the cross-domain library
            var scriptbase =
                Office.Samples.ListViewBasic.hostWebUrl + "/_layouts/15/";

            //Get the cross-domain library
            $.getScript(scriptbase + "SP.RequestExecutor.js", 
                //Get the Office controls runtime and 
                //  continue to the createControl function
                function () {
                    $.getScript("../Scripts/Office.Controls.js", createControl);
                }
            );
        </script>

        <!-- List View -->
        <script 
            src="../Scripts/Office.Controls.ListView.debug.js" 
            type="text/javascript">
        </script>

        <!-- SharePoint CSS -->
        <script type="text/javascript">
            document.addEventListener("DOMContentLoaded", function () {
                // The resource files are in a URL in the form:
                // web_url/_layouts/15/Resource.ashx
                var scriptbase =
                    Office.Samples.ListViewBasic.appWebUrl + "/_layouts/15/";

                // Dynamically create the invisible iframe.
                var blankiframe;
                var blankurl;
                var body;
                blankurl =
                    Office.Samples.ListViewBasic.appWebUrl + "/Pages/blank.html";
                blankiframe = document.createElement("iframe");
                blankiframe.setAttribute("src", blankurl);
                blankiframe.setAttribute("style", "display: none");
                body = document.getElementsByTagName("body");
                body[0].appendChild(blankiframe);

                // Dynamically create the link element.
                var dclink;
                var head;
                dclink = document.createElement("link");
                dclink.setAttribute("rel", "stylesheet");
                dclink.setAttribute("href",
                                    scriptbase +
                                    "defaultcss.ashx?ctag=" +
                                    Office.Samples.ListViewBasic.ctag
                                    );
                head = document.getElementsByTagName("head");
                head[0].appendChild(dclink);
            }, false);
        </script>
    </head>
    <body>
        Basic List View sample (HTML markup declaration):
        <div id="ListViewDiv"
            data-office-control="Office.Controls.ListView"
            data-office-options='{"listUrl" : getListUrl()}'>
        </div>

        <script type="text/javascript">
            function createControl() {
                //Initialize Controls Runtime
                Office.Controls.Runtime.initialize({
                    sharePointHostUrl: Office.Samples.ListViewBasic.hostWebUrl,
                    appWebUrl: Office.Samples.ListViewBasic.appWebUrl
                });

                //Render the widget, this must be executed after the
                //placeholder DOM is loaded
                Office.Controls.Runtime.renderAll();
            }

            function getListUrl() {
                return Office.Samples.ListViewBasic.appWebUrl +
                        "/_api/web/lists/getbytitle('Announcements')";
            }
        </script>
    </body>
    </html>
    ```

<br/>

> [!NOTE] 
> В приведенном выше примере кода явно указаны URL-адреса хост-сайта и сайта надстройки для инициализации среды выполнения для элементов управления Office. Однако если URL-адреса хост-сайта и сайта надстройки указаны в параметрах строки запроса **SPAppWebUrl** и **SPHostUrl** соответственно, то вы можете передать пустой объект, и код попытается получить параметры автоматически. Параметры **SPAppWebUrl** и **SPHostUrl** включаются в строку запроса при использовании маркера **{StandardTokens}**.
 
<br/>

В следующем примере показано, как передавать пустой объект в метод инициализации.

```
// Initialize with an empty object and the code 
// will attempt to get the tokens from the
// query string directly.
Office.Controls.Runtime.initialize({});
```

<br/>

### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения


1. Нажмите клавишу F5.
    
    > [!NOTE] 
    > При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.

2. Нажмите кнопку **Доверять**.
    
3. Выберите значок надстройки на странице **Содержимое сайта**.
    
Чтобы скачать этот пример из коллекции кода, см. пример кода [Использование экспериментального мини-приложения Desktop List View в надстройке](https://code.msdn.microsoft.com/office/sharepoint-2013-use-the-c3edb076).
 
## <a name="next-steps"></a>Дальнейшие действия

В этой статье показано, как использовать мини-приложение "Представление списка на рабочем столе" в своей надстройке с помощью HTML. Вы также можете ознакомиться со следующими сценариями и сведениями о мини-приложении.

### <a name="use-javascript-to-declare-the-desktop-list-view-widget"></a>Использование JavaScript для объявления мини-приложения Desktop List View

Для объявления мини-приложения можно использовать JavaScript, а не HTML. В этом случае в качестве заполнителя для мини-приложения можно использовать следующую разметку:

```HTML
<div id="ListViewDiv"></div>
```

<br/>

Для создания экземпляра List View используйте следующий код JavaScript:

```js
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: Office.Samples.ListViewBasic.appWebUrl + "/_api/web/lists/getbytitle('Announcements')"
    });
```

<br/>

Пример выполнения задач см. на странице **JSSimple.html** в примере кода [Использование экспериментального мини-приложения "Представление списка на рабочем столе" в надстройке](https://code.msdn.microsoft.com/office/sharepoint-2013-use-the-c3edb076).

### <a name="specify-a-view-to-display-the-data"></a>Указание представления для отображения данных

Мини-приложение List View показывает данные, используя спецификацию представления в списке SharePoint.

Если вы объявляете мини-приложение, используя разметки HTML, вы можете использовать следующий синтаксис для указания представления.

```HTML
<div id="ListViewDiv"
        data-office-control="Office.Controls.ListView"
        data-office-options="{listUrl: 'list URL',
                            viewID: 'GUID'
                            }">
</div> 

```

<br/>

Если вы объявляете мини-приложение, используя JavaScript, используйте следующий синтаксис для указания представления.

```js
new Office.Controls.ListView(
    document.getElementById("ListViewDiv"), {
        listUrl: "list URL",
        viewID: "GUID"
    });
```

<br/>

Вы можете использовать экспериментальную версию мини-приложения Desktop List View для показа данных в списках SharePoint. Мини-приложение показывает данные в режиме только для чтения. Свои идеи и комментарии вы можете оставить на [сайте UserVoice для разработчиков Office](http://officespdev.uservoice.com/).
 

## <a name="see-also"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Использование экспериментального мини-приложения People Picker в надстройках SharePoint](use-the-experimental-people-picker-widget-in-sharepoint-add-ins.md)
-  [Обзор экспериментальных мини-приложений Office для веб-страниц](office-web-widgetsexperimental-overview.md)
-  [Создание компонентов взаимодействия с пользователем в SharePoint](create-ux-components-in-sharepoint.md)
 

