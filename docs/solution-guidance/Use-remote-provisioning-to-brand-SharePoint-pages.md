---
title: "Использование удаленного обеспечения марки страницах SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 195d5e183850625d732ae696447cbc9a56ab1e8b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-remote-provisioning-to-brand-sharepoint-pages"></a><span data-ttu-id="2ccae-102">Использование удаленного обеспечения марки страницах SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ccae-102">Use remote provisioning to brand SharePoint pages</span></span>

<span data-ttu-id="2ccae-103">Использование удаленных подготовки для взаимодействия с темами в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ccae-103">Use remote provisioning to interact with themes in SharePoint.</span></span>

<span data-ttu-id="2ccae-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="2ccae-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="2ccae-105">Можно применить и взаимодействовать с тем с помощью удаленного подготовки функций в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2ccae-105">You can apply and interact with themes by using remote provisioning features in SharePoint.</span></span> <span data-ttu-id="2ccae-106">Эти функции поддерживаются следующие интерфейсы API:</span><span class="sxs-lookup"><span data-stu-id="2ccae-106">These features are provided by the following APIs:</span></span>

-  [<span data-ttu-id="2ccae-107">Метод ApplyTheme</span><span class="sxs-lookup"><span data-stu-id="2ccae-107">ApplyTheme method</span></span>](http://msdn.microsoft.com/library/52c567e8-03e6-7ba3-a9ed-cf4e3c22dbdd%28Office.15%29.aspx)
    
-  [<span data-ttu-id="2ccae-108">Класс ThemeInfo</span><span class="sxs-lookup"><span data-stu-id="2ccae-108">ThemeInfo class</span></span>](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx)
    
<span data-ttu-id="2ccae-109">Метод **ApplyTheme** обеспечивает питание изменение внешнего вида мастера.</span><span class="sxs-lookup"><span data-stu-id="2ccae-109">The  **ApplyTheme** method powers the Change the Look wizard.</span></span> <span data-ttu-id="2ccae-110">Мастер применяет внешний вид acomposed или пользовательского вида на сайте SharePoint с помощью указанных компонентов.</span><span class="sxs-lookup"><span data-stu-id="2ccae-110">The wizard applies acomposed look, or a custom look, to a SharePoint site by using specified components.</span></span> <span data-ttu-id="2ccae-111">Темы применяются для отдельных сайтов с сайта.</span><span class="sxs-lookup"><span data-stu-id="2ccae-111">Themes are applied on a site-by-site basis.</span></span>
<span data-ttu-id="2ccae-112">С помощью **ApplyTheme** и **ThemeInfo** интерфейсы API в CSOM и JSOM предоставляются **ApplyThemeApp** и интерфейсы API **ThemeInfo** на сервере.</span><span class="sxs-lookup"><span data-stu-id="2ccae-112">The  **ApplyThemeApp** and **ThemeInfo** server-side APIs are exposed via the **ApplyTheme** and **ThemeInfo** APIs in CSOM and JSOM.</span></span>
<span data-ttu-id="2ccae-113">Образец, показано, как применить существующую или новую тему видеть [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes) на репозиториев.</span><span class="sxs-lookup"><span data-stu-id="2ccae-113">For a sample that shows you how to apply an existing or custom theme, see  [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes) on GitHub.</span></span>

## <a name="applytheme-method"></a><span data-ttu-id="2ccae-114">Метод ApplyTheme</span><span class="sxs-lookup"><span data-stu-id="2ccae-114">ApplyTheme method</span></span>
<span data-ttu-id="2ccae-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="2ccae-115"></span></span>

<span data-ttu-id="2ccae-116">Метод **ApplyTheme** со стороны клиента при использовании удаленного подготовки для применения темы, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2ccae-116">Use the  **ApplyTheme** client-side method when you use remote provisioning to apply themes, as shown in the following example.</span></span>

```
public void ApplyTheme(
            string colorPaletteUrl,
            string fontSchemeUrl,
            string backgroundImageUrl,
            bool shareGenerated
             )
```

<span data-ttu-id="2ccae-117">Метод **ApplyTheme** использует следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="2ccae-117">The  **ApplyTheme** method uses the following parameters:</span></span>

- <span data-ttu-id="2ccae-118">colorPaletteUrl - зависящий от сервера URL-адрес файла цветовой палитры (например, spcolor).</span><span class="sxs-lookup"><span data-stu-id="2ccae-118">colorPaletteUrl - The server-relative URL of the color palette file (for example, spcolor).</span></span>
    
- <span data-ttu-id="2ccae-119">fontSchemeUrl - зависящий от сервера URL-адрес файла схемы шрифта (например, spfont).</span><span class="sxs-lookup"><span data-stu-id="2ccae-119">fontSchemeUrl - The server-relative URL of the font scheme file (for example, spfont).</span></span>
    
- <span data-ttu-id="2ccae-120">backgroundImageUrl - зависящий от сервера URL-адрес фонового изображения.</span><span class="sxs-lookup"><span data-stu-id="2ccae-120">backgroundImageUrl - The server-relative URL of the background image.</span></span> <span data-ttu-id="2ccae-121">Если нет фонового изображения, этот параметр Возвращает ссылку на **значение null** .</span><span class="sxs-lookup"><span data-stu-id="2ccae-121">If there is no background image, this parameter returns a **null** reference.</span></span>
    
- <span data-ttu-id="2ccae-122">shareGenerated — логическое значение.</span><span class="sxs-lookup"><span data-stu-id="2ccae-122">shareGenerated - A Boolean value.</span></span> <span data-ttu-id="2ccae-123">**Значение true,** Если созданных файлов темы, которые должны применяться к корневого веб-узла; **значение false,** если они находятся в текущем веб-узле.</span><span class="sxs-lookup"><span data-stu-id="2ccae-123">**True** if the generated theme files should be applied to the root web; **false** if they are to be stored in the current web.</span></span>

<span data-ttu-id="2ccae-124">**Примечание**  Параметр shareGenerated определяет, будет ли темой выходные файлы хранятся в папку, доступную через семейства веб-сайтов или веб-узла.</span><span class="sxs-lookup"><span data-stu-id="2ccae-124">**Note**  The shareGenerated parameter determines whether the themed output files are stored in a web-specific location or a location that is accessible across the site collection.</span></span> <span data-ttu-id="2ccae-125">Мы рекомендуем оставьте значение по умолчанию для соответствующего типа сайта.</span><span class="sxs-lookup"><span data-stu-id="2ccae-125">We recommend that you keep the default value for your site type.</span></span>

## <a name="themeinfo-class"></a><span data-ttu-id="2ccae-126">Класс ThemeInfo</span><span class="sxs-lookup"><span data-stu-id="2ccae-126">ThemeInfo class</span></span>
<span data-ttu-id="2ccae-127"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="2ccae-127"></span></span>

<span data-ttu-id="2ccae-128">CSOM кода можно использовать для получения сведений о вариантов оформления, применяемых к сайту.</span><span class="sxs-lookup"><span data-stu-id="2ccae-128">You can use CSOM code to get information about the composed looks that are applied to a site.</span></span> <span data-ttu-id="2ccae-129">Класс [ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx) Возвращает контекст, связанные с тем, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2ccae-129">The  [ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx) class gets the context associated with the themes, as shown in the following example.</span></span>

```
public ThemeInfo ThemeInfo { get; }
```

<span data-ttu-id="2ccae-130">Класс **ThemeInfo** можно использовать для получения сведений о темах, применяемых к сайту, включая описания, контекста, данных объекта, цвета и шрифты для указанного имени (и шрифты для указанного языка кода), а также URI для фона изображение, определенных для вариант оформления.</span><span class="sxs-lookup"><span data-stu-id="2ccae-130">You can use the  **ThemeInfo** class to get details about themes that are applied to a site, including descriptions, context, object data, colors, and fonts for the specified name (and fonts for the specified language code), as well as the URI for the background image defined for the composed look.</span></span>

## <a name="using-applytheme-and-themeinfo-in-csom-code"></a><span data-ttu-id="2ccae-131">Использование ApplyTheme и ThemeInfo в коде CSOM</span><span class="sxs-lookup"><span data-stu-id="2ccae-131">Using ApplyTheme and ThemeInfo in CSOM code</span></span>
<span data-ttu-id="2ccae-132"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="2ccae-132"></span></span>

<span data-ttu-id="2ccae-133">В следующем примере кода показано, как использовать **ApplyTheme** и **ThemeInfo** в коде CSOM.</span><span class="sxs-lookup"><span data-stu-id="2ccae-133">The following code example shows how to use  **ApplyTheme** and **ThemeInfo** in CSOM code.</span></span> <span data-ttu-id="2ccae-134">Этот код можно использовать в шаблоне удаленного подготовки.</span><span class="sxs-lookup"><span data-stu-id="2ccae-134">You can use this code in the remote provisioning pattern.</span></span> <span data-ttu-id="2ccae-135">Например можно программно, как указано в конструкторе создание вариантов оформления и подготовить их сайтов в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2ccae-135">For example, you might decide to create composed looks programmatically, as specified by a designer, and provision them to sites in your web application.</span></span>

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Text;
using System.IO;
using Microsoft.SharePoint.Client;

namespace ApplyThemeAppWeb.Pages
{
    public partial class Default : System.Web.UI.Page
    {
        public string _ContextToken 
        {
            get
            {
                if (ViewState["ContextToken"] == null)
                    return null;
                return ViewState["ContextToken"].ToString();
            }
            set
            {
                ViewState["ContextToken"] = value;
            }
        }

        public string _HostWeb
        {
            get
            {
                if (ViewState["HostWeb"] == null)
                    return null;
                return ViewState["HostWeb"].ToString();
            }
            set
            {
                ViewState["HostWeb"] = value;
            }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                _ContextToken = TokenHelper.GetContextTokenFromRequest(Page.Request);
                _HostWeb = Page.Request["SPHostUrl"];
            }

            StatusMessage.Text = string.Empty;
        }

        protected void GetThemeInfo_Click(object sender, EventArgs e)
        {
            try
            {
                StatusMessage.Text += GetThemeInfo();
            }
            catch (Exception ex)
            {
                StatusMessage.Text += Environment.NewLine + ex.ToString();
            }
        }

        protected void ApplyTheme_Click(object sender, EventArgs e)
        {
            try
            {
                ApplyTheme();
                StatusMessage.Text += "Theme applied. Click Get Theme Info to see changes." + Environment.NewLine;
            }
            catch (Exception ex)
            {
                StatusMessage.Text += Environment.NewLine + ex.ToString();
            }
        }

        private string GetThemeInfo()
        {
            using (var clientContext = TokenHelper.GetClientContextWithContextToken(_HostWeb, _ContextToken, Request.Url.Authority))
            {

                Web hostWebObj = clientContext.Web;
                ThemeInfo initialThemeInfo = hostWebObj.ThemeInfo;

                // Get the initial theme info for the web. No need to load the entire web object.
                clientContext.Load(hostWebObj, w => w.ThemeInfo, w => w.CustomMasterUrl);

                // Theme component info is available via a method call that must be run.
                var linkShade = initialThemeInfo.GetThemeShadeByName("Hyperlink");
                var titleFont = initialThemeInfo.GetThemeFontByName("title", 1033);

                // Run.
                clientContext.ExecuteQuery();

                // Use ThemeInfo to show some data about the theme currently applied to the web.
                StringBuilder initialInfo = new StringBuilder();
                initialInfo.AppendFormat("Current master page: {0}\r\n", hostWebObj.CustomMasterUrl);
                initialInfo.AppendFormat("Background Image: {0}\r\n", initialThemeInfo.ThemeBackgroundImageUri);
                initialInfo.AppendFormat("The \"Hyperlink\" Color for this theme is: {0}\r\n", linkShade.Value);
                initialInfo.AppendFormat("The \"title\" Font for this theme is: {0}\r\n", titleFont.Value);
                return initialInfo.ToString();
            }
        }

        protected void ApplyTheme()
        {
            using (var clientContext = TokenHelper.GetClientContextWithContextToken(_HostWeb, _ContextToken, Request.Url.Authority))
            {
                // Apply the new theme.

                // First, copy theme files to a temporary location (the web's Site Assets library).
                Web hostWebObj = clientContext.Web;
                Site hostSiteObj = clientContext.Site;
                Web hostRootWebObj = hostSiteObj.RootWeb;
                
                // Get the necessary lists and libraries.
                List themeLibrary = hostRootWebObj.Lists.GetByTitle("Theme Gallery");
                Folder themeFolder = themeLibrary.RootFolder.Folders.GetByUrl("15");
                List looksGallery = hostRootWebObj.Lists.GetByTitle("Composed Looks");
                List masterLibrary = hostRootWebObj.Lists.GetByTitle("Master Page Gallery");
                List assetLibrary = hostRootWebObj.Lists.GetByTitle("Site Assets");

                clientContext.Load(themeFolder, f => f.ServerRelativeUrl);
                clientContext.Load(masterLibrary, l => l.RootFolder);
                clientContext.Load(assetLibrary, l => l.RootFolder);

                // First, upload the theme files to the Theme Gallery.
                DirectoryInfo themeDir = new DirectoryInfo(Server.MapPath("/Theme"));
                foreach (var themeFile in themeDir.EnumerateFiles())
                {
                    FileCreationInformation newFile = new FileCreationInformation();
                    newFile.Content = System.IO.File.ReadAllBytes(themeFile.FullName);
                    newFile.Url = themeFile.Name;
                    newFile.Overwrite = true;
                    
                    // Sort by file extension into the correct library. 
                    switch (themeFile.Extension)
                    {
                        case ".spcolor":
                        case ".spfont":
                            Microsoft.SharePoint.Client.File uploadTheme = themeFolder.Files.Add(newFile);
                            clientContext.Load(uploadTheme);
                            break;
                        case ".master":
                        case ".html":
                            Microsoft.SharePoint.Client.File updloadMaster = masterLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(updloadMaster);
                            break;
                        default:
                            Microsoft.SharePoint.Client.File uploadAsset = assetLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(uploadAsset);
                            break;
                    }

                }

                // Run the file upload.
                clientContext.ExecuteQuery();

                // Create a new composed look for the theme.
                string themeFolderUrl = themeFolder.ServerRelativeUrl;
                string masterFolderUrl = masterLibrary.RootFolder.ServerRelativeUrl;

                // Optional: Use to make the custom theme available for selection in the UI. For
          // example, for OneDrive for Business sites, you don't need this code because 
                // the ability to set a theme is hidden. 
          ListItemCreationInformation newLook = new ListItemCreationInformation();
                Microsoft.SharePoint.Client.ListItem newLookItem = looksGallery.AddItem(newLook);
                newLookItem["Title"] = "Theme Sample Look";
                newLookItem["Name"] = "Theme Sample Look";

                FieldUrlValue masterFieldValue = new FieldUrlValue();
                masterFieldValue.Url = masterFolderUrl + "/seattle.master";
                newLookItem["MasterPageUrl"] = masterFieldValue;

                FieldUrlValue colorFieldValue = new FieldUrlValue();
                colorFieldValue.Url = themeFolderUrl + "/ThemeSample.spcolor";
                newLookItem["ThemeUrl"] = colorFieldValue;

                FieldUrlValue fontFieldValue = new FieldUrlValue();
                fontFieldValue.Url = themeFolderUrl + "/ThemeSample.spfont";
                newLookItem["FontSchemeUrl"] = fontFieldValue;

                newLookItem.Update();

                // Apply the master page.
                hostWebObj.CustomMasterUrl = masterFieldValue.Url;

                // Update between the last and next steps. ApplyTheme throws errors if the theme
          // and master page are updated in the same query.
                hostWebObj.Update();
                clientContext.ExecuteQuery();

                // Apply the theme.
                hostWebObj.ApplyTheme(
                    colorFieldValue.Url, // URL of the color palette (.spcolor) file,
                    fontFieldValue.Url, // URL to the font scheme (.spfont) file (optional)
                    null, // Background Image URL (optional, null here),
                    false // false stores the composed look files in this web only. True shares the composed look with the site collection (to which you need permission). 

                // Need to call update to apply the change to the host web.
                hostWebObj.Update();

                // Run the Update method.
                clientContext.ExecuteQuery();
            }
        }
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="2ccae-136">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2ccae-136">Additional resources</span></span>
<span data-ttu-id="2ccae-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="2ccae-137"></span></span>

-  [<span data-ttu-id="2ccae-138">Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="2ccae-138">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="2ccae-139">Использование состоит выполняет на сайты SharePoint торговая марка</span><span class="sxs-lookup"><span data-stu-id="2ccae-139">Use composed looks to brand SharePoint sites</span></span>](Use-composed-looks-to-brand-SharePoint-sites.md)
    
-  [<span data-ttu-id="2ccae-140">Пример Branding.Themes</span><span class="sxs-lookup"><span data-stu-id="2ccae-140">Branding.Themes sample</span></span>](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes)
