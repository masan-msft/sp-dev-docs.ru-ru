---
title: "Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 10a440ad261191df975cae695cffa5d6261a65a5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="use-a-sharepoint-websites-style-sheet-in-sharepoint-add-ins"></a>Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint
Узнайте, как использовать таблицы стилей веб-сайта SharePoint в надстройке SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Вы можете ссылаться на таблицу стилей веб-сайта SharePoint в вашей надстройке SharePoint и использовать ее для настройки стиля ваших веб-страниц с помощью таблицы стилей в SharePoint. Кроме того, если кто-либо изменяет таблицу стилей или тему веб-сайта SharePoint, то вы сможете применить новый набор стилей, не меняя ссылку на таблицу стилей в вашей надстройке.
 

 **Важно!** Если на ваших веб-страницах используется элемент управления хрома или эталонная страница надстройки, то стили уже доступны для использования, и ссылаться на таблицу стилей вручную, используя инструкции из этой статьи, не требуется. 
 


## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье
<a name="SP15Usestylesheetcontrol_Prereq"> </a>

Вам необходима среда разработки, описанная в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).
 

 

### <a name="core-concepts-to-know-before-using-the-sharepoint-style-sheet-in-a-sharepoint-add-in"></a>Основные понятия, связанные с использованием таблицы стилей SharePoint в надстройке SharePoint

В приведенной ниже таблице перечислены полезные статьи с описанием основных понятий, связанных с использованием таблиц стилей SharePoint.
 

 

**Таблица 1. Основные понятия, связанные с использованием таблиц стилей**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins.md)|Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать надстройки — небольшие и удобные в использовании решения для пользователей.|
| [Разработка пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins.md)|Сведения о параметрах и вариантах построения пользовательского интерфейса при создании надстроек SharePoint.|
| [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|Узнайте, в чем разница между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включить в Надстройка SharePoint, какие компоненты можно развернуть на хост-сайтах, а какие на сайтах надстроек, а также узнайте, как развертывать сайты надстроек в изолированном домене.|

## <a name="code-example-use-a-sharepoint-websites-style-sheet-in-a-sharepoint-add-in"></a>Пример кода. Использование таблицы стилей веб-сайта SharePoint в надстройке SharePoint
<a name="SP15Usestylesheetcontrol_Example"> </a>

В этом примере кода показано, как использовать таблицу стилей веб-сайта SharePoint. Это позволит сделать страницы удаленного веб-приложения похожими на страницы хост-сайта SharePoint.
 

 
Чтобы применить таблицу стилей в надстройке SharePoint, сделайте следующее:
 

 

1. Создайте надстройку SharePoint с размещением у поставщика. 
    
 
2. Подготовьте сайт надстройки, создав пустую страницу.
    
 
3. Добавьте в веб-проект страницу со ссылкой на таблицу стилей.
    
 
4. Измените элемент в манифесте надстройки.
    
 
На рис. 1 показана веб-страница SharePoint с использованием таблицы стилей.
 

 

**Рис. 1. Веб-страница с использованием таблицы стилей**

 

 
![Веб-страница с использованием элемента управления "Таблица стилей"](../images/StylesheetControl_result.png)
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a>Создание надстройки SharePoint и удаленных веб-проектов


1. Откройте Visual Studio от имени администратора. Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите пункт **Запуск от имени администратора**.
    
 
2. Создайте надстройку SharePoint с размещением у поставщика, как описано в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md), и задайте для нее имя itStylesheetAdd-in. 
    
 

### <a name="to-force-the-add-in-web-provisioning-by-creating-a-blank-page"></a>Подготовка сайта надстройки путем создания пустой страницы


1. Щелкните правой кнопкой мыши проект Надстройка SharePoint и добавьте новый модуль.
    
 
2. Щелкните правой кнопкой мыши новый модуль и добавьте новый элемент.
    
 
3. В разделе **Элементы Visual C#** > **Интернет** выберите пункт **HTML-страница**. Переименуйте страницу в **blank.html**.
    
 
4. Удалите содержимое файла blank.html.
    
 

### <a name="to-add-a-webpage-that-references-the-style-sheet-in-the-web-project"></a>Добавление веб-страницы, ссылающейся на таблицу стилей в веб-проекте


1. Щелкните веб-проект правой кнопкой мыши и добавьте новую веб-форму. Переименуйте ее в **StyleConsumer.aspx**.
    
 
2. Замените содержимое Web Form.aspx на приведенный ниже код, который выполняет перечисленные далее задачи.
    
      - Загружает страницу blank.html с сайта надстройки в невидимом фрейме IFrame.
    
 
  - Загружает файл defaultcss.ashx с сайта надстройки.
    
 
  - Использует доступные стили.
    
 

