---
title: "Фрагменты кода дизайнер SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 68caef4c-5941-4a88-b34b-f88122801cef
ms.openlocfilehash: 2c670d8fb7cd6ec3f293a3e5da9b75380005f598
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-design-manager-snippets"></a>Фрагменты кода дизайнер SharePoint
Фрагмент является представлением HTML компонентов SharePoint или элемента управления, например панели навигации или веб-части. С помощью коллекция фрагментов кода в диспетчере оформления, можно быстро добавить функциональные возможности SharePoint для главной страницы HTML или макет страницы.
## <a name="introduction-to-snippets-and-the-snippet-gallery"></a>Общие сведения о фрагменты кода и коллекция фрагментов кода
<a name="Introduction"> </a>

После преобразования главную страницу или создание макета страницы, у вас есть HTML-версии этой страницы. С помощью коллекция фрагментов кода можно быстро добавить определенных функций SharePoint, например поиска или навигации или каналов устройств для HTML-файла, связанного с главной странице или макету страницы. Коллекция фрагментов кода представляет собой страницу в диспетчере оформления которых можно:
  
    
    

- Выберите компонент SharePoint от тех, которые доступны на ленте.
    
  
- Настройка свойств для этого компонента.
    
  
- Предварительный просмотр внешнего вида в браузере.
    
  
- Скопируйте фрагмент кода HTML в буфер обмена, чтобы можно было вставить фрагмент в расположении в HTML-файл.
    
  
Коллекция фрагментов кода отображает различные параметры на ленте, в зависимости от того, редактировании главной странице или макету страницы  например, элементы управления навигацией, отображаются только для главных страниц и зоны веб-частей и элементов управления полей страницы, отображаются только для макетов страниц. Кроме того при изменении макета страницы полей страниц, доступных зависят от типа контента макета страницы, который требуется изменить.
  
    
    
После вставки фрагмента кода в HTML-файл, вы получаете разработки preview из HTML, представленные в примере. Также можно использовать preview на сервере в диспетчере оформления чтобы увидеть, как будет выглядеть элемент управления действующего сайта. Предварительный просмотр разработки может включать статические демонстрационных данных, но preview на сервере с помощью динамических данных, если он доступен. Например элемент управления навигации, которая отображает ссылки для перехода из набора терминов динамически отображать эти термины в предварительной версии на сервере, но предварительного просмотра во время разработки будет статический условия во время создания фрагмента. Динамических данных недоступен в предварительной версии на сервере для некоторых фрагменты кода, тем не менее, включая количество веб-частей. В этом случае preview на сервере может сказать **Предварительной версии недоступно**.
  
> [!NOTE]
> [!Примечание] Содержит фрагмент HTML-разметку, можно просмотреть во время разработки в редакторе HTML, но HTML-разметку содержатся в «запуск предварительного просмотра» и «предварительный просмотр плана» комментарии нельзя изменять так, как оно затрагивает только предварительного просмотра во время разработки, не как SharePoint воспроизводится в конечном счете фрагмента. Вместо этого стиля фрагмент кода, обычно необходимо определить и переопределения стилей SharePoint по умолчанию, которые применяются к фрагмента. 
  
    
    


  
    
    

## <a name="insert-a-snippet-from-the-snippet-gallery"></a>Вставить фрагмент кода из коллекции фрагмента
<a name="InsertSnippet"> </a>

Коллекция фрагментов кода отображает различные параметры в зависимости от файла, который требуется изменить. Например другой страницы макетов иметь различные наборы поля страниц, доступных для них. По этой причине для перехода к коллекция фрагментов кода, сначала нужно выбрать главную страницу или макет страницы для редактирования.
  
    
    

### <a name="to-insert-a-snippet"></a>Чтобы вставить фрагмент


