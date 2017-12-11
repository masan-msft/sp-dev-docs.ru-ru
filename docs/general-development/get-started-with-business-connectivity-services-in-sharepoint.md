---
title: "Начало работы с Business Connectivity Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c6bf3db0-db79-4b13-9834-891d24b2c9e5
ms.openlocfilehash: 971c338c4d05ddb8ede3cf5f77aa3eabebb2b1b3
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="get-started-with-business-connectivity-services-in-sharepoint"></a>Начало работы с Business Connectivity Services в SharePoint
Основные сведения о Business Connectivity Services (BCS) предоставляет разработчикам решений SharePoint, а также как приступить к работе с помощью службы BCS в различных типов решений.
## <a name="what-is-business-connectivity-services"></a>Что представляют собой Business Connectivity Services?

Business Connectivity Services (BCS) была введена в SharePoint Server 2010 как развитием каталога бизнес-данных, выпущенные в Office SharePoint Server 2007. Службы BCS дают SharePoint для работы с данными, которая размещается извне. Возможные источники могут включать баз данных, веб-служб, службы Windows Communication Foundation (WCF), Open Data Protocol (OData) источников и другие конфиденциальные данные, к которому осуществляется с помощью пользовательских сборок .NET.

<a href="#SP15GettingStartedBCS_WhatDoYouNeed"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_WhatCanYouDo"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#SP15GettingStartedBCS_LearnMore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a>

   
На рабочем месте динамические информационные работники необходим доступ к данным, которые находятся в отдельном программного обеспечения стандартов для примера:
  
    
    

- Структурированные данные, существует ли в организации корпоративных приложений, таких как планирования ресурсов предприятия (ERP) и приложения управления (CRM) ресурсов клиента.
    
  
- Неструктурированных данных в бизнес-приложений повышения производительности, такие как Microsoft Office, групп и совместной работы приложений, таких как SharePoint и службы Web 2.0, такие как веб-приложений, вики-сайты, блоги и сайтов социальных сетей.
    
  
Хотя большинство информационные работники большую часть их рабочего времени в рамках офисные приложения (например, среды Microsoft Office), они также необходим способ интеграции этой среде с корпоративных приложений и совместной работы программного обеспечения и службы, которые они используют. Службы BCS предоставляют этой возможности в SharePoint.
  
    
    

## <a name="get-started-with-business-connectivity-services"></a>Начало работы со службами Business Connectivity Services
<a name="SP15GettingStartedBCS_WhatDoYouNeed"> </a>

Для начала разработки с помощью службы BCS, необходимо следующее:
  
    
    

- SharePoint
    
  
- Visual Studio
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
    или
    
  
- SharePoint Designer
    
  
Сведения о том, как настроить среду разработки см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

### <a name="business-connectivity-services-essentials"></a>Основные службы подключения к бизнес-функции

В следующей таблице указаны основные концепции, которые необходимо ознакомиться с быстро приступить к разработке решений BCS.
  
    
    

**В таблице 1. Основные понятия, которые для понимания BCS**


