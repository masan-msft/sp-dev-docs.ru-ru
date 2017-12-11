---
title: "Модуль записи VSS SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: e0f94ae99936f77f80b419c95d2d17acfd872345
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-workflow-development-best-practices"></a>Рекомендации по разработке рабочих процессов SharePoint
Содержит коллекцию советы и рекомендации для разработчиков, использующих Visual Studio для создания рабочих процессов в SharePoint.
## <a name="workflow-development-best-practices"></a>Рекомендации по разработке рабочих процессов

Чтобы разработать без ошибок рабочих процессов для SharePoint, лучше всего, выполните некоторые общие рекомендации по работе или «практические советы». Это так ли вы используете SharePoint Designer 2013 или Visual Studio 2012 для разработки рабочего процесса.
  
    
    

-  [Приложения для SharePoint, которые содержат интегрированной рабочих процессов необходимо изменить тег в файле workflowmanifest.xml](sharepoint-workflow-development-best-practices.md#bkm_00)
    
  
-  [При использовании действие журнала в список журналов, Дополнительные сведения  лучше](sharepoint-workflow-development-best-practices.md#bkm_01)
    
  
-  [Записать значение каждой строки и переменную, которая выполняется построение в списке журнала](sharepoint-workflow-development-best-practices.md#bkm_02)
    
  
-  [Вывод журнала трассировки до и после каждого шага или важные единица работы в рабочем процессе](sharepoint-workflow-development-best-practices.md#bkm_03)
    
  
-  [Убедитесь, что переменные ненулевые и содержат ожидаемые значения](sharepoint-workflow-development-best-practices.md#bkm_04)
    
  
-  [Убедитесь, что строки в текстовых полях рабочего процесса не превышать 255 символов](sharepoint-workflow-development-best-practices.md#bkm_05)
    
  
-  [Используйте повышенного уровня разрешений на нейтральный учетной записи при использовании олицетворения](sharepoint-workflow-development-best-practices.md#bkm_06)
    
  
-  [В рабочих процессов для повторного использования используйте столбцов связи для обеспечения без ошибок список полей](sharepoint-workflow-development-best-practices.md#bkm_07)
    
  
-  [Разработка рабочего процесса: модель бизнес-процессов в одного рабочего процесса](sharepoint-workflow-development-best-practices.md#bkm_08)
    
  
-  [Разработка рабочего процесса: эффективное использование действия утверждения](sharepoint-workflow-development-best-practices.md#bkm_09)
    
  

### <a name="apps-for-sharepoint-that-contain-integrated-workflows-must-edit-a-tag-in-the-workflowmanifestxml-file"></a>Приложения для SharePoint, которые содержат интегрированной рабочих процессов необходимо изменить тег в файле workflowmanifest.xml
<a name="bkm_00"> </a>

Надстройки SharePoint, содержащие интегрированной рабочие процессы (которые могут быть связаны со списками на родительский сайт) отличаются от приложений обычного рабочего процесса, изменив следующий тег **true** в файле `workflowmanifest.xml` в пакет приложения:
  
    
    

```XML

<SPIntegratedWorkflow xmlns="http://schemas.microsoft.com/sharepoint/2014/app/integratedworkflow">
    <IntegratedApp>true</IntegratedApp>
</SPIntegratedWorkflow>

```


### <a name="when-you-use-the-log-to-history-list-action-more-information-is-better"></a>При использовании действие журнала в список журналов, Дополнительные сведения  лучше
<a name="bkm_01"> </a>

Действие **Журнала в список журналов** (или класса [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx) при использовании Visual Studio ) позволяет регистрации сведений о рабочего процесса сделано на заданный момент жизненного цикла рабочего процесса. Это позволяет одним из наиболее важные средства устранения неполадок, которые у вас есть. Дополнительные сведения о предоставлении на важных этапах рабочего процесса, проще устранения непредвиденных событий.
  
    
    
Дополнительные сведения см. в следующих статьях. 
  
    
    

-  [Действия рабочих процессов в SharePoint Designer 2010: краткий справочник по](https://support.office.com/en-us/article/Workflow-actions-in-SharePoint-Designer-2010-A-quick-reference-guide-5a7ad276-0ed7-49b0-b652-e56a77dd96c6?CorrelationId=9cff0340-2d05-4878-b3a0-aecb30b862ed&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA010376961)
    
  
-  Класс  [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx)
    
  
-  [Как: журнал в списке журнала из действия рабочего процесса](http://msdn.microsoft.com/en-us/library/ff798337.aspx)
    
  
-  [С помощью журнала для действия SharePoint списка журнала рабочего процесса для отладки](http://www.documentmanagementworkflowinfo.com/sample-sharepoint-workflows/use-log-to-history-list-sharepoint-designer-workflow-action-debug)
    
  

### <a name="write-the-value-of-every-string-and-variable-that-you-construct-to-the-history-list"></a>Записать значение каждой строки и переменную, которая выполняется построение в списке журнала
<a name="bkm_02"> </a>

Отладка рабочих процессов, которые были созданы с помощью SharePoint Designer намного проще при записи строки и переменные в списке журнала с помощью действия **Log to History List**.
  
    
    
Дополнительные сведения см. в следующих статьях. 
  
    
    

-  [Действия рабочих процессов в SharePoint Designer 2010: краткий справочник по](https://support.office.com/en-us/article/Workflow-actions-in-SharePoint-Designer-2010-A-quick-reference-guide-5a7ad276-0ed7-49b0-b652-e56a77dd96c6?CorrelationId=9cff0340-2d05-4878-b3a0-aecb30b862ed&ui=en-US&rs=en-US&ad=US&ocmsassetID=HA010376961)
    
  
-  Класс  [LogToHistoryListActivity](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowActions.LogToHistoryListActivity.aspx)
    
  
-  [Как: журнал в списке журнала из действия рабочего процесса](http://msdn.microsoft.com/en-us/library/ff798337.aspx)
    
  
-  [С помощью журнала для действия SharePoint списка журнала рабочего процесса для отладки](http://www.documentmanagementworkflowinfo.com/sample-sharepoint-workflows/use-log-to-history-list-sharepoint-designer-workflow-action-debug)
    
  

### <a name="output-a-trace-log-before-and-after-each-step-or-important-unit-of-work-in-the-workflow"></a>Вывод журнала трассировки до и после каждого шага или важные единица работы в рабочем процессе
<a name="bkm_03"> </a>

В целях отладки рабочих процессов, важно для сохранения удобной для восприятия информации до, используя следующую каждого значительные единица работы; Эти сведения должны быть зафиксированы журналов трассировки. Для получения дополнительных сведений см.:
  
    
    

-  [Запись в журнал трассировки](http://msdn.microsoft.com/en-us/library/aa979595.aspx)
    
  
-  [С помощью событий и отслеживания журналы в SharePoint](http://msdn.microsoft.com/en-us/library/ff647362.aspx)
    
  

### <a name="verify-that-variables-are-non-null-and-contain-expected-values"></a>Убедитесь, что переменные ненулевые и содержат ожидаемые значения
<a name="bkm_04"> </a>

Прежде чем использовать переменные в рабочих процессах, убедитесь, что нет значение null, переменных. Кроме того убедитесь, что переменные содержат ожидаемые значения и имеют правильный тип данных. Для получения дополнительных сведений см  [переменных и аргументов](http://msdn.microsoft.com/en-us/library/dd489456.aspx).
  
    
    

### <a name="ensure-that-strings-in-workflow-text-fields-do-not-exceed-255-characters"></a>Убедитесь, что строки в текстовых полях рабочего процесса не превышать 255 символов
<a name="bkm_05"> </a>

Допустимый максимум для строк в текстовых полях рабочего процесса  255 знаков. Если вы настроили текстовое поле, чтобы превышать данное ограничение, его содержимое будет усечено до 255 символов.
  
    
    

### <a name="use-elevated-permissions-on-a-neutral-account-when-using-impersonation"></a>Используйте повышенного уровня разрешений на нейтральный учетной записи при использовании олицетворения
<a name="bkm_06"> </a>

При использовании олицетворения, описанных в рабочий процесс, следует создать рабочий процесс, с помощью учетной записи нейтральный (то есть, учетной записи, не привязанных к определенного пользователя). Это предотвратит нарушение, если учетная запись автора становится устаревшим по любой причине рабочих процессов.
  
    
    
Для получения дополнительных сведений см. [Создание рабочего процесса с повышенным уровнем разрешений с помощью платформы рабочих процессов SharePoint](create-a-workflow-with-elevated-permissions-by-using-the-sharepoint-workflo.md).
  
    
    

### <a name="in-reusable-workflows-use-association-columns-to-ensure-error-free-list-fields"></a>В рабочих процессов для повторного использования используйте столбцов связи для обеспечения без ошибок список полей
<a name="bkm_07"> </a>

При создании повторно используемого рабочего процесса, который зависит от необходимости определенного поля списка, может (1) ограничения рабочего процесса к типу контента, который имеет указанного поля или (2) сделать это поле столбца с связи. Вариант 2 рекомендуется, поскольку возможно, что тип контента будет изменить и рабочий процесс для приостановки выполнения.
  
    
    

### <a name="workflow-design-model-a-business-process-in-a-single-workflow"></a>Разработка рабочего процесса: модель бизнес-процессов в одного рабочего процесса
<a name="bkm_08"> </a>

Где это возможно, гораздо лучше для моделирования бизнес-процессов в один рабочий процесс, чтобы разделить логику рабочего процесса на несколько небольших рабочих процессов.
  
    
    

### <a name="workflow-design-using-the-approval-action-effectively"></a>Разработка рабочего процесса: эффективное использование действия утверждения
<a name="bkm_09"> </a>

Где это возможно, вместо создания нескольких **Approval** действий, более эффективно использовать функцию **Stages** в **Approval** операции.
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Рабочие процессы в SharePoint](workflows-in-sharepoint.md)
    
  
-  [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md)
    
  
-  [Разработка рабочих процессов в SharePoint с помощью Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  

