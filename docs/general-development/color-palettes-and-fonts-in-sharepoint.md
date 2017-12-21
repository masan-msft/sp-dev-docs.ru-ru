---
title: "Цветовые палитры и шрифты в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c17d375b-151f-48ae-ac32-f2ce9e68d63f
ms.openlocfilehash: 0ae750c42451986a7f3bdc50111759a69e8a84db
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="color-palettes-and-fonts-in-sharepoint"></a><span data-ttu-id="ac73d-102">Цветовые палитры и шрифты в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-102">Color palettes and fonts in SharePoint</span></span>
<span data-ttu-id="ac73d-103">Воспользуйтесь этим справочником, чтобы определить цветовую палитру или схему шрифтов, которые используются на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac73d-103">Use this reference to define the color palette or font scheme that is used in a SharePoint site.</span></span>
## <a name="color-palettes"></a><span data-ttu-id="ac73d-104">Цветовые палитры</span><span class="sxs-lookup"><span data-stu-id="ac73d-104">Color palettes</span></span>
<span data-ttu-id="ac73d-105"><a name="color"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-105"><a name="color"> </a></span></span>

<span data-ttu-id="ac73d-p101">Цветовая палитра - сочетание цветов, использующихся на сайте SharePoint. Она определяется в файле цветовой палитры. Цветовые слоты также используются файлом предварительного просмотра эталонной страницы для создания изображений эскиза и для предварительного просмотра изображений. Ниже описывается структура файла цветовой палитры и предварительного просмотра эталонной страницы:</span><span class="sxs-lookup"><span data-stu-id="ac73d-p101">A color palette is the combination of colors that are used in a SharePoint site. The color palette for a SharePoint site is defined in a color palette file. Color slots are also used by the master page preview file to generate thumbnail and preview images of a site. The following describes the structure of the color palette file and the master page preview file:</span></span>
  
    
    

- <span data-ttu-id="ac73d-110">**Файл цветовой палитры (файл SPCOLOR)**</span><span class="sxs-lookup"><span data-stu-id="ac73d-110">**Color palette file (.spcolor)**</span></span>
    
    <span data-ttu-id="ac73d-p102">Эти файлы используются в мастере **изменения оформления**, который позволяет пользователям изменять внешний вид сайта с помощью тем пользовательского интерфейса SharePoint. По умолчанию вместе с SharePoint устанавливаются 32 файла цветовой палитры. Кроме того, предусмотрена возможность создания дополнительных файлов. Ниже приводится пример формата файла цветовой палитры.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p102">Color palette files are used in the **Change the look** wizard, which enables users to change the look and feel of their site by using the SharePoint themes user interface. By default, 32 color palette files are installed with SharePoint. You can also create additional color palette files. The following example shows the format of a color palette file.</span></span>
    

```xml  
<s:colorPalette isInverted="InvertedSetting" previewSlot1="Slot1" previewSlot2="Slot2" previewSlot3="Slot3" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:color name="ColorSlot" value="Color" />
    <!--additional color slots-->
</s:colorPalette>
```


  <span data-ttu-id="ac73d-115">В файле цветовой палитры заменяются следующие заполнители:</span><span class="sxs-lookup"><span data-stu-id="ac73d-115">In a color palette file, the following placeholders are replaced:</span></span>
    
