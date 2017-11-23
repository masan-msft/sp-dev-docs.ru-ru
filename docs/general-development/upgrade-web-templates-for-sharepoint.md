---
title: "Обновление веб-шаблоны для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 69048e4c-6d6d-4e4e-b74c-7c72ae444354
ms.openlocfilehash: cb8e3849b9853d593ce8504814e92066bf08a540
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="upgrade-web-templates-for-sharepoint"></a><span data-ttu-id="ce6c3-102">Обновление веб-шаблоны для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ce6c3-102">Upgrade web templates for SharePoint</span></span>
<span data-ttu-id="ce6c3-103">Сведения об обновлении настраиваемые веб-шаблоны SharePoint 2010 для использования в SharePoint после самостоятельного обновления.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-103">Learn about updating customized SharePoint 2010 web templates for use in SharePoint after a self-service upgrade.</span></span>
<span data-ttu-id="ce6c3-104">SharePoint значительно изменился базовых компонентах, которое используется для отображения внешний вид сайтов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-104">SharePoint has significantly changed the underlying components it uses to render the appearance of SharePoint sites.</span></span> <span data-ttu-id="ce6c3-105">Эти изменения настроек, выполненных для компонентов по умолчанию в SharePoint 2010, включите стилей, макеты страниц, главные страницы и темы.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-105">For customizations made to default components in SharePoint 2010, these new changes include styles, page layouts, master pages and themes.</span></span>
  
    
    

<span data-ttu-id="ce6c3-106">В этой статье представлены рекомендации по обновлению веб-шаблоны, чтобы они работали с новой платформы.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-106">This article provides guidance for updating your web templates so that they work with the new framework.</span></span>
## <a name="possible-behavior-after-a-self-service-site-upgrade"></a><span data-ttu-id="ce6c3-107">Возможные поведение после обновления самостоятельного создания сайтов</span><span class="sxs-lookup"><span data-stu-id="ce6c3-107">Possible behavior after a self-service site upgrade</span></span>

<span data-ttu-id="ce6c3-p102">При обновлении сервера SharePoint 2010 до версии 2013, Администраторы семейства сайтов показаны ссылку, которая позволяет обновлять свои сайты постепенно или обновление всех сайтов в семействе сайтов за один раз. Затем пользователи могут обновления и тестирование этих сайтов, содержащих настройки. Некоторые проблемы, которые пользователи могут возникнуть после обновления include:</span><span class="sxs-lookup"><span data-stu-id="ce6c3-p102">When you upgrade a server from SharePoint 2010 to 2013, site collection administrators are shown a link that lets them upgrade their sites gradually, or upgrade all sites in the site collection at once. Then users can upgrade and test those sites that contain customizations. Some of the problems that users might encounter after an upgrade include:</span></span>
  
    
    

- <span data-ttu-id="ce6c3-111">Фирменный стиль применяется для сайтов было изменено или отсутствует вообще.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-111">Branding applied to sites has been changed, or is missing altogether.</span></span>
    
  
- <span data-ttu-id="ce6c3-112">Настраиваемые компоненты не отображаться правильно.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-112">Custom components don't render correctly.</span></span>
    
  
- <span data-ttu-id="ce6c3-113">Страницы не прорисовывается, а пользователи получают неизвестные ошибки из SharePoint.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-113">Pages don't render at all, and the users receive unknown errors from SharePoint.</span></span>
    
  
- <span data-ttu-id="ce6c3-114">Компоненты, включаемые по умолчанию отключены после обновления.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-114">Features that are enabled by default are disabled after upgrade.</span></span>
    
  

## <a name="recommendations-for-upgrading-sites"></a><span data-ttu-id="ce6c3-115">Рекомендации по обновлению сайтов</span><span class="sxs-lookup"><span data-stu-id="ce6c3-115">Recommendations for upgrading sites</span></span>

<span data-ttu-id="ce6c3-116">При обновлении сайты обычно рекомендуется использовать сайта для проверки установки и тестирования компонентов для обеспечения совместимости и повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-116">When you upgrade sites, we generally recommend that you use the evaluation site to install and test your components for compatibility and performance.</span></span>
  
    
    
