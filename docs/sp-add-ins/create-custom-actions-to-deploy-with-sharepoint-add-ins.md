---
title: Создание дополнительных действий для развертывания в надстройках SharePoint
description: Создайте дополнительное действие в SharePoint, которое развертывается на хост-сайте во время развертывания надстройки SharePoint.
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 02e8f47f72dc5da974744cb6463b3ab72fdf2381
ms.sourcegitcommit: c57fc0e802661b0771f8b022964b6956ab4f6caf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2017
---
# <a name="create-custom-actions-to-deploy-with-sharepoint-add-ins"></a><span data-ttu-id="4be52-103">Создание дополнительных действий для развертывания с надстройками SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-103">Create custom actions to deploy with SharePoint Add-ins</span></span>

<span data-ttu-id="4be52-104">При создании надстройки SharePoint дополнительные действия позволяют взаимодействовать со списками и лентой на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="4be52-104">When you are creating a SharePoint Add-in, custom actions let you interact with the lists and the ribbon in the host web.</span></span> <span data-ttu-id="4be52-105">Эти действия развертываются на хост-сайте, когда конечные пользователи устанавливают вашу надстройку.</span><span class="sxs-lookup"><span data-stu-id="4be52-105">A custom action deploys to the host web when end users install your add-in.</span></span> <span data-ttu-id="4be52-106">Дополнительные действия могут открывать удаленную веб-страницу и передавать информацию через строку запроса.</span><span class="sxs-lookup"><span data-stu-id="4be52-106">Custom actions can open a remote webpage and pass information through the query string.</span></span> 

<span data-ttu-id="4be52-107">Для надстроек доступны два вида дополнительных действий: **Лента** и **Пункт меню**.</span><span class="sxs-lookup"><span data-stu-id="4be52-107">Two types of custom actions are available for add-ins: **Ribbon** and **Menu Item**.</span></span>
 
<span data-ttu-id="4be52-108"><a name="SP15Createcustomactionsapps_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="4be52-108"></span></span>

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="4be52-109">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="4be52-109">Prerequisites for using the examples in this article</span></span>

