---
title: "Оптимизация производительности страниц в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 262caeef-64fd-4e02-b947-d772faf01159
ms.openlocfilehash: 6600de1925c934868941c5af3789e680d67c0569
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="optimize-page-performance-in-sharepoint"></a><span data-ttu-id="5ac73-102">Оптимизация производительности страниц в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5ac73-102">Optimize page performance in SharePoint</span></span>
<span data-ttu-id="5ac73-103">Узнайте о возможностях для повышения производительности в страниц в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5ac73-103">Learn about features to improve performance in pages in SharePoint.</span></span> <span data-ttu-id="5ac73-104">Эти компоненты можно использовать для улучшения в географически распределенные реализации.</span><span class="sxs-lookup"><span data-stu-id="5ac73-104">These features can be used to enhance the experience in geographically distributed implementations.</span></span>
 <span data-ttu-id="5ac73-105">**Автор:** Дэвид Кроуфорд, корпорация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="5ac73-105">**Provided by:** David Crawford, Microsoft Corporation</span></span>
  
    
    

<span data-ttu-id="5ac73-106">В этой статье приведены инструкции по оптимизации производительности в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5ac73-106">This article provides instructions that will help optimize performance in SharePoint.</span></span> <span data-ttu-id="5ac73-107">SharePoint включает в себя функции, которые помогут оптимизировать загрузку страниц на региональной сети (сети).</span><span class="sxs-lookup"><span data-stu-id="5ac73-107">SharePoint includes features that help optimize page loading over a Wide Area Network (WAN).</span></span> <span data-ttu-id="5ac73-108">Разработка страниц в них небольшой и быстро как возможные дополняет эти улучшения производительности.</span><span class="sxs-lookup"><span data-stu-id="5ac73-108">Designing pages to make them as small and responsive as possible complements these performance improvements.</span></span>
## <a name="minimal-download-strategy-mds"></a><span data-ttu-id="5ac73-109">Стратегия минимальной загрузки (MDS)</span><span class="sxs-lookup"><span data-stu-id="5ac73-109">Minimal Download Strategy (MDS)</span></span>
<span data-ttu-id="5ac73-110"><a name="MDS"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-110"></span></span>

<span data-ttu-id="5ac73-p103">Стратегия минимальной загрузки (MDS) полагается на возможность загружать только определенные части страницы, отображаемой полностью на сервере. Загрузка только определенных частей предоставляет модель очень эффективным загрузки. Полностью отображаемой страницы не возвращением клиенту. Сервер должен иметь возможность точно определить компоненты, которые должны быть частью ответа и те, которые не нужны. Компоненты, которые могут быть или не быть части ответа включают скрипты, стили и разметки.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p103">Minimal Download Strategy (MDS) relies on the ability to download only specific portions of a page that is rendered fully on the server. Downloading only the specific portions provides a very efficient loading model. The fully rendered page is not returned to the client. The server must be able to accurately identify those pieces that must be part of the response and those that are not necessary. The pieces that may or may be not part of the response include scripts, styles, and markup.</span></span>
  
    
    
<span data-ttu-id="5ac73-116">В следующей таблице перечислены некоторые преимущества использования MDS.</span><span class="sxs-lookup"><span data-stu-id="5ac73-116">The following table shows some benefits of using MDS.</span></span>
  
    
    

<span data-ttu-id="5ac73-117">**В таблице 1. Преимущества использования MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-117">**Table 1. Benefits of using MDS**</span></span>


|<span data-ttu-id="5ac73-118">**Производительность**</span><span class="sxs-lookup"><span data-stu-id="5ac73-118">**Performance**</span></span>|<span data-ttu-id="5ac73-119">**Визуальные элементы**</span><span class="sxs-lookup"><span data-stu-id="5ac73-119">**Visuals**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5ac73-120">Не более чем объемов данных загружены за один запрос страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-120">Fewer amounts of data downloaded per page request.</span></span>  <br/> |<span data-ttu-id="5ac73-121">Браузер не обновления по перезагрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-121">No browser flashing caused by full page reload.</span></span>  <br/> |
|<span data-ttu-id="5ac73-122">Браузер должен обновить только области страницы, изменены с момента последнего запроса.</span><span class="sxs-lookup"><span data-stu-id="5ac73-122">Browser needs to update only the regions of the page that changed since the last request.</span></span>  <br/> |<span data-ttu-id="5ac73-123">Легко определить анимации.</span><span class="sxs-lookup"><span data-stu-id="5ac73-123">Easy to identify animations.</span></span>  <br/> |
|<span data-ttu-id="5ac73-124">Небольшой объем обработки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="5ac73-124">Small amount of processing required on the client.</span></span>  <br/><span data-ttu-id="5ac73-125">**Примечание:** Вдвое клиента 1 время загрузки страницы (PLT1) — из-за chrome каскадных таблиц стилей стилей (CSS) визуализации и JavaScript синтаксического анализа и выполнения.</span><span class="sxs-lookup"><span data-stu-id="5ac73-125">**Note:** Half of client Page-Load-Time 1 (PLT1) is due to chrome cascading style sheet (CSS) rendering and JavaScript parsing and execution.</span></span>           |<span data-ttu-id="5ac73-126">Изменения на странице привлечения внимания пользователя.</span><span class="sxs-lookup"><span data-stu-id="5ac73-126">Changes in the page attract user's attention.</span></span>  <br/> |
   
<span data-ttu-id="5ac73-p104">AJAX и MDS, технологий, запрашивающих только разделы страницы для сведения к минимуму данных Загрузка и повысить скорость отклика страницы. На следующем рисунке показана архитектура MDS.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p104">Both AJAX and MDS are technologies that request only sections of the page to minimize data download and improve page responsiveness. The following figure shows the MDS architecture.</span></span>
  
    
    

<span data-ttu-id="5ac73-129">**На рисунке 1. Архитектура MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-129">**Figure 1. MDS architecture**</span></span>

  
    
    

  
    
    
![Архитектура MDS](../images/OptimizePage_Fig01_MDSArchitecture.png)
  
    
    
<span data-ttu-id="5ac73-p105">Платформа MDS предполагается, что главная страница определяет хром и области содержимого. В MDS, SharePoint переход на страницу означает, что разрешения на запрос только содержимое для этих областей и ресурсы, от которых зависит страницы. Как только файлы для загрузки, что содержимое в браузере, код сценария применяет разметки или ресурсы на страницу соответствующим образом. Браузер работает так, как если бы запрошенную страницу загружен полностью с сервера.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p105">The MDS framework assumes that a master page defines a chrome and content regions. In MDS, SharePoint navigating to a page means requesting just the content for those regions and the resources that the page depends on. Once that content downloads to the browser, script code applies the markup or resources to the page as appropriate. The browser behaves as if the requested page had been loaded completely from the server.</span></span>
  
    
    

<span data-ttu-id="5ac73-135">**На рисунке 2. Хром и регионы на странице SharePoint**</span><span class="sxs-lookup"><span data-stu-id="5ac73-135">**Figure 2. Page chrome and regions in a SharePoint page**</span></span>

  
    
    

  
    
    
![Хром и регионы на странице SharePoint](../images/OptimizePage_Fig02_PageStructure.png)
  
    
    
<span data-ttu-id="5ac73-p106">Когда пользователи просмотра веб-сайта SharePoint в режиме MDS, они не приведет к страницам обратных передач и перезагружает целую страницу. Вместо этого URL-адрес страницы, просматриваемой не изменится и идентификатор фрагмента (знак "#") изменится на содержат страницы, просматриваемой. Имеет формат URL-адрес:  `[Path to site (spweb)] + /_layouts/15/start.aspx# + [path to page] + [query string]`</span><span class="sxs-lookup"><span data-stu-id="5ac73-p106">When users are browsing a SharePoint website in MDS mode, they will not cause full page postbacks and full page reloads. Instead, the URL for the page they are visiting will remain the same, and the fragment identifier (a "#"sign) will change to contain the page they are visiting. The format of the URL is:  `[Path to site (spweb)] + /_layouts/15/start.aspx# + [path to page] + [query string]`</span></span>
  
    
    
<span data-ttu-id="5ac73-140">Ниже приведены некоторые примеры URL-адресов в режиме MDS формате.</span><span class="sxs-lookup"><span data-stu-id="5ac73-140">The following table shows some examples of URLs formatted in MDS mode.</span></span>
  
    
    

<span data-ttu-id="5ac73-141">**В таблице 2. URL-адреса, отформатированные в режиме MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-141">**Table 2. URLs formatted in MDS mode**</span></span>


|<span data-ttu-id="5ac73-142">**URL-адрес не MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-142">**Non-MDS URL**</span></span>|<span data-ttu-id="5ac73-143">**URL-АДРЕС MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-143">**MDS URL**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5ac73-144">http://Server/SitePages/</span><span class="sxs-lookup"><span data-stu-id="5ac73-144">http://server/SitePages/</span></span>  <br/> |<span data-ttu-id="5ac73-145">http://Server/_layouts/15/Start.aspx#/SitePages/</span><span class="sxs-lookup"><span data-stu-id="5ac73-145">http://server/_layouts/15/start.aspx#/SitePages/</span></span>  <br/> |
|<span data-ttu-id="5ac73-146">http://Server/subsite/SitePages/Home.aspx</span><span class="sxs-lookup"><span data-stu-id="5ac73-146">http://server/subsite/SitePages/home.aspx</span></span>  <br/> |<span data-ttu-id="5ac73-147">http://Server/subsite/_layouts/15/Start.aspx#/SitePages/Home.aspx</span><span class="sxs-lookup"><span data-stu-id="5ac73-147">http://server/subsite/_layouts/15/start.aspx#/SitePages/home.aspx</span></span>  <br/> |
|<span data-ttu-id="5ac73-148">http://Server/_layouts/15/viewlsts.aspx?BaseType=0</span><span class="sxs-lookup"><span data-stu-id="5ac73-148">http://server/_layouts/15/viewlsts.aspx?BaseType=0</span></span>  <br/> |<span data-ttu-id="5ac73-149">http://Server/_layouts/15/Start.aspx#/_layouts/viewlsts.aspx?BaseType=0</span><span class="sxs-lookup"><span data-stu-id="5ac73-149">http://server/_layouts/15/start.aspx#/_layouts/viewlsts.aspx?BaseType=0</span></span>  <br/> |
   
