---
title: "Business Connectivity Services в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 64b7d032-4b83-4e9e-bc08-f0a161af5457
ms.openlocfilehash: 3c29b9a8908930d0346d5206645f42cad8e9fbec
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="business-connectivity-services-in-sharepoint"></a>Business Connectivity Services в SharePoint
Информация о службах Службы Business Connectivity Services (BCS), их назначении и требованиях для разработки приложений BCS в SharePoint. Вы можете использовать SharePoint в качестве концентратора для создания высокопроизводительных решений для совместной работы, которые могут работать с различными внешними системами. Службы Business Connectivity Services (BCS) предоставляет инфраструктуру, которая включает SharePoint для переноса данных из внешних систем в центральную. Благодаря гибким и расширяемым средствам для описания источника данных внешних систем и методу взаимодействия с ними, BCS дает веские основания для использования SharePoint в качестве центрального интерфейса для работы с устаревшими бизнес-системами в дополнение к новым Надстройки SharePoint.
  
    
    


## <a name="what-can-bcs-do"></a>Возможности BCS
<a name="BCSoverview_Whatcanbcsdo"> </a>

Службы BCS предоставляют механизмы, упрощающие для опытных пользователей, разработчиков и ИТ-специалистов подразделений выполнение перечисленных ниже задач.
  
    
    

- Отображение внешних данных из корпоративных приложений, веб-служб и служб OData в SharePoint и полнофункциональных клиентских приложениях Office.
    
  
- Добавление функций и возможностей в стиле Office (например, контактов, задач и встреч) ко внешним данным и службам.
    
  
- Обеспечение полного взаимодействия с данными, включая возможности выполнения обратной записи из приложений Office и SharePoint Server в базовые данные внешней системы и бизнес-объекты.
    
  
- Обеспечение автономного использования внешних данных и процессов.
    
  
- Соединение неструктурированного мира документов и людей и соответствующие структурированные данные, которые заблокированы во внешних системах.
    
  

## <a name="components-of-bcs"></a>Компоненты BCS
<a name="bkmk_Components"> </a>

На рис. 1 показаны функции, которые включены в SharePoint и Office 2013.
  
    
    

**Рис. 1. Набор функций служб Business Connectivity Services**

  
    
    

  
    
    
![Набор компонентов Business Connectivity Services](../images/BCSin2013FeatureSet.jpg)
  
    
    

  
    
    

  
    
    

## <a name="using-external-content-types-in-bcs"></a>Использование внешних типов контента в BCS
<a name="bkmk_UsingECTs"> </a>

Внешние типы контента являются ядром BCS. Они позволяют управлять и повторно использовать метаданные и поведения бизнес-элемента, например клиента или заказа, из центрального расположения. Они позволяют пользователям более осмысленно взаимодействовать с этими внешними данными и процессами.
  
    
    
В качестве примера рассмотрим такой бизнес-элемент как клиент. Вы хотите поместить данные из собственной базы данных и работать с ней в SharePoint. Вам также необходимо иметь возможность позволять своим продавцам пользоваться данными в автономном режиме в Outlook 2013. Либо вы хотите, чтобы пользователь имел возможность выбрать клиента из списка клиентов в документе с контактной информацией клиента внутри Microsoft Word. Для того чтобы все это осуществить, вы можете создать единый внешний тип контента и затем повторно использовать его при необходимости.
  
    
    
Дополнительную информацию по использованию внешних типов контента в BCS можно узнать в статье  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md).
  
    
    

## <a name="developing-solutions-using-bcs"></a>Разработка решений с использованием BCS
<a name="bkmk_DevelopingSolutionsUsingBCS"> </a>

В SharePoint можно построить широкий спектр решений с помощью BCS. Сюда относятся простые решения, которые основываются на собственных возможностях с небольшой настройкой или без нее, промежуточные решения, которые подразумевают пользовательские функции в SharePoint и Office 2013, и дополнительные решения, которые включают сложные сценарии и большие приложения, расширяющие их функционал. Дополнительные решения предполагают написание кода с использованием Visual Studio. Они могут быть полными комплексными приложениями или повторно используемыми компонентами на основе кода, которые включены в промежуточное решение.
  
    
    
BCS позволяет бизнес-пользователям быстро и легко решать широкий круг потребностей во внешних данных за счет использования веб-браузера и клиентского приложения Microsoft Office, например Word или Excel. Без необходимости написания кода пользователи могут собрать составные решения за счет функций BCS, например внешних списков и столбцы внешних данных и повторно используемых компонентов BCS, которые создаются разработчиками и утверждаются ИТ, в клиентских приложениях Office и сайтах SharePoint. Эти решения включают бизнес-пользователей (и их команды), которые позволяют работать с внешними данными так же легко, как с данными SharePoint, в автономном режиме или с подключением к Интернету либо напрямую в Office 2013.
  
    
    
Дополнительную информацию о начале работы можно узнать в статье  [Настройка среды разработки для BCS в SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).
  
    
    

## <a name="using-odata-with-business-connectivity-services-in-sharepoint"></a>Использование OData с помощью служб Business Connectivity Services в SharePoint
<a name="bkmk_ODataInBCS"> </a>

Протокол открытых данных (OData)  это веб-протокол, позволяющий раскрывать данные в Интернете с помощью таких технологий, как HTTP, Нотация объектов JavaScript (JSON) и AtomPub. Доступ к данным осуществляется через специально созданные URL-адреса. Данная архитектура позволяет вам взаимодействовать с данными, используя различные технологии.
  
    
    
Более подробную информацию можно узнать в статье  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md).
  
    
    

## <a name="in-this-section"></a>В этом разделе:
<a name="bkmk_inthissection"> </a>


-  [Новые возможности служб Business Connectivity Services в SharePoint](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [Начало работы со службами Business Connectivity Services в SharePoint](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md)
    
  
-  [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [Внешние события и оповещения в SharePoint](external-events-and-alerts-in-sharepoint.md)
    
  
-  [Добавьте в пределах внешних типов контента в SharePoint](add-in-scoped-external-content-types-in-sharepoint.md)
    
  
-  [Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [Справочник по программистов Business Connectivity Services для SharePoint](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  

## <a name="see-also"></a>См. также
<a name="bkmk_AdditionalResources"> </a>


-  [Добавление возможностей SharePoint](add-sharepoint-capabilities.md)
    
  
-  [Настройка среды разработки для BCS в SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md)
    
  
-  [Обзор разработки решений с помощью SharePoint](sharepoint-development-overview.md)
    
  

