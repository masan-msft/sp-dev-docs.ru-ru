---
title: "Добавление фрагмента кода \"Зона веб-частей\" в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7583b217-200c-4569-8f88-fe975c8ebd72
ms.openlocfilehash: 3fcccf3e3be505706bc97a7f7b343e4a2f48027a
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="add-a-web-part-zone-snippet-in-sharepoint"></a><span data-ttu-id="69413-102">Добавление фрагмента кода "Зона веб-частей" в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69413-102">How to: Add a Web Part zone snippet in SharePoint</span></span>

<span data-ttu-id="69413-103">Зона веб-частей  это фрагмент, который можно добавить к макету страницы, чтобы авторы контента могли добавлять, редактировать и удалять веб-части в этой зоне.</span><span class="sxs-lookup"><span data-stu-id="69413-103">A Web Part zone is a snippet that you can add to a page layout so that content authors can add, edit, or delete Web Parts in that zone.</span></span>

## <a name="introduction-to-the-web-part-zone-snippet"></a><span data-ttu-id="69413-104">Общие сведения о фрагменте зоны веб-частей</span><span class="sxs-lookup"><span data-stu-id="69413-104">Introduction to the Web Part zone snippet</span></span>
<span data-ttu-id="69413-105"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="69413-105"><a name="Introduction"> </a></span></span>

<span data-ttu-id="69413-p101">Веб-часть  это элемент управления сервера, который предоставляет некоторые функции SharePoint, а зона веб-частей  это контейнер, который определяет макет, поведение и другие свойства веб-частей в этой зоне. Например, зона веб-частей может указывать, будут ли веб-части в этой зоне:</span><span class="sxs-lookup"><span data-stu-id="69413-p101">A Web Part is a server control that provides a specific piece of SharePoint functionality, and a Web Part zone is a container that determines the layout, behavior, and other properties of the Web Parts contained in that zone. For example, a Web Part zone can specify whether the Web Parts in the zone:</span></span>
  
    
    

- <span data-ttu-id="69413-108">упорядочены по горизонтали или по вертикали;</span><span class="sxs-lookup"><span data-stu-id="69413-108">Are arranged in a horizontal or vertical layout.</span></span> 
    
  
- <span data-ttu-id="69413-109">отображать распространенные элементы пользовательского интерфейса, например строку заголовка или границу;</span><span class="sxs-lookup"><span data-stu-id="69413-109">Display common user interface (UI) elements such as a title bar or border.</span></span>
    
  
- <span data-ttu-id="69413-110">доступны для настройки авторами контента при редактировании страницы в браузере;</span><span class="sxs-lookup"><span data-stu-id="69413-110">Can be customized by content authors when they edit a page in the browser.</span></span>
    
  
- <span data-ttu-id="69413-111">доступны для персонализации посетителями сайта, которые создают личное представление веб-части при просмотре страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="69413-111">Can be personalized by site visitors who create a personal view of a Web Part when they view a page in the browser.</span></span>
    
  
<span data-ttu-id="69413-p102">На сайте публикации авторы контента с необходимыми разрешениями могут создавать или редактировать страницы, которые хранятся в библиотеке "Страницы". Как разработчик вы можете добавить зону веб-частей к макету страницы. Когда автор контента создает или редактирует страницу на основе ее макета, он может добавлять, редактировать или удалять веб-части в этой зоне. Например, вы можете добавить зону веб-частей к макету страницы, чтобы авторы контента могли:</span><span class="sxs-lookup"><span data-stu-id="69413-p102">In a publishing site, content authors with the necessary permissions can create or edit pages that reside in the Pages library. As a designer, you can add a Web Part zone to a page layout. When a content author creates or edits a page based on that page layout, the author can add, edit, or delete Web Parts in that zone. For example, you may want to add a Web Part zone to a page layout so that content authors can:</span></span>
  
    
    

