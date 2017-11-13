---
title: "Инструкции. Настройка макетов страниц для сайта на основе каталога в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 21d8db99-73b3-4429-b6cb-04e375af9f55
ms.openlocfilehash: 33c3859956e80ceae0c3171906b0784fb6726146
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint"></a>Инструкции. Настройка макетов страниц для сайта на основе каталогов в SharePoint
Узнайте, как создавать и настраивать макеты страниц категорий и страниц элементов каталога для сайта SharePoint с публикацией на нескольких сайтах.
## <a name="prerequisites-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a>Необходимые компоненты для создания и настройки макетов страниц сайта на основе каталогов
<a name="bk_prereqs"> </a>

Для выполнения действий, описанных в этом примере, вам необходимо следующее:
  
    
    

- редактор HTML;
    
  
- среда SharePoint для публикации на нескольких сайтах.
    
  
Сведения о настройке среды SharePoint для публикации на нескольких сайтах см. в статье [Настройка публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/en-us/library/jj656774.aspx).
  
    
    

### <a name="core-concepts-to-know-for-creating-and-customizing-page-layouts-for-a-catalog-based-site"></a>Основные понятия, используемые при создании и настройке макетов страниц сайта на основе каталогов

В таблице 1 приведены полезные статьи, которые помогут изучить основные понятия и действия, используемые для создания и настройки макетов страниц сайта на основе каталога.
  
    
    

**Таблица 1. Основные понятия, используемые при создании и настройке макетов страниц сайта на основе каталога**


|**Название статьи**|**Описание**|
|:-----|:-----|
| 
  [Обзор публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/en-us/library/jj635883.aspx) <br/> |Узнайте, как использовать веб-части поиска и публикацию на нескольких сайтах для создания адаптивных сайтов Интернета, интрасети и экстрасети SharePoint.  <br/> |
| [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md) <br/> |Узнайте, как создавать макеты страниц в SharePoint.  <br/> |
| [Инструкции. Устранение ошибок и предупреждений при предварительном просмотре страницы в SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md) <br/> |Узнайте о способах устранения проблем, которые препятствуют отрисовке страницы при предварительном просмотре со стороны сервера.  <br/> |
| [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md) <br/> |Узнайте о способах использования фрагментов для добавления функций SharePoint на главную страницу HTML или макет страницы.  <br/> |
   

## <a name="introduction-to-category-page-layouts-and-catalog-item-page-layouts"></a>Общие сведения о макетах страниц категорий и страниц элементов каталога
<a name="bk_introduction"> </a>

Страницы категорий и страницы элементов каталога — это макеты страниц, которые можно использовать для согласованного отображения структурированного содержимого каталога на сайте. По умолчанию SharePoint может автоматически создать один макет страницы категорий и один макет страницы элементов каталога для подключения к каталогу. Страницы, основанные на этих макетах, создаются в библиотеке страниц сайта публикации при подключении сайта к каталогу. Дополнительные сведения о макетах страниц см. в статье [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md). Дополнительные сведения о функциях, связанных с макетами страниц категорий и макетами страниц элементов каталога, см. в статье [Обзор публикации на нескольких сайтах в SharePoint](http://technet.microsoft.com/en-us/library/jj635883.aspx).
  
    
    
По умолчанию макеты страниц категорий и страниц элементов каталога создаются автоматически при подключении сайта публикации к каталогу. Вы также можете использовать Дизайнер для создания макетов страниц категорий и страниц элементов каталога, которые можно выбрать при подключении сайта публикации к каталогу или при настройке банка терминов навигации на сайте публикации.
  
    
    

## <a name="create-a-category-page-layout"></a>Создание макета страницы категорий
<a name="bk_createCategoryPage"> </a>

Перед созданием или настройкой макета страницы категорий мы рекомендуем создать сопоставленный сетевой диск, который указывает на **коллекцию главных страниц**. Дополнительные сведения см. в разделе  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    
Самый простой способ создать макет страницы категорий — позволить SharePoint автоматически сделать это при подключении сайта публикации к каталогу, а затем изменить разметку существующего макета. Кроме того, можно создать макет страницы категорий с нуля с помощью Дизайнера.
  
    
    

### <a name="to-customize-an-existing-category-page-layout-that-was-created-automatically-by-sharepoint"></a>Настройка макета страницы категорий, созданного SharePoint автоматически


1. С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.
    
  
2. Чтобы настроить макет страницы категорий, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.
    
  
3. Замените часть кода в заполнителе контента с элементом **id="PlaceHolderMain"** тем кодом, который требуется использовать в макете страницы.
    
    > **Важно!** Сохраните фрагмент кода для поиска контента, чтобы на странице категорий можно было отображать результаты поиска. 
4. Чтобы изменить и скопировать HTML-код для всех фрагментов, которые необходимо добавить на страницу, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).
    
  
5. Внесите необходимые изменения в разметку и сохраните файл.
    
  
6. Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.
    
  

