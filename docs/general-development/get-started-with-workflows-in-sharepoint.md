---
title: "Начало работы с рабочими процессами SharePoint"
ms.date: 09/25/2017
keywords: vs.sharepointtools.workflow4.workflowlist,VS.SharePointTools.Workflow4.WorkflowName
f1_keywords: vs.sharepointtools.workflow4.workflowlist,VS.SharePointTools.Workflow4.WorkflowName
ms.prod: sharepoint
ms.assetid: a2643cd7-474d-4e4c-85bb-00f0b6685a1d
ms.openlocfilehash: ae4354d1659ab4b70ea11a35f88c7fb8553e4048
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-workflows-in-sharepoint"></a>Начало работы с рабочими процессами SharePoint
Информация о недавно разработанном Workflow Manager Client 1.0, который обеспечивает инфраструктуру для рабочих процессов в SharePoint и метод интеграции рабочих процессов SharePoint с новой Модель для надстроек SharePoint.
> **Важно!** Инструкции по установке и настройке SharePoint и Microsoft Azure см. в статье [Установка и настройка диспетчера рабочих процессов SharePoint](set-up-and-configure-sharepoint-workflow-manager.md). 
  
    
    


## <a name="overview-of-workflows-in-sharepoint"></a>Обзор рабочего процесса в SharePoint
<a name="overview"> </a>

Рабочие процессы в SharePoint позволяют моделировать и автоматизировать бизнес-процессы. Эти процессы могут быть такими же простыми, как процесс утверждения документа одним утверждающим лицом (как показано на рис. 1), такими же сложными, как каталог товаров для клиентов, использующий вызовы веб-служб и поддержку базы данных, или такими же значительными, как практически любой структурированный бизнес-процесс, полный условий, циклов, входными данными пользователя, задачами и настраиваемыми действиями.
  
    
    

**Рисунок 1. Простой рабочий процесс SharePoint**

  
    
    

  
    
    
![Простой рабочий процесс](../images/wfSimple.gif)
  
    
    

  
    
    
SharePoint отмечает введение Workflow Manager Client 1.0 в качестве новой мощной платформы для рабочих процессов Visual Studio. Workflow Manager Client 1.0, созданный на Windows Workflow Foundation 4, имеет преимущества по сравнению с предыдущими версиями, которые отражают приверженность SharePoint к Модель для надстроек SharePoint и облачным вычислениям. Дополнительную информацию об этих изменениях можно посмотреть в статьях  [Что нового в рабочих процессах для SharePoint](what-s-new-in-workflows-for-sharepoint.md) и [Основные сведения о рабочих процессах в SharePoint](sharepoint-workflow-fundamentals.md).
  
    
    
Пожалуй, самым важным для разработчиков рабочих процессов является значительное усовершенствование и упрощение метода создания рабочих процессов. В настоящее время полностью декларативными (то есть на основе конструктора, а не кода) являются не только рабочие процессы, но и основные среды разработки рабочих процессов, такие как Visual Studio 2012 и SharePoint Designer 2013, которые были оптимизированы и упрощены.
  
    
    
Далее перечислены основные усовершенствования рабочих процессов в SharePoint. Более подробную информацию о новых возможностях рабочих процессов для SharePoint можно посмотреть в статье  [Что нового в рабочих процессах для SharePoint](what-s-new-in-workflows-for-sharepoint.md).
  
    
    

