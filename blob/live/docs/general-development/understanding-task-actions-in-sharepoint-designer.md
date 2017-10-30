---
title: "Общие сведения о действия с задачами в SharePoint Designer 2013"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6fd69e94-ebe1-4d5d-98db-b2f3ce16f098
ms.openlocfilehash: d552cfecf00972f0b21b513d6ff52d1f53316a41
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="understanding-task-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="41ab4-102">Общие сведения о действия с задачами в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="41ab4-102">Understanding Task Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="41ab4-103">Изучите использование действия задачи в SharePoint Designer 2013.</span><span class="sxs-lookup"><span data-stu-id="41ab4-103">Learn to use Task Actions in SharePoint Designer 2013.</span></span>
||
|:-----|
||
   

## <a name="overview-of-task-actions-in-sharepoint-designer-2013"></a><span data-ttu-id="41ab4-104">Общие сведения о действия с задачами в SharePoint Designer 2013</span><span class="sxs-lookup"><span data-stu-id="41ab4-104">Overview of Task Actions in SharePoint Designer 2013</span></span>
<span data-ttu-id="41ab4-105"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="41ab4-105"></span></span>

<span data-ttu-id="41ab4-106">Задачи в SharePoint используется для назначения работы для пользователя или группы и затем отслеживать ход выполнения, которые работают со временем.</span><span class="sxs-lookup"><span data-stu-id="41ab4-106">A task in SharePoint is used to assign work to a person or group and then track the progress of that work over time.</span></span> <span data-ttu-id="41ab4-107">Существует два действия рабочих процессов в SharePoint Designer 2013 предназначена для работы с задачами.</span><span class="sxs-lookup"><span data-stu-id="41ab4-107">There are two workflow actions in SharePoint Designer 2013 designed for working with tasks.</span></span>
  
    
    
<span data-ttu-id="41ab4-108">Эти действия, являются:</span><span class="sxs-lookup"><span data-stu-id="41ab4-108">These actions are:</span></span>
  
    
    

- <span data-ttu-id="41ab4-109">**Назначение задачи** используется для создания задачи SharePoint и назначить один из участников.</span><span class="sxs-lookup"><span data-stu-id="41ab4-109">**Assign a task** is used to create a SharePoint task and assign it to a single participant.</span></span>
    
  
- <span data-ttu-id="41ab4-110">**Запуск рабочего процесса** используется для назначения задачи для нескольких участников.</span><span class="sxs-lookup"><span data-stu-id="41ab4-110">**Start a task process** is used to assign a task to multiple participants.</span></span>
    
  
<span data-ttu-id="41ab4-111">Действия задач доступны в раскрывающемся меню **действия** на ленте SharePoint Designer 2013, как показано на рисунке.</span><span class="sxs-lookup"><span data-stu-id="41ab4-111">The Task Actions are accessed in the **Action** drop-down menu of the SharePoint Designer 2013 ribbon, as shown in the figure.</span></span>
  
    
    

<span data-ttu-id="41ab4-112">**Рисунок: Действия с задачами в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="41ab4-112">**Figure: Task Actions in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Действия задач доступны из раскрывающегося меню "Действие" на ленте SharePoint Designer 2013 Preview](../images/spd15-TaskActions1.png)
  
    
    

  
    
    

  
    
    

## <a name="using-task-actions-in-sharepoint"></a><span data-ttu-id="41ab4-114">С помощью действия с задачами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="41ab4-114">Using Task Actions in SharePoint</span></span>
<span data-ttu-id="41ab4-115"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="41ab4-115"></span></span>

<span data-ttu-id="41ab4-p102">Бизнес-процесса часто состоит из задачи, которые должны быть выполнены пользователями. Рабочий процесс управляет шаги процесса. Рабочий процесс использует Действия с задачами для назначения задач людей. Например при на работу новых сотрудников необходимо выполнить ряд задач. Одна задача может быть адаптация нового сотрудника. Задачи может потребоваться выполнить членом отдела кадров.</span><span class="sxs-lookup"><span data-stu-id="41ab4-p102">A business process often consists of tasks that must be performed by people. A workflow orchestrates the steps of a process. A workflow uses Task Actions to assign tasks to people. For example, when a new employee is hired a number of tasks need to be performed. One such task might be a new employee orientation. The task might need to be performed by a member of the Human Resources department.</span></span>
  
    
    
