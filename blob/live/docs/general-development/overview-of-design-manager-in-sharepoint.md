---
title: "Обзор Дизайнера в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 29834b3f-3815-4347-91d3-296387663114
ms.openlocfilehash: 253207ef3191f5868cd69b273c5e42c4b54ac410
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="overview-of-design-manager-in-sharepoint"></a><span data-ttu-id="8290a-102">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8290a-102">Overview of Design Manager in SharePoint</span></span>
<span data-ttu-id="8290a-103">Узнайте, как использовать Дизайнер для брендирования сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8290a-103">Get an overview of using Design Manager to brand your SharePoint site.</span></span> <span data-ttu-id="8290a-104">Дизайнер — это компонент, доступный на сайтах публикации как в SharePoint, так и в Office 365.</span><span class="sxs-lookup"><span data-stu-id="8290a-104">Design Manager is a publishing feature that is available in publishing sites in both SharePoint and Office 365.</span></span> 
## <a name="introduction-to-design-manager"></a><span data-ttu-id="8290a-105">Общие сведения о Дизайнере</span><span class="sxs-lookup"><span data-stu-id="8290a-105">Introduction to Design Manager</span></span>
<span data-ttu-id="8290a-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="8290a-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="8290a-107">Если вы хотите, чтобы ваш сайт SharePoint представлял бренд вашей компании и выглядел уникально, создайте собственное оформление с помощью Дизайнера.</span><span class="sxs-lookup"><span data-stu-id="8290a-107">If you want your SharePoint site to represent your organization's brand and not "look like SharePoint," you can create a custom design and use Design Manager to achieve that goal.</span></span> <span data-ttu-id="8290a-108">Дизайнер — это компонент SharePoint, который позволяет создать собственное, выверенное до пикселя оформление, используя знакомые средства веб-дизайна.</span><span class="sxs-lookup"><span data-stu-id="8290a-108">Design Manager is a feature in SharePoint that makes it easier to create a fully customized, pixel-perfect design while using the web-design tools that you're already familiar with.</span></span> <span data-ttu-id="8290a-109">Дизайнер — это компонент, доступный на сайтах публикации как в SharePoint, так и в Office 365.</span><span class="sxs-lookup"><span data-stu-id="8290a-109">Design Manager is a publishing feature that is available in publishing sites in both SharePoint and Office 365.</span></span> 
  
    
    
<span data-ttu-id="8290a-p103">Используя Дизайнер, вы можете спроектировать дизайн веб-сайта с помощью любого средства веб-разработки или HTML-редактора, который вы предпочитаете, применяя только HTML и CSS, после чего дизайн передается в SharePoint. Дизайнер — это главный ресурс и интерфейс, в котором можно управлять всеми аспектами пользовательского дизайна.</span><span class="sxs-lookup"><span data-stu-id="8290a-p103">With Design Manager, you can create a visual design for your website by using whatever web design tool or HTML editor you prefer, using only HTML and CSS, and then upload that design into SharePoint. Design Manager is the central hub and interface where you manage all aspects of a custom design.</span></span>
  
    
    
<span data-ttu-id="8290a-p104">Создание визуального дизайна сайта часто входит в более крупный процесс, в котором участвуют несколько людей или организаций. Обзор задач с более общей точки зрения см. в документе  [Дизайн и фирменная символика в SharePoint](http://go.microsoft.com/fwlink/?LinkId=262838).</span><span class="sxs-lookup"><span data-stu-id="8290a-p104">Creating the visual design of a site often fits into a larger process, in which multiple people or organizations are involved. For a roadmap of the tasks from a larger perspective, see  [Design and branding in SharePoint](http://go.microsoft.com/fwlink/?LinkId=262838)</span></span>
  
    
    
<span data-ttu-id="8290a-114">На высоком уровне дизайнер выполнит следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="8290a-114">At a high level, the designer will perform the following tasks:</span></span>
  
    
    

- <span data-ttu-id="8290a-p105">Изучит основные концепции проектирования SharePoint. Дополнительные сведения см. в статье  [Обзор модели страниц в SharePoint](overview-of-the-sharepoint-page-model.md).</span><span class="sxs-lookup"><span data-stu-id="8290a-p105">Understand core SharePoint design concepts. For more information, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model.md).</span></span>
    
  
- <span data-ttu-id="8290a-p106">Создаст макет дизайна с помощью HTML и CSS. Создание дизайна — основной навык веб-дизайнера, который в этой статье не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="8290a-p106">Create a mock-up of the design in HTML and CSS. Creating the design is a core skill of a web designer, and is not covered in this article.</span></span>
    
  
- <span data-ttu-id="8290a-p107">Реализует дизайн с помощью Дизайнера. В этой статье представлен обзор Дизайнера и описывается его использование для реализации визуального дизайна.</span><span class="sxs-lookup"><span data-stu-id="8290a-p107">Implement the design by using Design Manager. Sections of this article provide an introduction to Design Manager and the process of using Design Manager to implement a visual design.</span></span>
    
 


## <a name="use-design-manager-to-implement-a-design"></a><span data-ttu-id="8290a-121">Использование Дизайнера для оформления сайта</span><span class="sxs-lookup"><span data-stu-id="8290a-121">Use Design Manager to implement a design</span></span>
<span data-ttu-id="8290a-122"><a name="Use"> </a></span><span class="sxs-lookup"><span data-stu-id="8290a-122"><a name="Use"> </a></span></span>

