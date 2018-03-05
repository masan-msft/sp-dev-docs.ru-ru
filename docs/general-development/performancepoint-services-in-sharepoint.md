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
# <a name="performancepoint-services-in-sharepoint"></a>PerformancePoint Services в SharePoint
Ознакомьтесь с поддерживаемым сценариям разработки и архитектура расширения для служб PerformancePoint Services в SharePoint.
PerformancePoint Services — это приложение службы SharePoint. Она позволяет пользователям создавать бизнес-аналитики (BI) панелей мониторинга, которые обеспечивают представление о производительности организации. Можно создать настраиваемых отчетов, фильтров, табличных источников данных и преобразований систем показателей для расширения встроенных функций служб PerformancePoint Services. Например можно создать визуализации настраиваемого отчета, который оптимизирован для медицинского обслуживания отрасли и его интеграции в для повторного использования вертикальное решение.
  
    
    


## <a name="custom-performancepoint-services-reports-filters-and-tabular-data-sources-in-sharepoint"></a>Пользовательские отчеты служб PerformancePoint Services, фильтров и табличных источников данных в SharePoint
<a name="bkmk_CreateCustomObjects"> </a>

Собственная Службы PerformancePoint Services  [ReportView](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.ReportView.aspx) , [Filter](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Filter.aspx) и табличные [DataSource](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.DataSource.aspx) объекты можно расширять путем определения пользовательского значения для их свойства. Настраиваемый отчет, фильтров и расширений табличных источников данных обычно включают три компонента: обработчик или поставщик, приложение редактирования и метаданные расширения.
  
    
    

### <a name="renderers-and-providers-for-performancepoint-services-extensions"></a>Средств отображения и поставщиков для расширения Службы PerformancePoint Services

Тип объекта, который вы расширяете определяет, используется ли обработчик или поставщик. Использование средств отображения отчетов и фильтров расширения и фильтрации и расширения источника данных используйте поставщиков.
  
    
    

- Для визуализации отчета расширению отчета требуется обработчик. 
    
  
- Фильтр расширению отчета требуется обработчик для элемента управления выбора. Средство визуализации может быть собственный модуль подготовки отчетов или собственный Службы PerformancePoint Services визуализации. При использовании визуализации Службы PerformancePoint Services его просто зарегистрировать в расширении. Если вы используете собственный модуль подготовки отчетов, необходимо включить его в расширении.
    
  
- Фильтр расширению отчета требуется поставщик данных для подключения к базовому источнику данных.
    
  
- Расширениям источников данных для подключения к базовому источнику данных требуется поставщик.
    
  
Для получения дополнительных сведений о создании средств отображения и поставщиков в следующих разделах:
  
    
    

