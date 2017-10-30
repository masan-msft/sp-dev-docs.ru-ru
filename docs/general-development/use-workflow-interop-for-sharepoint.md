---
title: "Использование средств взаимодействия рабочих процессов для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: 3da21b5ba12d0e2b463a3e1a8b5807cd8a597862
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="use-workflow-interop-for-sharepoint"></a>Использование средств взаимодействия рабочих процессов для SharePoint
Предоставляет сведения об использовании средств взаимодействия рабочих процессов SharePoint в конструкторе рабочих процессов Visual Studio 2012. Рабочий процесс взаимодействия позволяет выполнять рабочего процесса SharePoint 2010 из рабочего процесса SharePoint. Это является важной функцией, которая позволяет повторно использовать существующие компоненты рабочих процессов и вызвать для действий рабочего процесса, не встроенные в SharePoint.

  
    
    


> **Важные:** Чтобы узнать, как использовать функции взаимодействия SharePoint рабочего процесса в SharePoint Designer 2013, просмотрите [действия по координации общее представление о в SharePoint Designer 2013](understanding-coordination-actions-in-sharepoint-designer.md). 
  
    
    


## <a name="sharepoint-workflow-interop"></a>Взаимодействие рабочих процессов SharePoint
<a name="bkm_interop"> </a>

Вот проблемы. У вас есть устаревших рабочих процессов SharePoint 2010, которые необходимо повторно использовать платформы SharePoint. Или, того, вы создаете новые рабочие процессы SharePoint и необходимые для вызова действия, которые доступны только в платформе SharePoint 2010. И вы не знаете, что делать. На самом деле, простое решение: использование рабочего процесса SharePoint взаимодействия.
  
    
    
Для нормальной работы с модуля рабочего процесса SharePoint, который основан на Windows Workflow Foundation 4 взаимодействия рабочих процессов SharePoint позволяет рабочих процессов SharePoint 2010 (основан на Windows Workflow Foundation 3). Хотя новый модуль выполнения Windows Workflow Foundation 4 размещается в диспетчер рабочих процессов, который используется в качестве внешней службы SharePoint по-прежнему содержит прежних версий узла рабочего процесса SharePoint, который используется для обработки рабочих процессов SharePoint 2010. Взаимодействие рабочих процессов SharePoint согласует среды выполнения двух, как показано на рисунке 1.
  
    
    

**На рисунке 1. Взаимодействие рабочих процессов SharePoint в действии**

  
    
    

  
    
    
![Мост межпрограммного взаимодействия с рабочим процессом](../images/wfInteropBridge.png)
  
    
    
Рассмотрим процесс показано на рисунке 1. Используйте буквы в поиске точек особое внимание на рисунке:
  
    
    


  
    
    
> Запускает ( **A** ) экземпляр рабочего процесса SharePoint для запуска диспетчера рабочих процессов нажмите на основе Windows Workflow Foundation 4. Обратите внимание на то, что диспетчер рабочих процессов не входит в SharePoint, но вместо этого используется в качестве внешней службы.
    
  

  
    
    
> ( **Б** ) достижении точки в рабочий процесс SharePoint — номер этапа 3 в диспетчер рабочих процессов - которой вы хотите вызвать рабочего процесса SharePoint 2010. В конструкторе рабочих процессов Visual Studio 2012 это делается при помощи действия **WF 2010 Пуск** , как показано на рисунке 2.
    
   **На рисунке 2. Плитка "Стадия" для запуска рабочего процесса SharePoint 2010.**

  

  ![Запуск рабочего процесса 2010](../images/wfInterop_Stage1.png)
  

    
    
    From the perspective of the SharePoint object model, this is accomplished using the  [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.StartWorkflow.aspx) method on the [WorkflowInteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx) class.
    
  

  
    
    