<span data-ttu-id="8290a-p108">Если посмотреть на Дизайнер, вы увидите ряд ссылок с левой стороны, представляющие высокоуровневые задачи, которые необходимо выполнить. В зависимости от дизайна и требований для сайта не все эти задачи потребуется выполнить, при этом они необязательно выполняются в указанном порядке. Тем не менее эта последовательность служит отправной точкой.</span><span class="sxs-lookup"><span data-stu-id="8290a-p108">When you look at Design Manager, you see a series of links on the left side that represent the high-level tasks that you have to perform. Depending on your design and your site's requirements, you may not have to perform all of these tasks, and you don't necessarily have to perform them in this order. Still, this sequence is a useful starting point.</span></span>
  
    
    

### <a name="before-you-begin"></a><span data-ttu-id="8290a-126">Подготовка к работе</span><span class="sxs-lookup"><span data-stu-id="8290a-126">Before you begin</span></span>

<span data-ttu-id="8290a-p109">Прежде чем использовать Дизайнер, необходим дизайн. Вы можете создать собственный или использовать готовый шаблон веб-сайта. "Дизайн" — это просто группа файлов, которые реализуют дизайн сайта, например:</span><span class="sxs-lookup"><span data-stu-id="8290a-p109">Before you can use Design Manager, you need a design. You can create your own, or use a ready-made website template. A "design" is simply a group of files that implement the visual design of your site, most commonly:</span></span>
  
    
    

- <span data-ttu-id="8290a-130">по крайней мере один HTML-файл, который будет преобразован в главную страницу SharePoint;</span><span class="sxs-lookup"><span data-stu-id="8290a-130">At least one HTML file that will be converted into a SharePoint master page</span></span>
    
  
- <span data-ttu-id="8290a-131">один или несколько CSS-файлов;</span><span class="sxs-lookup"><span data-stu-id="8290a-131">One or more CSS files</span></span>
    
  
- <span data-ttu-id="8290a-132">файлы JavaScript;</span><span class="sxs-lookup"><span data-stu-id="8290a-132">JavaScript files</span></span>
    
  
- <span data-ttu-id="8290a-133">изображения;</span><span class="sxs-lookup"><span data-stu-id="8290a-133">Images</span></span>
    
  
- <span data-ttu-id="8290a-134">другие вспомогательные файлы.</span><span class="sxs-lookup"><span data-stu-id="8290a-134">Other supporting files</span></span>
    
  
<span data-ttu-id="8290a-p110">При создании макета сайта на HTML и CSS вы, скорее всего, получите несколько HTML-файлов, в которых реализуются различные страницы или типы страниц. Помните, что только один из этих файлов будет преобразован в главную страницу (если у не несколько каналов устройства, где у каждого канала есть собственная главная страница — см. следующий раздел). После создания других элементов сайта, например макетов страниц и шаблонов отображения, с помощью Дизайнера можно перенести разметку из HTML-макета в HTML- и CSS-файлы, связанные с макетом страницы или шаблоном отображения.</span><span class="sxs-lookup"><span data-stu-id="8290a-p110">As you mock up your site in HTML and CSS, you will likely have several HTML files that implement designs for how you want different pages or types of pages to appear. Remember that only one of these HTML files will be converted into the master page (unless you have multiple device channels, where each channel has its own master page—see the following section). After you use Design Manager to create other site elements, such as page layouts or display templates, you can transfer markup from your HTML mock-ups to the HTML and CSS files associated with the page layout or display template.</span></span>
  
    
    
<span data-ttu-id="8290a-p111">Прежде чем начать, вам также следует получить необходимые разрешения SharePoint. Чтобы использовать Дизайнер требуется по крайней мере уровень разрешений Дизайнера.</span><span class="sxs-lookup"><span data-stu-id="8290a-p111">Before you begin, you also need the required SharePoint permissions. To use Design Manager, you must have at least the Designer permission level.</span></span>
  
    
    

### <a name="manage-device-channels"></a><span data-ttu-id="8290a-140">Управление каналами устройств</span><span class="sxs-lookup"><span data-stu-id="8290a-140">Manage device channels</span></span>

<span data-ttu-id="8290a-p112">Даже перед проектированием сайта следует учесть, на какие устройства будет ориентирован сайт и каким будет пользовательский интерфейс на каждом устройстве. Например, можно оптимизировать дизайн вашего сайта для определенного класса смартфонов и планшетных ПК.</span><span class="sxs-lookup"><span data-stu-id="8290a-p112">Even before you design your site, you want to consider what devices your site should target and what will be the user experience on each device. For example, you may want to optimize your site's design for a certain class of smart phones or tablets.</span></span>
  
    
    
<span data-ttu-id="8290a-p113">В зависимости от того, какие каналы вы определите, может потребоваться несколько дизайнов, а значит и несколько HTML-файлов, каждый из которых преобразуется в отдельную главную страницу. Кроме того, каждый HTML-файл (и каждая главная страница) может ссылаться на собственный CSS-файл. Перед проектированием сайта каналы устройств следует проанализировать в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="8290a-p113">Depending on what channels you define, you may want several designs, and so several HTML files, where each file gets converted into a separate master page. Also, each HTML file (and so each master page) can reference its own CSS file. Before you design your site, device channels are one of the first things to consider.</span></span>
  
    
    