<span data-ttu-id="41ab4-p103">Действий **Назначение задачи** и **запуска рабочего процесса**, находятся в меню **действия** раскрывающегося списка на ленте SharePoint Designer 2013. Можно добавить действия в рабочий процесс и настроить их для определенных обстоятельствах. Действие **Назначение задачи** используется для назначения задачи для одного участника. Действие при **запуске рабочего процесса** используется для назначения задачи для нескольких участников.</span><span class="sxs-lookup"><span data-stu-id="41ab4-p103">The **Assign a task** and **Start a task process** actions are located on the **Actions** drop-down menu in the SharePoint Designer 2013 ribbon. You can add the actions to your workflow and then customize them for your particular circumstance. The **Assign a task** action is used to assign a task to a single participant. The **Start a task process** action is used to assign a task to multiple participants.</span></span>
  
    
    

### <a name="assign-a-task"></a><span data-ttu-id="41ab4-126">Назначение задачи</span><span class="sxs-lookup"><span data-stu-id="41ab4-126">Assign a task</span></span>

<span data-ttu-id="41ab4-127">На рисунке показана действие **Назначение задачи**.</span><span class="sxs-lookup"><span data-stu-id="41ab4-127">The **Assign a task** action is shown in the figure.</span></span>
  
    
    

<span data-ttu-id="41ab4-128">**Рисунок: Назначить действие задачи в SharePoint Designer 2013**</span><span class="sxs-lookup"><span data-stu-id="41ab4-128">**Figure: The Assign a task action in SharePoint Designer 2013**</span></span>

  
    
    

  
    
    
![Действие "Назначение задачи" в SharePoint Designer 2013.](../images/SPD15-TaskActions2.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="41ab4-130">**Назначение задачи** действие принимает три входных данных: пользователю назначать задачи, результат переменной и переменной идентификатор задачи.</span><span class="sxs-lookup"><span data-stu-id="41ab4-130">The **Assign a task** action takes three inputs: the user to assign a task, the outcome variable, and the task id variable.</span></span>
  
    
    

- <span data-ttu-id="41ab4-p104">**этот пользователь**: открывает диалоговое окно **Назначение задачи**, как показано на рисунке. Используйте диалоговое окно для указания участника, названия задачи, описания, выполнения даты, параметров задач, настроек электронной почты и параметров результата.</span><span class="sxs-lookup"><span data-stu-id="41ab4-p104">**this user**: Opens the **Assign a Task** dialog as shown in the figure. Use the dialog to set the participant, task title, description, due date, task options, email options, and outcome options.</span></span>
    
  
- <span data-ttu-id="41ab4-133">**Переменная: результат**: присваивает переменной, которая будет использоваться для хранения результат задачи.</span><span class="sxs-lookup"><span data-stu-id="41ab4-133">**Variable: Outcome**: Assigns the variable that will hold the outcome of the task.</span></span>
    
  
- <span data-ttu-id="41ab4-134">**Переменная: TaskID**: присваивает переменной, которая будет использоваться для хранения идентификатор задачи.</span><span class="sxs-lookup"><span data-stu-id="41ab4-134">**Variable: TaskID**: Assigns the variable that will hold the id of the task.</span></span>
    
  

<span data-ttu-id="41ab4-135">**Рисунок: Диалоговое окно задач назначения**</span><span class="sxs-lookup"><span data-stu-id="41ab4-135">**Figure: The Assign a Task dialog box**</span></span>

  
    
    

  
    
    
![Использование диалогового окна "Назначение задачи" для указания участника, названия задачи, описания, даты выполнения, параметров задач, настроек электронной почты и параметров результата.](../images/SPD15-TaskActions3.png)
  
    
    

  
    
    

  
    
    

### <a name="start-a-task-process"></a><span data-ttu-id="41ab4-137">Запуск процесса задачи</span><span class="sxs-lookup"><span data-stu-id="41ab4-137">Start a task process</span></span>

<span data-ttu-id="41ab4-138">На рисунке показана действие при **запуске рабочего процесса**.</span><span class="sxs-lookup"><span data-stu-id="41ab4-138">The **Start a task process** action is shown in the figure.</span></span>
  
    
    

<span data-ttu-id="41ab4-139">**Рисунок: «Запуск процесса задач» действия.**</span><span class="sxs-lookup"><span data-stu-id="41ab4-139">**Figure: The "Start a task process" action.**</span></span>

  
    
    

  
    
    
![Для действия "Запуск процесса задач" используется два входных параметра: переменные "пользователи" и "результат"](../images/SPD15-TaskActions4.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="41ab4-141">Действие при **запуске рабочего процесса** используется два входных параметра: пользователи, которые будут принимать участие в задаче и переменной результата.</span><span class="sxs-lookup"><span data-stu-id="41ab4-141">The **Start a task process** action takes two inputs: the users that will participate in the task and the outcome variable.</span></span>
  
    
    

- <span data-ttu-id="41ab4-p105">**эти пользователи**: открывает диалоговое окно **Запуск процесса задачи**, как показано на рисунке. Используйте диалоговое окно Установка участника, названия задачи, описания, выполнения даты, параметров задач, настроек электронной почты и параметров результата.</span><span class="sxs-lookup"><span data-stu-id="41ab4-p105">**these users**: Opens the **Start a Task Process** dialog box as shown in the figure. Use the dialog box to set the participants, task title, description, due date, task options, email options, and outcome options.</span></span>
    
  
- <span data-ttu-id="41ab4-144">**Переменная: результат**: присваивает переменной, которая результата рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="41ab4-144">**Variable: Outcome**: Assigns the variable that holds the outcome of the task process.</span></span>
    
  

<span data-ttu-id="41ab4-145">**Рисунок: Диалоговое окно рабочего процесса Пуск**</span><span class="sxs-lookup"><span data-stu-id="41ab4-145">**Figure: The Start a Task Process dialog box**</span></span>

  
    
    

  
    
    
![Использование диалогового окна "Запуск процесса задач" для указания участника, названия задачи, описания, даты выполнения, параметров задач, настроек электронной почты и параметров результата.](../images/SPD15-TaskActions5.png)
  
    
    

  
    
    

  
    
    

## <a name="additional-resources"></a><span data-ttu-id="41ab4-147">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="41ab4-147">Additional resources</span></span>
<span data-ttu-id="41ab4-148"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="41ab4-148"></span></span>


-  [<span data-ttu-id="41ab4-149">Новые возможности рабочего процесса в SharePoint</span><span class="sxs-lookup"><span data-stu-id="41ab4-149">What's new in workflow in SharePoint</span></span>](http://msdn.microsoft.com/library/6ab8a28b-fa2f-4530-8b55-a7f663bf15ea.aspx)
    
  
-  [<span data-ttu-id="41ab4-150">Приступая к работе с рабочего процесса SharePoint</span><span class="sxs-lookup"><span data-stu-id="41ab4-150">Getting started with SharePoint workflow</span></span>](http://msdn.microsoft.com/library/cc73be76-a329-449f-90ab-86822b1c2ee8.aspx)
    
  
-  [<span data-ttu-id="41ab4-151">Разработка рабочих процессов в SharePoint Designer и Visio</span><span class="sxs-lookup"><span data-stu-id="41ab4-151">Workflow development in SharePoint Designer and Visio</span></span>](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [<span data-ttu-id="41ab4-152">Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)</span><span class="sxs-lookup"><span data-stu-id="41ab4-152">Workflow actions quick reference (SharePoint Workflow platform)</span></span>](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  

  
    
    