> ( **C** ) на этом этапе рабочего процесса SharePoint 2010 начинает выполнение в узле Windows Workflow Foundation 3,5 рабочего процесса в SharePoint. Однако включается особое внимание. В некоторых случаях вы можете 2013 рабочего процесса, чтобы ожидать в рабочий процесс 2010 для завершения работы (и может быть возвращены некоторые данные) перед тем как продолжить выполнение рабочего процесса 2013. В других сценариях это может быть не требуется и оба рабочие процессы могут выполняться независимо, параллельно.
    
    To control this behavior, the  [WorkflowInterop](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.WorkflowInterop.aspx) class, which controls executing workflows in the Windows Workflow Foundation 3.5 workflow host, provides a [Wait](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.WorkflowInterop.Wait.aspx) property. Setting this Boolean property to " **Yes**" (in the designer dialog box) or to **true** in the on the **Wait** property, causes the 2013 workflow to pause until the 2010 finished executing and returns a **completed** message.
    
    
    

   **На рисунке 3. Запустите диалоговое окно свойств рабочего процесса.**

  

  ![Установка свойств для действия "Запустить рабочий процесс"](../images/wfInterop_.png)
  

  

  

  
    
    
> Здесь приведен ( **D** ) приводит к практическим результатам по выбору **true** или **false** на **Wait** свойство (или **Да** или **Нет** в диалоговом окне Свойства). Если **Wait** **true**, затем рабочий процесс 2010 передает событие  [WorkflowCompleted](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropEventReceiver.WorkflowCompleted.aspx) (и, при необходимости, возвращает данные в качестве свойства [DynamicValue](http://msdn.microsoft.com/library/2af7983b-8357-4e0f-9ba9-dfdeed05a8a7.aspx) ). Дополнительные сведения о динамических значения можно [Understanding Dynamic Value](http://msdn.microsoft.com/library/c5702628-9625-4d19-95c5-13923e91fea1.aspx).
    
    Of course, if **Wait** is set to **false**, then your 2010 workflow executes, then terminates normally.
    
  

  
    
    
> ( **E** ) этот шаг применяется только в том случае, если ваше вызова рабочего процесса 2010 указан **Wait=true**. В этом случае 2013 workflow получил событие **WorkflowCompleted** и перезапускает выполнение 2013 рабочего процесса на то, что оно было остановлено.
    
  

  
    
    
> Затем ( **F** ) 2013 workflow завершает выполнение и завершается. Если **Wait=false**, затем рабочий процесс 2013 выполняет и завершает независимо от рабочего процесса 2010. 
    
  

## <a name="workflow-interop-design"></a>Взаимодействия разработки рабочего процесса
<a name="bkm_interopDesign"> </a>

Взаимодействия рабочих процессов SharePoint  это платформа обмена сообщениями, которое поддерживает один к одному экземпляру сопоставление действий рабочих процессов WF 3 и WF 4. WF 3 и WF 4 взаимодействовать через обмена сообщениями, реализуемые пространством набора действий WF 4 на  [WorkflowInteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx) .
  
    
    
Для поддержки взаимодействия рабочих процессов, конструирования рабочего процесса в SharePoint Designer предоставляет доступ к нового действия рабочих процессов **WF 2010 Пуск**, который является оболочкой для метода  [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.StartWorkflow.aspx) . Это действие позволяет запустить рабочий процесс списка или рабочий процесс сайта.
  
    
    
Действия на самом деле — это последовательность сообщений, которые происходят между диспетчера рабочих процессов и узел рабочего процесса SharePoint 2010, на котором работает внутри SharePoint. Эти два являются посредством уровень обмена сообщениями, как показано на рисунке 4. Последовательность начинается в диспетчер рабочих процессов SharePoint с помощью вызова метода **StartWorkflow** . Сообщение «Пуск» переходит в службе рабочих процессов в SharePoint, где в свою очередь запускает рабочий процесс внутри узла рабочего процесса SharePoint 2010. По завершении выполнения рабочего процесса 2010 происходит событие, которое отправляет сообщение «завершенная» с помощью publisher события диспетчера рабочих процессов 2013.
  
    
    

**На рисунке 4. Протокол взаимодействия обмена сообщениями рабочего процесса SharePoint**

  
    
    

  
    
    
![Обмен сообщениями межпрограммного взаимодействия с рабочим процессом](../images/wfInteropMessaging.png)
  
    
    

  
    
    

  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Общие сведения о рабочих процессах в SharePoint](get-started-with-workflows-in-sharepoint.md)
    
  
-  [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md)
    
  
-  [Общие сведения о действия по координации в SharePoint Designer 2013](understanding-coordination-actions-in-sharepoint-designer.md)
    
  
-  [WorkflowInteropService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropService.aspx)
    
  
-  [WorkflowInteropEventReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInteropEventReceiver.aspx)
    
  

  
    
    