|**Статья**|**Описание**|
|:-----|:-----|
| [Ключевые понятия модели данных сущности](http://msdn.microsoft.com/en-us/library/ee382840.aspx) <br/> |Модели данных сущности (EDM) использует три основные понятия для описания структуры данных: тип сущности, тип связи и свойства. Это наиболее важных концепций описания структуры данных в любой реализации EDM.  <br/> |
| [Рекомендации по обеспечению безопасности базовой для веб-приложений](http://msdn.microsoft.com/en-us/library/zdh19h94.aspx) <br/> |Широкое тема создания безопасного веб-приложения. В этом примере рассмотрения понять уязвимые места системы безопасности. Также необходимо ознакомиться с помощью средств безопасности операционной системы Windows, .NET Framework и ASP.NET. И, наконец очень важно понять, как использовать эти функции для борьбы с угрозами.  <br/> |
| [Службы данных WCF](http://msdn.microsoft.com/en-us/data/odata.aspx) <br/> |Службы данных WCF, ранее называлась служб данных ADO.NET, включите Создание и использование службы OData для веб-сайта.  <br/> |
| [Open Data Protocol (OData)](http://www.odata.org) <br/> |OData  это стандартный протокол для доступа к данным через URL-адрес. В основном он располагается в верхней части протокола HTTP, чтобы предоставить разрешение на чтение и запись функциями с помощью существующих команд HTTP.  <br/> |
| [Службы IIS](http://www.iis.net/) <br/> |Internet Information Services (IIS)  платформа, работающей в среде SharePoint. Следует понять, как создать веб-сайтов, виртуальные каталоги, веб-служб, URL-адреса, веб-безопасности и другие технологии, связанные с IIS.  <br/> |
| [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md) <br/> |Внешние типы контента описаны внешних систем, которые они представляют. Они являются для повторного использования, при импорте в SharePoint и могут использоваться для создания сложных решений без использования кода, с помощью SharePoint Designer 2013, Outlook 2013, веб-частей, внешних списков и пользовательских клиентских приложений.  <br/> |
| [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md) <br/> |SharePoint предоставляет возможность доступа к все объекты через тщательно построенный URL-адрес. Чтобы реализовать этот же функциональные возможности расширен BCS.  <br/> |
   

## <a name="what-can-you-do-with-business-connectivity-services"></a>Что можно делать со службами Business Connectivity Services
<a name="SP15GettingStartedBCS_WhatCanYouDo"> </a>

С BCS можно импортировать данные в SharePoint из множества различных источников. Например можно свести данные из базы данных внешнего SQL Server, традиционные веб-службы, службы WCF, собственный систем и службы OData.
  
    
    

**В таблице 2. Основные задачи по работе со службами Business Connectivity Services**


|**Задача**|**Описание**|
|:-----|:-----|
| [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md) <br/> |Сведения о создании Службы Business Connectivity Services (BCS) внешних типов контента.  <br/> |
| [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md) <br/> |Найдите сведения, которые необходимо приступить к созданию внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office компонентов.  <br/> |
| [Как: создание приемников внешних событий](how-to-create-external-event-receivers.md) <br/> |Узнайте концепции создания приемников событий, которые можно присоединить к внешним спискам и будет выполняться при обновлении внешних данных, представляемых списком.  <br/> |
| [Как: создание добавить в пределах внешнего типа контента в SharePoint](how-to-create-an-add-in-scoped-external-content-type-in-sharepoint.md) <br/> |Узнайте, как создать внешние типы контента, для которых установлены или областью действия на уровне приложения, что дает возможность создавать насыщенные приложения с помощью внешних источников данных.  <br/> |
| [Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |Сведения об использовании клиентской объектной модели SharePoint для работы с BCS в SharePoint.  <br/> |
   

## <a name="beyond-the-basics-learn-more-about-business-connectivity-services"></a>От простого к сложному: Узнайте больше о Business Connectivity Services
<a name="SP15GettingStartedBCS_LearnMore"> </a>

Когда главные основные понятия BCS, расширенные возможности можно использовать для создания многих эффективные типы решений.
  
    
    

**В таблице 3. Расширенные концепции в BCS**


|**Статья**|**Описание**|
|:-----|:-----|
| [Как: создать службу данных OData для использования в качестве внешней системы BCS](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md) <br/> |Узнайте, как создать интернет-адресуемую службу WCF, которая использует OData для отправки уведомлений в SharePoint при изменении базовых данных. Эти уведомления используются для запуска событий, которые прикреплены ко внешним спискам.  <br/> |
| [Справочник по схеме модели BDC для SharePoint](bdc-model-schema-reference-for-sharepoint.md) <br/> |Найдите справочную документацию по схеме модели BDC.  <br/> |
| [BCS клиента Справочник по объектной модели для SharePoint](bcs-client-object-model-reference-for-sharepoint.md) <br/> |Получите сводку объектов, доступных для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемые Business Connectivity Services (BCS).  <br/> |
| [Справочник по API-Интерфейс REST BCS для SharePoint](bcs-rest-api-reference-for-sharepoint.md) <br/> |Найдите справочные сведения для создания представлений состояния (REST) коды URI используются для доступа и управления источников OData.  <br/> |
   

## <a name="see-also"></a>См. также
<a name="SP15GettingStartedBCS_LearnMore"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Веб-сайт Open Data Protocol](http://www.odata.org/)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Внешние события и оповещения в SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Добавьте в пределах внешних типов контента в SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
