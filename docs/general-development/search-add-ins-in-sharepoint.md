---
title: "Надстройки поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 21682e45-dd78-4f3c-8f1e-cdd48de3bde2
ms.openlocfilehash: 30eea1616bceb6754883056339ad4642de8acb9f
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="search-add-ins-in-sharepoint"></a>Надстройки поиска в SharePoint
Сведения о поиска Надстройки SharePoint и как можно создавать свои собственные надстройки поиска. Надстройки, которые можно создать можно добавить к каталогу SharePoint надстройки, чтобы их можно использовать в локальном развертывании и Office 365. Надстройки поиска возможен только с данными, хранящимися в индексе поиска, а не исходного документа. Надстройки SharePoint  изолированная части функции, расширяющие возможности SharePoint веб-сайта. Эти надстройки путем интеграции с рекомендациями по SharePoint и веб-решения специфические потребности бизнеса и конечных пользователей. Надстройка может содержать различные элементы SharePoint, такие как списки, удаленных приемников событий, типов контента, рабочие процессы, настраиваемые действия рабочего процесса, столбцы сайта, модули, настраиваемые действия элемента меню, клиентского веб-частей и конфигурации поиска. Для получения дополнительных сведений см  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx).
  
    
    

Надстройка поиска — SharePoint надстройку в том, что использование функциональной возможности поиска. В надстройке поиска можно использовать интерфейс API поиска SharePoint для поиска контента. В зависимости от типа разрешения в [манифесте надстройки](http://msdn.microsoft.com/library/7cd5850f-cbf3-48d2-bcb7-59b8f4ed0e63%28Office.15%29.aspx)можно выполнить поиск внутри или за пределами содержимое надстройки. Кроме того можно также использовать надстройки поиска для распространения конфигурации поиска с одной установки SharePoint в другую.
Разработка основных надстройки поиска зависит от Выбор метода развертывания. В следующем разделе приводятся доступные параметры и их преимущества. Дополнительные сведения можно [выбрать шаблоны для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
  
    
    


## <a name="deploy-your-search-add-ins"></a>Развертывание надстройки поиска
<a name="SP15_Deploy_search_apps"> </a>

Развертывание надстройки поиска двумя способами:
  
    
    

1. SharePoint hosted - локальное развертывание. Надстройка поиска размещается внутри корпоративной сети на серверах компании. Компании Администраторы управляют надстройки. Этот сценарий предлагает гибкие возможности развертывания и поддержки, так как к оборудованию и программному обеспечению локально поддерживается администраторами.
    
  
2. У поставщика - любой веб-сервере размещения. Надстройка поиска размещается с любым поставщиком, за пределами клиента SharePoint server. 
    
  

## <a name="search-add-in-development-environment"></a>Среда разработки надстройки поиска
<a name="SP15_Search_app_dev_environment"> </a>

Создание надстройки поиска, используйте один из этих двух средах:
  
    
    

- Microsoft Visual Studio 2012 или Microsoft Visual Studio 2013 или Visual Studio 2015
    
  
- Средства разработки Napa для Office 365
    
  
С помощью Visual Studio 2013 и более поздних версий можно опубликовать надстройки поиска в локальной или в Office 365. Дополнительные сведения о средах разработки и как их использовать для создания надстроек поиска содержатся в разделе [Задание среды Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).
  
    
    

## <a name="apis-for-search-add-ins"></a>API-интерфейсы для поиска надстройки
<a name="SP15_APIs_search_apps"> </a>

Можно использовать широкий диапазон интерфейсов API, связанных с поиском, SharePoint предлагает для надстроек поиска. В следующей таблице перечислены эти интерфейсы API и место их библиотек классов.
  
    
    

**API-интерфейсов SharePoint для надстроек поиска**


|**Имя API**|**Библиотека классов**|
|:-----|:-----|
|Клиентская объектная модель .NET (CSOM)  <br/> |Microsoft.SharePoint.Client.Search.dll  <br/> |
|Silverlight CSOM  <br/> |Microsoft.SharePoint.Client.Search.Silverlight.dll  <br/> |
|Объектная модель ECMAScript (JavaScript, JScript) (JSOM)  <br/> |SP.search.js  <br/> |
|Поиск API-ИНТЕРФЕЙС REST  <br/> |http://Server/_api/Search/Query  <br/> |
   

### <a name="code-examples"></a>примеры кода

Вот несколько примеров кода, с помощью различных интерфейсов API. Каждый пример кода отправляет запрос простой Поиск, который содержит ключевое слово "SharePoint " Приложение-служба поиска (SSA).
  
    
    
 **Client-side Object Model (CSOM)**
  
    
    

  
    
    



```cs

using (ClientContext clientContext = new ClientContext("http://localhost"))
{
    KeywordQuery keywordQuery = new KeywordQuery(clientContext);
    keywordQuery.QueryText = "*";
    SearchExecutor searchExecutor = new SearchExecutor(clientContext);
    ClientResult<ResultTableCollection> results = 
        searchExecutor.ExecuteQuery(keywordQuery);
    clientContext.ExecuteQuery();
}
```

 **JavaScript Object Model (JSOM)**
  
    
    

  
    
    



```

var keywordQuery = new
Microsoft.SharePoint.Client.Search.Query.KeywordQuery(context);
keywordQuery.set_queryText('SharePoint');
var searchExecutor = new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(context);
results = searchExecutor.executeQuery(keywordQuery);
context.executeQueryAsync(onQuerySuccess, onQueryFail);
```

 **REST**
  
    
    

  
    
    
HTTP-запрос GET
  
    
    



```HTML

http://mylocalhost/_api/search/query?querytext='SharePoint'
```

HTTP-запрос POST
  
    
    



```HTML
{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'SharePoint'
}
```


## <a name="search-add-in-permissions"></a>Добавить разрешения поиска
<a name="SP15_Search_app_permissions"> </a>

Надстройки поиска отправлять запросы запроса Приложение-служба поиска (SSA) и надстроек, требуют различных типов разрешений для правильной работы. Можно настроить эти разрешения с помощью надстройки файл манифеста, который является частью надстройки каждого SharePoint. Добавить в файл манифеста можно изменять напрямую с помощью текстового редактора или изменять его с Visual Studio или Napa, как показано на следующих рисунках. 
  
    
    

**На рисунке 1: Установка разрешений для поиска надстроек в Visual Studio 2015**

  
    
    

  
    
    
![Настройка разрешений поискового приложения с помощью Visual Studio](../images/SP15_search_apps_permission_Visual_Studio.PNG)
  
    
    

  
    
    

  
    
    

**На рисунке 2: Настройка разрешений для надстроек поиска в средства разработки «Napa» Office 365**

  
    
    

  
    
    
![Настройка разрешений поискового приложения с помощью Napa](../images/SP15_search_app_permission_Napa.gif)
  
    
    
Надстройка SharePoint имеет свой собственный идентификатор, связанный с субъекта безопасности именем субъекта надстройки. Как пользователи и группы субъект надстройки имеет определенные разрешения и права. Субъект надстройки имеет права полного доступа add в веб-приложения, его необходимо только запрашивать разрешения на SharePoint ресурсы в другие расположения за пределами web надстройки, такие как семейств веб-сайтов или веб-сайт. В отличие от других Надстройки SharePoint надстройки поиска требуются только разрешения уровня пользователя, известных как **QueryAsUserIgnoreAppPrincipal**. Это разрешение позволяет запросов поиска надстройки на основе разрешений пользователя. Это означает, что поиск, возвращаются результаты, основанные на списки контроля доступа пользователя. 
  
    
    

### <a name="request-permissions-in-the-add-in-manifest-file"></a>Запрашивать разрешения в файле манифеста надстройки

Добавить в файл манифеста в формате XML и непосредственного редактирования. Для получения разрешений, создаваемом запроса, как показано в следующем примере:
  
    
    

```XML

<AppPermissionRequests>
  <AppPermissionRequest Scope="http://sharepoint/search" Right="QueryAsUserIgnoreAppPrincipal" />
</AppPermissionRequests>
```


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="SP15_Search_app_addresources"> </a>


-  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [Выбор шаблонов для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [Разрешения для надстроек в SharePoint](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx)
    
  
-  [Типы политик авторизации надстроек в SharePoint](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx)
    
  
-  [Важные аспекты архитектуры и разработки надстройки SharePoint](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx)
    
  
-  [Изучите структуру манифеста надстройки и пакет надстройки для SharePoint](http://msdn.microsoft.com/library/7cd5850f-cbf3-48d2-bcb7-59b8f4ed0e63%28Office.15%29.aspx)
    
  
-  [Добавление возможностей поиска для надстройки для SharePoint](http://blogs.msdn.com/b/officeapps/archive/2013/05/30/add-search-capabilities-to-your-apps-for-sharepoint.aspx)
    
  
-  [Экспорт и импорт параметров конфигурации поиска в SharePoint](exporting-and-importing-search-configuration-settings-in-sharepoint.md)
    
  
-  [Импорт и экспорт параметров конфигурации настраиваемого поиска в SharePoint (TechNet)](http://technet.microsoft.com/en-us/library/jj871675.aspx)
    
  

