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
# <a name="customize-a-list-view-in-sharepoint-add-ins-using-client-side-rendering"></a><span data-ttu-id="21f22-103">Настройка представления списка в надстройках SharePoint с использованием технологии клиентской обработки</span><span class="sxs-lookup"><span data-stu-id="21f22-103">Customize a list view in SharePoint Add-ins using client-side rendering</span></span>

<span data-ttu-id="21f22-104">Технология клиентской обработки в SharePoint позволяет создавать собственные выходные данные для набора элементов управления, размещенных на странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="21f22-104">In SharePoint, client-side rendering provides a way for you to produce your own output for a set of controls that are hosted on a SharePoint page.</span></span> <span data-ttu-id="21f22-105">Благодаря этому можно использовать хорошо известные технологии, например HTML и JavaScript, для задания логики отрисовки представлений списков в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="21f22-105">It enables you to use well-known technologies, such as HTML and JavaScript, to define the rendering logic of SharePoint list views.</span></span> <span data-ttu-id="21f22-106">Технология клиентской обработки дает возможность указывать собственные ресурсы JavaScript и размещать их в хранилищах данных, доступных ваших надстроек (например, в библиотеке документов).</span><span class="sxs-lookup"><span data-stu-id="21f22-106">With client-side rendering, you can specify your own JavaScript resources and host them in the data storage options that are available to your add-ins, such as in a document library.</span></span> <span data-ttu-id="21f22-107">Надстройка с размещением в SharePoint включает только компоненты SharePoint.</span><span class="sxs-lookup"><span data-stu-id="21f22-107">A SharePoint-hosted add-in includes only SharePoint components.</span></span> <span data-ttu-id="21f22-108">Ресурсы надстройки с размещением в SharePoint хранятся на изолированном дочернем сайте хост-сайта, называемом сайтом надстройки.</span><span class="sxs-lookup"><span data-stu-id="21f22-108">A SharePoint-hosted add-in has its resources in an isolated subsite of the host web, called the add-in web.</span></span>

<span data-ttu-id="21f22-109"><a name="SP15CSRlistview_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="21f22-109"></span></span>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="21f22-110">Что необходимо для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="21f22-110">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="21f22-111">Для выполнения действий, описанных в этом примере, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="21f22-111">To follow the steps in this example, you need the following:</span></span>

