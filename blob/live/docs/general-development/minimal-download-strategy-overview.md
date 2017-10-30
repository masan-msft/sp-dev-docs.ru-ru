---
title: "Общие сведения о минимальной загрузки стратегия"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 9aafff627fcc47dbb8bbd4402585669dd6ef5bae
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="minimal-download-strategy-overview"></a><span data-ttu-id="ace6b-102">Общие сведения о минимальной загрузки стратегия</span><span class="sxs-lookup"><span data-stu-id="ace6b-102">Minimal Download Strategy overview</span></span>
<span data-ttu-id="ace6b-103">Сведения о минимальной загрузки стратегии (MDS), это новая возможность в SharePoint, который сокращает время загрузки страницы при помощи только различия при переходе на новую страницу.</span><span class="sxs-lookup"><span data-stu-id="ace6b-103">Learn about Minimal Download Strategy (MDS), a new feature in SharePoint that reduces page load time by sending only the differences when users navigate to a new page.</span></span>
<span data-ttu-id="ace6b-104">Стратегия минимальной загрузки (MDS) — это новая технология в SharePoint, которое позволяет сократить объем данных, браузер для загрузки при переходе с одной страницы на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ace6b-104">Minimal Download Strategy (MDS) is a new technology in SharePoint that reduces the amount of data that the browser has to download when users navigate from one page to another in a SharePoint site.</span></span> <span data-ttu-id="ace6b-105">Когда пользователи просматривают сайте с поддержкой MDS, клиент обрабатывает только различия (или разностного) между текущей страницы и запрошенную страницу.</span><span class="sxs-lookup"><span data-stu-id="ace6b-105">When users browse an MDS-enabled site, the client processes only the differences (or delta) between the current page and the requested page.</span></span> <span data-ttu-id="ace6b-106">На рисунке 1 показано, что разделы, которые изменяют между страницами и, следовательно, требуют обновления.</span><span class="sxs-lookup"><span data-stu-id="ace6b-106">Figure 1 shows the sections that change from page to page and therefore require an update.</span></span> <span data-ttu-id="ace6b-107">Дельты обычно включает в себя данные в области (1) контента, а также другие компоненты, такие как элементы управления навигацией (2).</span><span class="sxs-lookup"><span data-stu-id="ace6b-107">The delta usually includes the data in the (1) content areas, as well as other components such as (2) navigation controls.</span></span>
  
    
    


<span data-ttu-id="ace6b-108">**На рисунке 1. Страница, Обработанная MDS**</span><span class="sxs-lookup"><span data-stu-id="ace6b-108">**Figure 1. Page processed with MDS**</span></span>

  
    
    

  
    
    
![Страница, обработанная MDS](../images/MDS_UpdateSections.png)
  
    
    
