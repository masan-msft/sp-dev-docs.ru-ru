---
title: "Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 8ed91929-fdb6-4fde-ba2a-7942870575f3
ms.openlocfilehash: 2ddd19599a6a88523cb38940355104d178500f3d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-using-the-client-object-model-with-external-data-in-sharepoint"></a>Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint
Сведения об использовании клиентской объектной модели SharePoint для работы с помощью Business Connectivity Services (BCS) в SharePoint.
## <a name="what-is-the-sharepoint-client-object-model"></a>Что такое клиентской объектной модели SharePoint?

Клиентская объектная модель для SharePoint — это набор библиотек на стороне клиента, которые представляют серверной объектной модели. Они собраны в трех разных библиотек DLL с использованием различных типов разработки. Клиентская объектная модель содержит большую часть основных функций сервера API. Позволяет получить доступ к одной типам функциональные возможности из браузера сценариев и также .NET веб-приложений и приложений Silverlight.  <br/> Чтобы улучшить и расширить возможности по работе с внешними данными, Службы Business Connectivity Services (BCS) расширил клиентской объектной модели, чтобы включить дополнительные функции.  <br/> 

<a href="#BCScsom_getstarted"><img alt="Get set up" src="../images/mod_icon_getstartbox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Tasks"><img alt="Get to work" src="../images/mod_icon_dobox.gif" /></a>&nbsp;&nbsp;&nbsp;<a href="#BCScsom_Learnmore"><img alt="Learn more" src="../images/mod_icon_startbox.gif" /></a></p>

## <a name="get-started-using-the-sharepoint-client-object-model-with-external-data"></a>Начало работы с помощью клиентской объектной модели SharePoint с внешними данными
<a name="BCScsom_getstarted"> </a>

Разработка решений с помощью объектной модели клиента SharePoint (CSOM), необходимо следующее:
  
    
    

- SharePoint
    
  
- Visual Studio 2012
    
  
- Инструменты разработчика Office для Visual Studio 2012
    
  
Сведения о том, как настроить среду разработки см [в среде разработки для BCS в SharePoint](setting-up-a-development-environment-for-bcs-in-sharepoint.md).
  
    
    
Для доступа к возможности, предоставляемые в клиентской объектной модели, требуется только для добавления ссылки на файлы **Microsoft.SharePoint.Client.Runtime.dll** и **Microsoft.SharePoint.Client.dll** в их проектах. Можно также использовать клиентской объектной модели, ссылки на следующие библиотеки DLL в глобальный кэш сборок:
  
    
    

-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.Runtime.dll`
    
  
-  `\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\isapi\\Microsoft.SharePoint.Client.dll`
    
  

### <a name="sharepoint-client-object-model-essentials"></a>Основные компоненты объектной модели SharePoint клиента

Следующие статьи поможет вам понять, Дополнительные сведения о клиентской объектной модели в SharePoint.
  
    
    

**В таблице 1. Основные понятия, которые для Общие сведения о клиентской объектной модели**


|**Статья**|**Описание**|
|:-----|:-----|
| [Внешние типы контента в SharePoint](external-content-types-in-sharepoint.md) <br/> |Прочитав эту статью, вы узнаете, что можно делать с внешними типами контента и что необходимо для их создания в SharePoint.  <br/> |
| [Использование источников OData со службами Business Connectivity Services в SharePoint](using-odata-sources-with-business-connectivity-services-in-sharepoint.md) <br/> |Предоставляет сведения, которые помогут приступить к работе Создание внешних типов контента на основе источников OData и использовать эти данные в SharePoint или Office 2013 компонентов.  <br/> |
| [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md) <br/> |Сведения о некоторых наборов API, которые предоставляются в SharePoint, включая серверной объектной модели, различных клиентских объектных моделей и веб-службы REST/OData.  <br/> |
| [Справка по API клиента .NET для SharePoint](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx) <br/> |Сведения о клиенте .NET библиотеки классов в SharePoint.  <br/> |
| [Справочник по JavaScript API для SharePoint](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx) <br/> |Сведения о библиотеках объектов JavaScript в SharePoint.  <br/> |
   

## <a name="what-can-you-do-with-the-client-object-model"></a>Что можно делать с помощью клиентской объектной модели
<a name="BCScsom_Tasks"> </a>

Клиентская объектная модель SharePoint можно использовать для извлечения, обновления и управления данными, содержащимися в SharePoint. SharePoint предоставляет клиенту библиотек в различные форматы для учета большинства разработчиков. Для разработчиков веб-приложений, использующих языками сценариев клиентская библиотека предлагается в JavaScript. Для разработчиков .NET предлагается как клиент .NET управляемой библиотеки DLL. Клиентская библиотека для разработчиков приложений Silverlight, обеспечивается Silverlight DLL.
  
    
    
Изучение статей в таблице 2, Дополнительные сведения о клиентской объектной модели в SharePoint.
  
    
    

**В таблице 2. Основные задачи по использованию клиентской объектной модели с помощью внешних данных**


|**Задача**|**Описание**|
|:-----|:-----|
| [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx) <br/> |Узнайте, как создавать код для выполнения базовых операций с клиентской объектной модели SharePoint.  <br/> |
| [Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md) <br/> |Сведения об использовании клиентской объектной модели SharePoint для работы с объектами SharePoint BCS с помощью сценариев на основе браузера.  <br/> |
   
Ниже приведены некоторые основные примеры задач, которые можно выполнить с помощью CSOM.
  
    
    

### <a name="get-a-specific-entity"></a>Получение определенной сущности

В этом примере показано, как получить контекст из SharePoint, а затем извлеките объект источника данных.
  
    
    

```cs

