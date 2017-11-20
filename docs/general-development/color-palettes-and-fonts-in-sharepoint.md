---
title: "Цветовые палитры и шрифты в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c17d375b-151f-48ae-ac32-f2ce9e68d63f
ms.openlocfilehash: ec01f0c272c9ce3d7362e16f1bc73a4918373507
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="color-palettes-and-fonts-in-sharepoint"></a>Цветовые палитры и шрифты в SharePoint
Воспользуйтесь этим справочником, чтобы определить цветовую палитру или схему шрифтов, которые используются на сайте SharePoint.
## <a name="color-palettes"></a>Цветовые палитры
<a name="color"> </a>

Цветовая палитра - сочетание цветов, использующихся на сайте SharePoint. Она определяется в файле цветовой палитры. Цветовые слоты также используются файлом предварительного просмотра эталонной страницы для создания изображений эскиза и для предварительного просмотра изображений. Ниже описывается структура файла цветовой палитры и предварительного просмотра эталонной страницы:
  
    
    

- **Файл цветовой палитры (файл SPCOLOR)**
    
    Эти файлы используются в мастере **изменения оформления**, который позволяет пользователям изменять внешний вид сайта с помощью тем пользовательского интерфейса SharePoint. По умолчанию вместе с SharePoint устанавливаются 32 файла цветовой палитры. Кроме того, предусмотрена возможность создания дополнительных файлов. Ниже приводится пример формата файла цветовой палитры.
    

```xml  
<s:colorPalette isInverted="InvertedSetting" previewSlot1="Slot1" previewSlot2="Slot2" previewSlot3="Slot3" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:color name="ColorSlot" value="Color" />
    <!--additional color slots-->
</s:colorPalette>
```


  В файле цветовой палитры заменяются следующие заполнители:
    