<span data-ttu-id="ce6c3-117">В следующих разделах подробно, необходимых для обновления в веб-шаблона.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-117">The following sections detail what you need to update in the web template.</span></span>
  
    
    

### <a name="update-master-page-references"></a><span data-ttu-id="ce6c3-118">Обновление ссылок на главную страницу</span><span class="sxs-lookup"><span data-stu-id="ce6c3-118">Update master page references</span></span>

<span data-ttu-id="ce6c3-119">После обновления для SharePoint ссылки настраиваемой главной страницы, которые содержит веб-шаблон будет иметь значение главную страницу по умолчанию с именем **seattle.master**.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-119">After an upgrade to SharePoint, any custom master page references that your web template contains will be set to the default master page named **seattle.master**.</span></span> <span data-ttu-id="ce6c3-120">Если настройка главную страницу по умолчанию в SharePoint 2010, необходимо изменить ссылку на странице, настраиваемых в порядке для настройки отображаться.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-120">If you customized the default master page in SharePoint 2010, you will need to change the reference to that custom page in order for your customizations to appear.</span></span>
  
    
    

### <a name="update-available-features"></a><span data-ttu-id="ce6c3-121">Доступные возможности обновления</span><span class="sxs-lookup"><span data-stu-id="ce6c3-121">Update available features</span></span>

<span data-ttu-id="ce6c3-122">При обновлении сайта для использования SharePoint веб-шаблоны, функции, которые присоединяются к шаблону по умолчанию, удаляются.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-122">When you upgrade a site to use SharePoint web templates, features that are attached to the template by default are removed.</span></span> <span data-ttu-id="ce6c3-123">Следовательно уменьшается доступные функции обновленных веб-шаблона.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-123">As a consequence, the available functionality of an upgraded web template is reduced.</span></span>
  
    
    
<span data-ttu-id="ce6c3-p105">Чтобы добавить функциональные возможности по умолчанию шаблон, необходимо изменить файл Onet.xml для веб-шаблона, который содержит список компонентов. Чтобы добавить компоненты по умолчанию веб-шаблон, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-p105">To add the default functionality back to the template, you must modify the Onet.xml file for the web template that contains the feature list. To add the default features back to your web template, do the following:</span></span>
  
    
    

### <a name="to-add-default-features-back-to-the-web-template"></a><span data-ttu-id="ce6c3-126">Чтобы добавить по умолчанию компоненты резервного веб-шаблон</span><span class="sxs-lookup"><span data-stu-id="ce6c3-126">To add default features back to the web template</span></span>


1. <span data-ttu-id="ce6c3-127">Откройте проект Visual Studio, который содержит веб-шаблон, который требуется обновить.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-127">Open the Visual Studio project that contains the web template you want to update.</span></span>
    
  
2. <span data-ttu-id="ce6c3-128">В **Обозревателе решений** найдите файл Onet.xml в проекте.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-128">In **Solution Explorer**, find the Onet.xml file in your project.</span></span>
    
  
3. <span data-ttu-id="ce6c3-129">Откройте файл Onet.xml в редакторе XML.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-129">Open Onet.xml in an XML editor.</span></span>
    
  
4. <span data-ttu-id="ce6c3-130">Убедитесь в том, что каждой из функций в таблице 1 содержатся в разделе **WebFeatures**.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-130">Make sure that each of the features in Table 1 are contained in the **WebFeatures** section.</span></span>
    
   <span data-ttu-id="ce6c3-131">**В таблице 1. По умолчанию веб-шаблона функции**</span><span class="sxs-lookup"><span data-stu-id="ce6c3-131">**Table 1. Default web template features**</span></span>


