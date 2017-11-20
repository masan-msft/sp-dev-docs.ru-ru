---
title: "Изменения в SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f1cd30c9-9a73-428d-9151-f1813b43b020
ms.openlocfilehash: e336ccd9ad1a257ffa3c8bb44ed3b4933c8784ea
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="whats-changed-in-sharepoint-designer-2013"></a><span data-ttu-id="2333d-102">Изменения в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="2333d-102">What's changed in SharePoint Designer 2013</span></span>
<span data-ttu-id="2333d-p101">Узнайте о возможностях, которые устарели или удалены из SharePoint Designer 2013. Устаревшие возможности включены в выпуск SharePoint для совместимости с предыдущими версиями продуктов, но они будут удалены из будущих версий.</span><span class="sxs-lookup"><span data-stu-id="2333d-p101">Learn about features that are deprecated in or removed from SharePoint Designer 2013. Features that are deprecated are included in the SharePoint release for compatibility with previous product versions but will be removed from future versions.</span></span>
## <a name="discontinued-features-in-sharepoint-designer-2013"></a><span data-ttu-id="2333d-105">Неподдерживаемые возможности в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="2333d-105">Discontinued features in SharePoint Designer 2013</span></span>
<span data-ttu-id="2333d-106"><a name="WhatsChangedSharePointDesigner2013_DiscontinuedFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="2333d-106"></span></span>

<span data-ttu-id="2333d-107">Следующие возможности устарели или были удалены из SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="2333d-107">The following features are deprecated in SharePoint Designer 2013 or have been removed.</span></span>
  
    
    

### <a name="sharepoint-2010-workflow-platform"></a><span data-ttu-id="2333d-108">Платформа рабочих процессов SharePoint 2010</span><span class="sxs-lookup"><span data-stu-id="2333d-108">SharePoint 2010 Workflow platform</span></span>
<span data-ttu-id="2333d-109"><a name="WhatsChangedSharePointDesigner2013_WorkflowPlatform"> </a></span><span class="sxs-lookup"><span data-stu-id="2333d-109"></span></span>

 <span data-ttu-id="2333d-p102">**Описание изменения.** Некоторые возможности платформы рабочих процессов SharePoint 2010, которые зависят от Windows Workflow Foundation 3.0, устарели в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2333d-p102">**Description of the change.** Some features of the SharePoint 2010 Workflow platform that are dependent on Windows Workflow Foundation 3.0 are deprecated in SharePoint.</span></span>
  
    
    
 <span data-ttu-id="2333d-112">**Причина изменения.** В SharePoint представлена новая платформа рабочих процессов SharePoint, которая основана на Windows Workflow Foundation 4.0 и интегрирована с Workflow Manager 1.0.</span><span class="sxs-lookup"><span data-stu-id="2333d-112">**Reason for the change.** SharePoint introduces a new SharePoint Workflow platform that is built upon Windows Workflow Foundation 4.0 and that is integrated with Workflow Manager 1.0.</span></span>
  
    
    
 <span data-ttu-id="2333d-p103">**Путь миграции.** В SharePoint Designer 2013 по-прежнему можно создавать рабочие процессы SharePoint 2010 и использовать все возможности рабочих процессов SharePoint 2010, выбрав платформу рабочих процессов SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="2333d-p103">**Migration path.** In SharePoint Designer 2013, you can still create a SharePoint 2010 Workflow and use all of the SharePoint 2010 Workflow features by choosing the SharePoint 2010 Workflow platform.</span></span>
  
    
    
<span data-ttu-id="2333d-p104">Вы также можете интегрировать функции платформы рабочих процессов SharePoint 2010 в новой платформе рабочих процессов SharePoint. Для этого создайте рабочий процесс SharePoint 2010, выбрав платформу рабочих процессов SharePoint 2010. Затем создайте рабочий процесс SharePoint, выбрав платформу рабочих процессов SharePoint. Используйте действия **Запустить рабочий процесс списка** и **Запустить рабочий процесс сайта** в рабочем процессе SharePoint, чтобы вызвать рабочий процесс SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="2333d-p104">You can also integrate features from the SharePoint 2010 Workflow platform into the new SharePoint Workflow platform. To do this, create a SharePoint 2010 Workflow by choosing the SharePoint 2010 Workflow platform; create a SharePoint Workflow by choosing the SharePoint Workflow platform; and then use the **Start a list workflow** and **Start a site workflow** actions in the SharePoint Workflow to call the SharePoint 2010 Workflow.</span></span>
  
    
    
