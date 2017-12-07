---
title: "Добавление пользовательской функции клиентской обработки в надстройку SharePoint, размещаемую в SharePoint"
description: "Настройте отрисовку и проверку элементов управления на страницах надстройки, создайте и зарегистрируйте код JavaScript, запустите и протестируйте надстройку."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: a3bbe8333e4caef11a479d89627ff8307dde659f
ms.sourcegitcommit: 655e325aec73c8b7c6b5e3aaf71fbb4d2d223b5d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2017
---
# <a name="add-custom-client-side-rendering-to-a-sharepoint-hosted-sharepoint-add-in"></a><span data-ttu-id="155aa-103">Добавление пользовательской функции клиентской обработки в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-103">Add custom client-side rendering to a SharePoint-hosted SharePoint Add-in</span></span>
 
<span data-ttu-id="155aa-104">Эта восьмая часть серии статей, посвященной основам разработки надстроек SharePoint, размещаемых в SharePoint. Для начала ознакомьтесь со статьей [Надстройки SharePoint](sharepoint-add-ins.md) и предыдущими статьями из этой серии.</span><span class="sxs-lookup"><span data-stu-id="155aa-104">This is the eighth in a series of articles about the basics of developing SharePoint-hosted SharePoint Add-ins. You should first be familiar with  [SharePoint Add-ins](sharepoint-add-ins.md) and the previous articles in this series:</span></span>
 