1. Откройте свой сайт публикации.
    
  
2. Нажмите значок шестеренки "Параметры" в правом верхнем углу страницы, а затем выберите **Дизайнер**.
    
  
3. В диспетчере оформления на левой панели навигации слева выберите **Изменить главную страницу** или **Изменение макетов страниц**, в зависимости от того, какой тип файла требуется изменить.
    
  
4. Выберите имя главной страницы или макет страницы, который вы хотите добавить фрагменты кода для.
    
  
5. Чтобы открыть коллекцию фрагментов, выберите **Фрагменты** в правом верхнем углу страницы предварительного просмотра на стороне сервера.
    
  
6. На ленте перейдите на вкладку **Конструктор** выберите фрагмент, который нужно добавить на страницу.
    
    При выборе фрагмент коллекция фрагментов кода обновляются, чтобы на странице отображается предварительный просмотр фрагмента свойства, доступные для фрагмента и фрагмент кода HTML, который можно скопировать в главной страницы HTML или макет страницы.
    
  
7. В разделе **Об этом компоненте** в правой части коллекции фрагментов щелкните или выберите заголовок раздела, чтобы развернуть или свернуть группу свойств, а затем настройте все нужные настраиваемые параметры.
    
    В верхнем разделе с именем важные отображаются свойства, которые являются наиболее важные для основных целей фрагмента. Далее представлены ключевые свойства, которые необходимо изучить при использовании фрагмент.
    
    > [!NOTE]
    > [!Примечание] Если сетка свойств заголовка, который заканчивается на AjaxDelta, так как они применяются к элементам управления, связанные с минимальной загрузки стратегической, которое отключено главные страницы и макеты страниц, созданные через дизайнер следует игнорировать этих свойств. 

8. После настройки всех свойств выберите **обновление**. Обновляет Предварительный просмотр и фрагмент HTML в левой части страницы, чтобы разметка отражает пользовательских параметров. Всегда можно **сбросить** для возврата всех свойств к значениям по умолчанию.
    
  
9. В разделе **Фрагмент HTML** в левой части коллекции фрагментов выберите команду **Копировать в буфер обмена**.
    
  
10. В редакторе HTML откройте сопоставленный сетевой диск на своем компьютере, а затем откройте HTML-файл для эталонной страницы или макета, к которым добавляется фрагмент.
    
  
11. Вставьте фрагмент в том месте HTML-файла, где должна отображаться разметка.
    
    Каждый фрагмент содержит HTML-код, который предоставляет visual предварительной версии компонента и образец данных. Не следует изменять этот HTML-код для предварительного просмотра только для чтения внутри тегов **<!--PS>** и **<!--PE>**, поскольку эта разметка влияет на только во время разработки preview фрагмента, не фрагмента отображения действующего сайта.
    
  
12. Для просмотра на сервере фрагмент, сохраните файл HTML-код для синхронизации изменений в файле связанного ASP.NET и обновите на сервере предварительного просмотра в диспетчере оформления.
    
    В отличие от предварительного просмотра во время разработки предварительного просмотра на сервере показан элемент управления, как отобразить с помощью SharePoint.
    
  

## <a name="understand-the-markup-in-an-html-snippet"></a>Понимание разметки в фрагмента кода HTML
<a name="UnderstandMarkup"> </a>

Он содержит четыре основных раздела:
  
    
    

- **Заголовок** с начала теги **<div>** и **<!--CS>** (за исключением пользовательских ASP.NET фрагменты кода, которые не помещаются в тег **<div>** )
    
  
- **Разметка SharePoint**, где фрагменты заключены в **<!--MS>** начала и **<!--ME>** закрывающие теги
    
  
- **Предварительный просмотр HTML-код** внутри **<!--PS>** start и **<!--PE>** закрывающие теги
    
  
- **Нижний колонтитул** с закрывающие теги **<!--CE>** и **</div>**
    
  
Все разделы фрагмент, за исключением предварительного просмотра HTML, заключаются в HTML-код комментариев во избежание взаимодействия с помощью модели объектов документа (DOM) и существующего стилей. Фрагмент начинается с именем компонента и затем включает фактический разметки ASP.NET, предварительный просмотр HTML-код для отрисовки во время разработки и затем к концу тегов. Закомментированы разметка ASP.NET, но SharePoint Удаляет теги комментариев и используется эта разметка при HTML-файл синхронизируется с .master или .aspx файла. Если вы знаете ASP.NET, можно настроить этот разметки в фрагменте.
  
    
    
