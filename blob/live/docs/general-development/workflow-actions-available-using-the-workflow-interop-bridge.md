---
title: "Действия рабочего процесса можно получить с моста взаимодействия рабочих процессов"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: a8903440-ff8f-41a4-8c2a-5dbe12c07cfb
ms.openlocfilehash: 1fcc19e690fbc662b8bea46949c698b82967f882
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="workflow-actions-available-using-the-workflow-interop-bridge"></a><span data-ttu-id="40a4a-102">Действия рабочего процесса можно получить с моста взаимодействия рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="40a4a-102">Workflow actions available using the workflow interop bridge</span></span>
<span data-ttu-id="40a4a-103">Содержит краткий список действий рабочих процессов в SharePoint 2010, доступные для рабочих процессов SharePoint с помощью моста взаимодействия рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="40a4a-103">Contains a concise list of workflow actions in SharePoint 2010 that are available to SharePoint workflows by using the workflow interop bridge.</span></span>
## <a name="workflow-actions-for-the-interop-bridge"></a><span data-ttu-id="40a4a-104">Действия рабочего процесса для моста взаимодействия</span><span class="sxs-lookup"><span data-stu-id="40a4a-104">Workflow actions for the interop bridge</span></span>
<span data-ttu-id="40a4a-105"><a name="bkm_wfactions"> </a></span><span class="sxs-lookup"><span data-stu-id="40a4a-105"><a name="bkm_wfactions"> </a></span></span>

