---
title: "Преобразование HTML-файла в эталонную страницу SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a76ab289-3256-45de-ac63-d5112a74e3c7
ms.openlocfilehash: d76397e79d1580c2b113810523c2ce119a731ba4
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="convert-an-html-file-into-a-master-page-in-sharepoint"></a>Преобразование HTML-файла в эталонную страницу SharePoint

Благодаря Дизайнеру вы можете конвертировать HTML-файл в эталонную страницу SharePoint  MASTER-файл. После преобразования HTML-файл и эталонная страница будут связаны, чтобы при редактировании и сохранении HTML-файла эти изменения синхронизировались со связанной эталонной страницей.

## <a name="introduction-to-converting-a-master-page"></a>Общие сведения о преобразовании эталонной страницы
<a name="Introduction"> </a>

 С помощью компонента "Дизайнер" вы можете преобразовать HTML-файл в эталонную страницу SharePoint — MASTER-файл. После преобразования HTML-файл и эталонная страница будут связаны, чтобы при редактировании и сохранении HTML-файла эти изменения синхронизировались со связанной эталонной страницей.
  
    
    
Зачем преобразовывать HTML-файл, а не создавать MASTER-файл с нуля? В SharePoint эталонные страницы работают точно так же, как в ASP.NET, но в SharePoint для корректного отображения эталонной страницы также необходимо, чтобы на странице присутствовали определенные элементы, например элементы управления и заполнители контента, относящиеся к SharePoint. Если вы используете "Дизайнер" для преобразования HTML-файла в полноценную эталонную страницу SharePoint, то вам не потребуется знание разметки ASP.NET или SharePoint. Вместо этого вы можете сосредоточиться на разработке сайта с помощью HTML, CSS и JavaScript.
  
    
    
При преобразовании HTML-файла в эталонную страницу происходит следующее:
  
    
    

- В коллекции эталонных страниц создается MASTER-файл с таким же именем, как у HTML-файла.
    
  
- В MASTER-файл добавляется вся разметка, необходимая SharePoint, поэтому эталонная страница отображается правильно.
    
  
- В исходный HTML-файл добавляется разметка, например комментарии, теги **\<div\>**, фрагменты кода и заполнители контента.
    
  
- HTML-файл и эталонная страница связываются, поэтому в дальнейшем при сохранении внесенных в HTML-файл изменений, этот файл будет синхронизирован с MASTER-файлом.
    
> [!NOTE]
> Синхронизация выполняется только в одном направлении. Изменения эталонной страницы HTML будут синхронизированы со связанным MASTER-файлом, однако если вы редактируете непосредственно MASTER-файл, внесенные изменения не будут синхронизированы с HTML-файлом. У каждой эталонной страницы HTML (и каждого макета HTML-страницы) есть свойство **Связанный файл**, для которого по умолчанию задано значение **True**, что обеспечивает связь и синхронизацию между файлами.
  
    
    

Если у вас есть пара связанных файлов (HTML и MASTER) и вы изменяете MASTER-файл, не нарушая связь, внесенные изменения будут сохранены, но вы не сможете отметить или опубликовать этот файл, то есть по большому счету эти изменения не сохраняются. Любые изменения в файле HTML перезаписывают MASTER-файл. Если вы отметите или опубликуете HTML-файл, то его изменения перезапишут любые изменения, которые были сделаны в MASTER-файле. Изменения, внесенные в MASTER-файл, будут изменены.
  
    
    
Если вы разработчик, обладающий опытом работы с ASP.NET, то вы можете работать с MASTER-файлом отдельно, нарушив связь между файлами. Чтобы отменить связь между HTML-файлом и MASTER-файлом, в компоненте "Дизайнер" нажмите **Изменить свойства** для HTML-файла, а затем снимите флажок **Связанный файл**. Позже вы можете заново связать файлы, изменив свойства и установив этот флажок. В этом случае HTML-файл снова заменит MASTER-файл, а изменения, внесенные в MASTER-файл, будут потеряны.
  
    
    

## <a name="prepare-the-html-file-for-conversion"></a>Подготовка HTML-файла к преобразованию
<a name="Prepare"> </a>

Прежде чем преобразовывать HTML-файл, ознакомьтесь с приведенными ниже советами и рекомендациями.
  
    
    

