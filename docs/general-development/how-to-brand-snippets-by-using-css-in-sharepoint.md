---
title: "Фрагменты кода марки с помощью CSS в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18d07b6-1a6b-4589-a65c-932b67cef595
ms.openlocfilehash: 4ed891c06956c4d2ff79cd681b81a3869a03cc3c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="brand-snippets-by-using-css-in-sharepoint"></a>Фрагменты кода марки с помощью CSS в SharePoint

Применять стиль фрагмент, переопределить стилей по умолчанию с помощью настраиваемого CSS. Идентификаторы CSS и значения выбора элементов можно использовать для переопределения стилей по умолчанию, применяемые к элементам, или можно использовать редактор HTML или средства, такие как средства разработчика F12 в Internet Explorer для идентификации и переопределения стили установленный по умолчанию.

## <a name="introduction-to-styling-snippets-with-css"></a>Общие сведения о фрагменты стилей с помощью CSS
<a name="Introduction"> </a>

Преобразование HTML-главной страницы или создать макет страницы HTML, можно выполнить предварительный просмотр страницы в режиме предварительного просмотра дизайнер на сервере. На странице просмотра можно перейдите к коллекция фрагментов кода и затем скопируйте фрагментов кода HTML-файл. Фрагмент  это представление HTML управления SharePoint, такие как элемент управления навигации верхнего уровня или поле поиска.
  
    
    
После скопируйте фрагмент в HTML-файл в подключенный диск и затем сохранить изменения, можно обновить Предварительный просмотр HTML-файл, чтобы увидеть, как элемент управления отображается на сервере. Фрагменты кода содержат разметка, которая предоставляет предварительного просмотра во время разработки в редакторе HTML выбора, но не следует изменить Эта разметка, так как он доступен только для чтения и не влияет на порядок отображения элемента управления на сервере. В то же время, предварительного просмотра на сервере показывает preview надежностью с помощью динамических данных, если доступен  например, элемент управления навигации будет показывать текущей структуры навигации веб-узла с помощью динамических данных из источника данных, таких как банк терминов SharePoint для управляемой навигации.
  
> [!NOTE]
> Дополнительные сведения о сопоставлении сетевого диска можно [как: сопоставление сетевого диска коллекции SharePoint главных страниц](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md). 
  
    
    

По умолчанию фрагменты наследуют свои стили из таблицы стилей SharePoint, такие как corev15.css. Чтобы стиль фрагмент, необходимо переопределить эти стили по умолчанию с помощью настраиваемого CSS. Для этого можно выполнить следующие действия.
  
    
    

- Использование CSS идентификаторы и значения выбора элементов полностью переопределить стили по умолчанию, применяемые к выбранные элементы.
    
  
- Воспользуйтесь средством браузере, например средства разработчика F12 в Internet Explorer для проверки стилей по умолчанию в режиме предварительного просмотра в диспетчере оформления на сервере и затем определите определенные стили для переопределения.
    
  
- Используйте возможности редактора HTML для проверки стилей по умолчанию в режиме предварительного просмотра только для чтения фрагмент и определите определенные стили для переопределения. 
    
  
Для определения стилей по умолчанию с помощью средств разработки в браузере Internet Explorer, следует использовать preview на сервере в диспетчере оформления для просмотра главной страницы HTML или макет страницы, нажмите клавишу **F12** для запуска средства разработчика, выберите меню « **Поиск** », а затем нажмите **выбрать элемент, нажмите кнопку**. Это позволяет щелкните элементы на странице и посмотрите, какой точно стили, чтобы переопределить, добавив CSS для пользовательской таблицы стилей, HTML главной страницы или страницы макета ссылки на.
  
    
    
Таблицы стилей SharePoint по умолчанию содержат множество стили, которые можно сделать его сложного для идентификации определенных стилей. В качестве альтернативы для средства на основе браузера и в зависимости от редактора HTML можно проще копирование фрагмента коллекция фрагментов кода в HTML-файл и затем использовать редактор HTML для определения стилей. В коллекции фрагмент при выборе **обновления** и нажмите кнопку **Копировать в буфер обмена**, фрагмент содержит HTML-код для фрагмента. После копирования фрагмента в HTML-файл, можно проверить стилей, используемых в предварительной версии только для чтения, содержащихся в фрагменте. Таким образом, синтаксический анализ небольшому стилей по умолчанию.
  
    
    
