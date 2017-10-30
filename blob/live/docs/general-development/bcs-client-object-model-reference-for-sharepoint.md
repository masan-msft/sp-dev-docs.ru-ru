---
title: "BCS клиента Справочник по объектной модели для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fe7d12a3-6ea9-47f9-b69e-f66da9e661dc
ms.openlocfilehash: 648dd7c17e0ac4c7869d93df88ae155dcfde7b84
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="bcs-client-object-model-reference-for-sharepoint"></a><span data-ttu-id="7ce3a-102">BCS клиента Справочник по объектной модели для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-102">BCS client object model reference for SharePoint</span></span>

  
    
    
![Ссылки и библиотеки класса](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="7ce3a-104">Сведения об объектах, доступных для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, предоставляемые Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="7ce3a-104">Learn about the objects that are available for creating client-side scripts using the SharePoint client object model to access external data exposed by Business Connectivity Services (BCS).</span></span>
<span data-ttu-id="7ce3a-105">Доступны следующие объекты для создания клиентских скриптов с помощью клиентской объектной модели SharePoint для доступа к внешним данным, взаимодействующий с Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="7ce3a-105">The following objects are available for creating client-side scripts using the SharePoint client object model to access external data that is exposed by Business Connectivity Services (BCS).</span></span> <span data-ttu-id="7ce3a-106">BCS объектной модели, компоненты, предоставляемые клиентскую объектную модель, находятся в библиотеке Microsoft.SharePoint.Client.dll.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-106">The BCS object model components that are exposed to the client object model are located in Microsoft.SharePoint.Client.dll.</span></span>
  
    
    


## <a name="entity-object"></a><span data-ttu-id="7ce3a-107">Объект сущности</span><span class="sxs-lookup"><span data-stu-id="7ce3a-107">Entity object</span></span>
<span data-ttu-id="7ce3a-108"><a name="bkmk_Entity"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-108"></span></span>

<span data-ttu-id="7ce3a-p102">Объект **Entity** по сути представляет таблицу в базе данных. Методы и свойства, представленные здесь Показать объекты, которые можно управлять с помощью клиентской библиотеки кода. Каждый из этих вызовов сопоставляет непосредственно звонка server объектной модели. Тем не менее они могут вызываться отключением клиента, такие как и в веб-браузере с помощью JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-p102">The **Entity** object essentially represents a table in a database. The methods and properties presented here show the objects that can be manipulated through the use of the client code library. Each of these calls maps directly to a server object model call. However, they are callable by a detached client, such as in a web browser using JavaScript.</span></span>
  
    
    

<span data-ttu-id="7ce3a-113">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-113">**Methods**</span></span>


|<span data-ttu-id="7ce3a-114">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-114">**Methods**</span></span>|<span data-ttu-id="7ce3a-115">**Подпись метода**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-115">**Method signature**</span></span>|<span data-ttu-id="7ce3a-116">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-116">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-117">**Create**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-117">**Create**</span></span> <br/> | `Identity Create(FieldValueDictionary fieldValues, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="7ce3a-118">**FindSpecificDefault**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-118">**FindSpecificDefault**</span></span> <br/> | `EntityInstance FindSpecificDefault(Identity identity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="7ce3a-119">**FindspecificByBdcIDDefault**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-119">**FindspecificByBdcIDDefault**</span></span> <br/> | `EntityInstance FindSpecific(Identity identity, string specificFinderName, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="7ce3a-120">**FindSpecificByBdcID**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-120">**FindSpecificByBdcID**</span></span> <br/> | `EntityInstance FindSpecificByBdcIDDefault(string BdcIdentity, LobSystemInstance lobSystemInstanceName)` <br/> ||
|<span data-ttu-id="7ce3a-121">**GetCreatorView**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-121">**GetCreatorView**</span></span> <br/> | `EntityInstance FindSpecificByBdcID(string BdcIdentity, string specificFinderName,LobSystemInstance LobSystemInstanceName)` <br/> ||
|<span data-ttu-id="7ce3a-122">**GetDefaultSpecificFinderView**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-122">**GetDefaultSpecificFinderView**</span></span> <br/> | `View GetCreatorView(string methodInstanceName)` <br/> ||
|<span data-ttu-id="7ce3a-123">**GetSpecificFinderView_Client**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-123">**GetSpecificFinderView_Client**</span></span> <br/> | `View GetDefaultSpecificFinderView()` <br/> ||
|<span data-ttu-id="7ce3a-124">**GetUpdaterView_Client**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-124">**GetUpdaterView_Client**</span></span> <br/> | `View GetSpecificFinderView_Client( string specificFinderName)` <br/> ||
|<span data-ttu-id="7ce3a-125">**GetIdentifiers**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-125">**GetIdentifiers**</span></span> <br/> | `View GetUpdaterView_Client(string updaterName)` <br/> ||
|<span data-ttu-id="7ce3a-126">**GetIdentifiers()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-126">**GetIdentifiers()**</span></span> <br/> |||
   

<span data-ttu-id="7ce3a-127">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-127">**Properties**</span></span>


|<span data-ttu-id="7ce3a-128">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-128">**Property**</span></span>|<span data-ttu-id="7ce3a-129">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-129">**Description**</span></span>|
|:-----|:-----|
| `long EstimatedInstanceCount { get; }` <br/> |<span data-ttu-id="7ce3a-130">Получает число ожидаемых внешние элементы этого внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-130">Gets the number of expected external items of this external content type.</span></span>  <br/> |
| `string Name { get; }` <br/> |<span data-ttu-id="7ce3a-131">Возвращает имя объекта метаданных.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-131">Gets the name of the metadata object.</span></span>  <br/> |
| `string Namespace { get; }` <br/> |<span data-ttu-id="7ce3a-132">Возвращает пространство имен класса данных.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-132">Gets the namespace of the given data class.</span></span>  <br/> |
| `int GetIdentifierCount()` <br/> ||
   

## <a name="entityinstance-method"></a><span data-ttu-id="7ce3a-133">Метод экземпляра сущности</span><span class="sxs-lookup"><span data-stu-id="7ce3a-133">EntityInstance method</span></span>
<span data-ttu-id="7ce3a-134"><a name="bkmk_EntityInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-134"></span></span>


<span data-ttu-id="7ce3a-135">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-135">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-136">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-136">**Managed**</span></span>|<span data-ttu-id="7ce3a-137">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-137">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-138">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-138">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="7ce3a-139">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-139">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-140">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-140">**Methods**</span></span>


|<span data-ttu-id="7ce3a-141">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-141">**Method**</span></span>|<span data-ttu-id="7ce3a-142">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-142">**Return type**</span></span>|<span data-ttu-id="7ce3a-143">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-143">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-144">**Delete**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-144">**Delete**</span></span> <br/> |<span data-ttu-id="7ce3a-145">void</span><span class="sxs-lookup"><span data-stu-id="7ce3a-145">void</span></span>  <br/> |<span data-ttu-id="7ce3a-146">Удаление внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-146">Deletes the External Item.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-147">**FromXml**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-147">**FromXml**</span></span> <br/> |<span data-ttu-id="7ce3a-148">void</span><span class="sxs-lookup"><span data-stu-id="7ce3a-148">void</span></span>  <br/> |<span data-ttu-id="7ce3a-149">Задает значения в словаре из указанного XML.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-149">Sets the values in this dictionary from specified XML.</span></span>  <br/> <span data-ttu-id="7ce3a-150">**Подпись метода**          `FromXml(string xml)`</span><span class="sxs-lookup"><span data-stu-id="7ce3a-150">**Method signature**          `FromXml(string xml)`</span></span> <br/> |
|<span data-ttu-id="7ce3a-151">**GetIdentity**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-151">**GetIdentity**</span></span> <br/> |<span data-ttu-id="7ce3a-152">Identity</span><span class="sxs-lookup"><span data-stu-id="7ce3a-152">Identity</span></span>  <br/> |<span data-ttu-id="7ce3a-153">Получает идентификатор этого внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-153">Gets the identity of this External Item.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-154">**Delete**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-154">**Delete**</span></span> <br/> |<span data-ttu-id="7ce3a-155">void</span><span class="sxs-lookup"><span data-stu-id="7ce3a-155">void</span></span>  <br/> |<span data-ttu-id="7ce3a-156">Удаление внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-156">Deletes the External Item.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-157">**ToXml**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-157">**ToXml**</span></span> <br/> |<span data-ttu-id="7ce3a-158">string</span><span class="sxs-lookup"><span data-stu-id="7ce3a-158">string</span></span>  <br/> |<span data-ttu-id="7ce3a-159">Извлекает значения в формате XML.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-159">Retrieves the values in XML format.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-160">**Update**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-160">**Update**</span></span> <br/> |<span data-ttu-id="7ce3a-161">void</span><span class="sxs-lookup"><span data-stu-id="7ce3a-161">void</span></span>  <br/> |<span data-ttu-id="7ce3a-162">Отправляет данные изменения, внесенные внешнего элемента.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-162">Submits the changes made to the External Item.</span></span>  <br/> |
   

  
    
    

<span data-ttu-id="7ce3a-163">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-163">**Properties**</span></span>


|<span data-ttu-id="7ce3a-164">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-164">**Property**</span></span>|<span data-ttu-id="7ce3a-165">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-165">**Return type**</span></span>|<span data-ttu-id="7ce3a-166">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-166">**Description**</span></span>|
|:-----|:-----|:-----|
| `this[string fieldDotNotation] { get; set; }` <br/> |<span data-ttu-id="7ce3a-167">Объект</span><span class="sxs-lookup"><span data-stu-id="7ce3a-167">Object</span></span>  <br/> |<span data-ttu-id="7ce3a-168">Получает или задает значение поля, на который ссылается точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-168">Gets or sets the value of the field referred to by the dot notation.</span></span>  <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |<span data-ttu-id="7ce3a-169">строка</span><span class="sxs-lookup"><span data-stu-id="7ce3a-169">string</span></span>  <br/> ||
   

## <a name="entityview-method"></a><span data-ttu-id="7ce3a-170">Метод EntityView</span><span class="sxs-lookup"><span data-stu-id="7ce3a-170">EntityView method</span></span>
<span data-ttu-id="7ce3a-171"><a name="bkmk_entityview"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-171"></span></span>

<span data-ttu-id="7ce3a-172">Определяет настраиваемое представление данных **сущности**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-172">Specifies a customized view of the **Entity** data</span></span>
  
    
    

<span data-ttu-id="7ce3a-173">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-173">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-174">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-174">**Managed**</span></span>|<span data-ttu-id="7ce3a-175">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-175">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-176">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-176">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="7ce3a-177">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-177">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-178">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-178">**Methods**</span></span>


|<span data-ttu-id="7ce3a-179">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-179">**Method**</span></span>|<span data-ttu-id="7ce3a-180">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-180">**Return type**</span></span>|<span data-ttu-id="7ce3a-181">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-181">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-182">**GetDefaultValues_Client()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-182">**GetDefaultValues_Client()**</span></span> <br/> |<span data-ttu-id="7ce3a-183">**Словаря**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-183">**FieldValueDictionary**</span></span> <br/> |<span data-ttu-id="7ce3a-184">Получает словарь значение поля, который содержит значения по умолчанию для этого представления.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-184">Gets a field value dictionary that contains the default values for this view.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-185">**GetXmlSchema()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-185">**GetXmlSchema()**</span></span> <br/> |<span data-ttu-id="7ce3a-186">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-186">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-187">Возвращает схему XML для представления.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-187">Gets the XML Schema of the view.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-188">**GetType (строка fieldDotNotation)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-188">**GetType(string fieldDotNotation)**</span></span> <br/> |<span data-ttu-id="7ce3a-189">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-189">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-190">Получает тип указанного поля.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-190">Gets the type of the specified field.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-191">**GetType (строка fieldDotNotation)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-191">**GetType(string fieldDotNotation)**</span></span> <br/> |<span data-ttu-id="7ce3a-192">**Дескриптор типа**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-192">**TypeDescriptor**</span></span> <br/> |<span data-ttu-id="7ce3a-193">Получает объект **TypeDescriptor**, соответствующий заданным точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-193">Gets the **TypeDescriptor** object that corresponds to the given dot notation.</span></span> <br/> |
   

<span data-ttu-id="7ce3a-194">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-194">**Properties**</span></span>


|<span data-ttu-id="7ce3a-195">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-195">**Property**</span></span>|<span data-ttu-id="7ce3a-196">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-196">**Return type**</span></span>|<span data-ttu-id="7ce3a-197">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-197">**Description**</span></span>|
|:-----|:-----|:-----|
| `Fields { get; }` <br/> |<span data-ttu-id="7ce3a-198">**FieldCollection**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-198">**FieldCollection**</span></span> <br/> |<span data-ttu-id="7ce3a-199">Получает коллекцию всех полей в представлении.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-199">Gets the collection of fields in the view.</span></span>  <br/> |
| `Name { get; }` <br/> |<span data-ttu-id="7ce3a-200">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-200">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-201">Получает имя объекта **View**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-201">Gets the name of this **View** object</span></span> <br/> |
| `RelatedSpecificFinderName { get; }` <br/> |<span data-ttu-id="7ce3a-202">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-202">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-203">Получает имя специальный метод поиска **MethodInstance**, которая связана с этого представления.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-203">Retrieves the name of the specific finder **MethodInstance** that this view is tied to.</span></span> <br/> |
   

## <a name="lobsystem-method"></a><span data-ttu-id="7ce3a-204">Метод бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="7ce3a-204">LobSystem method</span></span>
<span data-ttu-id="7ce3a-205"><a name="bkmk_LobSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-205"></span></span>


  
    
    

<span data-ttu-id="7ce3a-206">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-206">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-207">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-207">**Managed**</span></span>|<span data-ttu-id="7ce3a-208">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-208">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-209">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-209">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="7ce3a-210">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-210">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-211">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-211">**Methods**</span></span>


|<span data-ttu-id="7ce3a-212">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-212">**Method**</span></span>|<span data-ttu-id="7ce3a-213">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-213">**Return type**</span></span>|<span data-ttu-id="7ce3a-214">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-214">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-215">**GetLobSystemInstances()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-215">**GetLobSystemInstances()**</span></span> <br/> |<span data-ttu-id="7ce3a-216">**void**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-216">**void**</span></span> <br/> |<span data-ttu-id="7ce3a-217">Предоставляет список экземпляров системы LOB.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-217">Gives the list of LOB system instances.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-218">**Name**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-218">**Name**</span></span> <br/> |<span data-ttu-id="7ce3a-219">**void**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-219">**void**</span></span> <br/> |<span data-ttu-id="7ce3a-220">Получает имя **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-220">Gets the name of the **LobSystem**.</span></span>  <br/> |
   

<span data-ttu-id="7ce3a-221">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-221">**Properties**</span></span>


|<span data-ttu-id="7ce3a-222">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-222">**Property**</span></span>|<span data-ttu-id="7ce3a-223">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-223">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-224">Нет</span><span class="sxs-lookup"><span data-stu-id="7ce3a-224">None.</span></span>  <br/> ||
   

## <a name="lobsysteminstance-method"></a><span data-ttu-id="7ce3a-225">Метод бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="7ce3a-225">LobSystemInstance method</span></span>
<span data-ttu-id="7ce3a-226"><a name="bkmk_LobSystemInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-226"></span></span>


  
    
    

<span data-ttu-id="7ce3a-227">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-227">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-228">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-228">**Managed**</span></span>|<span data-ttu-id="7ce3a-229">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-229">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-230">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-230">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="7ce3a-231">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-231">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-232">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-232">**Methods**</span></span>


|<span data-ttu-id="7ce3a-233">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-233">**Method**</span></span>|<span data-ttu-id="7ce3a-234">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-234">**Return type**</span></span>|<span data-ttu-id="7ce3a-235">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-235">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-236">Нет.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-236">None.</span></span>  <br/> |<span data-ttu-id="7ce3a-237">**void**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-237">**void**</span></span> <br/> ||
   

<span data-ttu-id="7ce3a-238">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-238">**Properties**</span></span>


|<span data-ttu-id="7ce3a-239">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-239">**Property**</span></span>|<span data-ttu-id="7ce3a-240">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-240">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-241">Нет</span><span class="sxs-lookup"><span data-stu-id="7ce3a-241">None.</span></span>  <br/> ||
   

## <a name="identifier-method"></a><span data-ttu-id="7ce3a-242">Метод идентификатор</span><span class="sxs-lookup"><span data-stu-id="7ce3a-242">Identifier method</span></span>
<span data-ttu-id="7ce3a-243"><a name="bkmk_Identifier"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-243"></span></span>


  
    
    

<span data-ttu-id="7ce3a-244">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-244">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-245">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-245">**Managed**</span></span>|<span data-ttu-id="7ce3a-246">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-246">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-247">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-247">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="7ce3a-248">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-248">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-249">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-249">**Methods**</span></span>


|<span data-ttu-id="7ce3a-250">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-250">**Method**</span></span>|<span data-ttu-id="7ce3a-251">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-251">**Return type**</span></span>|<span data-ttu-id="7ce3a-252">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-252">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-253">**ContainsLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-253">**ContainsLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="7ce3a-254">**bool**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-254">**bool**</span></span> <br/> |<span data-ttu-id="7ce3a-255">Определяет, содержит ли объект метаданных локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-255">Determines whether the metadata object contains localized display name.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-256">**GetDefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-256">**GetDefaultDisplayName**</span></span> <br/> |<span data-ttu-id="7ce3a-257">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-257">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-258">Возвращает отображаемое имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-258">Returns the default display name.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-259">**GetLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-259">**GetLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="7ce3a-260">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-260">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-261">Возвращает локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-261">Returns the localized display name.</span></span>  <br/> |
   

<span data-ttu-id="7ce3a-262">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-262">**Properties**</span></span>


|<span data-ttu-id="7ce3a-263">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-263">**Property**</span></span>|<span data-ttu-id="7ce3a-264">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-264">**Return type**</span></span>|<span data-ttu-id="7ce3a-265">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-265">**Description**</span></span>|
|:-----|:-----|:-----|
| `IdentifierType {get;}` <br/> |<span data-ttu-id="7ce3a-266">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-266">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-267">Возвращает тип идентификатора.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-267">Returns the type of identifier.</span></span>  <br/> |
| `Name {get;}` <br/> |<span data-ttu-id="7ce3a-268">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-268">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-269">Получает имя идентификатора.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-269">Gets the name of the identifier.</span></span>  <br/> |
   

## <a name="identifiercollection-method"></a><span data-ttu-id="7ce3a-270">Метод IdentifierCollection</span><span class="sxs-lookup"><span data-stu-id="7ce3a-270">IdentifierCollection method</span></span>
<span data-ttu-id="7ce3a-271"><a name="bkmk_IdentifierCollection"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-271"></span></span>


  
    
    

<span data-ttu-id="7ce3a-272">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-272">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-273">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-273">**Managed**</span></span>|<span data-ttu-id="7ce3a-274">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-274">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-275">**Microsoft.BusinessData.MetadataModel.Collections**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-275">**Microsoft.BusinessData.MetadataModel.Collections**</span></span> <br/> |<span data-ttu-id="7ce3a-276">**SP. BusinessData.Collections**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-276">**SP.BusinessData.Collections**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-277">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-277">**Methods**</span></span>


|<span data-ttu-id="7ce3a-278">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-278">**Method**</span></span>|<span data-ttu-id="7ce3a-279">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-279">**Return type**</span></span>|<span data-ttu-id="7ce3a-280">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-280">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-281">Нет.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-281">None.</span></span>  <br/> |<span data-ttu-id="7ce3a-282">**void**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-282">**void**</span></span> <br/> ||
   

<span data-ttu-id="7ce3a-283">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-283">**Properties**</span></span>


|<span data-ttu-id="7ce3a-284">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-284">**Property**</span></span>|<span data-ttu-id="7ce3a-285">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-285">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-286">Нет</span><span class="sxs-lookup"><span data-stu-id="7ce3a-286">None.</span></span>  <br/> ||
   

## <a name="identity-method"></a><span data-ttu-id="7ce3a-287">Метод удостоверений</span><span class="sxs-lookup"><span data-stu-id="7ce3a-287">Identity method</span></span>
<span data-ttu-id="7ce3a-288"><a name="bkmk_Identity"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-288"></span></span>


  
    
    

<span data-ttu-id="7ce3a-289">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-289">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-290">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-290">**Managed**</span></span>|<span data-ttu-id="7ce3a-291">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-291">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-292">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-292">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="7ce3a-293">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-293">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-294">**Конструктор**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-294">**Constructor**</span></span>


|<span data-ttu-id="7ce3a-295">**Конструктор**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-295">**Constructor**</span></span>|<span data-ttu-id="7ce3a-296">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-296">**Description**</span></span>|
|:-----|:-----|
| `public Identity (Object[] identifierValues)` <br/> |<span data-ttu-id="7ce3a-297">Создает новый экземпляр класса с помощью массив значений идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-297">Constructs a new instance of the class by using an array of identifier values.</span></span>  <br/> |
   

<span data-ttu-id="7ce3a-298">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-298">**Methods**</span></span>


|<span data-ttu-id="7ce3a-299">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-299">**Method**</span></span>|<span data-ttu-id="7ce3a-300">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-300">**Return type**</span></span>|<span data-ttu-id="7ce3a-301">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-301">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-302">**Serialize**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-302">**Serialize**</span></span> <br/> |<span data-ttu-id="7ce3a-303">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-303">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-304">Возвращает строковое представление удостоверения.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-304">Gets a string representation of the identity.</span></span>  <br/> |
   

<span data-ttu-id="7ce3a-305">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-305">**Properties**</span></span>


|<span data-ttu-id="7ce3a-306">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-306">**Property**</span></span>|<span data-ttu-id="7ce3a-307">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-307">**Return type**</span></span>|<span data-ttu-id="7ce3a-308">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-308">**Description**</span></span>|
|:-----|:-----|:-----|
| `IdentifierCount { get; }` <br/> |<span data-ttu-id="7ce3a-309">**int**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-309">**int**</span></span> <br/> |<span data-ttu-id="7ce3a-310">Возвращает число идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-310">Returns the number of identifiers.</span></span>  <br/> |
| `IsTemporary { get; }` <br/> |<span data-ttu-id="7ce3a-311">**bool**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-311">**bool**</span></span> <br/> |<span data-ttu-id="7ce3a-312">Проверяет, является ли идентификатор временного.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-312">Checks whether the identity is temporary.</span></span>  <br/> |
| `this[int identifierIndex] { get; }` <br/> |<span data-ttu-id="7ce3a-313">**Object**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-313">**Object**</span></span> <br/> |<span data-ttu-id="7ce3a-p103">Получает элемент по указанному индексу. CSOM не поддерживает на основе int индексирования. На основе строки доступа к данным реализован для того же.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-p103">Retrieves the element at the given index. CSOM does not support int-based indexing. String-based accessor implemented for the same.</span></span>  <br/> |
| `TemporaryId { get; }` <br/> |<span data-ttu-id="7ce3a-317">**Guid**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-317">**Guid**</span></span> <br/> |<span data-ttu-id="7ce3a-318">Возвращает временной части удостоверения.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-318">Returns the temporary part of the identity.</span></span>  <br/> |
   

## <a name="fieldvaluedictionary-method"></a><span data-ttu-id="7ce3a-319">Метод словаря</span><span class="sxs-lookup"><span data-stu-id="7ce3a-319">FieldValueDictionary method</span></span>
<span data-ttu-id="7ce3a-320"><a name="bkmk_FieldValueDictionary"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-320"></span></span>


  
    
    

<span data-ttu-id="7ce3a-321">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-321">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-322">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-322">**Managed**</span></span>|<span data-ttu-id="7ce3a-323">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-323">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-324">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-324">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="7ce3a-325">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-325">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-326">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-326">**Methods**</span></span>


|<span data-ttu-id="7ce3a-327">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-327">**Method**</span></span>|<span data-ttu-id="7ce3a-328">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-328">**Return type**</span></span>|<span data-ttu-id="7ce3a-329">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-329">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-330">**FromXml**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-330">**FromXml**</span></span> <br/> |<span data-ttu-id="7ce3a-331">**void**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-331">**void**</span></span> <br/> |<span data-ttu-id="7ce3a-332">Задает значения в словаре из указанного XML.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-332">Sets the values in this dictionary from specified XML.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-333">**GetCollectionSize**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-333">**GetCollectionSize**</span></span> <br/> |<span data-ttu-id="7ce3a-334">целое</span><span class="sxs-lookup"><span data-stu-id="7ce3a-334">int</span></span>  <br/> |<span data-ttu-id="7ce3a-335">Возвращает размер семейства сайтов, на который ссылается точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-335">Returns the size of the collection that the dot notation refers to.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-336">**ToXml**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-336">**ToXml**</span></span> <br/> |<span data-ttu-id="7ce3a-337">string</span><span class="sxs-lookup"><span data-stu-id="7ce3a-337">string</span></span>  <br/> |<span data-ttu-id="7ce3a-338">Извлекает значения в формате XML.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-338">Retrieves the values in XML format.</span></span>  <br/> |
   

<span data-ttu-id="7ce3a-339">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-339">**Properties**</span></span>


|<span data-ttu-id="7ce3a-340">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-340">**Property**</span></span>|<span data-ttu-id="7ce3a-341">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-341">**Description**</span></span>|
|:-----|:-----|
| `Object this[string fieldDotNotation] { get; set; }` <br/> |<span data-ttu-id="7ce3a-342">Получает или задает значение поля, на который ссылается точечную нотацию.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-342">Gets or sets the value of the field referred to by the dot notation.</span></span>  <br/> |
   

## <a name="entityfieldcollection-method"></a><span data-ttu-id="7ce3a-343">Метод EntityFieldCollection</span><span class="sxs-lookup"><span data-stu-id="7ce3a-343">EntityFieldCollection method</span></span>
<span data-ttu-id="7ce3a-344"><a name="bkmk_EntityFieldCollection"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-344"></span></span>


  
    
    

<span data-ttu-id="7ce3a-345">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-345">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-346">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-346">**Managed**</span></span>|<span data-ttu-id="7ce3a-347">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-347">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-348">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-348">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="7ce3a-349">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-349">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-350">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-350">**Methods**</span></span>


|<span data-ttu-id="7ce3a-351">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-351">**Method**</span></span>|<span data-ttu-id="7ce3a-352">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-352">**Return type**</span></span>|<span data-ttu-id="7ce3a-353">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-353">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-354">Нет.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-354">None.</span></span>  <br/> |<span data-ttu-id="7ce3a-355">**void**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-355">**void**</span></span> <br/> ||
   

<span data-ttu-id="7ce3a-356">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-356">**Properties**</span></span>


|<span data-ttu-id="7ce3a-357">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-357">**Property**</span></span>|<span data-ttu-id="7ce3a-358">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-358">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-359">Нет</span><span class="sxs-lookup"><span data-stu-id="7ce3a-359">None.</span></span>  <br/> ||
   

## <a name="entityfield-method"></a><span data-ttu-id="7ce3a-360">Метод EntityField</span><span class="sxs-lookup"><span data-stu-id="7ce3a-360">EntityField method</span></span>
<span data-ttu-id="7ce3a-361"><a name="bkmk_Entityfield"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-361"></span></span>


  
    
    

<span data-ttu-id="7ce3a-362">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-362">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-363">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-363">**Managed**</span></span>|<span data-ttu-id="7ce3a-364">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-364">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-365">**Microsoft.BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-365">**Microsoft.BusinessData.Runtime**</span></span> <br/> |<span data-ttu-id="7ce3a-366">**SP. BusinessData.Runtime**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-366">**SP.BusinessData.Runtime**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-367">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-367">**Methods**</span></span>


|<span data-ttu-id="7ce3a-368">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-368">**Method**</span></span>|<span data-ttu-id="7ce3a-369">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-369">**Return type**</span></span>|<span data-ttu-id="7ce3a-370">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-370">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-371">Нет</span><span class="sxs-lookup"><span data-stu-id="7ce3a-371">None.</span></span>  <br/> |<span data-ttu-id="7ce3a-372">void</span><span class="sxs-lookup"><span data-stu-id="7ce3a-372">void</span></span>  <br/> ||
   

<span data-ttu-id="7ce3a-373">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-373">**Properties**</span></span>


|<span data-ttu-id="7ce3a-374">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-374">**Property**</span></span>|<span data-ttu-id="7ce3a-375">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-375">**Return type**</span></span>|<span data-ttu-id="7ce3a-376">**Только чтение**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-376">**Read Only**</span></span>|<span data-ttu-id="7ce3a-377">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-377">**Description**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-378">**ContainsLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-378">**ContainsLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="7ce3a-379">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-379">**Boolean**</span></span> <br/> |<span data-ttu-id="7ce3a-380">Да</span><span class="sxs-lookup"><span data-stu-id="7ce3a-380">Yes</span></span>  <br/> |<span data-ttu-id="7ce3a-381">Определяет, содержит ли поле локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-381">Determines whether the field contains a localized display name.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-382">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-382">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="7ce3a-383">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-383">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-384">Да</span><span class="sxs-lookup"><span data-stu-id="7ce3a-384">Yes</span></span>  <br/> |<span data-ttu-id="7ce3a-385">Получает отображаемое имя по умолчанию поля.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-385">Retrieves the default display name of the Field.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-386">**GetLocalizedDisplayName**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-386">**GetLocalizedDisplayName**</span></span> <br/> |<span data-ttu-id="7ce3a-387">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-387">**string**</span></span> <br/> ||<span data-ttu-id="7ce3a-388">Получает локализованное отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-388">Retrieves the localized display name of the Field.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-389">**Name**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-389">**Name**</span></span> <br/> |<span data-ttu-id="7ce3a-390">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-390">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-391">Да</span><span class="sxs-lookup"><span data-stu-id="7ce3a-391">Yes</span></span>  <br/> |<span data-ttu-id="7ce3a-392">Получает имя поля.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-392">Retrieves the name of the Field.</span></span>  <br/> |
   

## <a name="typedescriptor-class"></a><span data-ttu-id="7ce3a-393">Класс TypeDescriptor</span><span class="sxs-lookup"><span data-stu-id="7ce3a-393">TypeDescriptor class</span></span>
<span data-ttu-id="7ce3a-394"><a name="bkmk_TypeDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-394"></span></span>


  
    
    

<span data-ttu-id="7ce3a-395">**Пространства имен**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-395">**Namespaces**</span></span>


|<span data-ttu-id="7ce3a-396">**Managed (Управляемая)**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-396">**Managed**</span></span>|<span data-ttu-id="7ce3a-397">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-397">**JavaScript**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-398">**Microsoft.BusinessData.MetadataModel**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-398">**Microsoft.BusinessData.MetadataModel**</span></span> <br/> |<span data-ttu-id="7ce3a-399">**SP. BusinessData**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-399">**SP.BusinessData**</span></span> <br/> |
   

<span data-ttu-id="7ce3a-400">**Методы**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-400">**Methods**</span></span>


|<span data-ttu-id="7ce3a-401">**Метод**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-401">**Method**</span></span>|<span data-ttu-id="7ce3a-402">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-402">**Return type**</span></span>|<span data-ttu-id="7ce3a-403">**Только чтение**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-403">**Read Only**</span></span>|<span data-ttu-id="7ce3a-404">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-404">**Description**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-405">**ContainsLocalizedDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-405">**ContainsLocalizedDisplayName()**</span></span> <br/> |<span data-ttu-id="7ce3a-406">**Boolean**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-406">**Boolean**</span></span> <br/> |<span data-ttu-id="7ce3a-407">Да</span><span class="sxs-lookup"><span data-stu-id="7ce3a-407">Yes</span></span>  <br/> |<span data-ttu-id="7ce3a-408">Определяет, содержит ли дескриптор типа локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-408">Determines whether the type descriptor contains a localized display name.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-409">**GetLocalizedDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-409">**GetLocalizedDisplayName()**</span></span> <br/> |<span data-ttu-id="7ce3a-410">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-410">**string**</span></span> <br/> |<span data-ttu-id="7ce3a-411">Да</span><span class="sxs-lookup"><span data-stu-id="7ce3a-411">Yes</span></span>  <br/> |<span data-ttu-id="7ce3a-412">Возвращает локализованное отображаемое имя.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-412">Returns the localized display name.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-413">**GetDefaultDisplayName()**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-413">**GetDefaultDisplayName()**</span></span> <br/> |<span data-ttu-id="7ce3a-414">**string**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-414">**string**</span></span> <br/> ||<span data-ttu-id="7ce3a-415">Возвращает отображаемое имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-415">Returns the default display name.</span></span>  <br/> |
   

<span data-ttu-id="7ce3a-416">**Properties**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-416">**Properties**</span></span>


|<span data-ttu-id="7ce3a-417">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-417">**Property**</span></span>|<span data-ttu-id="7ce3a-418">**Возвращаемый тип**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-418">**Return type**</span></span>|<span data-ttu-id="7ce3a-419">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-419">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="7ce3a-420">**Name**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-420">**Name**</span></span> <br/> |<span data-ttu-id="7ce3a-421">string</span><span class="sxs-lookup"><span data-stu-id="7ce3a-421">string</span></span>  <br/> |<span data-ttu-id="7ce3a-422">Получает имя поля.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-422">Retrieves the name of the Field.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-423">**Имя типа**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-423">**TypeName**</span></span> <br/> |<span data-ttu-id="7ce3a-424">string</span><span class="sxs-lookup"><span data-stu-id="7ce3a-424">string</span></span>  <br/> |<span data-ttu-id="7ce3a-425">Получает имя типа данных, представленного в этом дескриптором типа.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-425">Retrieves the name of the data type represented by this type descriptor.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-426">**IsReadOnly**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-426">**IsReadOnly**</span></span> <br/> |<span data-ttu-id="7ce3a-427">Логический</span><span class="sxs-lookup"><span data-stu-id="7ce3a-427">Boolean</span></span>  <br/> |<span data-ttu-id="7ce3a-428">Определяет, является ли этот тип дескриптора структуру данных только для чтения.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-428">Determines whether this type descriptor represents a read-only data structure.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-429">**ContainsReadOnly**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-429">**ContainsReadOnly**</span></span> <br/> |<span data-ttu-id="7ce3a-430">Логический</span><span class="sxs-lookup"><span data-stu-id="7ce3a-430">Boolean</span></span>  <br/> |<span data-ttu-id="7ce3a-431">Определяет, представляют ли этот дескриптор типа или одного из его дочерние элементы структуры данных только для чтения.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-431">Determines whether this type descriptor or one of its children represent a read-only data structure.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-432">**IsCollection**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-432">**IsCollection**</span></span> <br/> |<span data-ttu-id="7ce3a-433">Логический</span><span class="sxs-lookup"><span data-stu-id="7ce3a-433">Boolean</span></span>  <br/> |<span data-ttu-id="7ce3a-434">Определяет, представляет ли описанного типа структуры данных семейства сайтов.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-434">Determines whether the described type represents a collection data structure.</span></span>  <br/> |
   

## <a name="interfaces"></a><span data-ttu-id="7ce3a-435">Интерфейсы</span><span class="sxs-lookup"><span data-stu-id="7ce3a-435">Interfaces</span></span>
<span data-ttu-id="7ce3a-436"><a name="bkmk_Interfaces"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-436"></span></span>

<span data-ttu-id="7ce3a-437">Пространство имен является **Microsoft.BusinessData.MetadataModel**.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-437">The namespace is **Microsoft.BusinessData.MetadataModel**.</span></span>
  
    
    


|<span data-ttu-id="7ce3a-438">**Интерфейс**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-438">**Interface**</span></span>|<span data-ttu-id="7ce3a-439">**Описание**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-439">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="7ce3a-440">**IMetadataCatalog**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-440">**IMetadataCatalog**</span></span> <br/> |<span data-ttu-id="7ce3a-p104">Точка входа для объектной модели BDC. Используйте **DatabaseBasedMetadataCatalog** на сервере.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-p104">The entry point into the BDC object model. Use the **DatabaseBasedMetadataCatalog** on the server. </span></span><br/> |
|<span data-ttu-id="7ce3a-443">**ILobSystem**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-443">**ILobSystem**</span></span> <br/> |<span data-ttu-id="7ce3a-444">Содержит сведения о внешней системе.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-444">Contains the details about an external system.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-445">**IEntity**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-445">**IEntity**</span></span> <br/> |<span data-ttu-id="7ce3a-446">Внешний тип контента в хранилище метаданных службы подключения к бизнес-данным.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-446">An external content type in the BDC Metadata Store.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-447">**IMethod**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-447">**IMethod**</span></span> <br/> |<span data-ttu-id="7ce3a-448">Операция, которую можно выполнить с внешним типом контента.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-448">An operation that can be performed on the external content type.</span></span>  <br/> |
|<span data-ttu-id="7ce3a-449">**IEntityInstance**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-449">**IEntityInstance**</span></span> <br/> |<span data-ttu-id="7ce3a-450">Экземпляр сущности (также известной как внешнего элемента) представляет собой отдельный элемент, возвращенный из внешней системы в BDC.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-450">An entity instance (also known as external item) is a single item returned from an external system in BDC.</span></span>  <br/> <span data-ttu-id="7ce3a-p105">Интерфейс **IEntityInstance** выделяет используемых источников данных и изолирует клиентов от необходимости сведения схемы написания кода конкретного приложения; позволяет им получить доступ к всем бизнес-данным в одном упрощенный способ. С помощью интерфейса **IEntityInstance**, можно работать со строкой данных из базы данных в точно так же, так как работа с сложную структуру .NET Framework, возвращаемый веб-службой. </span><span class="sxs-lookup"><span data-stu-id="7ce3a-p105">The **IEntityInstance** interface abstracts the underlying data sources and insulates the clients from having to learn application-specific coding paradigms; it enables them to access all business data in a single, simplified way. By using the **IEntityInstance** interface, you can work with a row of data from a database in just the same way as working with a complex .NET Framework structure returned by a web service. </span></span><br/> <span data-ttu-id="7ce3a-p106">Экземпляр сущности в BDC имеет специальной семантики, подключенного к нему. Например имеет возможность знать, какие поля или поля строки, представляющие идентификатор для экземпляра сущности и позволяет звонить методы, такие как **GetAssociated**, **GetIdentifierValues**и **Execute**на этот экземпляр сущности. </span><span class="sxs-lookup"><span data-stu-id="7ce3a-p106">An entity instance in BDC has special semantics attached to it. For example, it has the ability to know which field or fields in the row represent the identifier for the entity instance, and it enables you to call methods, such as **GetAssociated**, **GetIdentifierValues**, and **Execute**, on that entity instance.  </span></span><br/> |
|<span data-ttu-id="7ce3a-455">**IEntityInstanceEnumerator**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-455">**IEntityInstanceEnumerator**</span></span> <br/> |<span data-ttu-id="7ce3a-p107">Перечислителя может использоваться для чтения данных в коллекции внешние элементы, но не может использоваться для изменения коллекции. **IEntityInstanceEnumerator** поддерживает потоковая передача и поэтому очень полезен при возврате серверного приложения больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-p107">Enumerators can be used to read the data in the external items collection, but they cannot be used to modify the underlying collection. **IEntityInstanceEnumerator** supports streaming and is therefore very useful when the back-end application returns large amounts of data. </span></span><br/> |
   

## <a name="client-object-model-faq"></a><span data-ttu-id="7ce3a-458">Вопросы и ответы по объектной модели клиента</span><span class="sxs-lookup"><span data-stu-id="7ce3a-458">Client Object model FAQ</span></span>
<span data-ttu-id="7ce3a-459"><a name="bkmk_ClientObjectModelFAQ"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-459"></span></span>


- <span data-ttu-id="7ce3a-460">**Does <Method> тег нужно включить в запрос CAML при запросе внешнего списка**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-460">**Does the <Method> tag need to be included in a CAML query when querying an external list**</span></span>
    
    <span data-ttu-id="7ce3a-461">Нет.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-461">No.</span></span> 
    
  
- <span data-ttu-id="7ce3a-462">**Есть ли необходимость всех полей во внешний список с помощью запроса CAML?**</span><span class="sxs-lookup"><span data-stu-id="7ce3a-462">**Do all fields in the external list need to be specified in the CAML query?**</span></span>
    
    <span data-ttu-id="7ce3a-463">Использование тега текст ViewXML в модели BDC, разработчик можно указать только те поля, которые необходимы и CSOM API-интерфейсы для списков будет возвращать только те поля.</span><span class="sxs-lookup"><span data-stu-id="7ce3a-463">Using the ViewXML tag in the BDC model, the developer can specify only those fields that are required and the CSOM APIs for Lists will return only those fields.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="7ce3a-464">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7ce3a-464">Additional resources</span></span>
<span data-ttu-id="7ce3a-465"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="7ce3a-465"></span></span>


-  [<span data-ttu-id="7ce3a-466">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-466">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
-  [<span data-ttu-id="7ce3a-467">Справка по API клиента .NET для SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-467">.NET client API reference for SharePoint Online</span></span>](http://msdn.microsoft.com/library/88e5e1b9-eab2-4f3b-a3f2-75c96b86f1f4%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="7ce3a-468">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-468">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7ce3a-469">Как: используйте клиентская библиотека кода для доступа к внешним данным в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-469">How to: Use the client code library to access external data in SharePoint</span></span>](how-to-use-the-client-code-library-to-access-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7ce3a-470">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-470">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="7ce3a-471">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="7ce3a-471">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
