---
title: "Сайт фирменной символики и страница центра развертывания решений SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 6d522af8f85a750656ef53b00785591bac4f93b4
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="sharepoint-site-branding-and-page-customization-solutions"></a><span data-ttu-id="8b513-102">Сайт фирменной символики и страница центра развертывания решений SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b513-102">SharePoint site branding and page customization solutions</span></span>

<span data-ttu-id="8b513-103">Используйте модель страницы SharePoint и вариантов оформления, модуль SharePoint 2013 темы и CSS для фирменной символики сайта SharePoint и страницы.</span><span class="sxs-lookup"><span data-stu-id="8b513-103">Use the SharePoint page model and composed looks, the SharePoint 2013 theming engine, and CSS to brand your SharePoint site and pages.</span></span>

<span data-ttu-id="8b513-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="8b513-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="8b513-105">Можно настроить внешний вид и функции сайта SharePoint двумя способами:</span><span class="sxs-lookup"><span data-stu-id="8b513-105">You can customize the look and feel of a SharePoint site in two ways:</span></span>

- <span data-ttu-id="8b513-106">С помощью модуля темы для создания пользовательских тем (вариантов оформления в SharePoint 2013 и SharePoint Online).</span><span class="sxs-lookup"><span data-stu-id="8b513-106">By using the theming engine to create custom themes (composed looks in SharePoint 2013 and SharePoint Online).</span></span> <span data-ttu-id="8b513-107">Как минимум тем определения цветов.</span><span class="sxs-lookup"><span data-stu-id="8b513-107">At a minimum, themes define colors.</span></span> <span data-ttu-id="8b513-108">Полный тема определяет цвета, шрифты, фонового изображения и связанных главной страницы и .preview-файл, определяющий, как просмотреть главную страницу.</span><span class="sxs-lookup"><span data-stu-id="8b513-108">A complete theme defines colors, fonts, a background image, and the associated master page, and a .preview file that defines how the .master page is previewed.</span></span> <span data-ttu-id="8b513-109">Удаленный подготовки шаблон можно использовать для применения темы к сайтам.</span><span class="sxs-lookup"><span data-stu-id="8b513-109">You can use the remote provisioning pattern to apply themes to sites.</span></span>

- <span data-ttu-id="8b513-110">Необходимо создать пользовательские каскадные таблицы стилей (CSS) для применения к сайтам SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8b513-110">By creating custom cascading style sheets (CSS) to apply to SharePoint Online sites.</span></span> <span data-ttu-id="8b513-111">Приложения для SharePoint и удаленных подготовки шаблон можно использовать для подготовки сайтов SharePoint с помощью настраиваемого CSS.</span><span class="sxs-lookup"><span data-stu-id="8b513-111">You can use an app for SharePoint and the remote provisioning pattern to provision SharePoint sites to use custom CSS.</span></span>

<span data-ttu-id="8b513-112">Фирменная символика изменения в диапазоне от недорогих и простых дорогого и комплексного.</span><span class="sxs-lookup"><span data-stu-id="8b513-112">Branding changes range from low-cost and simple to high-cost and complex.</span></span> <span data-ttu-id="8b513-113">Пользователи могут использовать пользовательский Интерфейс для применения вариантов оформления, включая фонового изображения, цветовой палитры, шрифты, главной страницы и файл связанного .preview для главной страницы.</span><span class="sxs-lookup"><span data-stu-id="8b513-113">Users can use the UI to apply composed looks, which include a background image, color palette, fonts, a master page, and an associated .preview file for the master page.</span></span> <span data-ttu-id="8b513-114">Модуль SharePoint 2013 темы можно использовать для создания вариантов оформления и подготовка сайтов, и можно создавать настраиваемые CSS для изменения внешнего вида сайта и его элементы.</span><span class="sxs-lookup"><span data-stu-id="8b513-114">You can use the SharePoint 2013 theming engine to design composed looks and provision sites, and you can create custom CSS to modify the look and feel of your site and its elements.</span></span>

