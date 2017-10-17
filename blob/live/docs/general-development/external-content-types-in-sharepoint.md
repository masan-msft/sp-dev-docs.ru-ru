---
title: "Внешние типы контента в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 11d7adb5-5388-4517-ae03-beb7be1c6981
ms.openlocfilehash: 4b4f27d7a3e30da28eee1f68eea1faf958e5f678
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="external-content-types-in-sharepoint"></a><span data-ttu-id="2e117-102">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-102">External content types in SharePoint</span></span>
<span data-ttu-id="2e117-103">Прочитав эту статью, вы узнаете, что можно делать с внешними типами контента и что необходимо для их создания в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e117-103">Learn what you can do with external content types and what you need to start creating them in SharePoint.</span></span>
## <a name="what-is-an-external-content-type"></a><span data-ttu-id="2e117-104">Что такое внешний тип контента?</span><span class="sxs-lookup"><span data-stu-id="2e117-104">What is an external content type?</span></span>
<span data-ttu-id="2e117-105"><a name="SP15ectoverview_what"> </a></span><span class="sxs-lookup"><span data-stu-id="2e117-105"></span></span>

<span data-ttu-id="2e117-p101">Внешний тип контента  это основное понятие Службы Business Connectivity Services (BCS). Внешние типы контента используются во всех компонентах и службах BCS. Они представляют собой описание метаданных для повторного использования сведений о подключениях и определений данных, а также поведения, которое необходимо применить к той или иной категории внешних данных.</span><span class="sxs-lookup"><span data-stu-id="2e117-p101">The external content type is a core concept of Business Connectivity Services (BCS). Used throughout the functionality and services offered by BCS, external content types are reusable metadata descriptions of connectivity information and data definitions plus the behaviors you want to apply to a certain category of external data.</span></span>
  
    
    
<span data-ttu-id="2e117-108">Внешние типы контента позволяют управлять метаданными и поведение бизнес-сущности, например клиентом или заказом, и повторно использовать их из центрального расположения. С их помощью пользователи могут взаимодействовать с внешними данными и процессами в более осмысленном виде.</span><span class="sxs-lookup"><span data-stu-id="2e117-108">External content types enable you to manage and reuse the metadata and behaviors of a business entity, such as a customer or order from a central location, and enable users to interact with that external data and processes in a more meaningful way.</span></span>
  
    
    
<span data-ttu-id="2e117-109">Ниже приведены некоторые преимущества внешних типов контента.</span><span class="sxs-lookup"><span data-stu-id="2e117-109">The following are some of the benefits of using external content types:</span></span>
  
    
    