### <a name="to-create-a-category-page-layout-by-using-design-manager"></a>Создание макета страницы категорий с помощью Дизайнера


1. Выполните шаги 1-6 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  
2. На шаге 7 выберите тип контента **Страница статьи**.
    
  
3. Нажмите кнопку **OK**.
    
    На этом этапе SharePoint создает HTML-файл и ASPX-файл с таким же именем.
    
    В Дизайнере HTML-файл теперь отображается со столбцом **Состояние**, в котором отображается одно из двух состояний:
    
  - Ошибки
    
  
  - **Преобразование выполнено успешно**.
    
  
4. С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.
    
  
5. Чтобы настроить макет страницы категорий, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.
    
  
6. В теге **\<head\>** замените заполнитель контента с элементом **id="PlaceHolderPageTitle"** следующим:
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

7. Найдите заполнитель контента с элементом **id="PlaceHolderPageTitleInTitleArea"** и замените следующим:
    
```HTML
  
<!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitleInTitleArea" runat="server">-->
<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->
<!--ME:</asp:ContentPlaceHolder>-->
```

8. Замените разметку в заполнителе контента, содержащего элемент **id="PlaceHolderMain"** с разметкой, которую требуется использовать в макете страницы.
    
  
9. Чтобы изменить и скопировать HTML-код для фрагмента поиска контента и других фрагментов, которые необходимо добавить на страницу, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).
    
    > **Примечание.** При добавлении фрагмента кода для поиска контента в макет страницы обязательно измените запрос так, чтобы использовать источник результатов, созданный при подключении сайта публикации к каталогу. Дополнительные сведения см. в статье [Настройка источников результатов для управления веб-контентом в SharePoint](http://technet.microsoft.com/en-us/library/jj715262.aspx). 
10. Внесите другие необходимые изменения в код и сохраните файл.
    
  
11. Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.
    
  

## <a name="understanding-the-markup-in-the-html-category-page-layout"></a>Общие сведения о разметке в макете страницы категорий HTML
<a name="bk_CategoryPageMarkup"> </a>

При создании макета страницы создается ASPX-файл, используемый SharePoint, а определенная HTML-разметка добавляется в HTML-версию макета страницы. Макеты страниц категорий содержат компоненты разметки, добавляемые в зависимости от функции публикации в нескольких семействах сайтов и которые уникальны для макетов страниц категорий. Если вы хотите изменить макет страницы категорий HTML в редакторе HTML, вам будет полезно ознакомиться с этой разметкой.
  
    
    

### <a name="browser-window-page-title"></a>Заголовок страницы в окне браузера

Компонент, который отображается в заполнителе контента с **id="PlaceHolderPageTitle"**, содержит разметку, которая сообщает SharePoint о необходимости использования свойства термина в качестве заголовка страницы в окне браузера вместо стандартного значения поля страницы. В следующем коде показана разметка для заголовка страницы в окне браузера.
  
    
    

```HTML

<!--CS: Start Taxonomy TermProperty Snippet-->
<!--SPM:<%@Register Tagprefix="Taxonomy"  Namespace="Microsoft.SharePoint.Taxonomy" Assembly="Microsoft.SharePoint.Taxonomy, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
<!--MS:<Taxonomy:TermProperty Property="Name" runat="server">-->
<!--ME:</Taxonomy:TermProperty>-->
```


### <a name="page-title"></a>Заголовок страницы

Компонент, который отображается в заполнителе контента с **id="PlaceHolderPageTitleInTitleArea"**, содержит разметку, которая сообщает SharePoint о необходимости использования свойства термина в качестве заголовка страницы вместо фрагмента **SPTitleBreadcrumb** и стандартного значения поля заголовка страницы. В следующем коде показана разметка для заголовка страницы.
  
    
    

```HTML

<!--SPM:<asp:SiteMapPath runat="server" ParentLevelsDisplayed="1" SiteMapProvider="CurrentNavigationSwitchableProvider"/>-->"
```


### <a name="content-search-snippet"></a>Фрагмент поиска контента

Компоненты, которые отображаются после фрагмента контента страницы, в заполнителе контента с **id="PlaceHolderMain"**, содержат разметку для фрагмента зоны веб-части, которая содержит четыре зоны веб-частей. Первая зона включает в себя фрагмент поиска контента, который отображает веб-часть поиска контента на странице. Этот фрагмент также содержит сведения, которые помогают веб-части поиска контента запросить источник результатов и показать результаты на странице. Последние три зоны веб-частей будут пустыми. Если вы решили создать макет страницы категорий, необходимо добавить разметку для фрагмента поиска контента в HTML-файл разметки страницы. В следующем коде показана разметка для фрагмента поиска контента. Замените  _ResultSourceID_ на GUID источника результатов, а вместо _CatalogURL_ укажите URL-адрес каталога.
  
    
    

> **Примечание.** Идентификаторы GUID для **ID** и **\_\_WebPartId** случайным образом создаются SharePoint при добавлении фрагментов кода в макет страницы.
  
    
    


```HTML
<!--
CS: Start Content Search Snippet-->
<!--SPM:<%@Register Tagprefix="a781102493" Namespace="Microsoft.Office.Server.Search.WebControls" Assembly="Microsoft.Office.Server.Search, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<a781102493:ContentBySearchWebPart runat="server" DataProviderJSON="{&amp;#34;QueryTemplate&amp;#34;:&amp;#34;&amp;#34;,&amp;#34;SourceID&amp;#34;
:&amp;#34;ResultSourceID&amp;#34;,&amp;#34;PropertiesJson&amp;#34;:&amp;#34;
{'Tag':'{Term.IDWithChildren}','Scope':'CatalogURL'}&amp;#34;}" ResultsPerPage="3" RenderTemplateId="~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/Control_ListWithPaging.js" 
ItemTemplateId="~sitecollection/_catalogs/masterpage/Display Templates/Content Web Parts/Item_PictureOnTop.js" SelectedPropertiesJson="[&amp;#34;WorkId&amp;#34;,&amp;#34;Rank&amp;#34;,&amp;#34;Title&amp;#34;,&amp;#34;Author&amp;#34;,&amp;#34;
Size&amp;#34;,&amp;#34;Path&amp;#34;,&amp;#34;Description&amp;#34;,&amp;#34;Write&amp;#34;,&amp;#34;CollapsingStatus&amp;#34;,&amp;#34;
HitHighlightedSummary&amp;#34;,&amp;#34;HitHighlightedProperties&amp;#34;,&amp;#34;ContentClass&amp;#34;,&amp;#34;
PictureThumbnailURL&amp;#34;,&amp;#34;ServerRedirectedURL&amp;#34;,&amp;#34;ServerRedirectedEmbedURL&amp;#34;,&amp;#34;
ServerRedirectedPreviewURL&amp;#34;,&amp;#34;FileExtension&amp;#34;,&amp;#34;ContentTypeId&amp;#34;,&amp;#34;ParentLink&amp;#34;,&amp;#34;
ViewsLifeTime&amp;#34;,&amp;#34;ViewsRecent&amp;#34;,&amp;#34;SectionNames&amp;#34;,&amp;#34;SectionIndexes&amp;#34;,&amp;#34;
SiteLogo&amp;#34;,&amp;#34;SiteDescription&amp;#34;,&amp;#34;deeplinks&amp;#34;,&amp;#34;importance&amp;#34;]" ShouldHideControlWhenEmpty="True" FrameType="None" SuppressWebPartChrome="False" Description="$Resources:Microsoft.Office.Server.Search,CBS_Description;" IsIncluded="True" 
ZoneID="" PartOrder="0" FrameState="Normal" AllowRemove="True" AllowZoneChange="True" 
AllowMinimize="True" AllowConnect="True" AllowEdit="True" AllowHide="True" IsVisible="True" 
DetailLink="" HelpLink="" HelpMode="Modeless" Dir="Default" PartImageSmall="" IsIncludedFilter="" ExportControlledProperties="True" ConnectionID="00000000-0000-0000-0000-000000000000" ID="g_54e35103_6f29_4dd9_b93b_8d4c863834af" ChromeType="None" ExportMode="All" __MarkupType="vsattributemarkup" __WebPartId="54e35103-6f29-4dd9-b93b-8d4c863834af" 
WebPart="true" Height="" Width="" Title="$Resources:cms,WebPartZoneTitle_Dynamic;">-->
<!--ME:</a781102493:ContentBySearchWebPart>-->
<!--CE: End Content Search Snippet-->

```


## <a name="create-a-catalog-item-page-layout"></a>Создание макета страницы элементов каталога
<a name="bk_createCatItemPage"> </a>

Перед созданием или настройкой макета страницы элементов каталога мы рекомендуем создать сопоставленный сетевой диск, который указывает на коллекцию главных страниц. Дополнительные сведения см. в разделе  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    
Как и для макета страницы категорий, самый простой способ создать макет страницы элементов каталога — позволить SharePoint сделать это автоматически при подключении сайта публикации к каталогу и добавить в существующий макет дополнительную разметку. Кроме того, можно создать макет страницы элементов каталога с нуля с помощью Дизайнера.
  
    
    

### <a name="to-customize-an-existing-catalog-item-page-layout-that-was-created-automatically-by-sharepoint"></a>Настройка макета страницы элементов каталога, созданного SharePoint автоматически


1. С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.
    
  
2. Чтобы настроить макет страницы элементов каталога, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.
    
  
3. Добавьте в заполнитель контента, содержащего элемент **id="PlaceHolderMain"**, разметку, которую требуется использовать в макете страницы.
    
  
4. Удалите все фрагменты, которые не требуются, из макета страницы и переместите оставшиеся фрагменты туда, где необходимо показывать значения свойств.
    
    > **Внимание!** По умолчанию фрагмент кода для зоны веб-частей, который содержит фрагмент кода для повторного использования элементов каталога, добавляется в макет страницы. Этот фрагмент кода включает в себя поставщик данных, возвращающий результаты запроса, которые используются всеми другими фрагментами кода на странице. Мы рекомендуем оставить этот фрагмент кода для повторного использования элементов каталога в данном фрагменте кода для зоны веб-частей по умолчанию. Можно переместить фрагмент кода для повторного использования элементов каталога за пределы зоны веб-частей, также можно изменить свойство, которое он показывает. Однако необходимо сохранить фрагмент кода для повторного использования элементов каталога в макете страницы. Дополнительные сведения см. разделе [Поля страницы](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields) далее в этой статье. 
5. Чтобы изменить и скопировать HTML-код для всех фрагментов, которые необходимо использовать на странице, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).
    
  
6. Внесите необходимые изменения в разметку и сохраните файл.
    
  
7. Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.
    
  

