---
title: "Фильтрация по ролям безопасности для поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fbbf0cc4-e135-426a-9996-34eb954dbd5a
ms.openlocfilehash: e88ad2c0ee1af00255d607d94f81693011fd9851
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="custom-security-trimming-for-search-in-sharepoint"></a><span data-ttu-id="81c09-102">Фильтрация по ролям безопасности для поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="81c09-102">Custom security trimming for Search in SharePoint</span></span>
<span data-ttu-id="81c09-103">Сведения о двух типах интерфейсов триммера безопасности, **ISecurityTrimmerPre** и **ISecurityTrimmerPost**и действия, которые необходимо выполнить, чтобы создать пользовательский триммер безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-103">Learn about the two kinds of custom security trimmer interfaces, **ISecurityTrimmerPre** and **ISecurityTrimmerPost**, and the steps you must take to create a custom security trimmer.</span></span>
<span data-ttu-id="81c09-104">Во время выполнения запроса поиска в SharePoint выполняет фильтрацию по ролям безопасности результатов поиска, основанные на идентификатор пользователя, отправившего запрос, с помощью сведения о безопасности, полученный из компонента обхода контента.</span><span class="sxs-lookup"><span data-stu-id="81c09-104">At query time, Search in SharePoint performs security trimming of search results that are based on the identity of the user submitting the query, by using the security information obtained from the crawl component.</span></span>
  
    
    

<span data-ttu-id="81c09-105">Возможно, некоторые сценарии, тем не менее, в которых результаты фильтрации по ролям встроенные функции безопасности не достаточно для конкретной ситуации.</span><span class="sxs-lookup"><span data-stu-id="81c09-105">You might have certain scenarios, however, in which the built-in security trimming results aren't sufficient for your requirements.</span></span> <span data-ttu-id="81c09-106">В подобных ситуациях необходимо реализовать фильтрации по ролям безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-106">In such scenarios, you need to implement custom security trimming.</span></span> <span data-ttu-id="81c09-107">Поиск в SharePoint предоставляет поддержку для фильтрации по ролям безопасности через интерфейс [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) , [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) интерфейс и интерфейс [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) (устарело) в [ Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) пространства имен.</span><span class="sxs-lookup"><span data-stu-id="81c09-107">Search in SharePoint provides support for custom security trimming through the  [ISecurityTrimmerPre](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx) interface, [ISecurityTrimmerPost](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx) interface, and [ISecurityTrimmer2](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmer2.aspx) interface (deprecated) in the [Microsoft.Office.Server.Search.Query](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.aspx) namespace.</span></span>

> [!NOTE]
> <span data-ttu-id="81c09-108">Настраиваемые перед триммеры не поддерживают идентификаторы безопасности Windows в списки управления доступом, только утверждений.</span><span class="sxs-lookup"><span data-stu-id="81c09-108">Custom pre-trimmers don't support Windows SIDs in ACLs, only claims.</span></span> <span data-ttu-id="81c09-109">Если какие-либо идентификатор безопасности заявляют, что возвращаются типы из настраиваемого триммера предварительной, полученные записи управления доступом в индексе кодируется как утверждение, не как ИД безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-109">If any of the SID claim types are returned from a custom pre-trimmer, the resulting ACEs in the index will be encoded as a claim, not as SID.</span></span> <span data-ttu-id="81c09-110">Поэтому они не соответствуют удостоверения пользователя Windows, основанных на ИД безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-110">Hence they do not match Windows user identities that are based on SIDs.</span></span>
  
    
    


## <a name="implementing-the-interfaces-for-custom-security-trimming"></a><span data-ttu-id="81c09-111">Реализация интерфейсов для фильтрации по ролям безопасности</span><span class="sxs-lookup"><span data-stu-id="81c09-111">Implementing the interfaces for custom security trimming</span></span>
<span data-ttu-id="81c09-112"><a name="Implementing_the_interfaces"> </a></span><span class="sxs-lookup"><span data-stu-id="81c09-112"></span></span>