- <span data-ttu-id="69413-p103">отображать результаты поискового запроса с помощью веб-части поиска контента. Авторы могут обновлять или изменять поисковый запрос, если веб-часть на основе поиска хранится в зоне веб-частей;</span><span class="sxs-lookup"><span data-stu-id="69413-p103">Display the results of a search query by using a Content Search Web Part. Authors can update or modify the search query when a search-driven Web Part resides inside a Web Part zone.</span></span>
    
  
- <span data-ttu-id="69413-118">встраивать видеоролики и аудиофайлы в веб-страницу с помощью веб-части "Мультимедиа";</span><span class="sxs-lookup"><span data-stu-id="69413-118">Embed video or audio clips in a webpage by using a Media Web Part.</span></span>
    
  
- <span data-ttu-id="69413-119">создавать списки гиперссылок, которые легко редактировать, группировать и упорядочивать, с помощью веб-части "Сводная ссылка";</span><span class="sxs-lookup"><span data-stu-id="69413-119">Create lists of hyperlinks that are easily edited, grouped, or reordered by using a Summary Link Web Part.</span></span>
    
  
- <span data-ttu-id="69413-120">создать карту сайта, которая содержит список всех страниц на сайте и автоматически обновляется при добавлении, удалении, переименовании или перемещении страницы, с помощью веб-части "Оглавление".</span><span class="sxs-lookup"><span data-stu-id="69413-120">Create a site map that lists all pages in a site and that is automatically updated whenever a page is added, deleted, renamed, or moved by using a Table of Contents Web Part.</span></span>
    
  

### <a name="when-to-use-web-part-zones"></a><span data-ttu-id="69413-121">Когда использовать зоны веб-частей</span><span class="sxs-lookup"><span data-stu-id="69413-121">When to use Web Part zones</span></span>

<span data-ttu-id="69413-p104">Если макет страницы включает одну или несколько зон веб-частей, то они доступны на всех страницах, использующих этот макет, что позволяет авторам вставлять веб-части в эти зоны. Позволяя авторам вставлять веб-части на страницы, вы ослабляете свой контроль над пользовательским интерфейсом сайта. Например, автор может вставить веб-часть "Оглавление" на страницу, которая отображает части вашего сайта, на которые пользователи не должны переходить с текущей страницы.</span><span class="sxs-lookup"><span data-stu-id="69413-p104">When a page layout includes one or more Web Part zones, the Web Part zones are available on all pages that use that layout, which enables authors to insert Web Parts onto those pages. If you enable authors to insert Web Parts on pages, you reduce your control over the users' experience of the site. For example, an author could insert a Table of Contents Web Part onto a page that exposes parts of your site that you don't want visitors to navigate to from the current page.</span></span>
  
    
    
<span data-ttu-id="69413-p105">Если вам нужен полный контроль над внешним видом веб-части на вашем сайте и эта веб-часть должна отображаться на всех страницах определенного типа, добавьте веб-часть непосредственно на эталонную страницу.</span><span class="sxs-lookup"><span data-stu-id="69413-p105">If you want complete control over how a Web Part appears on your site, and if you want that Web Part to appear on all pages of a certain type, add the Web Part directly to a page layout. If you want a Web Part to appear on all pages in a site, you can also add a Web Part directly to a master page.</span></span>
  
> [!NOTE]
> <span data-ttu-id="69413-127">Зоны веб-частей доступны на макетах страниц, но недоступны на эталонных страницах — зоны позволяют авторам изменять веб-части, а авторы обычно не меняют эталонную страницу.</span><span class="sxs-lookup"><span data-stu-id="69413-127">Web Part zones are available on page layouts but not on master pages—the purpose of zones is to allow authors to modify Web Parts, and authors typically don't edit a master page.</span></span> 
  
    
    

<span data-ttu-id="69413-p106">Вы также можете добавлять зоны веб-частей к макетам страниц, но ограничивать их использование. Например, вы можете добавить веб-части к зоне, а затем задать свойство этой зоны, чтобы авторы контента могли редактировать свойства существующих веб-частей, но не могли добавлять и удалять веб-части в зоне. Зоны веб-частей имеют ряд свойств, которые служат для двух целей. Один набор свойств можно использовать для организации макета и форматирования веб-частей на странице. Другой позволяет обеспечить дополнительный уровень защиты от изменения (или "блокирование") веб-частей в зоне.</span><span class="sxs-lookup"><span data-stu-id="69413-p106">You can also add Web Part zones to a page layout but restrict their use. For example, you can add Web Parts to a zone, and then set a property of that zone so that content authors can edit the properties of existing Web Parts but not add or remove Web Parts from the zone. Web Part zones have a set of properties that serve a dual purpose. You can use one subset of properties to organize the layout and format of Web Parts on the page. You can use another subset of properties to provide an additional level of protection from modification (or "lock down") of the Web Parts within the zone.</span></span>
  
    
    