- Рассмотрим модель страниц в SharePoint. Дополнительные сведения см. в статье [Обзор модели страниц в SharePoint](overview-of-the-sharepoint-page-model.md). При создании HTML-макетов для сайта у вас наверняка будет несколько HTML-файлов для разных типов страниц, например статьи или страницы категории, содержащей веб-части, в которых отображаются элементы определенной категории из каталога. Однако только один HTML-файл будет преобразован в эталонную страницу. HTML-файл можно преобразовать в эталонную страницу, но невозможно преобразовать непосредственно в макет страницы, так как для этого необходимы поля страницы.
    
  
- Убедитесь, что HTML-файл совместим с форматом XML. Для успешного преобразования HTML-файл должен быть совместимым с XML. К сожалению, это требование переопределяет некоторые стандарты HTML 5. Например, в HTML 5 можно указать значение **doctype** в нижнем регистре, но в XML значение **doctype** следует указывать прописными буквами. Кроме того, из HTML-файла следует удалить теги **\<form\>**. Вы можете пропустить HTML-файл через внешнее средство проверки XML, чтобы обнаружить ошибки XML перед преобразованием.
    
  
- Ниже представлены важные рекомендации, связанные со ссылками CSS.
    
  - Не помещайте блоки **\<style\>** в тег **\<head\>**. Эти стили удаляются во время преобразования. Вместо этого ссылайтесь в HTML-файле на внешний CSS-файл.
    
  
  - Добавьте параметр `ms-design-css-conversion="no"` в тег **\<CSS link\>**, если вы используете веб-шрифт.
    
  
  - Будьте осторожны, применяя стили к общим HTML-тегам, например **\<body\>**, **\<div\>** и **\<img\>**. Все содержимое оформления SharePoint, включая ленту, находится внутри тега **\<body\>**. Стили, которые обычно применялись бы к тегу **\<body\>**, следует применять к тегу **\<div id="s4-bodyContainer"\>**, который SharePoint использует для основного текста страницы. Кроме того, SharePoint использует множество изображений, на которые влияют стили, применяемые к тегу **\<img\>**.
    
  
  - Многие дизайнеры настраивают стиль навигации, применяя классы к элементам **\<ul\>** и **\<li\>**. Однако в SharePoint используется динамический элемент навигации, который можно добавить на эталонную страницу из коллекции фрагментов кода. По умолчанию к элементам навигации SharePoint применены стили, которые необходимо переопределять.
    
  
- Ниже указаны возможные проблемы с именованием файлов.
    
  - Файлы Index.html и Index.htm будут иметь один и тот же MASTER-файл.
    
  
  - Файлы Design/Index.html и Design/SubDesign/Index.html будут преобразованы в отдельные MASTER-файлы, но они оба будут отображаться в списке эталонной странице в Дизайнере как Index.html. Чтобы устранить неоднозначность, щелкните каждый файл или нажмите кнопку с многоточием, чтобы увидеть полный путь.
    
  
- Если вы добавляете мини-приложение JavaScript, убедитесь, что открывающий тег **\<script\>** находится на отдельной строке.
    
```
  
<script>
(function( …

```

Не помещайте их в одну строку, как показано ниже.
    


```
  
<Script> (function( …
```

- Ссылка на библиотеку JQuery (внешняя ссылка) должна находиться перед тегом **\</head\>**.
    
  

## <a name="convert-the-html-file-into-a-master-page"></a>Преобразование HTML-файла в эталонную страницу
<a name="Convert"> </a>

Перед преобразованием HTML-файла необходимо отправить все файлы оформления, включая HTML-файл. Дополнительные сведения см. в статье [Инструкции. Сопоставление сетевого диска с коллекцией эталонных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).
  
    
    

### <a name="to-convert-the-html-file-into-a-master-file"></a>Преобразование HTML-файла в MASTER-файл


1. Перейдите на сайт публикации.
    
  
2. В правом верхнем углу страницы выберите пункт **Параметры**, а затем выберите **Дизайнер**.
    
  
3. Откройте "Дизайнер" и в области навигации слева выберите команду **Изменить главные страницы**.
    
  
4. Выберите пункт **Преобразование HTML-файла в главную страницу SharePoint**.
    
  
5. В диалоговом окне **Выбор актива** найдите и выберите преобразуемый HTML-файл.
    
    > [!NOTE]
    > При отправке файлов разработки сохраните все файлы, связанные с одним оформлением, в собственной папке в коллекции главных страниц. Когда выполняется копирование папки разработки на подключенный сетевой диск, коллекция эталонных страниц сохраняет всю созданную вами структуру папок. 
