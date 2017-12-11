---
title: "Обновление пользовательских тем и CSS в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8d1a4e3a-ae6f-41a5-bd80-3398ba541207
ms.openlocfilehash: d0e4096ec6f79eb75a9ff386e0f66a88c234d7ad
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="upgrade-custom-themes-and-css-to-sharepoint"></a><span data-ttu-id="3ffc5-102">Обновление пользовательских тем и CSS в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-102">Upgrade custom themes and CSS to SharePoint</span></span>
<span data-ttu-id="3ffc5-103">Описание обновления проблемы, связанные с тем настроек, например настраиваемых CSS и настраиваемых главных страниц и как обновить настроек для работы в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-103">Learn about upgrade issues with themes customizations, such as custom CSS and custom master pages, and how to update customizations to work in SharePoint.</span></span>
## <a name="introduction-to-themes-customizations-and-upgraded-sharepoint-sites"></a><span data-ttu-id="3ffc5-104">Общие сведения о темах настроек и обновленных сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-104">Introduction to themes customizations and upgraded SharePoint sites</span></span>
<span data-ttu-id="3ffc5-105"><a name="Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffc5-105"></span></span>

<span data-ttu-id="3ffc5-106">Взаимодействие темы в SharePoint была переработана для упрощения процесса настройки сайтов, изменяя макет сайта, цветовой палитры, схемы шрифтов и фонового изображения.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-106">The theming experience in SharePoint was redesigned to simplify the process of customizing sites by changing the site layout, color palette, font scheme, and background image.</span></span> <span data-ttu-id="3ffc5-107">Пользовательский интерфейс тем был изменен и набор новые форматы файлов, связанных с тем.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-107">The themes user interface was redesigned and there is a set of new file formats related to themes.</span></span> <span data-ttu-id="3ffc5-108">Пользовательские темы, которые были созданы в SharePoint 2010 не может использоваться на сайтах SharePoint, необходимо повторно создать их.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-108">Custom themes that were created in SharePoint 2010 cannot be used on SharePoint sites, you must re-create them.</span></span> <span data-ttu-id="3ffc5-109">Настраиваемые CSS-файлы могут не работать успешно на сайтах SharePoint до после обновления для работы с новой главной страницы, цвет слотами и другие изменения темы.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-109">Custom CSS files may not work successfully on SharePoint sites until after they are updated to work with the new master pages, color slots, and other theming changes.</span></span>
  
    
    