-  _InvertedSetting_ - это логическое значение, в котором значение **true** соответствует цветовой палитре со светлым текстом на темном фоне. Тогда как значение **false** соответствует цветовой палитре с темным текстом на светлом фоне.
    
  
-  _Slot1_ - имя заметки цветового слота, которое используется в качестве первого блока значка палитры в средстве выбора цветовой палитры при работе с темами.
    
  
-  _Slot2_ - имя заметки цветового слота, которое используется в качестве второго блока значка палитры в средстве выбора цветовой палитры при работе с темами.
    
  
-  _Slot3_ - имя заметки цветового слота, которое используется в качестве третьего блока значка палитры в средстве выбора палитры при работе с темами.
    
  
-  _ColorSlot_ - имя заметки определяемого цветового слота, например "НазваниеСайта".
    
  
-  _Color_ - это шестнадцатеричное значение цвета, используемое для указанного цветового слота. Оно может быть представлено в виде 6 (RRGGBB) или 8 цифр (AARRGGBB). Если шестнадцатеричное значение представлено 8 цифрами, первые две цифры обозначают уровень прозрачности цвета в диапазоне 00-FF, что соответствует значениям от 0 до 255. Если оно представлено 6 цифрами, по умолчанию установлен уровень непрозрачности со значением 100 % или FF.
    
  

  Файлы цветовой палитры расположены в коллекции тем корневого сайта (в папке **15** http:// _ИмяСемействаСайтов_/_catalogs/theme/15/ семейства веб-сайтов). Чтобы получить доступ к коллекции тем из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** выберите элемент **Темы**, а затем выберите папку **15**.
    
  
- **Файл предварительного просмотра эталонной страницы (файл PREVIEW)**
    
  Файлы предварительного просмотра эталонной страницы используются для создания эскизов и изображений предварительного просмотра при работе с мастером **изменения оформления**. Чтобы эталонную страницу можно было использовать в мастере **изменения оформления**, для нее обязательно создается соответствующий файл предварительного просмотра. Файл предварительного просмотра - это файл со специальным форматированием, в котором есть разделы для цветовой палитры и схемы цветов по умолчанию, а также для CSS и HTML с маркерами. Он использует маркеры строк для получения значений цветовых слотов, имен шрифтов и локализованных строк пользовательского интерфейса. Ниже приведен пример использования цветовых слотов в файле предварительного просмотра эталонной страницы.
    


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


  Дополнительные сведения см. в статье [Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).
    
  

> **Совет.** Вы можете использовать цветовую палитру SharePoint при создании вариантов оформления для SharePoint. Вы можете [скачать цветовую палитру SharePoint](http://www.microsoft.com/en-us/download/details.aspx?id=38182) из Центра загрузки Майкрософт.
  
    
    


### <a name="color-slot-mapping"></a>Сопоставление цветовых слотов
<a name="colorSlots"> </a>

В таблице 1 описаны доступные цветовые слоты и область их применения на сайтах SharePoint.
  
    
    

> **Примечание.** Что касается элементов навигации, под нажатием подразумевается щелчок или касание. "Выбор" означает переход пользователя на страницу. Далее приведена сводка по обычной последовательности действий и цветовым слотам, применяемым к ссылке на каждом этапе. Основной текст ссылки: HeaderNavigationText. Пользователь наводит указатель на ссылку: HeaderNavigationHoverText. Пользователь нажимает или выбирает ссылку: HeaderNavigationPressedText. Пользователь переходит на выбранную страницу. Цветовой слот, применяемый к элементу навигации для страницы, которую просматривает пользователь: HeaderNavigationSelectedText.
  
    
    


**Таблица 1. Цветовые слоты**


|**Имя заметки**|**Применение цвета в пользовательском интерфейсе**|**Имя маркера**|
|:-----|:-----|:-----|
|BodyText  <br/> |Обычный текст  <br/> |[T_THEME_COLOR_BODYTEXT]  <br/> |
|SubtleBodyText  <br/> |Основной текст, который по цвету должен быть светлее обычного, например текст метаданных.  <br/> |[T_THEME_COLOR_SUBTLEBODYTEXT]  <br/> |
|StrongBodyText  <br/> |Выделение более насыщенным цветом основного текста, который должен отличаться от обычного.  <br/> |[T_THEME_COLOR_STRONGBODYTEXT]  <br/> |
|DisabledText  <br/> |Отключенный текст, например элементы меню, к которым нет доступа.  <br/> |[T_THEME_COLOR_DISABLEDTEXT]  <br/> |
|SiteTitle  <br/> |Цвет текста заголовка.  <br/> |[T_THEME_COLOR_SITETITLE]  <br/> |
|WebPartHeading  <br/> |Цвет текста заголовков веб-частей.  <br/> |[T_THEME_COLOR_WEBPARTHEADING]  <br/> |
|ErrorText  <br/> |Основной цвет, который при необходимости используется для текста сообщения об ошибке, границ и фона.  <br/> |[T_THEME_COLOR_ERRORTEXT]  <br/> |
|AccentText  <br/> |Цвет, который применяется для контрастного основного текста.  <br/> |[T_THEME_COLOR_ACCENTTEXT]  <br/> |
|SearchURL  <br/> |Цвет URL-адреса в результатах поиска. Он также используется для выделения новых элементов или уведомлений об успешной доставке.  <br/> |[T_THEME_COLOR_SEARCHURL]  <br/> |
|Hyperlink  <br/> |Цвет текста гиперссылок.  <br/> |[T_THEME_COLOR_HYPERLINK]  <br/> |
|HyperlinkFollowed  <br/> |Цвет текста просмотренных гиперссылок.  <br/> |[T_THEME_COLOR_HYPERLINKFOLLOWED]  <br/> |
|HyperlinkActive  <br/> |Цвет гиперссылки при нажатии.  <br/> |[T_THEME_COLOR_HYPERLINKACTIVE]  <br/> |
|CommandLinks  <br/> |Большие ссылки на команды, которые из-за своего размера должны быть немного светлее основного текста.  <br/> |[T_THEME_COLOR_COMMANDLINKS]  <br/> |
|CommandLinksSecondary  <br/> |Цвет текста более коротких ссылок на команды, который должен быть насыщеннее, чтобы выделяться на фоне остального текста.  <br/> |[T_THEME_COLOR_COMMANDLINKSSECONDARY]  <br/> |
|CommandLinksHover  <br/> |Цвет ссылки на команду при наведении на нее курсора мыши.  <br/> |[T_THEME_COLOR_COMMANDLINKSHOVER]  <br/> |
|CommandLinksPressed  <br/> |Цвет ссылки на команду при нажатии на нее.  <br/> |[T_THEME_COLOR_COMMANDLINKSPRESSED]  <br/> |
|CommandLinksDisabled  <br/> |Цвет отключенной ссылки на команду.  <br/> |[T_THEME_COLOR_COMMANDLINKSDISABLED]  <br/> |
|BackgroundOverlay  <br/> |Основной цвет фона, видимый между необязательным фоновым изображением и содержимым страницы.  <br/> |[T_THEME_COLOR_BACKGROUNDOVERLAY]  <br/> |
|DisabledBackground  <br/> |Фон для отключенных элементов, таких как элементы управления браузером, например поле ввода или поле выбора, за исключением кнопок.  <br/> |[T_THEME_COLOR_DISABLEDBACKGROUND]  <br/> |
|PageBackground  <br/> |Цвет фона страницы, который виден за необязательным фоновым изображением.  <br/> |[T_THEME_COLOR_PAGEBACKGROUND]  <br/> |
|HeaderBackground  <br/> |Цвет фона области верхнего колонтитула страницы.  <br/> |[T_THEME_COLOR_HEADERBACKGROUND]  <br/> |
|FooterBackground  <br/> |Цвет фона области нижнего колонтитула страницы.  <br/> |[T_THEME_COLOR_FOOTERBACKGROUND]  <br/> |
|SelectionBackground  <br/> |Цвет фона выбранных элементов списка и пунктов раскрывающегося меню.  <br/> |[T_THEME_COLOR_SELECTIONBACKGROUND]  <br/> |
|HoverBackground  <br/> |Цвет фона элементов списка и пунктов раскрывающегося меню при наведении на них курсора мыши.  <br/> |[T_THEME_COLOR_HOVERBACKGROUND]  <br/> |
|RowAccent  <br/> |Контрастная левая граница выбранных элементов списка.  <br/> |[T_THEME_COLOR_ROWACCENT]  <br/> |
|StrongLines  <br/> |Границы элементов управления браузером при наведении на них курсора мыши.  <br/> |[T_THEME_COLOR_STRONGLINES]  <br/> |
|Lines  <br/> |Границы элементов управления браузером.  <br/> |[T_THEME_COLOR_LINES]  <br/> |
|SubtleLines  <br/> |Слабо выделенный цвет границы, например линии сетки для встроенной правки.  <br/> |[T_THEME_COLOR_SUBTLELINES]  <br/> |
|DisabledLines  <br/> |Цвет границ для элементов управления браузером, таких как поля ввода и поля выбора.  <br/> |[T_THEME_COLOR_DISABLEDLINES]  <br/> |
|AccentLines  <br/> |Цвет границы фокуса для выбранных элементов управления браузером.  <br/> |[T_THEME_COLOR_ACCENTLINES]  <br/> |
|DialogBorder  <br/> |Цвет границы диалогового окна.  <br/> |[T_THEME_COLOR_DIALOGBORDER]  <br/> |
|Навигация  <br/> |Цвет текста элементов горизонтальной и вертикальной панелей навигации.  <br/> |[T_THEME_COLOR_NAVIGATION]  <br/> |
|NavigationAccent  <br/> |Цвет текста элемента горизонтальной панели навигации.  <br/> |[T_THEME_COLOR_NAVIGATIONACCENT]  <br/> |
|NavigationHover  <br/> |Цвет текста панели навигации при наведении на него курсора мыши. Применяется к верхней панели навигации и панели быстрого запуска в горизонтальном режиме.  <br/> |[T_THEME_COLOR_NAVIGATIONHOVER]  <br/> |
|NavigationPressed  <br/> |Цвет текста элемента панели навигации при его нажатии. Применяется к верхней панели навигации и панели быстрого запуска в горизонтальном режиме.  <br/> |[T_THEME_COLOR_NAVIGATIONPRESSED]  <br/> |
|NavigationHoverBackground  <br/> |Цвет фона элементов панели быстрого доступа в вертикальном режиме при наведении курсора мыши на элемент панели навигации.  <br/> |[T_THEME_COLOR_NAVIGATIONHOVERBACKGROUND]  <br/> |
|NavigationSelectedBackground  <br/> |Цвет фона элементов панели быстрого доступа в вертикальном режиме после выбора элемента панели навигации.  <br/> |[T_THEME_COLOR_NAVIGATIONSELECTEDBACKGROUND]  <br/> |
|EmphasisText  <br/> |Цвет текста, появляющегося поверх акцентного фона.  <br/> |[T_THEME_COLOR_EMPHASISTEXT]  <br/> |
|EmphasisBackground  <br/> |Контрастный цвет фона, который появляется позади акцентного текста.  <br/> |[T_THEME_COLOR_EMPHASISBACKGROUND]  <br/> |
|EmphasisHoverBackground  <br/> |Цвет фона при наведении курсора мыши для элементов, расположенных на акцентном фоне.  <br/> |[T_THEME_COLOR_EMPHASISHOVERBACKGROUND]  <br/> |
|EmphasisBorder  <br/> |Цвет границы элементов, расположенных на акцентном фоне.  <br/> |[T_THEME_COLOR_EMPHASISBORDER]  <br/> |
|EmphasisHoverBorder  <br/> |Цвет границы при наведении курсора мыши для элементов, расположенных на акцентном фоне.  <br/> |[T_THEME_COLOR_EMPHASISHOVERBORDER]  <br/> |
|SubtleEmphasisText  <br/> |Текст, который появляется поверх слабо выделенного акцентного фона.  <br/> |[T_THEME_COLOR_SUBTLEEMPHASISTEXT]  <br/> |
|SubtleEmphasisCommandLinks  <br/> |Цвет ссылки на команду для ссылок, появляющихся поверх слабо выделенного акцентного фона.  <br/> |[T_THEME_COLOR_SUBTLEEMPHASISCOMMANDLINKS]  <br/> |
|SubtleEmphasisBackground  <br/> |Фон, поверх которого появляется слабо выделенный акцентный текст.  <br/> |[T_THEME_COLOR_SUBTLEEMPHASISBACKGROUND]  <br/> |
|TopBarText  <br/> |Цвет текста и глифа для приветственного меню, значков панели быстрого доступа и закрытых вкладок на ленте.  <br/> |[T_THEME_COLOR_TOPBARTEXT]  <br/> |
|TopBarBackground  <br/> |Цвет фона верхней панели, видимой под панелью иерархической навигации или справа от нее.  <br/> |[T_THEME_COLOR_TOPBARBACKGROUND]  <br/> |
|TopBarHoverText  <br/> |Цвет текста и глифа для приветственного меню, значков панели быстрого доступа и закрытых вкладок на ленте при наведении на них курсора мыши.  <br/> |[T_THEME_COLOR_TOPBARHOVERTEXT]  <br/> |
|TopBarPressedText  <br/> |Цвет текста и глифа для приветственного меню, значков панели быстрого доступа и закрытых вкладок на ленте при нажатии на них.  <br/> |[T_THEME_COLOR_TOPBARPRESSEDTEXT]  <br/> |
|HeaderText  <br/> |Цвет основного текста для любого элемента в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERTEXT]  <br/> |
|HeaderSubtleText  <br/> |Текст подсказки для поля поиска, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERSUBTLETEXT]  <br/> |
|HeaderDisableText  <br/> |Текст отключенного поля поиска, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERDISABLETEXT]  <br/> |
|HeaderNavigationText  <br/> |Цвет основного текста навигационных ссылок в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONTEXT]  <br/> |
|HeaderNavigationHoverText  <br/> |Цвет текста навигационных ссылок в области верхнего колонтитула при наведении на них курсора мыши.  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONHOVERTEXT]  <br/> |
|HeaderNavigationPressedText  <br/> |Цвет текста навигационных ссылок в области верхнего колонтитула при выборе ссылки.  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONPRESSEDTEXT]  <br/> |
|HeaderNavigationSelectedText  <br/> |Цвет текста навигационных ссылок в области верхнего колонтитула, когда ссылка уже выбрана.  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONSELECTEDTEXT]  <br/> |
|HeaderLines  <br/> |Линии поля поиска, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERLINES]  <br/> |
|HeaderStrongLines  <br/> |Линии поля поиска, расположенного в области верхнего колонтитула, при наведении курсора мыши.  <br/> |[T_THEME_COLOR_HEADERSTRONGLINES]  <br/> |
|HeaderAccentLines  <br/> |Линии выделенного поля поиска, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERACCENTLINES]  <br/> |
|HeaderSublteLines  <br/> |Слабо выделенные линии, находящиеся внутри области верхнего колонтитула (не применяется в CSS по умолчанию).  <br/> |[T_THEME_COLOR_HEADERSUBTLELINES]  <br/> |
|HeaderDisabledLines  <br/> |Линии отключенного поля поиска, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERDISABLEDLINES]  <br/> |
|HeaderDisabledBackground  <br/> |Фон отключенного поля поиска, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERDISABLEDBACKGROUND]  <br/> |
|HeaderFlyoutBorder  <br/> |Граница раскрывающегося меню из области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERFLYOUTBORDER]  <br/> |
|HeaderSiteTitle  <br/> |Цвет текста названия сайта, расположенного в области верхнего колонтитула.  <br/> |[T_THEME_COLOR_HEADERSITETITLE]  <br/> |
|SuiteBarBackground  <br/> |Цвет фона панели иерархической навигации.  <br/> |[T_THEME_COLOR_SUITEBARBACKGROUND]  <br/> |
|SuiteBarHoverBackground  <br/> |Цвет фона панели иерархической навигации при наведении курсора мыши.  <br/> |[T_THEME_COLOR_SUITEBARHOVERBACKGROUND]  <br/> |
|SuiteBarText  <br/> |Цвет текста и глифа для элементов панели иерархической навигации.  <br/> |[T_THEME_COLOR_SUITEBARTEXT]  <br/> |
|SuiteBarDisabledText  <br/> |Цвет текста и глифа для отключенных элементов панели иерархической навигации (не используется в CSS по умолчанию).  <br/> |[T_THEME_COLOR_SUITEBARDISABLEDTEXT]  <br/> |
|ButtonText  <br/> |Цвет текста кнопок.  <br/> |[T_THEME_COLOR_BUTTONTEXT]  <br/> |
|ButtonDisabledText  <br/> |Цвет текста отключенных кнопок.  <br/> |[T_THEME_COLOR_BUTTONDISABLEDTEXT]  <br/> |
|ButtonBackground  <br/> |Цвет фона кнопок.  <br/> |[T_THEME_COLOR_BUTTONBACKGROUND]  <br/> |
|ButtonHoverBackground  <br/> |Цвет фона кнопок при наведении курсора мыши.  <br/> |[T_THEME_COLOR_BUTTONHOVERBACKGROUND]  <br/> |
|ButtonPressedBackground  <br/> |Цвет фона кнопок при нажатии.  <br/> |[T_THEME_COLOR_BUTTONPRESSEDBACKGROUND]  <br/> |
|ButtonDisabledBackground  <br/> |Цвет фона отключенных кнопок.  <br/> |[T_THEME_COLOR_BUTTONDISABLEDBACKGROUND]  <br/> |
|ButtonBorder  <br/> |Цвет границы кнопок.  <br/> |[T_THEME_COLOR_BUTTONBORDER]  <br/> |
|ButtonHoverBorder  <br/> |Цвет границы кнопок при наведении курсора мыши.  <br/> |[T_THEME_COLOR_BUTTONHOVERBORDER]  <br/> |
|ButtonPressedBorder  <br/> |Цвет границы кнопок при нажатии.  <br/> |[T_THEME_COLOR_BUTTONPRESSEDBORDER]  <br/> |
|ButtonDisabledBorder  <br/> |Цвет границы отключенных кнопок.  <br/> |[T_THEME_COLOR_BUTTONDISABLEDBORDER]  <br/> |
|ButtonGlyph  <br/> |Цвет глифа на кнопке.  <br/> |[T_THEME_COLOR_BUTTONGLYPH]  <br/> |
|ButtonGlyphActive  <br/> |Цвет глифа на кнопке при наведении курсора мыши.  <br/> |[T_THEME_COLOR_BUTTONGLYPHACTIVE]  <br/> |
|ButtonGlyphDisabled  <br/> |Цвет глифа для неактивной кнопки.  <br/> |[T_THEME_COLOR_BUTTONGLYPHDISABLED]  <br/> |
|TileText  <br/> |Текст, отображаемый в верхней части наложения фона плитки.  <br/> |[T_THEME_COLOR_TILETEXT]  <br/> |
|TileBackgroundOverlay  <br/> |Цвет наложения фона плиток.  <br/> |[T_THEME_COLOR_TILEBACKGROUNDOVERLAY]  <br/> |
|ContentAccent1  <br/> |Первый акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).  <br/> |[T_THEME_COLOR_CONTENTACCENT1]  <br/> |
|ContentAccent2  <br/> |Второй акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).  <br/> |[T_THEME_COLOR_CONTENTACCENT2]  <br/> |
|ContentAccent3  <br/> |Третий акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).  <br/> |[T_THEME_COLOR_CONTENTACCENT3]  <br/> |
|ContentAccent4  <br/> |Четвертый акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).  <br/> |[T_THEME_COLOR_CONTENTACCENT4]  <br/> |
|ContentAccent5  <br/> |Пятый акцентный цвет, доступный пользователю в средстве выбора цвета в редакторе форматированного текста.  <br/> |[T_THEME_COLOR_CONTENTACCENT5]  <br/> |
|ContentAccent6  <br/> |Шестой акцентный цвет, доступный пользователю в средстве выбора цвета (редакторе форматированного текста).  <br/> |[T_THEME_COLOR_CONTENTACCENT6]  <br/> |
   

