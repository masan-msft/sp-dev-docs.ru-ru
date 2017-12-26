---
title: "Создание фирменного стиля для страниц SharePoint с помощью CSS"
ms.date: 11/03/2017
ms.openlocfilehash: b491e21a1b96d9d2843b092e763b5d45835e2e5d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-css-to-brand-sharepoint-pages"></a>Создание фирменного стиля для страниц SharePoint с помощью CSS
Использование CSS для поддержки фирменного стиля и оформления сайта в SharePoint. Узнайте, как использовать CSS в эталонных страницах и файле corev15.css, а также о роли скомпонованных представлений в настраиваемом фирменном стиле.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Каскадная таблица стилей (CSS) играет важную роль в фирменном стиле SharePoint. Для успешной настройки оформления сайта в SharePoint 2013 и SharePoint Online важно понимать, как SharePoint использует CSS.

## <a name="css-branding-overview"></a>Общие сведения о фирменном стиле CSS
<a name="sectionSection0"> </a>

При создании семейства веб-сайтов в SharePoint создается коллекция эталонных страниц (_catalogs/masterpage), в которой хранится большинство ресурсов фирменного стиля, в том числе изображения, файлы с расширениями MASTER и CSS, HTML-файлы, а также файлы JavaScript.

В SharePoint 2013 для сайтов групп, сайтов публикации, а также для сайтов групп с поддержкой публикации по умолчанию используется страница seattle.master. Для сайтов OneDrive для бизнеса используется страница mysite15.master. Каждый MASTER-файл ссылается на файл corev15.css, созданный на основе нескольких CSS-файлов, которые входят в состав SharePoint.

Все стандартные эталонные страницы используют файл corev15.css при обработке стилей и при помощи общего доступа к каскадам и CSS-файлам определяют, какие стили применяются к тем или иным элементам управления и объектам в различных областях страницы. Кроме того, несколько CSS-файлов объединяют для создания файла oslo.css, который используется вместе с эталонной страницей oslo.master.

## <a name="css-in-master-pages"></a>CSS в эталонных страницах
<a name="sectionSection1"> </a>