<span data-ttu-id="69413-133">Для различных уровней контроля над внешним видом веб-частей на сайте вы можете:</span><span class="sxs-lookup"><span data-stu-id="69413-133">For varying levels of control over how Web Parts are presented on your site, you can:</span></span>
  
    
    

- <span data-ttu-id="69413-p107">добавить веб-части непосредственно на эталонную страницу или макет страницы. Это означает, что авторы контента не могут изменять веб-части;</span><span class="sxs-lookup"><span data-stu-id="69413-p107">Add Web Parts directly to a master page or page layout. This means content authors cannot modify the Web Parts.</span></span>
    
  
- <span data-ttu-id="69413-136">добавить веб-части к зонам на макетах страниц, но ограничить эти зоны только веб-частями по умолчанию, которые вы добавляете;</span><span class="sxs-lookup"><span data-stu-id="69413-136">Add Web Parts to zones on page layouts, but restrict those zones to only the default Web Parts that you add.</span></span>
    
  
- <span data-ttu-id="69413-137">добавить зоны веб-частей на макеты страниц и предоставить авторам контента полный контроль над внешним видом и конфигурацией веб-частей в этих зонах.</span><span class="sxs-lookup"><span data-stu-id="69413-137">Add Web Part zones to page layouts, and give content authors complete control over what Web Parts appear in those zones and how they are configured.</span></span>
    
  
<span data-ttu-id="69413-138">Свойства зоны веб-частей могут указывать, разрешается ли авторам контента изменять:</span><span class="sxs-lookup"><span data-stu-id="69413-138">The properties of a Web Part zone can specify whether content authors are allowed to change:</span></span>
  
    
    

- <span data-ttu-id="69413-139">макеты веб-частей в зоне путем добавления, удаления, изменения размеров и перемещения веб-частей;</span><span class="sxs-lookup"><span data-stu-id="69413-139">The layout of Web Parts in the zone by adding, deleting, resizing, or moving the Web Parts.</span></span>
    
  
- <span data-ttu-id="69413-140">параметры веб-частей для всех пользователей (общее представление веб-части);</span><span class="sxs-lookup"><span data-stu-id="69413-140">The Web Part settings for all users (the shared view of a Web Part).</span></span>
    
  
- <span data-ttu-id="69413-141">личные параметры веб-частей (личное представление веб-части).</span><span class="sxs-lookup"><span data-stu-id="69413-141">Their personal Web Part settings (the personal view of a Web Part).</span></span>
    
  
<span data-ttu-id="69413-142">В таблице 1 показаны важные свойства, которые следует учитывать, если требуется ограничить зону веб-частей.</span><span class="sxs-lookup"><span data-stu-id="69413-142">Table 1 shows important properties to consider when you want to restrict a Web Part zone.</span></span>
  
    
    

<span data-ttu-id="69413-143">**Таблица 1. Свойства зоны веб-частей, используемые для ограничения авторов контента**</span><span class="sxs-lookup"><span data-stu-id="69413-143">**Table 1. Web Part zone properties used to restrict content authors**</span></span>