Пример: Вот разметка по умолчанию для изменения режима панели, просто контейнер, в котором условно отображаются другие содержимое и элементы управления.
  
    
    

### <a name="header"></a>Верхний колонтитул


```HTML

<div data-name="EditModePanelShowInEdit">
    <!--CS: Start Edit Mode Panel Snippet-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
```


### <a name="html-preview"></a>Предварительный просмотр HTML-код


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Edit Mode Panel Properties.
    
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="footer"></a>Нижний колонтитул


```HTML

<!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Edit Mode Panel Snippet-->
</div>
```

Ниже представлена разметка по умолчанию для навигации в начало фрагмента, которого является более сложным, поскольку в этом фрагменте содержит несколько различных элементов управления, с некоторыми вложенных в друг с другом, включая источник данных для терминов навигации, замещаемого элемента управления и заполнитель контента.
  
> [!NOTE]
> [!Примечание] Некоторые элементы управления, такие как заполнитель контента, содержат пустые теги предварительном HTML, так как этот элемент не требует визуальное представление на странице. 
  
    
    


### <a name="header"></a>Верхний колонтитул


```HTML

<div data-name="TopNavigationNoFlyoutWithStartNode">
<!--CS: Start Top Navigation Snippet-->    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<SharePoint:AjaxDelta ID="DeltaTopNavigation" BlockElement="true" CssClass="ms-displayInline ms-core-navigation ms-dialogHidden" runat="server">-->
```


### <a name="html-preview"></a>Предварительный просмотр HTML-код


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--MS:<SharePoint:DelegateControl runat="server" ControlId="TopNavigationDataSource" Id="topNavigationDelegate">-->
```


### <a name="html-preview"></a>Предварительный просмотр HTML-код


```HTML
<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<span style="display:none">
<table cellpadding="4" cellspacing="0" style="font:messagebox;color:buttontext;background-color:buttonface;border: solid 1px;border-top-color:buttonhighlight;border-left-color:buttonhighlight;border-bottom-color:buttonshadow;border-right-color:buttonshadow">
<tr><td nowrap="nowrap">
<span style="font-weight:bold">PortalSiteMapDataSource</span> - topSiteMap</td></tr><tr><td></td></tr></table></span>
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--MS:<Template_Controls>-->
<!--MS:<asp:SiteMapDataSource ShowStartingNode="True" SiteMapProvider="SPNavigationProvider" ID="topSiteMap" runat="server" StartingNodeUrl="sid:1002">-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--ME:</asp:SiteMapDataSource>-->
<!--ME:</Template_Controls>-->
<!--ME:</SharePoint:DelegateControl>--><a name="startNavigation"></a>
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--MS:<asp:ContentPlaceHolder ID="PlaceHolderTopNavBar" runat="server">-->
<!--MS:<SharePoint:AspMenu ID="TopNavigationMenu" runat="server" EnableViewState="false" DataSourceID="topSiteMap" AccessKey="&amp;#60;%$Resources:wss,navigation_accesskey%&amp;#62;" UseSimpleRendering="true" UseSeparateCss="false" Orientation="Horizontal" StaticDisplayLevels="2" AdjustForShowStartingNode="false" MaximumDynamicDisplayLevels="0" SkipLinkText="">-->
```


### <a name="html-preview"></a>Предварительный просмотр HTML-код


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<link rel="stylesheet" type="text/css" href="/_layouts/15/1033/styles/menu-21.css" />
<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
<ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
<li class="static">
<a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" tabindex="0" title="Default Publishing Site" href="/sites/PubSite/Pages/default.aspx" accesskey="1">
<span class="additional-background ms-navedit-flyoutArrow">
<span class="menu-item-text">Default Publishing Site</span></span></a></li></ul></div>
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--ME:</SharePoint:AspMenu>-->
<!--ME:</asp:ContentPlaceHolder>-->
```