### <a name="to-create-a-catalog-item-page-layout-by-using-design-manager"></a>Создание макета страницы элементов каталога с помощью Дизайнера


1. Выполните шаги 1-6 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  
2. На шаге 7 выберите **Удаленный каталог**, а затем выберите каталог, который содержит данные, которые будут отображаться на странице.
    
  
3. Нажмите кнопку **OK**.
    
    На этом этапе SharePoint создает HTML-файл и ASPX-файл с таким же именем.
    
    В Дизайнере HTML-файл теперь отображается со столбцом **Состояние**, в котором отображается одно из двух состояний:
    
  - Ошибки
    
  
  - **Преобразование выполнено успешно**.
    
  
4. С помощью проводника Windows откройте сетевой диск, сопоставленный с коллекцией главных страниц.
    
  
5. Чтобы настроить макет страницы элементов каталога, измените HTML-файл, который находится непосредственно на сервере. Для этого откройте и измените HTML-файл на сопоставленном диске с помощью HTML-редактора. Каждый раз при сохранении HTML-файл все изменения синхронизируются со связанным ASPX-файлом.
    
  
6. Добавьте в заполнитель контента, содержащего элемент **id="PlaceHolderMain"**, разметку, которую требуется использовать в макете страницы.
    
  
7. Удалите все фрагменты, которые не требуются, из макета страницы и переместите оставшиеся фрагменты туда, где необходимо показывать значения свойств.
    
    > **Внимание!** По умолчанию фрагмент кода для зоны веб-частей, который содержит фрагмент кода для повторного использования элементов каталога, добавляется в макет страницы. Этот фрагмент кода включает в себя поставщик данных, возвращающий результаты запроса, которые используются всеми другими фрагментами кода на странице. Мы рекомендуем оставить этот фрагмент кода для повторного использования элементов каталога в данном фрагменте кода для зоны веб-частей по умолчанию. Можно переместить фрагмент кода для повторного использования элементов каталога за пределы зоны веб-частей, также можно изменить свойство, которое он показывает. Однако необходимо сохранить фрагмент кода для повторного использования элементов каталога в макете страницы. Дополнительные сведения см. разделе [Поля страницы](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md#bk_pagefields) далее в этой статье. 
8. Чтобы изменить и скопировать HTML-код для всех фрагментов, которые необходимо использовать на странице, выполните шаги с 1 по 11 из раздела "Вставка фрагмента из коллекции фрагментов" статьи  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).
    
  
9. Внесите необходимые изменения в разметку и сохраните файл.
    
  
10. Выполните шаги с 9 по 11 из раздела "Создание макета страницы" статьи  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md), чтобы проверить состояние файла, просмотреть макет страницы и устранить все ошибки.
    
  

