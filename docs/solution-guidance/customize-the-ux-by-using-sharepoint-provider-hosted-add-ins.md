---
title: "Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек"
ms.date: 11/03/2017
ms.openlocfilehash: 28f14fa6a15e367232b1384952ed6b7fefbfb3de
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="customize-the-ux-by-using-sharepoint-provider-hosted-add-ins"></a>Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек

Настройка компонентов пользовательского интерфейса SharePoint удаленно с помощью провайдера надстроек. 

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

В этой статье описываются примеры, показывающие, рекомендации по настройке компонентов пользовательского интерфейса SharePoint, включая следующие сценарии:

- Управление страницами (Добавление и изменение вики-страниц).
    
- Отображение надстроек и данных в модальных диалоговых окон.
    
- Создание персонализированной элементов пользовательского интерфейса.
    
- Клиентская обработка (развертывание файлов JSLink, настройки отображения поля в списках SharePoint).
    
- Веб-части и добавить в часть выполнение различных операций (удаленно подготовки и выполнения от части скрипта надстройки в надстройке размещением у поставщика).
    
- Объединение данных и кэширование (с использованием локальное хранилище HTML5 и файлы cookie HTTP сократить количество вызовов службы в SharePoint).

## <a name="page-manipulation"></a>Управление страницами
<a name="bmPageManipulate"> </a>

Пример [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ModifyPages) включает два сценария обработки страницы:

- Создание вики-страниц.
    
- Изменение макета вики-страниц. 
    
В этом примере используются библиотеки страниц сайта по умолчанию и существующих встроенных макетов. Также можно обновить его на использование библиотека настраиваемых вики-страниц и пользовательских макетов. Пользовательский Интерфейс надстройки включает в себя две кнопки, создание вики-страницы и две ссылки для просмотра вики-страницы, которые можно создать.

**На рисунке 1. Начальная страница для образца манипуляции страницы**

![Страница для образца манипуляции страница запуска](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/8c6353d9-b339-4563-b945-eaea3d4da2a8.png)

Пример кода в первом случае определяет, будет ли вы уже создали вики-страниц. Если нет, ее добавляет файл в библиотеке страниц сайта и возвращает URL-адреса.

**Примечание:** Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.

```
var newpage = pageLibrary.RootFolder.Files.AddTemplateFile(newWikiPageUrl, TemplateFileType.WikiPage);
ctx.Load(newpage);
ctx.ExecuteQuery();
wikiPageUrl = String.Format("sitepages/{0}", wikiPageName);
```

В обоих случаях в этом примере добавляется введены с помощью текстовое поле на странице "Запуск" с помощью метода **AddHtmlToWikiPage** в вспомогательный класс с именем **LabHelper**HTML-код. Этот метод вставляет HTML-код из формы внутри поля _WikiField_ вики-страницы.

```
public void AddHtmlToWikiPage(ClientContext ctx, Web web, string folder, string html, string page)
        {
            Microsoft.SharePoint.Client.Folder pagesLib = web.GetFolderByServerRelativeUrl(folder);
            ctx.Load(pagesLib.Files);
            ctx.ExecuteQuery();

            Microsoft.SharePoint.Client.File wikiPage = null;

            foreach (Microsoft.SharePoint.Client.File aspxFile in pagesLib.Files)
            {
                if (aspxFile.Name.Equals(page, StringComparison.InvariantCultureIgnoreCase))
                {
                    wikiPage = aspxFile;
                    break;
                }
            }

            if (wikiPage == null)
            {
                return;
            }

            ctx.Load(wikiPage);
            ctx.Load(wikiPage.ListItemAllFields);
            ctx.ExecuteQuery();

            string wikiField = (string)wikiPage.ListItemAllFields["WikiField"];

            Microsoft.SharePoint.Client.ListItem listItem = wikiPage.ListItemAllFields;
            listItem["WikiField"] = html;
            listItem.Update();
            ctx.ExecuteQuery();
        }
```