<span data-ttu-id="4be52-110">Вам необходима среда разработки, описанная в статье [Создание надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="4be52-110">You need a development environment as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>

### <a name="core-concepts-to-help-you-understand-custom-actions"></a><span data-ttu-id="4be52-111">Что нужно знать о дополнительных действиях</span><span class="sxs-lookup"><span data-stu-id="4be52-111">Core concepts to help you understand custom actions</span></span>

<span data-ttu-id="4be52-112">В таблице ниже перечислены полезные статьи, в которых описаны понятия и действия, связанные с настройкой дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="4be52-112">The following table lists useful articles that can help you understand the concepts and steps that are involved in a custom action scenario.</span></span>

<span data-ttu-id="4be52-113">**Таблица 1. Основные понятия по дополнительным действиям**</span><span class="sxs-lookup"><span data-stu-id="4be52-113">**Table 1. Core concepts for custom actions**</span></span>

|<span data-ttu-id="4be52-114">**Статья**</span><span class="sxs-lookup"><span data-stu-id="4be52-114">**Article**</span></span>|<span data-ttu-id="4be52-115">**Описание**</span><span class="sxs-lookup"><span data-stu-id="4be52-115">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="4be52-116">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-116">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="4be52-117">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать надстройки — небольшие и удобные в использовании решения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="4be52-117">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="4be52-118">Разработка пользовательского интерфейса для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-118">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)|<span data-ttu-id="4be52-119">Узнайте, как создать удобную надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4be52-119">Learn about the user experience (UX) options that you have when you are building SharePoint Add-ins.</span></span>|
| [<span data-ttu-id="4be52-120">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-120">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|<span data-ttu-id="4be52-p102">Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты необходимо разворачивать на хост-сайте, а какие на сайте надстройки, и как выполнить развертывание сайта надстройки в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="4be52-p102">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|

<span data-ttu-id="4be52-123"><a name="SP15Createcustomactionsapps_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="4be52-123"></span></span>

## <a name="code-example-create-a-custom-action-in-the-host-web-document-libraries"></a><span data-ttu-id="4be52-124">Пример кода. Создание дополнительного действия в библиотеках документов хост-сайта</span><span class="sxs-lookup"><span data-stu-id="4be52-124">Code example: Create a custom action in the host web document libraries</span></span>

<span data-ttu-id="4be52-125">Чтобы создать дополнительное действие в библиотеках документов хост-сайта, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4be52-125">Follow these steps to create a custom action in the host web document libraries:</span></span>

1. <span data-ttu-id="4be52-126">Создайте надстройку SharePoint и удаленные веб-проекты.</span><span class="sxs-lookup"><span data-stu-id="4be52-126">Create the SharePoint Add-in and remote web projects.</span></span>

2. <span data-ttu-id="4be52-127">Добавьте веб-страницу надстройки для дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="4be52-127">To add an add-in webpage for the custom actions</span></span>

3. <span data-ttu-id="4be52-128">Добавьте дополнительное действие "Пункт меню" в проект надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4be52-128">Add a Menu Item custom action to the SharePoint Add-in project.</span></span>

4. <span data-ttu-id="4be52-129">Добавьте дополнительное действия "Лента" в проект надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4be52-129">Add a custom action feature to the SharePoint Add-in project.</span></span>
    
5. <span data-ttu-id="4be52-130">Укажите домашнюю страницу хост-сайта в качестве начальной страницы надстройки.</span><span class="sxs-lookup"><span data-stu-id="4be52-130">Set the add-in start page to the host web home page</span></span>

6. <span data-ttu-id="4be52-131">Соберите и запустите решение.</span><span class="sxs-lookup"><span data-stu-id="4be52-131">Build and run the solution</span></span>
    

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a><span data-ttu-id="4be52-132">Создание надстройки SharePoint и удаленных веб-проектов</span><span class="sxs-lookup"><span data-stu-id="4be52-132">To create the SharePoint Add-in and remote web projects</span></span>

1. <span data-ttu-id="4be52-133">Откройте Visual Studio от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="4be52-133">Open Visual Studio 2015 as administrator.</span></span> <span data-ttu-id="4be52-134">(Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="4be52-134">(To do this, right-click the Visual Studio 2015 icon on the **Start** menu, and select **Run as administrator**.)</span></span>   
 
2. <span data-ttu-id="4be52-135">Создайте надстройку SharePoint с размещением у поставщика, как описано в [этой статье](get-started-creating-provider-hosted-sharepoint-add-ins.md), и назовите ее **CustomActionsApp**.</span><span class="sxs-lookup"><span data-stu-id="4be52-135">Create the provider-hosted SharePoint Add-in as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md) and name itCustomActionsApp.</span></span> 

### <a name="to-add-an-add-in-webpage-for-the-custom-actions"></a><span data-ttu-id="4be52-136">Добавление веб-страницы надстройки для дополнительных действий</span><span class="sxs-lookup"><span data-stu-id="4be52-136">To add an add-in webpage for the custom actions</span></span>

1. <span data-ttu-id="4be52-137">После создания решения Visual Studio щелкните правой кнопкой мыши проект веб-приложения (не проект надстройки SharePoint) и выберите **Добавить** > **Новый элемент** > **Интернет** > **Веб-форма**, чтобы добавить новую веб-форму.</span><span class="sxs-lookup"><span data-stu-id="4be52-137">After the Visual Studio solution has been created, right-click the web application project (not the SharePoint Add-in project) and add a new Web Form by choosing  **Add** > **New Item** > **Web** > **Web Form**. Name the form CustomActionTarget.aspx.</span></span> <span data-ttu-id="4be52-138">Присвойте форме имя **CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="4be52-138">Name the form **CustomActionTarget.aspx**.</span></span> 
 
2. <span data-ttu-id="4be52-139">В файле CustomActionTarget.aspx замените весь элемент **html** и его дочерние элементы следующим HTML-кодом.</span><span class="sxs-lookup"><span data-stu-id="4be52-139">In the CustomActionTarget.aspx file, replace the entire **html** element and its children with the following HTML code.</span></span> <span data-ttu-id="4be52-140">Оставьте всю разметку над элементом **html** без изменений.</span><span class="sxs-lookup"><span data-stu-id="4be52-140">Leave all the markup above the **html** element as it is.</span></span> <span data-ttu-id="4be52-141">HTML-код содержит скрипт JavaScript, который выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="4be52-141">The HTML code contains JavaScript that performs the following tasks:</span></span>
    
    - <span data-ttu-id="4be52-142">Предоставляет заполнитель для параметров строки запроса.</span><span class="sxs-lookup"><span data-stu-id="4be52-142">Provides a placeholder for the query string parameters.</span></span>
    
    - <span data-ttu-id="4be52-143">Извлекает параметры из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="4be52-143">Extracts the parameters from the query string.</span></span>
    
    - <span data-ttu-id="4be52-144">Отображает параметры в заполнителе.</span><span class="sxs-lookup"><span data-stu-id="4be52-144">Renders the parameters in the placeholder.</span></span>

    > [!IMPORTANT] 
    > <span data-ttu-id="4be52-145">Маркеры ItemURL и ItemID передаются только при наличии выделенного элемента.</span><span class="sxs-lookup"><span data-stu-id="4be52-145">The ItemURL and ItemID tokens only get passed when there is an item selected.</span></span> <span data-ttu-id="4be52-146">В готовой надстройке SharePoint код должен обрабатывать ситуации, когда выбранного элемента нет.</span><span class="sxs-lookup"><span data-stu-id="4be52-146">In a production quality SharePoint Add-in, your code needs to handle situations where no item is selected.</span></span> <span data-ttu-id="4be52-147">В этом примере код оповещает пользователя о том, что не был выбран ни один элемент.</span><span class="sxs-lookup"><span data-stu-id="4be52-147">In this example, the code alerts the user that no item has been selected.</span></span> 

    ```HTML
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <title>Custom action target</title>
    </head>
    <body>
        <h2>Query string parameters passed by the custom action:</h2>

        <!-- Placeholder for query string parameters -->
        <ul id="qsparams"/>

        <!-- Main JavaScript function, renders
            the query string parameters -->
        <script lang="javascript">
            var params = document.URL.split("?")[1].split("&amp;");
            var paramsHTML = "";
        
            // Extracts the parameters from the query string.
            // Parameters are URLencoded, decode for rendering
            // in page.
            for (var i = 0; i < params.length; i = i + 1) {
                params[i] = decodeURIComponent(params[i]);
                paramsHTML += "<li>" + params[i] + "</li>";
            }

            // Alert the user when no item has been selected.
            // (The SPListItemId is the 5th parameter.)
            if (params[5] === undefined) {
                paramsHTML += "<div> <h3> No item has been selected from the list.  Please select an item. </h3> </div> ";
            }

            // Render parameters in the placeholder.
            document.getElementById("qsparams").innerHTML =
                paramsHTML;
        </script>
    </body>
    </html>
    ```

<br/>

### <a name="to-add-a-menu-item-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="4be52-148">Добавление дополнительного действия "Пункт меню" в проект надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-148">To add a menu item custom action to the SharePoint Add-in project</span></span>

1. <span data-ttu-id="4be52-149">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие элемента меню**.</span><span class="sxs-lookup"><span data-stu-id="4be52-149">Right-click the SharePoint Add-in project, and choose **Add** > **New Item** > **Office/SharePoint** > **Menu Item Custom Action**.</span></span> 

2. <span data-ttu-id="4be52-150">Оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4be52-150">Keep the default name and choose  **Add**.</span></span>

3. <span data-ttu-id="4be52-151">Мастер "Создание настраиваемого действия для пункта меню" задаст вам несколько вопросов.</span><span class="sxs-lookup"><span data-stu-id="4be52-151">The Create Custom Action for Ribbon Wizard asks you a series of questions.</span></span> <span data-ttu-id="4be52-152">Ответьте на них, используя следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="4be52-152">Give the answers from the following table, and then select Finish.</span></span>
    
    <span data-ttu-id="4be52-153">**Таблица 2. Свойства дополнительного действия "Пункт меню"**</span><span class="sxs-lookup"><span data-stu-id="4be52-153">**Table 2. Menu Item custom action properties**</span></span>

    |<span data-ttu-id="4be52-154">**Вопрос о свойстве**</span><span class="sxs-lookup"><span data-stu-id="4be52-154">**Property question**</span></span>|<span data-ttu-id="4be52-155">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="4be52-155">**Answer**</span></span>|
    |:-----|:-----|
    |<span data-ttu-id="4be52-156">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="4be52-156">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="4be52-157">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="4be52-157">Select **Host Web**.</span></span>|
    |<span data-ttu-id="4be52-158">К какой области относится настраиваемое действие?</span><span class="sxs-lookup"><span data-stu-id="4be52-158">Where is the custom action scoped to?</span></span>|<span data-ttu-id="4be52-159">Выберите **Шаблон списка**.</span><span class="sxs-lookup"><span data-stu-id="4be52-159">Select **List Template**.</span></span>|
    |<span data-ttu-id="4be52-160">Каким конкретным элементом ограничена область настраиваемого действия?</span><span class="sxs-lookup"><span data-stu-id="4be52-160">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="4be52-161">Выберите **Библиотека документов**.</span><span class="sxs-lookup"><span data-stu-id="4be52-161">Select **Document Library**.</span></span>|
    |<span data-ttu-id="4be52-162">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="4be52-162">What is the text on the menu item?</span></span>|<span data-ttu-id="4be52-163">Введите **My Custom Action** (Мое дополнительное действие).</span><span class="sxs-lookup"><span data-stu-id="4be52-163">Type  **My Custom Action**.</span></span>|
    |<span data-ttu-id="4be52-164">Куда ведет настраиваемое действие?</span><span class="sxs-lookup"><span data-stu-id="4be52-164">Where does the custom action navigate to?</span></span>|<span data-ttu-id="4be52-165">Выберите страницу **CustomActionAppWeb\CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="4be52-165">Choose the  **CustomActionAppWeb\CustomActionTarget.aspx** page.</span></span>|

4. <span data-ttu-id="4be52-166">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="4be52-166">Select **Finish**.</span></span>
    
    <span data-ttu-id="4be52-167">Visual Studio создает следующую разметку в файле elements.xml для дополнительного действия "Пункт меню":</span><span class="sxs-lookup"><span data-stu-id="4be52-167">Visual Studio generates the following markup in the elements.xml file of the menu item custom action feature:</span></span>

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <Elements 
        xmlns="http://schemas.microsoft.com/sharepoint/">
        <!-- RegistrationId attribute is the list type id,
            in this case, a document library (id=101). -->
    <CustomAction 
        Id="65695319-4784-478e-8dcd-4e541cb1d682.CustomAction"
        RegistrationType="List"
        RegistrationId="101"
        Location="EditControlBlock"
        Sequence="10001"
        Title="Invoke custom action">
        <!-- 
        Update the Url below to the page you want the custom action to use.
        Start the URL with the token ~remoteAppUrl if the page is in the
        associated web project, use ~appWebUrl if page is in the add-in project.
        -->
        <UrlAction Url=
    "~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}" />
    </CustomAction>
    </Elements>

    ```

    <br/>

5. <span data-ttu-id="4be52-168">Добавьте следующие параметры запроса в конец атрибута **Url** элемента **UrlAction**:</span><span class="sxs-lookup"><span data-stu-id="4be52-168">Add the following query parameters to the end of the **Url** attribute of the **UrlAction** element:</span></span>
    
    `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}`
    
    <span data-ttu-id="4be52-169">Элемент **UrlAction** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4be52-169">The **UrlAction** element should look like the following:</span></span>
    
    ` <UrlAction Url= "~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}" />`

> [!NOTE] 
> <span data-ttu-id="4be52-170">В этом примере удаленная веб-страница открывается в полном окне, когда пользователь выбирает дополнительное действие в меню.</span><span class="sxs-lookup"><span data-stu-id="4be52-170">Note In this example, the remote web page opens in a full window when the user selects the custom action from the menu. Custom menu actions can also open a remote webpage in a dialog box by using the HostWebDialog attribute. For more information, see SharePoint-Add-in-Localization.</span></span> <span data-ttu-id="4be52-171">Дополнительные действия меню также позволяют открывать удаленную веб-страницу в диалоговом окне с помощью атрибута **HostWebDialog**.</span><span class="sxs-lookup"><span data-stu-id="4be52-171">Custom menu actions can also open a remote webpage in a dialog box by using the **HostWebDialog** attribute.</span></span> <span data-ttu-id="4be52-172">Дополнительные сведения см. на странице [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span><span class="sxs-lookup"><span data-stu-id="4be52-172">For more information, see [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span></span>

### <a name="to-add-a-ribbon-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="4be52-173">Добавление дополнительного действия "Лента" в проект надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-173">To add a Ribbon custom action to the SharePoint Add-in project</span></span>

1. <span data-ttu-id="4be52-174">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие ленты**.</span><span class="sxs-lookup"><span data-stu-id="4be52-174">Right-click the SharePoint Add-in project, and choose  **Add** > **New Item** > **Office/SharePoint** > **Ribbon Custom Action**.</span></span> 

2. <span data-ttu-id="4be52-175">Оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4be52-175">Keep the default name and choose  **Add**.</span></span>
 
3. <span data-ttu-id="4be52-176">Мастер "Создание настраиваемого действия для ленты" задаст вам несколько вопросов.</span><span class="sxs-lookup"><span data-stu-id="4be52-176">The Create Custom Action for Ribbon Wizard asks you a series of questions.</span></span> <span data-ttu-id="4be52-177">Ответьте на них, используя следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="4be52-177">Give the answers from the following table, and then select Finish.</span></span>
    
    <span data-ttu-id="4be52-178">**Таблица 3. Свойства дополнительного действия "Лента"**</span><span class="sxs-lookup"><span data-stu-id="4be52-178">**Table 3. Ribbon custom action properties**</span></span>
    
    |<span data-ttu-id="4be52-179">**Вопрос о свойстве**</span><span class="sxs-lookup"><span data-stu-id="4be52-179">**Property question**</span></span>|<span data-ttu-id="4be52-180">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="4be52-180">**Answer**</span></span>|
    |:-----|:-----|
    |<span data-ttu-id="4be52-181">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="4be52-181">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="4be52-182">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="4be52-182">Select **Host Web**.</span></span>|
    |<span data-ttu-id="4be52-183">К какой области относится настраиваемое действие?</span><span class="sxs-lookup"><span data-stu-id="4be52-183">Where is the custom action scoped to?</span></span>|<span data-ttu-id="4be52-184">Выберите **Шаблон списка**.</span><span class="sxs-lookup"><span data-stu-id="4be52-184">Select **List Template**.</span></span>|
    |<span data-ttu-id="4be52-185">Каким конкретным элементом ограничена область настраиваемого действия?</span><span class="sxs-lookup"><span data-stu-id="4be52-185">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="4be52-186">Выберите **Библиотека документов**.</span><span class="sxs-lookup"><span data-stu-id="4be52-186">Select **Document Library**.</span></span>|
    |<span data-ttu-id="4be52-187">Где находится элемент управления?</span><span class="sxs-lookup"><span data-stu-id="4be52-187">Where is the control located?</span></span>|<span data-ttu-id="4be52-188">Выберите **Ribbon.Documents.Manage**.</span><span class="sxs-lookup"><span data-stu-id="4be52-188">Choose  **Ribbon.Documents.Manage**.</span></span>|
    |<span data-ttu-id="4be52-189">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="4be52-189">What is the text on the menu item?</span></span>|<span data-ttu-id="4be52-190">Введите **My Custom Ribbon Button** (Моя дополнительная кнопка ленты).</span><span class="sxs-lookup"><span data-stu-id="4be52-190">Type  **My Custom Ribbon Button**.</span></span>|
    |<span data-ttu-id="4be52-191">Куда ведет настраиваемое действие?</span><span class="sxs-lookup"><span data-stu-id="4be52-191">Where does the custom action navigate to?</span></span>|<span data-ttu-id="4be52-192">Выберите страницу **CustomActionAppWeb\CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="4be52-192">Choose the  **CustomActionAppWeb\CustomActionTarget.aspx** page.</span></span>|

4. <span data-ttu-id="4be52-193">Visual Studio создает следующую разметку в файле elements.xml для функции дополнительного действия "Лента":</span><span class="sxs-lookup"><span data-stu-id="4be52-193">Visual Studio generates the following markup in the elements.xml file of the Ribbon custom action feature:</span></span>
        
    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
    <CustomAction Id="85691508-c076-4f43-93d4-96b4d5253a09.RibbonCustomAction1"
                    RegistrationType="List"
                    RegistrationId="101"
                    Location="CommandUI.Ribbon"
                    Sequence="10001"
                    Title="Invoke &amp;apos;RibbonCustomAction1&amp;apos; action">
        <CommandUIExtension>
        <!-- 
        Update the UI definitions below with the controls and the command actions
        that you want to enable for the custom action.
        -->
        <CommandUIDefinitions>
            <CommandUIDefinition Location="Ribbon.Documents.Manage.Controls._children">
            <Button Id="Ribbon.Documents.Manage.RibbonCustomAction1Button"
                    Alt="My Custom Ribbon Button"
                    Sequence="100"
                    Command="Invoke_RibbonCustomAction1ButtonRequest"
                    LabelText="My Custom Ribbon Button"
                    TemplateAlias="o1"
                    Image32by32="_layouts/15/images/placeholder32x32.png"
                    Image16by16="_layouts/15/images/placeholder16x16.png" />
            </CommandUIDefinition>
        </CommandUIDefinitions>
        <CommandUIHandlers>
            <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest"
                            CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}"/>
        </CommandUIHandlers>
        </CommandUIExtension >
    </CustomAction>
    </Elements> 

    ```

    <br/>