|<span data-ttu-id="ce6c3-132">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="ce6c3-132">**DisplayName**</span></span>|<span data-ttu-id="ce6c3-133">**Код компонента**</span><span class="sxs-lookup"><span data-stu-id="ce6c3-133">**Feature ID**</span></span>|
|:-----|:-----|
|<span data-ttu-id="ce6c3-134">AccSvcAddAccessApp</span><span class="sxs-lookup"><span data-stu-id="ce6c3-134">AccSvcAddAccessApp</span></span>  <br/> |<span data-ttu-id="ce6c3-135">d2b9ec23-526b-42c5-87b6-852bd83e0364</span><span class="sxs-lookup"><span data-stu-id="ce6c3-135">d2b9ec23-526b-42c5-87b6-852bd83e0364</span></span>  <br/> |
|<span data-ttu-id="ce6c3-136">AnnouncementsList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-136">AnnouncementsList</span></span>  <br/> |<span data-ttu-id="ce6c3-137">00BFEA71-D1CE-42de-9C63-A44004CE0104</span><span class="sxs-lookup"><span data-stu-id="ce6c3-137">00bfea71-d1ce-42de-9c63-a44004ce0104</span></span>  <br/> |
|<span data-ttu-id="ce6c3-138">BaseWeb</span><span class="sxs-lookup"><span data-stu-id="ce6c3-138">BaseWeb</span></span>  <br/> |<span data-ttu-id="ce6c3-139">99fe402e-89a0-45aa-9163-85342e865dc8</span><span class="sxs-lookup"><span data-stu-id="ce6c3-139">99fe402e-89a0-45aa-9163-85342e865dc8</span></span>  <br/> |
|<span data-ttu-id="ce6c3-140">BizAppsListTemplates</span><span class="sxs-lookup"><span data-stu-id="ce6c3-140">BizAppsListTemplates</span></span>  <br/> |<span data-ttu-id="ce6c3-141">065c78be-5231-477e-a972-14177cc5b3c7</span><span class="sxs-lookup"><span data-stu-id="ce6c3-141">065c78be-5231-477e-a972-14177cc5b3c7</span></span>  <br/> |
|<span data-ttu-id="ce6c3-142">ContactsList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-142">ContactsList</span></span>  <br/> |<span data-ttu-id="ce6c3-143">00BFEA71-7E6D-4186-9BA8-C047AC750105</span><span class="sxs-lookup"><span data-stu-id="ce6c3-143">00bfea71-7e6d-4186-9ba8-c047ac750105</span></span>  <br/> |
|<span data-ttu-id="ce6c3-144">ContactsList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-144">ContactsList</span></span>  <br/> |<span data-ttu-id="ce6c3-145">00BFEA71-7E6D-4186-9BA8-C047AC750105</span><span class="sxs-lookup"><span data-stu-id="ce6c3-145">00bfea71-7e6d-4186-9ba8-c047ac750105</span></span>  <br/> |
|<span data-ttu-id="ce6c3-146">CustomList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-146">CustomList</span></span>  <br/> |<span data-ttu-id="ce6c3-147">00BFEA71-DE22-43B2-A848-C05709900100</span><span class="sxs-lookup"><span data-stu-id="ce6c3-147">00bfea71-de22-43b2-a848-c05709900100</span></span>  <br/> |
|<span data-ttu-id="ce6c3-148">DataConnectionLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-148">DataConnectionLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-149">00bfea71-dbd7-4f72-b8cb-da7ac0440130</span><span class="sxs-lookup"><span data-stu-id="ce6c3-149">00bfea71-dbd7-4f72-b8cb-da7ac0440130</span></span>  <br/> |
|<span data-ttu-id="ce6c3-150">DataSourceLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-150">DataSourceLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-151">00BFEA71-F381-423D-B9D1-DA7A54C50110</span><span class="sxs-lookup"><span data-stu-id="ce6c3-151">00bfea71-f381-423d-b9d1-da7a54c50110</span></span>  <br/> |
|<span data-ttu-id="ce6c3-152">DiscussionsList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-152">DiscussionsList</span></span>  <br/> |<span data-ttu-id="ce6c3-153">00BFEA71-6A49-43FA-B535-D15C05500108</span><span class="sxs-lookup"><span data-stu-id="ce6c3-153">00bfea71-6a49-43fa-b535-d15c05500108</span></span>  <br/> |
|<span data-ttu-id="ce6c3-154">DocumentLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-154">DocumentLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-155">00BFEA71-E717-4E80-AA17-D0C71B360101</span><span class="sxs-lookup"><span data-stu-id="ce6c3-155">00bfea71-e717-4e80-aa17-d0c71b360101</span></span>  <br/> |
|<span data-ttu-id="ce6c3-156">EventsList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-156">EventsList</span></span>  <br/> |<span data-ttu-id="ce6c3-157">00BFEA71-EC85-4903-972D-EBE475780106</span><span class="sxs-lookup"><span data-stu-id="ce6c3-157">00bfea71-ec85-4903-972d-ebe475780106</span></span>  <br/> |
|<span data-ttu-id="ce6c3-158">EventsList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-158">EventsList</span></span>  <br/> |<span data-ttu-id="ce6c3-159">00BFEA71-EC85-4903-972D-EBE475780106</span><span class="sxs-lookup"><span data-stu-id="ce6c3-159">00bfea71-ec85-4903-972d-ebe475780106</span></span>  <br/> |
|<span data-ttu-id="ce6c3-160">ExternalList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-160">ExternalList</span></span>  <br/> |<span data-ttu-id="ce6c3-161">00bfea71-9549-43f8-b978-e47e54a10600</span><span class="sxs-lookup"><span data-stu-id="ce6c3-161">00bfea71-9549-43f8-b978-e47e54a10600</span></span>  <br/> |
|<span data-ttu-id="ce6c3-162">FollowingContent</span><span class="sxs-lookup"><span data-stu-id="ce6c3-162">FollowingContent</span></span>  <br/> |<span data-ttu-id="ce6c3-163">a7a2793e-67cd-4dc1-9fd0-43f61581207a</span><span class="sxs-lookup"><span data-stu-id="ce6c3-163">a7a2793e-67cd-4dc1-9fd0-43f61581207a</span></span>  <br/> |
|<span data-ttu-id="ce6c3-164">GanttTasksList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-164">GanttTasksList</span></span>  <br/> |<span data-ttu-id="ce6c3-165">00BFEA71-513D-4CA0-96C2-6A47775C0119</span><span class="sxs-lookup"><span data-stu-id="ce6c3-165">00bfea71-513d-4ca0-96c2-6a47775c0119</span></span>  <br/> |
|<span data-ttu-id="ce6c3-166">GettingStarted</span><span class="sxs-lookup"><span data-stu-id="ce6c3-166">GettingStarted</span></span>  <br/> |<span data-ttu-id="ce6c3-167">4aec7207-0d02-4f4f-aa07-b370199cd0c7</span><span class="sxs-lookup"><span data-stu-id="ce6c3-167">4aec7207-0d02-4f4f-aa07-b370199cd0c7</span></span>  <br/> |
|<span data-ttu-id="ce6c3-168">GridList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-168">GridList</span></span>  <br/> |<span data-ttu-id="ce6c3-169">00BFEA71-3A1D-41D3-A0EE-651D11570120</span><span class="sxs-lookup"><span data-stu-id="ce6c3-169">00bfea71-3a1d-41d3-a0ee-651d11570120</span></span>  <br/> |
|<span data-ttu-id="ce6c3-170">HierarchyTasksList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-170">HierarchyTasksList</span></span>  <br/> |<span data-ttu-id="ce6c3-171">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span><span class="sxs-lookup"><span data-stu-id="ce6c3-171">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span></span>  <br/> |
|<span data-ttu-id="ce6c3-172">IPFSWebFeatures</span><span class="sxs-lookup"><span data-stu-id="ce6c3-172">IPFSWebFeatures</span></span>  <br/> |<span data-ttu-id="ce6c3-173">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span><span class="sxs-lookup"><span data-stu-id="ce6c3-173">f9ce21f8-f437-4f7e-8bc6-946378c850f0</span></span>  <br/> |
|<span data-ttu-id="ce6c3-174">IssuesList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-174">IssuesList</span></span>  <br/> |<span data-ttu-id="ce6c3-175">00BFEA71-5932-4F9C-AD71-1557E5751100</span><span class="sxs-lookup"><span data-stu-id="ce6c3-175">00bfea71-5932-4f9c-ad71-1557e5751100</span></span>  <br/> |
|<span data-ttu-id="ce6c3-176">LinksList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-176">LinksList</span></span>  <br/> |<span data-ttu-id="ce6c3-177">00BFEA71-5932-4F9C-AD71-1557E5751100</span><span class="sxs-lookup"><span data-stu-id="ce6c3-177">00bfea71-5932-4f9c-ad71-1557e5751100</span></span>  <br/> |
|<span data-ttu-id="ce6c3-178">MBrowserRedirect</span><span class="sxs-lookup"><span data-stu-id="ce6c3-178">MBrowserRedirect</span></span>  <br/> |<span data-ttu-id="ce6c3-179">d95c97f3-e528-4da2-ae9f-32b3535fbb59</span><span class="sxs-lookup"><span data-stu-id="ce6c3-179">d95c97f3-e528-4da2-ae9f-32b3535fbb59</span></span>  <br/> |
|<span data-ttu-id="ce6c3-180">MDSFeature</span><span class="sxs-lookup"><span data-stu-id="ce6c3-180">MDSFeature</span></span>  <br/> |<span data-ttu-id="ce6c3-181">87294c72-f260-42f3-a41b-981a2ffce37a</span><span class="sxs-lookup"><span data-stu-id="ce6c3-181">87294c72-f260-42f3-a41b-981a2ffce37a</span></span>  <br/> |
|<span data-ttu-id="ce6c3-182">MobilityRedirect</span><span class="sxs-lookup"><span data-stu-id="ce6c3-182">MobilityRedirect</span></span>  <br/> |<span data-ttu-id="ce6c3-183">f41cc668-37e5-4743-b4a8-74d1db3fd8a4</span><span class="sxs-lookup"><span data-stu-id="ce6c3-183">f41cc668-37e5-4743-b4a8-74d1db3fd8a4</span></span>  <br/> |
|<span data-ttu-id="ce6c3-184">MySiteMicroBlog</span><span class="sxs-lookup"><span data-stu-id="ce6c3-184">MySiteMicroBlog</span></span>  <br/> |<span data-ttu-id="ce6c3-185">ea23650b-0340-4708-b465-441a41c37af7</span><span class="sxs-lookup"><span data-stu-id="ce6c3-185">ea23650b-0340-4708-b465-441a41c37af7</span></span>  <br/> |
|<span data-ttu-id="ce6c3-186">NoCodeWorkflowLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-186">NoCodeWorkflowLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-187">00BFEA71-F600-43F6-A895-40C0DE7B0117</span><span class="sxs-lookup"><span data-stu-id="ce6c3-187">00bfea71-f600-43f6-a895-40c0de7b0117</span></span>  <br/> |
|<span data-ttu-id="ce6c3-188">PictureLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-188">PictureLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-189">00BFEA71-52D4-45B3-B544-B1C71B620109</span><span class="sxs-lookup"><span data-stu-id="ce6c3-189">00bfea71-52d4-45b3-b544-b1c71b620109</span></span>  <br/> |
|<span data-ttu-id="ce6c3-190">PremiumWeb</span><span class="sxs-lookup"><span data-stu-id="ce6c3-190">PremiumWeb</span></span>  <br/> |<span data-ttu-id="ce6c3-191">0806d127-06e6-447a-980e-2e90b03101b8</span><span class="sxs-lookup"><span data-stu-id="ce6c3-191">0806d127-06e6-447a-980e-2e90b03101b8</span></span>  <br/> |
|<span data-ttu-id="ce6c3-192">PromotedLinksList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-192">PromotedLinksList</span></span>  <br/> |<span data-ttu-id="ce6c3-193">192efa95-e50c-475e-87ab-361cede5dd7f</span><span class="sxs-lookup"><span data-stu-id="ce6c3-193">192efa95-e50c-475e-87ab-361cede5dd7f</span></span>  <br/> |
|<span data-ttu-id="ce6c3-194">ReportListTemplate</span><span class="sxs-lookup"><span data-stu-id="ce6c3-194">ReportListTemplate</span></span>  <br/> |<span data-ttu-id="ce6c3-195">2510d73f-7109-4ccc-8a1c-314894deeb3a</span><span class="sxs-lookup"><span data-stu-id="ce6c3-195">2510d73f-7109-4ccc-8a1c-314894deeb3a</span></span>  <br/> |
|<span data-ttu-id="ce6c3-196">SiteFeed</span><span class="sxs-lookup"><span data-stu-id="ce6c3-196">SiteFeed</span></span>  <br/> |<span data-ttu-id="ce6c3-197">15a572c6-e545-4d32-897a-bab6f5846e18</span><span class="sxs-lookup"><span data-stu-id="ce6c3-197">15a572c6-e545-4d32-897a-bab6f5846e18</span></span>  <br/> |
|<span data-ttu-id="ce6c3-198">SiteFeedController</span><span class="sxs-lookup"><span data-stu-id="ce6c3-198">SiteFeedController</span></span>  <br/> |<span data-ttu-id="ce6c3-199">5153156a-63af-4fac-b557-91bd8c315432</span><span class="sxs-lookup"><span data-stu-id="ce6c3-199">5153156a-63af-4fac-b557-91bd8c315432</span></span>  <br/> |
|<span data-ttu-id="ce6c3-200">SurveysList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-200">SurveysList</span></span>  <br/> |<span data-ttu-id="ce6c3-201">00BFEA71-EB8A-40B1-80C7-506BE7590102</span><span class="sxs-lookup"><span data-stu-id="ce6c3-201">00bfea71-eb8a-40b1-80c7-506be7590102</span></span>  <br/> |
|<span data-ttu-id="ce6c3-202">TaskListNewsFeed</span><span class="sxs-lookup"><span data-stu-id="ce6c3-202">TaskListNewsFeed</span></span>  <br/> |<span data-ttu-id="ce6c3-203">ff13819a-a9ac-46fb-8163-9d53357ef98d</span><span class="sxs-lookup"><span data-stu-id="ce6c3-203">ff13819a-a9ac-46fb-8163-9d53357ef98d</span></span>  <br/> |
|<span data-ttu-id="ce6c3-204">TasksList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-204">TasksList</span></span>  <br/> |<span data-ttu-id="ce6c3-205">00BFEA71-A83E-497E-9BA0-7A5C597D0107</span><span class="sxs-lookup"><span data-stu-id="ce6c3-205">00bfea71-a83e-497e-9ba0-7a5c597d0107</span></span>  <br/> |
|<span data-ttu-id="ce6c3-206">TeamCollab</span><span class="sxs-lookup"><span data-stu-id="ce6c3-206">TeamCollab</span></span>  <br/> |<span data-ttu-id="ce6c3-207">00bfea71-4ea5-48d4-a4ad-7ea5c011abe5</span><span class="sxs-lookup"><span data-stu-id="ce6c3-207">00bfea71-4ea5-48d4-a4ad-7ea5c011abe5</span></span>  <br/> |
|<span data-ttu-id="ce6c3-208">WebPageLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-208">WebPageLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-209">00BFEA71-C796-4402-9F2F-0EB9A6E71B18</span><span class="sxs-lookup"><span data-stu-id="ce6c3-209">00bfea71-c796-4402-9f2f-0eb9a6e71b18</span></span>  <br/> |
|<span data-ttu-id="ce6c3-210">WikiPageHomePage</span><span class="sxs-lookup"><span data-stu-id="ce6c3-210">WikiPageHomePage</span></span>  <br/> |<span data-ttu-id="ce6c3-211">00bfea71-d8fe-4fec-8dad-01c19a6e4053</span><span class="sxs-lookup"><span data-stu-id="ce6c3-211">00bfea71-d8fe-4fec-8dad-01c19a6e4053</span></span>  <br/> |
|<span data-ttu-id="ce6c3-212">WorkflowHistoryList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-212">WorkflowHistoryList</span></span>  <br/> |<span data-ttu-id="ce6c3-213">00BFEA71-4EA5-48D4-A4AD-305CF7030140</span><span class="sxs-lookup"><span data-stu-id="ce6c3-213">00bfea71-4ea5-48d4-a4ad-305cf7030140</span></span>  <br/> |
|<span data-ttu-id="ce6c3-214">workflowProcessList</span><span class="sxs-lookup"><span data-stu-id="ce6c3-214">workflowProcessList</span></span>  <br/> |<span data-ttu-id="ce6c3-215">00BFEA71-2D77-4A75-9FCA-76516689E21A</span><span class="sxs-lookup"><span data-stu-id="ce6c3-215">00bfea71-2d77-4a75-9fca-76516689e21a</span></span>  <br/> |
|<span data-ttu-id="ce6c3-216">WorkflowServiceStore</span><span class="sxs-lookup"><span data-stu-id="ce6c3-216">WorkflowServiceStore</span></span>  <br/> |<span data-ttu-id="ce6c3-217">2c63df2b-ceab-42c6-aeff-b3968162d4b1</span><span class="sxs-lookup"><span data-stu-id="ce6c3-217">2c63df2b-ceab-42c6-aeff-b3968162d4b1</span></span>  <br/> |
|<span data-ttu-id="ce6c3-218">WorkflowTask</span><span class="sxs-lookup"><span data-stu-id="ce6c3-218">WorkflowTask</span></span>  <br/> |<span data-ttu-id="ce6c3-219">57311b7a-9afd-4ff0-866e-9393ad6647b1</span><span class="sxs-lookup"><span data-stu-id="ce6c3-219">57311b7a-9afd-4ff0-866e-9393ad6647b1</span></span>  <br/> |
|<span data-ttu-id="ce6c3-220">XmlFormLibrary</span><span class="sxs-lookup"><span data-stu-id="ce6c3-220">XmlFormLibrary</span></span>  <br/> |<span data-ttu-id="ce6c3-221">00BFEA71-1E1D-4562-B56A-F05371BB0115</span><span class="sxs-lookup"><span data-stu-id="ce6c3-221">00bfea71-1e1d-4562-b56a-f05371bb0115</span></span>  <br/> |
   
