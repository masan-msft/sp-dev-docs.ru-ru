---
title: "Инструкции. Применение эталонной страницы к сайту в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 04861390-84d5-40ea-b0db-6c0748eff196
ms.openlocfilehash: a015d4d276933219a548693e11e6e67671cef983
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-apply-a-master-page-to-a-site-in-sharepoint"></a><span data-ttu-id="d6ca3-102">Инструкции. Применение эталонной страницы к сайту в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6ca3-102">How to: Apply a master page to a site in SharePoint</span></span>
<span data-ttu-id="d6ca3-103">Узнайте, как назначить эталонную страницу для сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-103">Learn how to map a master page to a SharePoint site.</span></span>
## <a name="mapping-a-master-page-to-a-site"></a><span data-ttu-id="d6ca3-104">Назначение эталонной страницы для сайта</span><span class="sxs-lookup"><span data-stu-id="d6ca3-104">Mapping a master page to a site</span></span>

<span data-ttu-id="d6ca3-p101">В SharePoint эталонная страница задает общие элементы фрейма, например хром, для всех страниц на сайте. После создания эталонной страницы ее можно назначить сайту. Это можно делать для всех страниц публикации, предназначенных для всех пользователей, или для административных страниц, используемых для технического обслуживания. Кроме того, если вы настраиваете дочерний или родительский сайт, эталонную страницу можно унаследовать от родительского сайта. В этой статье представлены указания по назначению созданной эталонной страницы для сайта, наследованию эталонной страницы от родительского сайта и назначению эталонной страницы для определенного канала устройств.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-p101">In SharePoint, a master page defines the shared framing elements such as the chrome for all pages in your site. After a master page is created, it can be mapped to a site. This could be for all publishing pages designated for all users, or for the administrative pages used for site maintenance. Alternatively, if you are configuring a child site of a parent site, you can inherit the master page from the parent. This article provides the steps to map a created master page to a site, inherit the master page from a parent site, or map a master page to a specific device channel.</span></span>
  
    
    

> <span data-ttu-id="d6ca3-110">**Примечание.** Дополнительные сведения о компоненте "Дизайнер" и эталонных страницах см. в статье [Обзор компонента "Дизайнер" в SharePoint](overview-of-design-manager-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d6ca3-110">**Note** For more information about Design Manager and master pages, see  [Overview of Design Manager in SharePoint](overview-of-design-manager-in-sharepoint.md). For more information about how to create device channels, see  SharePoint Design Manager device channels.</span></span> <span data-ttu-id="d6ca3-111">Дополнительные сведения о создании каналов устройств см. в статье [Каналы устройств в компоненте "Дизайнер" SharePoint](sharepoint-design-manager-device-channels.md).</span><span class="sxs-lookup"><span data-stu-id="d6ca3-111">Note For more information about Design Manager and master pages, see  Overview of Design Manager in SharePoint. For more information about how to create device channels, see  [SharePoint Design Manager device channels](sharepoint-design-manager-device-channels.md).</span></span> 
  
    
    


### <a name="to-map-a-master-page-to-a-sharepoint-site"></a><span data-ttu-id="d6ca3-112">Сопоставление эталонной страницы с сайтом SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6ca3-112">To map a master page to a SharePoint site</span></span>


1.  <span data-ttu-id="d6ca3-113">На странице **Параметры сайта** для соответствующего сайта выберите в разделе **Внешний вид и функции** элемент **Эталонная страница**.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-113">In **Site Settings** for the designated site, under the **Look and Feel** section, choose **Master Page**.</span></span>
    
    > <span data-ttu-id="d6ca3-114">**Примечание.** Если там нет ссылки **Эталонная страница**, то необходимо включить функцию публикации, выполнив указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-114">**Note** If the **Master Page** link is not there, you need to enable the publishing feature with these steps. Navigate to Site Settings | Site Collection Administration | Site Collection Features. Scroll down to the SharePoint Server Publishing Infrastructure feature and press Activate.</span></span> <span data-ttu-id="d6ca3-115">Перейдите к разделу **Параметры сайта | Администрирование семейства веб-сайтов | Возможности семейства веб-сайтов**.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-115">Navigate to **Site Settings | Site Collection Administration | Site Collection Features**.</span></span> <span data-ttu-id="d6ca3-116">Прокрутите вниз до функции **Инфраструктура публикации SharePoint Server** и нажмите **Активировать**.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-116">Scroll down to the **SharePoint Server Publishing Infrastructure** feature and press **Activate**.</span></span> 
2. <span data-ttu-id="d6ca3-117">На странице **Параметры главной страницы сайта** выберите один из двух вариантов в разделе **Главная страница сайта** или **Главная системная страница**:</span><span class="sxs-lookup"><span data-stu-id="d6ca3-117">On **Site Master Page Settings**, select one of the two options for the **Site Master Page** or **System Master Page** sections:</span></span>
    
  - <span data-ttu-id="d6ca3-118">**Наследовать главную страницу сайта от родительского сайта** Выберите этот вариант, если вы настраиваете дочерний сайт SharePoint и хотите использовать эталонную страницу родительского сайта.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-118">**Inherit site master page from parent site** Choose this option if you are configuring a child SharePoint site and want to use the parent master page.</span></span>
    
    > <span data-ttu-id="d6ca3-119">**Примечание.** Если вы работаете на родительском сайте верхнего уровня, этот параметр будет недоступен.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-119">**Note** If you are working on the top-level parent site this option is unavailable.</span></span> 
  - <span data-ttu-id="d6ca3-p104">**Укажите главную страницу для этого сайта и всех его дочерних сайтов** Выберите этот вариант, если требуется назначить определенную эталонную страницу для сайта или отдельную эталонную страницу для административных страниц. Для вас доступно раскрывающееся поле с именем **По умолчанию** или **Все каналы** в зависимости от конфигурации сайта или системы, чтобы вы могли выбрать определенную эталонную страницу из коллекции. Выберите нужную эталонную страницу из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-p104">**Specify a master page to be used by this site and all sites that inherit from it** Choose this option if you want to map a specific master page to the site, or if you want to map a specific master page for administrative pages. A drop-down box named **Default** or **All Channels** is available for you, depending on your site or system configuration, so you can select a specific master page stored in the master page gallery. Select the desired master page from the drop-down box.</span></span>
    
    > <span data-ttu-id="d6ca3-123">**Примечание.** Если настроены какие-либо каналы устройств, будут доступны дополнительные раскрывающиеся поля для дополнительных параметров сопоставления эталонных страниц.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-123">**Note** If you have any device channels configured, there are additional drop-down boxes available for additional master page mapping options.</span></span> 
3. <span data-ttu-id="d6ca3-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6ca3-124">Choose **OK**.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="d6ca3-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d6ca3-125">Additional resources</span></span>
<span data-ttu-id="d6ca3-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d6ca3-126"></span></span>


-  [<span data-ttu-id="d6ca3-127">Разработка макета сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6ca3-127">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d6ca3-128">Обзор Дизайнера в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6ca3-128">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d6ca3-129">Новые возможности разработки сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d6ca3-129">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  