<span data-ttu-id="8290a-p114">С помощью каналов устройств можно отображать один сайт публикации разными способами, сопоставляя различные дизайны с разными устройствами. У каждого канала может быть собственная главная страница, связанная с таблицей стилей, которая оптимизирована для определенного устройства. Каждый канал указывает подстроки агента пользователя для одного или нескольких устройств, например "ОС Windows Phone". Эти правила определяют, какие устройства включены в каждый канал. Когда посетители просматривают сайт, каждый канал захватывает трафик для заданного устройства или класса устройств, таких как Windows Phone, и посетители видят сайт с дизайном, оптимизированным для их устройства.</span><span class="sxs-lookup"><span data-stu-id="8290a-p114">With device channels, you can render a single publishing site in multiple ways by mapping different designs to different devices. Each channel can have its own master page that links to a style sheet that is optimized for a specific device. Each channel specifies the user agent substrings for one or more devices, such as "Windows Phone OS". These are rules that determine what devices are included in each channel. Then, when visitors browse your site, each channel captures the traffic for its specified device or class of devices, such as Windows phones, and visitors see your site in a design optimized for their specific device.</span></span>
  
    
    
<span data-ttu-id="8290a-p115">Каналы устройств создаются и хранятся в списке SharePoint, в которых учитывается порядок, потому что у каналов устройств также есть рейтинг. Каналы устройств в списке упорядочены сверху вниз, а правила включения обрабатываются в заданном порядке. Это означает, что каналы устройств с наиболее конкретными правилами должны находиться вверху. Например, канал для "Windows Phone 7.0" должен идти перед каналом для "ОС Windows Phone".</span><span class="sxs-lookup"><span data-stu-id="8290a-p115">Device channels are created and stored in a SharePoint list in which order matters, because device channels also have rankings. Device channels in the list are ordered from top to bottom, and the inclusion rules are processed in that order. This means that you want device channels with the most specific rules at the top. For example, a channel targeting "Windows Phone OS 7.0" should precede a channel targeting "Windows Phone OS".</span></span>
  
    
    

### <a name="upload-design-files"></a><span data-ttu-id="8290a-155">Отправка файлов дизайна</span><span class="sxs-lookup"><span data-stu-id="8290a-155">Upload design files</span></span>

<span data-ttu-id="8290a-p116">При создании дизайна можно использовать любой HTML-редактор и работать с файлами локально на вашем компьютере. Но, в конце концов, вам потребуется загрузить эти файлы в коллекцию главных страниц сайта SharePoint, чтобы с помощью Дизайнера преобразовать, изучить и улучшить ваш дизайн.</span><span class="sxs-lookup"><span data-stu-id="8290a-p116">When you create a design, you can use whatever HTML editor you prefer and work with files locally on your computer. But, eventually, you will have to upload those files to the Master Page Gallery of your SharePoint site, so that you can use Design Manager to convert, preview, and polish your design.</span></span>
  
    
    
<span data-ttu-id="8290a-p117">Самый простой способ отправить файлы и продолжить работу с ними  сопоставить диск на вашем компьютере с коллекцией главных страниц сайта SharePoint. При этом папка на компьютере будет сопоставлена с коллекцией главных страниц, а вы сможете работать с файлами, которые находятся на сервере в SharePoint так же, как с локальными файлами.</span><span class="sxs-lookup"><span data-stu-id="8290a-p117">The easiest way to upload and continue to work on design files is to map a drive on your computer to the Master Page Gallery of your SharePoint site. This connects a folder on your computer to the Master Page Gallery, so that you can work on files that reside on the server in SharePoint as if they were local files.</span></span>
  
    
    
<span data-ttu-id="8290a-p118">После подключения сетевого диска вы сможете отправить дизайн в SharePoint, просто копируя файлы дизайна в папку на сопоставленном диске компьютера, подключенного к SharePoint. После преобразования HTML-файла в главную страницу SharePoint, создания макетов страниц и шаблонов отображения, с которыми связан соответствующий HTML-файл, вы можете продолжить редактировать связанные HTML-файлы в HTML-редакторе на локальном компьютере. Каждый раз при сохранении файла на сопоставленном диске SharePoint автоматически синхронизирует файлы на локальном компьютере с коллекцией главных страниц. Вы можете создать собственную структуру папок на сопоставленном диске. Ее будет поддерживать SharePoint, и она будет показана в коллекции главных страниц. Сохраните все файлы, связанные с одним дизайном, в одной папке, и скопируйте ее на сопоставленный диск, когда вы будете готовы отправить дизайн.</span><span class="sxs-lookup"><span data-stu-id="8290a-p118">After you map a network drive, you can upload your design to SharePoint simply by copying the design files to a folder on the mapped drive of your computer that is connected to SharePoint. After you convert your HTML file to a SharePoint master page, and after you create page layouts and display templates that each have their own associated HTML file, you can continue to edit those associated HTML files in your HTML editor on your computer. Each time you save a file in the mapped drive, SharePoint automatically synchronizes the files on your computer with the Master Page Gallery. You can create your own folder structure on the mapped drive, and that structure is maintained by SharePoint and appears in the Master Page Gallery. You should keep all files related to one design in a single folder, and then copy that folder to the mapped drive when you are ready to upload your design.</span></span>
  
    
    
<span data-ttu-id="8290a-165">Дополнительные сведения см. в статье  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="8290a-165">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    

### <a name="edit-master-pages"></a><span data-ttu-id="8290a-166">Изменение главных страниц</span><span class="sxs-lookup"><span data-stu-id="8290a-166">Edit master pages</span></span>