5. <span data-ttu-id="4be52-194">Добавьте следующие параметры запроса в конец атрибута **CommandAction** элемента **CommandUIHandler**:</span><span class="sxs-lookup"><span data-stu-id="4be52-194">Add the following query parameters to the end of the **CommandAction** attribute of the **CommandUIHandler** element:</span></span>
    
    `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}`
    
    <span data-ttu-id="4be52-195">Элемент **CommandUIHandler** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4be52-195">The **CommandUIHandler** element should look like the following:</span></span>
    
    ` <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest" CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}" />`
    
    > [!NOTE] 
    > <span data-ttu-id="4be52-196">Дополнительные действия для ленты используют **SelectedListId** и **SelectedItemId**.</span><span class="sxs-lookup"><span data-stu-id="4be52-196">Ribbon custom actions use **SelectedListId** and **SelectedItemId**.</span></span> <span data-ttu-id="4be52-197">**ListId** и **ItemId** работают только с дополнительными действиями "Пункт меню".</span><span class="sxs-lookup"><span data-stu-id="4be52-197">**Note  Ribbon custom actions use  SelectedListId and SelectedItemId.  ListId** and **ItemId** work only with menu item custom actions.</span></span>

### <a name="to-set-the-add-in-start-page-to-the-host-web-home-page"></a><span data-ttu-id="4be52-198">Установка домашней страницы хост-сайта в качестве начальной страницы надстройки</span><span class="sxs-lookup"><span data-stu-id="4be52-198">Set the add-in start page to the host web home page</span></span>