ClientContext ctx = new ClientContext("http://sharepointservername"); 
Web web = ctx.Web; 
ctx.Load(web); 
Entity entity = ctx.Web.GetEntity("http://sharepointservername", "EntityName"); 
ctx.Load(entity); 
ctx.ExecuteQuery(); 

```


### <a name="create-a-generic-invoker"></a>Создание универсальных вызова

В этом примере показано, как создавать универсальные вызова таким образом, можно создать объект сущности для работы в коде.
  
    
    

```cs

ObjectCollection myObj; 
entity.Execute("MethodInstanceName", lsi, myObj); 
ctx.Load(myObj); 
ctx.ExecuteQuery(); 

```


### <a name="retrieve-paged-result-sets"></a>Получение наборов выгружаемый результатов

Следующем примере показано, как получить отфильтрованные выгружаемый набор данных. В этом случае значение страницы равно 50.
  
    
    

```cs

// Find filters for given Method Name. 
FilterCollection fCollection = entity.GetFilters("methodName"); 
ctx.Load(fCollection); 
ctx.ExecuteQuery(); 
FilterCollection modifiedFCollection = new FilterCollection(); 
foreach( Filter filter in fCollection) 
{ 
    if( filter.FilterField.equals("X.Y.Z.Country")) 
    { 
        filter.FilterValue = "India"; 
        modifiedFCollection.Add(Filter); 
    } 
    if(filter.FilterType == FilterType.Limit) 
    { 
        filter.FilterValue = 50; 
        modifiedFCollection.Add(Filter); 
    } 
} 
EntityInstanceCollection eCollection = entity.FindFiltered(modifiedFCollection, 
"nameOfFinder", lsi); 
ctx.ExecuteQuery(); 

```


### <a name="query-for-filtered-information"></a>Запрос отфильтрованные сведения

Приведенный ниже показано, как для возврата набора отфильтрованных результатов. В этом случае отфильтровано столбец данных  это поле **X.Y.Z.Country**. Код ищет все действия со значением «Индия» и помещает, в коллекцию.
  
    
    

```cs

// Find filters for given Method Name. 
FilterCollection fCollection = entity.GetFilters("methodName"); 
ctx.Load(fCollection); 
ctx.ExecuteQuery(); 
FilterCollection modifiedFCollection = new FilterCollection(); 
foreach( Filter filter in fCollection) 
{ 
    if( filter.FilterField.equals("X.Y.Z.Country")) 
    { 
        filter.FilterValue = "India"; 
        modifiedFCollection.Add(Filter); 
    } 
} 
EntityInstanceCollection eCollection = entity.FindFiltered(modifiedFCollection, 
"nameOfFinder", lsi); 
ctx.ExecuteQuery(); 

```


## <a name="beyond-the-basics-learn-more-about-the-client-object-model"></a>От простого к сложному: Дополнительные сведения о клиентской объектной модели
<a name="BCScsom_Learnmore"> </a>

Дополнительные сведения об использовании клиентской объектной модели в SharePoint можно сведения, приведенные в таблице 3.
  
    
    

**В таблице 3. Расширенные концепции для клиентской объектной модели**


|**Статья**|**Описание**|
|:-----|:-----|
| [BCS клиента Справочник по объектной модели для SharePoint](bcs-client-object-model-reference-for-sharepoint.md) <br/> |Обобщаются объектов для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемым BCS.  <br/> |
   

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="BCScsom_Learnmore"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [Выполнение базовых операций с использованием кода библиотеки клиента в SharePoint](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [SharePoint: Доступ к сложным внешним типам контента с помощью CSOM](http://code.msdn.microsoft.com/office/SharePoint-Accessing-ccbc24cf)
    
  
