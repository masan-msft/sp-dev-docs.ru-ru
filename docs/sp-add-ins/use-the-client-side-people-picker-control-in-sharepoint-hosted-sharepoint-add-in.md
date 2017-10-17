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
# <a name="use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins"></a>Использование клиентского элемента управления "Выбор людей" в надстройках SharePoint с размещением в SharePoint
В этой статье рассказывается, как использовать клиентский элемент управления "Выбор людей" в надстройках SharePoint, размещаемых в SharePoint.
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 


 **Важно!** В этой статье предполагается, что вы умеете создавать надстройки SharePoint, размещаемые в SharePoint. Чтобы узнать, как это сделать, изучите статью [Приступая к созданию надстроек SharePoint, размещаемых у поставщика](get-started-creating-provider-hosted-sharepoint-add-ins.md).
 


## <a name="what-is-the-client-side-people-picker-control-in-sharepoint"></a>Что представляет собой клиентский элемент управления "Выбор людей" в SharePoint?
<a name="bk_whatIs"> </a>

Клиентский элемент управления "Выбор людей" дает пользователям возможность быстро искать и выбирать допустимые учетные записи пользователей для людей, групп и требований в организации. Средство выбора представляет собой элемент управления HTML и JavaScript, работающий в разных браузерах. Средство выбора несложно добавить в надстройку: добавьте в разметку элемент-контейнер для этого элемента управления, ссылки на него и его зависимости. Затем в скрипте вызовите глобальную функцию **SPClientPeoplePicker_InitStandaloneControlWrapper** для отображения и инициализации этого средства выбора.
 

 
Средство выбора представлено объектом **SPClientPeoplePicker**, предоставляющим методы, которые другие клиентские элементы управления могут использовать для получения сведений из этого средства выбора или для выполнения других действий. С помощью свойств объекта **SPClientPeoplePicker** можно настроить соответствующие параметры этого средства выбора, например разрешить выбор нескольких пользователей или указать параметры кэширования. Данное средство выбора также использует параметры конфигурации веб-приложений, в частности параметры доменных служб Active Directory или параметры лесов назначения. Параметры конфигурации веб-приложений собираются автоматически (из свойства **SPWebApplication.PeoplePickerSettings**).
 

 
Средство выбора включает указанные ниже компоненты.
 

 

- Текстовое поле для ввода имен пользователей, групп и утверждений.
    
 
- Элемент управления "Интервал", в котором отображаются имена сопоставленных пользователей, групп и требований.
    
 
- Скрытый элемент **div**, который автоматически заполняет раскрывающийся список соответствующими результатами запросов.
    
 
- Элемент управления для автозаполнения.
    
 

 **Примечание.** Средство выбора и его функциональность заданы в файлах скриптов **clientforms.js**, **clientpeoplepicker.js** и **autofill.js**, которые расположены в папке %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS на сервере.
 


## <a name="prerequisites-for-setting-up-your-development-environment-to-use-the-client-side-people-picker-control-in-a-sharepoint-add-in-2013"></a>Компоненты, необходимые для настройки среды разработки, чтобы можно было использовать клиентский элемент управления "Выбор людей" в надстройке SharePoint 2013
<a name="bk_prereqs"> </a>

В этой статье предполагается, что вы создаете надстройку для SharePoint с помощью Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, то необходимые условия выполняются.
 

 

 **Примечание.** Сведения о том, как зарегистрировать Сайт разработчика и начать использовать Napa, см. в статье [Настройка среды разработки для надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md).
 

Если вы не используете Napa на Сайте разработчика, вам потребуется выполнить указанные ниже компоненты.
 

 