- <span data-ttu-id="2e117-p102">**Повторное использование:** внешний тип контента  это определение бизнес-сущности данных, поддерживающее повторное использование. После его создания вы можете использовать его с любым компонентом представления в BCS, чтобы сделать взаимодействие с внешними данными более удобным и простым.</span><span class="sxs-lookup"><span data-stu-id="2e117-p102">**Provide reusability:** An external content type is a reusable data definition of a business entity. After you create it, you can use it with any of the presentation features in BCS to provide a rich user experience to interact with external data.</span></span>
    
  
- <span data-ttu-id="2e117-p103">**Инкапсуляция сложности внешних систем:** внешние типы контента позволяют информационным сотрудникам создавать бизнес-решения, не волнуясь о сложных процессах взаимодействия с внешними системами, например о подключения данных и интерфейсах кода. После создания внешнего типа контента он становится доступным для использования любым необходимым способом (если у пользователей есть разрешения на выполнение соответствующей операции и доступ к внешним данным). При этом пользователю не требуется знать, где внешние данные расположены или как подключиться к ним.</span><span class="sxs-lookup"><span data-stu-id="2e117-p103">**Encapsulate complexities of external systems:** External content types enable information workers to assemble business solutions without having to handle the complexities of the external systems, such as connectivity information and code interfaces. After someone creates an external content type, it is available to users for use in any way they need (provided they have the permissions to perform that operation and access the external data). However, the user does not need to know anything about the location of the external data or how to connect to it.</span></span>
    
  
- <span data-ttu-id="2e117-p104">**Встроенное поведение Office и SharePoint:** внешние типы контента предоставляют внешним данным и службам различные типы поведения элементов Office (например, контактов, задач, календарей в Outlook, документов в Word и списков в SharePoint Workspace), элементов SharePoint (например, списков, веб-частей и страниц профиля) и разнообразные возможности (например, поиска или автономной работы). Чтобы пользователи могли работать в знакомых им средах, не "охотясь" за данными и не учась с нуля взаимодействовать с другими, в том числе специальными, пользовательскими интерфейсами.</span><span class="sxs-lookup"><span data-stu-id="2e117-p104">**Provide built-in Office and SharePoint behavior:** External content types provide Office item-type behaviors (such as Contacts, Tasks, Calendars in Outlook, documents in Word, and lists in SharePoint Workspace); SharePoint behaviors (such as lists, Web Parts, and profile pages); and capabilities (such as the ability to search or work offline) to external data and services. So users can work in their familiar work environments without having to hunt for data or learn and interact with different (and proprietary) user interfaces.</span></span>
    
  
- <span data-ttu-id="2e117-p105">**Более безопасный доступ:** внешние типы контента обеспечивают безопасность как во внешних системах, так и в SharePoint. Вы можете получить полный контроль над доступом к данным, настроив параметры безопасности в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e117-p105">**Help provide more secure access:** External content types adhere to the security put in place by both the external system and SharePoint. You can have full control of who accesses what data by configuring security in SharePoint.</span></span>
    
  
- <span data-ttu-id="2e117-p106">**Простое обслуживание:** так как внешние типы контента можно создать один раз и использовать в нескольких решениях в различных сценариях, ими легко управлять. Например, можно контролировать разрешения доступа, подключения и определения данных централизованно.</span><span class="sxs-lookup"><span data-stu-id="2e117-p106">**Simplify maintenance:** Because external content types can be created once and used by multiple solutions in various scenarios, you can manage them easily. For example, you can manage their access permissions and connection and data definitions in one central location.</span></span>
    
  
- <span data-ttu-id="2e117-p107">**Поиск внешних данных:** вы можете использовать Поиск SharePoint Server из портала интрасети для поиска сведений об определенном внешнем типе контента, например клиенте. Поиск SharePoint Server получает данные непосредственно из внешней системы. Следовательно, пользователи могут получить нужные сведения без утверждения или установки отдельного приложения.</span><span class="sxs-lookup"><span data-stu-id="2e117-p107">**Enable external data search:** You can use SharePoint Server search from an intranet portal to look up information about a specific external content type, such as a customer. SharePoint Server search retrieves the data directly from the external system. Consequently, users can get the information they need without having to get approval or install a separate application.</span></span>
    
  
- <span data-ttu-id="2e117-p108">**Работа в автономном режиме:** вы можете перевести внешние типы контента в автономный режим в Outlook 2013. Службы Business Connectivity Services (BCS) предоставляет расширенный кэш и функции автономной работы, а также поддерживает операции на основе кэша. Пользователи могут легко и эффективно работать с внешними данными, даже если они находятся в автономном режиме, а подключение к серверу медленное, нестабильное или недоступно. Операции чтения и записи, выполняемые с кэшированными бизнес-сущностями, синхронизируются, когда подключение к серверу возобновляется.</span><span class="sxs-lookup"><span data-stu-id="2e117-p108">**Enable working offline:** You can take external content types offline in Outlook 2013. Business Connectivity Services (BCS) provides rich cache and offline work features and supports cache-based operations. Users can manipulate external data seamlessly and efficiently, even when they are offline or if the server connectivity is slow, intermittent, or unavailable. The read/write operations performed against cached business entities are synchronized when a connection to the server becomes available.</span></span>
    
  

## <a name="prerequisites-for-working-with-bcs-external-content-types"></a><span data-ttu-id="2e117-128">Необходимые компоненты для работы с внешними типами контента BCS</span><span class="sxs-lookup"><span data-stu-id="2e117-128">Prerequisites for working with BCS external content types</span></span>
<span data-ttu-id="2e117-129"><a name="SP15ectoverview_prereq"> </a></span><span class="sxs-lookup"><span data-stu-id="2e117-129"></span></span>

<span data-ttu-id="2e117-130">Чтобы приступить к созданию внешних типов контента, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="2e117-130">To get started creating external content types, you will need the following:</span></span>
  
    
    

- <span data-ttu-id="2e117-131">SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-131">SharePoint</span></span>
    
  
- <span data-ttu-id="2e117-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2e117-132">Visual Studio 2012</span></span>
    
  
- <span data-ttu-id="2e117-133">Инструменты разработчика Office для Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2e117-133">Office Developer Tools for Visual Studio 2012</span></span>
    
    <span data-ttu-id="2e117-134"> или </span><span class="sxs-lookup"><span data-stu-id="2e117-134">or</span></span>
    
  
