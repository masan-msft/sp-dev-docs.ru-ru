---
title: "Создание многократно используемых компонентов для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bb4467e2-57f0-4cf1-91b8-4d3d8d2358cb
ms.openlocfilehash: c51ae0c737445f5812afbf35f3fe1d28c7c6284c
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="build-reusable-components-for-sharepoint"></a><span data-ttu-id="d465c-102">Создание многократно используемых компонентов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d465c-102">Build reusable components for SharePoint</span></span>
<span data-ttu-id="d465c-103">Сведения о некоторых наиболее важные для повторного использования компонентов, которые можно создать в SharePoint, включая веб-частей, рабочие процессы, настраиваемые списки и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d465c-103">Learn about some of the most important reusable components you can build in SharePoint, including Web Parts, workflows, custom lists, and more.</span></span>
## <a name="reusable-components-in-sharepoint"></a><span data-ttu-id="d465c-104">Для повторного использования компонентов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d465c-104">Reusable components in SharePoint</span></span>
<span data-ttu-id="d465c-105"><a name="SP15Reusecomp_Reusable"> </a></span><span class="sxs-lookup"><span data-stu-id="d465c-105"></span></span>

<span data-ttu-id="d465c-106">При использовании SharePoint можно создавать различные компоненты, такие как списки, веб-частей и типов контента, которые можно использовать в различных приложениях, сайтов и решений.</span><span class="sxs-lookup"><span data-stu-id="d465c-106">Using SharePoint, you can build a variety of components, such as lists, Web Parts, and content types, which you can reuse in various apps, sites, and solutions.</span></span> <span data-ttu-id="d465c-107">В этом разделе представлены некоторые из наиболее распространенных компонентов для повторного использования, которые можно создать в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d465c-107">This section summarizes some of the most common reusable components that you can build in SharePoint.</span></span> <span data-ttu-id="d465c-108">В этой документации в дальнейшем будет содержать сведения о дополнительных компонентов, можно построить.</span><span class="sxs-lookup"><span data-stu-id="d465c-108">Future updates to this documentation will contain information about additional components you can build.</span></span>
  
    
    

