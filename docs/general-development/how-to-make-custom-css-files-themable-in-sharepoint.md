---
title: "Сделать настраиваемые CSS-файлы тем в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b8c82c77-c836-47f9-a11e-6c9c656d436b
ms.openlocfilehash: 6a2febe12c0420a75024937b3127504ca00592f6
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="make-custom-css-files-themable-in-sharepoint"></a>Сделать настраиваемые CSS-файлы тем в SharePoint

Узнайте, как добавьте разметку комментарий стилей CSS-файл, чтобы его можно использовать в модуле темы SharePoint.

## <a name="introduction-to-annotations"></a>Общие сведения о аннотаций
<a name="Intro"> </a>

Примечания, разметку специальные стиль комментариев, сообщают engine темы SharePoint как свойства темы в CSS-файл. При применении темы к сайту engine темы заменяет значения свойств CSS значения соответствующие темы. В SharePoint можно использовать примечания для изменения цвета, шрифта и фонового изображения. Можно также изменить цвет изображения. При использовании настраиваемого CSS-файлы, если вы хотите использовать их с помощью механизма темы SharePoint необходимо добавить эти аннотации CSS-файлы. Если применить тему для сайта, использующего настраиваемые CSS-файлы, и вы не добавили аннотации, свойства CSS не изменяются. Это может привести к сайтом с несоответствие разработки.
  
    
    
В этой статье описываются доступные заметки и регистрация CSS-файлы.
  
    
    
Дополнительные сведения о пользовательских тем можно [как: развернуть пользовательской темы в SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) и [как: создать файл предварительного просмотра главной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).
  
    
    

## <a name="add-annotations-to-custom-css-files"></a>Добавлять примечания к настраиваемые CSS-файлы
<a name="annotations"> </a>

Заметки сообщить engine темы SharePoint как свойства темы в CSS-файл. В этом разделе описываются доступные заметки и как их использовать.
  
    
    

### <a name="replacecolor-annotation"></a>ReplaceColor заметки
<a name="replaceColor"> </a>

Заметки **ReplaceColor** заменяет значение цвета цвет указанного темы. Его можно использовать со свойствами CSS, которые определяют значения цвета, такие как **color**, **background-color**, **border** и т. д.
  
    
    
Ниже приводится формат **ReplaceColor** заметки.
  
    
    



```

/* [ReplaceColor(themeColor:"ColorSlot"[, themeShade:"ShadeValue"][, themeTint:"TintValue"][, opacity:"OpacityValue"])] */

```