<span data-ttu-id="2333d-117">Следующие возможности доступны только на платформе рабочих процессов SharePoint 2010.</span><span class="sxs-lookup"><span data-stu-id="2333d-117">The following features are available only on the SharePoint 2010 Workflow platform:</span></span>
  
    
    

- <span data-ttu-id="2333d-118">Действия:</span><span class="sxs-lookup"><span data-stu-id="2333d-118">Actions:</span></span>
    
  - <span data-ttu-id="2333d-119">Остановить рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="2333d-119">Stop Workflow</span></span>
    
  
  - <span data-ttu-id="2333d-120">Записать версию набора документов</span><span class="sxs-lookup"><span data-stu-id="2333d-120">Capture a Version of the Document Set</span></span>
    
  
  - <span data-ttu-id="2333d-121">Отправить набор документов в репозиторий</span><span class="sxs-lookup"><span data-stu-id="2333d-121">Send Document Set to Repository</span></span>
    
  
  - <span data-ttu-id="2333d-122">Задать состояние утверждения контента для набора документов</span><span class="sxs-lookup"><span data-stu-id="2333d-122">Set Content Approval Status for the Document Set</span></span>
    
  
  - <span data-ttu-id="2333d-123">Начать процесс утверждения набора документов</span><span class="sxs-lookup"><span data-stu-id="2333d-123">Start Document Set Approval Process</span></span>
    
  
  - <span data-ttu-id="2333d-124">Объявить запись</span><span class="sxs-lookup"><span data-stu-id="2333d-124">Declare Record</span></span>
    
  
  - <span data-ttu-id="2333d-125">Изменить состояние утверждения контента</span><span class="sxs-lookup"><span data-stu-id="2333d-125">Set Content Approval Status</span></span>
    
  
  - <span data-ttu-id="2333d-126">Отменить объявление записи</span><span class="sxs-lookup"><span data-stu-id="2333d-126">Undeclare Record</span></span>
    
  
  - <span data-ttu-id="2333d-127">Добавить элемент списка</span><span class="sxs-lookup"><span data-stu-id="2333d-127">Add List Item</span></span> 
    
  
  - <span data-ttu-id="2333d-128">Наследование родительских разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="2333d-128">Inherit List Item Parent Permissions</span></span>
    
  
  - <span data-ttu-id="2333d-129">Удалить разрешения для элемента списка</span><span class="sxs-lookup"><span data-stu-id="2333d-129">Remove List Item Permissions</span></span>
    
  
  - <span data-ttu-id="2333d-130">Заменить разрешения для элемента списка</span><span class="sxs-lookup"><span data-stu-id="2333d-130">Replace List Item Permissions</span></span>
    
  
  - <span data-ttu-id="2333d-131">Найти руководителя для пользователя</span><span class="sxs-lookup"><span data-stu-id="2333d-131">Lookup Manager of a User</span></span>
    
  
  - <span data-ttu-id="2333d-132">Назначить форму группе</span><span class="sxs-lookup"><span data-stu-id="2333d-132">Assign a Form to a Group</span></span>
    
  
  - <span data-ttu-id="2333d-133">Назначить элемент списка дел</span><span class="sxs-lookup"><span data-stu-id="2333d-133">Assign a To-Do Item</span></span>
    
  
  - <span data-ttu-id="2333d-134">Получить данные от пользователя</span><span class="sxs-lookup"><span data-stu-id="2333d-134">Collect Data from a User</span></span>
    
  
  - <span data-ttu-id="2333d-135">Начать процесс утверждения</span><span class="sxs-lookup"><span data-stu-id="2333d-135">Start Approval Process</span></span>
    
  
  - <span data-ttu-id="2333d-136">Начать настраиваемый рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="2333d-136">Start Custom Task Process</span></span>
    
  
  - <span data-ttu-id="2333d-137">Начать процесс сбора отзывов</span><span class="sxs-lookup"><span data-stu-id="2333d-137">Start Feedback Process</span></span>
    
  
  - <span data-ttu-id="2333d-138">Копировать элемент списка (SharePoint Designer 2013 поддерживает только действие копирование документа)</span><span class="sxs-lookup"><span data-stu-id="2333d-138">Copy List Item (SharePoint Designer 2013 supports only the document-copying action.)</span></span>
    
  
