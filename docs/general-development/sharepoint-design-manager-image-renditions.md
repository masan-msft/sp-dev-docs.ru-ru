---
title: Дизайнер SharePoint изображений
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d08a74c0-5674-4f26-8646-11ea1f081c85
ms.openlocfilehash: 046db2d1e8dbee808bbcacbf75516ca21c822313
ms.sourcegitcommit: a3cd408c6878f5b04730287a0a4f81c557653864
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/22/2018
---
# <a name="sharepoint-design-manager-image-renditions"></a><span data-ttu-id="df94e-102">Дизайнер SharePoint изображений</span><span class="sxs-lookup"><span data-stu-id="df94e-102">SharePoint Design Manager image renditions</span></span>
<span data-ttu-id="df94e-p101">Узнайте, как создать представление изображения, как добавить его на страницу и обрезка его. Передача изображения определяет измерения, которые используются для отображения изображений на сайтах публикации SharePoint. Показ изображений позволяют отображать версии по-разному размера изображения на различных страниц на сайте публикации в зависимости от одного источника изображения. Создать представление изображения, необходимо указать ширину и высоту для всех изображений, использующих представление этого изображения. Показ изображений, доступных для каждого изображения, которые отправлены в библиотеке этого семейства веб-сайтов. Например разработчики могут создавать представление изображения для отображения эскизов и другой представление изображения для отображения изображений баннера. Когда изображение добавляется на страницу, автор может указать представление изображения для использования на изображения. Авторы могут также обрезать представление изображения, чтобы указать часть изображения для использования в представление изображения. Размер правильный изображения отображается, когда страница отображена.</span><span class="sxs-lookup"><span data-stu-id="df94e-p101">Learn how to create an image rendition, how to add it to a page, and how to crop it. An image rendition defines the dimensions that are used to display images in SharePoint publishing sites. Image renditions enable you to display differently sized versions of an image on different pages in a publishing site, based on the same source image. When you create an image rendition, you specify the width and/or height for all images that use that image rendition. The image renditions are available for every image that is uploaded to a library in that site collection. For example, designers can create an image rendition to display thumbnail images and another image rendition to display banner images. When an image is added to a page, the author can specify the image rendition to use on that image. Authors can also crop the image rendition to specify the portion of the image to use in the image rendition. The correct image size is displayed when the page is rendered.</span></span>
  
    
    

<span data-ttu-id="df94e-p102">Показ изображений позволяет отображать один образ несколькими способами. Изображение может отображаться в различных размеров или с помощью различных обрезки. При первом запросе изображение SharePoint Server использует представление указанного изображения для создания образа. Когда пользователь просматривает сайт SharePoint, версию соответствующего размера изображения загружается на клиентский компьютер. Это уменьшает размер файла, который будет загружен в клиент, который позволяет повысить производительность узла.</span><span class="sxs-lookup"><span data-stu-id="df94e-p102">Image renditions enable you to render a single image in multiple ways. An image can be displayed in various sizes or with different cropping. The first time that an image is requested, SharePoint Server uses the specified image rendition to generate the image. When a user views a SharePoint site, the correctly sized version of the image is downloaded to the client computer. This reduces the size of the file that is downloaded to the client, which improves site performance.</span></span>
## <a name="prerequisites-for-managing-image-renditions"></a><span data-ttu-id="df94e-117">Необходимые условия для управления изображений</span><span class="sxs-lookup"><span data-stu-id="df94e-117">Prerequisites for managing image renditions</span></span>
<span data-ttu-id="df94e-118"><a name="Prerequisites"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-118"></span></span>

<span data-ttu-id="df94e-119">Так как изображений имеют зависимости от других функций в SharePoint, убедитесь, что соответствуют предварительным требованиям, в этом разделе, перед выполнением процедур, описанных в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="df94e-119">Because image renditions have dependencies on other features in SharePoint, make sure that you meet the prerequisites in this section before you perform the procedures in this topic.</span></span> <span data-ttu-id="df94e-120">Следующие необходимые компоненты:</span><span class="sxs-lookup"><span data-stu-id="df94e-120">Prerequisites include:</span></span>
  
    
    

