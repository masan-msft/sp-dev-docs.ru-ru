---
title: "Создание элементов управления пользовательского интерфейса с помощью SharePoint у поставщика надстроек"
ms.date: 11/03/2017
ms.openlocfilehash: a5ec35589ae00a6062be724a68910365102161c3
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-ux-controls-by-using-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="7a707-102">Создание элементов управления пользовательского интерфейса с помощью SharePoint у поставщика надстроек</span><span class="sxs-lookup"><span data-stu-id="7a707-102">Create UX controls by using SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="7a707-103">Создание элементов управления пользовательского интерфейса в SharePoint у поставщика надстроек, работы и обрабатываются как элементы управления пользовательского интерфейса на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="7a707-103">Create UX controls in SharePoint provider-hosted add-ins that work and behave like UX controls on the host web.</span></span> 

<span data-ttu-id="7a707-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="7a707-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="7a707-105">В статье описывается три примеры, показывающие, как реализовать элементов управления пользовательского интерфейса в размещение у поставщика в надстройке:</span><span class="sxs-lookup"><span data-stu-id="7a707-105">The article describes three samples that show you how to implement UX controls in your provider-hosted add-in:</span></span>

- <span data-ttu-id="7a707-106">[Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) - показано, как добавить элемент управления средства выбора людей.</span><span class="sxs-lookup"><span data-stu-id="7a707-106">[Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) - Shows you how to add a people picker control.</span></span>
    
- <span data-ttu-id="7a707-107">[Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) - показано, как реализовать элемент управления меню локализуемых таксономии.</span><span class="sxs-lookup"><span data-stu-id="7a707-107">[Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) - Shows you how to implement a localizable taxonomy menu control.</span></span>
    
- <span data-ttu-id="7a707-108">[Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) - показано, как реализовать элемент управления "Выбор" таксономии.</span><span class="sxs-lookup"><span data-stu-id="7a707-108">[Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) - Shows you how to implement a taxonomy picker control.</span></span>
    
