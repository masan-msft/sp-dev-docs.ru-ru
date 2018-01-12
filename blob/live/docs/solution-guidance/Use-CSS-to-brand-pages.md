---
title: "Создание фирменного стиля для страниц SharePoint с помощью CSS"
ms.date: 11/03/2017
ms.openlocfilehash: b491e21a1b96d9d2843b092e763b5d45835e2e5d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="use-css-to-brand-sharepoint-pages"></a><span data-ttu-id="ae15f-102">Создание фирменного стиля для страниц SharePoint с помощью CSS</span><span class="sxs-lookup"><span data-stu-id="ae15f-102">Use CSS to brand SharePoint pages</span></span>
<span data-ttu-id="ae15f-103">Использование CSS для поддержки фирменного стиля и оформления сайта в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ae15f-103">Use CSS to support branding and site design in SharePoint.</span></span> <span data-ttu-id="ae15f-104">Узнайте, как использовать CSS в эталонных страницах и файле corev15.css, а также о роли скомпонованных представлений в настраиваемом фирменном стиле.</span><span class="sxs-lookup"><span data-stu-id="ae15f-104">Find out about CSS is master pages, the corev15.css file, and composed looks in custom branding.</span></span>

<span data-ttu-id="ae15f-105">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="ae15f-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="ae15f-106">Каскадная таблица стилей (CSS) играет важную роль в фирменном стиле SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ae15f-106">Cascading style sheet (CSS) plays a large role in SharePoint branding.</span></span> <span data-ttu-id="ae15f-107">Для успешной настройки оформления сайта в SharePoint 2013 и SharePoint Online важно понимать, как SharePoint использует CSS.</span><span class="sxs-lookup"><span data-stu-id="ae15f-107">To successfully customize the site design in SharePoint 2013 and SharePoint Online, it's useful to be familiar with how SharePoint uses CSS.</span></span>

## <a name="css-branding-overview"></a><span data-ttu-id="ae15f-108">Общие сведения о фирменном стиле CSS</span><span class="sxs-lookup"><span data-stu-id="ae15f-108">CSS branding overview</span></span>
<span data-ttu-id="ae15f-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="ae15f-109"></span></span>

<span data-ttu-id="ae15f-110">При создании семейства веб-сайтов в SharePoint создается коллекция эталонных страниц (_catalogs/masterpage), в которой хранится большинство ресурсов фирменного стиля, в том числе изображения, файлы с расширениями MASTER и CSS, HTML-файлы, а также файлы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ae15f-110">When you create a SharePoint site collection, SharePoint creates a Master Page Gallery (_catalogs/masterpage) where most branding assets, including .master, .css, image, HTML, and JavaScript files are stored.</span></span>

<span data-ttu-id="ae15f-111">В SharePoint 2013 для сайтов групп, сайтов публикации, а также для сайтов групп с поддержкой публикации по умолчанию используется страница seattle.master.</span><span class="sxs-lookup"><span data-stu-id="ae15f-111">In SharePoint 2013, SharePoint uses the seattle.master page by default for Team sites, Publishing sites, and Team sites with Publishing enabled.</span></span> <span data-ttu-id="ae15f-112">Для сайтов OneDrive для бизнеса используется страница mysite15.master.</span><span class="sxs-lookup"><span data-stu-id="ae15f-112">It uses mysite15.master for OneDrive for Business sites.</span></span> <span data-ttu-id="ae15f-113">Каждый MASTER-файл ссылается на файл corev15.css, созданный на основе нескольких CSS-файлов, которые входят в состав SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ae15f-113">Each .master file refers to the corev15.css file, which is built from a variety of .css files delivered with SharePoint out of the box.</span></span>

<span data-ttu-id="ae15f-114">Все стандартные эталонные страницы используют файл corev15.css при обработке стилей и при помощи общего доступа к каскадам и CSS-файлам определяют, какие стили применяются к тем или иным элементам управления и объектам в различных областях страницы.</span><span class="sxs-lookup"><span data-stu-id="ae15f-114">All default master pages use corev15.css when processing styles, and rely on the CSS cascade and CSS file sharing to resolve which styles are applied to specific controls and elements in regions of a page.</span></span> <span data-ttu-id="ae15f-115">Кроме того, несколько CSS-файлов объединяют для создания файла oslo.css, который используется вместе с эталонной страницей oslo.master.</span><span class="sxs-lookup"><span data-stu-id="ae15f-115">Multiple CSS files are also combined to build the oslo.css file, which is used with the oslo.master master page.</span></span>

