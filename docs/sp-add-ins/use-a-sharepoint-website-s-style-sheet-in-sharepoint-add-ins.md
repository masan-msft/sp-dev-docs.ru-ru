---
title: Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint
description: Добавьте ссылку на таблицу стилей веб-сайта SharePoint в надстройку SharePoint и используйте ее для оформления веб-страниц.
ms.date: 12/14/2017
ms.prod: sharepoint
ms.openlocfilehash: 257a112548de365bd61efa2ee1ca4ae66164ca3b
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="use-a-sharepoint-websites-style-sheet-in-sharepoint-add-ins"></a>Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint

Вы можете ссылаться на таблицу стилей веб-сайта SharePoint в вашей надстройке SharePoint и использовать ее для настройки стиля ваших веб-страниц с помощью таблицы стилей в SharePoint. Кроме того, если кто-либо изменяет таблицу стилей или тему веб-сайта SharePoint, то вы сможете применить новый набор стилей, не меняя ссылку на таблицу стилей в вашей надстройке.
 
> [!IMPORTANT] 
> Если на ваших веб-страницах используется элемент управления хрома или эталонная страница надстройки, стили уже доступны и ссылаться на таблицу стилей вручную, используя инструкции из этой статьи, не требуется. 
 
<a name="SP15Usestylesheetcontrol_Prereq"> </a>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Необходимые условия для использования примеров в этой статье

Вам необходима среда разработки, описанная в разделе [Два типа надстроек SharePoint (с размещением в SharePoint и у поставщика)](sharepoint-add-ins.md#two-types-of-sharepoint-add-ins-sharepoint-hosted-and-provider-hosted).

### <a name="core-concepts-to-know-before-using-the-sharepoint-style-sheet-in-a-sharepoint-add-in"></a>Ключевые понятия, с которыми необходимо ознакомиться перед использованием таблицы стилей SharePoint в надстройке SharePoint

Ниже перечислены полезные статьи, в которых описано, как использовать таблицы стилей SharePoint.

|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins.md)|Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать надстройки — небольшие и удобные в использовании решения для пользователей.|
| [Разработка пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins.md)|Сведения о параметрах и вариантах построения пользовательского интерфейса при создании надстроек SharePoint.|
| [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты необходимо разворачивать на хост-сайте, а какие на сайте надстройки, и как выполнить развертывание сайта надстройки в изолированном домене.|

<a name="SP15Usestylesheetcontrol_Example"> </a>

## <a name="code-example-use-a-sharepoint-websites-style-sheet-in-a-sharepoint-add-in"></a>Пример кода. Использование таблицы стилей веб-сайта SharePoint в надстройке SharePoint

В этом примере кода показано, как использовать таблицу стилей веб-сайта SharePoint. Это позволяет сделать страницы удаленного веб-приложения похожими на страницы хост-сайта SharePoint.

### <a name="to-use-the-style-sheet-in-a-sharepoint-add-in"></a>Использование таблицы стилей в надстройке SharePoint

1. Создайте надстройку SharePoint с размещением у поставщика.

2. Подготовьте сайт надстройки, создав пустую страницу.

3. Добавьте в веб-проект страницу со ссылкой на таблицу стилей.

4. Измените элемент в манифесте надстройки.

На следующем рисунке показана веб-страница SharePoint, на которой используется таблица стилей.

**Веб-страница, на которой используется таблица стилей**

![Веб-страница, на которой используется таблица стилей](../images/StylesheetControl_result.png)
 
<br/>

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a>Создание надстройки SharePoint и удаленных веб-проектов

1. Откройте Visual Studio от имени администратора. (Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.)

2. Создайте надстройку SharePoint с размещением у поставщика, как описано в [этой статье](get-started-creating-provider-hosted-sharepoint-add-ins.md), и назовите ее **StylesheetAdd-in**. 

### <a name="to-force-the-add-in-web-provisioning-by-creating-a-blank-page"></a>Подготовка сайта надстройки путем создания пустой страницы

1. Щелкните правой кнопкой мыши проект Надстройка SharePoint и добавьте новый модуль.
    
2. Щелкните правой кнопкой мыши новый модуль и добавьте новый элемент.

3. В разделе **Элементы Visual C#** > **Интернет** выберите **HTML-страница**. Переименуйте страницу в **blank.html**.

4. Удалите содержимое файла blank.html.

### <a name="to-add-a-webpage-that-references-the-style-sheet-in-the-web-project"></a>Чтобы добавить веб-страницу со ссылками на таблицу стилей в веб-проекте, выполните следующие действия

1. Щелкните правой кнопкой мыши веб-проект и добавьте новую веб-форму. Переименуйте ее в **StyleConsumer.aspx**.

2. Замените содержимое Web Form.aspx следующим кодом, который выполняет перечисленные далее задачи.
    
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

    <br/>

В некоторых случаях, чтобы скачать CSS-файл и изображения для применения стиля, пользователь должен сначала пройти проверку подлинности в SharePoint. Теги link не позволяют пользователю, не вошедшему в систему, пройти аутентификацию автоматически. Загружайте ресурс страницы с сайта надстройки на вашу веб-страницу для принудительной аутентификации перед связыванием с CSS-файлом. В этом примере страница blank.html загружается в невидимом фрейме IFrame.
    
### <a name="to-edit-the-startpage-element-in-the-add-in-manifest"></a>Изменение элемента StartPage в манифесте надстройки

1. Дважды щелкните файл **AppManifest.xml** в **обозревателе решений**.
  
2. В раскрывающемся меню **Начальная страница** выберите веб-страницу, использующую таблицу стилей.
    
### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения

1. Убедитесь, что проект надстройки SharePoint выбран как запускаемый проект.

2. Нажмите клавишу F5.
    
    > [!NOTE] 
    > После нажатия клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.

3. Нажмите кнопку **Доверять**.
    
4. Выберите значок надстройки **StylesheetBasic**.
 
5. На следующем рисунке показана готовая веб-страница, на которой используются стили SharePoint.
    
    **Таблица стилей, используемая на странице**
  
    ![Таблица стилей, используемая на веб-странице](../images/StylesheetControl_result2.png)

6. Вы также можете перейти на хост-сайт и изменить тему. Обновите веб-страницу надстройки, чтобы использовать новые стили.
    
#### <a name="troubleshooting-the-solution"></a>Устранение неполадок в решении

|**Проблема**|**Решение**|
|:-----|:-----|
|Visual Studio не открывает браузер после нажатия клавиши F5.|Установите проект надстройки для SharePoint в качестве запускаемого проекта.|
|Ошибка сертификата.|Задайте для свойства **SSL включен** веб-проекта значение **false**. В проекте надстройки SharePoint задайте для свойства **Веб-проект** значение **None**, а затем снова укажите в нем имя веб-проекта.|

## <a name="see-also"></a>Дополнительные ресурсы
<a name="SP15Usestylesheetcontrol_Addresources"> </a>

- [Пример кода. Использование таблицы стилей SharePoint в надстройке](https://code.msdn.microsoft.com/office/SharePoint-2013-Use-the-7a8684e2/view/Discussions)
- [Создание компонентов взаимодействия с пользователем в SharePoint](create-ux-components-in-sharepoint.md)

 