5. <span data-ttu-id="ce6c3-222">Сохраните изменения и развертывания обычным образом.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-222">Save your changes, and deploy as you would normally.</span></span>
    
  

> <span data-ttu-id="ce6c3-223">**Примечание:** Может также потребоваться для активации этих компонентов в программе центра администрирования.</span><span class="sxs-lookup"><span data-stu-id="ce6c3-223">**Note:** You may also need to activate these features in the Central Administration utility.</span></span> 
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="ce6c3-224">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ce6c3-224">Additional resources</span></span>
<span data-ttu-id="ce6c3-225"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="ce6c3-225"></span></span>


-  [<span data-ttu-id="ce6c3-226">Обновление настроек сайта для SharePoint</span><span class="sxs-lookup"><span data-stu-id="ce6c3-226">Upgrade site customizations for SharePoint</span></span>](upgrade-site-customizations-for-sharepoint.md)
    
  
-  [<span data-ttu-id="ce6c3-227">SharePoint 2010 и веб-шаблоны</span><span class="sxs-lookup"><span data-stu-id="ce6c3-227">SharePoint 2010 and web templates</span></span>](http://blogs.msdn.com/b/vesku/archive/2010/10/14/sharepoint-2010-and-web-templates.aspx)
    
  
-  [<span data-ttu-id="ce6c3-228">Планирование обновления семейства веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="ce6c3-228">Plan to upgrade a site collection</span></span>](https://technet.microsoft.com/ru-ru/library/ff191199.aspx)
    
  
-  [<span data-ttu-id="ce6c3-229">Планирование обновлений семейств сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="ce6c3-229">Plan for site collection upgrades in SharePoint</span></span>](http://technet.microsoft.com/ru-ru/library/ff191199.aspx)
    
  

  
    
    

