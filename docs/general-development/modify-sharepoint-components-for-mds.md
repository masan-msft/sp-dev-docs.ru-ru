---
title: "Изменение компонентов SharePoint для MDS"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c967be7c-f29f-481a-9ce2-915ead315dcd
ms.openlocfilehash: 4639c5c0c53dfa080081316d744614db1b1bcc68
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="modify-sharepoint-components-for-mds"></a>Изменение компонентов SharePoint для MDS
Узнайте, как изменить компоненты проекта SharePoint, чтобы использовать преимущества из минимальной загрузки стратегии (MDS) в SharePoint.
Стратегия минимальной загрузки (MDS) позволяет повысить удобство работы пользователей, возвращая с сервера только части страницы, необходимые для отображения должным образом в браузере. Так как страница полностью отображаться не возвращается клиенту, сервер должен быть точно определить части, которые необходимы для отображения страницы. Может потребоваться изменить компоненты в проекте SharePoint, чтобы они помечаются как спецификации MDS и может работать с обработчиком MDS. Дополнительные сведения о MDS в [обзоре стратегия минимальной загрузки](minimal-download-strategy-overview.md).
  
    
    


## <a name="why-modify-sharepoint-components"></a>Почему изменения компонентов SharePoint ?
<a name="bk_whymodify"> </a>

Как описано в  [Общие сведения о минимальной загрузки стратегия](minimal-download-strategy-overview.md)элементы управления SharePoint работают ли изменять их пользоваться всеми преимуществами MDS. Тем не менее когда компонентов не соответствует спецификации MDS, модуль MDS вопросы обработки отказа. В отработки отказа модуль MDS принимает дополнительных кругового пути для перенаправления браузера с полной версией новая страница, которого занимает определенное время. Пользователи имеют наилучшего взаимодействия при изменении компоненты для работы с MDS и избежать обработки отказа каждый раз, когда они перейдите на новую страницу в SharePoint. Обычно требуется изменять главные страницы, ASP.NET страниц, элементов управления и веб-частей. 
  
    
    

  
    
    

## <a name="master-pages"></a>Эталонные страницы.
<a name="SP15MDSDev_MasterPages"> </a>

Главная страница предоставляет шаблон, который позволяет MDS определение области контента, которые должны быть обновлены когда кто-то переходит на новую страницу. Оптимизация главных страниц является одним из наиболее важных шагов, необходимо выполнить по оптимизации производительности, так как главные страницы определение разделов, которые требуют обновления контента. Главная страница Seattle.master, включенные в состав SharePoint является хорошим примером оптимизированный главной страницы. На рисунке 1 показаны примеры компонентов на главной странице Seattle.master, измените со страницы на страницу, например (1) основной области содержимого, (2) левой панели навигации и заголовок страницы (3).
  
    
    

**На рисунке 1. Компоненты, которые необходимо обновить на главной странице**  
    
![Компоненты, которые необходимо обновить на главной странице](../images/MDS_SeattleMaster.png)
  
> [!NOTE]
> [!Примечание] Существует множество дополнительных компонентов на главной странице Seattle.master, которые изменяют со страницы на страницу, например, таблицы стилей и файлы JavaScript. На рисунке 1 показано только несколько примеров. 
  
    
    

Существуют различные шаблоны для оптимизации компонентов в главную страницу. Шаблон можно использовать для следующих компонентов:
  
    
    

- HTML-код области и элементов управления
    
  
- Таблицы стилей
    
  
- файлы JavaScript;
    
  
- Заголовок страницы
    
  
HTML-код области и элементы управления являются MDS совместимые, если они помещаются в тегах **SharePoint:AjaxDelta**. Перенос контента в **SharePoint:AjaxDelta** теги, передача сигналов, что модуль MDS следует обновить вложенных элементов и HTML. Если элемент управления или раздел HTML не изменяется со страницы на страницу, он не будут отправляться клиенту. Таким образом необходимо учитывать следующие элементы управления вне **AjaxDelta** тегов. В Seattle.master главной странице показано на рисунке 1 (1) основной области содержимого заключается в теги **AjaxDelta**, как показано ниже.
  
    
    



```cs
<SharePoint:AjaxDelta
            id="DeltaPlaceHolderMain"
            BlockElement="true"
            IsMainContent="true"
            runat="server">
    <a id="mainContent" name="mainContent" tabindex="-1"></a>
    <asp:ContentPlaceHolder id="PlaceHolderMain" runat="server" />
</SharePoint:AjaxDelta>
```

Другой пример шаблона **AjaxDelta**  (2) левой панели навигации на рисунке 1. В следующем коде показано, как элемент управления заключается в **AjaxDelta** тегов, а также множество элементов управления и HTML-код.
  
    
    



```cs
<SharePoint:AjaxDelta
            id="DeltaPlaceHolderLeftNavBar"
            BlockElement="true"
            CssClass="ms-core-navigation"
            role="navigation"
            runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderLeftNavBar" runat="server">
        <a id="startNavigation" name="startNavigation" tabIndex="-1"></a>
        <asp:ContentPlaceHolder id="PlaceHolderLeftNavBarTop" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderQuickLaunchTop" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderLeftNavBarDataSource" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderCalendarNavigator" runat="server" />
        <asp:ContentPlaceHolder id="PlaceHolderLeftActions" runat="server" />
        <!-- There are more controls and HTML in this placeholder in the Seattle master page -->
    </asp:ContentPlaceHolder>
</SharePoint:AjaxDelta>
```