-  <span data-ttu-id="ac73d-p103">_InvertedSetting_ - это логическое значение, в котором значение **true** соответствует цветовой палитре со светлым текстом на темном фоне. Тогда как значение **false** соответствует цветовой палитре с темным текстом на светлом фоне.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p103">_InvertedSetting_ is a Boolean value. **true** if the color palette is generally light text on a dark background. **false** if the color palette is generally dark text on a light background.</span></span>
    
  
-  <span data-ttu-id="ac73d-119">_Slot1_ - имя заметки цветового слота, которое используется в качестве первого блока значка палитры в средстве выбора цветовой палитры при работе с темами.</span><span class="sxs-lookup"><span data-stu-id="ac73d-119">_Slot1_ is the annotation name of the color slot to use as the first block of the palette icon in the color palette picker of the theming experience.</span></span>
    
  
-  <span data-ttu-id="ac73d-120">_Slot2_ - имя заметки цветового слота, которое используется в качестве второго блока значка палитры в средстве выбора цветовой палитры при работе с темами.</span><span class="sxs-lookup"><span data-stu-id="ac73d-120">_Slot2_ is the annotation name of the color slot to use as the second block of the palette icon in the color palette picker of the theming experience.</span></span>
    
  
-  <span data-ttu-id="ac73d-121">_Slot3_ - имя заметки цветового слота, которое используется в качестве третьего блока значка палитры в средстве выбора палитры при работе с темами.</span><span class="sxs-lookup"><span data-stu-id="ac73d-121">_Slot3_ is the annotation name of the color slot to use as the third block of the palette icon in the color palette picker of the theming experience.</span></span>
    
  
-  <span data-ttu-id="ac73d-122">_ColorSlot_ - имя заметки определяемого цветового слота, например "НазваниеСайта".</span><span class="sxs-lookup"><span data-stu-id="ac73d-122">_ColorSlot_ is the annotation name of the color slot that you are defining (for example, SiteTitle).</span></span>
    
  
-  <span data-ttu-id="ac73d-p104">_Color_ - это шестнадцатеричное значение цвета, используемое для указанного цветового слота. Оно может быть представлено в виде 6 (RRGGBB) или 8 цифр (AARRGGBB). Если шестнадцатеричное значение представлено 8 цифрами, первые две цифры обозначают уровень прозрачности цвета в диапазоне 00-FF, что соответствует значениям от 0 до 255. Если оно представлено 6 цифрами, по умолчанию установлен уровень непрозрачности со значением 100 % или FF.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p104">_Color_ is the hexadecimal value of the color to use for the specified color slot. This may be in 6 digits (RRGGBB) or 8 digits (AARRGGBB). If the hexadecimal value is 8 digits, the first two digits represent the opacity level (00-FF, which maps to 0-255). If the hexadecimal value is 6 digits, the default opacity is 100% or FF.</span></span>
    
  

  <span data-ttu-id="ac73d-p105">Файлы цветовой палитры расположены в коллекции тем корневого сайта (в папке **15** http:// _ИмяСемействаСайтов_/_catalogs/theme/15/ семейства веб-сайтов). Чтобы получить доступ к коллекции тем из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** выберите элемент **Темы**, а затем выберите папку **15**.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p105">The color palette files are located in the Theme Gallery of the root site, in the site collection in the **15** folder (http:// _SiteCollectionName_/_catalogs/theme/15/). To access the Theme Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, select **Themes**, and then select **15**.</span></span>
    
  
- <span data-ttu-id="ac73d-129">**Файл предварительного просмотра эталонной страницы (файл PREVIEW)**</span><span class="sxs-lookup"><span data-stu-id="ac73d-129">**Master page preview file (.preview)**</span></span>
    
  <span data-ttu-id="ac73d-p106">Файлы предварительного просмотра эталонной страницы используются для создания эскизов и изображений предварительного просмотра при работе с мастером **изменения оформления**. Чтобы эталонную страницу можно было использовать в мастере **изменения оформления**, для нее обязательно создается соответствующий файл предварительного просмотра. Файл предварительного просмотра - это файл со специальным форматированием, в котором есть разделы для цветовой палитры и схемы цветов по умолчанию, а также для CSS и HTML с маркерами. Он использует маркеры строк для получения значений цветовых слотов, имен шрифтов и локализованных строк пользовательского интерфейса. Ниже приведен пример использования цветовых слотов в файле предварительного просмотра эталонной страницы.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p106">Master page preview files are used to generate thumbnail images and preview images when you use the **Change the look** wizard. A master page must have a corresponding preview file to be used in the **Change the look** wizard. A preview file is a specially formatted file that has sections for the default color palette, default font scheme, tokenized CSS, and tokenized HTML. It uses string tokens to get the value of color slots, font names, and localized UI strings. The following example shows color slots being used in the master page preview file.</span></span>
    


```HTML
  
[ID] #dgp-pageContainer
{
    background-color: [T_THEME_COLOR_PAGEBACKGROUND];
    color: [T_THEME_COLOR_BODYTEXT];
    width: 100%;
    height:100%;     
    background-image: url('[T_IMAGE]');       
    background-size: cover;
    font-family: [T_BODY_FONT];   
}
```


  <span data-ttu-id="ac73d-135">Дополнительные сведения см. в статье [Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="ac73d-135">For more information, see  [How to: Create a master page preview file in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)</span></span>
    
  

> <span data-ttu-id="ac73d-136">**Совет.** Вы можете использовать цветовую палитру SharePoint при создании вариантов оформления для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac73d-136">**Tip:** You can use the SharePoint color palette tool to help you create SharePoint designs.</span></span> <span data-ttu-id="ac73d-137">Вы можете [скачать цветовую палитру SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=38182) из Центра загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ac73d-137">You can  [download the SharePoint color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) from the Microsoft Download Center.</span></span>
  
    
    


### <a name="color-slot-mapping"></a><span data-ttu-id="ac73d-138">Сопоставление цветовых слотов</span><span class="sxs-lookup"><span data-stu-id="ac73d-138">Color slot mapping</span></span>
<span data-ttu-id="ac73d-139"><a name="colorSlots"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-139"><a name="colorSlots"> </a></span></span>

<span data-ttu-id="ac73d-140">В таблице 1 описаны доступные цветовые слоты и область их применения на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ac73d-140">Table 1 describes the color slots that are available and where color slots are used in a SharePoint site.</span></span>
  
> [!NOTE]
> <span data-ttu-id="ac73d-141">Что касается элементов навигации, под нажатием подразумевается щелчок или касание, под выбором — переход пользователя на страницу. Далее приведена сводка по обычной последовательности действий и местам использования цветов, применяемым к ссылке на каждом этапе. Основной текст ссылки: HeaderNavigationText. Пользователь наводит указатель на ссылку: HeaderNavigationHoverText. Пользователь нажимает или выбирает ссылку: HeaderNavigationPressedText. Пользователь переходит на выбранную страницу.</span><span class="sxs-lookup"><span data-stu-id="ac73d-141">Note: When discussing navigation items,pressed applies to when a user clicks or touches a navigation item.Selected applies to when a user is navigated to the page.>  The following summarizes a normal flow of actions and the color slot that applies to the navigation item link at each step:>  The base text of a navigation item link: HeaderNavigationText>  A user hovers the cursor over the navigation item link: HeaderNavigationHoverText>  A user clicks, touches, or chooses the navigation item link: HeaderNavigationPressedText>  The user is navigated to the chosen page.</span></span> <span data-ttu-id="ac73d-142">Место использования цвета, применяемое к элементу навигации для страницы, которую просматривает пользователь: HeaderNavigationSelectedText.</span><span class="sxs-lookup"><span data-stu-id="ac73d-142">The color slot that applies to the navigation item for the page the user is now on: HeaderNavigationSelectedText</span></span>
  
    
    


<span data-ttu-id="ac73d-143">**Таблица 1. Цветовые слоты**</span><span class="sxs-lookup"><span data-stu-id="ac73d-143">**Table 1. Color slots**</span></span>


|<span data-ttu-id="ac73d-144">**Имя заметки**</span><span class="sxs-lookup"><span data-stu-id="ac73d-144">**Annotation Name**</span></span>|<span data-ttu-id="ac73d-145">**Применение цвета в пользовательском интерфейсе**</span><span class="sxs-lookup"><span data-stu-id="ac73d-145">**Where the Color Is Used in the UI**</span></span>|<span data-ttu-id="ac73d-146">**Имя маркера**</span><span class="sxs-lookup"><span data-stu-id="ac73d-146">**Token Name**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="ac73d-147">BodyText</span><span class="sxs-lookup"><span data-stu-id="ac73d-147">BodyText</span></span>  <br/> |<span data-ttu-id="ac73d-148">Обычный текст</span><span class="sxs-lookup"><span data-stu-id="ac73d-148">Normal body text.</span></span>  <br/> |<span data-ttu-id="ac73d-149">[T_THEME_COLOR_BODYTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-149">[T_THEME_COLOR_BODYTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-150">SubtleBodyText</span><span class="sxs-lookup"><span data-stu-id="ac73d-150">SubtleBodyText</span></span>  <br/> |<span data-ttu-id="ac73d-p109">Основной текст, который по цвету должен быть светлее обычного, например текст метаданных.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p109">Body text that must be lighter than normal. An example is metadata text.</span></span>  <br/> |<span data-ttu-id="ac73d-153">[T_THEME_COLOR_SUBTLEBODYTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-153">[T_THEME_COLOR_SUBTLEBODYTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-154">StrongBodyText</span><span class="sxs-lookup"><span data-stu-id="ac73d-154">StrongBodyText</span></span>  <br/> |<span data-ttu-id="ac73d-155">Выделение более насыщенным цветом основного текста, который должен отличаться от обычного.</span><span class="sxs-lookup"><span data-stu-id="ac73d-155">Body text color for text that must stand out from normal body text.</span></span>  <br/> |<span data-ttu-id="ac73d-156">[T_THEME_COLOR_STRONGBODYTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-156">[T_THEME_COLOR_STRONGBODYTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-157">DisabledText</span><span class="sxs-lookup"><span data-stu-id="ac73d-157">DisabledText</span></span>  <br/> |<span data-ttu-id="ac73d-p110">Отключенный текст, например элементы меню, к которым нет доступа.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p110">Disabled text. For example, unavailable items in menus.</span></span>  <br/> |<span data-ttu-id="ac73d-160">[T_THEME_COLOR_DISABLEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-160">[T_THEME_COLOR_DISABLEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-161">SiteTitle</span><span class="sxs-lookup"><span data-stu-id="ac73d-161">SiteTitle</span></span>  <br/> |<span data-ttu-id="ac73d-162">Цвет текста заголовка.</span><span class="sxs-lookup"><span data-stu-id="ac73d-162">The text color of the page title.</span></span>  <br/> |<span data-ttu-id="ac73d-163">[T_THEME_COLOR_SITETITLE]</span><span class="sxs-lookup"><span data-stu-id="ac73d-163">[T_THEME_COLOR_SITETITLE]</span></span>  <br/> |
|<span data-ttu-id="ac73d-164">WebPartHeading</span><span class="sxs-lookup"><span data-stu-id="ac73d-164">WebPartHeading</span></span>  <br/> |<span data-ttu-id="ac73d-165">Цвет текста заголовков веб-частей.</span><span class="sxs-lookup"><span data-stu-id="ac73d-165">Text color for Web Part headings.</span></span>  <br/> |<span data-ttu-id="ac73d-166">[T_THEME_COLOR_WEBPARTHEADING]</span><span class="sxs-lookup"><span data-stu-id="ac73d-166">[T_THEME_COLOR_WEBPARTHEADING]</span></span>  <br/> |
|<span data-ttu-id="ac73d-167">ErrorText</span><span class="sxs-lookup"><span data-stu-id="ac73d-167">ErrorText</span></span>  <br/> |<span data-ttu-id="ac73d-168">Основной цвет, который при необходимости используется для текста сообщения об ошибке, границ и фона.</span><span class="sxs-lookup"><span data-stu-id="ac73d-168">The main error color that is used for error text, borders, and backgrounds, as needed.</span></span>  <br/> |<span data-ttu-id="ac73d-169">[T_THEME_COLOR_ERRORTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-169">[T_THEME_COLOR_ERRORTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-170">AccentText</span><span class="sxs-lookup"><span data-stu-id="ac73d-170">AccentText</span></span>  <br/> |<span data-ttu-id="ac73d-171">Цвет, который применяется для контрастного основного текста.</span><span class="sxs-lookup"><span data-stu-id="ac73d-171">Text color for accented body text.</span></span>  <br/> |<span data-ttu-id="ac73d-172">[T_THEME_COLOR_ACCENTTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-172">[T_THEME_COLOR_ACCENTTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-173">SearchURL</span><span class="sxs-lookup"><span data-stu-id="ac73d-173">SearchURL</span></span>  <br/> |<span data-ttu-id="ac73d-p111">Цвет URL-адреса в результатах поиска. Он также используется для выделения новых элементов или уведомлений об успешной доставке.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p111">Text color for the URL found in search results. Also used to highlight new items or successful status notifications.</span></span>  <br/> |<span data-ttu-id="ac73d-176">[T_THEME_COLOR_SEARCHURL]</span><span class="sxs-lookup"><span data-stu-id="ac73d-176">[T_THEME_COLOR_SEARCHURL]</span></span>  <br/> |
|<span data-ttu-id="ac73d-177">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="ac73d-177">Hyperlink</span></span>  <br/> |<span data-ttu-id="ac73d-178">Цвет текста гиперссылок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-178">Text color for hyperlinks.</span></span>  <br/> |<span data-ttu-id="ac73d-179">[T_THEME_COLOR_HYPERLINK]</span><span class="sxs-lookup"><span data-stu-id="ac73d-179">[T_THEME_COLOR_HYPERLINK]</span></span>  <br/> |
|<span data-ttu-id="ac73d-180">HyperlinkFollowed</span><span class="sxs-lookup"><span data-stu-id="ac73d-180">HyperlinkFollowed</span></span>  <br/> |<span data-ttu-id="ac73d-181">Цвет текста просмотренных гиперссылок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-181">Text color for followed hyperlinks.</span></span>  <br/> |<span data-ttu-id="ac73d-182">[T_THEME_COLOR_HYPERLINKFOLLOWED]</span><span class="sxs-lookup"><span data-stu-id="ac73d-182">[T_THEME_COLOR_HYPERLINKFOLLOWED]</span></span>  <br/> |
|<span data-ttu-id="ac73d-183">HyperlinkActive</span><span class="sxs-lookup"><span data-stu-id="ac73d-183">HyperlinkActive</span></span>  <br/> |<span data-ttu-id="ac73d-184">Цвет гиперссылки при нажатии.</span><span class="sxs-lookup"><span data-stu-id="ac73d-184">Hyperlink color when pressed.</span></span>  <br/> |<span data-ttu-id="ac73d-185">[T_THEME_COLOR_HYPERLINKACTIVE]</span><span class="sxs-lookup"><span data-stu-id="ac73d-185">[T_THEME_COLOR_HYPERLINKACTIVE]</span></span>  <br/> |
|<span data-ttu-id="ac73d-186">CommandLinks</span><span class="sxs-lookup"><span data-stu-id="ac73d-186">CommandLinks</span></span>  <br/> |<span data-ttu-id="ac73d-187">Большие ссылки на команды, которые из-за своего размера должны быть немного светлее основного текста.</span><span class="sxs-lookup"><span data-stu-id="ac73d-187">Large command links that must be a bit lighter than body text because of their size.</span></span>  <br/> |<span data-ttu-id="ac73d-188">[T_THEME_COLOR_COMMANDLINKS]</span><span class="sxs-lookup"><span data-stu-id="ac73d-188">[T_THEME_COLOR_COMMANDLINKS]</span></span>  <br/> |
|<span data-ttu-id="ac73d-189">CommandLinksSecondary</span><span class="sxs-lookup"><span data-stu-id="ac73d-189">CommandLinksSecondary</span></span>  <br/> |<span data-ttu-id="ac73d-190">Цвет текста более коротких ссылок на команды, который должен быть насыщеннее, чтобы выделяться на фоне остального текста.</span><span class="sxs-lookup"><span data-stu-id="ac73d-190">Command link color for links that are smaller, and therefore have a stronger color to stand out.</span></span>  <br/> |<span data-ttu-id="ac73d-191">[T_THEME_COLOR_COMMANDLINKSSECONDARY]</span><span class="sxs-lookup"><span data-stu-id="ac73d-191">[T_THEME_COLOR_COMMANDLINKSSECONDARY]</span></span>  <br/> |
|<span data-ttu-id="ac73d-192">CommandLinksHover</span><span class="sxs-lookup"><span data-stu-id="ac73d-192">CommandLinksHover</span></span>  <br/> |<span data-ttu-id="ac73d-193">Цвет ссылки на команду при наведении на нее курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-193">Command link color on hover.</span></span>  <br/> |<span data-ttu-id="ac73d-194">[T_THEME_COLOR_COMMANDLINKSHOVER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-194">[T_THEME_COLOR_COMMANDLINKSHOVER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-195">CommandLinksPressed</span><span class="sxs-lookup"><span data-stu-id="ac73d-195">CommandLinksPressed</span></span>  <br/> |<span data-ttu-id="ac73d-196">Цвет ссылки на команду при нажатии на нее.</span><span class="sxs-lookup"><span data-stu-id="ac73d-196">Command link color when pressed.</span></span>  <br/> |<span data-ttu-id="ac73d-197">[T_THEME_COLOR_COMMANDLINKSPRESSED]</span><span class="sxs-lookup"><span data-stu-id="ac73d-197">[T_THEME_COLOR_COMMANDLINKSPRESSED]</span></span>  <br/> |
|<span data-ttu-id="ac73d-198">CommandLinksDisabled</span><span class="sxs-lookup"><span data-stu-id="ac73d-198">CommandLinksDisabled</span></span>  <br/> |<span data-ttu-id="ac73d-199">Цвет отключенной ссылки на команду.</span><span class="sxs-lookup"><span data-stu-id="ac73d-199">Command link color when command link is disabled.</span></span>  <br/> |<span data-ttu-id="ac73d-200">[T_THEME_COLOR_COMMANDLINKSDISABLED]</span><span class="sxs-lookup"><span data-stu-id="ac73d-200">[T_THEME_COLOR_COMMANDLINKSDISABLED]</span></span>  <br/> |
|<span data-ttu-id="ac73d-201">BackgroundOverlay</span><span class="sxs-lookup"><span data-stu-id="ac73d-201">BackgroundOverlay</span></span>  <br/> |<span data-ttu-id="ac73d-202">Основной цвет фона, видимый между необязательным фоновым изображением и содержимым страницы.</span><span class="sxs-lookup"><span data-stu-id="ac73d-202">The main background color that is visible between the optional background image and the page content.</span></span>  <br/> |<span data-ttu-id="ac73d-203">[T_THEME_COLOR_BACKGROUNDOVERLAY]</span><span class="sxs-lookup"><span data-stu-id="ac73d-203">[T_THEME_COLOR_BACKGROUNDOVERLAY]</span></span>  <br/> |
|<span data-ttu-id="ac73d-204">DisabledBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-204">DisabledBackground</span></span>  <br/> |<span data-ttu-id="ac73d-205">Фон для отключенных элементов, таких как элементы управления браузером, например поле ввода или поле выбора, за исключением кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-205">Background for disabled elements such as browser controls, for example, input box or select box (except buttons).</span></span>  <br/> |<span data-ttu-id="ac73d-206">[T_THEME_COLOR_DISABLEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-206">[T_THEME_COLOR_DISABLEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-207">PageBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-207">PageBackground</span></span>  <br/> |<span data-ttu-id="ac73d-p112">Цвет фона страницы, который виден за необязательным фоновым изображением.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p112">The background color of the page. Appears behind the optional background image.</span></span>  <br/> |<span data-ttu-id="ac73d-210">[T_THEME_COLOR_PAGEBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-210">[T_THEME_COLOR_PAGEBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-211">HeaderBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-211">HeaderBackground</span></span>  <br/> |<span data-ttu-id="ac73d-212">Цвет фона области верхнего колонтитула страницы.</span><span class="sxs-lookup"><span data-stu-id="ac73d-212">The background color for the header area of the page.</span></span>  <br/> |<span data-ttu-id="ac73d-213">[T_THEME_COLOR_HEADERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-213">[T_THEME_COLOR_HEADERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-214">FooterBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-214">FooterBackground</span></span>  <br/> |<span data-ttu-id="ac73d-215">Цвет фона области нижнего колонтитула страницы.</span><span class="sxs-lookup"><span data-stu-id="ac73d-215">The background color for the footer area of the page.</span></span>  <br/> |<span data-ttu-id="ac73d-216">[T_THEME_COLOR_FOOTERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-216">[T_THEME_COLOR_FOOTERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-217">SelectionBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-217">SelectionBackground</span></span>  <br/> |<span data-ttu-id="ac73d-218">Цвет фона выбранных элементов списка и пунктов раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="ac73d-218">The background color for selected list items and drop-down menu items.</span></span>  <br/> |<span data-ttu-id="ac73d-219">[T_THEME_COLOR_SELECTIONBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-219">[T_THEME_COLOR_SELECTIONBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-220">HoverBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-220">HoverBackground</span></span>  <br/> |<span data-ttu-id="ac73d-221">Цвет фона элементов списка и пунктов раскрывающегося меню при наведении на них курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-221">The background color for list items and drop-down menu items on hover.</span></span>  <br/> |<span data-ttu-id="ac73d-222">[T_THEME_COLOR_HOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-222">[T_THEME_COLOR_HOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-223">RowAccent</span><span class="sxs-lookup"><span data-stu-id="ac73d-223">RowAccent</span></span>  <br/> |<span data-ttu-id="ac73d-224">Контрастная левая граница выбранных элементов списка.</span><span class="sxs-lookup"><span data-stu-id="ac73d-224">The accented left border on selected list items.</span></span>  <br/> |<span data-ttu-id="ac73d-225">[T_THEME_COLOR_ROWACCENT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-225">[T_THEME_COLOR_ROWACCENT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-226">StrongLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-226">StrongLines</span></span>  <br/> |<span data-ttu-id="ac73d-227">Границы элементов управления браузером при наведении на них курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-227">Borders for browser controls on hover.</span></span>  <br/> |<span data-ttu-id="ac73d-228">[T_THEME_COLOR_STRONGLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-228">[T_THEME_COLOR_STRONGLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-229">Lines</span><span class="sxs-lookup"><span data-stu-id="ac73d-229">Lines</span></span>  <br/> |<span data-ttu-id="ac73d-230">Границы элементов управления браузером.</span><span class="sxs-lookup"><span data-stu-id="ac73d-230">Borders for browser controls.</span></span>  <br/> |<span data-ttu-id="ac73d-231">[T_THEME_COLOR_LINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-231">[T_THEME_COLOR_LINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-232">SubtleLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-232">SubtleLines</span></span>  <br/> |<span data-ttu-id="ac73d-p113">Слабо выделенный цвет границы, например линии сетки для встроенной правки.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p113">Subtle border color. For example, gridlines for inline editing.</span></span>  <br/> |<span data-ttu-id="ac73d-235">[T_THEME_COLOR_SUBTLELINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-235">[T_THEME_COLOR_SUBTLELINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-236">DisabledLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-236">DisabledLines</span></span>  <br/> |<span data-ttu-id="ac73d-237">Цвет границ для элементов управления браузером, таких как поля ввода и поля выбора.</span><span class="sxs-lookup"><span data-stu-id="ac73d-237">Border color for disabled browser controls such as input boxes and select boxes.</span></span>  <br/> |<span data-ttu-id="ac73d-238">[T_THEME_COLOR_DISABLEDLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-238">[T_THEME_COLOR_DISABLEDLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-239">AccentLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-239">AccentLines</span></span>  <br/> |<span data-ttu-id="ac73d-240">Цвет границы фокуса для выбранных элементов управления браузером.</span><span class="sxs-lookup"><span data-stu-id="ac73d-240">Focused border color for selected browser controls.</span></span>  <br/> |<span data-ttu-id="ac73d-241">[T_THEME_COLOR_ACCENTLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-241">[T_THEME_COLOR_ACCENTLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-242">DialogBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-242">DialogBorder</span></span>  <br/> |<span data-ttu-id="ac73d-243">Цвет границы диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ac73d-243">Dialog box border color.</span></span>  <br/> |<span data-ttu-id="ac73d-244">[T_THEME_COLOR_DIALOGBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-244">[T_THEME_COLOR_DIALOGBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-245">Навигация</span><span class="sxs-lookup"><span data-stu-id="ac73d-245">Navigation</span></span>  <br/> |<span data-ttu-id="ac73d-246">Цвет текста элементов горизонтальной и вертикальной панелей навигации.</span><span class="sxs-lookup"><span data-stu-id="ac73d-246">Text color for horizontal and vertical navigation items.</span></span>  <br/> |<span data-ttu-id="ac73d-247">[T_THEME_COLOR_NAVIGATION]</span><span class="sxs-lookup"><span data-stu-id="ac73d-247">[T_THEME_COLOR_NAVIGATION]</span></span>  <br/> |
|<span data-ttu-id="ac73d-248">NavigationAccent</span><span class="sxs-lookup"><span data-stu-id="ac73d-248">NavigationAccent</span></span>  <br/> |<span data-ttu-id="ac73d-249">Цвет текста элемента горизонтальной панели навигации.</span><span class="sxs-lookup"><span data-stu-id="ac73d-249">Text color for a selected horizontal navigation item.</span></span>  <br/> |<span data-ttu-id="ac73d-250">[T_THEME_COLOR_NAVIGATIONACCENT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-250">[T_THEME_COLOR_NAVIGATIONACCENT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-251">NavigationHover</span><span class="sxs-lookup"><span data-stu-id="ac73d-251">NavigationHover</span></span>  <br/> |<span data-ttu-id="ac73d-p114">Цвет текста панели навигации при наведении на него курсора мыши. Применяется к верхней панели навигации и панели быстрого запуска в горизонтальном режиме.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p114">Navigation text color on hover. Applies to top navigation, and to Quick Launch in horizontal mode.</span></span>  <br/> |<span data-ttu-id="ac73d-254">[T_THEME_COLOR_NAVIGATIONHOVER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-254">[T_THEME_COLOR_NAVIGATIONHOVER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-255">NavigationPressed</span><span class="sxs-lookup"><span data-stu-id="ac73d-255">NavigationPressed</span></span>  <br/> |<span data-ttu-id="ac73d-p115">Цвет текста элемента панели навигации при его нажатии. Применяется к верхней панели навигации и панели быстрого запуска в горизонтальном режиме.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p115">Text color of navigation item when pressed. Applies to top navigation, and to Quick Launch in horizontal mode.</span></span>  <br/> |<span data-ttu-id="ac73d-258">[T_THEME_COLOR_NAVIGATIONPRESSED]</span><span class="sxs-lookup"><span data-stu-id="ac73d-258">[T_THEME_COLOR_NAVIGATIONPRESSED]</span></span>  <br/> |
|<span data-ttu-id="ac73d-259">NavigationHoverBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-259">NavigationHoverBackground</span></span>  <br/> |<span data-ttu-id="ac73d-260">Цвет фона элементов панели быстрого доступа в вертикальном режиме при наведении курсора мыши на элемент панели навигации.</span><span class="sxs-lookup"><span data-stu-id="ac73d-260">Background color of Quick Launch items in vertical mode on hover over the navigation item.</span></span>  <br/> |<span data-ttu-id="ac73d-261">[T_THEME_COLOR_NAVIGATIONHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-261">[T_THEME_COLOR_NAVIGATIONHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-262">NavigationSelectedBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-262">NavigationSelectedBackground</span></span>  <br/> |<span data-ttu-id="ac73d-263">Цвет фона элементов панели быстрого доступа в вертикальном режиме после выбора элемента панели навигации.</span><span class="sxs-lookup"><span data-stu-id="ac73d-263">Background color of Quick Launch items in vertical mode after the navigation item is selected.</span></span>  <br/> |<span data-ttu-id="ac73d-264">[T_THEME_COLOR_NAVIGATIONSELECTEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-264">[T_THEME_COLOR_NAVIGATIONSELECTEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-265">EmphasisText</span><span class="sxs-lookup"><span data-stu-id="ac73d-265">EmphasisText</span></span>  <br/> |<span data-ttu-id="ac73d-266">Цвет текста, появляющегося поверх акцентного фона.</span><span class="sxs-lookup"><span data-stu-id="ac73d-266">The text color that appears on top of emphasis background.</span></span>  <br/> |<span data-ttu-id="ac73d-267">[T_THEME_COLOR_EMPHASISTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-267">[T_THEME_COLOR_EMPHASISTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-268">EmphasisBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-268">EmphasisBackground</span></span>  <br/> |<span data-ttu-id="ac73d-269">Контрастный цвет фона, который появляется позади акцентного текста.</span><span class="sxs-lookup"><span data-stu-id="ac73d-269">The accented background color that appears directly behind emphasis text.</span></span>  <br/> |<span data-ttu-id="ac73d-270">[T_THEME_COLOR_EMPHASISBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-270">[T_THEME_COLOR_EMPHASISBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-271">EmphasisHoverBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-271">EmphasisHoverBackground</span></span>  <br/> |<span data-ttu-id="ac73d-272">Цвет фона при наведении курсора мыши для элементов, расположенных на акцентном фоне.</span><span class="sxs-lookup"><span data-stu-id="ac73d-272">Background color on hover, for elements that are using emphasis background.</span></span>  <br/> |<span data-ttu-id="ac73d-273">[T_THEME_COLOR_EMPHASISHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-273">[T_THEME_COLOR_EMPHASISHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-274">EmphasisBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-274">EmphasisBorder</span></span>  <br/> |<span data-ttu-id="ac73d-275">Цвет границы элементов, расположенных на акцентном фоне.</span><span class="sxs-lookup"><span data-stu-id="ac73d-275">Border color for elements that are using emphasis background.</span></span>  <br/> |<span data-ttu-id="ac73d-276">[T_THEME_COLOR_EMPHASISBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-276">[T_THEME_COLOR_EMPHASISBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-277">EmphasisHoverBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-277">EmphasisHoverBorder</span></span>  <br/> |<span data-ttu-id="ac73d-278">Цвет границы при наведении курсора мыши для элементов, расположенных на акцентном фоне.</span><span class="sxs-lookup"><span data-stu-id="ac73d-278">Border color on hover for elements that are using emphasis background.</span></span>  <br/> |<span data-ttu-id="ac73d-279">[T_THEME_COLOR_EMPHASISHOVERBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-279">[T_THEME_COLOR_EMPHASISHOVERBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-280">SubtleEmphasisText</span><span class="sxs-lookup"><span data-stu-id="ac73d-280">SubtleEmphasisText</span></span>  <br/> |<span data-ttu-id="ac73d-281">Текст, который появляется поверх слабо выделенного акцентного фона.</span><span class="sxs-lookup"><span data-stu-id="ac73d-281">Text that appears on top of subtle emphasis background.</span></span>  <br/> |<span data-ttu-id="ac73d-282">[T_THEME_COLOR_SUBTLEEMPHASISTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-282">[T_THEME_COLOR_SUBTLEEMPHASISTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-283">SubtleEmphasisCommandLinks</span><span class="sxs-lookup"><span data-stu-id="ac73d-283">SubtleEmphasisCommandLinks</span></span>  <br/> |<span data-ttu-id="ac73d-284">Цвет ссылки на команду для ссылок, появляющихся поверх слабо выделенного акцентного фона.</span><span class="sxs-lookup"><span data-stu-id="ac73d-284">Command link color for links that appear on top of subtle emphasis background.</span></span>  <br/> |<span data-ttu-id="ac73d-285">[T_THEME_COLOR_SUBTLEEMPHASISCOMMANDLINKS]</span><span class="sxs-lookup"><span data-stu-id="ac73d-285">[T_THEME_COLOR_SUBTLEEMPHASISCOMMANDLINKS]</span></span>  <br/> |
|<span data-ttu-id="ac73d-286">SubtleEmphasisBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-286">SubtleEmphasisBackground</span></span>  <br/> |<span data-ttu-id="ac73d-287">Фон, поверх которого появляется слабо выделенный акцентный текст.</span><span class="sxs-lookup"><span data-stu-id="ac73d-287">Background that appears directly behind subtle emphasis text.</span></span>  <br/> |<span data-ttu-id="ac73d-288">[T_THEME_COLOR_SUBTLEEMPHASISBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-288">[T_THEME_COLOR_SUBTLEEMPHASISBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-289">TopBarText</span><span class="sxs-lookup"><span data-stu-id="ac73d-289">TopBarText</span></span>  <br/> |<span data-ttu-id="ac73d-290">Цвет текста и глифа для приветственного меню, значков панели быстрого доступа и закрытых вкладок на ленте.</span><span class="sxs-lookup"><span data-stu-id="ac73d-290">Text and glyph color for the welcome menu, quick access toolbar icons, and closed ribbon tabs.</span></span>  <br/> |<span data-ttu-id="ac73d-291">[T_THEME_COLOR_TOPBARTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-291">[T_THEME_COLOR_TOPBARTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-292">TopBarBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-292">TopBarBackground</span></span>  <br/> |<span data-ttu-id="ac73d-293">Цвет фона верхней панели, видимой под панелью иерархической навигации или справа от нее.</span><span class="sxs-lookup"><span data-stu-id="ac73d-293">The background color for the top bar, which is seen below and to the right of the suite navigation.</span></span>  <br/> |<span data-ttu-id="ac73d-294">[T_THEME_COLOR_TOPBARBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-294">[T_THEME_COLOR_TOPBARBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-295">TopBarHoverText</span><span class="sxs-lookup"><span data-stu-id="ac73d-295">TopBarHoverText</span></span>  <br/> |<span data-ttu-id="ac73d-296">Цвет текста и глифа для приветственного меню, значков панели быстрого доступа и закрытых вкладок на ленте при наведении на них курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-296">Text and glyph color on hover for the welcome menu, quick access toolbar icons, and closed ribbon tabs.</span></span>  <br/> |<span data-ttu-id="ac73d-297">[T_THEME_COLOR_TOPBARHOVERTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-297">[T_THEME_COLOR_TOPBARHOVERTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-298">TopBarPressedText</span><span class="sxs-lookup"><span data-stu-id="ac73d-298">TopBarPressedText</span></span>  <br/> |<span data-ttu-id="ac73d-299">Цвет текста и глифа для приветственного меню, значков панели быстрого доступа и закрытых вкладок на ленте при нажатии на них.</span><span class="sxs-lookup"><span data-stu-id="ac73d-299">Text and glyph color for when the welcome menu, quick access toolbar icons, or closed ribbon tabs are pressed.</span></span>  <br/> |<span data-ttu-id="ac73d-300">[T_THEME_COLOR_TOPBARPRESSEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-300">[T_THEME_COLOR_TOPBARPRESSEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-301">HeaderText</span><span class="sxs-lookup"><span data-stu-id="ac73d-301">HeaderText</span></span>  <br/> |<span data-ttu-id="ac73d-302">Цвет основного текста для любого элемента в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-302">The base text color for anything in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-303">[T_THEME_COLOR_HEADERTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-303">[T_THEME_COLOR_HEADERTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-304">HeaderSubtleText</span><span class="sxs-lookup"><span data-stu-id="ac73d-304">HeaderSubtleText</span></span>  <br/> |<span data-ttu-id="ac73d-305">Текст подсказки для поля поиска, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-305">Helper text for the search box when in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-306">[T_THEME_COLOR_HEADERSUBTLETEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-306">[T_THEME_COLOR_HEADERSUBTLETEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-307">HeaderDisableText</span><span class="sxs-lookup"><span data-stu-id="ac73d-307">HeaderDisableText</span></span>  <br/> |<span data-ttu-id="ac73d-308">Текст отключенного поля поиска, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-308">Text for the search box, if the search box is disabled when in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-309">[T_THEME_COLOR_HEADERDISABLETEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-309">[T_THEME_COLOR_HEADERDISABLETEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-310">HeaderNavigationText</span><span class="sxs-lookup"><span data-stu-id="ac73d-310">HeaderNavigationText</span></span>  <br/> |<span data-ttu-id="ac73d-311">Цвет основного текста навигационных ссылок в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-311">Base text color for navigation links in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-312">[T_THEME_COLOR_HEADERNAVIGATIONTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-312">[T_THEME_COLOR_HEADERNAVIGATIONTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-313">HeaderNavigationHoverText</span><span class="sxs-lookup"><span data-stu-id="ac73d-313">HeaderNavigationHoverText</span></span>  <br/> |<span data-ttu-id="ac73d-314">Цвет текста навигационных ссылок в области верхнего колонтитула при наведении на них курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-314">Text color for navigation links in the header area when you hover over the link.</span></span>  <br/> |<span data-ttu-id="ac73d-315">[T_THEME_COLOR_HEADERNAVIGATIONHOVERTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-315">[T_THEME_COLOR_HEADERNAVIGATIONHOVERTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-316">HeaderNavigationPressedText</span><span class="sxs-lookup"><span data-stu-id="ac73d-316">HeaderNavigationPressedText</span></span>  <br/> |<span data-ttu-id="ac73d-317">Цвет текста навигационных ссылок в области верхнего колонтитула при выборе ссылки.</span><span class="sxs-lookup"><span data-stu-id="ac73d-317">Text color for navigation links in the header area when you press the link.</span></span>  <br/> |<span data-ttu-id="ac73d-318">[T_THEME_COLOR_HEADERNAVIGATIONPRESSEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-318">[T_THEME_COLOR_HEADERNAVIGATIONPRESSEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-319">HeaderNavigationSelectedText</span><span class="sxs-lookup"><span data-stu-id="ac73d-319">HeaderNavigationSelectedText</span></span>  <br/> |<span data-ttu-id="ac73d-320">Цвет текста навигационных ссылок в области верхнего колонтитула, когда ссылка уже выбрана.</span><span class="sxs-lookup"><span data-stu-id="ac73d-320">Text color for navigation links in the header area after the link is selected.</span></span>  <br/> |<span data-ttu-id="ac73d-321">[T_THEME_COLOR_HEADERNAVIGATIONSELECTEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-321">[T_THEME_COLOR_HEADERNAVIGATIONSELECTEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-322">HeaderLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-322">HeaderLines</span></span>  <br/> |<span data-ttu-id="ac73d-323">Линии поля поиска, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-323">Search box lines when the search box is in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-324">[T_THEME_COLOR_HEADERLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-324">[T_THEME_COLOR_HEADERLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-325">HeaderStrongLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-325">HeaderStrongLines</span></span>  <br/> |<span data-ttu-id="ac73d-326">Линии поля поиска, расположенного в области верхнего колонтитула, при наведении курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-326">Search box lines on hover when the search box is in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-327">[T_THEME_COLOR_HEADERSTRONGLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-327">[T_THEME_COLOR_HEADERSTRONGLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-328">HeaderAccentLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-328">HeaderAccentLines</span></span>  <br/> |<span data-ttu-id="ac73d-329">Линии выделенного поля поиска, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-329">Search box lines on focus when the search box is in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-330">[T_THEME_COLOR_HEADERACCENTLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-330">[T_THEME_COLOR_HEADERACCENTLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-331">HeaderSublteLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-331">HeaderSublteLines</span></span>  <br/> |<span data-ttu-id="ac73d-p116">Слабо выделенные линии, находящиеся внутри области верхнего колонтитула (не применяется в CSS по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ac73d-p116">Subtle lines found inside the header area. Not used in default CSS.</span></span>  <br/> |<span data-ttu-id="ac73d-334">[T_THEME_COLOR_HEADERSUBTLELINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-334">[T_THEME_COLOR_HEADERSUBTLELINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-335">HeaderDisabledLines</span><span class="sxs-lookup"><span data-stu-id="ac73d-335">HeaderDisabledLines</span></span>  <br/> |<span data-ttu-id="ac73d-336">Линии отключенного поля поиска, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-336">Search box lines if the search box is disabled when it's in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-337">[T_THEME_COLOR_HEADERDISABLEDLINES]</span><span class="sxs-lookup"><span data-stu-id="ac73d-337">[T_THEME_COLOR_HEADERDISABLEDLINES]</span></span>  <br/> |
|<span data-ttu-id="ac73d-338">HeaderDisabledBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-338">HeaderDisabledBackground</span></span>  <br/> |<span data-ttu-id="ac73d-339">Фон отключенного поля поиска, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-339">Search box background if the search box is disabled when it's in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-340">[T_THEME_COLOR_HEADERDISABLEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-340">[T_THEME_COLOR_HEADERDISABLEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-341">HeaderFlyoutBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-341">HeaderFlyoutBorder</span></span>  <br/> |<span data-ttu-id="ac73d-342">Граница раскрывающегося меню из области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-342">Border for drop-down menus when originating from the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-343">[T_THEME_COLOR_HEADERFLYOUTBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-343">[T_THEME_COLOR_HEADERFLYOUTBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-344">HeaderSiteTitle</span><span class="sxs-lookup"><span data-stu-id="ac73d-344">HeaderSiteTitle</span></span>  <br/> |<span data-ttu-id="ac73d-345">Цвет текста названия сайта, расположенного в области верхнего колонтитула.</span><span class="sxs-lookup"><span data-stu-id="ac73d-345">Text color for the site title when in the header area.</span></span>  <br/> |<span data-ttu-id="ac73d-346">[T_THEME_COLOR_HEADERSITETITLE]</span><span class="sxs-lookup"><span data-stu-id="ac73d-346">[T_THEME_COLOR_HEADERSITETITLE]</span></span>  <br/> |
|<span data-ttu-id="ac73d-347">SuiteBarBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-347">SuiteBarBackground</span></span>  <br/> |<span data-ttu-id="ac73d-348">Цвет фона панели иерархической навигации.</span><span class="sxs-lookup"><span data-stu-id="ac73d-348">Background color for the suite navigation.</span></span>  <br/> |<span data-ttu-id="ac73d-349">[T_THEME_COLOR_SUITEBARBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-349">[T_THEME_COLOR_SUITEBARBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-350">SuiteBarHoverBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-350">SuiteBarHoverBackground</span></span>  <br/> |<span data-ttu-id="ac73d-351">Цвет фона панели иерархической навигации при наведении курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-351">Background color on hover for the suite navigation.</span></span>  <br/> |<span data-ttu-id="ac73d-352">[T_THEME_COLOR_SUITEBARHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-352">[T_THEME_COLOR_SUITEBARHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-353">SuiteBarText</span><span class="sxs-lookup"><span data-stu-id="ac73d-353">SuiteBarText</span></span>  <br/> |<span data-ttu-id="ac73d-354">Цвет текста и глифа для элементов панели иерархической навигации.</span><span class="sxs-lookup"><span data-stu-id="ac73d-354">Text and glyph color for the suite navigation items.</span></span>  <br/> |<span data-ttu-id="ac73d-355">[T_THEME_COLOR_SUITEBARTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-355">[T_THEME_COLOR_SUITEBARTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-356">SuiteBarDisabledText</span><span class="sxs-lookup"><span data-stu-id="ac73d-356">SuiteBarDisabledText</span></span>  <br/> |<span data-ttu-id="ac73d-p117">Цвет текста и глифа для отключенных элементов панели иерархической навигации (не используется в CSS по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="ac73d-p117">Text and glyph color for disabled suite items. Not used in default CSS.</span></span>  <br/> |<span data-ttu-id="ac73d-359">[T_THEME_COLOR_SUITEBARDISABLEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-359">[T_THEME_COLOR_SUITEBARDISABLEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-360">ButtonText</span><span class="sxs-lookup"><span data-stu-id="ac73d-360">ButtonText</span></span>  <br/> |<span data-ttu-id="ac73d-361">Цвет текста кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-361">Text color for buttons.</span></span>  <br/> |<span data-ttu-id="ac73d-362">[T_THEME_COLOR_BUTTONTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-362">[T_THEME_COLOR_BUTTONTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-363">ButtonDisabledText</span><span class="sxs-lookup"><span data-stu-id="ac73d-363">ButtonDisabledText</span></span>  <br/> |<span data-ttu-id="ac73d-364">Цвет текста отключенных кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-364">Text color for disabled buttons.</span></span>  <br/> |<span data-ttu-id="ac73d-365">[T_THEME_COLOR_BUTTONDISABLEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-365">[T_THEME_COLOR_BUTTONDISABLEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-366">ButtonBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-366">ButtonBackground</span></span>  <br/> |<span data-ttu-id="ac73d-367">Цвет фона кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-367">Background color for buttons.</span></span>  <br/> |<span data-ttu-id="ac73d-368">[T_THEME_COLOR_BUTTONBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-368">[T_THEME_COLOR_BUTTONBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-369">ButtonHoverBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-369">ButtonHoverBackground</span></span>  <br/> |<span data-ttu-id="ac73d-370">Цвет фона кнопок при наведении курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-370">Background color for buttons on hover.</span></span>  <br/> |<span data-ttu-id="ac73d-371">[T_THEME_COLOR_BUTTONHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-371">[T_THEME_COLOR_BUTTONHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-372">ButtonPressedBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-372">ButtonPressedBackground</span></span>  <br/> |<span data-ttu-id="ac73d-373">Цвет фона кнопок при нажатии.</span><span class="sxs-lookup"><span data-stu-id="ac73d-373">Background color for buttons while pressed.</span></span>  <br/> |<span data-ttu-id="ac73d-374">[T_THEME_COLOR_BUTTONPRESSEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-374">[T_THEME_COLOR_BUTTONPRESSEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-375">ButtonDisabledBackground</span><span class="sxs-lookup"><span data-stu-id="ac73d-375">ButtonDisabledBackground</span></span>  <br/> |<span data-ttu-id="ac73d-376">Цвет фона отключенных кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-376">Background color for disabled buttons.</span></span>  <br/> |<span data-ttu-id="ac73d-377">[T_THEME_COLOR_BUTTONDISABLEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="ac73d-377">[T_THEME_COLOR_BUTTONDISABLEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="ac73d-378">ButtonBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-378">ButtonBorder</span></span>  <br/> |<span data-ttu-id="ac73d-379">Цвет границы кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-379">Border color for buttons.</span></span>  <br/> |<span data-ttu-id="ac73d-380">[T_THEME_COLOR_BUTTONBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-380">[T_THEME_COLOR_BUTTONBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-381">ButtonHoverBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-381">ButtonHoverBorder</span></span>  <br/> |<span data-ttu-id="ac73d-382">Цвет границы кнопок при наведении курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-382">Border color for buttons on hover.</span></span>  <br/> |<span data-ttu-id="ac73d-383">[T_THEME_COLOR_BUTTONHOVERBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-383">[T_THEME_COLOR_BUTTONHOVERBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-384">ButtonPressedBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-384">ButtonPressedBorder</span></span>  <br/> |<span data-ttu-id="ac73d-385">Цвет границы кнопок при нажатии.</span><span class="sxs-lookup"><span data-stu-id="ac73d-385">Border color for buttons while pressed.</span></span>  <br/> |<span data-ttu-id="ac73d-386">[T_THEME_COLOR_BUTTONPRESSEDBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-386">[T_THEME_COLOR_BUTTONPRESSEDBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-387">ButtonDisabledBorder</span><span class="sxs-lookup"><span data-stu-id="ac73d-387">ButtonDisabledBorder</span></span>  <br/> |<span data-ttu-id="ac73d-388">Цвет границы отключенных кнопок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-388">Border color for buttons that are disabled.</span></span>  <br/> |<span data-ttu-id="ac73d-389">[T_THEME_COLOR_BUTTONDISABLEDBORDER]</span><span class="sxs-lookup"><span data-stu-id="ac73d-389">[T_THEME_COLOR_BUTTONDISABLEDBORDER]</span></span>  <br/> |
|<span data-ttu-id="ac73d-390">ButtonGlyph</span><span class="sxs-lookup"><span data-stu-id="ac73d-390">ButtonGlyph</span></span>  <br/> |<span data-ttu-id="ac73d-391">Цвет глифа на кнопке.</span><span class="sxs-lookup"><span data-stu-id="ac73d-391">Glyph color for a glyph that appears in a button.</span></span>  <br/> |<span data-ttu-id="ac73d-392">[T_THEME_COLOR_BUTTONGLYPH]</span><span class="sxs-lookup"><span data-stu-id="ac73d-392">[T_THEME_COLOR_BUTTONGLYPH]</span></span>  <br/> |
|<span data-ttu-id="ac73d-393">ButtonGlyphActive</span><span class="sxs-lookup"><span data-stu-id="ac73d-393">ButtonGlyphActive</span></span>  <br/> |<span data-ttu-id="ac73d-394">Цвет глифа на кнопке при наведении курсора мыши.</span><span class="sxs-lookup"><span data-stu-id="ac73d-394">Glyph color on hover, for a glyph that appears in a button.</span></span>  <br/> |<span data-ttu-id="ac73d-395">[T_THEME_COLOR_BUTTONGLYPHACTIVE]</span><span class="sxs-lookup"><span data-stu-id="ac73d-395">[T_THEME_COLOR_BUTTONGLYPHACTIVE]</span></span>  <br/> |
|<span data-ttu-id="ac73d-396">ButtonGlyphDisabled</span><span class="sxs-lookup"><span data-stu-id="ac73d-396">ButtonGlyphDisabled</span></span>  <br/> |<span data-ttu-id="ac73d-397">Цвет глифа для неактивной кнопки.</span><span class="sxs-lookup"><span data-stu-id="ac73d-397">Glyph color for a disabled button.</span></span>  <br/> |<span data-ttu-id="ac73d-398">[T_THEME_COLOR_BUTTONGLYPHDISABLED]</span><span class="sxs-lookup"><span data-stu-id="ac73d-398">[T_THEME_COLOR_BUTTONGLYPHDISABLED]</span></span>  <br/> |
|<span data-ttu-id="ac73d-399">TileText</span><span class="sxs-lookup"><span data-stu-id="ac73d-399">TileText</span></span>  <br/> |<span data-ttu-id="ac73d-400">Текст, отображаемый в верхней части наложения фона плитки.</span><span class="sxs-lookup"><span data-stu-id="ac73d-400">The text that appears on top of the tile background overlay.</span></span>  <br/> |<span data-ttu-id="ac73d-401">[T_THEME_COLOR_TILETEXT]</span><span class="sxs-lookup"><span data-stu-id="ac73d-401">[T_THEME_COLOR_TILETEXT]</span></span>  <br/> |
|<span data-ttu-id="ac73d-402">TileBackgroundOverlay</span><span class="sxs-lookup"><span data-stu-id="ac73d-402">TileBackgroundOverlay</span></span>  <br/> |<span data-ttu-id="ac73d-403">Цвет наложения фона плиток.</span><span class="sxs-lookup"><span data-stu-id="ac73d-403">The background overlay color for tiles.</span></span>  <br/> |<span data-ttu-id="ac73d-404">[T_THEME_COLOR_TILEBACKGROUNDOVERLAY]</span><span class="sxs-lookup"><span data-stu-id="ac73d-404">[T_THEME_COLOR_TILEBACKGROUNDOVERLAY]</span></span>  <br/> |
|<span data-ttu-id="ac73d-405">ContentAccent1</span><span class="sxs-lookup"><span data-stu-id="ac73d-405">ContentAccent1</span></span>  <br/> |<span data-ttu-id="ac73d-406">Первый акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).</span><span class="sxs-lookup"><span data-stu-id="ac73d-406">The first accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="ac73d-407">[T_THEME_COLOR_CONTENTACCENT1]</span><span class="sxs-lookup"><span data-stu-id="ac73d-407">[T_THEME_COLOR_CONTENTACCENT1]</span></span>  <br/> |
|<span data-ttu-id="ac73d-408">ContentAccent2</span><span class="sxs-lookup"><span data-stu-id="ac73d-408">ContentAccent2</span></span>  <br/> |<span data-ttu-id="ac73d-409">Второй акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).</span><span class="sxs-lookup"><span data-stu-id="ac73d-409">The second accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="ac73d-410">[T_THEME_COLOR_CONTENTACCENT2]</span><span class="sxs-lookup"><span data-stu-id="ac73d-410">[T_THEME_COLOR_CONTENTACCENT2]</span></span>  <br/> |
|<span data-ttu-id="ac73d-411">ContentAccent3</span><span class="sxs-lookup"><span data-stu-id="ac73d-411">ContentAccent3</span></span>  <br/> |<span data-ttu-id="ac73d-412">Третий акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).</span><span class="sxs-lookup"><span data-stu-id="ac73d-412">The third accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="ac73d-413">[T_THEME_COLOR_CONTENTACCENT3]</span><span class="sxs-lookup"><span data-stu-id="ac73d-413">[T_THEME_COLOR_CONTENTACCENT3]</span></span>  <br/> |
|<span data-ttu-id="ac73d-414">ContentAccent4</span><span class="sxs-lookup"><span data-stu-id="ac73d-414">ContentAccent4</span></span>  <br/> |<span data-ttu-id="ac73d-415">Четвертый акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).</span><span class="sxs-lookup"><span data-stu-id="ac73d-415">The fourth accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="ac73d-416">[T_THEME_COLOR_CONTENTACCENT4]</span><span class="sxs-lookup"><span data-stu-id="ac73d-416">[T_THEME_COLOR_CONTENTACCENT4]</span></span>  <br/> |
|<span data-ttu-id="ac73d-417">ContentAccent5</span><span class="sxs-lookup"><span data-stu-id="ac73d-417">ContentAccent5</span></span>  <br/> |<span data-ttu-id="ac73d-418">Пятый акцентный цвет, доступный пользователю в средстве выбора цвета в редакторе форматированного текста.</span><span class="sxs-lookup"><span data-stu-id="ac73d-418">The fifth accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="ac73d-419">[T_THEME_COLOR_CONTENTACCENT5]</span><span class="sxs-lookup"><span data-stu-id="ac73d-419">[T_THEME_COLOR_CONTENTACCENT5]</span></span>  <br/> |
|<span data-ttu-id="ac73d-420">ContentAccent6</span><span class="sxs-lookup"><span data-stu-id="ac73d-420">ContentAccent6</span></span>  <br/> |<span data-ttu-id="ac73d-421">Шестой акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).</span><span class="sxs-lookup"><span data-stu-id="ac73d-421">The sixth accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="ac73d-422">[T_THEME_COLOR_CONTENTACCENT6]</span><span class="sxs-lookup"><span data-stu-id="ac73d-422">[T_THEME_COLOR_CONTENTACCENT6]</span></span>  <br/> |
   

## <a name="font-schemes"></a><span data-ttu-id="ac73d-423">Схемы шрифтов</span><span class="sxs-lookup"><span data-stu-id="ac73d-423">Font schemes</span></span>
<span data-ttu-id="ac73d-424"><a name="font"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-424"><a name="font"> </a></span></span>

<span data-ttu-id="ac73d-p118">Шрифты указываются в схеме шрифтов (файле SPFONT) и файле предварительного просмотра эталонной страницы (файле PREVIEW) данного сайта SharePoint. Схема шрифтов определяет шрифты для четырех областей: названия, панели навигации, заголовка и основного текста. SharePoint содержит семь схем шрифтов. Вы также можете создавать дополнительные схемы. Файлы схем шрифтов хранятся во вложенной папке **15** коллекции тем корневого сайта в семействе веб-сайтов (http:// _ИмяСемействаСайтов_/_catalogs/theme/15/). Чтобы получить доступ к коллекции тем из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** щелкните ссылку **Темы**, а затем выберите папку **15**.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p118">Fonts are defined in the font scheme (.spfont file) and the master page preview (.preview file) for a given SharePoint site. The font scheme defines the fonts that are used in four areas: title, navigation, heading, and body. Seven font schemes are included in SharePoint. You can create additional font schemes. The font scheme files are located in the **15** subfolder of the Theme Gallery of the root site of the site collection (http:// _SiteCollectionName_/_catalogs/theme/15/). To access the Theme Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, select **Themes**, and then select **15**.</span></span>
  
    
    
<span data-ttu-id="ac73d-431">Ниже приводится пример формата для файла SPFONT.</span><span class="sxs-lookup"><span data-stu-id="ac73d-431">The following example describes the format for an .spfont file.</span></span>
  
    
    



```xml

<?xml version="1.0" encoding="utf-8"?>
<s:fontScheme name="FontSchemeName" previewSlot1="Slot1" previewSlot2="Slot2" xmlns:s="http://schemas.microsoft.com/sharepoint/">
  <s:fontSlots>
    <s:fontSlot name="FontSlotName">
      <s:latin typeface="LatinScriptFont" />
      <s:ea typeface="EAScriptFont"/>
      <s:cs typeface="CSFont" />
      <s:font script="Language" typeface="ScriptFont" />
      <!--Additional fonts-->
  </s:fontSlots>
  <!--Additional font slots-->
</s:fontScheme>
```

<span data-ttu-id="ac73d-432">В файле SPFONT заменяются следующие заполнители:</span><span class="sxs-lookup"><span data-stu-id="ac73d-432">In an .spfont file, the following placeholders are replaced:</span></span>
  
    
    

-  <span data-ttu-id="ac73d-433">_FontSchemeName_ - имя схемы шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-433">_FontSchemeName_ is the name of the font scheme.</span></span>
    
  
-  <span data-ttu-id="ac73d-434">_Slot1_ - имя слота шрифта, который используется в качестве первого блока значка шрифта в средстве выбора схемы шрифтов, доступном в мастере **изменения оформления**.</span><span class="sxs-lookup"><span data-stu-id="ac73d-434">_Slot1_ is the name of the font slot that you want to use as the first block of the font icon in the font scheme picker in the **Change the look** wizard.</span></span>
    
  
-  <span data-ttu-id="ac73d-435">_Slot2_ - имя слота шрифта, который используется в качестве второго блока значка шрифта в средстве выбора схемы шрифтов, доступном в мастере **изменения оформления**.</span><span class="sxs-lookup"><span data-stu-id="ac73d-435">_Slot2_ is the name of the font slot that you want to use as the second block of the font icon in the font scheme picker in the **Change the look** wizard.</span></span>
    
  
-  <span data-ttu-id="ac73d-436">_FontSlotName_ - имя определяемого слота шрифта, например название.</span><span class="sxs-lookup"><span data-stu-id="ac73d-436">_FontSlotName_ is the name of the font slot that you are defining (for example, title).</span></span>
    
  
-  <span data-ttu-id="ac73d-p119">_LatinScriptFont_ - шрифт, используемый для латинского письма. Он также выступает в качестве резервного, т. е. применяется для языков, для которых не установлен определенный шрифт в схеме шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p119">_LatinScriptFont_ is the font to use for Latin scripts. This font is also the fallback font. That is, this is the font that is used for a language that does not have a script that is explicitly set in the font scheme.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ac73d-440">Вам необходимо указать дополнительные сведения для использования веб-шрифтов в шрифтовой схеме.</span><span class="sxs-lookup"><span data-stu-id="ac73d-440">Note: You must provide additional information to use web fonts in your font scheme.</span></span> <span data-ttu-id="ac73d-441">Дополнительные сведения см. в разделе [Веб-шрифты](#webFont) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="ac73d-441">For more information, see the  [Web fonts](#webFont) section in this article.</span></span>
-  <span data-ttu-id="ac73d-p121">_EAScriptFont_ - это шрифт, который используется для сценариев языков Восточной Азии. Элемент **<s:ea>** не используется в SharePoint в настоящее время, но этот элемент **<s:ea>** требуется в схеме шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p121">_EAScriptFont_ is the font to use for East Asia scripts. The **<s:ea>** element is not currently used by SharePoint. But, the **<s:ea>** element is still required in the font scheme.</span></span>
    
  
-  <span data-ttu-id="ac73d-p122">_CSFont_ - это шрифт, используемый в сложных сценариях. Элемент **<s:cs>** не используется в SharePoint в настоящее время, но этот элемент **<s:cs>** требуется в схеме шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p122">_CSFont_ is the font to use for complex scripts. The **<s:cs>** element is not currently used by SharePoint. But, the **<s:cs>** element is still required in the font scheme.</span></span>
    
  
-  <span data-ttu-id="ac73d-448">_Language_ - это набор знаков.</span><span class="sxs-lookup"><span data-stu-id="ac73d-448">_Language_ is the language script.</span></span>
    
  
-  <span data-ttu-id="ac73d-449">_ScriptFont_ - это шрифт, который используется для определенного набора знаков.</span><span class="sxs-lookup"><span data-stu-id="ac73d-449">_ScriptFont_ is the font to use for the specified language script.</span></span>
    
  
<span data-ttu-id="ac73d-450">Ниже приводится пример части файла SPFONT.</span><span class="sxs-lookup"><span data-stu-id="ac73d-450">The following example shows a portion of an .spfont file.</span></span>
  
    
    



```xml

<s:fontScheme name="Georgia" previewSlot1="title" previewSlot2="body" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:fontSlots>
        <s:fontSlot name="title">
            <s:latin typeface="Georgia"/>
            <s:ea typeface=""/>
            <s:cs typeface="Segoe UI Light" />
            <s:font script="Arab" typeface="Tahoma" />
            <s:font script="Deva" typeface="Mangal" />
            <s:font script="Grek" typeface="Segoe UI Light" />
            <s:font script="Hang" typeface="Malgun Gothic" />
            <s:font script="Hans" typeface="Microsoft YaHei" />
            <s:font script="Hant" typeface="Microsoft JhengHei" />
            <s:font script="Hebr" typeface="Tahoma" />
            <s:font script="Hira" typeface="Meiryo" />
            <s:font script="Thai" typeface="Tahoma" />
            <s:font script="Armn" typeface="Tahoma" />
            <s:font script="Beng" typeface="Vrinda" />
            <s:font script="Cher" typeface="Plantagenet Cherokee" />
            <s:font script="Ethi" typeface="Nyala" />
            <s:font script="Geor" typeface="Sylfaen" />
            <s:font script="Gujr" typeface="Shruti" />
            <s:font script="Guru" typeface="Raavi" />
            <s:font script="Knda" typeface="Tunga" />
            <s:font script="Khmr" typeface="DaunPenh" />
            <s:font script="Laoo" typeface="DokChampa" />
            <s:font script="Mlym" typeface="Kartika" />
            <s:font script="Mymr" typeface="Myanmar Text" />
            <s:font script="Orya" typeface="Kalinga" />
            <s:font script="Sinh" typeface="Iskoola Pota" />
            <s:font script="Syrc" typeface="Estrangelo Edessa" />
            <s:font script="Taml" typeface="Latha" />
            <s:font script="Telu" typeface="Gautami" />
            <s:font script="Thaa" typeface="MV Boli" />
            <s:font script="Tibt" typeface="Cordia New" />
            <s:font script="Yiii" typeface="Microsoft Yi Baiti" />
        </s:fontSlot>
???
```

<span data-ttu-id="ac73d-p123">SharePoint обеспечивает поддержку веб-шрифтов. Чтобы использовать их в своей схеме шрифтов, необходимо предоставить дополнительные сведения. Подробнее об этом можно узнать в разделе  [Веб-шрифты](#webFont) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p123">SharePoint includes support for web fonts. You must provide additional information to use web fonts in your font scheme. For more information, see the  [Web fonts](#webFont) section in this article.</span></span>
  
    
    

### <a name="web-safe-fonts"></a><span data-ttu-id="ac73d-454">Шрифты, соответствующие веб-палитре</span><span class="sxs-lookup"><span data-stu-id="ac73d-454">Web-safe fonts</span></span>
<span data-ttu-id="ac73d-455"><a name="websafeFont"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-455"><a name="websafeFont"> </a></span></span>

<span data-ttu-id="ac73d-p124">Шрифты, соответствующие веб-палитре, представляют собой набор широко используемых шрифтов, которые по умолчанию доступны на большинстве устройств. Чтобы указать шрифт, соответствующий веб-палитре, в схеме шрифтов, включите его имя в атрибут **typeface** слота шрифта. Ниже приводится пример использования шрифта, соответствующего веб-палитре, в схеме шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p124">Web-safe fonts are a set of fonts that are widely used and available on most devices by default. To specify a web-safe font in the font scheme, include the name of the font in the **typeface** attribute of the font slot. The following example shows a web-safe font used in a font scheme.</span></span>
  
    
    

```xml

<s:fontSlot name="title">
  <s:latin typeface="Georgia"/>
???
</s:fontSlot>
```


### <a name="web-fonts"></a><span data-ttu-id="ac73d-459">Веб-шрифты</span><span class="sxs-lookup"><span data-stu-id="ac73d-459">Web fonts</span></span>
<span data-ttu-id="ac73d-460"><a name="webFont"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-460"><a name="webFont"> </a></span></span>

<span data-ttu-id="ac73d-p125">Веб-шрифты - это шрифты, доступные в Интернете. Когда пользователь просматривает сайт, на котором используются веб-шрифты, веб-браузер скачивает необходимые файлы шрифтов вместе со всей страницей. Чтобы использовать веб-шрифт, необходимо указать URL-адрес ваших файлов шрифтов в четырех форматах (для обеспечения поддержки различными браузерами), а также маленький и большой эскизы, которые используются средством выбора схем шрифтов для определения имен шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-p125">Web fonts are fonts that are available on the Internet. When a user views a site that uses web fonts, the web browser downloads the necessary font files along with the rest of the page. To specify a web font, you must provide the URL to your web font files in four font formats (for support across browsers), and a small and large thumbnail image to use to render the font names in the font scheme picker.</span></span>
  
    
    
<span data-ttu-id="ac73d-464">В приведенном ниже примере указаны сведения, необходимые для использования веб-шрифта в элементе **<s:latin>**.</span><span class="sxs-lookup"><span data-stu-id="ac73d-464">The following example describes the information that is required to use a web font in an **<s:latin>** element.</span></span>
  
    
    



```xml

<s:latin typeface="FontName"
  eotsrc="EotFile"
  woffsrc="WoffFile"
  ttfsrc="TtfFile"
  svgsrc="SvgFile"
  largeimgsrc="LargeImgFile"
  smallimgsrc="SmallImgFile" />

```

<span data-ttu-id="ac73d-465">В этом примере использования веб-шрифта заменяются следующие заполнители:</span><span class="sxs-lookup"><span data-stu-id="ac73d-465">In this example of using a web font, the following placeholders would be replaced:</span></span>
  
    
    

-  <span data-ttu-id="ac73d-466">_FontName_ - имя веб-шрифта.</span><span class="sxs-lookup"><span data-stu-id="ac73d-466">_FontName_ is the name of the web font.</span></span>
    
  
-  <span data-ttu-id="ac73d-467">_EotFile_ - относительный URL-адрес файла внедряемых шрифтов Open Type.</span><span class="sxs-lookup"><span data-stu-id="ac73d-467">_EotFile_ is the relative URL to the Embedded Open Type font file.</span></span>
    
  
-  <span data-ttu-id="ac73d-468">_WoffFile_ - относительный URL-адрес файла шрифта WOFF (Web Open Font Format).</span><span class="sxs-lookup"><span data-stu-id="ac73d-468">_WoffFile_ is the relative URL to the Web Open Font Format font file.</span></span>
    
  
-  <span data-ttu-id="ac73d-469">_TtfFile_ - относительный URL-адрес файла шрифта TrueType.</span><span class="sxs-lookup"><span data-stu-id="ac73d-469">_TtfFile_ is the relative URL to the TrueType font file.</span></span>
    
  
-  <span data-ttu-id="ac73d-470">_SvgFile_ - относительный URL-адрес файла шрифта для масштабируемого векторного рисунка (SVG).</span><span class="sxs-lookup"><span data-stu-id="ac73d-470">_SvgFile_ is the relative URL to the Scalable Vector Graphics font file.</span></span>
    
  
-  <span data-ttu-id="ac73d-471">_LargeImgFile_ - относительный URL-адрес большого эскиза, используемого в средстве выбора схемы шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-471">_LargeImgFile_ is the relative URL to the large thumbnail image that you want to use in the font scheme picker.</span></span>
    
  
-  <span data-ttu-id="ac73d-472">_SmallImgFile_ - относительный URL-адрес маленького эскиза, используемый в средстве выбора схемы шрифтов.</span><span class="sxs-lookup"><span data-stu-id="ac73d-472">_SmallImgFile_ is the relative URL to the small thumbnail image that you want to use in the font scheme picker.</span></span>
    
  

### <a name="font-slots"></a><span data-ttu-id="ac73d-473">Слоты шрифтов</span><span class="sxs-lookup"><span data-stu-id="ac73d-473">Font slots</span></span>
<span data-ttu-id="ac73d-474"><a name="fontSlot"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-474"><a name="fontSlot"> </a></span></span>

<span data-ttu-id="ac73d-475">В таблице 1 представлены доступные слоты шрифтов, а также области их применения на странице.</span><span class="sxs-lookup"><span data-stu-id="ac73d-475">Table 1 describes the available font slots and where they are used in a page.</span></span>
  
    
    

<span data-ttu-id="ac73d-476">**Таблица 1. Слоты шрифтов**</span><span class="sxs-lookup"><span data-stu-id="ac73d-476">**Table 1. Font slots**</span></span>


|<span data-ttu-id="ac73d-477">**Имя слота шрифта**</span><span class="sxs-lookup"><span data-stu-id="ac73d-477">**Font Slot Name**</span></span>|<span data-ttu-id="ac73d-478">**Описание**</span><span class="sxs-lookup"><span data-stu-id="ac73d-478">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ac73d-479">title</span><span class="sxs-lookup"><span data-stu-id="ac73d-479">title</span></span>  <br/> |<span data-ttu-id="ac73d-480">Используется в названии страницы.</span><span class="sxs-lookup"><span data-stu-id="ac73d-480">Used for the page title.</span></span>  <br/> |
|<span data-ttu-id="ac73d-481">перемещение</span><span class="sxs-lookup"><span data-stu-id="ac73d-481">navigation</span></span>  <br/> |<span data-ttu-id="ac73d-482">Используется для элементов горизонтальной и вертикальной панели навигации на странице.</span><span class="sxs-lookup"><span data-stu-id="ac73d-482">Used for the horizontal and vertical navigation elements on the page.</span></span>  <br/> |
|<span data-ttu-id="ac73d-483">large-heading</span><span class="sxs-lookup"><span data-stu-id="ac73d-483">large-heading</span></span>  <br/> |<span data-ttu-id="ac73d-484">Используется в заголовках H1.</span><span class="sxs-lookup"><span data-stu-id="ac73d-484">Used for the H1 heading.</span></span>  <br/> |
|<span data-ttu-id="ac73d-485">heading</span><span class="sxs-lookup"><span data-stu-id="ac73d-485">heading</span></span>  <br/> |<span data-ttu-id="ac73d-486">Используется для заголовков H2 и H3, названий веб-частей, диалоговых окон и выносок.</span><span class="sxs-lookup"><span data-stu-id="ac73d-486">Used for H2 and H3 headings, Web Part titles, dialog box titles, and callout titles.</span></span>  <br/> |
|<span data-ttu-id="ac73d-487">small-heading</span><span class="sxs-lookup"><span data-stu-id="ac73d-487">small-heading</span></span>  <br/> |<span data-ttu-id="ac73d-488">Используется для заголовков H4.</span><span class="sxs-lookup"><span data-stu-id="ac73d-488">Used for H4 headings.</span></span>  <br/> |
|<span data-ttu-id="ac73d-489">large-body</span><span class="sxs-lookup"><span data-stu-id="ac73d-489">large-body</span></span>  <br/> |<span data-ttu-id="ac73d-490">Используется для крупного основного текста размером 15 и 19 пикселей.</span><span class="sxs-lookup"><span data-stu-id="ac73d-490">Used for large body text (15 pixels and 19 pixels).</span></span>  <br/> |
|<span data-ttu-id="ac73d-491">body</span><span class="sxs-lookup"><span data-stu-id="ac73d-491">body</span></span>  <br/> |<span data-ttu-id="ac73d-492">Основной шрифт, который используется для остального текста на странице.</span><span class="sxs-lookup"><span data-stu-id="ac73d-492">The base font that is used everywhere else on the page.</span></span>  <br/> |
   

## <a name="see-also"></a><span data-ttu-id="ac73d-493">См. также</span><span class="sxs-lookup"><span data-stu-id="ac73d-493">See also</span></span>
<span data-ttu-id="ac73d-494"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ac73d-494"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="ac73d-495">Общие сведения о темах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-495">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="ac73d-496">Инструкции. Развертывание пользовательской темы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-496">How to: Deploy a custom theme in SharePoint</span></span>](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ac73d-497">Обновление пользовательских тем и CSS для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-497">Upgrade custom themes and CSS to SharePoint</span></span>](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [<span data-ttu-id="ac73d-498">Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-498">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="ac73d-499">Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-499">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [<span data-ttu-id="ac73d-500">Фирменная символика и конструкция возможности дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="ac73d-500">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

  
    
    

