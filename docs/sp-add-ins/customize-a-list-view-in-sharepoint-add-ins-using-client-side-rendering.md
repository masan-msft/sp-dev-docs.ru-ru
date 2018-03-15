---
title: "Настройка представления списка в надстройках SharePoint с использованием клиентской обработки"
description: "Настройте представление списка в надстройке с размещением в SharePoint, используя технологию клиентской обработки в SharePoint."
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 1496cc0b2715a692cb091a4282716590d36071a9
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="customize-a-list-view-in-sharepoint-add-ins-using-client-side-rendering"></a>Настройка представления списка в надстройках SharePoint с использованием технологии клиентской обработки

Технология клиентской обработки в SharePoint позволяет создавать собственные выходные данные для набора элементов управления, размещенных на странице SharePoint. Благодаря этому можно использовать хорошо известные технологии, например HTML и JavaScript, для задания логики отрисовки представлений списков в SharePoint. Технология клиентской обработки дает возможность указывать собственные ресурсы JavaScript и размещать их в хранилищах данных, доступных ваших надстроек (например, в библиотеке документов). Надстройка с размещением в SharePoint включает только компоненты SharePoint. Ресурсы надстройки с размещением в SharePoint хранятся на изолированном дочернем сайте хост-сайта, называемом сайтом надстройки.

<a name="SP15CSRlistview_Prereq"> </a>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Что необходимо для использования примеров в этой статье

Для выполнения действий, описанных в этом примере, вам потребуется следующее:

-  [Visual Studio 2015 и Инструменты разработчика Microsoft Office последней версии](https://www.visualstudio.com/vs/office-tools/).

- Среда разработки SharePoint (для локальных сценариев необходимо изолировать надстройку).

Инструкции по настройке подходящей среды разработки см. в статье [Два типа надстроек SharePoint (с размещением в SharePoint и у поставщика)](sharepoint-add-ins.md#two-types-of-sharepoint-add-ins-sharepoint-hosted-and-provider-hosted).

### <a name="core-concepts-to-help-you-understand-list-view-customization-with-client-side-rendering"></a>Основные понятия, связанные с настройкой представления списка с использованием технологии клиентской обработки

В приведенной ниже таблице перечислены полезные статьи, в которых описаны понятия, связанные с настройкой представления списка.

|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins.md)|Изучите новую модель надстроек в Microsoft SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.|
| [Разработка пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins.md)|Изучите различные варианты пользовательского интерфейса, доступные при создании надстроек SharePoint.|
| [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты необходимо разворачивать на хост-сайте, а какие на сайте надстройки, и как выполнить развертывание сайта надстройки в изолированном домене.|

<a name="SP15CSRlistview_Codeexample"> </a>

## <a name="code-example-customize-a-list-view-by-using-client-side-rendering"></a>Пример кода: настройка представления списка с использованием технологии клиентской обработки

Чтобы настроить представление списка, развернутое на сайте надстройки, используя технологию клиентской обработки, выполните указанные ниже действия.

1. Создайте проект надстройки SharePoint.

2. Создайте новое определение списка с настраиваемым представлением.

3. Укажите особую логику обработки в файле JavaScript.

Ниже показано представление списка объявлений, отрисованное с помощью технологии клиентской обработки.

**Особое представление списка объявлений**

![Особое представление списка объявлений](../images/CSRListView_result.png)

### <a name="to-create-the-sharepoint-add-in-project"></a>Создание проекта надстройки SharePoint

1. Откройте Visual Studio 2015 от имени администратора. Для этого щелкните правой кнопкой мыши значок **Visual Studio** в меню **Пуск** и выберите **Запуск от имени администратора**.

2. Создайте новый проект с помощью шаблона **Надстройка SharePoint**.
    
   Ниже показано расположение шаблона **Надстройка SharePoint** в Visual Studio 2015: **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки Office**.
    
   **Шаблон Visual Studio "Надстройка SharePoint"**

   ![Шаблон Visual Studio "Надстройка SharePoint"](../images/AppForSharePointVSTemplate.PNG)

3. Укажите URL-адрес веб-сайта SharePoint, который планируется использовать для отладки.
    
4. Выберите **SharePoint-hosted** (Размещение в SharePoint) в качестве варианта размещения надстройки.

### <a name="to-create-a-new-list-definition"></a>Создание определения списка

1. Щелкните правой кнопкой мыши проект надстройки для SharePoint и добавьте новый элемент **List**. Создайте настраиваемый список на основе объявлений.

2. Скопируйте следующую разметку и вставьте ее в элемент **Views** файла Schema.xml вашего компонента списка. Эта разметка выполняет следующие задачи.
    
    - Объявляет новое представление с именем Overridable и атрибутом BaseViewID=2.

    - Предоставляет значение для элемента **JSLink**, которое указывает на файл JavaScript с надстройкой.
    
    > [!NOTE] 
    > Свойство JSLink не поддерживается в списках "Survey" (Опрос) и "Events" (События). Календарь SharePoint представляет собой список "Events" (События).

    ```XML
    <View BaseViewID="2" 
        Name="8d2719f3-c3c3-415b-989d-33840d8e2ddb" 
        DisplayName="Overridable" 
        Type="HTML" 
        WebPartZoneID="Main" 
        SetupPath="pages\viewpage.aspx" 
        Url="Overridable.aspx"
        DefaultView="TRUE">
    <ViewFields>
        <FieldRef Name="Title" />
    </ViewFields>
    <Query />
    <Toolbar Type="Standard" />
    <XslLink>main.xsl</XslLink>
    <JSLink Default="TRUE">~site/Scripts/CSRListView.js</JSLink>
    </View>
    ```

<br/>

### <a name="to-provide-the-custom-rendering-logic-in-a-javascript-file"></a>Указание особой логики отрисовки в файле JavaScript

1. Щелкните правой кнопкой мыши папку **Scripts** и добавьте новый файл JavaScript. Назовите его **CSRListView.js**.

2. Скопируйте указанный ниже код и вставьте его в файл CSRListView.js. Этот код выполняет следующие задачи:
    
    - Предоставляет обработчики событий для событий **PreRender** и **PostRender**.

    - Предоставляет шаблоны для наборов шаблонов Header, Footer и Item.

    - Регистрирует шаблоны.

    ```js
    
    (function () {
        // Initialize the variable that stores the objects.
        var overrideCtx = {};
        overrideCtx.Templates = {};

        // Assign functions or plain html strings to the templateset objects:
        // header, footer and item.
        overrideCtx.Templates.Header = "<B><#=ctx.ListTitle#></B>" +
            "<hr><ul id='unorderedlist'>";

        // This template is assigned to the CustomItem function.
        overrideCtx.Templates.Item = customItem;
        overrideCtx.Templates.Footer = "</ul>";

        // Set the template to the:
        //  Custom list definition ID
        //  Base view ID
        overrideCtx.BaseViewID = 2;
        overrideCtx.ListTemplateType = 10057;

        // Assign a function to handle the
        // PreRender and PostRender events
        overrideCtx.OnPreRender = preRenderHandler;
        overrideCtx.OnPostRender = postRenderHandler;

        // Register the template overrides.
        SPClientTemplates.TemplateManager.RegisterTemplateOverrides(overrideCtx);
    })();

    // This function builds the output for the item template.
    // It uses the context object to access announcement data.
    function customItem(ctx) {

        // Build a listitem entry for every announcement in the list.
        var ret = "<li>" + ctx.CurrentItem.Title + "</li>";
        return ret;
    }

    // The preRenderHandler attends the OnPreRender event
    function preRenderHandler(ctx) {

        // Override the default title with user input.
        ctx.ListTitle = prompt("Type a title", ctx.ListTitle);
    }

    // The postRenderHandler attends the OnPostRender event
    function postRenderHandler(ctx) {

        // You can manipulate the DOM in the postRender event
        var ulObj;
        var i, j;

        ulObj = document.getElementById("unorderedlist");
        
        // Reverse order the list.
        for (i = 1; i < ulObj.children.length; i++) {
            var x = ulObj.children[i];
            for (j = 1; j < ulObj.children.length; j++) {
                var y = ulObj.children[j];
                if(x.innerText<y.innerText){                  
                    ulObj.insertBefore(y, x);
                }
            }
        }
    }
    ```

<br/>

### <a name="to-build-and-run-the-solution"></a>Сборка и запуск решения

1. Нажмите клавишу F5.
    
    > [!NOTE] 
    > При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.

2. Нажмите кнопку **Доверять**.   
 
3. Перейдите к своему настраиваемому списку, введя адрес _/Lists/<экземпляр_вашего_списка>_, относительный для каталога вашей надстройки в домене сайта надстройки (а не в домене хост-сайта). Добавьте одно или несколько объявлений. На ленте выберите представление **Переопределяемый**.
    
## <a name="see-also"></a>См. также
<a name="SP15CSRlistview_AddResources"> </a>

-  [Пример кода: настройка представления списка в надстройке с помощью технологии клиентской обработки](https://code.msdn.microsoft.com/office/SharePoint-2013-Customize-61761017)
-  [Создание компонентов взаимодействия с пользователем в SharePoint](create-ux-components-in-sharepoint.md)