Кое-что необходимо помнить о тегах **AjaxDelta**  это невозможно вложить их. Теги **AjaxDelta** на верхнем уровне необходимые необходимо указать в структуре главной страницы.
  
    
    
Последний пример на рисунке 1  Заголовок страницы (3), в котором требуется специальный шаблон, который используется тег **SharePoint:PageTitle**. В следующем коде показан тег **PageTitle** как используется на главной странице Seattle.master.
  
    
    



```cs

<SharePoint:PageTitle runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">
        <SharePoint:ProjectProperty Property="Title" runat="server" />
    </asp:ContentPlaceHolder>
</SharePoint:PageTitle>
```

Главная страница также может включать файлы JavaScript и таблицы стилей. Ядро сервера необходимо определить CSS и JavaScript необходимые файлы. Чтобы определить ресурсы файлы CSS при необходимости, используйте следующий шаблон.
  
    
    



```cs

<SharePoint:CssLink runat="server" Version="15"/>
<SharePoint:CssRegistration Name="my_styles.css" runat="server" />
```

Обратите внимание на то, что у вас есть только один тег **CssLink** на главную страницу, но может вызывать много тегов **CssRegistration**, можно добавить множество CSS-файлы. Используйте следующий шаблон для файлов JavaScript.
  
    
    



```cs

<SharePoint:ScriptLink language="javascript" name="my_javascript.js" runat="server" />
```

Включая файлы CSS и JavaScript с помощью **style** и **script** теги HTML в MDS не поддерживается.
  
    
    

## <a name="aspnet-pages"></a>Страницы ASP.NET
<a name="SP15MDSDev_ASPNET"> </a>

Проект содержит ASP.NET страниц, вероятно, требуется ли ссылки на файлы CSS и JavaScript. Теги HTML **style** и **script** не совместимы с MDS. Используйте шаблоны **CssRegistration** и **ScriptLink**, описано в предыдущем разделе.
  
    
    
На страницах ASP.NET могут также использовать метод **Response.Output** для записи содержимого на страницу, которая не допускается в MDS. Вместо этого можно использовать следующие методы спецификации MDS класса [SPHttpUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.aspx) :
  
    
    

-  [WriteNoEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteNoEncode.aspx)
    
  
-  [WriteHtmlEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncode.aspx)
    
  
-  [WriteEcmaScriptStringLiteralEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteEcmaScriptStringLiteralEncode.aspx)
    
  
-  [WriteHtmlEncodeAllowSimpleTextFormatting()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncodeAllowSimpleTextFormatting.aspx)
    
  
-  [WriteHtmlUrlAttributeEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlUrlAttributeEncode.aspx)
    
  
-  [WriteUrlKeyValueEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlKeyValueEncode.aspx)
    
  
-  [WriteUrlPathEncode()](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlPathEncode.aspx)
    
  
Помимо ссылки на файлы JavaScript, ASP.NET страниц может иметь JavaScript встроенного кода. Использовать следующий шаблон, чтобы сделать сценарий блокирует MDS совместимые.
  
    
    



```cs
<SharePoint:ScriptBlock runat="server" >
    // Your JavaScript code here.
</SharePoint:ScriptBlock>
```


## <a name="controls-and-web-parts"></a>Элементы управления и веб-частей
<a name="SP15MDSDev_WebParts"> </a>

Необходимо также отметить веб-частей и элементов управления, как MDS спецификации. В следующем коде показан шаблон для использования.
  
    
    

```cs

[assembly: Microsoft.SharePoint.WebControlssCompliantAttribute(IsCompliant = true)]
namespace VisualWebPartProject2.VisualWebPart1
{
    // Rest of your control logic
```

Кроме того элементов управления и веб-частей должны регистрировать свои ресурсы с помощью методов в классе  [SPPageContentManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPPageContentManager.aspx) . Основные ресурсы, JavaScript фрагменты кода и скрытые файлы, которые могут быть зарегистрированы с помощью **RegisterClientScriptBlock** и **RegisterHiddenField**.
  
    
    
Веб-частей и элементов управления можно также использовать XSLT-файлов для управления процессом визуализации. XSLT-файлы могут иметь вложенные JavaScript кода или файлов. Модуль MDS необходимо знать об этих ресурсов. Можно регистрировать JavaScript ресурсы, с помощью объекта расширения XSLT с именем **pcm**. Хорошим примером того, как использовать объект **pcm** содержится в файле TEMPLATE\\LAYOUTS\\XSL\\fldtypes.xsl %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\. В следующем коде показано, как файл **fldtypes.xsl** использует объект **pcm** для регистрации JavaScript ресурсы.
  
    
    



```XML

<xsl:value-of select="pcm:RegisterScriptBlock(concat('block1',$ViewCounter), string($scriptbody1))"/>
<xsl:value-of select="pcm:RegisterScriptLink('/_layouts/15/wssactionmenu.js')"/>
```


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Общие сведения о минимальной загрузки стратегия](minimal-download-strategy-overview.md)
    
  
-  [Создание сайтов для SharePoint](build-sites-for-sharepoint.md)
    
  