<span data-ttu-id="8290a-167">Создание главной страницы с фирменной символикой, которая содержит все требуемые функции SharePoint, например элементы навигации и поиска, по сути, состоит из трех этапов:</span><span class="sxs-lookup"><span data-stu-id="8290a-167">Creating a fully branded master page that contains all of the SharePoint functionality that you want, such as navigation and search, is basically a three-step process:</span></span>
  
    
    

1. <span data-ttu-id="8290a-168">преобразование HTML-файла в главную страницу SharePoint;</span><span class="sxs-lookup"><span data-stu-id="8290a-168">Convert an HTML file into a SharePoint master page.</span></span>
    
  
2. <span data-ttu-id="8290a-169">предварительный просмотр главной страницы и устранение ошибок;</span><span class="sxs-lookup"><span data-stu-id="8290a-169">Preview the master page and fix any issues.</span></span>
    
  
3. <span data-ttu-id="8290a-170">добавление фрагментов кода SharePoint на главную страницу.</span><span class="sxs-lookup"><span data-stu-id="8290a-170">Add SharePoint snippets to the master page.</span></span>
    
  
<span data-ttu-id="8290a-171">Каждый из этих трех шагов выполняется на другой странице в Дизайнере.</span><span class="sxs-lookup"><span data-stu-id="8290a-171">Each of these three steps is performed on a different page in Design Manager.</span></span>
  
    
    

#### <a name="convert-an-html-file"></a><span data-ttu-id="8290a-172">Преобразование HTML-файла</span><span class="sxs-lookup"><span data-stu-id="8290a-172">Convert an HTML file</span></span>

<span data-ttu-id="8290a-p119">Основная функция Дизайнера — преобразование HTML-дизайна в главную страницу SharePoint. Для успешного отображения главной страницы SharePoint она должна содержать множество элементов ASP.NET и элементов, относящихся к SharePoint. При преобразовании HTML-файла в главную страницу Дизайнер создает MASTER-файл, содержащий все эти обязательные элементы, поэтому вам не следует о них волноваться. Во время преобразования некоторые элементы HTML-разметки (например, комментарии) также добавляются в исходный HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="8290a-p119">The core feature of Design Manager is that it converts your HTML design into a SharePoint master page. To render successfully, a SharePoint master page must contain many ASP.NET elements and elements that are specific to SharePoint. When you convert an HTML file to a master page, Design Manager creates a .master file that contains all of these required elements, so that you don't have to know about them. During conversion, some HTML markup (such as comments) also gets added to your original HTML file.</span></span>
  
    
    
<span data-ttu-id="8290a-p120">После преобразования HTML-файл и главная страница SharePoint связываются, так что после изменения и сохранения HTML-файла на сопоставленном диске главная страница обновляется автоматически. В Дизайнер у главной HTML-страницы есть свойство с именем **Связанный файл**, который определяет ли, синхронизируются ли изменения в HTML-файле с MASTER-файлом.</span><span class="sxs-lookup"><span data-stu-id="8290a-p120">After the conversion, your HTML file and the SharePoint master page are associated, so that when you edit and save the HTML file in your mapped drive, the master page is updated automatically. In Design Manager, the HTML master page has a property named **Associated File** that determines whether changes to the HTML file are synced to the .master file.</span></span>
  
> [!NOTE]
> <span data-ttu-id="8290a-p121">Дизайнер также позволяет начать дизайн с минимальной главный страницы. В этом случае вам не нужно начинать с HTML, вы можете создать главную HTML-страницу, содержащую минимальные элементы, необходимые для отображения главной страницы в SharePoint, а затем спроектировать свой дизайн, изменив главную HTML-страницу.</span><span class="sxs-lookup"><span data-stu-id="8290a-p121">Design Manager also provides an option to begin your design by using a minimal master page. In this scenario, you don't have to begin with an HTML design; instead, you can create an HTML master page that contains the minimum page elements necessary to render the master page correctly in SharePoint, and then build out your design by editing the HTML master page.</span></span> 
  
    
    


#### <a name="preview-the-master-page"></a><span data-ttu-id="8290a-181">Предварительный просмотр главной страницы</span><span class="sxs-lookup"><span data-stu-id="8290a-181">Preview the master page</span></span>

<span data-ttu-id="8290a-p122">Кроме преобразования главной страницы, Дизайнер позволяет просмотреть ее в том виде, в котором она отображается на сервер (а не так, как она показана в редакторе HTML). Так вы сможете динамически изучить главную страницу и исправить любые проблемы, которые могут помешать ее отрисовке. Например, HTML-файл должен быть XML-совместимым, поэтому необходимо исправить небольшие проблемы с разметкой, например добавить закрывающие теги для всех элементов. Чтобы исправить ошибки, следует отредактировать HTML-файл, сохранить его и обновить страницу на сервере.</span><span class="sxs-lookup"><span data-stu-id="8290a-p122">In addition to converting your master page, Design Manager provides a server-side preview (vs. the design-time preview in your HTML editor), so that you can get a live preview of your master page and fix any issues that might prevent the page from rendering. For example, your HTML file must be XML-compliant, so you may have to fix minor markup issues such as providing closing tags for all elements. To fix any issues, you should edit the HTML file, save it, and then refresh the server-side preview.</span></span>
  
    
    
