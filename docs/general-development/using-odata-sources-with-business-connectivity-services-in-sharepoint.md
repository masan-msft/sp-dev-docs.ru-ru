---
title: "Использование источников OData со службами Business Connectivity Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 7a87e5bf-4428-4055-b113-7665a93e7326
ms.openlocfilehash: 40dcb00b9ab16c621aafd053691315ea9f4f99f7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="using-odata-sources-with-business-connectivity-services-in-sharepoint"></a>Использование источников OData со службами Business Connectivity Services в SharePoint
Узнайте, как приступить к созданию внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office 2013 компонентов.
## <a name="odata-and-the-odata-connector"></a>OData и соединитель OData
<a name="SP15getstartedOdata_whatisodata"> </a>

Open Data protocol (OData) позволяет получить доступ к источнику данных, таких как базы данных, просмотрев имеющиеся специально созданный URL-адрес. Это позволяет упрощенный подход для подключений и работа с источниками данных, размещенных в пределах организации. 
  
    
    
OData  это протокол, который используется HTTP, Atom и Нотация объектов JavaScript (JSON) позволяет разработчикам создавать приложения, которые взаимодействуют с возрастающих число источников данных. Microsoft поддерживает создание этот стандарт, чтобы разрешить обмен данными между приложениями и хранилища данных, доступных из Интернета.
  
    
    
Новый соединитель OData позволяет связываться с поставщиками OData SharePoint.
  
    
    
В SharePoint Business Connectivity Services (BCS) могут обмениваться данными источников OData или производители, без написания кода непосредственно к источнику OData. Производители предоставляют доступ к своим данным структурированным способом с помощью веб-службы. Некоторые производители могут разрешить обновление базовых данных, а некоторые могут разрешить доступ только для чтения. Для целей рекламу, какие операции можно выполнить производитель имеет службы документа в указанный URL-адрес конечной. SharePoint уже производитель OData. Данные списка SharePoint в виде источника OData для любого объекта-получателя, имеющей соответствующие права.
  
    
    

### <a name="examples-of-odata-producers"></a>Примеры поставщики OData
<a name="ExamplesOfODataProducers"> </a>

Ниже приведены некоторые примеры реализаций OData. Эти приложения и службы предоставляют доступ к своим данным через протокол OData.
  
    
    

- SharePoint Foundation 2010
    
  
- SharePoint Server 2010
    
  
- SQL Azure
    
  
- Хранение таблицы Microsoft Azure.
    
  
- Microsoft Azure Магазин
    
  
-  Службы SQL Server Reporting Services
    
  
- Microsoft Dynamics CRM 2011 г.
    
  
- Windows Live
    
  
Список поставщики служб OData в разделе  [веб-сайт Open Data Protocol](http://www.odata.org/ecosystem).
  
    
    

## <a name="prerequisites-for-working-with-the-bcs-odata-connector"></a>Необходимые условия для работы с BCS соединитель OData
<a name="SP15GetstartedOdata_prereq"> </a>

Чтобы разработать основе внешних типов контента, необходимо следующее:
  
    
    

- Visual Studio 2012
    
  
- SharePoint
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
Сведения о том, как настроить среду разработки см [в среде Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="creating-external-content-types-for-odata-data-sources"></a>Создание внешних типов контента для источников данных OData
<a name="SP15GetstartedOdata_creatingECT"> </a>

Для SharePoint использовать данные, предоставляемые элементом определенного producer OData внешний тип контента должен быть создан внутри SharePoint. Как с помощью всех SharePoint внешних типов контента, он содержит все сведения о подключении, необходимые для подключения и взаимодействия с внешней системы.
  
    
    
Создание внешнего типа контента, который использует источник данных OData похоже на создание любой внешнего типа контента. Можно использовать Visual Studio 2012 для автоматического создания OData внешних типов контента. Необходимо просто предоставить представлений состояния (REST) конечной точки источника OData при создании внешнего типа контента. Дополнительные сведения можно [как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md).
  
    
    

## <a name="in-this-section"></a>В этой статье
<a name="SP15GetstartedOdata_inthissect"> </a>


-  [Как: создать внешний тип контента из источника OData в SharePoint](how-to-create-an-external-content-type-from-an-odata-source-in-sharepoint.md)
    
  
-  [Как: создать службу данных OData для использования в качестве внешней системы BCS](how-to-create-an-odata-data-service-for-use-as-a-bcs-external-system.md)
    
  
-  [Как: Создание внешнего списка с помощью источника данных OData в SharePoint](how-to-create-an-external-list-using-an-odata-data-source-in-sharepoint.md)
    
  

## <a name="see-also"></a>См. также
<a name="SP15GetstartedOdata_addres"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

