---
title: "Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек"
ms.date: 11/03/2017
ms.openlocfilehash: 28f14fa6a15e367232b1384952ed6b7fefbfb3de
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="customize-the-ux-by-using-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="a74e0-102">Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек</span><span class="sxs-lookup"><span data-stu-id="a74e0-102">Customize the UX by using SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="a74e0-103">Настройка компонентов пользовательского интерфейса SharePoint удаленно с помощью провайдера надстроек.</span><span class="sxs-lookup"><span data-stu-id="a74e0-103">Customize SharePoint UX components remotely by using provider-hosted add-ins.</span></span> 

<span data-ttu-id="a74e0-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="a74e0-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="a74e0-105">В этой статье описываются примеры, показывающие, рекомендации по настройке компонентов пользовательского интерфейса SharePoint, включая следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="a74e0-105">This article describes samples that show best practices for customizing SharePoint UX components, including the following scenarios:</span></span>

- <span data-ttu-id="a74e0-106">Управление страницами (Добавление и изменение вики-страниц).</span><span class="sxs-lookup"><span data-stu-id="a74e0-106">Page manipulation (adding and modifying a wiki page).</span></span>
    
- <span data-ttu-id="a74e0-107">Отображение надстроек и данных в модальных диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="a74e0-107">Showing add-ins and data in modal dialog boxes.</span></span>
    
- <span data-ttu-id="a74e0-108">Создание персонализированной элементов пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a74e0-108">Creating personalized UI elements.</span></span>
    
- <span data-ttu-id="a74e0-109">Клиентская обработка (развертывание файлов JSLink, настройки отображения поля в списках SharePoint).</span><span class="sxs-lookup"><span data-stu-id="a74e0-109">Client-side rendering (deploying JSLink files that customize the rendering of fields in SharePoint lists).</span></span>
    
- <span data-ttu-id="a74e0-110">Веб-части и добавить в часть выполнение различных операций (удаленно подготовки и выполнения от части скрипта надстройки в надстройке размещением у поставщика).</span><span class="sxs-lookup"><span data-stu-id="a74e0-110">Web Part and add-in part manipulation (remotely provision and run an add-in script part in a provider-hosted add-in).</span></span>
    
- <span data-ttu-id="a74e0-111">Объединение данных и кэширование (с использованием локальное хранилище HTML5 и файлы cookie HTTP сократить количество вызовов службы в SharePoint).</span><span class="sxs-lookup"><span data-stu-id="a74e0-111">Data aggregation and caching (using HTML5 local storage and HTTP cookies to reduce the number of service calls to SharePoint).</span></span>

## <a name="page-manipulation"></a><span data-ttu-id="a74e0-112">Управление страницами</span><span class="sxs-lookup"><span data-stu-id="a74e0-112">Page manipulation</span></span>
<span data-ttu-id="a74e0-113"><a name="bmPageManipulate"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-113"></span></span>

<span data-ttu-id="a74e0-114">Пример [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ModifyPages) включает два сценария обработки страницы:</span><span class="sxs-lookup"><span data-stu-id="a74e0-114">The [Core.ModifyPages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.ModifyPages) sample includes two page manipulation scenarios:</span></span>

- <span data-ttu-id="a74e0-115">Создание вики-страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-115">Create a wiki page.</span></span>
    
- <span data-ttu-id="a74e0-116">Изменение макета вики-страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-116">Modify the layout of a wiki page.</span></span> 
    
<span data-ttu-id="a74e0-117">В этом примере используются библиотеки страниц сайта по умолчанию и существующих встроенных макетов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-117">This sample uses the default site pages library and existing out-of-the-box layouts.</span></span> <span data-ttu-id="a74e0-118">Также можно обновить его на использование библиотека настраиваемых вики-страниц и пользовательских макетов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-118">You can also update it to use a custom wiki page library and custom layouts.</span></span> <span data-ttu-id="a74e0-119">Пользовательский Интерфейс надстройки включает в себя две кнопки, создание вики-страницы и две ссылки для просмотра вики-страницы, которые можно создать.</span><span class="sxs-lookup"><span data-stu-id="a74e0-119">The add-in UI includes two buttons that create both wiki pages, and two links for viewing the wiki pages you create.</span></span>

<span data-ttu-id="a74e0-120">**На рисунке 1. Начальная страница для образца манипуляции страницы**</span><span class="sxs-lookup"><span data-stu-id="a74e0-120">**Figure 1. Start page for the page manipulation sample**</span></span>

![Страница для образца манипуляции страница запуска](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/8c6353d9-b339-4563-b945-eaea3d4da2a8.png)

<span data-ttu-id="a74e0-122">Пример кода в первом случае определяет, будет ли вы уже создали вики-страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-122">The sample code for the first scenario determines whether you've already created the wiki page.</span></span> <span data-ttu-id="a74e0-123">Если нет, ее добавляет файл в библиотеке страниц сайта и возвращает URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="a74e0-123">If not, it adds the file to the site pages library and returns its URL.</span></span>

<span data-ttu-id="a74e0-124">**Примечание:** Код, приведенный в данной статье предоставляется в качестве-без никаких гарантий, явных или подразумеваемых, включая никаких гарантий соответствие для определенной задачи, окупаемость или не нарушения прав.</span><span class="sxs-lookup"><span data-stu-id="a74e0-124">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

```
var newpage = pageLibrary.RootFolder.Files.AddTemplateFile(newWikiPageUrl, TemplateFileType.WikiPage);
ctx.Load(newpage);
ctx.ExecuteQuery();
wikiPageUrl = String.Format("sitepages/{0}", wikiPageName);
```

<span data-ttu-id="a74e0-125">В обоих случаях в этом примере добавляется введены с помощью текстовое поле на странице "Запуск" с помощью метода **AddHtmlToWikiPage** в вспомогательный класс с именем **LabHelper**HTML-код.</span><span class="sxs-lookup"><span data-stu-id="a74e0-125">In both scenarios, the sample adds the HTML entered via the text box on the start page by using the **AddHtmlToWikiPage** method in a helper class named **LabHelper**.</span></span> <span data-ttu-id="a74e0-126">Этот метод вставляет HTML-код из формы внутри поля _WikiField_ вики-страницы.</span><span class="sxs-lookup"><span data-stu-id="a74e0-126">This method inserts the HTML from the form inside the _WikiField_ field of the wiki page.</span></span>

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

