---
title: "PerformancePoint Services в SharePoint"
ms.date: 09/25/2017
keywords: "доступ к fco определений в SharePoint, бизнес-аналитики в SharePoint с использованием служб performancepoint services, бизнес-аналитики в SharePoint, бизнес-аналитики с помощью performancepoint services в SharePoint, создание преобразования системы показателей с помощью performancepoint в Настройка performancepoint в sharepoint, создание источника данных в SharePoint, библиотеки DLL, используемые для разработки performancepoint расширение performancepoint services для SharePoint, элемент управления настраиваемого фильтра в SharePoint, расширения настраиваемых performancepoint Фильтр, SharePoint, FCO в sharepoint performancepoint, создание фильтров в SharePoint, как FCO в pps performancepoint, Приступая к работе со службами performancepoint services, интеграции служб performancepoint services в sharepoint, сборки performancepoint используется в разработке, performancepoint пользовательские источники данных, настраиваемые фильтры performancepoint, настраиваемые отчеты performancepoint performancepoint преобразований системы показателей, сценариях разработки performancepoint, служб performancepoint services Создание в SharePoint, отчет отчетов разработки, сценарии разработки performancepoint services, программирование служб performancepoint services, sdk performancepoint services, нестандартные панели мониторинга pps в SharePoint, разработка pps, программирование pps, pps sdk Модуль подготовки в SharePoint, приложения-службы SharePoint PerformancePoint"
f1_keywords:
- accessing fco definitions in SharePoint,bi in SharePoint using performancepoint services,business intelligence in SharePoint,business intelligence using performancepoint services in SharePoint,create scorecard transforms using performancepoint in SharePoint,custom filter control in SharePoint,custom performancepoint extensions,customize performancepoint in sharepoint,data source creation in SharePoint,dlls used for performancepoint development,extending performancepoint services for sharepoint,fcos in sharepoint performancepoint,filter creation in SharePoint,filters as fcos in pps performancepoint,getting started with performancepoint services,integration of performancepoint services in sharepoint,performancepoint assemblies used in development,performancepoint custom data sources,performancepoint custom filters,performancepoint custom reports,performancepoint custom scorecard transforms,performancepoint development scenarios,performancepoint services development,performancepoint services development scenarios,performancepoint services programming,performancepoint services sdk,pps custom dashboards in SharePoint,pps development,pps programming,pps sdk,report creation in SharePoint,report renderer in SharePoint,SharePoint service application PerformancePoint
ms.prod: sharepoint
ms.assetid: fb159708-d6b4-40c1-b5cc-4bb2071a7930
ms.openlocfilehash: ce0a29e9adba8e1606088444a2189f2f62bc4301
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="performancepoint-services-in-sharepoint"></a><span data-ttu-id="0a921-103">PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-103">PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="0a921-104">Ознакомьтесь с поддерживаемым сценариям разработки и архитектура расширения для служб PerformancePoint Services в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a921-104">Learn about supported development scenarios and the extensibility architecture for PerformancePoint Services in SharePoint.</span></span>
<span data-ttu-id="0a921-105">PerformancePoint Services — это приложение службы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0a921-105">PerformancePoint Services is a SharePoint service application.</span></span> <span data-ttu-id="0a921-106">Она позволяет пользователям создавать бизнес-аналитики (BI) панелей мониторинга, которые обеспечивают представление о производительности организации.</span><span class="sxs-lookup"><span data-stu-id="0a921-106">It enables users to create business intelligence (BI) dashboards that provide insight into an organization's performance.</span></span> <span data-ttu-id="0a921-107">Можно создать настраиваемых отчетов, фильтров, табличных источников данных и преобразований систем показателей для расширения встроенных функций служб PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="0a921-107">You can create custom reports, filters, tabular data sources, and scorecard transforms to extend the native functionality of PerformancePoint Services.</span></span> <span data-ttu-id="0a921-108">Например можно создать визуализации настраиваемого отчета, который оптимизирован для медицинского обслуживания отрасли и его интеграции в для повторного использования вертикальное решение.</span><span class="sxs-lookup"><span data-stu-id="0a921-108">For example, you can create a custom report visualization that is optimized for the medical industry and then integrate it into a reusable vertical solution.</span></span>
  
    
    


