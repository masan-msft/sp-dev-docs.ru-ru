---
title: "Объектная модель рабочих процессов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: be615a89-3201-4cd8-bbc7-15f3abf9f668
ms.openlocfilehash: 02434d1a009b54ad971145d53cb1c47b52a096ad
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-workflow-object-model"></a>Объектная модель рабочих процессов SharePoint
Получите Краткое введение в объектной модели рабочих процессов в SharePoint.
## <a name="sharepoint-workflow-object-model"></a>Объектная модель рабочих процессов SharePoint
<a name="bk_SPwfom"> </a>

Для Windows Workflow Foundation 4, но с нововведения, которые позволяют функциональности рабочих процессов в SharePoint как правило и в SharePoint надстройки в частности, объектной модели SharePoint построен на основе объектной модели .NET Framework 4. Собственной объектной модели .NET Framework 4 для Windows Workflow Foundation 4 находится в.NET Framework [пространства имен System.Workflow](http://msdn.microsoft.com/en-us/library/gg145026.aspx).
  
    
    
Можно рассматривать объектной модели SharePoint, рабочий процесс  как набор служб рабочих процессов. Существует четыре службы: 
  
    
    

- **Экземпляра службы управления:** Управляет экземпляров рабочих процессов и их выполнения.
    
  
- **Развертывания службы:** Управляет развертывания определений рабочих процессов.
    
  
- **Взаимодействия службы:** Управляет моста взаимодействия для поддержки прежних версий рабочих процессов.
    
  
- **Системы обмена сообщениями службы:** Управляет транспорта и сообщений.
    
  

### <a name="sharepoint-workflow-namespaces"></a>Пространства имен рабочих процессов SharePoint

Рабочий процесс объектной модели SharePoint, с другой стороны, содержатся в десяти пространства имен: пять из них являются зарегистрированными пространствами имен и пять другим пользователям, Microsoft Office пространства имен.
  
    
    
 пространства имен **Microsoft.SharePoint**:
  
    
    

-  [Microsoft.SharePoint.Workflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.aspx)
    
  
-  [Microsoft.SharePoint.Workflow.Application](https://msdn.microsoft.com/library/Microsoft.SharePoint.Workflow.Application.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowActions](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowActions.WithKey](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.WithKey.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowServices](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.aspx)
    
  
-  [Microsoft.SharePoint.WorkflowServices.Activities](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.aspx)
    
  
 пространства имен **Microsoft.Office**:
  
    
    

-  [Microsoft.Office.Workflow](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.aspx)
    
  
-  [Microsoft.Office.Workflow.Actions](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Actions.aspx)
    
  
-  [Microsoft.Office.Workflow.Feature](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Feature.aspx)
    
  
-  [Microsoft.Office.Workflow.Routing](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Routing.aspx)
    
  
-  [Microsoft.Office.Workflow.Utility](https://msdn.microsoft.com/library/Microsoft.Office.Workflow.Utility.aspx)
    
  

### <a name="sharepoint-workflow-schemas"></a>Схемы рабочих процессов SharePoint

Справочник по содержимого для схем SharePoint содержащиеся в узле ссылку под названием [схемы рабочих процессов](http://msdn.microsoft.com/library/b36ded16-3ffd-4931-811e-c402c1e35b07%28Office.15%29.aspx)и содержать следующие элементы:
  
    
    

-  [Справочник по схеме WorkflowActions4](http://msdn.microsoft.com/library/1c0112de-0139-e64d-d3d6-658541695391%28Office.15%29.aspx)
    
  
-  [Справочник по схеме WorkflowActions3](http://msdn.microsoft.com/library/7a03ead8-30e0-4601-9c6f-edfb04ce57f9%28Office.15%29.aspx)
    
  
-  [Обзор схемы конфигурации рабочего процесса](http://msdn.microsoft.com/library/63824239-6eb2-4cf1-ba84-44eace4d3781%28Office.15%29.aspx)
    
  
-  [Справочник по схеме WorkflowInfo](http://msdn.microsoft.com/library/f3bdcc70-15a0-44b2-9b01-330f13430354%28Office.15%29.aspx)
    
  

## <a name="see-also"></a>См. также
<a name="bk_additionalresources"> </a>


-  [Краткое описание Windows Workflow Foundation (WF) в .NET 4 для разработчика](http://msdn.microsoft.com/en-us/library/ee342461.aspx)
    
  
-  [Windows Workflow Foundation 4.0: Hello, рабочий процесс!](http://weblogs.asp.net/gunnarpeipman/archive/2009/07/08/windows-workflow-foundation-4-0-hello-workflow.aspx)
    
  
-  [Windows Workflow Foundation (WF) (en)](http://msdn.microsoft.com/en-us/netframework/dd733248)
    
  
-  [Справочник по действий рабочих процессов для SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [Разработка рабочих процессов в SharePoint с помощью Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