<span data-ttu-id="7a707-109">В этих примерах используйте JavaScript и JSOM для взаимодействия с SharePoint и использование [междоменной библиотеки](https://msdn.microsoft.com/en-us/library/office/fp179927%28v=office.15%29.aspx) для обработки вызовов функций из надстройки на несущий домен сайта.</span><span class="sxs-lookup"><span data-stu-id="7a707-109">These samples use JavaScript and the JSOM to communicate with SharePoint and use the [cross-domain library](https://msdn.microsoft.com/en-us/library/office/fp179927%28v=office.15%29.aspx) to handle function calls from the add-in to the host site domain.</span></span>

## <a name="people-picker-control"></a><span data-ttu-id="7a707-110">Элемент управления для выбора людей</span><span class="sxs-lookup"><span data-stu-id="7a707-110">People picker control</span></span>
<span data-ttu-id="7a707-111"><a name="bmPeoplePicker"> </a></span><span class="sxs-lookup"><span data-stu-id="7a707-111"></span></span>

<span data-ttu-id="7a707-112">В примере [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) показано, как для реализации управления средства выбора людей в размещенном у поставщика надстройки с.</span><span class="sxs-lookup"><span data-stu-id="7a707-112">The [Core.PeoplePicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.PeoplePicker) sample shows you how to implement a people picker control in a provider-hosted add-in.</span></span> <span data-ttu-id="7a707-113">Когда пользователь начинает ввод имени в поле ввода текста, поиск элемента управления, хранилище профилей пользователей для возможных совпадений и отображает их в пользовательском Интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="7a707-113">When the user starts typing a name into the text input box, the control searches the user profile store for potential matches, and displays them in the UI.</span></span> <span data-ttu-id="7a707-114">Надстройки отображает элемент управления "Выбор" Настраиваемая и расширяемая совместно с запущенным на удаленном компьютере, который отправляет запрос в хранилище профилей пользователей на сайт узла в соответствии с входные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a707-114">The add-in displays a configurable and extensible people picker control that runs on a remote host and queries the user profile store on the host site to match user inputs.</span></span>

<span data-ttu-id="7a707-115">**На рисунке 1. Элемент управления для выбора людей**</span><span class="sxs-lookup"><span data-stu-id="7a707-115">**Figure 1. People picker control**</span></span>

![Элемент управления для выбора людей](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/ae6e2198-6f63-4ea1-a739-34f64ecd9117.png)
    
> [!NOTE] 
> <span data-ttu-id="7a707-117">Решение Visual Studio 2013 пример содержит модуль с именем «Фиктивное», чтобы убедиться, что при развертывании надстройки создает add-in web.</span><span class="sxs-lookup"><span data-stu-id="7a707-117">The Visual Studio 2013 solution for the sample contains a module named "Dummy" to ensure that when the add-in is deployed, it creates an add-in web.</span></span> <span data-ttu-id="7a707-118">Надстройка web является обязательным для междоменных вызовов.</span><span class="sxs-lookup"><span data-stu-id="7a707-118">An add-in web is required for cross-domain calls.</span></span>

<span data-ttu-id="7a707-119">Папка скрипты проекта Core.PeoplePickerWeb содержит файлы app.js и peoplepickercontrol.js (а также файлы ресурсов средства выбора людей для поддержки дополнительных языков).</span><span class="sxs-lookup"><span data-stu-id="7a707-119">The Scripts folder of the Core.PeoplePickerWeb project contains app.js and peoplepickercontrol.js files (along with people picker resource files for additional language support).</span></span> <span data-ttu-id="7a707-120">Файл app.js извлекает контекст клиента с помощью междоменной библиотеки и подключает HTML-код в файл Default.aspx в элементе управления средства выбора людей.</span><span class="sxs-lookup"><span data-stu-id="7a707-120">The app.js file fetches client context by using the cross-domain library and hooks the HTML in the Default.aspx file into the people picker control.</span></span> <span data-ttu-id="7a707-121">Содержит файл Default.aspx `<div>` возможность поиска тегов, которые реализуют текстовое поле и людей.</span><span class="sxs-lookup"><span data-stu-id="7a707-121">The Default.aspx file contains the  `<div>` tags that implement both the text box and the people search capability.</span></span>

> [!NOTE] 
> <span data-ttu-id="7a707-122">Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="7a707-122">The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
<div id="divAdministrators" class="cam-peoplepicker-userlookup ms-fullWidth">
  <span id="spanAdministrators"></span>
<asp:TextBox ID="inputAdministrators" runat="server" CssClass="cam-peoplepicker-edit" Width="70"></asp:TextBox>
</div>
<div id="divAdministratorsSearch" class="cam-peoplepicker-usersearch ms-emphasisBorder"></div>
<asp:HiddenField ID="hdnAdministrators" runat="server" />

```

<span data-ttu-id="7a707-123">Выберите файл app.js создает и настраивает элемента управления средства выбора людей.</span><span class="sxs-lookup"><span data-stu-id="7a707-123">The app.js file then creates and configures a people picker control.</span></span>

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

<span data-ttu-id="7a707-124">Элемент управления средства выбора людей запрашивает объект **ClientPeoplePickerWebServiceInterface** в библиотеке JSOM для запуска операций поиска для пользователей, имена которых соответствуют строк символов, введенных.</span><span class="sxs-lookup"><span data-stu-id="7a707-124">The people picker control queries the  **ClientPeoplePickerWebServiceInterface** object in the JSOM library to initiate searches for users whose names match the character strings entered.</span></span>

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

## <a name="taxonomy-menu-control"></a><span data-ttu-id="7a707-125">Элемент управления меню таксономии</span><span class="sxs-lookup"><span data-stu-id="7a707-125">Taxonomy menu control</span></span>
<span data-ttu-id="7a707-126"><a name="bmTaxMenu"> </a></span><span class="sxs-lookup"><span data-stu-id="7a707-126"></span></span>

<span data-ttu-id="7a707-127">Пример [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) показано, как реализовать элемент управления меню локализуемых таксономии, заполняются из хранилища терминов в размещение у поставщика в надстройке.</span><span class="sxs-lookup"><span data-stu-id="7a707-127">The [Core.TaxonomyMenu](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyMenu) sample shows you how to implement a localizable taxonomy menu control that is populated from the term store in a provider-hosted add-in.</span></span> <span data-ttu-id="7a707-128">Надстройки также настраивает языки хранилища необходимые терминов, группы, наборы и условия для заполнения в меню и проверяет пользователя языковые параметры, чтобы задать язык интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7a707-128">The add-in also sets up the required term store languages, groups, sets, and terms for populating the menu, and checks the user's language preference to set the display language.</span></span>

<span data-ttu-id="7a707-129">Надстройка реализует класс **TaxonomyHelper** (CSOM), который выполняет настройку банка терминов и заполняет ее условия.</span><span class="sxs-lookup"><span data-stu-id="7a707-129">The add-in implements a  **TaxonomyHelper** class (CSOM) that sets up the term store and populates it with terms.</span></span> <span data-ttu-id="7a707-130">Он затем загружает в корневой папке сайта файл JavaScript, которая отображает навигационных ссылок.</span><span class="sxs-lookup"><span data-stu-id="7a707-130">It then uploads into the site's root folder a JavaScript file that displays the navigational links.</span></span>

<span data-ttu-id="7a707-131">Надстройка настраивает банк терминов на сайт узла.</span><span class="sxs-lookup"><span data-stu-id="7a707-131">The add-in sets up the term store on the host site.</span></span> <span data-ttu-id="7a707-132">Используется для создания группы терминов и набор CSOM объекты и методы и заполняет набор с четырьмя термины терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-132">It uses CSOM objects and methods to create a term group and set, and then populates the term set with four terms.</span></span> 

<span data-ttu-id="7a707-133">**На рисунке 2. Экран программы установки хранилища терминов**</span><span class="sxs-lookup"><span data-stu-id="7a707-133">**Figure 2. Term store setup screen**</span></span>

![Экран программы установки хранилища терминов](media/create-ux-controls-by-using-sharepoint-provider-hosted-add-ins/011ba839-7bc3-4a12-819a-6436deab2e34.png)

<span data-ttu-id="7a707-135">При выборе кнопки **банк терминов программы установки** надстройки:</span><span class="sxs-lookup"><span data-stu-id="7a707-135">When you choose the  **Setup term store** button, the add-in:</span></span>

- <span data-ttu-id="7a707-136">Следит за тем, что необходимые языков (английский, немецкий, французский и шведский) включены в банке терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-136">Makes sure that the required languages (English, German, French, and Swedish) are enabled in the term store.</span></span>
    
- <span data-ttu-id="7a707-137">Создает группу терминов и набор терминов и заполняет набор с четыре новых терминов терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-137">Creates a term group and term set and populates the term set with four new terms.</span></span>
    
<span data-ttu-id="7a707-138">Следующий код в класс **TaxonomyHelper** проверяет, что включены необходимых языков, и если они не позволяет им.</span><span class="sxs-lookup"><span data-stu-id="7a707-138">The following code in the  **TaxonomyHelper** class verifies that the required languages are enabled, and if they're not, it enables them.</span></span>

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

<span data-ttu-id="7a707-139">И, наконец следующий код в тот же класс **TaxonomyHelper** создает каждого нового терминов, а также метки для немецкого, французском и шведском языках.</span><span class="sxs-lookup"><span data-stu-id="7a707-139">Finally, the following code in the same  **TaxonomyHelper** class creates each new term, along with labels for the German, French, and Swedish languages.</span></span> <span data-ttu-id="7a707-140">Также устанавливает значение для свойства **_Sys_Nav_SimpleLinkUrl** эквивалентно свойству **простой ссылкой или заголовок** в средство управления банками терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-140">It also sets a value for the **_Sys_Nav_SimpleLinkUrl** property, which is equivalent to the **Simple Link or Header** property in the Term Store Management Tool.</span></span> <span data-ttu-id="7a707-141">В этом случае URL-адрес для каждого термина указывает на корневой узел.</span><span class="sxs-lookup"><span data-stu-id="7a707-141">In this case, the URL for each term points back to the root site.</span></span>

```
var term = termSet.CreateTerm(termName, 1033, Guid.NewGuid());
term.CreateLabel(termNameGerman, 1031, false);
term.CreateLabel(termNameFrench, 1036, false);
term.CreateLabel(termNameSwedish, 1053, false);
term.SetLocalCustomProperty("_Sys_Nav_SimpleLinkUrl", clientContext.Web.ServerRelativeUrl);
```

<span data-ttu-id="7a707-142">Далее надстройки вставляет файл topnav.js в корневой папке сайта узла.</span><span class="sxs-lookup"><span data-stu-id="7a707-142">Next, the add-in inserts the topnav.js file into the root folder of the host site.</span></span> <span data-ttu-id="7a707-143">Этот файл содержит JavaScript, который вставляет ссылки из этого набора терминов в панели навигации на домашнюю страницу узла.</span><span class="sxs-lookup"><span data-stu-id="7a707-143">This file contains the JavaScript that inserts the links from this term set into the navigation of the host site's home page.</span></span> <span data-ttu-id="7a707-144">Пользовательский Интерфейс также показано, как будет выглядеть навигационных ссылок сайта узла после надстройки загружает файл JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7a707-144">The add-in UI also shows you how the navigational links will appear on the host site after the add-in uploads the JavaScript file.</span></span>

<span data-ttu-id="7a707-145">Следующий код в файле topnav.js использует JSOM для поиска предпочтительный язык пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a707-145">The following code in the topnav.js file uses JSOM to check for the user's preferred language.</span></span>

```
var targetUser = "i:0#.f|membership|" + _spPageContextInfo.userLoginName;
        context = new SP.ClientContext.get_current();
var peopleManager = new SP.UserProfiles.PeopleManager(context);
var userProperty = peopleManager.getUserProfilePropertyFor(targetUser, "SPS-MUILanguages");
```

<span data-ttu-id="7a707-146">Надстройка затем определяет, соответствует ли язык пользователя один из доступных языков.</span><span class="sxs-lookup"><span data-stu-id="7a707-146">The add-in then determines whether the user's language preference matches one of the enabled languages.</span></span> <span data-ttu-id="7a707-147">Если совпадение найдено, следующий код получает условия и связанные метки для предпочтительный язык пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a707-147">If it finds a match, the following code gets the terms and the associated labels for the user's preferred language.</span></span>

```
while (termEnumerator.moveNext()) {
    var currentTerm = termEnumerator.get_current();
    var label = currentTerm.getDefaultLabel(lcid);

    termItems.push(currentTerm);
    termLabels.push(label);
    context.load(currentTerm);
```

<span data-ttu-id="7a707-148">И, наконец следующий код в файле topnav.js вставляет ссылки, содержащие термины в элемент верхнего переходов сайта узла.</span><span class="sxs-lookup"><span data-stu-id="7a707-148">Finally, the following code in the topnav.js file inserts links that contain the terms into the top navigational element of the host site.</span></span>

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

## <a name="taxonomy-picker-control"></a><span data-ttu-id="7a707-149">Элемент управления для выбора таксономии</span><span class="sxs-lookup"><span data-stu-id="7a707-149">Taxonomy picker control</span></span>
<span data-ttu-id="7a707-150"><a name="bmTaxPicker"> </a></span><span class="sxs-lookup"><span data-stu-id="7a707-150"></span></span>

<span data-ttu-id="7a707-151">Пример [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) показано, как реализовать элемента управления "Выбор" таксономии в размещенном у поставщика надстройки с.</span><span class="sxs-lookup"><span data-stu-id="7a707-151">The [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) sample shows you how to implement a taxonomy picker control in a provider-hosted add-in.</span></span> <span data-ttu-id="7a707-152">Когда пользователь начинает ввод терминов в поле ввода текста, поиск элемента управления банк терминов для потенциал сопоставляет и отображает их в списке в поле ввода.</span><span class="sxs-lookup"><span data-stu-id="7a707-152">When the user starts typing a term into the text input box, the control searches the term store for potential matches and displays them in a list under the input box.</span></span>

<span data-ttu-id="7a707-153">Надстройка создает HTML-страницу, которая соответствует требования средства выбора JSOM таксономии и добавление и настройка элемента управления.</span><span class="sxs-lookup"><span data-stu-id="7a707-153">The add-in creates an HTML page that conforms to the JSOM taxonomy picker requirements, and then adds and configures the control.</span></span> <span data-ttu-id="7a707-154">Библиотека JSOM используется для запроса банк терминов сайта узла.</span><span class="sxs-lookup"><span data-stu-id="7a707-154">It uses the JSOM library to query the host site's term store.</span></span> <span data-ttu-id="7a707-155">Средство выбора таксономии взаимодействует с SharePoint служба управляемых метаданных, который необходимо разрешение на запись на уровне разрешений таксономии, чтобы его можно чтения наборы терминов закрытой и записи в открытые наборы терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-155">The taxonomy picker communicates with the SharePoint Managed Metadata Service, which requires write permission at the taxonomy permission scope so that it can read from closed term sets and write to open term sets.</span></span> <span data-ttu-id="7a707-156">Убедитесь в том, что файл AppManifest.xml значение разрешения на запись в соответствующие области.</span><span class="sxs-lookup"><span data-stu-id="7a707-156">Make sure that the AppManifest.xml file has set the write permission at the appropriate scope.</span></span>

<span data-ttu-id="7a707-157">Папка скрипты проекта [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) содержит файлы app.js и taxonomypickercontrol.js (а также таксономии "Выбор" файл ресурсов для поддержки дополнительных языков).</span><span class="sxs-lookup"><span data-stu-id="7a707-157">The Scripts folder of the [Core.TaxonomyPicker](https://github.com/SharePoint/PnP/tree/dev/Components/Core.TaxonomyPicker) project contains app.js and taxonomypickercontrol.js files (along with a taxonomy picker resource file for additional language support).</span></span> <span data-ttu-id="7a707-158">Файл app.js извлекает контекст клиента с помощью междоменной библиотеки и подключает HTML-код в файл Default.aspx в элементе управления средства выбора таксономии.</span><span class="sxs-lookup"><span data-stu-id="7a707-158">The app.js file fetches client context by using the cross-domain library and hooks the HTML in the Default.aspx file into the taxonomy picker control.</span></span> <span data-ttu-id="7a707-159">Файл Default.aspx содержит скрытых полей, который реализует текстовое поле и возможность выбора таксономии.</span><span class="sxs-lookup"><span data-stu-id="7a707-159">The Default.aspx file contains the hidden field that implements both the text box and the taxonomy picker capability.</span></span> <span data-ttu-id="7a707-160">Он также добавляет маркированного списка для отображения предложений, возвращенные банка терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-160">It also adds a bulleted list to display suggestions returned from the term store.</span></span>

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

<span data-ttu-id="7a707-161">Выберите файл app.js создает и настраивает элемент управления "Выбор" таксономии.</span><span class="sxs-lookup"><span data-stu-id="7a707-161">The app.js file then creates and configures a taxonomy picker control.</span></span>

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

<span data-ttu-id="7a707-162">Элемент управления "Выбор" таксономии использует следующий код для открытия экземпляра **TaxonomySession** в JSOM для загрузки с условиями от банка терминов.</span><span class="sxs-lookup"><span data-stu-id="7a707-162">The taxonomy picker control uses the following code to open a  **TaxonomySession** instance in the JSOM to load all the terms from the term store.</span></span>

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

<span data-ttu-id="7a707-163">Элемент управления "Выбор" таксономии ищет потенциальные совпадения из загруженных термины и добавляет новых терминов в банке терминов при необходимости.</span><span class="sxs-lookup"><span data-stu-id="7a707-163">The taxonomy picker control then looks for potential matches from the loaded terms, and adds new terms to the term store as needed.</span></span>

## <a name="see-also"></a><span data-ttu-id="7a707-164">См. также</span><span class="sxs-lookup"><span data-stu-id="7a707-164">See also</span></span>
<span data-ttu-id="7a707-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7a707-165"></span></span>

- [<span data-ttu-id="7a707-166">Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="7a707-166">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="7a707-167">Доступ к данным SharePoint 2013 из надстроек с помощью междоменной библиотеки</span><span class="sxs-lookup"><span data-stu-id="7a707-167">Access SharePoint 2013 data from add-ins using the cross-domain library</span></span>](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx)