<span data-ttu-id="81c09-p104">Интерфейс **ISecurityTrimmerPre** выполняет вычисление предварительная фильтрацию по ролям или предварительного запроса, где переписывать поисковый запрос для добавления сведений о безопасности перед сопоставление поисковый запрос в поисковый индекс. Интерфейс **ISecurityTrimmerPost** выполняет вычисление после обрезки или после запроса, где удаляются результатов поиска, прежде чем они возвращаются пользователю.</span><span class="sxs-lookup"><span data-stu-id="81c09-p104">The **ISecurityTrimmerPre** interface carries out pre-trimming, or pre-query evaluation, where the search query is rewritten to add security information before the search query is matched to the search index. The **ISecurityTrimmerPost** interface carries out post-trimming, or post-query evaluation, where the search results are pruned before they are returned to the user.</span></span>
  
    
    
<span data-ttu-id="81c09-p105">Рекомендуется использовать предварительная фильтрацию по ролям для повышения производительности и общие правильность; Предварительная фильтрацию по ролям предотвращает утечки информации для уточнения данных и нажатия количество экземпляров. После trimmers можно использовать в случаях, где фильтрации по ролям безопасности непредусмотренным точно с помощью фильтров запроса; Например при наличии в зависимости от часового пользователя выдачи запроса, таких как только официальный рабочее время документы нужно отфильтровать нет на месте.</span><span class="sxs-lookup"><span data-stu-id="81c09-p105">We recommend the use of pre-trimming for performance and general correctness; pre-trimming prevents information leakage for refiner data and hit count instances. Post-trimmers can be used in cases where the security trimming cannot be represented accurately with query filters; for example, if there is a need to filter away documents depending on the local time of the user issuing the query, such as during official business hours only.</span></span>
  
    
    

### <a name="implementing-the-isecuritytrimmerpre-interface"></a><span data-ttu-id="81c09-117">Реализация интерфейса ISecurityTrimmerPre</span><span class="sxs-lookup"><span data-stu-id="81c09-117">Implementing the ISecurityTrimmerPre interface</span></span>

<span data-ttu-id="81c09-118">Создание настраиваемых безопасности старые устройство обрезки для результатов поиска, необходимо создать компонентом, который интерфейс **ISecurityTrimmerPre**.</span><span class="sxs-lookup"><span data-stu-id="81c09-118">To create a custom security pre-trimmer for search results, you must create a component that implements the **ISecurityTrimmerPre** interface.</span></span>
  
    
    
<span data-ttu-id="81c09-119">Интерфейс **ISecurityTrimmerPre** содержит два метода, которые необходимо реализовать: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) и [AddAccess(Boolean, Claims)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .</span><span class="sxs-lookup"><span data-stu-id="81c09-119">The **ISecurityTrimmerPre** interface contains two methods that you must implement: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.Initialize.aspx) and [AddAccess(Boolean, Claims)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.AddAccess.aspx) .</span></span>
  
    
    

#### <a name="initialize-method"></a><span data-ttu-id="81c09-120">Метод Initialize</span><span class="sxs-lookup"><span data-stu-id="81c09-120">Initialize Method</span></span>

<span data-ttu-id="81c09-p106">Метод **Initialize** выполняется при устройство обрезки старые безопасности загружается в рабочий процесс, пока не будет повторно рабочий процесс не выполняет еще раз. Два параметра передаются в метод:</span><span class="sxs-lookup"><span data-stu-id="81c09-p106">The **Initialize** method is executed when the security pre-trimmer is loaded into the worker process, and does not execute again until the worker process is recycled. Two parameters are passed into the method:</span></span>
  
    
    

