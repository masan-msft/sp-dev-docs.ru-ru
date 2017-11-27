---
title: "Надстройки поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 21682e45-dd78-4f3c-8f1e-cdd48de3bde2
ms.openlocfilehash: 79522329a6a06808be5e3034a5d82ed9c3a35590
ms.sourcegitcommit: 4ceb9b0dd0a9974df6180ca9959a1e9f452c7518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="search-add-ins-in-sharepoint"></a><span data-ttu-id="50be8-102">Надстройки поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-102">Search add-ins in SharePoint</span></span>
<span data-ttu-id="50be8-p101">Сведения о поиска Надстройки SharePoint и как можно создавать свои собственные надстройки поиска. Надстройки, которые можно создать можно добавить к каталогу SharePoint надстройки, чтобы их можно использовать в локальном развертывании и Office 365. Надстройки поиска возможен только с данными, хранящимися в индексе поиска, а не исходного документа. Надстройки SharePoint  изолированная части функции, расширяющие возможности SharePoint веб-сайта. Эти надстройки путем интеграции с рекомендациями по SharePoint и веб-решения специфические потребности бизнеса и конечных пользователей. Надстройка может содержать различные элементы SharePoint, такие как списки, удаленных приемников событий, типов контента, рабочие процессы, настраиваемые действия рабочего процесса, столбцы сайта, модули, настраиваемые действия элемента меню, клиентского веб-частей и конфигурации поиска. Для получения дополнительных сведений см  [Надстройки SharePoint](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="50be8-p101">Learn about search SharePoint Add-ins and how you can create your own search add-ins. The add-ins you create can be added to the SharePoint add-ins catalog so that they can be used in both on-premises deployment and Office 365. Search add-ins only work with data that is stored in the search index and not with the original source documents. SharePoint Add-ins are self-contained pieces of functionality that extend the capabilities of a SharePoint website. These add-ins solve specific business and end-user needs by integrating the best of the web and SharePoint. An add-in can contain various SharePoint elements like Lists, Remote Event Receivers, Content Types, Workflows, Workflow Custom Activities, Site Columns, Modules, Menu Item Custom Actions, Client Web Parts, and Search Configurations. For more information, see  [SharePoint Add-ins](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx).</span></span>
  
    
    

<span data-ttu-id="50be8-109">Надстройка поиска — SharePoint надстройку в том, что использование функциональной возможности поиска.</span><span class="sxs-lookup"><span data-stu-id="50be8-109">A search add-in is an SharePoint Add-in that uses search functionality.</span></span> <span data-ttu-id="50be8-110">В надстройке поиска можно использовать интерфейс API поиска SharePoint для поиска контента.</span><span class="sxs-lookup"><span data-stu-id="50be8-110">In a search add-in, you can use the SharePoint Search API to locate content.</span></span> <span data-ttu-id="50be8-111">В зависимости от типа разрешения в [манифесте надстройки](http://msdn.microsoft.com/library/7cd5850f-cbf3-48d2-bcb7-59b8f4ed0e63%28Office.15%29.aspx)можно выполнить поиск внутри или за пределами содержимое надстройки.</span><span class="sxs-lookup"><span data-stu-id="50be8-111">Depending on the type of permissions set up in your [add-in manifest](http://msdn.microsoft.com/library/7cd5850f-cbf3-48d2-bcb7-59b8f4ed0e63%28Office.15%29.aspx), you can search either inside or outside the contents of the add-in.</span></span> <span data-ttu-id="50be8-112">Кроме того можно также использовать надстройки поиска для распространения конфигурации поиска с одной установки SharePoint в другую.</span><span class="sxs-lookup"><span data-stu-id="50be8-112">In addition, you can also use a search add-in to distribute search configurations from one SharePoint installation to another.</span></span>
<span data-ttu-id="50be8-113">Разработка основных надстройки поиска зависит от Выбор метода развертывания.</span><span class="sxs-lookup"><span data-stu-id="50be8-113">The core design of a search add-in depends on the deployment method that you choose.</span></span> <span data-ttu-id="50be8-114">В следующем разделе приводятся доступные параметры и их преимущества.</span><span class="sxs-lookup"><span data-stu-id="50be8-114">The following section summarizes the available options and their benefits.</span></span> <span data-ttu-id="50be8-115">Дополнительные сведения можно [выбрать шаблоны для разработки и размещения надстройки SharePoint](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="50be8-115">For more information, see  [Choose patterns for developing and hosting your SharePoint Add-in](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)</span></span>
  
    
    


## <a name="deploy-your-search-add-ins"></a><span data-ttu-id="50be8-116">Развертывание надстройки поиска</span><span class="sxs-lookup"><span data-stu-id="50be8-116">Deploy your search add-ins</span></span>
<span data-ttu-id="50be8-117"><a name="SP15_Deploy_search_apps"> </a></span><span class="sxs-lookup"><span data-stu-id="50be8-117"></span></span>

<span data-ttu-id="50be8-118">Развертывание надстройки поиска двумя способами:</span><span class="sxs-lookup"><span data-stu-id="50be8-118">There are two ways to deploy your search add-in:</span></span>
  
    
    

1. <span data-ttu-id="50be8-p103">SharePoint hosted - локальное развертывание. Надстройка поиска размещается внутри корпоративной сети на серверах компании. Компании Администраторы управляют надстройки. Этот сценарий предлагает гибкие возможности развертывания и поддержки, так как к оборудованию и программному обеспечению локально поддерживается администраторами.</span><span class="sxs-lookup"><span data-stu-id="50be8-p103">SharePoint hosted - On-premises deployment. The search add-in is hosted inside the corporate network on the company's servers. The company's administrators manage the add-in. This scenario offers flexibility in deployment and support because the hardware and software is maintained locally by the administrators.</span></span>
    
  
2. <span data-ttu-id="50be8-p104">У поставщика - любой веб-сервере размещения. Надстройка поиска размещается с любым поставщиком, за пределами клиента SharePoint server.</span><span class="sxs-lookup"><span data-stu-id="50be8-p104">Provider hosted - Any web server hosting. The search add-in is hosted by any provider, outside of the customer's SharePoint server.</span></span> 
    
  

## <a name="search-add-in-development-environment"></a><span data-ttu-id="50be8-125">Среда разработки надстройки поиска</span><span class="sxs-lookup"><span data-stu-id="50be8-125">Search add-in development environment</span></span>
<span data-ttu-id="50be8-126"><a name="SP15_Search_app_dev_environment"> </a></span><span class="sxs-lookup"><span data-stu-id="50be8-126"></span></span>

<span data-ttu-id="50be8-127">Создание надстройки поиска, используйте следующий среды:</span><span class="sxs-lookup"><span data-stu-id="50be8-127">To create a search add-in, use following environment:</span></span>
  
    
    

- <span data-ttu-id="50be8-128">Microsoft Visual Studio 2012 или Microsoft Visual Studio 2013 или Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="50be8-128">Microsoft Visual Studio 2012 or Microsoft Visual Studio 2013 or Visual Studio 2015</span></span>
        
  
<span data-ttu-id="50be8-129">С помощью Visual Studio 2013 и более поздних версий можно опубликовать надстройки поиска в локальной или в Office 365.</span><span class="sxs-lookup"><span data-stu-id="50be8-129">With Visual Studio 2013 and later, you can publish your search add-ins to both on-premises or in Office 365.</span></span> <span data-ttu-id="50be8-130">Дополнительные сведения о средах разработки и как их использовать для создания надстроек поиска содержатся в разделе [Задание среды Общая разработка для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="50be8-130">For more information about the development environments and how to use them to create search add-ins, see  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="apis-for-search-add-ins"></a><span data-ttu-id="50be8-131">API-интерфейсы для поиска надстройки</span><span class="sxs-lookup"><span data-stu-id="50be8-131">APIs for search add-ins</span></span>
<span data-ttu-id="50be8-132"><a name="SP15_APIs_search_apps"> </a></span><span class="sxs-lookup"><span data-stu-id="50be8-132"></span></span>

<span data-ttu-id="50be8-133">Можно использовать широкий диапазон интерфейсов API, связанных с поиском, SharePoint предлагает для надстроек поиска. В следующей таблице перечислены эти интерфейсы API и место их библиотек классов.</span><span class="sxs-lookup"><span data-stu-id="50be8-133">You can use the wide range of search-related APIs that SharePoint offers for search add-ins. The following table lists these APIs and the location of their class libraries.</span></span>
  
    
    

<span data-ttu-id="50be8-134">**API-интерфейсов SharePoint для надстроек поиска**</span><span class="sxs-lookup"><span data-stu-id="50be8-134">**SharePoint APIs for Search add-ins**</span></span>


|<span data-ttu-id="50be8-135">**Имя API**</span><span class="sxs-lookup"><span data-stu-id="50be8-135">**API name**</span></span>|<span data-ttu-id="50be8-136">**Библиотека классов**</span><span class="sxs-lookup"><span data-stu-id="50be8-136">**Class library**</span></span>|
|:-----|:-----|
|<span data-ttu-id="50be8-137">Клиентская объектная модель .NET (CSOM)</span><span class="sxs-lookup"><span data-stu-id="50be8-137">.NET client object model (CSOM)</span></span>  <br/> |<span data-ttu-id="50be8-138">Microsoft.SharePoint.Client.Search.dll</span><span class="sxs-lookup"><span data-stu-id="50be8-138">Microsoft.SharePoint.Client.Search.dll</span></span>  <br/> |
|<span data-ttu-id="50be8-139">Silverlight CSOM</span><span class="sxs-lookup"><span data-stu-id="50be8-139">Silverlight CSOM</span></span>  <br/> |<span data-ttu-id="50be8-140">Microsoft.SharePoint.Client.Search.Silverlight.dll</span><span class="sxs-lookup"><span data-stu-id="50be8-140">Microsoft.SharePoint.Client.Search.Silverlight.dll</span></span>  <br/> |
|<span data-ttu-id="50be8-141">Объектная модель ECMAScript (JavaScript, JScript) (JSOM)</span><span class="sxs-lookup"><span data-stu-id="50be8-141">ECMAScript (JavaScript, JScript) object model (JSOM)</span></span>  <br/> |<span data-ttu-id="50be8-142">SP.search.js</span><span class="sxs-lookup"><span data-stu-id="50be8-142">SP.search.js</span></span>  <br/> |
|<span data-ttu-id="50be8-143">Поиск API-ИНТЕРФЕЙС REST</span><span class="sxs-lookup"><span data-stu-id="50be8-143">Search REST API</span></span>  <br/> |<span data-ttu-id="50be8-144">http://Server/_api/Search/Query</span><span class="sxs-lookup"><span data-stu-id="50be8-144">http://server/_api/search/query</span></span>  <br/> |
   

### <a name="code-examples"></a><span data-ttu-id="50be8-145">примеры кода</span><span class="sxs-lookup"><span data-stu-id="50be8-145">Code examples</span></span>

<span data-ttu-id="50be8-p106">Вот несколько примеров кода, с помощью различных интерфейсов API. Каждый пример кода отправляет запрос простой Поиск, который содержит ключевое слово "SharePoint " Приложение-служба поиска (SSA).</span><span class="sxs-lookup"><span data-stu-id="50be8-p106">Here are some code examples using the different APIs. Each code example sends a simple Search query that contains the keyword "SharePoint" to the Search service application (SSA).</span></span>
  
    
    
 <span data-ttu-id="50be8-148">**Client-side Object Model (CSOM)**</span><span class="sxs-lookup"><span data-stu-id="50be8-148">**Client-side Object Model (CSOM)**</span></span>
  
    
    

  
    
    



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

 <span data-ttu-id="50be8-149">**JavaScript Object Model (JSOM)**</span><span class="sxs-lookup"><span data-stu-id="50be8-149">**JavaScript Object Model (JSOM)**</span></span>
  
    
    

  
    
    



```

var keywordQuery = new
Microsoft.SharePoint.Client.Search.Query.KeywordQuery(context);
keywordQuery.set_queryText('SharePoint');
var searchExecutor = new Microsoft.SharePoint.Client.Search.Query.SearchExecutor(context);
results = searchExecutor.executeQuery(keywordQuery);
context.executeQueryAsync(onQuerySuccess, onQueryFail);
```

 <span data-ttu-id="50be8-150">**REST**</span><span class="sxs-lookup"><span data-stu-id="50be8-150">**REST**</span></span>
  
    
    

  
    
    
<span data-ttu-id="50be8-151">HTTP-запрос GET</span><span class="sxs-lookup"><span data-stu-id="50be8-151">HTTP GET request</span></span>
  
    
    



```HTML

http://mylocalhost/_api/search/query?querytext='SharePoint'
```

<span data-ttu-id="50be8-152">HTTP-запрос POST</span><span class="sxs-lookup"><span data-stu-id="50be8-152">HTTP POST request</span></span>
  
    
    



```HTML
{
'__metadata' : {'type' : 'Microsoft.Office.Server.Search.REST.SearchRequest'},
'Querytext' : 'SharePoint'
}
```


## <a name="search-add-in-permissions"></a><span data-ttu-id="50be8-153">Добавить разрешения поиска</span><span class="sxs-lookup"><span data-stu-id="50be8-153">Search add-in permissions</span></span>
<span data-ttu-id="50be8-154"><a name="SP15_Search_app_permissions"> </a></span><span class="sxs-lookup"><span data-stu-id="50be8-154"></span></span>

<span data-ttu-id="50be8-p107">Надстройки поиска отправлять запросы запроса Приложение-служба поиска (SSA) и надстроек, требуют различных типов разрешений для правильной работы. Можно настроить эти разрешения с помощью надстройки файл манифеста, который является частью надстройки каждого SharePoint. Добавить в файл манифеста можно изменять напрямую с помощью текстового редактора или изменять его с Visual Studio или Napa, как показано на следующих рисунках.</span><span class="sxs-lookup"><span data-stu-id="50be8-p107">Search add-ins send query requests to the Search service application (SSA), and the add-ins require different types of permissions to function correctly. You can configure these permissions via the add-in manifest file, which is a part of each SharePoint add-in. You can modify the add-in manifest file directly with a text editor, or you can modify it with Visual Studio or Napa, as shown in the following figures.</span></span> 
  
    
    

<span data-ttu-id="50be8-158">**На рисунке 1: Установка разрешений для поиска надстроек в Visual Studio 2015**</span><span class="sxs-lookup"><span data-stu-id="50be8-158">**Figure 1: Setting up permissions for search add-ins in Visual Studio 2015**</span></span>

  
    
    

  
    
    
![Настройка разрешений поискового приложения с помощью Visual Studio](../images/SP15_search_apps_permission_Visual_Studio.PNG)
  
    
    

  
    
    

  
    
    

<span data-ttu-id="50be8-160">**На рисунке 2: Настройка разрешений для надстроек поиска в средства разработки «Napa» Office 365**</span><span class="sxs-lookup"><span data-stu-id="50be8-160">**Figure 2: Setting up permissions for search add-ins in "Napa" Office 365 Development Tools**</span></span>

  
    
    

  
    
    
![Настройка разрешений поискового приложения с помощью Napa](../images/SP15_search_app_permission_Napa.gif)
  
    
    
<span data-ttu-id="50be8-p108">Надстройка SharePoint имеет свой собственный идентификатор, связанный с субъекта безопасности именем субъекта надстройки. Как пользователи и группы субъект надстройки имеет определенные разрешения и права. Субъект надстройки имеет права полного доступа add в веб-приложения, его необходимо только запрашивать разрешения на SharePoint ресурсы в другие расположения за пределами web надстройки, такие как семейств веб-сайтов или веб-сайт. В отличие от других Надстройки SharePoint надстройки поиска требуются только разрешения уровня пользователя, известных как **QueryAsUserIgnoreAppPrincipal**. Это разрешение позволяет запросов поиска надстройки на основе разрешений пользователя. Это означает, что поиск, возвращаются результаты, основанные на списки контроля доступа пользователя.</span><span class="sxs-lookup"><span data-stu-id="50be8-p108">An SharePoint Add-in has its own identity and is associated with a security principal, called an add-in principal. Like users and groups, an add-in principal has certain permissions and rights. The add-in principal has full control rights to the add-in web, so it only needs to request permissions to SharePoint resources in the host web or other locations outside the add-in web, such as site collections. Unlike other SharePoint Add-ins, a search add-in requires only user-level permissions, known as **QueryAsUserIgnoreAppPrincipal**. This permission lets you query the search add-in based on the user's permissions. This means that search results will be returned based on the user's ACLs.</span></span> 
  
    
    

### <a name="request-permissions-in-the-add-in-manifest-file"></a><span data-ttu-id="50be8-168">Запрашивать разрешения в файле манифеста надстройки</span><span class="sxs-lookup"><span data-stu-id="50be8-168">Request permissions in the add-in manifest file</span></span>

<span data-ttu-id="50be8-p109">Добавить в файл манифеста в формате XML и непосредственного редактирования. Для получения разрешений, создаваемом запроса, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="50be8-p109">The add-in manifest file is in XML format and can be edited directly. To get permissions, you write a request, as shown in the following example:</span></span>
  
    
    

```XML

<AppPermissionRequests>
  <AppPermissionRequest Scope="http://sharepoint/search" Right="QueryAsUserIgnoreAppPrincipal" />
</AppPermissionRequests>
```


## <a name="additional-resources"></a><span data-ttu-id="50be8-171">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="50be8-171">Additional resources</span></span>
<span data-ttu-id="50be8-172"><a name="SP15_Search_app_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="50be8-172"></span></span>


-  [<span data-ttu-id="50be8-173">Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-173">SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/cd1eda9e-8e54-4223-93a9-a6ea0d18df70%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="50be8-174">Выбор шаблонов для разработки и размещения надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-174">Choose patterns for developing and hosting your SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/05ce5435-0a03-4ddc-976b-c33b08d03457%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="50be8-175">Разрешения для надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-175">Add-in permissions in SharePoint</span></span>](http://msdn.microsoft.com/library/5f7a8440-3c09-4cf8-83ec-c236bfa2d6c4%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="50be8-176">Типы политик авторизации надстроек в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-176">Add-in authorization policy types in SharePoint</span></span>](http://msdn.microsoft.com/library/124879c7-a746-4c10-96a7-da76ad5327f0%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="50be8-177">Важные аспекты архитектуры и разработки надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-177">Important aspects of the SharePoint Add-in architecture and development landscape</span></span>](http://msdn.microsoft.com/library/ae96572b-8f06-4fd3-854f-fc312f7f2d88%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="50be8-178">Изучите структуру манифеста надстройки и пакет надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-178">Explore the app manifest structure and the package of a SharePoint Add-in</span></span>](http://msdn.microsoft.com/library/7cd5850f-cbf3-48d2-bcb7-59b8f4ed0e63%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="50be8-179">Добавление возможностей поиска для надстройки для SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-179">Add search capabilities to your add-ins for SharePoint</span></span>](http://blogs.msdn.com/b/officeapps/archive/2013/05/30/add-search-capabilities-to-your-apps-for-sharepoint.aspx)
    
  
-  [<span data-ttu-id="50be8-180">Экспорт и импорт параметров конфигурации поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50be8-180">Exporting and importing search configuration settings in SharePoint</span></span>](exporting-and-importing-search-configuration-settings-in-sharepoint.md)
    
  
-  [<span data-ttu-id="50be8-181">Импорт и экспорт параметров конфигурации настраиваемого поиска в SharePoint (TechNet)</span><span class="sxs-lookup"><span data-stu-id="50be8-181">Export and import customized search configuration settings in SharePoint (TechNet)</span></span>](http://technet.microsoft.com/en-us/library/jj871675.aspx)
    
  

