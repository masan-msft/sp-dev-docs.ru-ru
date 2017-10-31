---
title: "Использование клиентского элемента управления \"Выбор людей\" в надстройках SharePoint с размещением в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: ab5c3d1cb7c47518a4806af2fc075f1730e53399
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="d3288-102">Использование клиентского элемента управления "Выбор людей" в надстройках SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3288-102">Use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins</span></span>
<span data-ttu-id="d3288-103">В этой статье рассказывается, как использовать клиентский элемент управления "Выбор людей" в надстройках SharePoint, размещаемых в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3288-103">Learn how to use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins.</span></span>
 

 <span data-ttu-id="d3288-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="d3288-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


 <span data-ttu-id="d3288-p102">**Важно!** В этой статье предполагается, что вы умеете создавать надстройки SharePoint, размещаемые в SharePoint. Чтобы узнать, как это сделать, изучите статью [Приступая к созданию надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="d3288-p102">**Important**  This topic assumes that you know how to create a SharePoint-hosted SharePoint Add-in. To learn how to create one, start at  [Get started creating provider-hosted SharePoint Add-ins](get-started-creating-provider-hosted-sharepoint-add-ins.md).</span></span>
 


## <a name="what-is-the-client-side-people-picker-control-in-sharepoint"></a><span data-ttu-id="d3288-109">Что представляет собой клиентский элемент управления "Выбор людей" в SharePoint?</span><span class="sxs-lookup"><span data-stu-id="d3288-109">What is the client-side People Picker control in SharePoint?</span></span>
<span data-ttu-id="d3288-110"><a name="bk_whatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="d3288-110"><a name="bk_whatIs"> </a></span></span>

<span data-ttu-id="d3288-p103">Клиентский элемент управления "Выбор людей" дает пользователям возможность быстро искать и выбирать допустимые учетные записи пользователей для людей, групп и требований в организации. Средство выбора представляет собой элемент управления HTML и JavaScript, работающий в разных браузерах. Средство выбора несложно добавить в надстройку: добавьте в разметку элемент-контейнер для этого элемента управления, ссылки на него и его зависимости. Затем в скрипте вызовите глобальную функцию **SPClientPeoplePicker_InitStandaloneControlWrapper** для отображения и инициализации этого средства выбора.</span><span class="sxs-lookup"><span data-stu-id="d3288-p103">The client-side People Picker control lets users quickly search for and select valid user accounts for people, groups, and claims in their organization. The picker is an HTML and JavaScript control that provides cross-browser support. Adding the picker to your add-in is easy: In your markup, add a container element for the control and references for the control and its dependencies. Then in your script, call the  **SPClientPeoplePicker_InitStandaloneControlWrapper** global function to render and initialize the picker.</span></span>
 

 
<span data-ttu-id="d3288-p104">Средство выбора представлено объектом **SPClientPeoplePicker**, предоставляющим методы, которые другие клиентские элементы управления могут использовать для получения сведений из этого средства выбора или для выполнения других действий. С помощью свойств объекта **SPClientPeoplePicker** можно настроить соответствующие параметры этого средства выбора, например разрешить выбор нескольких пользователей или указать параметры кэширования. Данное средство выбора также использует параметры конфигурации веб-приложений, в частности параметры доменных служб Active Directory или параметры лесов назначения. Параметры конфигурации веб-приложений собираются автоматически (из свойства **SPWebApplication.PeoplePickerSettings**).</span><span class="sxs-lookup"><span data-stu-id="d3288-p104">The picker is represented by the  **SPClientPeoplePicker** object, which provides methods that other client-side controls can use to get information from the picker or to perform other operations. You can use **SPClientPeoplePicker** properties to configure the picker with control-specific settings, such as allowing multiple users or specifying caching options. The picker also uses web application configuration settings such as Active Directory Domain Services parameters or targeted forests. Web application configuration settings are picked up automatically (from the **SPWebApplication.PeoplePickerSettings** property).</span></span>
 

 
<span data-ttu-id="d3288-119">Средство выбора включает указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="d3288-119">The picker has the following components:</span></span>
 

 

- <span data-ttu-id="d3288-120">Текстовое поле для ввода имен пользователей, групп и утверждений.</span><span class="sxs-lookup"><span data-stu-id="d3288-120">An input text box to enter names for users, groups, and claims.</span></span>
    
 
- <span data-ttu-id="d3288-121">Элемент управления "Интервал", в котором отображаются имена сопоставленных пользователей, групп и требований.</span><span class="sxs-lookup"><span data-stu-id="d3288-121">A span control that shows the names of resolved users, groups, and claims.</span></span>
    
 
- <span data-ttu-id="d3288-122">Скрытый элемент **div**, который автоматически заполняет раскрывающийся список соответствующими результатами запросов.</span><span class="sxs-lookup"><span data-stu-id="d3288-122">A hidden  **div** element that autofills a drop-down box with matching query results.</span></span>
    
 
- <span data-ttu-id="d3288-123">Элемент управления для автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="d3288-123">An autofill control.</span></span>
    
 

 <span data-ttu-id="d3288-124">**Примечание.** Средство выбора и его функциональность заданы в файлах скриптов **clientforms.js**, **clientpeoplepicker.js** и **autofill.js**, которые расположены в папке %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS на сервере.</span><span class="sxs-lookup"><span data-stu-id="d3288-124">**Note**  The picker and its functionality are defined in the  **clientforms.js**,  **clientpeoplepicker.js**, and  **autofill.js** script files, which are located in the %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS folder on the server.</span></span>
 


## <a name="prerequisites-for-setting-up-your-development-environment-to-use-the-client-side-people-picker-control-in-a-sharepoint-add-in-2013"></a><span data-ttu-id="d3288-125">Компоненты, необходимые для настройки среды разработки, чтобы можно было использовать клиентский элемент управления "Выбор людей" в надстройке SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="d3288-125">Prerequisites for setting up your development environment to use the client-side People Picker control in a SharePoint Add-in 2013</span></span>
<span data-ttu-id="d3288-126"><a name="bk_prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="d3288-126"><a name="bk_prereqs"> </a></span></span>

<span data-ttu-id="d3288-p105">В этой статье предполагается, что вы создаете надстройку для SharePoint с помощью Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, то необходимые условия выполняются.</span><span class="sxs-lookup"><span data-stu-id="d3288-p105">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span>
 

 

 <span data-ttu-id="d3288-129">**Примечание.** Сведения о том, как зарегистрировать Сайт разработчика и начать использовать Napa, см. в статье [Настройка среды разработки для надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md).</span><span class="sxs-lookup"><span data-stu-id="d3288-129">**Note**  Go to  [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md) to find out how to sign up for a Developer Site and start using Napa.</span></span>
 

<span data-ttu-id="d3288-130">Если вы не используете Napa на Сайте разработчика, вам потребуется выполнить указанные ниже компоненты.</span><span class="sxs-lookup"><span data-stu-id="d3288-130">If you're not using Napa on a Developer Site, you'll need the following:</span></span>
 

 

- <span data-ttu-id="d3288-131">SharePoint хотя бы с одним конечным пользователем;</span><span class="sxs-lookup"><span data-stu-id="d3288-131">SharePoint with at least one target user</span></span>
    
 
- <span data-ttu-id="d3288-132">Visual Studio 2012 или Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d3288-132">Visual Studio 2012 or Visual Studio 2013</span></span>
    
 
- <span data-ttu-id="d3288-133">Инструменты разработчика Office для Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d3288-133">Office Developer Tools for Visual Studio 2013</span></span>
    
 

 <span data-ttu-id="d3288-134">**Примечание.** Рекомендации по настройке среды разработки согласно вашим потребностям см. в статье [Начало создания надстроек Office и SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3288-134">**Note**  For guidance about how to set up a development environment that fits your needs, see  [Start building Office and SharePoint Add-ins](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).</span></span>
 

<span data-ttu-id="d3288-p106">В следующих действиях описываются общие действия для добавления элемента управления выбора в надстройку и последующего получения ее сведений о пользователях в другом клиентском элементе управления. Соответствующий код можно найти в разделе  [Пример кода. Использование клиентского элемента управления "Выбор людей"](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-in.md#bk_example).</span><span class="sxs-lookup"><span data-stu-id="d3288-p106">The following steps describe the high-level steps for adding the picker to your add-in and then getting its user information from another client-side control. See  [Code example: Using the client-side People Picker](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-in.md#bk_example) for the corresponding code.</span></span>
 

 
<span data-ttu-id="d3288-137">Клиентский элемент управления "Выбор людей" можно использовать в приложениях для SharePoint с размещением в SharePoint, но невозможно использовать в надстройках с размещением у поставщика. Пример реализации элемента управления "Выбор людей" в надстройке с размещением у поставщика можно скачать на веб-сайте  [Примеры модели надстроек Office](http://officeams.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="d3288-137">You can use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins, but not in provider-hosted add-ins. For a sample that shows how to implement a people-picker control in a provider-hosted add-in, download the  [Office Add-in Model Samples](http://officeams.codeplex.com).</span></span>
 

 

## <a name="use-the-client-side-people-picker-control-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="d3288-138">Использование клиентского элемента управления "Выбор людей" в надстройках, размещаемых в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3288-138">Use the client-side People Picker control in a SharePoint-hosted add-in</span></span>
<span data-ttu-id="d3288-139"><a name="bk_steps"> </a></span><span class="sxs-lookup"><span data-stu-id="d3288-139"><a name="bk_steps"> </a></span></span>


### <a name="in-your-page-markup"></a><span data-ttu-id="d3288-140">В разметке страницы</span><span class="sxs-lookup"><span data-stu-id="d3288-140">In your page markup</span></span>


1. <span data-ttu-id="d3288-141">Добавьте ссылки в раздел зависимостей скриптов клиентского элемента управления "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="d3288-141">Add references to the client-side People Picker control's script dependencies.</span></span>
    
 
2. <span data-ttu-id="d3288-p107">Добавьте HTML-теги для пользовательского интерфейса страницы. В надстройке в этом примере заданы два элемента **div**: один для отображения средства выбора и второй для пользовательского интерфейса — кнопка, вызывающая скрипт для запроса средства выбора и элементов, отображающих сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="d3288-p107">Add the HTML tags for the page UI. The add-in in this example defines two  **div** elements: one for the picker to render in and one for the UI: a button that invokes script to query the picker and the elements that display user information.</span></span>
    
 

### <a name="in-your-script"></a><span data-ttu-id="d3288-144">В скрипте</span><span class="sxs-lookup"><span data-stu-id="d3288-144">In your script</span></span>


1. <span data-ttu-id="d3288-145">Создайте словарь JSON для использования в качестве схемы, в которой хранятся свойства этого средства выбора, например **AllowMultipleValues** и **MaximumEntitySuggestions**.</span><span class="sxs-lookup"><span data-stu-id="d3288-145">Create a JSON dictionary to use as a schema that stores picker-specific properties, such as  **AllowMultipleValues** and **MaximumEntitySuggestions**.</span></span>
    
 
2. <span data-ttu-id="d3288-146">Вызовите глобальную функцию **SPClientPeoplePicker_InitStandaloneControlWrapper**.</span><span class="sxs-lookup"><span data-stu-id="d3288-146">Call the  **SPClientPeoplePicker_InitStandaloneControlWrapper** global function.</span></span>
    
 
3. <span data-ttu-id="d3288-147">Получите объект средства выбора на странице.</span><span class="sxs-lookup"><span data-stu-id="d3288-147">Get the picker object from the page.</span></span>
    
 
4. <span data-ttu-id="d3288-p108">Отправьте запрос в средство выбора. В надстройке в этом примере метод **GetAllUserInfo** вызывается для получения всех сведений о сопоставленных пользователях, а метод **GetAllUserKeys** — для получения ключей для этих сопоставленных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d3288-p108">Query the picker. The add-in in this example calls the  **GetAllUserInfo** method to get all user information for the resolved users and the **GetAllUserKeys** method to just get the keys for the resolved users.</span></span>
    
 
5. <span data-ttu-id="d3288-p109">Получите идентификатор пользователя с помощью объектной модели JavaScript. Идентификатор пользователя не включается в данные, возвращаемые средством выбора, поэтому надстройка вызывает метод **SP.Web.ensureUser** и получает идентификатор от возвращенного объекта **SP.User**.</span><span class="sxs-lookup"><span data-stu-id="d3288-p109">Get the user ID by using the JavaScript object model. The user ID isn't included in the information that's returned by the picker, so the add-in calls the  **SP.Web.ensureUser** method and gets the ID from the returned **SP.User** object.</span></span>
    
 
<span data-ttu-id="d3288-152">Отображение, инициализация и другая функциональность для элемента управления выбора обрабатывается на сервере, включая поиск и разрешение ввода пользователя при работе с поставщиками проверки подлинности SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3288-152">Rendering, initializing, and other functionality for the picker are handled by the server, including searching and resolving user input against the SharePoint authentication providers.</span></span>
 

 

## <a name="code-example-using-the-client-side-people-picker-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="d3288-153">Пример кода: использование клиентского элемента управления "Выбор людей" в надстройке, размещаемой в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3288-153">Code example: Using the client-side People Picker in a SharePoint-hosted add-in</span></span>
<span data-ttu-id="d3288-154"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="d3288-154"><a name="bk_example"> </a></span></span>

<span data-ttu-id="d3288-155">В примерах кода HTML и JavaScript ниже показано, как добавить клиентский элемент управления "Выбор людей" в надстройку, размещаемую в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d3288-155">The following HTML and JavaScript code examples add a client-side People Picker control to a SharePoint-hosted add-in.</span></span>
 

 
<span data-ttu-id="d3288-p110">В первом примере показана разметка страницы для тегов **PlaceHolderMain****asp:Content** на странице Default.aspx. Этот код ссылается на зависимости в скрипте средства выбора, передает уникальный идентификатор в элемент DOM, в котором будет отображаться средство выбора, и задает пользовательский интерфейс надстройки.</span><span class="sxs-lookup"><span data-stu-id="d3288-p110">The first example shows the page markup for the  **PlaceHolderMain** **asp:Content** tags in the Default.aspx page. This code references the picker's script dependencies, gives a unique ID to the DOM element where the picker will render, and defines the add-in's UI.</span></span>
 

 



```HTML
<asp:Content ContentPlaceHolderId="PlaceHolderMain" runat="server">
    <SharePoint:ScriptLink name="clienttemplates.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="clientforms.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="clientpeoplepicker.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="autofill.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="sp.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="sp.runtime.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <SharePoint:ScriptLink name="sp.core.js" runat="server" LoadAfterUI="true" Localizable="false" />
    <div id="peoplePickerDiv"></div>
    <div>
        <br/>
        <input type="button" value="Get User Info" onclick="getUserInfo()"></input>
        <br/>
        <h1>User info:</h1>
        <p id="resolvedUsers"></p>
        <h1>User keys:</h1>
        <p id="userKeys"></p> 
        <h1>User ID:</h1>
        <p id="userId"></p>
    </div>
</asp:Content>
```


 <span data-ttu-id="d3288-158">**Примечание.** В зависимости от используемой среды вам, возможно, не потребуется явно ссылаться на все эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="d3288-158">**Note**  Depending on your environment, you might not have to explicitly reference all of these dependencies.</span></span>
 

<span data-ttu-id="d3288-p111">В следующем примере показан скрипт для файла App.js. Этот скрипт инициализирует и отображает элемент управления выбора, а затем запрашивает у него пользовательские сведения и получает ИД пользователя с помощью объектной модели JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d3288-p111">The following example shows the script from the App.js file. This script initializes and renders the picker, queries it for user information, and then gets the user ID by using the JavaScript object model.</span></span>
 

 



```
// Run your custom code when the DOM is ready.
$(document).ready(function () {

    // Specify the unique ID of the DOM element where the
    // picker will render.
    initializePeoplePicker('peoplePickerDiv');
});

// Render and initialize the client-side People Picker.
function initializePeoplePicker(peoplePickerElementId) {

    // Create a schema to store picker properties, and set the properties.
    var schema = {};
    schema['PrincipalAccountType'] = 'User,DL,SecGroup,SPGroup';
    schema['SearchPrincipalSource'] = 15;
    schema['ResolvePrincipalSource'] = 15;
    schema['AllowMultipleValues'] = true;
    schema['MaximumEntitySuggestions'] = 50;
    schema['Width'] = '280px';

    // Render and initialize the picker. 
    // Pass the ID of the DOM element that contains the picker, an array of initial
    // PickerEntity objects to set the picker value, and a schema that defines
    // picker properties.
    this.SPClientPeoplePicker_InitStandaloneControlWrapper(peoplePickerElementId, null, schema);
}

// Query the picker for user information.
function getUserInfo() {

    // Get the people picker object from the page.
    var peoplePicker = this.SPClientPeoplePicker.SPClientPeoplePickerDict.peoplePickerDiv_TopSpan;

    // Get information about all users.
    var users = peoplePicker.GetAllUserInfo();
    var userInfo = '';
    for (var i = 0; i < users.length; i++) {
        var user = users[i];
        for (var userProperty in user) { 
            userInfo += userProperty + ':  ' + user[userProperty] + '<br>';
        }
    }
    $('#resolvedUsers').html(userInfo);

    // Get user keys.
    var keys = peoplePicker.GetAllUserKeys();
    $('#userKeys').html(keys);

    // Get the first user's ID by using the login name.
    getUserId(users[0].Key);
}

// Get the user ID.
function getUserId(loginName) {
    var context = new SP.ClientContext.get_current();
    this.user = context.get_web().ensureUser(loginName);
    context.load(this.user);
    context.executeQueryAsync(
         Function.createDelegate(null, ensureUserSuccess), 
         Function.createDelegate(null, onFail)
    );
}

function ensureUserSuccess() {
    $('#userId').html(this.user.get_id());
}

function onFail(sender, args) {
    alert('Query failed. Error: ' + args.get_message());
}
```


## <a name="additional-resources"></a><span data-ttu-id="d3288-161">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3288-161">Additional resources</span></span>
<span data-ttu-id="d3288-162"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d3288-162"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="d3288-163">Создание компонентов пользовательского интерфейса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3288-163">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="d3288-164">Общие сведения о средстве выбора людей и поставщиках требований (SharePoint)</span><span class="sxs-lookup"><span data-stu-id="d3288-164">People Picker and claims providers overview (SharePoint)</span></span>](http://technet.microsoft.com/library/gg602078.aspx)
    
 
-  [<span data-ttu-id="d3288-165">Настройка средства выбора людей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d3288-165">Configure People Picker in SharePoint</span></span>](http://technet.microsoft.com/library/gg602075.aspx)
    
 