-  <span data-ttu-id="81c09-123">_staticProperties_:  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) объект, содержащий конфигурации свойства, заданные для устройство обрезки безопасности при регистрации приложения службы поиска.</span><span class="sxs-lookup"><span data-stu-id="81c09-123">_staticProperties_: A  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) object containing the configuration properties that are specified for the security trimmer when it is registered with the Search service application.</span></span>
    
  
-  <span data-ttu-id="81c09-124">_searchApplication_:  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) объект, который представляет приложения службы поиска.</span><span class="sxs-lookup"><span data-stu-id="81c09-124">_searchApplication_: A  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) object that represents the Search service application.</span></span>
    
  

#### <a name="addaccess-method"></a><span data-ttu-id="81c09-125">Метод AddAccess</span><span class="sxs-lookup"><span data-stu-id="81c09-125">AddAccess Method</span></span>

<span data-ttu-id="81c09-126">Метод **AddAccess** выполняется на устройство до обрезки, для каждого запроса входящих перед вычислением запрос один раз.</span><span class="sxs-lookup"><span data-stu-id="81c09-126">The **AddAccess** method is executed once per pre-trimmer, for each incoming query before the query is evaluated.</span></span>
  
    
    
<span data-ttu-id="81c09-127">Два параметра передаются в этот метод:</span><span class="sxs-lookup"><span data-stu-id="81c09-127">Two parameters are passed into this method:</span></span> 
  
    
    

-  <span data-ttu-id="81c09-128">_sessionProperties_: **[T:System.Collections.Generic.IDictionary<String,Object>]** объект, который содержит свойства запроса.</span><span class="sxs-lookup"><span data-stu-id="81c09-128">_sessionProperties_: A **[T:System.Collections.Generic.IDictionary<String,Object>]** object that contains the properties of the query.</span></span>
    
  
-  <span data-ttu-id="81c09-129">_userIdentity_:  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) объект, который содержит удостоверение пользователя.</span><span class="sxs-lookup"><span data-stu-id="81c09-129">_userIdentity_: A  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) object that contains the user identity.</span></span>
    
  

### <a name="implementing-the-isecuritytrimmerpost-interface"></a><span data-ttu-id="81c09-130">Реализация интерфейса ISecurityTrimmerPost</span><span class="sxs-lookup"><span data-stu-id="81c09-130">Implementing the ISecurityTrimmerPost interface</span></span>

<span data-ttu-id="81c09-131">Чтобы создать пользовательский безопасности после устройство обрезки для результатов поиска, необходимо создать компонентом, который интерфейс **ISecurityTrimmerPost**.</span><span class="sxs-lookup"><span data-stu-id="81c09-131">To create a custom security post-trimmer for search results, you must create a component that implements the **ISecurityTrimmerPost** interface.</span></span>
  
    
    
<span data-ttu-id="81c09-132">Интерфейс **ISecurityTrimmerPost** содержит два метода, которые необходимо реализовать: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) и **CheckAccess(IList<String>, IList<String>, IDictionary<String, Object>, IIdentity)**.</span><span class="sxs-lookup"><span data-stu-id="81c09-132">The **ISecurityTrimmerPost** interface contains two methods that you must implement: [Initialize(NameValueCollection, SearchServiceApplication)](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.Initialize.aspx) and **CheckAccess(IList<String>, IList<String>, IDictionary<String, Object>, IIdentity)**.</span></span>
  
    
    

#### <a name="initialize-method"></a><span data-ttu-id="81c09-133">Метод Initialize</span><span class="sxs-lookup"><span data-stu-id="81c09-133">Initialize method</span></span>

<span data-ttu-id="81c09-p107">Метод **Initialize** выполняется при устройство обрезки безопасности загружается в рабочий процесс, пока не будет повторно рабочий процесс не выполняет еще раз. Два параметра передаются в метод: и</span><span class="sxs-lookup"><span data-stu-id="81c09-p107">The **Initialize** method is executed when the security trimmer is loaded into the worker process, and does not execute again until the worker process is recycled. Two parameters are passed into the method:and</span></span>
  
    
    