1. <span data-ttu-id="4be52-199">В примере ниже у надстройки SharePoint нет своего сайта, а ее удаленное веб-приложение существует только для размещения формы.</span><span class="sxs-lookup"><span data-stu-id="4be52-199">The continuing sample SharePoint Add-in doesn't have any add-in web and its remote web application exists only to host the form. So the start page of the add-in should be set to the home page of the host web.</span></span> <span data-ttu-id="4be52-200">Поэтому начальной страницей надстройки следует сделать домашнюю страницу хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="4be52-200">The continuing sample SharePoint Add-in doesn't have any add-in web and its remote web application exists only to host the form. So the start page of the add-in should be set to the home page of the host web.</span></span> 
    
    <span data-ttu-id="4be52-201">Для начала выберите проект надстройки SharePoint (не проект веб-приложения) в **обозревателе решений** и скопируйте в буфер обмена значение свойства **URL-адрес сайта**, включая протокол (например, `https://contoso.sharepoint.com`).</span><span class="sxs-lookup"><span data-stu-id="4be52-201">To begin, select the SharePoint Add-in project (not the web application project) in **Solution Explorer** and copy the value of the **Site URL** property, including the protocol (for example `https://contoso.sharepoint.com`) into the clipboard.</span></span> 
    
2. <span data-ttu-id="4be52-202">Откройте манифест надстройки, а затем вставьте URL-адрес в поле **Начальная страница**.</span><span class="sxs-lookup"><span data-stu-id="4be52-202">Open the add-in manifest, and then paste the URL into the **Start Page** box.</span></span>
    
