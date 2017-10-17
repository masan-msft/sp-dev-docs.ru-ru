---
title: "Создание простой надстройки для SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 1551c0a7d5cb453a5093563298c9afb9225f7997
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-basic-sharepoint-hosted-add-in-by-using-napa-office-365-development-tools"></a>Создание простой надстройки для SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365
Узнайте, как создать простую надстройку SharePoint с размещением в SharePoint с помощью средств разработки Napa для Office 365.
 

 
![Кнопка "Запустить"](../images/Apps_NAPA_Run_Button.png)
 
 [Запустить этот пример сейчас!](http://go.microsoft.com/fwlink/?LinkId=313212)
 

 **Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).
 

Napa — это средство, с помощью которого можно создавать надстройки SharePoint с размещением в SharePoint. Средство Napa само по себе представлено в виде надстройки SharePoint (с размещением у поставщика), которую можно установить на веб-сайтах SharePoint Online, созданных с помощью шаблона **Сайт разработчика**. На домашней странице сайтов разработчиков SharePoint находится библиотека **Тестируемые надстройки**. Инструкции по созданию сайта разработчика и установке Napa приводятся далее в этой статье.
 

 **Примечание.** Мы не поддерживаем установку средства Napa в локальной системе SharePoint.
 

С помощью Napa можно создавать собственные Надстройки SharePoint в браузере, а не в Visual Studio. В случае более сложных сценариев можно в любое время скачать свой проект и открыть его в Visual Studio.
 
В этой статье можно узнать, как создать простую Надстройка SharePoint с размещением в SharePoint, используя Napa. Созданная надстройка будет содержать элементы управления и код для управления списками и элементами списка. 
 

 **Примечание.** С помощью средства Napa можно создать надстройку SharePoint, которая размещается только в SharePoint, но не у поставщика. Различия между этими типами надстроек см. в статье [Надстройки SharePoint](sharepoint-add-ins.md). Средство Napa не поддерживает обновленную семантику надстроек SharePoint, которая описана в статье [Обновление веб-компонентов надстройки в SharePoint](update-add-in-web-components-in-sharepoint.md). Поэтому, чтобы обновить надстройку, созданную в Napa, необходимо сначала экспортировать ее в Visual Studio. Соответствующие инструкции приведены далее в этой статье. Вы также можете создать надстройку SharePoint с помощью Visual Studio. Дополнительные сведения см. в статье [Знакомство с созданием надстроек SharePoint с размещением в SharePoint](get-started-creating-sharepoint-hosted-sharepoint-add-ins.md).
 


## <a name="optionally-get-an-office-365-developer-site"></a>Получение сайта разработчика Office 365 (необязательно)
<a name="Prerequisites"> </a>

