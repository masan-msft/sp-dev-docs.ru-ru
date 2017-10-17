---
title: "Примеры рабочих процессов SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ffaccd6b-426d-4ca0-b62f-bc7b14641a49
ms.openlocfilehash: 42abbc0a0b8e1ae8522092fce06452429cf673b7
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-workflow-samples"></a>Примеры рабочих процессов SharePoint
Примеры рабочих процессов, иллюстрирующие создание и реализацию рабочих процессов SharePoint на новой платформе Workflow Manager Client 1.0.
## <a name="workflow-samples-for-sharepoint"></a>Примеры рабочих процессов для SharePoint
<a name="bkm_wfsamples"> </a>

Эта серия примеров рабочих процессов была разработана для демонстрации широких возможностей рабочих процессов в SharePoint. Они разработаны с помощью Visual Studio 2012 и доступны в  [коллекции примеров MSDN](http://code.msdn.microsoft.com/). Ниже приводятся ссылки на отдельные примеры.
  
    
    

### <a name="sharepoint-workflow-call-an-external-web-service"></a>Рабочий процесс SharePoint: вызов внешней веб-службы

В этом примере используется Visual Studio, чтобы продемонстрировать создание рабочего процесса, который вызывает внешнюю веб-службу с помощью действия **HttpGet**. При вызове веб-службы рабочий процесс также использует тип данных **DynamicValue**.
  
    
    
Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: вызов внешней веб-службы](http://code.msdn.microsoft.com/SharePoint-workflow-48ea87d4).
  
    
    

### <a name="sharepoint-workflow-create-a-custom-action"></a>Рабочий процесс SharePoint: создание настраиваемого действия

В этом примере Visual Studio используется для создания рабочего процесса, который вызывает внешнюю веб-службу. При вызове веб-службы рабочий процесс также использует новый тип данных **DynamicValue**. Часть рабочего процесса, которая вызывает веб-службу и извлекает сведения из ответа, находится внутри настраиваемого действия, **GetNWCustomerDetailsWorkflow**.
  
    
    
Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: создание настраиваемого действия](http://code.msdn.microsoft.com/SharePoint-workflow-41e5c0f9).
  
    
    

### <a name="sharepoint-workflow-sales-tax-calculator"></a>Рабочий процесс SharePoint: калькулятор налога на продажу

В этом исчерпывающем примере рабочий процесс использует веб-службу, чтобы получить соответствующую налоговую ставку в зависимости от местоположения клиента, а затем использует базовую цену, чтобы вычислить налог на продажу и общую стоимость.
  
    
    
Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: калькулятор налога на продажу](http://code.msdn.microsoft.com/SharePoint-workflow-f7a1a8ba).
  
    
    

### <a name="sharepoint-workflow-use-a-task-action-in-sharepoint-designer"></a>Рабочий процесс SharePoint: использование действия задачи в SharePoint Designer

Расширенное пошаговое руководство по реализации действий задач в рабочем процессе, созданном с помощью Microsoft SharePoint Designer 2013.
  
    
    
Пример с файлом readme доступен по ссылке:  [Рабочий процесс SharePoint: использование действия задачи в SharePoint Designer](http://code.msdn.microsoft.com/SharePoint-workflow-942a5441).
  
    
    

### <a name="sharepoint-workflow-workflow-om-in-a-sharepoint-app"></a>Рабочий процесс SharePoint: объектная модель рабочих процессов в приложении для SharePoint

Пример кода **Рабочий процесс SharePoint: объектная модель рабочих процессов в приложении для SharePoint** представляет собой размещаемое в SharePoint приложение, которое использует JSOM рабочих процессов SharePoint для развертывания определений рабочих процессов на сайт приложения и "родительский сайт" (то есть сайт SharePoint, на котором размещается приложение).
  
    
    
Вы можете найти этот пример кода здесь:  [Рабочий процесс SharePoint: объектная модель рабочих процессов в приложении для SharePoint](http://code.msdn.microsoft.com/SharePoint-workflow-050f5211).
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkm_additional"> </a>


-  [Общие сведения о рабочих процессах в SharePoint](get-started-with-workflows-in-sharepoint.md)
    
  
-  [Установка и настройка диспетчера рабочих процессов SharePoint](set-up-and-configure-sharepoint-workflow-manager.md)
    
  
-  [Что нового в рабочих процессах для SharePoint](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [Справочник по действий рабочих процессов для SharePoint](workflow-actions-and-activities-reference-for-sharepoint.md)
    
  
-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  