3. <span data-ttu-id="4be52-203">При необходимости можно удалить страницу Default.aspx из проекта веб-приложения, так как она не используется в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4be52-203">Optionally, you can delete the Default.aspx page from the web application project, because it is not used in the SharePoint Add-in.</span></span>
    
### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="4be52-204">Сборка и запуск решения</span><span class="sxs-lookup"><span data-stu-id="4be52-204">To build and run the solution</span></span>

1. <span data-ttu-id="4be52-205">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="4be52-205">Select the F5 key.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="4be52-206">При нажатии клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="4be52-206">Note  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>

2. <span data-ttu-id="4be52-207">Нажмите кнопку **Доверять**.</span><span class="sxs-lookup"><span data-stu-id="4be52-207">Select the **Trust It** button.</span></span> <span data-ttu-id="4be52-208">Откроется страница сайта разработчика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4be52-208">Choose the  Trust It button. The default page of your developer site opens.</span></span>

3. <span data-ttu-id="4be52-209">Перейдите в любую библиотеку документов на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="4be52-209">Navigate to any document library in the host web.</span></span>
    
   <span data-ttu-id="4be52-210">**Запуск дополнительного действия меню**</span><span class="sxs-lookup"><span data-stu-id="4be52-210">**Launching a custom menu action**</span></span>

   ![Библиотека документов с открытой выноской для документа; меню, которое открывает кнопка выноски, и открытое меню "Дополнительно"](../images/477cecf5-03ff-46ff-9c25-a5f9a86d43f4.png)

