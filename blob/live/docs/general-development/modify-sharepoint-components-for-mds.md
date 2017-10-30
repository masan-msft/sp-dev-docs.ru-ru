---
title: "Изменение компонентов SharePoint для MDS"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c967be7c-f29f-481a-9ce2-915ead315dcd
ms.openlocfilehash: 697a284f3d07c6b3ddcdad005578ba3f9f7700ac
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="modify-sharepoint-components-for-mds"></a><span data-ttu-id="9bcde-102">Изменение компонентов SharePoint для MDS</span><span class="sxs-lookup"><span data-stu-id="9bcde-102">Modify SharePoint components for MDS</span></span>
<span data-ttu-id="9bcde-103">Узнайте, как изменить компоненты проекта SharePoint, чтобы использовать преимущества из минимальной загрузки стратегии (MDS) в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9bcde-103">Learn how to modify the components in your SharePoint project to take advantage of Minimal Download Strategy (MDS) in SharePoint.</span></span>
<span data-ttu-id="9bcde-104">Стратегия минимальной загрузки (MDS) позволяет повысить удобство работы пользователей, возвращая с сервера только части страницы, необходимые для отображения должным образом в браузере.</span><span class="sxs-lookup"><span data-stu-id="9bcde-104">Minimal Download Strategy (MDS) improves the user experience by returning from the server only the portions of a page required to render it properly in the browser.</span></span> <span data-ttu-id="9bcde-105">Так как страница полностью отображаться не возвращается клиенту, сервер должен быть точно определить части, которые необходимы для отображения страницы.</span><span class="sxs-lookup"><span data-stu-id="9bcde-105">Because the fully-rendered page is not returned to the client, the server must be able to accurately identify the portions that are required to render the page.</span></span> <span data-ttu-id="9bcde-106">Может потребоваться изменить компоненты в проекте SharePoint, чтобы они помечаются как спецификации MDS и может работать с обработчиком MDS.</span><span class="sxs-lookup"><span data-stu-id="9bcde-106">You might need to modify the components in your SharePoint project so that they are identified as MDS-compliant and can work with the MDS engine.</span></span> <span data-ttu-id="9bcde-107">Дополнительные сведения о MDS в [обзоре стратегия минимальной загрузки](minimal-download-strategy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bcde-107">Learn more about MDS in  [Minimal Download Strategy overview](minimal-download-strategy-overview.md).</span></span>
  
    
    


## <a name="why-modify-sharepoint-components"></a><span data-ttu-id="9bcde-108">Почему изменения компонентов SharePoint ?</span><span class="sxs-lookup"><span data-stu-id="9bcde-108">Why modify SharePoint components?</span></span>
<span data-ttu-id="9bcde-109"><a name="bk_whymodify"> </a></span><span class="sxs-lookup"><span data-stu-id="9bcde-109"><a name="bk_whymodify"> </a></span></span>

<span data-ttu-id="9bcde-p102">Как описано в  [Общие сведения о минимальной загрузки стратегия](minimal-download-strategy-overview.md)элементы управления SharePoint работают ли изменять их пользоваться всеми преимуществами MDS. Тем не менее когда компонентов не соответствует спецификации MDS, модуль MDS вопросы обработки отказа. В отработки отказа модуль MDS принимает дополнительных кругового пути для перенаправления браузера с полной версией новая страница, которого занимает определенное время. Пользователи имеют наилучшего взаимодействия при изменении компоненты для работы с MDS и избежать обработки отказа каждый раз, когда они перейдите на новую страницу в SharePoint. Обычно требуется изменять главные страницы, ASP.NET страниц, элементов управления и веб-частей.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p102">As explained in  [Minimal Download Strategy overview](minimal-download-strategy-overview.md), SharePoint controls work whether or not you modify them to take full advantage of MDS. However, when your components are not MDS compliant, the MDS engine issues a failover. In a failover, the MDS engine takes an extra round trip to redirect the browser to the full version of the new page, which takes time. Users have the best experience when you modify components to work with MDS and avoid a failover every time they browse to a new page in SharePoint. You usually need to modify master pages, ASP.NET pages, controls, and Web Parts.</span></span> 
  
    
    

  
    
    

## <a name="master-pages"></a><span data-ttu-id="9bcde-115">Эталонные страницы.</span><span class="sxs-lookup"><span data-stu-id="9bcde-115">Master pages</span></span>
<span data-ttu-id="9bcde-116"><a name="SP15MDSDev_MasterPages"> </a></span><span class="sxs-lookup"><span data-stu-id="9bcde-116"><a name="SP15MDSDev_MasterPages"> </a></span></span>

<span data-ttu-id="9bcde-p103">Главная страница предоставляет шаблон, который позволяет MDS определение области контента, которые должны быть обновлены когда кто-то переходит на новую страницу. Оптимизация главных страниц является одним из наиболее важных шагов, необходимо выполнить по оптимизации производительности, так как главные страницы определение разделов, которые требуют обновления контента. Главная страница Seattle.master, включенные в состав SharePoint является хорошим примером оптимизированный главной страницы. На рисунке 1 показаны примеры компонентов на главной странице Seattle.master, измените со страницы на страницу, например (1) основной области содержимого, (2) левой панели навигации и заголовок страницы (3).</span><span class="sxs-lookup"><span data-stu-id="9bcde-p103">The master page provides a template that lets MDS identify the content regions that may need to be updated when someone navigates to a new page. Optimizing your master pages is one of the most important steps to take when optimizing performance because master pages identify sections that require updated content.. The Seattle.master master page included with SharePoint is a good example of an optimized master page. Figure 1 shows examples of components in the Seattle.master master page that change from page to page, such as the (1) main content area, (2) left navigation bar, and (3) page title.</span></span>
  
    
    

<span data-ttu-id="9bcde-121">**На рисунке 1. Компоненты, которые необходимо обновить на главной странице**</span><span class="sxs-lookup"><span data-stu-id="9bcde-121">**Figure 1. Components that require updates in a master page**</span></span>

  
    
    

  
    
    
![Компоненты, которые необходимо обновить на главной странице](../images/MDS_SeattleMaster.png)
  
    
    

    
> <span data-ttu-id="9bcde-123">**Примечание:** Существует множество дополнительных компонентов на главной странице Seattle.master, которые изменяют со страницы на страницу, такие как файлы JavaScript и таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="9bcde-123">**Note:** There are many more components in the Seattle.master master page that change from page to page, such as style sheets and JavaScript files.</span></span> <span data-ttu-id="9bcde-124">На рисунке 1 показано только несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="9bcde-124">Figure 1 shows only a few examples.</span></span> 
  
    
    

<span data-ttu-id="9bcde-p105">Существуют различные шаблоны для оптимизации компонентов в главную страницу. Шаблон можно использовать для следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="9bcde-p105">There are different patterns to optimize the components in a master page. You can use a pattern for the following components:</span></span>
  
    
    

- <span data-ttu-id="9bcde-127">HTML-код области и элементов управления</span><span class="sxs-lookup"><span data-stu-id="9bcde-127">HTML regions and controls</span></span>
    
  
- <span data-ttu-id="9bcde-128">Таблицы стилей</span><span class="sxs-lookup"><span data-stu-id="9bcde-128">Style sheets</span></span>
    
  
- <span data-ttu-id="9bcde-129">файлы JavaScript;</span><span class="sxs-lookup"><span data-stu-id="9bcde-129">JavaScript files</span></span>
    
  
- <span data-ttu-id="9bcde-130">Заголовок страницы</span><span class="sxs-lookup"><span data-stu-id="9bcde-130">Page title</span></span>
    
  
<span data-ttu-id="9bcde-p106">HTML-код области и элементы управления являются MDS совместимые, если они помещаются в тегах **SharePoint:AjaxDelta**. Перенос контента в **SharePoint:AjaxDelta** теги, передача сигналов, что модуль MDS следует обновить вложенных элементов и HTML. Если элемент управления или раздел HTML не изменяется со страницы на страницу, он не будут отправляться клиенту. Таким образом необходимо учитывать следующие элементы управления вне **AjaxDelta** тегов. В Seattle.master главной странице показано на рисунке 1 (1) основной области содержимого заключается в теги **AjaxDelta**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p106">HTML regions and controls are MDS compatible if they are wrapped in **SharePoint:AjaxDelta** tags. By wrapping the content in **SharePoint:AjaxDelta** tags, you are signaling that the MDS engine should update the enclosed controls and HTML. If a control or HTML section doesn't change from page to page, it should not be sent to the client. Therefore, you should keep these controls outside of **AjaxDelta** tags. In the Seattle.master master page shown in Figure 1, the (1) main content area is wrapped in **AjaxDelta** tags, as shown here.</span></span>
  
    
    



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

<span data-ttu-id="9bcde-p107">Другой пример шаблона **AjaxDelta**  (2) левой панели навигации на рисунке 1. В следующем коде показано, как элемент управления заключается в **AjaxDelta** тегов, а также множество элементов управления и HTML-код.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p107">Another example of the **AjaxDelta** pattern is the (2) left navigation bar in Figure 1. The following code shows how the control is wrapped in **AjaxDelta** tags along with many other controls and HTML.</span></span>
  
    
    



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

<span data-ttu-id="9bcde-p108">Кое-что необходимо помнить о тегах **AjaxDelta**  это невозможно вложить их. Теги **AjaxDelta** на верхнем уровне необходимые необходимо указать в структуре главной страницы.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p108">One last thing to remember about **AjaxDelta** tags is that you can't nest them. You should specify **AjaxDelta** tags at the highest required level in the master page structure.</span></span>
  
    
    
<span data-ttu-id="9bcde-p109">Последний пример на рисунке 1  Заголовок страницы (3), в котором требуется специальный шаблон, который используется тег **SharePoint:PageTitle**. В следующем коде показан тег **PageTitle** как используется на главной странице Seattle.master.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p109">The last example in Figure 1 is the (3) page title, which requires a special pattern that uses the **SharePoint:PageTitle** tag. The following code shows the **PageTitle** tag as used in the Seattle.master master page.</span></span>
  
    
    



```cs

<SharePoint:PageTitle runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server">
        <SharePoint:ProjectProperty Property="Title" runat="server" />
    </asp:ContentPlaceHolder>
</SharePoint:PageTitle>
```

<span data-ttu-id="9bcde-p110">Главная страница также может включать файлы JavaScript и таблицы стилей. Ядро сервера необходимо определить CSS и JavaScript необходимые файлы. Чтобы определить ресурсы файлы CSS при необходимости, используйте следующий шаблон.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p110">Your master page can also include style sheets and JavaScript files. The server engine needs to identify both CSS and JavaScript files as required. To identify the CSS files resources as required, use the following pattern.</span></span>
  
    
    



```cs

<SharePoint:CssLink runat="server" Version="15"/>
<SharePoint:CssRegistration Name="my_styles.css" runat="server" />
```

<span data-ttu-id="9bcde-p111">Обратите внимание на то, что у вас есть только один тег **CssLink** на главную страницу, но может вызывать много тегов **CssRegistration**, можно добавить множество CSS-файлы. Используйте следующий шаблон для файлов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p111">Note that you can have only one **CssLink** tag per master page, but you can have many **CssRegistration** tags, so you can add many CSS files. Use the following pattern for JavaScript files.</span></span>
  
    
    



```cs

<SharePoint:ScriptLink language="javascript" name="my_javascript.js" runat="server" />
```

<span data-ttu-id="9bcde-147">Включая файлы CSS и JavaScript с помощью **style** и **script** теги HTML в MDS не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="9bcde-147">Including CSS and JavaScript files using HTML **style** and **script** tags is not supported in MDS.</span></span>
  
    
    

## <a name="aspnet-pages"></a><span data-ttu-id="9bcde-148">Страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9bcde-148">ASP.NET pages</span></span>
<span data-ttu-id="9bcde-149"><a name="SP15MDSDev_ASPNET"> </a></span><span class="sxs-lookup"><span data-stu-id="9bcde-149"><a name="SP15MDSDev_ASPNET"> </a></span></span>

<span data-ttu-id="9bcde-p112">Проект содержит ASP.NET страниц, вероятно, требуется ли ссылки на файлы CSS и JavaScript. Теги HTML **style** и **script** не совместимы с MDS. Используйте шаблоны **CssRegistration** и **ScriptLink**, описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p112">If your project includes ASP.NET pages, you probably need to reference CSS and JavaScript files. The HTML **style** and **script** tags are not compatible with MDS. Instead, use the **CssRegistration** and **ScriptLink** patterns explained in the previous section.</span></span>
  
    
    
<span data-ttu-id="9bcde-p113">На страницах ASP.NET могут также использовать метод **Response.Output** для записи содержимого на страницу, которая не допускается в MDS. Вместо этого можно использовать следующие методы спецификации MDS класса [SPHttpUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.aspx) :</span><span class="sxs-lookup"><span data-stu-id="9bcde-p113">Your ASP.NET pages may also use the **Response.Output** method to write content to the page, which is not allowed in MDS. Instead, you can use the following MDS-compliant methods of the [SPHttpUtility](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.aspx) class:</span></span>
  
    
    

-  [<span data-ttu-id="9bcde-155">WriteNoEncode()</span><span class="sxs-lookup"><span data-stu-id="9bcde-155">WriteNoEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteNoEncode.aspx)
    
  
-  [<span data-ttu-id="9bcde-156">WriteHtmlEncode()</span><span class="sxs-lookup"><span data-stu-id="9bcde-156">WriteHtmlEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncode.aspx)
    
  
-  [<span data-ttu-id="9bcde-157">WriteEcmaScriptStringLiteralEncode()</span><span class="sxs-lookup"><span data-stu-id="9bcde-157">WriteEcmaScriptStringLiteralEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteEcmaScriptStringLiteralEncode.aspx)
    
  
-  [<span data-ttu-id="9bcde-158">WriteHtmlEncodeAllowSimpleTextFormatting()</span><span class="sxs-lookup"><span data-stu-id="9bcde-158">WriteHtmlEncodeAllowSimpleTextFormatting()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncodeAllowSimpleTextFormatting.aspx)
    
  
-  [<span data-ttu-id="9bcde-159">WriteHtmlUrlAttributeEncode()</span><span class="sxs-lookup"><span data-stu-id="9bcde-159">WriteHtmlUrlAttributeEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlUrlAttributeEncode.aspx)
    
  
-  [<span data-ttu-id="9bcde-160">WriteUrlKeyValueEncode()</span><span class="sxs-lookup"><span data-stu-id="9bcde-160">WriteUrlKeyValueEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlKeyValueEncode.aspx)
    
  
-  [<span data-ttu-id="9bcde-161">WriteUrlPathEncode()</span><span class="sxs-lookup"><span data-stu-id="9bcde-161">WriteUrlPathEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlPathEncode.aspx)
    
  
<span data-ttu-id="9bcde-p114">Помимо ссылки на файлы JavaScript, ASP.NET страниц может иметь JavaScript встроенного кода. Использовать следующий шаблон, чтобы сделать сценарий блокирует MDS совместимые.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p114">Besides referencing JavaScript files, your ASP.NET pages can have inline JavaScript code. Use the following pattern to make your script blocks MDS compatible.</span></span>
  
    
    



```cs
<SharePoint:ScriptBlock runat="server" >
    // Your JavaScript code here.
</SharePoint:ScriptBlock>
```


## <a name="controls-and-web-parts"></a><span data-ttu-id="9bcde-164">Элементы управления и веб-частей</span><span class="sxs-lookup"><span data-stu-id="9bcde-164">Controls and Web Parts</span></span>
<span data-ttu-id="9bcde-165"><a name="SP15MDSDev_WebParts"> </a></span><span class="sxs-lookup"><span data-stu-id="9bcde-165"><a name="SP15MDSDev_WebParts"> </a></span></span>

<span data-ttu-id="9bcde-p115">Необходимо также отметить веб-частей и элементов управления, как MDS спецификации. В следующем коде показан шаблон для использования.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p115">You also need to mark your controls and Web Parts as MDS compliant. The following code shows the pattern to use.</span></span>
  
    
    

```cs

[assembly: Microsoft.SharePoint.WebControlssCompliantAttribute(IsCompliant = true)]
namespace VisualWebPartProject2.VisualWebPart1
{
    // Rest of your control logic
```

<span data-ttu-id="9bcde-p116">Кроме того элементов управления и веб-частей должны регистрировать свои ресурсы с помощью методов в классе  [SPPageContentManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPPageContentManager.aspx) . Основные ресурсы, JavaScript фрагменты кода и скрытые файлы, которые могут быть зарегистрированы с помощью **RegisterClientScriptBlock** и **RegisterHiddenField**.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p116">Also, your controls and Web Parts need to register their resources using the methods in the  [SPPageContentManager](https://msdn.microsoft.com/library/Microsoft.SharePoint.WebControls.SPPageContentManager.aspx) class. The most common resources are JavaScript snippets and hidden files, which can be registered using the **RegisterClientScriptBlock** and **RegisterHiddenField**, respectively.</span></span>
  
    
    
<span data-ttu-id="9bcde-p117">Веб-частей и элементов управления можно также использовать XSLT-файлов для управления процессом визуализации. XSLT-файлы могут иметь вложенные JavaScript кода или файлов. Модуль MDS необходимо знать об этих ресурсов. Можно регистрировать JavaScript ресурсы, с помощью объекта расширения XSLT с именем **pcm**. Хорошим примером того, как использовать объект **pcm** содержится в файле TEMPLATE\\LAYOUTS\\XSL\\fldtypes.xsl %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\. В следующем коде показано, как файл **fldtypes.xsl** использует объект **pcm** для регистрации JavaScript ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9bcde-p117">Your controls and Web Parts can also use XSLT files to control the rendering process. Your XSLT files can have embedded JavaScript code or files. The MDS engine needs to know about these resources. You can register the JavaScript resources using an XSLT extension object named **pcm**. A great example of how to use the **pcm** object is in the %ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS\\XSL\\fldtypes.xsl file. The following code shows how the **fldtypes.xsl** file uses the **pcm** object to register JavaScript resources.</span></span>
  
    
    



```XML

<xsl:value-of select="pcm:RegisterScriptBlock(concat('block1',$ViewCounter), string($scriptbody1))"/>
<xsl:value-of select="pcm:RegisterScriptLink('/_layouts/15/wssactionmenu.js')"/>
```


## <a name="additional-resources"></a><span data-ttu-id="9bcde-176">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9bcde-176">Additional resources</span></span>
<span data-ttu-id="9bcde-177"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9bcde-177"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="9bcde-178">Общие сведения о минимальной загрузки стратегия</span><span class="sxs-lookup"><span data-stu-id="9bcde-178">Minimal Download Strategy overview</span></span>](minimal-download-strategy-overview.md)
    
  
-  [<span data-ttu-id="9bcde-179">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="9bcde-179">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  