В зависимости от фрагмента и степень настройки можно полностью переопределить все стили по умолчанию, вместо выбор стилей установленный по умолчанию для переопределения с помощью CSS идентификаторы и значения выбора элементов. Следующий пример демонстрирует этот метод используется для применение пользовательских стилей к фрагменту верхней панели навигации.
  
    
    

## <a name="example-style-the-top-navigation-snippet"></a>Пример: Стиль фрагмент верхней панели навигации
<a name="Example"> </a>

В верхней панели навигации фрагменте — это один из наиболее часто используемые фрагменты кода, поэтому он также является одним из наиболее часто фирменной символики фрагменты кода. На сайте SharePoint можно выбрать параметр для использования управляемой навигации, чтобы банка терминов, становится источник данных для фрагмента верхней панели навигации. Таким образом, можно использовать средство управления терминами хранилища в **Настройках сайта** для добавления или удаления терминам навигации и управления таксономии навигации, которая отображается по навигации в начало фрагмента.
  
    
    
В этом примере на сайте используется управляемая навигация, элемент управления навигации верхнего уровня извлекает его записи из банка терминов. Существует один уровень всплывающие окна, отображаются при наведении указателя на термин навигации верхнего уровня, например, **компьютеры**. В этом разделе показано, как эти настраиваемые стили переопределить стилей SharePoint по умолчанию.
  
    
    

### <a name="sample-1-navigation-div-from-the-html-mockup-file"></a>Пример 1: Навигации \<div\> из HTML-файл макета

Прежде чем использовать Дизайнер, при разработке макета HTML для главной страницы, скорее всего используется HTML и CSS для разработки элемент функциональным верхней панели навигации. В этом примере HTML используется базовая структура для верхней панели навигации: ** \<div\> ** идентификатор и имя класса, в список для записи навигации верхнего уровня и вложенных списков для каждого подменю всплывающего в элемент.
  
    
    

```HTML

<div id="navigation" class="msax-Navigation">
   <ul>
      <li><a href="#">Cameras</a>
         <ul>
            <li><a href="#">Camcorders</a></li>
            <li><a href="#">Digital cameras</a></li>
            <li><a href="#">Disposable cameras</a></li>
            <li><a href="#">Film cameras</a></li>
         </ul>
      </li>
      <li><a href="#">Computers</a>
         <ul>
            <li><a href="#">Desktops</a></li>
            <li><a href="#">Laptops</a></li>
            <li><a href="#">Netbooks</a></li>
            <li><a href="#">Tablets</a></li>
         </ul>
      </li>
      <li><a href="#">Media</a>
         <ul>
            <li><a href="#">Movies</a></li>
            <li><a href="#">Music</a></li>
            <li><a href="#">TV shows </a></li>
            <li><a href="#">Video games </a></li>
         </ul>
      </li>
      <li></li>
   </ul>
</div>

```


### <a name="sample-2-navigation-div-styled-with-custom-css"></a>Пример 2: Навигации \<div\> со стилем с помощью настраиваемого CSS

Чтобы переопределить значение по умолчанию стилей SharePoint в макете HTML-файле включают стандартной связи в CSS-файл `(<link rel="stylesheet" type="text/css" href="URLtoYourCustomCSSFile"/>`) непосредственно перед закрывающим тегом ** \</head\> ** тег.
  
    
    
В этих примерах HTML и CSS Обратите внимание на следующее:
  
    
    

- Записи навигации со стилями, используя формат `.msax-Navigation ul li` не напрямую, чтобы применять классы ** \<ul\> ** или ** \<li\> ** тегов.
    
  
- Стили используется синтаксис `.msax-Navigation ul li` вместо `.msax-Navigation ul>li` так как фрагмент разметки может содержать промежуточных ** \<div\> ** между выбранные элементы.
    
  
- Макете HTML-код содержит пустой ** \<li\>\</li\> ** элемента в качестве последней записи верхнего уровня ** \<ul\>**. Это, поскольку с включенным управляемой навигации, SharePoint добавляет команду **Изменить связи** как последний элемент навигации верхнего уровня и окончательный сайта обычно не требуется отображать этот параметр. CSS примере используются `.msax-Navigation ul li:last-child` выберите эту запись и задайте отображаемое значение `none`. Пустой ** \<li\>\</li\> ** элемент в HTML-файл является временной заменой запись **Изменить связи** по умолчанию. Необходимо учитывать этом последнем ** \<li\> ** элемент при использовании сайтом управляемой навигации и таблицы стилей CSS используются какие-либо `li:last-child` селекторы.
    
  



