---
title: "BCS клиента Справочник по объектной модели для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fe7d12a3-6ea9-47f9-b69e-f66da9e661dc
ms.openlocfilehash: 270b8d32d5f416f9e4ac37f1452ea672a737b5b1
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="bcs-client-object-model-reference-for-sharepoint"></a><span data-ttu-id="5b291-102">BCS клиента Справочник по объектной модели для SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-102">BCS client object model reference for SharePoint</span></span>

  
    
    
![Ссылки и библиотеки класса](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="5b291-104">Сведения об объектах, доступных для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемые Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="5b291-104">Learn about the objects that are available for creating client-side scripts using the SharePoint client object model to access external data exposed by Business Connectivity Services (BCS).</span></span>
<span data-ttu-id="5b291-105">Доступны следующие объекты для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, взаимодействующий с Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="5b291-105">The following objects are available for creating client-side scripts using the SharePoint client object model to access external data that is exposed by Business Connectivity Services (BCS).</span></span> <span data-ttu-id="5b291-106">BCS объектной модели, компоненты, предоставляемые клиентскую объектную модель, находятся в библиотеке Microsoft.SharePoint.Client.dll.</span><span class="sxs-lookup"><span data-stu-id="5b291-106">The BCS object model components that are exposed to the client object model are located in Microsoft.SharePoint.Client.dll.</span></span>
  
    
    


## <a name="entity-object"></a><span data-ttu-id="5b291-107">Объект сущности</span><span class="sxs-lookup"><span data-stu-id="5b291-107">Entity object</span></span>
<span data-ttu-id="5b291-108"><a name="bkmk_Entity"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-108"></span></span>

<span data-ttu-id="5b291-p102">Объект **Entity** по сути представляет таблицу в базе данных. Методы и свойства, представленные здесь Показать объекты, которые можно управлять с помощью клиентской библиотеки кода. Каждый из этих вызовов сопоставляет непосредственно звонка server объектной модели. Тем не менее они могут вызываться отключением клиента, такие как и в веб-браузере с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5b291-p102">The **Entity** object essentially represents a table in a database. The methods and properties presented here show the objects that can be manipulated through the use of the client code library. Each of these calls maps directly to a server object model call. However, they are callable by a detached client, such as in a web browser using JavaScript.</span></span>
  
    
    

<span data-ttu-id="5b291-113">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-113">**Methods**</span></span>


|<span data-ttu-id="5b291-114">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-114">**Methods**</span></span>|<span data-ttu-id="5b291-115">**Подпись метода**</span><span class="sxs-lookup"><span data-stu-id="5b291-115">**Method signature**</span></span>|<span data-ttu-id="5b291-116">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-116">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-117">**Create**</span><span class="sxs-lookup"><span data-stu-id="5b291-117">**Create**</span></span> <br/> | `Identity Create(FieldValueDictionary fieldValues, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="5b291-118">**FindSpecificDefault**</span><span class="sxs-lookup"><span data-stu-id="5b291-118">**FindSpecificDefault**</span></span> <br/> | `EntityInstance FindSpecificDefault(Identity identity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="5b291-119">**FindspecificByBdcIDDefault**</span><span class="sxs-lookup"><span data-stu-id="5b291-119">**FindspecificByBdcIDDefault**</span></span> <br/> | `EntityInstance FindSpecific(Identity identity, string specificFinderName, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="5b291-120">**FindSpecificByBdcID**</span><span class="sxs-lookup"><span data-stu-id="5b291-120">**FindSpecificByBdcID**</span></span> <br/> | `EntityInstance FindSpecificByBdcIDDefault(string BdcIdentity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="5b291-121">**GetCreatorView**</span><span class="sxs-lookup"><span data-stu-id="5b291-121">**GetCreatorView**</span></span> <br/> | `EntityInstance FindSpecificByBdcID(string BdcIdentity, string specificFinderName,LobSystemInstance LobSystemInstanceName)` <br/> ||
|<span data-ttu-id="5b291-122">**GetDefaultSpecificFinderView**</span><span class="sxs-lookup"><span data-stu-id="5b291-122">**GetDefaultSpecificFinderView**</span></span> <br/> | `View GetCreatorView(string methodInstanceName)` <br/> ||
|<span data-ttu-id="5b291-123">**GetSpecificFinderView_Client**</span><span class="sxs-lookup"><span data-stu-id="5b291-123">**GetSpecificFinderView_Client**</span></span> <br/> | `View GetDefaultSpecificFinderView()` <br/> ||
|<span data-ttu-id="5b291-124">**GetUpdaterView_Client**</span><span class="sxs-lookup"><span data-stu-id="5b291-124">**GetUpdaterView_Client**</span></span> <br/> | `View GetSpecificFinderView_Client( string specificFinderName)` <br/> ||
|<span data-ttu-id="5b291-125">**GetIdentifiers**</span><span class="sxs-lookup"><span data-stu-id="5b291-125">**GetIdentifiers**</span></span> <br/> | `View GetUpdaterView_Client(string updaterName)` <br/> ||
|<span data-ttu-id="5b291-126">**GetIdentifiers()**</span><span class="sxs-lookup"><span data-stu-id="5b291-126">**GetIdentifiers()**</span></span> <br/> |||
   

<span data-ttu-id="5b291-127">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="5b291-127">**Properties**</span></span>


|<span data-ttu-id="5b291-128">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-128">**Property**</span></span>|<span data-ttu-id="5b291-129">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-129">**Description**</span></span>|
|:-----|:-----|
| `long EstimatedInstanceCount { get; }` <br/> |<span data-ttu-id="5b291-130">Получает число ожидаемых внешние элементы этого внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="5b291-130">Gets the number of expected external items of this external content type.</span></span>  <br/> |
| `string Name { get; }` <br/> |<span data-ttu-id="5b291-131">Возвращает имя объекта метаданных.</span><span class="sxs-lookup"><span data-stu-id="5b291-131">Gets the name of the metadata object.</span></span>  <br/> |
| `string Namespace { get; }` <br/> |<span data-ttu-id="5b291-132">Возвращает пространство имен класса данных.</span><span class="sxs-lookup"><span data-stu-id="5b291-132">Gets the namespace of the given data class.</span></span>  <br/> |
| `int GetIdentifierCount()` <br/> ||
   

## <a name="entityinstance-method"></a><span data-ttu-id="5b291-133">Метод экземпляра сущности</span><span class="sxs-lookup"><span data-stu-id="5b291-133">EntityInstance method</span></span>
<span data-ttu-id="5b291-134"><a name="bkmk_EntityInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-134"></span></span>


<span data-ttu-id="5b291-135">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-135">**Namespaces**</span></span>


|<span data-ttu-id="5b291-136">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-136">**Managed**</span></span>|<span data-ttu-id="5b291-137">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-137">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-138">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-138">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="5b291-139">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-139">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="5b291-140">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-140">**Methods**</span></span>


|<span data-ttu-id="5b291-141">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-141">**Method**</span></span>|<span data-ttu-id="5b291-142">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-142">**Return type**</span></span>|<span data-ttu-id="5b291-143">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-143">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-144">**Delete**</span><span class="sxs-lookup"><span data-stu-id="5b291-144">**Delete**</span></span> <br/> |<span data-ttu-id="5b291-145">void</span><span class="sxs-lookup"><span data-stu-id="5b291-145">void</span></span>  <br/> |<span data-ttu-id="5b291-146">Удаление внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="5b291-146">Deletes the External Item.</span></span>  <br/> |
|<span data-ttu-id="5b291-147">**FromXml**</span><span class="sxs-lookup"><span data-stu-id="5b291-147">**FromXml**</span></span> <br/> |<span data-ttu-id="5b291-148">void</span><span class="sxs-lookup"><span data-stu-id="5b291-148">void</span></span>  <br/> |<span data-ttu-id="5b291-149">Задает значения в словаре из указанного XML.</span><span class="sxs-lookup"><span data-stu-id="5b291-149">Sets the values in this dictionary from specified XML.</span></span>  <br/> <span data-ttu-id="5b291-150">**Подпись метода**          `FromXml(string xml)`</span><span class="sxs-lookup"><span data-stu-id="5b291-150">**Method signature**          `FromXml(string xml)`</span></span> <br/> |
|<span data-ttu-id="5b291-151">**GetIdentity**</span><span class="sxs-lookup"><span data-stu-id="5b291-151">**GetIdentity**</span></span> <br/> |<span data-ttu-id="5b291-152">Identity</span><span class="sxs-lookup"><span data-stu-id="5b291-152">Identity</span></span>  <br/> |<span data-ttu-id="5b291-153">Получает идентификатор этого внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="5b291-153">Gets the identity of this External Item.</span></span>  <br/> |
|<span data-ttu-id="5b291-154">**Delete**</span><span class="sxs-lookup"><span data-stu-id="5b291-154">**Delete**</span></span> <br/> |<span data-ttu-id="5b291-155">void</span><span class="sxs-lookup"><span data-stu-id="5b291-155">void</span></span>  <br/> |<span data-ttu-id="5b291-156">Удаление внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="5b291-156">Deletes the External Item.</span></span>  <br/> |
|<span data-ttu-id="5b291-157">**ToXml**</span><span class="sxs-lookup"><span data-stu-id="5b291-157">**ToXml**</span></span> <br/> |<span data-ttu-id="5b291-158">string</span><span class="sxs-lookup"><span data-stu-id="5b291-158">string</span></span>  <br/> |<span data-ttu-id="5b291-159">Извлекает значения в формате XML.</span><span class="sxs-lookup"><span data-stu-id="5b291-159">Retrieves the values in XML format.</span></span>  <br/> |
|<span data-ttu-id="5b291-160">**Update**</span><span class="sxs-lookup"><span data-stu-id="5b291-160">**Update**</span></span> <br/> |<span data-ttu-id="5b291-161">void</span><span class="sxs-lookup"><span data-stu-id="5b291-161">void</span></span>  <br/> |<span data-ttu-id="5b291-162">Отправляет данные изменения, внесенные внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="5b291-162">Submits the changes made to the External Item.</span></span>  <br/> |
   

  
    
    

<span data-ttu-id="5b291-163">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-163">**Properties**</span></span>


|<span data-ttu-id="5b291-164">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-164">**Property**</span></span>|<span data-ttu-id="5b291-165">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-165">**Return type**</span></span>|<span data-ttu-id="5b291-166">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-166">**Description**</span></span>|
|:-----|:-----|:-----|
| `this[string fieldDotNotation] { get; set; }` <br/> |<span data-ttu-id="5b291-167">Объект</span><span class="sxs-lookup"><span data-stu-id="5b291-167">Object</span></span>  <br/> |<span data-ttu-id="5b291-168">Получает или задает значение поля, на который ссылается точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="5b291-168">Gets or sets the value of the field referred to by the dot notation.</span></span>  <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |<span data-ttu-id="5b291-169">строка</span><span class="sxs-lookup"><span data-stu-id="5b291-169">string</span></span>  <br/> ||
   

## <a name="entityview-method"></a><span data-ttu-id="5b291-170">Метод EntityView</span><span class="sxs-lookup"><span data-stu-id="5b291-170">EntityView method</span></span>
<span data-ttu-id="5b291-171"><a name="bkmk_entityview"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-171"></span></span>

<span data-ttu-id="5b291-172">Определяет настраиваемое представление данных **сущности**</span><span class="sxs-lookup"><span data-stu-id="5b291-172">Specifies a customized view of the **Entity** data</span></span>
  
    
    

<span data-ttu-id="5b291-173">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-173">**Namespaces**</span></span>


|<span data-ttu-id="5b291-174">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-174">**Managed**</span></span>|<span data-ttu-id="5b291-175">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-175">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-176">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="5b291-176">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="5b291-177">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="5b291-177">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="5b291-178">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-178">**Methods**</span></span>


|<span data-ttu-id="5b291-179">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-179">**Method**</span></span>|<span data-ttu-id="5b291-180">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-180">**Return type**</span></span>|<span data-ttu-id="5b291-181">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-181">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-182">**GetDefaultValues_Client()**</span><span class="sxs-lookup"><span data-stu-id="5b291-182">**GetDefaultValues_Client()**</span></span> <br/> |<span data-ttu-id="5b291-183">**Словаря**</span><span class="sxs-lookup"><span data-stu-id="5b291-183">**FieldValueDictionary**</span></span> <br/> |<span data-ttu-id="5b291-184">Получает словарь значение поля, который содержит значения по умолчанию для этого представления.</span><span class="sxs-lookup"><span data-stu-id="5b291-184">Gets a field value dictionary that contains the default values for this view.</span></span>  <br/> |
|<span data-ttu-id="5b291-185">**GetXmlSchema()**</span><span class="sxs-lookup"><span data-stu-id="5b291-185">**GetXmlSchema()**</span></span> <br/> |<span data-ttu-id="5b291-186">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-186">**string**</span></span> <br/> |<span data-ttu-id="5b291-187">Возвращает схему XML для представления.</span><span class="sxs-lookup"><span data-stu-id="5b291-187">Gets the XML Schema of the view.</span></span>  <br/> |
|<span data-ttu-id="5b291-188">**GetType (строка fieldDotNotation)**</span><span class="sxs-lookup"><span data-stu-id="5b291-188">**GetType(string fieldDotNotation)**</span></span> <br/> |<span data-ttu-id="5b291-189">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-189">**string**</span></span> <br/> |<span data-ttu-id="5b291-190">Получает тип указанного поля.</span><span class="sxs-lookup"><span data-stu-id="5b291-190">Gets the type of the specified field.</span></span>  <br/> |
|<span data-ttu-id="5b291-191">**GetType (строка fieldDotNotation)**</span><span class="sxs-lookup"><span data-stu-id="5b291-191">**GetType(string fieldDotNotation)**</span></span> <br/> |<span data-ttu-id="5b291-192">**Дескриптор типа**</span><span class="sxs-lookup"><span data-stu-id="5b291-192">**TypeDescriptor**</span></span> <br/> |<span data-ttu-id="5b291-193">Получает объект **TypeDescriptor**, соответствующий заданным точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="5b291-193">Gets the **TypeDescriptor** object that corresponds to the given dot notation.</span></span> <br/> |
   

<span data-ttu-id="5b291-194">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-194">**Properties**</span></span>


|<span data-ttu-id="5b291-195">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-195">**Property**</span></span>|<span data-ttu-id="5b291-196">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-196">**Return type**</span></span>|<span data-ttu-id="5b291-197">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-197">**Description**</span></span>|
|:-----|:-----|:-----|
| `Fields { get; }` <br/> |<span data-ttu-id="5b291-198">**FieldCollection**</span><span class="sxs-lookup"><span data-stu-id="5b291-198">**FieldCollection**</span></span> <br/> |<span data-ttu-id="5b291-199">Получает коллекцию всех полей в представлении.</span><span class="sxs-lookup"><span data-stu-id="5b291-199">Gets the collection of fields in the view.</span></span>  <br/> |
| `Name { get; }` <br/> |<span data-ttu-id="5b291-200">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-200">**string**</span></span> <br/> |<span data-ttu-id="5b291-201">Получает имя объекта **View**</span><span class="sxs-lookup"><span data-stu-id="5b291-201">Gets the name of this **View** object</span></span> <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |<span data-ttu-id="5b291-202">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-202">**string**</span></span> <br/> |<span data-ttu-id="5b291-203">Получает имя специальный метод поиска **MethodInstance**, которая связана с этого представления.</span><span class="sxs-lookup"><span data-stu-id="5b291-203">Retrieves the name of the specific finder **MethodInstance** that this view is tied to.</span></span> <br/> |
   

## <a name="lobsystem-method"></a><span data-ttu-id="5b291-204">Метод бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="5b291-204">LobSystem method</span></span>
<span data-ttu-id="5b291-205"><a name="bkmk_LobSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-205"></span></span>


  
    
    

<span data-ttu-id="5b291-206">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-206">**Namespaces**</span></span>


|<span data-ttu-id="5b291-207">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-207">**Managed**</span></span>|<span data-ttu-id="5b291-208">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-208">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-209">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="5b291-209">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="5b291-210">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="5b291-210">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="5b291-211">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-211">**Methods**</span></span>


|<span data-ttu-id="5b291-212">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-212">**Method**</span></span>|<span data-ttu-id="5b291-213">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-213">**Return type**</span></span>|<span data-ttu-id="5b291-214">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-214">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-215">**GetLobSystemInstances()**</span><span class="sxs-lookup"><span data-stu-id="5b291-215">**GetLobSystemInstances()**</span></span> <br/> |<span data-ttu-id="5b291-216">**void**</span><span class="sxs-lookup"><span data-stu-id="5b291-216">**void**</span></span> <br/> |<span data-ttu-id="5b291-217">Предоставляет список экземпляров системы LOB.</span><span class="sxs-lookup"><span data-stu-id="5b291-217">Gives the list of LOB system instances.</span></span>  <br/> |
|<span data-ttu-id="5b291-218">**Name**</span><span class="sxs-lookup"><span data-stu-id="5b291-218">**Name**</span></span> <br/> |<span data-ttu-id="5b291-219">**void**</span><span class="sxs-lookup"><span data-stu-id="5b291-219">**void**</span></span> <br/> |<span data-ttu-id="5b291-220">Получает имя **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="5b291-220">Gets the name of the **LobSystem**.</span></span>  <br/> |
   

<span data-ttu-id="5b291-221">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-221">**Properties**</span></span>


|<span data-ttu-id="5b291-222">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-222">**Property**</span></span>|<span data-ttu-id="5b291-223">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-223">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-224">Нет</span><span class="sxs-lookup"><span data-stu-id="5b291-224">None.</span></span>  <br/> ||
   

## <a name="lobsysteminstance-method"></a><span data-ttu-id="5b291-225">Метод бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="5b291-225">LobSystemInstance method</span></span>
<span data-ttu-id="5b291-226"><a name="bkmk_LobSystemInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-226"></span></span>


  
    
    

<span data-ttu-id="5b291-227">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-227">**Namespaces**</span></span>


|<span data-ttu-id="5b291-228">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-228">**Managed**</span></span>|<span data-ttu-id="5b291-229">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-229">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-230">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="5b291-230">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="5b291-231">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="5b291-231">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="5b291-232">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-232">**Methods**</span></span>


|<span data-ttu-id="5b291-233">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-233">**Method**</span></span>|<span data-ttu-id="5b291-234">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-234">**Return type**</span></span>|<span data-ttu-id="5b291-235">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-235">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-236">Нет.</span><span class="sxs-lookup"><span data-stu-id="5b291-236">None.</span></span>  <br/> |<span data-ttu-id="5b291-237">**void**</span><span class="sxs-lookup"><span data-stu-id="5b291-237">**void**</span></span> <br/> ||
   

<span data-ttu-id="5b291-238">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-238">**Properties**</span></span>


|<span data-ttu-id="5b291-239">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-239">**Property**</span></span>|<span data-ttu-id="5b291-240">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-240">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-241">Нет</span><span class="sxs-lookup"><span data-stu-id="5b291-241">None.</span></span>  <br/> ||
   

## <a name="identifier-method"></a><span data-ttu-id="5b291-242">Метод идентификатор</span><span class="sxs-lookup"><span data-stu-id="5b291-242">Identifier method</span></span>
<span data-ttu-id="5b291-243"><a name="bkmk_Identifier"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-243"></span></span>


  
    
    

<span data-ttu-id="5b291-244">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-244">**Namespaces**</span></span>


|<span data-ttu-id="5b291-245">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-245">**Managed**</span></span>|<span data-ttu-id="5b291-246">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-246">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-247">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="5b291-247">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="5b291-248">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="5b291-248">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="5b291-249">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-249">**Methods**</span></span>


|<span data-ttu-id="5b291-250">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-250">**Method**</span></span>|<span data-ttu-id="5b291-251">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-251">**Return type**</span></span>|<span data-ttu-id="5b291-252">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-252">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-253">**ContainsLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="5b291-253">**ContainsLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="5b291-254">**bool**</span><span class="sxs-lookup"><span data-stu-id="5b291-254">**bool**</span></span> <br/> |<span data-ttu-id="5b291-255">Определяет, содержит ли объект метаданных локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="5b291-255">Determines whether the metadata object contains localized display name.</span></span>  <br/> |
|<span data-ttu-id="5b291-256">**GetDefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="5b291-256">**GetDefaultDisplayName**</span></span> <br/> |<span data-ttu-id="5b291-257">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-257">**string**</span></span> <br/> |<span data-ttu-id="5b291-258">Возвращает отображаемое имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5b291-258">Returns the default display name.</span></span>  <br/> |
|<span data-ttu-id="5b291-259">**GetLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="5b291-259">**GetLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="5b291-260">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-260">**string**</span></span> <br/> |<span data-ttu-id="5b291-261">Возвращает локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="5b291-261">Returns the localized display name.</span></span>  <br/> |
   

<span data-ttu-id="5b291-262">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-262">**Properties**</span></span>


|<span data-ttu-id="5b291-263">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-263">**Property**</span></span>|<span data-ttu-id="5b291-264">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-264">**Return type**</span></span>|<span data-ttu-id="5b291-265">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-265">**Description**</span></span>|
|:-----|:-----|:-----|
| `IdentifierType {get;}` <br/> |<span data-ttu-id="5b291-266">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-266">**string**</span></span> <br/> |<span data-ttu-id="5b291-267">Возвращает тип идентификатора.</span><span class="sxs-lookup"><span data-stu-id="5b291-267">Returns the type of identifier.</span></span>  <br/> |
| `Name {get;}` <br/> |<span data-ttu-id="5b291-268">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-268">**string**</span></span> <br/> |<span data-ttu-id="5b291-269">Получает имя идентификатора.</span><span class="sxs-lookup"><span data-stu-id="5b291-269">Gets the name of the identifier.</span></span>  <br/> |
   

## <a name="identifiercollection-method"></a><span data-ttu-id="5b291-270">Метод IdentifierCollection</span><span class="sxs-lookup"><span data-stu-id="5b291-270">IdentifierCollection method</span></span>
<span data-ttu-id="5b291-271"><a name="bkmk_IdentifierCollection"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-271"></span></span>


  
    
    

<span data-ttu-id="5b291-272">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-272">**Namespaces**</span></span>


|<span data-ttu-id="5b291-273">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-273">**Managed**</span></span>|<span data-ttu-id="5b291-274">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-274">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-275">**Microsoft.BusinessData.MetadataModel.Collections**</span><span class="sxs-lookup"><span data-stu-id="5b291-275">**Microsoft.BusinessData.MetadataModel.Collections**</span></span> <br/> |<span data-ttu-id="5b291-276">**SP. BusinessData.Collections**</span><span class="sxs-lookup"><span data-stu-id="5b291-276">**SP.BusinessData.Collections**</span></span> <br/> |
   

<span data-ttu-id="5b291-277">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-277">**Methods**</span></span>


|<span data-ttu-id="5b291-278">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-278">**Method**</span></span>|<span data-ttu-id="5b291-279">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-279">**Return type**</span></span>|<span data-ttu-id="5b291-280">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-280">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-281">Нет.</span><span class="sxs-lookup"><span data-stu-id="5b291-281">None.</span></span>  <br/> |<span data-ttu-id="5b291-282">**void**</span><span class="sxs-lookup"><span data-stu-id="5b291-282">**void**</span></span> <br/> ||
   

<span data-ttu-id="5b291-283">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-283">**Properties**</span></span>


|<span data-ttu-id="5b291-284">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-284">**Property**</span></span>|<span data-ttu-id="5b291-285">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-285">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-286">Нет</span><span class="sxs-lookup"><span data-stu-id="5b291-286">None.</span></span>  <br/> ||
   

## <a name="identity-method"></a><span data-ttu-id="5b291-287">Метод удостоверений</span><span class="sxs-lookup"><span data-stu-id="5b291-287">Identity method</span></span>
<span data-ttu-id="5b291-288"><a name="bkmk_Identity"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-288"></span></span>


  
    
    

<span data-ttu-id="5b291-289">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-289">**Namespaces**</span></span>


|<span data-ttu-id="5b291-290">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-290">**Managed**</span></span>|<span data-ttu-id="5b291-291">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-291">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-292">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-292">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="5b291-293">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-293">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="5b291-294">**Конструктор**</span><span class="sxs-lookup"><span data-stu-id="5b291-294">**Constructor**</span></span>


|<span data-ttu-id="5b291-295">**Конструктор**</span><span class="sxs-lookup"><span data-stu-id="5b291-295">**Constructor**</span></span>|<span data-ttu-id="5b291-296">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-296">**Description**</span></span>|
|:-----|:-----|
| `public Identity (Object[] identifierValues)` <br/> |<span data-ttu-id="5b291-297">Создает новый экземпляр класса с помощью массив значений идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="5b291-297">Constructs a new instance of the class by using an array of identifier values.</span></span>  <br/> |
   

<span data-ttu-id="5b291-298">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-298">**Methods**</span></span>


|<span data-ttu-id="5b291-299">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-299">**Method**</span></span>|<span data-ttu-id="5b291-300">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-300">**Return type**</span></span>|<span data-ttu-id="5b291-301">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-301">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-302">**Serialize**</span><span class="sxs-lookup"><span data-stu-id="5b291-302">**Serialize**</span></span> <br/> |<span data-ttu-id="5b291-303">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-303">**string**</span></span> <br/> |<span data-ttu-id="5b291-304">Возвращает строковое представление удостоверения.</span><span class="sxs-lookup"><span data-stu-id="5b291-304">Gets a string representation of the identity.</span></span>  <br/> |
   

<span data-ttu-id="5b291-305">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-305">**Properties**</span></span>


|<span data-ttu-id="5b291-306">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-306">**Property**</span></span>|<span data-ttu-id="5b291-307">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-307">**Return type**</span></span>|<span data-ttu-id="5b291-308">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-308">**Description**</span></span>|
|:-----|:-----|:-----|
| `IdentifierCount { get; }` <br/> |<span data-ttu-id="5b291-309">**int**</span><span class="sxs-lookup"><span data-stu-id="5b291-309">**int**</span></span> <br/> |<span data-ttu-id="5b291-310">Возвращает число идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="5b291-310">Returns the number of identifiers.</span></span>  <br/> |
| `IsTemporary { get; }` <br/> |<span data-ttu-id="5b291-311">**bool**</span><span class="sxs-lookup"><span data-stu-id="5b291-311">**bool**</span></span> <br/> |<span data-ttu-id="5b291-312">Проверяет, является ли идентификатор временного.</span><span class="sxs-lookup"><span data-stu-id="5b291-312">Checks whether the identity is temporary.</span></span>  <br/> |
| `this[int identifierIndex] { get; }` <br/> |<span data-ttu-id="5b291-313">**Object**</span><span class="sxs-lookup"><span data-stu-id="5b291-313">**Object**</span></span> <br/> |<span data-ttu-id="5b291-p103">Получает элемент по указанному индексу. CSOM не поддерживает на основе int индексирования. На основе строки доступа к данным реализован для того же.</span><span class="sxs-lookup"><span data-stu-id="5b291-p103">Retrieves the element at the given index. CSOM does not support int-based indexing. String-based accessor implemented for the same.</span></span>  <br/> |
| `TemporaryId { get; }` <br/> |<span data-ttu-id="5b291-317">**Guid**</span><span class="sxs-lookup"><span data-stu-id="5b291-317">**Guid**</span></span> <br/> |<span data-ttu-id="5b291-318">Возвращает временной части удостоверения.</span><span class="sxs-lookup"><span data-stu-id="5b291-318">Returns the temporary part of the identity.</span></span>  <br/> |
   

## <a name="fieldvaluedictionary-method"></a><span data-ttu-id="5b291-319">Метод словаря</span><span class="sxs-lookup"><span data-stu-id="5b291-319">FieldValueDictionary method</span></span>
<span data-ttu-id="5b291-320"><a name="bkmk_FieldValueDictionary"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-320"></span></span>


  
    
    

<span data-ttu-id="5b291-321">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-321">**Namespaces**</span></span>


|<span data-ttu-id="5b291-322">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-322">**Managed**</span></span>|<span data-ttu-id="5b291-323">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-323">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-324">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-324">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="5b291-325">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-325">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="5b291-326">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-326">**Methods**</span></span>


|<span data-ttu-id="5b291-327">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-327">**Method**</span></span>|<span data-ttu-id="5b291-328">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-328">**Return type**</span></span>|<span data-ttu-id="5b291-329">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-329">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-330">**FromXml**</span><span class="sxs-lookup"><span data-stu-id="5b291-330">**FromXml**</span></span> <br/> |<span data-ttu-id="5b291-331">**void**</span><span class="sxs-lookup"><span data-stu-id="5b291-331">**void**</span></span> <br/> |<span data-ttu-id="5b291-332">Задает значения в словаре из указанного XML.</span><span class="sxs-lookup"><span data-stu-id="5b291-332">Sets the values in this dictionary from specified XML.</span></span>  <br/> |
|<span data-ttu-id="5b291-333">**GetCollectionSize**</span><span class="sxs-lookup"><span data-stu-id="5b291-333">**GetCollectionSize**</span></span> <br/> |<span data-ttu-id="5b291-334">целое</span><span class="sxs-lookup"><span data-stu-id="5b291-334">int</span></span>  <br/> |<span data-ttu-id="5b291-335">Возвращает размер семейства сайтов, на который ссылается точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="5b291-335">Returns the size of the collection that the dot notation refers to.</span></span>  <br/> |
|<span data-ttu-id="5b291-336">**ToXml**</span><span class="sxs-lookup"><span data-stu-id="5b291-336">**ToXml**</span></span> <br/> |<span data-ttu-id="5b291-337">string</span><span class="sxs-lookup"><span data-stu-id="5b291-337">string</span></span>  <br/> |<span data-ttu-id="5b291-338">Извлекает значения в формате XML.</span><span class="sxs-lookup"><span data-stu-id="5b291-338">Retrieves the values in XML format.</span></span>  <br/> |
   

<span data-ttu-id="5b291-339">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-339">**Properties**</span></span>


|<span data-ttu-id="5b291-340">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-340">**Property**</span></span>|<span data-ttu-id="5b291-341">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-341">**Description**</span></span>|
|:-----|:-----|
| `Object this[string fieldDotNotation] { get; set; }` <br/> |<span data-ttu-id="5b291-342">Получает или задает значение поля, на который ссылается точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="5b291-342">Gets or sets the value of the field referred to by the dot notation.</span></span>  <br/> |
   

## <a name="entityfieldcollection-method"></a><span data-ttu-id="5b291-343">Метод EntityFieldCollection</span><span class="sxs-lookup"><span data-stu-id="5b291-343">EntityFieldCollection method</span></span>
<span data-ttu-id="5b291-344"><a name="bkmk_EntityFieldCollection"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-344"></span></span>


  
    
    

<span data-ttu-id="5b291-345">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-345">**Namespaces**</span></span>


|<span data-ttu-id="5b291-346">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-346">**Managed**</span></span>|<span data-ttu-id="5b291-347">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-347">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-348">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-348">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="5b291-349">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-349">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="5b291-350">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-350">**Methods**</span></span>


|<span data-ttu-id="5b291-351">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-351">**Method**</span></span>|<span data-ttu-id="5b291-352">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-352">**Return type**</span></span>|<span data-ttu-id="5b291-353">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-353">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-354">Нет.</span><span class="sxs-lookup"><span data-stu-id="5b291-354">None.</span></span>  <br/> |<span data-ttu-id="5b291-355">**void**</span><span class="sxs-lookup"><span data-stu-id="5b291-355">**void**</span></span> <br/> ||
   

<span data-ttu-id="5b291-356">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-356">**Properties**</span></span>


|<span data-ttu-id="5b291-357">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-357">**Property**</span></span>|<span data-ttu-id="5b291-358">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-358">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-359">Нет</span><span class="sxs-lookup"><span data-stu-id="5b291-359">None.</span></span>  <br/> ||
   

## <a name="entityfield-method"></a><span data-ttu-id="5b291-360">Метод EntityField</span><span class="sxs-lookup"><span data-stu-id="5b291-360">EntityField method</span></span>
<span data-ttu-id="5b291-361"><a name="bkmk_Entityfield"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-361"></span></span>


  
    
    

<span data-ttu-id="5b291-362">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-362">**Namespaces**</span></span>


|<span data-ttu-id="5b291-363">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-363">**Managed**</span></span>|<span data-ttu-id="5b291-364">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-364">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-365">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-365">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="5b291-366">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="5b291-366">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="5b291-367">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-367">**Methods**</span></span>


|<span data-ttu-id="5b291-368">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-368">**Method**</span></span>|<span data-ttu-id="5b291-369">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-369">**Return type**</span></span>|<span data-ttu-id="5b291-370">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-370">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-371">Нет</span><span class="sxs-lookup"><span data-stu-id="5b291-371">None.</span></span>  <br/> |<span data-ttu-id="5b291-372">void</span><span class="sxs-lookup"><span data-stu-id="5b291-372">void</span></span>  <br/> ||
   

<span data-ttu-id="5b291-373">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-373">**Properties**</span></span>


|<span data-ttu-id="5b291-374">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-374">**Property**</span></span>|<span data-ttu-id="5b291-375">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-375">**Return type**</span></span>|<span data-ttu-id="5b291-376">**Только чтение**</span><span class="sxs-lookup"><span data-stu-id="5b291-376">**Read Only**</span></span>|<span data-ttu-id="5b291-377">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-377">**Description**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="5b291-378">**ContainsLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="5b291-378">**ContainsLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="5b291-379">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="5b291-379">**Boolean**</span></span> <br/> |<span data-ttu-id="5b291-380">Да</span><span class="sxs-lookup"><span data-stu-id="5b291-380">Yes</span></span>  <br/> |<span data-ttu-id="5b291-381">Определяет, содержит ли поле локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="5b291-381">Determines whether the field contains a localized display name.</span></span>  <br/> |
|<span data-ttu-id="5b291-382">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="5b291-382">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="5b291-383">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-383">**string**</span></span> <br/> |<span data-ttu-id="5b291-384">Да</span><span class="sxs-lookup"><span data-stu-id="5b291-384">Yes</span></span>  <br/> |<span data-ttu-id="5b291-385">Получает отображаемое имя по умолчанию поля.</span><span class="sxs-lookup"><span data-stu-id="5b291-385">Retrieves the default display name of the Field.</span></span>  <br/> |
|<span data-ttu-id="5b291-386">**GetLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="5b291-386">**GetLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="5b291-387">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-387">**string**</span></span> <br/> ||<span data-ttu-id="5b291-388">Получает локализованное отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="5b291-388">Retrieves the localized display name of the Field.</span></span>  <br/> |
|<span data-ttu-id="5b291-389">**Name**</span><span class="sxs-lookup"><span data-stu-id="5b291-389">**Name**</span></span> <br/> |<span data-ttu-id="5b291-390">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-390">**string**</span></span> <br/> |<span data-ttu-id="5b291-391">Да</span><span class="sxs-lookup"><span data-stu-id="5b291-391">Yes</span></span>  <br/> |<span data-ttu-id="5b291-392">Получает имя поля.</span><span class="sxs-lookup"><span data-stu-id="5b291-392">Retrieves the name of the Field.</span></span>  <br/> |
   

## <a name="typedescriptor-class"></a><span data-ttu-id="5b291-393">Класс TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="5b291-393">TypeDescriptor class</span></span>
<span data-ttu-id="5b291-394"><a name="bkmk_TypeDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-394"></span></span>


  
    
    

<span data-ttu-id="5b291-395">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="5b291-395">**Namespaces**</span></span>


|<span data-ttu-id="5b291-396">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="5b291-396">**Managed**</span></span>|<span data-ttu-id="5b291-397">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="5b291-397">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-398">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="5b291-398">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="5b291-399">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="5b291-399">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="5b291-400">**Методы**</span><span class="sxs-lookup"><span data-stu-id="5b291-400">**Methods**</span></span>


|<span data-ttu-id="5b291-401">**Метод**</span><span class="sxs-lookup"><span data-stu-id="5b291-401">**Method**</span></span>|<span data-ttu-id="5b291-402">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-402">**Return type**</span></span>|<span data-ttu-id="5b291-403">**Только чтение**</span><span class="sxs-lookup"><span data-stu-id="5b291-403">**Read Only**</span></span>|<span data-ttu-id="5b291-404">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-404">**Description**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="5b291-405">**ContainsLocalizedDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="5b291-405">**ContainsLocalizedDisplayName()**</span></span> <br/> |<span data-ttu-id="5b291-406">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="5b291-406">**Boolean**</span></span> <br/> |<span data-ttu-id="5b291-407">Да</span><span class="sxs-lookup"><span data-stu-id="5b291-407">Yes</span></span>  <br/> |<span data-ttu-id="5b291-408">Определяет, содержит ли дескриптор типа локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="5b291-408">Determines whether the type descriptor contains a localized display name.</span></span>  <br/> |
|<span data-ttu-id="5b291-409">**GetLocalizedDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="5b291-409">**GetLocalizedDisplayName()**</span></span> <br/> |<span data-ttu-id="5b291-410">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-410">**string**</span></span> <br/> |<span data-ttu-id="5b291-411">Да</span><span class="sxs-lookup"><span data-stu-id="5b291-411">Yes</span></span>  <br/> |<span data-ttu-id="5b291-412">Возвращает локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="5b291-412">Returns the localized display name.</span></span>  <br/> |
|<span data-ttu-id="5b291-413">**GetDefaultDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="5b291-413">**GetDefaultDisplayName()**</span></span> <br/> |<span data-ttu-id="5b291-414">**string**</span><span class="sxs-lookup"><span data-stu-id="5b291-414">**string**</span></span> <br/> ||<span data-ttu-id="5b291-415">Возвращает отображаемое имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5b291-415">Returns the default display name.</span></span>  <br/> |
   

<span data-ttu-id="5b291-416">**Properties**</span><span class="sxs-lookup"><span data-stu-id="5b291-416">**Properties**</span></span>


|<span data-ttu-id="5b291-417">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="5b291-417">**Property**</span></span>|<span data-ttu-id="5b291-418">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="5b291-418">**Return type**</span></span>|<span data-ttu-id="5b291-419">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-419">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="5b291-420">**Name**</span><span class="sxs-lookup"><span data-stu-id="5b291-420">**Name**</span></span> <br/> |<span data-ttu-id="5b291-421">string</span><span class="sxs-lookup"><span data-stu-id="5b291-421">string</span></span>  <br/> |<span data-ttu-id="5b291-422">Получает имя поля.</span><span class="sxs-lookup"><span data-stu-id="5b291-422">Retrieves the name of the Field.</span></span>  <br/> |
|<span data-ttu-id="5b291-423">**Имя типа**</span><span class="sxs-lookup"><span data-stu-id="5b291-423">**TypeName**</span></span> <br/> |<span data-ttu-id="5b291-424">string</span><span class="sxs-lookup"><span data-stu-id="5b291-424">string</span></span>  <br/> |<span data-ttu-id="5b291-425">Получает имя типа данных, представленного в этом дескриптором типа.</span><span class="sxs-lookup"><span data-stu-id="5b291-425">Retrieves the name of the data type represented by this type descriptor.</span></span>  <br/> |
|<span data-ttu-id="5b291-426">**IsReadOnly**</span><span class="sxs-lookup"><span data-stu-id="5b291-426">**IsReadOnly**</span></span> <br/> |<span data-ttu-id="5b291-427">Логический</span><span class="sxs-lookup"><span data-stu-id="5b291-427">Boolean</span></span>  <br/> |<span data-ttu-id="5b291-428">Определяет, является ли этот тип дескриптора структуру данных только для чтения.</span><span class="sxs-lookup"><span data-stu-id="5b291-428">Determines whether this type descriptor represents a read-only data structure.</span></span>  <br/> |
|<span data-ttu-id="5b291-429">**ContainsReadOnly**</span><span class="sxs-lookup"><span data-stu-id="5b291-429">**ContainsReadOnly**</span></span> <br/> |<span data-ttu-id="5b291-430">Логический</span><span class="sxs-lookup"><span data-stu-id="5b291-430">Boolean</span></span>  <br/> |<span data-ttu-id="5b291-431">Определяет, представляют ли этот дескриптор типа или одного из его дочерние элементы структуры данных только для чтения.</span><span class="sxs-lookup"><span data-stu-id="5b291-431">Determines whether this type descriptor or one of its children represent a read-only data structure.</span></span>  <br/> |
|<span data-ttu-id="5b291-432">**IsCollection**</span><span class="sxs-lookup"><span data-stu-id="5b291-432">**IsCollection**</span></span> <br/> |<span data-ttu-id="5b291-433">Логический</span><span class="sxs-lookup"><span data-stu-id="5b291-433">Boolean</span></span>  <br/> |<span data-ttu-id="5b291-434">Определяет, представляет ли описанного типа структуры данных семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="5b291-434">Determines whether the described type represents a collection data structure.</span></span>  <br/> |
   

## <a name="interfaces"></a><span data-ttu-id="5b291-435">Интерфейсы</span><span class="sxs-lookup"><span data-stu-id="5b291-435">Interfaces</span></span>
<span data-ttu-id="5b291-436"><a name="bkmk_Interfaces"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-436"></span></span>

<span data-ttu-id="5b291-437">Пространство имен является **Microsoft.BusinessData.MetadataModel**.</span><span class="sxs-lookup"><span data-stu-id="5b291-437">The namespace is **Microsoft.BusinessData.MetadataModel**.</span></span>
  
    
    


|<span data-ttu-id="5b291-438">**Интерфейс**</span><span class="sxs-lookup"><span data-stu-id="5b291-438">**Interface**</span></span>|<span data-ttu-id="5b291-439">**Описание**</span><span class="sxs-lookup"><span data-stu-id="5b291-439">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="5b291-440">**IMetadataCatalog**</span><span class="sxs-lookup"><span data-stu-id="5b291-440">**IMetadataCatalog**</span></span> <br/> |<span data-ttu-id="5b291-p104">Точка входа для объектной модели BDC. Используйте **DatabaseBasedMetadataCatalog** на сервере.</span><span class="sxs-lookup"><span data-stu-id="5b291-p104">The entry point into the BDC object model. Use the **DatabaseBasedMetadataCatalog** on the server. </span></span><br/> |
|<span data-ttu-id="5b291-443">**ILobSystem**</span><span class="sxs-lookup"><span data-stu-id="5b291-443">**ILobSystem**</span></span> <br/> |<span data-ttu-id="5b291-444">Содержит сведения о внешней системе.</span><span class="sxs-lookup"><span data-stu-id="5b291-444">Contains the details about an external system.</span></span>  <br/> |
|<span data-ttu-id="5b291-445">**IEntity**</span><span class="sxs-lookup"><span data-stu-id="5b291-445">**IEntity**</span></span> <br/> |<span data-ttu-id="5b291-446">Внешний тип контента в хранилище метаданных службы подключения к бизнес-данным.</span><span class="sxs-lookup"><span data-stu-id="5b291-446">An external content type in the BDC Metadata Store.</span></span>  <br/> |
|<span data-ttu-id="5b291-447">**IMethod**</span><span class="sxs-lookup"><span data-stu-id="5b291-447">**IMethod**</span></span> <br/> |<span data-ttu-id="5b291-448">Операция, которую можно выполнить с внешним типом контента.</span><span class="sxs-lookup"><span data-stu-id="5b291-448">An operation that can be performed on the external content type.</span></span>  <br/> |
|<span data-ttu-id="5b291-449">**IEntityInstance**</span><span class="sxs-lookup"><span data-stu-id="5b291-449">**IEntityInstance**</span></span> <br/> |<span data-ttu-id="5b291-450">Экземпляр сущности (также известной как внешнего элемента) представляет собой отдельный элемент, возвращенный из внешней системы в BDC.</span><span class="sxs-lookup"><span data-stu-id="5b291-450">An entity instance (also known as external item) is a single item returned from an external system in BDC.</span></span>  <br/> <span data-ttu-id="5b291-p105">Интерфейс **IEntityInstance** выделяет используемых источников данных и изолирует клиентов от необходимости сведения схемы написания кода конкретного приложения; позволяет им получить доступ к всем бизнес-данным в одном упрощенный способ. С помощью интерфейса **IEntityInstance**, можно работать со строкой данных из базы данных в точно так же, так как работа с сложную структуру .NET Framework, возвращаемый веб-службой. </span><span class="sxs-lookup"><span data-stu-id="5b291-p105">The **IEntityInstance** interface abstracts the underlying data sources and insulates the clients from having to learn application-specific coding paradigms; it enables them to access all business data in a single, simplified way. By using the **IEntityInstance** interface, you can work with a row of data from a database in just the same way as working with a complex .NET Framework structure returned by a web service. </span></span><br/> <span data-ttu-id="5b291-p106">Экземпляр сущности в BDC имеет специальной семантики, подключенного к нему. Например имеет возможность знать, какие поля или поля строки, представляющие идентификатор для экземпляра сущности и позволяет звонить методы, такие как **GetAssociated**, **GetIdentifierValues**и **Execute**на этот экземпляр сущности. </span><span class="sxs-lookup"><span data-stu-id="5b291-p106">An entity instance in BDC has special semantics attached to it. For example, it has the ability to know which field or fields in the row represent the identifier for the entity instance, and it enables you to call methods, such as **GetAssociated**, **GetIdentifierValues**, and **Execute**, on that entity instance.  </span></span><br/> |
|<span data-ttu-id="5b291-455">**IEntityInstanceEnumerator**</span><span class="sxs-lookup"><span data-stu-id="5b291-455">**IEntityInstanceEnumerator**</span></span> <br/> |<span data-ttu-id="5b291-p107">Перечислителя может использоваться для чтения данных в коллекции внешние элементы, но не может использоваться для изменения коллекции. **IEntityInstanceEnumerator** поддерживает потоковая передача и поэтому очень полезен при возврате серверного приложения больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="5b291-p107">Enumerators can be used to read the data in the external items collection, but they cannot be used to modify the underlying collection. **IEntityInstanceEnumerator** supports streaming and is therefore very useful when the back-end application returns large amounts of data. </span></span><br/> |
   

## <a name="client-object-model-faq"></a><span data-ttu-id="5b291-458">Вопросы и ответы по объектной модели клиента</span><span class="sxs-lookup"><span data-stu-id="5b291-458">Client Object model FAQ</span></span>
<span data-ttu-id="5b291-459"><a name="bkmk_ClientObjectModelFAQ"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-459"></span></span>


- <span data-ttu-id="5b291-460">**Does <Method> тег нужно включить в запрос CAML при запросе внешнего списка**</span><span class="sxs-lookup"><span data-stu-id="5b291-460">**Does the <Method> tag need to be included in a CAML query when querying an external list**</span></span>
    
    <span data-ttu-id="5b291-461">Нет.</span><span class="sxs-lookup"><span data-stu-id="5b291-461">No.</span></span> 
    
  
- <span data-ttu-id="5b291-462">**Есть ли необходимость всех полей во внешний список с помощью запроса CAML?**</span><span class="sxs-lookup"><span data-stu-id="5b291-462">**Do all fields in the external list need to be specified in the CAML query?**</span></span>
    
    <span data-ttu-id="5b291-463">Использование тега текст ViewXML в модели BDC, разработчик можно указать только те поля, которые необходимы и CSOM API-интерфейсы для списков будет возвращать только те поля.</span><span class="sxs-lookup"><span data-stu-id="5b291-463">Using the ViewXML tag in the BDC model, the developer can specify only those fields that are required and the CSOM APIs for Lists will return only those fields.</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="5b291-464">См. также</span><span class="sxs-lookup"><span data-stu-id="5b291-464">See also</span></span>
<span data-ttu-id="5b291-465"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="5b291-465"></span></span>


-  [<span data-ttu-id="5b291-466">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-466">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="5b291-467">Справка по API клиента .NET для SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-467">.NET client API reference for SharePoint Online</span></span>](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="5b291-468">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-468">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="5b291-469">Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-469">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="5b291-470">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-470">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="5b291-471">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b291-471">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