4. <span data-ttu-id="4be52-212">Нажмите кнопку выноски (**...**) для любого документа.</span><span class="sxs-lookup"><span data-stu-id="4be52-212">Choose the callout button ( **...**) for any document. The callout opens.</span></span> <span data-ttu-id="4be52-213">Откроется выноска.</span><span class="sxs-lookup"><span data-stu-id="4be52-213">The callout opens.</span></span>

5. <span data-ttu-id="4be52-214">Нажмите кнопку выноски (**...**) на выноске.</span><span class="sxs-lookup"><span data-stu-id="4be52-214">Choose the callout button ( **...**) on the callout.</span></span> 

6. <span data-ttu-id="4be52-215">Выберите **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="4be52-215">Select **Advanced tools (Kudu)**.</span></span>

7. <span data-ttu-id="4be52-216">Выберите в контекстном меню **My Custom Menu Action** (Мое дополнительное действие меню).</span><span class="sxs-lookup"><span data-stu-id="4be52-216">Select **My Custom Menu Action** in the context menu.</span></span> <span data-ttu-id="4be52-217">На открывшейся удаленной веб-странице вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="4be52-217">Choose  My Custom Menu Action in the context menu. You should see something like the following on the remote webpage that opens:</span></span>
    
   <span data-ttu-id="4be52-218">**Удаленная веб-страница с параметрами из дополнительного действия**</span><span class="sxs-lookup"><span data-stu-id="4be52-218">**Remote webpage with parameters from the custom action**</span></span>  
   <span data-ttu-id="4be52-219">![Веб-страница с параметрами из дополнительного действия](../images/CustomActions_target.png)</span><span class="sxs-lookup"><span data-stu-id="4be52-219">![Web page with parameters from a custom action](../images/CustomActions_target.png)</span></span>

