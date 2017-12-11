---
title: "Подготовка к Установка и настройка среды разработки рабочего процесса SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b6a3321f-4131-4a8e-9cb7-7a1b4ab9e26b
ms.openlocfilehash: 9d6afa7404fb31ad62e386f4204e1ae268e9acf9
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="prepare-to-set-up-and-configure-a-sharepoint-workflow-development-environment"></a>Подготовка к Установка и настройка среды разработки рабочего процесса SharePoint
Узнайте, как настроить среду разработки рабочего процесса для разработки рабочих процессов SharePoint в качестве самостоятельных [приложений для SharePoint](http://msdn.microsoft.com/library/fp179930.aspx) с помощью Visual Studio 2012.
## <a name="overview-of-workflow-development-in-sharepoint"></a>Общие сведения о разработке рабочих процессов в SharePoint

Несмотря на то, что рабочие процессы были частью SharePoint начиная с более ранними версиями, рабочих процессов для SharePoint — это много расширенные и улучшенные возможности платформы. 
  
    
    

- Во-первых рабочие процессы SharePoint теперь основанные на  [Windows Workflow Foundation 4.5](http://msdn.microsoft.com/library/dd489441%28v=vs.110%29), которая является частью .NET Framework 4.5.
    
  
- Во-вторых ядро выполнения рабочего процесса, [Диспетчер рабочих процессов](http://msdn.microsoft.com/library/windowsazure/jj193528%28v=azure.10%29.aspx), была отделена от SharePoint и выполняется независимо друг от друга. Это обеспечивает гибкость и масштабируемость. (Внимание, что для обеспечения обратной совместимости обработчик прежних версий workflow 2010 остается частью SharePoint).
    
  
- Вместо разработка рабочих процессов путем написания кода C#, создание рабочих процессов в Visual Studio с помощью конструктора рабочих процессов, поддерживающей декларативные выражения.
    
  
- Интеграция рабочих процессов SharePoint с новой модели приложений, что означает, что вы можете теперь реализовать рабочих процессов в SharePoint надстройки.
    
  
- Вы также можете создавать рабочих процессов SharePoint с помощью SharePoint Designer 2013. Для получения дополнительных сведений см [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md).
    
  

### <a name="get-started"></a>Начало работы

Сначала off и познакомьтесь с новой модели приложений и концепцию Надстройки SharePoint, окунув на следующие: 
  
    
    

|||
|:-----|:-----|
| [SharePoint для разработчиков](http://msdn.microsoft.com/en-us/sharepoint) <br/> |Портал для разработчиков на сайте SharePoint, где внимание уделяется приложений для SharePoint.  <br/> |
| [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx) <br/> |Узнайте, что такое приложений для SharePoint, зачем создавать их и базовых принципах, необходимых для их создания в SharePoint.  <br/> |
| [Новое название приложений для SharePoint](http://msdn.microsoft.com/library/05b07b04-6c8b-4b7e-bd86-e32c589dfead%28Office.15%29.aspx) <br/> |Портал разработчиков сайт, предназначенный для создания приложений для Office и приложений для SharePoint.  <br/> |
| [Обзор разработки решений для SharePoint](sharepoint-development-overview.md) <br/> |SharePoint — это платформа разработки приложений для SharePoint и фермы решения. Познакомьтесь с возможностях и функциях SharePoint, чтобы начать разработку.  <br/> |
| [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md) <br/> |В этой статье представлен высокоуровневый обзор инфраструктуры рабочих процессов в SharePoint, в том числе описание архитектуры платформы и мост взаимодействия рабочих процессов.  <br/> |
   
Следующим шагом является убедитесь, что у вас есть установки среды разработки актуальных рабочего процесса. Не требуется для разработки на сервере SharePoint, но конечно требует установки SharePoint Server для разработки с помощью.
  
    
    
Ниже приведены компоненты, необходимые. Важно установить эти элементы в указанном порядке:
  
    
    

1. **Установка среды SharePoint**
    
  -  [Обновление SharePoint (KB2767999)](http://support.microsoft.com/kb/2767999)
    
  
  - Кроме того можно подписаться на  [среды разработки Office 365](http://msdn.microsoft.com/library/office/apps/fp179924%28v=office.15%29)
    
  
2. **Установка среды диспетчера рабочих процессов**
    
  -  [Накопительный пакет диспетчера рабочих процессов версии 1.0 (KB2799754)](http://support.microsoft.com/kb/2799754/en-us)
    
  
3. **Установка среды разработки Visual Studio 2012**
    
  -  [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/downloads#vs)
    
  
  -  [Visual Studio 2012 обновления 2 (KB2797912)](http://support.microsoft.com/kb/2797912)
    
  
  -  [Обновление .NET framework 4.5 (KB2750149)](http://support.microsoft.com/kb/2750149/en-us)
    
  
  -  [Office Developer Tools для Visual Studio 2012](http://aka.ms/OfficeDevToolsForVS2012)
    
  

### <a name="if-you-have-the-preview-version"></a>Если установлена версия «Версия»

Если предварительные (то есть, "Просмотр") версии SharePoint Server, Workflow Manager 1.0 или Инструменты разработчика Office для Visual Studio 2013 (версий до марта 2013 г.), необходимо обновить установки. Ниже приведен список соответствующих обновлений:
  
    
    

-  [Обновление SharePoint (KB2767999)](http://support.microsoft.com/kb/2767999)
    
  
-  [Microsoft Azure шины 1.0 накопительный пакет обновления (KB2799752)](http://support.microsoft.com/kb/2799752/en-us)
    
  
-  [Накопительный пакет диспетчера рабочих процессов версии 1.0 (KB2799754)](http://support.microsoft.com/kb/2799754/en-us)
    
  

### <a name="you-must-also-update-workflow-projects-created-with-the-preview-version"></a>Также необходимо обновить рабочий процесс проекты, созданные с версией «Версия»

Версии компонентов Visual Studio рабочего процесса и их соответствующие обновления внесены важные изменения, которые улучшают работу производительность, масштабируемость и надежность. К сожалению эти обновления необходимо обновить проектов рабочих процессов, созданных с помощью средства просмотра.
  
    
    
Чтобы упростить этот процесс, мы предоставляют средство преобразования, можно получить через CodePlex. Средство вызывается [Конвертер рабочего процесса SharePoint для Visual Studio 2012](http://wfconverter.codeplex.com/).
  
    
    
Ниже представлена сводка изменений, которые необходимо обновить проекты рабочего процесса:
  
    
    

- Справочные материалы действия, которые **Item Guid** заменяются **Item Id**. Эти изменения имеют важных последствия:
    
  - [LookupSPListItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.LookupSPListItemGuid.aspx) и [GetCurrentItemGuid](https://msdn.microsoft.com/library/Microsoft.SharePoint.WorkflowServices.Activities.GetCurrentItemGuid.aspx) действия удаляются из инструментарий; их замены действий, **LookupSPListItemId** и **GetCurrentItemId**.
    
  
  - На другие задачи, использующие **Item Guid**вы найдете **Item Id** добавлена и **Item Guid** скрытым. Существующие проекты, использующие **Item Guid** будет продолжать работать (за исключением очень большие списки, содержащие более 5000 элементов, которая является одной из причин для изменения).
    
  
- Существует новый формат упаковки для рабочих процессов в приложениях.
    
  
- Справочник по сборке действий рабочего процесса в XAML был изменен для указания на новый прокси-сервера во время разработки сборки вместо фактических действий сборки пакета обновления.
    
  

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Настройка локальной среды разработки надстроек SharePoint](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [Что нового в рабочих процессах для SharePoint](what-s-new-in-workflows-for-sharepoint.md)
    
  
-  [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
-  [Рабочие процессы в SharePoint](workflows-in-sharepoint.md)
    
  

