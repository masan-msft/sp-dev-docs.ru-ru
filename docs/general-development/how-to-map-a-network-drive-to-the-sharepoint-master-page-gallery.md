---
title: "Сопоставление сетевого диска коллекции SharePoint главных страниц"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7d416f6e-2471-4d03-97ae-4e8d907784c6
ms.openlocfilehash: 39067623f653eec5764652255590ab5edf7e3741
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery"></a><span data-ttu-id="8fb35-102">Как: сопоставление сетевого диска коллекции SharePoint главных страниц</span><span class="sxs-lookup"><span data-stu-id="8fb35-102">How to: Map a network drive to the SharePoint Master Page Gallery</span></span>
<span data-ttu-id="8fb35-103">Узнайте, как сопоставление сетевого диска коллекции главных страниц, чтобы руководитель проекта можно использовать для передачи файлов разработки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8fb35-103">Learn how to map a network drive to the Master Page Gallery so that you can use Design Manager to upload design files in SharePoint.</span></span>
<span data-ttu-id="8fb35-104">Можно создать визуальный дизайн веб-сайта с помощью любого средств веб-разработки или редактора HTML и затем использовать Дизайнер для импорта разработки в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8fb35-104">You can create a visual design for your website by using any web design tool or HTML editor, and then use Design Manager to import the design into SharePoint.</span></span> <span data-ttu-id="8fb35-105">Для этого необходимо убедитесь в том, что средство разработки сохраняет его файлы в веб-узла Коллекция главных страниц, являющийся, где ожидает найти файлы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8fb35-105">To do this, you have to make sure that the design tool stores its files in your site's Master Page Gallery, which is where SharePoint expects to find the files.</span></span> <span data-ttu-id="8fb35-106">Мы рекомендуем сопоставление сетевого диска коллекции главных страниц для упрощения сохранять файлы в нужное место.</span><span class="sxs-lookup"><span data-stu-id="8fb35-106">We recommend that you map a network drive to the Master Page Gallery to make it easier to save files in the correct location.</span></span>
  
    
    

<span data-ttu-id="8fb35-107">Во-первых поиск расположения коллекции главных страниц.</span><span class="sxs-lookup"><span data-stu-id="8fb35-107">First, find the location of the Master Page Gallery.</span></span>
### <a name="to-find-the-location-of-the-master-page-gallery"></a><span data-ttu-id="8fb35-108">Чтобы найти расположение коллекции главных страниц</span><span class="sxs-lookup"><span data-stu-id="8fb35-108">To find the location of the Master Page Gallery</span></span>


