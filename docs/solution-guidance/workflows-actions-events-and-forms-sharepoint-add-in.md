---
title: "Рабочие процессы, действия (действия), события и форм в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: d20da3810fc6c6f0cc32eda185ec7cfd45d1f607
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="workflows-actions-activities-events-and-forms-in-the-sharepoint-add-in-model"></a>Рабочие процессы, действия (действия), события и форм в объектная модель SharePoint
=================================================================================

<a name="summary"></a>Summary
-------

Выбор подхода к реализации рабочих процессов и их связанные компоненты отличается новой модели надстройки SharePoint от был с кодом полного доверия.  В типичных полного доверия кода (FTC) / сценарий решения фермы, рабочие процессы и их связанных компонентов, разработанных с помощью кода на стороне сервера и развернуты через решений SharePoint.  Рабочие процессы и их связанных компонентов выполнялись на сервере SharePoint.

В SharePoint надстройки модели сценарии рабочие процессы и их связанных компонентов разработанных с помощью кода, который выполняется на удаленных серверах.  Зарегистрированные рабочие процессы и их компоненты, связанные со службой рабочего процесса, но весь код выполняется на удаленных серверах.

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы хотели бы предоставить со следующими рекомендациями высокого уровня для создания рабочих процессов и их связанных компонентов в новой модели надстройки SharePoint.

- Код рабочие процессы, недоступны в Office 365 клиенты или с помощью модели надстройки SharePoint в целом.
- Фоновый код все связанные с рабочими процессами и их связанные компоненты должны быть расположены в внешние веб-службы, запущенные на удаленном сервере.

<a name="options-to-create-custom-workflows-and-their-associated-components"></a>Параметры для создания настраиваемых рабочих процессов и их связанные компоненты
------------------------------------------------------------------
У вас есть несколько вариантов для создания настраиваемых рабочих процессов и их связанных компонентов.

- Создание настраиваемых рабочих процессов
- Создайте настраиваемые действия рабочего процесса
- Создание настраиваемого рабочего процесса событий
- Создание форм настраиваемых рабочих процессов

<a name="create-custom-workflows"></a>Создание настраиваемых рабочих процессов
-----------------------
В этот параметр, настраиваемых рабочих процессов создания, развертывания и связанных с веб узла в SharePoint.