```HTML

.msax-Navigation {
margin: 10px 0px; top: 0px; position: relative;
z-index:200;
}
.msax-Navigation a {
margin: 0px; padding: 0px; border: 0px currentColor;
}
.msax-Navigation ul {
list-style: none; margin: 0px; padding: 0px; font-size: 16px; z-index:200;
}
.msax-Navigation ul li {
padding: 10px; display: inline-block; position: relative; z-index:200;
}
.msax-Navigation ul li:first-child {
margin: 0px;
}
.msax-Navigation ul li:last-child {
margin: 0px; padding: 0px; display: none;
}
.msax-Navigation ul li a.selected, .msax-Navigation ul li.selected {
background-color: rgb(58,60,62) !important;
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a {
width: 100%; color: rgb(58,60,62); font-size: 16px;
}
.msax-Navigation ul li:hover {
background-color: rgb(58,60,62);
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a:hover {
text-decoration: none;
color:rgb(255,255,255) !important;
}
.msax-Navigation li ul {
left: 0px; top: 35px; display: none; position: absolute; min-width: 100px; box-shadow: 5px 5px 10px 0px rgb(0,0,0); background-color: rgb(58,60,62);
}
.msax-Navigation li:hover ul {
display: block; z-index: 150;
}
.msax-Navigation li li {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li:last-child {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li a {
width: 100%; padding-left: 10px; display: block; color:rgb(255,255,255) !important;
}
.msax-Navigation li li:hover {
background-color: rgb(120, 120, 120);
}

```


### <a name="sample-3-read-only-preview-of-the-top-navigation-snippet"></a>Пример 3: Предварительный просмотр только для чтения фрагмента верхней панели навигации

После того как настраиваемые стили реализованы в вашей макете HTML и у вас есть элемент функциональным верхней панели навигации, выполните обычные действия.
  
    
    

1. Сопоставление сетевого диска.
    
  
2. Отправьте файлы проекта.
    
  
3. Преобразование HTML-файла в эталонную страницу
    
  
4. Предварительный просмотр и устранения неполадок.
    
  
5. Добавьте фрагмент верхней панели навигации на главную страницу HTML с помощью коллекция фрагментов кода.
    
  
Коллекция фрагментов кода при настройке свойства фрагмента верхней панели навигации, обратите внимание на следующее:
  
    
    

