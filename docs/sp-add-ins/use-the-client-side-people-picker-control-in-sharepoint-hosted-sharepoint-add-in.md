---
title: "Использование клиентского элемента управления \"Выбор людей\" в надстройках SharePoint с размещением в SharePoint"
description: "Используйте клиентское средство выбора людей для быстрого поиска и выбора действительных учетных записей для людей, групп и утверждений в организации."
ms.date: 12/20/2017
ms.prod: sharepoint
ms.openlocfilehash: 6abffcc1451b7cc6262e068fbbc29a751a067fe7
ms.sourcegitcommit: 6f2b3b5bd81c2de4f761e10ed5e2f0b9c3c485bf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins"></a><span data-ttu-id="442a8-103">Использование клиентского средства выбора людей в надстройках SharePoint с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="442a8-103">Use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="442a8-104">В этой статье предполагается, что вы знаете,</span><span class="sxs-lookup"><span data-stu-id="442a8-104">Important  This topic assumes that you know how to create a SharePoint-hosted SharePoint Add-in. To learn how to create one, start at  Get started creating provider-hosted SharePoint Add-ins.</span></span> <span data-ttu-id="442a8-105">[как создать надстройку SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="442a8-105">To learn how to create one, see [Get started creating SharePoint-hosted SharePoint Add-ins](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).</span></span>
 
<span data-ttu-id="442a8-106"><a name="bk_whatIs"> </a></span><span class="sxs-lookup"><span data-stu-id="442a8-106"></span></span>

## <a name="what-is-the-client-side-people-picker-control-in-sharepoint"></a><span data-ttu-id="442a8-107">Что представляет собой клиентское средство выбора людей в SharePoint?</span><span class="sxs-lookup"><span data-stu-id="442a8-107">What is the client-side People Picker control in SharePoint?</span></span>

<span data-ttu-id="442a8-108">Клиентское средство выбора людей позволяет пользователям быстро находить действительные учетные записи для людей, групп и утверждений в организации.</span><span class="sxs-lookup"><span data-stu-id="442a8-108">Learn how to use the client-side People Picker control in SharePoint Add-ins. The client-side People Picker control lets users quickly search for and select valid user accounts for people, groups, and claims in their organization. The picker is an HTML and JavaScript control that provides cross-browser support.</span></span> <span data-ttu-id="442a8-109">Средство выбора представляет собой элемент управления HTML и JavaScript, работающий в разных браузерах.</span><span class="sxs-lookup"><span data-stu-id="442a8-109">The picker is an HTML and JavaScript control that provides cross-browser support.</span></span> 

<span data-ttu-id="442a8-110">Добавить средство выбора в надстройку легко:</span><span class="sxs-lookup"><span data-stu-id="442a8-110">Adding the picker to your add-in is easy:</span></span> 

1. <span data-ttu-id="442a8-111">В коде добавьте элемент контейнера для этого элемента управления, а также ссылки на последний и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="442a8-111">In your markup, add a container element for the control and references for the control and its dependencies.</span></span> 

2. <span data-ttu-id="442a8-112">В скрипт добавьте вызов глобальной функции **SPClientPeoplePicker_InitStandaloneControlWrapper** для отрисовки и инициализации средства выбора.</span><span class="sxs-lookup"><span data-stu-id="442a8-112">In your script, call the **SPClientPeoplePicker_InitStandaloneControlWrapper** global function to render and initialize the picker.</span></span>

<span data-ttu-id="442a8-113">Средство выбора представлено объектом **SPClientPeoplePicker**, предоставляющим методы, которые другие клиентские элементы управления могут использовать для получения сведений из этого средства выбора или для выполнения других действий.</span><span class="sxs-lookup"><span data-stu-id="442a8-113">The picker is represented by the **SPClientPeoplePicker** object, which provides methods that other client-side controls can use to get information from the picker or to perform other operations.</span></span> <span data-ttu-id="442a8-114">С помощью свойств объекта **SPClientPeoplePicker** можно настроить соответствующие параметры этого средства выбора (например, разрешить выбор нескольких пользователей или указать параметры кэширования).</span><span class="sxs-lookup"><span data-stu-id="442a8-114">You can use **SPClientPeoplePicker** properties to configure the picker with control-specific settings, such as allowing multiple users or specifying caching options.</span></span> 

<span data-ttu-id="442a8-115">Данное средство выбора также использует параметры конфигурации веб-приложений, в частности параметры доменных служб Active Directory или параметры целевых лесов.</span><span class="sxs-lookup"><span data-stu-id="442a8-115">The picker also uses web application configuration settings such as Active Directory Domain Services parameters or targeted forests.</span></span> <span data-ttu-id="442a8-116">Параметры конфигурации веб-приложений собираются автоматически (из свойства **SPWebApplication.PeoplePickerSettings**).</span><span class="sxs-lookup"><span data-stu-id="442a8-116">Web application configuration settings are picked up automatically (from the **SPWebApplication.PeoplePickerSettings** property).</span></span>
 
