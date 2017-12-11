---
title: "Справочник по действий рабочих процессов для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 88e09f75-480f-4a68-87a6-b496350345cc
ms.openlocfilehash: 4f808bbc0e8d6f08d2779a1e3d6b2343f9a5dd01
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="workflow-actions-and-activities-reference-for-sharepoint"></a>Справочник по действий рабочих процессов для SharePoint
Сведения о действия рабочего процесса, доступных для разработки рабочего процесса в SharePoint Designer 2013 и классы действий рабочего процесса, доступные для разработчиков рабочих процессов с помощью Visual Studio 2012.
## <a name="workflow-activities-and-actions"></a>Действия рабочего процесса и действия
<a name="bkm_Activities"> </a>

Рабочий процесс действия представления объектов на уровне кода, которые обрабатывают вызовы методов различным интерфейсам API, которые образуют поведение рабочего процесса. Взаимодействие с действий рабочего процесса в коде, с помощью или другой среде разработки.
  
    
    
Чтобы получить список доступных действий видеть [классы действий рабочего процесса в SharePoint](workflow-activity-classes-in-sharepoint.md).
  
    
    
С другой стороны, бизнес-процессов действия являются программы-оболочки для объектов, которые инкапсулируют этих базовых действий и представить их в форме понятное SharePoint Designer. Взаимодействие с действия рабочего процесса в SharePoint Designer.
  
    
    
Список действий рабочих процессов недоступны в разделе [действия рабочего процесса для быстрого доступа (платформа рабочих процессов SharePoint)](workflow-actions-quick-reference-sharepoint-workflow-platform.md) и [действия рабочего процесса можно получить с моста взаимодействия рабочих процессов](workflow-actions-available-using-the-workflow-interop-bridge.md).
  
    
    

## <a name="windows-workflow-foundation-40-activities"></a>Действия Windows Workflow Foundation 4.0
<a name="bkm_WF4"> </a>

Несмотря на то, что SharePoint платформу и инфраструктуру позволяют специальный активности классы для создания настраиваемых рабочих процессов SharePoint, можно использовать одно из действий, представленными Windows Workflow Foundation (WF) 4.0. Эти классы действий WF 4.0, доступны в Microsoft .NET Framework 4 в пространстве имен  [System.Activities.Statements](http://msdn.microsoft.com/en-us/library/system.activities.statements.aspx) .
  
    
    
Классы действий WF 4.0 представлены некоторые полезные возможности, которые не может найти в библиотеке классов активности SharePoint. Например WF 4.0 включает в себя класс **If**, который позволяет создавать условного действия. Кроме того можно использовать действие [System.ServiceModel.Activities.Send](http://msdn.microsoft.com/en-us/library/system.servicemodel.activities.send.aspx) для подключения к веб-служб.
  
    
    

## <a name="in-this-section"></a>В этом разделе
<a name="bkm_inthissection"> </a>


-  [Классы действий рабочего процесса в SharePoint](workflow-activity-classes-in-sharepoint.md)
    
  
-  [Краткий справочник по действиям рабочего процесса (платформа рабочих процессов в SharePoint)](workflow-actions-quick-reference-sharepoint-workflow-platform.md)
    
  
-  [Действия рабочего процесса можно получить с моста взаимодействия рабочих процессов](workflow-actions-available-using-the-workflow-interop-bridge.md)
    
  

## <a name="see-also"></a>См. также
<a name="bkm_addlres"> </a>


-  [Разработка рабочих процессов в SharePoint с помощью Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md)
    
  
-  [Рабочие процессы в SharePoint](workflows-in-sharepoint.md)
    
  

