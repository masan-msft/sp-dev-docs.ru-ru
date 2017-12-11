---
title: "Создание минимальной главной страницы в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 634aa471-07e1-41d6-aa80-27f7ef7e9dc8
ms.openlocfilehash: c7554383f757c5f70b87ab7eabd8651272da6275
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="create-a-minimal-master-page-in-sharepoint"></a><span data-ttu-id="0fc91-102">Создание минимальной главной страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0fc91-102">Create a minimal master page in SharePoint</span></span>

<span data-ttu-id="0fc91-103">Минимальная Главная страница содержит только элементы на страницы, которые необходимы для отображения страницы в браузере с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0fc91-103">A minimal master page contains only those page elements that are required by SharePoint to render the page correctly in the browser.</span></span> <span data-ttu-id="0fc91-104">С помощью диспетчера оформления можно быстро создать Минимальная Главная страница без предварительного для разработки и преобразование HTML-файл.</span><span class="sxs-lookup"><span data-stu-id="0fc91-104">With Design Manager, you can quickly create a minimal master page without first having to design and convert an HTML file.</span></span>

## <a name="introduction-to-the-minimal-master-page"></a><span data-ttu-id="0fc91-105">Общие сведения о минимальной главной страницы</span><span class="sxs-lookup"><span data-stu-id="0fc91-105">Introduction to the minimal master page</span></span>
<span data-ttu-id="0fc91-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="0fc91-106"></span></span>

<span data-ttu-id="0fc91-107">С помощью диспетчера оформления можно преобразовать типичного HTML-файла в главную страницу SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0fc91-107">With Design Manager, you can convert a typical HTML file into a SharePoint master page.</span></span> <span data-ttu-id="0fc91-108">Однако, если у вас нет готовых макет, можно по-прежнему быстро начать с нуля путем создания минимальной главной страницы.</span><span class="sxs-lookup"><span data-stu-id="0fc91-108">But, if you don't have a prebuilt mock-up, you can still quickly start from scratch by creating a minimal master page.</span></span> <span data-ttu-id="0fc91-109">Минимальная Главная страница содержит элементы страниц, необходимые SharePoint для отображения страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="0fc91-109">The minimal master page contains only those page elements required by SharePoint to render the page in the browser.</span></span>
  
    
    