8. <span data-ttu-id="4be52-220">Нажмите в браузере кнопку **Назад**, чтобы вернуться в библиотеку.</span><span class="sxs-lookup"><span data-stu-id="4be52-220">Click the  **Back** button on your browser to return to the library.</span></span>
    
   <span data-ttu-id="4be52-221">**Запуск дополнительного действия "Лента"**</span><span class="sxs-lookup"><span data-stu-id="4be52-221">**Launching a custom ribbon action**</span></span>

   ![Библиотека документов с выбранным документом, открытой вкладкой "Файл" и дополнительной кнопкой на ленте.](../images/b315cb68-ff6a-4770-a1dc-738696ab71d2.png)

9. <span data-ttu-id="4be52-223">Выберите любой документ.</span><span class="sxs-lookup"><span data-stu-id="4be52-223">Select any document.</span></span>

10. <span data-ttu-id="4be52-224">Откройте на ленте вкладку **Файл**.</span><span class="sxs-lookup"><span data-stu-id="4be52-224">Open the **File** tab on the ribbon.</span></span>

11. <span data-ttu-id="4be52-225">Выберите **My Custom Ribbon Button** (Моя дополнительная кнопка ленты).</span><span class="sxs-lookup"><span data-stu-id="4be52-225">Type  **My Custom Ribbon Button**.</span></span> <span data-ttu-id="4be52-226">Отобразится та же удаленная веб-страница.</span><span class="sxs-lookup"><span data-stu-id="4be52-226">Choose  My Custom Ribbon Button. You see the same remote web page.</span></span>