<span data-ttu-id="5ac73-p107">Объект, используемый для навигации AJAX  **AjaxNavigate**. По умолчанию остается экземпляр **AjaxNavigate** необходимо использовать именованные **ajaxNavigate**. Чтобы использовать экземпляр **ajaxNavigate**:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p107">The object used for the AJAX navigation is **AjaxNavigate**. By default, there is an instance of **AjaxNavigate** available for you to use named **ajaxNavigate**. To use the **ajaxNavigate** instance:</span></span>
  
    
    



```cs

ajaxNavigate.update(serverRelativeURL, null);
```

<span data-ttu-id="5ac73-153">Если необходимо, элемент управления или веб-части на прослушивание события переходов, можно использовать **Добавьте\_перейдите** обработчика.</span><span class="sxs-lookup"><span data-stu-id="5ac73-153">If you want a control or Web Part to listen to the navigation events, you can use the **add\_navigate** handler.</span></span> <span data-ttu-id="5ac73-154">При вызове обработчика функции обратного вызова получает ссылку на объект навигации и проанализированного хэш-значения в словаре.</span><span class="sxs-lookup"><span data-stu-id="5ac73-154">When the handler is called, your callback function receives a reference to the navigation object and the parsed hash values in a dictionary.</span></span> <span data-ttu-id="5ac73-155">Элемент управления или веб-части можно получить значение параметра интересов из словаря, сравнивать с текущим значением и решить, какое действие необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="5ac73-155">The control or Web Part can retrieve the value for the parameter of interest from the dictionary, compare it to the current value, and decide what action it needs to take.</span></span> <span data-ttu-id="5ac73-156">Общие действия — Отправить запрос AJAX к серверу для получения данных или изменение порядка элементов в представлении.</span><span class="sxs-lookup"><span data-stu-id="5ac73-156">A common action is to send an AJAX request to the server to retrieve some data or reorder the items in the view.</span></span> <span data-ttu-id="5ac73-157">По завершении элемент управления прослушивание события переходов, можно использовать **Удаление\_перейдите** обработчика.</span><span class="sxs-lookup"><span data-stu-id="5ac73-157">When a control has finished listening to navigation events, it can use the **remove\_navigate** handler.</span></span>
  
    
    
<span data-ttu-id="5ac73-p109">MDS также поддерживает несколько хэш-символы в пары "ключ значение". MDS добавляет знак решетки после URL-адрес. Имеет формат метки хэш-функции в URL-адрес: http://server/_layouts/15/start.aspx#/SitePages/page.aspx#key1=value1#key2=value2. В следующем примере кода показано, как обновить метки хэш-функции.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p109">MDS also supports multiple hash marks in key/value pairs. MDS appends the hash marks after the URL. The format of hash marks in the URL is: http://server/_layouts/15/start.aspx#/SitePages/page.aspx#key1=value1#key2=value2. The following code example shows how to update the hash marks.</span></span>
  
    
    



```
var updateParts;
updateParts = {key1: "value1", key2: "value2", keyn: "valuen"}
ajaxNavigate.update(null, updateParts);

```

<span data-ttu-id="5ac73-p110">Если в том, что страницы в веб-сайте постоянно не используют для загрузки полной страницы, можно отключить функцию MDS. Можно также отключить функцию MDS, если необходимо использовать другой метод для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p110">If you find that the pages in your website constantly fall back to download the full page, you might want to consider turning the MDS feature off. You might also want to turn the MDS feature off if you need to use a different strategy to improve performance.</span></span>
  
    
    
<span data-ttu-id="5ac73-p111">Конкретного элемента на странице убедитесь, что критические ресурсы, необходимые для работы известно, что инфраструктура MDS во время отрисовки сервера. Чтобы преобразовать существующий проект для использования MDS, вам потребуется обновить следующие файлы и компоненты:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p111">A particular element in the page must make sure that the critical resources needed to work are known to the MDS infrastructure at server rendering time. To convert an existing project to use MDS, you need to update the following files and components:</span></span>
  
    
    

- <span data-ttu-id="5ac73-166">Эталонные страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-166">Master pages</span></span>
    
  
- <span data-ttu-id="5ac73-167">ASP.NET страниц</span><span class="sxs-lookup"><span data-stu-id="5ac73-167">ASP.NET pages</span></span>
    
  
- <span data-ttu-id="5ac73-168">Настраиваемые главные страницы для ошибки</span><span class="sxs-lookup"><span data-stu-id="5ac73-168">Custom master pages for errors</span></span>
    
  
- <span data-ttu-id="5ac73-169">файлы JavaScript;</span><span class="sxs-lookup"><span data-stu-id="5ac73-169">JavaScript files</span></span>
    
  
- <span data-ttu-id="5ac73-170">Элементы управления и веб-частей</span><span class="sxs-lookup"><span data-stu-id="5ac73-170">Controls and Web Parts</span></span>
    
  

### <a name="master-pages"></a><span data-ttu-id="5ac73-171">Эталонные страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-171">Master pages</span></span>

<span data-ttu-id="5ac73-p112">Основные изменения на главной странице является заключите областей разметки HTML, который будут отправляться клиенту с специальный элемент управления с именем **SharePoint:AjaxDelta**. Наиболее распространенные компоненты, которые должны быть заключены в элемент управления **SharePoint:AjaxDelta** являются элементы управления, встроенные в chrome главной страницы и владельцев контента месте. Если элемент управления не то же самое, на всех страницах веб-узла, его следует оболочку не **SharePoint:AjaxDelta** управления. В следующей разметке показана видимым заполнитель контента, заключенной в элемент управления **SharePoint:AjaxDelta**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p112">The main change in the master page is to surround the regions of HTML markup that will be sent to the client with a special control named **SharePoint:AjaxDelta**. The most common parts that need to be surrounded by a **SharePoint:AjaxDelta** control are the controls embedded in the master page chrome and the content place holders. If a control is the same on all pages within a site, it should not be wrapped by a **SharePoint:AjaxDelta** control. The following markup shows a visible content placeholder surrounded by a **SharePoint:AjaxDelta** control.</span></span>
  
    
    

```HTML

<SharePoint:AjaxDelta id="DeltaPlaceHolderMain" IsMainContent="true" runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderMain" runat="server" />
</SharePoint:AjaxDelta>
```

<span data-ttu-id="5ac73-p113">Элементы управления с содержимым, зависящие от текущего URL-адреса должны быть заключены в элемент управления **SharePoint:AjaxDelta**. В следующей разметке показана меню, заключенной в элемент управления **SharePoint:AjaxDelta**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p113">Controls that have content dependent on the current URL must be wrapped in a **SharePoint:AjaxDelta** control. The following markup shows a menu surrounded by a **SharePoint:AjaxDelta** control.</span></span>
  
    
    



```HTML

<SharePoint:AjaxDelta id="DeltaBreadcrumbDropdown" runat="server">
    <SharePoint:PopoutMenu
        runat="server"
        ID="GlobalBreadCrumbNavPopout"
        IconUrl=IMGCLUSTER_FG_IMG
        IconAlt=LOC_ATTR_WSS(master_breadcrumbIconAlt)
        IconOffsetX=IMGCLUSTER_FG_LEFT(BREADCRUMBBUTTON)
        IconOffsetY=IMGCLUSTER_FG_TOP(BREADCRUMBBUTTON)
        IconWidth=IMGCLUSTER_FG_WIDTH(BREADCRUMBBUTTON)
        IconHeight=IMGCLUSTER_FG_HEIGHT(BREADCRUMBBUTTON)
        AnchorCss="s4-breadcrumb-anchor"
        AnchorOpenCss="s4-breadcrumb-anchor-open"
        MenuCss="s4-breadcrumb-menu">
    </SharePoint:PopoutMenu>
</SharePoint:AjaxDelta>

```


> <span data-ttu-id="5ac73-178">**Примечание:** Элемент управления **SharePoint:AjaxDelta** не должен быть вложенным сам в себя.</span><span class="sxs-lookup"><span data-stu-id="5ac73-178">**Note:** The **SharePoint:AjaxDelta** control should not be nested within itself.</span></span> <span data-ttu-id="5ac73-179">Укажите этот элемент управления на верхнем уровне обязательным.</span><span class="sxs-lookup"><span data-stu-id="5ac73-179">Specify this control at the highest required level.</span></span>
  
    
    

<span data-ttu-id="5ac73-p115">Если необходимо включить файла каскадных таблиц стилей (CSS), необходимо использовать элементы управления **SharePoint:CssLink** и **SharePoint:CssRegistration**. Для работы в режиме MDS и не являющиеся MDS были обновлены следующие элементы управления. Следующая разметка демонстрируется использование элементов управления **SharePoint:CssLink** и **SharePoint:CssRegistration**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p115">If you need to include a cascading style sheet (CSS) file, you need to use the **SharePoint:CssLink** and **SharePoint:CssRegistration** controls. These controls have been updated to work in both MDS and non-MDS mode. The following markup shows how to use the **SharePoint:CssLink** and **SharePoint:CssRegistration** controls.</span></span>
  
    
    