-  <span data-ttu-id="81c09-136">_staticProperties_:  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) объект, содержащий свойства конфигурации, заданному для устройство обрезки безопасности при регистрации приложения службы поиска.</span><span class="sxs-lookup"><span data-stu-id="81c09-136">_staticProperties_: A  [NameValueCollection](https://msdn.microsoft.com/library/System.Collections.Specialized.NameValueCollection.aspx) object containing the configuration properties specified for the security trimmer when it is registered with the Search service application.</span></span>
    
  
-  <span data-ttu-id="81c09-137">_searchApplication_:  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) объект, который представляет приложения службы поиска.</span><span class="sxs-lookup"><span data-stu-id="81c09-137">_searchApplication_: A  [SearchServiceApplication](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Administration.SearchServiceApplication.aspx) object that represents the Search service application.</span></span>
    
  

#### <a name="checkaccess-method"></a><span data-ttu-id="81c09-138">Метод CheckAccess</span><span class="sxs-lookup"><span data-stu-id="81c09-138">CheckAccess method</span></span>

<span data-ttu-id="81c09-139">Метод **CheckAccess** выполняется один раз в устройство после обрезки, для каждого запроса результирующий набор, после оценки запроса.</span><span class="sxs-lookup"><span data-stu-id="81c09-139">The **CheckAccess** method is executed once per post-trimmer, for each result set query, after the query is evaluated.</span></span>
  
    
    
<span data-ttu-id="81c09-140">Четыре параметры передаются в этот метод:</span><span class="sxs-lookup"><span data-stu-id="81c09-140">Four parameters are passed into this method:</span></span>
  
    
    