### <a name="html-preview"></a>Предварительный просмотр HTML-код


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a>Разметка SharePoint


```HTML

<!--ME:</SharePoint:AjaxDelta>-->
```


### <a name="footer"></a>Нижний колонтитул


```HTML
<!--CE: End Top Navigation Snippet-->
</div>
```


### <a name="types-of-markup"></a>Типы разметки

Вот разбивкой типами разметки, включенные в фрагмент.
  
    
    
 **Регистрация имен SharePoint** SPM ("SharePoint разметки") указывает строку регистрации пространства имен SharePoint.
  
    
    



```HTML

<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

 **Комментарии** CS и CE («Комментарий начала» и «комментарий окончания») помогают синтаксический анализ строки разметки.
  
    
    



```HTML
<!--CS: Start Top Navigation Snippet-->
…
<!--CE: End Top Navigation Snippet-->

```

 **Фрагменты кода** MS и ME («разметки начала» и «разметка окончания») обозначения начала и окончания управления SharePoint или фрагмент. Некоторые фрагменты кода, такой как ленты или выше, элемент управления навигации в начало содержать несколько элементов управления, включенная в один фрагмент.
  
    
    



```HTML

<!--MS:<SharePoint:DelegateControl runat="server" ControlId="TopNavigationDataSource" Id="topNavigationDelegate">-->
…
<!--ME:</SharePoint:DelegateControl>--><a name="startNavigation"></a>

<!--MS:<Template_Controls>-->
…
<!--ME:</Template_Controls>-->

<!--MS:<asp:SiteMapDataSource ShowStartingNode="True" SiteMapProvider="SPNavigationProvider" ID="topSiteMap" runat="server" StartingNodeUrl="sid:1002">-->
…
<!--ME:</asp:SiteMapDataSource>-->

```

 **Предварительная версия блоки** PS и заключите раздел HTML-код, который не следует изменять среда Предустановки («Начало просмотра» и «предварительный просмотр плана»). В этих разделах предварительной версии являются моментальный снимок времени элемента управления SharePoint Вставка фрагмента. Предварительный просмотр позволяет работать более осмысленно на HTML-файл в редакторе HTML со стороны клиента. Однако изменения содержимого или применения стилей в рамках этой предварительной версии не влияет устойчивые на master-файл, который является то, что SharePoint будет в конечном счете с помощью. Применять стиль фрагмент, необходимо определить и переопределения стилей SharePoint с помощью собственных настраиваемых CSS.
  
    
    



```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><span style="display:none"><table cellpadding="4" cellspacing="0" style="font:messagebox;color:buttontext;background-color:buttonface;border: solid 1px;border-top-color:buttonhighlight;border-left-color:buttonhighlight;border-bottom-color:buttonshadow;border-right-color:buttonshadow"><tr><td nowrap="nowrap"><span style="font-weight:bold">PortalSiteMapDataSource</span> - topSiteMap</td></tr><tr><td></td></tr></table></span><!--PE: End of READ-ONLY PREVIEW-->

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><link rel="stylesheet" type="text/css" href="/_layouts/15/1033/styles/menu-21.css" /><div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox"><ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static"><li class="static"><a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" tabindex="0" title="Default Publishing Site" href="/sites/PubSite/Pages/default.aspx" accesskey="1"><span class="additional-background ms-navedit-flyoutArrow"><span class="menu-item-text">Default Publishing Site</span></span></a></li></ul></div><!--PE: End of READ-ONLY PREVIEW-->
```


## <a name="see-also"></a>См. также
<a name="Resources"> </a>


-  [Инструкции. Преобразование HTML-файла в эталонную страницу SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Как: Добавление фрагмента панель режима изменения в SharePoint](how-to-add-an-edit-mode-panel-snippet-in-sharepoint.md)
    
  
-  [Как: добавить фрагмент Trim безопасности в SharePoint](how-to-add-a-security-trim-snippet-in-sharepoint.md)
    
  

