# <a name="customize-a-list-view-in-sharepoint-add-ins-using-client-side-rendering"></a>Настройка представления списка в надстройках SharePoint с использованием технологии клиентской обработки
В этой статье рассказывается, как настроить представление списка в надстройке, размещаемой в SharePoint, с использованием технологии клиентской обработки в SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 

В SharePoint технология клиентской обработки позволяет вам создавать собственные выходные данные для набора элементов управления, размещенных на странице SharePoint. Благодаря ей вы можете использовать хорошо известные технологии, например HTML и JavaScript, для задания логики отрисовки представлений списков в SharePoint. Технология клиентской обработки дает вам возможность указывать собственные ресурсы JavaScript и размещать их в хранилищах данных, доступных для ваших надстроек, например в библиотеке документов. Надстройка, размещаемая в SharePoint, включает только компоненты SharePoint. Ресурсы надстройки, размещаемой в SharePoint, хранятся на изолированном дочернем сайте хост-сайта, называемом сайтом надстройки.
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a>Компоненты, необходимые для использования примеров в этой статье
<a name="SP15CSRlistview_Prereq"> </a>

Чтобы выполнить действия, указанные в этом примере, вам потребуются указанные ниже компоненты.
 

 

-  [Visual Studio 2015 и Инструменты разработчика Microsoft Office последней версии](https://www.visualstudio.com/features/office-tools-vs).
    
 
- Среда разработки SharePoint (для локальных сценариев необходимо изолировать надстройку).
    
 
Руководство по настройке среды разработки согласно вашим потребностям см. в статье о том, как [приступить к созданию надстроек Office и SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).
 

 

### <a name="core-concepts-to-help-you-understand-list-view-customization-with-client-side-rendering"></a>Основные понятия, упрощающие понимание процесса настройки представления списка с использованием технологии клиентской обработки

В таблице ниже перечислены полезные статьи, с помощью которых вам будет проще изучить основные понятия, используемые для настройки представлений списков.
 

 

**Табл. 1. Основные понятия для настройки представлений списков в надстройке**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Надстройки SharePoint](sharepoint-add-ins)|Изучите новую модель надстроек в Microsoft SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.|
| [Разработка пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins)|Изучите различные варианты пользовательского интерфейса, доступные при создании надстроек SharePoint.|
| [Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint-2013)|Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты разворачиваются на хост-сайте, какие компоненты разворачиваются на сайте надстройки, и как выполняется развертывание сайта надстройки в изолированном домене.|

## <a name="code-example-customize-a-list-view-by-using-client-side-rendering"></a>Пример кода: настройка представления списка с использованием технологии клиентской обработки
<a name="SP15CSRlistview_Codeexample"> </a>

Чтобы настроить представление списка, развернутое на сайте надстройки, с помощью технологии клиентской обработки, выполните указанные ниже действия.
 

 

1. Создайте проект надстройки для SharePoint.
    
 
2. Создайте новое определение списка с настраиваемым представлением.
    
 
3. Создайте настраиваемую логику обработки в файле JavaScript.
    
 
На рис. 1 показано представление списка объявлений, отрисованное с помощью технологии клиентской обработки.
 

 

**Рис. 1. Настраиваемое представление списка объявлений**

 

 
![Настраиваемое представление списка объявлений](../../images/CSRListView_result.png)
 

### <a name="to-create-the-sharepoint-add-in-project"></a>Создание проекта надстройки SharePoint


1. Запустите Visual Studio 2015 от имени администратора. (Для этого щелкните правой копкой мыши значок **Visual Studio** в меню **Пуск** и выберите пункт **Запуск от имени администратора**.)
    
 
2. Создайте проект с использованием шаблона **Надстройка SharePoint**.
    
    На рис. 2 показано расположение шаблона **Надстройка SharePoint** в Visual Studio 2015: **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки Office**.
    

    **Рис. 2. Шаблон Visual Studio "Надстройка SharePoint"**

 

  ![Шаблон Visual Studio "Надстройка SharePoint"](../../images/AppForSharePointVSTemplate.PNG)
 

 

 