## <a name="css-in-master-pages"></a><span data-ttu-id="ae15f-116">CSS в эталонных страницах</span><span class="sxs-lookup"><span data-stu-id="ae15f-116">CSS in master pages</span></span>
<span data-ttu-id="ae15f-117"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="ae15f-117"></span></span>

<span data-ttu-id="ae15f-118">Заполнитель содержимого `<SharePoint:CssRegistration>`, соответствующий классу [WebControls.CssRegistration](https://msdn.microsoft.com/ru-RU/library/office/microsoft.sharepoint.webcontrols.cssregistration.aspx) в серверной объектной модели, определяет CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="ae15f-118">The  `<SharePoint:CssRegistration>` content placeholder, which corresponds to the [WebControls.CssRegistration](https://msdn.microsoft.com/ru-RU/library/office/microsoft.sharepoint.webcontrols.cssregistration.aspx) class in the server-side object model, defines the CSS file.</span></span> <span data-ttu-id="ae15f-119">При обработке страницы SharePoint заменяет не только ссылку на эталонную страницу, но и соответствующие маркеры.</span><span class="sxs-lookup"><span data-stu-id="ae15f-119">Like a reference to a master page, SharePoint replaces the tokens in the master page when the page is processed.</span></span> <span data-ttu-id="ae15f-120">Класс [WebControls.CssLink](https://msdn.microsoft.com/ru-RU/library/office/microsoft.sharepoint.webcontrols.csslink.aspx) считывает данные регистрации из эталонной страницы и вставляет тег `<link>` в создаваемый HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="ae15f-120">The [WebControls.CssLink](https://msdn.microsoft.com/ru-RU/library/office/microsoft.sharepoint.webcontrols.csslink.aspx) class reads the registration from the master page and inserts a `<link>` tag in the resulting HTML file that is generated.</span></span>

<span data-ttu-id="ae15f-121">Рассмотрим приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="ae15f-121">Consider the following example.</span></span>

```
<SharePoint:CssRegistration name="<% $SPUrl:~SiteCollection/Style Library/~language/Core Styles/contoso.css%>" runat="server"/>
```

<span data-ttu-id="ae15f-122">В среде выполнения этот код обрабатывается, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae15f-122">At runtime, this code is rendered as follows.</span></span>

```
<link rel="stylesheet" type="text/css" href="/sites/nopub/Style%20Library/en-US/Core%20Styles/contoso.css">
```

<span data-ttu-id="ae15f-123">При отрисовке страницы класс **CSSLink** обрабатывает все таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="ae15f-123">The  **CSSLink** class renders all style sheets when the page is rendered.</span></span> <span data-ttu-id="ae15f-124">Если определить в собственном CSS-файле стили, также определенные в файле corev15.css, они будут заменены.</span><span class="sxs-lookup"><span data-stu-id="ae15f-124">If you define styles in a custom .css file that are also defined in corev15.css, they are overwritten.</span></span>

## <a name="corev15css-file"></a><span data-ttu-id="ae15f-125">Файл Corev15.cs</span><span class="sxs-lookup"><span data-stu-id="ae15f-125">Corev15.css file</span></span>
<span data-ttu-id="ae15f-126"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="ae15f-126"></span></span>

<span data-ttu-id="ae15f-127">Многие таблицы CSS применяются к SharePoint по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ae15f-127">A lot of CSS is applied to SharePoint by default.</span></span> <span data-ttu-id="ae15f-128">Файл corev15.css — это основной источник стилей в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ae15f-128">The corev15.css file is the main source for styles in SharePoint.</span></span> <span data-ttu-id="ae15f-129">Этот файл хранится в папке SharePoint 15 на сервере (во вложенной папке ` \TEMPLATE\LAYOUTS\1033\STYLES\Themable\COREV15.CSS`), а не в коллекции эталонных страниц корневого сайта и домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="ae15f-129">This file is stored in the SharePoint 15 folder on the server at ` \TEMPLATE\LAYOUTS\1033\STYLES\Themable\COREV15.CSS` and not in the Master Page Gallery of the root site and home page.</span></span>

<span data-ttu-id="ae15f-130">Чтобы узнать, как SharePoint использует стандартные каскадные таблицы стилей (CSS), откройте файл corev15.css с помощью средств разработчика в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="ae15f-130">To see how SharePoint uses CSS out of the box, look at the corev15.css file by using the developer tools in your web browser.</span></span> <span data-ttu-id="ae15f-131">В Internet Explorer откройте панель инструментов разработчика Internet Explorer (для этого нажмите клавишу **F12**) и выберите вкладку **CSS**, чтобы просмотреть файл corev15.css.</span><span class="sxs-lookup"><span data-stu-id="ae15f-131">In Internet Explorer, use the Internet Explorer Developer Toolbar (access it by pressing  **F12**) and choose the  **CSS** tab to view corev15.css.</span></span>

<span data-ttu-id="ae15f-132">Стили, определяемые в файле corev15.css, содержат префиксы .ms- и .s4-, указывающие на то, что эти стили были созданы корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ae15f-132">Styles defined in corev15.css use the .ms- , and .s4- prefixes, which indicate styles that were created by Microsoft.</span></span> <span data-ttu-id="ae15f-133">В corev15.css также используется много дочерних и наследуемых селекторов.</span><span class="sxs-lookup"><span data-stu-id="ae15f-133">Corev15.css also uses a lot of child and descendent selectors.</span></span> 

<span data-ttu-id="ae15f-134">Просматривая файл, вы заметите множество комментариев в следующем формате: `/* [ReplaceFont ( themeFont:"body")] */`.</span><span class="sxs-lookup"><span data-stu-id="ae15f-134">When you view the file, you'll notice many comments in this format:  `/* [ReplaceFont ( themeFont:"body")] */`.</span></span> <span data-ttu-id="ae15f-135">SharePoint считывает эти комментарии во время применения скомпонованного представления.</span><span class="sxs-lookup"><span data-stu-id="ae15f-135">SharePoint reads these comments when a composed look is applied.</span></span> <span data-ttu-id="ae15f-136">Эти комментарии указывают SharePoint на то, что необходимо заменить атрибут CSS, расположенный сразу после комментария.</span><span class="sxs-lookup"><span data-stu-id="ae15f-136">The comments tell SharePoint to change the attribute of the CSS that immediately follows the comment.</span></span> <span data-ttu-id="ae15f-137">Применение скомпонованного представления может привести к изменению многих применяемых цветов, шрифтов и фоновых изображений по умолчанию, а также к последующему обновлению параметров в файле corev15.css.</span><span class="sxs-lookup"><span data-stu-id="ae15f-137">Applying a composed look might change many of the default colors, fonts, and background images that are applied, and subsequently update the settings in corev15.css.</span></span>

> [!NOTE] 
> <span data-ttu-id="ae15f-138">Если вы выберите файл corev15.css подобным образом, загрузится не сохраненная, а отображаемая каскадная таблица стилей (CSS).</span><span class="sxs-lookup"><span data-stu-id="ae15f-138">Note  Selecting the corev15.css file this way loads the rendered CSS rather than the saved CSS.</span></span> <span data-ttu-id="ae15f-139">Иногда эти две таблицы отличаются друг от друга.</span><span class="sxs-lookup"><span data-stu-id="ae15f-139">Sometimes you might find discrepancies between the two.</span></span> <span data-ttu-id="ae15f-140">Агенты пользователя, например браузеры, также могут изменять отрисовку в ответ на действия пользователей.</span><span class="sxs-lookup"><span data-stu-id="ae15f-140">User agents such as browsers can also change rendering in response to user actions.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ae15f-141">Не входите на сервер и не изменяйте основные CSS-файлы SharePoint в корневом разделе.</span><span class="sxs-lookup"><span data-stu-id="ae15f-141">Important  Do not log on to the server and edit or customize core SharePoint CSS files in the SharePoint root.</span></span> <span data-ttu-id="ae15f-142">Подобные действия негативно отразятся на поддержке и обновлении.</span><span class="sxs-lookup"><span data-stu-id="ae15f-142">Doing so will negatively impact support and upgrade.</span></span> <span data-ttu-id="ae15f-143">Не следует изменять сам файл corev15.css. Лучше создать копию, переименовать ее и вносить изменения уже в новый файл.</span><span class="sxs-lookup"><span data-stu-id="ae15f-143">Never edit the corev15.css directly; always create a copy, rename it, and edit the new file instead.</span></span> <span data-ttu-id="ae15f-144">После внесения изменений в файл corev15.css новый фирменный стиль применяется ко всем веб-приложениям на сервере.</span><span class="sxs-lookup"><span data-stu-id="ae15f-144">Editing corev15.css will apply branding to all web applications on the server.</span></span>

### <a name="to-create-a-custom-style-sheet-for-sharepoint"></a><span data-ttu-id="ae15f-145">Создание настраиваемой таблицы стилей для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ae15f-145">To create a custom style sheet for SharePoint</span></span>

1. <span data-ttu-id="ae15f-146">Создайте копию файла corev15.css и назовите ее contosov15.css.</span><span class="sxs-lookup"><span data-stu-id="ae15f-146">Make a copy of corev15.css and name it contosov15.css.</span></span>
    
2. <span data-ttu-id="ae15f-147">Откройте файл contosov15.css и внесите изменения в строку CssRegistration, как показано в примере ниже, чтобы она указывала на файл contosov15.css, а не на corev15.css.</span><span class="sxs-lookup"><span data-stu-id="ae15f-147">Open contosov15.css and modify the CssRegistration line to point to contosov15.css from corev15.css, as shown in the following example.</span></span>
    
  ```
  <SharePoint:CssRegistration Name="Themable/contoso.css" runat="server" />
  ```

3. <span data-ttu-id="ae15f-148">Под строкой CssRegistration добавьте строку, приведенную ниже.</span><span class="sxs-lookup"><span data-stu-id="ae15f-148">Below the CssRegistration line, add the following.</span></span>
    
  ```
  <SharePoint:CssRegistration name="/_catalogs/masterpage/contoso/contoso.css" 
runat="server">

  ```

## <a name="composed-looks-in-custom-branding"></a><span data-ttu-id="ae15f-149">Скомпонованные представления в настраиваемом фирменном стиле</span><span class="sxs-lookup"><span data-stu-id="ae15f-149">Composed looks in custom branding</span></span>
<span data-ttu-id="ae15f-150"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="ae15f-150"></span></span>

<span data-ttu-id="ae15f-151">Вы можете использовать скомпонованные представления в настраиваемом фирменном стиле, если таблица CSS вызывается из эталонной страницы.</span><span class="sxs-lookup"><span data-stu-id="ae15f-151">You can use composed looks in custom branding when CSS is called from a master page.</span></span> <span data-ttu-id="ae15f-152">CSS-файл хранится в файловой системе SharePoint в одном из следующих расположений:</span><span class="sxs-lookup"><span data-stu-id="ae15f-152">The CSS file is stored in the SharePoint file system in one of the following locations:</span></span> 

-  `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable`
    
-  `/Style Library/Themable/`
    
-  `/Style Library/{culture}/Themable/`
    
<span data-ttu-id="ae15f-153">Собственные файлы стилей можно размещать в папках `/Style Library/Themable/` и `/Style Library/{culture}/Themable/`. Папка `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable` не поддерживает редактирование, поэтому в ней нельзя хранить собственные файлы.</span><span class="sxs-lookup"><span data-stu-id="ae15f-153">You can place custom branding files in  `/Style Library/Themable/` and `/Style Library/{culture}/Themable/`, but  `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable` is not editable, so you can't store custom files in that location.</span></span>

> [!NOTE] 
> <span data-ttu-id="ae15f-154">Если эти папки не существуют по умолчанию, их можно создать вручную. В этом случае SharePoint распознает их как тематические.</span><span class="sxs-lookup"><span data-stu-id="ae15f-154">Note  If these locations don't exist by default, you can create them manually and SharePoint will recognize them as themable.</span></span>

## <a name="applying-custom-css-to-a-sharepoint-page"></a><span data-ttu-id="ae15f-155">Применение собственной таблицы стилей CSS к странице SharePoint</span><span class="sxs-lookup"><span data-stu-id="ae15f-155">Applying custom CSS to a SharePoint page</span></span>
<span data-ttu-id="ae15f-156"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="ae15f-156"></span></span>

<span data-ttu-id="ae15f-157">Вы можете добавлять настраиваемые таблицы CSS в поля форматированного текста и зоны веб-частей.</span><span class="sxs-lookup"><span data-stu-id="ae15f-157">You can add custom CSS to rich text fields and Web Part zones.</span></span> <span data-ttu-id="ae15f-158">Чтобы добавить CSS в поле форматированного текста, перейдите в режим правки страницы и на ленте выберите элементы **Вставка** > **Код внедрения**.</span><span class="sxs-lookup"><span data-stu-id="ae15f-158">To add CSS to a rich text field, put the page in edit mode and choose  **Insert** > **Embed Code** from the ribbon.</span></span> <span data-ttu-id="ae15f-159">В зонах веб-частей для добавления HTML-файлов, скриптов и внутренних таблиц стилей используйте веб-часть редактора скриптов.</span><span class="sxs-lookup"><span data-stu-id="ae15f-159">For Web Part zones, use the Script Editor Web Part to add HTML, scripts, or an internal style sheet.</span></span> <span data-ttu-id="ae15f-160">Этот подход рекомендуется применять, чтобы скрыть панель быстрого запуска в стандартном пользовательском интерфейсе SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ae15f-160">You can use this approach to hide the Quick Launch navigation in the default SharePoint UI.</span></span> <span data-ttu-id="ae15f-161">Если с SharePoint Online используется функция NoScript, она отключает веб-часть редактора скриптов.</span><span class="sxs-lookup"><span data-stu-id="ae15f-161">If you are using SharePoint Online and the NoScript feature, NoScript will disable Script Editor Web Part.</span></span>

<span data-ttu-id="ae15f-162">Примените таблицу CSS к сайту SharePoint с помощью внешней таблицы стилей, включив ссылку на нее в тег `<link>`, находящийся внутри тегов `<head>` страницы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ae15f-162">Apply CSS to a SharePoint site by using an external style sheet and including a reference to the style sheet in the  `<link>` tag inside the `<head>` tags of the SharePoint page.</span></span>

<span data-ttu-id="ae15f-163">В приведенном ниже примере кода показано, как добавить настраиваемую таблицу CSS в библиотеку ресурсов, вставить ссылку на URL-адрес CSS с помощью дополнительного действия, а затем создать дополнительное действие для создания ссылки на новый CSS-файл.</span><span class="sxs-lookup"><span data-stu-id="ae15f-163">The following code example shows how to upload custom CSS to the asset library, apply a reference to the CSS URL with a custom action, and then create a custom action to build a link to the new CSS file.</span></span> <span data-ttu-id="ae15f-164">Этот код входит в состав примера [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="ae15f-164">This code is part of the  [Branding.AlternateCSSAndSiteLogo ](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) sample on GitHub.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="ae15f-165">См. также</span><span class="sxs-lookup"><span data-stu-id="ae15f-165">See also</span></span>
<span data-ttu-id="ae15f-166"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ae15f-166"></span></span>

-  [<span data-ttu-id="ae15f-167">Решения для создания фирменного стиля и настройки страниц на сайтах SharePoint</span><span class="sxs-lookup"><span data-stu-id="ae15f-167">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="ae15f-168">Пример Branding.AlternateCSSAndSiteLogo</span><span class="sxs-lookup"><span data-stu-id="ae15f-168">Branding.AlternateCSSAndSiteLogo sample</span></span>](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
