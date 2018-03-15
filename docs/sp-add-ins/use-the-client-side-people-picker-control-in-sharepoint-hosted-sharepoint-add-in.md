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
# <a name="use-the-client-side-people-picker-control-in-sharepoint-hosted-sharepoint-add-ins"></a>Использование клиентского средства выбора людей в надстройках SharePoint с размещением в SharePoint

> [!IMPORTANT] 
> В этой статье предполагается, что вы знаете, [как создать надстройку SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).
 
<a name="bk_whatIs"> </a>

## <a name="what-is-the-client-side-people-picker-control-in-sharepoint"></a>Что представляет собой клиентское средство выбора людей в SharePoint?

Клиентское средство выбора людей позволяет пользователям быстро находить действительные учетные записи для людей, групп и утверждений в организации. Средство выбора представляет собой элемент управления HTML и JavaScript, работающий в разных браузерах. 

Добавить средство выбора в надстройку легко: 

1. В коде добавьте элемент контейнера для этого элемента управления, а также ссылки на последний и его зависимости. 

2. В скрипт добавьте вызов глобальной функции **SPClientPeoplePicker_InitStandaloneControlWrapper** для отрисовки и инициализации средства выбора.

Средство выбора представлено объектом **SPClientPeoplePicker**, предоставляющим методы, которые другие клиентские элементы управления могут использовать для получения сведений из этого средства выбора или для выполнения других действий. С помощью свойств объекта **SPClientPeoplePicker** можно настроить соответствующие параметры этого средства выбора (например, разрешить выбор нескольких пользователей или указать параметры кэширования). 

Данное средство выбора также использует параметры конфигурации веб-приложений, в частности параметры доменных служб Active Directory или параметры целевых лесов. Параметры конфигурации веб-приложений собираются автоматически (из свойства **SPWebApplication.PeoplePickerSettings**).
 
Средство выбора включает следующие компоненты:

- Текстовое поле для ввода имен пользователей, групп и утверждений.
- Элемент управления "Интервал", в котором отображаются имена сопоставленных пользователей, групп и требований.
- Скрытый элемент **div**, который автоматически заполняет раскрывающийся список соответствующими результатами запроса.
- Элемент управления для автозаполнения.
    
> [!NOTE] 
> Средство выбора и его функциональность заданы в файлах сценариев **clientforms.js**, **clientpeoplepicker.js** и **autofill.js**, которые расположены в папке %ProgramFiles%\Common Files\Microsoft Shared\web server extensions\15\TEMPLATE\LAYOUTS на сервере.
 
<a name="bk_prereqs"> </a>

## <a name="prerequisites-for-setting-up-your-development-environment-to-use-the-client-side-people-picker-control-in-a-sharepoint-add-in"></a>Требования к среде разработки для использования клиентского средства выбора людей в надстройке SharePoint

В этой статье предполагается, что вы создаете надстройку для SharePoint, используя Napa на сайте разработчика Office 365. Если вы используете эту среду разработки, у вас уже установлены необходимые компоненты.
 
> [!NOTE] 
> Сведения о том, как зарегистрировать сайт разработчика и начать использовать Napa, см. в статье [Настройка среды разработки надстроек SharePoint в Office 365](set-up-a-development-environment-for-sharepoint-add-ins-on-office-365.md).
 
Если вы не используете Napa на сайте разработчика, вам потребуется следующие компоненты:

- SharePoint хотя бы с одним пользователем;
- Visual Studio 2012 или Visual Studio 2013;
- Инструменты разработчика Office для Visual Studio 2013.
    
> [!NOTE] 
> Рекомендации по настройке подходящей среды разработки см. в статье [Надстройки SharePoint](sharepoint-add-ins.md#two-types-of-sharepoint-add-ins-sharepoint-hosted-and-provider-hosted).
 
В приведенных ниже разделах указаны общие инструкции по добавлению средства выбора в надстройку и получению сведений о пользователях из другого клиентского элемента управления. Соответствующий код см. в разделе [Пример кода: использование клиентского средства выбора людей](#bk_example).

Клиентское средство выбора людей можно использовать в надстройках SharePoint с размещением в SharePoint, но не в надстройках с размещением у поставщика. 

<a name="bk_steps"> </a>

## <a name="use-the-client-side-people-picker-control-in-a-sharepoint-hosted-add-in"></a>Использование клиентского средства выбора людей в надстройке с размещением в SharePoint

### <a name="in-your-page-markup"></a>В разметке страницы

1. Добавьте ссылки в раздел зависимостей скриптов клиентского элемента управления "Выбор людей".

2. Добавьте теги HTML для пользовательского интерфейса страницы. В надстройке из данного примера задается два элемента **div**: один для отображения элемента управления выбора и второй для пользовательского интерфейса кнопка, вызывающая скрипт для запроса этого элемента управления выбора и элементов, отображающих данные о пользователе.
    
### <a name="in-your-script"></a>В скрипте

1. Создайте словарь JSON для использования в качестве схемы, в которой хранятся свойства этого элемента управления выбора, такие как **AllowMultipleValues** и **MaximumEntitySuggestions**.

2. Вызовите глобальную функцию **SPClientPeoplePicker_InitStandaloneControlWrapper**.

3. Получите объект средства выбора на странице.

4. Отправьте запрос средству выбора. Надстройка в этом примере вызывает метод **GetAllUserInfo** для получения всех сведений о сопоставленных пользователях, а также метод **GetAllUserKeys** для получения ключей для этих сопоставленных пользователей.

5. Получите ИД пользователя с помощью объектной модели JavaScript. ИД пользователя не включается в данные, которое возвращается элементом выбора, поэтому надстройка вызывает метод **SP.Web.ensureUser** и получает ИД от возвращенного объекта **SP.User**.

Отображение, инициализация и другая функциональность для элемента управления выбора обрабатывается на сервере, включая поиск и разрешение ввода пользователя при работе с поставщиками проверки подлинности SharePoint.
 
<a name="bk_example"> </a>

## <a name="code-example-using-the-client-side-people-picker-in-a-sharepoint-hosted-add-in"></a>Пример кода: использование клиентского средства выбора людей в надстройке с размещением в SharePoint

Примеры кода HTML и JavaScript, приведенные ниже, добавляют клиентское средство выбора людей в надстройку с размещением в SharePoint.

В первом примере показана разметка страницы для тегов **PlaceHolderMain asp:Content** на странице Default.aspx. Этот код ссылается на зависимости в скрипте средства выбора, присваивает уникальный идентификатор элементу DOM, содержащему средство выбора, и определяет пользовательский интерфейс надстройки.

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
> В зависимости от используемой среды вам, возможно, не потребуется явно ссылаться на все эти зависимости.
 
<br/>

В приведенном ниже примере показан **скрипт из файла App.js**. Этот скрипт инициализирует и отрисовывает средство выбора, а затем запрашивает информацию о пользователях и получает ИД пользователя, используя объектную модель JavaScript.

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

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Создание компонентов пользовательского интерфейса в SharePoint](create-ux-components-in-sharepoint.md)
-  [Общие сведения о средстве выбора людей и поставщиках требований (SharePoint)](http://technet.microsoft.com/library/gg602078.aspx)
-  [Настройка средства выбора людей в SharePoint](http://technet.microsoft.com/library/gg602075.aspx)
    
 