- <span data-ttu-id="2333d-139">Условия:</span><span class="sxs-lookup"><span data-stu-id="2333d-139">Conditions:</span></span>
    
  - <span data-ttu-id="2333d-140">Если текущее поле элемента равно значению</span><span class="sxs-lookup"><span data-stu-id="2333d-140">If current item field equals value</span></span>
    
  
  - <span data-ttu-id="2333d-141">Проверка уровней разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="2333d-141">Check list item permission levels</span></span>
    
  
  - <span data-ttu-id="2333d-142">Проверка разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="2333d-142">Check list item permissions</span></span>
    
  
- <span data-ttu-id="2333d-143">Шаги:</span><span class="sxs-lookup"><span data-stu-id="2333d-143">Steps:</span></span>
    
  - <span data-ttu-id="2333d-144">Шаг олицетворения</span><span class="sxs-lookup"><span data-stu-id="2333d-144">Impersonation Step:</span></span>
    
  
- <span data-ttu-id="2333d-145">Источники данных:</span><span class="sxs-lookup"><span data-stu-id="2333d-145">Data sources:</span></span>
    
  - <span data-ttu-id="2333d-146">Поиск профиля пользователя</span><span class="sxs-lookup"><span data-stu-id="2333d-146">User Profile lookup</span></span>
    
  
- <span data-ttu-id="2333d-147">Другие возможности:</span><span class="sxs-lookup"><span data-stu-id="2333d-147">Other features:</span></span>
    
  - <span data-ttu-id="2333d-148">Интеграция с Visio</span><span class="sxs-lookup"><span data-stu-id="2333d-148">Visio integration</span></span>
    
  
  - <span data-ttu-id="2333d-149">Столбец связи</span><span class="sxs-lookup"><span data-stu-id="2333d-149">Association Column</span></span>
    
  
  - <span data-ttu-id="2333d-150">Связь с типом контента для рабочего процесса для повторного использования</span><span class="sxs-lookup"><span data-stu-id="2333d-150">Content Type Association for reusable workflow</span></span>
    
  
  - <span data-ttu-id="2333d-151">Функция "Требуются разрешения на управление списками" или "Требуются разрешения на управление веб-сайтом" для рабочего процесса списка или сайта</span><span class="sxs-lookup"><span data-stu-id="2333d-151">'Require Manage List/Web Permission' feature for list/site workflow</span></span>
    
  
  - <span data-ttu-id="2333d-152">Тип глобального рабочего процесса для повторного использования</span><span class="sxs-lookup"><span data-stu-id="2333d-152">Globally reusable workflow type</span></span>
    
  
  - <span data-ttu-id="2333d-153">Возможность визуализации рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="2333d-153">Workflow visualization option</span></span>
    
  

### <a name="sharepoint-page-design-features"></a><span data-ttu-id="2333d-154">Возможности проектирования страниц SharePoint</span><span class="sxs-lookup"><span data-stu-id="2333d-154">SharePoint page-design features</span></span>
<span data-ttu-id="2333d-155"><a name="WhatsChangedSharePointDesigner2013_PageDesignFeatures"> </a></span><span class="sxs-lookup"><span data-stu-id="2333d-155"></span></span>

<span data-ttu-id="2333d-156">Следующая возможность недоступна в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2333d-156">The following feature is not available in SharePoint.</span></span>
  
    
    