## <a name="understanding-the-markup-in-the-html-catalog-item-page-layout"></a>Общие сведения о разметке в макете страницы элементов каталога HTML
<a name="bk_CatItemMarkup"> </a>

При создании макета страницы создается ASPX-файл, используемый SharePoint, а определенная HTML-разметка добавляется в HTML-версию макета страницы. Макеты страниц элементов каталога содержат компоненты разметки, добавляемые в зависимости от функции публикации в нескольких семействах сайтов и которые уникальны для макетов страниц элементов каталога. Если вы хотите изменить макет страницы элементов каталога HTML в редакторе HTML, вам будет полезно ознакомиться с этой разметкой.
  
    
    

### <a name="browser-window-page-title"></a>Заголовок страницы в окне браузера

Компонент, который отображается в заполнителе контента с **id="PlaceHolderPageTitle"**, содержит фрагмент повторного использования элементов каталога, который сообщает SharePoint о необходимости использовать элемент каталога в качестве заголовка страницы в окне браузера вместо стандартного значения поля заголовка страницы. В следующем коде показана разметка для заголовка страницы в окне браузера.
  
    
    

> **Примечание.** Идентификаторы GUID для **ID** и **__WebPartId** случайным образом создаются SharePoint при добавлении фрагментов кода в макет страницы.
  
    
    