- <span data-ttu-id="df94e-p104">**Семейство сайтов публикации** Где добавлении изображений семейства веб-сайтов должен быть создан с помощью портал публикации или шаблон семейства сайтов каталога продуктов. Или компоненты публикации должна быть включена в семействе сайтов, где необходимо использовать изображений. Для получения дополнительных сведений см [Обзор публикации для сайтов Интернета, интрасети и экстрасети](http://technet.microsoft.com/en-us/library/jj635881%28office.15%29.aspx) в библиотеке TechNet.</span><span class="sxs-lookup"><span data-stu-id="df94e-p104">**A publishing site collection** The site collection where you are adding image renditions must have been created by using the Publishing Portal or the Product Catalog site collection template. Or, publishing features must be enabled on the site collection where you want to use image renditions. For more information, see [Overview of publishing to Internet, intranet, and extranet sites](http://technet.microsoft.com/en-us/library/jj635881%28office.15%29.aspx) in the TechNet Library.</span></span>
    
  
- <span data-ttu-id="df94e-p105">**Настройки кэша больших двоичных ОБЪЕКТОВ** Дисковый кэш BLOB-ОБЪЕКТОВ управляет кэширование больших двоичных объектов (BLOB), например, часто используемые изображения, аудио, видео файлы и другие файлы, используемые для отображения веб-страниц, такие как CSS-файлов и JS-файлы. Кэш больших двоичных ОБЪЕКТОВ необходимо включить на каждом интерфейсном веб-сервере, на которых вы собираетесь использовать изображений. Если кэш больших двоичных ОБЪЕКТОВ не включен, всегда используется исходного изображения. Дополнительные сведения можно [настроить параметры кэша для веб-приложения](http://technet.microsoft.com/en-us/library/cc770229.aspx) в библиотеке TechNet.</span><span class="sxs-lookup"><span data-stu-id="df94e-p105">**A configured BLOB cache** The disk-based BLOB cache controls the caching for binary large objects (BLOBs), such as frequently used image, audio, and video files, and other files that are used to display webpages, such as .css files and .js files. The BLOB cache must be enabled on each front-end web server where you want to use image renditions. If the BLOB cache is not enabled, the original image is always used. For more information, see [Configure cache settings for a Web application](http://technet.microsoft.com/en-us/library/cc770229.aspx) in the TechNet Library.</span></span>
    
  
- <span data-ttu-id="df94e-p106">**Библиотеки активов (рекомендуется)** Шаблон библиотеки активов можно использовать для настройки в библиотеке, которая позволяет легко хранить, упорядочивать и находить мультимедийными ресурсами, такие как изображения, аудио или видео файлов. Дополнительные сведения можно [настроить библиотеки активов для хранения файлов изображений, аудио или видео](http://office.microsoft.com/en-us/sharepoint-server-help/set-up-an-asset-library-to-store-image-audio-or-video-files-HA102785730.aspx) на сайте Office.com.</span><span class="sxs-lookup"><span data-stu-id="df94e-p106">**An asset library (recommended)** You can use the Asset Library template to set up a library that makes it easy to store, organize, and find rich media assets, such as image, audio, or video files. For more information, see [Set up an Asset Library to store image, audio, or video files](http://office.microsoft.com/en-us/sharepoint-server-help/set-up-an-asset-library-to-store-image-audio-or-video-files-HA102785730.aspx) on Office.com.</span></span>
    
  

## <a name="create-an-image-rendition"></a><span data-ttu-id="df94e-130">Создать представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-130">Create an image rendition</span></span>
<span data-ttu-id="df94e-131"><a name="Create"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-131"></span></span>

<span data-ttu-id="df94e-132">При создании представление изображения SharePoint создается уникальный идентификатор, определяющий представление этого изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-132">When an image rendition is created, SharePoint creates a unique ID that identifies that image rendition.</span></span> <span data-ttu-id="df94e-133">Изображение появляется, когда SharePoint Server сначала получает запрос на представление изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-133">An image is generated when SharePoint Server first receives a request for the image rendition.</span></span>
  
    
    

### <a name="to-create-an-image-rendition"></a><span data-ttu-id="df94e-134">Чтобы создать представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-134">To create an image rendition</span></span>


1. <span data-ttu-id="df94e-135">Проверьте, что учетная запись пользователя, выполняющая эту процедуру, имеет разрешения как минимум на сайт верхнего уровня семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="df94e-135">Verify that the user account that is performing this procedure has, at minimum, Design permissions to the top-level site of the site collection.</span></span>
    
  
2. <span data-ttu-id="df94e-136">В браузере перейдите на сайт верхнего уровня семейства сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="df94e-136">In a browser, go to the top-level site of the publishing site collection.</span></span>
    
  
3. <span data-ttu-id="df94e-p108">Щелкните значок **Параметры**. На странице " **Параметры узла** " в разделе **внешний вид и функции** выберите **Изображений**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p108">Choose the **Settings** icon. On the **Site Settings** page, in the **Look and Feel** section, choose **Image Renditions**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-p109">[!Примечание] Страница изображений можно также открыть с по умолчанию домашней страницы сайта публикации. В разделе **я Visual Designer** выберите **Настройка изображений**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p109">The Image Renditions page can also be opened from the default home page of the publishing site. In the **I'm the Visual Designer** section, choose **Configure image renditions**.</span></span> 
     

4. <span data-ttu-id="df94e-141">На странице **Представления изображений** выберите пункт **Добавить элемент**.</span><span class="sxs-lookup"><span data-stu-id="df94e-141">On the **Image Renditions** page, choose **Add new item**.</span></span>
    
  
5. <span data-ttu-id="df94e-p110">На странице **Новый представление изображения** в поле **имя** введите имя нового представления. Например введитеThumbnail_Small.</span><span class="sxs-lookup"><span data-stu-id="df94e-p110">On the **New Image Rendition** page, in the **Name** box, enter a name for the rendition. For example, enterThumbnail_Small.</span></span>
    
  
6. <span data-ttu-id="df94e-144">В текстовых полях **Ширина** и **Высота** укажите значения ширины и высоты представления в пикселях, а затем нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-144">In the **Width** and **Height** text boxes, enter the width and height, in pixels, of the rendition, and then choose **Save**.</span></span>
    
  

## <a name="edit-an-image-rendition"></a><span data-ttu-id="df94e-145">Изменить представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-145">Edit an image rendition</span></span>
<span data-ttu-id="df94e-146"><a name="Edit"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-146"></span></span>

<span data-ttu-id="df94e-p111">При редактировании представление изображения нового измерения вступили в силу во время следующего запрошенного изображения. Если изображения, который был создан ранее представление изображения, изображение повторно с помощью нового измерения во время следующего запрошенного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p111">When an image rendition is edited, the new dimensions take effect the next time that the image is requested. If there is an image that was generated previously from the image rendition, the image is regenerated with the new dimensions the next time that the image is requested.</span></span>
  
    
    

### <a name="to-edit-an-image-rendition"></a><span data-ttu-id="df94e-149">Чтобы изменить представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-149">To edit an image rendition</span></span>


1. <span data-ttu-id="df94e-150">Проверьте, что учетная запись пользователя, выполняющая эту процедуру, имеет разрешения как минимум на сайт верхнего уровня семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="df94e-150">Verify that the user account that is performing this procedure has, at minimum, Design permissions to the top-level site of the site collection.</span></span>
    
  
2. <span data-ttu-id="df94e-151">В браузере перейдите на сайт верхнего уровня семейства сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="df94e-151">In a browser, go to the top-level site of the publishing site collection.</span></span>
    
  
3. <span data-ttu-id="df94e-p112">Щелкните значок **Параметры**. На странице " **Параметры узла** " в разделе **внешний вид и функции** выберите **Изображений**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p112">Choose the **Settings** icon. On the **Site Settings** page, in the **Look and Feel** section, choose **Image Renditions**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-p113">[!Примечание] Страница **Изображений** можно также открыть с по умолчанию домашней страницы сайта публикации. В разделе **я Visual Designer** выберите **Настройка изображений**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p113">The **Image Renditions** page can also be opened from the default home page of the publishing site. In the **I'm the Visual Designer** section, choose **Configure image renditions**.</span></span> 

4. <span data-ttu-id="df94e-156">На странице **Изображений** выберите представление изображения, который требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="df94e-156">On the **Image Renditions** page, choose the image rendition that you want to edit.</span></span>
    
  
5. <span data-ttu-id="df94e-157">На странице **Изменить представление изображения** измените имя, ширину или высоту представление изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-157">On the **Edit Image Rendition** page, modify the name, width, or height of the image rendition.</span></span>

     > [!NOTE]
  > <span data-ttu-id="df94e-158">Чтобы использовать же представление изображения на всех веб-сайтов в пределах одного семейства сайтов, перейдите к файлу изображения непосредственно и изменение представления из него.</span><span class="sxs-lookup"><span data-stu-id="df94e-158">To use the same image rendition on all webs within the same site collection, go to the image file directly and edit renditions from there.</span></span> 

## <a name="add-an-image-rendition"></a><span data-ttu-id="df94e-159">Добавьте представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-159">Add an image rendition</span></span>
<span data-ttu-id="df94e-160"><a name="Add"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-160"></span></span>

<span data-ttu-id="df94e-p114">При добавлении изображения на страницу на сайте публикации SharePoint, можно указать представление изображения для этого изображения. При отображении страницы в браузере отображается правильное изображение размером. Можно указать представление изображения в редактор форматированного текста, в элементе управления поля изображения или в URL-адрес изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p114">When you add an image to a page in a SharePoint publishing site, you can specify the image rendition to use for that image. When the page is rendered in a browser, the correct image size is displayed. You can specify the image rendition in the Rich Text Editor, in an image field control, or in the image URL.</span></span>
  
    
    

### <a name="specify-the-image-rendition-by-using-the-rich-text-editor"></a><span data-ttu-id="df94e-164">Укажите представление изображения с помощью редактора форматированного текста</span><span class="sxs-lookup"><span data-stu-id="df94e-164">Specify the image rendition by using the Rich Text Editor</span></span>

<span data-ttu-id="df94e-p115">При вставке изображения на странице, можно указать представление изображения для использования, чтобы размер правильный изображения отображается, когда страница отображена. Можно указать представление изображения в редактор форматированного текста только для изображений, которые хранятся в одном семействе сайтов, как страницы, которая сейчас изменяется.</span><span class="sxs-lookup"><span data-stu-id="df94e-p115">When an image is inserted in a page, you can specify the image rendition to use so that the correct image size is displayed when the page is rendered. You can specify the image rendition in the Rich Text Editor only for images that are stored in the same site collection as the page that is being edited.</span></span>
  
    
    

### <a name="to-specify-an-image-rendition-by-using-the-rich-text-editor"></a><span data-ttu-id="df94e-167">Чтобы задать представление изображения с помощью редактора форматированного текста</span><span class="sxs-lookup"><span data-stu-id="df94e-167">To specify an image rendition by using the Rich Text Editor</span></span>


1. <span data-ttu-id="df94e-168">На вкладке **Страница** нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-168">On the **Page** tab, choose **Edit**.</span></span>
    
  
2. <span data-ttu-id="df94e-169">Выберите значок **Параметры** и нажмите кнопку **Добавить страницу**.</span><span class="sxs-lookup"><span data-stu-id="df94e-169">Choose the **Settings** icon, and then choose **Add a page**.</span></span>
    
  
3. <span data-ttu-id="df94e-170">В окне **"Добавление"** введите имя для этой страницы и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="df94e-170">In the **Add a page** window, enter a name for the page, and then choose **Create**.</span></span>
    
  
4. <span data-ttu-id="df94e-171">Установите указатель мыши в поле **Содержимого страницы**.</span><span class="sxs-lookup"><span data-stu-id="df94e-171">Place the pointer in the **Page Content** field.</span></span>
    
  
5. <span data-ttu-id="df94e-172">На вкладке **Вставка** выберите **изображение** и выберите **Из SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="df94e-172">On the **Insert** tab, choose **Picture**, and then choose **From SharePoint**.</span></span>
    
  
6. <span data-ttu-id="df94e-p116">Найдите изображения, которое нужно добавить на страницу, выберите изображение и нажмите кнопку **Вставить**. Изображение будет отображаться в полный размер.</span><span class="sxs-lookup"><span data-stu-id="df94e-p116">Locate the image that you want to add to the page, select the image, and then choose **Insert**. The image will be displayed at full size.</span></span>
    
  
7. <span data-ttu-id="df94e-p117">На вкладке **Конструктор** в группе **выберите** нажмите кнопку **Выбрать представления** и выберите представление изображения. Изображение будет отображаться в зависимости от размера, заданного для представление изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p117">On the **Design** tab, in the **Select** group, choose **Pick Rendition**, and then select an image rendition. The image will display according to the size specified for the image rendition.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-177">[!Примечание] Команда **Выберите вариант** доступен только для изображений, которые хранятся в одном семействе сайтов, как страницы, которая сейчас изменяется.</span><span class="sxs-lookup"><span data-stu-id="df94e-177">The **Pick Rendition** command is available only for images that are stored in the same site collection as the page that is being edited.</span></span>

8. <span data-ttu-id="df94e-178">Если нужно обрезать представление изображения, выберите **Выбрать представление** и выберите **Изменение представления**.</span><span class="sxs-lookup"><span data-stu-id="df94e-178">If you want to crop the image rendition, choose **Pick Rendition**, and then choose **Edit Renditions**.</span></span>
    
    <span data-ttu-id="df94e-179">Дополнительные сведения о кадрирование изображений разделе  [Обрезка представление изображения](#Crop) в этой статье.</span><span class="sxs-lookup"><span data-stu-id="df94e-179">For more information about cropping image renditions, see the  [Crop an image rendition](#Crop) section of this article.</span></span>
    
  

### <a name="specify-the-image-rendition-in-the-image-url"></a><span data-ttu-id="df94e-180">Укажите представление изображения в URL-адрес изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-180">Specify the image rendition in the image URL</span></span>

<span data-ttu-id="df94e-181">Можно указать представление изображения, добавив параметры RenditionID, ширину или высоту URL-адрес изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-181">You can specify the image rendition by adding the RenditionID, Width, or Height parameters to the image URL.</span></span>
  
    
    
 <span data-ttu-id="df94e-182">**RenditionID** Параметр RenditionID используется для указания идентификатора представление изображения для использования.</span><span class="sxs-lookup"><span data-stu-id="df94e-182">**RenditionID** Use the RenditionID parameter to specify the ID of the image rendition to use.</span></span>
  
    
    
 <span data-ttu-id="df94e-p118">**Ширина** Параметр ширины задать ширину в пикселях представление изображения. SharePoint Server пытается найти представление изображения указанной ширины. Рассмотрим процедуру SharePoint Server пытается найти представление изображения, шириной, размер которого превышает указанный ширины. При наличии нескольких изображений, соответствующие этому критерию, SharePoint Server использует представление изображения с ближайшим ширины для заданного. Если нет представление изображения с шириной, равно или больше, чем указанная ширина используется исходного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p118">**Width** Use the Width parameter to specify the width, in pixels, of the image rendition. SharePoint Server tries to find an image rendition with the specified width. Next, SharePoint Server tries to find an image rendition that has a width that is larger than the specified width. If there are multiple image renditions that match this criterion, SharePoint Server uses the image rendition with the closest width to what was specified. If there is no image rendition with a width that is equal to or larger than the specified width the original image is used.</span></span>
  
    
    
 <span data-ttu-id="df94e-p119">**Высота** Параметр высоте укажите высоту в пикселях представление изображения. SharePoint Server пытается найти представление изображения с указанным высоту. Рассмотрим процедуру SharePoint Server пытается найти представление изображения, высота, размер которого превышает указанный высоту. При наличии нескольких изображений, соответствующие этому критерию, SharePoint Server использует представление изображения с ближайшим высоту для заданного. Если нет представление изображения с высоту, равно или больше, чем указанная высота используется исходного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p119">**Height** Use the Height parameter to specify the height, in pixels, of the image rendition. SharePoint Server tries to find an image rendition with the specified height. Next, SharePoint Server tries to find an image rendition that has a height that is larger than the specified height. If there are multiple image renditions that match this criterion, SharePoint Server uses the image rendition with the closest height to what was specified. If there is no image rendition with a height that is equal to or larger than the specified height the original image is used.</span></span>
  
    
    
 <span data-ttu-id="df94e-p120">**Ширину и высоту** Если указан параметр ширину и высоту параметр, SharePoint Server пытается найти представление изображения с указанной ширины и высоты. Рассмотрим процедуру SharePoint Server пытается найти представление, ближайшего к указанной отношение ширину и высоту. Если имеется несколько соответствий, выбирается представление изображения, который имеет ближайшего большего соотношение ширину и высоту до требуемого размера.</span><span class="sxs-lookup"><span data-stu-id="df94e-p120">**Width and Height** If both the Width parameter and the Height parameter are specified, SharePoint Server tries to find an image rendition with the specified width and height. Next, SharePoint Server tries to find a rendition that is closest to the width/height ratio specified. If there are multiple matches, the image rendition that has the closest larger width/height ratio to the requested size is chosen.</span></span>
  
> [!NOTE]
> <span data-ttu-id="df94e-196">[!Примечание] Если URL-адрес изображения включает параметр RenditionID и параметры ширину и высоту, ширину и высоту параметры игнорируются.</span><span class="sxs-lookup"><span data-stu-id="df94e-196">If the image URL includes the RenditionID parameter and Width and Height parameters, the Width and Height parameters are ignored.</span></span> 
  
    
    

<span data-ttu-id="df94e-197">Следующем примере показано, как использовать параметр RenditionID:</span><span class="sxs-lookup"><span data-stu-id="df94e-197">The following example shows how to use the RenditionID parameter:</span></span>
  
    
    



```HTML

<img src="/sites/pub/Assets/Lighthouse.jpg?RenditionID=2" />
```

<span data-ttu-id="df94e-198">Следующем примере показано, как использовать параметры ширину и высоту:</span><span class="sxs-lookup"><span data-stu-id="df94e-198">The following example shows how to use the Width and Height parameters:</span></span>
  
    
    



```HTML
<img src="/sites/pub/Assets/Lighthouse.jpg?Width=400&amp;Height=200" />
```


### <a name="specify-the-image-rendition-in-the-image-field-control"></a><span data-ttu-id="df94e-199">Укажите представление изображения в поле рисунка</span><span class="sxs-lookup"><span data-stu-id="df94e-199">Specify the image rendition in the image field control</span></span>

<span data-ttu-id="df94e-p121">Разработчик может указать представление изображения для использования в поле рисунка. Свойство **RenditionId** используется для определения идентификатора представление изображения. Для получения дополнительных сведений см **RenditionId**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p121">A developer can specify the image rendition to use in the image field control. Use the **RenditionId** property to set the ID of the image rendition. For more information, see **RenditionId**.</span></span>
  
    
    

## <a name="crop-an-image-rendition"></a><span data-ttu-id="df94e-203">Обрезка представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-203">Crop an image rendition</span></span>
<span data-ttu-id="df94e-204"><a name="Crop"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-204"></span></span>

<span data-ttu-id="df94e-p122">По умолчанию представление изображения создается в центре изображения. Можно изменить представление изображения для отдельных изображений, обрезки часть изображения, которое требуется использовать. Например, если фотографию показывает маяком сцены, но представление изображения не отображает весь маяком (см), можно изменить область выбранного изображения для отображения всей маяком (см).</span><span class="sxs-lookup"><span data-stu-id="df94e-p122">By default, an image rendition is generated from the center of the image. You can adjust the image rendition for individual images by cropping the portion of the image that you want to use. For example, if a photo shows a lighthouse scene but the image rendition does not show the whole lighthouse (see Figure 1), you can change the selected image area so that the whole lighthouse is displayed (see Figure 2).</span></span> 
  
    
    

<span data-ttu-id="df94e-208">**На рисунке 1. Представление исходного изображения**</span><span class="sxs-lookup"><span data-stu-id="df94e-208">**Figure 1. Original image rendition**</span></span>

  
    
    

  
    
    
![Представление исходного изображения](../images/ImgRendition_orig.PNG)
  
    
    

<span data-ttu-id="df94e-210">**На рисунке 2. Передача обрезанного изображения**</span><span class="sxs-lookup"><span data-stu-id="df94e-210">**Figure 2. Cropped image rendition**</span></span>

  
    
    

  
    
    
![Представление обрезанного изображения](../images/ImgRendition_crop.PNG)
  
    
    
<span data-ttu-id="df94e-212">Передача изображения можно обрезки в библиотеке активов или на странице, без изменения исходного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-212">An image rendition can be cropped in the asset library or on a page, without changing the original image.</span></span> 
  
    
    
<span data-ttu-id="df94e-213">Показ изображений можно обрезки следующими способами:</span><span class="sxs-lookup"><span data-stu-id="df94e-213">Image renditions can be cropped in the following ways:</span></span>
  
    
    

- <span data-ttu-id="df94e-p123">Разработчики могут обрезать представление изображения в библиотеке активов. К примеру конструктор может потребоваться указать, как оно отображается в представление эскизное изображение.</span><span class="sxs-lookup"><span data-stu-id="df94e-p123">Designers can crop an image rendition in the asset library. For example, a designer may want to specify how an image appears in the thumbnail image rendition.</span></span>
    
  
- <span data-ttu-id="df94e-p124">Авторы можно обрезать представление изображения, когда они вставить изображение на страницу. Это позволяет им настроить внешний вид их страницы. Когда автор обрезает представление изображения, при этом также изменяется представление изображения для этого образа. Любой пользователь, использующий представление этого изображения видит обрезанного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p124">Authors can crop an image rendition when they insert an image into a page. This enables them to customize the look of their page. When an author crops an image rendition, this also changes the image rendition for that image. Anyone who uses that image rendition sees the cropped image.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-p125">[!Примечание] Автор может обрезать представление изображения, только в том случае, если исходное изображение хранится в библиотеке, входящих в семейство сайтов как страницы, которая сейчас изменяется. К примеру в сценарии публикации на нескольких сайтах, автор может обрезать представление изображения, только в том случае, если изображение хранится в одном семействе сайтов, как содержимого каталога. В противном случае представление изображения должны быть обрезанными библиотеки активов</span><span class="sxs-lookup"><span data-stu-id="df94e-p125">An author can crop an image rendition only when the original image is stored in a library that is in the same site collection as the page that is being edited. For example, in cross-site publishing scenarios, an author can crop the image rendition only if the image is stored in the same site collection as the catalog content. Otherwise, the image rendition must be cropped in the asset library.</span></span> 

### <a name="crop-an-image-rendition-in-the-asset-library"></a><span data-ttu-id="df94e-223">Обрезка представление изображения в библиотеки активов.</span><span class="sxs-lookup"><span data-stu-id="df94e-223">Crop an image rendition in the asset library</span></span>

<span data-ttu-id="df94e-224">Разработчики могут обрезать представление изображения в библиотеке активов.</span><span class="sxs-lookup"><span data-stu-id="df94e-224">Designers can crop an image rendition in the asset library.</span></span>
  
    
    

### <a name="to-crop-an-image-rendition-in-the-asset-library"></a><span data-ttu-id="df94e-225">Обрезка представление изображения в библиотеки активов.</span><span class="sxs-lookup"><span data-stu-id="df94e-225">To crop an image rendition in the asset library</span></span>


1. <span data-ttu-id="df94e-226">Убедитесь, что учетная запись пользователя, используемая для выполнения этой процедуры имеет разрешения на запись в библиотеку активов, где находится изображение.</span><span class="sxs-lookup"><span data-stu-id="df94e-226">Verify that the user account that is performing this procedure has Write permissions to the asset library where the image is located.</span></span>
    
  
2. <span data-ttu-id="df94e-227">В браузере перейдите в библиотеку активов.</span><span class="sxs-lookup"><span data-stu-id="df94e-227">In a browser, go to the asset library.</span></span>
    
  
3. <span data-ttu-id="df94e-228">Наведите указатель мыши в правом нижнем углу представления, которого вы хотите изменить, выберите многоточие ****изображения, которое отображается, а затем выберите **Изменить ПРЕДСТАВЛЕНИЙ**.</span><span class="sxs-lookup"><span data-stu-id="df94e-228">Position the pointer in the lower-right corner of the image whose rendition you want to change, select the ellipses ( **...**) that appears, and then choose **EDIT RENDITIONS**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-p126">[!Примечание] Можно также открыть страницу **Изменение представления**, наведите указатель мыши на изображение предварительного просмотра в библиотеки активов, а затем выбрав флажок, который отображается в нижней части изображения предварительного просмотра. На вкладке **Конструктор** выберите **Изменение представления**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p126">You can also open the **Edit Renditions** page by placing the pointer over the preview image in the asset library, and then selecting the check box that appears at the bottom of the preview image. Then, on the **Design** tab, choose **Edit Renditions**.</span></span> 

    <span data-ttu-id="df94e-231">На странице изменения представления отображаются изображения для предварительного просмотра для каждого представление изображения, который определен в коллекции веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="df94e-231">The Edit Renditions page displays a preview image for each image rendition that is defined in the site collection.</span></span>
    
  
4. <span data-ttu-id="df94e-232">Найдите представление изображения, который требуется изменить и затем выберите **щелкните, чтобы изменить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-232">Locate the image rendition that you want to change, and then choose **Click to change**.</span></span>
    
  
5. <span data-ttu-id="df94e-233">В окне **Представления обрезки** используйте средство изображения для выбора часть изображения, которое будет использоваться в представление изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-233">In the **Crop Rendition** window, use the image tool to select the portion of the image that you want to use in the image rendition.</span></span>
    
  
6. <span data-ttu-id="df94e-234">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-234">Choose **Save**.</span></span>
    
  
<span data-ttu-id="df94e-235">Если изображения и редактируемой страницы в одном семействе сайтов, также можно обрезать представление изображения с помощью редактора форматированного текста.</span><span class="sxs-lookup"><span data-stu-id="df94e-235">If the image and the page that is being edited are in the same site collection, you also can crop an image rendition by using the Rich Text Editor.</span></span>
  
    
    

### <a name="crop-an-image-rendition-on-a-page"></a><span data-ttu-id="df94e-236">Обрезка представление изображения на странице</span><span class="sxs-lookup"><span data-stu-id="df94e-236">Crop an image rendition on a page</span></span>

<span data-ttu-id="df94e-p127">Авторы можно обрезать представление изображения, когда они вставить изображение на страницу. Это позволяет им настроить внешний вид их страницы. Когда автор обрезает представление изображения, при этом также изменяется представление изображения для этого образа. Любой пользователь, использующий представление этого изображения видит обрезанного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p127">Authors can crop an image rendition when they insert an image into a page. This enables them to customize the look of their page. When an author crops an image rendition, this also changes the image rendition for that image. Anyone who uses that image rendition sees the cropped image.</span></span>
  
    
    

### <a name="to-crop-an-image-rendition-on-a-page"></a><span data-ttu-id="df94e-241">Обрезка представление изображения на странице</span><span class="sxs-lookup"><span data-stu-id="df94e-241">To crop an image rendition on a page</span></span>


1. <span data-ttu-id="df94e-242">Убедитесь, что учетная запись пользователя, используемая для выполнения этой процедуры имеет разрешения на запись в библиотеку активов, где находится изображение.</span><span class="sxs-lookup"><span data-stu-id="df94e-242">Verify that the user account that is performing this procedure has Write permissions to the asset library where the image is located.</span></span>
    
  
2. <span data-ttu-id="df94e-243">В браузере перейдите на сайт SharePoint, который содержит изображение.</span><span class="sxs-lookup"><span data-stu-id="df94e-243">In a browser, go to the SharePoint site that contains the image.</span></span>
    
  
3. <span data-ttu-id="df94e-244">На вкладке **Страница** нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-244">On the **Page** tab, choose **Edit**.</span></span>
    
  
4. <span data-ttu-id="df94e-245">Выберите изображение, которое нужно обрезать.</span><span class="sxs-lookup"><span data-stu-id="df94e-245">Select the image that you want to crop.</span></span>
    
  
5. <span data-ttu-id="df94e-246">На вкладке **изображение** на ленте в группе **выберите** нажмите кнопку **Выбрать представление** и выберите **Изменение представления**.</span><span class="sxs-lookup"><span data-stu-id="df94e-246">On the **Image** tab of the ribbon, in the **Select** group, choose **Pick Rendition**, and then choose **Edit Renditions**.</span></span>
    
    <span data-ttu-id="df94e-247">На странице **Изменения представления** отображаются изображения для предварительного просмотра для каждого представление изображения, который определен в коллекции веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="df94e-247">The **Edit Renditions** page displays a preview image for each image rendition that is defined in the site collection.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-248">[!Примечание] Команда **Выберите вариант** доступен только для изображений, которые хранятся в одном семействе сайтов, как страницы, которая сейчас изменяется.</span><span class="sxs-lookup"><span data-stu-id="df94e-248">The **Pick Rendition** command is available only for images that are stored in the same site collection as the page that is being edited.</span></span>

6. <span data-ttu-id="df94e-249">Найдите представление изображения, который требуется изменить и затем выберите **щелкните, чтобы изменить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-249">Locate the image rendition that you want to change, and then choose **Click to change**.</span></span>
    
  
7. <span data-ttu-id="df94e-250">В окне **Представления обрезки** используйте средство изображения для выбора часть изображения для использования в представление изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-250">In the **Crop Rendition** window, use the image tool to select the portion of the image to use in the image rendition.</span></span>
    
  
8. <span data-ttu-id="df94e-251">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-251">Choose **Save**.</span></span>
    
  

## <a name="delete-an-image-rendition"></a><span data-ttu-id="df94e-252">Удалить представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-252">Delete an image rendition</span></span>
<span data-ttu-id="df94e-253"><a name="Delete"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-253"></span></span>

<span data-ttu-id="df94e-p128">При удалении представление изображения, передача изображения больше не создаются для изображений. Если сайт запрашивает представление удаленного изображения, возвращается исходного изображения.</span><span class="sxs-lookup"><span data-stu-id="df94e-p128">When an image rendition is deleted, that image rendition is no longer generated for images. If a site requests the deleted image rendition, the original image is returned.</span></span>
  
    
    

### <a name="to-delete-an-image-rendition"></a><span data-ttu-id="df94e-256">Чтобы удалить представление изображения</span><span class="sxs-lookup"><span data-stu-id="df94e-256">To delete an image rendition</span></span>


1. <span data-ttu-id="df94e-257">Проверьте, что учетная запись пользователя, выполняющая эту процедуру, имеет разрешения как минимум на сайт верхнего уровня семейства веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="df94e-257">Verify that the user account that is performing this procedure has, at minimum, Design permissions to the top-level site of the site collection.</span></span>
    
  
2. <span data-ttu-id="df94e-258">В браузере перейдите на сайт верхнего уровня семейства сайтов публикации.</span><span class="sxs-lookup"><span data-stu-id="df94e-258">In a browser, go to the top-level site of the publishing site collection.</span></span>
    
  
3. <span data-ttu-id="df94e-p129">Щелкните значок **Параметры**. На странице " **Параметры узла** " в разделе **внешний вид и функции** выберите **Изображений**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p129">Choose the **Settings** icon. On the **Site Settings** page, in the **Look and Feel** section, choose **Image Renditions**.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="df94e-p130">[!Примечание] Страница **Изображений** можно также открыть с по умолчанию домашней страницы сайта публикации. В разделе **я Visual Designer** выберите **Настройка изображений**.</span><span class="sxs-lookup"><span data-stu-id="df94e-p130">The **Image Renditions** page can also be opened from the default home page of the publishing site. In the **I'm the Visual Designer** section, choose **Configure image renditions**.</span></span> 

4. <span data-ttu-id="df94e-263">На странице **Изображений** найдите представление изображения, который требуется удалить и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="df94e-263">On the **Image Renditions** page, locate the image rendition that you want to delete, and then choose **Delete**.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="df94e-264">См. также</span><span class="sxs-lookup"><span data-stu-id="df94e-264">See also</span></span>
<span data-ttu-id="df94e-265"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="df94e-265"></span></span>

-  [<span data-ttu-id="df94e-266">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="df94e-266">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md) 
-  [<span data-ttu-id="df94e-267">Фирменная символика и конструкция возможности дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="df94e-267">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
-  [<span data-ttu-id="df94e-268">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="df94e-268">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  

