---
title: "Общие сведения о действия с событиями в SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fe4ad8cf-2c6f-488d-8b33-6bf4357018ac
ms.openlocfilehash: 07ec3fe8c0a131b9f5a87df55e5745a664aba825
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="understanding-eventing-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="4e56c-102">Общие сведения о действия с событиями в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="4e56c-102">Understanding Eventing Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="4e56c-103">Изучите использование действия с событиями в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="4e56c-103">Learn to use Eventing Actions in SharePoint Designer 2013.</span></span>
## <a name="overview-of-eventing-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="4e56c-104">Общие сведения о действия с событиями в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="4e56c-104">Overview of Eventing Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="4e56c-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="4e56c-105"></span></span>

<span data-ttu-id="4e56c-p101">Рабочий процесс SharePoint можно подписаться на уведомления, когда сообщение добавлены или изменены. Элемент добавлены или изменены, называется события. Рабочий процесс можно подождать эти события происходить перед тем как продолжить с рабочим процессом. Действия с событиями в SharePoint Designer 2013 являются:</span><span class="sxs-lookup"><span data-stu-id="4e56c-p101">A SharePoint workflow can subscribe to be notified when an item is added or changed. When an item is added or changed, it is called an event. A workflow can wait for these events to happen before proceeding with the workflow. The Eventing actions in SharePoint Designer 2013 are:</span></span> 
  
    
    

- <span data-ttu-id="4e56c-110">**Ожидание события в элемент списка:** Используется для ожидания новый элемент, чтобы создать или изменить элемент.</span><span class="sxs-lookup"><span data-stu-id="4e56c-110">**Wait for Event in List Item:** Used to wait for a new item to be created or an item to be changed.</span></span>
    
  
- <span data-ttu-id="4e56c-111">**Ожидание события проекта:** Используется для ожидания для возврата, фиксации или отправки проекта.</span><span class="sxs-lookup"><span data-stu-id="4e56c-111">**Wait for Project Event:** Used to wait for a project to be checked in, committed, or submitted.</span></span>
    
  
- <span data-ttu-id="4e56c-112">**Ждать изменения поля в текущем элементе:** Используется для ожидания для поля должен быть изменен в текущем элементе.</span><span class="sxs-lookup"><span data-stu-id="4e56c-112">**Wait for Field Change in Current Item:** Used to wait for a field to be changed in the current item.</span></span>
    
  
<span data-ttu-id="4e56c-113">Действия событий осуществляется в ленте SharePoint Designer 2013, как показано на рисунках в меню **Действие**.</span><span class="sxs-lookup"><span data-stu-id="4e56c-113">The Eventing actions are accessed in the **Action** drop-down menu of the SharePoint Designer 2013 ribbon as shown in the figures.</span></span>
  
> [!NOTE] 
> <span data-ttu-id="4e56c-114">[!Примечание] **Project Web App действий** доступны только при работе с сайта Project Web App.</span><span class="sxs-lookup"><span data-stu-id="4e56c-114">The **Project Web App Actions** are only available when working with a Project Web App site.</span></span>
  
    
    


<span data-ttu-id="4e56c-115">**Действие события в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="4e56c-115">**Eventing Action in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Действия событий в SharePoint Designer 2013](../images/SPD15-EventingActions1.png)
  
    
    

<span data-ttu-id="4e56c-117">**Действие события Project Web App в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="4e56c-117">**Project Web App Eventing Action in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Выбор действия события проекта](../images/SPD15-EventingActions4.png)
  
    
    

<span data-ttu-id="4e56c-119">**Ждать изменения поля в текущем элементе событий в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="4e56c-119">**Wait for Field Change in Current Item event in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Выбор "Ждать изменения поля" в текущем элементе.](../images/wf15-eventingactions3.png)
  
    
    

  
    
    

  
    
    

## <a name="using-eventing-actions-in-sharepoint"></a><span data-ttu-id="4e56c-121">С помощью действия с событиями в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e56c-121">Using Eventing Actions in SharePoint</span></span>
<span data-ttu-id="4e56c-122"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="4e56c-122"></span></span>

