---
title: "Создание элементов управления пользовательского интерфейса с помощью SharePoint у поставщика надстроек"
ms.date: 11/03/2017
ms.openlocfilehash: a5ec35589ae00a6062be724a68910365102161c3
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-ux-controls-by-using-sharepoint-provider-hosted-add-ins"></a>Создание элементов управления пользовательского интерфейса с помощью SharePoint у поставщика надстроек

Создание элементов управления пользовательского интерфейса в SharePoint у поставщика надстроек, работы и обрабатываются как элементы управления пользовательского интерфейса на веб-сайт. 

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

В статье описывается три примеры, показывающие, как реализовать элементов управления пользовательского интерфейса в размещение у поставщика в надстройке:

- [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) - показано, как добавить элемент управления средства выбора людей.
    
- [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) - показано, как реализовать элемент управления меню локализуемых таксономии.
    
- [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) - показано, как реализовать элемент управления "Выбор" таксономии.
    
В этих примерах используйте JavaScript и JSOM для взаимодействия с SharePoint и использование [междоменной библиотеки](https://msdn.microsoft.com/en-us/library/office/fp179927%28v=office.15%29.aspx) для обработки вызовов функций из надстройки на несущий домен сайта.

## <a name="people-picker-control"></a>Элемент управления для выбора людей
<a name="bmPeoplePicker"> </a>

В примере [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) показано, как для реализации управления средства выбора людей в размещенном у поставщика надстройки с. Когда пользователь начинает ввод имени в поле ввода текста, поиск элемента управления, хранилище профилей пользователей для возможных совпадений и отображает их в пользовательском Интерфейсе. Надстройки отображает элемент управления "Выбор" Настраиваемая и расширяемая совместно с запущенным на удаленном компьютере, который отправляет запрос в хранилище профилей пользователей на сайт узла в соответствии с входные данные пользователя.

**На рисунке 1. Элемент управления для выбора людей**

![Элемент управления для выбора людей](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/ae6e2198-6f63-4ea1-a739-34f64ecd9117.png)
    
> [!NOTE] 
> Решение Visual Studio 2013 пример содержит модуль с именем «Фиктивное», чтобы убедиться, что при развертывании надстройки создает add-in web. Надстройка web является обязательным для междоменных вызовов.

Папка скрипты проекта Core.PeoplePickerWeb содержит файлы app.js и peoplepickercontrol.js (а также файлы ресурсов средства выбора людей для поддержки дополнительных языков). Файл app.js извлекает контекст клиента с помощью междоменной библиотеки и подключает HTML-код в файл Default.aspx в элементе управления средства выбора людей. Содержит файл Default.aspx `<div>` возможность поиска тегов, которые реализуют текстовое поле и людей.

> [!NOTE] 
> Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```
<div id="divAdministrators" class="cam-peoplepicker-userlookup ms-fullWidth">
  <span id="spanAdministrators"></span>
<asp:TextBox ID="inputAdministrators" runat="server" CssClass="cam-peoplepicker-edit" Width="70"></asp:TextBox>
</div>
<div id="divAdministratorsSearch" class="cam-peoplepicker-usersearch ms-emphasisBorder"></div>
<asp:HiddenField ID="hdnAdministrators" runat="server" />

```

Выберите файл app.js создает и настраивает элемента управления средства выбора людей.

```
//Make a people picker control.
//1. context = SharePoint Client Context object
//2. $('#spanAdministrators') = SPAN that will 'host' the people picker control
//3. $('#inputAdministrators') = INPUT that will be used to capture user input
//4. $('#divAdministratorsSearch') = DIV that will show the 'drop-down' of the picker
//5. $('#hdnAdministrators') = INPUT hidden control that will host a resolved users
peoplePicker = new CAMControl.PeoplePicker(context, $('#spanAdministrators'), $('#inputAdministrators'), $('#divAdministratorsSearch'), $('#hdnAdministrators'));
// required to pass the variable name here!
peoplePicker.InstanceName = "peoplePicker";
// Hookup everything.
peoplePicker.Initialize();

```

Элемент управления средства выбора людей запрашивает объект **ClientPeoplePickerWebServiceInterface** в библиотеке JSOM для запуска операций поиска для пользователей, имена которых соответствуют строк символов, введенных.

```
if (searchText.length >= parent.GetMinimalCharactersBeforeSearching()) {
                            resultDisplay = 'Searching...';
                            if (typeof resultsSearching != 'undefined') {
                                resultDisplay = resultsSearching;
                            }

                  var searchbusy = parent.Format('<div class=\'ms-emphasisBorder\' style=\'width: 400px; padding: 4px; border-left: none; border-bottom: none; border-right: none; cursor: default;\'>{0}</div>', resultDisplay);
                            parent.PeoplePickerDisplay.html(searchbusy);
                            // Display the suggestion box.
                            parent.ShowSelectionBox();

                   var query = new SP.UI.ApplicationPages.ClientPeoplePickerQueryParameters();
                            query.set_allowMultipleEntities(false);
                            query.set_maximumEntitySuggestions(2000);
                            query.set_principalType(parent.GetPrincipalType());
                            query.set_principalSource(15);
                            query.set_queryString(searchText);
                            var searchResult = SP.UI.ApplicationPages.ClientPeoplePickerWebServiceInterface.clientPeoplePickerSearchUser(parent.SharePointContext, query);

                  // Update the global queryID variable so that you can correlate incoming delegate calls.
                            parent._queryID = parent._queryID + 1;
                            var queryIDToPass = parent._queryID;
                            parent._lastQueryID = queryIDToPass;

                  // Make the SharePoint request.
                            parent.SharePointContext.executeQueryAsync(Function.createDelegate(this, function () { parent.QuerySuccess(queryIDToPass, searchResult); }),
                                                Function.createDelegate(this, function () { parent.QueryFailure(queryIDToPass); }));

```

## <a name="taxonomy-menu-control"></a>Элемент управления меню таксономии
<a name="bmTaxMenu"> </a>

Пример [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) показано, как реализовать элемент управления меню локализуемых таксономии, заполняются из хранилища терминов в размещение у поставщика в надстройке. Надстройки также настраивает языки хранилища необходимые терминов, группы, наборы и условия для заполнения в меню и проверяет пользователя языковые параметры, чтобы задать язык интерфейса.

Надстройка реализует класс **TaxonomyHelper** (CSOM), который выполняет настройку банка терминов и заполняет ее условия. Он затем загружает в корневой папке сайта файл JavaScript, которая отображает навигационных ссылок.

Надстройка настраивает банк терминов на сайт узла. Используется для создания группы терминов и набор CSOM объекты и методы и заполняет набор с четырьмя термины терминов. 

**На рисунке 2. Экран программы установки хранилища терминов**

![Экран программы установки хранилища терминов](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/011ba839-7bc3-4a12-819a-6436deab2e34.png)

При выборе кнопки **банк терминов программы установки** надстройки:

- Следит за тем, что необходимые языков (английский, немецкий, французский и шведский) включены в банке терминов.
    
- Создает группу терминов и набор терминов и заполняет набор с четыре новых терминов терминов.
    
Следующий код в класс **TaxonomyHelper** проверяет, что включены необходимых языков, и если они не позволяет им.

```
var languages = new int[] { 1031, 1033, 1036, 1053 };
            Array.ForEach(languages, l => { 
                if (!termStore.Languages.Contains(l)) 
                    termStore.AddLanguage(l); 
            });

            termStore.CommitAll();
            clientContext.ExecuteQuery();

// Create the term group.
termGroup = termStore.CreateGroup("Taxonomy Navigation", groupId);
                clientContext.Load(termGroup);
                clientContext.ExecuteQuery();
```

И, наконец следующий код в тот же класс **TaxonomyHelper** создает каждого нового терминов, а также метки для немецкого, французском и шведском языках. Также устанавливает значение для свойства **_Sys_Nav_SimpleLinkUrl** эквивалентно свойству **простой ссылкой или заголовок** в средство управления банками терминов. В этом случае URL-адрес для каждого термина указывает на корневой узел.

```
var term = termSet.CreateTerm(termName, 1033, Guid.NewGuid());
term.CreateLabel(termNameGerman, 1031, false);
term.CreateLabel(termNameFrench, 1036, false);
term.CreateLabel(termNameSwedish, 1053, false);
term.SetLocalCustomProperty("_Sys_Nav_SimpleLinkUrl", clientContext.Web.ServerRelativeUrl);
```

Далее надстройки вставляет файл topnav.js в корневой папке сайта узла. Этот файл содержит JavaScript, который вставляет ссылки из этого набора терминов в панели навигации на домашнюю страницу узла. Пользовательский Интерфейс также показано, как будет выглядеть навигационных ссылок сайта узла после надстройки загружает файл JavaScript.

Следующий код в файле topnav.js использует JSOM для поиска предпочтительный язык пользователя.

```
var targetUser = "i:0#.f|membership|" + _spPageContextInfo.userLoginName;
        context = new SP.ClientContext.get_current();
var peopleManager = new SP.UserProfiles.PeopleManager(context);
var userProperty = peopleManager.getUserProfilePropertyFor(targetUser, "SPS-MUILanguages");
```

Надстройка затем определяет, соответствует ли язык пользователя один из доступных языков. Если совпадение найдено, следующий код получает условия и связанные метки для предпочтительный язык пользователя.

```
while (termEnumerator.moveNext()) {
    var currentTerm = termEnumerator.get_current();
    var label = currentTerm.getDefaultLabel(lcid);

    termItems.push(currentTerm);
    termLabels.push(label);
    context.load(currentTerm);
```

И, наконец следующий код в файле topnav.js вставляет ссылки, содержащие термины в элемент верхнего переходов сайта узла.

```
html += "<ul style='margin-top: 0px; margin-bottom: 0px;'>"
        for (var i in termItems) {
            var term = termItems[i];
            var termLabel = termLabels[i];
            var linkName = termLabel.get_value() != 0 ? termLabel.get_value() : term.get_name();
            var linkUrl = term.get_localCustomProperties()['_Sys_Nav_SimpleLinkUrl'];

            html += "<li style='display: inline;list-style-type: none; padding-right: 20px;'><a href='" + linkUrl + "'>" + linkName + "</a></li>";
        }
        html += "</ul>";

        $('#DeltaTopNavigation').html(html);
        SP.UI.Notify.removeNotification(nid);
```

## <a name="taxonomy-picker-control"></a>Элемент управления для выбора таксономии
<a name="bmTaxPicker"> </a>

Пример [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) показано, как реализовать элемента управления "Выбор" таксономии в размещенном у поставщика надстройки с. Когда пользователь начинает ввод терминов в поле ввода текста, поиск элемента управления банк терминов для потенциал сопоставляет и отображает их в списке в поле ввода.

Надстройка создает HTML-страницу, которая соответствует требования средства выбора JSOM таксономии и добавление и настройка элемента управления. Библиотека JSOM используется для запроса банк терминов сайта узла. Средство выбора таксономии взаимодействует с SharePoint служба управляемых метаданных, который необходимо разрешение на запись на уровне разрешений таксономии, чтобы его можно чтения наборы терминов закрытой и записи в открытые наборы терминов. Убедитесь в том, что файл AppManifest.xml значение разрешения на запись в соответствующие области.

Папка скрипты проекта [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) содержит файлы app.js и taxonomypickercontrol.js (а также таксономии "Выбор" файл ресурсов для поддержки дополнительных языков). Файл app.js извлекает контекст клиента с помощью междоменной библиотеки и подключает HTML-код в файл Default.aspx в элементе управления средства выбора таксономии. Файл Default.aspx содержит скрытых полей, который реализует текстовое поле и возможность выбора таксономии. Он также добавляет маркированного списка для отображения предложений, возвращенные банка терминов.

```
<div style="left: 50%; width: 600px; margin-left: -300px; position: absolute;">
            <table>
                <tr>
                    <td class="ms-formlabel" valign="top"><h3 class="ms-standardheader">Keywords Termset:</h3></td>
                    <td class="ms-formbody" valign="top">
                        <div class="ms-core-form-line" style="margin-bottom: 0px;">
                            <asp:HiddenField runat="server" id="taxPickerKeywords" />
                        </div>
                    </td>
                </tr>
            </table>

            <asp:Button runat="server" OnClick="SubmitButton_Click" Text="Submit" />

            <asp:BulletedList runat="server" ID="SelectedValues" DataTextField="Label" />
</div>
```

Выберите файл app.js создает и настраивает элемент управления "Выбор" таксономии.

```
// Load scripts for calling taxonomy APIs.
                    $.getScript(layoutsRoot + 'init.js',
                        function () {
                            $.getScript(layoutsRoot + 'sp.taxonomy.js',
                                function () {
                                    // Bind the taxonomy picker to the default keywords term set.
                                    $('#taxPickerKeywords').taxpicker({ isMulti: true, allowFillIn: true, useKeywords: true }, context);
                                });
                        });

```

Элемент управления "Выбор" таксономии использует следующий код для открытия экземпляра **TaxonomySession** в JSOM для загрузки с условиями от банка терминов.

```
// Get the taxonomy session by using CSOM.
            var taxSession = SP.Taxonomy.TaxonomySession.getTaxonomySession(spContext);
            //Use the default term store...this could be extended here to support additional term stores.
            var termStore = taxSession.getDefaultSiteCollectionTermStore();

            // Get the term set based on the properties of the term set.
            if (this.Id != null)
                this.RawTermSet = termStore.getTermSet(this.Id); // Get term set by ID.
            else if (this.UseHashtags)
                this.RawTermSet = termStore.get_hashTagsTermSet(); // Get the hashtags term set.
            else if (this.UseKeywords)
                this.RawTermSet = termStore.get_keywordsTermSet(); // Get the keywords term set.

            // Get all terms for the term set and organize them in the async callback.
            this.RawTerms = this.RawTermSet.getAllTerms();
            spContext.load(this.RawTermSet);
            spContext.load(this.RawTerms);
            spContext.executeQueryAsync(Function.createDelegate(this, this.termsLoadedSuccess), Function.createDelegate(this, this.termsLoadedFailed));

```

Элемент управления "Выбор" таксономии ищет потенциальные совпадения из загруженных термины и добавляет новых терминов в банке терминов при необходимости.

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [Доступ к данным SharePoint 2013 из надстроек с помощью междоменной библиотеки](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx)