- <span data-ttu-id="2e117-135">SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="2e117-135">SharePoint Designer 2013</span></span>
    
  
<span data-ttu-id="2e117-136">Сведения о настройке среды разработки для создания внешних типов контента см. в статье  [Настройка общей среды разработки для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="2e117-136">To set up a development environment for creating external content types, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="what-can-you-do-with-external-content-types"></a><span data-ttu-id="2e117-137">Что можно делать с внешними типами контента?</span><span class="sxs-lookup"><span data-stu-id="2e117-137">What can you do with external content types?</span></span>
<span data-ttu-id="2e117-138"><a name="SP15ectoverview_whattodo"> </a></span><span class="sxs-lookup"><span data-stu-id="2e117-138"></span></span>

<span data-ttu-id="2e117-139">Если SharePoint настроен для взаимодействия с внешней системой, внешние типы контента можно использовать для создания следующих объектов для представления данных:</span><span class="sxs-lookup"><span data-stu-id="2e117-139">When SharePoint is configured to communicate with the external system, you can use the external content types to create the following objects to present the underlying data:</span></span>
  
    
    

- <span data-ttu-id="2e117-140">**Внешние списки**</span><span class="sxs-lookup"><span data-stu-id="2e117-140">**External lists**</span></span>
    
    <span data-ttu-id="2e117-p109">Внешний список предоставляет доступ к данным из внешних систем так же, как и к списку SharePoint. Внешние списки используют внешние типы контента как источники данных. Внешние списки позволяют применять уже определенные метаданные о внешнем типе контента, чтобы создать список SharePoint с внешними данными, который аналогичен любым другим спискам SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e117-p109">An external list enables access to data from external systems in the same way that SharePoint list data is accessed. External lists use external content types as their data sources. External lists enable you to use the metadata that is already defined about an external content type to create a SharePoint list that has external data that looks and performs like any other SharePoint list.</span></span>
    
    <span data-ttu-id="2e117-p110">Вы также можете перевести внешние списки в автономный режим для их использования в Outlook 2013. Это позволяет работать с внешними данными так же, как и с собственными типами элементов Outlook, такими как контакты, задачи и записи, и использовать внешние данные в клиентских приложениях Office.</span><span class="sxs-lookup"><span data-stu-id="2e117-p110">You can also take external lists offline to be used in Outlook 2013. This allows you to work with external data just like native Outlook Item types, such as Contacts, Tasks, and Posts, and use the external data in Office client applications.</span></span>
    
    <span data-ttu-id="2e117-p111">Внешние списки позволяют записывать данные во внешнюю систему, если она это разрешает и внешний тип контента соответствующим образом настроен. Это означает, что пользователи могут редактировать внешние данные напрямую. Любые изменения, внесенные в элементы списка, автоматически синхронизируются с внешней системой. Кроме того, с помощью кнопки **Обновить данные** в списке можно синхронизировать данные вручную и автоматически получить обновленные данные из внешней системы.</span><span class="sxs-lookup"><span data-stu-id="2e117-p111">External lists enable writing back to the external system if the external system allows it, and if it is modeled accordingly by the external content type. This implies that users can edit external data directly from within. Any changes that were made to the items in the list are synchronized automatically with the external system. Also by using the **Refresh data** button in the list, you can synchronize and get updated data from the external system automatically.</span></span>
    
  
- <span data-ttu-id="2e117-150">**Столбцы внешних данных**</span><span class="sxs-lookup"><span data-stu-id="2e117-150">**External Data Columns**</span></span>
    
    <span data-ttu-id="2e117-p112">Столбец внешних данных позволяет пользователям добавлять данные из внешних типов контента в стандартные списки SharePoint. Как и внешние списки, столбцы внешних данных могут отображать данные из любого внешнего типа контента, созданного в Службы Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="2e117-p112">The external data column enables users to add data from external content types to standard SharePoint lists. Just like an external list, external data columns can display data from any external content type that is modeled in Business Connectivity Services (BCS).</span></span>
    
  
- <span data-ttu-id="2e117-153">**Веб-части бизнес-данных**</span><span class="sxs-lookup"><span data-stu-id="2e117-153">**Business Data Web Parts**</span></span>
    
    <span data-ttu-id="2e117-154">SharePoint предоставляет пять различных веб-частей для работы с внешними данными: список бизнес-данных, элемент бизнес-данных, построитель элементов бизнес-данных, список связанных бизнес-данных и действия с бизнес-данными.</span><span class="sxs-lookup"><span data-stu-id="2e117-154">SharePoint provides five different Web Parts for working with external data: Business Data List, Business Data Item, Business Data Item Builder, Business Data Related List, and Business Data Actions.</span></span>
    
  
- <span data-ttu-id="2e117-155">**Средство выбора внешнего типа контента**</span><span class="sxs-lookup"><span data-stu-id="2e117-155">**External Content Type Picker**</span></span>
    
    <span data-ttu-id="2e117-p113">Средство выбора внешнего типа контента предоставляет пользователям набор функций выбора и сопоставления. Его можно встроить в форму или на страницу, если пользователям требуется возможность выбора внешнего типа контента из списка доступных типов.</span><span class="sxs-lookup"><span data-stu-id="2e117-p113">An External Content Type Picker provides picking and resolving functionality to the user. You can embed a picker in a form or page for scenarios where a user should be able to choose an external content type from the list of available external content types.</span></span> 
    
  
- <span data-ttu-id="2e117-158">**Средство выбора внешних элементов**</span><span class="sxs-lookup"><span data-stu-id="2e117-158">**External Item Picker**</span></span>
    
    <span data-ttu-id="2e117-p114">Средство выбора внешних элементов предоставляет возможности выбора и сопоставления внешних элементов на сервере и в расширенных клиентских приложениях Office. Его можно встроить в форму или на страницу, если пользователям требуется возможность выбора внешнего элемента, например клиента, из списка клиентов.</span><span class="sxs-lookup"><span data-stu-id="2e117-p114">An External Item Picker provides picking and resolving functionality for external items on the server and in rich-client Office applications. You can embed a picker in a form or page for scenarios where a user should be able to pick an external item, such as a customer from a list of customers.</span></span> 
    
  
- <span data-ttu-id="2e117-161">**Страницы профилей**</span><span class="sxs-lookup"><span data-stu-id="2e117-161">**Profile Pages**</span></span>
    
    <span data-ttu-id="2e117-p115">Страницы профиля  это страницы SharePoint в SharePoint, на которых отображаются подробные сведения о внешнем элементе. Как и любые другие Страница "Веб-части" SharePoint, эту страницу можно настроить для отображения сведений о внешнем элементе.</span><span class="sxs-lookup"><span data-stu-id="2e117-p115">Profile Pages are SharePoint pages in SharePoint that display the details about an external item. Just like any other SharePoint Web Parts page, you can customize this page to show details of an external item.</span></span>
    
  
- <span data-ttu-id="2e117-164">**Настраиваемые страницы и приложения**</span><span class="sxs-lookup"><span data-stu-id="2e117-164">**Custom pages and applications**</span></span>
    
    <span data-ttu-id="2e117-165">Вы можете использовать средства программирования SharePoint, например объектную модель SharePoint, клиентскую объектную модель и URL-адреса REST.</span><span class="sxs-lookup"><span data-stu-id="2e117-165">You can use the SharePoint programmability options, such as the SharePoint object model, client object model, and Representational State Transfer (REST) URLs.</span></span>
    
  
<span data-ttu-id="2e117-166">В таблице 1 представлены примеры задач, которые иллюстрируется работу с внешними типами контента.</span><span class="sxs-lookup"><span data-stu-id="2e117-166">Table 1 contains examples of tasks that illustrate working with external content types.</span></span>
  
    
    

<span data-ttu-id="2e117-167">**Таблица 1. Основные задачи по работе с внешними типами контента**</span><span class="sxs-lookup"><span data-stu-id="2e117-167">**Table 1. Basic tasks for working with external content types**</span></span>


|<span data-ttu-id="2e117-168">**Задача**</span><span class="sxs-lookup"><span data-stu-id="2e117-168">**Task**</span></span>|<span data-ttu-id="2e117-169">**Описание**</span><span class="sxs-lookup"><span data-stu-id="2e117-169">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="2e117-170">Как: создать внешний тип контента из источника OData в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-170">How to: Create an external content type from an OData source in SharePoint</span></span>](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |<span data-ttu-id="2e117-171">Узнайте, как использовать Visual Studio 2012 для обнаружения опубликованных источников OData и создания внешнего типа контента для многократного использования в SharePoint Службы Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="2e117-171">Learn how to use Visual Studio 2012 to discover a published OData source, and create a reusable external content type for use in SharePoint Business Connectivity Services (BCS).</span></span>  <br/> |
| [<span data-ttu-id="2e117-172">Инструкции. Создание внешних типов контента для SQL Server в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-172">How to: Create external content types for SQL Server in SharePoint</span></span>](how-to-create-external-content-types-for-sql-server-in-sharepoint.md) <br/> |<span data-ttu-id="2e117-173">Узнайте, как создать внешний тип контента на основе базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e117-173">Learn how to create an external content type based on a SQL Server database.</span></span>  <br/> |
   

## <a name="additional-resources"></a><span data-ttu-id="2e117-174">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2e117-174">Additional resources</span></span>
<span data-ttu-id="2e117-175"><a name="SP15ectoverview_addres"> </a></span><span class="sxs-lookup"><span data-stu-id="2e117-175"></span></span>


-  [<span data-ttu-id="2e117-176">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-176">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2e117-177">Как: создание добавить в пределах внешнего типа контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-177">How to: Create an add-in-scoped external content type in SharePoint</span></span>](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2e117-178">Инструкции. Создание внешних типов контента для SQL Server в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-178">How to: Create external content types for SQL Server in SharePoint</span></span>](how-to-create-external-content-types-for-sql-server-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2e117-179">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-179">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="2e117-180">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2e117-180">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  