## <a name="font-schemes"></a>Схемы шрифтов
<a name="font"> </a>

Шрифты указываются в схеме шрифтов (файле SPFONT) и файле предварительного просмотра эталонной страницы (файле PREVIEW) данного сайта SharePoint. Схема шрифтов определяет шрифты для четырех областей: названия, панели навигации, заголовка и основного текста. SharePoint содержит семь схем шрифтов. Вы также можете создавать дополнительные схемы. Файлы схем шрифтов хранятся во вложенной папке **15** коллекции тем корневого сайта в семействе веб-сайтов (http:// _ИмяСемействаСайтов_/_catalogs/theme/15/). Чтобы получить доступ к коллекции тем из пользовательского интерфейса SharePoint, в разделе **Коллекция веб-дизайнера** на странице **Параметры сайта** щелкните ссылку **Темы**, а затем выберите папку **15**.
  
    
    
Ниже приводится пример формата для файла SPFONT.
  
    
    



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

В файле SPFONT заменяются следующие заполнители:
  
    
    

-  _FontSchemeName_ - имя схемы шрифтов.
    
  
-  _Slot1_ - имя слота шрифта, который используется в качестве первого блока значка шрифта в средстве выбора схемы шрифтов, доступном в мастере **изменения оформления**.
    
  
-  _Slot2_ - имя слота шрифта, который используется в качестве второго блока значка шрифта в средстве выбора схемы шрифтов, доступном в мастере **изменения оформления**.
    
  
-  _FontSlotName_ - имя определяемого слота шрифта, например название.
    
  
-  _LatinScriptFont_ - шрифт, используемый для латинского письма. Он также выступает в качестве резервного, т. е. применяется для языков, для которых не установлен определенный шрифт в схеме шрифтов.
    
    > **Примечание.** Вам необходимо указать дополнительные сведения для использования веб-шрифтов в шрифтовой схеме. Дополнительные сведения см. в разделе [Веб-шрифты](#webFont) этой статьи.
-  _EAScriptFont_ - это шрифт, который используется для сценариев языков Восточной Азии. Элемент **<s:ea>** не используется в SharePoint в настоящее время, но этот элемент **<s:ea>** требуется в схеме шрифтов.
    
  
-  _CSFont_ - это шрифт, используемый в сложных сценариях. Элемент **<s:cs>** не используется в SharePoint в настоящее время, но этот элемент **<s:cs>** требуется в схеме шрифтов.
    
  
-  _Language_ - это набор знаков.
    
  
-  _ScriptFont_ - это шрифт, который используется для определенного набора знаков.
    
  
Ниже приводится пример части файла SPFONT.
  
    
    



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

SharePoint обеспечивает поддержку веб-шрифтов. Чтобы использовать их в своей схеме шрифтов, необходимо предоставить дополнительные сведения. Подробнее об этом можно узнать в разделе  [Веб-шрифты](#webFont) этой статьи.
  
    
    

### <a name="web-safe-fonts"></a>Шрифты, соответствующие веб-палитре
<a name="websafeFont"> </a>

Шрифты, соответствующие веб-палитре, представляют собой набор широко используемых шрифтов, которые по умолчанию доступны на большинстве устройств. Чтобы указать шрифт, соответствующий веб-палитре, в схеме шрифтов, включите его имя в атрибут **typeface** слота шрифта. Ниже приводится пример использования шрифта, соответствующего веб-палитре, в схеме шрифтов.
  
    
    

```xml

<s:fontSlot name="title">
  <s:latin typeface="Georgia"/>
???
</s:fontSlot>
```


### <a name="web-fonts"></a>Веб-шрифты
<a name="webFont"> </a>

Веб-шрифты - это шрифты, доступные в Интернете. Когда пользователь просматривает сайт, на котором используются веб-шрифты, веб-браузер скачивает необходимые файлы шрифтов вместе со всей страницей. Чтобы использовать веб-шрифт, необходимо указать URL-адрес ваших файлов шрифтов в четырех форматах (для обеспечения поддержки различными браузерами), а также маленький и большой эскизы, которые используются средством выбора схем шрифтов для определения имен шрифтов.
  
    
    
В приведенном ниже примере указаны сведения, необходимые для использования веб-шрифта в элементе **<s:latin>**.
  
    
    



```xml

<s:latin typeface="FontName"
  eotsrc="EotFile"
  woffsrc="WoffFile"
  ttfsrc="TtfFile"
  svgsrc="SvgFile"
  largeimgsrc="LargeImgFile"
  smallimgsrc="SmallImgFile" />

```

В этом примере использования веб-шрифта заменяются следующие заполнители:
  
    
    

-  _FontName_ - имя веб-шрифта.
    
  
-  _EotFile_ - относительный URL-адрес файла внедряемых шрифтов Open Type.
    
  
-  _WoffFile_ - относительный URL-адрес файла шрифта WOFF (Web Open Font Format).
    
  
-  _TtfFile_ - относительный URL-адрес файла шрифта TrueType.
    
  
-  _SvgFile_ - относительный URL-адрес файла шрифта для масштабируемого векторного рисунка (SVG).
    
  
-  _LargeImgFile_ - относительный URL-адрес большого эскиза, используемого в средстве выбора схемы шрифтов.
    
  
-  _SmallImgFile_ - относительный URL-адрес маленького эскиза, используемый в средстве выбора схемы шрифтов.
    
  

### <a name="font-slots"></a>Слоты шрифтов
<a name="fontSlot"> </a>

В таблице 1 представлены доступные слоты шрифтов, а также области их применения на странице.
  
    
    

**Таблица 1. Слоты шрифтов**


|**Имя слота шрифта**|**Описание**|
|:-----|:-----|
|title  <br/> |Используется в названии страницы.  <br/> |
|перемещение  <br/> |Используется для элементов горизонтальной и вертикальной панели навигации на странице.  <br/> |
|large-heading  <br/> |Используется в заголовках H1.  <br/> |
|heading  <br/> |Используется для заголовков H2 и H3, названий веб-частей, диалоговых окон и выносок.  <br/> |
|small-heading  <br/> |Используется для заголовков H4.  <br/> |
|large-body  <br/> |Используется для крупного основного текста размером 15 и 19 пикселей.  <br/> |
|body  <br/> |Основной шрифт, который используется для остального текста на странице.  <br/> |
   

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Общие сведения о темах для SharePoint](themes-overview-for-sharepoint.md)
    
  
-  [Инструкции. Развертывание пользовательской темы в SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [Обновление пользовательских тем и CSS для SharePoint](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [Фирменная символика и конструкция возможности дизайнер SharePoint](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

  
    
    