<span data-ttu-id="442a8-117">Средство выбора включает следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="442a8-117">The picker has the following components:</span></span>

- <span data-ttu-id="442a8-118">Текстовое поле для ввода имен пользователей, групп и утверждений.</span><span class="sxs-lookup"><span data-stu-id="442a8-118">An input text box to enter names for users, groups, and claims.</span></span>
- <span data-ttu-id="442a8-119">Элемент управления "Интервал", в котором отображаются имена сопоставленных пользователей, групп и требований.</span><span class="sxs-lookup"><span data-stu-id="442a8-119">A span control that shows the names of resolved users, groups, and claims.</span></span>
- <span data-ttu-id="442a8-120">Скрытый элемент **div**, который автоматически заполняет раскрывающийся список соответствующими результатами запроса.</span><span class="sxs-lookup"><span data-stu-id="442a8-120">A hidden **div** element that autofills a drop-down box with matching query results.</span></span>
- <span data-ttu-id="442a8-121">Элемент управления для автозаполнения.</span><span class="sxs-lookup"><span data-stu-id="442a8-121">An autofill control.</span></span>
    
> [!NOTE] 
> <span data-ttu-id="442a8-122">Средство выбора и его функциональность заданы в файлах сценариев **clientforms.js**, **clientpeoplepicker.js** и **autofill.js**, которые расположены в папке %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS на сервере.</span><span class="sxs-lookup"><span data-stu-id="442a8-122">Note  The picker and its functionality are defined in the  **clientforms.js**,  **clientpeoplepicker.js**, and  **autofill.js** script files, which are located in the %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS folder on the server.</span></span>
 
<span data-ttu-id="442a8-123"><a name="bk_prereqs"> </a></span><span class="sxs-lookup"><span data-stu-id="442a8-123"></span></span>

## <a name="prerequisites-for-setting-up-your-development-environment-to-use-the-client-side-people-picker-control-in-a-sharepoint-add-in"></a><span data-ttu-id="442a8-124">Требования к среде разработки для использования клиентского средства выбора людей в надстройке SharePoint</span><span class="sxs-lookup"><span data-stu-id="442a8-124">Prerequisites for setting up your development environment to use the client-side People Picker control in a SharePoint Add-in 2013</span></span>

<span data-ttu-id="442a8-125">В этой статье предполагается, что вы создаете надстройку для SharePoint, используя Napa на сайте разработчика Office 365.</span><span class="sxs-lookup"><span data-stu-id="442a8-125">This article assumes that you create the SharePoint Add-in by using Napa on an Office 365 Developer Site. If you're using this development environment, you've already met the prerequisites.</span></span> <span data-ttu-id="442a8-126">Если вы используете эту среду разработки, у вас уже установлены необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="442a8-126">If you're using this development environment, you've already met the prerequisites.</span></span>
 
> [!NOTE] 
> <span data-ttu-id="442a8-127">Сведения о том, как зарегистрировать сайт разработчика и начать использовать Napa, см. в статье [Настройка среды разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md).</span><span class="sxs-lookup"><span data-stu-id="442a8-127">To find out how to sign up for a developer site and start using Napa, see [Set up a development environment for SharePoint Add-ins on Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md).</span></span>
 
<span data-ttu-id="442a8-128">Если вы не используете Napa на сайте разработчика, вам потребуется следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="442a8-128">If you're not using Napa on a Developer Site, you'll need the following:</span></span>

- <span data-ttu-id="442a8-129">SharePoint хотя бы с одним пользователем;</span><span class="sxs-lookup"><span data-stu-id="442a8-129">SharePoint with at least one target user</span></span>
- <span data-ttu-id="442a8-130">Visual Studio 2012 или Visual Studio 2013;</span><span class="sxs-lookup"><span data-stu-id="442a8-130">Visual Studio 2012 or Visual Studio 2013</span></span>
- <span data-ttu-id="442a8-131">Инструменты разработчика Office для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="442a8-131">Office Developer Tools for Visual Studio 2013</span></span>
    