-  <span data-ttu-id="21f22-112">[Visual Studio 2015 и Инструменты разработчика Microsoft Office последней версии](https://www.visualstudio.com/vs/office-tools/).</span><span class="sxs-lookup"><span data-stu-id="21f22-112">[Visual Studio 2015 and the latest Microsoft Office Developer Tools ](https://www.visualstudio.com/vs/office-tools/)</span></span>

- <span data-ttu-id="21f22-113">Среда разработки SharePoint (для локальных сценариев необходимо изолировать надстройку).</span><span class="sxs-lookup"><span data-stu-id="21f22-113">A SharePoint development environment (add-in isolation required for on-premises scenarios)</span></span>

<span data-ttu-id="21f22-114">Инструкции по настройке подходящей среды разработки см. в статье [Два типа надстроек SharePoint (с размещением в SharePoint и у поставщика)](sharepoint-add-ins.md#two-types-of-sharepoint-add-ins-sharepoint-hosted-and-provider-hosted).</span><span class="sxs-lookup"><span data-stu-id="21f22-114">Note  For guidance about how to set up a development environment that fits your needs, see  Start building Office and SharePoint Add-ins.</span></span>

### <a name="core-concepts-to-help-you-understand-list-view-customization-with-client-side-rendering"></a><span data-ttu-id="21f22-115">Основные понятия, связанные с настройкой представления списка с использованием технологии клиентской обработки</span><span class="sxs-lookup"><span data-stu-id="21f22-115">Core concepts to help you understand list view customization with client-side rendering</span></span>

<span data-ttu-id="21f22-116">В приведенной ниже таблице перечислены полезные статьи, в которых описаны понятия, связанные с настройкой представления списка.</span><span class="sxs-lookup"><span data-stu-id="21f22-116">The following table lists useful articles that can help you understand the concepts that are involved in a list view customization scenario.</span></span>

|<span data-ttu-id="21f22-117">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="21f22-117">**Article title**</span></span>|<span data-ttu-id="21f22-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="21f22-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="21f22-119">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="21f22-119">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="21f22-120">Изучите новую модель надстроек в Microsoft SharePoint, с помощью которой можно создавать небольшие и удобные в использовании надстройки для пользователей.</span><span class="sxs-lookup"><span data-stu-id="21f22-120">Learn about the new add-in model in Microsoft SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="21f22-121">Разработка пользовательского интерфейса для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="21f22-121">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)|<span data-ttu-id="21f22-122">Изучите различные варианты пользовательского интерфейса, доступные при создании надстроек SharePoint.</span><span class="sxs-lookup"><span data-stu-id="21f22-122">Learn about the UX options that you have when you are building SharePoint Add-ins.</span></span>|
| [<span data-ttu-id="21f22-123">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="21f22-123">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|<span data-ttu-id="21f22-p102">Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты необходимо разворачивать на хост-сайте, а какие на сайте надстройки, и как выполнить развертывание сайта надстройки в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="21f22-p102">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|

<span data-ttu-id="21f22-126"><a name="SP15CSRlistview_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="21f22-126"></span></span>

## <a name="code-example-customize-a-list-view-by-using-client-side-rendering"></a><span data-ttu-id="21f22-127">Пример кода: настройка представления списка с использованием технологии клиентской обработки</span><span class="sxs-lookup"><span data-stu-id="21f22-127">Code example: Customize a list view by using client-side rendering</span></span>

<span data-ttu-id="21f22-128">Чтобы настроить представление списка, развернутое на сайте надстройки, используя технологию клиентской обработки, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="21f22-128">The following steps show you how to customize a list view that is deployed to the add-in web by using client-side rendering.</span></span>

1. <span data-ttu-id="21f22-129">Создайте проект надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="21f22-129">Create the SharePoint Add-in project.</span></span>

2. <span data-ttu-id="21f22-130">Создайте новое определение списка с настраиваемым представлением.</span><span class="sxs-lookup"><span data-stu-id="21f22-130">Create a new list definition with a custom view.</span></span>

3. <span data-ttu-id="21f22-131">Укажите особую логику обработки в файле JavaScript.</span><span class="sxs-lookup"><span data-stu-id="21f22-131">Provide the custom rendering logic in a JavaScript file.</span></span>

<span data-ttu-id="21f22-132">Ниже показано представление списка объявлений, отрисованное с помощью технологии клиентской обработки.</span><span class="sxs-lookup"><span data-stu-id="21f22-132">Figure 1 shows a client-side rendered view of an announcements list.</span></span>

<span data-ttu-id="21f22-133">**Особое представление списка объявлений**</span><span class="sxs-lookup"><span data-stu-id="21f22-133">**Custom view of an announcements list**</span></span>

![Особое представление списка объявлений](../images/CSRListView_result.png)

### <a name="to-create-the-sharepoint-add-in-project"></a><span data-ttu-id="21f22-135">Создание проекта надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="21f22-135">To create the SharePoint Add-in project</span></span>

1. <span data-ttu-id="21f22-136">Откройте Visual Studio 2015 от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="21f22-136">Open Visual Studio 2015 as administrator.</span></span> <span data-ttu-id="21f22-137">Для этого щелкните правой кнопкой мыши значок **Visual Studio** в меню **Пуск** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="21f22-137">(To do this, right-click the Visual Studio 2015 icon on the Start menu, and select Run as administrator.)</span></span>

2. <span data-ttu-id="21f22-138">Создайте новый проект с помощью шаблона **Надстройка SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="21f22-138">Create a new project using the **SharePoint Add-in** template.</span></span>
    
   <span data-ttu-id="21f22-139">Ниже показано расположение шаблона **Надстройка SharePoint** в Visual Studio 2015: **Шаблоны** > **Visual C#** > **Office/SharePoint** > **Надстройки Office**.</span><span class="sxs-lookup"><span data-stu-id="21f22-139">Figure 2 shows the location of the **SharePoint Add-in** template in Visual Studio 2015, under **Templates** > **Visual C#** > **Office/SharePoint** > **Office Add-ins**.</span></span>
    
   <span data-ttu-id="21f22-140">**Шаблон Visual Studio "Надстройка SharePoint"**</span><span class="sxs-lookup"><span data-stu-id="21f22-140">**Figure 2. Add-in for SharePoint Visual Studio template**</span></span>

   ![Шаблон Visual Studio "Надстройка SharePoint"](../images/AppForSharePointVSTemplate.PNG)

3. <span data-ttu-id="21f22-142">Укажите URL-адрес веб-сайта SharePoint, который планируется использовать для отладки.</span><span class="sxs-lookup"><span data-stu-id="21f22-142">Provide the URL of the SharePoint website that you want to use for debugging.</span></span>
    
4. <span data-ttu-id="21f22-143">Выберите **SharePoint-hosted** (Размещение в SharePoint) в качестве варианта размещения надстройки.</span><span class="sxs-lookup"><span data-stu-id="21f22-143">Select **SharePoint-hosted** as the hosting option for your add-in.</span></span>

### <a name="to-create-a-new-list-definition"></a><span data-ttu-id="21f22-144">Создание определения списка</span><span class="sxs-lookup"><span data-stu-id="21f22-144">To create a new list definition</span></span>

1. <span data-ttu-id="21f22-p104">Щелкните правой кнопкой мыши проект надстройки для SharePoint и добавьте новый элемент **List**. Создайте настраиваемый список на основе объявлений.</span><span class="sxs-lookup"><span data-stu-id="21f22-p104">Right-click the SharePoint Add-in project, and add a new **List** item. Create a customizable list based on Announcements.</span></span>

2. <span data-ttu-id="21f22-p105">Скопируйте следующую разметку и вставьте ее в элемент **Views** файла Schema.xml вашего компонента списка. Эта разметка выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="21f22-p105">Copy the following markup and paste it in the **Views** element in the Schema.xml file of your list feature. The markup performs the following tasks:</span></span>
    
    - <span data-ttu-id="21f22-149">Объявляет новое представление с именем Overridable и атрибутом BaseViewID=2.</span><span class="sxs-lookup"><span data-stu-id="21f22-149">Declares a new view named Overridable with a BaseViewID=2.</span></span>

    - <span data-ttu-id="21f22-150">Предоставляет значение для элемента **JSLink**, которое указывает на файл JavaScript с надстройкой.</span><span class="sxs-lookup"><span data-stu-id="21f22-150">Provides a value for the **JSLink** element that points to a JavaScript file that is provisioned with the add-in.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="21f22-p106">Свойство JSLink не поддерживается в списках "Survey" (Опрос) и "Events" (События). Календарь SharePoint представляет собой список "Events" (События).</span><span class="sxs-lookup"><span data-stu-id="21f22-p106">The JSLink property is not supported on Survey or Events lists. A SharePoint calendar is an Events list.</span></span>

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

### <a name="to-provide-the-custom-rendering-logic-in-a-javascript-file"></a><span data-ttu-id="21f22-153">Указание особой логики отрисовки в файле JavaScript</span><span class="sxs-lookup"><span data-stu-id="21f22-153">To provide the custom rendering logic in a JavaScript file</span></span>

1. <span data-ttu-id="21f22-154">Щелкните правой кнопкой мыши папку **Scripts** и добавьте новый файл JavaScript.</span><span class="sxs-lookup"><span data-stu-id="21f22-154">Right-click the  **Scripts** folder, and add a new JavaScript file. Name the fileCSRListView.js.</span></span> <span data-ttu-id="21f22-155">Назовите его **CSRListView.js**.</span><span class="sxs-lookup"><span data-stu-id="21f22-155">Name the file **CSRListView.js**.</span></span>

2. <span data-ttu-id="21f22-p108">Скопируйте указанный ниже код и вставьте его в файл CSRListView.js. Этот код выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="21f22-p108">Copy the following code and paste it in the CSRListView.js file. The code performs the following tasks:</span></span>
    
    - <span data-ttu-id="21f22-158">Предоставляет обработчики событий для событий **PreRender** и **PostRender**.</span><span class="sxs-lookup"><span data-stu-id="21f22-158">Provides event handlers for the **PreRender** and **PostRender** events.</span></span>

    - <span data-ttu-id="21f22-159">Предоставляет шаблоны для наборов шаблонов Header, Footer и Item.</span><span class="sxs-lookup"><span data-stu-id="21f22-159">Provides templates for the Header, Footer, and Item template sets.</span></span>

    - <span data-ttu-id="21f22-160">Регистрирует шаблоны.</span><span class="sxs-lookup"><span data-stu-id="21f22-160">Registers the templates.</span></span>

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

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="21f22-161">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="21f22-161">To build and run the solution</span></span>

1. <span data-ttu-id="21f22-162">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="21f22-162">Select the F5 key.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="21f22-163">При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="21f22-163">Note  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>

2. <span data-ttu-id="21f22-164">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="21f22-164">Select the **Trust It** button.</span></span>   
 
3. <span data-ttu-id="21f22-165">Перейдите к своему настраиваемому списку, введя адрес _/Lists/<экземпляр_вашего_списка>_, относительный для каталога вашей надстройки в домене сайта надстройки (а не в домене хост-сайта).</span><span class="sxs-lookup"><span data-stu-id="21f22-165">Go to your custom List by entering the  _/Lists/<your_list_instance>_ address relative to your add-in directory in the add-in web domain (not the host web domain). Add one or two announcements. On the ribbon, choose the Overridable view.</span></span> <span data-ttu-id="21f22-166">Добавьте одно или несколько объявлений.</span><span class="sxs-lookup"><span data-stu-id="21f22-166">Add one or two announcements.</span></span> <span data-ttu-id="21f22-167">На ленте выберите представление **Переопределяемый**.</span><span class="sxs-lookup"><span data-stu-id="21f22-167">On the ribbon, select the **Overridable** view.</span></span>
    
## <a name="see-also"></a><span data-ttu-id="21f22-168">См. также</span><span class="sxs-lookup"><span data-stu-id="21f22-168">See also</span></span>
<span data-ttu-id="21f22-169"><a name="SP15CSRlistview_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="21f22-169"></span></span>

-  [<span data-ttu-id="21f22-170">Пример кода: настройка представления списка в надстройке с помощью технологии клиентской обработки</span><span class="sxs-lookup"><span data-stu-id="21f22-170">Code sample: Customize a list view in an add-in using client-side rendering</span></span>](https://code.msdn.microsoft.com/office/SharePoint-2013-Customize-61761017)
-  [<span data-ttu-id="21f22-171">Создание компонентов взаимодействия с пользователем в SharePoint</span><span class="sxs-lookup"><span data-stu-id="21f22-171">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