Замените _ColorSlot_ имя заметки разъем цвет для использования. Чтобы просмотреть список доступных разъемов разделу, посвященному [разъем сопоставление цветов](color-palettes-and-fonts-in-sharepoint.md#colorSlots) [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
    
Используйте параметр необязательно **themeShade**, если вы хотите затемнить цвет темы. Замените _ShadeValue_ числовое значение от 0,0 (без изменений) для версии 1.0 (самый темный).
  
    
    
Используйте параметр необязательно **themeTint**, если вы хотите осветлить цвет темы. Замените _TintValue_ числовое значение от 0,0 (без изменений) для версии 1.0 (очень светлый).
  
    
    
Используйте параметр необязательно **opacity**, если вы хотите задать непрозрачность цвет темы. Замените _OpacityValue_ числовое значение, указывающее, непрозрачность. Непрозрачность параметр в диапазоне от 0.0 (полностью прозрачный) до 1.0 (полная непрозрачность).
  
    
    
Ниже приведены примеры **ReplaceColor** заметки, используемых в CSS-файл.
  
    
    

-  `/* [ReplaceColor(themeColor:"BodyText")] */ color:#444;`
    
  
-  `/* [ReplaceColor(themeColor:"BackgroundOverlay",opacity:"0.5")] */ background-color:#fff;`
    
  
-  `/* [ReplaceColor(themeColor:"EmphasisBackground",themeTint:"0.05")] */ background-color:#f2faff;`
    
  

### <a name="replacefont-annotation"></a>ReplaceFont заметки
<a name="replaceFont"> </a>

Заметки **ReplaceFont** добавляет шрифт темы указанного списка доступных шрифтов. Его можно использовать со свойствами CSS **font** и **font-family**.
  
    
    
Ниже приводится формат **ReplaceFont** заметки.
  
    
    



```

/* [ReplaceFont(themeFont:"FontSlot")] */
```

Замените _FontSlot_ имя разъем шрифта для использования. Чтобы просмотреть список доступных шрифта разъемов разделу, посвященному [слотами шрифта](color-palettes-and-fonts-in-sharepoint.md#fontSlot) [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
    
Ниже показан пример **ReplaceFont** заметки. В этом примере Если разъем **body** шрифтов определяется как Courier в теме, Courier добавляются как первый элемент в списке доступных шрифтов в мастере **Choose the Look**.
  
    
    

-  `/* [ReplaceFont(themeFont:"body")] */ font-family:"Segoe UI","Segoe",Tahoma,Helvetica,Arial,sans-serif;`
    
  

### <a name="replacebgimage-annotation"></a>ReplaceBGImage заметки
<a name="replaceBGimage"> </a>

Заметки **ReplaceBGImage** заменяет фонового изображения в CSS-файл фонового изображения темы. Его можно использовать со свойствами CSS **background** и **background-image**.
  
    
    
Ниже приводится формат **ReplaceBGImage** заметки. Заметки **ReplaceBGImage** можно также использовать с фильтром **AlphaImageLoader** для поддержки более ранних версий Internet Explorer.
  
    
    



```
/* [ReplaceBGImage] */
```


### <a name="recolorimage-annotation"></a>RecolorImage заметки
<a name="replaceBGimage"> </a>

Заметки **RecolorImage** recolors указываемое изображение.
  
    
    
Следующие описывает формат **RecolorImage** заметки.
  
    
    



```
/* [RecolorImage(themeColor:"ColorSlot"[, method:["Tinting"|"Blending"|"Filling"]][, includeRectangle: {x:x-Setting,y:y-Setting,width:RegionWidth,height:RegionHeight})] */

```

Замените _ColorSlot_ имя заметки разъем цвет. Чтобы просмотреть список доступных разъемов разделу, посвященному [разъем сопоставление цветов](color-palettes-and-fonts-in-sharepoint.md#colorSlots) [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
    
Используйте параметр необязательно **method**, если вы хотите указать метод recoloring.
  
    
    
Используйте параметр необязательно **includeRectangle**, если вы хотите изменить цвет для отдельного региона изображения. Замените _x-Setting_,  _y-Setting_,  _RegionWidth_и  _RegionHeight_ оси x, оси y, ширину и высоту области, которую требуется изменить цвет.
  
    
    
Ниже приведены примеры **RecolorImage** заметки, используемых в CSS-файл.
  
    
    

-  `/* [RecolorImage(themeColor:"SubtleBodyText",method:"Tinting")] */ background-image:url("/_layouts/15/images/tabtitlerowbottombg.png?rev=23");`
    
  
-  `/* [RecolorImage(themeColor:"BodyText",method:"Filling",includeRectangle:{x:161,y:178,width:16;height:16})] */ background:url("/_layouts/15/images/spcommon.png?rev=23") no-repeat -161px -178px;`
    
  

## <a name="upload-the-css-file-to-the-themable-folder-in-the-style-library"></a>Отправка CSS-файл в папку Themable в библиотеку стилей
<a name="uploadCSS"> </a>

Размещение настраиваемого CSS-файлы в папку Themable в библиотеку стилей (не Themable папке в коллекции главных страниц). Обработчик тем распознает только CSS-файлы, сохраненные в папке Themable в библиотеке стилей. Для сайтов публикации автоматически создается папка Themable. В противном случае можно создать папку Themable в правильном месте (http:// _SiteCollectionName_Style Library / __языка/Themable /).
  
    
    

> **Примечание:** Имя папки _языка_ должно быть в формате 4-значного _Яя сс_ для идентификации языка и региональных параметров, соответственно. Например, en-us или ar-sa. Для получения дополнительных сведений см [идентификаторы языков и значения идентификаторов OptionState в Office 2013](http://technet.microsoft.com/en-us/library/cc179219.aspx). 
  
    
    

CSS-файлы должны вернули и опубликован. Если CSS-файлы изменяются, необходимо повторно применить темы для внесенных изменений.
  
    
    

## <a name="register-the-css-file"></a>Регистрация CSS-файла
<a name="registerCSS"> </a>

Необходимо зарегистрировать CSS-файла в главную страницу, прежде чем CSS-файла можно использовать ядром темы. Если применить тему к сайту, направляет главную страницу в CSS-файл. Регистрация CSS-файла, добавьте элемент **<SharePoint:CssRegistration>** в элемент **<head>** главной страницы. Ниже показан формат элемента **<SharePoint:CssRegistration>**.
  
    
    

```HTML

<SharePoint:CssRegistration Name="CSSFileLocation" runat="server" />
```

Замените  _CSSFileLocation_ расположение CSS-файла.
  
    
    
Ниже приведен пример элемента **<SharePoint:CssRegistration>**.
  
    
    



```HTML
<head>
…
<SharePoint:CssRegistration Name="<%$SPUrl:~SiteCollection/Style Library/~language/Themable/MyCustomFile.css%>" runat="server" />
</head>
```


> **Примечание:** Маркер **%$SPUrl** не может использоваться в SharePoint Foundation 2013. Необходимо использовать URL-адрес, чтобы указать расположение CSS-файла.
  
    
    


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="addresources"> </a>


-  [Общие сведения о темах для SharePoint](themes-overview-for-sharepoint.md)
    
  
-  [Инструкции. Развертывание пользовательской темы в SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [Обновление пользовательских тем и CSS для SharePoint](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [Цветовые палитры и шрифты в SharePoint](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [Фирменная символика и конструкция возможности дизайнер SharePoint](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