<span data-ttu-id="a74e0-127">Пример кода для второй сценарий создает новый экземпляр **WebPartEntity** .</span><span class="sxs-lookup"><span data-stu-id="a74e0-127">The sample code for the second scenario creates a new **WebPartEntity** instance.</span></span> <span data-ttu-id="a74e0-128">Затем он использует методы в вспомогательный класс для заполнения веб-части с помощью XML.</span><span class="sxs-lookup"><span data-stu-id="a74e0-128">It then uses methods in a helper class to populate the Web Part with XML.</span></span> <span data-ttu-id="a74e0-129">XML-код отображается список рекомендуемых ссылок, включая [http://www.bing.com](http://www.bing.com) и на домашней странице [Разработчик офисных решений/PnP репозиториев](https://github.com/SharePoint/PnP) репозитория.</span><span class="sxs-lookup"><span data-stu-id="a74e0-129">The XML displays a promoted links list, including both [http://www.bing.com](http://www.bing.com) and the home page of the [OfficeDev/PnP GitHub](https://github.com/SharePoint/PnP) repository.</span></span>

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

<span data-ttu-id="a74e0-130">Вспомогательный код отображает рекомендуемых ссылок с таблицей внутри веб-части **XsltListViewWebPart** .</span><span class="sxs-lookup"><span data-stu-id="a74e0-130">The helper code displays the promoted links with a table inside an **XsltListViewWebPart** Web Part.</span></span>

<span data-ttu-id="a74e0-131">**На рисунке 2. Вторая страница вики-сайта с помощью XsltListViewWebPart и рекомендуемых ссылок в таблице**</span><span class="sxs-lookup"><span data-stu-id="a74e0-131">**Figure 2. Second wiki page with XsltListViewWebPart and promoted links table**</span></span>

![Вторая страница вики-сайта с помощью XsltListViewWeb часть и рекомендуемых ссылок в таблице](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/6dc60a0b-b11a-4fe9-ad06-6b4d0d4b8b24.png)

<span data-ttu-id="a74e0-133">Объект **WpPromotedLinks** в экземпляре **LabHelper** содержит XML, который определяет внешний вид веб-часть, будут внедрены в вики-страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-133">The **WpPromotedLinks** object on the **LabHelper** instance contains XML that defines the appearance of the Web Part that will be embedded into the wiki page.</span></span> <span data-ttu-id="a74e0-134">Метод **AddWebPartToWikiPage** вставляет недавно определенной веб-части в новое `div` тега на вики-страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-134">The **AddWebPartToWikiPage** method then inserts the newly defined Web Part inside a new `div` tag on the wiki page.</span></span>

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

## <a name="showing-add-ins-and-data-in-modal-dialog-boxes"></a><span data-ttu-id="a74e0-135">Отображение надстроек и данных в модальных диалоговых окон</span><span class="sxs-lookup"><span data-stu-id="a74e0-135">Showing add-ins and data in modal dialog boxes</span></span>
<span data-ttu-id="a74e0-136"><a name="bmPageManipulate"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-136"></span></span>

<span data-ttu-id="a74e0-137">Пример [Core.Dialog](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.Dialog) показаны два метода для внедрения поле модальное диалоговое окно ссылки.</span><span class="sxs-lookup"><span data-stu-id="a74e0-137">The [Core.Dialog](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Core.Dialog) sample shows two methods for embedding modal dialog box links.</span></span> <span data-ttu-id="a74e0-138">Эти ссылки отображает страницу, размещаемые у поставщика надстройки в сайт узла SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a74e0-138">These links display a provider-hosted add-in page into a SharePoint host site.</span></span> <span data-ttu-id="a74e0-139">Надстройки с помощью клиентской объектной модели (CSOM) для создания настраиваемого действия и JavaScript для запуска и отображать данные, содержащиеся в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="a74e0-139">The add-in uses the client object model (CSOM) to create the custom action and JavaScript to start and display information inside the dialog box.</span></span> <span data-ttu-id="a74e0-140">Так как некоторые из этих сведений поступают из сайта узла, также используется объектная модель JavaScript (JSOM) для получения сведений из сайта узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-140">Because some of this information comes from the host site, it also uses the JavaScript object model (JSOM) to retrieve information from the host site.</span></span> <span data-ttu-id="a74e0-141">И так как надстройки выполняется в другом домене размещения сайта SharePoint, также использует кросс доменной библиотеки SharePoint для выполнения вызовов на сайт узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-141">And because the add-in is running in a different domain than the SharePoint host site, it also uses the SharePoint cross-domain library to make the calls to the host site.</span></span>

<span data-ttu-id="a74e0-142">**Примечание:** Дополнительные сведения об использовании междоменной библиотеки в этом сценарии видеть [данные доступа к SharePoint 2013 от надстроек с помощью междоменной библиотеки](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a74e0-142">**Note:** For more information about using the cross-domain library in this scenario, see [Access SharePoint 2013 data from add-ins using the cross-domain library](http://msdn.microsoft.com/library/bc37ff5c-1285-40af-98ae-01286696242d%28Office.15%29.aspx).</span></span>

<span data-ttu-id="a74e0-143">Начальная страница — это страница, которая отображается в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="a74e0-143">The start page is the page that appears in the dialog box.</span></span> <span data-ttu-id="a74e0-144">Обрабатывать все различия в отображения, заданном контексте отображения (диалоговое окно и веб-страницы), надстройки определяет, является ли он отображается в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="a74e0-144">To handle any differences in display given the display context (dialog box versus full-page), the add-in determines whether it's being displayed in a dialog box.</span></span> <span data-ttu-id="a74e0-145">Это осуществляется с помощью параметра строки запроса, который передается, а также ссылки, запустите диалоговых окон.</span><span class="sxs-lookup"><span data-stu-id="a74e0-145">It does this by using a query string parameter that is passed along with the links that start the dialog boxes.</span></span>

```
private string SetIsDlg(string isDlgValue)
        {
            var urlParams = HttpUtility.ParseQueryString(Request.QueryString.ToString());
            urlParams.Set("IsDlg", isDlgValue);
            return string.Format("{0}://{1}:{2}{3}?{4}", Request.Url.Scheme, Request.Url.Host, Request.Url.Port, Request.Url.AbsolutePath, urlParams.ToString());
        }
```

<span data-ttu-id="a74e0-146">Можно например, выбрать для отображения определенных элементов пользовательского интерфейса (например, кнопки) или даже различные макеты, в зависимости от того, является ли содержимое отображается в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="a74e0-146">You could, for example, choose to display certain UI elements (like buttons) or even different page layouts, depending on whether or not the content is being displayed in a dialog box.</span></span>

<span data-ttu-id="a74e0-147">Начальная страница пользовательского интерфейса представлены два варианта для создания ссылки на поле, а также список всех списков на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="a74e0-147">The start page UI presents two options for creating links to the dialog box, along with a list of all the lists on the host web.</span></span> <span data-ttu-id="a74e0-148">Также в нем представлен **ОК** и **Отмена** кнопок, можно использовать в контексте поле диалогового окна для закрытия диалогового окна поля и/или строки дополнительные действия в надстройку.</span><span class="sxs-lookup"><span data-stu-id="a74e0-148">It also presents **OK** and **Cancel** buttons that you can use in the dialog box context to close the dialog box and/or prompt additional actions in the add-in.</span></span>

<span data-ttu-id="a74e0-149">После нажатия кнопки **Добавить элемент меню** надстройки создает объект **CustomActionEntity** , который запускает диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="a74e0-149">When you choose the **Add menu item** button, the add-in creates a **CustomActionEntity** object that starts the dialog box.</span></span> <span data-ttu-id="a74e0-150">Затем метод [расширения основных OfficeDevPnP](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) , с именем **AddCustomAction** используется для добавления нового настраиваемого действия в меню **Параметры сайта** .</span><span class="sxs-lookup"><span data-stu-id="a74e0-150">It then uses the [OfficeDevPnP Core extension](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) method named **AddCustomAction** to add the new custom action to the **Site Settings** menu.</span></span>

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

<span data-ttu-id="a74e0-151">Метод **AddCustomAction** добавляет дополнительное действие в коллекцию **UserCustomActions** , который связан с сайтом SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a74e0-151">The **AddCustomAction** method adds the custom action to the **UserCustomActions** collection that is associated with the SharePoint site.</span></span>

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

<span data-ttu-id="a74e0-152">При нажатии кнопки **Добавить страницы с веб-часть редактора скрипт** , надстройка использует методы **AddWikiPage** и **AddWebPartToWikiPage** создает вики-страниц в библиотеке страниц сайта и добавляет настроенный редактор сценариев веб-части на страницу.</span><span class="sxs-lookup"><span data-stu-id="a74e0-152">When you choose the **Add page with script editor web part** button, the add-in uses the methods **AddWikiPage** and **AddWebPartToWikiPage** to create a wiki page inside the site pages library and add a configured Script Editor Web Part to the page.</span></span>

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

<span data-ttu-id="a74e0-153">Метод **AddWikiPage** загружает библиотеку страниц сайта.</span><span class="sxs-lookup"><span data-stu-id="a74e0-153">The **AddWikiPage** method loads the site pages library.</span></span> <span data-ttu-id="a74e0-154">Если вики-страниц, указанного идентификатором [основных OfficeDevPnP](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) надстройки еще не существует, он создает страницы.</span><span class="sxs-lookup"><span data-stu-id="a74e0-154">If the wiki page specified by the add-in [OfficeDevPnP core](https://github.com/SharePoint/PnP/tree/dev/OfficeDevPnP.Core) doesn't already exist, it creates the page.</span></span>

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

<span data-ttu-id="a74e0-155">Метод **AddWebPartToWikiPage** вставляет недавно определенной веб-части в новое `<div>` тега на вики-страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-155">The **AddWebPartToWikiPage** method inserts the newly defined Web Part inside a new `<div>` tag on the wiki page.</span></span> <span data-ttu-id="a74e0-156">Затем используется для получения информации, которая заполняет список списков SharePoint на хост-сайта JSOM и междоменной библиотеки.</span><span class="sxs-lookup"><span data-stu-id="a74e0-156">It then uses JSOM and the cross-domain library to retrieve the information that populates the list of SharePoint lists on the host web.</span></span>

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

## <a name="personalized-ui-elements"></a><span data-ttu-id="a74e0-157">Личные элементы пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="a74e0-157">Personalized UI elements</span></span>
<span data-ttu-id="a74e0-158"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-158"></span></span>

<span data-ttu-id="a74e0-159">Пример [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization) показано, как использовать внедренные JavaScript и значения, хранящиеся в профилях пользователей и списки SharePoint для индивидуальной настройки элементы пользовательского интерфейса на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="a74e0-159">The [Branding.UIElementPersonalization](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.UIElementPersonalization) sample shows how to use embedded JavaScript and values stored in user profiles and SharePoint lists to personalize UI elements on the host web.</span></span> <span data-ttu-id="a74e0-160">Он также использует локальное хранилище HTML5 для сведения к минимуму звонков на сайт узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-160">It also uses HTML5 local storage to minimize calls to the host site.</span></span>

<span data-ttu-id="a74e0-161">Пример начальная страница выдает запрос добавьте одну из трех строк (XX, гг или ЯЯ) **Сведения обо мне** разделе на странице профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="a74e0-161">The sample's start page prompts you to add one of three strings (XX, YY, or ZZ) to the **About Me** section of your user profile page.</span></span>

<span data-ttu-id="a74e0-162">Добавить в уже развернут три изображения и списка SharePoint, который содержит заголовки и URL-адреса для каждого изображения, а также дополнительные поля, который привязан к одной из трех строк каждого изображения.</span><span class="sxs-lookup"><span data-stu-id="a74e0-162">The add-in has already deployed three images and a SharePoint list that contains titles and URLs for each image, along with an additional field that ties each image to one of the three strings.</span></span> <span data-ttu-id="a74e0-163">После нажатия кнопки **параметров вставки** надстройки внедряет файл personalize.js в коллекции настраиваемых действий пользователя.</span><span class="sxs-lookup"><span data-stu-id="a74e0-163">After you choose the **Inject customization** button, the add-in embeds the personalize.js file into the user custom actions collection.</span></span>

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

<span data-ttu-id="a74e0-164">Так как сайты группы SharePoint по умолчанию используется [Стратегия минимальной загрузки (MDS)](http://msdn.microsoft.com/en-us/library/office/dn456544%28v=office.15%29.aspx), код в файле personalize.js сначала пытается зарегистрироваться MDS.</span><span class="sxs-lookup"><span data-stu-id="a74e0-164">Because SharePoint team sites by default use the [Minimal Download Strategy (MDS)](http://msdn.microsoft.com/en-us/library/office/dn456544%28v=office.15%29.aspx), the code in the personalize.js file first attempts to register itself with MDS.</span></span> <span data-ttu-id="a74e0-165">Таким образом, при загрузке страницы, которая содержит JavaScript, MDS компонентами ядра СУБД starets функцию main (**RemoteManager_Inject**).</span><span class="sxs-lookup"><span data-stu-id="a74e0-165">This way, when you load the page that contains the JavaScript, the MDS engine starets the main function (**RemoteManager_Inject**).</span></span> <span data-ttu-id="a74e0-166">Если MDS отключен, эта функция запускается немедленно.</span><span class="sxs-lookup"><span data-stu-id="a74e0-166">If MDS is disabled, this function starts right away.</span></span>

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

<span data-ttu-id="a74e0-167">Функция **personalizeIt()** проверяет локальное хранилище HTML5, прежде чем оно берет сведения о профилях пользователей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-167">The **personalizeIt()** function checks HTML5 local storage before it looks up user profile information.</span></span> <span data-ttu-id="a74e0-168">Если он переходит на сведения о профилях пользователей, он содержит сведения, которые он получает в локальном хранилище HTML5.</span><span class="sxs-lookup"><span data-stu-id="a74e0-168">If it goes to user profile information, it stores the information that it retrieves in HTML5 local storage.</span></span>

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

<span data-ttu-id="a74e0-169">Файл personalize.js также содержит код, который проверяет, истек ли срок действия ключа локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="a74e0-169">The personalize.js file also contains code that checks to determine whether the local storage key has expired.</span></span> <span data-ttu-id="a74e0-170">Это не встроенных в локальном хранилище HTML5.</span><span class="sxs-lookup"><span data-stu-id="a74e0-170">This isn't built into HTML5 local storage.</span></span>

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

## <a name="client-side-rendering"></a><span data-ttu-id="a74e0-171">Обработка на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="a74e0-171">Client-side rendering</span></span>
<span data-ttu-id="a74e0-172"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-172"></span></span>

<span data-ttu-id="a74e0-173">Пример [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering) описывается использование размещение у поставщика в надстройке удаленно подготавливать артефактов SharePoint и JSLink файлов с использованием обработки на стороне клиента для настройки внешнего вида и поведения полей списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a74e0-173">The [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering) sample shows how to use a provider-hosted add-in to remotely provision SharePoint artifacts and JSLink files that use client-side rendering to customize the look and behavior of SharePoint list fields.</span></span> <span data-ttu-id="a74e0-174">Файлы JSLink и присвойте обработки на стороне клиента, можно настроить как элементы управления на странице SharePoint (представления списка, списка полей и добавление и изменение форм) отображаются.</span><span class="sxs-lookup"><span data-stu-id="a74e0-174">JSLink files and client-side rendering give you control over how controls on a SharePoint page (list views, list fields, and add and edit forms) are rendered.</span></span> <span data-ttu-id="a74e0-175">Этот элемент управления может частичному или полному устранению потребности в настраиваемых типов полей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-175">This control can reduce or eliminate the need for custom field types.</span></span> <span data-ttu-id="a74e0-176">Отображение на стороне клиента позволяет удаленно управлять внешний вид поля списка в удаленном режиме.</span><span class="sxs-lookup"><span data-stu-id="a74e0-176">Client-side rendering makes it possible to remotely control list field appearance remotely.</span></span>

<span data-ttu-id="a74e0-177">Примера объединяет примеры JSLink из [примеров кода со стороны клиента визуализации (JSLink)](http://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a) в одной размещением у поставщика надстройки для SharePoint, подготавливает файлы JSLink.</span><span class="sxs-lookup"><span data-stu-id="a74e0-177">The sample combines the JSLink samples from the [Client-side rendering (JSLink) code samples](http://code.msdn.microsoft.com/office/Client-side-rendering-JS-2ed3538a) into a single provider-hosted add-in for SharePoint that provisions the JSLink files.</span></span> <span data-ttu-id="a74e0-178">Отображение на стороне клиента позволяет использовать стандартный веб-технологий, таких как HTML и JavaScript, определение логики отрисовки типы настраиваемых и предварительно определенные поля.</span><span class="sxs-lookup"><span data-stu-id="a74e0-178">Client-side rendering enables you to use standard web technologies, such as HTML and JavaScript, to define the rendering logic of custom and predefined field types.</span></span>

<span data-ttu-id="a74e0-179">При запуске примера начальная страница выдает запрос для подготовки к примеры.</span><span class="sxs-lookup"><span data-stu-id="a74e0-179">When you start the sample, the start page prompts you to provision all the samples.</span></span>

<span data-ttu-id="a74e0-180">**На рисунке 3. Начальная страница образца обработки на стороне клиента**</span><span class="sxs-lookup"><span data-stu-id="a74e0-180">**Figure 3. Start page of the client-side rendering sample**</span></span>

![Откройте страницу пример обработки на стороне клиента](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/bfa1b472-976b-4bdc-95df-537cee5570e6.png)

<span data-ttu-id="a74e0-182">При выборе **Примеры временного**надстройки развертывает изображения, а также все списки SharePoint, представления списка, элементов списка, форм и файлов JavaScript, используемые в каждом примера.</span><span class="sxs-lookup"><span data-stu-id="a74e0-182">When you choose **Provision Samples**, the add-in deploys an image as well as all the SharePoint lists, list views, list items, forms, and JavaScript files that are used in each sample.</span></span> <span data-ttu-id="a74e0-183">Надстройка создает папку с именем JSLink-примеры в библиотеку стилей, а затем загружает файлы JavaScript в эту папку.</span><span class="sxs-lookup"><span data-stu-id="a74e0-183">The add-in creates a folder named JSLink-Samples in the Style Library, and then uploads the JavaScript files into that folder.</span></span> <span data-ttu-id="a74e0-184">Метод **UploadFileToFolder** работает передача и возврат каждого файла JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a74e0-184">The **UploadFileToFolder** method does the work of uploading and checking in each JavaScript file.</span></span>

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

### <a name="sample-1-apply-formatting-to-a-list-column"></a><span data-ttu-id="a74e0-185">Пример 1: Применение форматирования для столбца списка</span><span class="sxs-lookup"><span data-stu-id="a74e0-185">Sample 1: Apply formatting to a list column</span></span>

<span data-ttu-id="a74e0-186">Пример 1 показано, как применять форматирование к столбца списка на основе значения поля.</span><span class="sxs-lookup"><span data-stu-id="a74e0-186">Sample 1 shows how to apply formatting to a list column based on the field value.</span></span> <span data-ttu-id="a74e0-187">Значения полей приоритет 1 (высокий), 2 (обычный) и 3 (низкий) отображаются в красный, оранжевый и желтый.</span><span class="sxs-lookup"><span data-stu-id="a74e0-187">Priority field values of 1 (High), 2 (Normal), and 3 (Low) are displayed in red, orange, and yellow.</span></span>

<span data-ttu-id="a74e0-188">**На рисунке 4. Настраиваемый список отображения поля**</span><span class="sxs-lookup"><span data-stu-id="a74e0-188">**Figure 4. Custom list field display**</span></span>

![Настраиваемый список отображения поля](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/1481adfa-efc9-4b59-b07f-bb330f02d2bb.png)

<span data-ttu-id="a74e0-190">Следующие JavaScript переопределяет отображения поля по умолчанию и создает новый шаблон отображения для поля списка **приоритет** .</span><span class="sxs-lookup"><span data-stu-id="a74e0-190">The following JavaScript overrides the default field display and creates a new display template for the **Priority** list field.</span></span> <span data-ttu-id="a74e0-191">Эта технология анонимная функция, которая загружает контекстные сведения о поле, отображаемое для переопределения используется в все примеры.</span><span class="sxs-lookup"><span data-stu-id="a74e0-191">The technique in the anonymous function that loads the contextual information about the field whose display you want to override is used in all the samples.</span></span>

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

### <a name="sample-2-shorten-long-text"></a><span data-ttu-id="a74e0-192">Пример 2: Сокращение длинного текста</span><span class="sxs-lookup"><span data-stu-id="a74e0-192">Sample 2: Shorten long text</span></span>

<span data-ttu-id="a74e0-193">Пример 2 показано, как удалять длинный текст в поле **Body** список **извещений** .</span><span class="sxs-lookup"><span data-stu-id="a74e0-193">Sample 2 shows you how to truncate long text stored in the **Body** field of an **Announcements** list.</span></span> <span data-ttu-id="a74e0-194">Полный текст отображается как всплывающее окно, которое появляется при наведении указателя на элемент списка, как показано на рисунке 8.</span><span class="sxs-lookup"><span data-stu-id="a74e0-194">The full text displays as a popup that appears whenever you hover over a list item, as shown in Figure 8.</span></span>

<span data-ttu-id="a74e0-195">**На рисунке 5. Всплывающее окно показывает отображаемое поле сокращенный список**</span><span class="sxs-lookup"><span data-stu-id="a74e0-195">**Figure 5. Shortened list field display showing popup**</span></span>

![Всплывающее окно показывает отображаемое поле усеченных списка](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/a5e6d2af-f1f9-4bcc-9278-e56fd42c2e64.png)

<span data-ttu-id="a74e0-197">Следующие JavaScript сокращает поля к **основному** тексту и вызывает полный текст, который отображается как всплывающее окно с помощью атрибут **title** на **охватывать** тег.</span><span class="sxs-lookup"><span data-stu-id="a74e0-197">The following JavaScript shortens the **Body** field text and causes the full text to appear as a popup via the **title** attribute on the **span** tag.</span></span>

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

### <a name="sample-3-display-an-image-with-a-document-name"></a><span data-ttu-id="a74e0-198">Пример 3: Отобразить изображение с именем документа</span><span class="sxs-lookup"><span data-stu-id="a74e0-198">Sample 3: Display an image with a document name</span></span>

<span data-ttu-id="a74e0-199">Пример 3 показано, как отобразить изображение рядом с именем документа в библиотеке документов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-199">Sample 3 shows you how to display an image next to a document name inside a document library.</span></span> <span data-ttu-id="a74e0-200">Красный значок появляется при использовании значения поля **Конфиденциальность** **Да**, как показано на рисунке 6.</span><span class="sxs-lookup"><span data-stu-id="a74e0-200">A red badge appears whenever the **Confidential** field value is set to **Yes**, as shown in Figure 6.</span></span> 

<span data-ttu-id="a74e0-201">**На рисунке 6. Отображаемое изображение рядом с именем документа**</span><span class="sxs-lookup"><span data-stu-id="a74e0-201">**Figure 6. Image display next to document name**</span></span>

![Отображаемое изображение рядом с именем документа](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/f2768dfd-ae05-4afc-8dbe-26dc4e7dca6d.png)

<span data-ttu-id="a74e0-203">Следующие JavaScript проверяет значение поля **Конфиденциальность** и затем настраивает отображаемое **имя** поля, на основе значения другого поля.</span><span class="sxs-lookup"><span data-stu-id="a74e0-203">The following JavaScript checks the **Confidential** field value and then customizes the **Name** field display based on the value of another field.</span></span> <span data-ttu-id="a74e0-204">В примере используется изображения, который загрузил при выборе **Примеры подготовки**.</span><span class="sxs-lookup"><span data-stu-id="a74e0-204">The sample uses the image that is uploaded when you choose **Provision Samples**.</span></span> 

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

### <a name="sample-4-display-a-bar-chart"></a><span data-ttu-id="a74e0-205">Пример 4: Отображения линейчатой диаграммы</span><span class="sxs-lookup"><span data-stu-id="a74e0-205">Sample 4: Display a bar chart</span></span>

<span data-ttu-id="a74e0-206">Пример 4 показано, как для отображения линейчатой диаграммы в поле **% завершения** списка задач.</span><span class="sxs-lookup"><span data-stu-id="a74e0-206">Sample 4 shows you how to display a bar chart in the **% Complete** field of a task list.</span></span> <span data-ttu-id="a74e0-207">Внешний вид линейчатая диаграмма зависит от значение поля **% завершения** , как показано на рисунке 10.</span><span class="sxs-lookup"><span data-stu-id="a74e0-207">The appearance of the bar chart depends on the value of the **% Complete** field, as shown in Figure 10.</span></span> <span data-ttu-id="a74e0-208">Обратите внимание на то, что линейчатая диаграмма, также будут отображаться в формах для создания и редактирования элементов списка задач.</span><span class="sxs-lookup"><span data-stu-id="a74e0-208">Note that a bar chart will also appear in the forms for creating and editing task list items.</span></span>

<span data-ttu-id="a74e0-209">Следующий код создает отображения линейчатой диаграммы и связывание его с помощью представления и отображения форм (**percentCompleteViewFiledTemplate**), а затем с помощью нового и редактировать формы (**percentCompleteEditFiledTemplate**).</span><span class="sxs-lookup"><span data-stu-id="a74e0-209">The following code creates the bar chart display and associates it with the view and display forms (**percentCompleteViewFiledTemplate**) and then with the new and edit forms (**percentCompleteEditFiledTemplate**).</span></span>

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

<span data-ttu-id="a74e0-210">**На рисунке 7. Линейчатая диаграмма, отображаемых в поле % завершения**</span><span class="sxs-lookup"><span data-stu-id="a74e0-210">**Figure 7. Bar chart displayed in the % Complete field**</span></span>

![Линейчатая диаграмма, отображаемых в поле % завершения](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fb36f27a-2eb7-4c5f-8428-b85b65369ea9.png)

### <a name="sample-5-change-the-rendering-template"></a><span data-ttu-id="a74e0-212">Пример 5: Изменение шаблона отображения</span><span class="sxs-lookup"><span data-stu-id="a74e0-212">Sample 5: Change the rendering template</span></span>

<span data-ttu-id="a74e0-213">Пример 5 показано, как изменить шаблон отображения представления списка.</span><span class="sxs-lookup"><span data-stu-id="a74e0-213">Sample 5 shows you how to change the rendering template for a list view.</span></span> <span data-ttu-id="a74e0-214">Это представление отображает заголовки элемента списка, разверните узел как accordions при их выборе.</span><span class="sxs-lookup"><span data-stu-id="a74e0-214">This view displays list item titles that expand like accordions when you select them.</span></span> <span data-ttu-id="a74e0-215">Расширенное представление отображает дополнительные список полей элемента, как показано на рисунке 8.</span><span class="sxs-lookup"><span data-stu-id="a74e0-215">The expanded view shows you additional list item fields, as shown in Figure 8.</span></span>

<span data-ttu-id="a74e0-216">**На рисунке 8. Представления списков свернутые и расширенное элемента**</span><span class="sxs-lookup"><span data-stu-id="a74e0-216">**Figure 8. Collapsed and expanded list item views**</span></span>

![Представления списков свернутые и расширенное элемента](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/fd185eef-e2be-4523-9adb-d524b84ecc26.png)

<span data-ttu-id="a74e0-218">Следующий код выполняет настройку шаблона и регистрирует его с помощью шаблона списка.</span><span class="sxs-lookup"><span data-stu-id="a74e0-218">The following code sets up the template and registers it with the list template.</span></span> <span data-ttu-id="a74e0-219">Выполняет настройку общий макет и затем использует обработчик события **OnPostRender** для регистрации функцию JavaScript, которая выполняется при отображении списка.</span><span class="sxs-lookup"><span data-stu-id="a74e0-219">It sets up the overall layout, and then uses the **OnPostRender** event handler to register the JavaScript function that executes when the list is rendered.</span></span> <span data-ttu-id="a74e0-220">Эта функция событие связывается с CSS и событие обработки, который реализует аккордеона функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="a74e0-220">This function associates the event with the CSS and event handling that implements the accordion functionality.</span></span>

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

### <a name="sample-6-validate-field-values"></a><span data-ttu-id="a74e0-221">Пример 6: Проверка значений полей</span><span class="sxs-lookup"><span data-stu-id="a74e0-221">Sample 6: Validate field values</span></span>

<span data-ttu-id="a74e0-222">Пример 6 показано, как использование регулярных выражений для проверки значений полей, предоставленные пользователем.</span><span class="sxs-lookup"><span data-stu-id="a74e0-222">Sample 6 shows you how to use regular expressions to validate field values supplied by the user.</span></span> <span data-ttu-id="a74e0-223">Когда пользователь вводит недопустимый адрес электронной почты в текстовом поле поля **электронной почты** отображается сообщение красный значок ошибки.</span><span class="sxs-lookup"><span data-stu-id="a74e0-223">A red error message appears when the user types an invalid email address into the **Email** field text box.</span></span> <span data-ttu-id="a74e0-224">Это происходит, когда пользователь создает или изменяет элемент списка, как показано на рисунке 9.</span><span class="sxs-lookup"><span data-stu-id="a74e0-224">This happens when the user either creates or edits a list item, as shown in Figure 9.</span></span>

<span data-ttu-id="a74e0-225">**На рисунке 9. Сообщение об ошибке для недопустимых поля ввода текста**</span><span class="sxs-lookup"><span data-stu-id="a74e0-225">**Figure 9. Error message for invalid field text input**</span></span>

![Сообщение об ошибке для недопустимых поля ввода текста](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/d0d1faf1-aa03-4df8-a1a6-db86fff1f463.png)

<span data-ttu-id="a74e0-227">Следующий код задает заполнитель для шаблона для отображения сообщения об ошибке и регистрирует в функции обратного вызова, которые запускаются каждый раз, когда пользователь пытается отправить форму.</span><span class="sxs-lookup"><span data-stu-id="a74e0-227">The following code sets up the template with a placeholder for displaying the error message and registers the callback functions that fire whenever the user tries to submit the forms.</span></span> <span data-ttu-id="a74e0-228">Первый обратного вызова возвращает значение в столбце **электронной почты** и второй обратного вызова использует регулярные выражения для проверки строковое значение.</span><span class="sxs-lookup"><span data-stu-id="a74e0-228">The first callback returns the value of the **Email** column, and the second callback uses regular expressions to validate the string value.</span></span>

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

### <a name="sample-7-make-list-item-edit-fields-read-only"></a><span data-ttu-id="a74e0-229">Образец 7: Внесите изменение поля только для чтения элемента списка</span><span class="sxs-lookup"><span data-stu-id="a74e0-229">Sample 7: Make list item edit fields read-only</span></span>

<span data-ttu-id="a74e0-230">Пример семь показано, как сделать списка полей формы редактирования элемента только для чтения.</span><span class="sxs-lookup"><span data-stu-id="a74e0-230">Sample seven shows you how to make list item edit form fields read-only.</span></span> <span data-ttu-id="a74e0-231">Поля только для чтения Показать с редактирования элементов управления, как показано на рисунке 10.</span><span class="sxs-lookup"><span data-stu-id="a74e0-231">The read-only fields show with no editing controls, as shown in Figure 10.</span></span>

<span data-ttu-id="a74e0-232">**На рисунке 10. Форма редактирования поле только для чтения для настраиваемого списка**</span><span class="sxs-lookup"><span data-stu-id="a74e0-232">**Figure 10. Read-only field on a custom list edit form**</span></span>

![Форма редактирования поля только для чтения в пользовательском списке](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/de441289-8276-4e7c-8530-d08192e29000.png)

<span data-ttu-id="a74e0-234">В следующем примере кода показано изменение **заголовка**, **AssignedTo**и форма редактирования **приоритет** поля в элементе списка, чтобы они отображаются значения поля только при использовании без редактирования элементов управления.</span><span class="sxs-lookup"><span data-stu-id="a74e0-234">The following code example modifies the **Title**, **AssignedTo**, and **Priority** fields in the list item edit form so that they show the field values only with no editing controls.</span></span> <span data-ttu-id="a74e0-235">В коде показан способ обработки синтаксического анализа требований для различных типов полей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-235">The code shows how to handle the parsing requirements for different field types.</span></span>

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

### <a name="sample-8-hide-fields"></a><span data-ttu-id="a74e0-236">Образец 8: Скрыть поля</span><span class="sxs-lookup"><span data-stu-id="a74e0-236">Sample 8: Hide fields</span></span>

<span data-ttu-id="a74e0-237">Пример 8 показано, как скрытые поля в новый элемент списка или изменение форм.</span><span class="sxs-lookup"><span data-stu-id="a74e0-237">Sample 8 shows you how to hide fields in list item new and edit forms.</span></span> <span data-ttu-id="a74e0-238">Пример скрывает поле **предшественников** , когда пользователь создает или изменяет элемент списка задач.</span><span class="sxs-lookup"><span data-stu-id="a74e0-238">The sample hides the **Predecessors** field when a user creates or edits a task list item.</span></span>

<span data-ttu-id="a74e0-239">В этом примере выполняется развертывание как изменить и новая форма для список с именем **CSR скрыть элементы управления списка**.</span><span class="sxs-lookup"><span data-stu-id="a74e0-239">This sample deploys as the edit and new form for a list called **CSR-Hide-Controls list**.</span></span> <span data-ttu-id="a74e0-240">Сведения о просмотре формы после развертывания образца можно [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering).</span><span class="sxs-lookup"><span data-stu-id="a74e0-240">For information about how to view the form after you deploy the sample, see [Branding.ClientSideRendering](https://github.com/SharePoint/PnP/tree/dev/Samples/Branding.ClientSideRendering).</span></span>

<span data-ttu-id="a74e0-241">Следующий код находит **предшественников** поля в HTML-код формы и оно скрывается.</span><span class="sxs-lookup"><span data-stu-id="a74e0-241">The following code finds the **Predecessors** field in the HTML of the form and hides it.</span></span> <span data-ttu-id="a74e0-242">Поле остается в HTML-код, но пользователь не может видеть его в браузере.</span><span class="sxs-lookup"><span data-stu-id="a74e0-242">The field remains present in the HTML, but the user can't see it in the browser.</span></span>

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

## <a name="web-part-and-add-in-part-manipulation"></a><span data-ttu-id="a74e0-243">Веб-части и выполнение различных операций часть "надстройки"</span><span class="sxs-lookup"><span data-stu-id="a74e0-243">Web part and add-in part manipulation</span></span>
<span data-ttu-id="a74e0-244"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-244"></span></span>

<span data-ttu-id="a74e0-245">Пример [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) показано, как использовать части добавьте в скрипт для внедрения сценариев, работающих в размещенном у поставщика надстройки с на страницу SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a74e0-245">The [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) sample shows how to use add-in script parts to embed scripts running in a provider-hosted add-in on a SharePoint page.</span></span> <span data-ttu-id="a74e0-246">В этом примере показано, как для изменения пользовательского интерфейса на страницу сайта узла развертывание части скрипта надстройки и добавив его на страницу SharePoint из коллекции веб-части.</span><span class="sxs-lookup"><span data-stu-id="a74e0-246">This sample shows how to modify the UI of a page on the host site by deploying an add-in script part and adding it to a SharePoint page from the webpart gallery.</span></span>

<span data-ttu-id="a74e0-247">Части скрипта надстройки — как веб-части, добавьте на страницу SharePoint из коллекции веб-частей, но в данном случае WebPart-файл внедряет файл JavaScript, на котором выполняется удаленно в надстройке размещением у поставщика.</span><span class="sxs-lookup"><span data-stu-id="a74e0-247">An add-in script part is like a web part in that you can add it to a SharePoint page from the web part gallery, but in this case the .webpart file embeds a JavaScript file that runs remotely in a provider-hosted add-in.</span></span> <span data-ttu-id="a74e0-248">Часть скрипта надстройка запускается в `<div>` тега на странице SharePoint и поэтому обеспечивает более проектирования и чем вы получите с частями надстройки, которые запускаются в Интернет-кадров.</span><span class="sxs-lookup"><span data-stu-id="a74e0-248">The add-in script part runs inside a  `<div>` tag on the SharePoint page and therefore provides a more responsive design and experience than you get with add-in parts that run in IFrames.</span></span>

<span data-ttu-id="a74e0-249">Начальная страница отображается кнопка **Сценарий запуска** , развертывает часть добавить в сценарий в коллекцию веб-частей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-249">The start page includes a **Run Scenario** button that deploys the add-in script part to the web part gallery.</span></span> <span data-ttu-id="a74e0-250">В следующем примере кода создает экземпляр **FileCreationInformationObject** , который содержит содержимое WebPart-файл и затем загружает новый файл в коллекции веб-частей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-250">The following code example constructs a **FileCreationInformationObject** instance that contains the contents of the .webpart file and then uploads the new file into the web part gallery.</span></span> <span data-ttu-id="a74e0-251">Обратите внимание на то, что можно также выполнить этот код автоматически при установке части надстройки или как часть процесса подготовки семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-251">Note that you can also run this code automatically when the add-in part installs or as part of the site collection provisioning process.</span></span>

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

<span data-ttu-id="a74e0-252">По завершении этого шага можно найти часть скрипта надстройки **сведения о профилях пользователей** внутри новой категории **Add-in части скрипта** в коллекции веб-частей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-252">After you finish this step, you can locate the **User profile information** add-in script part inside a new **Add-in Script Part** category in the web part gallery.</span></span> <span data-ttu-id="a74e0-253">После добавления скрипта надстройка части на страницу, удаленно выполняемого JavaScript управляет отображения информации на странице.</span><span class="sxs-lookup"><span data-stu-id="a74e0-253">After you add the add-in script part to the page, the remotely running JavaScript controls the display of the information on the page.</span></span>

<span data-ttu-id="a74e0-254">При просмотре части надстройки скрипта в режиме редактирования, вы увидите внедряет файл JavaScript, на котором выполняется удаленно.</span><span class="sxs-lookup"><span data-stu-id="a74e0-254">When you view the add-in script part in edit mode, you'll see that it embeds the JavaScript file that is running remotely.</span></span> <span data-ttu-id="a74e0-255">Сценарий userprofileinformation.js использует JSON для получения данных профиля пользователя из сайта узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-255">The userprofileinformation.js script uses the JSON to get user profile information from the host site.</span></span> 

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

## <a name="provisioning-publishing-features"></a><span data-ttu-id="a74e0-256">Подготовка компоненты публикации</span><span class="sxs-lookup"><span data-stu-id="a74e0-256">Provisioning publishing features</span></span>
<span data-ttu-id="a74e0-257"><a name="bmPersonalized"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-257"></span></span>

<span data-ttu-id="a74e0-258">В примере [Provisioning.PublishingFeatures](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.PublishingFeatures) показано, как по выполнению распространенных задач с помощью сайтов публикации, размещенные в Office 365; Например, подготовки и с помощью макетов страниц, главные страницы и темы или внедрения JavaScript в макеты страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-258">The [Provisioning.PublishingFeatures](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Provisioning.PublishingFeatures) sample shows how to do common tasks with publishing sites that are hosted on Office 365; for example, provisioning and using page layouts, master pages, and themes, or embedding JavaScript in page layouts.</span></span> <span data-ttu-id="a74e0-259">Также показано, как применять фильтры, которые управляют, какие шаблоны сайтов, доступны для дочерних сайтов и какие макетов страниц доступны на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="a74e0-259">It also shows how to apply filters that control what site templates are available for subsites and what page layouts are available on the host web.</span></span>

<span data-ttu-id="a74e0-260">Надстройка размещением у поставщика использует CSOM для подготовки часто используемых элементов пользовательского интерфейса на веб-сайтах публикации и JavaScript используется для создания более динамичным каждый раз в макеты страниц, которые можно развернуть для сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="a74e0-260">The provider-hosted add-in uses CSOM to provision commonly used UI elements on publishing sites, and it uses JavaScript to create more dynamic experiences in page layouts that you can deploy to publishing sites.</span></span> <span data-ttu-id="a74e0-261">Также показаны различия между с помощью главных страниц и тем в веб-сайтах публикации.</span><span class="sxs-lookup"><span data-stu-id="a74e0-261">It also shows the differences between using master pages and themes in publishing sites.</span></span>

<span data-ttu-id="a74e0-262">**Важные:**  Чтобы функциональность в работе в этом примере, необходимо активировать функции публикации на вашем сайте.</span><span class="sxs-lookup"><span data-stu-id="a74e0-262">**Important:**  To make the functionality in this sample work, you need to activate the publishing features on your site.</span></span> <span data-ttu-id="a74e0-263">Сведения можно [включить компоненты публикации](https://support.office.com/en-us/article/Enable-publishing-features-479677a6-8b33-4ac7-907d-071c1c7e4518?CorrelationId=22291615-2acd-46be-8813-9e6c48d01a32&amp;ui=en-US&amp;rs=en-US&amp;ad=US).</span><span class="sxs-lookup"><span data-stu-id="a74e0-263">For information, see [Enable publishing features](https://support.office.com/en-us/article/Enable-publishing-features-479677a6-8b33-4ac7-907d-071c1c7e4518?CorrelationId=22291615-2acd-46be-8813-9e6c48d01a32&amp;ui=en-US&amp;rs=en-US&amp;ad=US).</span></span>

<span data-ttu-id="a74e0-264">Начальная страница образца предоставляет три сценария настройки пользовательского интерфейса веб-сайтах публикации:</span><span class="sxs-lookup"><span data-stu-id="a74e0-264">The sample start page presents you with three scenarios for customizing the UI of publishing sites:</span></span> 

- <span data-ttu-id="a74e0-265">Развертывание макетов страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-265">Deploy page layouts.</span></span>
    
- <span data-ttu-id="a74e0-266">Развертывание главные страницы и темы.</span><span class="sxs-lookup"><span data-stu-id="a74e0-266">Deploy master pages and themes.</span></span>
    
- <span data-ttu-id="a74e0-267">Фильтровать доступные макеты страниц и шаблонов сайта на сайт узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-267">Filter the available page layouts and site templates on the host site.</span></span>

### <a name="scenario-1-deploy-pages"></a><span data-ttu-id="a74e0-268">Сценарий 1: Развертывание страниц</span><span class="sxs-lookup"><span data-stu-id="a74e0-268">Scenario 1: Deploy pages</span></span>

<span data-ttu-id="a74e0-269">Сценарий 1 показано, как развернуть настраиваемую страницу макета.</span><span class="sxs-lookup"><span data-stu-id="a74e0-269">Scenario 1 shows you how to deploy a custom page layout.</span></span> <span data-ttu-id="a74e0-270">Кнопка **Развернуть макеты страниц** , показано на рисунке 11 создает новый макет страницы и страница, использующая макета.</span><span class="sxs-lookup"><span data-stu-id="a74e0-270">The **Deploy page layouts** button shown in Figure 11 creates a new page layout and a page that uses that layout.</span></span>

<span data-ttu-id="a74e0-271">**На рисунке 11. Нажмите кнопку, чтобы развернуть макеты страниц**</span><span class="sxs-lookup"><span data-stu-id="a74e0-271">**Figure 11. Button to deploy page layouts**</span></span>

![Кнопка, которая выполняет развертывание макеты страниц](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/141b3b83-9a74-4528-825a-efd94183526d.png)

<span data-ttu-id="a74e0-273">Новая страница можно просмотреть, перейдя на страницу только что созданный Демонстрация на свой сайт узла, который содержит внедренные JavaScript и отображает сведения о профилях пользователей.</span><span class="sxs-lookup"><span data-stu-id="a74e0-273">You can view the new page by going to the newly created demo page on your host site, which contains embedded JavaScript and displays user profile information.</span></span>

<span data-ttu-id="a74e0-274">Пример отображает сведения этого пользователя на странице.</span><span class="sxs-lookup"><span data-stu-id="a74e0-274">The sample displays this user's information on the page.</span></span> <span data-ttu-id="a74e0-275">Он также добавляет страницы, хотя в этом случае объект **PublishingPageInformation** используется для создания новой страницы.</span><span class="sxs-lookup"><span data-stu-id="a74e0-275">It also adds a page, although in this case it uses a **PublishingPageInformation** object to create the new page.</span></span>

<span data-ttu-id="a74e0-276">В этом примере добавляется новый макет страницы, передача файла в коллекции главных страниц и назначить его тип контента макета страницы.</span><span class="sxs-lookup"><span data-stu-id="a74e0-276">The sample adds a new page layout by uploading a file to the master page gallery and assigning it the page layout content type.</span></span> <span data-ttu-id="a74e0-277">Следующий код принимает путь для ASPX-файла (который можно развернуть как ресурс в проекте Visual Studio 2013) и добавляет его в качестве макета страницы в коллекции главных страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-277">The following code takes the path to a *.aspx file (which you can deploy as a resource in your Visual Studio 2013 project) and adds it as a page layout in the master page gallery.</span></span>

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

<span data-ttu-id="a74e0-278">Вы можете проверить, что новая страница с помощью нового макета страницы, перейдя на библиотеки **страниц** сайта узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-278">You can verify that your new page is using the new page layout by going to the **Pages** library of the host site.</span></span>

### <a name="scenario-2-deploy-master-pages-and-themes"></a><span data-ttu-id="a74e0-279">Сценарий 2: Развертывание главные страницы и темы</span><span class="sxs-lookup"><span data-stu-id="a74e0-279">Scenario 2: Deploy master pages and themes</span></span>

<span data-ttu-id="a74e0-280">Сценарий 2 показано, как развернуть и включить главные страницы и темы для сайта узла с размещением у поставщика надстройки с.</span><span class="sxs-lookup"><span data-stu-id="a74e0-280">Scenario 2 shows you how to deploy and set master pages and themes for the host site from a provider-hosted add-in.</span></span> <span data-ttu-id="a74e0-281">При выборе **Развернуть основные и использовать его** на начальной странице пример образца развертывает и применяется настраиваемой главной страницы сайта узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-281">When you choose **Deploy master and use it** on the sample start page, the sample deploys and applies a custom master page to the host site.</span></span> <span data-ttu-id="a74e0-282">Вы увидите новой главной страницы, перейдя на домашнюю страницу сайта.</span><span class="sxs-lookup"><span data-stu-id="a74e0-282">You can see the new master page by going to the home page of the site.</span></span>

<span data-ttu-id="a74e0-283">Передача файла *.master в коллекции главных страниц и присвоить его тип контента главной страницы добавляется новой главной страницы.</span><span class="sxs-lookup"><span data-stu-id="a74e0-283">The sample adds a new master page by uploading a *.master file to the master page gallery and assigning it the master page content type.</span></span> <span data-ttu-id="a74e0-284">Приведенный ниже код принимает путь файла *.master (который можно развернуть как ресурс в проекте Visual Studio 2013) и добавляет его в качестве главной страницы в коллекции главных страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-284">The following code takes the path to a *.master file (which you can deploy as a resource in your Visual Studio 2013 project) and adds it as a master page in the master page gallery.</span></span>

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

<span data-ttu-id="a74e0-285">Следующим шагом является установка URL-адрес новой главной страницы в качестве значения для как **MasterUrl** , так и **CustomMasterUrl** свойства **веб-** объект, представляющий сайт.</span><span class="sxs-lookup"><span data-stu-id="a74e0-285">The next step is to set the URL of the new master page as the value for both the **MasterUrl** and **CustomMasterUrl** properties of the **Web** object that represents the site.</span></span> <span data-ttu-id="a74e0-286">Пример обрабатывает их с одним методом, который получает URL-адрес новой главной страницы в коллекции главных страниц и присваивает это значение свойства **Web.MasterUrl** и **Web.CustomMasterUrl** .</span><span class="sxs-lookup"><span data-stu-id="a74e0-286">The sample handles this with a single method that fetches the URL of the new master page in the master page gallery and then assigns that value to the **Web.MasterUrl** and **Web.CustomMasterUrl** properties.</span></span>

```
// Assign master page to the host web.
                clientContext.Web.SetMasterPagesForSiteByName("contoso.master", "contoso.master");

```

<span data-ttu-id="a74e0-287">При выборе **темы развертывать и использовать его**образца развертывает и применение пользовательской темы для сайта узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-287">When you choose **Deploy theme and use it**, the sample deploys and applies a custom theme to the host site.</span></span> <span data-ttu-id="a74e0-288">Пример задает цветовую палитру, фонового изображения и схемы шрифтов темы, путем добавления новой темы с этими значениями (которые можно развернуть как ресурсы в проекте Visual Studio 2013) в коллекцию тем.</span><span class="sxs-lookup"><span data-stu-id="a74e0-288">The sample sets the color palette, background image, and font scheme of the theme by adding a new theme with those values (which you can deploy as resources inside your Visual Studio 2013 project) to the theme gallery.</span></span> <span data-ttu-id="a74e0-289">Следующий код создает новую тему.</span><span class="sxs-lookup"><span data-stu-id="a74e0-289">The following code creates the new theme.</span></span>

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

<span data-ttu-id="a74e0-290">Следующим шагом является установка этого новую тему как тему для сайта.</span><span class="sxs-lookup"><span data-stu-id="a74e0-290">The next step is to set this new theme as the theme for the site.</span></span> <span data-ttu-id="a74e0-291">Следующий код выполняет следующее получение темы из коллекции тем, а затем применяет значения его на сайт узла.</span><span class="sxs-lookup"><span data-stu-id="a74e0-291">The following code does this by fetching the theme from the theme gallery and then applying its values to the host site.</span></span>

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

### <a name="scenario-3-filter-available-page-layouts-and-site-templates"></a><span data-ttu-id="a74e0-292">Сценарий 3: Фильтровать доступные макеты страниц и шаблоны сайтов</span><span class="sxs-lookup"><span data-stu-id="a74e0-292">Scenario 3: Filter available page layouts and site templates</span></span>

<span data-ttu-id="a74e0-293">Сценарий 3 показано, как ограничить возможности, которые пользователи будут иметь при их применении шаблонов для новых сайтов и макетов страниц.</span><span class="sxs-lookup"><span data-stu-id="a74e0-293">Scenario 3 shows you how to limit the options that users have when they apply templates to new sites, and layouts to new pages.</span></span> <span data-ttu-id="a74e0-294">При выборе **Применить фильтры для хост-сайта** в образце начальная страница, примера наборы пользовательский макет страницы по умолчанию и один макет страницы дополнительные как другие параметр только для новых страниц, которые пользователь создает.</span><span class="sxs-lookup"><span data-stu-id="a74e0-294">When you choose **Apply filters to host web** on the sample start page, the sample sets a custom page layout as the default and one additional page layout as the only other option for any new pages that a user creates.</span></span> <span data-ttu-id="a74e0-295">Примера также сокращает число доступных параметров для пользователей при создании новых дочерних сайтов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-295">The sample also reduces the number of available options for users when they create new subsites.</span></span> <span data-ttu-id="a74e0-296">На рисунке 12 показано, как выглядит поле выбора шаблона сайта, перед и после применения фильтров.</span><span class="sxs-lookup"><span data-stu-id="a74e0-296">Figure 12 shows what the site template selection box looks like both before and after the filters have been applied.</span></span>

<span data-ttu-id="a74e0-297">**На рисунке 12. Выбор шаблона веб-сайтов до и после применения образцы фильтров**</span><span class="sxs-lookup"><span data-stu-id="a74e0-297">**Figure 12. Site template selection before and after sample filters have been applied**</span></span>

![Выбор шаблона веб-сайтов до и после применения образцы фильтров](media/customize-the-ux-by-using-sharepoint-provider-hosted-add-ins/46c0e39d-dfec-45ed-9b72-ff3f6d5e1916.png)

<span data-ttu-id="a74e0-299">Образец задает доступные макеты страниц и по умолчанию, передав файлы связанного *.aspx методы для методов расширения, как показано в примере кода.</span><span class="sxs-lookup"><span data-stu-id="a74e0-299">The sample sets both the default and available page layouts by passing the associated *.aspx files to methods to extension methods, as shown in the code.</span></span>

```
                List<string> pageLayouts = new List<string>();
                pageLayouts.Add("ContosoLinksBelow.aspx");
                pageLayouts.Add("ContosoLinksRight.aspx");
                clientContext.Web.SetAvailablePageLayouts(clientContext.Web, pageLayouts);

                // Set default page layout for the site
                clientContext.Web.SetDefaultPageLayoutForSite(clientContext.Web, "ContosoLinksBelow.aspx");

```
<span data-ttu-id="a74e0-300">Пример задает список доступных шаблонов, выполнив что-то вроде.</span><span class="sxs-lookup"><span data-stu-id="a74e0-300">The sample sets the available site templates by doing something similar.</span></span> <span data-ttu-id="a74e0-301">В этом случае передает экземпляры **WebTemplateEntity** , которые определяют каждый шаблон сайта метод расширения **SetAvailableWebTemplates**.</span><span class="sxs-lookup"><span data-stu-id="a74e0-301">In this case it passes the **WebTemplateEntity** instances that define each site template to an extension method called **SetAvailableWebTemplates**.</span></span>

```
List<WebTemplateEntity> templates = new List<WebTemplateEntity>();
                templates.Add(new WebTemplateEntity() { LanguageCode = "1035", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "STS#0" });
                templates.Add(new WebTemplateEntity() { LanguageCode = "", TemplateName = "BLOG#0" });
                clientContext.Web.SetAvailableWebTemplates(templates);

```

<span data-ttu-id="a74e0-302">Все три этих методов расширения - **SetAvailablePageLayouts**, **SetDefaultPageLayoutForSite**и **SetAvailableWebTemplates** - работает так же, как.</span><span class="sxs-lookup"><span data-stu-id="a74e0-302">All three of these extension methods - **SetAvailablePageLayouts**, **SetDefaultPageLayoutForSite**, and **SetAvailableWebTemplates** - work in the same way.</span></span> <span data-ttu-id="a74e0-303">Они создают XML-документов, которые содержат пары "ключ значение", которые определяют доступные и макеты по умолчанию и доступных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-303">They create XML documents that contain key/value pairs that define the available and default layouts and the available templates.</span></span> <span data-ttu-id="a74e0-304">Затем они передавать эти документы в метод Дополнительные расширения **SetPropertyBagValue**.</span><span class="sxs-lookup"><span data-stu-id="a74e0-304">They then pass these documents to an additional extension method called **SetPropertyBagValue**.</span></span> <span data-ttu-id="a74e0-305">Этот метод реализован в [расширении OfficeDevPnPCore](hhttps://github.com/SharePoint/PnP-sites-core).</span><span class="sxs-lookup"><span data-stu-id="a74e0-305">This method is implemented in [OfficeDevPnPCore extension](hhttps://github.com/SharePoint/PnP-sites-core).</span></span> <span data-ttu-id="a74e0-306">После его устанавливает соответствующее свойство контейнеры, эти контейнеры свойств будут использоваться для фильтрации параметров в интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="a74e0-306">After it sets up the appropriate property bags, these property bags are then used to filter options in the interface.</span></span>

<span data-ttu-id="a74e0-307">Из трех методов **SetAvailableWebTemplates** показан полный шаблон.</span><span class="sxs-lookup"><span data-stu-id="a74e0-307">Of the three methods, **SetAvailableWebTemplates** shows the full pattern.</span></span>

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

<span data-ttu-id="a74e0-308">Контейнер свойств **InheritWebTemplates** следит за тем, что любые шаблоны, которые обычно наследуются от родительского сайта также учитываются при создании дочерних сайтов.</span><span class="sxs-lookup"><span data-stu-id="a74e0-308">The **InheritWebTemplates** property bag makes sure that any templates that are normally inherited from the parent site also are ignored when you create subsites.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a74e0-309">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a74e0-309">Additional resources</span></span>
<span data-ttu-id="a74e0-310"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a74e0-310"></span></span>

- [<span data-ttu-id="a74e0-311">Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a74e0-311">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
    
- [<span data-ttu-id="a74e0-312">Provisioning.Pages</span><span class="sxs-lookup"><span data-stu-id="a74e0-312">Provisioning.Pages</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Provisioning.Pages)
    
- [<span data-ttu-id="a74e0-313">Branding.ApplyBranding</span><span class="sxs-lookup"><span data-stu-id="a74e0-313">Branding.ApplyBranding</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ApplyBranding)