```HTML

<SharePoint:CssLink runat="server" Version="15"/>
<SharePoint:CssRegistration Name="my_stylesheet.css" runat="server" />
```


> <span data-ttu-id="5ac73-183">**Осторожность:** Может иметь только один элемент управления **SharePoint:CssLink** на каждой странице.</span><span class="sxs-lookup"><span data-stu-id="5ac73-183">**Caution:** You can have only one **SharePoint:CssLink** control per page.</span></span> <span data-ttu-id="5ac73-184">В режиме MDS сообщение об ошибке при наличии более одного элемента управления **SharePoint:CssLink** на странице.</span><span class="sxs-lookup"><span data-stu-id="5ac73-184">In MDS mode, you get an error if you have more than one **SharePoint:CssLink** control in a page.</span></span> <span data-ttu-id="5ac73-185">Включая CSS-файла с помощью стиля HTML-элемент не поддерживается в режиме MDS, так как логика сервер не может определить файл как обязательный ресурс при отображении ответа.</span><span class="sxs-lookup"><span data-stu-id="5ac73-185">Including a CSS file using an HTML style element is not supported in MDS mode, because the server logic cannot identify the file as a required resource when the response is rendered.</span></span>
  
    
    

<span data-ttu-id="5ac73-p117">Чтобы включить файл JavaScript, используйте элемент управления **SharePoint:ScriptLink**. Следующая разметка показано, как использовать элемент управления **SharePoint:ScriptLink**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p117">To include a JavaScript file, use the **SharePoint:ScriptLink** control. The following markup shows how to use the **SharePoint:ScriptLink** control.</span></span>
  
    
    



```HTML

<SharePoint:ScriptLink language="javascript" name="my_javascriptfile.js" runat="server" />
```


> <span data-ttu-id="5ac73-188">**Осторожность:** Включая файл JavaScript, с помощью скрипта HTML-тег не поддерживается в режиме MDS, так как логика сервер не может определить файл как обязательный ресурс при отображении ответа.</span><span class="sxs-lookup"><span data-stu-id="5ac73-188">**Caution:** Including a JavaScript file using the HTML script tag is not supported in MDS mode, because the server logic cannot identify the file as a required resource when the response is rendered.</span></span> 
  
    
    

<span data-ttu-id="5ac73-p118">Чтобы отобразить элемент заголовка в элемент head на странице, мы используем специальные шаблон с помощью элемента управления **SharePoint:PageTitle**. Следующая разметка показано, как использовать элемент управления **SharePoint:PageTitle**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p118">To render the title element inside the head element in the page, we use a special pattern using the **SharePoint:PageTitle** control. The following markup shows how to use the **SharePoint:PageTitle** control.</span></span>
  
    
    



```HTML
<SharePoint:PageTitle runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server" />
</SharePoint:PageTitle>

```


> <span data-ttu-id="5ac73-191">**Примечание:** Каждую отдельную страницу необходимо переопределить заголовок с указанием замены для управления **asp: ContentPlaceHolder** внутри элемента управления **SharePoint:PageTitle** .</span><span class="sxs-lookup"><span data-stu-id="5ac73-191">**Note:** Each individual page must override the title by providing a replacement for the **asp:ContentPlaceHolder** control inside the **SharePoint:PageTitle** control.</span></span>
  
    
    


### <a name="aspnet-pages"></a><span data-ttu-id="5ac73-192">ASP.NET страниц</span><span class="sxs-lookup"><span data-stu-id="5ac73-192">ASP.NET pages</span></span>

<span data-ttu-id="5ac73-193">Чтобы включить JavaScript или CSS-файла, используйте же **SharePoint:ScriptLink** и **SharePoint:CssLink** элементы управления описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="5ac73-193">To include a JavaScript or CSS file, use the same **SharePoint:ScriptLink** and **SharePoint:CssLink** controls described in the previous section.</span></span>
  
    
    
<span data-ttu-id="5ac73-p119">В предыдущих версиях SharePoint некоторые страницы запись контента с помощью свойства **Response.Output**. При использовании MDS это больше не допускается. Вам необходимо изменить вызовы **Response.Output** новый интерфейс API. В следующей таблице показаны интерфейсы API, которые часто используются в страницах SharePoint и новые API MDS жалоб.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p119">In previous versions of SharePoint, some pages write content by using the **Response.Output** property. If you are using MDS, this is no longer allowed. You have to change the calls to **Response.Output** to use a new API. The following table shows APIs that are commonly used in SharePoint pages and the new MDS-complaint API.</span></span>
  
    
    

<span data-ttu-id="5ac73-198">**В таблице 3. Часто используемые интерфейсы API и спецификации MDS списков**</span><span class="sxs-lookup"><span data-stu-id="5ac73-198">**Table 3. Commonly used APIs and their MDS-compliant alternatives**</span></span>