<span data-ttu-id="8290a-p123">При предварительном просмотре главной страницы можно использовать параметр **Изменить страницу предварительного просмотра** в левом верхнем углу, чтобы просматривать главную страницу вместе с любой существующей страницей или создать новую страницы для предварительного просмотра. В отличие от предварительного просмотра во время проектирования в HTML-редакторе этот серверный режим предварительного просмотра обеспечивает полнофункциональное динамическое отображение страницы, поэтому вы можете отредактировать HTML-файл и сохранить его, чтобы последние изменения синхронизировались со связанным MASTER-файлом. Затем вы обновите страницу на сервере и сможете изучить модификации дизайна в браузере.</span><span class="sxs-lookup"><span data-stu-id="8290a-p123">When you preview a master page, you can use the **Change Preview Page** option in the top-left corner to preview the master page along with any existing page, or create a new page to preview with. Unlike the design-time preview of your HTML master page in an HTML editor, this server-side preview is a fully functional live preview, so you may prefer to edit the HTML file, save it so that the latest changes are synced to the associated .master file, and refresh the live preview and view your latest design changes in the browser.</span></span>
  
    
    

#### <a name="add-snippets"></a><span data-ttu-id="8290a-187">Добавление фрагментов</span><span class="sxs-lookup"><span data-stu-id="8290a-187">Add snippets</span></span>

<span data-ttu-id="8290a-p124">После преобразования главной страницы и ее изучения можно приступить к добавлению фрагментов кода на главную страницу. Фрагмент — это HTML-представление компонента SharePoint, например элемента управления навигацией, поля поиска или веб-части, который можно добавить на главную страницу. Добавление фрагментов на главную страницу — это быстрый способ реализации полного спектра функций SharePoint на главной странице. Добавление фрагментов состоит из трех этапов:</span><span class="sxs-lookup"><span data-stu-id="8290a-p124">After you convert your master page and successfully preview it, you are ready to add snippets to the master page. A snippet is an HTML representation of a SharePoint component—such as a navigation control or search box or Web Part—that you can add to your master page. Adding snippets to your master page is how you quickly build the full range of SharePoint functionality into your master page. Adding snippets is basically a three-step process:</span></span>
  
    
    

1. <span data-ttu-id="8290a-192">поиск фрагментов в коллекции фрагментов и их настройка;</span><span class="sxs-lookup"><span data-stu-id="8290a-192">Find and configure snippets in the Snippet Gallery.</span></span>
    
  
2. <span data-ttu-id="8290a-193">копирование фрагментов на главную HTML-страницу;</span><span class="sxs-lookup"><span data-stu-id="8290a-193">Copy snippets to your HTML master page.</span></span>
    
  
3. <span data-ttu-id="8290a-194">предварительный просмотр и изменение стиля фрагментов с помощью CSS.</span><span class="sxs-lookup"><span data-stu-id="8290a-194">Preview and style snippets by using CSS.</span></span>
    