-  <span data-ttu-id="81c09-141">_documentUrls_: A [IList\<T\> ](http://msdn2.microsoft.com/EN-US/library/5y536ey6) объект, который содержит URL-адреса для каждого элемента контента в результатах поиска, соответствующие правила обхода контента.</span><span class="sxs-lookup"><span data-stu-id="81c09-141">_documentUrls_: A  [IList\<T\>](http://msdn2.microsoft.com/EN-US/library/5y536ey6) object that contain the URLs for each content item from the search results that match the crawl rule.</span></span>
    
  
-  <span data-ttu-id="81c09-142">_documentAcls_: A [IList\<T\> ](http://msdn2.microsoft.com/EN-US/library/5y536ey6) object, содержащий элемент списков управления доступом для каждого элемента контента, чьи доступа — это будет определено в реализации триммера безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-142">_documentAcls_: A  [IList\<T\>](http://msdn2.microsoft.com/EN-US/library/5y536ey6) object containing item ACLs for each content item whose access is to be determined by the security trimmer implementation.</span></span>
    
  
-  <span data-ttu-id="81c09-143">_управляющегопользователями_: A [IDictionary\<TKey, TValue\> ](http://msdn2.microsoft.com/EN-US/library/s4ys34ea) object, содержащий контейнер временные свойств.</span><span class="sxs-lookup"><span data-stu-id="81c09-143">_sessionProperties_: A  [IDictionary\<TKey, TValue\>](http://msdn2.microsoft.com/EN-US/library/s4ys34ea) object containing the transient property bag.</span></span>
    
  
-  <span data-ttu-id="81c09-144">_userIdentity_: объекта  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) , из которого исполняющих объектов можно получить учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="81c09-144">_userIdentity_: An  [IIdentity](https://msdn.microsoft.com/library/System.Security.Principal.IIdentity.aspx) object from which implementers can retrieve the user's identity.</span></span>
    
  
<span data-ttu-id="81c09-p108">Метод **CheckAccess** возвращает [BitArray](https://msdn.microsoft.com/library/System.Collections.BitArray.aspx) объект, который представляет массив значений **true** или **false**, один для каждого URL-адреса элемента содержимого в **IList** объект, который был передан в качестве первого параметра метода. Компонент обработки запросов использует эти значения для выполнения после фильтрации по ролям безопасности результатов. Если значение массива для определенного элемента контента **true**, элемент включается в возвращаемые результаты; Если значение массива **false**, удалить элемент.</span><span class="sxs-lookup"><span data-stu-id="81c09-p108">The **CheckAccess** method returns a [BitArray](https://msdn.microsoft.com/library/System.Collections.BitArray.aspx) object that represents an array of **true** or **false** values, one for each content item URL in the **IList** object that is passed as the first parameter of the method. The query processing component uses these values to perform the security post-trimming of the results. If the array value for a particular content item is **true**, the item is included in the returned results; if the array value is **false**, the item is removed.</span></span>
  
    
    
<span data-ttu-id="81c09-p109">При реализации метода **CheckAccess** можно использовать двумя элементам данных для каждого элемента определить, следует ли возвращать **true** или **false** для элемента: удостоверение пользователя, отправившего запрос и URL-адрес элемента содержимого. Кроме того можно также передать информацию ACL настраиваемый документ от соединителя метода **CheckAccess**.</span><span class="sxs-lookup"><span data-stu-id="81c09-p109">When implementing the **CheckAccess** method, you can use two pieces of information for each item to determine whether to return **true** or **false** for the item: the identity of the user who submitted the query and the URL of the content item. Alternatively, you can also pass custom document ACL information from the connector to the **CheckAccess** method.</span></span>
  
    
    

#### <a name="retrieving-the-user-identity-for-your-security-trimmer"></a><span data-ttu-id="81c09-150">Получение удостоверение пользователя для вашей безопасности устройство обрезки</span><span class="sxs-lookup"><span data-stu-id="81c09-150">Retrieving the user identity for your security trimmer</span></span>

<span data-ttu-id="81c09-151">Удостоверение пользователя можно извлекать с текущего участника потока, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="81c09-151">You can retrieve the user's identity by accessing the thread's current principal, as shown in the following code example.</span></span>
  
    
    

```cs

IIdentity userIdentity = System.Threading.Thread.CurrentPrincipal.Identity;
```

<span data-ttu-id="81c09-152">Также необходимо включить следующую директиву пространства имен.</span><span class="sxs-lookup"><span data-stu-id="81c09-152">You must also include the following namespace directive.</span></span>
  
    
    



```cs
using System.Security.Principal;
```

<span data-ttu-id="81c09-153">Идентификатор пользователя также можно получить из параметра **passedUserIdentity** метода **CheckAccess**.</span><span class="sxs-lookup"><span data-stu-id="81c09-153">You can also retrieve the identity of the user from the **CheckAccess** method's **passedUserIdentity** parameter.</span></span>
  
    
    

#### <a name="passing-document-acls-from-the-connector-to-your-security-trimmers"></a><span data-ttu-id="81c09-154">Передача ACL документа из соединительную линию в вашей trimmers безопасности</span><span class="sxs-lookup"><span data-stu-id="81c09-154">Passing document ACLs from the connector to your security trimmers</span></span>

<span data-ttu-id="81c09-155">Соединитель, названия, является мост связи между SharePoint и внешней системы, на котором размещается внешних данных.</span><span class="sxs-lookup"><span data-stu-id="81c09-155">A connector, as the name implies, is a communication bridge between SharePoint and the external system that hosts the external data.</span></span> <span data-ttu-id="81c09-156">При работе с помощью настраиваемых соединителей можно передать сведения списка управления Доступом документа непосредственно после триммер путем установки свойства **docaclmeta** документа.</span><span class="sxs-lookup"><span data-stu-id="81c09-156">If you are working with custom connectors, you can pass the document's ACL information directly to the post-trimmer by setting the **docaclmeta** document property.</span></span> <span data-ttu-id="81c09-157">Настроенные соединители и конечные триммеры имеют одинаковый формат и интерпретации поля, вы можете использовать для передачи пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="81c09-157">As long as the configured connectors and post-trimmers have the same format and interpretation of the field, you are free to use it to pass custom data.</span></span>
  
    
    
<span data-ttu-id="81c09-p111">Строки, хранящиеся в **docaclmeta** соединителем будет контактной в параметре _documentAcls_ при вызове метод **CheckAccess** устройство обрезки настраиваемые безопасности. Обычный документ ACL в свойстве **docacl** обрабатываются по ролям безопасности основные и не отображаются на устройство обрезки настраиваемые безопасности. Аналогичным образом свойство **docaclmeta** не влияет на фильтрации по ролям безопасности основные.</span><span class="sxs-lookup"><span data-stu-id="81c09-p111">The strings stored in **docaclmeta** by the connector will surface in the _documentAcls_ parameter when the **CheckAccess** method of the custom security trimmer is invoked. The regular document ACLs in the **docacl** property are processed by basic security trimming and are not visible to the custom security trimmer. Similarly, the **docaclmeta** property does not have any effect on basic security trimming.</span></span>
  
    
    

#### <a name="post-trimmers-and-their-effect-on-refiner-count-for-security-trimmers"></a><span data-ttu-id="81c09-161">После trimmers и их влияние на количество уточнения для trimmers безопасности</span><span class="sxs-lookup"><span data-stu-id="81c09-161">Post-trimmers and their effect on refiner count for security trimmers</span></span>

<span data-ttu-id="81c09-p112">При работе с после trimmers важно Обратите внимание на то, что имеется два типа таблицы результатов: **RelevantResults** и **RefinementResults**. После trimmers применяются только к найденных результатов в **RelevantResults**. Таким образом возможно, там будут уточнения, связанные с ним в текстах усеченных обращений и **RefinementResults** count может быть больше или равно **RelevantResults**. Можно решить такое поведение двумя способами:</span><span class="sxs-lookup"><span data-stu-id="81c09-p112">When working with post-trimmers, it is important to notice that there are two types of result tables: **RelevantResults** and the **RefinementResults**. Post-trimmers are applied only to the result hits in the **RelevantResults**. Consequently, there may be refiners related to the post-trimmed hits and the **RefinementResults** count may be larger than or equal to the **RelevantResults**. You can address this behavior in two ways:</span></span>
  
    
    

- <span data-ttu-id="81c09-166">Исключение конфиденциальных уточнений панели уточнения результатов поиска в веб-части по умолчанию, чтобы утечки нет информации с помощью уточнения.</span><span class="sxs-lookup"><span data-stu-id="81c09-166">Exclude the sensitive refiners from the refinement panel in the default Web Part so that no information is leaked via the refiners.</span></span>
    
  
- <span data-ttu-id="81c09-167">Использование настраиваемых веб-части для отображения уточнения или результаты при использовании после trimmers таким образом, чтобы **RefinementResults** могут быть скрыты элегантно в случаях, где **RefinementResults** count превышает число **RelevantResults**.</span><span class="sxs-lookup"><span data-stu-id="81c09-167">Use a custom Web Part to display results or refiners when using post-trimmers so that the **RefinementResults** may be elegantly hidden in cases where the **RefinementResults** count exceeds the **RelevantResults** count.</span></span>
    
  

### <a name="retrieving-individual-configuration-properties-for-your-security-trimmer"></a><span data-ttu-id="81c09-168">Получение свойств отдельной конфигурации для вашей безопасности устройство обрезки</span><span class="sxs-lookup"><span data-stu-id="81c09-168">Retrieving individual configuration properties for your security trimmer</span></span>

<span data-ttu-id="81c09-p113">Можно получить доступ к отдельной конфигурации свойства, используя имя свойства, который был указан при регистрации устройство обрезки после безопасности. Например следующий код возвращает значение для настройки свойство с именем **CheckLimit**.</span><span class="sxs-lookup"><span data-stu-id="81c09-p113">You can access an individual configuration property by using the property name that was specified when the security post-trimmer was registered. For example, the following code retrieves the value for a configuration property named **CheckLimit**.</span></span>
  
    
    

```cs
public void Initialize(NameValueCollection staticProperties, SearchServiceApplication searchApplication)
{
    if (staticProperties["CheckLimitProperty"] != null)
    {
         intCheckLimit = Convert.ToInt32(staticProperties["CheckLimitProperty"]);
    }
}
```


## <a name="deploying-the-custom-security-trimmer-component"></a><span data-ttu-id="81c09-171">Развертывание компонента настраиваемого триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="81c09-171">Deploying the custom security trimmer component</span></span>
<span data-ttu-id="81c09-172"><a name="Deploying_the_trimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="81c09-172"></span></span>

<span data-ttu-id="81c09-p114">После создания устройство обрезки выборочные ее необходимо развернуть в глобальный кэш на любом сервере роль запроса. Шаг 2 в  [Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md) описывает процесс развертывания устройство обрезки выборочные глобальный кэш.</span><span class="sxs-lookup"><span data-stu-id="81c09-p114">After you create the custom security trimmer, you must deploy it to the global assembly cache on any server in the Query role. Step 2 in  [How to: Use a custom security trimmer for SharePoint Server search results](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md) describes the process for deploying the custom security trimmer to the global assembly cache.</span></span>
  
    
    

## <a name="registering-the-custom-security-trimmer"></a><span data-ttu-id="81c09-175">Регистрация пользовательского триммера безопасности</span><span class="sxs-lookup"><span data-stu-id="81c09-175">Registering the custom security trimmer</span></span>
<span data-ttu-id="81c09-176"><a name="Registering_the_trimmer"> </a></span><span class="sxs-lookup"><span data-stu-id="81c09-176"></span></span>

<span data-ttu-id="81c09-177">После trimmers для регистрации обрезки выборочные необходимо связать с определенного приложения службы поиска и правило обхода контента; для предварительного trimmers это не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="81c09-177">For post-trimmers, you must associate a custom security trimmer registration with a specific Search service application and crawl rule; for pre-trimmers, this is optional.</span></span>
  
    
    
<span data-ttu-id="81c09-178">Используйте командлет **SPEnterpriseSearchSecurityTrimmer**Командная консоль SharePoint зарегистрировать устройство выборочные обрезки.</span><span class="sxs-lookup"><span data-stu-id="81c09-178">You use the **SPEnterpriseSearchSecurityTrimmer** cmdlet of the SharePoint Management Shell to register a custom security trimmer.</span></span>
  
    
    
<span data-ttu-id="81c09-179">В следующей таблице описаны параметры, которые использует командлет.</span><span class="sxs-lookup"><span data-stu-id="81c09-179">The following table describes the parameters that the cmdlet uses.</span></span>
  
    
    

<span data-ttu-id="81c09-180">**Таблица 1. Параметры командлета SPEnterpriseSearchSecurityTrimmer**</span><span class="sxs-lookup"><span data-stu-id="81c09-180">**Table 1. Parameters used by the SPEnterpriseSearchSecurityTrimmer cmdlet**</span></span>


|<span data-ttu-id="81c09-181">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="81c09-181">**Parameter**</span></span>|<span data-ttu-id="81c09-182">**Описание**</span><span class="sxs-lookup"><span data-stu-id="81c09-182">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="81c09-183">_Приложение службы_</span><span class="sxs-lookup"><span data-stu-id="81c09-183">_SearchApplication_</span></span> <br/> |<span data-ttu-id="81c09-p115">Обязательно. Имя приложения службы поиска, например «приложения службы поиска».</span><span class="sxs-lookup"><span data-stu-id="81c09-p115">Required. The name of the Search service application, for example "Search Service Application".</span></span>  <br/> |
| <span data-ttu-id="81c09-186">_Имя типа_</span><span class="sxs-lookup"><span data-stu-id="81c09-186">_typeName_</span></span> <br/> |<span data-ttu-id="81c09-p116">Обязательный атрибут. Строгое имя сборки пользовательских триммеров безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-p116">Required. The strong name of the custom security trimmer assembly.</span></span>  <br/> |
| <span data-ttu-id="81c09-189">_RulePath_</span><span class="sxs-lookup"><span data-stu-id="81c09-189">_RulePath_</span></span> <br/> |<span data-ttu-id="81c09-p117">Обязательно для после trimmers; необязательно для предварительного trimmers. Правило обхода контента для устройство обрезки безопасности.</span><span class="sxs-lookup"><span data-stu-id="81c09-p117">Required for post-trimmers; optional for pre-trimmers. The crawl rule for the security trimmer.  </span></span><br/> <span data-ttu-id="81c09-192">**Примечание**: рекомендуется использовать одно правило каждого источника контента.</span><span class="sxs-lookup"><span data-stu-id="81c09-192">**Note**: We recommend using one crawl rule per content source.</span></span>           |
| <span data-ttu-id="81c09-193">_id_</span><span class="sxs-lookup"><span data-stu-id="81c09-193">_id_</span></span> <br/> |<span data-ttu-id="81c09-p118">Обязательный атрибут. Идентификатор триммера безопасности. Это уникальное значение. При регистрации триммера безопасности с идентификатором, который уже зарегистрирован для другого триммера безопасности, то регистрация первого триммера заменяется регистрацией второго.</span><span class="sxs-lookup"><span data-stu-id="81c09-p118">Required. The security trimmer identifier (ID). This value is unique; if a security trimmer is registered with an ID that is already registered for another security trimmer, the registration for the first trimmer is overwritten with the registration for the second trimmer.</span></span>  <br/> |
| <span data-ttu-id="81c09-197">_properties_</span><span class="sxs-lookup"><span data-stu-id="81c09-197">_properties_</span></span> <br/> |<span data-ttu-id="81c09-p119">Необязательный атрибут. Пары имя/значение, указывающие свойства конфигурации. Должны иметь следующий формат:  `Name1~Value1~Name2~Value~???`</span><span class="sxs-lookup"><span data-stu-id="81c09-p119">Optional. The name-value pairs specifying the configuration properties. Must be in the following format:  `Name1~Value1~Name2~Value~???`</span></span> <br/> |
   
<span data-ttu-id="81c09-201">Пример основные команды для регистрации устройство выборочные обрезки и пример, задающее свойства конфигурации, читайте в статье  [Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span><span class="sxs-lookup"><span data-stu-id="81c09-201">For an example of a basic command for registering a custom security trimmer and a sample that specifies the configuration properties, see  [How to: Use a custom security trimmer for SharePoint Server search results](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md).</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="81c09-202">См. также</span><span class="sxs-lookup"><span data-stu-id="81c09-202">See also</span></span>
<span data-ttu-id="81c09-203"><a name="bk_sectrimmer_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="81c09-203"></span></span>


-  [<span data-ttu-id="81c09-204">Способ: использование пользовательского триммера безопасности для результатов поиска SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="81c09-204">How to: Use a custom security trimmer for SharePoint Server search results</span></span>](how-to-use-a-custom-security-trimmer-for-sharepoint-server-search-results.md)
    
  
-  [<span data-ttu-id="81c09-205">ISecurityTrimmerPre</span><span class="sxs-lookup"><span data-stu-id="81c09-205">ISecurityTrimmerPre</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPre.aspx)
    
  
-  [<span data-ttu-id="81c09-206">ISecurityTrimmerPost</span><span class="sxs-lookup"><span data-stu-id="81c09-206">ISecurityTrimmerPost</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.ISecurityTrimmerPost.aspx)
    
  
-  [<span data-ttu-id="81c09-207">Общие сведения о Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="81c09-207">Overview of Business Connectivity Services in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/ee661740.aspx)
    
  
