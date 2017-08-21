# <a name="add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="3a2d8-101">Добавление пользовательского кода клиентской обработки к надстройке SharePoint, размещенной в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-101">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>
<span data-ttu-id="3a2d8-102">Узнайте, как настраивать отрисовку и проверку элементов управления на страницах надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-102">Customize the rendering and validation of controls in  spappplural pages.</span></span>
 
<span data-ttu-id="3a2d8-p101">**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p101">The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint#bk_newname).</span></span>
 
<span data-ttu-id="3a2d8-p102">Эта восьмая часть серии статей, посвященной основам разработки надстроек, размещаемых в SharePoint. Для начала следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии:</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p102">Customize the rendering and validation of controls in SharePoint Add-ins pages. This is the eighth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins) and the previous articles in this series:</span></span>
 
-  [<span data-ttu-id="3a2d8-108">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-108">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
-  [<span data-ttu-id="3a2d8-109">Развертывание и установка размещаемых в SharePoint надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-109">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
-  [<span data-ttu-id="3a2d8-110">Добавление настраиваемых столбцов в надстройки, размещенные в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-110">Add custom columns to a SharePoint-hostedSharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
-  [<span data-ttu-id="3a2d8-111">Добавление настраиваемого типа контента в надстройки, размещенные в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-111">Add a custom content type to a SharePoint-hostedSharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
-  [<span data-ttu-id="3a2d8-112">Добавление веб-части на страницу в надстройке, размещенной в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-112">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
-  [<span data-ttu-id="3a2d8-113">Добавление рабочего процесса к надстройке, размещенной в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-113">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
-  [<span data-ttu-id="3a2d8-114">Добавление настраиваемых страниц и стилей в надстройки, размещенные в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a2d8-114">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in)

<span data-ttu-id="3a2d8-p103">**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeClientRenderedControl.sln.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p103">**Note** If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeClientRenderedControl.sln file.</span></span>
 
<span data-ttu-id="3a2d8-p104">Используя немного клиентского кода JavaScript, вы можете настраивать отрисовку веб-частей, большинства типов полей (столбцов) и других элементов управления, назначив файл JavaScript свойству **JSLink** элемента управления, например **SPField.JSLink**. Таким способом вы также можете добавлять логику проверки на стороне клиента. В этой статье рассматривается настройка отрисовки поля в списке из надстройки SharePoint "Employee Orientation" (Обучение сотрудников) с помощью клиентской обработки.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p104">You can use a little client-side JavaScript to customize the rendering of Web Parts, most types of fields (columns), and some other controls, by assigning a JavaScript file to the **JSLink** property of the control, such as **SPField.JSLink**. You can also add client-side validation logic in this way. In this article you customize the rendering of a field in a list of the Employee Orientation SharePoint Add-in by using client-side rendering.</span></span>
 
 <span data-ttu-id="3a2d8-120">**Примечание.** Если в браузере пользователя отключен JavaScript, то SharePoint будет использовать серверные функции отрисовки и проверки.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-120">**Note** If the end-user has JavaScript disabled in their browser, SharePoint will fall back to server-side rendering and validation.</span></span>
 
 <span data-ttu-id="3a2d8-p105">**Примечание.** Свойство JSLink не поддерживается в списках Survey и Events. Календарь SharePoint представляет собой список Events.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p105">**Note** The JSLink property is not supported on Survey or Events lists. A SharePoint calendar is an Events list.</span></span>
 
## <a name="create-and-register-the-javascript"></a><span data-ttu-id="3a2d8-123">Создание и регистрация файлов JavaScript</span><span class="sxs-lookup"><span data-stu-id="3a2d8-123">Create and register the JavaScript</span></span>

- <span data-ttu-id="3a2d8-124">В **обозревателе решений** щелкните правой кнопкой мыши узел **Скрипты** и выберите **Добавить** > **Новый элемент** > **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-124">In  **Solution Explorer**, right-click the  **Scripts** node and choose **Add** > **New Item** > **Web**.</span></span>
- <span data-ttu-id="3a2d8-125">Выберите **Файл JavaScript** и задайте для него имя OrientationStageRendering.js.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-125">Choose **JavaScript File** and name itOrientationStageRendering.js.</span></span>
- <span data-ttu-id="3a2d8-126">Настраиваемая отрисовка поля должна выполняться автоматически, поэтому добавьте в JavaScript анонимный метод, который будет автоматически запускаться при загрузке файла с указанным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-126">Your custom rendering of the field should happen automatically, so add an anonymous method to the JavaScript that runs automatically when the file loads with the following code.</span></span>

```
  (function () {

})();
```

- <span data-ttu-id="3a2d8-127">В тексте этого метода (т. е. между символами { и }) добавьте указанный ниже код, чтобы создать объекты JSON (нотации объектов Javascript) для отрисовки контекста переопределения, шаблонов в контексте и шаблонов для полей.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-127">In the body fo this method (between the { } characters), add the following code to create JSON (Javascript Object Notation) objects for the rendering override context, the templates in the context, and the templates for the fields.</span></span>
    
```
  var customRenderingOverride = {};
customRenderingOverride.Templates = {};
customRenderingOverride.Templates.Fields = {

}
```

- <span data-ttu-id="3a2d8-p106">В тексте объекта шаблона  `Fields` добавьте указанный ниже JSON. Имя свойства `OrientationStage` идентифицирует поле, настроившее отрисовку. Значением свойства является другой объект JSON. Свойство `View` идентифицирует контекст страницы, в котором применяется настраиваемая отрисовка. В данном случае объект сообщает SharePoint, что необходимо использовать настраиваемую отрисовку представлений списков. (Другие параметры будут использоваться для форм изменения, создания и отображения.) Значение свойства ( `renderOrientationStage`) это имя метода настраиваемой отрисовки, который вы создадите на одном из следующих этапов.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p106">In the body of the  `Fields` template object, add the following JSON. The property name `OrientationStage` identifies the field that has customized rendering. The value of the property is another JSON object. The `View` property identifies the page context in which the custom rendering is applied. In this case, the object is telling SharePoint to use the customized rendering on list views. (Other options would be for the Edit, New, and Display forms.) The value of the property, `renderOrientationStage`, is the name of the custom rendering method which you create in a later step.</span></span>
    
```
  "OrientationStage": { "View": renderOrientationStage }
```

- <span data-ttu-id="3a2d8-p107">Последнее, что должен сделать анонимный метод, сообщить диспетчеру шаблонов SharePoint о переопределении отрисовки. Добавьте указанную ниже строку в конец раздела body метода.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p107">The last thing that the anonymous method must do is tell SharePoint's template manager about the rendering override. Add the following line to the end of the body of the method.</span></span>
    
```
  SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
```

   <span data-ttu-id="3a2d8-136">Теперь метод должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="3a2d8-136">The method should now look like the following.</span></span>
    
```
  (function () {
    var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = {
        "OrientationStage": { "View": renderOrientationStage }
    }

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
})();
```

- <span data-ttu-id="3a2d8-p108">Добавьте указанный ниже метод в файл. Он задает для значения столбца **Orientation Stage** (Этап вводного обучения) красный цвет, если оно равно Not Started (Не начат), или зеленый, если задано значение Completed (Завершен). (`ctx` — это объект контекста клиента, объявленный во встроенном сценарии SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p108">Add the following method to the file. It sets the color of the **Orientation Stage** column value to red when the value is "Not Started" and to green when the value is "Completed". (The `ctx` object is a client context object that is declared by in-the-box SharePoint script.)</span></span>
    
```
  function renderOrientationStage(ctx) {
    var orientationStageValue = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];
    if (orientationStageValue == "Not Started")  {
        return "<span style='color:red'>" + orientationStageValue + "</span>"
    }
    else if (orientationStageValue == "Completed") {
        return "<span style='color:green'>" + orientationStageValue + "</span>"
    }
    else {
        return orientationStageValue;
    }
}
```

- <span data-ttu-id="3a2d8-140">В **обозревателе решений** разверните узел **Столбцы сайта**, а затем — **OrientationStage**. После этого откройте файл elements.xml.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-140">In **Solution Explorer**, expand **Site Columns** and then **OrientationStage**; and then open the elements.xml file.</span></span> 
- <span data-ttu-id="3a2d8-141">Чтобы сообщить SharePoint, что необходимо использовать специальный код JavaScript, добавьте новый атрибут **JSLink** в элемент **Field**, а затем в качестве его значения назначьте следующий URL-адрес: `~site/Scripts/OrientationStageRendering.js`.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-141">To tell SharePoint to use your custom JavaScript, add a new attribute, **JSLink**, to the **Field** element, and then assign the following URL as its value: `~site/Scripts/OrientationStageRendering.js`.</span></span>
    
<span data-ttu-id="3a2d8-p109">**Примечание.** Свойство **JSLink** всегда представляет собой файл, а не метод. Невозможно указать среде SharePoint, какой метод выполнять. По этой причине файл содержит метод, который запускается автоматически.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p109">**Note** The **JSLink** property is always a file, not a method. There's no way to tell SharePoint which method to run. That is why the file contains a method that runs automatically.</span></span>

<span data-ttu-id="3a2d8-145">Теперь открывающий тег элемента **Field** должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="3a2d8-145">The start tag for the **Field** element will now look like the following.</span></span>
    
```
  <Field
       ID="{some_guid_here}"
       Name="OrientationStage"
       Title="OrientationStage"
       DisplayName="Orientation Stage"
       Description="The current orientation stage of the employee."
       Type="Choice"
       Required="TRUE"
       Group="Employee Orientation" 
       JSLink="~site/Scripts/OrientationStageRendering.js">
<!-- child elements and end tag omitted -->
```

- <span data-ttu-id="3a2d8-146">Откройте страницу Default.aspx и добавьте приведенный ниже код в качестве последнего дочернего элемента для элемента **asp:Content**, где для свойства **ContentPlaceHolderID** задано значение **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-146">Open the Default.aspx page and add the following code as the last child of the **asp:Content** element that has **ContentPlaceHolderID** set to **PlaceHolderMain**.</span></span> 
    
```XML
  <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
    Text="List View Page for New Employees in Seattle" /></p>

```

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="3a2d8-147">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="3a2d8-147">Run and test the add-in</span></span>

- <span data-ttu-id="3a2d8-p110">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p110">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
 
- <span data-ttu-id="3a2d8-p111">Настроенная нами клиентская обработка влияет на отрисовку поля только на странице представления списка, а не в веб-части представления списка, размещенной на домашней странице. Это вызвано тем, что по умолчанию веб-часть использует клиентскую обработку. Существует способы изменить это, но они слишком сложны для нашего простого примера. Следовательно, чтобы увидеть клиентскую обработку в действии, перейдите по ссылке в конце страницы **List View Page for New Employees in Seattle** (Страница представления списка новых сотрудников в Сиэтле).</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p111">The client-side rendering that you have configured affects the rendering of the field only on the list view page, not in the list view Web Part that we put on the home page. This is because the Web Part defaults to server-side rendering. There are ways to reverse this, but they are too advanced for this simple example. So, to see the client-side rendering in action, click the link at the bottom of the page **List View Page for New Employees in Seattle**.</span></span>
 
- <span data-ttu-id="3a2d8-154">Чтобы посмотреть, как работает настраиваемая отрисовка цвета, когда откроется страница представления списка, для некоторых элементов присвойте полю **Orientation Stage** (Этап вводного обучения) значение **Not Started** (Не начат), а для других — значение **Completed** (Завершен).</span><span class="sxs-lookup"><span data-stu-id="3a2d8-154">When the list view page opens, set the **Orientation Stage** value for some items to **Not Started** and set others to **Completed** to see the custom color rendering.</span></span>
    
<span data-ttu-id="3a2d8-155">**Список с настраиваемой клиентской обработкой**</span><span class="sxs-lookup"><span data-stu-id="3a2d8-155">**List with custom client-side rendering**</span></span>

![Список новых сотрудников в Сиэтле, где в столбце "Этап адаптации" значения "Не начато" отмечены красным цветом, а значения "Завершено" — зеленым. Другие значения отмечены черным цветом.](../../images/dc8e2b7d-1747-4b65-aab4-6fc93c6867d4.PNG)
  
- <span data-ttu-id="3a2d8-p113">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p113">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
- <span data-ttu-id="3a2d8-p114">Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуем отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-p114">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in **Solution Explorer** and choose **Retract**.</span></span>

## 
<span data-ttu-id="3a2d8-162"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="3a2d8-162"></span></span>

<span data-ttu-id="3a2d8-163">В статье  [Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in) этой серии вы добавите настраиваемый элемент меню и настраиваемую кнопку на ленту в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a2d8-163">In the next article in this series, you'll add a custom menu item and custom button to the ribbon in the SharePoint Add-in:  [Create a custom ribbon button in the host web of a SharePoint Add-in](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in).</span></span>
 