-  [Как: создание средств отображения отчетов для PerformancePoint Services в SharePoint](how-to-create-report-renderers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [Как: создать фильтр поставщиков данных для служб PerformancePoint Services в SharePoint](how-to-create-filter-data-providers-for-performancepoint-services-in-sharepoint.md)
    
  
-  [Как: Создание поставщиков табличных источников данных для служб PerformancePoint Services в SharePoint](how-to-create-tabular-data-source-providers-for-performancepoint-services-in-sha.md)
    
  

### <a name="editor-applications-for-performancepoint-services-extensions-in-sharepoint"></a>Редактор приложений для расширения служб PerformancePoint Services в SharePoint

Настраиваемые редакторы позволяют пользователям определение свойств для настраиваемого объекта, взаимодействия с объектами в репозитории и инициализация конечных точек для настраиваемых отчетов и фильтры. Редактора должны предоставлять свойства, чтобы разрешить пользователям просматривать и изменять. Редакторы можно открыть из объектов в Конструктор панели мониторинга PerformancePoint или из элементов в список контента PerformancePoint или библиотеки подключений к данным PerformancePoint. Чтобы интегрировать в Конструктор панели мониторинга взаимодействия при разработке, должен иметь возможность открыть из универсальный код ресурса (URI), редактора и URI должна быть зарегистрирована для настраиваемого объекта в файле web.config Службы PerformancePoint Services.
  
    
    
Дополнительные сведения о создании редакторы в следующих разделах:
  
    
    

-  [Как: создать отчет редакторы для служб PerformancePoint Services в SharePoint](how-to-create-report-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [Как: создать фильтр редакторы для служб PerformancePoint Services в SharePoint](how-to-create-filter-editors-for-performancepoint-services-in-sharepoint.md)
    
  
-  [Как: создание табличных данных редакторы исходного для служб PerformancePoint Services в SharePoint](how-to-create-tabular-data-source-editors-for-performancepoint-services-in-share.md)
    
  
> [!NOTE]
> [!Примечание] Конструктор панели мониторинга PerformancePoint позволяет создавать и удалять пользовательские объекты, поэтому редактора необходимо предоставить логику для создания или удаления объектов. 
  
    
    


### <a name="configuration-metadata-for-performancepoint-services-extensions-in-sharepoint"></a>Метаданные конфигурации для расширения служб PerformancePoint Services в SharePoint

Необходимо указать метаданных для расширения в файле web.config Службы PerformancePoint Services во время установки. Метаданные включает в себя **type**, **subType**, **RendererClass**, **EditorURI**и **Resources** атрибуты.
  
    
    
Для создания настраиваемого объекта, Конструктор панели мониторинга возвращает объект метаданных из файла web.config Службы PerformancePoint Services и затем создает объект в качестве типа контента в хранилище Конструктор панели мониторинга. После создания настраиваемого объекта, Конструктор панели мониторинга отображается ссылка в редактор.
  
    
    
Дополнительные сведения о метаданные расширения можно  [Регистрация расширений служб PerformancePoint вручную](http://msdn.microsoft.com/library/3aa6d340-4b05-46b3-9648-2b6e18e04e09%28Office.15%29.aspx).
  
    
    

## <a name="custom-transforms-for-performancepoint-services-scorecards-in-sharepoint"></a>Настраиваемых преобразований для систем показателей PerformancePoint Services в SharePoint
<a name="bkmk_CreateCustomObjects"> </a>

Преобразований изменение внешнего вида, содержимого или функциональные возможности систем показателей перед запроса источника данных, после запроса источника данных или перед отображением системы показателей в веб-части. Например, Службы PerformancePoint Services используются преобразования нужно выполнить несколько операций перед отображением представления системы показателей, таких как развертывание именованные наборы, вычислений накопительные пакеты обновления и сетей статистические выражения. Эти изменения применяются во время выполнения и не изменяйте в определении объекта системы показателей.
  
    
    
Дополнительные сведения о преобразований системы показателей можно [как: создать преобразования системы показателей для служб PerformancePoint Services в SharePoint](how-to-create-scorecard-transforms-for-performancepoint-services-in-sharepoint-2.md).
  
> [!NOTE]
> [!Примечание] Если преобразование изменяет значения данных в системе показателей, изменения распространяются напрямую в отчеты стратегической карты, использующие эту систему в качестве источника данных. Кроме того, изменения в системе показателей могут повлиять на отчеты о ключевых показателях эффективности. 
  
    
    


## <a name="extensibility-architecture-for-performancepoint-services-in-sharepoint"></a>Архитектура расширения для служб PerformancePoint Services в SharePoint
<a name="bkmk_PerfPointArch"> </a>

Поддерживаемые расширения выполняются в рамках экземпляра приложения Службы PerformancePoint Services на интерфейсном веб-сервере или на сервере приложений, как показано на следующей схеме.
  
    
    

**Рисунок 1. Архитектура расширяемости PerformancePoint Services**

  
    
    

  
    
    
![Точки расширения служб PerformancePoint](../images/SPS14_PerfPoint_ArchOverview.gif)
  
    
    

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-front-end-web-server"></a>Расширения служб PerformancePoint Services, которые запускаются на интерфейсном веб-сервере SharePoint

Настраиваемые редакторы (и другие поддерживаемые настраиваемые приложения), выполните на интерфейсном веб-сервере в рамках экземпляра приложения Службы PerformancePoint Services. Редакторы обычно развертываются как ASPX-страницы и устанавливаются в путь  `%ProgramFiles%\\Common Files\\Microsoft Shared\\web server extensions\\15\\TEMPLATE\\LAYOUTS`. Редакторы вызова  [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) объектов или объектов [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) для автора или процесс содержимое, следующим образом:
  
    
    

- Объекты отчетов и фильтров следует использовать  [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) для всех задач репозитория.
    
  
- Объекты источника данных следует использовать для выполнения задач, **Create** и **Update**, чтобы эти задачи выполняются в контексте приложения-службы Службы PerformancePoint Services [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) . **Read** (get) и **Delete** задачи выполняются с помощью [BIMonitoringServiceApplicationProxy](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.BIMonitoringServiceApplicationProxy.aspx) или [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) . (Однако пользовательских данных источника приложения, которые запускаются на сервере приложений могут вызывать [SPDataStore](https://msdn.microsoft.com/library/Microsoft.PerformancePoint.Scorecards.Store.SPDataStore.aspx) непосредственно.)
    
  

### <a name="performancepoint-services-extensions-that-run-on-the-sharepoint-application-server"></a>Расширения служб PerformancePoint Services, которые запускаются на сервере приложений SharePoint

Настраиваемых средств отображения, поставщиков и преобразования системы показателей, выполните на сервере приложений. Сервер приложений содержит среднего уровня бизнес-логики для экземпляра Службы PerformancePoint Services.
  
    
    

## <a name="see-also"></a>См. также
<a name="bkmk_AdditionalResources"> </a>


-  [Базовые концепции разработки PerformancePoint Services](http://msdn.microsoft.com/library/5d2c183b-95f8-4930-b6d0-f3ffe1ee166e%28Office.15%29.aspx)
    
  
-  [Примеры кода для PerformancePoint Services в SharePoint Server 2010](http://msdn.microsoft.com/library/97f0cbd4-03ef-44f8-9869-699df9d9c97f%28Office.15%29.aspx)
    
  
-  [Устранение неполадок вопросы и ответы по разработке PerformancePoint Services](http://msdn.microsoft.com/library/a90156e2-0522-46a1-9fc9-b6c8d2fffad7%28Office.15%29.aspx)
    
  