<span data-ttu-id="8b513-115">**Важные**  Можно создать настраиваемые главные страницы и другие структурные элементы в рамках пользовательского брендинга проекта, но долгосрочного затрат на поддержку настраиваемых главных страниц и других настраиваемых элементов структурные высокой.</span><span class="sxs-lookup"><span data-stu-id="8b513-115">**Important**  Although it's possible to create custom master pages and other structural elements as part of a custom branding project, the long-term cost of supporting custom master pages and other custom structural elements is high.</span></span> <span data-ttu-id="8b513-116">Настраиваемый фирменный стиль можно сделать его более высоких для вашей организации применить обновления и обеспечение непрерывной поддержки.</span><span class="sxs-lookup"><span data-stu-id="8b513-116">Custom branding can make it more costly for your organization to apply upgrades and provide ongoing support.</span></span>

<span data-ttu-id="8b513-117">В этом разделе выполняется построение знания о [разработки в SharePoint и средства разработки и рекомендации](SharePoint-development-and-design-tools-and-practices.md), показывающие, как настроить внешний вид и функции сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-117">This section builds on your knowledge about [SharePoint development and design tools and practices](SharePoint-development-and-design-tools-and-practices.md), to show you how to customize the look and feel of a SharePoint site.</span></span>

## <a name="key-terms-and-concepts-related-to-sharepoint-branding"></a><span data-ttu-id="8b513-118">Ключевые термины и концепции, связанные с фирменной настройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b513-118">Key terms and concepts related to SharePoint branding</span></span>
<span data-ttu-id="8b513-119"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="8b513-119"></span></span>