<span data-ttu-id="40a4a-106">Инфраструктура рабочих процессов SharePoint построен на Windows Workflow Foundation (WF) 4 и таким образом выполняется рабочих процессов в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="40a4a-106">The SharePoint workflow infrastructure is built on Windows Workflow Foundation (WF) 4 and therefore executes workflows in Microsoft Azure.</span></span> <span data-ttu-id="40a4a-107">По этой причине некоторые действия из рабочих процессов SharePoint 2010 доступны в SharePoint, только при использовании [взаимодействия рабочих процессов SharePoint ](sharepoint-workflow-fundamentals.md#bkm_InteropBridge).</span><span class="sxs-lookup"><span data-stu-id="40a4a-107">For this reason, some actions from SharePoint 2010 workflows are available in SharePoint only when using the  [SharePoint workflow interop ](sharepoint-workflow-fundamentals.md#bkm_InteropBridge).</span></span> 
  
    
    
<span data-ttu-id="40a4a-108">Перечисленные ниже действия, доступны только при использовании моста взаимодействия рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="40a4a-108">The following actions are available only when you use the workflow interop bridge.</span></span>
  
    
    

- <span data-ttu-id="40a4a-109">Добавить разрешения для элемента списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-109">Add List Item Permissions</span></span>
    
  
- <span data-ttu-id="40a4a-110">Назначить форму группе</span><span class="sxs-lookup"><span data-stu-id="40a4a-110">Assign a Form to a Group</span></span>
    
  
- <span data-ttu-id="40a4a-111">Назначить элемент списка дел</span><span class="sxs-lookup"><span data-stu-id="40a4a-111">Assign a To-do Item</span></span>
    
  
- <span data-ttu-id="40a4a-112">Записать версию набора документов</span><span class="sxs-lookup"><span data-stu-id="40a4a-112">Capture a version of the Document Set</span></span>
    
  
- <span data-ttu-id="40a4a-113">Получить данные от пользователя</span><span class="sxs-lookup"><span data-stu-id="40a4a-113">Collect Data from a User</span></span>
    
  
- <span data-ttu-id="40a4a-114">Копировать элемент списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-114">Copy List Item</span></span>
    
  
- <span data-ttu-id="40a4a-115">Объявить запись</span><span class="sxs-lookup"><span data-stu-id="40a4a-115">Declare Record</span></span>
    
  
- <span data-ttu-id="40a4a-116">Наследование родительских разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-116">Inherit List Item Parent Permissions</span></span>
    
  
- <span data-ttu-id="40a4a-117">Найти руководителя для пользователя</span><span class="sxs-lookup"><span data-stu-id="40a4a-117">Lookup Manager of a User</span></span>
    
  
- <span data-ttu-id="40a4a-118">Удалить разрешения для элемента списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-118">Remove List Item Permissions</span></span>
    
  
- <span data-ttu-id="40a4a-119">Заменить разрешения для элемента списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-119">Replace List Item Permissions</span></span>
    
  
- <span data-ttu-id="40a4a-120">Отправить набор документов в репозиторий</span><span class="sxs-lookup"><span data-stu-id="40a4a-120">Send Document Set to Repository</span></span>
    
  
- <span data-ttu-id="40a4a-121">Изменить состояние утверждения контента</span><span class="sxs-lookup"><span data-stu-id="40a4a-121">Set Content Approval Status</span></span>
    
  
- <span data-ttu-id="40a4a-122">Задать состояние утверждения контента для набора документов</span><span class="sxs-lookup"><span data-stu-id="40a4a-122">Set Content Approval Status for the Document Set</span></span>
    
  
- <span data-ttu-id="40a4a-123">Задать состояние рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="40a4a-123">Set Workflow Status</span></span>
    
  
- <span data-ttu-id="40a4a-124">Начать процесс утверждения</span><span class="sxs-lookup"><span data-stu-id="40a4a-124">Start Approval Process</span></span>
    
  
- <span data-ttu-id="40a4a-125">Начать настраиваемый рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="40a4a-125">Start Custom Task Process</span></span>
    
  
- <span data-ttu-id="40a4a-126">Начать процесс утверждения набора документов</span><span class="sxs-lookup"><span data-stu-id="40a4a-126">Start Document Set Approval Process</span></span>
    
  
- <span data-ttu-id="40a4a-127">Начать процесс сбора отзывов</span><span class="sxs-lookup"><span data-stu-id="40a4a-127">Start Feedback Process</span></span>
    
  
- <span data-ttu-id="40a4a-128">Отменить объявление записи</span><span class="sxs-lookup"><span data-stu-id="40a4a-128">Undeclare Record</span></span>
    
  

## <a name="conditions-and-blocks"></a><span data-ttu-id="40a4a-129">Условия и блоки</span><span class="sxs-lookup"><span data-stu-id="40a4a-129">Conditions and blocks</span></span>
<span data-ttu-id="40a4a-130"><a name="bkm_wfconditions"> </a></span><span class="sxs-lookup"><span data-stu-id="40a4a-130"><a name="bkm_wfconditions"> </a></span></span>

 <span data-ttu-id="40a4a-131">**Условия:**</span><span class="sxs-lookup"><span data-stu-id="40a4a-131">**Conditions**</span></span>
  
    
    

- <span data-ttu-id="40a4a-132">Если текущее поле элемента равно значению</span><span class="sxs-lookup"><span data-stu-id="40a4a-132">If current item field equals value</span></span>
    
  
- <span data-ttu-id="40a4a-133">Проверка уровней разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-133">Check list item permission levels</span></span>
    
  
- <span data-ttu-id="40a4a-134">Проверка разрешений для элемента списка</span><span class="sxs-lookup"><span data-stu-id="40a4a-134">Check list item permissions</span></span>
    
  
 <span data-ttu-id="40a4a-135">**Блоки**</span><span class="sxs-lookup"><span data-stu-id="40a4a-135">**Blocks**</span></span>
  
    
    

- <span data-ttu-id="40a4a-136">Блокировать олицетворения</span><span class="sxs-lookup"><span data-stu-id="40a4a-136">Impersonation block</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="40a4a-137">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="40a4a-137">Additional resources</span></span>
<span data-ttu-id="40a4a-138"><a name="bkm_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="40a4a-138"><a name="bkm_addlresources"> </a></span></span>


-  [<span data-ttu-id="40a4a-139">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="40a4a-139">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [<span data-ttu-id="40a4a-140">Взаимодействие рабочих процессов SharePoint </span><span class="sxs-lookup"><span data-stu-id="40a4a-140">SharePoint workflow interop </span></span>](sharepoint-workflow-fundamentals.md#bkm_InteropBridge)
    
  
-  [<span data-ttu-id="40a4a-141">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="40a4a-141">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="40a4a-142">Установка и настройка диспетчера рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="40a4a-142">Set up and configure SharePoint Workflow Manager</span></span>](set-up-and-configure-sharepoint-workflow-manager.md)
    
  