1. <span data-ttu-id="8fb35-p102">На сайте, для которого Создание проекта запустите диспетчер структуры. (Например, в меню **Параметры** выберите **Дизайнер**.)</span><span class="sxs-lookup"><span data-stu-id="8fb35-p102">On the site for which you are creating a design, start Design Manager. (For example, on the **Settings** menu, choose **Design Manager**.)</span></span>
    
    > <span data-ttu-id="8fb35-111">**Важные:** Если сайт размещен в SharePoint Online, при входе на сайт, используя свои учетные данные Office 365, убедитесь в том, что вы установите флажок **оставаться в системе** .</span><span class="sxs-lookup"><span data-stu-id="8fb35-111">**Important:** If your site is hosted in SharePoint Online, when you sign in to the site by using your Office 365 credentials, make sure that you select the **Keep me signed in** check box.</span></span> <span data-ttu-id="8fb35-112">Дополнительные сведения можно [настроить, а также для устранения неполадок сетевых дисков, подключиться к сайтам SharePoint Online в Office 365 для предприятий](http://support.microsoft.com/kb/2616712).</span><span class="sxs-lookup"><span data-stu-id="8fb35-112">For more information, see [How to configure and to troubleshoot mapped network drives that connect to SharePoint Online sites in Office 365 for enterprises](http://support.microsoft.com/kb/2616712).</span></span> 
2. <span data-ttu-id="8fb35-113">В маркированном списке выберите **Отправить файлов проекта**.</span><span class="sxs-lookup"><span data-stu-id="8fb35-113">In the numbered list, select **Upload Design Files**.</span></span>
    
  
3. <span data-ttu-id="8fb35-p104">Дизайнер: отправить файлы разработки страница содержит расположение коллекции главных страниц. Расположение, вероятно, заканчивается на  `/_catalogs/masterpage/`. Это расположение, к которому будет сопоставление сетевого диска.</span><span class="sxs-lookup"><span data-stu-id="8fb35-p104">The Design Manager: Upload Design Files page contains the location of the Master Page Gallery. The location probably ends in  `/_catalogs/masterpage/`. This is the location to which you will map a network drive.</span></span>
    
  
4. <span data-ttu-id="8fb35-117">Запишите расположение коллекции главных страниц или скопируйте его в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="8fb35-117">Make a note of the location of the Master Page Gallery, or copy it to the Clipboard.</span></span>
    
  
<span data-ttu-id="8fb35-p105">На компьютере, работающего под управлением средства разработки или редактора HTML в расположение, скопированный сопоставление сетевого диска. Сопоставление сетевого диска процедура отличается в зависимости от операционной системы:</span><span class="sxs-lookup"><span data-stu-id="8fb35-p105">On the computer that runs your design tool or HTML editor, map a network drive to the location that you just copied. The procedure for mapping a network drive differs depending on the computer's operating system:</span></span>
- <span data-ttu-id="8fb35-120">Если компьютер работает под управлением Windows 8, выполните действия, описанные в статье  [Создание ярлыка для сопоставления сетевого диска](http://windows.microsoft.com/en-us/windows-8/create-shortcut-to-map-network-drive)версии Windows 8.</span><span class="sxs-lookup"><span data-stu-id="8fb35-120">If the computer is running Windows 8, follow the steps that are described in the Windows 8 version of the article  [Create a shortcut to (map) a network drive](http://windows.microsoft.com/en-us/windows-8/create-shortcut-to-map-network-drive).</span></span>
    
  
- <span data-ttu-id="8fb35-121">Если компьютер работает под управлением Windows 7, выполните действия, описанные в статье  [Создание ярлыка для сопоставления сетевого диска](http://windows.microsoft.com/en-US/windows7/Create-a-shortcut-to-map-a-network-drive)версии Windows 7.</span><span class="sxs-lookup"><span data-stu-id="8fb35-121">If the computer is running Windows 7, follow the steps that are described in the Windows 7 version of the article  [Create a shortcut to (map) a network drive](http://windows.microsoft.com/en-US/windows7/Create-a-shortcut-to-map-a-network-drive).</span></span>
    
  
- <span data-ttu-id="8fb35-122">Если компьютер работает под управлением Windows Vista, выполните действия, описанные в статье  [Создание ярлыка для сопоставления сетевого диска](http://windows.microsoft.com/en-US/windows-vista/Create-a-shortcut-to-map-a-network-drive)версии .</span><span class="sxs-lookup"><span data-stu-id="8fb35-122">If the computer is running Windows Vista, follow the steps that are described in the version of the article  [Create a shortcut to (map) a network drive](http://windows.microsoft.com/en-US/windows-vista/Create-a-shortcut-to-map-a-network-drive).</span></span>
    
  
- <span data-ttu-id="8fb35-123">Если компьютер работает под управлением Windows XP, выполните действия, описанные в статье  [подключение и отключение сетевого диска в Windows XP](http://support.microsoft.com/kb/308582).</span><span class="sxs-lookup"><span data-stu-id="8fb35-123">If the computer is running Windows XP, follow the steps that are described in the article  [How to connect and disconnect a network drive in Windows XP](http://support.microsoft.com/kb/308582).</span></span>
    
  
- <span data-ttu-id="8fb35-124">***Если компьютер работает под управлением другой операционной системы, следуйте инструкциям для создания ярлыка в новое расположение для этой операционной системы.***</span><span class="sxs-lookup"><span data-stu-id="8fb35-124">***If the computer is running another operating system, follow the instructions for creating a shortcut to a new location for that operating system.***</span></span> <span data-ttu-id="8fb35-125">Может потребоваться задать разные учетные данные для подключения к сайту SharePoint, и может потребоваться указать, что подключение восстановлены при каждом входе в систему компьютера.</span><span class="sxs-lookup"><span data-stu-id="8fb35-125">You might have to provide different credentials for connecting to the SharePoint site, and you might have to specify that the connection be re-established every time that you log on to the computer.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="8fb35-126">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8fb35-126">Additional resources</span></span>
<span data-ttu-id="8fb35-127"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8fb35-127"></span></span>


-  [<span data-ttu-id="8fb35-128">Инструкции. Применение эталонной страницы к сайту в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8fb35-128">How to: Apply a master page to a site in SharePoint</span></span>](how-to-apply-a-master-page-to-a-site-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8fb35-129">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="8fb35-129">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="8fb35-130">Каналы устройств в компоненте "Дизайнер" SharePoint</span><span class="sxs-lookup"><span data-stu-id="8fb35-130">SharePoint Design Manager device channels</span></span>](sharepoint-design-manager-device-channels.md)
    
  
-  [<span data-ttu-id="8fb35-131">Способ: изменение страницы предварительного просмотра в диспетчере оформления SharePoint</span><span class="sxs-lookup"><span data-stu-id="8fb35-131">How to: Change the preview page in SharePoint Design Manager</span></span>](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [<span data-ttu-id="8fb35-132">Дизайнер SharePoint изображений</span><span class="sxs-lookup"><span data-stu-id="8fb35-132">SharePoint Design Manager image renditions</span></span>](sharepoint-design-manager-image-renditions.md)
    
  