<span data-ttu-id="3ffc5-110">В этой статье описываются проблемы, которые могут возникнуть при попытке использовать пользовательских тем SharePoint 2010, SharePoint 2010 CSS и настраиваемых CSS с новой версии интерфейса темы.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-110">This article describes the issues that may occur when you try to use custom SharePoint 2010 themes, SharePoint 2010 CSS, and custom CSS with the new theming experience.</span></span> <span data-ttu-id="3ffc5-111">Здесь также объясняется изменения, которые необходимо внести в пользовательских тем SharePoint 2010, SharePoint 2010 CSS и настраиваемых CSS, если вы хотите использовать их на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-111">It also explains the changes you have to make to your custom SharePoint 2010 themes, SharePoint 2010 CSS, and custom CSS if you want to use them in SharePoint sites.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="3ffc5-112">Темы SharePoint 2010 можно использовать для семейств веб-сайтов, на которых выполняется в режиме 2010.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-112">SharePoint 2010 themes can be used on site collections that are running in 2010 mode.</span></span> <span data-ttu-id="3ffc5-113">Дополнительные сведения о режимах семейств сайтов можно [Планирование обновлений семейств сайтов в SharePoint](http://technet.microsoft.com/en-us/library/ff191199.aspx) или [Планирование обновления для SharePoint](https://technet.microsoft.com/en-us/library/cc303429.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-113">For more information about site collection modes, see  [Plan for site collection upgrades in SharePoint](http://technet.microsoft.com/en-us/library/ff191199.aspx) or [Plan for upgrade to SharePoint](https://technet.microsoft.com/en-us/library/cc303429.aspx).</span></span> 
  
    
    

<span data-ttu-id="3ffc5-114">Дополнительные сведения о темах можно [Общие сведения о темах для SharePoint](themes-overview-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-114">For more information about themes, see  [Themes overview for SharePoint](themes-overview-for-sharepoint.md).</span></span>
  
    
    

## <a name="custom-sharepoint-2010-themes-in-sharepoint"></a><span data-ttu-id="3ffc5-115">Пользовательских тем SharePoint 2010 в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-115">Custom SharePoint 2010 themes in SharePoint</span></span>
<span data-ttu-id="3ffc5-116"><a name="themes"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffc5-116"></span></span>

<span data-ttu-id="3ffc5-117">В SharePoint 2010 тем хранятся в файлах THMX.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-117">In SharePoint 2010, themes were stored in THMX files.</span></span> <span data-ttu-id="3ffc5-118">В SharePoint существует набор новых форматов файлов, связанных с тем.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-118">In SharePoint, there is a set of new file formats related to themes.</span></span> <span data-ttu-id="3ffc5-119">Палитры цветов и схемы шрифтов, хранятся в отдельных XML-файлов (.spcolor и .spfont файлов, соответственно).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-119">Color palettes and font schemes are stored in separate XML files (.spcolor and .spfont files, respectively).</span></span> 
  
    
    
<span data-ttu-id="3ffc5-120">Нельзя обновить файл THMX с SharePoint 2010 для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-120">You cannot upgrade a THMX file from SharePoint 2010 to SharePoint.</span></span> <span data-ttu-id="3ffc5-121">Если применить пользовательскую тему для веб-сайта SharePoint 2010, при обновлении до SharePoint, темы файлы остаются на месте, но темы больше не применяется к сайту и сайта переходит в тему по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-121">If you applied a custom theme to your SharePoint 2010 site, when you upgrade to SharePoint, the theme files remain in place, but the theme is no longer applied to the site, and the site reverts to the default theme.</span></span> <span data-ttu-id="3ffc5-122">Если вы хотите использовать настройки тем SharePoint 2010 на сайтах SharePoint, необходимо повторно создать их с помощью рекомендациями по SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-122">If you want to use your SharePoint 2010 themes customizations on SharePoint sites, you must re-create them using the SharePoint theming guidance.</span></span>
  
    
    
<span data-ttu-id="3ffc5-123">Дополнительные сведения о создании настроек тем можно [как: развернуть пользовательской темы в SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) и [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-123">For more information about creating themes customizations, see  [How to: Deploy a custom theme in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) and [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span> <span data-ttu-id="3ffc5-124">Можно также использовать средство SharePoint цветовой палитры для создания проектов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-124">You can also use the SharePoint color palette tool to help you create SharePoint designs.</span></span> <span data-ttu-id="3ffc5-125">Вы можете [загрузить средство SharePoint цветовой палитры](http://www.microsoft.com/en-us/download/details.aspx?id=38182) из центра загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-125">You can  [ download the SharePoint color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) from the Microsoft Download Center.</span></span>
  
    
    

> <span data-ttu-id="3ffc5-126">**Совет:** Файл THMX можно открыть в приложении PowerPoint узнать цвета, определенные в пользовательской темы, а затем использовать средство цветовой палитры для повторного создания цвета как файла цветовой палитры (.spcolor-файл).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-126">**Tip:** You can open a THMX file in PowerPoint to see how the colors are defined in the custom theme and then use the color palette tool to re-create the colors as a color palette file (an .spcolor file).</span></span> <span data-ttu-id="3ffc5-127">Цветовой палитры — сочетание цвета, используемые на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-127">A color palette is the combination of colors that are used in a SharePoint site.</span></span> 
  
    
    

<span data-ttu-id="3ffc5-128">Можно также использовать один из предустановленной темы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-128">You can also decide to use one of the preinstalled SharePoint themes.</span></span> <span data-ttu-id="3ffc5-129">Дополнительные сведения см. в статье [Выбор темы для сайта публикации](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx?CTT=1).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-129">For more information, see  [Choose a theme for your publishing site](http://office.microsoft.com/en-us/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx?CTT=1) on Office.com.</span></span>
  
    
    

## <a name="upgrading-customized-master-pages"></a><span data-ttu-id="3ffc5-130">Обновление настраиваемых главных страниц</span><span class="sxs-lookup"><span data-stu-id="3ffc5-130">Upgrading customized master pages</span></span>
<span data-ttu-id="3ffc5-131"><a name="MasterPages"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffc5-131"></span></span>

<span data-ttu-id="3ffc5-132">При обновлении сайта SharePoint 2010 для SharePoint, сайт будет настроен на использование главную страницу по умолчанию для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-132">When you upgrade a SharePoint 2010 site to SharePoint, the site is configured to use the default master page for SharePoint.</span></span> <span data-ttu-id="3ffc5-133">Если у вас есть настраиваемой главной страницы сайта SharePoint 2010, по-прежнему находится на сайте и его можно применить к сайту SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-133">If you had a custom master page for your SharePoint 2010 site, it still resides in the site and you can apply it to the SharePoint site.</span></span> <span data-ttu-id="3ffc5-134">Для применения настраиваемой главной страницы к обновленного сайта можно использовать пользовательский интерфейс SharePoint или класс **SPWeb** .</span><span class="sxs-lookup"><span data-stu-id="3ffc5-134">You can use the SharePoint user interface or the **SPWeb** class to apply the custom master page to the upgraded site.</span></span> <span data-ttu-id="3ffc5-135">Дополнительные сведения о том, как изменить главную страницу можно [как: применение главной страницы к сайту SharePoint](how-to-apply-a-master-page-to-a-site-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-135">For more information about how to change the master page, see [How to: Apply a master page to a site in SharePoint](how-to-apply-a-master-page-to-a-site-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="3ffc5-136">Прежде чем применять ли настраиваемой главной страницы SharePoint 2010 к обновленного сайта SharePoint, учтите следующее:</span><span class="sxs-lookup"><span data-stu-id="3ffc5-136">Consider the following before you decide whether to apply the SharePoint 2010 custom master page to the upgraded SharePoint site:</span></span>
  
    
    

- <span data-ttu-id="3ffc5-137">**Если настраиваемой главной страницы зависит от настраиваемого CSS-файлы:** Применение настраиваемой главной страницы для обновленного сайта должен возвращать сайт до его исходного интерфейса 2010.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-137">**If the custom master page depends on custom CSS files:** Applying the custom master page to the upgraded site should return the site to its original 2010 experience.</span></span> <span data-ttu-id="3ffc5-138">Однако нельзя применить тему SharePoint на сайт.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-138">But, you will be unable to apply a SharePoint theme to the site.</span></span>
    
    <span data-ttu-id="3ffc5-139">Если вы хотите использовать пользовательскую главную страницу и файлов CSS вместе с взаимодействием с SharePoint темы, необходимо обновить CSS-файлы для использования нового слотами цвет SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-139">If you want to use the custom master page and custom CSS files together with the SharePoint theming experience, you must update the CSS files to use the new SharePoint color slots.</span></span> <span data-ttu-id="3ffc5-140">Если вы хотите получить доступ к настраиваемой главной страницы из пользовательского интерфейса темы, также необходимо создать файл предварительного просмотра главной страницы.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-140">If you want to access the custom master page from the themes user interface, you also have to create a master page preview file.</span></span> <span data-ttu-id="3ffc5-141">Дополнительные сведения можно [как: создать файл предварительного просмотра главной страницы в SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-141">For more information, see  [How to: Create a master page preview file in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="3ffc5-142">**Если настраиваемой главной страницы зависит от SharePoint 2010 CSS-файлы:** CSS-файлы значительно изменилась от SharePoint 2010 для SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-142">**If the custom master page depends on SharePoint 2010 CSS files:** CSS files have changed significantly from SharePoint 2010 to SharePoint.</span></span> <span data-ttu-id="3ffc5-143">Во многих случаях необходимо переработки на главной странице, чтобы она может работать с новые классы, прежде чем можно успешно применить к обновленного сайта.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-143">In many cases, you will have to rework the master page so that it can work with new classes before you can successfully apply it to the upgraded site.</span></span> <span data-ttu-id="3ffc5-144">Дополнительные сведения о CSS-классов обратитесь к разделу **с помощью CSS хост-сайта в приложениях для SharePoint** в [рекомендации по проектированию пользовательского интерфейса SharePoint надстройки](http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-144">For more information about CSS classes, see the **Using the host web CSS in apps for SharePoint** section in [SharePoint Add-ins UX design guidelines](http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx).</span></span>
    
  

## <a name="sharepoint-2010-css-and-custom-css-files"></a><span data-ttu-id="3ffc5-145">Настраиваемые CSS-файлы и SharePoint 2010 CSS</span><span class="sxs-lookup"><span data-stu-id="3ffc5-145">SharePoint 2010 CSS and custom CSS files</span></span>
<span data-ttu-id="3ffc5-146"><a name="CSS"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffc5-146"></span></span>

<span data-ttu-id="3ffc5-147">Немодифицированного SharePoint 2010 CSS-файлы и настраиваемые CSS-файлы не может использоваться на сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-147">Unmodified SharePoint 2010 CSS files and custom CSS files cannot be used on SharePoint sites.</span></span> <span data-ttu-id="3ffc5-148">Ниже описаны изменения SharePoint, которые применяются к SharePoint 2010 CSS и настраиваемые CSS-файлы.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-148">The following describes SharePoint changes that apply to SharePoint 2010 CSS and custom CSS files:</span></span>
  
    
    

- <span data-ttu-id="3ffc5-149">**Цвет ячейки**.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-149">**Color slots**.</span></span> <span data-ttu-id="3ffc5-150">Существенно увеличена числом разъемов доступные цвета в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-150">The number of available color slots has increased significantly in SharePoint.</span></span> <span data-ttu-id="3ffc5-151">Прежде чем их можно использовать в новой версии интерфейса темы необходимо обновить слотами цвет в SharePoint 2010 CSS-файлы.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-151">You must update the color slots in SharePoint 2010 CSS files before they can be used in the new theming experience.</span></span> <span data-ttu-id="3ffc5-152">Для получения дополнительных сведений обратитесь к разделу [сопоставления разъем цвет](color-palettes-and-fonts-in-sharepoint.md#colorSlots) в [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-152">For more information, see the  [Color slot mapping](color-palettes-and-fonts-in-sharepoint.md#colorSlots) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="3ffc5-153">**Слотами шрифта**.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-153">**Font slots**.</span></span> <span data-ttu-id="3ffc5-154">Следует просмотрите список доступных шрифта слотами и убедитесь, что CSS-файлы, которые вы хотите использовать в SharePoint с помощью слотами правильный шрифт.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-154">You should review the list of available font slots and verify that the CSS files you want to use in SharePoint are using the correct font slots.</span></span> <span data-ttu-id="3ffc5-155">Для получения дополнительных сведений обратитесь к разделу [слотами шрифтов](color-palettes-and-fonts-in-sharepoint.md#fontSlot) в [палитры цветов и шрифтов в SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-155">For more information, see the  [Font slots](color-palettes-and-fonts-in-sharepoint.md#fontSlot) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="3ffc5-156">**Новое примечание**.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-156">**New annotation**.</span></span> <span data-ttu-id="3ffc5-157">SharePoint имеет нового примечания, которая позволяет заменить фонового изображения.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-157">SharePoint has a new annotation that lets you replace the background image.</span></span> <span data-ttu-id="3ffc5-158">Дополнительные сведения можно [как: сделать настраиваемые CSS-файлы тем в SharePoint](how-to-make-custom-css-files-themable-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-158">For more information, see  [How to: Make custom CSS files themable in SharePoint](how-to-make-custom-css-files-themable-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="3ffc5-159">**Новые классы**.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-159">**New classes**.</span></span> <span data-ttu-id="3ffc5-160">Может потребоваться обновить CSS-файлы для работы с новых классов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3ffc5-160">You may have to update CSS files to work with the new classes in SharePoint.</span></span> <span data-ttu-id="3ffc5-161">Дополнительные сведения о CSS-классов (также называется CSS-стили) обратитесь к разделу **с помощью CSS хост-сайта в приложениях для SharePoint** в [рекомендации по проектированию пользовательского интерфейса SharePoint надстройки](http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ffc5-161">For more information about CSS classes (also referred to as CSS styles), see the **Using the host web CSS in apps for SharePoint** section in [SharePoint Add-ins UX design guidelines](http://msdn.microsoft.com/library/a4a8f53c-27d7-43dc-b6db-aa7b1f1c7d45%28Office.15%29.aspx).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="3ffc5-162">См. также</span><span class="sxs-lookup"><span data-stu-id="3ffc5-162">See also</span></span>
<span data-ttu-id="3ffc5-163"><a name="addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="3ffc5-163"></span></span>


-  [<span data-ttu-id="3ffc5-164">Общие сведения о темах для SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-164">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="3ffc5-165">Инструкции. Создание файла предварительного просмотра эталонной страницы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-165">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ffc5-166">Инструкции. Развертывание пользовательской темы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-166">How to: Deploy a custom theme in SharePoint</span></span>](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ffc5-167">Цветовые палитры и шрифты в SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-167">Color palettes and fonts in SharePoint</span></span>](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3ffc5-168">Блог команды разработчиков SharePoint. Свой собственный стиль с помощью тем SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-168">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [<span data-ttu-id="3ffc5-169">Фирменная символика и конструкция возможности дизайнер SharePoint</span><span class="sxs-lookup"><span data-stu-id="3ffc5-169">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