> [!NOTE] 
> <span data-ttu-id="442a8-132">Рекомендации по настройке подходящей среды разработки см. в статье [Надстройки SharePoint](sharepoint-add-ins.md#two-types-of-sharepoint-add-ins-sharepoint-hosted-and-provider-hosted).</span><span class="sxs-lookup"><span data-stu-id="442a8-132">Note  For guidance about how to set up a development environment that fits your needs, see  Start building Office and SharePoint Add-ins.</span></span>
 
<span data-ttu-id="442a8-133">В приведенных ниже разделах указаны общие инструкции по добавлению средства выбора в надстройку и получению сведений о пользователях из другого клиентского элемента управления.</span><span class="sxs-lookup"><span data-stu-id="442a8-133">The following steps describe the high-level steps for adding the picker to your add-in and then getting its user information from another client-side control. See  Code example: Using the client-side People Picker for the corresponding code.</span></span> <span data-ttu-id="442a8-134">Соответствующий код см. в разделе [Пример кода: использование клиентского средства выбора людей](#bk_example).</span><span class="sxs-lookup"><span data-stu-id="442a8-134">For the corresponding code, see [Code example: Using the client-side People Picker](#bk_example).</span></span>

<span data-ttu-id="442a8-135">Клиентское средство выбора людей можно использовать в надстройках SharePoint с размещением в SharePoint, но не в надстройках с размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="442a8-135">You can use the client-side People Picker control in SharePoint-hosted SharePoint Add-ins, but not in provider-hosted add-ins. For a sample that shows how to implement a people-picker control in a provider-hosted add-in, download the  Office Add-in Model Samples.</span></span> 

<span data-ttu-id="442a8-136"><a name="bk_steps"> </a></span><span class="sxs-lookup"><span data-stu-id="442a8-136"></span></span>

## <a name="use-the-client-side-people-picker-control-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="442a8-137">Использование клиентского средства выбора людей в надстройке с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="442a8-137">Use the client-side People Picker control in a SharePoint-hosted add-in</span></span>

### <a name="in-your-page-markup"></a><span data-ttu-id="442a8-138">В разметке страницы</span><span class="sxs-lookup"><span data-stu-id="442a8-138">In your page markup</span></span>

1. <span data-ttu-id="442a8-139">Добавьте ссылки в раздел зависимостей скриптов клиентского элемента управления "Выбор людей".</span><span class="sxs-lookup"><span data-stu-id="442a8-139">Add references to the client-side People Picker control's script dependencies.</span></span>

2. <span data-ttu-id="442a8-p107">Добавьте теги HTML для пользовательского интерфейса страницы. В надстройке из данного примера задается два элемента **div**: один для отображения элемента управления выбора и второй для пользовательского интерфейса кнопка, вызывающая скрипт для запроса этого элемента управления выбора и элементов, отображающих данные о пользователе.</span><span class="sxs-lookup"><span data-stu-id="442a8-p107">Add the HTML tags for the page UI. The add-in in this example defines two **div** elements: one for the picker to render in and one for the UI: a button that invokes script to query the picker and the elements that display user information.</span></span>
    
### <a name="in-your-script"></a><span data-ttu-id="442a8-142">В скрипте</span><span class="sxs-lookup"><span data-stu-id="442a8-142">In your script</span></span>

1. <span data-ttu-id="442a8-143">Создайте словарь JSON для использования в качестве схемы, в которой хранятся свойства этого элемента управления выбора, такие как **AllowMultipleValues** и **MaximumEntitySuggestions**.</span><span class="sxs-lookup"><span data-stu-id="442a8-143">Create a JSON dictionary to use as a schema that stores picker-specific properties, such as **AllowMultipleValues** and **MaximumEntitySuggestions**.</span></span>

2. <span data-ttu-id="442a8-144">Вызовите глобальную функцию **SPClientPeoplePicker_InitStandaloneControlWrapper**.</span><span class="sxs-lookup"><span data-stu-id="442a8-144">Call the **SPClientPeoplePicker_InitStandaloneControlWrapper** global function.</span></span>

3. <span data-ttu-id="442a8-145">Получите объект средства выбора на странице.</span><span class="sxs-lookup"><span data-stu-id="442a8-145">Get the picker object from the page.</span></span>

4. <span data-ttu-id="442a8-146">Отправьте запрос средству выбора.</span><span class="sxs-lookup"><span data-stu-id="442a8-146">Query the picker.</span></span> <span data-ttu-id="442a8-147">Надстройка в этом примере вызывает метод **GetAllUserInfo** для получения всех сведений о сопоставленных пользователях, а также метод **GetAllUserKeys** для получения ключей для этих сопоставленных пользователей.</span><span class="sxs-lookup"><span data-stu-id="442a8-147">Query the picker. The add-in in this example calls the **GetAllUserInfo** method to get all user information for the resolved users and the **GetAllUserKeys** method to just get the keys for the resolved users.</span></span>

5. <span data-ttu-id="442a8-p109">Получите ИД пользователя с помощью объектной модели JavaScript. ИД пользователя не включается в данные, которое возвращается элементом выбора, поэтому надстройка вызывает метод **SP.Web.ensureUser** и получает ИД от возвращенного объекта **SP.User**.</span><span class="sxs-lookup"><span data-stu-id="442a8-p109">Get the user ID by using the JavaScript object model. The user ID isn't included in the information that's returned by the picker, so the add-in calls the **SP.Web.ensureUser** method and gets the ID from the returned **SP.User** object.</span></span>

<span data-ttu-id="442a8-150">Отображение, инициализация и другая функциональность для элемента управления выбора обрабатывается на сервере, включая поиск и разрешение ввода пользователя при работе с поставщиками проверки подлинности SharePoint.</span><span class="sxs-lookup"><span data-stu-id="442a8-150">Rendering, initializing, and other functionality for the picker are handled by the server, including searching and resolving user input against the SharePoint authentication providers.</span></span>
 
<span data-ttu-id="442a8-151"><a name="bk_example"> </a></span><span class="sxs-lookup"><span data-stu-id="442a8-151"></span></span>

## <a name="code-example-using-the-client-side-people-picker-in-a-sharepoint-hosted-add-in"></a><span data-ttu-id="442a8-152">Пример кода: использование клиентского средства выбора людей в надстройке с размещением в SharePoint</span><span class="sxs-lookup"><span data-stu-id="442a8-152">Code example: Using the client-side People Picker in a SharePoint-hosted add-in</span></span>

<span data-ttu-id="442a8-153">Примеры кода HTML и JavaScript, приведенные ниже, добавляют клиентское средство выбора людей в надстройку с размещением в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="442a8-153">The following HTML and JavaScript code examples add a client-side People Picker control to a SharePoint-hosted add-in.</span></span>

<span data-ttu-id="442a8-154">В первом примере показана разметка страницы для тегов **PlaceHolderMain asp:Content** на странице Default.aspx.</span><span class="sxs-lookup"><span data-stu-id="442a8-154">The first example shows the page markup for the  **PlaceHolderMainasp:Content** tags in the Default.aspx page. This code references the picker's script dependencies, gives a unique ID to the DOM element where the picker will render, and defines the add-in's UI.</span></span> <span data-ttu-id="442a8-155">Этот код ссылается на зависимости в скрипте средства выбора, присваивает уникальный идентификатор элементу DOM, содержащему средство выбора, и определяет пользовательский интерфейс надстройки.</span><span class="sxs-lookup"><span data-stu-id="442a8-155">The first example shows the page markup for the  PlaceHolderMainasp:Content tags in the Default.aspx page. This code references the picker's script dependencies, gives a unique ID to the DOM element where the picker will render, and defines the add-in's UI.</span></span>

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

<br/>

> [!NOTE] 
> <span data-ttu-id="442a8-156">В зависимости от используемой среды вам, возможно, не потребуется явно ссылаться на все эти зависимости.</span><span class="sxs-lookup"><span data-stu-id="442a8-156">Depending on your environment, you might not have to explicitly reference all of these dependencies.</span></span>
 
<br/>

<span data-ttu-id="442a8-157">В приведенном ниже примере показан **скрипт из файла App.js**.</span><span class="sxs-lookup"><span data-stu-id="442a8-157">The following example shows the **script from the App.js file**.</span></span> <span data-ttu-id="442a8-158">Этот скрипт инициализирует и отрисовывает средство выбора, а затем запрашивает информацию о пользователях и получает ИД пользователя, используя объектную модель JavaScript.</span><span class="sxs-lookup"><span data-stu-id="442a8-158">The following example shows the script from the App.js file. This script initializes and renders the picker, queries it for user information, and then gets the user ID by using the JavaScript object model.</span></span>

```js

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

<br/>

## <a name="see-also"></a><span data-ttu-id="442a8-159">См. также</span><span class="sxs-lookup"><span data-stu-id="442a8-159">See also</span></span>
<span data-ttu-id="442a8-160"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="442a8-160"></span></span>

-  [<span data-ttu-id="442a8-161">Создание компонентов пользовательского интерфейса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="442a8-161">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
-  [<span data-ttu-id="442a8-162">Общие сведения о средстве выбора людей и поставщиках требований (SharePoint)</span><span class="sxs-lookup"><span data-stu-id="442a8-162">People Picker and claims providers overview (SharePoint)</span></span>](http://technet.microsoft.com/library/gg602078.aspx)
-  [<span data-ttu-id="442a8-163">Настройка средства выбора людей в SharePoint</span><span class="sxs-lookup"><span data-stu-id="442a8-163">Configure People Picker in SharePoint</span></span>](http://technet.microsoft.com/library/gg602075.aspx)
    
 