> <span data-ttu-id="d465c-109">**Примечание:** Существуют некоторые ограничения на какие компоненты можно использовать в SharePoint надстройки. Для получения дополнительных сведений см [хост-сайты, добавьте в веб-сайтов и компоненты SharePoint в SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d465c-109">**Note:** There are some restrictions on which components you can use in SharePoint Add-ins. For more information, see  [Host webs, add-in webs, and SharePoint components in SharePoint](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx).</span></span> 
  
    
    


- <span data-ttu-id="d465c-p102">**Веб-части**, чаще всего для расширения SharePoint. Обучение для построения веб-частей  это отличный способ, чтобы начать разработку для SharePoint. Дополнительные сведения можно [Стандартные блоки разработки в SharePoint: Technologies for Creating SharePoint Applications](http://msdn.microsoft.com/library/138422cf-c140-466a-bcd8-cacba51ef886%28Office.15%29.aspx#bb2_WebParts).</span><span class="sxs-lookup"><span data-stu-id="d465c-p102">**Web Parts** are the most common way to extend SharePoint. Learning to build Web Parts is a great way to start SharePoint development. For more information, see [SharePoint Developer Building Blocks: Technologies for Creating SharePoint Applications](http://msdn.microsoft.com/library/138422cf-c140-466a-bcd8-cacba51ef886%28Office.15%29.aspx#bb2_WebParts).</span></span>
    
  
- <span data-ttu-id="d465c-p103">**Настраиваемые списки** на сайтах SharePoint укажите расположение для хранения данных. Операции с данными в списках SharePoint рекомендуется широко используемых. Списки можно использовать для хранения данных, можно получить доступ программными средствами. Дополнительные сведения можно [стандартный блок: списки и библиотеки документов](http://msdn.microsoft.com/library/16da8f64-f53b-4490-8636-db0e4d7a6912%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d465c-p103">**Custom lists** in SharePoint sites provide locations to store data. Data manipulation in SharePoint lists is a widely used practice. You can use lists to contain data that you access programmatically. For more information, see [Building Block: Lists and Document Libraries](http://msdn.microsoft.com/library/16da8f64-f53b-4490-8636-db0e4d7a6912%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="d465c-117">**Рабочие процессы** позволяют пожалейте и стандартизации бизнес-процессов и являетесь одним из средства, необходимые для реализации определенного сценария.</span><span class="sxs-lookup"><span data-stu-id="d465c-117">**Workflows** enable you to codify and standardize business processes, and are one of the essential tools for implementing certain scenarios.</span></span> <span data-ttu-id="d465c-118">Для получения дополнительных сведений см [рабочих процессов в SharePoint](workflows-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d465c-118">For more information, see [Workflows in SharePoint](workflows-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="d465c-119">**Внешние типы контента** доступность данных из за пределами развертывания SharePoint для приложения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d465c-119">**External content types** make data from outside the SharePoint deployment available to the SharePoint application.</span></span> <span data-ttu-id="d465c-120">Для получения дополнительных сведений см [внешние типы контента в SharePoint](external-content-types-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="d465c-120">For more information, see [External content types in SharePoint](external-content-types-in-sharepoint.md).</span></span>
    
  
- <span data-ttu-id="d465c-p106">Вы можете определить **тип контента**, который является прототип элемента списка. При использовании типов контента для списка список можно определить, чтобы он содержит только элементы одного типа контента, или можно указать, что он может содержать элементы из одного из нескольких типов контента. Для получения дополнительных сведений см [Введение в типы контента](http://msdn.microsoft.com/library/a345a6c5-7031-46ab-a2c2-37bedc3012f4%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d465c-p106">You can define a **content type** that is a prototype of a list item. If you are using content types for a list, you can define the list so that it contains only items of one content type, or you can specify that it can contain items of one of several content types. For more information, see [Introduction to Content Types](http://msdn.microsoft.com/library/a345a6c5-7031-46ab-a2c2-37bedc3012f4%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="d465c-p107">**Типы столбцов** и **типов полей** позволяют определять расширенном метаданных для стандартных полей и столбцов в списках SharePoint. Можно определить столбец сайта (в коллекции столбцов сайта) определенного типа данных, которые можно использовать во всем веб-узла. Это напоминает определение домены в проект схемы базы данных. Это позволяет убедитесь, что столбцы в нескольких списках используют то же пространство значение. Для получения дополнительных сведений см [Настраиваемых типов полей](http://msdn.microsoft.com/library/1345b345-226d-443a-918f-af123a3c7b13%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d465c-p107">**Column types** and **field types** enable you to define rich metadata for standardized fields and columns in SharePoint lists. You can define a site column (in a site column gallery) of a specific data type that you can use throughout your site. This resembles defining domains in database schema design. It lets you ensure that columns in several lists use the same value space. For more information, see [Custom Field Types](http://msdn.microsoft.com/library/1345b345-226d-443a-918f-af123a3c7b13%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="d465c-p108">**Приемники событий** позволяют создавать обработчиков событий, которые вызываются при, например пользователям добавлять, удалять и изменять элементы в списках или библиотеки документов SharePoint. Дополнительные сведения можно [стандартный блок: обработка событий](http://msdn.microsoft.com/library/212cf488-43cb-4250-82d5-3b962b6e56e6%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d465c-p108">**Event receivers** enable you to write event handlers that are called when, for example, users add, delete, or modify items in SharePoint document libraries or lists. For more information, see [Building Block: Event Handling](http://msdn.microsoft.com/library/212cf488-43cb-4250-82d5-3b962b6e56e6%28Office.15%29.aspx).</span></span>
    
  
- <span data-ttu-id="d465c-p109">**Удаленные приемники событий** предоставляют возможность уведомления внешних систем событий SharePoint. Можно указать свойства конечной точки и событий, чтобы вызвать, когда происходит событие. Для получения дополнительных сведений см [Создание удаленного приемника событий в надстройках SharePoint](http://msdn.microsoft.com/library/628c6103-52f9-4d85-9464-4a6862b36640%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d465c-p109">**Remote event receivers** provide a way to notify external systems of SharePoint events. You can specify the endpoint and event properties to call when an event happens. For more information, see [Create a remote event receiver in SharePoint Add-ins](http://msdn.microsoft.com/library/628c6103-52f9-4d85-9464-4a6862b36640%28Office.15%29.aspx).</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="d465c-134">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d465c-134">Additional resources</span></span>
<span data-ttu-id="d465c-135"><a name="SP15Reusecomp_AddRes"> </a></span><span class="sxs-lookup"><span data-stu-id="d465c-135"></span></span>


-  [<span data-ttu-id="d465c-136">Модели программирования в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d465c-136">Programming models in SharePoint</span></span>](programming-models-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d465c-137">Настройка общей среды разработки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d465c-137">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [<span data-ttu-id="d465c-138">Обзор разработки решений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="d465c-138">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  
-  [<span data-ttu-id="d465c-139">Хост-сайты, сайты надстроек и компоненты SharePoint в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d465c-139">Host webs, add-in webs, and SharePoint components in SharePoint</span></span>](http://msdn.microsoft.com/library/b791cdf5-8aa2-47fa-bc4c-aee437354759%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d465c-140">Стандартные блоки SharePoint Foundation 2010</span><span class="sxs-lookup"><span data-stu-id="d465c-140">SharePoint Foundation 2010 Building Blocks</span></span>](http://msdn.microsoft.com/library/0d7f5106-dcbd-442e-9907-d28a323bbe11%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d465c-141">SharePoint для разработчиков стандартные блоки: Технологии создания приложений SharePoint (часть 1 из 2)</span><span class="sxs-lookup"><span data-stu-id="d465c-141">SharePoint Developer Building Blocks: Technologies for Creating SharePoint Applications (Part 1 of 2)</span></span>](http://msdn.microsoft.com/library/7ef04158-d149-4301-ab91-4617677eefc4%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="d465c-142">SharePoint для разработчиков стандартные блоки: Технологии создания приложений SharePoint (часть 2 из 2)</span><span class="sxs-lookup"><span data-stu-id="d465c-142">SharePoint Developer Building Blocks: Technologies for Creating SharePoint Applications (Part 2 of 2)</span></span>](http://msdn.microsoft.com/library/138422cf-c140-466a-bcd8-cacba51ef886%28Office.15%29.aspx)
    
  