#### <a name="design-view-and-split-view"></a><span data-ttu-id="2333d-157">Конструктор и комбинированный режим</span><span class="sxs-lookup"><span data-stu-id="2333d-157">Design view and Split view</span></span>
<span data-ttu-id="2333d-158"><a name="WhatsChangedSharePointDesigner2013_DesignViewSplitView"> </a></span><span class="sxs-lookup"><span data-stu-id="2333d-158"></span></span>

 <span data-ttu-id="2333d-159">**Описание изменения.** SharePoint Designer 2010 содержит три представления для редактирования страниц HTML и ASPX: представление кода, "Конструктор" и комбинированный режим.</span><span class="sxs-lookup"><span data-stu-id="2333d-159">**Description of the change.**SharePoint Designer 2010 has three views for editing HTML and ASPX pages: Code view, Design view, and Split view.</span></span> <span data-ttu-id="2333d-160">"Конструктор" и комбинированный режим удалены из SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="2333d-160">Design view and Split view are removed from SharePoint Designer 2013.</span></span> <span data-ttu-id="2333d-161">Удаление представления "Конструктор" и комбинированного режима влияет на функции SharePoint Designer 2013, используемые для редактирования веб-частей и эталонных страниц.</span><span class="sxs-lookup"><span data-stu-id="2333d-161">The removal of Design view and Split view affects the features of SharePoint Designer 2013 that are used for editing Web Parts and master pages.</span></span> <span data-ttu-id="2333d-162">Если вы редактируете страницы в SharePoint Designer 2013, необходимо использовать представление кода.</span><span class="sxs-lookup"><span data-stu-id="2333d-162">If you edit pages in SharePoint Designer 2013, you must use Code view.</span></span>
  
    
    
 <span data-ttu-id="2333d-p106">**Причина изменения.** По сравнению с текущими версиями Internet Explorer конструктор  это более старая технология, которая не поддерживает множество новых тегов HTML5 и CSS.</span><span class="sxs-lookup"><span data-stu-id="2333d-p106">**Reason for the change.** Compared to current versions of Internet Explorer, Design view is an older technology that does not support many new HTML5 and CSS tags.</span></span>
  
    
    
 <span data-ttu-id="2333d-p107">**Путь миграции.** Если вы изменили страницы в представлении кода, можно нажать клавишу **F12** для предварительного просмотра страницы в браузере. Или же можно использовать Visual Studio для редактирования страницы.</span><span class="sxs-lookup"><span data-stu-id="2333d-p107">**Migration path.** If you edit pages in Code view, you can press **F12** to preview the page in the browser. Alternatively, you can use Visual Studio to edit pages.</span></span>
  
    
    
<span data-ttu-id="2333d-168">Если вы хотите создать визуальное оформление или фирменный стиль сайта в режиме WYSIWYG (режиме точного отображения), можно использовать любой профессиональный редактор HTML, например Microsoft Expression Web.</span><span class="sxs-lookup"><span data-stu-id="2333d-168">If you want to visually design or brand your site, and you want a WYSIWYG ("what you see is what you get") page-editing experience, you can use any professional HTML editor, such as Microsoft Expression Web. Then you can import your HTML files into sps15short by using the new Design Manager, which is a feature included in publishing sites, such as the Publishing Portal Site Collection site template.</span></span> <span data-ttu-id="2333d-169">Затем вы можете импортировать HTML-файлы в SharePoint с помощью "Дизайнера" — компонента, доступного на сайтах публикации, например в шаблоне "Семейство веб-сайтов портала публикации".</span><span class="sxs-lookup"><span data-stu-id="2333d-169">If you want to visually design or brand your site, and you want a WYSIWYG ("what you see is what you get") page-editing experience, you can use any professional HTML editor, such as Microsoft Expression Web. Then you can import your HTML files into SharePoint Server 2013 by using the new Design Manager, which is a feature included in publishing sites, such as the Publishing Portal Site Collection site template.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="2333d-170">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="2333d-170">Additional resources</span></span>
<span data-ttu-id="2333d-171"><a name="WhatsChangedSharePointDesigner2013_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="2333d-171"></span></span>


-  [<span data-ttu-id="2333d-172">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="2333d-172">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="2333d-173">Отличия SharePoint 2010 от SharePoint</span><span class="sxs-lookup"><span data-stu-id="2333d-173">Changes from SharePoint 2010 to SharePoint</span></span>](http://technet.microsoft.com/ru-RU/library/ff607742%28v=office.15%29.aspx)
    
  
-  [<span data-ttu-id="2333d-174">Новые возможности рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="2333d-174">What's new in workflow in SharePoint Server 2013</span></span>](http://technet.microsoft.com/ru-RU/library/jj219638%28v=office.15%29.aspx)
    
  

  
    
    