<span data-ttu-id="0fc91-110">При создании Минимальная Главная страница дизайнер создает master-файл и соответствующий HTML-файл, чтобы пользователь может работать с HTML-файл, если вы предпочитаете.</span><span class="sxs-lookup"><span data-stu-id="0fc91-110">When you create a minimal master page, Design Manager creates both the .master file and an associated HTML file, so that you can still work with only the HTML file if you prefer.</span></span> <span data-ttu-id="0fc91-111">Работа с Минимальная Главная страница именно то же, что работа с главной страницы, преобразование из HTML-файла.</span><span class="sxs-lookup"><span data-stu-id="0fc91-111">Working with a minimal master page is exactly the same as working with a master page that you convert from an HTML file.</span></span> <span data-ttu-id="0fc91-112">Связаны, таким образом, чтобы каждый раз, когда редактирование и сохранить HTML-файл, эти изменения синхронизируются связанного главную страницу HTML-файл и главные страницы.</span><span class="sxs-lookup"><span data-stu-id="0fc91-112">The HTML file and master page are associated, so that whenever you edit and save the HTML file, those changes are synced to the associated master page.</span></span> <span data-ttu-id="0fc91-113">И HTML-файл содержит особые типы разметки, которые делают синхронизации с master-файл, возможно.</span><span class="sxs-lookup"><span data-stu-id="0fc91-113">And the HTML file contains special types of markup that make syncing with the .master file possible.</span></span> <span data-ttu-id="0fc91-114">Дополнительные сведения об этой связи и эти типы разметки можно [как: преобразование HTML-файла в главную страницу в SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0fc91-114">For more information about this association and these types of markup, see  [How to: Convert an HTML file into a master page in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="0fc91-115">Начиная с Минимальная Главная страница используется при:</span><span class="sxs-lookup"><span data-stu-id="0fc91-115">Starting with a minimal master page is useful when:</span></span>
  
    
    

- <span data-ttu-id="0fc91-116">Необходимо быстро начать с нуля и создают дизайна в HTML-файле, связанном с Минимальная Главная страница вместо начиная с помощью файла HTML макет.</span><span class="sxs-lookup"><span data-stu-id="0fc91-116">You want to start quickly from scratch, and then build out your design in the HTML file that's associated with the minimal master page, instead of starting with a mock-up HTML file.</span></span>
    
  
- <span data-ttu-id="0fc91-p104">Чтобы быстро проверить или прототип элемент проекта, который требует работы главную страницу SharePoint. Например создание Минимальная Главная страница не требуется Подготовка HTML-файла для преобразования или разрешения возникновения ошибок предварительного просмотра, к которым приводят разметка, которая не является допустимым в HTML-файл. Это означает, что сразу же можно работать с предварительной версии на сервере или коллекция фрагментов кода.</span><span class="sxs-lookup"><span data-stu-id="0fc91-p104">You want to rapidly test or prototype a design element that requires a working SharePoint master page. For example, creating a minimal master page does not require preparing an HTML file for conversion or resolving any preview errors that result from markup that is not valid in the HTML file. This means you can immediately work with the server-side preview or the Snippet Gallery.</span></span>
    
  
- <span data-ttu-id="0fc91-p105">Вы хотите поработать непосредственно с master-файл. Если вы разработчик ASP.NET или разработчиков SharePoint, можно создать Минимальная Главная страница, удалить связь между HTML-файл и файл .master, сняв флажок **Связанных файлов** в свойствах HTML-файл и затем работайте непосредственно с файлом .master.</span><span class="sxs-lookup"><span data-stu-id="0fc91-p105">You want to work directly with the .master file. If you're an ASP.NET developer or a SharePoint developer, you can create a minimal master page, remove the association between the HTML file and the .master file by clearing the **Associated File** check box in the properties of the HTML file, and then work directly with the .master file.</span></span>
    
  

## <a name="create-a-minimal-master-page"></a><span data-ttu-id="0fc91-122">Создание Минимальная Главная страница</span><span class="sxs-lookup"><span data-stu-id="0fc91-122">Create a minimal master page</span></span>
<span data-ttu-id="0fc91-123"><a name="CreateMinimalMaster"> </a></span><span class="sxs-lookup"><span data-stu-id="0fc91-123"></span></span>


  
    
    

### <a name="to-create-a-minimal-master-page"></a><span data-ttu-id="0fc91-124">Чтобы создать Минимальная Главная страница</span><span class="sxs-lookup"><span data-stu-id="0fc91-124">To create a minimal master page</span></span>


1. <span data-ttu-id="0fc91-125">Перейдите на сайт публикации.</span><span class="sxs-lookup"><span data-stu-id="0fc91-125">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="0fc91-126">В правом верхнем углу страницы выберите пункт **Параметры**, а затем выберите **Дизайнер**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-126">In the upper-right corner of the page, choose **Settings**, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="0fc91-127">В Дизайнере в левой области панели навигации выберите команду **Изменить главные страницы**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-127">In Design Manager, in the left navigation pane, choose **Edit Master Pages**.</span></span>
    
  
4. <span data-ttu-id="0fc91-128">Выберите команду **Создать минимальной главной страницы**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-128">Choose **Create a minimal master page**.</span></span>
    
  
5. <span data-ttu-id="0fc91-129">В диалоговом окне **Создание главной страницы** введите имя главной страницы и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-129">In the **Create a Master Page** dialog box, enter a name for the master page, and then choose **OK**.</span></span>
    
    <span data-ttu-id="0fc91-130">На этом этапе SharePoint создает master-файл и соответствующий HTML-файл с тем же именем в коллекции главных страниц.</span><span class="sxs-lookup"><span data-stu-id="0fc91-130">At this point, SharePoint creates both a .master file and an associated HTML file with the same name in the Master Page Gallery.</span></span>
    
    <span data-ttu-id="0fc91-131">В диспетчере оформления HTML-файл теперь отображается со **преобразования успешно**, отображается в столбце состояние.</span><span class="sxs-lookup"><span data-stu-id="0fc91-131">In Design Manager, your HTML file now appears with **Conversion successful** displayed in the Status column.</span></span>
    
  
6. <span data-ttu-id="0fc91-132">Щелкните ссылку в столбце состояние для предварительного просмотра в файл.</span><span class="sxs-lookup"><span data-stu-id="0fc91-132">Follow the link in the Status column to preview the file.</span></span>
    
    <span data-ttu-id="0fc91-133">Просмотр страницы  это интерактивный просмотр главной страницы на сервере.</span><span class="sxs-lookup"><span data-stu-id="0fc91-133">The preview page is a live server-side preview of your master page.</span></span>
    
    <span data-ttu-id="0fc91-134">Дополнительные сведения о предварительном просмотре эталонной страницы с различными страницами см. в статье [Инструкции. Изменение страницы предварительного просмотра в компоненте "Дизайнер" SharePoint](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0fc91-134">For more information about previewing the master page with different pages, see  [How to: Change the preview page in SharePoint Design Manager](how-to-change-the-preview-page-in-sharepoint-design-manager.md).</span></span>
    
    <span data-ttu-id="0fc91-135">Предварительный просмотр страницы также содержит ссылку **фрагменты** в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="0fc91-135">The preview page also contains a **Snippets** link in the upper-right corner.</span></span> <span data-ttu-id="0fc91-136">Этой ссылке откроется коллекция фрагментов кода, где можно начать, заменив static или макет элементов управления в данный проект динамических элементов управления SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0fc91-136">This link opens the Snippet Gallery, where you can begin replacing static or mock-up controls in your design with dynamic SharePoint controls.</span></span> <span data-ttu-id="0fc91-137">Дополнительные сведения см. в статье [Фрагменты кода в компоненте "Дизайнер" SharePoint](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="0fc91-137">For more information, see [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
    <span data-ttu-id="0fc91-138">После успешного предварительного просмотра эталонной страницы в HTML-файл будет добавлен тег **\<div\>**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-138">After your master page previews successfully, you will see a **\<div\>** tag that gets added to your HTML file.</span></span> <span data-ttu-id="0fc91-139">Возможно, чтобы увидеть тег **\<div\>**, потребуется прокрутить страницу вниз.</span><span class="sxs-lookup"><span data-stu-id="0fc91-139">You may have to scroll to the bottom of the page to see the **\<div\>** tag.</span></span>
    
    <span data-ttu-id="0fc91-140">Этот тег **\<div\>** является основным блоком контента.</span><span class="sxs-lookup"><span data-stu-id="0fc91-140">This **\<div\>** is the main content block.</span></span> <span data-ttu-id="0fc91-141">Он находится в заполнителе контента с именем **ContentPlaceHolderMain**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-141">It resides inside a content placeholder named **ContentPlaceHolderMain**.</span></span> <span data-ttu-id="0fc91-142">Во время выполнения, когда посетитель просматривает ваш сайт и запрашивает страницу, в этот заполнитель добавляется контент из макета страницы для соответствующей области содержимого.</span><span class="sxs-lookup"><span data-stu-id="0fc91-142">At run time, when a visitor browses your site and requests a page, this content placeholder gets filled with content from a page layout that contains content in a matching content region.</span></span> <span data-ttu-id="0fc91-143">Этот тег **\<div\>** следует поместить там, где должны отображаться макеты страниц на эталонной странице.</span><span class="sxs-lookup"><span data-stu-id="0fc91-143">You should position this **\<div\>** where you want your page layouts to appear on the master page.</span></span>
    
  
7. <span data-ttu-id="0fc91-144">Можно изменить HTML-файл, который находится непосредственно на сервере с помощью редактора HTML могут открывать и редактировать HTML-файл в подключенный диск.</span><span class="sxs-lookup"><span data-stu-id="0fc91-144">You can edit the HTML file that resides directly on the server by using an HTML editor to open and edit the HTML file in a mapped drive.</span></span> <span data-ttu-id="0fc91-145">Каждый раз при сохранении HTML-файл, все изменения синхронизируются связанного файла.</span><span class="sxs-lookup"><span data-stu-id="0fc91-145">Each time you save the HTML file, any changes are synced to the associated .master file.</span></span> <span data-ttu-id="0fc91-146">Дополнительные сведения см. в статье  [Как: сопоставление сетевого диска коллекции главных страниц SharePoint](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="0fc91-146">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
8. <span data-ttu-id="0fc91-p110">Для работы только с master-файл, а не HTML-файл, необходимо разорвать связь между двумя файлами. В диспетчере оформления, на странице "Изменить главную страницу" выберите HTML-файла, откройте меню **Свойства** и затем выберите **Изменить свойства**. На вкладке **Правка** снимите флажок **Связанный файл** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0fc91-p110">To work only with the .master file and not the HTML file, you must break the association between the two files. In Design Manager, on the Edit Master Pages page, select the HTML file, open the **Properties** menu, and then choose **Edit Properties**. On the **Edit** tab, clear the **Associated File** check box, and then choose **Save**.</span></span>
    
    <span data-ttu-id="0fc91-p111">Нарушение связи позволяет работать непосредственно с master-файл и сохранить изменения без необходимости их перезаписанного все изменения, внесенные в HTML-файл. Можно восстановить этой связи в любое время. Если восстановить связь, соответствующий HTML-файл синхронизации master-файл и заменить его.</span><span class="sxs-lookup"><span data-stu-id="0fc91-p111">Breaking the association enables you to work directly with the .master file and save changes without having them overwritten by any changes made to the HTML file. You can restore this association at any time. If you restore the association, the associated HTML file will sync to the .master file and overwrite it.</span></span>
    
  

## <a name="understand-the-associated-html-file"></a><span data-ttu-id="0fc91-153">Понять, соответствующий HTML-файл</span><span class="sxs-lookup"><span data-stu-id="0fc91-153">Understand the associated HTML file</span></span>
<span data-ttu-id="0fc91-154"><a name="UnderstandHTML"> </a></span><span class="sxs-lookup"><span data-stu-id="0fc91-154"></span></span>

<span data-ttu-id="0fc91-155">При создании Минимальная Главная страница создается HTML-файла, связанного с master-файл, и этот HTML-файл содержит большой объем разметки, относящиеся к работе с SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0fc91-155">When you create a minimal master page, an HTML file is created that's associated with the .master file, and this HTML file contains many lines of markup that are specific to how SharePoint works.</span></span> <span data-ttu-id="0fc91-156">Большая часть этой разметкой можно игнорировать и большая часть его не отображается в последнем разметки веб-узла источника просмотра в браузере, но эта разметка крайне важна для синхронизации изменений из HTML-файла для файла, SharePoint использует.</span><span class="sxs-lookup"><span data-stu-id="0fc91-156">You can safely ignore most of this markup, and most of it does not appear in the final markup of your site when you view source in the browser, but this markup is critical for syncing changes from the HTML file to the .master file that SharePoint actually uses.</span></span> <span data-ttu-id="0fc91-157">Каждый раз, когда сохранить изменения в HTML-файле, эта разметка SharePoint позволяет этого же изменение в следует обратить внимание на связанный master-файл в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="0fc91-157">Each time you save a change to your HTML file, this SharePoint markup makes it possible for that same change to be made to the associated .master file in the background.</span></span> <span data-ttu-id="0fc91-158">Для получения дополнительных сведений см образцы разметки в [как: преобразование HTML-файла в главную страницу в SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="0fc91-158">For more information, see the markup samples in  [How to: Convert an HTML file into a master page in SharePoint](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="0fc91-159">См. также</span><span class="sxs-lookup"><span data-stu-id="0fc91-159">See also</span></span>
<span data-ttu-id="0fc91-160"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="0fc91-160"></span></span>


-  [<span data-ttu-id="0fc91-161">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0fc91-161">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0fc91-162">Инструкции. Создание макета страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0fc91-162">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0fc91-163">Инструкции. Преобразование HTML-файла в эталонную страницу SharePoint</span><span class="sxs-lookup"><span data-stu-id="0fc91-163">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0fc91-164">Фрагменты кода дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="0fc91-164">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