- В разделе **важные** вверху не изменяйте свойством **CssClass**.
    
  
- Не вносите никаких изменений в свойства под заголовком **AjaxDelta**, так как эти свойства связаны с MDS свойства, которые SharePoint использует для преобразования фрагмент HTML в соответствующем фрагменте ASP.NET. Это относится к любой фрагмент не только фрагмент верхней панели навигации.
    
  
- Если вы планируете переопределить стилей SharePoint по умолчанию, в коллекция фрагментов кода, в разделе **Behavior** **AspMenu** (может быть более одного раздела **Behavior** Если фрагмент содержит более одного элемента управления, такие как замещаемого элемента управления), присвойте **ClientIDMode** **Static**. Если оставить значение по умолчанию **ClientIDMode** установки, **Inherit**, применяемые CSS фрагмент классы будет изменяться в зависимости от порядок использования фрагменты на странице. Дополнительные сведения о **ClientIDMode** [Control.ClientIDMode свойство](http://msdn.microsoft.com/en-us/library/system.web.ui.control.clientidmode.aspx)см.
    
    Например по умолчанию, элемент управления верхней панели навигации использует атрибуты идентификатор SharePoint по умолчанию, такие как **zz5_TopNavigationMenu** и **zz6_RootAspMenu**. Изменяя **ClientIDMode** **Static**, можно сделать возможным для использования этих кодов по умолчанию в качестве селекторы в свои собственные CSS для переопределения стилей SharePoint по умолчанию.
    
  
- Некоторые свойства уже настроена для сделать фирменной символики в верхней панели навигации фрагменте удобства, устраняя поведение динамических CSS и JavaScript по умолчанию  например, по умолчанию **UseSimpleRendering** задано значение **True**, **MaximumDynamicDisplayLevels** задано значение **0**. Дополнительные сведения о конкретных свойствах фрагмент верхней панели навигации можно  [AspMenu свойства](http://msdn.microsoft.com/en-us/library/ms412476.aspx) и [Свойства меню](http://msdn.microsoft.com/en-us/library/282668a1.aspx).
    
  
После настройки фрагмента верхней панели навигации в коллекция фрагментов кода выберите **обновления**и нажмите кнопку **Копировать в буфер обмена**. На главной странице HTML, удалите содержимое панели навигации `<div id="navigation" class="msax-Navigation">` , который содержит элемент управления макета (удалить только содержимое ** \<div\> ** тега, не ** \<div\> ** тега самого) и затем скопируйте фрагмент в панели навигации ** \<div\>**. При необходимости изменить положение панели навигации ** \<div\>**, обычно непосредственно после начала `<div id="s4-bodyContainer">` тега, но перед ** \<div\> ** содержащий `PlaceHolderMain`.
  
    
    
Для удобного сравнения с HTML-код навигации ** \<div\> ** выше, следующий пример содержит структуру переходов ** \<div\> ** часть фрагмента верхней панели навигации. Обратите внимание на то, что это не всей фрагмента.
  
    
    



```HTML

<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
     <ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
          <li class="static">
          <a accesskey="1" class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Cameras</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/camcorders" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Camcorders</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/digital-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Digital cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/disposable-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Disposable cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/film-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Film cameras</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Computers</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/desktops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Desktops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/laptops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Laptops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/netbooks" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Netbooks</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/tablets" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Tablets</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Media</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/movies" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Movies</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/music" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Music</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/tv-shows" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">TV shows</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/video-games" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Video games</span></span></a></li>
          </ul>
          </li>
          <li class="static ms-verticalAlignTop ms-listMenu-editLink ms-navedit-editArea">
          <span id="zz7_TopNavigationMenu_NavMenu_Edit" class="ms-navedit-editSpan">
          <a id="zz7_TopNavigationMenu_NavMenu_EditLinks" class="ms-navedit-editLinksText" href="#" onclick="g_QuickLaunchMenu = null; EnsureScriptParams('quicklaunch.js', 'QuickLaunchInitEditMode', 'zz7_TopNavigationMenu', 2, 0, 0, ''); cancelDefault(event); return false;">
          <span class="ms-displayInlineBlock">
          <span class="ms-navedit-editLinksIconWrapper ms-verticalAlignMiddle">
          <img class="ms-navedit-editLinksIcon" src="/_layouts/15/images/spcommon.png?rev=23" /></span><span class="ms-metadata ms-verticalAlignMiddle">Edit Links</span></span></a><span id="zz7_TopNavigationMenu_NavMenu_Loading" class="ms-navedit-menuLoading ms-hide"><a id="zz7_TopNavigationMenu_NavMenu_GearsLink" href="#" onclick="HideGears(); return false;" title="This animation indicates the operation is in progress. Click to remove this animated image."><img id="zz7_TopNavigationMenu_NavMenu_GearsImage" src="/_layouts/15/images/loadingcirclests16.gif?rev=23" /></a></span><div id="zz7_TopNavigationMenu_NavMenu_ErrorMsg" class="ms-navedit-errorMsg">
          </div>
          </span></li>
     </ul>
</div>

```

Вместо использования только настраиваемые стили, в некоторых случаях сценарий, где необходимо переопределить только определенный стиль. Например чтобы скрыть узел **Изменение ссылки**, можно создать настраиваемый стиль, который используется по умолчанию идентификатор **zz7_TopNavigationMenu_NavMenu_Edit**, чтобы задать параметры отображения `none`.
  
    
    

## <a name="see-also"></a>См. также
<a name="Additional"> </a>


-  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md)
    
  
-  [Обзор Дизайнера в SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Инструкции. Преобразование HTML-файла в эталонную страницу SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Разработка макета сайта в SharePoint](develop-the-site-design-in-sharepoint.md)
    
  

