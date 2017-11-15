---
title: "Как применение стилей поля страниц в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e227613d-0e4d-4312-924d-bb55e1fe4293
ms.openlocfilehash: f8651a073c67d67e5a20a805c6bb9a2356141ae8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-apply-styles-to-page-fields-in-sharepoint"></a>Как: применение стилей поля страниц в SharePoint
В макете страницы можно применить стили для поля страницы, и эти стили, применяются к любое содержимое, добавленные в окончательную авторы контента при создании страницы из макета страницы. Кроме того вы имеют параметры для управления стилями содержимого в поле страницы RichHtmlField.
## <a name="introduction-to-applying-styles-to-page-fields"></a>Общие сведения о применение стилей поля страниц
<a name="Introduction"> </a>

Разработчик у вас есть полный контроль над расположения и стиля поля страниц на макет страницы и всех страниц, созданных в этом макете страницы. При авторы контента создавать страницы из браузера, нельзя перемещать поля страницы на странице или переопределяют стили, которые можно указать. Это гарантирует, что ваше фирменной символики читаемых через все страницы на сайте.
  
    
    
Существует две основные категории типов полей, которые следует учитывать применить стили для поля страницы.
  
    
    

- **Типы полей, отличные от RichHtmlField** Поля страниц, которые будут включены в макете страницы соответствует тип контента для макета страницы. В поле страницы может быть множество типов, таких как однострочного текста (текстовое поле) или многострочный текст (NoteField). Разработчик будут применяться стили для всех этих полей страницы таким же образом, с помощью стилей в поле страницы непосредственно в макет страницы.
    
  
- **RichHtmlField** Управления поля форматированного HTML (HTML публикации поле)  наиболее эффективные и часто используемых элементов управления в макеты страниц. По умолчанию в поле с расширенными возможностями HTML авторы контента используют ленты для форматирования и применения стилей к содержимому, а для вставки таблицы, мультимедиа, такие как изображения и видео- и веб-частей. Этот тип поля полезен, когда нужно предоставить возможность добавлять и стиля содержимого, которые можно управлять параметрами авторы контента. Можно управлять RichHtmlField двумя способами:
    
  - **Создание пользовательской таблицы стилей** По умолчанию стили, доступные на ленте RichHtmlField поступают из таблицы стилей с именем HtmlEditorStyles.css. Свойство **PrefixStyleSheet** в этом фрагменте можно настроить для отображения на ленте авторам использовать настраиваемые стили.
    
  
  - **Настройка свойств разрешить** Фрагмент кода для RichHtmlField имеет 28 доступные свойства, которые начинаются с **Allow**и сделать определенные команды или группы команд на ленте, становится недоступной для авторы содержимого можно использовать эти свойства. Например если значение свойства **AllowFontsMenu** **False**, авторы нельзя использовать меню «Шрифт» на ленте для изменения какие шрифта применяется к тексту; Вместо этого они могут использовать стили CSS, которые можно указать.
    
  
Для всех типов полей страницы, включая RichHtmlField конструкторе определяет, как содержимое со стилями. RichHtmlField можно использовать для предоставления авторы контента свободу действий для вставки Форматированный контент и применения стилей; по-прежнему имеет полный контроль над можно добавлять содержимое и стили, что может применяться.
  
    
    

## <a name="applying-styles-to-page-fields-other-than-richhtmlfield"></a>Применение стилей к поля страниц, отличный от RichHtmlField
<a name="Applying"> </a>

С помощью элемента управления поля страницы можно определить стили, используемые контента. Авторы могут добавить содержимое на страницу, но конструктора элементов управления, как этот контент визуализируется с помощью CSS применяется для этих элементов управления.
  
    
    
В разметке страницы HTML каждое поле страницы заключено в тег **\<div\>**. Чтобы применить стиль к полю страницы, вы можете просто добавить стиль к тегу **\<div\>**, например `<div style="font-weight:bold"`. Однако более распространенный и удобный способ — добавление атрибута **id** в тег **\<div\>** для каждого поля страницы в разметке с последующим использованием атрибута **id** для выбора стилей во внешней таблице стилей. Таким образом, если у вас есть несколько каналов устройств, а у каждого канала есть своя таблица стилей, вы можете применить разные стили к каждому полю страницы для каждого канала. Например, приведенное ниже поле страницы типа TextField (другое название — "Многострочный текст") может содержать только атрибут **id** в теге **\<div\>**.
  
    
    



```HTML

<div id="ShortSummaryPageField">
<!--CS: Start Page Field: ShortSummary Snippet-->
<!--SPM:<%@Register Tagprefix="PageFieldNoteField" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<PageFieldNoteField:NoteField FieldName="a5249942-2dc5-4917-85e2-661d019ad548" runat="server">-->
<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><div align="left" class="ms-formfieldcontainer"><div class="ms-formfieldlabelcontainer" nowrap="nowrap"><span class="ms-formfieldlabel" nowrap="nowrap">ShortSummary</span></div><div class="ms-formfieldvaluecontainer"><div class="ms-rtestate-field">ShortSummary field value.</div></div></div><!--PE: End of READ-ONLY PREVIEW-->
<!--ME:</PageFieldNoteField:NoteField>-->
<!--CE: End Page Field: ShortSummary Snippet-->
</div>
```