Пример кода для второй сценарий создает новый экземпляр **WebPartEntity** . Затем он использует методы в вспомогательный класс для заполнения веб-части с помощью XML. XML-код отображается список рекомендуемых ссылок, включая [http://www.bing.com](http://www.bing.com) и на домашней странице [Разработчик офисных решений/PnP репозиториев](https://github.com/SharePoint/PnP) репозитория.

```
WebPartEntity wp2 = new WebPartEntity();
wp2.WebPartXml = new LabHelper().WpPromotedLinks(linksID, string.Format("{0}/Lists/{1}", 
                                                                Request.QueryString["SPHostUrl"], "Links"), 
                                                                string.Format("{0}/{1}", Request.QueryString["SPHostUrl"], 
                                                                scenario2PageUrl), "$Resources:core,linksList");
wp2.WebPartIndex = 1;
wp2.WebPartTitle = "Links";

new LabHelper().AddWebPartToWikiPage(ctx, ctx.Web, "SitePages", wp2, scenario2Page, 2, 1, false);
new LabHelper().AddHtmlToWikiPage(ctx, ctx.Web, "SitePages", htmlEntry.Text, scenario2Page, 2, 2);

this.hplPage2.NavigateUrl = string.Format("{0}/{1}", Request.QueryString["SPHostUrl"], scenario2PageUrl);
```

Вспомогательный код отображает рекомендуемых ссылок с таблицей внутри веб-части **XsltListViewWebPart** .

**На рисунке 2. Вторая страница вики-сайта с помощью XsltListViewWebPart и рекомендуемых ссылок в таблице**

![Вторая страница вики-сайта с помощью XsltListViewWeb часть и рекомендуемых ссылок в таблице](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/6dc60a0b-b11a-4fe9-ad06-6b4d0d4b8b24.png)

Объект **WpPromotedLinks** в экземпляре **LabHelper** содержит XML, который определяет внешний вид веб-часть, будут внедрены в вики-страниц. Метод **AddWebPartToWikiPage** вставляет недавно определенной веб-части в новое `div` тега на вики-страниц.

```
XmlDocument xd = new XmlDocument();
            xd.PreserveWhitespace = true;
            xd.LoadXml(wikiField);

            // Sometimes the wikifield content seems to be surrounded by an additional div. 
            XmlElement layoutsTable = xd.SelectSingleNode("div/div/table") as XmlElement;
            if (layoutsTable == null)
            {
                layoutsTable = xd.SelectSingleNode("div/table") as XmlElement;
            }

            XmlElement layoutsZoneInner = layoutsTable.SelectSingleNode(string.Format("tbody/tr[{0}]/td[{1}]/div/div", row, col)) as XmlElement;
            // - space element
            XmlElement space = xd.CreateElement("p");
            XmlText text = xd.CreateTextNode(" ");
            space.AppendChild(text);

            // - wpBoxDiv
            XmlElement wpBoxDiv = xd.CreateElement("div");
            layoutsZoneInner.AppendChild(wpBoxDiv);

            if (addSpace)
            {
                layoutsZoneInner.AppendChild(space);
            }

            XmlAttribute attribute = xd.CreateAttribute("class");
            wpBoxDiv.Attributes.Append(attribute);
            attribute.Value = "ms-rtestate-read ms-rte-wpbox";
            attribute = xd.CreateAttribute("contentEditable");
            wpBoxDiv.Attributes.Append(attribute);
            attribute.Value = "false";
            // - div1
            XmlElement div1 = xd.CreateElement("div");
            wpBoxDiv.AppendChild(div1);
            div1.IsEmpty = false;
            attribute = xd.CreateAttribute("class");
            div1.Attributes.Append(attribute);
            attribute.Value = "ms-rtestate-read " + wpdNew.Id.ToString("D");
            attribute = xd.CreateAttribute("id");
            div1.Attributes.Append(attribute);
            attribute.Value = "div_" + wpdNew.Id.ToString("D");
            // - div2
            XmlElement div2 = xd.CreateElement("div");
            wpBoxDiv.AppendChild(div2);
            div2.IsEmpty = false;
            attribute = xd.CreateAttribute("style");
            div2.Attributes.Append(attribute);
            attribute.Value = "display:none";
            attribute = xd.CreateAttribute("id");
            div2.Attributes.Append(attribute);
            attribute.Value = "vid_" + wpdNew.Id.ToString("D");

            ListItem listItem = webPartPage.ListItemAllFields;
            listItem["WikiField"] = xd.OuterXml;
            listItem.Update();
            ctx.ExecuteQuery();
```

## <a name="showing-add-ins-and-data-in-modal-dialog-boxes"></a>Отображение надстроек и данных в модальных диалоговых окон
<a name="bmPageManipulate"> </a>

Пример [Core.Dialog](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.Dialog) показаны два метода для внедрения поле модальное диалоговое окно ссылки. Эти ссылки отображает страницу, размещаемые у поставщика надстройки в сайт узла SharePoint. Надстройки с помощью клиентской объектной модели (CSOM) для создания настраиваемого действия и JavaScript для запуска и отображать данные, содержащиеся в диалоговом окне. Так как некоторые из этих сведений поступают из сайта узла, также используется объектная модель JavaScript (JSOM) для получения сведений из сайта узла. И так как надстройки выполняется в другом домене размещения сайта SharePoint, также использует кросс доменной библиотеки SharePoint для выполнения вызовов на сайт узла.

**Примечание:** Дополнительные сведения об использовании междоменной библиотеки в этом сценарии видеть [данные доступа к SharePoint 2013 от надстроек с помощью междоменной библиотеки](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx).

Начальная страница — это страница, которая отображается в диалоговом окне. Обрабатывать все различия в отображения, заданном контексте отображения (диалоговое окно и веб-страницы), надстройки определяет, является ли он отображается в диалоговом окне. Это осуществляется с помощью параметра строки запроса, который передается, а также ссылки, запустите диалоговых окон.

```
private string SetIsDlg(string isDlgValue)
        {
            var urlParams = HttpUtility.ParseQueryString(Request.QueryString.ToString());
            urlParams.Set("IsDlg", isDlgValue);
            return string.Format("{0}://{1}:{2}{3}?{4}", Request.Url.Scheme, Request.Url.Host, Request.Url.Port, Request.Url.AbsolutePath, urlParams.ToString());
        }
```

Можно например, выбрать для отображения определенных элементов пользовательского интерфейса (например, кнопки) или даже различные макеты, в зависимости от того, является ли содержимое отображается в диалоговом окне.

Начальная страница пользовательского интерфейса представлены два варианта для создания ссылки на поле, а также список всех списков на веб-сайт. Также в нем представлен **ОК** и **Отмена** кнопок, можно использовать в контексте поле диалогового окна для закрытия диалогового окна поля и/или строки дополнительные действия в надстройку.

После нажатия кнопки **Добавить элемент меню** надстройки создает объект **CustomActionEntity** , который запускает диалоговое окно. Затем метод [расширения основных OfficeDevPnP](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) , с именем **AddCustomAction** используется для добавления нового настраиваемого действия в меню **Параметры сайта** .

```
StringBuilder modelDialogScript = new StringBuilder(10);
modelDialogScript.Append("javascript:var dlg=SP.UI.ModalDialog.showModalDialog({url: '");
modelDialogScript.Append(String.Format("{0}", SetIsDlg("1")));
modelDialogScript.Append("', dialogReturnValueCallback:function(res, val) {} });");       

// Create a custom action.
CustomActionEntity customAction = new CustomActionEntity()
{
  Title = "Office AMS Dialog sample",                
  Description = "Shows how to start an add-in inside a dialog box.",
  Location = "Microsoft.SharePoint.StandardMenu",
  Group = "SiteActions",
  Sequence = 10000,
  Url = modelDialogScript.ToString(),
};

// Add the custom action to the site.
cc.Web.AddCustomAction(customAction);
```

Метод **AddCustomAction** добавляет дополнительное действие в коллекцию **UserCustomActions** , который связан с сайтом SharePoint.

```
var newAction = existingActions.Add();
            newAction.Description = customAction.Description;
            newAction.Location = customAction.Location;
            if (customAction.Location == JavaScriptExtensions.SCRIPT_LOCATION)
            {
                newAction.ScriptBlock = customAction.ScriptBlock;
            }
            else
            {
                newAction.Sequence = customAction.Sequence;
                newAction.Url = customAction.Url;
                newAction.Group = customAction.Group;
                newAction.Title = customAction.Title;
                newAction.ImageUrl = customAction.ImageUrl;
                if (customAction.Rights != null)
                {
                    newAction.Rights = customAction.Rights;
                }
            }
            newAction.Update();
            web.Context.Load(web, w => w.UserCustomActions);
            web.Context.ExecuteQuery();
```

При нажатии кнопки **Добавить страницы с веб-часть редактора скрипт** , надстройка использует методы **AddWikiPage** и **AddWebPartToWikiPage** создает вики-страниц в библиотеке страниц сайта и добавляет настроенный редактор сценариев веб-части на страницу.

```
string scenario1Page = String.Format("scenario1-{0}.aspx", DateTime.Now.Ticks);
string scenario1PageUrl = cc.Web.AddWikiPage("Site Pages", scenario1Page);
cc.Web.AddLayoutToWikiPage("SitePages", WikiPageLayout.OneColumn, scenario1Page);
WebPartEntity scriptEditorWp = new WebPartEntity();
scriptEditorWp.WebPartXml = ScriptEditorWebPart();
scriptEditorWp.WebPartIndex = 1;
scriptEditorWp.WebPartTitle = "Script editor test"; 
cc.Web.AddWebPartToWikiPage("SitePages", scriptEditorWp, scenario1Page, 1, 1, false);
```

Метод **AddWikiPage** загружает библиотеку страниц сайта. Если вики-страниц, указанного идентификатором [основных OfficeDevPnP](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) надстройки еще не существует, он создает страницы.

```
public static string AddWikiPage(this Web web, string wikiPageLibraryName, string wikiPageName)
        {
            string wikiPageUrl = "";


            var pageLibrary = web.Lists.GetByTitle(wikiPageLibraryName);

            web.Context.Load(pageLibrary.RootFolder, f => f.ServerRelativeUrl);
            web.Context.ExecuteQuery();

            var pageLibraryUrl = pageLibrary.RootFolder.ServerRelativeUrl;
            var newWikiPageUrl = pageLibraryUrl + "/" + wikiPageName;

            var currentPageFile = web.GetFileByServerRelativeUrl(newWikiPageUrl);

            web.Context.Load(currentPageFile, f => f.Exists);
            web.Context.ExecuteQuery();

            if (!currentPageFile.Exists)
            {
                var newpage = pageLibrary.RootFolder.Files.AddTemplateFile(newWikiPageUrl, TemplateFileType.WikiPage);

                web.Context.Load(newpage);
                web.Context.ExecuteQuery();

                wikiPageUrl = UrlUtility.Combine("sitepages", wikiPageName);
            }

            return wikiPageUrl;
        }
```

Метод **AddWebPartToWikiPage** вставляет недавно определенной веб-части в новое `<div>` тега на вики-страниц. Затем используется для получения информации, которая заполняет список списков SharePoint на хост-сайта JSOM и междоменной библиотеки.

```
function printAllListNamesFromHostWeb() {
        var context;
        var factory;
        var appContextSite;
        var collList;

        context = new SP.ClientContext(appWebUrl);
        factory = new SP.ProxyWebRequestExecutorFactory(appWebUrl);
        context.set_webRequestExecutorFactory(factory);
        appContextSite = new SP.AppContextSite(context, spHostUrl);

        this.web = appContextSite.get_web();
        collList = this.web.get_lists();
        context.load(collList);

        context.executeQueryAsync(
            Function.createDelegate(this, successHandler),
            Function.createDelegate(this, errorHandler)
        );
```

## <a name="personalized-ui-elements"></a>Личные элементы пользовательского интерфейса
<a name="bmPersonalized"> </a>

Пример [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization) показано, как использовать внедренные JavaScript и значения, хранящиеся в профилях пользователей и списки SharePoint для индивидуальной настройки элементы пользовательского интерфейса на веб-сайт. Он также использует локальное хранилище HTML5 для сведения к минимуму звонков на сайт узла.

Пример начальная страница выдает запрос добавьте одну из трех строк (XX, гг или ЯЯ) **Сведения обо мне** разделе на странице профиля пользователя.

Добавить в уже развернут три изображения и списка SharePoint, который содержит заголовки и URL-адреса для каждого изображения, а также дополнительные поля, который привязан к одной из трех строк каждого изображения. После нажатия кнопки **параметров вставки** надстройки внедряет файл personalize.js в коллекции настраиваемых действий пользователя.

```
public void AddPersonalizeJsLink(ClientContext ctx, Web web)
        {
            string scenarioUrl = String.Format("{0}://{1}:{2}/Scripts", this.Request.Url.Scheme,
                                                this.Request.Url.DnsSafeHost, this.Request.Url.Port);
            string revision = Guid.NewGuid().ToString().Replace("-", "");
            string personalizeJsLink = string.Format("{0}/{1}?rev={2}", scenarioUrl, "personalize.js", revision);

            StringBuilder scripts = new StringBuilder(@"
                var headID = document.getElementsByTagName('head')[0]; 
                var");

            scripts.AppendFormat(@"
                newScript = document.createElement('script');
                newScript.type = 'text/javascript';
                newScript.src = '{0}';
                headID.appendChild(newScript);", personalizeJsLink);
            string scriptBlock = scripts.ToString();

            var existingActions = web.UserCustomActions;
            ctx.Load(existingActions);
            ctx.ExecuteQuery();

            var actions = existingActions.ToArray();
            foreach (var action in actions)
            {
                if (action.Description == "personalize" &amp;&amp;
                    action.Location == "ScriptLink")
                {
                    action.DeleteObject();
                    ctx.ExecuteQuery();
                }
            }

            var newAction = existingActions.Add();
            newAction.Description = "personalize";
            newAction.Location = "ScriptLink";
            
            newAction.ScriptBlock = scriptBlock;
            newAction.Update();
            ctx.Load(web, s => s.UserCustomActions);
            ctx.ExecuteQuery();
        }
```

Так как сайты группы SharePoint по умолчанию используется [Стратегия минимальной загрузки (MDS)](http://msdn.microsoft.com/en-us/library/office/dn456544%28v=office.15%29.aspx), код в файле personalize.js сначала пытается зарегистрироваться MDS. Таким образом, при загрузке страницы, которая содержит JavaScript, MDS компонентами ядра СУБД starets функцию main (**RemoteManager_Inject**). Если MDS отключен, эта функция запускается немедленно.

```
// Register script for MDS, if possible.
RegisterModuleInit("personalize.js", RemoteManager_Inject); //MDS registration
RemoteManager_Inject(); //non-MDS run

if (typeof (Sys) != "undefined" &amp;&amp; Boolean(Sys) &amp;&amp; Boolean(Sys.Application)) {
    Sys.Application.notifyScriptLoaded();h
}

if (typeof (NotifyScriptLoadedAndExecuteWaitingJobs) == "function") {
    NotifyScriptLoadedAndExecuteWaitingJobs("scenario1.js");
}
// The RemoteManager_Inject function is the entry point for loading the other scripts that perform the customizations. When a given script depends on another script, be sure to load the dependent script after the one on which it depends. This sample loads the JQuery library before the personalizeIt function that uses JQuery.
function RemoteManager_Inject() {

    var jQuery = "https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js";

    // Load jQuery. 
    loadScript(jQuery, function () {

        personalizeIt();

    });
}
```

Функция **personalizeIt()** проверяет локальное хранилище HTML5, прежде чем оно берет сведения о профилях пользователей. Если он переходит на сведения о профилях пользователей, он содержит сведения, которые он получает в локальном хранилище HTML5.

```
function personalizeIt() {
    clientContext = SP.ClientContext.get_current();

    var fileref = document.createElement('script');
    fileref.setAttribute("type", "text/javascript");
    fileref.setAttribute("src", "/_layouts/15/SP.UserProfiles.js");
    document.getElementsByTagName("head")[0].appendChild(fileref);

    SP.SOD.executeOrDelayUntilScriptLoaded(function () {        

        // Get localstorage values if they exist.
        buCode = localStorage.getItem("bucode");
        buCodeTimeStamp = localStorage.getItem("buCodeTimeStamp");

        // Determine whether the page already has embedded personalized image.
        var pageTitle = $('#pageTitle')[0].innerHTML;
        if (pageTitle.indexOf("img") > -1) {
            personalized = true;
        }
        else {
            personalized = false;
        }        

        // If nothing is in localstorage, get profile data, which will also populate localstorage.
        if (buCode == "" || buCode == null) {
            getProfileData(clientContext);
            personalized = false;
        }
        else {
            // Check for expiration.            
            if (isKeyExpired("buCodeTimeStamp")) {                
                getProfileData(clientContext);

                if (buCode != "" || buCode != null) {
                    // Set timestamp for expiration.
                    currentTime = Math.floor((new Date().getTime()) / 1000);
                    localStorage.setItem("buCodeTimeStamp", currentTime);

                    // Set personalized to false so that the code can check for a new image in case buCode was updated.
                    personalized = false;
                }
            }            
        }

        // Load image or make sure it is current based on the value in AboutMe.
        if (!personalized) {
            loadPersonalizedImage(buCode);
        }


    }, 'SP.UserProfiles.js');
}
```

Файл personalize.js также содержит код, который проверяет, истек ли срок действия ключа локального хранилища. Это не встроенных в локальном хранилище HTML5.

```
// Check to see if the key has expired
function isKeyExpired(TimeStampKey) {

    // Retrieve the example setting for expiration in seconds.
    var expiryStamp = localStorage.getItem(TimeStampKey);

    if (expiryStamp != null &amp;&amp; cacheTimeout != null) {

        // Retrieve the timestamp and compare against specified cache timeout settings to see if it is expired.
        var currentTime = Math.floor((new Date().getTime()) / 1000);

        if (currentTime - parseInt(expiryStamp) > parseInt(cacheTimeout)) {
            return true; //Expired
        }
        else {
            return false;
        }
    }
    else {
        //default 
        return true;
    }
}
```

## <a name="client-side-rendering"></a>Обработка на стороне клиента
<a name="bmPersonalized"> </a>

Пример [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering) описывается использование размещение у поставщика в надстройке удаленно подготавливать артефактов SharePoint и JSLink файлов с использованием обработки на стороне клиента для настройки внешнего вида и поведения полей списка SharePoint. Файлы JSLink и присвойте обработки на стороне клиента, можно настроить как элементы управления на странице SharePoint (представления списка, списка полей и добавление и изменение форм) отображаются. Этот элемент управления может частичному или полному устранению потребности в настраиваемых типов полей. Отображение на стороне клиента позволяет удаленно управлять внешний вид поля списка в удаленном режиме.

Примера объединяет примеры JSLink из [примеров кода со стороны клиента визуализации (JSLink)](http://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a) в одной размещением у поставщика надстройки для SharePoint, подготавливает файлы JSLink. Отображение на стороне клиента позволяет использовать стандартный веб-технологий, таких как HTML и JavaScript, определение логики отрисовки типы настраиваемых и предварительно определенные поля.

При запуске примера начальная страница выдает запрос для подготовки к примеры.

**На рисунке 3. Начальная страница образца обработки на стороне клиента**

![Откройте страницу пример обработки на стороне клиента](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/bfa1b472-976b-4bdc-95df-537cee5570e6.png)

При выборе **Примеры временного**надстройки развертывает изображения, а также все списки SharePoint, представления списка, элементов списка, форм и файлов JavaScript, используемые в каждом примера. Надстройка создает папку с именем JSLink-примеры в библиотеку стилей, а затем загружает файлы JavaScript в эту папку. Метод **UploadFileToFolder** работает передача и возврат каждого файла JavaScript.

```
public static void UploadFileToFolder(Web web, string filePath, Folder folder)
        {
            using (FileStream fs = new FileStream(filePath, FileMode.Open))
            {
                FileCreationInformation flciNewFile = new FileCreationInformation();

                flciNewFile.ContentStream = fs;
                flciNewFile.Url = System.IO.Path.GetFileName(filePath);
                flciNewFile.Overwrite = true;

                Microsoft.SharePoint.Client.File uploadFile = folder.Files.Add(flciNewFile);
                uploadFile.CheckIn("CSR sample js file", CheckinType.MajorCheckIn);

                folder.Context.Load(uploadFile);
                folder.Context.ExecuteQuery();
            }
        }
```

### <a name="sample-1-apply-formatting-to-a-list-column"></a>Пример 1: Применение форматирования для столбца списка

Пример 1 показано, как применять форматирование к столбца списка на основе значения поля. Значения полей приоритет 1 (высокий), 2 (обычный) и 3 (низкий) отображаются в красный, оранжевый и желтый.

**На рисунке 4. Настраиваемый список отображения поля**

![Настраиваемый список отображения поля](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/1481adfa-efc9-4b59-b07f-bb330f02d2bb.png)

Следующие JavaScript переопределяет отображения поля по умолчанию и создает новый шаблон отображения для поля списка **приоритет** . Эта технология анонимная функция, которая загружает контекстные сведения о поле, отображаемое для переопределения используется в все примеры.

```
(function () {

    // Create object that has the context information about the field that you want to render differently.
    var priorityFiledContext = {};
    priorityFiledContext.Templates = {};
    priorityFiledContext.Templates.Fields = {
        // Apply the new rendering for Priority field in List View.
        "Priority": { "View": priorityFiledTemplate }
    };

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(priorityFiledContext);

})();

// This function provides the rendering logic for list view.
function priorityFiledTemplate(ctx) {

    var priority = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];

    // Return HTML element with appropriate color based on the Priority column's value.
    switch (priority) {
        case "(1) High":
            return "<span style='color :#f00'>" + priority + "</span>";
            break;
        case "(2) Normal":
            return "<span style='color :#ff6a00'>" + priority + "</span>";
            break;
        case "(3) Low":
            return "<span style='color :#cab023'>" + priority + "</span>";
    }
}
```

### <a name="sample-2-shorten-long-text"></a>Пример 2: Сокращение длинного текста

Пример 2 показано, как удалять длинный текст в поле **Body** список **извещений** . Полный текст отображается как всплывающее окно, которое появляется при наведении указателя на элемент списка, как показано на рисунке 8.

**На рисунке 5. Всплывающее окно показывает отображаемое поле сокращенный список**

![Всплывающее окно показывает отображаемое поле усеченных списка](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/a5e6d2af-f1f9-4bcc-9278-e56fd42c2e64.png)

Следующие JavaScript сокращает поля к **основному** тексту и вызывает полный текст, который отображается как всплывающее окно с помощью атрибут **title** на **охватывать** тег.

```
function bodyFiledTemplate(ctx) {

    var bodyValue = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];

    // This regex expression is used to delete HTML tags from the Body field.
    var regex = /(<([^>]+)>)/ig;

    bodyValue = bodyValue.replace(regex, "");

    var newBodyValue = bodyValue;

    if (bodyValue &amp;&amp; bodyValue.length >= 100)
    {
        newBodyValue = bodyValue.substring(0, 100) + " ...";
    }

    return "<span title='" + bodyValue + "'>" + newBodyValue + "</span>";

}
```

### <a name="sample-3-display-an-image-with-a-document-name"></a>Пример 3: Отобразить изображение с именем документа

Пример 3 показано, как отобразить изображение рядом с именем документа в библиотеке документов. Красный значок появляется при использовании значения поля **Конфиденциальность** **Да**, как показано на рисунке 6. 

**На рисунке 6. Отображаемое изображение рядом с именем документа**

![Отображаемое изображение рядом с именем документа](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/f2768dfd-ae05-4afc-8dbe-26dc4e7dca6d.png)

Следующие JavaScript проверяет значение поля **Конфиденциальность** и затем настраивает отображаемое **имя** поля, на основе значения другого поля. В примере используется изображения, который загрузил при выборе **Примеры подготовки**. 

```
function linkFilenameFiledTemplate(ctx) {

    var confidential = ctx.CurrentItem["Confidential"];
    var title = ctx.CurrentItem["FileLeafRef"];

    // This Regex expression use to delete extension (.docx, .pdf ...) form the file name.
    title = title.replace(/\.[^/.]+$/, "")

    // Check confidential field value.
    if (confidential &amp;&amp; confidential.toLowerCase() == 'yes') {
        // Render HTML that contains the file name and the confidential icon
        return title + "&amp;nbsp;<img src= '" + _spPageContextInfo.siteServerRelativeUrl + "/Style%20Library/JSLink-Samples/imgs/Confidential.png' alt='Confidential Document' title='Confidential Document'/>";
    }
    else
    {
        return title;
    }
}
```

### <a name="sample-4-display-a-bar-chart"></a>Пример 4: Отображения линейчатой диаграммы

Пример 4 показано, как для отображения линейчатой диаграммы в поле **% завершения** списка задач. Внешний вид линейчатая диаграмма зависит от значение поля **% завершения** , как показано на рисунке 10. Обратите внимание на то, что линейчатая диаграмма, также будут отображаться в формах для создания и редактирования элементов списка задач.

Следующий код создает отображения линейчатой диаграммы и связывание его с помощью представления и отображения форм (**percentCompleteViewFiledTemplate**), а затем с помощью нового и редактировать формы (**percentCompleteEditFiledTemplate**).

```
// This function provides the rendering logic for View and Display forms.
function percentCompleteViewFiledTemplate(ctx) {

    var percentComplete = ctx.CurrentItem[ctx.CurrentFieldSchema.Name];
    return "<div style='background-color: #e5e5e5; width: 100px;  display:inline-block;'> \
            <div style='width: " + percentComplete.replace(/\s+/g, '') + "; background-color: #0094ff;'> \
            &amp;nbsp;</div></div>&amp;nbsp;" + percentComplete;

}

// This function provides the rendering logic for New and Edit forms.
function percentCompleteEditFiledTemplate(ctx) {

    var formCtx = SPClientTemplates.Utility.GetFormContextForCurrentField(ctx);

    // Register a callback just before submit.
    formCtx.registerGetValueCallback(formCtx.fieldName, function () {
        return document.getElementById('inpPercentComplete').value;
    });

    return "<input type='range' id='inpPercentComplete' name='inpPercentComplete' min='0' max='100' \
            oninput='outPercentComplete.value=inpPercentComplete.value' value='" + formCtx.fieldValue + "' /> \
            <output name='outPercentComplete' for='inpPercentComplete' >" + formCtx.fieldValue + "</output>%";
}
```

**На рисунке 7. Линейчатая диаграмма, отображаемых в поле % завершения**

![Линейчатая диаграмма, отображаемых в поле % завершения](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fb36f27a-2eb7-4c5f-8428-b85b65369ea9.png)

### <a name="sample-5-change-the-rendering-template"></a>Пример 5: Изменение шаблона отображения

Пример 5 показано, как изменить шаблон отображения представления списка. Это представление отображает заголовки элемента списка, разверните узел как accordions при их выборе. Расширенное представление отображает дополнительные список полей элемента, как показано на рисунке 8.

**На рисунке 8. Представления списков свернутые и расширенное элемента**

![Представления списков свернутые и расширенное элемента](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fd185eef-e2be-4523-9adb-d524b84ecc26.png)

Следующий код выполняет настройку шаблона и регистрирует его с помощью шаблона списка. Выполняет настройку общий макет и затем использует обработчик события **OnPostRender** для регистрации функцию JavaScript, которая выполняется при отображении списка. Эта функция событие связывается с CSS и событие обработки, который реализует аккордеона функциональные возможности.

```
(function () {

    // jQuery library is required in this sample.
    // Fallback to loading jQuery from a CDN path if the local is unavailable
    (window.jQuery || document.write('<script src="//ajax.aspnetcdn.com/ajax/jquery/jquery-1.10.0.min.js"><\/script>'));

    // Create object that has the context information about the field that you want to render differently.
    var accordionContext = {};
    accordionContext.Templates = {};

    // Be careful when adding the header for the template, because it will break the default list view render.
    accordionContext.Templates.Header = "<div class='accordion'>";
    accordionContext.Templates.Footer = "</div>";

    // Add OnPostRender event handler to add accordion click events and style.
    accordionContext.OnPostRender = accordionOnPostRender;

    // This line of code tells the TemplateManager that you want to change all the HTML for item row rendering.
    accordionContext.Templates.Item = accordionTemplate;

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(accordionContext);

})();

// This function provides the rendering logic.
function accordionTemplate(ctx) {
    var title = ctx.CurrentItem["Title"];
    var description = ctx.CurrentItem["Description"];

    // Return whole item html
    return "<h2>" + title + "</h2><p>" + description + "</p><br/>";
}

function accordionOnPostRender() {

    // Register event to collapse and expand when selecting accordion header.
    $('.accordion h2').click(function () {
        $(this).next().slideToggle();
    }).next().hide();

    $('.accordion h2').css('cursor', 'pointer');
}
```

### <a name="sample-6-validate-field-values"></a>Пример 6: Проверка значений полей

Пример 6 показано, как использование регулярных выражений для проверки значений полей, предоставленные пользователем. Когда пользователь вводит недопустимый адрес электронной почты в текстовом поле поля **электронной почты** отображается сообщение красный значок ошибки. Это происходит, когда пользователь создает или изменяет элемент списка, как показано на рисунке 9.

**На рисунке 9. Сообщение об ошибке для недопустимых поля ввода текста**

![Сообщение об ошибке для недопустимых поля ввода текста](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/d0d1faf1-aa03-4df8-a1a6-db86fff1f463.png)

Следующий код задает заполнитель для шаблона для отображения сообщения об ошибке и регистрирует в функции обратного вызова, которые запускаются каждый раз, когда пользователь пытается отправить форму. Первый обратного вызова возвращает значение в столбце **электронной почты** и второй обратного вызова использует регулярные выражения для проверки строковое значение.

```
function emailFiledTemplate(ctx) {

    var formCtx = SPClientTemplates.Utility.GetFormContextForCurrentField(ctx);

    // Register a callback just before submit.
    formCtx.registerGetValueCallback(formCtx.fieldName, function () {
        return document.getElementById('inpEmail').value;
    });

    // Create container for various validations.
    var validators = new SPClientForms.ClientValidation.ValidatorSet();
    validators.RegisterValidator(new emailValidator());

    // Validation failure handler.
    formCtx.registerValidationErrorCallback(formCtx.fieldName, emailOnError);

    formCtx.registerClientValidator(formCtx.fieldName, validators);

    return "<span dir='none'><input type='text' value='" + formCtx.fieldValue + "'  maxlength='255' id='inpEmail' class='ms-long'> \
            <br><span id='spnError' class='ms-formvalidation ms-csrformvalidation'></span></span>";
}

// Custom validation object to validate email format.
emailValidator = function () {
    emailValidator.prototype.Validate = function (value) {
        var isError = false;
        var errorMessage = "";

        //Email format Regex expression
        var emailRejex = /\S+@\S+\.\S+/;

        if (!emailRejex.test(value) &amp;&amp; value.trim()) {
            isError = true;
            errorMessage = "Invalid email address";
        }

        // Send error message to error callback function (emailOnError).
        return new SPClientForms.ClientValidation.ValidationResult(isError, errorMessage);
    };
};

// Add error message to spnError element under the input field element.
function emailOnError(error) {
    document.getElementById("spnError").innerHTML = "<span role='alert'>" + error.errorMessage + "</span>";
}
```

### <a name="sample-7-make-list-item-edit-fields-read-only"></a>Образец 7: Внесите изменение поля только для чтения элемента списка

Пример семь показано, как сделать списка полей формы редактирования элемента только для чтения. Поля только для чтения Показать с редактирования элементов управления, как показано на рисунке 10.

**На рисунке 10. Форма редактирования поле только для чтения для настраиваемого списка**

![Форма редактирования поля только для чтения в пользовательском списке](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/de441289-8276-4e7c-8530-d08192e29000.png)

В следующем примере кода показано изменение **заголовка**, **AssignedTo**и форма редактирования **приоритет** поля в элементе списка, чтобы они отображаются значения поля только при использовании без редактирования элементов управления. В коде показан способ обработки синтаксического анализа требований для различных типов полей.

```
function readonlyFieldTemplate(ctx) {

    // Reuse SharePoint JavaScript libraries.
    switch (ctx.CurrentFieldSchema.FieldType) {
        case "Text":
        case "Number":
        case "Integer":
        case "Currency":
        case "Choice":
        case "Computed":
            return SPField_FormDisplay_Default(ctx);

        case "MultiChoice":
            prepareMultiChoiceFieldValue(ctx);
            return SPField_FormDisplay_Default(ctx);

        case "Boolean":
            return SPField_FormDisplay_DefaultNoEncode(ctx);

        case "Note":
            prepareNoteFieldValue(ctx);
            return SPFieldNote_Display(ctx);

        case "File":
            return SPFieldFile_Display(ctx);

        case "Lookup":
        case "LookupMulti":
                return SPFieldLookup_Display(ctx);           

        case "URL":
            return RenderFieldValueDefault(ctx);

        case "User":
            prepareUserFieldValue(ctx);
            return SPFieldUser_Display(ctx);

        case "UserMulti":
            prepareUserFieldValue(ctx);
            return SPFieldUserMulti_Display(ctx);

        case "DateTime":
            return SPFieldDateTime_Display(ctx);

        case "Attachments":
            return SPFieldAttachments_Default(ctx);

        case "TaxonomyFieldType":
            //Re-use JavaScript from the sp.ui.taxonomy.js SharePoint JavaScript library
            return SP.UI.Taxonomy.TaxonomyFieldTemplate.renderDisplayControl(ctx);
    }
}

// User control needs specific formatted value to render content correctly.
function prepareUserFieldValue(ctx) {
    var item = ctx['CurrentItem'];
    var userField = item[ctx.CurrentFieldSchema.Name];
    var fieldValue = "";

    for (var i = 0; i < userField.length; i++) {
        fieldValue += userField[i].EntityData.SPUserID + SPClientTemplates.Utility.UserLookupDelimitString + userField[i].DisplayText;

        if ((i + 1) != userField.length) {
            fieldValue += SPClientTemplates.Utility.UserLookupDelimitString
        }
    }

    ctx["CurrentFieldValue"] = fieldValue;
}

// Choice control needs specific formatted value to render content correctly.
function prepareMultiChoiceFieldValue(ctx) {

    if (ctx["CurrentFieldValue"]) {
        var fieldValue = ctx["CurrentFieldValue"];

        var find = ';#';
        var regExpObj = new RegExp(find, 'g');

        fieldValue = fieldValue.replace(regExpObj, '; ');
        fieldValue = fieldValue.replace(/^; /g, '');
        fieldValue = fieldValue.replace(/; $/g, '');

        ctx["CurrentFieldValue"] = fieldValue;
    }
}

// Note control needs specific formatted value to render content correctly.
function prepareNoteFieldValue(ctx) {

    if (ctx["CurrentFieldValue"]) {
        var fieldValue = ctx["CurrentFieldValue"];
        fieldValue = "<div>" + fieldValue.replace(/\n/g, '<br />'); + "</div>";

        ctx["CurrentFieldValue"] = fieldValue;
    }
} 
```

### <a name="sample-8-hide-fields"></a>Образец 8: Скрыть поля

Пример 8 показано, как скрытые поля в новый элемент списка или изменение форм. Пример скрывает поле **предшественников** , когда пользователь создает или изменяет элемент списка задач.

В этом примере выполняется развертывание как изменить и новая форма для список с именем **CSR скрыть элементы управления списка**. Сведения о просмотре формы после развертывания образца можно [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering).

Следующий код находит **предшественников** поля в HTML-код формы и оно скрывается. Поле остается в HTML-код, но пользователь не может видеть его в браузере.

```
(function () {

    // jQuery library is required in this sample.
    // Fallback to loading jQuery from a CDN path if the local is unavailable.
    (window.jQuery || document.write('<script src="//ajax.aspnetcdn.com/ajax/jquery/jquery-1.10.0.min.js"><\/script>'));

    // Create object that has the context information about the field that we want to render differently.
    var hiddenFiledContext = {};
    hiddenFiledContext.Templates = {}; 
    hiddenFiledContext.Templates.OnPostRender = hiddenFiledOnPreRender;
    hiddenFiledContext.Templates.Fields = {
        // Apply the new rendering for Predecessors field in New and Edit forms.
        "Predecessors": {
            "NewForm": hiddenFiledTemplate,
            "EditForm": hiddenFiledTemplate
        }
    };

    SPClientTemplates.TemplateManager.RegisterTemplateOverrides(hiddenFiledContext);

})();


// This function provides the rendering logic.
function hiddenFiledTemplate() {
    return "<span class='csrHiddenField'></span>";
}

// This function provides the rendering logic.
function hiddenFiledOnPreRender(ctx) {
    jQuery(".csrHiddenField").closest("tr").hide();
}

```

## <a name="web-part-and-add-in-part-manipulation"></a>Веб-части и выполнение различных операций часть "надстройки"
<a name="bmPersonalized"> </a>

Пример [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) показано, как использовать части добавьте в скрипт для внедрения сценариев, работающих в размещенном у поставщика надстройки с на страницу SharePoint. В этом примере показано, как для изменения пользовательского интерфейса на страницу сайта узла развертывание части скрипта надстройки и добавив его на страницу SharePoint из коллекции веб-части.

Части скрипта надстройки — как веб-части, добавьте на страницу SharePoint из коллекции веб-частей, но в данном случае WebPart-файл внедряет файл JavaScript, на котором выполняется удаленно в надстройке размещением у поставщика. Часть скрипта надстройка запускается в `<div>` тега на странице SharePoint и поэтому обеспечивает более проектирования и чем вы получите с частями надстройки, которые запускаются в Интернет-кадров.

Начальная страница отображается кнопка **Сценарий запуска** , развертывает часть добавить в сценарий в коллекцию веб-частей. В следующем примере кода создает экземпляр **FileCreationInformationObject** , который содержит содержимое WebPart-файл и затем загружает новый файл в коллекции веб-частей. Обратите внимание на то, что можно также выполнить этот код автоматически при установке части надстройки или как часть процесса подготовки семейства веб-сайтов.

```
var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
using (var clientContext = spContext.CreateUserClientContextForSPHost())
{
    var folder = clientContext.Web.Lists.GetByTitle("Web Part Gallery").RootFolder;
    clientContext.Load(folder);
    clientContext.ExecuteQuery();

    // Upload the OneDrive for Business Usage Guidelines.docx.
    using (var stream = System.IO.File.OpenRead(Server.MapPath("~/userprofileinformation.webpart")))
    {
        FileCreationInformation fileInfo = new FileCreationInformation();
        fileInfo.ContentStream = stream;
        fileInfo.Overwrite = true;
        fileInfo.Url = "userprofileinformation.webpart";
        File file = folder.Files.Add(fileInfo);
        clientContext.ExecuteQuery();
    }

    // Update the group for uplaoded web part.
    var list = clientContext.Web.Lists.GetByTitle("Web Part Gallery");
    CamlQuery camlQuery = CamlQuery.CreateAllItemsQuery(100);
    Microsoft.SharePoint.Client.ListItemCollection items = list.GetItems(camlQuery);
    clientContext.Load(items);
    clientContext.ExecuteQuery();
    foreach (var item in items)
    {
        // Random group name to differentiate it from the rest.
        if (item["FileLeafRef"].ToString().ToLowerInvariant() == "userprofileinformation.webpart")
        {
            item["Group"] = "add-in Script Part";
            item.Update();
            clientContext.ExecuteQuery();
        }
    }

    lblStatus.Text = string.Format("add-in script part has been added to web part gallery. You can find 'User Profile Information' script part under 'Add-in Script Part' group in the <a href='{0}'>host web</a>.", spContext.SPHostUrl.ToString());
}
```

По завершении этого шага можно найти часть скрипта надстройки **сведения о профилях пользователей** внутри новой категории **Add-in части скрипта** в коллекции веб-частей. После добавления скрипта надстройка части на страницу, удаленно выполняемого JavaScript управляет отображения информации на странице.

При просмотре части надстройки скрипта в режиме редактирования, вы увидите внедряет файл JavaScript, на котором выполняется удаленно. Сценарий userprofileinformation.js использует JSON для получения данных профиля пользователя из сайта узла. 

```
function sharePointReady() {
  clientContext = SP.ClientContext.get_current();

  var fileref = document.createElement('script');
  fileref.setAttribute("type", "text/javascript");
  fileref.setAttribute("src", "/_layouts/15/SP.UserProfiles.js");
  document.getElementsByTagName("head")[0].appendChild(fileref);

  SP.SOD.executeOrDelayUntilScriptLoaded(function () {

    //Get Instance of People Manager Class       
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext);

    //Get properties of the current user
    userProfileProperties = peopleManager.getMyProperties();
    clientContext.load(userProfileProperties);
    clientContext.executeQueryAsync(Function.createDelegate(this, function (sender, args) {
      var firstname = userProfileProperties.get_userProfileProperties()['FirstName'];
      var name = userProfileProperties.get_userProfileProperties()['PreferredName'];
      var title = userProfileProperties.get_userProfileProperties()['Title'];
      var aboutMe = userProfileProperties.get_userProfileProperties()['AboutMe'];
      var picture = userProfileProperties.get_userProfileProperties()['PictureURL'];

      var html = "<div><h2>Welcome " + firstname + "</h2></div><div><div style='float: left; margin-left:10px'><img style='float:left;margin-right:10px' src='" + picture + "' /><b>Name</b>: " + name + "<br /><b>Title</b>: " + title + "<br />" + aboutMe + "</div></div>";

      document.getElementById('UserProfileAboutMe').innerHTML = html;
    }), Function.createDelegate(this, function (sender, args) {
      console.log('The following error has occurred while loading user profile property: ' + args.get_message());
    }));
  }, 'SP.UserProfiles.js');
}

```

## <a name="provisioning-publishing-features"></a>Подготовка компоненты публикации
<a name="bmPersonalized"> </a>

В примере [Provisioning.PublishingFeatures](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.PublishingFeatures) показано, как по выполнению распространенных задач с помощью сайтов публикации, размещенные в Office 365; Например, подготовки и с помощью макетов страниц, главные страницы и темы или внедрения JavaScript в макеты страниц. Также показано, как применять фильтры, которые управляют, какие шаблоны сайтов, доступны для дочерних сайтов и какие макетов страниц доступны на веб-сайт.

Надстройка размещением у поставщика использует CSOM для подготовки часто используемых элементов пользовательского интерфейса на веб-сайтах публикации и JavaScript используется для создания более динамичным каждый раз в макеты страниц, которые можно развернуть для сайтов публикации. Также показаны различия между с помощью главных страниц и тем в веб-сайтах публикации.

**Важные:**  Чтобы функциональность в работе в этом примере, необходимо активировать функции публикации на вашем сайте. Сведения можно [включить компоненты публикации](https://support.office.com/en-us/article/Enable-publishing-features-479677a6-8b33-4ac7-907d-071c1c7e4518?CorrelationId=22291615-2acd-46be-8813-9e6c48d01a32&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

Начальная страница образца предоставляет три сценария настройки пользовательского интерфейса веб-сайтах публикации: 

- Развертывание макетов страниц.
    
- Развертывание главные страницы и темы.
    
- Фильтровать доступные макеты страниц и шаблонов сайта на сайт узла.

### <a name="scenario-1-deploy-pages"></a>Сценарий 1: Развертывание страниц

Сценарий 1 показано, как развернуть настраиваемую страницу макета. Кнопка **Развернуть макеты страниц** , показано на рисунке 11 создает новый макет страницы и страница, использующая макета.

**На рисунке 11. Нажмите кнопку, чтобы развернуть макеты страниц**

![Кнопка, которая выполняет развертывание макеты страниц](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/141b3b83-9a74-4528-825a-efd94183526d.png)

Новая страница можно просмотреть, перейдя на страницу только что созданный Демонстрация на свой сайт узла, который содержит внедренные JavaScript и отображает сведения о профилях пользователей.

Пример отображает сведения этого пользователя на странице. Он также добавляет страницы, хотя в этом случае объект **PublishingPageInformation** используется для создания новой страницы.

В этом примере добавляется новый макет страницы, передача файла в коллекции главных страниц и назначить его тип контента макета страницы. Следующий код принимает путь для ASPX-файла (который можно развернуть как ресурс в проекте Visual Studio 2013) и добавляет его в качестве макета страницы в коллекции главных страниц.

```
// Get the path to the file that you are about to deploy.
            List masterPageGallery = web.GetCatalog((int)ListTemplateType.MasterPageCatalog);
            Folder rootFolder = masterPageGallery.RootFolder;
            web.Context.Load(masterPageGallery);
            web.Context.Load(rootFolder);
            web.Context.ExecuteQuery();

            var fileBytes = System.IO.File.ReadAllBytes(sourceFilePath);

            // Use CSOM to upload the file.
            FileCreationInformation newFile = new FileCreationInformation();
            newFile.Content = fileBytes;
            newFile.Url = UrlUtility.Combine(rootFolder.ServerRelativeUrl, fileName);
            newFile.Overwrite = true;

            Microsoft.SharePoint.Client.File uploadFile = rootFolder.Files.Add(newFile);
            web.Context.Load(uploadFile);
            web.Context.ExecuteQuery();

            // Check out the file if needed.
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                if (uploadFile.CheckOutType == CheckOutType.None)
                {
                    uploadFile.CheckOut();
                }
            }

            // Get content type for ID to assign associated content type information.
            ContentType associatedCt = web.GetContentTypeById(associatedContentTypeID);

            var listItem = uploadFile.ListItemAllFields;
            listItem["Title"] = title;
            listItem["MasterPageDescription"] = description;
            // Set the item as page layout.
            listItem["ContentTypeId"] = Constants.PAGE_LAYOUT_CONTENT_TYPE;
            // Set the associated content type ID property
            listItem["PublishingAssociatedContentType"] = string.Format(";#{0};#{1};#", associatedCt.Name, associatedCt.Id);
            listItem["UIVersion"] = Convert.ToString(15);
            listItem.Update();

            // Check in the page layout if needed.
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                uploadFile.CheckIn(string.Empty, CheckinType.MajorCheckIn);
                listItem.File.Publish(string.Empty);
            }
            web.Context.ExecuteQuery();
```

Вы можете проверить, что новая страница с помощью нового макета страницы, перейдя на библиотеки **страниц** сайта узла.

### <a name="scenario-2-deploy-master-pages-and-themes"></a>Сценарий 2: Развертывание главные страницы и темы

Сценарий 2 показано, как развернуть и включить главные страницы и темы для сайта узла с размещением у поставщика надстройки с. При выборе **Развернуть основные и использовать его** на начальной странице пример образца развертывает и применяется настраиваемой главной страницы сайта узла. Вы увидите новой главной страницы, перейдя на домашнюю страницу сайта.

Передача файла *.master в коллекции главных страниц и присвоить его тип контента главной страницы добавляется новой главной страницы. Приведенный ниже код принимает путь файла *.master (который можно развернуть как ресурс в проекте Visual Studio 2013) и добавляет его в качестве главной страницы в коллекции главных страниц.

```
string fileName = Path.GetFileName(sourceFilePath);

            // Get the path to the file that you are about to deploy.
            List masterPageGallery = web.GetCatalog((int)ListTemplateType.MasterPageCatalog);
            Folder rootFolder = masterPageGallery.RootFolder;
            web.Context.Load(masterPageGallery);
            web.Context.Load(rootFolder);
            web.Context.ExecuteQuery();

            // Get the file name from the provided path.
            var fileBytes = System.IO.File.ReadAllBytes(sourceFilePath);

            // Use CSOM to upload the file.
            FileCreationInformation newFile = new FileCreationInformation();
            newFile.Content = fileBytes;
            newFile.Url = UrlUtility.Combine(rootFolder.ServerRelativeUrl, fileName);
            newFile.Overwrite = true;

            Microsoft.SharePoint.Client.File uploadFile = rootFolder.Files.Add(newFile);
            web.Context.Load(uploadFile);
            web.Context.ExecuteQuery();


            var listItem = uploadFile.ListItemAllFields;
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                if (uploadFile.CheckOutType == CheckOutType.None)
                {
                    uploadFile.CheckOut();
                }
            }

            listItem["Title"] = title;
            listItem["MasterPageDescription"] = description;
            // Set content type as master page.
            listItem["ContentTypeId"] = Constants.MASTERPAGE_CONTENT_TYPE;
            listItem["UIVersion"] = uiVersion;
            listItem.Update();
            if (masterPageGallery.ForceCheckout || masterPageGallery.EnableVersioning)
            {
                uploadFile.CheckIn(string.Empty, CheckinType.MajorCheckIn);
                listItem.File.Publish(string.Empty);
            }
            web.Context.Load(listItem);
            web.Context.ExecuteQuery();
```

Следующим шагом является установка URL-адрес новой главной страницы в качестве значения для как **MasterUrl** , так и **CustomMasterUrl** свойства **веб-** объект, представляющий сайт. Пример обрабатывает их с одним методом, который получает URL-адрес новой главной страницы в коллекции главных страниц и присваивает это значение свойства **Web.MasterUrl** и **Web.CustomMasterUrl** .

```
// Assign master page to the host web.
                clientContext.Web.SetMasterPagesForSiteByName("contoso.master", "contoso.master");

```

При выборе **темы развертывать и использовать его**образца развертывает и применение пользовательской темы для сайта узла. Пример задает цветовую палитру, фонового изображения и схемы шрифтов темы, путем добавления новой темы с этими значениями (которые можно развернуть как ресурсы в проекте Visual Studio 2013) в коллекцию тем. Следующий код создает новую тему.

```
List themesOverviewList = web.GetCatalog((int)ListTemplateType.DesignCatalog);
           web.Context.Load(themesOverviewList);
           web.Context.ExecuteQuery(); 
                ListItemCreationInformation itemInfo = new ListItemCreationInformation();
                Microsoft.SharePoint.Client.ListItem item = themesOverviewList.AddItem(itemInfo);
                item["Name"] = themeName;
                item["Title"] = themeName;
                if (!string.IsNullOrEmpty(colorFileName))
                {
                    item["ThemeUrl"] = UrlUtility.Combine(rootWeb.ServerRelativeUrl, string.Format(Constants.THEMES_DIRECTORY, Path.GetFileName(colorFileName)));
                }
                if (!string.IsNullOrEmpty(fontFileName))
                {
                    item["FontSchemeUrl"] = UrlUtility.Combine(rootWeb.ServerRelativeUrl, string.Format(Constants.THEMES_DIRECTORY, Path.GetFileName(fontFileName)));
                }
                if (!string.IsNullOrEmpty(backgroundName))
                {
                    item["ImageUrl"] = UrlUtility.Combine(rootWeb.ServerRelativeUrl, string.Format(Constants.THEMES_DIRECTORY, Path.GetFileName(backgroundName)));
                }
                item["DisplayOrder"] = 11;
                item.Update();
                web.Context.ExecuteQuery();
```

Следующим шагом является установка этого новую тему как тему для сайта. Следующий код выполняет следующее получение темы из коллекции тем, а затем применяет значения его на сайт узла.

```
 CamlQuery query = new CamlQuery();
                // Find the theme by themeName.
                string camlString = string.Format(CAML_QUERY_FIND_BY_FILENAME, themeName);
                query.ViewXml = camlString;
                var found = themeList.GetItems(query);
                rootWeb.Context.Load(found);
                LoggingUtility.Internal.TraceVerbose("Getting theme: {0}", themeName);
                rootWeb.Context.ExecuteQuery();
                if (found.Count > 0)
                {
                    ListItem themeEntry = found[0];

                    / /Set the properties for applying the custom theme that was just uploaded.
                    string spColorURL = null;
                    if (themeEntry["ThemeUrl"] != null &amp;&amp; themeEntry["ThemeUrl"].ToString().Length > 0)
                    {
                        spColorURL = UrlUtility.MakeRelativeUrl((themeEntry["ThemeUrl"] as FieldUrlValue).Url);
                    }
                    string spFontURL = null;
                    if (themeEntry["FontSchemeUrl"] != null &amp;&amp; themeEntry["FontSchemeUrl"].ToString().Length > 0)
                    {
                        spFontURL = UrlUtility.MakeRelativeUrl((themeEntry["FontSchemeUrl"] as FieldUrlValue).Url);
                    }
                    string backGroundImage = null;
                    if (themeEntry["ImageUrl"] != null &amp;&amp; themeEntry["ImageUrl"].ToString().Length > 0)
                    {
                        backGroundImage = UrlUtility.MakeRelativeUrl((themeEntry["ImageUrl"] as FieldUrlValue).Url);
                    }

                    // Set theme for demonstration.
                    // TODO: Why is shareGenerated false? If deploying to root an inheriting, then maybe use shareGenerated = true.
                    web.ApplyTheme(spColorURL,
                                        spFontURL,
                                        backGroundImage,
                                        false);
                    web.Context.ExecuteQuery();
```

### <a name="scenario-3-filter-available-page-layouts-and-site-templates"></a>Сценарий 3: Фильтровать доступные макеты страниц и шаблоны сайтов

Сценарий 3 показано, как ограничить возможности, которые пользователи будут иметь при их применении шаблонов для новых сайтов и макетов страниц. При выборе **Применить фильтры для хост-сайта** в образце начальная страница, примера наборы пользовательский макет страницы по умолчанию и один макет страницы дополнительные как другие параметр только для новых страниц, которые пользователь создает. Примера также сокращает число доступных параметров для пользователей при создании новых дочерних сайтов. На рисунке 12 показано, как выглядит поле выбора шаблона сайта, перед и после применения фильтров.

**На рисунке 12. Выбор шаблона веб-сайтов до и после применения образцы фильтров**

![Выбор шаблона веб-сайтов до и после применения образцы фильтров](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/46c0e39d-dfec-45ed-9b72-ff3f6d5e1916.png)

Образец задает доступные макеты страниц и по умолчанию, передав файлы связанного *.aspx методы для методов расширения, как показано в примере кода.

```
                List<string> pageLayouts = new List<string>();
                pageLayouts.Add("ContosoLinksBelow.aspx");
                pageLayouts.Add("ContosoLinksRight.aspx");
                clientContext.Web.SetAvailablePageLayouts(clientContext.Web, pageLayouts);

                // Set default page layout for the site
                clientContext.Web.SetDefaultPageLayoutForSite(clientContext.Web, "ContosoLinksBelow.aspx");

```
Пример задает список доступных шаблонов, выполнив что-то вроде. В этом случае передает экземпляры **WebTemplateEntity** , которые определяют каждый шаблон сайта метод расширения **SetAvailableWebTemplates**.

```
List<WebTemplateEntity> templates = new List<WebTemplateEntity>();
                templates.Add(new WebTemplateEntity() { LanguageCode = "1035", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "BLOG#0" });
                clientContext.Web.SetAvailableWebTemplates(templates);

```

Все три этих методов расширения - **SetAvailablePageLayouts**, **SetDefaultPageLayoutForSite**и **SetAvailableWebTemplates** - работает так же, как. Они создают XML-документов, которые содержат пары "ключ значение", которые определяют доступные и макеты по умолчанию и доступных шаблонов. Затем они передавать эти документы в метод Дополнительные расширения **SetPropertyBagValue**. Этот метод реализован в [расширении OfficeDevPnPCore](hhttps://github.com/SharePoint/PnP-sites-core). После его устанавливает соответствующее свойство контейнеры, эти контейнеры свойств будут использоваться для фильтрации параметров в интерфейсе.

Из трех методов **SetAvailableWebTemplates** показан полный шаблон.

```
public static void SetAvailableWebTemplates(this Web web, List<WebTemplateEntity> availableTemplates)
        {
            string propertyValue = string.Empty;

            LanguageTemplateHash languages = new LanguageTemplateHash();
            foreach (var item in availableTemplates)
            {
                AddTemplateToCollection(languages, item);
            }

            if (availableTemplates.Count > 0)
            {
                XmlDocument xd = new XmlDocument();
                XmlNode xmlNode = xd.CreateElement("webtemplates");
                xd.AppendChild(xmlNode);
                foreach (var language in languages)
                {
                    XmlNode xmlLcidNode = xmlNode.AppendChild(xd.CreateElement("lcid"));
                    XmlAttribute xmlAttribute = xd.CreateAttribute("id");
                    xmlAttribute.Value = language.Key;
                    xmlLcidNode.Attributes.SetNamedItem(xmlAttribute);

                    foreach (string item in language.Value)
                    {
                        XmlNode xmlWTNode = xmlLcidNode.AppendChild(xd.CreateElement("webtemplate"));
                        XmlAttribute xmlAttributeName = xd.CreateAttribute("name");
                        xmlAttributeName.Value = item;
                        xmlWTNode.Attributes.SetNamedItem(xmlAttributeName);
                    }
                }
                propertyValue = xmlNode.OuterXml;
            }
            // Save the XML entry to property bag.
            web.SetPropertyBagValue(AvailableWebTemplates, propertyValue);
            // Set that templates are not inherited.
            web.SetPropertyBagValue(InheritWebTemplates, "False");

```

Контейнер свойств **InheritWebTemplates** следит за тем, что любые шаблоны, которые обычно наследуются от родительского сайта также учитываются при создании дочерних сайтов.

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

- [Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [Provisioning.Pages](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
- [Branding.ApplyBranding](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
