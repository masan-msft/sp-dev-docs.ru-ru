---
title: "Развертывание пользовательской темы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f703df24-8e56-4e6a-bc37-95acbb3c83e8
ms.openlocfilehash: 0f292d4d51cdce69b5828bdbd39c3514cc7ece27
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="deploy-a-custom-theme-in-sharepoint"></a>Развертывание пользовательской темы в SharePoint

Узнайте, как развертывать пользовательскую тему на сайте SharePoint, используя пользовательский интерфейс или приемник компонента. SharePoint содержит предустановленные темы. Кроме того, можно создавать пользовательские темы с помощью собственных дополнительных цветовых палитр, эталонных страниц и схем шрифтов. После отправки файлов в коллекцию тем и коллекцию эталонных страниц можно приступать к развертыванию темы на сайте с помощью пользовательского интерфейса или кода. Сведения о цветовых палитрах и схемах шрифтов см. в статье [Цветовые палитры и шрифты в SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
> [!NOTE]
> Информация в этой статье относится только к классическим сайтам SharePoint. Сведения для современных сайтов SharePoint см. в статье [Настройка тем для сайтов SharePoint](https://docs.microsoft.com/ru-RU/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview).


## <a name="core-concepts-to-know-to-deploy-a-theme"></a>Основные сведения о развертывании темы
<a name="core"> </a>

В таблице 1 перечислены статьи, содержащие основные понятия, которые нужно знать при развертывании тем.
  
    
    

**Таблица 1. Основные понятия, которые нужно знать при развертывании темы**


|**Название статьи**|**Описание**|
|:-----|:-----|
| [Общие сведения о темах для SharePoint](themes-overview-for-sharepoint.md) <br/> |Сведения о работе с темами в SharePoint.  <br/> |
| [События компонента](http://msdn.microsoft.com/ru-RU/library/ms469501.aspx) <br/> |Сведения о событиях компонента, позволяющих отслеживать события, возникающие при установке компонента в ферму серверов, и реагировать на них должным образом.  <br/> |
   

## <a name="upload-files-to-the-theme-gallery-and-the-master-page-gallery"></a>Отправка файлов в коллекцию тем и коллекцию эталонных страниц
<a name="section1"> </a>

Для создания пользовательских тем можно использовать собственные дополнительные цветовые палитры и схемы шрифтов. Отправьте их в коллекцию тем, чтобы получить к ним доступ при изменении дизайна во время работы с темами или при программном применении темы. Аналогично в коллекцию эталонных страниц можно отправить дополнительные эталонные страницы и соответствующие файлы предварительного просмотра для добавления дополнительных макетов сайта. Ниже описано, куда помещать эти файлы.
  
    
    

- **Коллекция эталонных страниц**. Содержит файлы эталонных страниц и соответствующие им файлы предварительного просмотра (файлы PREVIEW). Файл предварительного просмотра эталонной страницы требуется, если необходимо, чтобы эталонная страница была доступна в мастере **изменения оформления**. Файлы JavaScript и другие файлы для оформления также можно отправлять в коллекцию эталонных страниц.
    
    Чтобы получить доступ к коллекции эталонных страниц из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** выберите пункт **Главные страницы**. Вы также можете перейти непосредственно на сайт по ссылке http:// _ИмяСайта_/_catalogs/masterpage/.
    
  
- **Коллекция тем**. Содержит цветовые палитры и схемы шрифтов, доступные для работы с темами. SharePoint ищет доступные цветовые палитры и схемы шрифтов в папке **15**.
    
    Чтобы получить доступ к коллекции тем из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** выберите пункт **Темы**. Вы также можете перейти непосредственно на сайт по ссылке http:// _ИмяСемействаСайтов_/_catalogs/theme/15/.
    
  
- **Библиотека стилей**. Содержит пользовательские файлы CSS, необходимые при работе с темами. Чтобы перейти непосредственно к библиотеке стилей, замените  _ИмяСемействаСайтов_ и _язык_ в этом URL-адресе: http:// _ИмяСемействаСайтов_/Style Library/ _язык_/Themable/.
    
    > **Примечание.** Сохраняйте пользовательские CSS-файлы в папке Themable в библиотеке стилей, а не в коллекции эталонных страниц. Обработчик тем распознает только CSS-файлы, сохраненные в папке Themable в библиотеке стилей. 

> **Примечание.** Если для коллекции эталонных страниц и коллекции тем включено управление версиями, чтобы обработчик тем мог использовать файлы оформления, их необходимо опубликовать. 
  
    
    


## <a name="deploy-a-theme-by-using-the-user-interface"></a>Развертывание темы с помощью пользовательского интерфейса
<a name="section2"> </a>

Вариант оформления, или макет, включает в себя цветовую палитру, схему шрифтов, фоновое изображение и эталонную страницу, которые определяют внешний вид сайта. Список вариантов оформления содержит те из них, которые доступны в коллекции макетов. Чтобы создать макет, добавьте элемент в список вариантов оформления и укажите для него эталонную страницу, цветовую палитру, схему шрифтов и фоновое изображение.
  
    
    

> **Примечание.** Чтобы эталонная страница была доступна в коллекции макетов, требуется файл предварительного просмотра. 
  
    
    


### <a name="to-add-a-composed-look"></a>Добавление варианта оформления


1. Щелкните значок **Параметры**, затем выберите пункт **Параметры сайта**.
    
  
2. В разделе **Коллекция веб-дизайнера** щелкните ссылку **Варианты оформления**.
    
  
3. В списке **Варианты оформления** щелкните ссылку **Создайте элемент**.
    
  
4. В текстовом поле **Название** введите название макета.
    
  
5. В текстовом поле **Имя** введите имя макета, которое отображается в списке вариантов оформления и в коллекции макетов.
    
  
6. В текстовом поле **URL-адрес главной страницы** введите URL-адрес эталонной страницы (можно использовать относительный URL-адрес).
    
  
7. В текстовом поле **URL-адрес темы** введите URL-адрес цветовой палитры, т. е. URL-адрес, ведущий к файлу SPCOLOR (можно использовать относительный URL-адрес).
    
  
8. В текстовом поле **URL-адрес изображения** введите URL-адрес фонового изображения. Этот шаг необязательный. Можно использовать относительный URL-адрес.
    
  
9. В текстовом поле **URL-адрес шрифтовой схемы** введите URL-адрес схемы шрифтов, т. е. URL-адрес, ведущий к файлу SPFONT. Этот шаг необязательный. Можно использовать относительный URL-адрес.
    
  
10. В текстовом поле **Порядок отображения** укажите для макета порядковый номер, определяющий место макета в коллекции макетов.
    
  
11. Нажмите **Сохранить**.
    
    > **Примечание.** Если возникнет проблема со значениями, вариант оформления не будет добавлен в библиотеку макетов (без записи в файлах журнала). Если не удается добавить вариант оформления, это может быть вызвано одной из следующих причин: не удается найти файл, возникла проблема с форматом одного из файлов или SharePoint не может получить доступ к файлам. 
      > Теперь вы можете использовать библиотеку макетов, чтобы применить новый дизайн. Дополнительные сведения см. в статье [Выбор темы для сайта публикации](http://office.microsoft.com/ru-RU/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx).
  
    
    

## <a name="deploy-a-theme-by-using-code"></a>Развертывание темы с помощью кода
<a name="section3"> </a>

Вы можете выполнить развертывание темы, используя приемник компонента.
  
    
    

### <a name="to-deploy-a-theme-by-using-a-feature-receiver"></a>Для этого:


1. Создайте класс приемника компонента, который наследует классу  [SPFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.aspx) .
    
  
2. В методе  [FeatureActivated](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.FeatureActivated.aspx) создайте объект [SPTheme](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.aspx) , использующий нужную цветовую палитру и схему шрифтов, а затем примените тему к своему сайту.
    
    Ниже показано, как развернуть собственную цветовую палитру и шрифтовую схему на сайте.
    


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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Разработка макета сайта в SharePoint](develop-the-site-design-in-sharepoint.md)
    
  
-  [Цветовые палитры и шрифты в SharePoint](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  