## <a name="custom-performancepoint-services-reports-filters-and-tabular-data-sources-in-sharepoint"></a><span data-ttu-id="0a921-109">Пользовательские отчеты служб PerformancePoint Services, фильтров и табличных источников данных в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-109">Custom PerformancePoint Services reports, filters, and tabular data sources in SharePoint</span></span>
<span data-ttu-id="0a921-110"><a name="bkmk_CreateCustomObjects"> </a></span><span class="sxs-lookup"><span data-stu-id="0a921-110"></span></span>

<span data-ttu-id="0a921-p102">Собственная Службы PerformancePoint Services  [ReportView](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.aspx) , [Filter](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.aspx) и табличные [DataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.aspx) объекты можно расширять путем определения пользовательского значения для их свойства. Настраиваемый отчет, фильтров и расширений табличных источников данных обычно включают три компонента: обработчик или поставщик, приложение редактирования и метаданные расширения.</span><span class="sxs-lookup"><span data-stu-id="0a921-p102">You can extend native PerformancePoint Services  [ReportView](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.aspx) , [Filter](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.aspx) , and tabular [DataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.aspx) objects by defining custom values for their properties. Custom report, filter, and tabular data source extensions typically include three components: a renderer or provider, an editor application, and extension metadata.</span></span>
  
    
    

### <a name="renderers-and-providers-for-performancepoint-services-extensions"></a><span data-ttu-id="0a921-113">Средств отображения и поставщиков для расширения Службы PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="0a921-113">Renderers and providers for PerformancePoint Services extensions</span></span>

<span data-ttu-id="0a921-p103">Тип объекта, который вы расширяете определяет, используется ли обработчик или поставщик. Использование средств отображения отчетов и фильтров расширения и фильтрации и расширения источника данных используйте поставщиков.</span><span class="sxs-lookup"><span data-stu-id="0a921-p103">The type of object that you are extending determines whether it uses a renderer or a provider. Report and filter extensions use renderers, and filter and data source extensions use providers.</span></span>
  
    
    

- <span data-ttu-id="0a921-116">Для визуализации отчета расширению отчета требуется обработчик.</span><span class="sxs-lookup"><span data-stu-id="0a921-116">Report extensions require a renderer for the report visualization.</span></span> 
    
  
- <span data-ttu-id="0a921-p104">Фильтр расширению отчета требуется обработчик для элемента управления выбора. Средство визуализации может быть собственный модуль подготовки отчетов или собственный Службы PerformancePoint Services визуализации. При использовании визуализации Службы PerformancePoint Services его просто зарегистрировать в расширении. Если вы используете собственный модуль подготовки отчетов, необходимо включить его в расширении.</span><span class="sxs-lookup"><span data-stu-id="0a921-p104">Filter extensions require a renderer for the selection control. The renderer can be a custom renderer or a native PerformancePoint Services renderer. If you are using a PerformancePoint Services renderer, you simply register it in your extension. If you are using a custom renderer, you must also include it in your extension.</span></span>
    
  
- <span data-ttu-id="0a921-121">Фильтр расширению отчета требуется поставщик данных для подключения к базовому источнику данных.</span><span class="sxs-lookup"><span data-stu-id="0a921-121">Filter extensions require a data provider to connect to the underlying data source.</span></span>
    
  
- <span data-ttu-id="0a921-122">Расширениям источников данных для подключения к базовому источнику данных требуется поставщик.</span><span class="sxs-lookup"><span data-stu-id="0a921-122">Data source extensions require a provider to connect to the underlying data source.</span></span>
    
  
<span data-ttu-id="0a921-123">Для получения дополнительных сведений о создании средств отображения и поставщиков в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="0a921-123">For more information, see the following topics about creating renderers and providers:</span></span>
  
    
    