<br/>

#### <a name="troubleshooting-the-solution"></a><span data-ttu-id="4be52-227">Устранение неполадок в решении</span><span class="sxs-lookup"><span data-stu-id="4be52-227">Table 2. Troubleshooting the solution</span></span>

|<span data-ttu-id="4be52-228">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="4be52-228">**Problem**</span></span>|<span data-ttu-id="4be52-229">**Решение**</span><span class="sxs-lookup"><span data-stu-id="4be52-229">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="4be52-230">Visual Studio не открывает браузер после нажатия клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="4be52-230">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="4be52-231">Сделайте проект надстройки SharePoint запускаемым.</span><span class="sxs-lookup"><span data-stu-id="4be52-231">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="4be52-232">Маркеры в URL-адресе не разрешаются после нажатия клавиши F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4be52-232">The tokens in the URL are not resolved after you press the F5 key in Visual Studio.</span></span>|<span data-ttu-id="4be52-233">Перейдите на страницу **Содержимое сайта** на хост-сайте и выберите значок вашей надстройки.</span><span class="sxs-lookup"><span data-stu-id="4be52-233">Go to the  **Site Contents** page in the host web, and click the icon for your add-in.</span></span>|

## <a name="see-also"></a><span data-ttu-id="4be52-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4be52-234">See also</span></span>
<span data-ttu-id="4be52-235"><a name="SP15Createcustomactionsapps_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="4be52-235"></span></span>

- [<span data-ttu-id="4be52-236">Пример кода. Открытие удаленной веб-страницы надстройки с помощью дополнительного действия ECB</span><span class="sxs-lookup"><span data-stu-id="4be52-236">Code sample: Open a remote add-in webpage using an ECB custom action</span></span>](https://code.msdn.microsoft.com/office/SharePoint-2013-Open-a-36d1598d)    
- [<span data-ttu-id="4be52-237">Создание компонентов взаимодействия с пользователем в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4be52-237">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)