- Расширенные возможности подключения к облачному выполнению рабочих процессов. В действительности в SharePoint между локальными рабочими процессами и рабочими процессами на основе Office 365 нет абсолютно никакой разницы.
    
  
- Рабочие процессы SharePoint 2010, которые включаются с помощью  [Взаимодействие рабочих процессов SharePoint ](sharepoint-workflow-fundamentals.md#bkm_InteropBridge), полностью совместимы в SharePoint.
    
  
- Расширенная выразительность разработки с помощью событий и действий Visual Studio, веб-служб и классических программных структур в декларативной среде без использования кода.
    
  
- Масштабируемость и надежность, соответствующие требованиям для Office 365и модели облачных приложений.
    
  
- Усовершенствованная надежность связи для повышения уровня высокофункциональных интегрированных систем. Возможность вызывать рабочие процессы и управлять или из любой внешней системы. Кроме того, рабочий процесс может выполнять вызовы веб-служб для любого потока или источника данных с помощью протоколов HTTP, SOAP, протокола передачи данных (OData) и представления репрезентативного состояния (REST).
    
  
- Расширенные возможности разработки в SharePoint Designer 2013 для неспециалистов и возможность создания логики рабочих процессов в Visio.
    
  
- Улучшенная, но все же упрощенная разработка рабочих процессов в Visual Studio, включая поддержку для настраиваемых действий рабочих процессов, быстрая разработка в декларативной среде, развертка в один шаг и поддержка при разработке Надстройки SharePoint.
    
  
- Полная поддержка для Надстройки SharePoint на базе рабочих процессов, где рабочие процессы выполняют функции среднего уровня управления бизнес-процессами.
    
  

## <a name="workflow-manager-client-10-and-the-model-for-sharepoint-add-ins"></a>Workflow Manager Client 1.0 и Модель для надстроек SharePoint
<a name="bm_appModel"> </a>

Visual Studio 2012 оптимизирован для разработки Надстройки SharePoint на основе рабочих процессов и использования огромной мощи и гибкости Модель для надстроек SharePoint. Вы можете использовать объектную модель рабочих процессов SharePoint, чтобы включить логику рабочих процессов в основу приложения SharePoint таким образом, что конечные пользователи будут взаимодействовать с поверхностью самого приложения, в то время как приложение будет работать за счет логики рабочих процессов.
  
    
    
Кроме того, Visual Studio 2012 идеально подходит для разработки Надстройки Office, которые могут запускать рабочие процессы изнутри приложения Microsoft Office.
  
    
    

## <a name="authoring-sharepoint-workflows"></a>Разработка рабочих процессов SharePoint
<a name="bm_authoringwf"> </a>

Существует две основные среды разработки для Workflow Manager Client 1.0: SharePoint Designer 2013 и Visual Studio. Кроме того, нетехнические работники могут использовать Visio, чтобы построить логику рабочего процесса, которую можно импортировать в SharePoint Designer и собрать в проект рабочего процесса SharePoint.
  
    
    
Тем не менее, основными средами разработки являются Visual Studio 2012 и SharePoint Designer 2013. Чтобы определить, какое из этих решений подойдет вам лучше всего, ознакомьтесь со сравнительной таблицей из раздела  [Сравнение SharePoint Designer с Visual Studio](develop-sharepoint-workflows-using-visual-studio.md#bkm_Comparing).
  
    
    

## <a name="sharepoint-designer-2013-as-workflow-authoring-tool"></a>SharePoint Designer 2013 как средство разработки рабочих процессов
<a name="bm_spd"> </a>

Во многом SharePoint Designer 2013 является средством для разработки рабочих процессов SharePoint. Несмотря на то что некоторые расширенные задачи (например, создание дополнительных действий) требуют вмешательства со стороны разработчика с использованием Visual Studio, SharePoint Designer 2013 обеспечивает самый гибкий способ разработки рабочих процессов для самого широкого круга пользователей.
  
    
    

## <a name="create-a-workflow-using-visual-studio-2012"></a>Создание рабочего процесса с помощью Visual Studio 2012
<a name="create"> </a>

Visual Studio 2012 имеет встроенные типы проектов рабочих процессов SharePoint. Чтобы создать проект рабочего процесса SharePoint в Visual Studio, выполните описанные ниже действия.
  
    
    

### <a name="to-create-a-workflow-using-visual-studio"></a>Чтобы создать рабочий процесс с помощью Visual Studio:


1. Откройте Visual Studio 2012 и создайте новый проект. В диалоговом окне **Создать проект** выберите пункт **Шаблоны**, **Visual C#**, **Office SharePoint**, **Решения SharePoint** и **Проект SharePoint**, как показано на рис. 2.
    
   **Рисунок 2. Диалоговое окно "Создать проект"**

  

  ![Диалоговое окно "Создание проекта"](../images/wfNewProject_b2.png)
  

  

  
2. В созданном проекте выберите в меню **Проект** команду **Добавить новый элемент**, а затем выберите в разделе **Office SharePoint** пункт **Рабочий процесс**, как показано на рис. 3.
    
   **Рисунок 3. Диалоговое окно "Добавить новый элемент"**

  

  ![Диалоговое окно "Добавление нового элемента"](../images/wfAddNewItemDialog_b2.png)
  

  

  
3. После создания проекта рабочего процесса перед вами появится область конструктора для создания рабочего процесса. Среда разработки рабочего процесса содержит настраиваемую панель элементов с большим набором элементов разработки рабочего процесса.
    
   **Рисунок 4. Панель инструментов разработки рабочего процесса в Visual Studio**

  

  ![Панель элементов рабочего процесса](../images/wfToolbox_b2.png)
  

  

  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="information"> </a>

Более подробную информацию о **Надстройки SharePoint** можно найти в следующих статьях:
  
    
    

-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Что следует рассмотреть, прежде чем приступать к разработке надстроек SharePoint](http://msdn.microsoft.com/library/0942fdce-3227-496a-8873-399fc1dbb72c%28Office.15%29.aspx)
    
  
-  [Важные аспекты архитектуры и разработки надстройки SharePoint](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx)
    
  
-  [Работа с внешними данными в SharePoint](http://msdn.microsoft.com/library/1534a5f4-1d83-45b4-9714-3a1995677d85%28Office.15%29.aspx)
    
  
Более подробную информацию о разработке рабочих процессов с использованием **Visual Studio 2012** и **SharePoint Designer 2013** можно найти в следующих статьях:
  
    
    

-  [Разработка рабочих процессов в SharePoint с помощью Visual Studio](develop-sharepoint-workflows-using-visual-studio.md)
    
  
-  [Разработка рабочих процессов в SharePoint Designer и Visio](workflow-development-in-sharepoint-designer-and-visio.md)
    
  
Более подобную информацию о Windows Workflow Foundation 4 можно найти в следующих статьях: 
  
    
    

-  
  [Краткое описание Windows Workflow Foundation (WF) в .NET 4 для разработчика](http://msdn.microsoft.com/en-us/library/ee342461.aspx)
    
  
-  
  [Новые возможности в Windows Workflow Foundation](http://msdn.microsoft.com/en-us/library/dd489410%28v=vs.110%29.aspx)
    
  
-  [Первые шаги с Windows Workflow Foundation](http://msdn.microsoft.com/en-us/netframework/first-steps-with-wf.aspx)
    
  
-  
  [Путь рабочего процесса. Общие сведения о Windows Workflow Foundation](http://msdn.microsoft.com/en-us/library/dd851337.aspx)
    
  
-  
  [Общие сведения об обработчике правил для Windows Workflow Foundation](http://msdn.microsoft.com/en-us/library/dd554919.aspx)
    
  
-  
  [Интеграция Windows Workflow Foundation и Windows Communication Foundation](http://msdn.microsoft.com/en-us/library/cc626077.aspx)
    
  