<span data-ttu-id="8290a-195">Дополнительные сведения см. в статье  [Фрагменты кода дизайнер SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="8290a-195">For more information, see  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  

#### <a name="find-and-configure-snippets-in-the-snippet-gallery"></a><span data-ttu-id="8290a-196">Поиск фрагментов в коллекция фрагментов и их настройка</span><span class="sxs-lookup"><span data-stu-id="8290a-196">Find and configure snippets in the Snippet Gallery</span></span>

<span data-ttu-id="8290a-p125">В коллекции фрагментов вы можете сразу увидеть, какие компоненты доступны для редактируемого типа файла: главной страницы или макета страницы. Выберите фрагмент на ленте. В таблице свойств справа можно настроить свойства этого экземпляра фрагмента. Затем нажмите кнопку **Обновить**, чтобы обновить HTML-фрагмент в левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="8290a-p125">The Snippet Gallery is where you can quickly see which components are available for the type of file you're editing, either master page or page layout. On the ribbon, you select a snippet. In the property grid on the right, you can configure the properties for this instance of a snippet, and then choose **Update** to refresh the HTML snippet on the left.</span></span>
  
    
    

#### <a name="copy-snippets-to-your-html-master-page"></a><span data-ttu-id="8290a-200">Копирование фрагментов на главную HTML-страницу</span><span class="sxs-lookup"><span data-stu-id="8290a-200">Copy snippets to your HTML master page</span></span>

<span data-ttu-id="8290a-p126">После настройки фрагмента скопируйте его в буфер обмена, а затем вставьте его в нужном месте в HTML-файле. HTML-дизайн может уже содержать макет или статические элементы управления, в таком случае вы можете удалить или закомментировать их, заменив их на динамические фрагменты из коллекции фрагментов.</span><span class="sxs-lookup"><span data-stu-id="8290a-p126">After you configure a snippet, you copy it to the Clipboard and then paste it at the right spot in your HTML file. Your HTML design may already contain mockup or static controls, in which case you'll want to delete them or comment them out as you replace them with dynamic snippets from the Snippet Gallery.</span></span>
  
    
    

#### <a name="preview-and-style-snippets-by-using-css"></a><span data-ttu-id="8290a-203">Предварительный просмотр и изменение стиля фрагментов с помощью CSS</span><span class="sxs-lookup"><span data-stu-id="8290a-203">Preview and style snippets by using CSS</span></span>

<span data-ttu-id="8290a-p127">После копирования фрагментов в HTML-файл и сохранения изменений можно обновить главную страницу на сервере, чтобы увидеть, как отображается элемент управления. Фрагменты содержат разметку, которая позволяет просматривать страницу во время разработки в HTML-редакторе, но в серверном режиме предварительного просмотра страница отображается со всеми интерактивными данными, например элемент управления навигацией покажет текущую структуру навигации сайта с динамическими данными из источника данных.</span><span class="sxs-lookup"><span data-stu-id="8290a-p127">After you copy snippets into your HTML file and then save the changes, you can refresh the server-side preview of the master page to see how the control is rendered. Snippets contain markup that provides a design-time preview in an HTML editor, but the server-side preview shows a full-fidelity preview with live data—for example, a navigation control will show the site's current navigation structure with live data from your data source.</span></span>
  
    
    
<span data-ttu-id="8290a-p128">По умолчанию большинство фрагментов наследуют стили из главной таблицы стилей SharePoint, corev15.css. Для задания стиля фрагмента необходимо указать, какие стили применяются к фрагменту, и переопределить с помощью настраиваемой каскадной таблицы стилей (CSS). Для определения этих стилей по умолчанию можно использовать средства браузера, например инструменты разработчика в Internet Explorer. В режиме предварительного просмотра главной страницы на сервере в Internet Explorer нажмите клавишу **F12**, нажмите кнопку **Найти**, а затем выберите параметр **Выбрать элемент щелчком**. После этого вы сможете щелкнуть фрагмент и посмотреть, какие именно стили следует переопределить, добавив CSS в ту или иную таблицу стилей, с которой связана ваша главная страница.</span><span class="sxs-lookup"><span data-stu-id="8290a-p128">By default, most snippets inherit styles from the main SharePoint style sheet, corev15.css. To style a snippet, you have to identify what styles are applied to the snippet and then override them with custom CSS. To identify these default styles, you can use a browser tool such as the developer tools in Internet Explorer. While viewing your master page in the server-side preview in Internet Explorer, press **F12**, choose **Find**, and then choose **Select element by click**. This lets you click the snippet and see exactly what styles to override by adding CSS to whatever custom style sheet your master page links to.</span></span>
  
    
    

### <a name="edit-display-templates"></a><span data-ttu-id="8290a-211">Изменение шаблонов отображения</span><span class="sxs-lookup"><span data-stu-id="8290a-211">Edit display templates</span></span>

<span data-ttu-id="8290a-p129">При использовании локальной установки SharePoint Server вы можете отображать результаты запросов поиска в виде контента на страницах с помощью веб-части поиска контента и других веб-частей на основе поиска. Веб-части на основе поиска используют шаблоны отображения для двух основных целей:</span><span class="sxs-lookup"><span data-stu-id="8290a-p129">If you are using an on-premises installation of SharePoint Server, you can use the Content Search Web Part and other search-driven Web Parts to display the results of search queries as content on your pages. Search-driven Web Parts use display templates for two main purposes:</span></span>
  
    
    

- <span data-ttu-id="8290a-214">для сопоставления управляемых свойств, которые возвращаются в списке результатов, со свойствами, которые будут доступны для JavaScript, включая любой пользовательский код JavaScript, который вы реализуете;</span><span class="sxs-lookup"><span data-stu-id="8290a-214">To map the managed properties that are returned in search-result items to properties that will be available for JavaScript, including whatever custom JavaScript you choose to implement.</span></span>
    
  
- <span data-ttu-id="8290a-215">для показа и настройки стиля отображения этих свойств с помощью HTML и CSS.</span><span class="sxs-lookup"><span data-stu-id="8290a-215">To use HTML and CSS to present and style how those properties are displayed.</span></span>
    
  
<span data-ttu-id="8290a-p130">При работе с главными страницами и макетами страниц вы редактируете связанный HTML-файл, но не MASTER- или ASPX­-файл. Аналогичным образом шаблоны отображения состоят из HTML-файла и связанного JS-файла, при этом редактируется только HTML-файл. При каждом сохранении этого HTML-файла SharePoint автоматически обновляет связанный JS-файл.</span><span class="sxs-lookup"><span data-stu-id="8290a-p130">With master pages and page layouts, you edit an associated HTML file but not the .master file or .aspx file. Similarly, display templates are made of an HTML file and an associated .js file, where you edit only the HTML file. Each time you save that HTML file, SharePoint automatically updates the associated .js file.</span></span>
  
    
    
<span data-ttu-id="8290a-p131">Если вам требуется создать настраиваемый шаблон отображения, скопируйте, а затем измените один из существующих шаблонов отображения. Это полезно, так как шаблоны по умолчанию содержат полезные сведения в комментариях в HTML-файле. Кроме того, вы получите правильную базовую структуру страницы и основу для выполнения основных задач, например сопоставления полей ввода.</span><span class="sxs-lookup"><span data-stu-id="8290a-p131">When you want to create a custom display template, you should begin by copying and then modifying one of the existing display templates. This is helpful because the default display templates contain information in comments in the HTML files, and you'll have the proper basic page structure and a framework in place for basic tasks like mapping input fields.</span></span>
  
    
    

### <a name="edit-page-layouts"></a><span data-ttu-id="8290a-221">Изменение макетов страниц</span><span class="sxs-lookup"><span data-stu-id="8290a-221">Edit page layouts</span></span>

<span data-ttu-id="8290a-p132">Процесс создания макета страницы немного отличается от создания главной страницы. В случае с главной страницей вы начинаете с HTML-дизайна, преобразуете его в главную страницу SharePoint и продолжаете редактировать соответствующий HTML-файл. Но при работе с макетом страницы вы сначала создаете макет в Дизайнере, который формирует ASPX- и HTML-файл, а затем изменяете соответствующий HTML-файл с сопоставленного диска в HTML-редакторе. Дизайнер используется для создания макета страницы, чтобы получить правильный набор полей для макета страницы.</span><span class="sxs-lookup"><span data-stu-id="8290a-p132">The process for creating a page layout is a bit different from that for creating a master page. For a master page, you start with an HTML design, convert that into a SharePoint master page, and then continue to edit the associated HTML file. But for a page layout, you first create the page layout in Design Manager, which creates an .aspx file and an HTML file, and then you edit the associated HTML file from the mapped drive in your HTML editor. The reason you have to use Design Manager to create a page layout is so that the correct set of page fields can get added to the page layout.</span></span>
  
    
    
<span data-ttu-id="8290a-p133">При создании макета страницы вы выбираете главную страницу для предварительного просмотра и выбираете тип контента макета страницы. Тип контента — это схема полей и типов данных, а поля, доступные в типе контента макета страницы, определяют, какие элементы управления полями доступны на макете страницы. Сначала создайте макет страницы в браузере, чтобы затем добавить в него поля.</span><span class="sxs-lookup"><span data-stu-id="8290a-p133">When you create a page layout, you select a master page with which to preview your page layout, and you select a Page Layout Content Type. A content type is a schema of fields and data types, and the fields available in the page layout content type determine what page field controls are available on the page layout that you design. You create a page layout in the browser first so that the page fields can be added.</span></span>
  
    
    
<span data-ttu-id="8290a-229">После создания макета страницы со связанным HTML-файлом, оставшиеся действия аналогичны созданию главной страницы.</span><span class="sxs-lookup"><span data-stu-id="8290a-229">After you create a page layout with its associated HTML file, the remaining steps are the same as for a master page:</span></span>
  
    
    

- <span data-ttu-id="8290a-230">Изучите макет страницы и исправьте ошибки, а затем сохраните HTML-версию.</span><span class="sxs-lookup"><span data-stu-id="8290a-230">Preview the page layout and fix any issues by editing and saving the HTML version.</span></span>
    
  
- <span data-ttu-id="8290a-231">Добавьте фрагменты в макет страницы (настройте, скопируйте, просмотрите и задайте стиль).</span><span class="sxs-lookup"><span data-stu-id="8290a-231">Add snippets to the page layout (configure, copy, preview, style).</span></span>
    
  
<span data-ttu-id="8290a-p134">В коллекции фрагментов доступны различные фрагменты для макетов страниц и главных страниц. На ленте отображаются только фрагменты, связанные с этим типом файла. Например, фрагменты навигации и поля поиска доступны только для главной страницы, а поля страниц доступны только для макета страницы.</span><span class="sxs-lookup"><span data-stu-id="8290a-p134">In the Snippet Gallery, different snippets are available for page layouts and master pages, and the ribbon displays only the snippets that are relevant for that type of file. For example, navigation and search box snippets are available only for a master page, while page fields are available only on a page layout.</span></span>
  
    
    
<span data-ttu-id="8290a-p135">При создании макета страницы базовая задача состоит в размещении и определения стиля полей страницы, которые будут отображать контент, созданный авторами. Стили макета страницы могут находиться в любой из таблицы стилей, с которой связана главная страница. Кроме того, каждый макет страницы может быть связан с собственной таблицей стилей. Если HTML-дизайн содержит контент, который более подходит для макета страницы, а не главной страницы, следует перенести его из главной HTML-­страницы, а затем применить эти стили к нужным элементам управления и элементам соответствующего макета страницы.</span><span class="sxs-lookup"><span data-stu-id="8290a-p135">When you design a page layout, your basic task is to position and style the page field controls that will display content created by content authors. The styles for a page layout can reside in whatever style sheet the master page links to, or each page layout can link to its own specific style sheet. If your HTML design includes content more suitable for a page layout than a master page, you want to transfer that content out of your HTML master page, and then apply those styles to the correct controls and elements of the relevant page layout.</span></span>
  
    
    
<span data-ttu-id="8290a-237">Дополнительные сведения см. в статье  [Инструкции. Создание макета страницы в SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="8290a-237">For more information, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
  
    
    

### <a name="create-themes-and-composed-looks"></a><span data-ttu-id="8290a-238">Создание тем и вариантов оформления</span><span class="sxs-lookup"><span data-stu-id="8290a-238">Create themes and composed looks</span></span>

<span data-ttu-id="8290a-239">В Office 365, но не в локальных средах SharePoint, с помощью Дизайнера можно создавать темы и варианты оформления.</span><span class="sxs-lookup"><span data-stu-id="8290a-239">In the Office 365, but not in on-premises SharePoint installations, Design Manager has the option of creating themes and composed looks.</span></span> <span data-ttu-id="8290a-240">Тема — это набор шрифтов и цветов, которые можно применить к специальному оформлению (то есть к эталонной странице).</span><span class="sxs-lookup"><span data-stu-id="8290a-240">A theme is a set of fonts and colors that can be applied to a custom design (meaning a master page).</span></span> <span data-ttu-id="8290a-241">Темы определяются в XML-файлах, отправляемых в коллекцию тем.</span><span class="sxs-lookup"><span data-stu-id="8290a-241">Themes are defined in .xml files that you upload to the Themes gallery.</span></span> <span data-ttu-id="8290a-242">Если вы хотите, чтобы ваша эталонная страница поддерживала темы, на нее нужно добавить специальную разметку, используемую SharePoint для вставки шрифтов и цветов.</span><span class="sxs-lookup"><span data-stu-id="8290a-242">If you want a custom master page to be theme-able, you need to add special markup to the master page that SharePoint recognizes and uses to insert theme elements such as fonts and colors.</span></span>
  
    
<span data-ttu-id="8290a-243">Вариант оформления — это всего лишь связь между фоновым изображением, темой (шрифтами и цветами) и оформлением (эталонной страницей).</span><span class="sxs-lookup"><span data-stu-id="8290a-243">A composed look is just an association between a background image, a theme (meaning fonts and colors), and a design (meaning a master page).</span></span> <span data-ttu-id="8290a-244">Вариант оформления включает предопределенные элементы дизайна (темы, фоновые изображения и эталонные страницы), которые можно использовать в различных комбинациях.</span><span class="sxs-lookup"><span data-stu-id="8290a-244">A composed look takes predefined design elements—themes, background images, and master pages—and enables them to be used in many different combinations.</span></span>
  
    

### <a name="publish-and-apply-design"></a><span data-ttu-id="8290a-245">Публикация и применение дизайна</span><span class="sxs-lookup"><span data-stu-id="8290a-245">Publish and apply design</span></span>

<span data-ttu-id="8290a-p138">Большинство ресурсов, используемых дизайнов, такие как изображения, HTML-файлы, CSS-файлы и файлы JavaScript, будут храниться в коллекции главных страниц. Коллекция главных страниц — это библиотека документов SharePoint с включенным по умолчанию управлением версиями, которая создает основные и вспомогательные (черновые) версии при каждом изменении файла.</span><span class="sxs-lookup"><span data-stu-id="8290a-p138">Most assets used by your design, such as images, HTML, CSS, and JavaScript files, will reside in the Master Page Gallery. The Master Page Gallery is a SharePoint document library that by default has versioning turned on, which creates major and minor (draft) versions each time you edit a file.</span></span>
  
    
    
<span data-ttu-id="8290a-p139">Перед применением дизайна к сайту сначала необходимо опубликовать основную версию каждого файла или актива, используемого дизайном. При создании сайта в тестовой среде следует отключить управление версиями для коллекции главных страниц, чтобы не публиковать каждый файл перед предварительным просмотром сайта. Но это не рекомендуется, если вы работаете с действующим сайтом.</span><span class="sxs-lookup"><span data-stu-id="8290a-p139">Before you can apply your design to a site, you first have to publish a major version of each file or asset used by your design. If you are designing your site in a test environment, you should turn off versioning for the Master Page Gallery, so that you don't have to remember to publish every file before you preview the site. But this is not a best practice if you are designing on a live site.</span></span>
  
    
    
<span data-ttu-id="8290a-p140">После публикации всех файлов дизайна вы можете применить дизайн, назначив готовые главные страницы сайту. Сайту может быть назначено несколько главных страниц для каждого канала устройств, а на этой странице Дизайнера вы можете применить главную страницу к каналу.</span><span class="sxs-lookup"><span data-stu-id="8290a-p140">After you publish all the design files, you are ready to apply the design by assigning your finished master pages to your site. Each site can have a different master page assigned to each device channel, and this page of Design Manager is where you apply a master page to a channel.</span></span>
  
    
    

### <a name="create-a-design-package"></a><span data-ttu-id="8290a-253">Создание пакета конструктора</span><span class="sxs-lookup"><span data-stu-id="8290a-253">Create a design package</span></span>

<span data-ttu-id="8290a-p141">Пакет конструктора — это простой способ сбора файлов и ресурсов, используемых в дизайне, их экспорта из одного сайта, импорта на другой сайт и применения дизайна к новому сайту. При реализации и улучшении дизайна действующего семейства веб-сайтов с помощью пакета конструктора можно перенести ваш дизайн.</span><span class="sxs-lookup"><span data-stu-id="8290a-p141">A design package is an easy way to collect all the files and assets used by your design, export them from one site, import them into another site, and apply the design to the new site. If you implement and polish your design in a test site collection and want to deploy it in a live site collection, you can use a design package to transfer your design.</span></span>
  
    
    
<span data-ttu-id="8290a-p142">Пакет разработки — это WSP-файл, файл решения SharePoint, который представляет собой специальный тип CAB-файла. При создании или импорте пакета конструктора WSP-файл сохраняется в каталоге решений. После импорта пакета он активируется автоматически. Если главные страницы и макеты страниц были опубликованы до их упаковки и если главные страницы были назначены каналам устройств до упаковки, дизайн автоматически применяется к сайту при развертывании пакета конструктора. В противном случае для применения макета к новому сайту необходимо просто опубликовать файлы дизайна и применить главные страницы к каналам устройства.</span><span class="sxs-lookup"><span data-stu-id="8290a-p142">A design package is a .wsp file, a SharePoint solution file, which is basically a special type of .cab file. When you create or import a design package, the .wsp file is stored in the Solutions gallery. After you import a design package, the package is automatically activated. If the master pages and page layouts were published before they were packaged, and if the master pages were assigned to device channels before they were packaged, the design will be automatically applied to the site when the design package is deployed. Otherwise, to apply the design to the new site, you just have to publish the design files and apply the master pages per device channel.</span></span>
  



## <a name="see-also"></a><span data-ttu-id="8290a-261">См. также</span><span class="sxs-lookup"><span data-stu-id="8290a-261">See also</span></span>
<span data-ttu-id="8290a-262"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="8290a-262"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="8290a-263">Обзор модели страниц в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8290a-263">Overview of the SharePoint page model</span></span>](overview-of-the-sharepoint-page-model.md)
    
  
-  [<span data-ttu-id="8290a-264">Инструкции. Преобразование HTML-файла в эталонную страницу SharePoint</span><span class="sxs-lookup"><span data-stu-id="8290a-264">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8290a-265">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8290a-265">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  