-  [<span data-ttu-id="155aa-105">Знакомство с созданием надстроек SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-105">Get started creating SharePoint-hosted SharePoint Add-ins</span></span>](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md)
-  [<span data-ttu-id="155aa-106">Развертывание и установка надстроек SharePoint, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-106">Deploy and install a SharePoint-hosted SharePoint Add-in</span></span>](deploy-and-install-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="155aa-107">Добавление настраиваемых столбцов в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-107">Add custom columns to a SharePoint-hosted SharePoint Add-in</span></span>](add-custom-columns-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="155aa-108">Добавление пользовательского типа контента в надстройку SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-108">Add a custom content type to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-content-type-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="155aa-109">Добавление веб-части на страницу в надстройке SharePoint, размещаемую в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-109">Add a Web Part to a page in a SharePoint-hosted SharePoint Add-in</span></span>](add-a-web-part-to-a-page-in-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="155aa-110">Добавление рабочего процесса в надстройку для SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-110">Add a workflow to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-workflow-to-a-sharepoint-hosted-sharepoint-add-in.md)
-  [<span data-ttu-id="155aa-111">Добавление настраиваемых страниц и стилей в надстройки SharePoint, размещаемые в SharePoint</span><span class="sxs-lookup"><span data-stu-id="155aa-111">Add a custom page and style to a SharePoint-hosted SharePoint Add-in</span></span>](add-a-custom-page-and-style-to-a-sharepoint-hosted-sharepoint-add-in.md)

> [!NOTE]
> <span data-ttu-id="155aa-112">Если вы изучали предыдущие статьи этой серии о надстройках, размещаемых в SharePoint, то у вас уже есть решение для Visual Studio, которое можно использовать для работы с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="155aa-112">Note  If you have been working through this series about SharePoint-hosted add-ins, then you have a Visual Studio solution that you can use to continue with this topic. You can also download the repository at  SharePoint_SP-hosted_Add-Ins_Tutorials and open the BeforeClientRenderedControl.sln file.</span></span> <span data-ttu-id="155aa-113">Кроме того, вы можете скачать репозиторий на веб-странице [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) и открыть файл BeforeClientRenderedControl.sln.</span><span class="sxs-lookup"><span data-stu-id="155aa-113">You can also download the repository at [SharePoint_SP-hosted_Add-Ins_Tutorials](https://github.com/OfficeDev/SharePoint_SP-hosted_Add-Ins_Tutorials) and open the BeforeClientRenderedControl.sln file.</span></span>
 
<span data-ttu-id="155aa-114">Вы можете использовать небольшой фрагмент клиентского кода JavaScript для настройки отрисовки веб-частей, большинства типов полей (столбцов) и некоторых других элементов управления, назначив файл JavaScript в качестве свойства **JSLink** элемента управления, например **SPField.JSLink**.</span><span class="sxs-lookup"><span data-stu-id="155aa-114">You can use a little client-side JavaScript to customize the rendering of Web Parts, most types of fields (columns), and some other controls, by assigning a JavaScript file to the  **JSLink** property of the control, such as **SPField.JSLink**. You can also add client-side validation logic in this way. In this article you customize the rendering of a field in a list of the Employee Orientation SharePoint Add-in by using client-side rendering.</span></span> <span data-ttu-id="155aa-115">Кроме того, таким способом вы можете добавить логику проверки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="155aa-115">You can also add client-side validation logic in this way.</span></span> <span data-ttu-id="155aa-116">Работая с этой статьей, вы настроите отрисовку поля в списке надстройки SharePoint Employee Orientation (Обучение сотрудников) с помощью функции клиентской обработки.</span><span class="sxs-lookup"><span data-stu-id="155aa-116">In this article, you customize the rendering of a field in a list of the Employee Orientation SharePoint Add-in by using client-side rendering.</span></span>
 
> [!NOTE]
> - <span data-ttu-id="155aa-117">Если в браузере пользователя отключен JavaScript, то SharePoint будет использовать серверные функции отрисовки и проверки.</span><span class="sxs-lookup"><span data-stu-id="155aa-117">Note  If the end-user has JavaScript disabled in their browser, SharePoint will fall back to server-side rendering and validation.</span></span>
> - <span data-ttu-id="155aa-p103">Свойство JSLink не поддерживается в списках Survey (Опрос) или Events (События). Календарь SharePoint представляет собой список Events (События).</span><span class="sxs-lookup"><span data-stu-id="155aa-p103">The JSLink property is not supported on Survey or Events lists. A SharePoint calendar is an Events list.</span></span>

## <a name="create-and-register-the-javascript"></a><span data-ttu-id="155aa-120">Создание и регистрация файлов JavaScript</span><span class="sxs-lookup"><span data-stu-id="155aa-120">Create and register the JavaScript</span></span>

1. <span data-ttu-id="155aa-121">В **обозревателе решений** щелкните правой кнопкой мыши узел **Скрипты** и выберите **Добавить** > **Новый элемент** > **Интернет**.</span><span class="sxs-lookup"><span data-stu-id="155aa-121">In  **Solution Explorer**, right-click the  **Scripts** node and choose **Add** > **New Item** > **Web**.</span></span> 

2. <span data-ttu-id="155aa-122">Выберите **файл JavaScript** и присвойте ему имя **OrientationStageRendering.js**.</span><span class="sxs-lookup"><span data-stu-id="155aa-122">Choose **JavaScript File** and name it **OrientationStageRendering.js**.</span></span> 

3. <span data-ttu-id="155aa-123">Созданная вами пользовательская отрисовка поля должна выполняться автоматически, поэтому используйте указанный ниже код, чтобы добавить анонимный метод в код JavaScript, который запускается автоматически при загрузке файла:</span><span class="sxs-lookup"><span data-stu-id="155aa-123">Your custom rendering of the field should happen automatically, so add an anonymous method to the JavaScript that runs automatically when the file loads with the following code.</span></span>

    ```
      (function () {

      })();
    ```

4. <span data-ttu-id="155aa-124">В тексте этого метода (между символами { и }) добавьте указанный ниже код, чтобы создать объекты JSON (Javascript Object Notation) для отрисовки контекста переопределения, шаблонов в контексте и шаблонов для полей.</span><span class="sxs-lookup"><span data-stu-id="155aa-124">In the body fo this method (between the { } characters), add the following code to create JSON (Javascript Object Notation) objects for the rendering override context, the templates in the context, and the templates for the fields.</span></span>
    
    ```
      var customRenderingOverride = {};
    customRenderingOverride.Templates = {};
    customRenderingOverride.Templates.Fields = {

    }
    ```

5. <span data-ttu-id="155aa-125">В тексте объекта шаблона **Fields** (Поля) добавьте указанный ниже объект JSON.</span><span class="sxs-lookup"><span data-stu-id="155aa-125">In the body of the **Fields** template object, add the following JSON.</span></span>

    ```
      "OrientationStage": { "View": renderOrientationStage }
    ```

   - <span data-ttu-id="155aa-126">Имя свойства `OrientationStage` идентифицирует поле, для которого имеется пользовательская отрисовка.</span><span class="sxs-lookup"><span data-stu-id="155aa-126">The property name `OrientationStage` identifies the field that has customized rendering.</span></span> 
   - <span data-ttu-id="155aa-127">Значение свойства представляет собой еще один объект JSON.</span><span class="sxs-lookup"><span data-stu-id="155aa-127">The value of the property is another JSON object.</span></span> 
   - <span data-ttu-id="155aa-128">Свойство `View` идентифицирует контекст страницы, в котором применяется пользовательская отрисовка.</span><span class="sxs-lookup"><span data-stu-id="155aa-128">The `View` property identifies the page context in which the custom rendering is applied.</span></span> <span data-ttu-id="155aa-129">В этом случае объект сообщает SharePoint, что для представлений списков необходимо использовать пользовательскую отрисовку.</span><span class="sxs-lookup"><span data-stu-id="155aa-129">In this case, the object is telling SharePoint to use the customized rendering on list views.</span></span> <span data-ttu-id="155aa-130">(Другие варианты предназначены для форм Edit [Редактирование], New [Создание] и Display [Отображение].)</span><span class="sxs-lookup"><span data-stu-id="155aa-130">(Other options would be for the Edit, New, and Display forms.)</span></span> 
   - <span data-ttu-id="155aa-131">Значение свойства `renderOrientationStage` — это имя метода пользовательской отрисовки, который вы создадите на одном из последующих этапов.</span><span class="sxs-lookup"><span data-stu-id="155aa-131">The value of the property `renderOrientationStage` is the name of the custom rendering method that you create in a later step.</span></span>

6. <span data-ttu-id="155aa-p105">Последнее, что должен сделать анонимный метод, сообщить диспетчеру шаблонов SharePoint о переопределении отрисовки. Добавьте указанную ниже строку в конец раздела body метода.</span><span class="sxs-lookup"><span data-stu-id="155aa-p105">The last thing that the anonymous method must do is tell SharePoint's template manager about the rendering override. Add the following line to the end of the body of the method.</span></span>
    
    ```
      SPClientTemplates.TemplateManager.RegisterTemplateOverrides(customRenderingOverride);
    ```

   <span data-ttu-id="155aa-134">Теперь метод должен выглядеть примерно так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="155aa-134">The method should now look like the following.</span></span>
    
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

7. <span data-ttu-id="155aa-135">Добавьте указанный ниже метод в файл.</span><span class="sxs-lookup"><span data-stu-id="155aa-135">Add the following content to the file:</span></span> <span data-ttu-id="155aa-136">Он задает красный цвет для значения столбца **Orientation Stage** (Этап обучения), когда это значение равно `Not Started`, и зеленый цвет, когда значение равно `Completed`.</span><span class="sxs-lookup"><span data-stu-id="155aa-136">Add the following method to the file. It sets the color of the  Orientation Stage column value to red when the value is "Not Started" and to green when the value is "Completed". (The  object is a client context object that is declared by in-the-box SharePoint script.)</span></span> <span data-ttu-id="155aa-137">(Объект `ctx` представляет собой объект контекста клиента, объявленный встроенным скриптом SharePoint.)</span><span class="sxs-lookup"><span data-stu-id="155aa-137">(The `ctx` object is a client context object that is declared by in-the-box SharePoint script.)</span></span>
    
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

8. <span data-ttu-id="155aa-138">В **обозревателе решений** разверните узел **Столбцы сайта**, а затем — **OrientationStage** (Этап обучения). После этого откройте файл elements.xml.</span><span class="sxs-lookup"><span data-stu-id="155aa-138">In  **Solution Explorer**, expand  **Site Columns** and then **OrientationStage**; and then open the elements.xml file.</span></span> 

9. <span data-ttu-id="155aa-139">Чтобы сообщить SharePoint, что необходимо использовать ваш пользовательский код JavaScript, добавьте новый атрибут **JSLink** в элемент **Field** (Поле), а затем в качестве его значения укажите следующий URL-адрес: `~site/Scripts/OrientationStageRendering.js`.</span><span class="sxs-lookup"><span data-stu-id="155aa-139">To tell SharePoint to use your custom JavaScript, add a new attribute,  **JSLink**, to the  **Field** element, and then assign the following URL as its value: `~site/Scripts/OrientationStageRendering.js`.</span></span>
    
   > [!NOTE]
   > <span data-ttu-id="155aa-140">Значение свойства **JSLink** всегда представляет собой файл, а не метод.</span><span class="sxs-lookup"><span data-stu-id="155aa-140">The **JSLink** property is always a file, not a method.</span></span> <span data-ttu-id="155aa-141">Не существует способа сообщить SharePoint, какой метод необходимо запустить. Именно поэтому файл содержит метод, который запускается автоматически.</span><span class="sxs-lookup"><span data-stu-id="155aa-141">The JSLink property is always a file, not a method. There's no way to tell SharePoint which method to run. That is why the file contains a method that runs automatically.</span></span>

   <span data-ttu-id="155aa-142">Теперь тег start для элемента **Field** (Поле) будет выглядеть указанным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="155aa-142">The start tag for the **Field** element will now look like the following.</span></span>
    
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

10. <span data-ttu-id="155aa-143">Откройте страницу Default.aspx и добавьте указанный ниже код в качестве последнего дочернего элемента для элемента **asp:Content**, у которого **ContentPlaceHolderID** имеет значение **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="155aa-143">Open the Default.aspx page and add the following code as the last child of the **asp:Content** element that has **ContentPlaceHolderID** set to **PlaceHolderMain**.</span></span> 
    
    ```XML
      <p><asp:HyperLink runat="server" NavigateUrl="JavaScript:window.location = _spPageContextInfo.webAbsoluteUrl + '/Lists/NewEmployeesInSeattle/AllItems.aspx';" 
        Text="List View Page for New Employees in Seattle" /></p>

    ```

## <a name="run-and-test-the-add-in"></a><span data-ttu-id="155aa-144">Запуск и тестирование надстройки</span><span class="sxs-lookup"><span data-stu-id="155aa-144">Run and test the add-in</span></span>

1. <span data-ttu-id="155aa-p108">Нажмите клавишу F5, чтобы развернуть и запустить надстройку. Visual Studio выполнит временную установку надстройки на тестовом сайте SharePoint и сразу же запустит ее.</span><span class="sxs-lookup"><span data-stu-id="155aa-p108">Use the F5 key to deploy and run your add-in. Visual Studio makes a temporary installation of the add-in on your test SharePoint site and immediately runs the add-in.</span></span> 
 
2. <span data-ttu-id="155aa-147">Настроенная вами клиентская обработка влияет на отрисовку поля только на странице представления списка, а не в веб-части представления списка, которую мы поместили на домашнюю страницу.</span><span class="sxs-lookup"><span data-stu-id="155aa-147">The client-side rendering that you have configured affects the rendering of the field only on the list view page, not in the list view Web Part that we put on the home page.</span></span> <span data-ttu-id="155aa-148">Это связано с тем, что по умолчанию веб-часть использует обработку на сервере.</span><span class="sxs-lookup"><span data-stu-id="155aa-148">This is because the Web Part defaults to server-side rendering.</span></span> <span data-ttu-id="155aa-149">Существуют способы изменить это, но они слишком сложны, чтобы использовать их в этом простом примере.</span><span class="sxs-lookup"><span data-stu-id="155aa-149">There are ways to reverse this, but they are too advanced for this simple example.</span></span> <span data-ttu-id="155aa-150">Таким образом, чтобы посмотреть, как работает клиентская обработка, щелкните ссылку в нижней части страницы **List View Page for New Employees in Seattle** (Страница представления списка для новых сотрудников в Сиэтле).</span><span class="sxs-lookup"><span data-stu-id="155aa-150">So, to see the client-side rendering in action, select the link at the bottom of the page **List View Page for New Employees in Seattle**.</span></span>
 
3. <span data-ttu-id="155aa-151">Чтобы посмотреть, как работает настраиваемая отрисовка цвета, когда откроется страница представления списка, для некоторых элементов присвойте полю **Orientation Stage** (Этап вводного обучения) значение **Not Started** (Не начат), а для других значение **Completed** (Завершен).</span><span class="sxs-lookup"><span data-stu-id="155aa-151">When the list view page opens, set the **Orientation Stage** value for some items to **Not Started** and set others to **Completed** to see the custom color rendering.</span></span>
    
   <span data-ttu-id="155aa-152">*Рис. 1. Список с настраиваемой клиентской обработкой*</span><span class="sxs-lookup"><span data-stu-id="155aa-152">*List with custom client-side rendering*</span></span>

   ![Список новых сотрудников в Сиэтле, где в столбце "Этап адаптации" значения "Не начато" отмечены красным цветом, а значения "Завершено" — зеленым. Другие значения отмечены черным цветом.](../images/dc8e2b7d-1747-4b65-aab4-6fc93c6867d4.PNG)
  
4. <span data-ttu-id="155aa-155">Чтобы завершить сеанс отладки, закройте окно браузера или остановите отладку в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="155aa-155">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span> <span data-ttu-id="155aa-156">При каждом нажатии клавиши F5 Visual Studio будет отзывать предыдущую версию надстройки и устанавливать последнюю.</span><span class="sxs-lookup"><span data-stu-id="155aa-156">To end the debugging session, close the browser window or stop debugging in Visual Studio. Each time that you press F5, Visual Studio will retract the previous version of the add-in and install the latest one.</span></span>
    
5. <span data-ttu-id="155aa-157">Вы будете работать с этой надстройкой и решением Visual Studio при изучении других статей, поэтому при перерывах в работе рекомендуется отзывать надстройку.</span><span class="sxs-lookup"><span data-stu-id="155aa-157">You will work with this add-in and Visual Studio solution in other articles, and it's a good practice to retract the add-in one last time when you are done working with it for a while. Right-click the project in  Solution Explorer and choose Retract.</span></span> <span data-ttu-id="155aa-158">В **обозревателе решений** щелкните проект правой кнопкой мыши и выберите пункт **Отозвать**.</span><span class="sxs-lookup"><span data-stu-id="155aa-158">Right-click the project in  **Solution Explorer** and choose **Retract**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="155aa-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="155aa-159">Next steps</span></span>
<span data-ttu-id="155aa-160"><a name="Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="155aa-160"></span></span>

<span data-ttu-id="155aa-161">Работая со следующей статьей этой серии, вы [создадите настраиваемую кнопку ленты на хост-сайте надстройки SharePoint](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="155aa-161">In the next article in this series, you'll add a custom menu item and custom button to the ribbon in the SharePoint Add-in:  [Create a custom ribbon button in the host web of a SharePoint Add-in](create-a-custom-ribbon-button-in-the-host-web-of-a-sharepoint-add-in.md).</span></span>
 