```HTML

<!--CS: [Title] Start Catalog-Item Reuse Snippet-->
<!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;Title&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_863912c1_c849_46dc_8781_2920ee2bc83f" __WebPartId="{863912c1-c849-46dc-8781-2920ee2bc83f}">-->
<!--SPM:<RenderFormat>-->
<!--DC:Renders value from search without any additional formatting.-->
<!--SPM:</RenderFormat>-->
<!--SPM:</cc1:CatalogItemReuseWebPart>-->
<!--CE:End Catalog-Item Reuse Snippet-->

```


### <a name="page-fields"></a>Поля страницы
<a name="bk_pagefields"> </a>

Компоненты, которые отображаются в заполнителе контента с **id="PlaceHolderMain"**, содержат фрагменты для полей **Title**, **Page Content** и **Catalog-Item URL**. Вы можете удалить любой из них. В следующем примере кода показана разметки для этих полей страницы.
  
    
    

```HTML

<div>
    <!--CS: Start Page Field: Title Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldTextField" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
        <!--MS:<PageFieldTextField:TextField FieldName="fa564e0f-0c70-4ab9-b863-0177e6ddd247" 
runat="server">-->
        <!--ME:</PageFieldTextField:TextField>-->
    <!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Page Field: Title Snippet-->
</div>
<div>
    <!--CS: Start Page Field: Page Content Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldRichHtmlField" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<PageFieldRichHtmlField:RichHtmlField FieldName="f55c4d88-1f2e-4ad9-aaa8-819af4ee7ee8" runat="server">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
            <div id="ctl02_label" style="display:none">Page Content</div>
            <div id="ctl02__ControlWrapper_RichHtmlField" class="ms-rtestate-field" style="display:inline" aria-labelledby="ctl02_label">
                <div align="left" class="ms-formfieldcontainer">
                    <div class="ms-formfieldlabelcontainer" nowrap="nowrap">
                        <span class="ms-formfieldlabel" nowrap="nowrap">Page Content</span>
                    </div>
                    <div class="ms-formfieldvaluecontainer">
                        <div class="ms-rtestate-field">Page Content field value. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div>
                    </div>
                </div>
            </div>
        <!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</PageFieldRichHtmlField:RichHtmlField>-->
    <!--CE: End Page Field: Page Content Snippet-->
</div>
<div>
    <!--CS: Start Page Field: Catalog-Item URL Snippet-->
    <!--SPM:<%@Register Tagprefix="PageFieldCatalogSourceFieldControl" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<PageFieldCatalogSourceFieldControl:CatalogSourceFieldControl FieldName="75772bbf-0c25-4710-b52c-7b78344ad136" runat="server">-->
    <!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
        <div align="left" class="ms-formfieldcontainer">
            <div class="ms-formfieldlabelcontainer" nowrap="nowrap">
                <span class="ms-formfieldlabel" nowrap="nowrap">Catalog-Item URL</span>
            </div>
            <div class="ms-formfieldvaluecontainer">
                <a href="http://www.example.com">Link to sample web site.</a>
            </div>
        </div>
    <!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</PageFieldCatalogSourceFieldControl:CatalogSourceFieldControl>-->
    <!--CE: End Page Field: Catalog-Item URL Snippet-->
</div>

```