6. Нажмите кнопку **Вставить**.
    
    На этом этапе SharePoint преобразует HTML-файл в MASTER-файл с таким же именем.
    
    Теперь в компоненте "Дизайнер" для вашего HTML-файла отображается столбец "Состояние", в котором показано одно из двух возможных состояний:
    
  - **Предупреждения и ошибки**.
    
  
  - **Преобразование выполнено успешно**.
    
  
7. Перейдите по ссылке в столбце "Состояние" для предварительного просмотра файла, а также ошибок или предупреждений, касающихся эталонной страницы.
    
    Страница предварительного просмотра — это страница динамического просмотра эталонной страницы на стороне сервера. Верхняя часть области предварительного просмотра отображает предупреждения или ошибки, которые необходимо устранить, изменив HTML-файл в редакторе HTML. Для того чтобы эталонная страница правильно отображалась во время предварительного просмотра, все ошибки должны быть устранены.
    
    Дополнительные сведения об устранении ошибок и предупреждений см. в статье [Инструкции. Устранение ошибок и предупреждений во время предварительного просмотра страницы в SharePoint](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md).
    
    Дополнительные сведения о предварительном просмотре эталонной страницы с различными страницами см. в статье [Инструкции. Изменение страницы предварительного просмотра в компоненте "Дизайнер" SharePoint](how-to-change-the-preview-page-in-sharepoint-design-manager.md).
    
    На странице предварительного просмотра также есть ссылка "Фрагменты кода" в правом верхнем углу. Эта ссылка ведет к коллекции фрагментов кода, где можно начать заменять статические или временные элементы управления в оформлении на динамические элементы управления SharePoint. Дополнительные сведения см. в статье [Фрагменты кода в компоненте "Дизайнер" SharePoint](sharepoint-design-manager-snippets.md).
    
  