|<span data-ttu-id="8b513-120">**Концепция или термин**</span><span class="sxs-lookup"><span data-stu-id="8b513-120">**Term or concept**</span></span>|<span data-ttu-id="8b513-121">**Определение**</span><span class="sxs-lookup"><span data-stu-id="8b513-121">**Definition**</span></span>|<span data-ttu-id="8b513-122">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="8b513-122">**More information**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="8b513-123">Альтернативной таблицы CSS</span><span class="sxs-lookup"><span data-stu-id="8b513-123">Alternate CSS</span></span>|<span data-ttu-id="8b513-124">Файл CSS, используемый по умолчанию, который можно применять к внешнего вида веб-узла.</span><span class="sxs-lookup"><span data-stu-id="8b513-124">A CSS file other than the default that you can apply to the look and feel of your site.</span></span>|<span data-ttu-id="8b513-125">Использование альтернативной таблицы CSS для применения настраиваемых CSS к сайту и всем его дочерним сайтам.</span><span class="sxs-lookup"><span data-stu-id="8b513-125">Use alternate CSS to apply custom CSS to a site and all of its subsites.</span></span> |
|<span data-ttu-id="8b513-126">CSS</span><span class="sxs-lookup"><span data-stu-id="8b513-126">CSS</span></span>|<span data-ttu-id="8b513-127">Язык, сообщающий как отображать документ XML или HTML стили браузера.</span><span class="sxs-lookup"><span data-stu-id="8b513-127">A language that tells a browser how to render an HTML or XML document's styles.</span></span> <span data-ttu-id="8b513-128">CSS разделяет содержимое документа (HTML или XML) из представления содержимого.</span><span class="sxs-lookup"><span data-stu-id="8b513-128">CSS separates document content (HTML or XML) from how the content is presented.</span></span>||
|<span data-ttu-id="8b513-129">Вариант оформления</span><span class="sxs-lookup"><span data-stu-id="8b513-129">Composed look</span></span>|<span data-ttu-id="8b513-130">Сочетание шрифтов, цветовой палитры, фонового изображения и связанную главную страницу, которые применяются к сайту.</span><span class="sxs-lookup"><span data-stu-id="8b513-130">A combination of fonts, a color palette, a background image, and an associated master page that are applied to the site.</span></span> <span data-ttu-id="8b513-131">Изображения схемы и цвет шрифта являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="8b513-131">Font scheme and color images are optional.</span></span> <span data-ttu-id="8b513-132">Ниже приведен расположения файлов по умолчанию для вариантов оформления: папка Gallery\15 темы</span><span class="sxs-lookup"><span data-stu-id="8b513-132">The following is the default file location for composed looks: Theme Gallery\15 folder</span></span>|<p><span data-ttu-id="8b513-133">Вариантов оформления являются удобным способом для изменения внешнего вида сайтов без внесения изменений в структуру сайта.</span><span class="sxs-lookup"><span data-stu-id="8b513-133">Composed looks are a convenient way to change the look and feel of sites without making any changes to the structure of a site.</span></span></p><p><span data-ttu-id="8b513-134">SharePoint 2013 поставляется несколько вариантов оформления по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b513-134">SharePoint 2013 ships several composed looks by default.</span></span> <span data-ttu-id="8b513-135">После применения вариант оформления, SharePoint применяет все связанные рабочую область вариант оформления на сайт.</span><span class="sxs-lookup"><span data-stu-id="8b513-135">When a user applies a composed look, SharePoint applies all the associated design elements of the composed look to a site.</span></span></p>|
|<span data-ttu-id="8b513-136">Веб-часть поиска контента (CSWP)</span><span class="sxs-lookup"><span data-stu-id="8b513-136">Content Search Web Part (CSWP)</span></span>|<span data-ttu-id="8b513-137">Отображение содержимого из результатов поиска на основе указанного запроса.</span><span class="sxs-lookup"><span data-stu-id="8b513-137">Renders content from search results based on a specified query.</span></span>| <p><span data-ttu-id="8b513-138">[Веб-часть поиска контента в SharePoint 2013](http://social.technet.microsoft.com/wiki/contents/articles/15843.content-search-web-part-in-sharepoint-2013.aspx) (TechNet)</span><span class="sxs-lookup"><span data-stu-id="8b513-138">[Content Search Web Part in SharePoint 2013](http://social.technet.microsoft.com/wiki/contents/articles/15843.content-search-web-part-in-sharepoint-2013.aspx) (TechNet)</span></span> </p><p><span data-ttu-id="8b513-139">[Веб-часть поиска контента в SharePoint 2013](http://msdn.microsoft.com/library/6fb4bf41-0846-4dca-ad9e-906afdfd3d2b.aspx) (MSDN)</span><span class="sxs-lookup"><span data-stu-id="8b513-139">[Content Search Web Part in SharePoint 2013](http://msdn.microsoft.com/library/6fb4bf41-0846-4dca-ad9e-906afdfd3d2b.aspx) (MSDN)</span></span></p>|
|<span data-ttu-id="8b513-140">corev15.CSS</span><span class="sxs-lookup"><span data-stu-id="8b513-140">corev15.css</span></span>|<span data-ttu-id="8b513-141">CSS-файл, который содержит большую часть основных функций для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-141">The CSS file that contains most of the main functionality for SharePoint.</span></span> <span data-ttu-id="8b513-142">Ниже приведен расположение: _layouts\15 папка по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8b513-142">The following is the default file location:_layouts\15 folder</span></span>||
|<span data-ttu-id="8b513-143">CSSRegistration</span><span class="sxs-lookup"><span data-stu-id="8b513-143">CSSRegistration</span></span>|<span data-ttu-id="8b513-144">Ссылка на главной странице, такие как seattle.master, загружаемой большинство CSS, применяемый к большая часть пользовательского интерфейса по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b513-144">A reference in a master page, such as seattle.master, that loads most CSS that is applied to most of the default UI.</span></span>|<span data-ttu-id="8b513-145">Использование элемента управления **CSSRegistration** на главной странице для переопределения по умолчанию CSS.</span><span class="sxs-lookup"><span data-stu-id="8b513-145">Use the  **CSSRegistration** control in a master page to override default CSS.</span></span>|
|<span data-ttu-id="8b513-146">Настраиваемое действие</span><span class="sxs-lookup"><span data-stu-id="8b513-146">Custom action</span></span>|<span data-ttu-id="8b513-147">Действия, которые можно использовать для настройки и работать со списками и на ленте на хост-сайта.</span><span class="sxs-lookup"><span data-stu-id="8b513-147">Actions you can use to customize and interact with lists and the ribbon on the host web.</span></span>| [<span data-ttu-id="8b513-148">Как: Создание настраиваемых действий для развертывания с помощью SharePoint надстройки</span><span class="sxs-lookup"><span data-stu-id="8b513-148">How to: Create custom actions to deploy with SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/bbd11f94-1798-453e-bbb0-e5eb0df8dc75.aspx)|
|<span data-ttu-id="8b513-149">Каналы устройств</span><span class="sxs-lookup"><span data-stu-id="8b513-149">Device channels</span></span>|<span data-ttu-id="8b513-150">Один сайт публикации SharePoint в несколько способов отображения с использованием уникальных каналы для отображения контента конечного на определенных устройствах.</span><span class="sxs-lookup"><span data-stu-id="8b513-150">Render a single SharePoint publishing site in more than one way by using unique channels to target content rendering on specific devices.</span></span>| [<span data-ttu-id="8b513-151">Каналы устройств в компоненте "Дизайнер" SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-151">SharePoint 2013 Design Manager device channels</span></span>](http://msdn.microsoft.com/library/a924bd7b-a5e3-41bf-b0a7-3e43945fa951.aspx)|
|<span data-ttu-id="8b513-152">Шаблоны отображения</span><span class="sxs-lookup"><span data-stu-id="8b513-152">Display templates</span></span>|<span data-ttu-id="8b513-153">Шаблоны, используемые веб-частей поиска для отображения результатов запроса, внесенные в индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="8b513-153">Templates used by Search Web Parts to show the results of a query made to the search index.</span></span>| [<span data-ttu-id="8b513-154">Шаблоны для отображения дизайнер SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-154">SharePoint 2013 Design Manager display templates</span></span>](http://msdn.microsoft.com/library/1a782bac-48ee-4baf-8751-0f943a306e0f.aspx)|
|<span data-ttu-id="8b513-155">Передача изображения</span><span class="sxs-lookup"><span data-stu-id="8b513-155">Image rendition</span></span>|<span data-ttu-id="8b513-156">Отображение версии по-разному размера изображения на сайте публикации на основании одного источника изображения.</span><span class="sxs-lookup"><span data-stu-id="8b513-156">Display differently sized versions of an image on a publishing site based on the same source image.</span></span>| [<span data-ttu-id="8b513-157">Дизайнер SharePoint 2013 изображений</span><span class="sxs-lookup"><span data-stu-id="8b513-157">SharePoint 2013 Design Manager image renditions</span></span>](http://msdn.microsoft.com/library/d08a74c0-5674-4f26-8646-11ea1f081c85.aspx)|
|<span data-ttu-id="8b513-158">Управляемые метаданные</span><span class="sxs-lookup"><span data-stu-id="8b513-158">Managed metadata</span></span>| <span data-ttu-id="8b513-159">Компоненты SharePoint, которые позволяют вам определения терминов, наборов терминов, группы и подписи для терминов.</span><span class="sxs-lookup"><span data-stu-id="8b513-159">Features in SharePoint that enable you to define terms, term sets, groups, and labels for terms.</span></span> <span data-ttu-id="8b513-160">Иногда называется таксономии.</span><span class="sxs-lookup"><span data-stu-id="8b513-160">Sometimes referred to as taxonomy.</span></span> <span data-ttu-id="8b513-161">В SharePoint 2013 системы управляемых метаданных является основой для управляемой навигации.</span><span class="sxs-lookup"><span data-stu-id="8b513-161">In SharePoint 2013, the managed metadata system is the foundation for managed navigation.</span></span>| [<span data-ttu-id="8b513-162">Управляемые метаданные и навигация в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-162">Managed metadata and navigation in SharePoint 2013</span></span>](http://msdn.microsoft.com/library/b66d4ec1-a2ef-49cc-8ca5-a6b516bff02e.aspx)|
|<span data-ttu-id="8b513-163">Управляемая навигация</span><span class="sxs-lookup"><span data-stu-id="8b513-163">Managed navigation</span></span>|<span data-ttu-id="8b513-164">Навигации для сайтов публикации, построенного на основе управляемых метаданных.</span><span class="sxs-lookup"><span data-stu-id="8b513-164">Navigation for publishing sites that is built based on managed metadata.</span></span> <span data-ttu-id="8b513-165">Навигация строится на основе указанного набора терминов в банке терминов.</span><span class="sxs-lookup"><span data-stu-id="8b513-165">Navigation is built from a specified term set in the term store.</span></span> | [<span data-ttu-id="8b513-166">Управляемая навигация в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-166">Managed navigation in SharePoint 2013</span></span>](http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02.aspx)|
|<span data-ttu-id="8b513-167">Главная страница</span><span class="sxs-lookup"><span data-stu-id="8b513-167">Master page</span></span>|<span data-ttu-id="8b513-168">Страница, стандартизация поведение и презентации панели навигации слева и области верхней панели навигации на странице SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-168">A page that standardizes the behavior and presentation of the left navigation and top navigation areas of a SharePoint page.</span></span>| [<span data-ttu-id="8b513-169">Эталонные страницы, коллекция эталонных страниц и макеты страниц в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-169">Master pages, the Master Page Gallery, and page layouts in SharePoint 2013</span></span>](http://msdn.microsoft.com/library/80b9a360-bc2e-46c6-b0ca-1bc487b73db6.aspx)|
|<span data-ttu-id="8b513-170">Коллекция главных страниц</span><span class="sxs-lookup"><span data-stu-id="8b513-170">Master Page Gallery</span></span>|<span data-ttu-id="8b513-171">Библиотека специальных документов в SharePoint 2013 все фирменной символики элементы главные страницы, макеты страниц, файлов JavaScript, CSS и изображения являются хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b513-171">A special document library in SharePoint 2013 where all branding elements-master pages, page layouts, JavaScript files, CSS, and images-are stored by default.</span></span> <span data-ttu-id="8b513-172">Каждый сайт имеет свой собственный Gallery.When главных страницы, создание настраиваемых фирменной символики элементы, мы рекомендуем хранения настраиваемых активов в структуре файла по умолчанию коллекции главных страниц.</span><span class="sxs-lookup"><span data-stu-id="8b513-172">Every site has its own Master Page Gallery.When you create custom branding elements, we recommend that you store custom assets in the default Master Page Gallery file structure.</span></span>| [<span data-ttu-id="8b513-173">Эталонные страницы, коллекция эталонных страниц и макеты страниц в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-173">Master pages, the Master Page Gallery, and page layouts in SharePoint 2013</span></span>](http://msdn.microsoft.com/library/80b9a360-bc2e-46c6-b0ca-1bc487b73db6.aspx)|
|<span data-ttu-id="8b513-174">Oslo.master</span><span class="sxs-lookup"><span data-stu-id="8b513-174">Oslo.master</span></span>|<span data-ttu-id="8b513-175">Главная страница в SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="8b513-175">A master page in SharePoint 2013.</span></span>|<span data-ttu-id="8b513-176">Перемещает текущая структура навигации в той же позиции области верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="8b513-176">Moves the current navigation into the same position as the top navigation region.</span></span> |
|<span data-ttu-id="8b513-177">Элемент управления содержимым страницы</span><span class="sxs-lookup"><span data-stu-id="8b513-177">Page content control</span></span>|<span data-ttu-id="8b513-178">Элемент управления на сайте публикации, где можно добавить веб-части.</span><span class="sxs-lookup"><span data-stu-id="8b513-178">A control on a publishing site where a Web Part can be added.</span></span>||
|<span data-ttu-id="8b513-179">Макет страницы</span><span class="sxs-lookup"><span data-stu-id="8b513-179">Page layout</span></span>|<span data-ttu-id="8b513-180">Шаблон для публикации страницу сайта, который позволяет пользователям SharePoint размещать на странице в едином виде.</span><span class="sxs-lookup"><span data-stu-id="8b513-180">A template for a SharePoint publishing site page that lets users lay out information on the page in a consistent way.</span></span>||
|<span data-ttu-id="8b513-181">Панель быстрого запуска</span><span class="sxs-lookup"><span data-stu-id="8b513-181">Quick Launch</span></span>|<span data-ttu-id="8b513-182">Управляет элементы навигации в левой части страницы сайта совместной работы.</span><span class="sxs-lookup"><span data-stu-id="8b513-182">Manages the navigation elements on the left side of the page of a collaboration site.</span></span>|<span data-ttu-id="8b513-183">Заголовок ссылки добавляются в группу элементов навигации.</span><span class="sxs-lookup"><span data-stu-id="8b513-183">You can add heading links to group navigation items.</span></span>|
|<span data-ttu-id="8b513-184">REST</span><span class="sxs-lookup"><span data-stu-id="8b513-184">REST</span></span>|<span data-ttu-id="8b513-185">Без сведений о состоянии архитектурные стиль, выделяет элементы архитектуры и использует HTTP-команды для чтения и записи данных из веб-страниц, содержащих XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="8b513-185">A stateless architectural style that abstracts architectural elements and uses HTTP verbs to read and write data from web pages that contain XML files.</span></span>| [<span data-ttu-id="8b513-186">Начало работы со службой REST для SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-186">Get started with the SharePoint 2013 REST service</span></span>](http://msdn.microsoft.com/library/2de035a0-ac75-43bd-9665-5c5a59c4c590.aspx)|
|<span data-ttu-id="8b513-187">Корневой веб-узел</span><span class="sxs-lookup"><span data-stu-id="8b513-187">Root web</span></span>|<span data-ttu-id="8b513-188">Первый веб-страница в семействе сайтов.</span><span class="sxs-lookup"><span data-stu-id="8b513-188">The first web page in a site collection.</span></span>|<span data-ttu-id="8b513-189">Корневого веб-узла иногда называется корня веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8b513-189">The root web is also sometimes referred to as the Web Application Root.</span></span> |
|<span data-ttu-id="8b513-190">Seattle.master</span><span class="sxs-lookup"><span data-stu-id="8b513-190">Seattle.master</span></span>|<span data-ttu-id="8b513-191">Главную страницу по умолчанию для сайтов публикации и веб-сайтов групп SharePoint 2013.</span><span class="sxs-lookup"><span data-stu-id="8b513-191">The default .master page for SharePoint 2013 team sites and publishing sites.</span></span>||
|<span data-ttu-id="8b513-192">Макет сайта</span><span class="sxs-lookup"><span data-stu-id="8b513-192">Site layout</span></span>|<span data-ttu-id="8b513-193">Посетите главную страницу.</span><span class="sxs-lookup"><span data-stu-id="8b513-193">See master page.</span></span>|<span data-ttu-id="8b513-194">Макет сайта с помощью соответствующего файла .preview объединяет главную страницу темы.</span><span class="sxs-lookup"><span data-stu-id="8b513-194">The site layout combines the .master page of a theme with its corresponding .preview file.</span></span>|
|<span data-ttu-id="8b513-195">Структурированная навигация</span><span class="sxs-lookup"><span data-stu-id="8b513-195">Structured navigation</span></span>|<span data-ttu-id="8b513-196">Структуры переходов сайтов публикации, основанный на иерархию сайта публикации.</span><span class="sxs-lookup"><span data-stu-id="8b513-196">A navigation structure for publishing sites that is based on the site hierarchy of the publishing site.</span></span> <span data-ttu-id="8b513-197">Можно добавить заголовки, а также ссылки на вручную заменить или настроить структурированная навигация, которое автоматически создает SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-197">You can add headers and links to manually replace or customize the structured navigation that SharePoint automatically generates.</span></span>| [<span data-ttu-id="8b513-198">Как: Настройка навигации в SharePoint Server 2010 (ECM)</span><span class="sxs-lookup"><span data-stu-id="8b513-198">How to: Customize Navigation in SharePoint Server 2010 (ECM)</span></span>](https://msdn.microsoft.com/en-us/library/office/ms558975%28v=office.14%29.aspx)|
|<span data-ttu-id="8b513-199">Темы</span><span class="sxs-lookup"><span data-stu-id="8b513-199">Theme</span></span>|<span data-ttu-id="8b513-200">Простой способ применения освещения фирменной символики на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-200">A simple way to apply light branding to a SharePoint site.</span></span> <span data-ttu-id="8b513-201">Расположение файла по умолчанию для темы — это папка _themes сайта.</span><span class="sxs-lookup"><span data-stu-id="8b513-201">The default file location for themes is the _themes folder of the site.</span></span>|<p><span data-ttu-id="8b513-202">Темы являются эффективное использование фирменной символики для сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-202">Themes are an easy way to apply custom branding to SharePoint sites.</span></span></p><p>[<span data-ttu-id="8b513-203">Общие сведения о темах для SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-203">Themes overview for SharePoint 2013</span></span>](http://msdn.microsoft.com/library/ae585dd3-82fe-46bb-ac93-065edc0a16f4.aspx)</p><p> [<span data-ttu-id="8b513-204">Инструкции. Развертывание пользовательской темы в SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-204">How to: Deploy a custom theme in SharePoint 2013</span></span>](http://msdn.microsoft.com/library/f703df24-8e56-4e6a-bc37-95acbb3c83e8.aspx)</p>|
|<span data-ttu-id="8b513-205">Модуль темы</span><span class="sxs-lookup"><span data-stu-id="8b513-205">Theming engine</span></span>|<span data-ttu-id="8b513-206">Набор файлов и функциональные возможности, которые определяют внешний вид, удобство, поведение и сопоставления файлов из состоит оформления.</span><span class="sxs-lookup"><span data-stu-id="8b513-206">A set of files and functionality that define the look, feel, behavior, and file associations of composed looks.</span></span>||
|<span data-ttu-id="8b513-207">Строка агента пользователя</span><span class="sxs-lookup"><span data-stu-id="8b513-207">User Agent String</span></span>|<span data-ttu-id="8b513-208">Сведения о, браузер передает на веб-сайт, определяющий программного обеспечения, с помощью запроса с сервера.</span><span class="sxs-lookup"><span data-stu-id="8b513-208">Information that a browser passes to a website that identifies the software that makes the request from the server.</span></span>| [<span data-ttu-id="8b513-209">Каналы устройств в компоненте "Дизайнер" SharePoint 2013</span><span class="sxs-lookup"><span data-stu-id="8b513-209">SharePoint 2013 Design Manager device channels</span></span>](http://msdn.microsoft.com/library/a924bd7b-a5e3-41bf-b0a7-3e43945fa951.aspx)|
|<span data-ttu-id="8b513-210">Пользовательского настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="8b513-210">User Custom Action</span></span>|<span data-ttu-id="8b513-211">Свойство CSOM, которое возвращает коллекцию настраиваемых действий для веб-сайта, списка или семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="8b513-211">A CSOM property that returns the collection of custom actions for a website, list, or site collection.</span></span> <span data-ttu-id="8b513-212">Расположение файла по умолчанию — это следующее: 15\TEMPLATE\FEATURES</span><span class="sxs-lookup"><span data-stu-id="8b513-212">The default file location is the following: 15\TEMPLATE\FEATURES</span></span><p><span data-ttu-id="8b513-213">Например:</span><span class="sxs-lookup"><span data-stu-id="8b513-213">For example:</span></span></p><p><span data-ttu-id="8b513-214">&lt;HideCustomAction GroupId = «Коллекции»</span><span class="sxs-lookup"><span data-stu-id="8b513-214">&lt;HideCustomAction GroupId="Galleries"</span></span><br /><span data-ttu-id="8b513-215">&nbsp;&nbsp;&nbsp;HideActionId = «Темы»</span><span class="sxs-lookup"><span data-stu-id="8b513-215">&nbsp;&nbsp;&nbsp;HideActionId="Themes"</span></span><br /><span data-ttu-id="8b513-216">&nbsp;&nbsp;&nbsp;Location="Microsoft.SharePoint.SiteSettings»&gt;</span><span class="sxs-lookup"><span data-stu-id="8b513-216">&nbsp;&nbsp;&nbsp;Location="Microsoft.SharePoint.SiteSettings"&gt;</span></span></p>|<p>[<span data-ttu-id="8b513-217">Класс UserCustomAction</span><span class="sxs-lookup"><span data-stu-id="8b513-217">UserCustomAction class</span></span>](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx)</p><p>[<span data-ttu-id="8b513-218">Как: Создание настраиваемых действий для развертывания с помощью SharePoint надстройки</span><span class="sxs-lookup"><span data-stu-id="8b513-218">How to: Create custom actions to deploy with SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/bbd11f94-1798-453e-bbb0-e5eb0df8dc75.aspx)</p><p><span data-ttu-id="8b513-219">[Как: работа с настраиваемыми действиями пользователя](https://msdn.microsoft.com/en-us/library/office/ee538686%28v=office.14%29.aspx) [По умолчанию идентификаторы расположений пользовательских действий и](http://msdn.microsoft.com/library/6889686e-f6e6-4da0-bfd4-099878614980.aspx)</span><span class="sxs-lookup"><span data-stu-id="8b513-219">[How to: Work with User Custom Actions](https://msdn.microsoft.com/en-us/library/office/ee538686%28v=office.14%29.aspx) [Default Custom Action Locations and IDs](http://msdn.microsoft.com/library/6889686e-f6e6-4da0-bfd4-099878614980.aspx)</span></span></p>|

## <a name="in-this-section"></a><span data-ttu-id="8b513-220">В этом разделе:</span><span class="sxs-lookup"><span data-stu-id="8b513-220">In this section</span></span>
<span data-ttu-id="8b513-221"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="8b513-221"></span></span>

|<span data-ttu-id="8b513-222">**Статья**</span><span class="sxs-lookup"><span data-stu-id="8b513-222">**Article**</span></span>|<span data-ttu-id="8b513-223">**Показано, как для...**</span><span class="sxs-lookup"><span data-stu-id="8b513-223">**Shows you how to...**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="8b513-224">Использование состоит выполняет на сайты SharePoint торговая марка</span><span class="sxs-lookup"><span data-stu-id="8b513-224">Use composed looks to brand SharePoint sites</span></span>](Use-composed-looks-to-brand-SharePoint-sites.md)|<span data-ttu-id="8b513-225">Применение вариантов оформления, включая цвета, шрифты и фонового изображения, к сайтам SharePoint 2013 и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8b513-225">Apply composed looks, including colors, fonts, and a background image, to your SharePoint 2013 and SharePoint Online sites.</span></span>|
| [<span data-ttu-id="8b513-226">Использование удаленного обеспечения марки страницах SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b513-226">Use remote provisioning to brand SharePoint pages</span></span>](Use-remote-provisioning-to-brand-SharePoint-pages.md)|<span data-ttu-id="8b513-227">Использование удаленных подготовки для взаимодействия с темами в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-227">Use remote provisioning to interact with themes in SharePoint.</span></span>|
| [<span data-ttu-id="8b513-228">Использование CSS для страницы SharePoint торговая марка</span><span class="sxs-lookup"><span data-stu-id="8b513-228">Use CSS to brand SharePoint pages</span></span>](Use-CSS-to-brand-pages.md)|<span data-ttu-id="8b513-229">Использование удаленных подготовки для взаимодействия с темами в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8b513-229">Use remote provisioning to interact with themes in SharePoint.</span></span>|
| [<span data-ttu-id="8b513-230">Настройка страницы SharePoint с помощью удаленного подготовки и CSS</span><span class="sxs-lookup"><span data-stu-id="8b513-230">Customize a SharePoint page by using remote provisioning and CSS</span></span>](Customize-a-SharePoint-page-by-using-remote-provisioning-and-CSS.md)|<span data-ttu-id="8b513-231">Использование CSS для настройки SharePoint поля форматированного текста и зоны веб-частей.</span><span class="sxs-lookup"><span data-stu-id="8b513-231">Use CSS to customize SharePoint rich text fields and Web Part Zones.</span></span>|
| [<span data-ttu-id="8b513-232">Фирменная символика существующих сайтов SharePoint и области страницы обновления</span><span class="sxs-lookup"><span data-stu-id="8b513-232">Update the branding of existing SharePoint sites and page regions</span></span>](update-the-branding-of-existing-sharepoint-sites-and-page-regions.md) | <span data-ttu-id="8b513-233">Настройка, а затем обновите фирменной настройки существующих сайтов SharePoint или областей страниц SharePoint, включая ленту, структуры переходов сайта, в меню Параметры, представлении дерева и содержимого страницы.</span><span class="sxs-lookup"><span data-stu-id="8b513-233">Customize and then refresh the branding of existing SharePoint sites or regions of SharePoint pages, including the ribbon, the site navigation, the Settings menu, the tree view, and the page content.</span></span>
|[<span data-ttu-id="8b513-234">Настройка OneDrive для бизнеса фирменного стиля сайтов</span><span class="sxs-lookup"><span data-stu-id="8b513-234">Customize OneDrive for Business site branding</span></span>](Customization-Options-For-OD4B-Sites.md)| <span data-ttu-id="8b513-235">Настройка OneDrive для бизнеса сайтов в Office 365 или с помощью модели надстройки, в зависимости от требований вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8b513-235">Customize OneDrive for Business sites in Office 365 or by using the add-in model, depending on your organization's requirements.</span></span>|

## <a name="additional-resources"></a><span data-ttu-id="8b513-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b513-236">Additional resources</span></span>
<span data-ttu-id="8b513-237"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8b513-237"></span></span>

-  [<span data-ttu-id="8b513-238">Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="8b513-238">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)

-  [<span data-ttu-id="8b513-239">Модель страницы и страницы SharePoint</span><span class="sxs-lookup"><span data-stu-id="8b513-239">SharePoint pages and the page model</span></span>](SharePoint-pages-and-the-page-model.md)

-  [<span data-ttu-id="8b513-240">Средства разработки и проектирования SharePoint и рекомендации</span><span class="sxs-lookup"><span data-stu-id="8b513-240">SharePoint development and design tools and practices</span></span>](SharePoint-development-and-design-tools-and-practices.md)