-  [<span data-ttu-id="0a921-124">Как: создание средств отображения отчетов для PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-124">How to: Create report renderers for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0a921-125">Как: создать фильтр поставщиков данных для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-125">How to: Create filter data providers for PerformancePoint Services in SharePoint</span></span>](how-to-create-filter-data-providers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0a921-126">Как: Создание поставщиков табличных источников данных для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-126">How to: Create tabular data source providers for PerformancePoint Services in SharePoint</span></span>](how-to-create-tabular-data-source-providers-for-performancepoint-services-in-sha.md)
    
  

### <a name="editor-applications-for-performancepoint-services-extensions-in-sharepoint"></a><span data-ttu-id="0a921-127">Редактор приложений для расширения служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-127">Editor applications for PerformancePoint Services extensions in SharePoint</span></span>

<span data-ttu-id="0a921-p105">Настраиваемые редакторы позволяют пользователям определение свойств для настраиваемого объекта, взаимодействия с объектами в репозитории и инициализация конечных точек для настраиваемых отчетов и фильтры. Редактора должны предоставлять свойства, чтобы разрешить пользователям просматривать и изменять. Редакторы можно открыть из объектов в Конструктор панели мониторинга PerformancePoint или из элементов в список контента PerformancePoint или библиотеки подключений к данным PerformancePoint. Чтобы интегрировать в Конструктор панели мониторинга взаимодействия при разработке, должен иметь возможность открыть из универсальный код ресурса (URI), редактора и URI должна быть зарегистрирована для настраиваемого объекта в файле web.config Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="0a921-p105">Custom editors enable users to define properties for a custom object, interact with objects in the repository, and initialize endpoints for custom reports and filters. Your editor should expose the properties that you want to enable users to view and modify. Editors can be opened from objects in PerformancePoint Dashboard Designer or from items in the PerformancePoint Content List or PerformancePoint Data Connections Library. To integrate into the Dashboard Designer authoring experience, your editor must be able to open from a uniform resource identifier (URI), and the URI must be registered for the custom object in the PerformancePoint Services web.config file.</span></span>
  
    
    
<span data-ttu-id="0a921-132">Дополнительные сведения о создании редакторы в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="0a921-132">For more information about creating editors, see the following topics:</span></span>
  
    
    

-  [<span data-ttu-id="0a921-133">Как: создать отчет редакторы для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-133">How to: Create report editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-report-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0a921-134">Как: создать фильтр редакторы для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-134">How to: Create filter editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="0a921-135">Как: создание табличных данных редакторы исходного для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-135">How to: Create tabular data source editors for PerformancePoint Services in SharePoint</span></span>](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
> [!NOTE]
> <span data-ttu-id="0a921-136">[!Примечание] Конструктор панели мониторинга PerformancePoint позволяет создавать и удалять пользовательские объекты, поэтому редактора необходимо предоставить логику для создания или удаления объектов.</span><span class="sxs-lookup"><span data-stu-id="0a921-136">PerformancePoint Dashboard Designer can create and delete custom objects, so your editor does not need to provide logic for creating or deleting objects.</span></span> 
  
    
    


### <a name="configuration-metadata-for-performancepoint-services-extensions-in-sharepoint"></a><span data-ttu-id="0a921-137">Метаданные конфигурации для расширения служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-137">Configuration metadata for PerformancePoint Services extensions in SharePoint</span></span>

<span data-ttu-id="0a921-p106">Необходимо указать метаданных для расширения в файле web.config Службы PerformancePoint Services во время установки. Метаданные включает в себя **type**, **subType**, **RendererClass**, **EditorURI**и **Resources** атрибуты.</span><span class="sxs-lookup"><span data-stu-id="0a921-p106">You must specify metadata for your extension in the PerformancePoint Services web.config file during the installation process. The metadata includes **type**, **subType**, **RendererClass**, **EditorURI**, and **Resources** attributes.</span></span>
  
    
    
<span data-ttu-id="0a921-p107">Для создания настраиваемого объекта, Конструктор панели мониторинга возвращает объект метаданных из файла web.config Службы PerformancePoint Services и затем создает объект в качестве типа контента в хранилище Конструктор панели мониторинга. После создания настраиваемого объекта, Конструктор панели мониторинга отображается ссылка в редактор.</span><span class="sxs-lookup"><span data-stu-id="0a921-p107">To create a custom object, Dashboard Designer retrieves the object's metadata from the PerformancePoint Services web.config file and then creates the object as a content type in the Dashboard Designer repository. After creating the custom object, Dashboard Designer displays a link to the editor.</span></span>
  
    
    
<span data-ttu-id="0a921-142">Дополнительные сведения о метаданные расширения можно  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a921-142">For more information about extension metadata, see  [How to: Manually Register PerformancePoint Services Extensions](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).</span></span>
  
    
    

## <a name="custom-transforms-for-performancepoint-services-scorecards-in-sharepoint"></a><span data-ttu-id="0a921-143">Настраиваемых преобразований для систем показателей PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-143">Custom transforms for PerformancePoint Services scorecards in SharePoint</span></span>
<span data-ttu-id="0a921-144"><a name="bkmk_CreateCustomObjects"> </a></span><span class="sxs-lookup"><span data-stu-id="0a921-144"></span></span>

<span data-ttu-id="0a921-p108">Преобразований изменение внешнего вида, содержимого или функциональные возможности систем показателей перед запроса источника данных, после запроса источника данных или перед отображением системы показателей в веб-части. Например, Службы PerformancePoint Services используются преобразования нужно выполнить несколько операций перед отображением представления системы показателей, таких как развертывание именованные наборы, вычислений накопительные пакеты обновления и сетей статистические выражения. Эти изменения применяются во время выполнения и не изменяйте в определении объекта системы показателей.</span><span class="sxs-lookup"><span data-stu-id="0a921-p108">Transforms change the appearance, contents, or functionality of scorecards before querying the data source, after querying the data source, or before rendering the scorecard in the Web Part. For example, PerformancePoint Services uses transforms to perform several operations before rendering a scorecard view, such as expanding named sets, computing rollups, and computing aggregations. These changes are applied at run time and they do not modify the definition of the scorecard object.</span></span>
  
    
    
<span data-ttu-id="0a921-148">Дополнительные сведения о преобразований системы показателей можно [как: создать преобразования системы показателей для служб PerformancePoint Services в SharePoint](how-to-create-scorecard-transforms-for-performancepoint-services-in-sharepoint-2.md).</span><span class="sxs-lookup"><span data-stu-id="0a921-148">For more information about scorecard transforms, see  [How to: Create scorecard transforms for PerformancePoint Services in SharePoint](how-to-create-scorecard-transforms-for-performancepoint-services-in-sharepoint-2.md).</span></span>
  
> [!NOTE]
> <span data-ttu-id="0a921-p109">[!Примечание] Если преобразование изменяет значения данных в системе показателей, изменения распространяются напрямую в отчеты стратегической карты, использующие эту систему в качестве источника данных. Кроме того, изменения в системе показателей могут повлиять на отчеты о ключевых показателях эффективности.</span><span class="sxs-lookup"><span data-stu-id="0a921-p109">If a transform modifies the data values in a scorecard, the changes propagate directly to Strategy Map reports that use the scorecard as a data source. In addition, changes to scorecards may affect KPI Details reports.</span></span> 
  
    
    


## <a name="extensibility-architecture-for-performancepoint-services-in-sharepoint"></a><span data-ttu-id="0a921-151">Архитектура расширения для служб PerformancePoint Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-151">Extensibility architecture for PerformancePoint Services in SharePoint</span></span>
<span data-ttu-id="0a921-152"><a name="bkmk_PerfPointArch"> </a></span><span class="sxs-lookup"><span data-stu-id="0a921-152"></span></span>

<span data-ttu-id="0a921-153">Поддерживаемые расширения выполняются в рамках экземпляра приложения Службы PerformancePoint Services на интерфейсном веб-сервере или на сервере приложений, как показано на следующей схеме.</span><span class="sxs-lookup"><span data-stu-id="0a921-153">Supported extensions run within a PerformancePoint Services application instance, either on the front-end web server or on the application server, as shown in the following diagram.</span></span>
  
    
    

<span data-ttu-id="0a921-154">**Рисунок 1. Архитектура расширяемости PerformancePoint Services**</span><span class="sxs-lookup"><span data-stu-id="0a921-154">**Figure 1. PerformancePoint Services extensibility architecture**</span></span>

  
    
    

  
    
    
![Точки расширения служб PerformancePoint](../images/SPS14_PerfPoint_ArchOverview.gif)
  
    
    

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-front-end-web-server"></a><span data-ttu-id="0a921-156">Расширения служб PerformancePoint Services, которые запускаются на интерфейсном веб-сервере SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-156">PerformancePoint Services extensions that run on the SharePoint front-end web server</span></span>

<span data-ttu-id="0a921-p110">Настраиваемые редакторы (и другие поддерживаемые настраиваемые приложения), выполните на интерфейсном веб-сервере в рамках экземпляра приложения Службы PerformancePoint Services. Редакторы обычно развертываются как ASPX-страницы и устанавливаются в путь  `%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS`. Редакторы вызова  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) объектов или объектов [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) для автора или процесс содержимое, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0a921-p110">Custom editors (and other supported custom applications) run on the front-end web server within a PerformancePoint Services application instance. Editors are typically deployed as .aspx pages and are installed in the path  `%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS`. Editors call the  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) object or [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) object to author or process content, as follows:</span></span>
  
    
    

- <span data-ttu-id="0a921-160">Объекты отчетов и фильтров следует использовать  [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) для всех задач репозитория.</span><span class="sxs-lookup"><span data-stu-id="0a921-160">Report and filter objects should use  [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) for all repository tasks.</span></span>
    
  
- <span data-ttu-id="0a921-p111">Объекты источника данных следует использовать для выполнения задач, **Create** и **Update**, чтобы эти задачи выполняются в контексте приложения-службы Службы PerformancePoint Services [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) . **Read** (get) и **Delete** задачи выполняются с помощью [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) или [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) . (Однако пользовательских данных источника приложения, которые запускаются на сервере приложений могут вызывать [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) непосредственно.)</span><span class="sxs-lookup"><span data-stu-id="0a921-p111">Data source objects should use  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) to perform **Create** and **Update** tasks so that these tasks are performed within the context of the PerformancePoint Services service application. **Read** (get) and **Delete** tasks can be performed by using [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) or [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) . (However, custom data source applications that run on the application server can call [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) directly.)</span></span>
    
  

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-application-server"></a><span data-ttu-id="0a921-164">Расширения служб PerformancePoint Services, которые запускаются на сервере приложений SharePoint</span><span class="sxs-lookup"><span data-stu-id="0a921-164">PerformancePoint Services extensions that run on the SharePoint application server</span></span>