8. Чтобы устранить ошибки, с помощью HTML-редактора откройте и измените HTML-файл на подключенном диске на стороне сервера. Каждый раз при сохранении HTML-файла, все изменения синхронизируется со связанным MASTER-файлом.
    
  
9. После успешного предварительного просмотра эталонной страницы в HTML-файл будет добавлен тег **\<div\>**. Возможно, чтобы увидеть тег **\<div\>**, потребуется прокрутить страницу вниз.
    
    Этот тег **\<div\>** является основным блоком контента. Он находится в заполнителе контента с именем **ContentPlaceHolderMain**. Во время выполнения, когда посетитель просматривает ваш сайт и запрашивает страницу, в этот заполнитель добавляется контент из макета страницы для соответствующей области содержимого. Этот тег **\<div\>** следует поместить там, где должны отображаться макеты страниц на эталонной странице.
    
    Если HTML-файл содержит статический или временный контент в основном тексте страницы, теперь начинается процесс удаления этого статического контента с эталонной HTML-страницы и применения этих стилей к другим элементам модели страниц SharePoint, например макетам страниц, полям страниц, фрагментам кода и шаблонам отображения. Пример вы найдете в статье [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  

## <a name="understanding-the-html-file-after-conversion"></a>Общие сведения об HTML-файле после преобразования
<a name="Understand"> </a>

После преобразования HTML-файла в эталонную страницу в этот файл будет добавлено большое количество строк разметки. Вы можете не обращать внимания на большую ее часть, так как она не будет отображаться в конечной разметке вашего сайта при просмотре источника в браузере, однако эта разметка критична для преобразования вашего HTML-файла в MASTER-файл, который фактически используется SharePoint. Каждый раз при сохранении HTML-файла эта разметка SharePoint позволяет выполнить аналогичные изменения в связанном MASTER-файле в фоновом режиме.
  
    
    
Добавляемая разметка включает теги, расположенные до тега **\<head\>** и в нем, фрагменты кода и заполнители контента. Большая часть разметки заключена в теги комментариев. Каждый раз при сохранении изменений в HTML-файле в процессе преобразования вырезаются комментарии, чтобы можно было использовать заключенную в них разметку ASP.NET.
  
    
    

### <a name="types-of-markup"></a>Типы разметки

Ниже представлены типы разметки, которые добавляются в HTML-файл.
  
    
    

- **Свойства документа.** Тег **\<mso\>** содержит метаданные SharePoint, в том числе сведения о самом файле и некоторые свойства, необходимые для успешного преобразования в MASTER-файл.
    
```HTML
  
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
```

- **Регистрация пространства имен SharePoint.** Тег **\<SPM\>** ("разметка SharePoint") содержит строку, регистрирующую пространство имен SharePoint.
    
```HTML
  
<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

- **Комментарии.** Теги **\<CS\>** и **\<CE\>** (начало и конец комментария) игнорируются во время преобразования. Эти теги призваны помочь вам проанализировать строки разметки.
    
```HTML
  
<!--CS: Start Page Head Contents Snippet-->
…
<!--CE: End Page Head Contents Snippet-->

  <!--CS: Start Ribbon Snippet-->
…
<!--CE: End Ribbon Snippet-->

<!--CS: Start PlaceHolderMain Snippet-->
…
<!--CE: End PlaceHolderMain Snippet-->
```

- **Фрагменты кода.** Теги **\<MS\>** и **\<ME\>** (начало и конец разметки) обозначают начало и конец элемента управления SharePoint или фрагмента кода. Фрагмент кода — это элемент управления SharePoint, добавляющий функции SharePoint на страницу. Вы можете добавлять их самостоятельно с помощью коллекции фрагментов кода. Дополнительные сведения см. в статье [Фрагменты кода в компоненте "Дизайнер" SharePoint](sharepoint-design-manager-snippets.md).
    
```HTML
  
<!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
```

- **Блоки предварительного просмотра**. Теги **\<PS\>** и **\<PE\>** (начало и конец предварительного просмотра) окружают раздел HTML-кода, который не следует редактировать, так как этот раздел влияет только на предварительный просмотр в ходе разработки. Эти разделы представляют собой моментальный снимок элемента управления SharePoint, вставляемого фрагментом кода. Предварительный просмотр помогает более осознанно работать с HTML-файлом в клиентском редакторе HTML. Однако изменение контента или стилей для предварительного просмотра не окажет долговременного влияния на MASTER-файл, который в конечном итоге использует SharePoint. Чтобы применить стиль к фрагменту кода, необходимо идентифицировать и переопределить стили SharePoint в пользовательской таблице CSS.
    
```HTML
  
<!--PS: Start of READ-ONLY PREVIEW (do not modify) -->
<div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div>
<!--PE: End of READ-ONLY PREVIEW -->
```

- **Идентификаторы SharePoint**. С двумя фрагментами кода, добавляемыми в HTML-файл в ходе преобразования ("Содержимое заголовка страницы" и "Лента SharePoint"), связаны идентификаторы SharePoint или SID (00 и 02 соответственно). Эти идентификаторы позволяют сократить фрагменты кода и сделать HTML-код страницы более удобочитаемым.
    
```HTML
  
<!--SID:00 -->

<!--SID:02 {Ribbon}-->
```


### <a name="added-snippets"></a>Добавленные фрагменты кода

Важно знать о двух фрагментах кода, которые будут добавлены в HTML-файл. Эти фрагменты кода добавляются автоматически во время преобразования, но они могут быть недоступны для добавления из коллекции фрагментов кода.
  
    
    

- **Лента**. Чтобы авторы контента могли создавать страницы и контент на сайте SharePoint, эталонной странице необходимы лента и "навигация по набору" — новая функция SharePoint. Лента содержится во фрагменте кода для фильтрации по ролям безопасности, поэтому когда посетитель просматривает сайт, лента видна только пользователям, прошедшим проверку подлинности, и не видна анонимным пользователям. Вы можете переместить ленту в другое место страницы или стиля, переопределив стандартные классы CSS, но не рекомендуем перемещать и менять местами компоненты (например, меню "Действия сайта") на ленте.
    
```HTML
  
<!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
<!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
<!--ME:</wssucw:Welcome>-->
<!--ME:</SharePoint:SPSecurityTrimmedControl>-->
```

- **ContentPlaceHolderMain**. В конце тега **\<div id="s4-bodyContainer"\>** (перед закрывающим тегом **\</body\>**) в ходе преобразования вставляется заполнитель контента с именем **PlaceHolderMain**. Внутри этого фрагмента находится желтый тег **\<div\>** с черными границами, который отображается в представлении конструктора в редакторе HTML или в окне предварительного просмотра на сервере в компоненте "Дизайнер".
    
    Этот тег **\<div\>** представляет область, в которую будет добавлен контент, заданный макетами страниц и самими страницами. Фрагмент **PlaceHolderMain** следует переместить в ту область эталонной страницы, которую заполнят макеты страниц, — область структуры сайта, которая отличается на разных страницах сайта.
    


```HTML
  
<!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
```


## <a name="reference-examples-of-sharepoint-markup-added-to-the-html-file"></a>Справочник. Примеры разметки SharePoint, добавленной в HTML-файл
<a name="Reference"> </a>

Ниже приведен пример разметки, добавленной в HTML-файл после его преобразования в эталонную страницу.
  
    
    

### <a name="markup-added-to-the-head-tag"></a>Разметка, добавленная в тег \<head\>


```HTML

<head>
        <meta http-equiv="X-UA-Compatible" content="IE=10" />
        <!--CS: Start Page Head Contents Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SID:00 -->
        <meta name="GENERATOR" content="Microsoft SharePoint" />
        <meta http-equiv="Content-type" content="text/html; charset=utf-8" />
        <meta http-equiv="Expires" content="0" />
        <!--MS:<SharePoint:RobotsMetaTag runat="server">-->
        <!--ME:</SharePoint:RobotsMetaTag>-->
        <!--MS:<SharePoint:PageTitle runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">-->
                <!--MS:<SharePoint:ProjectProperty Property="Title" runat="server">-->
                <!--ME:</SharePoint:ProjectProperty>-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:PageTitle>-->
        <!--MS:<SharePoint:StartScript runat="server">-->
        <!--ME:</SharePoint:StartScript>-->
        <!--MS:<SharePoint:CssLink runat="server" Version="15">-->
        <!--ME:</SharePoint:CssLink>-->
        <!--MS:<SharePoint:CacheManifestLink runat="server">-->
        <!--ME:</SharePoint:CacheManifestLink>-->
        <!--MS:<SharePoint:PageRenderMode runat="server" RenderModeType="Standard">-->
        <!--ME:</SharePoint:PageRenderMode>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="core.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="menu.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="callout.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="sharing.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:ScriptLink language="javascript" name="suitelinks.js" OnDemand="true" runat="server" Localizable="false">-->
        <!--ME:</SharePoint:ScriptLink>-->
        <!--MS:<SharePoint:CustomJSUrl runat="server">-->
        <!--ME:</SharePoint:CustomJSUrl>-->
        <!--MS:<SharePoint:SoapDiscoveryLink runat="server">-->
        <!--ME:</SharePoint:SoapDiscoveryLink>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaPlaceHolderAdditionalPageHead" Container="false" runat="server">-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderAdditionalPageHead" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
            <!--MS:<SharePoint:DelegateControl runat="server" ControlId="AdditionalPageHead" AllowMultipleControls="true">-->
            <!--ME:</SharePoint:DelegateControl>-->
            <!--MS:<asp:ContentPlaceHolder id="PlaceHolderBodyAreaClass" runat="server">-->
            <!--ME:</asp:ContentPlaceHolder>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--MS:<SharePoint:CssRegistration Name="Themable/corev15.css" runat="server">-->
        <!--ME:</SharePoint:CssRegistration>-->
        <!--MS:<SharePoint:AjaxDelta id="DeltaSPWebPartManager" runat="server">-->
            <!--MS:<WebPartPages:SPWebPartManager runat="server">-->
            <!--ME:</WebPartPages:SPWebPartManager>-->
        <!--ME:</SharePoint:AjaxDelta>-->
        <!--CE: End Page Head Contents Snippet-->
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <!--DC:Business Solutions-->
        <link rel="stylesheet" href="css/style.css" type="text/css" charset="utf-8" />
        <!--[if lte IE 7]>
  <link rel="stylesheet" href="css/ie.css" type="text/css" charset="utf-8"/> 
 <![endif]-->
        <!--[if gte mso 9]><xml>
<mso:CustomDocumentProperties>
<mso:HtmlDesignFromMaster msdt:dt="string"></mso:HtmlDesignFromMaster>
<mso:HtmlDesignStatusAndPreview msdt:dt="string">http://[server_name]/sites/PubSite/_catalogs/masterpage/[site_name]/index.html, Conversion successful.</mso:HtmlDesignStatusAndPreview>
<mso:ContentTypeId msdt:dt="string">0x0101000F1C8B9E0EB4BE489F09807B2C53288F0054AD6EF48B9F7B45A142F8173F171BD10003D357F861E29844953D5CAA1D4D8A3A0084F0F9C7FCB65541A59990D173DA60FA</mso:ContentTypeId>
<mso:HtmlDesignAssociated msdt:dt="string">1</mso:HtmlDesignAssociated>
<mso:HtmlDesignConversionSucceeded msdt:dt="string">True</mso:HtmlDesignConversionSucceeded>
</mso:CustomDocumentProperties>
</xml><![endif]-->
    </head>

```


### <a name="markup-added-after-the-start-body-tag"></a>Разметка, добавленная после открывающего тега \<body\>


#### <a name="ribbon-snippet"></a>Фрагмент кода ленты


```HTML

<!--CS: Start Ribbon Snippet-->
        <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
        <!--SPM:<%@Register Tagprefix="wssucw" TagName="Welcome" Src="~/_controltemplates/15/Welcome.ascx"%>-->
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" HideFromSearchCrawler="true" EmitDiv="true">-->
            <div id="TurnOnAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOnAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(true);UpdateAccessibilityUI();document.getElementById('linkTurnOffAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnonaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
            <div id="TurnOffAccessibility" style="display:none" class="s4-notdlg noindex">
                <a id="linkTurnOffAcc" href="#" class="ms-accessible ms-acc-button" onclick="SetIsAccessibilityFeatureEnabled(false);UpdateAccessibilityUI();document.getElementById('linkTurnOnAcc').focus();return false;">
                    <!--MS:<SharePoint:EncodedLiteral runat="server" text="&amp;lt;%$Resources:wss,master_turnoffaccessibility%&amp;gt;" EncodeMethod="HtmlEncode">-->
                    <!--ME:</SharePoint:EncodedLiteral>-->
                </a>
            </div>
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <div id="ms-designer-ribbon">
            <!--SID:02 {Ribbon}-->
            <!--PS: Start of READ-ONLY PREVIEW (do not modify) --><div class="DefaultContentBlock" style="background:rgb(0, 114, 198); color:white; width:100%; padding:8px; height:64px; overflow:hidden;">The SharePoint ribbon will be here when your file is either previewed on or applied to your site.</div><!--PE: End of READ-ONLY PREVIEW -->
        </div>
        <!--MS:<SharePoint:SPSecurityTrimmedControl runat="server" AuthenticationRestrictions="AnonymousUsersOnly">-->
            <!--MS:<wssucw:Welcome runat="server" EnableViewState="false">-->
            <!--ME:</wssucw:Welcome>-->
        <!--ME:</SharePoint:SPSecurityTrimmedControl>-->
        <!--CE: End Ribbon Snippet-->

```


#### <a name="two-sharepoint-div-tags"></a>Два тега \<div\> в SharePoint


```HTML

<div id="s4-workspace">
            <div id="s4-bodyContainer">

```


### <a name="markup-added-before-the-closing-body-tag-and-two-closing-div-tags"></a>Разметка, добавленная перед закрывающим тегом \</body\> и двумя закрывающими тегами \</div\>


```HTML

<div data-name="ContentPlaceHolderMain">
                    <!--CS: Start PlaceHolderMain Snippet-->
                    <!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
                    <!--MS:<SharePoint:AjaxDelta ID="DeltaPlaceHolderMain" IsMainContent="true" runat="server">-->
                        <!--MS:<asp:ContentPlaceHolder ID="PlaceHolderMain" runat="server">-->
                            <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
            This div, which you should delete, represents the content area that your Page Layouts and pages will fill. Design your Master Page around this content placeholder.
        
                            </div>
                        <!--ME:</asp:ContentPlaceHolder>-->
                    <!--ME:</SharePoint:AjaxDelta>-->
                    <!--CE: End PlaceHolderMain Snippet-->
                </div>

```


## <a name="see-also"></a>См. также
<a name="Additional"> </a>


-  [Обзор Дизайнера в SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md)
    
  