Заполнитель содержимого `<SharePoint:CssRegistration>`, соответствующий классу [WebControls.CssRegistration](https://msdn.microsoft.com/ru-RU/library/office/microsoft.sharepoint.webcontrols.cssregistration.aspx) в серверной объектной модели, определяет CSS-файл. При обработке страницы SharePoint заменяет не только ссылку на эталонную страницу, но и соответствующие маркеры. Класс [WebControls.CssLink](https://msdn.microsoft.com/ru-RU/library/office/microsoft.sharepoint.webcontrols.csslink.aspx) считывает данные регистрации из эталонной страницы и вставляет тег `<link>` в создаваемый HTML-файл.

Рассмотрим приведенный ниже пример.

```
<SharePoint:CssRegistration name="<% $SPUrl:~SiteCollection/Style Library/~language/Core Styles/contoso.css%>" runat="server"/>
```

В среде выполнения этот код обрабатывается, как описано ниже.

```
<link rel="stylesheet" type="text/css" href="/sites/nopub/Style%20Library/en-US/Core%20Styles/contoso.css">
```

При отрисовке страницы класс **CSSLink** обрабатывает все таблицы стилей. Если определить в собственном CSS-файле стили, также определенные в файле corev15.css, они будут заменены.

## <a name="corev15css-file"></a>Файл Corev15.cs
<a name="sectionSection2"> </a>

Многие таблицы CSS применяются к SharePoint по умолчанию. Файл corev15.css — это основной источник стилей в SharePoint. Этот файл хранится в папке SharePoint 15 на сервере (во вложенной папке ` \TEMPLATE\LAYOUTS\1033\STYLES\Themable\COREV15.CSS`), а не в коллекции эталонных страниц корневого сайта и домашней страницы.

Чтобы узнать, как SharePoint использует стандартные каскадные таблицы стилей (CSS), откройте файл corev15.css с помощью средств разработчика в веб-браузере. В Internet Explorer откройте панель инструментов разработчика Internet Explorer (для этого нажмите клавишу **F12**) и выберите вкладку **CSS**, чтобы просмотреть файл corev15.css.

Стили, определяемые в файле corev15.css, содержат префиксы .ms- и .s4-, указывающие на то, что эти стили были созданы корпорацией Майкрософт. В corev15.css также используется много дочерних и наследуемых селекторов. 

Просматривая файл, вы заметите множество комментариев в следующем формате: `/* [ReplaceFont ( themeFont:"body")] */`. SharePoint считывает эти комментарии во время применения скомпонованного представления. Эти комментарии указывают SharePoint на то, что необходимо заменить атрибут CSS, расположенный сразу после комментария. Применение скомпонованного представления может привести к изменению многих применяемых цветов, шрифтов и фоновых изображений по умолчанию, а также к последующему обновлению параметров в файле corev15.css.

> [!NOTE] 
> Если вы выберите файл corev15.css подобным образом, загрузится не сохраненная, а отображаемая каскадная таблица стилей (CSS). Иногда эти две таблицы отличаются друг от друга. Агенты пользователя, например браузеры, также могут изменять отрисовку в ответ на действия пользователей.

> [!IMPORTANT] 
> Не входите на сервер и не изменяйте основные CSS-файлы SharePoint в корневом разделе. Подобные действия негативно отразятся на поддержке и обновлении. Не следует изменять сам файл corev15.css. Лучше создать копию, переименовать ее и вносить изменения уже в новый файл. После внесения изменений в файл corev15.css новый фирменный стиль применяется ко всем веб-приложениям на сервере.

### <a name="to-create-a-custom-style-sheet-for-sharepoint"></a>Создание настраиваемой таблицы стилей для SharePoint

1. Создайте копию файла corev15.css и назовите ее contosov15.css.
    
2. Откройте файл contosov15.css и внесите изменения в строку CssRegistration, как показано в примере ниже, чтобы она указывала на файл contosov15.css, а не на corev15.css.
    
  ```
  <SharePoint:CssRegistration Name="Themable/contoso.css" runat="server" />
  ```

3. Под строкой CssRegistration добавьте строку, приведенную ниже.
    
  ```
  <SharePoint:CssRegistration name="/_catalogs/masterpage/contoso/contoso.css" 
runat="server">

  ```

## <a name="composed-looks-in-custom-branding"></a>Скомпонованные представления в настраиваемом фирменном стиле
<a name="sectionSection3"> </a>

Вы можете использовать скомпонованные представления в настраиваемом фирменном стиле, если таблица CSS вызывается из эталонной страницы. CSS-файл хранится в файловой системе SharePoint в одном из следующих расположений: 

-  `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable`
    
-  `/Style Library/Themable/`
    
-  `/Style Library/{culture}/Themable/`
    
Собственные файлы стилей можно размещать в папках `/Style Library/Themable/` и `/Style Library/{culture}/Themable/`. Папка `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable` не поддерживает редактирование, поэтому в ней нельзя хранить собственные файлы.

> [!NOTE] 
> Если эти папки не существуют по умолчанию, их можно создать вручную. В этом случае SharePoint распознает их как тематические.

## <a name="applying-custom-css-to-a-sharepoint-page"></a>Применение собственной таблицы стилей CSS к странице SharePoint
<a name="sectionSection4"> </a>

Вы можете добавлять настраиваемые таблицы CSS в поля форматированного текста и зоны веб-частей. Чтобы добавить CSS в поле форматированного текста, перейдите в режим правки страницы и на ленте выберите элементы **Вставка** > **Код внедрения**. В зонах веб-частей для добавления HTML-файлов, скриптов и внутренних таблиц стилей используйте веб-часть редактора скриптов. Этот подход рекомендуется применять, чтобы скрыть панель быстрого запуска в стандартном пользовательском интерфейсе SharePoint. Если с SharePoint Online используется функция NoScript, она отключает веб-часть редактора скриптов.

Примените таблицу CSS к сайту SharePoint с помощью внешней таблицы стилей, включив ссылку на нее в тег `<link>`, находящийся внутри тегов `<head>` страницы SharePoint.

В приведенном ниже примере кода показано, как добавить настраиваемую таблицу CSS в библиотеку ресурсов, вставить ссылку на URL-адрес CSS с помощью дополнительного действия, а затем создать дополнительное действие для создания ссылки на новый CSS-файл. Этот код входит в состав примера [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) на сайте GitHub.

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using System.IO;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.EventReceivers;

namespace AlternateCSSAppAutohostedWeb.Services
{
    public class AppEventReceiver : IRemoteEventService
    {
        public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {
            SPRemoteEventResult result = new SPRemoteEventResult();

            try
            {
                using (ClientContext clientContext = TokenHelper.CreateAppEventClientContext(properties, false))
                {
                    if (clientContext != null)
                    {
                        Web hostWebObj = clientContext.Web;

                        List assetLibrary = hostWebObj.Lists.GetByTitle("Site Assets");
                        clientContext.Load(assetLibrary, l => l.RootFolder);

                        // First, upload the CSS files to the Asset library.
                        DirectoryInfo themeDir = new DirectoryInfo(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "CSS");
                        foreach (var themeFile in themeDir.EnumerateFiles())
                        {
                            FileCreationInformation newFile = new FileCreationInformation();
                            newFile.Content = System.IO.File.ReadAllBytes(themeFile.FullName);
                            newFile.Url = themeFile.Name;
                            newFile.Overwrite = true;

                            Microsoft.SharePoint.Client.File uploadAsset = assetLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(uploadAsset);
                            break;
                        }
                        
                        string actionName = "SampleCSSLink";

                        // Now, apply a reference to the CSS URL via a custom action.
                        
                        // Clean up existing actions that you might have deployed.
                        var existingActions = hostWebObj.UserCustomActions;
                        clientContext.Load(existingActions);

                        // Run uploads and initialize the existing Actions collection.
                        clientContext.ExecuteQuery();

                        // Clean up existing actions.
                        foreach (var existingAction in existingActions)
                        {
                            if(existingAction.Name.Equals(actionName, StringComparison.InvariantCultureIgnoreCase))
                                existingAction.DeleteObject();
                        }
                        clientContext.ExecuteQuery();

                        // Build a custom action to write a link to our new CSS file.
                        UserCustomAction cssAction = hostWebObj.UserCustomActions.Add();
                        cssAction.Location = "ScriptLink";
                        cssAction.Sequence = 100;
                        cssAction.ScriptBlock = @"document.write('<link rel=""stylesheet"" href=""" + assetLibrary.RootFolder.ServerRelativeUrl + @"/cs-style.css"" />');";
                        cssAction.Name = actionName;
                        
                        // Apply.
                        cssAction.Update();
                        clientContext.ExecuteQuery();
                    }
                    result.Status = SPRemoteEventServiceStatus.Continue;
                    return result;
                }
            }
            catch (Exception ex)
            {
                result.Status = SPRemoteEventServiceStatus.CancelWithError;
                result.ErrorMessage = ex.Message;
                return result;
            }
            
        }

        public void ProcessOneWayEvent(SPRemoteEventProperties properties)
        {
            // This method is not used by app events.
        }
    }
}
```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [Пример Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