Дополнительные сведения о котором должен приходить стили и ссылки на стиль для макета страницы содержатся в разделе  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
  
    
    

## <a name="disabling-options-on-the-ribbon-of-a-richhtmlfield"></a>Отключение параметров на ленте RichHtmlField
<a name="Disabling"> </a>

Когда авторы контента создать или изменить страницу и добавлять содержимое RichHtmlField, с помощью браузера, их можно использовать команды на ленте для этого поля для форматирования стиля, или вставки Форматированный контент и мультимедиа. 
  
    
    
В коллекция фрагментов кода можно настроить свойства поля страницы типа RichHtmlField, таким образом, чтобы определенные команды или группы команд на ленте, становятся недоступными для авторов. К примеру задав свойство **AllowFontSizesMenu** **False**, можно отключить **Font Size** меню ленты. Свойства **AllowFonts** значение **False**, можно отключить всей группы **шрифта** на ленте.
  
    
    
После настройки этих свойств в коллекция фрагментов кода и затем обновить фрагмента в разметке фрагмент внутри комментария  `<!--MS:>` отображаются свойства.
  
    
    



```HTML

<div data-name="Page Field: ArticleBody">
<!--CS: Start Page Field: ArticleBody Snippet-->
<!--SPM:<%@Register Tagprefix="PageFieldRichHtmlField" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<PageFieldRichHtmlField:RichHtmlField runat="server" AllowFonts="False" FieldName="db3168db-8778-4fb6-a48f-57f598497388">-->
<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><div id="ctl02_label" style="display:none">ArticleBody</div><div id="ctl02__ControlWrapper_RichHtmlField" class="ms-rtestate-field" style="display:inline" aria-labelledby="ctl02_label"><div align="left" class="ms-formfieldcontainer"><div class="ms-formfieldlabelcontainer" nowrap="nowrap"><span class="ms-formfieldlabel" nowrap="nowrap">ArticleBody</span></div><div class="ms-formfieldvaluecontainer"><div class="ms-rtestate-field">ArticleBody field value. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div></div></div></div>
<!--PE: End of READ-ONLY PREVIEW-->
<!--ME:</PageFieldRichHtmlField:RichHtmlField>-->
<!--CE: End Page Field: ArticleBody Snippet-->
</div>
```


> **Примечание.** Если задать для атрибута **AllowFonts** значение **False**, создатели контента по-прежнему смогут использовать такие сочетания клавиш, как CTRL+B (жирный шрифт), для форматирования текста. Чтобы авторы не могли добавлять к тексту стили, вы можете задать для атрибута **AllowTextMarkup** значение **False**. В этом случае, когда автор пытается сохранить контент, где к тексту применены стили, редактор HTML в браузере возвращает ошибку и предлагает автору удалить недопустимую разметку. 
  
    
    

