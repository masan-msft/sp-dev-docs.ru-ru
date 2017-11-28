---
title: "Создание дополнительных действий для развертывания с надстройками SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 8772f35ad0f165e172356350f23bb1859d4a131a
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-custom-actions-to-deploy-with-sharepoint-add-ins"></a><span data-ttu-id="be329-102">Создание дополнительных действий для развертывания с надстройками SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-102">Create custom actions to deploy with SharePoint Add-ins</span></span>
<span data-ttu-id="be329-103">Узнайте, как создать дополнительное действие в SharePoint, которое разворачивается на хост-сайте во время развертывания надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be329-103">Learn how to create a custom action in SharePoint that deploys to the host web when you deploy a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="be329-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="be329-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="be329-p102">Дополнительные действия позволяют взаимодействовать со списками и лентой на хост-сайте. Дополнительное действие разворачивается на хост-сайте, когда конечные пользователи устанавливают вашу надстройку. Дополнительные действия могут открывать удаленную веб-страницу и передавать информацию через строку запроса. Для надстроек доступны дополнительные действия ленты и элемента меню.</span><span class="sxs-lookup"><span data-stu-id="be329-p102">When you are creating a SharePoint Add-in, custom actions let you interact with the lists and the ribbon in the host web. A custom action deploys to the host web when end users install your add-in. Custom actions can open a remote webpage and pass information through the query string. There are two types of custom actions available for add-ins: Ribbon andMenu Item custom actions.</span></span>
 

## <a name="prerequisites-for-using-the-examples-in-this-article"></a><span data-ttu-id="be329-111">Необходимые условия для использования примеров в этой статье</span><span class="sxs-lookup"><span data-stu-id="be329-111">Prerequisites for using the examples in this article</span></span>
<span data-ttu-id="be329-112"><a name="SP15Createcustomactionsapps_Prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="be329-112"></span></span>

<span data-ttu-id="be329-113">Вам необходима среда разработки, описанная в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="be329-113">You need a development environment as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
 

 

### <a name="core-concepts-to-help-you-understand-custom-actions"></a><span data-ttu-id="be329-114">Основные понятия по дополнительным действиям</span><span class="sxs-lookup"><span data-stu-id="be329-114">Core concepts to help you understand custom actions</span></span>

<span data-ttu-id="be329-115">В таблице ниже перечислены полезные статьи, в которых описаны понятия и действия, связанные с настройкой дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="be329-115">The following table lists useful articles that can help you understand the concepts and steps that are involved in a custom action scenario.</span></span>
 

 

<span data-ttu-id="be329-116">**Таблица 1. Основные понятия по дополнительным действиям**</span><span class="sxs-lookup"><span data-stu-id="be329-116">**Table 1. Core concepts for custom actions**</span></span>