|<span data-ttu-id="5ac73-199">**Часто используемые API**</span><span class="sxs-lookup"><span data-stu-id="5ac73-199">**Commonly used API**</span></span>|<span data-ttu-id="5ac73-200">**Альтернатива, совместимая с MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-200">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="5ac73-201">NoEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-201">NoEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.NoEncode.aspx) <br/> | [<span data-ttu-id="5ac73-202">WriteNoEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-202">WriteNoEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteNoEncode.aspx) <br/> |
| [<span data-ttu-id="5ac73-203">HtmlEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-203">HtmlEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.HtmlEncode.aspx) <br/> | [<span data-ttu-id="5ac73-204">WriteHtmlEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-204">WriteHtmlEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncode.aspx) <br/> |
| [<span data-ttu-id="5ac73-205">EcmaScriptStringLiteralEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-205">EcmaScriptStringLiteralEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.EcmaScriptStringLiteralEncode.aspx) <br/> | [<span data-ttu-id="5ac73-206">WriteEcmaScriptStringLiteralEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-206">WriteEcmaScriptStringLiteralEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteEcmaScriptStringLiteralEncode.aspx) <br/> |
| [<span data-ttu-id="5ac73-207">HtmlEncodeAllowSimpleTextFormatting()</span><span class="sxs-lookup"><span data-stu-id="5ac73-207">HtmlEncodeAllowSimpleTextFormatting()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.HtmlEncodeAllowSimpleTextFormatting.aspx) <br/> | [<span data-ttu-id="5ac73-208">WriteHtmlEncodeAllowSimpleTextFormatting()</span><span class="sxs-lookup"><span data-stu-id="5ac73-208">WriteHtmlEncodeAllowSimpleTextFormatting()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncodeAllowSimpleTextFormatting.aspx) <br/> |
| [<span data-ttu-id="5ac73-209">HtmlUrlAttributeEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-209">HtmlUrlAttributeEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.HtmlUrlAttributeEncode.aspx) <br/> | [<span data-ttu-id="5ac73-210">WriteHtmlUrlAttributeEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-210">WriteHtmlUrlAttributeEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlUrlAttributeEncode.aspx) <br/> |
| [<span data-ttu-id="5ac73-211">UrlKeyValueEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-211">UrlKeyValueEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.UrlKeyValueEncode.aspx) <br/> | [<span data-ttu-id="5ac73-212">WriteUrlKeyValueEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-212">WriteUrlKeyValueEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlKeyValueEncode.aspx) <br/> |
| [<span data-ttu-id="5ac73-213">UrlPathEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-213">UrlPathEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.UrlPathEncode.aspx) <br/> | [<span data-ttu-id="5ac73-214">WriteUrlPathEncode()</span><span class="sxs-lookup"><span data-stu-id="5ac73-214">WriteUrlPathEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlPathEncode.aspx) <br/> |
   
<span data-ttu-id="5ac73-p120">Если страница, элемент управления или веб-части направляет его выходные данные в свойстве **Response.Output**, то MDS восстановление после сбоя. При сбое обратно MDS, оно выполняет полного перехода на запрошенную страницу. Можно найти оскорбительного элемента управления с помощью свойства **DeltaPage ._shipRender** при отладке серверного компонента.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p120">If a page, control, or Web Part directs its output to the **Response.Output** property, it causes MDS to fail back. When MDS fails back, it performs a full navigation to the requested page. You can find the offending control by using the **DeltaPage ._shipRender** property while debugging the server component.</span></span>
  
    
    
<span data-ttu-id="5ac73-p121">Необходимо заменить элементы сценария встроенного HTML с элементами управления **SharePoint:ScriptBlock**. Ниже указаны сценария встроенный элемент HTML и элемент управления **SharePoint:ScriptBlock**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p121">You should replace HTML inline script elements with **SharePoint:ScriptBlock** controls. The following table shows an HTML inline script element and a **SharePoint:ScriptBlock** control.</span></span>
  
    
    

<span data-ttu-id="5ac73-220">**В таблице 4. Элемент script встроенного HTML-код и его альтернатива, совместимая с MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-220">**Table 4. HTML inline script element and its MDS-compliant alternative**</span></span>


|<span data-ttu-id="5ac73-221">**Элемент script встроенного HTML**</span><span class="sxs-lookup"><span data-stu-id="5ac73-221">**HTML inline script element**</span></span>|<span data-ttu-id="5ac73-222">**Альтернатива, совместимая с MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-222">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
|`<script type="text/javascript">`<br/>&nbsp;&nbsp;&nbsp;`// Your JavaScript code goes here.`<br/>`</script>`|`<SharePoint:ScriptBlock runat="server">`<br/>&nbsp;&nbsp;&nbsp;`// Your JavaScript code goes here.`<br/>`</SharePoint:ScriptBlock>`|
   
<span data-ttu-id="5ac73-p122">Введение в **SharePoint:ScriptBlock** на странице можно изменить область переменных на странице. В некоторых случаях требуется переместить объявления переменных из `<% %>` `<script runat="server"> <script>`. Чтобы проверить это, загрузите страницу в браузере после выполнения обновления.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p122">The introduction of the **SharePoint:ScriptBlock** in the page can change the scope of variables in page. Sometimes it is necessary to move the declaration of variables from `<% %>` to `<script runat="server"> <script>`. To test this, load the page in the browser after you perform updates.</span></span>
  
    
    

> <span data-ttu-id="5ac73-226">**Примечание:** Инфраструктура MDS не поддерживает VBScript, так как он не может быть зарегистрирована как сценарий в ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5ac73-226">**Note:** The MDS infrastructure does not support VBScript, because it cannot be registered as a script in ASP.NET.</span></span> <span data-ttu-id="5ac73-227">Сценарии должны быть преобразованы в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5ac73-227">Scripts have to be converted to JavaScript.</span></span> 
  
    
    

<span data-ttu-id="5ac73-p124">Гиперссылки на страницах ASP.NET необходимо обновить для использования **SPUpdatePage** типа. В таблице 5 показано гиперссылки на страницах ASP.NET и те же ссылки, обновлены с использованием типа **SPUpdatePage**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p124">HyperLinks in ASP.NET pages must be updated to use **SPUpdatePage** type. Table 5 shows hyperlinks in ASP.NET pages and the same links updated by using **SPUpdatePage** type.</span></span>
  
    
    

<span data-ttu-id="5ac73-230">**В таблице 5. Гиперссылки в ASP.NET и его альтернатива, совместимая с MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-230">**Table 5. Hyperlink in ASP.NET and its MDS-compliant alternative**</span></span>


|<span data-ttu-id="5ac73-231">**Гиперссылки в ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="5ac73-231">**Hyperlink in ASP.NET**</span></span>|<span data-ttu-id="5ac73-232">**Альтернатива, совместимая с MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-232">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
|`<a`<br/>&nbsp;&nbsp;&nbsp;`id=<%_STSWriteHTML("viewlist" + spList.BaseTemplate.ToString());%>`<br/>&nbsp;&nbsp;&nbsp;`href=<%_STSWriteURL(listViewUrl);%>`<br/>`>`|`<a`<br/>&nbsp;&nbsp;&nbsp;`id=<%_STSWriteHTML("viewlist" + spList.BaseTemplate.ToString());%>`<br/>&nbsp;&nbsp;&nbsp;`href=<%_STSWriteURL(listViewUrl);%>`<br/>&nbsp;&nbsp;&nbsp;`onclick="if (typeof(SPUpdatePage) !== 'undefined') return SPUpdatePage(this.href);"`<br/>`>`|
   

### <a name="custom-master-pages-for-errors"></a><span data-ttu-id="5ac73-233">Настраиваемые главные страницы для ошибки</span><span class="sxs-lookup"><span data-stu-id="5ac73-233">Custom master pages for errors</span></span>

<span data-ttu-id="5ac73-p125">Вы можете отобразить сообщения об ошибках в режиме MDS даже в том случае, если вы используете настраиваемой главной страницы ошибок. Чтобы использовать настраиваемую главную страницу ошибок в режиме MDS, необходимо определить **AjaxDelta** на главной странице ошибка, которая имеет свойство **id**, строка **"DeltaPlaceHolderMain"**. Содержимое сообщения об ошибке должно отображаться в **AjaxDelta**. При возвращении на страницу ошибки в браузере с сервера, обозреватель указывает, что основное содержимое для отображения данный и отображает для пользователя.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p125">You can display error messages in MDS mode, even when you are using a custom master page for errors. To use a custom master page for errors in MDS mode, you must define an **AjaxDelta** in the error master page that has the **id** property set to the string **"DeltaPlaceHolderMain"**. The content of the error message must be rendered into the **AjaxDelta**. When the error page is returned to the browser from the server, the browser identifies this as the main content to display and shows it to the user.</span></span>
  
    
    
<span data-ttu-id="5ac73-p126">Несмотря на то, что главная страница для страницы ошибок и Главная страница для **start.aspx** не явные совпадение, браузер можно обнаружить, что произошла ошибка. Браузер позволяет MDS для использования содержимого сообщения ошибки в рамках существующей главной страницы для сохранения согласованную и легко пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p126">Although the master page for the error page and the master page for **start.aspx** are not an explicit match, the browser can detect that an error has occurred. The browser allows MDS to use the relevant error message content within the existing master page in order to maintain a consistent and smooth user experience.</span></span>
  
    
    

### <a name="javascript-files"></a><span data-ttu-id="5ac73-240">файлы JavaScript;</span><span class="sxs-lookup"><span data-stu-id="5ac73-240">JavaScript files</span></span>

<span data-ttu-id="5ac73-p127">файлы JavaScript должна включать только объявления функций. Тем не менее существует множество сценарии прежних версий, которые содержат инициализации глобальных переменных. Для повторной инициализации при отображении новой страницы в режиме MDS необходимости глобальных переменных. **ExecuteAndRegisterBeginEndFunctions** можно использовать для инициализации глобальных переменных. В следующем примере кода показано, как использовать **ExecuteAndRegisterBeginEndFunctions**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p127">JavaScript files should include only function declarations. Nonetheless, there are many legacy scripts that contain global variable initializations. Global variables need to be reinitialized when a new page is rendered in MDS mode. You can use the **ExecuteAndRegisterBeginEndFunctions** to initialize global variables. The following code example shows how to use the **ExecuteAndRegisterBeginEndFunctions**.</span></span>
  
    
    

```

function ExecuteAndRegisterBeginEndFunctions(tag, beginFunc, endFunc, loadFunc)

```

<span data-ttu-id="5ac73-246">**ExecuteAndRegisterBeginEndFunctions** имеет следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="5ac73-246">The **ExecuteAndRegisterBeginEndFunctions** has the following parameters:</span></span>
  
    
    

-  <span data-ttu-id="5ac73-247">_tag_: имя файла, которая регистрирует обратных вызовов; она используется только для целей отладки.</span><span class="sxs-lookup"><span data-stu-id="5ac73-247">_tag_: The name of the file that registers the callbacks; it is used only for debugging purposes.</span></span>
    
  
-  <span data-ttu-id="5ac73-248">_beginFunc_: функция, которая вызывается перед запросить дельты страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-248">_beginFunc_: A function that is called before you request the page delta.</span></span>
    
  
-  <span data-ttu-id="5ac73-249">_endFunc_: функции, который вызывается после получения дельты, но до применения HTML и JavaScript новой страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-249">_endFunc_: A function that is called after you retrieve the delta, but before the HTML and JavaScript for the new page are applied.</span></span>
    
  
-  <span data-ttu-id="5ac73-250">_loadFunc_: функции, который вызывается после HTML и JavaScript для применения новой страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-250">_loadFunc_: A function that is called after the HTML and JavaScript for the new page is applied.</span></span>
    
  

### <a name="controls-and-web-parts"></a><span data-ttu-id="5ac73-251">Элементы управления и веб-частей</span><span class="sxs-lookup"><span data-stu-id="5ac73-251">Controls and Web Parts</span></span>

<span data-ttu-id="5ac73-p128">Чтобы использовать MDS, элементы управления веб-частей и наличие для регистрации ресурсы страниц с помощью объекта **SPPageContentManager**. Наиболее часто зарегистрированных ресурсы, с помощью **SPPageContentManager**, JavaScript фрагменты (функций и переменных JSON) и скрытых полей. В следующей таблице показаны общие шаблоны для вставки скрытых полей и JavaScript фрагменты кода и сделать это с помощью объекта **SPPageContentManager**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p128">To use MDS, controls and Web Parts have to register page resources by using the **SPPageContentManager** object. The most frequently registered resources using **SPPageContentManager** are JavaScript snippets (functions or JSON variables) and hidden fields. The following table shows common patterns for inserting hidden fields and JavaScript snippets, and how to do the same by using the **SPPageContentManager** object.</span></span>
  
    
    

<span data-ttu-id="5ac73-255">**В таблице 6. Общие рекомендации для отображения содержимого и их MDS-совместимые альтернативы**</span><span class="sxs-lookup"><span data-stu-id="5ac73-255">**Table 6. Common practices for rendering content and their MDS-compliant alternatives**</span></span>


|<span data-ttu-id="5ac73-256">**Принято для отображения содержимого**</span><span class="sxs-lookup"><span data-stu-id="5ac73-256">**Common practice for rendering content**</span></span>|<span data-ttu-id="5ac73-257">**Альтернатива, совместимая с MDS**</span><span class="sxs-lookup"><span data-stu-id="5ac73-257">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
|`output.Write("<input type=\\"hidden\\" name=\\"");`<br/>`output.Write(SPHttpUtility.NoEncode("HiddenField));`<br/>`output.Write("\\" value=\\"");`<br/>`output.Write(DigestValue);`<br/>`output.Write("\\" />");`|`SPPageContentManager.RegisterHiddenField(this, "HiddenField", DigestValue);`|
|`Page.ClientScript.RegisterClientScriptBlock(typeof(MyType), "MyKey", "var myvar=1", true);`|`SPPageContentManager.RegisterClientScriptBlock(this, typeof(MyType), "MyKey", "var myvar=1");`|
   

> <span data-ttu-id="5ac73-258">**Примечание:** Функции **RegisterHiddenField** и **RegisterClientScriptBlock** в объекте **SPPageContentManager** привести объект типа **элемента управления** или **страницы** в качестве первого параметра.</span><span class="sxs-lookup"><span data-stu-id="5ac73-258">**Note:** The **RegisterHiddenField** and **RegisterClientScriptBlock** functions in the **SPPageContentManager** object expect an object of type **Control** or **Page** in the first parameter.</span></span>
  
    
    

<span data-ttu-id="5ac73-p129">Модуль MDS использует первого параметра для фильтрации сценарии. Ниже приведены правила для фильтрации при отображении в режиме дельты MDS:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p129">The MDS engine uses the first parameter to filter the scripts. Here are the rules for filtering when a page is rendered in MDS delta mode:</span></span>
  
    
    

- <span data-ttu-id="5ac73-261">Если первый аргумент имеет тип **страницы**, сценарии будет выполняться в браузере.</span><span class="sxs-lookup"><span data-stu-id="5ac73-261">If the first argument is of type **Page**, the scripts will execute in the browser.</span></span>
    
  
- <span data-ttu-id="5ac73-262">Если первый аргумент не типа **страницы** и элемента управления попадает в разделе **SharePoint:AsyncDelta**, сценарии будет выполняться в браузере.</span><span class="sxs-lookup"><span data-stu-id="5ac73-262">If the first argument is not of type **Page** and the control falls under a **SharePoint:AsyncDelta**, the scripts will execute in the browser.</span></span>
    
  
- <span data-ttu-id="5ac73-263">Если первый аргумент веб-части, сценарии будет выполняться в браузере.</span><span class="sxs-lookup"><span data-stu-id="5ac73-263">If the first argument is a Web Part, the scripts will execute in the browser.</span></span>
    
  
<span data-ttu-id="5ac73-264">Многие интерфейсы API в предыдущих версиях SharePoint не предоставил текущего элемента управления в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="5ac73-264">Many APIs in previous versions of SharePoint did not provide the current control as an argument.</span></span> <span data-ttu-id="5ac73-265">Открытую объектную модель в SharePoint был разработан для предоставления в качестве альтернативного метода для регистрации в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="5ac73-265">The public object model in SharePoint was designed to provide an alternate method to register the resources.</span></span> <span data-ttu-id="5ac73-266">Методы, которые не предоставляют текущего элемента управления в качестве аргумента, по-прежнему в интерфейсе API для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="5ac73-266">The methods that do not provide the current control as an argument are still in the API for backward compatibility.</span></span>
  
    
    
<span data-ttu-id="5ac73-p131">Могут переходить между двумя страницами с помощью новой функции с именем **SPUpdatePage**. При отображении элемента управления или веб-части в режиме дельты MDS элементы управления **HyperLink** необходимо добавить обработчик **onclick** и вызова **SPUpdatePage**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p131">You can navigate between two pages by using a new function named **SPUpdatePage**. When a control or Web Part is rendered in MDS delta mode, the **HyperLink** controls must add the **onclick** handler and call **SPUpdatePage**.</span></span>
  
    
    
<span data-ttu-id="5ac73-p132">Необходимо обновить XSLT, используемых веб-частей, так как все ресурсы, добавляемых с помощью объекта **SPPageContentManager** чтобы сделать их MDS спецификации. Можно добавить JavaScript фрагменты кода для преобразования XSLT с помощью методов **RegisterScriptLink** и **RegisterScriptBlock** объекта **SPPageContentManager**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p132">You must update the XSLT used by Web Parts because all the resources must be added by using the **SPPageContentManager** object to make them MDS-compliant. You can add JavaScript snippets to the XSLT by using the **RegisterScriptLink** and **RegisterScriptBlock** methods of the **SPPageContentManager** object.</span></span>
  
    
    

## <a name="optimize-page-downloads"></a><span data-ttu-id="5ac73-271">Оптимизация загрузки страницы</span><span class="sxs-lookup"><span data-stu-id="5ac73-271">Optimize page downloads</span></span>
<span data-ttu-id="5ac73-272"><a name="MDS"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-272"></span></span>

<span data-ttu-id="5ac73-273">После формирования страницы понять, можно использовать различные методы для Оптимизация работы файл для загрузки для этой страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-273">Once you understand the composition of a page, you can use different methods to optimize the download experience for that page.</span></span> <span data-ttu-id="5ac73-274">В общем случае цель — для сведения к минимуму число полных обходов между клиентских и серверных компьютеров и для сокращения объема данных, который переходит по сети.</span><span class="sxs-lookup"><span data-stu-id="5ac73-274">In general, the goal is to minimize the number of round trips between client and server computers and to reduce the amount of data that goes over the network.</span></span> <span data-ttu-id="5ac73-275">В этой статье руководствоваться рекомендации, которые будут применяться в широком на множество различных реализаций SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5ac73-275">The guidance in this article includes recommendations that you can apply broadly to a variety of different implementations of SharePoint.</span></span>
  
    
    
<span data-ttu-id="5ac73-276">В таблице 7 показан пример загрузки времени, которые иллюстрируют различие между первого, во-вторых, и загружает последующие страницы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-276">Table 7 shows example loading times that illustrate the difference between the first, second, and subsequent page loads.</span></span>
  
    
    

<span data-ttu-id="5ac73-277">**В таблице 7. Время загрузки страницы**</span><span class="sxs-lookup"><span data-stu-id="5ac73-277">**Table 7. Page loading times**</span></span>

|||
|:-----|:-----|
|<span data-ttu-id="5ac73-278">Загрузки первой страницы</span><span class="sxs-lookup"><span data-stu-id="5ac73-278">First page load</span></span>  <br/> |<span data-ttu-id="5ac73-279">3-4 секунд</span><span class="sxs-lookup"><span data-stu-id="5ac73-279">3-4 seconds</span></span>  <br/> |
|<span data-ttu-id="5ac73-280">Второй загрузки страницы</span><span class="sxs-lookup"><span data-stu-id="5ac73-280">Second page load</span></span>  <br/> |<span data-ttu-id="5ac73-281">15 сек</span><span class="sxs-lookup"><span data-stu-id="5ac73-281">1.5 seconds</span></span>  <br/> |
|<span data-ttu-id="5ac73-282">Загружает последующие страницы</span><span class="sxs-lookup"><span data-stu-id="5ac73-282">Subsequent page loads</span></span>  <br/> |<span data-ttu-id="5ac73-283">1 с</span><span class="sxs-lookup"><span data-stu-id="5ac73-283">1 second</span></span>  <br/> |
   

> <span data-ttu-id="5ac73-284">**Примечание:** Загрузка времени может отличаться в конкретного сценария.</span><span class="sxs-lookup"><span data-stu-id="5ac73-284">**Note:** Loading times might be different in your particular scenario.</span></span> <span data-ttu-id="5ac73-285">Время загрузки, влияют много переменных, в том числе размер страницы, задержку и нагрузку на сервер.</span><span class="sxs-lookup"><span data-stu-id="5ac73-285">Loading times are affected by many variables, including, but not limited to, page size, latency, and server load.</span></span> 
  
    
    

<span data-ttu-id="5ac73-p135">Методы оптимизации страницы следует разделить на две категории: первый запрос страницы и последующие запросы страницы. Оптимизация для первого запроса страницы (время загрузки страницы 1 или PLT1)  это этих видов оптимизации, которые действуют в первый раз запросе страницы, но это не оказывает на обязательно последующие запросы страницы. Ниже приведены некоторые процессы оптимизации PLT1.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p135">You should categorize page optimization techniques into one of two categories: first page request and subsequent page requests. Optimizations for the first page request (page load time 1 or PLT1) are those kinds of optimizations that are effective the first time the page is requested, but that don't necessarily affect subsequent page requests. The following are some optimizations for PLT1:</span></span>
  
    
    

- <span data-ttu-id="5ac73-289">Оптимизация разметки HTML.</span><span class="sxs-lookup"><span data-stu-id="5ac73-289">Optimize HTML markup.</span></span>
    
  
- <span data-ttu-id="5ac73-p136">Использовать консолидированный изображений и файлов. Например, для объединения нескольких файлов CSS в одну. Объединение изображений в полосу изображения или кластера.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p136">Use consolidated images and files; for example, combine multiple CSS files into one. Combine images into an image strip or cluster.</span></span>
    
  
- <span data-ttu-id="5ac73-p137">Использование методов сжатия (уплотнения). Для получения дополнительных сведений см  [Сжатие (уплотнение) JavaScript и CSS-файлов](optimize-page-performance-in-sharepoint.md#OptimizingPagePerformance_Crunch).</span><span class="sxs-lookup"><span data-stu-id="5ac73-p137">Use compression (crunch) techniques. For more information, see  [Compress (crunch) JavaScript and CSS files](optimize-page-performance-in-sharepoint.md#OptimizingPagePerformance_Crunch).</span></span>
    
  
- <span data-ttu-id="5ac73-294">Убедитесь в том, что вы ссылаетесь рабочей версии общие библиотеки JavaScript, такие как jQuery, а не отладочные версии.</span><span class="sxs-lookup"><span data-stu-id="5ac73-294">Verify that you are referencing the production version of common JavaScript libraries, such as jQuery, instead of the debug versions.</span></span>
    
  
- <span data-ttu-id="5ac73-p138">Подумайте об использовании сети известных доставки содержимого (CDN) например  [Сети доставки содержимого Ajax Microsoft](http://www.asp.net/ajaxlibrary/cdn.ashx). Файлы, требуемые на страницах уже могут кэшироваться браузером клиента.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p138">Consider using a well-known content delivery network (CDN) such as the  [Microsoft Ajax Content Delivery Network](http://www.asp.net/ajaxlibrary/cdn.ashx). The files required in your pages may already be cached by the client browser.</span></span>
    
  
<span data-ttu-id="5ac73-p139">Оптимизация для последующие запросы страницы  это списки, которые могут улучшить взаимодействие с пользователем для загрузки последующие страницы. Ключ  это, необходимо сбалансировать потери в функциональные возможности с достигнуть прибыли. Если рост реализуется только первый раз пользователь нажимает клавишу сайта, оптимизация не стоит потеря функциональности.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p139">Optimizations for subsequent page requests are those that can improve the user experience for a subsequent page load. The key is that you need to balance loss in functionality against the gain achieved. If gain is only realized the first time a user hits a site, the optimization might not be worth the loss in functionality.</span></span>
  
    
    

## <a name="compress-crunch-javascript-and-css-files"></a><span data-ttu-id="5ac73-300">Сжатие (уплотнение) JavaScript и CSS-файлов</span><span class="sxs-lookup"><span data-stu-id="5ac73-300">Compress (crunch) JavaScript and CSS files</span></span>
<span data-ttu-id="5ac73-301"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-301"></span></span>

<span data-ttu-id="5ac73-p140">Файлы, содержащие стили и JavaScript может значительно уменьшается размер путем удаления пробельные символы, наследование стилей и повторное использование кода. Некоторые библиотеки поступают в регулярных (Отладка) и сжатые версии (crunched). Можно найти множество средств для автоматизации файл уплотнение, выполняя поиск в Интернете.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p140">Files that contain JavaScript and styles may be significantly reduced in size by removing whitespaces, style inheritance, and code reuse. Some libraries come in both regular (debug) and compressed (crunched) versions. You can find a variety of tools to automate file crunching by searching the Internet.</span></span>
  
    
    
<span data-ttu-id="5ac73-p141">Убедитесь, что сжатые версии развертываются на рабочем сервере. В этом примере показано, как можно сократить CSS-файла размером до сравнительно легко переопределение.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p141">Verify that the compressed versions are deployed to production servers. This example shows how a CSS file can be reduced in size through some relatively simple rewriting.</span></span>
  
    
    



```
.article-ByLine  {
  font-family: Tahoma,sans-serif; 
  font-size: 9.5pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}
.article-Caption { 
  font-family: Tahoma,sans-serif; 
  font-size: 8pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}
.article-Headline { 
  font-family: Tahoma,sans-serif; 
  font-size: 14pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: bold; 
  color: #000000
}
.article-SubHead  { 
  font-family: Tahoma, sans-serif; 
  font-size: 11pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}
.article-Text {
  font-family: Tahoma, sans-serif; 
  font-size: 10pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}

```

<span data-ttu-id="5ac73-p142">Обычно можно найти способы достижения же стиля и уменьшения размера файлов с эффективно переопределение CSS-файлы. Следующем примере показано, как для оптимизации предыдущий размер CSS путем наследования стилей от родительского элемента.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p142">You can usually find ways to achieve the same styling and reduce the size of your files by efficiently rewriting your CSS files. The following example shows how to optimize the previous CSS size by inheriting the styles from a parent element.</span></span>
  
    
    



```

BODY {font:100% Tahoma,sans-serif}
.art-By {font: 79%}
.art-Cap {font: 67%}
.art-Head {font: bold 117%}
.art-Sub {font: 92%}
.art-Txt {font: 83%}
```

<span data-ttu-id="5ac73-309">Первая версия CSS  783 символов, а вторая  140 символов.</span><span class="sxs-lookup"><span data-stu-id="5ac73-309">The first version of the CSS is 783 characters long, and the second is 140 characters long.</span></span>
  
    
    

## <a name="entity-tags"></a><span data-ttu-id="5ac73-310">Тегов объектов</span><span class="sxs-lookup"><span data-stu-id="5ac73-310">Entity tags</span></span>
<span data-ttu-id="5ac73-311"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-311"></span></span>

<span data-ttu-id="5ac73-p143">Теги сущностей (теги eTag) может привести к клиенту без необходимости перезагрузки файлы. Теги eTag предназначены для уникальной идентификации файлов с помощью номер, который создает сервер. В кластеров серверов каждый сервер создаст другой номер. Например браузер отправляет **Get** метод с **Изменения в том случае, если** поле заголовка для файла, обнаруженных в кэш. Если имеется только один сервер, файл, возможно, будет соответствовать и состояния http **304 Not-Modified** будут отправляться. Однако, если пользователь получает доступ к крупная ферма серверов, оно, вероятно, попадания на другой сервер с тегом другое лицо, вызывающие этот сервер для отправки файла в браузере.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p143">Entity tags (ETags) can cause the client to unnecessarily reload files. ETags are meant to uniquely identify files by using a number that the server generates. In clusters of servers, each server will create a different number. For example, a browser is sending a **Get** method with an **If-Modified** header field for a file that it found in its cache. If there is only one server, the file will probably match, and a **304 Not-Modified** http status will be sent. But, if the user is accessing a large server farm, it will probably hit a different server with a different entity tag, causing that server to send the file to the browser.</span></span>
  
    
    

## <a name="cache-settings"></a><span data-ttu-id="5ac73-318">Параметры кэширования</span><span class="sxs-lookup"><span data-stu-id="5ac73-318">Cache settings</span></span>
<span data-ttu-id="5ac73-319"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-319"></span></span>

<span data-ttu-id="5ac73-p144">Используйте Fiddler или аналогичное средство для проверки, является ли кэш служебные запросы. Наиболее распространенные причины, кэширование не запросы на обслуживание включают:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p144">Use Fiddler or a similar tool to verify whether the cache is serving requests. Some common reasons caching not serving requests include:</span></span>
  
    
    

- <span data-ttu-id="5ac73-322">Ресурсы не имеют значение даты окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="5ac73-322">Resources do not have an expiration date value.</span></span>
    
  
- <span data-ttu-id="5ac73-323">Строка запроса постоянно изменяется.</span><span class="sxs-lookup"><span data-stu-id="5ac73-323">The query string constantly changes.</span></span>
    
  
- <span data-ttu-id="5ac73-324">Суммы заголовка директива, а также **last-modified** управления кэшем **max-age** приводит к до текущей даты.</span><span class="sxs-lookup"><span data-stu-id="5ac73-324">The sum of **max-age** cache-control directive plus **last-modified** header results in a date previous to today.</span></span>
    
  
- <span data-ttu-id="5ac73-325">Прокси-серверы не поддерживают свойства **max-age**.</span><span class="sxs-lookup"><span data-stu-id="5ac73-325">The proxy servers do not support the **max-age** property.</span></span>
    
  
- <span data-ttu-id="5ac73-p145">Заголовок **элемента управления кэша** имеет значение **Нет кэша**. Значение **закрытого** кэширует ресурсов только для пользователя, который отправляет запрос.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p145">The **cache-control** header has a value of **no-cache**. A value of **private** caches the resource only for the user that issues the request.</span></span>
    
  

## <a name="number-and-size-of-images"></a><span data-ttu-id="5ac73-328">Числа и размера изображений</span><span class="sxs-lookup"><span data-stu-id="5ac73-328">Number and size of images</span></span>
<span data-ttu-id="5ac73-329"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-329"></span></span>

<span data-ttu-id="5ac73-p146">Следует свести к минимуму число образов на вашем сайте. Чтобы упростить этот объем работ, можно вставить несколько изображений в одном файле и затем отдельных изображений на странице ссылку. Не только уменьшается размер загружаемого файла, но меньше файлов привести снижение объема сетевого трафика. Это более сложный для разработки страниц с помощью этой технологии, но в ситуациях, где каждый время приема-передачи и размер файла счетчиков, он может оказаться ценных способ повышения производительности. На рисунке 3 показан пример один файл изображения, содержащий несколько изображений.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p146">You should minimize the number of images in your site. To help with that effort, you can embed multiple images in a single file and then reference individual images in your page. Not only will file download size decrease, but fewer files result in less network traffic. It is more complicated to author pages by using this technique, but in situations where every round trip and file size counts, it can prove to be valuable way to help improve performance. Figure 3 shows an example of a single image file that contains multiple images.</span></span>
  
    
    

<span data-ttu-id="5ac73-335">**На рисунке 3. Один файл изображения, содержащий несколько изображений**</span><span class="sxs-lookup"><span data-stu-id="5ac73-335">**Figure 3. Single image file that contains multiple images**</span></span>

  
    
    

  
    
    
![Один файл изображения, содержащий несколько изображений](../images/OptimizePage_Fig03_SingleImage.png)
  
    
    
<span data-ttu-id="5ac73-337">На рисунке 4 показано, как будет изменен файл изображения для отображения как отдельного изображения в таблице.</span><span class="sxs-lookup"><span data-stu-id="5ac73-337">Figure 4 shows how the image file is subsequently changed to display as individual pictures in a table.</span></span>
  
    
    

<span data-ttu-id="5ac73-338">**На рисунке 4. Несколько изображений, показанных в таблице**</span><span class="sxs-lookup"><span data-stu-id="5ac73-338">**Figure 4. Multiple images displayed in a table**</span></span>

  
    
    

  
    
    
![Несколько изображений, показанных в таблице](../images/OptimizePage_Fig04_ImageTable.png)
  
    
    
<span data-ttu-id="5ac73-p147">Манипуляция изображениями полностью выполняется с помощью классов таблиц стилей. В элементах **div** и **img** каждой ячейки таблицы использовались два основных класса. К этим классам относятся:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p147">Manipulation of the images was done entirely through style sheet classes. There were two primary classes used in **div** and **img** elements in each table cell. Those classes are as follows.</span></span>
  
    
    



```

BODY {font:100% Tahoma,sans-serif}
.art-By  {font: 79%}
.art-Cap {font: 67%}
.art-Head {font: bold 117%}
.art-Sub  {font: 92%}
.art-Txt {font: 83%}


.cluster { 
   height:50px; 
   position:relative; 
   width:50px; 
} 
.cluster img { 
   position:absolute; 
}
```

<span data-ttu-id="5ac73-p148">С каждым изображением связан класс, для связи используется идентификатор (ID) изображения. Этот стиль обрезает изображение и определяет смещение от первоначального изображения в кластере. К этим классам относятся:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p148">Each image has a class associated with it based on the identifier (ID) for the image. That style clips the picture and defines an offset from the initial picture in the cluster. Those classes are as follows.</span></span>
  
    
    



```

#person {
   border:none; 
   clip:rect(0, 49, 49, 0); 
} 
#keys { 
   clip:rect(0, 99, 49, 50); 
   left:-50px; 
} 
#people { 
   clip: rect(0, 149, 49, 100); 
   left:-100px; 
} 
#lock { 
   clip:rect(0, 199, 49, 150); 
   left:-150px; 
} 
#phone { 
   clip:rect(0,249, 49, 200); 
   left:-200px; 
}
#question {
    clip: rect(0, 299, 49, 250);
    left: -250px;
}
```


## <a name="list-view-pages"></a><span data-ttu-id="5ac73-346">Страницы представления списка</span><span class="sxs-lookup"><span data-stu-id="5ac73-346">List view pages</span></span>
<span data-ttu-id="5ac73-347"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-347"></span></span>

<span data-ttu-id="5ac73-p149">Корпорация Майкрософт работает для количественной оценки и повышения производительности время отрисовки страницы представления списка. Страницы представления списка  это страницы AllItems.aspx, используемый каждого списков и библиотек для включения просмотра содержимого. Время отображения страницы может зависеть от широко формат столбцов и число столбцов, отображаемые в представлении. Например параметры отображения и включение значки присутствия может сильно повлиять на время отображения. Свернутые группировки заняло значительно больше времени на отображение чем параметр расширенной группировки и оба были более медленными, чем параметр не группирования всех.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p149">Microsoft has worked to quantify and improve the performance of list view page rendering times. A list view page is the AllItems.aspx page that is used by each list and library to enable browsing of content. The rendering time of that page can vary widely based on the number of columns that are visible in the view and the format of the columns. For example, displaying options and enabling presence icons can greatly affect rendering time. The collapsed grouping option took significantly longer to render than the expanded grouping option, and both were slower than no grouping option at all.</span></span>
  
    
    
<span data-ttu-id="5ac73-p150">Такого рода особенности, поэтому важно тщательно проанализируйте, как представления, созданные в страницы представления списка, особенно при медленных сетевых соединений. При работе со списками, содержащих большое количество данных, важно тщательно проектирование всех представлений, особенно в представление по умолчанию. В общем случае можно ускорить время отображения страницы представления списка, используя следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5ac73-p150">These sorts of nuances are why it is important to carefully consider how views are constructed in list view pages, especially over slow network connections. When working with lists that contain a lot of data, it is important to carefully design all views, especially the default view. In general, you can speed up the rendering time of list view pages by using the following recommendations:</span></span>
  
    
    

- <span data-ttu-id="5ac73-356">Отображение только обязательно столбцов.</span><span class="sxs-lookup"><span data-stu-id="5ac73-356">Show only the strictly required columns.</span></span>
    
  
- <span data-ttu-id="5ac73-357">Если это возможно исключение столбцов, содержащих сведения о присутствии.</span><span class="sxs-lookup"><span data-stu-id="5ac73-357">If possible, exclude columns that include presence information.</span></span>
    
  
- <span data-ttu-id="5ac73-358">Используйте ссылки вместо меню "Правка" для просмотра сведений об элементе.</span><span class="sxs-lookup"><span data-stu-id="5ac73-358">Use a link instead of an edit menu to view the item details.</span></span>
    
  
<span data-ttu-id="5ac73-359">В следующей таблице описываются настройки, сокращающие время, необходимое для отображения представления.</span><span class="sxs-lookup"><span data-stu-id="5ac73-359">The following table describes customizations that reduce the time that is required for a view to render.</span></span>
  
    
    

<span data-ttu-id="5ac73-360">**В таблице 8. Настройки, сокращающие время, необходимое для отображения представления**</span><span class="sxs-lookup"><span data-stu-id="5ac73-360">**Table 8. Customizations that reduce the time required for the view to render**</span></span>


|<span data-ttu-id="5ac73-361">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="5ac73-361">**Item**</span></span>|<span data-ttu-id="5ac73-362">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5ac73-362">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5ac73-363">Тип представления</span><span class="sxs-lookup"><span data-stu-id="5ac73-363">View type</span></span>  <br/> |<span data-ttu-id="5ac73-364">Создание представления в виде табличного, а не стандартного представления.</span><span class="sxs-lookup"><span data-stu-id="5ac73-364">Create a view as a datasheet view instead of a standard view.</span></span>  <br/> |
|<span data-ttu-id="5ac73-365">Представление: ограничение числа элементов</span><span class="sxs-lookup"><span data-stu-id="5ac73-365">View: Item limit</span></span>  <br/> |<span data-ttu-id="5ac73-p151">Что-либо более 1000 скорее всего будут отображаться медленно. Через медленное соединение важно проверить, найти правильный баланс между объема данных, отображаемых во время и число полных обходов необходимо отобразить все данные. Увеличение количества строк, в которых отображаются во время, меньшее количество полных обходов, но размер страниц.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p151">Anything over 1,000 will likely render slowly. Over a slow connection, it is important to experiment to find the right balance between the quantity of data shown at a time and the number of round trips necessary to view all the data. The more rows that display at a time, the fewer round trips, but larger pages.</span></span>  <br/> |
|<span data-ttu-id="5ac73-369">Представление: фильтр</span><span class="sxs-lookup"><span data-stu-id="5ac73-369">View: Filter</span></span>  <br/> |<span data-ttu-id="5ac73-p152">Использование **[Today]** и **[Me]** ключевые слова для фильтрации элементов по актуальности или назначения. Использование состояние поля для отображения только активные элементы в используемых по умолчанию для просмотра. </span><span class="sxs-lookup"><span data-stu-id="5ac73-p152">Use **[Today]** and **[Me]** keywords to filter items by freshness or assignment. Use Status fields to show only active items in default views. </span></span><br/> |
|<span data-ttu-id="5ac73-372">Представление: столбцы</span><span class="sxs-lookup"><span data-stu-id="5ac73-372">View: Columns</span></span>  <br/> |<span data-ttu-id="5ac73-p153">Включайте минимальное число столбцов. Создайте представление по умолчанию с небольшим числом столбцов, обеспечивающее возможность высокоуровневого просмотра с возможностью дальнейшей детализации.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p153">Include the smallest number of columns. Create a default view with few columns that allows high-level browsing after which people can drill down.</span></span>  <br/> |
   
<span data-ttu-id="5ac73-p154">В следующей таблице описываются настройки, увеличивающие время, требуемое для отображения представления. Каждый дополнительный столбец немного увеличивает время отображения: до половины секунды на каждый столбец при быстром сетевом соединении и длине списка в 1000 элементов. Некоторые столбцы, как отмечено в таблице, увеличивают время отображения сильнее других.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p154">The following table describes customizations that will increase the time that is required for a view to render. Each additional column increases rendering time by a slight amount: up to a half-second per column over a fast network connection for a list of 1,000 items. Some columns increase rendering time more than others, as noted in the table.</span></span>
  
    
    

<span data-ttu-id="5ac73-378">**В таблице 9. Настройки, увеличивающая время, необходимое для отображения представления**</span><span class="sxs-lookup"><span data-stu-id="5ac73-378">**Table 9. Customizations that increase the time required for the view to render**</span></span>


|<span data-ttu-id="5ac73-379">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="5ac73-379">**Item**</span></span>|<span data-ttu-id="5ac73-380">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5ac73-380">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5ac73-381">Группировать</span><span class="sxs-lookup"><span data-stu-id="5ac73-381">Group By</span></span>  <br/> |<span data-ttu-id="5ac73-p155">Группирование добавляет HTML и JScript, что замедляет отображение больших списков. Сворачивание всех групп по умолчанию еще сильнее увеличивает время отображения из-за дополнительных действий с объектной моделью браузера.</span><span class="sxs-lookup"><span data-stu-id="5ac73-p155">Grouping adds HTML and JScript, which slows down rendering for large lists. Making all groups collapsed by default actually increases rendering time further because of additional operations on the browser object model.</span></span>  <br/> |
|<span data-ttu-id="5ac73-384">Столбец  заголовок с ссылкой на элемент с меню правки</span><span class="sxs-lookup"><span data-stu-id="5ac73-384">Column - title linked to item with edit menu</span></span>  <br/> |<span data-ttu-id="5ac73-385">Вариант "с ссылкой на элемент с меню правки" оказывается самым длинным, аналогичный вариант "с ссылкой на элемент" не приводит к заметному увеличению времени отображения.</span><span class="sxs-lookup"><span data-stu-id="5ac73-385">The option "linked to item with edit menu" takes the longest; the similar option "linked to item" does not increase rendering time noticeably.</span></span>  <br/> |
   

## <a name="developer-dashboard"></a><span data-ttu-id="5ac73-386">Панель мониторинга разработчика</span><span class="sxs-lookup"><span data-stu-id="5ac73-386">Developer Dashboard</span></span>
<span data-ttu-id="5ac73-387"><a name="DeveloperDashboard"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-387"></span></span>

<span data-ttu-id="5ac73-388">Информационная панель разработчика перестроение для SharePoint предоставить дополнительную информацию, включая MDS.</span><span class="sxs-lookup"><span data-stu-id="5ac73-388">The Developer Dashboard is rebuilt for SharePoint to provide more information, including MDS.</span></span> <span data-ttu-id="5ac73-389">Запускается в отдельном окне, чтобы предотвратить снижение визуализации фактические страницы, а также запрос на подробные сведения на каждой странице с представлением диаграммы.</span><span class="sxs-lookup"><span data-stu-id="5ac73-389">It runs in a separate window to avoid affecting rendering of the actual page, and it provides detailed request information per page with a chart view.</span></span> <span data-ttu-id="5ac73-390">Он также включает выделенной вкладки для записи в журнале единой ведения журналов (ULS) определенного запроса.</span><span class="sxs-lookup"><span data-stu-id="5ac73-390">It also includes a dedicated tab for Unified Logging System (ULS) log entries for a particular request.</span></span> <span data-ttu-id="5ac73-391">Дополнительные сведения для анализа запроса.</span><span class="sxs-lookup"><span data-stu-id="5ac73-391">Additional detailed information is included for request analysis.</span></span> <span data-ttu-id="5ac73-392">Он используется выделенного Windows Communication Foundation (WCF) служба (diagnosticsdata.svc) предназначена для предоставления сведений трассировки.</span><span class="sxs-lookup"><span data-stu-id="5ac73-392">It uses a dedicated Windows Communication Foundation (WCF) service (diagnosticsdata.svc) designed to provide tracing information.</span></span>
  
    
    
<span data-ttu-id="5ac73-393">Для получения дополнительных сведений о панели мониторинга разработчика:</span><span class="sxs-lookup"><span data-stu-id="5ac73-393">To learn more about the Developer Dashboard:</span></span>
  
    
    

-  <span data-ttu-id="5ac73-394">[Общие сведения о SharePoint обновленной панели мониторинга разработчиков](http://www.microsoft.com/resources/technet/en-us/office/media/video/videol?cid=stc&amp;amp;from=mscomstc&amp;amp;VideoID=505bdd61-1fcc-4125-97fc-b5f0dda72cbc) (видео).</span><span class="sxs-lookup"><span data-stu-id="5ac73-394">[Overview of the SharePoint renewed developer dashboard](http://www.microsoft.com/resources/technet/en-us/office/media/video/videol?cid=stc&amp;amp;from=mscomstc&amp;amp;VideoID=505bdd61-1fcc-4125-97fc-b5f0dda72cbc) (video).</span></span>
    
  
-  <span data-ttu-id="5ac73-395">[Обновленной панели мониторинга разработчиков](http://download.microsoft.com/download/7/7/3/773CA2C2-579B-408C-808E-A6F561194E20/Ig15_SP_IT_M10V3_devdash.pptx) (Панель слайдов PowerPoint).</span><span class="sxs-lookup"><span data-stu-id="5ac73-395">[Renewed Developer Dashboard](http://download.microsoft.com/download/7/7/3/773CA2C2-579B-408C-808E-A6F561194E20/Ig15_SP_IT_M10V3_devdash.pptx) (PowerPoint slide deck).</span></span>
    
  
<span data-ttu-id="5ac73-396">Чтобы включить панель разработчика, используйте следующий фрагмент кода Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5ac73-396">To enable the Developer Dashboard, use the following Windows PowerShell snippet code.</span></span>
  
    
    



```

$content = ([Microsoft.SharePoint.Administration.SPWebService]::ContentService)
$appsetting =$content.DeveloperDashboardSettings
$appsetting.DisplayLevel = [Microsoft.SharePoint.Administration.SPDeveloperDashboardLevel]::On
$appsetting.Update() 

```

<span data-ttu-id="5ac73-397">На рисунке 5 показана панель мониторинга разработчиков.</span><span class="sxs-lookup"><span data-stu-id="5ac73-397">Figure 5 shows the Developer Dashboard.</span></span>
  
    
    

<span data-ttu-id="5ac73-398">**На рисунке 5. Информационная панель разработчика**</span><span class="sxs-lookup"><span data-stu-id="5ac73-398">**Figure 5. Developer Dashboard**</span></span>

  
    
    

  
    
    
![Панель разработчика](../images/OptimizePage_Fig05_DevDashboard.png)
  
    
    
<span data-ttu-id="5ac73-400">Важно понимать, как эти запросы и число изображений и запросы влияют на производительность.</span><span class="sxs-lookup"><span data-stu-id="5ac73-400">It is important to understand how these requests and the number of images and queries affect performance.</span></span> <span data-ttu-id="5ac73-401">Существуют сходства, когда речь идет о представлений отрисовки списка на сервере (XSL или CAML), как они следовать рекомендациям же размер как представления списков отображаемой со стороны клиента.</span><span class="sxs-lookup"><span data-stu-id="5ac73-401">There are similarities when it comes to server-side rendered list views (XSL or CAML) as they follow the same size recommendations as client-side rendered list views.</span></span> <span data-ttu-id="5ac73-402">Тем не менее представление списка серверов, руководство заключается в создании только представлений списка необходимый для выполнения требований, когда ваша цель — оптимальной производительности, как тысячи представлений будет привести к снижению больше производительности из-за управление кэшем компиляции.</span><span class="sxs-lookup"><span data-stu-id="5ac73-402">However, server list view guidance is to create only list views necessary to accomplish your requirements when your goal is optimal performance, as thousands of views will cause greater degradation in performance due to compilation cache management.</span></span> <span data-ttu-id="5ac73-403">Характеристики физического компьютера, например, скорость процессора и памяти, будет выделения в общей скорости.</span><span class="sxs-lookup"><span data-stu-id="5ac73-403">The physical characteristics of the computer, such as memory and processor speed, will factor into the overall speed.</span></span> <span data-ttu-id="5ac73-404">Имеется также возмещение маршрутов запросов или их распределения.</span><span class="sxs-lookup"><span data-stu-id="5ac73-404">There is also consideration for where the requests route or how they are distributed.</span></span> <span data-ttu-id="5ac73-405">Чтобы лучше понять, как SharePoint маршрутизирует и распространять запросы, можно использовать средство диспетчера запросов.</span><span class="sxs-lookup"><span data-stu-id="5ac73-405">To better understand how SharePoint routes and distributes requests, you can use the Request Manager tool.</span></span> <span data-ttu-id="5ac73-406">Тем не менее посвященные запрашивающие рассылки выходит за рамки данной статьи.</span><span class="sxs-lookup"><span data-stu-id="5ac73-406">However, discussing request distribution is beyond the scope of this article.</span></span> <span data-ttu-id="5ac73-407">Дополнительные сведения можно [Настроить диспетчер запросов в SharePoint](http://technet.microsoft.com/library/jj712708.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ac73-407">For more information, see  [Configure Request Manager in SharePoint](http://technet.microsoft.com/library/jj712708.aspx).</span></span>
  
    
    

## <a name="conclusion"></a><span data-ttu-id="5ac73-408">Заключение</span><span class="sxs-lookup"><span data-stu-id="5ac73-408">Conclusion</span></span>
<span data-ttu-id="5ac73-409"><a name="bk_conclusion"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-409"></span></span>

<span data-ttu-id="5ac73-410">Большая часть рекомендации по оптимизации производительности страниц SharePoint 2010 относится к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5ac73-410">Much of the guidance for SharePoint 2010 page performance optimization applies to SharePoint.</span></span> <span data-ttu-id="5ac73-411">В этой статье приводятся некоторые элементы руководство по SharePoint 2010 при Освоение новой области, которые специально бы преимущества в отношении производительности.</span><span class="sxs-lookup"><span data-stu-id="5ac73-411">This article provides some of the elements of guidance for SharePoint 2010 while diving into new areas that would specifically benefit performance.</span></span> <span data-ttu-id="5ac73-412">Мы рассматриваются некоторые очевидны изменения и улучшения, например, MDS и улучшенные информационная панель разработчика.</span><span class="sxs-lookup"><span data-stu-id="5ac73-412">We covered some obvious changes or enhancements, for example, MDS and the enhanced Developer Dashboard.</span></span> <span data-ttu-id="5ac73-413">Мы оболочку с классической руководство: уплотнения вниз JavaScript и каскадные таблицы стилей, используйте CDN для общие библиотеки JavaScript, если это возможно для кэширования, объединять и сжатия изображений по возможности, ограничить или удалить ненужные данные из представления и построение внимательно представления списка.</span><span class="sxs-lookup"><span data-stu-id="5ac73-413">We wrapped up with the classic guidance: crunch down JavaScript and cascading style sheets, use a CDN for common JavaScript libraries if possible for caching, combine and compress images as much as possible, limit or remove unnecessary data from view, and construct list views judiciously.</span></span> <span data-ttu-id="5ac73-414">Методики и компоненты, обсуждаемые в этой статье "участие" для поддержки целей производительности.</span><span class="sxs-lookup"><span data-stu-id="5ac73-414">The techniques and features discussed in this article contribute to supporting your performance goals.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="5ac73-415">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ac73-415">Additional resources</span></span>
<span data-ttu-id="5ac73-416"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="5ac73-416"></span></span>


-  [<span data-ttu-id="5ac73-417">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="5ac73-417">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="5ac73-418">Дизайнер SharePoint изображений</span><span class="sxs-lookup"><span data-stu-id="5ac73-418">SharePoint Design Manager image renditions</span></span>](sharepoint-design-manager-image-renditions.md)
    
  
-  [<span data-ttu-id="5ac73-419">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5ac73-419">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="5ac73-420">Обзор модели страниц в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5ac73-420">Overview of the SharePoint page model</span></span>](overview-of-the-sharepoint-page-model.md)
    
  