|<span data-ttu-id="69413-144">**Имя свойства**</span><span class="sxs-lookup"><span data-stu-id="69413-144">**Property Name**</span></span>|<span data-ttu-id="69413-145">**Описание**</span><span class="sxs-lookup"><span data-stu-id="69413-145">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="69413-146">**AllowLayoutChange**</span><span class="sxs-lookup"><span data-stu-id="69413-146">**AllowLayoutChange**</span></span> <br/> |<span data-ttu-id="69413-147">Указывает, можно ли закрывать, сворачивать, удалять и восстанавливать веб-части в зоне.</span><span class="sxs-lookup"><span data-stu-id="69413-147">Specifies whether Web Parts within the zone can be closed, minimized, deleted, or restored.</span></span>  <br/> <span data-ttu-id="69413-p108">Если задано значение **False**, то пользователи не могут закрывать, сворачивать, удалять и восстанавливать веб-части в зоне, перетаскивать веб-части и другие зоны, а также перемещать веб-части и менять их местами. Пользователи также не могут добавлять веб-части из каталога, а несколько свойств, влияющих на пользовательский интерфейс веб-частей в зоне, отключено. Это свойство не влияет на возможность менять макет программным образом.</span><span class="sxs-lookup"><span data-stu-id="69413-p108">If set to **False**, users cannot close, minimize, delete, or restore Web Parts in the zone, drag Web Parts to a different zone, or rearrange or move Web Parts within the zone. Users also cannot add Web Parts from the Web Part catalog, and several properties that affect the UI of Web Parts in the zone are disabled. This property does not affect the ability to change the layout programmatically.  </span></span><br/> <span data-ttu-id="69413-151">Если задано значение **True**, то пользователи с соответствующими разрешениями могут выполнять эти действия.</span><span class="sxs-lookup"><span data-stu-id="69413-151">If set to **True**, users with appropriate permissions can perform these actions.</span></span>  <br/> |
|<span data-ttu-id="69413-152">**LockLayout**</span><span class="sxs-lookup"><span data-stu-id="69413-152">**LockLayout**</span></span> <br/> |<span data-ttu-id="69413-p109">Указывает, можно ли добавлять, удалять и перемещать веб-части в зоне, а также менять их размеры.</span><span class="sxs-lookup"><span data-stu-id="69413-p109">Specifies whether Web Parts within the zone can be added, deleted, resized, or moved. This property works the same whether the Web Part Page is in personal view or shared view.  </span></span><br/> <span data-ttu-id="69413-p110"> Если задано значение **True**, то затрагиваются следующие свойства каждой веб-части в зоне: **Зона (ZoneID)**, **Порядок частей (PartOrder)**, **Видимость на странице (IsVisible)**, **Высота (Height)**, **Ширина (Width)**, **Разрешить закрытие (AllowRemove)** и **IsIncluded** (команда **Закрыть** в меню **Веб-часть**). Остальные свойства веб-частей остаются без изменений.  </span><span class="sxs-lookup"><span data-stu-id="69413-p110">If set to **True**, the specific Web Part properties for each Web Part in the zone that are affected are: **Zone (ZoneID)**, **Part Order (PartOrder)**, **Visible on Page (IsVisible)**, **Height (Height)**, **Width (Width)**, **Allow Close (AllowRemove)**, and **IsIncluded** (the **Close** command on the **Web Part** menu). Other Web Part properties are not affected. </span></span><br/> <span data-ttu-id="69413-157">Если задано значение **False**, то свойства веб-частей определяют, можно ли выполнять изменения (а также соответствующие разрешения на сайте).</span><span class="sxs-lookup"><span data-stu-id="69413-157">If set to **False**, the Web Part properties determine whether modifications can be made (together with the appropriate site permissions).</span></span>  <br/> |
|<span data-ttu-id="69413-158">**AllowCustomization**</span><span class="sxs-lookup"><span data-stu-id="69413-158">**AllowCustomization**</span></span> <br/> |<span data-ttu-id="69413-159">Указывает, можно ли менять значения общих свойств веб-частей в зоне.</span><span class="sxs-lookup"><span data-stu-id="69413-159">Specifies whether shared property values of Web Parts within the zone can be modified.</span></span>  <br/> <span data-ttu-id="69413-160">Если задано значение **True**, то пользователи с соответствующими разрешениями могут изменять веб-части в зоне для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="69413-160">If set to **True**, users with appropriate permissions can make changes to the Web Parts in the zone for all users.</span></span>  <br/> <span data-ttu-id="69413-p111">Если задано значение **False**, то пользователи не могут изменять веб-части в зоне пользовательского интерфейса в общем представлении. Тем не менее, эти изменения можно выполнить программным способом и на странице "Управление веб-частями".</span><span class="sxs-lookup"><span data-stu-id="69413-p111">If set to **False**, users cannot make changes to the Web Parts in the zone in the UI in shared view. But, changes can still be made programmatically and by using the Web Part Maintenance page.  </span></span><br/> |
|<span data-ttu-id="69413-163">**AllowPersonalization**</span><span class="sxs-lookup"><span data-stu-id="69413-163">**AllowPersonalization**</span></span> <br/> |<span data-ttu-id="69413-164">Указывает, можно ли менять значения личных свойств веб-частей в зоне.</span><span class="sxs-lookup"><span data-stu-id="69413-164">Specifies whether personal property values of Web Parts within the zone can be modified.</span></span>  <br/> <span data-ttu-id="69413-165">Если задано значение **True**, то пользователи с соответствующими разрешениями могут выполнять личные изменения веб-частей в зоне.</span><span class="sxs-lookup"><span data-stu-id="69413-165">If set to **True**, users with appropriate permissions can make personal changes to the Web Parts in the zone.</span></span>  <br/> <span data-ttu-id="69413-166">Если задано значение **False**, то пользователи не могут выполнять изменения веб-частей через пользовательский интерфейс, если эта веб-часть не является личной и у них нет соответствующих разрешений.</span><span class="sxs-lookup"><span data-stu-id="69413-166">If set to **False**, users cannot make personal changes to the Web Parts through the UI, unless the Web Part is a private Web Part and they have appropriate permissions.</span></span>  <br/> |
   