<span data-ttu-id="ace6b-110">Можно определить сайтом с MDS включен, посмотрев URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="ace6b-110">You can identify a site that has MDS enabled by looking at the URL.</span></span> <span data-ttu-id="ace6b-111">Сайте с поддержкой MDS имеет страницы (3) **_layouts/15/start.aspx** в URL-адрес, а затем знак решетки ( **#** ) и относительный URL-адрес запрошенного ресурса, как показано на рисунке 1.</span><span class="sxs-lookup"><span data-stu-id="ace6b-111">An MDS-enabled site has the (3) **_layouts/15/start.aspx** page in the URL followed by a hash mark ( **#** ) and the relative URL of the requested resource, as shown in Figure 1.</span></span> <span data-ttu-id="ace6b-112">Например, вот MDS отформатированный URL-адрес страницы **newpage.aspx**: **https://sp_site/_layouts/15/start.aspx#/SitePages/newpage.aspx**эквивалентен по следующему URL-формате не MDS: **https://sp_site/SitePages /newpage.aspx**как разработчик, созданные компоненты SharePoint, которые требуются некоторые обновления, прежде чем можно эффективно работать в соответствии с MDS.</span><span class="sxs-lookup"><span data-stu-id="ace6b-112">For example, the following is the MDS-formatted URL for the page **newpage.aspx**: **https://sp_site/_layouts/15/start.aspx#/SitePages/newpage.aspx**It is equivalent to the following non-MDS-formatted URL: **https://sp_site/SitePages/newpage.aspx**As a developer, you might have created SharePoint components that need some updates before they can work seamlessly with MDS.</span></span> 
## <a name="enable-mds"></a><span data-ttu-id="ace6b-113">Включение MDS</span><span class="sxs-lookup"><span data-stu-id="ace6b-113">Enable MDS</span></span>
<span data-ttu-id="ace6b-114"><a name="SP15MDSOverview_Enable"> </a></span><span class="sxs-lookup"><span data-stu-id="ace6b-114"><a name="SP15MDSOverview_Enable"> </a></span></span>

<span data-ttu-id="ace6b-115">С помощью страницы администрирования сайта или SharePoint клиентских объектных моделей, можно включить MDS на вашем сайте.</span><span class="sxs-lookup"><span data-stu-id="ace6b-115">You can enable MDS in your site by using either the site administration pages or the SharePoint client object models.</span></span>
  
    
    
<span data-ttu-id="ace6b-116">Чтобы включить MDS по активации компонента на страницах администрирования, выберите пункт **Параметры сайта** > **Управление возможностями сайта** и активация компонента **Стратегия минимальной загрузки**.</span><span class="sxs-lookup"><span data-stu-id="ace6b-116">To enable MDS by activating the feature in the administration pages, choose **Site settings** > **Manage site features**, and activate the **Minimal Download Strategy** feature.</span></span>
  
    
    
<span data-ttu-id="ace6b-p103">Так как он активируется путем изменения свойства  [EnableMinimalDownload](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Web.EnableMinimalDownload.aspx) , можно также использовать клиентские API-интерфейсы. Приведенный ниже код показано, как включить MDS с помощью объектной модели JavaScript (JSOM).</span><span class="sxs-lookup"><span data-stu-id="ace6b-p103">Because the feature is activated by modifying the  [EnableMinimalDownload](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Web.EnableMinimalDownload.aspx) property, you can also use the client APIs. The following code shows how to enable MDS using the JavaScript object model (JSOM).</span></span>
  
    
    



```

var clientContext;

clientContext = new SP.ClientContext.get_current();
this.oWebsite = clientContext.get_web();

this.oWebsite.set_enableMinimalDownload(true);
this.oWebsite.update();

clientContext.load(this.oWebsite);

clientContext.executeQueryAsync(
    Function.createDelegate(this, successHandler),
    Function.createDelegate(this, errorHandler)
);

function successHandler() {
    alert("MDS is enabled in this site.");
}

function errorHandler() {
    alert("Request failed: " + arguments[1].get_message());
}
```


## <a name="benefits-of-using-mds"></a><span data-ttu-id="ace6b-119">Преимущества использования MDS</span><span class="sxs-lookup"><span data-stu-id="ace6b-119">Benefits of using MDS</span></span>
<span data-ttu-id="ace6b-120"><a name="SP15MDSOverview_Benefits"> </a></span><span class="sxs-lookup"><span data-stu-id="ace6b-120"><a name="SP15MDSOverview_Benefits"> </a></span></span>

<span data-ttu-id="ace6b-121">С помощью MDS предоставляет несколько преимуществ, включая:</span><span class="sxs-lookup"><span data-stu-id="ace6b-121">Using MDS provides several benefits, including:</span></span>
  
    
    

- <span data-ttu-id="ace6b-p104">**Скорость:** Это основной целью MDS. При использовании MDS, браузер не нужно повторно обработать chrome пользовательского интерфейса (UI). MDS сокращаются полезных данных, по сравнению с полной загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p104">**Speed:** This is the main objective of MDS. When you are using MDS, the browser doesn't have to reprocess the chrome user interface (UI). MDS also reduces the payload compared to a full page load.</span></span>
    
  
- <span data-ttu-id="ace6b-p105">**Плавного перехода:** Путем обновления только области, которые изменяют рисовании глаз пользователя к эти области, в отличие от загрузки полной страницы, где всей страницы "мигает." При обновлении всей страницы пользователь должен его обработки полностью определять новые. У пользователей есть легче навигации сайта, который обновляет только области, которые изменено на предыдущей странице.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p105">**Smooth transitions:** By updating only the areas that change, you draw the user's eye toward these areas, as opposed to a full page load where the whole page "flashes." When the whole page is updated, the user must parse it in its entirety to detect what is new. Users have an easier time navigating a site that only updates the areas that changed from the previous page.</span></span>
    
  
- <span data-ttu-id="ace6b-p106">**Элементы управления навигацией браузер:** Другие системы на основе AJAX следует путать кнопки **предыдущей** и **Далее** в браузерах. Поскольку MDS обновляет URL-адрес в окне браузера, кнопки предыдущей и следующей работают так же, как они должны.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p106">**Browser navigation controls:** Other AJAX-based systems confuse the **previous** and **next** buttons in browsers. Because MDS updates the URL in the browser window, the previous and next buttons work just as they are supposed to.</span></span>
    
  
- <span data-ttu-id="ace6b-p107">**Обратной совместимости:** Модуль MDS предоставляет навигации MDS сразу же или определяет, когда нельзя. В случае, где невозможно MDS навигации возникает вместо полной загрузки страницы. Этот процесс называется **отработки отказа** и гарантирует, что все страницы обработку должным образом, независимо от того, является ли они содержат MDS-совместимых компонентов. MDS также работает хорошо в средствах поиска из-за атрибута **href** теги привязки использует регулярные, не являющиеся формате MDS URL-адреса. Вместо этого ядро MDS в клиенте захватывает событие **onclick** и использует для связи с сервером.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p107">**Backward compatibility:** The MDS engine either provides MDS navigation immediately or detects when it isn't possible. In the case where MDS navigation isn't possible, a full page load occurs instead. This process is called **failover**, and it ensures that all pages render properly regardless of whether they contain MDS-compliant components. MDS also works nicely with search engines because the **href** attribute of anchor tags uses the regular, non MDS-formatted URLs. Instead, the MDS engine in the client captures the **onclick** event and uses it to communicate with the server.</span></span>
    
  

## <a name="mds-architecture"></a><span data-ttu-id="ace6b-135">Архитектура MDS</span><span class="sxs-lookup"><span data-stu-id="ace6b-135">MDS architecture</span></span>
<span data-ttu-id="ace6b-136"><a name="SP15MDSOverview_Architecture"> </a></span><span class="sxs-lookup"><span data-stu-id="ace6b-136"><a name="SP15MDSOverview_Architecture"> </a></span></span>

<span data-ttu-id="ace6b-p108">Основной механизм MDS являются очень просто. Основные компоненты MDS, два ядра, один на сервере, а другой в клиенте, которые работают вместе для расчета изменения и отображения страниц в браузере, при переходе пользователя со страницы на страницу на сайте. На рисунке 2 показано поток MDS, когда пользователь переходит к узлу поддержкой MDS.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p108">The basic mechanics of MDS are pretty simple. The main components of MDS are two engines, one in the server and another in the client, that work together to calculate the changes and render the pages in the browser when the user navigates from page to page in the site. Figure 2 shows the MDS flow when a user navigates through an MDS-enabled site.</span></span>
  
    
    

<span data-ttu-id="ace6b-140">**На рисунке 2. Поток MDS ВО время перехода пользователя сайта**</span><span class="sxs-lookup"><span data-stu-id="ace6b-140">**Figure 2. MDS flow when a user navigates the site**</span></span>

  
    
    

  
    
    
![Поток MDS во время перехода пользователя на веб-сайт](../images/MDS_GeneralFlow.png)
  
    
    

  
    
    

1. <span data-ttu-id="ace6b-142">Браузер запрашивает изменения между текущей страницы и его на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ace6b-142">The browser requests the changes between the current page and a new one in the SharePoint site.</span></span>
    
  
2. <span data-ttu-id="ace6b-143">Ядро MDS на сервере вычисляет интервал между текущей и новые страницы.</span><span class="sxs-lookup"><span data-stu-id="ace6b-143">The MDS engine in the server calculates the delta between the current and the new pages.</span></span>
    
  
3. <span data-ttu-id="ace6b-144">Модуль MDS на сервере отправляет дельты к ядру MDS в клиенте.</span><span class="sxs-lookup"><span data-stu-id="ace6b-144">The MDS engine in the server sends the delta to the MDS engine in the client.</span></span>
    
  
4. <span data-ttu-id="ace6b-145">Модуль MDS в клиенте заменяет измененных областей на текущей странице новое содержимое страницы.</span><span class="sxs-lookup"><span data-stu-id="ace6b-145">The MDS engine in the client replaces the changed areas on the current page with the new page content.</span></span>
    
  
<span data-ttu-id="ace6b-146">Страница с результатами  именно так, как было бы при страницы загружено без MDS.</span><span class="sxs-lookup"><span data-stu-id="ace6b-146">The resulting page is exactly as it would have been if the page had been downloaded without MDS.</span></span>
  
    
    
<span data-ttu-id="ace6b-p109">Модуль MDS в клиенте включает в себя диспетчер загрузки. Все запросы на странице направляются через диспетчер загрузки. Все элементы управления на странице необходимо подписаться на диспетчер загрузки, чтобы узнать, когда URL-адрес был изменен. Диспетчер загрузки выполняет один запрос для всех новых данных элемента управления. Должны иметь возможность работы в средствах поиска, модуль MDS не использует непосредственно атрибута **href** теги привязки для хранения MDS формат URL-адреса. Вместо этого функция **SPUpdatePage** обрабатывает событие **onclick** и использует его для связи с сервером. Функция **SPUpdatePage** объявляются в файле **_layouts/15/start.js**.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p109">The MDS engine in the client includes a download manager. All requests in the page are routed through the download manager. All controls in the page must subscribe to the download manager to learn when a URL has changed. The download manager makes one request for all the new control data. To be able to work with search engines, the MDS engine doesn't directly use the **href** attribute of anchor tags to store MDS-formatted URLs. Instead, the **SPUpdatePage** function handles the **onclick** event and uses it to communicate with the server. The **SPUpdatePage** function is declared in the **_layouts/15/start.js** file.</span></span>
  
    
    
<span data-ttu-id="ace6b-p110">Модуль MDS на сервере отправляет данные обратно клиенту. Эта информация может содержать HTML-код с внедренным скрипты и стили, XML или Нотация объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="ace6b-p110">The MDS engine in the server sends the information back to the client. This information can contain HTML with embedded scripts and styles, XML, or JavaScript Object Notation (JSON).</span></span>
  
    
    
<span data-ttu-id="ace6b-p111">URL-адрес играет важную роль в MDS. URL-адрес MDS выглядит следующим образом: **https://sp_site/_layouts/15/start.aspx#/SitePages/newpage.aspx**. **Start.aspx** содержит минимальной общего пользовательского интерфейса и инструкции по загрузке изменения страницы. MDS учитывает также часть адреса после знак решетки (#) как конечной страницы. Конечной страницы начинается с косой черты (/) следуют URL-адрес относительно SharePoint веб-сайта. Когда браузер получает URL-адрес, он видит, что не изменилось части слева от знака, поэтому он вызывает событие локальной навигации. Модуль MDS в клиенте захватывает событие локальной навигации и использует его для обновления MDS.</span><span class="sxs-lookup"><span data-stu-id="ace6b-p111">The URL plays an important role in MDS. An MDS URL looks like the following: **https://sp_site/_layouts/15/start.aspx#/SitePages/newpage.aspx**. **Start.aspx** contains minimal shared UI and instructions for loading page changes. MDS considers the part following the hash mark (#) as the target page. The target page starts with a slash (/) followed by a URL relative to the SharePoint website. When the browser receives the URL, it sees that the part to the left of the hash mark hasn't changed, so it fires a local navigation event. The MDS engine in the client captures the local navigation event and uses it to perform an MDS update.</span></span>
  
    
    
<span data-ttu-id="ace6b-p112">Как упоминалось ранее в этой статье, в некоторых случаях не можно определить, можно ли страницы обновления должным образом. В этих случаях модуль MDS вопросы **перехода на другой ресурс**, состоящий из дополнительных кругового пути для перенаправления браузера с полной версией новой страницы. Далее представлены наиболее распространенные причины, почему переход на другой ресурс:</span><span class="sxs-lookup"><span data-stu-id="ace6b-p112">As mentioned previously in this article, in some situations it's not possible to determine whether the page can be updated properly. In these situations, the MDS engine issues a **failover**, which consists of an extra round trip to redirect the browser to the full version of the new page. These are the most common reasons why failover occurs:</span></span>
  
    
    

- <span data-ttu-id="ace6b-166">На новой странице есть другой главной страницы.</span><span class="sxs-lookup"><span data-stu-id="ace6b-166">The new page has a different master page.</span></span>
    
  
- <span data-ttu-id="ace6b-167">Текущей главной страницы, была изменена.</span><span class="sxs-lookup"><span data-stu-id="ace6b-167">The current master page has changed.</span></span>
    
  
- <span data-ttu-id="ace6b-168">Модуль MDS обнаруживает несовместимым HTML, например:</span><span class="sxs-lookup"><span data-stu-id="ace6b-168">The MDS engine detects non-compliant HTML, for example:</span></span>
    
  - <span data-ttu-id="ace6b-169">Страниц с помощью ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="ace6b-169">Pages using ASP.NET 2.0</span></span>
    
  
  - <span data-ttu-id="ace6b-170">CSS или сценарии не зарегистрировано в модуль MDS</span><span class="sxs-lookup"><span data-stu-id="ace6b-170">CSS or scripts not registered in the MDS engine</span></span>
    
  
  - <span data-ttu-id="ace6b-171">Недопустимый HTML</span><span class="sxs-lookup"><span data-stu-id="ace6b-171">Illegal HTML</span></span>
    
  
- <span data-ttu-id="ace6b-172">Существует несовместимым элементов управления на странице, например:</span><span class="sxs-lookup"><span data-stu-id="ace6b-172">There are non-compliant controls on the page, for example:</span></span>
    
  - <span data-ttu-id="ace6b-173">Элемент управления не белом MDS модуля.</span><span class="sxs-lookup"><span data-stu-id="ace6b-173">The control is not in the MDS engine whitelist.</span></span>
    
  
  - <span data-ttu-id="ace6b-174">Элемент управления сборка не помечена как соответствующая требованиям.</span><span class="sxs-lookup"><span data-stu-id="ace6b-174">The control assembly is not marked as compliant.</span></span>
    
  
  - <span data-ttu-id="ace6b-175">Класс элемента управления не имеет атрибут MDS.</span><span class="sxs-lookup"><span data-stu-id="ace6b-175">The control class doesn't have the MDS attribute.</span></span>
    
  
<span data-ttu-id="ace6b-176">Средство MDS пытается восстановиться обработки отказа после перехода на новую страницу еще одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="ace6b-176">The MDS engine tries to recover from a failover after the user navigates to yet another new page.</span></span>
  
    
    

## <a name="developer-controls"></a><span data-ttu-id="ace6b-177">Элементы управления для разработчиков</span><span class="sxs-lookup"><span data-stu-id="ace6b-177">Developer controls</span></span>
<span data-ttu-id="ace6b-178"><a name="SP15MDSOverview_DevControls"> </a></span><span class="sxs-lookup"><span data-stu-id="ace6b-178"><a name="SP15MDSOverview_DevControls"> </a></span></span>

<span data-ttu-id="ace6b-p113">Благодаря механизм переключения элементов управления эффективной работы ли MDS включен на веб-сайты пользователей. Тем не менее рекомендуется обновить SharePoint элементы управления и компоненты, пользоваться всеми преимуществами MDS. Пользователи получают улучшения работы при MDS спецификации страниц и элементов управления. Хорошо подходят для получения оптимизирован для MDS следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ace6b-p113">Thanks to the failover mechanism, your controls work seamlessly whether or not MDS is enabled in your users' websites. However, it is a good idea to update your SharePoint controls and components to take full advantage of MDS. Users get a better experience when your pages and controls are MDS compliant. The following components are good candidates to get optimized for MDS:</span></span>
  
    
    

- <span data-ttu-id="ace6b-183">Эталонные страницы.</span><span class="sxs-lookup"><span data-stu-id="ace6b-183">Master pages</span></span>
    
  
- <span data-ttu-id="ace6b-184">Страницы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ace6b-184">ASP.NET pages</span></span>
    
  
- <span data-ttu-id="ace6b-185">Элементы управления и веб-частей</span><span class="sxs-lookup"><span data-stu-id="ace6b-185">Controls and Web Parts</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="ace6b-186">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ace6b-186">Additional resources</span></span>
<span data-ttu-id="ace6b-187"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ace6b-187"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="ace6b-188">EnableMinimalDownload</span><span class="sxs-lookup"><span data-stu-id="ace6b-188">EnableMinimalDownload</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Client.Web.EnableMinimalDownload.aspx)
    
  
-  [<span data-ttu-id="ace6b-189">Изменение компонентов SharePoint для MDS</span><span class="sxs-lookup"><span data-stu-id="ace6b-189">Modify SharePoint components for MDS</span></span>](modify-sharepoint-components-for-mds.md)
    
  
-  [<span data-ttu-id="ace6b-190">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ace6b-190">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  

