# <a name="add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in"></a>Добавление пользовательского кода клиентской обработки к надстройке SharePoint, размещенной в SharePoint
Узнайте, как настраивать отрисовку и проверку элементов управления на страницах надстроек SharePoint.
 
**Примечание.** Название "приложения для SharePoint" меняется на "надстройки SharePoint". Пока изменения не будут внесены полностью, в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio по-прежнему может встречаться термин "приложение". Дополнительные сведения см. в разделе [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint#bk_newname).
 
Эта восьмая часть серии статей, посвященной основам разработки надстроек, размещаемых в SharePoint. Для начала следует ознакомиться со статьей [Надстройки SharePoint](sharepoint-add-ins) и предыдущими статьями из этой серии:
 
-  [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins)
-  [Развертывание и установка размещаемых в SharePoint надстроек SharePoint](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in)
-  [Добавление настраиваемых столбцов в надстройки, размещенные в SharePoint](add-custom-columns-to-a-sharepoint-hostedsharepoint-add-in)
-  [Добавление настраиваемого типа контента в надстройки, размещенные в SharePoint](add-a-custom-content-type-to-a-sharepoint-hostedsharepoint-add-in)
-  [Добавление веб-части на страницу в надстройке, размещенной в SharePoint](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in)
-  [Добавление рабочего процесса к надстройке, размещенной в SharePoint](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in)
-  [Добавление настраиваемых страниц и стилей в надстройки, размещенные в SharePoint](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in)

**Примечание.** Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с данной статьей. Кроме того, вы можете скачать репозиторий [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeClientRenderedControl.sln.
 
Используя немного клиентского кода JavaScript, вы можете настраивать отрисовку веб-частей, большинства типов полей (столбцов) и других элементов управления, назначив файл JavaScript свойству **JSLink** элемента управления, например **SPField.JSLink**. Таким способом вы также можете добавлять логику проверки на стороне клиента. В этой статье рассматривается настройка отрисовки поля в списке из надстройки SharePoint "Employee Orientation" (Обучение сотрудников) с помощью клиентской обработки.
 
 **Примечание.** Если в браузере пользователя отключен JavaScript, то SharePoint будет использовать серверные функции отрисовки и проверки.
 
 **Примечание.** Свойство JSLink не поддерживается в списках Survey и Events. Календарь SharePoint представляет собой список Events.
 
## <a name="create-and-register-the-javascript"></a>Создание и регистрация файлов JavaScript

- В **обозревателе решений** щелкните правой кнопкой мыши узел **Скрипты** и выберите **Добавить** > **Новый элемент** > **Интернет**.
- Выберите **Файл JavaScript** и задайте для него имя OrientationStageRendering.js.
- Настраиваемая отрисовка поля должна выполняться автоматически, поэтому добавьте в JavaScript анонимный метод, который будет автоматически запускаться при загрузке файла с указанным ниже кодом.

```
  (function () {

})();
```

- В тексте этого метода (т. е. между символами { и }) добавьте указанный ниже код, чтобы создать объекты JSON (нотации объектов Javascript) для отрисовки контекста переопределения, шаблонов в контексте и шаблонов для полей.
    
```
  var customRenderingOverride = {};
customRenderingOverride.Templates = {};
customRenderingOverride.Templates.Fields = {

}
```

- В тексте объекта шаблона  `Fields` добавьте указанный ниже JSON. Имя свойства `OrientationStage` идентифицирует поле, настроившее отрисовку. Значением свойства является другой объект JSON. Свойство `View` идентифицирует контекст страницы, в котором применяется настраиваемая отрисовка. В данном случае объект сообщает SharePoint, что необходимо использовать настраиваемую отрисовку представлений списков. (Другие параметры будут использоваться для форм изменения, создания и отображения.) Значение свойства ( `renderOrientationStage`) это имя метода настраиваемой отрисовки, который вы создадите на одном из следующих этапов.
    
```
  "OrientationStage": { "View": renderOrientationStage }
```

- Последнее, что должен сделать анонимный метод, сообщить диспетчеру шаблонов SharePoint о переопределении отрисовки. Добавьте указанную ниже строку в конец раздела body метода.
    
```
  SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
```

   Теперь метод должен выглядеть примерно так:
    
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

- Добавьте указанный ниже метод в файл. Он задает для значения столбца **Orientation Stage** (Этап вводного обучения) красный цвет, если оно равно Not Started (Не начат), или зеленый, если задано значение Completed (Завершен). (`ctx` — это объект контекста клиента, объявленный во встроенном сценарии SharePoint.)
    
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

- В **обозревателе решений** разверните узел **Столбцы сайта**, а затем — **OrientationStage**. После этого откройте файл elements.xml. 
- Чтобы сообщить SharePoint, что необходимо использовать специальный код JavaScript, добавьте новый атрибут **JSLink** в элемент **Field**, а затем в качестве его значения назначьте следующий URL-адрес: `~site/Scripts/OrientationStageRendering.js`.
    
**Примечание.** Свойство **JSLink** всегда представляет собой файл, а не метод. Невозможно указать среде SharePoint, какой метод выполнять. По этой причине файл содержит метод, который запускается автоматически.

Теперь открывающий тег элемента **Field** должен выглядеть примерно так:
    
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

- Откройте страницу Default.aspx и добавьте приведенный ниже код в качестве последнего дочернего элемента для элемента **asp:Content**, где для свойства **ContentPlaceHolderID** задано значение **PlaceHolderMain**. 
    
```XML
  <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
    Text="List View Page for New Employees in Seattle" /></p>

```

## <a name="run-and-test-the-add-in"></a>Запуск и тестирование надстройки

- Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее. 
 
- Настроенная нами клиентская обработка влияет на отрисовку поля только на странице представления списка, а не в веб-части представления списка, размещенной на домашней странице. Это вызвано тем, что по умолчанию веб-часть использует клиентскую обработку. Существует способы изменить это, но они слишком сложны для нашего простого примера. Следовательно, чтобы увидеть клиентскую обработку в действии, перейдите по ссылке в конце страницы **List View Page for New Employees in Seattle** (Страница представления списка новых сотрудников в Сиэтле).
 
- Чтобы посмотреть, как работает настраиваемая отрисовка цвета, когда откроется страница представления списка, для некоторых элементов присвойте полю **Orientation Stage** (Этап вводного обучения) значение **Not Started** (Не начат), а для других — значение **Completed** (Завершен).
    
**Список с настраиваемой клиентской обработкой**

![Список новых сотрудников в Сиэтле, где в столбце "Этап адаптации" значения "Не начато" отмечены красным цветом, а значения "Завершено" — зеленым. Другие значения отмечены черным цветом.](../../images/dc8e2b7d-1747-4b65-aab4-6fc93c6867d4.PNG)
  
- Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio. При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать ее последнюю версию.
    
- Эти надстройка и решение Visual Studio будут рассматриваться и в других статьях, поэтому при перерывах в работе рекомендуем отзывать надстройку. В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.

## 
<a name="Nextsteps"> </a>

В статье  [Создание настраиваемой кнопки ленты на хост-сайте надстройки SharePoint](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in) этой серии вы добавите настраиваемый элемент меню и настраиваемую кнопку на ленту в надстройке SharePoint.
 