<span data-ttu-id="4e56c-p102">Рабочий процесс управляет бизнес-процессов. Бизнес-процесса важно часто вынуждены ждать освобождения элемента для добавления или обновления в списке SharePoint. С помощью действия событий можно подождать событие происходит и выполните действия рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="4e56c-p102">A workflow orchestrates business processes. In a business process it is often important to wait for an item to be added or updated in a SharePoint list. Using the Eventing actions you can wait for an event to happen and then perform a workflow action.</span></span>
  
    
    
<span data-ttu-id="4e56c-p103">Действия событий, находятся в раскрывающемся меню действия на ленте SharePoint Designer 2013. Можно добавить действие в рабочий процесс и его настройки для определенных обстоятельствах.</span><span class="sxs-lookup"><span data-stu-id="4e56c-p103">The Eventing actions are located on the Actions drop-down menu in the SharePoint Designer 2013 ribbon. You can add the action to your workflow and then customize it for your particular circumstance.</span></span>
  
    
    

### <a name="wait-for-event-in-list-item"></a><span data-ttu-id="4e56c-128">Подождать появления события в элементе списка</span><span class="sxs-lookup"><span data-stu-id="4e56c-128">Wait for Event in List Item</span></span>

<span data-ttu-id="4e56c-129">**Ожидание события в элемент списка** действие содержит две редактируемые области, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="4e56c-129">The **Wait for Event in List Item** action contains two editable regions, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="4e56c-130">**Подождать появления события в элементе списка**</span><span class="sxs-lookup"><span data-stu-id="4e56c-130">**Wait for Event in List Item**</span></span>

  
    
    

  
    
    
![Ожидание действия события в SharePoint Designer 2013](../images/SPD15-EventingActions2.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="4e56c-132">Две редактируемые области являются:</span><span class="sxs-lookup"><span data-stu-id="4e56c-132">The two editable regions are:</span></span>
  
    
    

- <span data-ttu-id="4e56c-133">**Это событие элемента:** Список и события, которое будут отслеживаться.</span><span class="sxs-lookup"><span data-stu-id="4e56c-133">**This item event:** The list and event that will be monitored.</span></span>
    
  
- <span data-ttu-id="4e56c-p104">**Выходной переменной:** Переменная, в котором следует сохранить GUID элемента, из которого произошло событие. Элементы содержат идентификатор и поля GUID. Идентификатор является уникальным для списка и глобальный уникальный идентификатор GUID. Например идентификатор первый элемент в списке будет номер 1 и идентификатор второго элемента будет номер 2. Идентификатор GUID глобальный уникальный и в формате значение 128-бит, состоящее из 8 шестнадцатеричных цифр, следуют три группы 4 шестнадцатеричных цифр, а затем по одной группе 12 шестнадцатеричных цифр. Идентификатор GUID, например: 6B29FC40-CA47-1067-B31D-00DD010662DA. **Ожидание события в элемент списка** действие извлекает идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="4e56c-p104">**Output variable:** A variable in which to save the GUID of the item from which the event originated. Items have both an ID and a GUID field. The ID is unique to the list and a GUID is globally unique. For example, the ID of the first item in the list will be the number 1 and the ID of the second item will be the number 2. The GUID is globally unique and in the format of a 128-bit value consisting of 8 hexadecimal digits, followed by three groups of 4 hexadecimal digits each, followed by one group of 12 hexadecimal digits. An example of a GUID is: 6B29FC40-CA47-1067-B31D-00DD010662DA. The **Wait for Event in List Item** action retrieves the GUID.</span></span>
    
  
<span data-ttu-id="4e56c-141">Щелкнув ссылку **это событие элемента** открывает диалоговое окно **Выбор события элемента списка**, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="4e56c-141">Clicking the **this item event** link opens the **Choose List Item Event** dialog box, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="4e56c-142">**Выберите диалоговое окно события элемента списка**</span><span class="sxs-lookup"><span data-stu-id="4e56c-142">**Choose List Item Event dialog box**</span></span>

  
    
    

  
    
    
![Диалоговое окно "Выбор события элемента списка"](../images/SPD15-EventingActions3.jpg)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="4e56c-p105">Тип события, соответствует раскрывающегося списка **событий**. Параметры, следует ожидать в элемент добавляется в список или дождитесь элемент, чтобы изменить в список. В раскрывающемся **списке** соответствует списка, за которым ведется наблюдение.</span><span class="sxs-lookup"><span data-stu-id="4e56c-p105">The **Event** drop-down list corresponds to the type of event. The options are to wait for an item to be added to a list or to wait for an item to be changed in a list. The **List** drop-down corresponds to the list that is monitored.</span></span>
  
    
    

### <a name="wait-for-project-event"></a><span data-ttu-id="4e56c-147">Подождите наступления события проекта</span><span class="sxs-lookup"><span data-stu-id="4e56c-147">Wait for Project Event</span></span>

<span data-ttu-id="4e56c-148">Действие **Ожидание события проекта** содержит один редактируемой области, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="4e56c-148">The **Wait for Project Event** action contains one editable region, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="4e56c-149">**Подождите наступления события проекта**</span><span class="sxs-lookup"><span data-stu-id="4e56c-149">**Wait for Project Event**</span></span>

  
    
    

  
    
    
![Ожидание события проекта в рабочем процессе](../images/SPD15-EventingActions5.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="4e56c-151"> Это редактируемой области:</span><span class="sxs-lookup"><span data-stu-id="4e56c-151">The editable region is:</span></span>
  
    
    

- <span data-ttu-id="4e56c-152">**Это событие проекта:** События project, которая должна ожидать рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="4e56c-152">**This project event:** The project event that the workflow should wait for.</span></span>
    
  
<span data-ttu-id="4e56c-p106">В раскрывающемся списке **это событие project** включает в себя три события проекта, из которых можно выбрать. К ним относятся ожидание проект, чтобы вернуть, фиксации или отправки.</span><span class="sxs-lookup"><span data-stu-id="4e56c-p106">The **This project event** drop-down includes three project events to choose from. These include waiting for the project to be checked in, committed, or submitted.</span></span>
  
    
    
<span data-ttu-id="4e56c-155">После обработки события рабочего процесса будет обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="4e56c-155">Once an event has occurred the workflow will continue to process.</span></span>
  
    
    

### <a name="wait-for-field-change-in-current-item"></a><span data-ttu-id="4e56c-156">Ждать изменения поля в текущем элементе</span><span class="sxs-lookup"><span data-stu-id="4e56c-156">Wait for Field Change in Current Item</span></span>

<span data-ttu-id="4e56c-157">**Ждать изменения поля в текущем элементе** действие содержит две редактируемые области, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="4e56c-157">The **Wait for Field Change in Current Item** action contains two editable regions, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="4e56c-158">**Ждать изменения поля в текущем элементе**</span><span class="sxs-lookup"><span data-stu-id="4e56c-158">**Wait for Field Change in Current Item**</span></span>

  
    
    

  
    
    
![Снимок экрана: действие события.](../images/wf15-eventingactions4.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="4e56c-160">Редактируемые области являются:</span><span class="sxs-lookup"><span data-stu-id="4e56c-160">The editable regions are:</span></span>
  
    
    

- <span data-ttu-id="4e56c-161">**Поля:** Поле в элементе, которое должны отслеживаться для изменения.</span><span class="sxs-lookup"><span data-stu-id="4e56c-161">**Field:** The field in the item that should be monitored for change.</span></span>
    
  
- <span data-ttu-id="4e56c-162">**Значение:** Значение, которое должно быть равно поля в порядке для рабочего процесса, чтобы продолжить работу.</span><span class="sxs-lookup"><span data-stu-id="4e56c-162">**Value:** The value that the field should equal in order for the workflow to proceed.</span></span>
    
  
<span data-ttu-id="4e56c-163">После изменения поля продолжается рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="4e56c-163">Once a field has changed the workflow continues.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="4e56c-164">См. также</span><span class="sxs-lookup"><span data-stu-id="4e56c-164">See also</span></span>
<span data-ttu-id="4e56c-165"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4e56c-165"></span></span>


-  [<span data-ttu-id="4e56c-166">Рабочий процесс в SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e56c-166">Workflow in SharePoint </span></span>](http://technet.microsoft.com/en-us/sharepoint/jj556245.aspx)
    
  
-  [<span data-ttu-id="4e56c-167">Новые возможности рабочих процессов SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e56c-167">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="4e56c-168">Начало работы с рабочими процессами SharePoint</span><span class="sxs-lookup"><span data-stu-id="4e56c-168">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="4e56c-169">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="4e56c-169">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="4e56c-170">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="4e56c-170">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

  
    
    