```
  <%@ Page Language="C#" AutoEventWireup="true" CodeBehind="StyleConsumer.aspx.cs" Inherits="StylesheetAppWeb.StyleConsumer" %>

<!DOCTYPE html>
<html>
<head>
    <title>Add-in using stylesheet</title>
</head>
<body>

    <!-- The main page title -->
    <h1 class="ms-core-pageTitle">Stylesheet add-in</h1>

    <!-- Some subtitle -->
    <h1 class="ms-accentText">For people</h1>

    <!-- Subtitle comments -->
    <h2 class="ms-accentText">who care about the style in their add-ins</h2>
    <p></p>
    <div>
        <h2 class="ms-webpart-titleText">Get started with style in your add-in... </h2>
        <a class="ms-commandLink" href="#">some command</a>
        <br />
        This sample shows you how to use some of the classes defined in the SharePoint website's style sheet.
    </div>

    <!-- Script to load SharePoint resources
        and load the blank.html page in
        the invisible iframe
        -->
    <script type="text/javascript">
        "use strict";
        var appweburl;

        (function () {
            var ctag;

            // Get the URI decoded add-in web URL.
            appweburl =
                decodeURIComponent(
                    getQueryStringParameter("SPAppWebUrl")
            );
            // Get the ctag from the SPClientTag token.
            ctag =
                decodeURIComponent(
                    getQueryStringParameter("SPClientTag")
            );

            // The resource files are in a URL in the form:
            // web_url/_layouts/15/Resource.ashx
            var scriptbase = appweburl + "/_layouts/15/";

            // Dynamically create the invisible iframe.
            var blankiframe;
            var blankurl;
            var body;
            blankurl = appweburl + "/Pages/blank.html";
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
            dclink.setAttribute("href", scriptbase + "defaultcss.ashx?ctag=" + ctag);
            head = document.getElementsByTagName("head");
            head[0].appendChild(dclink);
        })();

        // Function to retrieve a query string value.
        // For production purposes you may want to use
        //  a library to handle the query string.
        function getQueryStringParameter(paramToRetrieve) {
            var params;
            var strParams;

            params = document.URL.split("?")[1].split("&amp;");
            strParams = "";
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


    In some cases, the user has to be authenticated to SharePoint before your page will be able to download the CSS and images for styling. Link tags do not automatically authenticate a user who is not already signed in. Consider loading a page resource from the add-in web in your webpage to force the user's authentication before linking to the CSS file. In this example, the blank.html page is loaded in an invisible IFrame.
    
 

### <a name="to-edit-the-startpage-element-in-the-add-in-manifest"></a>Изменение элемента StartPage в манифесте надстройки


1. Дважды щелкните файл **AppManifest.xml** в **обозревателе решений**.
    
 
2. В раскрывающемся меню **Начальная страница** выберите веб-страницу, использующую таблицу стилей.
    
 

### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения


1. Убедитесь, что проект Надстройка SharePoint выбран как запускаемый проект.
    
 
2. Нажмите клавишу F5.
    
     **Примечание.** При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.
3. Нажмите кнопку **Доверять**.
    
 
4. Щелкните значок надстройки **StylesheetBasic**.
    
 
5. На рис. 2 показана готовая веб-страница, использующая стили SharePoint.
    
    **Рис. 2. Таблица стилей, используемая на странице**

 

  ![Элемент управления "Таблица стилей", используемый на веб-странице](../images/StylesheetControl_result2.png)
 

 

 
6. Вы также можете перейти на хост-сайт и изменить тему. Затем обновите веб-страницу надстройки, чтобы использовать новые стили.
    
 

**Таблица 2. Устранение неполадок в решении**


|**Проблема**|**Решение**|
|:-----|:-----|
|Visual Studio не открывает браузер после нажатия клавиши F5.|Установите проект Надстройка SharePoint в качестве запускаемого.|
|Ошибка сертификата.|Задайте для свойства **SSL включен** веб-проекта значение false. В проекте надстройки SharePoint задайте для свойства **Веб-проект** значение None, а затем снова укажите в нем имя веб-проекта.|

## <a name="next-steps"></a>Дальнейшие действия
<a name="SP15Usestylesheetcontrol_Nextsteps"> </a>

В этой статье показано, как использовать таблицу стилей в надстройке SharePoint. Далее вы можете узнать о других компонентах UX, доступных для надстроек SharePoint. Дополнительные сведения см. в следующих источниках:
 

 

-  [Пример кода. Использование таблицы стилей SharePoint в надстройке](http://code.msdn.microsoft.com/SharePoint-Use-the-7a8684e2)
    
 
-  [Использование клиентского элемента управления хрома в надстройках SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md)
    
 
-  [Создание дополнительных действий для развертывания с надстройками SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md)
    
 
-  [Создание веб-частей надстроек для установки вместе с надстройкой SharePoint](create-add-in-parts-to-install-with-your-sharepoint-add-in.md)
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15Usestylesheetcontrol_Addresources"> </a>


-  [Разработка пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins.md)
    
 
-  [Рекомендации по проектированию пользовательского интерфейса надстроек SharePoint](sharepoint-add-ins-ux-design-guidelines.md)
    
 
-  [Создание компонентов пользовательского интерфейса в SharePoint](create-ux-components-in-sharepoint.md)
    
 
-  [Что следует рассмотреть, прежде чем приступать к разработке надстроек SharePoint](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md)
    
 
-  [Важные аспекты разработки и архитектуры для надстроек SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 