В поле страницы RichHtmlField содержит 28 различных **Allow** свойства. Дополнительные сведения о какой элемент управления определенных свойств [Свойства RichHtmlField](http://msdn.microsoft.com/en-us/library/microsoft.sharepoint.publishing.webcontrols.richhtmlfield_properties) более подробные сведения добавлении и настройке фрагменты кода, посмотрите [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).
  
    
    

## <a name="controlling-the-styles-available-in-a-richhtmlfield"></a>Управление стили, доступные в RichHtmlField
<a name="Controlling"> </a>

В RichHtmlField авторы контента можно использовать параметры на ленте на форматирование содержимого. Эти параметры форматирования реализуются с помощью CSS и эти стили, определяются в таблицы стилей SharePoint, с именем HtmlEditorStyles.css, который находится на сервере в одном из следующих расположений:
  
    
    

- C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES 
    
  
- C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\FEATURES\\PublishingLayouts\\en-"мне нравится"
    
  
Так как RichHtmlField в браузере используется для реализации его стили CSS, можно создать собственные стили, которые совместимы с использованием фирменной символики сайта и затем вы можете предоставить эти стили на ленте для авторы контента для использования. Чтобы внесены незначительные изменения стилей по умолчанию, можно скопировать существующий стиль из HtmlEditorStyles.css таблицы стилей, на который ссылается макет страницы и измените стиля с помощью изменения свойства CSS и значения (но не "Выбор"). Также можно скрыть стили по умолчанию из ленты, скопировав вашей таблицы стилей, а затем параметр  `display:none`.
  
    
    
Чтобы реализовать настраиваемые стили, вы также создавать таблицы стилей с нуля путем изменения свойства **PrefixStyleSheet** для фрагмента RichHtmlField. По умолчанию это свойство имеет значение **ms-rte**и стилей в таблицу стилей по умолчанию HtmlEditorStyles.css каждого начинаются с данного префикса  например:
  
    
    



```HTML

H1. ms-rteElement-H1
{
-ms-name:"Heading 1";
-ms-element:"true";
}
```

При изменении значения свойства **PrefixStyleSheet** существующих стилей **ms-rte** нет в полнофункциональный редактор HTML и авторы контента доступны только стили, которые вы создаете, использующие новый префикс. Это означает, что если вы хотите использовать часть стилей по умолчанию, их необходимо скопировать в таблице стилей и изменения, чтобы они использовали новый префикс.
  
    
    

> **Примечание.** Свойство **PrefixStyleSheet** определяется для каждого поля страницы RichHtmlField, но в нескольких полях страницы для этого свойства может быть задано одно и то же значение. Таким образом, если несколько макетов страниц ссылаются на одну и ту же таблицу стилей, то несколько полей RichHtmlField в этих макетах могут содержать один и тот же префикс стиля и ссылаться на одни и те же стили.
  
    
    


### <a name="to-define-a-new-list-of-styles-for-a-richhtmlfield"></a>Определение нового списка стилей для объекта RichHtmlField


1. Перейдите на сайт публикации.
    
  
2. В правом верхнем углу страницы выберите пункт **Параметры**, а затем выберите **Дизайнер**.
    
  
3. В Дизайнере в левой области панели навигации выберите команду **Изменить макеты страниц**.
    
  
4. Выберите макет страницы, на котором будет находиться в поле страницы RichHtmlField.
    
  
5. В правом верхнем углу preview на сервере выберите **Коллекция фрагментов кода**.
    
  
6. На ленте выберите **Поля страниц** и выберите поле страницы типа **RichHtmlField**.
    
  
7. В сетке свойств разверните раздел **Разное** и затем измените свойство **PrefixStyleSheet** значение, отличное от **ms-rte** например, измените значение, которое должно **customstyle**.
    
    > **Важно!** Значение этого свойства должно быть целиком представлено в нижнем регистре. 
8. Нажмите **Обновить**.
    
  
9. В левой части коллекция фрагментов кода выберите команду **Копировать в буфер обмена**.
    
  
10. На сопоставленном сетевом диске на компьютере откройте макет HTML-страницы в редакторе HTML.
    
    > **Примечание.** Дополнительные сведения см. в статье [Инструкции. Сопоставление сетевого диска с коллекцией эталонных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md). 
11. В макете HTML-страницы вставьте фрагмент кода HTML в разделе **PlaceHolderMain**.
    
  
12. Сохраните макет страницы HTML. Макет страницы связанного .aspx синхронизации изменений в HTML-файл.
    
    На этом этапе Если автор создает или изменяет страница, основанная на этот макет страницы, без стилей доступны на ленте в редакторе HTML, так как это поле определенных параметров страницы используется только стили, начинающихся с новой префикс **customstyle**, но эти стили еще не определен.
    
  
13. На сервере перейдите к следующей папке и откройте HtmlEditorStyles.css:
    
    C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES
    
    Полезно для просмотра стилей по умолчанию, понимать, как они записываются в случае и возможно повторно использовать некоторые из них копировать их в таблице стилей и их изменение. После этого замените префикс по умолчанию **ms-rte** свои собственные префикса.
    
    > **Важно!** Не меняйте используемую по умолчанию таблицу стилей HtmlEditorStyles.css. Она предоставляет стили для каждого объекта RichHtmlField в ферме. Кроме того, при обновлении служб или установке новой версии этот файл может быть перезаписан, что приведет к потере всех изменений. 
14. Создайте в таблице стилей список новых стилей с новым префиксом.
    
    Например если **customstyle** новый префикс, таблицы стилей может содержать следующий стиль.
    


```HTML
  
H2.customstyleElement-H2
{
-ms-name:"Heading 2";
-ms-element:"true";
}
customstyleElement-H2
{
font-weight: bold;
font-family: Cambria;
font-size: 16pt;
} 

```


    For clarity, the class name and the name of the style as it appears on the ribbon are defined separately from the style properties. In this example, **H2** is the element selector for the style, and **customstyleElement-H2** is the class name of the style. The class name has two parts: **customstyle** is the prefix that you specified for this page field, and **Element** specifies that this style will appear in the **Page Elements** section of the **Styles** gallery on the ribbon of the HTML editor. The **-ms-name** property sets the display name that appears to content authors in the Styles gallery.
    
    SharePoint maps a style to a menu or command on the ribbon by parsing the class name immediately after the prefix and looking for one of these strings:
    
  - **Element**: раздел элементы страниц из коллекции стилей
    
  
  - **Style**: раздел стили текста из коллекции стилей
    
  
  - **FontSize**: размер шрифта меню
    
  
  - **ThemeFontFace**: меню "Шрифт"
    
  
  - **ForeColor**: меню Цвет шрифта
    
  
  - **BackColor**: выделение цветом меню
    
  
  - **Image**: меню "изображение"
    
  
  - **Table**: меню таблицы
    
  
  - **Position**: выравнивание кнопок в группе абзаца
    
  

    Дополнительные сведения о котором должно находиться стили для макета страницы содержатся в разделе  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="Additional"> </a>


-  [Обзор Дизайнера в SharePoint](overview-of-design-manager-in-sharepoint.md)
    
  
-  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md)
    
  