<span data-ttu-id="0a921-p112">Настраиваемых средств отображения, поставщиков и преобразования системы показателей, выполните на сервере приложений. Сервер приложений содержит среднего уровня бизнес-логики для экземпляра Службы PerformancePoint Services.</span><span class="sxs-lookup"><span data-stu-id="0a921-p112">Custom renderers, providers, and scorecard transforms run on the application server. The application server hosts the middle-tier business logic for the PerformancePoint Services instance.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="0a921-167">См. также</span><span class="sxs-lookup"><span data-stu-id="0a921-167">See also</span></span>
<span data-ttu-id="0a921-168"><a name="bkmk_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="0a921-168"></span></span>


-  [<span data-ttu-id="0a921-169">Базовые концепции разработки PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="0a921-169">Fundamentals of PerformancePoint Services Development</span></span>](http://msdn.microsoft.com/library/5d2c183b-95f8-4930-b6d0-f3ffe1ee166e%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0a921-170">Примеры кода для PerformancePoint Services в SharePoint Server 2010</span><span class="sxs-lookup"><span data-stu-id="0a921-170">Code Samples for PerformancePoint Services in SharePoint Server 2010</span></span>](http://msdn.microsoft.com/library/97f0cbd4-03ef-44f8-9869-699df9d9c97f%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="0a921-171">Устранение неполадок вопросы и ответы по разработке PerformancePoint Services</span><span class="sxs-lookup"><span data-stu-id="0a921-171">Troubleshooting and FAQs for PerformancePoint Services Development</span></span>](http://msdn.microsoft.com/library/a90156e2-0522-46a1-9fc9-b6c8d2fffad7%28Office.15%29.aspx)
    
  