3. Укажите URL-адрес веб-сайта SharePoint, который вы хотите использовать для отладки.
    
 
4. В качестве варианта размещения надстройки выберите пункт **Размещение в SharePoint**.
    
 

### <a name="to-create-a-new-list-definition"></a>Создание определения списка


1. Щелкните правой кнопкой мыши проект надстройки SharePoint и добавьте новый элемент **Список**. Создайте настраиваемый список на основе объявлений.
    
 
2. Скопируйте указанную ниже разметку и вставьте ее в элемент **Views** в файле Schema.xml вашего компонента списка. Эта разметка выполняет перечисленные ниже задачи.
    
      - Объявляет новое представление с именем Overridable и атрибутом BaseViewID=2.
    
 
  - Предоставляет значение для элемента **JSLink**, которое указывает на файл JavaScript, подготовленный вместе с надстройкой.
    
     **Примечание.** Свойство JSLink не поддерживается в списках Survey или Events. Календарь SharePoint представляет собой список Events.

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


### <a name="to-provide-the-custom-rendering-logic-in-a-javascript-file"></a>Создание настраиваемой логики отрисовки в файле JavaScript


1. Щелкните правой кнопкой мыши папку **Scripts** и добавьте новый файл JavaScript. Присвойте этому файлу имя fileCSRListView.js.
    
 
2. Скопируйте указанный ниже код и вставьте его в файл CSRListView.js. Этот код выполняет указанные ниже задачи.
    
      - Предоставляет обработчики событий для событий **PreRender** и **PostRender**.
    
 
  - Предоставляет шаблоны для наборов шаблонов Header, Footer и Item.
    
 
  - Регистрирует шаблоны.
    
 

```
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


### <a name="to-build-and-run-the-solution"></a>Построение и запуск решения


1. Нажмите клавишу F5.
    
     **Примечание.** Когда вы нажимаете клавишу F5, Visual Studio создает решение, развертывает надстройку и открывает страницу разрешений для надстройки.
2. Нажмите кнопку **Доверять**.
    
 
3. Перейдите в свой настраиваемый список, введя адрес _/Lists/<экземпляр_вашего_списка>_, относительный для каталога вашей надстройки в домене сайта надстройки (а не в домене хост-сайта). Добавьте одно или несколько объявлений. На ленте выберите представление **Переопределяемый**.
    
 

## <a name="next-steps"></a>Дальнейшие действия
<a name="SP15CSRlistview_Nextsteps"> </a>

В этой статье демонстрируется настройка представления списка в надстройке для SharePoint с использованием обработки на стороне клиента. Далее вы можете изучить другие компоненты взаимодействия с пользователем, доступные в надстройках для SharePoint. Дополнительные сведения можно найти в следующих источниках.
 

 

-  [Пример кода: настройка представления списка в надстройке с использованием технологии клиентской обработки](http://code.msdn.microsoft.com/SharePoint-2013-Customize-61761017)
    
 
-  [Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins)
    
 
-  [Использование клиентского элемента управления хрома в надстройках SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins)
    
 
-  [Создание дополнительных действий для развертывания с надстройками SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins)
    
 
-  [Создание веб-частей надстроек для установки вместе с надстройкой SharePoint](create-add-in-parts-to-install-with-your-sharepoint-add-in)
    
 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15CSRlistview_AddResources"> </a>


-  [Настройка локальной среды разработки для надстроек SharePoint](set-up-an-on-premises-development-environment-for-sharepoint-add-ins)
    
 
-  [Разработка пользовательского интерфейса для надстроек SharePoint](ux-design-for-sharepoint-add-ins)
    
 
-  [Создание компонентов пользовательского интерфейса в SharePoint](create-ux-components-in-sharepoint-2013)
    
 
-  [Что следует рассмотреть, прежде чем приступать к разработке надстроек SharePoint](three-ways-to-think-about-design-options-for-sharepoint-add-ins)
    
 
-  [Важные аспекты разработки и архитектуры для надстроек SharePoint](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscape)
    
 