- Настраиваемые рабочие процессы могут создаваться с использованием Visual Studio или SharePoint Designer.
    + В разделе [Разработка SharePoint 2013 рабочих процессов с помощью Visual Studio (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx) , который приводится сводка оба параметры и рассматриваются преимущества и недостатки каждого из них.
- Настраиваемые рабочие процессы могут развернуть и связанных с веб узла в SharePoint несколькими способами.
    - Рабочие процессы, созданные в Visual Studio автоматически упакованных внутри возможности развертывания.
    - Создания рабочих процессов в SharePoint designer необходимо экспортировать и импортировать их развертывания на сервере разработки на сервер приложений.
    - Рабочие процессы могут развернуть и связанных с веб узла в SharePoint с помощью удаленного подготовки шаблон.  В разделе [подготовки сайта (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md) для получения дополнительных сведений о шаблоне удаленного подготовки.

В следующем примере кода показано, как использовать CSOM для подготовки рабочего процесса и списки, поддерживающие рабочего процесса.

    public void ProvisionIncidentWorkflowAndRelatedLists(string incidentWorkflowFile, string suiteLevelWebAppUrl, string dispatcherName)
    {
        //Return the list the workflow will be associated with
        var incidentsList = CSOMUtil.GetListByTitle(clientContext, "Incidents");

        //Create a new WorkflowProvisionService class instance which uses the 
        //Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager to
        //provision and configure workflows
        var service = new WorkflowProvisionService(clientContext);

        //Read the workflow .XAML file
        var incidentWF = System.IO.File.ReadAllText(incidentWorkflowFile);

        //Create the WorkflowDefinition and use the 
        //Microsoft.SharePoint.Client.WorkflowServices.WorkflowServicesManager
        //to save and publish it.  
        //This method is shown below for reference.
        var incidentWFDefinitionId = service.SaveDefinitionAndPublish("Incident",
            WorkflowUtil.TranslateWorkflow(incidentWF));

        //Create the workflow tasks list
        var taskListId = service.CreateTaskList("Incident Workflow Tasks");

        //Create the workflow history list
        var historyListId = service.CreateHistoryList("Incident Workflow History");

        //Use the Microsoft.SharePoint.Client.WorkflowServices.WorkflowSubscriptionService to 
        //subscibe the workflow to the list the workflow is associated with, register the
        //events it is associated with, and register the tasks and history list. 
        //This method is shown below for reference.
        service.Subscribe("Incident Workflow", incidentWFDefinitionId, incidentsList.Id,
            WorkflowSubscritpionEventType.ItemAdded, taskListId, historyListId);
    }
    
    public Guid SaveDefinitionAndPublish(string name, string translatedWorkflows)
    {
        var definition = new WorkflowDefinition(ClientContext)
        {
            DisplayName = name,
            Xaml = translatedWorkflows
        };

        var deploymentService = workflowServicesManager.GetWorkflowDeploymentService();
        var result = deploymentService.SaveDefinition(definition);
        ClientContext.ExecuteQuery();

        deploymentService.PublishDefinition(result.Value);
        ClientContext.ExecuteQuery();

        return result.Value;
    }

    public Guid Subscribe(string name, Guid definitionId, Guid targetListId, WorkflowSubscritpionEventType eventTypes, Guid taskListId, Guid historyListId)
    {
        var eventTypesList = new List<string>();
        foreach (WorkflowSubscritpionEventType type in Enum.GetValues(typeof(WorkflowSubscritpionEventType)))
        {
            if ((type & eventTypes) > 0)
                eventTypesList.Add(type.ToString());
        }

        var subscription = new WorkflowSubscription(ClientContext)
        {
            Name = name,
            Enabled = true,
            DefinitionId = definitionId,
            EventSourceId = targetListId,
            EventTypes = eventTypesList.ToArray()
        };

        subscription.SetProperty("TaskListId", taskListId.ToString());
        subscription.SetProperty("HistoryListId", historyListId.ToString());

        var subscriptionService = workflowServicesManager.GetWorkflowSubscriptionService();
        var result = subscriptionService.PublishSubscriptionForList(subscription, targetListId);

        ClientContext.ExecuteQuery();
        return result.Value;
    }

**Когда это подходит?**

При необходимости для создания настраиваемых рабочих процессов с ним код, этот параметр, — это хорошо подходит.

**Приступая к работе**

Следующие статьи приведены инструкции для создания настраиваемых рабочих процессов.

- [Создание приложения рабочего процесса SharePoint с помощью Visual Studio 2012 г. (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [Как: создание рабочих процессов SharePoint 2013 с помощью Visual Studio (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)

<a name="create-custom-workflow-activities"></a>Создайте настраиваемые действия рабочего процесса
---------------------------------
В этот параметр, настраиваемые действия рабочего процесса создан и развернут в SharePoint.

- Настраиваемые действия рабочего процесса могут быть созданы с помощью Visual Studio.
- Настраиваемые действия рабочего процесса может быть создан с помощью SharePoint Designer.
- Настраиваемые действия рабочего процесса могут быть использованы в SharePoint Designer, после развертывания в среде SharePoint.

**Когда это подходит?**

Когда следует реализовать рабочих процессов в бизнес-процессов путем ожидания введите библиотека действий рабочих процессов в SharePoint Designer не выполняются, требования к

**Приступая к работе**

Следующей статье демонстрируется создание действий настраиваемого рабочего процесса с помощью Visual Studio.

- [Как: построение и развертывание настраиваемого действия рабочего процесса (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)

[Workflow.Activities (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) включает в себя несколько действий настраиваемого рабочего процесса, созданных с помощью Visual Studio.  Также показано, как использовать настраиваемые действия рабочего процесса в рабочий процесс.

<a name="create-custom-workflow-events"></a>Создание настраиваемого рабочего процесса событий
-----------------------------
В этот параметр, события настраиваемого рабочего процесса создан и развернут в SharePoint.

- События настраиваемый рабочий процесс может быть создан с помощью Visual Studio.
- События настраиваемый рабочий процесс может быть создан с помощью SharePoint Designer.
- Могут быть использованы события настраиваемых рабочих процессов в SharePoint Designer, после развертывания в среде SharePoint.

**Когда это подходит?**

Когда следует реализовать рабочих процессов в бизнес-процессы с требованиями требуют рабочих процессов следует ожидать в пользовательское событие перед тем как перейти.

**Приступая к работе**

[Workflow.CustomEvents (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents) демонстрируется создание рабочего процесса, который ожидает настраиваемую даже должно срабатывать, прежде чем продолжить.  Также демонстрируется использование JavaScript клиента со стороны объектной модели (JSOM) для Диспетчер служб рабочих процессов для создания настраиваемого события.

<a name="create-custom-workflow-forms"></a>Создание форм настраиваемых рабочих процессов
------------------------------------------------
В этом параметре форм пользовательских процессов создан и развернут в SharePoint.

- Форм пользовательских процессов могут быть созданы с помощью Visual Studio.
- Формы настраиваемый рабочий процесс может быть создан с помощью SharePoint Designer.
- Могут быть использованы форм настраиваемых рабочих процессов в SharePoint Designer, после развертывания в среде SharePoint.

**Когда это подходит?**

При необходимости для реализации рабочих процессов в бизнес-процессы с требованиями требуют настраиваемых форм.

**Приступая к работе**

Следующей статье показано, как создавать формы сопоставления и запуска пользовательского рабочего процесса и использовать их в рабочий процесс.

- [Как: Создание настраиваемых форм рабочих процессов SharePoint Server 2013 с помощью Visual Studio 2012 г. (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)

[Workflow.CustomTasks (PnP образец O365)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks) показано, как создать настраиваемые формы задачи и запуска и использовать их в рабочий процесс.

<a name="options-to-update-sharepoint-data-from-a-custom-workflow"></a>Параметры для обновления данных SharePoint из настраиваемого рабочего процесса
--------------------------------------------------------
У вас есть две возможности для изменения данных из настраиваемого рабочего процесса в SharePoint.

- Используйте маркер контекста и добавить в URL-адрес для проверки подлинности SharePoint.
- URL-адрес использования надстройки и веб-прокси SharePoint для проверки подлинности SharePoint.

<a name="use-the-context-token-and-add-in-web-url-to-authenticate-to-sharepoint"></a>Используйте маркер контекста и добавить в URL-адрес для проверки подлинности SharePoint
----------------------------------------------------------------------

В этот параметр, необходимо передать маркер контекста и добавить в URL-адрес из рабочего процесса службы, рабочий процесс вызывает через заголовки http.  Служба использует маркер контекста и добавить в URL-адрес для проверки подлинности в SharePoint и возвращает маркер доступа перед обновлением данных SharePoint. 

- Этот подход требует передачи контента маркер из рабочего процесса для веб-службы.

**Когда это подходит?**

Если вам требуется передача данных в SharePoint будет выполнена на уровне клиента.

**Приступая к работе**

Следующий пример показывает, как использовать маркер контекста и добавить в URL-адрес для проверки подлинности в SharePoint и изменения данных в SharePoint.

- [Workflow.CallCustomService (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)

Обратитесь к разделу [вызов Api веб-службы](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService#call-web-api-service) в [Workflow.CallCustomService (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README для получения дополнительных сведений о передаче маркер контекста и добавить в URL-адрес из рабочего процесса в службу.

Все остальные разделы [Workflow.CallCustomService (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService) README содержатся подробные сведения о всей рабочего процесса и удаленной службы и также пошаговыми руководствами для установки всех компонентов в Microsoft Azure.

<a name="use-the-add-in-web-url-and-the-sharepoint-web-proxy-to-authenticate-to-sharepoint"></a>URL-адрес использования надстройки и веб-прокси SharePoint для проверки подлинности SharePoint
---------------------------------------------------------------------------------

В этот параметр, когда вызывает рабочий процесс запускается, передаваемого Add-in web URL-адрес из рабочего процесса к службе рабочего процесса.  Служба передает Add-in web URL-адрес веб-прокси SharePoint.  Веб-прокси SharePoint использует Add-in web URL-адрес для проверки подлинности в SharePoint и возвращает маркер доступа.  После этого веб-прокси SharePoint добавляет маркер доступа заголовки http перед вызовом для изменения данных в SharePoint.

- Такой подход не требует передачи контента маркер из рабочего процесса для веб-службы.

**Когда это подходит?**

Если вам требуется передача данных в SharePoint будет выполнена на уровне сервера.

**Приступая к работе**

Следующий пример демонстрирует использование Add-in web URL-адрес и веб-прокси SharePoint для проверки подлинности в SharePoint и изменения данных в SharePoint.

- [Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)

Обратитесь к разделу [вызов Api веб-службы с помощью веб-прокси](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy#call-web-api-service-via-web-proxy) в [Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README для получения дополнительных сведений о вызове SharePoint веб-прокси.

Все остальные разделы [Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy) README содержатся подробные сведения о всей рабочего процесса и удаленной службы и также пошаговыми руководствами для установки всех компонентов в Microsoft Azure.

В разделе [запроса удаленной службы с помощью веб-прокси в SharePoint 2013 (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx) Дополнительные сведения о SharePoint веб-прокси.

<a name="related-links"></a>Ссылки по теме
=============
- [Объектная модель рабочего процесса SharePoint 2013 (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/jj163969.aspx)
- [Типичные сообщения об ошибках при разработке рабочих процессов для SharePoint (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn449112.aspx)
- [Использование средств взаимодействия рабочих процессов для SharePoint 2013 (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/jj670125.aspx)
- [Разработка рабочих процессов SharePoint 2013 с помощью Visual Studio (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/jj163199.aspx)
- [Веб-сайтов подготовки (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md)
- [Создание приложения рабочего процесса SharePoint с помощью Visual Studio 2012 г. (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn456545.aspx)
- [Как: создание рабочих процессов SharePoint 2013 с помощью Visual Studio (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn584771.aspx)
- [Как: построение и развертывание настраиваемого действия рабочего процесса (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/jj163911.aspx)
- [Как: Создание настраиваемых форм рабочих процессов SharePoint Server 2013 с помощью Visual Studio 2012 г. (статья MSDN)](https://msdn.microsoft.com/EN-US/library/office/dn518136.aspx)
- [Запроса удаленной службы с помощью веб-прокси в SharePoint 2013 (статья MSDN)](https://msdn.microsoft.com/en-us/library/office/fp179895.aspx)
- [Модули (надстройки SharePoint набора команд)](modules-sharepoint-add-in.md)
- [Веб-сайтов подготовки (добавить в SharePoint набора команд)](site-provisioning-sharepoint-add-in.md)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================
- [Workflow.Activities (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities)
- [Workflow.CustomEvents (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomEvents)
- [Workflow.CustomTasks (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CustomTasks)
- [Workflow.CallCustomService (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallCustomService)
- [Workflow.CallServiceUpdateSPViaProxy (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.CallServiceUpdateSPViaProxy)
- Примеры и содержимое в [http://aka.ms/OfficeDevPnP](http://aka.ms/OfficeDevPnP)

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D)
- SharePoint 2013 в локальной
