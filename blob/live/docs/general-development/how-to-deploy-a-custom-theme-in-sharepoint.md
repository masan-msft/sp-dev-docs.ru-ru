---
title: "Инструкции. Развертывание пользовательской темы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f703df24-8e56-4e6a-bc37-95acbb3c83e8
ms.openlocfilehash: 002ee3e01c3d68f28ceb4ac3e8c9f66b4a1dec8c
ms.sourcegitcommit: 11d9185437fc819ab41421c0f4fe06aa300b9d28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2017
---
# <a name="how-to-deploy-a-custom-theme-in-sharepoint"></a><span data-ttu-id="ea3a8-102">Инструкции. Развертывание пользовательской темы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea3a8-102">How to: Deploy a custom theme in SharePoint</span></span>
<span data-ttu-id="ea3a8-p101">Узнайте, как развертывать пользовательскую тему на сайте SharePoint, используя пользовательский интерфейс или приемник компонента. SharePoint содержит предустановленные темы. Кроме того, можно создавать пользовательские темы с помощью собственных дополнительных цветовых палитр, эталонных страниц и схем шрифтов. После отправки файлов в коллекцию тем и коллекцию эталонных страниц можно приступать к развертыванию темы на сайте с помощью пользовательского интерфейса или кода. Сведения о цветовых палитрах и схемах шрифтов см. в статье  [Цветовые палитры и шрифты в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p101">Learn how to deploy a custom theme to a SharePoint site by using the user interface or by implementing a feature receiver. SharePoint includes preinstalled themes. You can create custom themes by creating additional color palettes, font schemes, and master pages. After the files are uploaded to the Theme Gallery and the Master Page Gallery, you can deploy a theme to a site by using the user interface or by using code. For more information about color palettes and font schemes, see  [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
> [!NOTE]
> <span data-ttu-id="ea3a8-108">Информация в этой статье относится только к классическим сайтам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-108">This article only applies in the context of classic SharePoint site experience.</span></span> <span data-ttu-id="ea3a8-109">Сведения для современных сайтов SharePoint см. в статье [Настройка тем для сайтов SharePoint](https://docs.microsoft.com/ru-RU/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview).</span><span class="sxs-lookup"><span data-stu-id="ea3a8-109">If you are looking details around modern SharePoint sites and their theme support, please have a look on the following article - [SharePoint site theming](https://docs.microsoft.com/ru-RU/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview)</span></span>


## <a name="core-concepts-to-know-to-deploy-a-theme"></a><span data-ttu-id="ea3a8-110">Основные сведения о развертывании темы</span><span class="sxs-lookup"><span data-stu-id="ea3a8-110">Core concepts to know to deploy a theme</span></span>
<span data-ttu-id="ea3a8-111"><a name="core"> </a></span><span class="sxs-lookup"><span data-stu-id="ea3a8-111"></span></span>

<span data-ttu-id="ea3a8-112">В таблице 1 перечислены статьи, содержащие основные понятия, которые нужно знать при развертывании тем.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-112">Table 1 lists articles that can help you understand the core concepts of deploying themes.</span></span>
  
    
    

<span data-ttu-id="ea3a8-113">**Таблица 1. Основные понятия, которые нужно знать при развертывании темы**</span><span class="sxs-lookup"><span data-stu-id="ea3a8-113">**Table 1. Core concepts to deploy a theme**</span></span>


|<span data-ttu-id="ea3a8-114">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="ea3a8-114">**Article title**</span></span>|<span data-ttu-id="ea3a8-115">**Описание**</span><span class="sxs-lookup"><span data-stu-id="ea3a8-115">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="ea3a8-116">Общие сведения о темах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea3a8-116">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md) <br/> |<span data-ttu-id="ea3a8-117">Сведения о работе с темами в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-117">Learn about the theming experience in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="ea3a8-118">События компонента</span><span class="sxs-lookup"><span data-stu-id="ea3a8-118">Feature Events</span></span>](http://msdn.microsoft.com/ru-RU/library/ms469501.aspx) <br/> |<span data-ttu-id="ea3a8-119">Сведения о событиях компонента, позволяющих отслеживать события, возникающие при установке компонента в ферму серверов, и реагировать на них должным образом.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-119">Learn about feature events, which enable you to trap and respond to an event that occurs when a feature is installed in the server farm.</span></span>  <br/> |
   

## <a name="upload-files-to-the-theme-gallery-and-the-master-page-gallery"></a><span data-ttu-id="ea3a8-120">Отправка файлов в коллекцию тем и коллекцию эталонных страниц</span><span class="sxs-lookup"><span data-stu-id="ea3a8-120">Upload files to the Theme Gallery and the Master Page Gallery</span></span>
<span data-ttu-id="ea3a8-121"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="ea3a8-121"></span></span>

<span data-ttu-id="ea3a8-p103">Для создания пользовательских тем можно использовать собственные дополнительные цветовые палитры и схемы шрифтов. Отправьте их в коллекцию тем, чтобы получить к ним доступ при изменении дизайна во время работы с темами или при программном применении темы. Аналогично в коллекцию эталонных страниц можно отправить дополнительные эталонные страницы и соответствующие файлы предварительного просмотра для добавления дополнительных макетов сайта. Ниже описано, куда помещать эти файлы.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p103">You can create custom themes by creating additional color palettes and font schemes and uploading them to the Theme Gallery. The new color palettes and font schemes are then available to you when you modify a design in the theming experience or when you apply a theme programmatically. Similarly, if you want to have additional site layouts to choose from, you can upload additional master pages, and corresponding preview files, to the Master Page Gallery. The following list describes where to place the files:</span></span>
  
    
    

- <span data-ttu-id="ea3a8-p104">**Коллекция эталонных страниц**. Содержит файлы эталонных страниц и соответствующие им файлы предварительного просмотра (файлы PREVIEW). Файл предварительного просмотра эталонной страницы требуется, если необходимо, чтобы эталонная страница была доступна в мастере **изменения оформления**. Файлы JavaScript и другие файлы для оформления также можно отправлять в коллекцию эталонных страниц.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p104">**Master Page Gallery** Lists the master page files, and their corresponding preview files (.preview files). A master page preview file is required if you want the master page to be available in the **Change the look** wizard. JavaScript files and other design assets can also be uploaded to the Master Page Gallery.</span></span>
    
    <span data-ttu-id="ea3a8-p105">Чтобы получить доступ к коллекции эталонных страниц из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** выберите пункт **Главные страницы**. Вы также можете перейти непосредственно на сайт по ссылке http:// _ИмяСайта_/_catalogs/masterpage/.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p105">To access the Master Page Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, choose **Master pages**. You can also navigate directly to the site (http://  _SiteName_/_catalogs/masterpage/).</span></span>
    
  
- <span data-ttu-id="ea3a8-p106">**Коллекция тем**. Содержит цветовые палитры и схемы шрифтов, доступные для работы с темами. SharePoint ищет доступные цветовые палитры и схемы шрифтов в папке **15**.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p106">**Theme Gallery** Lists the color palettes and font schemes that are available to the theming experience. SharePoint looks in the **15** folder to determine the available color palettes and font schemes.</span></span>
    
    <span data-ttu-id="ea3a8-p107">Чтобы получить доступ к коллекции тем из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** выберите пункт **Темы**. Вы также можете перейти непосредственно на сайт по ссылке http:// _ИмяСемействаСайтов_/_catalogs/theme/15/.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p107">To access the Theme Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, choose **Themes**. You can also navigate directly to the site (http:// _SiteCollectionName_/_catalogs/theme/15/).</span></span>
    
  
- <span data-ttu-id="ea3a8-p108">**Библиотека стилей**. Содержит пользовательские файлы CSS, необходимые при работе с темами. Чтобы перейти непосредственно к библиотеке стилей, замените  _ИмяСемействаСайтов_ и _язык_ в этом URL-адресе: http:// _ИмяСемействаСайтов_/Style Library/ _язык_/Themable/.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p108">**Style library** Lists custom CSS files that you want to use in the theming experience. You can navigate directly to the Style library (replace _SiteCollectionName_ and _language_ in this URL: http:// _SiteCollectionName_/Style Library/ _language_/Themable/).</span></span>
    
    > <span data-ttu-id="ea3a8-137">**Примечание.** Сохраняйте пользовательские CSS-файлы в папке Themable в библиотеке стилей, а не в коллекции эталонных страниц.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-137">**Note** Place the custom CSS files in the Themable folder in the Style library, not the Themable folder in the Master Page Gallery. Only CSS files that are stored in the Themable folder in the Style library are recognized by the theming engine.</span></span> <span data-ttu-id="ea3a8-138">Обработчик тем распознает только CSS-файлы, сохраненные в папке Themable в библиотеке стилей.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-138">Place the custom CSS files in the Themable folder in the Style library, not the Themable folder in the Master Page Gallery. Only CSS files that are stored in the Themable folder in the Style library are recognized by the theming engine.</span></span> 

> <span data-ttu-id="ea3a8-139">**Примечание.** Если для коллекции эталонных страниц и коллекции тем включено управление версиями, чтобы обработчик тем мог использовать файлы оформления, их необходимо опубликовать.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-139">**Note** If you have versioning enabled on the Master Page Gallery and the Theme Gallery, you must also publish the design files before they can be used by the theming engine.</span></span> 
  
    
    


## <a name="deploy-a-theme-by-using-the-user-interface"></a><span data-ttu-id="ea3a8-140">Развертывание темы с помощью пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ea3a8-140">Deploy a theme by using the user interface</span></span>
<span data-ttu-id="ea3a8-141"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="ea3a8-141"></span></span>

<span data-ttu-id="ea3a8-p110">Вариант оформления, или макет, включает в себя цветовую палитру, схему шрифтов, фоновое изображение и эталонную страницу, которые определяют внешний вид сайта. Список вариантов оформления содержит те из них, которые доступны в коллекции макетов. Чтобы создать макет, добавьте элемент в список вариантов оформления и укажите для него эталонную страницу, цветовую палитру, схему шрифтов и фоновое изображение.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p110">A composed look, or design, is the color palette, font scheme, background image, and master page that determine the look and feel of a site. The Composed Looks list contains the composed looks that are available in the design gallery. You create a design by adding a list item in the Composed Looks list and specifying the master page, color palette, font scheme, and background image to use.</span></span>
  
    
    

> <span data-ttu-id="ea3a8-145">**Примечание.** Чтобы эталонная страница была доступна в коллекции макетов, требуется файл предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-145">**Note** A master page preview file is required if you want the master page to be available in the design gallery.</span></span> 
  
    
    


### <a name="to-add-a-composed-look"></a><span data-ttu-id="ea3a8-146">Добавление варианта оформления</span><span class="sxs-lookup"><span data-stu-id="ea3a8-146">To add a composed look</span></span>


1. <span data-ttu-id="ea3a8-147">Щелкните значок **Параметры**, затем выберите пункт **Параметры сайта**.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-147">Choose the **Settings** icon, and then choose **Site settings**.</span></span>
    
  
2. <span data-ttu-id="ea3a8-148">В разделе **Коллекция веб-дизайнера** щелкните ссылку **Варианты оформления**.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-148">Under **Web Designer Galleries**, choose **Composed looks**.</span></span>
    
  
3. <span data-ttu-id="ea3a8-149">В списке **Варианты оформления** щелкните ссылку **Создайте элемент**.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-149">In the **Composed Looks** list, select **new item**.</span></span>
    
  
4. <span data-ttu-id="ea3a8-150">В текстовом поле **Название** введите название макета.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-150">In the **Title** text box, enter a title for the design.</span></span>
    
  
5. <span data-ttu-id="ea3a8-p111">В текстовом поле **Имя** введите имя макета, которое отображается в списке вариантов оформления и в коллекции макетов.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p111">In the **Name** text box, enter a name for the design. The name appears in the Composed Looks list and in the design gallery.</span></span>
    
  
6. <span data-ttu-id="ea3a8-p112">В текстовом поле **URL-адрес главной страницы** введите URL-адрес эталонной страницы (можно использовать относительный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p112">In the **Master Page URL** text box, enter the URL of the master page. The URL can be a relative URL.</span></span>
    
  
7. <span data-ttu-id="ea3a8-p113">В текстовом поле **URL-адрес темы** введите URL-адрес цветовой палитры, т. е. URL-адрес, ведущий к файлу SPCOLOR (можно использовать относительный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p113">In the **Theme URL** text box, enter the URL of the color palette (the URL to the .spcolor file). The URL can be a relative URL.</span></span>
    
  
8. <span data-ttu-id="ea3a8-p114">В текстовом поле **URL-адрес изображения** введите URL-адрес фонового изображения. Этот шаг необязательный. Можно использовать относительный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p114">In the **Image URL** text box, enter the URL of the background image. This is optional. The URL can be a relative URL.</span></span>
    
  
9. <span data-ttu-id="ea3a8-p115">В текстовом поле **URL-адрес шрифтовой схемы** введите URL-адрес схемы шрифтов, т. е. URL-адрес, ведущий к файлу SPFONT. Этот шаг необязательный. Можно использовать относительный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p115">In the **Font Scheme URL** text box, enter the URL of the font scheme (the URL to the .spfont file). This is optional. The URL can be a relative URL.</span></span>
    
  
10. <span data-ttu-id="ea3a8-p116">В текстовом поле **Порядок отображения** укажите для макета порядковый номер, определяющий место макета в коллекции макетов.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-p116">In the **Display Order** text box, enter the display order number. This determines where the design appears in the design gallery.</span></span>
    
  
11. <span data-ttu-id="ea3a8-165">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-165">Choose **Save**.</span></span>
    
    > <span data-ttu-id="ea3a8-166">**Примечание.** Если возникнет проблема со значениями, вариант оформления не будет добавлен в библиотеку макетов (без записи в файлах журнала).</span><span class="sxs-lookup"><span data-stu-id="ea3a8-166">If there is an issue with the composed look values, the composed look is not added to the design gallery, and no message is recorded in the log files. The following are possible reasons why a composed look cannot be added: a file cannot be found, there is a formatting issue with one of the files, or SharePoint is unable to access the files.</span></span> <span data-ttu-id="ea3a8-167">Если не удается добавить вариант оформления, это может быть вызвано одной из следующих причин: не удается найти файл, возникла проблема с форматом одного из файлов или SharePoint не может получить доступ к файлам.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-167">If there is an issue with the composed look values, the composed look is not added to the design gallery, and no message is recorded in the log files. The following are possible reasons why a composed look cannot be added: a file cannot be found, there is a formatting issue with one of the files, or SharePoint is unable to access the files.</span></span> 
      > <span data-ttu-id="ea3a8-168">Теперь вы можете использовать библиотеку макетов, чтобы применить новый дизайн.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-168">You can now use the design gallery to apply the new design to your site. For more information, see Choose a theme for your publishing sitehttp://office.microsoft.com/ru-RU/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx on Office.com.</span></span> <span data-ttu-id="ea3a8-169">Дополнительные сведения см. в статье [Выбор темы для сайта публикации](http://office.microsoft.com/ru-RU/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea3a8-169">You can also decide to use one of the preinstalled SharePoint 2013 themes. For more information, see  [Choose a theme for your publishing site](http://office.microsoft.com/ru-RU/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx) on Office.com.</span></span>
  
    
    

## <a name="deploy-a-theme-by-using-code"></a><span data-ttu-id="ea3a8-170">Развертывание темы с помощью кода</span><span class="sxs-lookup"><span data-stu-id="ea3a8-170">Deploy a theme by using code</span></span>
<span data-ttu-id="ea3a8-171"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="ea3a8-171"></span></span>

<span data-ttu-id="ea3a8-172">Вы можете выполнить развертывание темы, используя приемник компонента.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-172">You can deploy a theme by implementing a feature receiver.</span></span>
  
    
    

### <a name="to-deploy-a-theme-by-using-a-feature-receiver"></a><span data-ttu-id="ea3a8-173">Для этого:</span><span class="sxs-lookup"><span data-stu-id="ea3a8-173">To deploy a theme by using a feature receiver</span></span>


1. <span data-ttu-id="ea3a8-174">Создайте класс приемника компонента, который наследует классу  [SPFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ea3a8-174">Create a feature receiver class that inherits from the  [SPFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.aspx) class.</span></span>
    
  
2. <span data-ttu-id="ea3a8-175">В методе  [FeatureActivated](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.FeatureActivated.aspx) создайте объект [SPTheme](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.aspx) , использующий нужную цветовую палитру и схему шрифтов, а затем примените тему к своему сайту.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-175">In the  [FeatureActivated](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.FeatureActivated.aspx) method, create an [SPTheme](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.aspx) object that uses the color palette and font scheme, and then apply the theme to your site.</span></span>
    
    <span data-ttu-id="ea3a8-176">Ниже показано, как развернуть собственную цветовую палитру и шрифтовую схему на сайте.</span><span class="sxs-lookup"><span data-stu-id="ea3a8-176">The following code example shows how to deploy a custom color palette and font scheme to a site.</span></span>
    


```cs
  
// Get the SPColor file. Replace with the path to your SPColor file.
SPFile colorPaletteFile = Web.GetFile("path to .spcolor file");
if (null == colorPaletteFile || !colorPaletteFile.Exists)
{
    // TODO: handle the error.
    return;
}

// Get the SPFont file. Replace with the path to your SPFont file.
SPFile fontSchemeFile = Web.GetFile("path to .spfont file");
if (null == fontSchemeFile || !fontSchemeFile.Exists)
{
    // TODO: handle the error.
    return;
}

// Open an SPTheme with the two files. Replace NewTheme with the name for your theme.
// Note: If you have a background image, you can specify the following:
// SPTheme.Open("NewTheme", colorPaletteFile, fontSchemeFile, backgroundURI)
SPTheme theme = SPTheme.Open("NewTheme", colorPaletteFile, fontSchemeFile);


// Now apply your theme to the site.
// The themed CSS output files are stored in the Themed folder of the Theme Gallery of the root web
// of the site collection. To specify that the files should be stored in the _themes folder within the root 
// web, pass false to the ApplyTo method.
theme.ApplyTo(Web, true);
```


    > **Note:**
      > The  _shareGenerated_ parameter in the **ApplyTo** method specifies whether the themed files can be shared across sites in a site collection. In general, it is set to **true** for SharePoint Server and SharePoint Online sites and set to **false** for SharePoint Foundation sites. The _shareGenerated_ parameter must be set to **true** if you intend the themed files to be shared. For more information, see [ApplyTo(SPWeb, Boolean)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.ApplyTo.aspx) .

    When a user applies a theme in the **Change the look** wizard, the wizard also updates a theme named Current in the Composed Looks list and the design gallery. When you apply a theme programmatically, you have to update the Current theme manually. The following example shows how to update the Current theme.
    


```cs
  
SPList designGallery = Web.GetCatalog(SPListTemplateType.DesignCatalog);
if (null == designGallery)
{
    // TODO: Handle the error.
    return;
}

SPQuery q = new SPQuery();
q.RowLimit = 1;
q.Query = "<Where><Eq><FieldRef Name='DisplayOrder'/><Value Type='Number'>0</Value></Eq></Where>";
q.ViewFields = "<FieldRef Name='DisplayOrder'/>";
q.ViewFieldsOnly = true;

SPListItemCollection currentItems = designGallery.GetItems(q);

If (currentItems.Count == 1)
{
    // Remove the old Current item.
    currentItems[0].Delete();
}

SPListItem currentItem = designGallery.AddItem();

currentItem["Name"] = SPResource.GetString(CultureInfo.CurrentUICulture, Strings.DesignGalleryCurrentItemName);
currentItem["Title"] = SPResource.GetString(CultureInfo.CurrentUICulture, Strings.DesignGalleryCurrentItemName);

// Change this line if you want to specify a different master page.
currentItem["MasterPageUrl"] = Web.MasterUrl;

// Replace with the path to your SPColor file.
currentItem["ThemeUrl"] = "path to .spcolor file";

// Delete the following line if you do not have a background image. Otherwise, replace with the path to
// the background image.
currentItem["ImageUrl"] = "path to background image"; 

// Replace with the path to your SPFont file. Or, you can delete this line if you want to use
// the default font scheme of the selected master page.
currentItem["FontSchemeUrl"] = "path to .spfont file"; 

currentItem["DisplayOrder"] = 0;
currentItem.Update();

```


## <a name="additional-resources"></a><span data-ttu-id="ea3a8-177">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ea3a8-177">Additional resources</span></span>
<span data-ttu-id="ea3a8-178"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ea3a8-178"></span></span>


-  [<span data-ttu-id="ea3a8-179">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea3a8-179">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ea3a8-180">Цветовые палитры и шрифты в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea3a8-180">Color palettes and fonts in SharePoint</span></span>](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ea3a8-181">Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea3a8-181">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ea3a8-182">Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint</span><span class="sxs-lookup"><span data-stu-id="ea3a8-182">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  