Если у вас еще нет подписки на SharePoint Online, которую можно использовать для разработки, ознакомьтесь со сведениями о ее получении в этом разделе. Если же она у вас есть, перейдите сразу к разделу  [Установка Napa](#Overview).
 

 

 **Примечание.** Возможно, у вас уже есть доступ к сайту разработчика для Office 365. **Вы являетесь подписчиком MSDN?** Visual Studio Ultimate и Visual Studio Premium с подпиской на MSDN включают бесплатную подписку разработчика приложений для Office 365. [Воспользуйтесь этим преимуществом прямо сегодня.](https://msdn.microsoft.com/subscriptions/manage/default.aspx) **У вас есть один из указанных ниже планов подписки на Office 365?** **В этом случае администратор подписки на Office 365 может создать сайт разработчика, ** используя [Центр администрирования Office 365](https://portal.microsoftonline.com/admin/default.aspx). Дополнительные сведения см. в статье [Создание сайта разработчика для существующей подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md). 
 

Получить план Office 365 можно двумя способами: 
 

 

- Начните с [бесплатной 30-дневной пробной версии](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=6881A1CB-F4EB-4db3-9F18-388898DAF510&amp;DL=DEVELOPERPACK) с лицензией для одного пользователя.
    
 
- Приобретите [подписку разработчика приложений для Office 365](https://portal.microsoftonline.com/Signup/MainSignUp.aspx?OfferId=C69E7747-2566-4897-8CBA-B998ED3BAB88&amp;DL=DEVELOPERPACK). 
    
 

 **Подсказка.** При выборе каждой из этих ссылок откроется новое окно или вкладка, чтобы указанные ниже инструкции оставались под рукой.
 


**Рис. 1. Доменное имя сайта разработчика Office 365**

 

 
![Страница 2 регистрационной формы для учетной записи Office 365](../images/ff384c69-56bf-4ceb-81c3-8b874e2407f0.png)
 

 

 

 

1. Первая страница (не показана) регистрационной формы не требует объяснений. Просто введите запрашиваемую информацию о себе и нажмите кнопку **Далее**.
    
 
2. На второй странице (рис. 1) укажите ИД администратора подписки.
    
 
3. Создайте поддомен **.onmicrosoft.com**. 
    
    После регистрации необходимо использовать полученные учетные данные (в формате _ИД_пользователя_@ _ваш_домен_.onmicrosoft.com) для входа на сайт портала Office 365, где можно управлять вашей учетной записью. Ваш сайт разработчика для SharePoint Online подготавливается к работе на новом домене: **http:// _ваш_домен_.sharepoint.com**.
    
 
4. Нажмите кнопку **Далее** и заполните последнюю страницу формы. Если вы хотите указать номер телефона, чтобы получить код подтверждения, можно ввести номер мобильного или стационарного телефона, но *не* номер VoIP.
    
 

    
 **Примечание.** Если при попытке зарегистрировать учетную запись разработчика выполнен вход в другую учетную запись Майкрософт, может отобразиться следующее сообщение: "Введенный ИД пользователя неверный. Возможно, он недействителен. Убедитесь, что вы вводите свой ИД пользователя, назначенный вам организацией. Он должен выглядеть так: *proverka@example.com* или *proverka@example.onmicrosoft.com*". Если появляется такое сообщение, выйдите из используемой учетной записи Майкрософт и повторите попытку. Если сообщение продолжает отображаться, очистите кэш браузера или выберите режим **Просмотр InPrivate**, а затем заполните форму.
 

По завершении регистрации в браузере откроется страница установки Office 365. Щелкните значок администратора, чтобы открыть страницу Центра администрирования.
 

 

**Рис. 2. Страница Центра администрирования Office 365**

 

 
![Снимок экрана с изображением Центра администрирования Office 365.](../images/SP15_Office365AdminInset_border.png)
 

 

1. Дождитесь, когда завершится подготовка к работе сайта разработчика. После этого обновите страницу Центра администрирования в браузере.
    
 
2. Пройдите по ссылке **Создание надстроек** в верхнем левом углу страницы, чтобы открыть сайт разработчиков. Должен открыться сайт, который выглядит так, как показано на рис. 3. На странице размещен список **Тестируемые надстройки**. Это подтверждает, что веб-сайт был создан с помощью шаблона сайта разработчика SharePoint. Если вместо него вы видите обычный сайт группы, подождите несколько минут и перезапустите сайт.
    
 
3. Обратите внимание на URL-адрес сайта. Он используется при создании проектов надстроек SharePoint в Visual Studio.
    
 

**Рис. 3. Домашняя страница сайта разработчика со списком "Тестируемые надстройки"**

 

 
![Снимок экрана с изображением домашней страницы сайта разработчика.](../images/SP15_DeveloperSiteHome_border.png)
 

 

 

## <a name="install-napa"></a>Установка Napa
<a name="Overview"> </a>

Если ваша подписка на не была изначально создана как Сайт разработчиков Office 365, тогда необходимо создать Сайт разработчика в пользовательском интерфейсе администратора подписки на и установить на нем средства Napa. Инструкции по созданию сайта приводятся в статье  [Создание сайта разработчика с использованием актуальной подписки на Office 365](create-a-developer-site-on-an-existing-office-365-subscription.md).
 

 
Чтобы установить средства Napa, откройте сайт разработчика и последовательно выберите элементы **Контент сайта** > **Добавление надстройки** > **Магазин SharePoint**. В магазине найдите средства Napa, а затем установите их. (Если у вас есть сайт разработчиков Office 365, возможно, средства Napa уже были установлены при создании сайта. В этом случае они будут отображаться на странице **Контент сайта**.)
 

 

## <a name="create-a-sharepoint-add-in-project"></a>Создание проекта для надстройки SharePoint
<a name="Create"> </a>


1. Откройте надстройку Napa на странице Office 365.
    
 
2. Выберите плитку **Add New Project** (Добавить новый проект), а затем — плитку **Add-in for SharePoint** (Надстройка для SharePoint).
    
 
3. Назовите проект "Test SharePoint Add-in" (Тестовая надстройка SharePoint) и нажмите кнопку **Create** (Создать).
    
    Откроется редактор кода с веб-страницей по умолчанию, содержащей пример кода, который можно запустить без внесения изменений.
    
 

## <a name="add-controls-to-the-home-page"></a>Добавление элементов управления на начальную страницу
<a name="AddControls1"> </a>

В Надстройка SharePoint добавьте на начальную страницу по умолчанию элементы управления для создания и удаления универсальных списков SharePoint, а также получения текущего числа списка на сайте Надстройка SharePoint. Код этих элементов будет добавлен позже.
 

 

### <a name="to-add-controls-to-the-home-page"></a>Добавление элементов управления на начальную страницу


1. В папке **Pages** (Страницы) в левой части страницы выберите страницу **Default.aspx**, если она еще не выбрана.
    
    Страница Default.aspx появится в редакторе кода. 
    
 
2. В разделе `PlaceHolderMain` добавьте следующий код под имеющимся HTML-кодом:
    
```HTML
  <br />
<div>
    <button id="getListCount">Get count of lists in web</button>
</div>
<br />
<div id="starter">
    <input type="text" value="List name here" id="createlistbox"/><button id="createlistbutton">Create List</button>
    <p>
    Lists
    <br />
    <select id="selectlistbox" ></select><button id="deletelistbutton">Delete Selected List</button>
    </p>
</div>
```


    The HTML creates these controls.
    
      - A button that gets the number of lists in the web of the SharePoint Add-in.
    
 
  - Кнопка для создания и удаления универсальных списков SharePoint.
    
 
  - список списков, доступных в надстройке.
    
 

## <a name="add-code-for-creating-and-deleting-lists"></a>Добавление кода для создания и удаления списков
<a name="AddCode1"> </a>

В этой процедуре добавляется код JavaScript, позволяющий создавать и удалять списки в надстройке SharePoint.
 

 

### <a name="to-add-code-for-creating-and-deleting-lists"></a>Добавление кода для создания и удаления списков


1. Выберите папку **Scripts** и щелкните ссылку **App.js**.
    
    В редакторе будет открыт файл кода JavaScript из шаблона проекта. Этот файл содержит код, который использует надстройка SharePoint. Вы можете добавить другой JS-файл и добавить код в него, а не в существующий файл, но в этом примере добавьте код в готовый файл **App.js**.
    
    На следующем этапе определяются функции для элементов управления, созданных в предыдущей процедуре.
    

|**Имя функции**|**Описание**|
|:-----|:-----|
| `getWebProperties()`|Когда подключена к элементу управления **getListCount**, извлекает число списков на сайте.|
| `createlist()`|Когда подключена к элементу управления **createListButton**, создает универсальный список SharePoint.|
| `deletelist()`|Когда подключена к элементу управления **deletelistbutton**, удаляет список, выбранный пользователем в списке доступных.|

    You'll also call the  `welcome()` and `displayLists()` functions, which this walkthrough will describe later.
    
 
2. В файле **App.js** к двум переменным по умолчанию добавьте переменные `web`, `lists` и `listItemcollection`, затем измените код в функции `$(document).ready()` в соответствии с указанным ниже примером.
    
     **Примечание.** В коде появятся подчеркивания, указывающие на ошибки. Позже они пропадут.

```
  'use strict';

var context = SP.ClientContext.get_current();
var user = context.get_web().get_currentUser();
var web = context.get_web();
var lists = web.get_lists();
var listItemCollection;  // This variable is used later when you add list items.

(function () {

// This code runs when the DOM is ready and creates a context object which is 
// needed to use the SharePoint object model.
$(document).ready(function () {
    getUserName();
    $("#getListCount").click(function (event) {
        getWebProperties();
        event.preventDefault();
    });

    $("#createlistbutton").click(function (event) {
        createlist();
        event.preventDefault();
    });

    $("#deletelistbutton").click(function (event) {
        deletelist();
        event.preventDefault();
    });
        displayLists();
    });

```


    In the next step, you'll add JavaScript functions for the definitions. Each function in the code is executed by calling  `executeQueryAsync()`, which executes the current pending request asynchronously on the server by using the client-side object model (CSOM) for SharePoint. When a function executes asynchronously, your script continues to run without waiting for the server to respond. Each  `executeQueryAsync()` call includes two event handlers. One handler responds if the function runs successfully, and the other handler responds if the function fails. This table describes the main functions.
    

|**Имя функции**|**Описание**|
|:-----|:-----|
| `welcome()`|Получает ссылку на текущий контекст сайта, а затем использует ее, чтобы задать информацию о текущем пользователе в этом контексте.|
| `getWebProperties()`|Получает коллекцию списков на текущем сайте и возвращает их число.|
| `displaylists()`|Получает текущую коллекцию списков на сайте. В случае успеха функция добавляет их имена в коллекцию в списке доступных списков.|
| `createlist()`|Создает универсальный список SharePoint (типа шаблона списка **genericList**) и дает ему имя, указанное пользователем в элементе управления **createlistbox**. Можно создать списки других типов. Дополнительные сведения о типах списков см. в статье [Перечисление SPListTemplateType](http://go.microsoft.com/fwlink/?LinkId=256687).|
| `deletelist()`|Удаляет список, выбранный пользователем в списке доступных.|
3. Добавьте указанный ниже код в конец функции `onGetUserNameFail()` в файле **App.js**.
    
```
  function getWebProperties() {
        // Get the number of lists in the current web.
        context.load(lists);
        context.executeQueryAsync(onWebPropsSuccess, onWebPropsFail);
    }

    function onWebPropsSuccess(sender, args) {
        alert('Number of lists in web: ' + lists.get_count());
    }

    function onWebPropsFail(sender, args) {
        alert('Failed to get list. Error: ' + args.get_message());
    }

    function displayLists() {
        // Get the available SharePoint lists, and then set them into 
        // the context.
        lists = web.get_lists();
        context.load(lists);
        context.executeQueryAsync(onGetListsSuccess, onGetListsFail);
    }

    function onGetListsSuccess(sender, args) {
        // Success getting the lists. Set references to the list 
        // elements and the list of available lists.
        var listEnumerator = lists.getEnumerator();
        var selectListBox = document.getElementById("selectlistbox");
        if (selectListBox.hasChildNodes()) {
            while (selectListBox.childNodes.length >= 1) {
                selectListBox.removeChild(selectListBox.firstChild);
            }
        }
        // Traverse the elements of the collection, and load the name of    
        // each list into the dropdown list box.
        while (listEnumerator.moveNext()) {
            var selectOption = document.createElement("option");
            selectOption.value = listEnumerator.get_current().get_title();
            selectOption.innerHTML = listEnumerator.get_current().get_title();
            selectListBox.appendChild(selectOption);
        }
    }

    function onGetListsFail(sender, args) {
        // Lists couldn't be loaded - display error.
        alert('Failed to get list. Error: ' + args.get_message());
    }

function createlist() {
        // Create a generic SharePoint list with the name that the user specifies.
        var listCreationInfo = new SP.ListCreationInformation();
        var listTitle = document.getElementById("createlistbox").value;
        listCreationInfo.set_title(listTitle);
        listCreationInfo.set_templateType(SP.ListTemplateType.genericList);
        lists = web.get_lists();
        var newList = lists.add(listCreationInfo);
        context.load(newList);
        context.executeQueryAsync(onListCreationSuccess, onListCreationFail);
    }

    function onListCreationSuccess() {
        displayLists();
    }

    function onListCreationFail(sender, args) {
        alert('Failed to create the list. ' + args.get_message());
    }

    function deletelist() {
        // Delete the list that the user specifies.
        var selectListBox = document.getElementById("selectlistbox");
        var selectedListTitle = selectListBox.value;
        var selectedList = web.get_lists().getByTitle(selectedListTitle);
        selectedList.deleteObject();
        context.executeQueryAsync(onDeleteListSuccess, onDeleteListFail);
    }

    function onDeleteListSuccess() {
        displayLists();
    }

    function onDeleteListFail(sender, args) {
        alert('Failed to delete the list. ' + args.get_message());
    }
```


## <a name="run-it"></a>Запуск
<a name="Run1"> </a>

Первая часть интерфейса и кода готова, поэтому запустите надстройку, чтобы проверить ее работу.
 

 

### <a name="to-run-the-add-in"></a>Порядок запуска надстройки


1. Внизу страницы нажмите кнопку запуска (
 
![Кнопка "Запустить"](../images/Apps_NAPA_Run_Button.png)
 
).
    
    The add-in is packaged, deployed, and installed on your Office 365 Developer Site.
    
    After installation, the SharePoint Add-in starts. If the add-in doesn't start automatically because, for example, a popup blocker is enabled, choose the add-in link to start the add-in.
    
 
2. Нажмите ссылку **Щелкните здесь, чтобы запустить надстройку в новом окне**.
    
    Появится окно для надстройки SharePoint.
    
 
3. Нажмите кнопку **Get count of lists in web** (Получить количество списков на веб-сайте).
    
    В диалоговом окне будет указано, что сайт текущей надстройки SharePoint содержит два списка. По умолчанию сайт содержит списки "Библиотека макетов" и "Коллекция главных страниц".
    
 
4. В поле **List name here** (Укажите имя здесь) введите "Test List" (Тестовый список) и нажмите кнопку **Create List** (Создать список).
    
 
5. Откройте список **Lists** (Списки), чтобы убедиться, что в нем есть новый список.
    
 
6. Снова нажмите кнопку **Get count of lists in web** (Получить количество списков на веб-сайте).
    
    Теперь на веб-странице содержится три списка, включая только что созданный.
    
 
7. В списке **Lists** (Списки) выберите **Test List** (Тестовый список), а затем нажмите кнопку **Delete Selected List** (Удалить выбранный список).
    
     **Test List** (Тестовый список) исчезнет из списка доступных списков.
    
 
8. По завершении работы закройте окно браузера, а затем нажмите кнопку **Закрыть** в окне **Запуск надстройки**, чтобы вернуться к редактируемому проекту.
    
 

## <a name="add-code-and-controls-for-adding-and-deleting-list-items"></a>Добавление кода и элементов управления для добавления и удаления элементов списков
<a name="AddControls2"> </a>

Теперь пользователи могут создавать и удалять списки, поэтому вы можете выполнить следующие действия, чтобы они могли добавлять и удалять элементы списков.
 

 

### <a name="to-add-code-and-controls-for-adding-and-deleting-list-items"></a>Добавление кода и элементов управления для добавления и удаления элементов списков


1. Откройте файл Default.aspx для редактирования.
    
 
2. В элементе `selectlistbox` добавьте указанный ниже код.
    
```XML
      <p>
    Items
    <br />
    <input type="text" value="item name here" id="createitembox"/><button id="createitembutton">Create Item</button>
    </p>
    <p>
    <select id="selectitembox"></select> <button id="deleteitembutton">Delete Selected Item</button>
    </p>
```


    This code adds an input box where users can specify the name of an item, a button to add the item to the list, and a button to delete the item from the list.
    
 
3. Выберите файл **App.js** для редактирования.
    
 
4. В функции `$(document).ready()` добавьте определения функций, вызываемых при нажатии кнопок **Создать элемент** и **Удалить выбранный элемент**. Кроме того, добавьте обработчик событий jQuery для списка **Списки**, чтобы гарантировать, что элементы списка будут обновляться при выборе нового списка.
    
```
  $("#createitembutton").click(function (event) {
            createitem();
            event.preventDefault();
        });

        $("#deleteitembutton").click(function (event) {
            deleteitem();
            event.preventDefault();
        });
    
        // Update the list items dropdown when a new list
        // is selected in the Lists dropdown.
        $("#selectlistbox").change(function (event) {
            getitems();
            event.preventDefault();
        });
```


     **Note**  If the list items aren't displaying when you run the add-in, be sure that the  `displayLists();` statement comes after the previous code.

    In the next step, you'll add JavaScript functions for the new definitions and a support function ( `getItems()`). This table describes what the main functions do.
    

|**Имя функции**|**Описание**|
|:-----|:-----|
| `createItem()`|Добавляет элемент в выбранный список и дает ему имя из поля **Items** (Элементы).|
| `deleteItem()`|Удаляет элемент, который пользователь выбрал из списка.|
| `getItems()`|Извлекает коллекцию элементов (и их дочерних элементов) из списка, выбранного пользователем.|
5. Добавьте следующий код в конец файла **App.js** после функции `onDeleteListFail()`.
    
```
  function createitem() {
    // Retrieve the list that the user chose, and add an item to it.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedListTitle = selectListBox.value;
    var selectedList = web.get_lists().getByTitle(selectedListTitle);

    var listItemCreationInfo = new SP.ListItemCreationInformation();
    var newItem = selectedList.addItem(listItemCreationInfo);
    var listItemTitle = document.getElementById("createitembox").value;
    newItem.set_item('Title', listItemTitle);
    newItem.update();
    context.load(newItem);
    context.executeQueryAsync(onItemCreationSuccess, onItemCreationFail);
}

function onItemCreationSuccess() {
    // Refresh the list of items.
    getitems();
}

function onItemCreationFail(sender, args) {
    // The item couldn't be created - display an error message.
    alert('Failed to create the item. ' + args.get_message());
}

function deleteitem() {
    // Delete the item that the user chose.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedListTitle = selectListBox.value;
    var selectedList = web.get_lists().getByTitle(selectedListTitle);
    var selectItemBox = document.getElementById("selectitembox");
    var selectedItemID = selectItemBox.value;
    var selectedItem = selectedList.getItemById(selectedItemID);
    selectedItem.deleteObject();
    selectedList.update();
    context.load(selectedList);
    context.executeQueryAsync(onDeleteItemSuccess, onDeleteItemFail);
}

function onDeleteItemSuccess() {
    // Refresh the list of items.
    getitems();
}

function onDeleteItemFail(sender, args) {
    // The item couldn't be deleted - display an error message.
    alert('Failed to delete the item. ' + args.get_message());
}

function getitems() {
    // Using a CAML query, get the items in the list that the user chose, and 
    // set the context to the collection of list items.
    var selectListBox = document.getElementById("selectlistbox");
    var selectedList = selectListBox.value;
    var selectedListTitle = web.get_lists().getByTitle(selectedList);  
    var camlQuery = new SP.CamlQuery();
    camlQuery.set_viewXml("<View><ViewFields>" +
        "<FieldRef Name='ID' />" +
        "<FieldRef Name='Title' />" +
        "</ViewFields></View>')");
    listItemCollection = selectedListTitle.getItems(camlQuery);
    context.load(listItemCollection, "Include(Title, ID)");
    context.executeQueryAsync(onGetItemsSuccess, onGetItemsFail);
}

function onGetItemsSuccess(sender, args) {
    // The list items were retrieved.
    // Show all child nodes.
    var listItemEnumerator = listItemCollection.getEnumerator();
    var selectItemBox = document.getElementById("selectitembox");
    if (selectItemBox.hasChildNodes()) {
        while (selectItemBox.childNodes.length >= 1) {
     selectItemBox.removeChild(selectItemBox.firstChild);
        }
    }
        while (listItemEnumerator.moveNext()) {
            var selectOption = document.createElement("option");
            selectOption.value = listItemEnumerator.get_current().get_item('ID');
            selectOption.innerHTML = listItemEnumerator.get_current().get_item('Title');
            selectItemBox.appendChild(selectOption);
        }
}

function onGetItemsFail(sender, args) {
    // The list items couldn't be retrieved - display an error message.
    alert('Failed to get items. Error: ' + args.get_message());
}
```


## <a name="run-the-revised-sharepoint-add-in"></a>Запуск измененной надстройки SharePoint
<a name="Run2"> </a>

Интерфейс и код готовы, поэтому запустите надстройку, чтобы проверить ее работу.
 

 

### <a name="to-run-the-revised-sharepoint-add-in"></a>Запуск измененной надстройки SharePoint


1. Внизу страницы нажмите кнопку **Запустить** еще раз.
    
 
2. В поле **List name here** (Укажите имя здесь) введите "New Test List" (Новый тестовый список) и нажмите кнопку **Create List** (Создать список).
    
    Новый список добавится в столбец **Lists** (Списки).
    
 
3. В столбце **Lists** (Списки) выберите **New Test List** (Новый тестовый список).
    
 
4. В поле **Item name here** (Укажите имя элемента) введите "Item 1" (Элемент 1) и нажмите кнопку **Create Item** (Создать элемент).
    
    Новый элемент списка появится в столбце **Items** (Элементы).
    
 
5. Повторите предыдущие действия, чтобы добавить элементы "Item 2" (Элемент 2) и "Item 3" (Элемент 3).
    
 
6. В списке элементов выберите **Item 2** (Элемент 2), а затем нажмите кнопку **Delete Selected Item** (Удалить выбранный элемент).
    
     **Item 2** (Элемент 2) исчезнет из списка элементов.
    
 
7. По окончании работы закройте окно браузера.
    
 

## <a name="export-the-project-to-visual-studio"></a>Экспорт проекта в Visual Studio
<a name="NextSteps"> </a>

Откройте свой проект в Visual Studio, нажав кнопку **Открыть в Visual Studio**, как показано на рисунке 3. Napa автоматически установит требуемые средства и откроет проект в Visual Studio.
 

 

**Рис. 3. Кнопка "Открыть в Visual Studio"**

 

 
![Кнопка "Открыть в Visual Studio"](../images/Apps_Napa_OpenInVS.png)
 

 

 

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="Additional"> </a>


-  [Обзор платформы разработки SharePoint](http://msdn.microsoft.com/library/f86e2695-4d7a-4fc5-bc23-689de96c4b06%28Office.15%29.aspx)
    
 
-  [Надстройки SharePoint](sharepoint-add-ins.md)
    
 