Если макет страницы элементов каталога был создан автоматически при подключении сайта публикации к каталогу или после выбора удаленного каталога во время создания макета страницы, то в макете также будет содержаться фрагмент зоны веб-части, в который входит фрагмент повторного использования элементов каталога. Он регистрирует поставщик данных для страницы. Фрагмент повторного использования элементов каталога содержит свойство **UseSharedDataProvider** со значением **False**. Фрагмент зоны веб-части можно удалить из макета страницы. Но фрагмент повторного использования элементов каталога должен храниться в разметке макета страницы, чтобы на элементы каталога могли отображаться на странице. При создании страницы, которая использует этот макет, можно настроить веб-часть так, чтобы она была скрыта, когда пользователь просматривает страницу.
  
    
    

> **Важно!** Если при создании макета страницы элементов каталога выбирается тип контента вместо удаленного каталога, необходимо добавить фрагмент кода для повторного использования элементов каталога в макет страницы. Ниже показан фрагмент кода для повторного использования элементов каталога, который размещен во фрагменте кода зоны веб-частей. Замените _ManagedPropertyName_ именем управляемого свойства, которое нужно показать, _ResultSourceID_ — идентификатором GUID источника результатов, а _CatalogURL_ — URL-адресом каталога.
  
    
    




```HTML

<div>
    <!--CS: Start Web Part Zone Snippet-->
    <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, 
Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--SPM:<%@Register Tagprefix="cc1"  Namespace="Microsoft.Office.Server.Search.WebControls" Assembly="Microsoft.Office.Server.Search, Version=15.0.0.0, Culture=neutral, 
PublicKeyToken=71e9bce111e9429c" %>-->
    <!--MS:<WebPartPages:WebPartZone runat="server" Title="&amp;#60;%$Resources:cms,WebPartZoneTitle_Body%&amp;#62;" AllowPersonalization="False" FrameType="TitleBarOnly" ID="Body" Orientation="Vertical">-->
        <!--MS:<ZoneTemplate>-->
            <!--CS: [ManagedPropertyName] Start Catalog-Item Reuse Snippet-->
            <!--DC:To render the search property using a rendering template, change the "UseServerSideRenderFormat" property to "False".-->
            <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" AddSEOPropertiesFromSearch="True" LogAnalyticsViewEvent="True" UseSharedDataProvider="False" OverwriteResultPath="False" DataProviderJSON="{&amp;#34;QueryTemplate&amp;#34;:&amp;#34;ListItemID:{URLTOKEN.1}&amp;#34;,&amp;#34;SourceID&amp;#34;:&amp;#34; ResultSourceID&amp;#34;,&amp;#34;PropertiesJson&amp;#34;:&amp;#34;{&amp;#39;Scope&amp;#39;:&amp;#39;  CatalogURL&amp;#39;,&amp;#39;Tag&amp;#39;:&amp;#39;{Term}&amp;#39;}&amp;#34;}" ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;ManagedPropertyName&amp;#34;]" Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" MissingAssembly="Cannot import this Web Part." ID="g_d63eebe7_207f_4e8c_9566_7381acc80cc7" __WebPartId="{d63eebe7-207f-4e8c-9566-7381acc80cc7}">-->
            <!--SPM:<RenderFormat>-->
            <!--DC:Renders value from search without any additional formatting.-->
            <!--SPM:</RenderFormat>-->
            <!--SPM:</cc1:CatalogItemReuseWebPart>-->
        <!--ME:</ZoneTemplate>-->
    <!--ME:</WebPartPages:WebPartZone>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>

```