> [!NOTE]
> <span data-ttu-id="69413-167">Зону веб-части невозможно вставить на панели канала устройства.</span><span class="sxs-lookup"><span data-stu-id="69413-167">Note: You cannot insert a Web Part zone inside a Device Channel Panel.</span></span> <span data-ttu-id="69413-168">Если вы хотите, чтобы авторы могли добавлять веб-части на страницу, и вас не беспокоит вес страницы для мобильных устройств, можете добавить поле страницы "Редактор форматированного текста" на панель канала устройства, а затем сообщить авторам, что веб-части следует добавлять туда.</span><span class="sxs-lookup"><span data-stu-id="69413-168">If you want to allow authors to add Web Parts to a page, and if you are not concerned about the page weight for mobile devices, you can add a Rich Text Editor page field to a Device Channel Panel, and then instruct authors to add Web Parts there.</span></span> <span data-ttu-id="69413-169">Вы можете добавлять веб-части непосредственно на панель канала устройства (без зоны веб-частей).</span><span class="sxs-lookup"><span data-stu-id="69413-169">You can add Web Parts directly to a Device Channel Panel (without a Web Part zone).</span></span> <span data-ttu-id="69413-170">Дополнительные сведения см. в статье [Сведения о том, как добавить фрагмент кода для панели канала устройства в SharePoint](how-to-add-a-device-channel-panel-snippet-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="69413-170">For more information, see  [How to: Add a Device Channel Panel snippet in SharePoint](how-to-add-a-device-channel-panel-snippet-in-sharepoint.md).</span></span> 
  
    
    


## <a name="inserting-a-web-part-zone-snippet"></a><span data-ttu-id="69413-171">Вставка фрагмента кода для зоны веб-частей</span><span class="sxs-lookup"><span data-stu-id="69413-171">Inserting a Web Part zone snippet</span></span>
<span data-ttu-id="69413-172"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="69413-172"><a name="InsertSnippet"> </a></span></span>

<span data-ttu-id="69413-p113">Как и все фрагменты, этот фрагмент добавляется из коллекции. Чтобы перейти в коллекцию фрагментов, необходимо сначала выбрать макет страницы для редактирования. Зоны веб-частей можно добавлять к макетам страниц, но нельзя добавлять к эталонным страницам.</span><span class="sxs-lookup"><span data-stu-id="69413-p113">Like all snippets, you add this snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a page layout to edit. Web Part zones can be added to page layouts but cannot be added to master pages.</span></span>
  
    
    

### <a name="to-insert-a-web-part-zone-snippet"></a><span data-ttu-id="69413-176">Вставка фрагмента зоны веб-частей</span><span class="sxs-lookup"><span data-stu-id="69413-176">To insert a Web Part zone snippet</span></span>


1. <span data-ttu-id="69413-177">Перейдите на сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="69413-177">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="69413-178">Нажмите значок шестеренки "Параметры" в правом верхнем углу страницы, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="69413-178">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="69413-179">В Дизайнере в левой области панели навигации выберите команду **Изменить макеты страниц**.</span><span class="sxs-lookup"><span data-stu-id="69413-179">In Design Manager, in the left navigation pane, choose **Edit Page Layouts**.</span></span>
    
  
4. <span data-ttu-id="69413-180">Выберите имя макета страницы, к которому нужно добавить фрагмент.</span><span class="sxs-lookup"><span data-stu-id="69413-180">Select the name of the page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="69413-181">Чтобы открыть коллекцию фрагментов, выберите **Фрагменты** в правом верхнем углу страницы предварительного просмотра на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="69413-181">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="69413-182">На вкладке ленты **Конструктор** нажмите **Зона веб-частей**.</span><span class="sxs-lookup"><span data-stu-id="69413-182">On the ribbon, on the **Design** tab, choose **Web Part zone**.</span></span>
    
  
7. <span data-ttu-id="69413-183">В разделе **Об этом компоненте** в правой части коллекции фрагментов щелкните или выберите заголовок раздела, чтобы развернуть или свернуть группу свойств, а затем настройте все нужные настраиваемые параметры.</span><span class="sxs-lookup"><span data-stu-id="69413-183">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="69413-p114">Раздел под названием **Важное** содержит ключевые свойства, необходимые для работы конкретного фрагмента. Идентификатор фрагмента является уникальным для зоны веб-частей. После копирования фрагмента на макет страницы не следует повторно использовать этот идентификатор. Если вам нужно добавить еще один фрагмент зоны веб-частей, нажмите **Обновить**, чтобы создать новый идентификатор для следующего фрагмента.</span><span class="sxs-lookup"><span data-stu-id="69413-p114">The section named **Important** contains the properties that are key to how this particular snippet works. For a Web Part zone, the snippet has a unique ID. After you copy the snippet into your page layout, you should not reuse this ID. If you want to add another Web Part zone snippet, choose **Refresh** to generate a new ID for the next snippet.</span></span>
    
    <span data-ttu-id="69413-188">Описания свойств, необходимых для ограничения зоны веб-частей (**LockLayout**, **AllowCustomization** и **AllowPersonalization**), см. в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="69413-188">For descriptions of properties that are necessary for restricting a Web Part zone ( **LockLayout**, **AllowCustomization**, and **AllowPersonalization**), see Table 1.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="69413-p115">Вы можете заметить, что имена некоторых свойств выделены полужирным шрифтом в таблице свойств коллекции фрагментов. Эти свойства имеют значения, которые были изменены по сравнению со значениями по умолчанию для этого компонента, но эти свойства могут быть необязательными для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="69413-p115">You may notice that some property names are bold in the property grid of the Snippet Gallery. These properties have values that have been changed from the default setting for this component, but these properties are not necessarily relevant to a designer scenario. In other words, a property may be bold but not necessarily important for your scenario.</span></span> 

8. <span data-ttu-id="69413-p116">Настроив свойства, нажмите **Обновить**. При этом обновляется фрагмент HTML в левой части страницы, чтобы разметка отражала настраиваемые параметры. Вы всегда можете нажать кнопку **Сбросить**, чтобы восстановить исходные значения всех свойств.</span><span class="sxs-lookup"><span data-stu-id="69413-p116">After you configure any properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="69413-195">В разделе **Фрагмент HTML** в левой части коллекции фрагментов выберите команду **Копировать в буфер обмена**.</span><span class="sxs-lookup"><span data-stu-id="69413-195">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="69413-196">В редакторе HTML откройте сопоставленный сетевой диск на своем компьютере, а затем откройте HTML-файл для эталонной страницы или макета, к которым добавляется фрагмент.</span><span class="sxs-lookup"><span data-stu-id="69413-196">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
    <span data-ttu-id="69413-197">Дополнительные сведения см. в статье  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="69413-197">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
11. <span data-ttu-id="69413-198">Вставьте фрагмент в том месте HTML-файла, где должна отображаться разметка.</span><span class="sxs-lookup"><span data-stu-id="69413-198">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="69413-199">При добавлении фрагмента к макету страницы необходимо добавить его в блок **PlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="69413-199">When you are adding the snippet to a page layout, make sure to paste the snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="69413-200">Замените **<div>** в разделе `class="DefaultContentBlock"` собственным контентом.</span><span class="sxs-lookup"><span data-stu-id="69413-200">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content.</span></span>
    
  
13. <span data-ttu-id="69413-201">Если вам нужно предварительно заполнить зону веб-частями (например, если в зоне авторам контента разрешено только менять существующие веб-части и запрещено создавать новые), вставьте фрагменты веб-частей после тега **<!--DC … -->**.</span><span class="sxs-lookup"><span data-stu-id="69413-201">If you want to prepopulate the zone with Web Parts—for example, if the zone will restrict content authors to modifying only existing Web Parts and not adding new ones—insert Web Part snippets where the **<!--DC … -->** tag appears.</span></span>
    
  
14. <span data-ttu-id="69413-202">Сохраните страницу, а затем обновите страницу предварительного просмотра на стороне сервера в Дизайнере, чтобы страница приняла ожидаемый вид.</span><span class="sxs-lookup"><span data-stu-id="69413-202">Save the page, and then refresh the server-side preview in Design Manager to make sure the page appears as expected.</span></span>
    
  

## <a name="understanding-the-snippet-markup"></a><span data-ttu-id="69413-203">Сведения о разметке фрагментов</span><span class="sxs-lookup"><span data-stu-id="69413-203">Understanding the snippet markup</span></span>
<span data-ttu-id="69413-204"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="69413-204"><a name="UnderstandMarkup"> </a></span></span>

<span data-ttu-id="69413-p117">Две важнейших части фрагмента зоны веб-частей  свойство **ID** и комментарий **<!--DC … -->**. У каждой зоны должен быть уникальный идентификатор. Если вам нужно добавить к макету страницы несколько веб-частей, обязательно нажимайте кнопку **Обновить** в коллекции фрагментов перед копированием каждого фрагмента, чтобы создать новый идентификатор. Комментарий **<!--DC … -->** необходимо заменить веб-частями, которые должны отображаться в зоне по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="69413-p117">The two most important parts of a Web Part zone snippet are the **ID** property and the **<!--DC … -->** comment. Each zone should have a unique ID. If you want to add more than one Web Part zone to your page layout, make sure to choose **Refresh** in the Snippet Gallery before copying each snippet so that a new ID is generated. The **<!--DC … -->** comment should be replaced with any Web Parts that you want to appear in the zone by default.</span></span>
  
    
    
<span data-ttu-id="69413-209">Дополнительные свойства, которые позволяют ограничить использование зон авторами контента ( **AllowCustomization**, **AllowPersonalization** и **LockLayout**), приводятся в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="69413-209">Additional properties that can be used to restrict how content authors can use zones ( **AllowCustomization**, **AllowPersonalization**, and **LockLayout**) are shown in the following code.</span></span>
  
> [!NOTE]
> <span data-ttu-id="69413-210">Свойства **AllowCustomization**, **AllowPersonalization** и **LockLayout** отображаются в разметке, только если изменить их значения по умолчанию в сетке свойств.</span><span class="sxs-lookup"><span data-stu-id="69413-210">The **AllowCustomization**, **AllowPersonalization**, and **LockLayout** properties appear in the markup only if you change their default values in the property grid.</span></span>
  
    
    




```HTML

<div data-name="WebPartZone">
    <!--CS: Start Web Part Zone Snippet-->
    <!--SPM:<%@Register Tagprefix="WebPartPages" Namespace="Microsoft.SharePoint.WebPartPages" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <div xmlns:ie="ie">
        <!--MS:<WebPartPages:WebPartZone runat="server" ID="x0e5f5212505f48a9aac43df13eeae4f9" AllowCustomization="True" AllowPersonalization="False" FrameType="TitleBarOnly" LockLayout="True" Orientation="Vertical">-->
            <!--MS:<ZoneTemplate>-->
               <!--DC: Replace this comment with default web parts for new pages. -->
            <!--ME:</ZoneTemplate>-->
        <!--ME:</WebPartPages:WebPartZone>-->
    </div>
    <!--CE: End Web Part Zone Snippet-->
</div>

```


## <a name="see-also"></a><span data-ttu-id="69413-211">См. также</span><span class="sxs-lookup"><span data-stu-id="69413-211">See also</span></span>
<span data-ttu-id="69413-212"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="69413-212"><a name="AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="69413-213">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="69413-213">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="69413-214">Класс WebPartZone</span><span class="sxs-lookup"><span data-stu-id="69413-214">WebPartZone class</span></span>](http://msdn.microsoft.com/ru-RU/library/system.web.ui.webcontrols.webparts.webpartzone.aspx)
    
  
-  [<span data-ttu-id="69413-215">Свойства WebPartZoneBase</span><span class="sxs-lookup"><span data-stu-id="69413-215">WebPartZoneBase properties</span></span>](http://msdn.microsoft.com/ru-RU/library/335sw9k3.aspx)
    
  
-  [<span data-ttu-id="69413-216">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="69413-216">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="69413-217">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69413-217">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