- SharePoint хотя бы с одним конечным пользователем;
    
 
- Visual Studio 2012 или Visual Studio 2013
    
 
- Инструменты разработчика Office для Visual Studio 2013
    
 

 **Примечание.** Рекомендации по настройке среды разработки согласно вашим потребностям см. в статье [Начало создания надстроек Office и SharePoint](http://msdn.microsoft.com/library/187f8c8c-1b15-471c-80b5-69a40e67deea.aspx).
 

В следующих действиях описываются общие действия для добавления элемента управления выбора в надстройку и последующего получения ее сведений о пользователях в другом клиентском элементе управления. Соответствующий код можно найти в разделе  [Пример кода. Использование клиентского элемента управления "Выбор людей"](use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-in.md#bk_example).
 

 
Клиентский элемент управления "Выбор людей" можно использовать в приложениях для SharePoint с размещением в SharePoint, но невозможно использовать в надстройках с размещением у поставщика. Пример реализации элемента управления "Выбор людей" в надстройке с размещением у поставщика можно скачать на веб-сайте  [Примеры модели надстроек Office](http://officeams.codeplex.com).
 

 

## <a name="use-the-client-side-people-picker-control-in-a-sharepoint-hosted-add-in"></a>Использование клиентского элемента управления "Выбор людей" в надстройках, размещаемых в SharePoint
<a name="bk_steps"> </a>


### <a name="in-your-page-markup"></a>В разметке страницы


1. Добавьте ссылки в раздел зависимостей скриптов клиентского элемента управления "Выбор людей".
    
 
2. Добавьте HTML-теги для пользовательского интерфейса страницы. В надстройке в этом примере заданы два элемента **div**: один для отображения средства выбора и второй для пользовательского интерфейса — кнопка, вызывающая скрипт для запроса средства выбора и элементов, отображающих сведения о пользователе.
    
 

### <a name="in-your-script"></a>В скрипте


1. Создайте словарь JSON для использования в качестве схемы, в которой хранятся свойства этого средства выбора, например **AllowMultipleValues** и **MaximumEntitySuggestions**.
    
 
2. Вызовите глобальную функцию **SPClientPeoplePicker_InitStandaloneControlWrapper**.
    
 
3. Получите объект средства выбора на странице.
    
 
4. Отправьте запрос в средство выбора. В надстройке в этом примере метод **GetAllUserInfo** вызывается для получения всех сведений о сопоставленных пользователях, а метод **GetAllUserKeys** — для получения ключей для этих сопоставленных пользователей.
    
 
5. Получите идентификатор пользователя с помощью объектной модели JavaScript. Идентификатор пользователя не включается в данные, возвращаемые средством выбора, поэтому надстройка вызывает метод **SP.Web.ensureUser** и получает идентификатор от возвращенного объекта **SP.User**.
    
 
Отображение, инициализация и другая функциональность для элемента управления выбора обрабатывается на сервере, включая поиск и разрешение ввода пользователя при работе с поставщиками проверки подлинности SharePoint.
 

 

## <a name="code-example-using-the-client-side-people-picker-in-a-sharepoint-hosted-add-in"></a>Пример кода: использование клиентского элемента управления "Выбор людей" в надстройке, размещаемой в SharePoint
<a name="bk_example"> </a>

В примерах кода HTML и JavaScript ниже показано, как добавить клиентский элемент управления "Выбор людей" в надстройку, размещаемую в SharePoint.
 

 
В первом примере показана разметка страницы для тегов **PlaceHolderMain****asp:Content** на странице Default.aspx. Этот код ссылается на зависимости в скрипте средства выбора, передает уникальный идентификатор в элемент DOM, в котором будет отображаться средство выбора, и задает пользовательский интерфейс надстройки.
 

 



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


 **Примечание.** В зависимости от используемой среды вам, возможно, не потребуется явно ссылаться на все эти зависимости.
 

В следующем примере показан скрипт для файла App.js. Этот скрипт инициализирует и отображает элемент управления выбора, а затем запрашивает у него пользовательские сведения и получает ИД пользователя с помощью объектной модели JavaScript.
 

 



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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Создание компонентов пользовательского интерфейса в SharePoint](create-ux-components-in-sharepoint.md)
    
 
-  [Общие сведения о средстве выбора людей и поставщиках требований (SharePoint)](http://technet.microsoft.com/library/gg602078.aspx)
    
 
-  [Настройка средства выбора людей в SharePoint](http://technet.microsoft.com/library/gg602075.aspx)
    
 