Если макет страницы элементов каталога был создан автоматически при подключении сайта публикации к каталогу или после выбора удаленного каталога во время создания макета страницы, остальная часть страницы содержит фрагменты повторного использования элементов каталога, соответствующие управляемым свойствам из каталога на сайте разработки. Эти управляемые свойства показывают сведения об определенном элементе каталога, который отображается с помощью макета страницы элементов каталога. Фрагменты повторного использования элементов каталога находятся за пределами зоны веб-частей и отображаются непосредственно на странице при выборе элемента на странице категорий. В таблице 2 перечислены управляемые свойства, которые автоматически добавляются в макет страницы элементов каталога.
  
    
    

> **Примечание.** Некоторые управляемые свойства добавляются, только если каталог находится в библиотеке страниц. В столбце **Используется** таблицы 2 показано, какие управляемые свойства используются и для библиотеки страниц, и для списка, а какие — только для библиотеки страниц.
  
    
    


**Таблица 2. Управляемые свойства фрагментов кода для повторного использования элементов каталога по умолчанию**


|**Управляемое свойство**|**Описание**|**Используется**|
|:-----|:-----|:-----|
|**AuthorOWSUSER** <br/> |Имя пользователя, создавшего страницу.  <br/> |Только библиотекой страниц  <br/> |
|**CreatedOWSDATE** <br/> |Дата создания страницы или элемента списка.  <br/> |Библиотекой страниц и списком  <br/> |
|**EditorOWSUSER** <br/> |Имя пользователя, который последним изменил страницу или элемент списка.  <br/> |Библиотекой страниц и списком  <br/> |
|**ListItemID** <br/> |Идентификатор страницы или элемента списка.  <br/> |Библиотекой страниц и списком  <br/> |
|**ModifiedOWSDATE** <br/> |Дата последнего изменения страницы или элемента списка.  <br/> |Библиотекой страниц и списком  <br/> |
|**PublishingContactOWSUSER** <br/> |Контакт — это столбец сайта, создаваемый функцией публикации. Он используется в типе контента страницы как пользователь или группа, представляющая контактное лицо для страницы.  <br/> |Только библиотекой страниц  <br/> |
|**PublishingIsFurlPageOWSBOOL** <br/> |Логическое значение, указывающее, связана ли страница с понятным URL-адресом.  <br/> |Только библиотекой страниц  <br/> |
|**PublishingPageContentOWSHTML** <br/> |HTML-контент страницы.  <br/> |Только библиотекой страниц  <br/> |
|**PublishingPageLayoutOWSURLH** <br/> |URL-адрес макета страницы, который использовался для создания страницы.  <br/> |Только библиотекой страниц  <br/> |
|**Title** <br/> |Заголовок страницы или элемента списка.  <br/> |Библиотека страниц и список  <br/> |
   
