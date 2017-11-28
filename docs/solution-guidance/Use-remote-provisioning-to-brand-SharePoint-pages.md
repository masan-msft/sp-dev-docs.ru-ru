---
title: "Использование удаленного обеспечения марки страницах SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 195d5e183850625d732ae696447cbc9a56ab1e8b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="use-remote-provisioning-to-brand-sharepoint-pages"></a>Использование удаленного обеспечения марки страницах SharePoint

Использование удаленных подготовки для взаимодействия с темами в SharePoint.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Можно применить и взаимодействовать с тем с помощью удаленного подготовки функций в SharePoint. Эти функции поддерживаются следующие интерфейсы API:

-  [Метод ApplyTheme](http://msdn.microsoft.com/library/52c567e8-03e6-7ba3-a9ed-cf4e3c22dbdd%28Office.15%29.aspx)
    
-  [Класс ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx)
    
Метод **ApplyTheme** обеспечивает питание изменение внешнего вида мастера. Мастер применяет внешний вид acomposed или пользовательского вида на сайте SharePoint с помощью указанных компонентов. Темы применяются для отдельных сайтов с сайта.
С помощью **ApplyTheme** и **ThemeInfo** интерфейсы API в CSOM и JSOM предоставляются **ApplyThemeApp** и интерфейсы API **ThemeInfo** на сервере.
Образец, показано, как применить существующую или новую тему видеть [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes) на репозиториев.

## <a name="applytheme-method"></a>Метод ApplyTheme
<a name="sectionSection0"> </a>

Метод **ApplyTheme** со стороны клиента при использовании удаленного подготовки для применения темы, как показано в следующем примере.

```
public void ApplyTheme(
            string colorPaletteUrl,
            string fontSchemeUrl,
            string backgroundImageUrl,
            bool shareGenerated
             )
```

Метод **ApplyTheme** использует следующие параметры:

- colorPaletteUrl - зависящий от сервера URL-адрес файла цветовой палитры (например, spcolor).
    
- fontSchemeUrl - зависящий от сервера URL-адрес файла схемы шрифта (например, spfont).
    
- backgroundImageUrl - зависящий от сервера URL-адрес фонового изображения. Если нет фонового изображения, этот параметр Возвращает ссылку на **значение null** .
    
- shareGenerated — логическое значение. **Значение true,** Если созданных файлов темы, которые должны применяться к корневого веб-узла; **значение false,** если они находятся в текущем веб-узле.

**Примечание**  Параметр shareGenerated определяет, будет ли темой выходные файлы хранятся в папку, доступную через семейства веб-сайтов или веб-узла. Мы рекомендуем оставьте значение по умолчанию для соответствующего типа сайта.

## <a name="themeinfo-class"></a>Класс ThemeInfo
<a name="sectionSection1"> </a>

CSOM кода можно использовать для получения сведений о вариантов оформления, применяемых к сайту. Класс [ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx) Возвращает контекст, связанные с тем, как показано в следующем примере.

```
public ThemeInfo ThemeInfo { get; }
```

Класс **ThemeInfo** можно использовать для получения сведений о темах, применяемых к сайту, включая описания, контекста, данных объекта, цвета и шрифты для указанного имени (и шрифты для указанного языка кода), а также URI для фона изображение, определенных для вариант оформления.

## <a name="using-applytheme-and-themeinfo-in-csom-code"></a>Использование ApplyTheme и ThemeInfo в коде CSOM
<a name="sectionSection2"> </a>

В следующем примере кода показано, как использовать **ApplyTheme** и **ThemeInfo** в коде CSOM. Этот код можно использовать в шаблоне удаленного подготовки. Например можно программно, как указано в конструкторе создание вариантов оформления и подготовить их сайтов в веб-приложения.

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

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>

-  [Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [Использование состоит выполняет на сайты SharePoint торговая марка](Use-composed-looks-to-brand-SharePoint-sites.md)
    
-  [Пример Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes)
