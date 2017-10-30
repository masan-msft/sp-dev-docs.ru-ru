---
title: "Публикация сайтов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 46b5a79c-962f-4a07-8316-d5005eabd0e0
ms.openlocfilehash: 499e42a703295db74702751f607e2b41fc7c04d5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="publish-sharepoint-sites"></a><span data-ttu-id="7d287-102">Публикация сайтов SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d287-102">Publish SharePoint sites</span></span>

<span data-ttu-id="7d287-103">После разработки или разрабатывают различные компоненты сайта и контента, их можно развернуть в текущем семействе сайтов и других семейств веб-сайтов  даже для семейств веб-сайтов, которые пересекать границы Интернета и интрасети.</span><span class="sxs-lookup"><span data-stu-id="7d287-103">After you design or develop site components and content, you can deploy them to the current site collection and other site collections—even to site collections that cross the intranet/Internet boundary.</span></span>
  
    
    


## <a name="cross-site-publishing"></a><span data-ttu-id="7d287-104">Публикация на нескольких сайтах</span><span class="sxs-lookup"><span data-stu-id="7d287-104">Cross-site publishing</span></span>

<span data-ttu-id="7d287-105">Сведения о  [публикации на нескольких сайтах](cross-site-publishing-in-sharepoint.md) и влияние планированию и публикация сайтов и их разработки контента и связанные элементы.</span><span class="sxs-lookup"><span data-stu-id="7d287-105">Learn about  [cross-site publishing](cross-site-publishing-in-sharepoint.md) and how it affects how you plan and publish sites and their content and associated design elements.</span></span>
  
    
    

## <a name="publishing-considerations-for-variations-and-multilingual-sites"></a><span data-ttu-id="7d287-106">Вопросы для вариантов и многоязычных сайтов публикации</span><span class="sxs-lookup"><span data-stu-id="7d287-106">Publishing considerations for variations and multilingual sites</span></span>

<span data-ttu-id="7d287-p101">Различные рынков иметь разные вкусы. Функция вариантов помогает учесть эти вкусы с указанием функциональные возможности, которые можно использовать для локализации и переводить контент, но также для публикации содержимого и его элементы связанного разработки семейств веб-сайтов по всему миру. Чтобы сделать публикуемый контент для локальных рынках успешно, рассмотрите советы, которые показывают, как проектирования и содержимое управления принятые решения могут повлиять на как опубликованный контент сайта и может отображать структуры.</span><span class="sxs-lookup"><span data-stu-id="7d287-p101">Different markets have different tastes. The variations feature helps accommodate those tastes by providing functionality that you can use to localize and translate content, but also to publish that content and its associated design elements to site collections all over the world. To help make publishing content to local markets successful, consider these tips that show how design and content management decisions you make can affect how published site contents and structure may render:</span></span>
  
    
    

- <span data-ttu-id="7d287-p102">Дублирование активов разработки положительно влияет на производительность сайта публикации и отображения, а также приводятся рекомендации управление сложных сайтов, для которых включено для вариантов меньше комплексного. Главная страница представляет собой файл ASP.NET, содержащий заполнителей контента, которые заполняются, отдельные экземпляры страниц и макетов страниц.</span><span class="sxs-lookup"><span data-stu-id="7d287-p102">Duplication of design assets positively affects the performance of site publishing and rendering and helps make managing complex sites that are enabled for variations less complex. A master page is an ASP.NET file that contains content placeholders that are populated by page layouts and individual instances of pages.</span></span> 
    
  
- <span data-ttu-id="7d287-p103">Если применить определенных типов содержимого для всех языковых стандартах в семействе веб-сайтов, лучше создать их в качестве сайта типов контента из корневого веб-узла. Можно также создать типы контента в разделе вариантов веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="7d287-p103">If certain content types apply to all locales in your site collection, it's best to create them as site content types of the root web. You can also create content types under variation sites.</span></span> 
    
  
- <span data-ttu-id="7d287-114">При добавлении дополнительных столбцов для исходного списка, добавив элемент с типом контента, который ранее не существует в этот список вариантов обновления схемы каждого целевого списка для отражения новых столбцов в следующий раз добавить элемент в целевой список.</span><span class="sxs-lookup"><span data-stu-id="7d287-114">If you add additional columns to a source list by adding an item with a content type that did not previously exist in that list, variations updates the schema of each target list to reflect the new columns the next time you add an item to that target list.</span></span> 
    
  
- <span data-ttu-id="7d287-p104">Управляемые навигации работает с вариантов. Структура навигации  на основе структуры веб-сайта SharePoint  по-прежнему работает: синхронизирует содержимого и структуры между исходной и целевой меток вариантов.</span><span class="sxs-lookup"><span data-stu-id="7d287-p104">Managed navigation works with variations. Structured navigation—based on the SharePoint website structure—also still works: it synchronizes the content and structure between the source and target variations labels.</span></span> 
    
  
- <span data-ttu-id="7d287-p105">Функция каналы устройств выделяет проблемы меняющегося представления содержимого для мобильных устройств из базового контента сайтов и структуры. Можно создавать главные страницы, содержащие пользователей в соответствии пользователя агента пользователя. Избегайте жестко кодировать в главной страницы контента, который требуется локализовать.</span><span class="sxs-lookup"><span data-stu-id="7d287-p105">The device channels feature abstracts the problem of varying the presentation of content for mobile devices from the underlying site content and structure. You can create master pages that present to users based on the user's user agent. Avoid hard-coding in a master page content that will need to be localized.</span></span>
    
  
- <span data-ttu-id="7d287-p106">Сайты с динамическим содержимым, собираются из нескольких источников рисков необходимости содержимое отображается на нескольких языках на той же странице. Например Избегайте случаях, когда статья содержимого страницы с одним языком во время отображения содержимого, отображаемом с помощью веб-части поиска контента на другом языке.</span><span class="sxs-lookup"><span data-stu-id="7d287-p106">Sites with dynamic content assembled from multiple sources risk having content rendered in multiple languages on the same page. For example, avoid cases where article page content is one language while content rendered by a Content Search Web Part is rendered in another language.</span></span> 
    
  
- <span data-ttu-id="7d287-p107">При работе с шаблонами отображения, используемые для нескольких языков, создайте файлы языковой поддержки и помещения их в разделе папки с именами с языковыми параметрами, которые они применяются к. Затем можно ссылаться на языковых файлов с помощью функции  `$includeLanguageScript` и `{Locale}` маркер.</span><span class="sxs-lookup"><span data-stu-id="7d287-p107">If you work with display templates that are used with multiple languages, create language files and place them under folders that are named with the locale that they apply to. You can then reference the language files with the  `$includeLanguageScript` function and the `{Locale}` token.</span></span>
    
    <span data-ttu-id="7d287-124">Если контента веб-части поиска использует свойство **Language** найти соответствующий файл CustomStrings.js для включения и его не существует, а код в шаблоне запрашивает строку для отображения, который не удается найти с помощью функции `$resource()` или `Srch.U.loadResource()` , контента веб-части поиска отображает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7d287-124">If the Content Search Web Part relies on the **Language** property to find the appropriate CustomStrings.js file to include and one doesn't exist, and code in the template requests a string to display that cannot be found by using the `$resource()` or `Srch.U.loadResource()` functions, the Content Search Web Part displays an error message.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="7d287-125">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7d287-125">Additional resources</span></span>
<span data-ttu-id="7d287-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="7d287-126"></span></span>


-  [<span data-ttu-id="7d287-127">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d287-127">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="7d287-128">Новые возможности разработки сайтов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7d287-128">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  