Управляемые свойства для пользовательских столбцов, добавляемых в библиотеку страниц или список, также включаются во фрагменты кода для повторного использования элементов каталога. Имя управляемого свойства зависит от типа столбца сайта, который используется при создании столбца сайта. Дополнительные сведения см. в статьях [Автоматически созданные управляемые свойства в SharePoint](http://technet.microsoft.com/en-us/library/jj613136.aspx) и [Обзор схемы поиска в SharePoint](http://technet.microsoft.com/en-us/library/jj219669.aspx).
  
    
    

> **Важно!** Столбец сайта **Page Image** в библиотеке страниц сопоставляется с управляемым свойством **PublishingImage**. Но управляемое свойство **PublishingImage** не добавляется автоматически в макет страницы элементов категорий. Чтобы добавить изображение в макет страницы, необходимо включить фрагмент кода для повторного использования элементов каталога для управляемого свойства **PublishingImage**. Указанный ниже HTML-код позволит добавить фрагмент кода для повторного использования элементов каталога, чтобы обеспечить отображение значения управляемого свойства **PublishingImage** в макете страницы. Замените _UniqueID_ идентификатором GUID, который является уникальным для каждого экземпляра фрагмента кода.
  
    
    




```HTML

<div>
<!--CS: [PublishingImage] Start Catalog-Item Reuse Snippet-->
<!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;PublishingImage&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_UniqueID" __WebPartId="{UniqueID}">-->
<!--SPM:<RenderFormat>-->
<!--SPM:<Format Type="HTML"> -->
<!--SPM:<Picture>-->True<!--SPM:</Picture>-->
<!--SPM:</Format> -->
<!--SPM:</RenderFormat>-->
<!--SPM:</cc1:CatalogItemReuseWebPart>-->
<!--CE:End Catalog-Item Reuse Snippet-->
</div>

```

Если вы создаете макет страницы элементов каталога с помощью Дизайнера и выбираете тип контента вместо удаленного каталога, вы можете добавить фрагменты повторного использования элементов каталога на страницу с помощью коллекции фрагментов. В следующем коде показана разметка фрагментов повторного использования для управляемых свойств **Title**, **PublishingPageContentOWSHTML**, **CreatedOWSDATE** и **owstaxIdPageCategory**.
  
    
    

> **Примечание.** Идентификаторы GUID для **ID** и **__WebPartId** случайным образом создаются SharePoint при добавлении фрагментов кода в макет страницы.
  
    
    




```HTML

<div>
    <!--CS: [Title] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;Title&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_0dc23bb8_8d34_4f9f_8085_5a6ac286cb9e" 
__WebPartId="{0dc23bb8-8d34-4f9f-8085-5a6ac286cb9e}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [PublishingPageContentOWSHTML] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;PublishingPageContentOWSHTML&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_25253a49_a9a6_4277_bf9d_416961024cee" 
__WebPartId="{25253a49-a9a6-4277-bf9d-416961024cee}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [CreatedOWSDATE] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;CreatedOWSDATE&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." 
ID="g_4e1f180b_12f8_4e50_84d7_c72b0ee3793f" 
__WebPartId="{4e1f180b-12f8-4e50-84d7-c72b0ee3793f}">-->
    <!--SPM:<RenderFormat>-->
    <!--SPM:<Format Type="DateTime"> -->
    <!--DC:To render Date and Time, change this value to False.-->
    <!--SPM:<DateOnly>-->True<!--SPM:</DateOnly>-->
    <!--SPM:</Format> -->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>
<div>
    <!--CS: [owstaxIdPageCategory] Start Catalog-Item Reuse Snippet-->
    <!--SPM:<cc1:CatalogItemReuseWebPart runat="server" UseServerSideRenderFormat="True" 
ResultType="" NumberOfItems="1" UseSharedDataProvider="True" OverwriteResultPath="False" 
ResultsPerPage="1"  SelectedPropertiesJson="[&amp;#34;owstaxIdPageCategory&amp;#34;]" 
Title="$Resources:Microsoft.Office.Server.Search,CBSItem_Title;" 
Description="$Resources:Microsoft.Office.Server.Search,CBSItem_Description;" 
MissingAssembly="Cannot import this Web Part." ID="g_22e39e9d_1b25_42c7_bf2a_7ebca37616d4" 
__WebPartId="{22e39e9d-1b25-42c7-bf2a-7ebca37616d4}">-->
    <!--SPM:<RenderFormat>-->
    <!--DC:Renders value from search without any additional formatting.-->
    <!--SPM:</RenderFormat>-->
    <!--SPM:</cc1:CatalogItemReuseWebPart>-->
    <!--CE:End Catalog-Item Reuse Snippet-->
</div>

```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Разработка макета сайта в SharePoint](develop-the-site-design-in-sharepoint.md)
    
  
-  [Обзор Дизайнера в SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Обзор модели страниц в SharePoint](overview-of-the-sharepoint-page-model.md)
    
  
-  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Шаблоны отображения Дизайнера SharePoint](sharepoint-design-manager-display-templates.md)
    
  