|<span data-ttu-id="be329-117">**Статья**</span><span class="sxs-lookup"><span data-stu-id="be329-117">**Article**</span></span>|<span data-ttu-id="be329-118">**Описание**</span><span class="sxs-lookup"><span data-stu-id="be329-118">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="be329-119">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-119">SharePoint Add-ins</span></span>](sharepoint-add-ins.md)|<span data-ttu-id="be329-120">Сведения о новой модели надстроек в SharePoint, с помощью которой можно создавать надстройки — небольшие и удобные в использовании решения для пользователей.</span><span class="sxs-lookup"><span data-stu-id="be329-120">Learn about the new add-in model in SharePoint that enables you to create add-ins, which are small, easy-to-use solutions for end users.</span></span>|
| [<span data-ttu-id="be329-121">Разработка пользовательского интерфейса для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-121">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)|<span data-ttu-id="be329-122">Узнайте, как создать удобную надстройку SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be329-122">Learn about the user experience (UX) options that you have when you are building SharePoint Add-ins.</span></span>|
| [<span data-ttu-id="be329-123">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-123">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](host-webs-add-in-webs-and-sharepoint-components-in-sharepoint.md)|<span data-ttu-id="be329-p103">Изучите различия между хост-сайтами и сайтами надстроек. Узнайте, какие компоненты SharePoint можно включать в надстройку для SharePoint, какие компоненты необходимо разворачивать на хост-сайте, а какие на сайте надстройки, и как выполнить развертывание сайта надстройки в изолированном домене.</span><span class="sxs-lookup"><span data-stu-id="be329-p103">Learn about the difference between host webs and add-in webs. Find out which SharePoint components can be included in a SharePoint Add-in, which components are deployed to the host web, which components are deployed to the add-in web, and how the add-in web is deployed in an isolated domain.</span></span>|

## <a name="code-example-create-a-custom-action-in-the-host-web-document-libraries"></a><span data-ttu-id="be329-126">Пример кода. Создание дополнительного действия в библиотеках документов хост-сайта</span><span class="sxs-lookup"><span data-stu-id="be329-126">Code example: Create a custom action in the host web document libraries</span></span>
<span data-ttu-id="be329-127"><a name="SP15Createcustomactionsapps_Codeexample"> </a></span><span class="sxs-lookup"><span data-stu-id="be329-127"></span></span>

<span data-ttu-id="be329-128">Чтобы создать дополнительное действие в библиотеках документов хост-сайта, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="be329-128">Follow these steps to create a custom action in the host web document libraries:</span></span>
 

 

1. <span data-ttu-id="be329-129">Создайте проект надстройки для SharePoint и удаленный веб-проект.</span><span class="sxs-lookup"><span data-stu-id="be329-129">Create the SharePoint Add-in and remote web projects.</span></span>
    
 
2. <span data-ttu-id="be329-130">Добавьте компонент дополнительного действия в проект надстройки для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be329-130">Add a custom action feature to the SharePoint Add-in project.</span></span>
    
 
3. <span data-ttu-id="be329-131">Добавьте веб-страницу надстройки в веб-проект.</span><span class="sxs-lookup"><span data-stu-id="be329-131">Add an add-in webpage to the web project.</span></span>
    
 

### <a name="to-create-the-sharepoint-add-in-and-remote-web-projects"></a><span data-ttu-id="be329-132">Создание надстройки SharePoint и удаленных веб-проектов</span><span class="sxs-lookup"><span data-stu-id="be329-132">To create the SharePoint Add-in and remote web projects</span></span>


1. <span data-ttu-id="be329-p104">Откройте Visual Studio от имени администратора. (Для этого щелкните правой кнопкой мыши значок Visual Studio в меню **Пуск** и выберите **Запуск от имени администратора**.)</span><span class="sxs-lookup"><span data-stu-id="be329-p104">Open Visual Studio as administrator. (To do this, right-click the Visual Studio icon on the  **Start** menu, and choose **Run as administrator**.)</span></span>
    
 
2. <span data-ttu-id="be329-135">Создайте надстройку SharePoint с размещением у поставщика, как описано в статье [Знакомство с созданием надстроек SharePoint с размещением у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md), и назовите ее itCustomActionsApp.</span><span class="sxs-lookup"><span data-stu-id="be329-135">Create the provider-hosted SharePoint Add-in as explained in  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md) and name itCustomActionsApp.</span></span> 
    
 

### <a name="to-add-an-add-in-webpage-for-the-custom-actions"></a><span data-ttu-id="be329-136">Добавление веб-страницы надстройки для дополнительных действий</span><span class="sxs-lookup"><span data-stu-id="be329-136">To add an add-in webpage for the custom actions</span></span>


1. <span data-ttu-id="be329-p105">После создания решения Visual Studio щелкните правой кнопкой проект веб-приложения (не проект надстройки SharePoint) и добавьте новую веб-форму. Для этого выберите **Добавить** > **Новый элемент** > **Веб** > **Веб-форма**. Назовите форму CustomActionTarget.aspx.</span><span class="sxs-lookup"><span data-stu-id="be329-p105">After the Visual Studio solution has been created, right-click the web application project (not the SharePoint Add-in project) and add a new Web Form by choosing  **Add** > **New Item** > **Web** > **Web Form**. Name the form CustomActionTarget.aspx.</span></span>
    
 
2. <span data-ttu-id="be329-p106">В файле CustomActionTarget.aspx замените весь элемент **html** и его дочерние элементы следующим кодом HTML. Оставьте всю разметку над элементом **html** без изменений. Код HTML содержит скрипт JavaScript, который выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="be329-p106">In the CustomActionTarget.aspx file, replace the entire  **html** element and it's children with the following HTML code. Leave all the markup above the **html** element as it is. The HTML code contains JavaScript that performs the following tasks:</span></span>
    
      - <span data-ttu-id="be329-142">Предоставляет заполнитель для параметров строки запроса.</span><span class="sxs-lookup"><span data-stu-id="be329-142">Provides a placeholder for the query string parameters.</span></span>
    
 
  - <span data-ttu-id="be329-143">Извлекает параметры из строки запроса.</span><span class="sxs-lookup"><span data-stu-id="be329-143">Extracts the parameters from the query string.</span></span>
    
 
  - <span data-ttu-id="be329-144">Отображает параметры в заполнителе.</span><span class="sxs-lookup"><span data-stu-id="be329-144">Renders the parameters in the placeholder.</span></span>
    
 

     <span data-ttu-id="be329-p107">**Важно!** Маркеры ItemURL и ItemID передаются, только когда выбран элемент. В производственной надстройке SharePoint код должен обрабатывать ситуации, когда элемент не выбран. В этом примере код предупреждает пользователя о том, что элемент не выбран.</span><span class="sxs-lookup"><span data-stu-id="be329-p107">**Important**  The ItemURL and ItemID tokens only get passed when there is an item selected. In a production quality SharePoint Add-in, your code needs to handle situations where no item is selected. In this example the code alerts the user that no item has been selected.</span></span> 

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


### <a name="to-add-a-menu-item-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="be329-148">Добавление дополнительного действия элемента меню в проект надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-148">To add a menu item custom action to the SharePoint Add-in project</span></span>


1. <span data-ttu-id="be329-149">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие элемента меню**.</span><span class="sxs-lookup"><span data-stu-id="be329-149">Right-click the SharePoint Add-in project, and choose  **Add** > **New Item** > **Office/SharePoint** > **Menu Item Custom Action**.</span></span> 
    
 
2. <span data-ttu-id="be329-150">Оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="be329-150">Keep the default name and choose  **Add**.</span></span>
    
 
3. <span data-ttu-id="be329-p108">Мастер **Создание настраиваемого действия для пункта меню** задаст вам несколько вопросов. Ответьте на них, используя следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="be329-p108">The  **Create Custom Action for Menu Item** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    
    <span data-ttu-id="be329-153">**Таблица 2. Свойства дополнительного действия элемента меню**</span><span class="sxs-lookup"><span data-stu-id="be329-153">**Table 2. Menu Item custom action properties**</span></span>


|<span data-ttu-id="be329-154">**Вопрос о свойстве**</span><span class="sxs-lookup"><span data-stu-id="be329-154">**Property question**</span></span>|<span data-ttu-id="be329-155">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="be329-155">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="be329-156">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-156">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="be329-157">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="be329-157">Choose  **Host Web**.</span></span>|
|<span data-ttu-id="be329-158">К какой области относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-158">Where is the custom action scoped to?</span></span>|<span data-ttu-id="be329-159">Выберите **Шаблон списка**.</span><span class="sxs-lookup"><span data-stu-id="be329-159">Choose  **List Template**.</span></span>|
|<span data-ttu-id="be329-160">К какому элементу относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-160">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="be329-161">Выберите **Библиотека документов**.</span><span class="sxs-lookup"><span data-stu-id="be329-161">Choose  **Document Library**.</span></span>|
|<span data-ttu-id="be329-162">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="be329-162">What is the text on the menu item?</span></span>|<span data-ttu-id="be329-163">Введите **Мое дополнительное действие**.</span><span class="sxs-lookup"><span data-stu-id="be329-163">Type  **My Custom Action**.</span></span>|
|<span data-ttu-id="be329-164">Куда будет вести дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-164">Where does the custom action navigate to?</span></span>|<span data-ttu-id="be329-165">Выберите страницу **CustomActionAppWeb\CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="be329-165">Choose the  **CustomActionAppWeb\CustomActionTarget.aspx** page.</span></span>|
4. <span data-ttu-id="be329-166">Нажмите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="be329-166">Choose  **Finish**.</span></span>
    
    <span data-ttu-id="be329-167">Visual Studio создает следующую разметку в файле elements.xml функции дополнительного действия элемента меню:</span><span class="sxs-lookup"><span data-stu-id="be329-167">Visual Studio generates the following markup in the elements.xml file of the menu item custom action feature:</span></span>
    


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

5. <span data-ttu-id="be329-168">Добавьте следующие параметры запроса в конец атрибута **Url** элемента **UrlAction**:</span><span class="sxs-lookup"><span data-stu-id="be329-168">Add the following query parameters to the end of the  **Url** attribute of the **UrlAction** element:</span></span>
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}`
    
    <span data-ttu-id="be329-169">Элемент **UrlAction** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="be329-169">The  **UrlAction** element should look like the following:</span></span>
    
     ` <UrlAction Url= "~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={ItemId}&amp;amp;SPListId={ListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}&amp;amp;SPItemURL={ItemUrl}" />`
    
 

 <span data-ttu-id="be329-p109">**Примечание.** В этом примере удаленная веб-страница открывается в полном окне, когда пользователь выбирает дополнительное действие в меню. Удаленную веб-страницу также можно открывать в диалоговом окне с помощью атрибута **HostWebDialog**. Дополнительные сведения см. в репозитории [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span><span class="sxs-lookup"><span data-stu-id="be329-p109">**Note**  In this example, the remote web page opens in a full window when the user selects the custom action from the menu. Custom menu actions can also open a remote webpage in a dialog box by using the  **HostWebDialog** attribute. For more information, see [SharePoint-Add-in-Localization](https://github.com/OfficeDev/SharePoint-Add-in-Localization).</span></span>
 


### <a name="to-add-a-ribbon-custom-action-to-the-sharepoint-add-in-project"></a><span data-ttu-id="be329-173">Добавление дополнительного действия ленты в проект надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-173">To add a Ribbon custom action to the SharePoint Add-in project</span></span>


1. <span data-ttu-id="be329-174">Щелкните правой кнопкой мыши проект надстройки SharePoint и выберите **Добавить** > **Новый элемент** > **Office/SharePoint** > **Настраиваемое действие ленты**.</span><span class="sxs-lookup"><span data-stu-id="be329-174">Right-click the SharePoint Add-in project, and choose  **Add** > **New Item** > **Office/SharePoint** > **Ribbon Custom Action**.</span></span> 
    
 
2. <span data-ttu-id="be329-175">Оставьте имя по умолчанию и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="be329-175">Keep the default name and choose  **Add**.</span></span>
    
 
3. <span data-ttu-id="be329-p110">Мастер **Создание настраиваемого действия для ленты** задаст вам несколько вопросов. Ответьте на них, используя следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="be329-p110">The  **Create Custom Action for Ribbon** wizard asks you a series of questions. Give the answers from the following table:</span></span>
    
    <span data-ttu-id="be329-178">**Таблица 3. Свойства дополнительного действия ленты**</span><span class="sxs-lookup"><span data-stu-id="be329-178">**Table 3. Ribbon custom action properties**</span></span>


|<span data-ttu-id="be329-179">**Вопрос о свойстве**</span><span class="sxs-lookup"><span data-stu-id="be329-179">**Property question**</span></span>|<span data-ttu-id="be329-180">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="be329-180">**Answer**</span></span>|
|:-----|:-----|
|<span data-ttu-id="be329-181">Где вы хотите разместить дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-181">Where do you want to expose the custom action?</span></span>|<span data-ttu-id="be329-182">Выберите вариант **хост-сайт**.</span><span class="sxs-lookup"><span data-stu-id="be329-182">Choose  **Host Web**.</span></span>|
|<span data-ttu-id="be329-183">К какой области относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-183">Where is the custom action scoped to?</span></span>|<span data-ttu-id="be329-184">Выберите **Шаблон списка**.</span><span class="sxs-lookup"><span data-stu-id="be329-184">Choose  **List Template**.</span></span>|
|<span data-ttu-id="be329-185">К какому элементу относится дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-185">Which particular item is the custom action scoped to?</span></span>|<span data-ttu-id="be329-186">Выберите **Библиотека документов**.</span><span class="sxs-lookup"><span data-stu-id="be329-186">Choose  **Document Library**.</span></span>|
|<span data-ttu-id="be329-187">Где находится элемент управления?</span><span class="sxs-lookup"><span data-stu-id="be329-187">Where is the control located?</span></span>|<span data-ttu-id="be329-188">Выберите **Ribbon.Documents.Manage**.</span><span class="sxs-lookup"><span data-stu-id="be329-188">Choose  **Ribbon.Documents.Manage**.</span></span>|
|<span data-ttu-id="be329-189">Какой текст будет указан в элементе меню?</span><span class="sxs-lookup"><span data-stu-id="be329-189">What is the text on the menu item?</span></span>|<span data-ttu-id="be329-190">Введите **Моя дополнительная кнопка ленты**.</span><span class="sxs-lookup"><span data-stu-id="be329-190">Type  **My Custom Ribbon Button**.</span></span>|
|<span data-ttu-id="be329-191">Куда будет вести дополнительное действие?</span><span class="sxs-lookup"><span data-stu-id="be329-191">Where does the custom action navigate to?</span></span>|<span data-ttu-id="be329-192">Выберите страницу **CustomActionAppWeb\CustomActionTarget.aspx**.</span><span class="sxs-lookup"><span data-stu-id="be329-192">Choose the  **CustomActionAppWeb\CustomActionTarget.aspx** page.</span></span>|
4. <span data-ttu-id="be329-193">Visual Studio создает следующую разметку в файле elements.xml функции дополнительного действия ленты:</span><span class="sxs-lookup"><span data-stu-id="be329-193">Visual Studio generates the following markup in the elements.xml file of the Ribbon custom action feature:</span></span>
    
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

5. <span data-ttu-id="be329-194">Добавьте следующие параметры запроса в конец атрибута **CommandAction** элемента **CommandUIHandler**:</span><span class="sxs-lookup"><span data-stu-id="be329-194">Add the following query parameters to the end of the  **CommandAction** attribute of the **CommandUIHandler** element:</span></span>
    
     `&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}`
    
    <span data-ttu-id="be329-195">Элемент **CommandUIHandler** должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="be329-195">The  **CommandUIHandler** element should look like the following:</span></span>
    
     ` <CommandUIHandler Command="Invoke_RibbonCustomAction1ButtonRequest" CommandAction="~remoteAppUrl/CustomActionTarget.aspx?{StandardTokens}&amp;amp;SPListItemId={SelectedItemId}&amp;amp;SPListId={SelectedListId}&amp;amp;SPSource={Source}&amp;amp;SPListURLDir={ListUrlDir}" />`
    
     <span data-ttu-id="be329-p111">**Примечание.** Дополнительные действия ленты используют **SelectedListId** и **SelectedItemId**. **ListId** и **ItemId** работают только с дополнительными действиями элементов меню.</span><span class="sxs-lookup"><span data-stu-id="be329-p111">**Note**  Ribbon custom actions use  **SelectedListId** and **SelectedItemId**.  **ListId** and **ItemId** work only with menu item custom actions.</span></span>

### <a name="set-the-add-in-start-page-to-the-host-web-home-page"></a><span data-ttu-id="be329-198">Установка домашней страницы хост-сайта в качестве начальной страницы надстройки</span><span class="sxs-lookup"><span data-stu-id="be329-198">Set the add-in start page to the host web home page</span></span>


1. <span data-ttu-id="be329-p112">В примере ниже у надстройки для SharePoint нет сайта надстройки, а ее удаленное веб-приложение существует только для размещения формы. Поэтому начальной страницей надстройки следует сделать домашнюю страницу хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="be329-p112">The continuing sample SharePoint Add-in doesn't have any add-in web and its remote web application exists only to host the form. So the start page of the add-in should be set to the home page of the host web.</span></span> 
    
    <span data-ttu-id="be329-201">Для начала выберите проект надстройки SharePoint (не проект веб-приложения) в **обозревателе решений** и скопируйте значение свойства **URL-адрес сайта**, включая протокол (например, **https://contoso.sharepoint.com**) в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="be329-201">To begin, select the SharePoint Add-in project (not the web application project) in  **Solution Explorer** and copy the value of the **Site URL** property, including the protocol (for example **https://contoso.sharepoint.com**) into the clipboard.</span></span> 
    
 
2. <span data-ttu-id="be329-202">Откройте манифест надстройки и вставьте URL-адрес в поле **Начальная страница**.</span><span class="sxs-lookup"><span data-stu-id="be329-202">Open the add-in manifest, and then paste the URL into the  **Start Page** box.</span></span>
    
 
3. <span data-ttu-id="be329-203">При необходимости можно удалить страницу Default.aspx из проекта веб-приложения, так как она не используется в надстройке SharePoint.</span><span class="sxs-lookup"><span data-stu-id="be329-203">Optionally, you can delete the Default.aspx page from the web application project, because it is not used in the SharePoint Add-in.</span></span>
    
 

### <a name="to-build-and-run-the-solution"></a><span data-ttu-id="be329-204">Для создания и запуска решения</span><span class="sxs-lookup"><span data-stu-id="be329-204">To build and run the solution</span></span>


1. <span data-ttu-id="be329-205">Нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="be329-205">Press the F5 key.</span></span>
    
     <span data-ttu-id="be329-206">**Примечание.** После нажатия клавиши F5 Visual Studio выполняет сборку решения, развертывает надстройку и открывает для нее страницу разрешений.</span><span class="sxs-lookup"><span data-stu-id="be329-206">**Note**  When you press F5, Visual Studio builds the solution, deploys the add-in, and opens the permissions page for the add-in.</span></span>
2. <span data-ttu-id="be329-p113">Нажмите кнопку **Доверять**. Откроется страница сайта разработчика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="be329-p113">Choose the  **Trust It** button. The default page of your developer site opens.</span></span>
    
 
3. <span data-ttu-id="be329-209">Перейдите в любую библиотеку документов на хост-сайте.</span><span class="sxs-lookup"><span data-stu-id="be329-209">Navigate to any document library in the host web.</span></span>
    
    <span data-ttu-id="be329-210">**Запуск дополнительного действия меню**</span><span class="sxs-lookup"><span data-stu-id="be329-210">**Launching a custom menu action**</span></span>

 

  ![Библиотека документов с открытой выноской для документа, меню, которое открывает кнопка выноски, и открытое меню "Дополнительно".](../images/477cecf5-03ff-46ff-9c25-a5f9a86d43f4.png)
 

 

 
4. <span data-ttu-id="be329-p114">Нажмите кнопку выноски (**...**) для любого документа. Откроется выноска.</span><span class="sxs-lookup"><span data-stu-id="be329-p114">Choose the callout button ( **...**) for any document. The callout opens.</span></span>
    
 
5. <span data-ttu-id="be329-214">Нажмите кнопку выноски (**...**) на выноске.</span><span class="sxs-lookup"><span data-stu-id="be329-214">Choose the callout button ( **...**) on the callout.</span></span> 
    
 
6. <span data-ttu-id="be329-215">Выберите **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="be329-215">Choose  **Advanced**.</span></span>
    
 
7. <span data-ttu-id="be329-p115">Выберите **Мое дополнительное действие меню** в контекстном меню. На открывшейся удаленной веб-странице вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="be329-p115">Choose  **My Custom Menu Action** in the context menu. You should see something like the following on the remote webpage that opens:</span></span>
    
    <span data-ttu-id="be329-218">**Удаленная веб-страница с параметрами из дополнительного действия**</span><span class="sxs-lookup"><span data-stu-id="be329-218">**Remote webpage with parameters from the custom action**</span></span>

 

  ![Веб-страница с параметрами из дополнительного действия](../images/CustomActions_target.png)
 

 

 
8. <span data-ttu-id="be329-220">Нажмите кнопку **Назад** в браузере, чтобы вернуться в библиотеку.</span><span class="sxs-lookup"><span data-stu-id="be329-220">Click the  **Back** button on your browser to return to the library.</span></span>
    
    <span data-ttu-id="be329-221">**Запуск дополнительного действия ленты**</span><span class="sxs-lookup"><span data-stu-id="be329-221">**Launching a custom ribbon action**</span></span>

 

  ![Библиотека документов с выбранным документом, открытой вкладкой "Файл" и дополнительной кнопкой на ленте.](../images/b315cb68-ff6a-4770-a1dc-738696ab71d2.png)
 

 

 
9. <span data-ttu-id="be329-223">Выберите любой документ.</span><span class="sxs-lookup"><span data-stu-id="be329-223">Select any document.</span></span>
    
 
10. <span data-ttu-id="be329-224">Откройте вкладку **Файл** на ленте.</span><span class="sxs-lookup"><span data-stu-id="be329-224">Open the  **File** tab on the ribbon.</span></span>
    
 
11. <span data-ttu-id="be329-p116">Выберите **Моя дополнительная кнопка ленты**. Отобразится та же удаленная веб-страница.</span><span class="sxs-lookup"><span data-stu-id="be329-p116">Choose  **My Custom Ribbon Button**. You see the same remote web page.</span></span>
    
 

<span data-ttu-id="be329-227">**Таблица 4. Поиск и устранение неполадок в решении**</span><span class="sxs-lookup"><span data-stu-id="be329-227">**Table 4. Troubleshooting the solution**</span></span>


|<span data-ttu-id="be329-228">**Проблема**</span><span class="sxs-lookup"><span data-stu-id="be329-228">**Problem**</span></span>|<span data-ttu-id="be329-229">**Решение**</span><span class="sxs-lookup"><span data-stu-id="be329-229">**Solution**</span></span>|
|:-----|:-----|
|<span data-ttu-id="be329-230">Visual Studio не открывает браузер после нажатия клавиши F5.</span><span class="sxs-lookup"><span data-stu-id="be329-230">Visual Studio does not open the browser after you press the F5 key.</span></span>|<span data-ttu-id="be329-231">Установите проект надстройки для SharePoint в качестве запускаемого проекта.</span><span class="sxs-lookup"><span data-stu-id="be329-231">Set the SharePoint Add-in project as the startup project.</span></span>|
|<span data-ttu-id="be329-232">Маркеры в URL-адресе не разрешаются после нажатия клавиши F5 в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be329-232">The tokens in the URL are not resolved after you press the F5 key in Visual Studio.</span></span>|<span data-ttu-id="be329-233">Перейдите на страницу **Контент сайта** на хост-сайте и щелкните значок надстройки.</span><span class="sxs-lookup"><span data-stu-id="be329-233">Go to the  **Site Contents** page in the host web, and click the icon for your add-in.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="be329-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be329-234">Next steps</span></span>
<span data-ttu-id="be329-235"><a name="SP15Createcustomactionsapps_Nextsteps"> </a></span><span class="sxs-lookup"><span data-stu-id="be329-235"></span></span>

<span data-ttu-id="be329-p117">В данной статье рассказывается, как создать дополнительное действие в надстройке для SharePoint. Далее вы можете изучить другие компоненты взаимодействия с пользователем, доступные в надстройках для SharePoint. Дополнительные сведения см. в указанных далее статьях.</span><span class="sxs-lookup"><span data-stu-id="be329-p117">This article demonstrated how to create a custom action in a SharePoint Add-in. As a next step, you can learn about other UX components that are available for SharePoint Add-ins. To learn more, see the following:</span></span>
 

 

-  [<span data-ttu-id="be329-238">Пример кода. Открытие удаленной веб-страницы надстройки с помощью дополнительного действия ECB</span><span class="sxs-lookup"><span data-stu-id="be329-238">Code sample: Open a remote add-in webpage using an ECB custom action</span></span>](http://code.msdn.microsoft.com/SharePoint-Open-e0ca1826)
    
 
-  [<span data-ttu-id="be329-239">SharePoint-Add-in-Localization</span><span class="sxs-lookup"><span data-stu-id="be329-239">SharePoint-Add-in-Localization</span></span>](https://github.com/OfficeDev/SharePoint-Add-in-Localization)
    
 
-  [<span data-ttu-id="be329-240">Пример кода. Использование дополнительных действий и междоменной библиотеки для заказа книг</span><span class="sxs-lookup"><span data-stu-id="be329-240">Code sample: Use custom actions and the cross-domain library to order books</span></span>](http://code.msdn.microsoft.com/SharePoint-Open-a-36d1598d)
    
 
-  [<span data-ttu-id="be329-241">Использование таблицы стилей веб-сайта SharePoint в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-241">Use a SharePoint website's style sheet in SharePoint Add-ins</span></span>](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="be329-242">Использование клиентского элемента управления хрома в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-242">Use the client chrome control in SharePoint Add-ins</span></span>](use-the-client-chrome-control-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="be329-243">Создание веб-частей надстроек для установки вместе с надстройкой SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-243">Create add-in parts to install with your SharePoint Add-in</span></span>](create-add-in-parts-to-install-with-your-sharepoint-add-in.md)
    
 

## <a name="additional-resources"></a><span data-ttu-id="be329-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="be329-244">Additional resources</span></span>
<span data-ttu-id="be329-245"><a name="SP15Createcustomactionsapps_AddResources"> </a></span><span class="sxs-lookup"><span data-stu-id="be329-245"><a name="SP15Createcustomactionsapps_AddResources"> </a></span></span>


-  [<span data-ttu-id="be329-246">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-246">Set up an on-premises development environment for SharePoint Add-ins</span></span>](set-up-an-on-premises-development-environment-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="be329-247">Разработка пользовательского интерфейса для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-247">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="be329-248">Рекомендации по проектированию пользовательского интерфейса надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-248">SharePoint Add-ins UX design guidelines</span></span>](sharepoint-add-ins-ux-design-guidelines.md)
    
 
-  [<span data-ttu-id="be329-249">Создание компонентов пользовательского интерфейса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-249">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="be329-250">Что следует рассмотреть, прежде чем приступать к разработке надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-250">Three ways to think about design options for SharePoint Add-ins</span></span>](three-ways-to-think-about-design-options-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="be329-251">Важные аспекты разработки и архитектуры для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="be329-251">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](important-aspects-of-the-sharepoint-add-in-architecture-and-development-landscap.md)
    
 

