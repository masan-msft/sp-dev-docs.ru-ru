---
title: "Запуск и настройка свойств рабочего процесса"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7386bbf9-3ed6-4732-bcdb-b27baed7397e
ms.openlocfilehash: 3dea52f65dfb581448e48789b40ffa07e4482813
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="workflow-initiation-and-configuration-properties"></a>Запуск и настройка свойств рабочего процесса
Общие сведения о инициализации и сопоставлении свойств, которые задает SharePoint для рабочих процессов.
## 

При запуске рабочего процесса SharePoint автоматически устанавливает количество сопоставления и запуска свойства, которые поддерживают рабочего процесса. Они перечислены ниже. Набор свойств, определенных отличается немного в зависимости от рабочих процессов **сайта** или рабочий процесс **списка**. Эти различия определяются в списках.
  
    
    
Используйте следующие рекомендации для сопоставления и запуска рабочих процессов с помощью объектной модели рабочих процессов (инициирование):
  
    
    

- Чтобы создать связь для рабочего процесса **списка**, используйте метод [PublishSubscriptionForList](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) .
    
  
- Чтобы создать связь для рабочего процесса **сайта**, используйте метод [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) .
    
  
- Чтобы запустить рабочий процесс **списка**, используйте метод [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) .
    
  
- Для запуска рабочего процесса **сайта**, используйте метод [StartWorkflow](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflow.aspx) .
    
> [!NOTE] 
> [!Примечание] Два метода для **связывания** рабочих процессов находятся в классе [WorkflowSubscriptionService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.aspx) во время на класс [WorkflowInstanceService](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.aspx) находятся два метода для **запуска** рабочих процессов.
  
    
    


## <a name="association-properties"></a>Сопоставления свойств

Значения свойства ассоциации устанавливаются при вызове  [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) . Значения свойств связи являются свойства уровня привязки, что означает, что все экземпляры рабочих процессов с помощью данного сопоставления совместно использовать такое же значение свойства. Значение свойства связи в пределах рабочим процессом можно извлечь с помощью действия **GetConfigurationValue**.
  
    
    
Ниже приведен список свойств связи, установленные по умолчанию для **списка** и **сайта** рабочих процессов при вызове [PublishSubscription](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscription.aspx) .
  
    
    

-  [AssociationTitle](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociationTitle.aspx)
    
  
-  [AssociatorUserId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.AssociatorUserId.aspx)
    
  
-  [LayoutsFolder](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.LayoutsFolder.aspx)
    
  
-  ParentContentTypeId()
    
  
- **HistoryListId***
    
  
- **TaskListId***
    
  
- **FormData***
    
  
- **SharePointWorkflowContext.Subscription.EventSourceId***
    
  
- **SharePointWorkflowContext.Subscription.EventType***
    
  
- **SharePointWorkflowContext.Subscription.DisplayName***
    
  
- **SharePointWorkflowContext.Subscription.Id***
    
  
- **SharePointWorkflowContext.Subscription.Name***
    
  
- **SharePointWorkflowContext.Subscription.CreatedDate***
    
  

> **Важные:** Свойства, помеченные звездочкой (\*) не определены в API рабочего процесса, чтобы получить доступ к их просто использовать их строковые значения. 
  
    
    

В случае **списка** рабочих процессов существует четыре дополнительных сопоставления свойств, определенных по умолчанию при вызове [PublishSubscriptionForList(WorkflowSubscription, Guid)](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowSubscriptionService.PublishSubscriptionForList.aspx) .
  
    
    

-  [ListId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListId.aspx)
    
  
-  [ListName](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowConfigurationPropertyName.ListName.aspx)
    
  
- **StatusColumnCreated***
    
  
- **StatusFieldName***
    
  

> [!IMPORTANT] 
> Свойства, помеченные звездочкой (\*) не определены в API рабочего процесса, чтобы получить доступ к их просто использовать их строковые значения. 
  
> [!NOTE] 
> [!Примечание] Можно добавить пользовательские сопоставления свойств с помощью формы связывания. 
  
    
    


## <a name="initiation-properties"></a>Свойства инициализации

Свойства запуска  это внешние переменные, значения которых установлены при запуске рабочего процесса  то есть, при вызове **StartWorkflow**. Тем не менее, значения свойств могут обновляться во время выполнения из экземпляра рабочего процесса с помощью действия **ExternalVariableValue**. Значения внешних переменных можно извлечь из *за пределами*  рабочего процесса с помощью [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstance.Properties.aspx) .
  
    
    
Внешние значения переменных специфичны для каждого экземпляра рабочего процесса (в отличие от свойства связи, где все экземпляры рабочих процессов совместно использовать те же значения свойства). 
  
    
    
Все экземпляры рабочих процессов (списка и сайта) иметь некоторые внешние переменные, которые устанавливаются по умолчанию при вызове **StartWorkflow**:
  
    
    

-  [InitiatorUserId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.InitiatorUserId.aspx)
    
  
-  [RetryCode](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RetryCode.aspx)
    
  
-  [RelatedItems](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.RelatedItems.aspx)
    
  
Список экземпляров рабочих процессов имеет некоторые дополнительные внешние переменные, которые устанавливаются по умолчанию при вызове  [StartWorkflowOnListItem](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.WorkflowInstanceService.StartWorkflowOnListItem.aspx) :
  
    
    

-  [CurrentItemUrl](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.CurrentItemUrl.aspx)
    
  
-  [ItemId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemId.aspx)
    
  
-  [ItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ItemGuid.aspx)
    
  
-  [ContextListId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.ContextListId.aspx)
    
  
-  [UniqueId](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.ExternalVariableName.UniqueId.aspx)
    
> [!NOTE] 
> [!Примечание] Можно добавить настраиваемые инициализации свойства с помощью форму запуска. 
  
    
    


## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

-  [Разработка рабочих процессов в SharePoint с помощью Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
-  [Как: создание рабочих процессов SharePoint с помощью Visual Studio](how-to-create-sharepoint-workflows-using-visual-studio.md)
    
  

  
    
    

