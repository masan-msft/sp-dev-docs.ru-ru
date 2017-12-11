---
title: "Справочник по схеме модели BDC для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 979a5ffc-f033-4e72-b2d1-11d8cb1b294a
ms.openlocfilehash: dd78f6a347894eff60149df672d251cfa4c26bd7
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="bdc-model-schema-reference-for-sharepoint"></a><span data-ttu-id="d5526-102">Справочник по схеме модели BDC для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-102">BDC model schema reference for SharePoint</span></span>
<span data-ttu-id="d5526-103">Содержит справочную документацию по схеме модели BDC (BDCMetadata.xsd), который можно использовать для создания внешних типов контента в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d5526-103">Contains reference documentation for the BDC model schema (BDCMetadata.xsd), which you can use to create external content types in SharePoint.</span></span> 
 [<span data-ttu-id="d5526-104">BDCMetadata.xsd</span><span class="sxs-lookup"><span data-stu-id="d5526-104">BDCMetadata.xsd</span></span>](http://schemas.microsoft.com/windows/2007/BusinessDataCatalog)
  
    
    


## <a name="accesscontrolentry-element"></a><span data-ttu-id="d5526-105">Элемент AccessControlEntry</span><span class="sxs-lookup"><span data-stu-id="d5526-105">AccessControlEntry element</span></span>
<span data-ttu-id="d5526-106"><a name="bkmk_AccessControlEntry"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-106"></span></span>

<span data-ttu-id="d5526-107">Содержит запись управления доступом (ACE), которая определяет права доступа для родительского элемента.</span><span class="sxs-lookup"><span data-stu-id="d5526-107">Contains an access control entry (ACE) that specifies access rights for the parent element.</span></span>
  
    
    
<span data-ttu-id="d5526-108">В статье  [Обзор системы безопасности служб Business Connectivity Services](http://technet.microsoft.com/en-us/library/ee661734%28office.14%29.aspx) приведены дополнительные сведения о Business Connectivity Services и системе безопасности.</span><span class="sxs-lookup"><span data-stu-id="d5526-108">See  [Business Connectivity Services security overview](http://technet.microsoft.com/en-us/library/ee661734%28office.14%29.aspx) to learn more about the Business Connectivity Services and security.</span></span>
  
    
    
 <span data-ttu-id="d5526-109">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-109">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-110">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-110">**Schema:** BDCMetadata</span></span>
  
    
    



```XML

<AccessControlEntry Principal = "String"> </AccessControlEntry>
```

<span data-ttu-id="d5526-111">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-111">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-112">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-112">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-113">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-113">**Attribute**</span></span>|<span data-ttu-id="d5526-114">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-114">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-115">Principal</span><span class="sxs-lookup"><span data-stu-id="d5526-115">Principal</span></span>  <br/> |<span data-ttu-id="d5526-116">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-116">Required.</span></span>  <br/> <span data-ttu-id="d5526-117">Имя участника безопасности, содержащего эту запись управления доступом.</span><span class="sxs-lookup"><span data-stu-id="d5526-117">The name of the security principal that has this ACE.</span></span>  <br/> <span data-ttu-id="d5526-118">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-118">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="d5526-119">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-119">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-120">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-120">**Element**</span></span>|<span data-ttu-id="d5526-121">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-121">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-122">Элемент Right в элементе AccessControlEntry (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-122">Right Element in AccessControlEntry (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a2e4bd6c-2306-b657-7290-cc9c9b262911%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-123">Элемент **Right**, который задает разрешения, доступные для участника безопасности.</span><span class="sxs-lookup"><span data-stu-id="d5526-123">A **Right** element that specifies the permissions available to the security principal.</span></span> <br/> |
   
 <span data-ttu-id="d5526-124">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-124">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-125">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-125">**Element**</span></span>|<span data-ttu-id="d5526-126">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-127">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-127">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-128">Список управления доступом (ACL), содержащий эту запись управления доступом.</span><span class="sxs-lookup"><span data-stu-id="d5526-128">The access control list (ACL) that contains this ACE.</span></span>  <br/> |
   

## <a name="accesscontrollist-element"></a><span data-ttu-id="d5526-129">Элемент AccessControlList</span><span class="sxs-lookup"><span data-stu-id="d5526-129">AccessControlList element</span></span>
<span data-ttu-id="d5526-130"><a name="bkmk_AccessControlList"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-130"></span></span>

<span data-ttu-id="d5526-131">Определяет список управления доступом (ACL) для родительского элемента.</span><span class="sxs-lookup"><span data-stu-id="d5526-131">Specifies an access control list (ACL) for the parent element.</span></span>
  
    
    
 <span data-ttu-id="d5526-132">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-132">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-133">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-133">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<AccessControlList></AccessControlList>
```

<span data-ttu-id="d5526-134">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-134">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-135">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-135">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-136">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-136">None</span></span>
  
    
    
 <span data-ttu-id="d5526-137">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-137">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-138">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-138">**Element**</span></span>|<span data-ttu-id="d5526-139">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-139">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-140">Элемент AccessControlEntry в AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-140">AccessControlEntry Element in AccessControlList (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-141">Элемент управления доступом (ACE).</span><span class="sxs-lookup"><span data-stu-id="d5526-141">An access control entry (ACE).</span></span>  <br/> |
   
 <span data-ttu-id="d5526-142">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-142">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-143">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-143">**Element**</span></span>|<span data-ttu-id="d5526-144">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-144">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-145">Элемент Model (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-145">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-146">Модель, которая содержит внешние типы контента в бизнес-приложение.</span><span class="sxs-lookup"><span data-stu-id="d5526-146">A model that contains external content types in a business application.</span></span>  <br/> |
| [<span data-ttu-id="d5526-147">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-147">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-148">Элементы LobSystem, которые содержатся в модели.</span><span class="sxs-lookup"><span data-stu-id="d5526-148">The LobSystems contained inside the model.</span></span>  <br/> |
| [<span data-ttu-id="d5526-149">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-149">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-150">Внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-150">An external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-151">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-151">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-152">Метод внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-152">A method of an external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-153">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-153">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-154">Связь.</span><span class="sxs-lookup"><span data-stu-id="d5526-154">An association.</span></span>  <br/> |
| [<span data-ttu-id="d5526-155">Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-155">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-156">Экземпляр метода внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-156">A method instance of an external content type.</span></span>  <br/> |
   

## <a name="action-element"></a><span data-ttu-id="d5526-157">Элемент Action</span><span class="sxs-lookup"><span data-stu-id="d5526-157">Action element</span></span>
<span data-ttu-id="d5526-158"><a name="bkmk_Action"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-158"></span></span>

<span data-ttu-id="d5526-159">Указывает действие, поддерживаемых внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-159">Specifies an action supported by an external content type.</span></span>
  
    
    
 <span data-ttu-id="d5526-160">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-160">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-161">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-161">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="d5526-162">Действия устранить разрыв между SharePoint и Office 2013 и внешняя система пользовательского интерфейса, предоставляя ссылку на внешнюю систему.</span><span class="sxs-lookup"><span data-stu-id="d5526-162">Actions bridge the gap between SharePoint and Office 2013 and an external system's user interface by providing a link back to the external system.</span></span> 
  
    
    
<span data-ttu-id="d5526-p102">По умолчанию Служба подключения к бизнес-данным (BDC) предоставляет действий, таких как **View Item**, **Edit Item**и **Delete Item** после модели эти операции в модели BDC. Помимо этих действий по умолчанию можно создать действия для других функций, которые необходимо присоединить к внешним типом контента. Например, можно использовать действия для выполнения простых действий, таких как отправка сообщения электронной почты для клиента из внешнего типа контента клиента или открытие клиента домашней страницы в браузере.</span><span class="sxs-lookup"><span data-stu-id="d5526-p102">By default, the Business Data Connectivity (BDC) service provides actions such as **View Item**, **Edit Item**, and **Delete Item** after you model these operations in the BDC model. In addition to these default actions, you can create actions for other functionality you want to attach to your external content type. For example, you can use actions to perform simple actions, such as sending email messages to a customer from the Customer external content type or opening a customer's home page in a browser.</span></span>
  
    
    
<span data-ttu-id="d5526-p103">Действия, передаются с внешним типом контента. То есть, после определения действия для внешнего типа контента, то действие отображается везде отображать этот внешний тип контента, в внешнего списка или веб-часть бизнес данных или в столбец внешних данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-p103">Actions travel with an external content type. That is, after you define an action for an external content type, the action appears everywhere you display that external content type—whether in an external list or Business Data Web Part or in an External Data column.</span></span> 
  
    
    



```XML
<Action Position = "Integer" IsOpenedInNewWindow = "Boolean" Url = "String" ImageUrl = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Action>
```

<span data-ttu-id="d5526-168">В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-168">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-169">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-169">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-170">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-170">**Attribute**</span></span>|<span data-ttu-id="d5526-171">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-171">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-172">**Position**</span><span class="sxs-lookup"><span data-stu-id="d5526-172">**Position**</span></span> <br/> |<span data-ttu-id="d5526-173">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-173">Required.</span></span>  <br/> <span data-ttu-id="d5526-174">Предлагаемые положение это действие среди других действий этот внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-174">The suggested position of this action among the other actions of this external content type.</span></span>  <br/> <span data-ttu-id="d5526-175">Тип атрибута: **Integer**</span><span class="sxs-lookup"><span data-stu-id="d5526-175">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="d5526-176">**IsOpenedInNewWindow**</span><span class="sxs-lookup"><span data-stu-id="d5526-176">**IsOpenedInNewWindow**</span></span> <br/> |<span data-ttu-id="d5526-177">Необязательный.</span><span class="sxs-lookup"><span data-stu-id="d5526-177">Optional.</span></span>  <br/> <span data-ttu-id="d5526-178">Указывает ли результаты выполнения действия в новом окне интерфейса пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5526-178">Specifies whether the results of executing an action are presented in a new user interface window.</span></span>  <br/> <span data-ttu-id="d5526-179">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-179">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-180">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-180">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-181">**Url**</span><span class="sxs-lookup"><span data-stu-id="d5526-181">**Url**</span></span> <br/> |<span data-ttu-id="d5526-182">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-182">Required.</span></span>  <br/> <span data-ttu-id="d5526-p104">URL-адрес для перехода при вызове действия. Строка URL-адреса  это строка формата .NET Framework. Каждого описателя формата (например, {0}) соответствует параметру **Action**.</span><span class="sxs-lookup"><span data-stu-id="d5526-p104">The URL to go to when the action is invoked. The URL string is a .NET Framework format string. Each format specifier (for example, {0}) corresponds to an **Action** parameter. </span></span><br/> <span data-ttu-id="d5526-186">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-186">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-187">**ImageUrl**</span><span class="sxs-lookup"><span data-stu-id="d5526-187">**ImageUrl**</span></span> <br/> |<span data-ttu-id="d5526-188">Необязательный.</span><span class="sxs-lookup"><span data-stu-id="d5526-188">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p105">Абсолютный или относительный путь для изображения значка для действия. Изображение значка должен быть 16 x 16 пикселей.</span><span class="sxs-lookup"><span data-stu-id="d5526-p105">The absolute or relative path to the icon image for the action. The icon image should be 16 x 16 pixels.  </span></span><br/> <span data-ttu-id="d5526-191">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-191">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-192">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-192">**Name**</span></span> <br/> |<span data-ttu-id="d5526-193">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-193">Required.</span></span>  <br/> <span data-ttu-id="d5526-194">Имя этого действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-194">The name of this action.</span></span>  <br/> <span data-ttu-id="d5526-195">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-195">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-196">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="d5526-196">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="d5526-197">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-197">Optional.</span></span>  <br/> <span data-ttu-id="d5526-198">Отображаемое имя по умолчанию для этого действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-198">The default display name for this action.</span></span>  <br/> <span data-ttu-id="d5526-199">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-199">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-200">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="d5526-200">**IsCached**</span></span> <br/> |<span data-ttu-id="d5526-201">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-201">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p106">Указывает, используется ли это действие часто. Это используется клиентская среда BDC для кэширования этого действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-p106">Specifies whether this action is used frequently. This is used by the BDC client runtime to cache this action.  </span></span><br/> <span data-ttu-id="d5526-204">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-204">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-205">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-205">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-206">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-206">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-207">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-207">**Element**</span></span>|<span data-ttu-id="d5526-208">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-208">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-209">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-209">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-210">Локализованные имена действие.</span><span class="sxs-lookup"><span data-stu-id="d5526-210">The localized names of the action.</span></span>  <br/> |
| [<span data-ttu-id="d5526-211">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-211">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-212">Свойства действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-212">The properties of the action.</span></span>  <br/> |
| [<span data-ttu-id="d5526-213">Элемент ActionParameters в элементе Action (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-213">ActionParameters Element in Action (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-214">Параметры действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-214">The parameters of the action.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-215">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-215">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-216">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-216">**Element**</span></span>|<span data-ttu-id="d5526-217">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-217">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-218">Элемент Actions в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-218">Actions Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-219">Список действий для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-219">The list of actions of an external content type.</span></span>  <br/> |
   

## <a name="actionparameter-element"></a><span data-ttu-id="d5526-220">Элемент ActionParameter</span><span class="sxs-lookup"><span data-stu-id="d5526-220">ActionParameter element</span></span>
<span data-ttu-id="d5526-221"><a name="bkmk_ActionParameter"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-221"></span></span>

<span data-ttu-id="d5526-p107">Задает параметры действия на основе URL-адреса. Определяет способ параметризации URL-адреса действия с данными, связанными с **EntityInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-p107">Specifies the parameters of a URL-based action. It defines how to parameterize the URL of an action with **EntityInstance**-specific data.</span></span>
  
    
    
 <span data-ttu-id="d5526-224">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-224">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-225">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-225">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="d5526-226">Атрибут URL-адреса действия на основе URL-адреса может принимать параметры с помощью элемента **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="d5526-226">The URL attribute of a URL-based action can receive parameters by using the **ActionParameter** element.</span></span>
  
    
    

> <span data-ttu-id="d5526-227">**Важно:**
> **ActionParameters** может представлять значения идентификатора, а также значений, которые соответствуют **дескрипторами типов** в **SpecificFinder** **сущности**.</span><span class="sxs-lookup"><span data-stu-id="d5526-227">**Important:**
**ActionParameters** can either represent identifier values, or values that correspond to **TypeDescriptors** in a **SpecificFinder** of the **Entity**.</span></span> <span data-ttu-id="d5526-228">**ActionParameter** представляет значение идентификатора при наличии свойство **IdOrdinal** .</span><span class="sxs-lookup"><span data-stu-id="d5526-228">The **ActionParameter** represents an identifier value when the **IdOrdinal** property is present.</span></span> <span data-ttu-id="d5526-229">Значение свойства указывает индекс идентификатор, значение которого представляет этот **ActionParameter** .</span><span class="sxs-lookup"><span data-stu-id="d5526-229">The value of the property specifies the index of the identifier whose value this **ActionParameter** represents.</span></span> <span data-ttu-id="d5526-230">Если свойство **IdOrdinal** не указан, **ActionParameter** представляет **дескриптор типа**, а атрибут **Name** указывает, представленное какие дескриптор типа.</span><span class="sxs-lookup"><span data-stu-id="d5526-230">If the **IdOrdinal** property is not specified, the **ActionParameter** represents a **TypeDescriptor**, and the **Name** attribute specifies which type descriptor is being represented.</span></span> <span data-ttu-id="d5526-231">**Имя** атрибута указано как **Временный путь**.</span><span class="sxs-lookup"><span data-stu-id="d5526-231">The **Name** attribute is specified as a **Dotted Path**.</span></span> 
  
    
    

<span data-ttu-id="d5526-232">Элемент **ActionParameter** принимает следующее свойство.</span><span class="sxs-lookup"><span data-stu-id="d5526-232">The **ActionParameter** element accepts the following property.</span></span>
  
    
    

> <span data-ttu-id="d5526-233">**Важные:** В свойствах учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="d5526-233">**Important:** Properties are case-sensitive.</span></span> 
  
    
    


<span data-ttu-id="d5526-234">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="d5526-234">**Properties**</span></span>


|<span data-ttu-id="d5526-235">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="d5526-235">**Property**</span></span>|<span data-ttu-id="d5526-236">**Тип**</span><span class="sxs-lookup"><span data-stu-id="d5526-236">**Type**</span></span>|<span data-ttu-id="d5526-237">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-237">**Description**</span></span>|<span data-ttu-id="d5526-238">**Обязательный атрибут.**</span><span class="sxs-lookup"><span data-stu-id="d5526-238">**Required.**</span></span>|<span data-ttu-id="d5526-239">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="d5526-239">**Default Value**</span></span>|<span data-ttu-id="d5526-240">**Ограничения/Приемлемые значения**</span><span class="sxs-lookup"><span data-stu-id="d5526-240">**Limits/Accepted Values**</span></span>|
|:-----|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d5526-241">**IdOrdinal**</span><span class="sxs-lookup"><span data-stu-id="d5526-241">**IdOrdinal**</span></span> <br/> |<span data-ttu-id="d5526-242">**System.Int32**</span><span class="sxs-lookup"><span data-stu-id="d5526-242">**System.Int32**</span></span> <br/> |<span data-ttu-id="d5526-243">Указывает, представляет ли **ActionParameter** идентификатор вместо поля.</span><span class="sxs-lookup"><span data-stu-id="d5526-243">Specifies if the **ActionParameter** represents an identifier instead of a field.</span></span> <br/> |<span data-ttu-id="d5526-244">Необязательный</span><span class="sxs-lookup"><span data-stu-id="d5526-244">Optional</span></span>  <br/> |||
   



```XML
<ActionParameter Index = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </ActionParameter>
```

<span data-ttu-id="d5526-245">В следующих разделах приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-245">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-246">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-246">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-247">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-247">**Attribute**</span></span>|<span data-ttu-id="d5526-248">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-248">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-249">**Index**</span><span class="sxs-lookup"><span data-stu-id="d5526-249">**Index**</span></span> <br/> |<span data-ttu-id="d5526-250">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-250">Required.</span></span>  <br/> <span data-ttu-id="d5526-251">Порядковый атрибут, который определяет позицию этого параметра **ActionParameter** среди других параметров **ActionParameters** в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="d5526-251">An ordinal attribute that specifies the position of this **ActionParameter** among other **ActionParameters** in the URL.</span></span> <br/> <span data-ttu-id="d5526-252">Тип атрибута: **Integer**</span><span class="sxs-lookup"><span data-stu-id="d5526-252">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="d5526-253">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-253">**Name**</span></span> <br/> |<span data-ttu-id="d5526-254">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-254">Required.</span></span>  <br/> <span data-ttu-id="d5526-255">Имя **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="d5526-255">The name of the **ActionParameter**.</span></span>  <br/> <span data-ttu-id="d5526-256">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-256">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-257">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="d5526-257">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="d5526-258">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-258">Optional.</span></span>  <br/> <span data-ttu-id="d5526-259">Отображаемое по умолчанию имя параметра **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="d5526-259">The default display name for the **ActionParameter**.</span></span>  <br/> <span data-ttu-id="d5526-260">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-260">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-261">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="d5526-261">**IsCached**</span></span> <br/> |<span data-ttu-id="d5526-262">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-262">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p109">Задает частоту использования этого параметра **ActionParameter**. Этот атрибут используется клиентской средой выполнения подключения к бизнес-данным для кэширования данного **Action**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p109">Specifies whether this **ActionParameter** is used frequently. This attribute is used by the BDC client runtime to cache this **Action**.  </span></span><br/> <span data-ttu-id="d5526-265">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-265">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-266">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-266">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-267">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-267">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-268">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-268">**Element**</span></span>|<span data-ttu-id="d5526-269">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-269">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-270">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-270">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-271">Локализованное имя параметра **ActionParameter** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d5526-271">The localized display names for the **ActionParameter**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-272">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-272">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-273">Свойства **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="d5526-273">The properties of the **ActionParameter**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-274">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-274">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-275">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-275">**Element**</span></span>|<span data-ttu-id="d5526-276">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-276">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-277">Элемент ActionParameters в элементе Action (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-277">ActionParameters Element in Action (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/e14df901-621c-1851-db78-e99fd3cf31ae%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-278">Элемент **ActionParameters**, содержащий этот **ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="d5526-278">The **ActionParameters** element that contains this **ActionParameter**.</span></span>  <br/> |
   

## <a name="actionparameters-element"></a><span data-ttu-id="d5526-279">Элемент ActionParameters</span><span class="sxs-lookup"><span data-stu-id="d5526-279">ActionParameters element</span></span>
<span data-ttu-id="d5526-280"><a name="bkmk_ActionParameters"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-280"></span></span>

<span data-ttu-id="d5526-281">Задает список **ActionParameters** для действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-281">Specifies a list of **ActionParameters** for an action.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-282">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-282">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-283">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-283">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<ActionParameters></ActionParameters>
```

<span data-ttu-id="d5526-284">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-284">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-285">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-285">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-286">Нет.</span><span class="sxs-lookup"><span data-stu-id="d5526-286">None.</span></span>
  
    
    
 <span data-ttu-id="d5526-287">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-287">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-288">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-288">**Element**</span></span>|<span data-ttu-id="d5526-289">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-289">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-290">Элемент ActionParameter в элементе ActionParameters (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-290">ActionParameter Element in ActionParameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-291">**ActionParameter**.</span><span class="sxs-lookup"><span data-stu-id="d5526-291">An **ActionParameter**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-292">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-292">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-293">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-293">**Element**</span></span>|<span data-ttu-id="d5526-294">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-294">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-295">Элемент Action в Actions (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-295">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-296">**Action**, к которой относятся следующие **ActionParameters**.</span><span class="sxs-lookup"><span data-stu-id="d5526-296">The **Action** that these **ActionParameters** belong to.</span></span> <br/> |
   

## <a name="actions-element"></a><span data-ttu-id="d5526-297">Элемент Actions</span><span class="sxs-lookup"><span data-stu-id="d5526-297">Actions element</span></span>
<span data-ttu-id="d5526-298"><a name="bkmk_Actions"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-298"></span></span>

<span data-ttu-id="d5526-299">Указывает список действий внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-299">Specifies a list of actions of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-300">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-300">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-301">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-301">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Actions></Actions>
```

<span data-ttu-id="d5526-302">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-302">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-303">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-303">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-304">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-304">None</span></span>
  
    
    
 <span data-ttu-id="d5526-305">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-305">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-306">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-306">**Element**</span></span>|<span data-ttu-id="d5526-307">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-307">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-308">Элемент Action в Actions (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-308">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-309">Действие внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-309">An action of an external content type.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-310">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-310">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-311">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-311">**Element**</span></span>|<span data-ttu-id="d5526-312">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-312">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-313">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-313">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-314">Внешний тип контента, к которой относятся следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d5526-314">The external content type that these actions belong to.</span></span>  <br/> |
   

## <a name="association-element"></a><span data-ttu-id="d5526-315">Элемент сопоставления</span><span class="sxs-lookup"><span data-stu-id="d5526-315">Association element</span></span>
<span data-ttu-id="d5526-316"><a name="bkmk_Association"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-316"></span></span>

<span data-ttu-id="d5526-p110">Элемент сопоставления связывает связанных внешних типов контента в системе. Например, клиент связан с заказа на продажу в системе AdventureWorks: клиенту делает заказов на продажу. Связь хранит указатели на источника и назначения внешних типов контента и указатель на бизнес-логики (объект **MethodInstance** ), который позволяет клиенту получить внешний тип контента назначения из внешнего типа контента источника. Обход **Association**  это вызов метода во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="d5526-p110">The Association element links related external content types within a system. For example, a customer is associated with a sales order in the AdventureWorks system: a customer makes sales orders. An Association holds pointers to the source and destination external content types and a pointer to the business logic (a **MethodInstance** object) that allows a client to get the destination external content type from the source external content type. The traversal of an **Association** is a method call on the external system.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-321">**Пространство имен:** http://schemas.microsoft.com/windows/2007/BusinessDataCatalog</span><span class="sxs-lookup"><span data-stu-id="d5526-321">**Namespace:** http://schemas.microsoft.com/windows/2007/BusinessDataCatalog</span></span>
  
    
    
 <span data-ttu-id="d5526-322">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-322">**Schema:** BDCMetadata</span></span>
  
    
    

> <span data-ttu-id="d5526-323">**Важные:** В свойствах учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="d5526-323">**Important:** Properties are case-sensitive.</span></span> 
  
    
    


<span data-ttu-id="d5526-324">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="d5526-324">**Properties**</span></span>


|<span data-ttu-id="d5526-325">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="d5526-325">**Property**</span></span>|<span data-ttu-id="d5526-326">**Тип**</span><span class="sxs-lookup"><span data-stu-id="d5526-326">**Type**</span></span>|<span data-ttu-id="d5526-327">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-327">**Description**</span></span>|<span data-ttu-id="d5526-328">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="d5526-328">**Required**</span></span>|<span data-ttu-id="d5526-329">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="d5526-329">**Default Value**</span></span>|<span data-ttu-id="d5526-330">**Ограничения/Приемлемые значения**</span><span class="sxs-lookup"><span data-stu-id="d5526-330">**Limits/Accepted Values**</span></span>|
|:-----|:-----|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d5526-331">**HideOnProfilePage**</span><span class="sxs-lookup"><span data-stu-id="d5526-331">**HideOnProfilePage**</span></span> <br/> |<span data-ttu-id="d5526-332">**System.Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-332">**System.Boolean**</span></span> <br/> |<span data-ttu-id="d5526-333">Указывает, следует ли добавить связанного внешнего типа контента на страницу профиля главной внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-333">Specifies whether the related external content type should be added to the profile page of the master external content type.</span></span>  <br/> |<span data-ttu-id="d5526-334">Необязательный</span><span class="sxs-lookup"><span data-stu-id="d5526-334">Optional</span></span>  <br/> |||
   



```XML
<Association Type = "String" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Association>
```

<span data-ttu-id="d5526-335">В следующих разделах приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-335">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-336">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-336">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-337">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-337">**Attribute**</span></span>|<span data-ttu-id="d5526-338">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-338">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-339">**Type**</span><span class="sxs-lookup"><span data-stu-id="d5526-339">**Type**</span></span> <br/> |<span data-ttu-id="d5526-340">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-340">Required.</span></span>  <br/> <span data-ttu-id="d5526-341">**MethodInstanceType**, определяющее тип связи.</span><span class="sxs-lookup"><span data-stu-id="d5526-341">The **MethodInstanceType** that specifies the type of the Association.</span></span> <br/> <span data-ttu-id="d5526-342">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-342">The following table lists the possible values for this attribute.</span></span>  <br/>         <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-343">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-343">Value</span></span></p></th><th><p><span data-ttu-id="d5526-344">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-344">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-345">AssociationNavigator</span><span class="sxs-lookup"><span data-stu-id="d5526-345">AssociationNavigator</span></span></p></td><td><p><span data-ttu-id="d5526-346">**MethodInstance**  это **AssociationNavigator**.</span><span class="sxs-lookup"><span data-stu-id="d5526-346">The **MethodInstance** is an **AssociationNavigator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-347">Соединитель</span><span class="sxs-lookup"><span data-stu-id="d5526-347">Associator</span></span></p></td><td><p><span data-ttu-id="d5526-348">**MethodInstance**  это **Associator**.</span><span class="sxs-lookup"><span data-stu-id="d5526-348">The **MethodInstance** is an **Associator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-349">Метод disassociator</span><span class="sxs-lookup"><span data-stu-id="d5526-349">Disassociator</span></span></p></td><td><p><span data-ttu-id="d5526-350">**MethodInstance**  это **Disassociator**.</span><span class="sxs-lookup"><span data-stu-id="d5526-350">The **MethodInstance** is a **Disassociator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-351">**Данные BulkAssociatedIdEnumerator**</span><span class="sxs-lookup"><span data-stu-id="d5526-351">**BulkAssociatedIdEnumerator**</span></span></p></td><td><p><span data-ttu-id="d5526-352">**MethodInstance**  это **BulkAssociatedIdEnumerator**.</span><span class="sxs-lookup"><span data-stu-id="d5526-352">The **MethodInstance** is a **BulkAssociatedIdEnumerator**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-353">**Метод BulkAssociationNavigator**</span><span class="sxs-lookup"><span data-stu-id="d5526-353">**BulkAssociationNavigator**</span></span></p></td><td><p><span data-ttu-id="d5526-354">**MethodInstance**  это **BulkAssociationNavigator**.</span><span class="sxs-lookup"><span data-stu-id="d5526-354">The **MethodInstance** is a **BulkAssociationNavigator**.</span></span></p></td></tr></tbody></table>|
|<span data-ttu-id="d5526-355">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5526-355">Default</span></span>  <br/> |<span data-ttu-id="d5526-356">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-356">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p111">Указывает, является ли связь по умолчанию среди всех сопоставлений, общий доступ к его тип, содержащего внешнего типа контента. Если параметр имеет значение **true**, связь, по умолчанию среди всех сопоставлений, общий доступ к его тип, содержащего внешнего типа контента. Если параметр имеет значение **false**, связь не по умолчанию среди всех сопоставлений, общий доступ к его тип, содержащего внешнего типа контента. </span><span class="sxs-lookup"><span data-stu-id="d5526-p111">Specifies whether the Association is the default among all Associations sharing its type within the containing external content type. If set to **true**, the Association is the default among all Associations sharing its type within the containing external content type. If set to **false**, the Association is not the default among all Associations sharing its type within the containing external content type.  </span></span><br/> <span data-ttu-id="d5526-360">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-360">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-361">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-361">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-362">ReturnParameterName</span><span class="sxs-lookup"><span data-stu-id="d5526-362">ReturnParameterName</span></span>  <br/> |<span data-ttu-id="d5526-363">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-363">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p112">Имя параметра, который содержит **ReturnTypeDescriptor** связи. Атрибут **Direction** параметр должен содержать значение "В работе", "InOut" или "Вернуть". </span><span class="sxs-lookup"><span data-stu-id="d5526-p112">The name of the parameter that contains the **ReturnTypeDescriptor** of the Association. The **Direction** attribute of the parameter must contain a value of either "Out", "InOut", or "Return". </span></span><br/> <span data-ttu-id="d5526-366">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-366">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-367">ReturnTypeDescriptorName</span><span class="sxs-lookup"><span data-stu-id="d5526-367">ReturnTypeDescriptorName</span></span>  <br/> |<span data-ttu-id="d5526-368">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-368">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p113">Это рекомендуется. Вместо этого используйте **ReturnTypeDescriptorPath**.</span><span class="sxs-lookup"><span data-stu-id="d5526-p113">This has been deprecated. Use the **ReturnTypeDescriptorPath** instead. </span></span><br/> <span data-ttu-id="d5526-371">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-371">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-372">ReturnTypeDescriptorLevel</span><span class="sxs-lookup"><span data-stu-id="d5526-372">ReturnTypeDescriptorLevel</span></span>  <br/> |<span data-ttu-id="d5526-373">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-373">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p114">Это рекомендуется. Вместо этого используйте **ReturnTypeDescriptorPath**.</span><span class="sxs-lookup"><span data-stu-id="d5526-p114">This has been deprecated. Use the **ReturnTypeDescriptorPath** instead. </span></span><br/> <span data-ttu-id="d5526-376">Тип атрибута: **Integer**</span><span class="sxs-lookup"><span data-stu-id="d5526-376">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="d5526-377">ReturnTypeDescriptorPath</span><span class="sxs-lookup"><span data-stu-id="d5526-377">ReturnTypeDescriptorPath</span></span>  <br/> |<span data-ttu-id="d5526-378">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-378">Optional.</span></span>  <br/> <span data-ttu-id="d5526-379">Точками путь **TypeDescriptor** связи.</span><span class="sxs-lookup"><span data-stu-id="d5526-379">The dotted path of the **TypeDescriptor** of the Association.</span></span> <br/> <span data-ttu-id="d5526-380">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-380">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-381">Имя</span><span class="sxs-lookup"><span data-stu-id="d5526-381">Name</span></span>  <br/> |<span data-ttu-id="d5526-382">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-382">Required.</span></span>  <br/> <span data-ttu-id="d5526-383">Имя связи.</span><span class="sxs-lookup"><span data-stu-id="d5526-383">The name of the Association.</span></span>  <br/> <span data-ttu-id="d5526-384">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-384">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-385">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-385">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-386">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-386">Optional.</span></span>  <br/> <span data-ttu-id="d5526-387">Отображаемое имя по умолчанию для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="d5526-387">The default display name for the Association.</span></span>  <br/> <span data-ttu-id="d5526-388">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-388">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-389">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-389">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-390">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-390">Optional.</span></span>  <br/> <span data-ttu-id="d5526-391">Указывает, используются ли часто этого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="d5526-391">Specifies whether this Association is frequently used.</span></span>  <br/> <span data-ttu-id="d5526-392">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-392">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-393">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-393">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-394">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-394">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-395">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-395">**Element**</span></span>|<span data-ttu-id="d5526-396">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-396">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-397">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-397">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-398">Элемент **LocalizedDisplayNames** Указывает список локализованные имена для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="d5526-398">The **LocalizedDisplayNames** element specifies a list of localized names for the Association.</span></span> <br/> |
| [<span data-ttu-id="d5526-399">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-399">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-400">Элемент Properties указывает свойства связи.</span><span class="sxs-lookup"><span data-stu-id="d5526-400">The Properties element specifies the properties of the Association.</span></span>  <br/> |
| [<span data-ttu-id="d5526-401">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-401">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-402">Элемент **AccessControlList** указывает набор прав доступа для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="d5526-402">The **AccessControlList** element specifies a set of access rights for the Association.</span></span> <br/> |
| [<span data-ttu-id="d5526-403">Элемент SourceEntity в элементе Association (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-403">SourceEntity Element in Association (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/19fb5f38-4e85-7fb0-2562-281b9a9ffbef%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-404">Элемент **SourceEntity** указывает внешний тип контента источника в связь.</span><span class="sxs-lookup"><span data-stu-id="d5526-404">The **SourceEntity** element specifies the source external content type in the association.</span></span> <br/> |
| [<span data-ttu-id="d5526-405">Элемент DestinationEntity в элементе Association (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-405">DestinationEntity Element in Association (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/15c53c3b-888d-67c7-af7d-ef36922eeebc%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-406">Элемент **DestinationEntity** указывает внешний тип контента назначения в связь.</span><span class="sxs-lookup"><span data-stu-id="d5526-406">The **DestinationEntity** element specifies the destination external content type in the Association.</span></span> <br/> |
   
 <span data-ttu-id="d5526-407">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-407">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-408">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-408">**Element**</span></span>|<span data-ttu-id="d5526-409">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-409">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-410">Элементы "экземпляры метода" в методе (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-410">MethodInstances Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-411">Элемент **MethodInstances**, которая содержит связь.</span><span class="sxs-lookup"><span data-stu-id="d5526-411">The **MethodInstances** element that contains the Association.</span></span> <br/> |
   

## <a name="associationgroup-element"></a><span data-ttu-id="d5526-412">Элемент AssociationGroup</span><span class="sxs-lookup"><span data-stu-id="d5526-412">AssociationGroup element</span></span>
<span data-ttu-id="d5526-413"><a name="bkmk_AssociationGroup"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-413"></span></span>

<span data-ttu-id="d5526-p115">Указывает **AssociationGroup**. **AssociationGroup**  это конструкция, связанных с ними **AssociationMethods**, связывает вместе. Например **GetOrdersForCustomer**, **GetCustomerForOrder**и **AssociateCustomerToOrder** являются все методы связи, которые работают на же отношение между клиентом и порядке.</span><span class="sxs-lookup"><span data-stu-id="d5526-p115">Specifies an **AssociationGroup**. **AssociationGroup** is a construct that ties the related **AssociationMethods** together. For example, **GetOrdersForCustomer**, **GetCustomerForOrder**, and **AssociateCustomerToOrder** are all association methods that work on the same relationship between Customer and Order.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-417">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-417">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-418">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-418">**Schema:** BDCMetadata</span></span>
  
    
    
 <span data-ttu-id="d5526-419">**AssociationGroup** должны быть определены в элементе сущности, которая является целевой **AssociationReferences**, не помечены как **Reverse**или источника **AssociationReferences**, помеченные как обратный.</span><span class="sxs-lookup"><span data-stu-id="d5526-419">**AssociationGroup** must be defined on the Entity element that is the Destination of the **AssociationReferences** that are not marked as **Reverse**, or the Source of the **AssociationReferences** that are marked as Reverse.</span></span>
  
    
    



```XML
<AssociationGroup Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </AssociationGroup>
```

<span data-ttu-id="d5526-420">В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-420">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-421">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-421">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-422">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-422">**Attribute**</span></span>|<span data-ttu-id="d5526-423">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-423">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-424">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-424">**Name**</span></span> <br/> |<span data-ttu-id="d5526-425">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-425">Required.</span></span>  <br/> <span data-ttu-id="d5526-426">Имя **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-426">The name of the **AssociationGroup**.</span></span>  <br/> <span data-ttu-id="d5526-427">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-427">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-428">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="d5526-428">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="d5526-429">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-429">Optional.</span></span>  <br/> <span data-ttu-id="d5526-430">Отображаемое имя по умолчанию **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-430">The default display name of the **AssociationGroup**.</span></span>  <br/> <span data-ttu-id="d5526-431">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-431">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-432">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="d5526-432">**IsCached**</span></span> <br/> |<span data-ttu-id="d5526-433">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-433">Optional.</span></span>  <br/> <span data-ttu-id="d5526-434">Указывает, используется ли **AssociationGroup** часто.</span><span class="sxs-lookup"><span data-stu-id="d5526-434">Specifies whether the **AssociationGroup** is used frequently.</span></span> <br/> <span data-ttu-id="d5526-435">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-435">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-436">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-436">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-437">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-437">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-438">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-438">**Element**</span></span>|<span data-ttu-id="d5526-439">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-439">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-440">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-440">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-441">Локализованные имена **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-441">The localized names of the **AssociationGroup**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-442">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-442">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-443">Свойства **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-443">The properties of the **AssociationGroup**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-444">Элемент AssociationReference в AssociationGroup (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-444">AssociationReference Element in AssociationGroup (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/e32c5267-53b0-9ff0-6e9a-1cb00d9f1d57%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-445">**AssociationReference** из **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-445">An **AssociationReference** of an **AssociationGroup**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-446">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-446">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-447">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-447">**Element**</span></span>|<span data-ttu-id="d5526-448">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-448">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-449">Элемент AssociationGroups в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-449">AssociationGroups Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-450">Элемент **AssociationGroups**, содержащий этот **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-450">The **AssociationGroups** element that contains this **AssociationGroup**.</span></span>  <br/> |
   

## <a name="associationgroups-element"></a><span data-ttu-id="d5526-451">Элемент AssociationGroups</span><span class="sxs-lookup"><span data-stu-id="d5526-451">AssociationGroups element</span></span>
<span data-ttu-id="d5526-452"><a name="bkmk_AssociationGroups"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-452"></span></span>

<span data-ttu-id="d5526-453">Указывает список элементов **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-453">Specifies a list of **AssociationGroup** elements.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-454">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-454">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-455">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-455">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<AssociationGroups></AssociationGroups>
```

<span data-ttu-id="d5526-456">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-456">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-457">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-457">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-458">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-458">None</span></span>
  
    
    
 <span data-ttu-id="d5526-459">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-459">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-460">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-460">**Element**</span></span>|<span data-ttu-id="d5526-461">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-461">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-462">Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-462">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-463">**AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-463">An **AssociationGroup**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-464">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-464">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-465">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-465">**Element**</span></span>|<span data-ttu-id="d5526-466">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-466">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-467">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-467">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-468">Внешний тип контента, с которым связана этот элемент **AssociationGroups**.</span><span class="sxs-lookup"><span data-stu-id="d5526-468">The external content type that this **AssociationGroups** element is associated with.</span></span> <br/> |
   

## <a name="associationreference-element"></a><span data-ttu-id="d5526-469">Элемент AssociationReference</span><span class="sxs-lookup"><span data-stu-id="d5526-469">AssociationReference element</span></span>
<span data-ttu-id="d5526-470"><a name="bkmk_AssociationReference"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-470"></span></span>

<span data-ttu-id="d5526-471">Задает **AssociationReference** **AssociationGroup**.</span><span class="sxs-lookup"><span data-stu-id="d5526-471">Specifies an **AssociationReference** in an **AssociationGroup**.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-472">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-472">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-473">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-473">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<AssociationReference EntityNamespace = "String" EntityName = "String" AssociationName = "String" Reverse = "Boolean"> </AssociationReference>
```

<span data-ttu-id="d5526-474">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-474">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-475">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-475">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-476">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-476">**Attribute**</span></span>|<span data-ttu-id="d5526-477">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-477">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-478">Пространство имен сущности</span><span class="sxs-lookup"><span data-stu-id="d5526-478">EntityNamespace</span></span>  <br/> |<span data-ttu-id="d5526-479">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-479">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p116">Пространство имен внешнего типа контента, где определяется **Association**. Если указан параметр **EntityName**, **EntityNamespace** является обязательным. </span><span class="sxs-lookup"><span data-stu-id="d5526-p116">The namespace of the external content type where the **Association** is defined. If **EntityName** is specified, **EntityNamespace** is required. </span></span><br/> <span data-ttu-id="d5526-482">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-482">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-483">EntityName</span><span class="sxs-lookup"><span data-stu-id="d5526-483">EntityName</span></span>  <br/> |<span data-ttu-id="d5526-484">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-484">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p117">Имя внешнего типа контента, где определяется **Association**. Если указан параметр **EntityNamespace**, **EntityName** является обязательным. </span><span class="sxs-lookup"><span data-stu-id="d5526-p117">The name of the external content type where the **Association** is defined. If **EntityNamespace** is specified, **EntityName** is required. </span></span><br/> <span data-ttu-id="d5526-487">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-487">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-488">AssociationName</span><span class="sxs-lookup"><span data-stu-id="d5526-488">AssociationName</span></span>  <br/> |<span data-ttu-id="d5526-489">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-489">Required.</span></span>  <br/> <span data-ttu-id="d5526-490">Имя **Association**.</span><span class="sxs-lookup"><span data-stu-id="d5526-490">The name of the **Association**.</span></span>  <br/> <span data-ttu-id="d5526-491">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-491">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-492">Обратный</span><span class="sxs-lookup"><span data-stu-id="d5526-492">Reverse</span></span>  <br/> |<span data-ttu-id="d5526-493">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-493">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p118">Указывает, что указанный **Association** имеет его источника и назначения на обратный. Это означает, что **Association** работает в обратном направлении, по сравнению с другими связей в одном **AssociationGroup**. Например если **AssociationGroup** ссылается на **Association** "GetOrdersForCustomer", возвращение порядок элементов для заданного элемента клиента, затем **AssociationGroup**  это в направлении клиента в порядке. Другие **AssociationReference**, создание ссылок на другой связи "GetCustomerForOrder", должны быть отмечены как обратный, из-за этого сопоставления в направлении заказов для клиента. </span><span class="sxs-lookup"><span data-stu-id="d5526-p118">Specifies that the referenced **Association** has its source and destination reversed. This would indicate the **Association** is working in the opposite direction compared to other associations in the same **AssociationGroup**. For example, if the **AssociationGroup** references an **Association** "GetOrdersForCustomer", returning Order items for the given Customer item, then the **AssociationGroup** is in the direction of Customer to Order. The other **AssociationReference**, referencing another association "GetCustomerForOrder", must be marked as reverse, because this association is in the direction of Order to Customer.  </span></span><br/> <span data-ttu-id="d5526-498">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-498">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-499">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-499">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-500">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-500">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-501">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-501">None</span></span>
  
    
    
 <span data-ttu-id="d5526-502">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-502">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-503">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-503">**Element**</span></span>|<span data-ttu-id="d5526-504">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-504">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-505">Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-505">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-506">**AssociationGroup**, к которому принадлежит этот **AssociationReference**.</span><span class="sxs-lookup"><span data-stu-id="d5526-506">The **AssociationGroup** that this **AssociationReference** belongs to.</span></span> <br/> |
   

## <a name="converttype-element"></a><span data-ttu-id="d5526-507">Элемент ConvertType</span><span class="sxs-lookup"><span data-stu-id="d5526-507">ConvertType element</span></span>
<span data-ttu-id="d5526-508"><a name="bkmk_ConvertType"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-508"></span></span>

<span data-ttu-id="d5526-509">Задает правило, которое требуется преобразовать тип данных значения данных в другой тип данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-509">Specifies the rule to convert the data type of a data value into another data type.</span></span>
  
    
    
 <span data-ttu-id="d5526-510">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-510">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-511">Схема: **Schema:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-511">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="d5526-p119">Элемент Convert правило для преобразования типа данных значения данных в другой тип данных. Если правила применяются в порядке, это правило определяет тип данных значения данных для преобразования в тип данных, заданный атрибутом BDCType. Если правила применяются в обратном порядке, это правило определяет тип данных значения данных для преобразования в тип данных, заданный атрибутом **LOBType**. Например это правило можно указать преобразование значение даты, полученный из внешней системы, в языка и региональных параметров конфиденциальных строка, которая будет отображаться в конечном счете для пользователя, и преобразование обновленное значение для этой строки обратно в даты, совместимое с внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-p119">The Convert element specifies the rule to convert the data type of a data value into another data type. When the rules are applied in order, this rule specifies the data type of the data value to be converted to the data type specified by the BDCType attribute. When the rules are applied in reverse order, this rule specifies the data type of the data value to be converted to the data type specified by the **LOBType** attribute. For example, this rule can specify converting a date value obtained from an external system, into a culture and locale sensitive string which will eventually be displayed to the user, and converting the updated value for that string back into the date that is compatible with the external system.</span></span>
  
    
    

> <span data-ttu-id="d5526-516">**Предупреждение:**
> **ConvertType** не поддерживает преобразование между **System.String** и **System.DateTime**не григорианский календарь.</span><span class="sxs-lookup"><span data-stu-id="d5526-516">**Caution:**
**ConvertType** does not support non-Gregorian calendars for conversions between **System.String** and **System.DateTime**.</span></span> 
  
    
    




```XML
<ConvertType LOBType = "String" BDCType = "String"> </ConvertType>
```

<span data-ttu-id="d5526-517">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-517">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-518">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-518">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-519">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-519">**Attribute**</span></span>|<span data-ttu-id="d5526-520">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-520">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-521">LOBType</span><span class="sxs-lookup"><span data-stu-id="d5526-521">LOBType</span></span>  <br/> |<span data-ttu-id="d5526-522">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-522">Required.</span></span>  <br/> <span data-ttu-id="d5526-523">Тип данных для преобразования значения в при правила применяются в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="d5526-523">The data type to convert the data value into when the rules are applied in reverse order.</span></span>  <br/> <span data-ttu-id="d5526-524">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-524">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-525">BDCType</span><span class="sxs-lookup"><span data-stu-id="d5526-525">BDCType</span></span>  <br/> |<span data-ttu-id="d5526-526">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-526">Required.</span></span>  <br/> <span data-ttu-id="d5526-527">Тип данных для преобразования значения в при применении правила в порядке.</span><span class="sxs-lookup"><span data-stu-id="d5526-527">The data type to convert the data value into when the rules are applied in order.</span></span>  <br/> <span data-ttu-id="d5526-528">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-528">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-529">LOBLocale</span><span class="sxs-lookup"><span data-stu-id="d5526-529">LOBLocale</span></span>  <br/> |<span data-ttu-id="d5526-530">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-530">Optional.</span></span>  <br/> <span data-ttu-id="d5526-531">Языковой стандарт данные, получаемые из внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-531">The locale of the data that is received from the external system.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-532">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-532">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-533">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-533">None</span></span>
  
    
    
 <span data-ttu-id="d5526-534">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-534">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-535">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-535">**Element**</span></span>|<span data-ttu-id="d5526-536">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-536">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-537">Элемент Interpretation в элементе TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-537">Interpretation Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-538">Правила, применяемые к данным, хранящимся в структуры данных, представленные в **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-538">The rules to apply to the data stored in the data structures that are represented by a **TypeDescriptor**.</span></span>  <br/> |
   

## <a name="defaultvalue-element"></a><span data-ttu-id="d5526-539">Элемент DefaultValue</span><span class="sxs-lookup"><span data-stu-id="d5526-539">DefaultValue element</span></span>
<span data-ttu-id="d5526-540"><a name="bkmk_DefaultValue"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-540"></span></span>

<span data-ttu-id="d5526-541">Представляет значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d5526-541">Represents a default value.</span></span>
  
    
    
 <span data-ttu-id="d5526-542">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-542">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-543">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-543">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<DefaultValue MethodInstanceName = "String" Type = "String"> </DefaultValue>
```

<span data-ttu-id="d5526-544">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-544">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-545">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-545">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-546">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-546">**Attribute**</span></span>|<span data-ttu-id="d5526-547">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-547">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-548">**MethodInstanceName**</span><span class="sxs-lookup"><span data-stu-id="d5526-548">**MethodInstanceName**</span></span> <br/> |<span data-ttu-id="d5526-549">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-549">Required.</span></span>  <br/> <span data-ttu-id="d5526-550">Имя **MethodInstance**, к которому применяется этот DefaultValue.</span><span class="sxs-lookup"><span data-stu-id="d5526-550">The name of the **MethodInstance** to which this DefaultValue applies.</span></span> <br/> <span data-ttu-id="d5526-551">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-551">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-552">**Type**</span><span class="sxs-lookup"><span data-stu-id="d5526-552">**Type**</span></span> <br/> | <span data-ttu-id="d5526-553">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-553">Required.</span></span> <br/>  <span data-ttu-id="d5526-554">Тип данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d5526-554">The data type of the default value.</span></span> <br/>  <span data-ttu-id="d5526-555">Ниже приведены допустимые значения для этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-555">The following are the acceptable values for this attribute.</span></span> <br/> <span data-ttu-id="d5526-556">**System.Int16**</span><span class="sxs-lookup"><span data-stu-id="d5526-556">**System.Int16**</span></span> <br/> <span data-ttu-id="d5526-557">**System.Int32**</span><span class="sxs-lookup"><span data-stu-id="d5526-557">**System.Int32**</span></span> <br/> <span data-ttu-id="d5526-558">**System.Int64**</span><span class="sxs-lookup"><span data-stu-id="d5526-558">**System.Int64**</span></span> <br/> <span data-ttu-id="d5526-559">**System.Single**</span><span class="sxs-lookup"><span data-stu-id="d5526-559">**System.Single**</span></span> <br/> <span data-ttu-id="d5526-560">**System.Double**</span><span class="sxs-lookup"><span data-stu-id="d5526-560">**System.Double**</span></span> <br/> <span data-ttu-id="d5526-561">**System.Decimal**</span><span class="sxs-lookup"><span data-stu-id="d5526-561">**System.Decimal**</span></span> <br/> <span data-ttu-id="d5526-562">**System.Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-562">**System.Boolean**</span></span> <br/> <span data-ttu-id="d5526-563">**System.Byte**</span><span class="sxs-lookup"><span data-stu-id="d5526-563">**System.Byte**</span></span> <br/> <span data-ttu-id="d5526-564">**System.UInt16**</span><span class="sxs-lookup"><span data-stu-id="d5526-564">**System.UInt16**</span></span> <br/> <span data-ttu-id="d5526-565">**System.UInt32**</span><span class="sxs-lookup"><span data-stu-id="d5526-565">**System.UInt32**</span></span> <br/> <span data-ttu-id="d5526-566">**System.UInt64**</span><span class="sxs-lookup"><span data-stu-id="d5526-566">**System.UInt64**</span></span> <br/> <span data-ttu-id="d5526-567">**System.Guid**</span><span class="sxs-lookup"><span data-stu-id="d5526-567">**System.Guid**</span></span> <br/> <span data-ttu-id="d5526-568">**System.String**</span><span class="sxs-lookup"><span data-stu-id="d5526-568">**System.String**</span></span> <br/> <span data-ttu-id="d5526-569">**System.DateTime**</span><span class="sxs-lookup"><span data-stu-id="d5526-569">**System.DateTime**</span></span> <br/>  <span data-ttu-id="d5526-570">Любой другой тип serializable (например, где  `Type.IsSerializable == true`)</span><span class="sxs-lookup"><span data-stu-id="d5526-570">Any other serializable type (such as where `Type.IsSerializable == true`)</span></span>  <br/>  <span data-ttu-id="d5526-571">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-571">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="d5526-572">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-572">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-573">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-573">None</span></span>
  
    
    
 <span data-ttu-id="d5526-574">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-574">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-575">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-575">**Element**</span></span>|<span data-ttu-id="d5526-576">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-576">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-577">Элемент DefaultValues в элементе TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-577">DefaultValues Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx)||
   

## <a name="defaultvalues-element"></a><span data-ttu-id="d5526-578">Элемент DefaultValues</span><span class="sxs-lookup"><span data-stu-id="d5526-578">DefaultValues element</span></span>
<span data-ttu-id="d5526-579"><a name="bkmk_DefaultValues"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-579"></span></span>

<span data-ttu-id="d5526-580">Задает список **DefaultValues** **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-580">Specifies a list of **DefaultValues** of a **TypeDescriptor**.</span></span>
  
    
    
 <span data-ttu-id="d5526-581">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-581">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-582">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-582">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<DefaultValues></DefaultValues>
```

<span data-ttu-id="d5526-583">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-583">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-584">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-584">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-585">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-585">None</span></span>
  
    
    
 <span data-ttu-id="d5526-586">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-586">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-587">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-587">**Element**</span></span>|<span data-ttu-id="d5526-588">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-588">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-589">Элемент DefaultValue в элементе DefaultValues (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-589">DefaultValue Element in DefaultValues (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ddb67f64-6361-7b59-6724-4680484d585d%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-590">Значение по умолчанию **TypeDescriptor** для **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-590">The default value of a **TypeDescriptor** for a **MethodInstance**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-591">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-591">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-592">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-592">**Element**</span></span>|<span data-ttu-id="d5526-593">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-593">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-594">Элемент TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-594">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-595">**TypeDescriptor**, к которой относятся следующие **DefaultValues**.</span><span class="sxs-lookup"><span data-stu-id="d5526-595">The **TypeDescriptor** that these **DefaultValues** belong to.</span></span> <br/> |
   

## <a name="destinationentity-element"></a><span data-ttu-id="d5526-596">Элемент DestinationEntity</span><span class="sxs-lookup"><span data-stu-id="d5526-596">DestinationEntity element</span></span>
<span data-ttu-id="d5526-597"><a name="bkmk_DestinationEntity"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-597"></span></span>

<span data-ttu-id="d5526-598">Определяет внешний тип контента назначения в **Association**.</span><span class="sxs-lookup"><span data-stu-id="d5526-598">Specifies the destination external content type in the **Association**.</span></span>
  
    
    
 <span data-ttu-id="d5526-599">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-599">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-600">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-600">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<DestinationEntity Namespace = "String" Name = "String"> </DestinationEntity>
```

<span data-ttu-id="d5526-601">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-601">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-602">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-602">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-603">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-603">**Attribute**</span></span>|<span data-ttu-id="d5526-604">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-604">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-605">**Namespace**</span><span class="sxs-lookup"><span data-stu-id="d5526-605">**Namespace**</span></span> <br/> |<span data-ttu-id="d5526-606">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-606">Required.</span></span>  <br/> <span data-ttu-id="d5526-607">Имя пространства имен сущности.</span><span class="sxs-lookup"><span data-stu-id="d5526-607">The name of the entity namespace.</span></span>  <br/> <span data-ttu-id="d5526-608">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-608">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-609">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-609">**Name**</span></span> <br/> |<span data-ttu-id="d5526-610">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-610">Required.</span></span>  <br/> <span data-ttu-id="d5526-611">Имя конечной сущности.</span><span class="sxs-lookup"><span data-stu-id="d5526-611">The name of the destination entity.</span></span>  <br/> <span data-ttu-id="d5526-612">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-612">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="d5526-613">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-613">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-614">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-614">None</span></span>
  
    
    
 <span data-ttu-id="d5526-615">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-615">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-616">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-616">**Element**</span></span>|<span data-ttu-id="d5526-617">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-617">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-618">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-618">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx)||
   

## <a name="entities-element"></a><span data-ttu-id="d5526-619">Элемент сущности</span><span class="sxs-lookup"><span data-stu-id="d5526-619">Entities element</span></span>
<span data-ttu-id="d5526-620"><a name="bkmk_Entities"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-620"></span></span>

<span data-ttu-id="d5526-621">Указывает список внешних типов контента в внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-621">Specifies a list of external content types in an external system.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-622">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-622">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-623">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-623">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Entities></Entities>
```

<span data-ttu-id="d5526-624">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-624">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-625">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-625">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-626">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-626">None</span></span>
  
    
    
 <span data-ttu-id="d5526-627">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-627">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-628">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-628">**Element**</span></span>|<span data-ttu-id="d5526-629">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-629">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-630">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-630">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-631">Внешний тип контента в внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-631">An external content type in an external system.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-632">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-632">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-633">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-633">**Element**</span></span>|<span data-ttu-id="d5526-634">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-634">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-635">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-635">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-636">Внешняя система.</span><span class="sxs-lookup"><span data-stu-id="d5526-636">An external system.</span></span>  <br/> |
   

## <a name="entity-element"></a><span data-ttu-id="d5526-637">Элемент сущности</span><span class="sxs-lookup"><span data-stu-id="d5526-637">Entity element</span></span>
<span data-ttu-id="d5526-638"><a name="bkmk_Entity"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-638"></span></span>

<span data-ttu-id="d5526-639">Указывает внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-639">Specifies an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-640">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-640">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-641">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-641">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Entity Namespace = "String" Version = "String" EstimatedInstanceCount = "Integer" DefaultOperationMode = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Entity>
```

<span data-ttu-id="d5526-642">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-642">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-643">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-643">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-644">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-644">**Attribute**</span></span>|<span data-ttu-id="d5526-645">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-645">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-646">**Namespace**</span><span class="sxs-lookup"><span data-stu-id="d5526-646">**Namespace**</span></span> <br/> |<span data-ttu-id="d5526-647">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-647">Required.</span></span>  <br/> <span data-ttu-id="d5526-648">Пространство имен, которому принадлежит этот внешний тип контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-648">The namespace that this external content type belongs to.</span></span>  <br/> <span data-ttu-id="d5526-649">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-649">Attribute type: **String**</span></span> <br/> <span data-ttu-id="d5526-650">**Примечание**: пространство имен не должны содержать специальные знак звездочка " **\***«.</span><span class="sxs-lookup"><span data-stu-id="d5526-650">**Note**: The namespace should not contain the asterisk special character " **\***".</span></span>           |
|<span data-ttu-id="d5526-651">**Version**</span><span class="sxs-lookup"><span data-stu-id="d5526-651">**Version**</span></span> <br/> |<span data-ttu-id="d5526-652">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-652">Required.</span></span>  <br/> <span data-ttu-id="d5526-653">Номер версии данного внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-653">The version number of this external content type.</span></span>  <br/> <span data-ttu-id="d5526-654">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-654">Attribute type: **String**</span></span> <br/> <span data-ttu-id="d5526-655">**Осторожность:** При изменении модели BDC, необходимо увеличить номер версии внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-655">**Caution:** When the BDC model changes, you must increase the version number of the external content type.</span></span> <span data-ttu-id="d5526-656">При изменении структуры внешнего типа контента, следует увеличить основной номер.</span><span class="sxs-lookup"><span data-stu-id="d5526-656">If the structure of an external content type changes, you should increase the major number.</span></span> <span data-ttu-id="d5526-657">Структурные изменения примеры Добавление поля **SpecificFinder** или изменение поле идентификатора.</span><span class="sxs-lookup"><span data-stu-id="d5526-657">Examples of structural changes include adding a field to a **SpecificFinder** or changing an identifier field.</span></span> <span data-ttu-id="d5526-658">Если изменения не влияет на структуру внешнего типа контента, например при добавлении метода creator, изменение сведения о подключении или при изменении имена дескрипторов **бизнес-системам** и тип, необходимо изменить номер сборки и номер редакции.</span><span class="sxs-lookup"><span data-stu-id="d5526-658">If the change does not affect the structure of the external content type, for example, when adding a creator method, changing connection information, or when changing names of **LobSystems** and type descriptors, you should change the build number and revision number.</span></span>          |
|<span data-ttu-id="d5526-659">**EstimatedInstanceCount**</span><span class="sxs-lookup"><span data-stu-id="d5526-659">**EstimatedInstanceCount**</span></span> <br/> |<span data-ttu-id="d5526-660">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-660">Optional.</span></span>  <br/> <span data-ttu-id="d5526-661">Предполагаемое количество внешних элементов, содержащихся в во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="d5526-661">The estimated number of external items contained by the external system.</span></span>  <br/> <span data-ttu-id="d5526-662">Значение по умолчанию: 10000</span><span class="sxs-lookup"><span data-stu-id="d5526-662">Default value: 10000</span></span>  <br/> <span data-ttu-id="d5526-663">Тип атрибута: **Integer**</span><span class="sxs-lookup"><span data-stu-id="d5526-663">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="d5526-664">**DefaultOperationMode**</span><span class="sxs-lookup"><span data-stu-id="d5526-664">**DefaultOperationMode**</span></span> <br/> |<span data-ttu-id="d5526-665">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-665">Optional.</span></span>  <br/> <span data-ttu-id="d5526-666">Задает поведение по умолчанию при взаимодействии с внешней системы во время создания, удаления, обновления или чтение внешних элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-666">Specifies the default behavior when interacting with the external system while creating, deleting, updating, or reading external items.</span></span>  <br/> <span data-ttu-id="d5526-667">Значение по умолчанию: по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5526-667">Default value: Default</span></span>  <br/> <span data-ttu-id="d5526-668">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-668">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-669">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-669">Value</span></span></p></th><th><p><span data-ttu-id="d5526-670">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-670">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-671">Оперативный режим</span><span class="sxs-lookup"><span data-stu-id="d5526-671">Online</span></span></p></td><td><p><span data-ttu-id="d5526-672">Кэшированные внешние элементы для всех операций обхода и напрямую взаимодействовать с внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-672">Bypass the cached external items for all operations and interact with the external system directly.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-673">Кэширования данных</span><span class="sxs-lookup"><span data-stu-id="d5526-673">Cached</span></span></p></td><td><p><span data-ttu-id="d5526-p121">Выполните <b>Создание</b>, <b>Чтение</b>, <b>обновление</b> и <b>Удаление</b> операций непосредственно с внешним кэшированные элементы. Для операций <b>чтения</b> если запрошенные внешние элементы в кэше, используйте внешние элементы в кэше. В противном случае обход кэша для получения внешних элементов из внешней системы и поместить его в кэш для дальнейшего использования. </span><span class="sxs-lookup"><span data-stu-id="d5526-p121">Perform <b>Create</b>, <b>Read</b>, <b>Update</b>, and <b>Delete</b> operations directly against the cached external items. For <b>Read</b> operations, if the requested external items are available in the cache, use the external items in the cache. Otherwise, bypass the cache to obtain the external items from the external system, and put it in the cache for later use.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-677">Автономный режим</span><span class="sxs-lookup"><span data-stu-id="d5526-677">Offline</span></span></p></td><td><p><span data-ttu-id="d5526-678">Выполните <b>Создание</b>, <b>Чтение</b>, <b>обновление</b> и <b>Удаление</b> операций с кэшированные внешние элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-678">Perform <b>Create</b>, <b>Read</b>, <b>Update</b>, and <b>Delete</b> operations against only the cached external items.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-679">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5526-679">Default</span></span></p></td><td><p><span data-ttu-id="d5526-p122">Используйте системы по умолчанию. При этом используется режим кэширования, если среда поддерживает кэширование внешние элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-p122">Use the System default behavior. This uses Cached mode if the environment supports caching external items.</span></span></p></td></tr></tbody></table>|
|<span data-ttu-id="d5526-682">Name</span><span class="sxs-lookup"><span data-stu-id="d5526-682">Name</span></span>  <br/> |<span data-ttu-id="d5526-683">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-683">Required.</span></span>  <br/> <span data-ttu-id="d5526-684">Имя внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-684">The name of the external content type.</span></span>  <br/> <span data-ttu-id="d5526-685">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-685">Attribute type: **String**</span></span> <br/> <span data-ttu-id="d5526-686">**Примечание**: имя внешнего типа контента не должны содержать специальные знак звездочка " **\***«.</span><span class="sxs-lookup"><span data-stu-id="d5526-686">**Note**: The name of an external content type should not contain the asterisk special character " **\***".</span></span>           |
|<span data-ttu-id="d5526-687">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-687">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-688">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-688">Optional.</span></span>  <br/> <span data-ttu-id="d5526-689">По умолчанию отображаемое имя внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-689">The default display name of the external content type.</span></span>  <br/> <span data-ttu-id="d5526-690">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-690">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-691">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-691">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-692">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-692">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p123">Указывает, будет ли часто используемые этот внешний тип контента. Если параметр имеет значение true, Служба подключения к бизнес-данным (BDC) будет кэшировать этот внешний тип контента в памяти.</span><span class="sxs-lookup"><span data-stu-id="d5526-p123">Specifies whether this external content type will be frequently used. If set to true, Business Data Connectivity (BDC) service will cache this external content type in memory.  </span></span><br/> <span data-ttu-id="d5526-695">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-695">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-696">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-696">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-697">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-697">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-698">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-698">**Element**</span></span>|<span data-ttu-id="d5526-699">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-699">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-700">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-700">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-701">Локализованное имя данного внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-701">The localized display names of this external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-702">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-702">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-703">Свойства данного внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-703">The properties of this external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-704">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-704">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-705">Список управления доступом (ACL) этого внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-705">The access control list (ACL) of this external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-706">Элемент Identifiers в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-706">Identifiers Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-707">Идентификаторы внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-707">The identifiers of the external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-708">Элемент Methods в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-708">Methods Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-709">Методы внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-709">The methods of the external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-710">Элемент AssociationGroups в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-710">AssociationGroups Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b50c2648-daea-d8c0-039a-b95590b9924c%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-711">Связь группы внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-711">The association groups of the external content type.</span></span>  <br/> |
| [<span data-ttu-id="d5526-712">Элемент Actions в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-712">Actions Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c5a6c08d-a3df-61db-3ce3-1e6837bbf221%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-713">Действия внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-713">The actions of the external content type.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-714">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-714">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-715">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-715">**Element**</span></span>|<span data-ttu-id="d5526-716">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-716">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-717">Элемент Entities в LobSystem (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-717">Entities Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-718">Список внешних типов контента в этом внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-718">The list of external content types in this external system.</span></span>  <br/> |
   

## <a name="filterdescriptor-element"></a><span data-ttu-id="d5526-719">Элемент FilterDescriptor</span><span class="sxs-lookup"><span data-stu-id="d5526-719">FilterDescriptor element</span></span>
<span data-ttu-id="d5526-720"><a name="bkmk_FilterDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-720"></span></span>

<span data-ttu-id="d5526-721">Задает дескриптор фильтра для метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-721">Specifies a filter descriptor of a method.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-722">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-722">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-723">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-723">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<FilterDescriptor Type = "String" FilterField = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </FilterDescriptor>
```

<span data-ttu-id="d5526-724">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-724">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-725">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-725">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-726">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-726">**Attribute**</span></span>|<span data-ttu-id="d5526-727">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-727">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-728">Тип</span><span class="sxs-lookup"><span data-stu-id="d5526-728">Type</span></span>  <br/> |<span data-ttu-id="d5526-729">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-729">Required.</span></span>  <br/> <span data-ttu-id="d5526-730">Тип дескриптора фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-730">The type of the filter descriptor.</span></span>  <br/> <span data-ttu-id="d5526-731">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-731">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-732">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-732">Value</span></span></p></th><th><p><span data-ttu-id="d5526-733">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-733">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-734">Limit</span><span class="sxs-lookup"><span data-stu-id="d5526-734">Limit</span></span></p></td><td><p><span data-ttu-id="d5526-735">Используется при запросе внешние системы и значения, из которых можно интерпретации ограничение на количество внешние элементы **экземпляры сущностей** , которые возвращаются при вызове метода, к которому он принадлежит.</span><span class="sxs-lookup"><span data-stu-id="d5526-735">Used while querying an external system and the value of which can be interpreted as a limit on the number of external items **EntityInstances** that are returned when the method that it belongs to is called.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-736">PageNumber</span><span class="sxs-lookup"><span data-stu-id="d5526-736">PageNumber</span></span></p></td><td><p /></td></tr><tr><td><p><span data-ttu-id="d5526-737">Wildcard</span><span class="sxs-lookup"><span data-stu-id="d5526-737">Wildcard</span></span></p></td><td><p><span data-ttu-id="d5526-p124">Используется при запросе внешней системы. Его значение представляет шаблон регулярных и подстановочных знаков, который является, с которым сравнивается значение отдельного поля set **EntityInstances**. Внешняя система возвращает только тех **EntityInstances**, значения поля соответствуют заданному шаблону. </span><span class="sxs-lookup"><span data-stu-id="d5526-p124">Used while querying an external system. Its value represents a pattern of regular and wildcard characters that is matched against the value of a particular field of the set of **EntityInstances**. The external system returns only those **EntityInstances** whose field values match the specified pattern.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-741">UserContext</span><span class="sxs-lookup"><span data-stu-id="d5526-741">UserContext</span></span></p></td><td><p><span data-ttu-id="d5526-p125">Используется при запросе внешней системы. В качестве значения этого свойства любым клиентским приложением может автоматически задаваться удостоверение пользователя, вызывающего внешнюю систему. В дальнейшем это значение может использоваться внешней системой для авторизации и фильтрации возвращаемых результатов.</span><span class="sxs-lookup"><span data-stu-id="d5526-p125">Used while querying an external system. Its value can be set automatically by any client application to the identity of the user who is calling the external system. This value can then be used by the external system to authorize and then filter the results returned.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-745">UserCulture</span><span class="sxs-lookup"><span data-stu-id="d5526-745">UserCulture</span></span></p></td><td><p /></td></tr><tr><td><p><span data-ttu-id="d5526-746">Username</span><span class="sxs-lookup"><span data-stu-id="d5526-746">Username</span></span></p></td><td><p /></td></tr><tr><td><p><span data-ttu-id="d5526-747">Password</span><span class="sxs-lookup"><span data-stu-id="d5526-747">Password</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="d5526-748">LastId</span><span class="sxs-lookup"><span data-stu-id="d5526-748">LastId</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="d5526-749">SsoTicket</span><span class="sxs-lookup"><span data-stu-id="d5526-749">SsoTicket</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="d5526-750">UserProfile</span><span class="sxs-lookup"><span data-stu-id="d5526-750">UserProfile</span></span></p></td><td><p><span data-ttu-id="d5526-p126">Используется при запросе внешней системы. Для получения значения этого свойства необходимо проверить текущий профиль пользователя. Это значение используется внешней системой для фильтрации возвращаемых результатов.</span><span class="sxs-lookup"><span data-stu-id="d5526-p126">Used while querying an external system. Its value can be obtained by examining the current user's profile. The external system can use its value to filter the results returned.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-754">Comparison</span><span class="sxs-lookup"><span data-stu-id="d5526-754">Comparison</span></span></p></td><td><p><span data-ttu-id="d5526-p127">Используется при запросе внешней системы. Во внешней системе возможно сравнение значения атрибута **ComparisonFilter** со значением отдельного поля в наборе элементов **EntityInstances**. В этом случае возвращаются только те элементы **EntityInstances**, для которых значения поля прошли проверку сравнением. </span><span class="sxs-lookup"><span data-stu-id="d5526-p127">Used while querying an external system. An external system can compare a **ComparisonFilter** value with the value of a particular field of a set of **EntityInstances** and only those **EntityInstances** where the field values pass the comparison test can be returned.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-757">Временная метка</span><span class="sxs-lookup"><span data-stu-id="d5526-757">Timestamp</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="d5526-758">Input</span><span class="sxs-lookup"><span data-stu-id="d5526-758">Input</span></span></p></td><td><p><span data-ttu-id="d5526-p128">Используется при вызове операции во внешней системе. Во внешней системе значение атрибута **InputFilter** может использоваться в качестве дополнительных аргументов операции.</span><span class="sxs-lookup"><span data-stu-id="d5526-p128">Used while calling an operation in an external system. An external system can use the value of an **InputFilter** as additional arguments for the operation.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-761">Output</span><span class="sxs-lookup"><span data-stu-id="d5526-761">Output</span></span></p></td><td><p><span data-ttu-id="d5526-p129">Используется при вызове операции во внешней системе. Дополнительные результаты операции, которые недоступны для получения с помощью атрибута **ReturnTypeDescriptor**, извлекаются в качестве значения атрибута **InputOutputFilter**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p129">Used while calling an operation in an external system. Additional results of an operation that cannot be captured by **ReturnTypeDescriptor** can be retrieved as a value of the **InputOutputFilter**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-764">InputOutput</span><span class="sxs-lookup"><span data-stu-id="d5526-764">InputOutput</span></span></p></td><td><p><span data-ttu-id="d5526-p130">Используется при вызове операции во внешней системе. Значение атрибута **InputOutputFilter** может использоваться во внешней системе в качестве дополнительных аргументов операции. Дополнительные результаты операции, которые недоступны для получения с помощью атрибута **ReturnTypeDescriptor**, извлекаются в качестве значения атрибута **InputOutputFilter**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p130">Used while calling an operation in an external system. An external system can use the value of an **InputOutputFilter** as additional arguments for the operation, and additional results of an operation that cannot be captured by **ReturnTypeDescriptor** can be retrieved as a value of the **InputOutputFilter**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-767">Batching</span><span class="sxs-lookup"><span data-stu-id="d5526-767">Batching</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="d5526-768">BatchingTermination</span><span class="sxs-lookup"><span data-stu-id="d5526-768">BatchingTermination</span></span></p></td><td /></tr><tr><td><p><span data-ttu-id="d5526-769">ActivityId</span><span class="sxs-lookup"><span data-stu-id="d5526-769">ActivityId</span></span></p></td><td><p><span data-ttu-id="d5526-p131">Атрибут **ActivityId** используется при вызове операции внешней системы. Этому атрибуту присваивается значение, соответствующее идентификатору GUID, который представляет текущий контекст операции. Если это значение недоступно, формируется случайный идентификатор GUID. В SharePoint Foundation 2010 в этом фильтре используется идентификатор **CorrelationID**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p131">**ActivityId** is used when calling an operation on the external system. Its value is set to a GUID that represents the current operation context. If no such value is available, this filter generates a random GUID. On SharePoint Foundation 2010, this filter uses the **CorrelationID**.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="d5526-774">FilterField</span><span class="sxs-lookup"><span data-stu-id="d5526-774">FilterField</span></span>  <br/> |<span data-ttu-id="d5526-775">Необязательный.</span><span class="sxs-lookup"><span data-stu-id="d5526-775">Optional.</span></span>  <br/> <span data-ttu-id="d5526-776">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-776">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-777">Имя</span><span class="sxs-lookup"><span data-stu-id="d5526-777">Name</span></span>  <br/> |<span data-ttu-id="d5526-778">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-778">Required.</span></span>  <br/> <span data-ttu-id="d5526-779">Имя дескриптора фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-779">The name of the filter descriptor.</span></span>  <br/> <span data-ttu-id="d5526-780">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-780">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-781">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-781">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-782">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-782">Optional.</span></span>  <br/> <span data-ttu-id="d5526-783">Установленное по умолчанию отображаемое имя дескриптора фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-783">The default display name of the filter descriptor.</span></span>  <br/> <span data-ttu-id="d5526-784">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-784">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-785">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-785">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-786">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-786">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p132">Задает частоту использования этого дескриптора фильтра. Если установлено значение **true**, в службе Служба подключения к бизнес-данным (BDC) выполняется кэширование этого дескриптора в памяти.</span><span class="sxs-lookup"><span data-stu-id="d5526-p132">Specifies whether this filter descriptor is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches this filter descriptor in memory.  </span></span><br/> <span data-ttu-id="d5526-789">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-789">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-790">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-790">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-791">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-791">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-792">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-792">**Element**</span></span>|<span data-ttu-id="d5526-793">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-793">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-794">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-794">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-795">Локализованные отображаемые имена дескриптора фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-795">The localized display names of this filter descriptor.</span></span>  <br/> |
| [<span data-ttu-id="d5526-796">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-796">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-797">Свойства дескриптора фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-797">The properties of this filter descriptor.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-798">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-798">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-799">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-799">**Element**</span></span>|<span data-ttu-id="d5526-800">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-800">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-801">Элемент FilterDescriptors в элементе Method (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-801">FilterDescriptors Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-802">Список дескрипторов фильтра для метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-802">A list of filter descriptors of a method.</span></span>  <br/> |
   

## <a name="filterdescriptors-element"></a><span data-ttu-id="d5526-803">Элемент FilterDescriptors</span><span class="sxs-lookup"><span data-stu-id="d5526-803">FilterDescriptors element</span></span>
<span data-ttu-id="d5526-804"><a name="bkmk_FilterDescriptors"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-804"></span></span>

<span data-ttu-id="d5526-805">Задает список дескрипторов фильтра для метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-805">Specifies a list of filter descriptors of a method.</span></span>
  
    
    
 <span data-ttu-id="d5526-806">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-806">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-807">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-807">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<FilterDescriptors></FilterDescriptors>
```

<span data-ttu-id="d5526-808">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-808">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-809">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-809">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-810">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-810">None</span></span>
  
    
    
 <span data-ttu-id="d5526-811">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-811">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-812">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-812">**Element**</span></span>|<span data-ttu-id="d5526-813">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-813">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-814">Элемент FilterDescriptor в элементе FilterDescriptors (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-814">FilterDescriptor Element in FilterDescriptors (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-815">Дескриптор фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-815">A filter descriptor.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-816">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-816">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-817">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-817">**Element**</span></span>|<span data-ttu-id="d5526-818">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-818">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-819">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-819">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-820">Метод, которому принадлежит этот список дескрипторов фильтра.</span><span class="sxs-lookup"><span data-stu-id="d5526-820">The method this list of filter descriptors belongs to.</span></span>  <br/> |
   

## <a name="identifier-element"></a><span data-ttu-id="d5526-821">Идентификатор элемента</span><span class="sxs-lookup"><span data-stu-id="d5526-821">Identifier element</span></span>
<span data-ttu-id="d5526-822"><a name="bkmk_Identifier"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-822"></span></span>

<span data-ttu-id="d5526-823">Задает идентификатор внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-823">Specifies an identifier of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-824">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-824">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-825">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-825">**Schema:** BDCMetadata</span></span>
  
    
> [!NOTE]
> 
> <span data-ttu-id="d5526-p133">[!Примечание] Служба подключения к бизнес-данным (BDC) позволяет сопоставления идентификаторов для полей с типами данных допускает значение NULL. Тем не менее для основного идентификаторов BDC приведет к ошибке при **null**значение из этих идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="d5526-p133">Business Data Connectivity (BDC) service enables the mapping of identifiers to fields with nullable data types. However, for primary identifiers, BDC will cause an error when the value of these identifiers are **null**.</span></span> 
  
    
    




```XML
<Identifier TypeName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Identifier>
```

<span data-ttu-id="d5526-828">В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-828">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-829">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-829">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-830">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-830">**Attribute**</span></span>|<span data-ttu-id="d5526-831">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-831">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-832">TypeName</span><span class="sxs-lookup"><span data-stu-id="d5526-832">TypeName</span></span>  <br/> |<span data-ttu-id="d5526-833">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-833">Required.</span></span>  <br/> <span data-ttu-id="d5526-834">Тип данных значение, соответствующее идентификатору.</span><span class="sxs-lookup"><span data-stu-id="d5526-834">The data type of the value that corresponds to the identifier.</span></span>  <br/> <span data-ttu-id="d5526-835">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-835">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-836">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-836">Value</span></span></p></th><th><p><span data-ttu-id="d5526-837">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-837">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-838">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="d5526-838">System.Boolean</span></span></p></td><td><p><span data-ttu-id="d5526-839">Бит.</span><span class="sxs-lookup"><span data-stu-id="d5526-839">A bit.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-840">System.Byte</span><span class="sxs-lookup"><span data-stu-id="d5526-840">System.Byte</span></span></p></td><td><p><span data-ttu-id="d5526-841">Число в диапазоне от 0 до 255 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-841">A number ranging from 0 to 255 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-842">System.Char</span><span class="sxs-lookup"><span data-stu-id="d5526-842">System.Char</span></span></p></td><td><p><span data-ttu-id="d5526-843">Символ Юникода.</span><span class="sxs-lookup"><span data-stu-id="d5526-843">A Unicode character.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-844">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="d5526-844">System.DateTime</span></span></p></td><td><p><span data-ttu-id="d5526-p134">Даты и времени от 12:00:00 полночь 1 января 1 Domini Anno (Common эра) в 11:59:59 P.M. 31 декабря, 9999 года (Common эра) включительно, с разрешением до 100 наносекунд.</span><span class="sxs-lookup"><span data-stu-id="d5526-p134">A date and time ranging from 12:00:00 midnight, January 1, 1 Anno Domini (Common Era) to 11:59:59 P.M. December 31, 9999 Anno Domini (Common Era) inclusive, in resolution of 100 nanoseconds.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-847">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="d5526-847">System.Decimal</span></span></p></td><td><p><span data-ttu-id="d5526-848">Число в диапазоне от отрицательные 79,228,162,514,264,337,593,543,950,335 для плюс 79,228,162,514,264,337,593,543,950,335 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-848">A number ranging from negative 79,228,162,514,264,337,593,543,950,335 to positive 79,228,162,514,264,337,593,543,950,335 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-849">System.Double</span><span class="sxs-lookup"><span data-stu-id="d5526-849">System.Double</span></span></p></td><td><p><span data-ttu-id="d5526-850">Двойной точности число от отрицательные 1, 79769313486232E308 для положительных 1, 79769313486232E308 включительно и положительного, отрицательные нулю, положительное infinity, отрицательные infinity и не является числовым (NaN).</span><span class="sxs-lookup"><span data-stu-id="d5526-850">A double precision number ranging from negative 1.79769313486232e308 to positive 1.79769313486232e308 inclusive, and positive zero, negative zero, positive infinity, negative infinity, and not-a-number (NaN).</span></span> </p></td></tr><tr><td><p><span data-ttu-id="d5526-851">System.Guid</span><span class="sxs-lookup"><span data-stu-id="d5526-851">System.Guid</span></span></p></td><td><p><span data-ttu-id="d5526-852">ИДЕНТИФИКАТОР GUID.</span><span class="sxs-lookup"><span data-stu-id="d5526-852">A GUID.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-853">System.Int16</span><span class="sxs-lookup"><span data-stu-id="d5526-853">System.Int16</span></span></p></td><td><p><span data-ttu-id="d5526-854">Число в диапазоне от минус 32768 до положительное 32767 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-854">A number ranging from negative 32768 to positive 32767 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-855">System.Int32</span><span class="sxs-lookup"><span data-stu-id="d5526-855">System.Int32</span></span></p></td><td><p><span data-ttu-id="d5526-856">Число от 0 до 4 294 967 295 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-856">A number ranging from 0 to 4,294,967,295 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-857">System.Int64</span><span class="sxs-lookup"><span data-stu-id="d5526-857">System.Int64</span></span></p></td><td><p><span data-ttu-id="d5526-858">Число в диапазоне от 0 до 18446744073709551615 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-858">A number ranging from 0 to 18,446,744,073,709,551,615 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-859">System.SByte</span><span class="sxs-lookup"><span data-stu-id="d5526-859">System.SByte</span></span></p></td><td><p><span data-ttu-id="d5526-860">Число в диапазоне от минус 128 до плюс 127 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-860">A number ranging from negative 128 to positive 127 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-861">System.Single</span><span class="sxs-lookup"><span data-stu-id="d5526-861">System.Single</span></span></p></td><td><p><span data-ttu-id="d5526-862">Запятой одинарной точности число в диапазоне минус 3, 402823E38 для положительных 3, 402823E38 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-862">A single precision number ranging from negative 3.402823e38 to positive 3.402823e38 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-863">System.String</span><span class="sxs-lookup"><span data-stu-id="d5526-863">System.String</span></span></p></td><td><p><span data-ttu-id="d5526-864">Строка текста в формате Юникода.</span><span class="sxs-lookup"><span data-stu-id="d5526-864">A string of Unicode text.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-865">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d5526-865">System.TimeSpan</span></span></p></td><td><p><span data-ttu-id="d5526-866">Продолжительность от отрицательные 10675199 дней 2 часа 48 минут 5 секунд 477 миллисекунд 580 миллисекундах 800 наносекунд до положительное 10675199 дней 2 часа 48 минут 5 секунд 477 миллисекунд 580 включительно, в решение 100 наносекунд наносекунд 800 миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="d5526-866">A duration ranging from negative 10675199 days 2 hours 48 minutes 5 seconds 477 milliseconds 580 microseconds 800 nanoseconds to positive 10675199 days 2 hours 48 minutes 5 seconds 477 milliseconds 580 microseconds 800 nanoseconds inclusive, in resolution of 100 nanoseconds.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-867">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="d5526-867">System.UInt16</span></span></p></td><td><p><span data-ttu-id="d5526-868">Число в диапазоне от 0 до 65535 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-868">A number ranging from 0 to 65535 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-869">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="d5526-869">System.UInt32</span></span></p></td><td><p><span data-ttu-id="d5526-870">Число от 0 до 4 294 967 295 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-870">A number ranging from 0 to 4,294,967,295 inclusive.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-871">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="d5526-871">System.UInt64</span></span></p></td><td><p><span data-ttu-id="d5526-872">Число от 0 до 18,446,744,709,551,615 включительно.</span><span class="sxs-lookup"><span data-stu-id="d5526-872">A number ranging from 0 to 18,446,744,709,551,615 inclusive.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="d5526-873">Name</span><span class="sxs-lookup"><span data-stu-id="d5526-873">Name</span></span>  <br/> |<span data-ttu-id="d5526-874">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-874">Required.</span></span>  <br/> <span data-ttu-id="d5526-875">Имя идентификатора.</span><span class="sxs-lookup"><span data-stu-id="d5526-875">The name of the identifier.</span></span>  <br/> <span data-ttu-id="d5526-876">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-876">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-877">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-877">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-878">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-878">Optional.</span></span>  <br/> <span data-ttu-id="d5526-879">По умолчанию отображаемое имя идентификатора.</span><span class="sxs-lookup"><span data-stu-id="d5526-879">The default display name of the identifier.</span></span>  <br/> <span data-ttu-id="d5526-880">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-880">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-881">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-881">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-882">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-882">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p135">Указывает, используется ли этот идентификатор часто. Если параметр имеет значение **true**, Служба подключения к бизнес-данным (BDC) кэширует идентификатор в памяти.</span><span class="sxs-lookup"><span data-stu-id="d5526-p135">Specifies whether this identifier is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches the identifier in memory.  </span></span><br/> <span data-ttu-id="d5526-885">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-885">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-886">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-886">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-887">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-887">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-888">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-888">**Element**</span></span>|<span data-ttu-id="d5526-889">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-889">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-890">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-890">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-891">Локализованное имя идентификатора.</span><span class="sxs-lookup"><span data-stu-id="d5526-891">The localized display names of the identifier.</span></span>  <br/> |
| [<span data-ttu-id="d5526-892">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-892">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-893">Свойства идентификатора.</span><span class="sxs-lookup"><span data-stu-id="d5526-893">The properties of the identifier.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-894">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-894">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-895">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-895">**Element**</span></span>|<span data-ttu-id="d5526-896">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-896">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-897">Элемент Identifiers в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-897">Identifiers Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/6566cb43-4f9e-9a2e-7ec0-89057d7daacc%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-898">Список идентификаторов для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-898">A list of identifiers of an external content type.</span></span>  <br/> |
   

## <a name="identifiers-element"></a><span data-ttu-id="d5526-899">Элемент Identifiers</span><span class="sxs-lookup"><span data-stu-id="d5526-899">Identifiers element</span></span>
<span data-ttu-id="d5526-900"><a name="bkmk_Identifiers"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-900"></span></span>

<span data-ttu-id="d5526-901">Задает список идентификаторов для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-901">Specifies a list of identifiers of an external content type.</span></span>
  
    
    
 <span data-ttu-id="d5526-902">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-902">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-903">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-903">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Identifiers></Identifiers>
```

<span data-ttu-id="d5526-904">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-904">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-905">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-905">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-906">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-906">None</span></span>
  
    
    
 <span data-ttu-id="d5526-907">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-907">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-908">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-908">**Element**</span></span>|<span data-ttu-id="d5526-909">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-909">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-910">Элемент Identifier в элементе Identifiers (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-910">Identifier Element in Identifiers (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-911">Задает идентификатор.</span><span class="sxs-lookup"><span data-stu-id="d5526-911">Specifies an identifier.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-912">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-912">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-913">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-913">**Element**</span></span>|<span data-ttu-id="d5526-914">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-914">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-915">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-915">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-916">Внешний тип контента, которому принадлежит этот список идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="d5526-916">The external content type that contains this list of identifiers.</span></span>  <br/> |
   

## <a name="interpretation-element"></a><span data-ttu-id="d5526-917">Элемент интерпретации</span><span class="sxs-lookup"><span data-stu-id="d5526-917">Interpretation element</span></span>
<span data-ttu-id="d5526-918"><a name="bkmk_Interpretation"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-918"></span></span>

<span data-ttu-id="d5526-p136">Задает правил, применяемых к данным, хранящимся в структуры данных, представленного **дескриптор типа**. Эти правила обычно указываются изменение значений данных, возвращаемых внешней системы для упрощения их представления в пользовательском интерфейсе. Когда значение получен из внешней системы, заданных правил должны применяться в порядке, в котором они указаны в элементе **Interpretation**. Первое правило должны быть установлены в значение данных, полученных из внешней системы; последовательных правила применяются к значению от приложения предыдущее правило. Когда значение отправляется для внешней системы, заданных правил должны применяться в обратном порядке, в котором они указаны в элементе **Interpretation**. Первое правило должны быть установлены в значение данных, полученных от пользователя. последовательных правила применяются к значению от приложения предыдущее правило.</span><span class="sxs-lookup"><span data-stu-id="d5526-p136">Specifies the rules to apply to the data stored in the data structures represented by a **TypeDescriptor**. These rules are typically specified to change the data values returned by an external system to make it easier to represent them in the user interface. When the data value is obtained from the external system, the specified rules must be applied in the order they are specified in the **Interpretation** element. The first rule must be applied to the data value received from the external system; the consecutive rules apply to the data value that result from the application of the previous rule. When the data value is sent to external system, the specified rules must be applied in the reverse order they are specified in the **Interpretation** element. The first rule must be applied to the data value received from the user; the consecutive rules apply to the data value that result from the application of the previous rule.</span></span>
  
    
    
 <span data-ttu-id="d5526-925">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-925">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-926">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-926">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Interpretation></Interpretation>
```

<span data-ttu-id="d5526-927">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-927">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-928">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-928">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-929">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-929">None</span></span>
  
    
    
 <span data-ttu-id="d5526-930">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-930">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-931">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-931">**Element**</span></span>|<span data-ttu-id="d5526-932">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-932">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-933">Элемент ConvertType в элементе Interpretation (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-933">ConvertType Element in Interpretation (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c474cf2c-b631-f3c9-daf1-f05d3e0d385f%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-934">Элемент **ConvertType**, указывающее, преобразования типа данных в другой тип данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-934">A **ConvertType** element that specifies the conversion of a data type to another data type.</span></span> <br/> |
| [<span data-ttu-id="d5526-935">Элемент NormalizeDateTime в элементе Interpretation (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-935">NormalizeDateTime Element in Interpretation (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/bbae3bfa-0754-d576-2bee-1ac0e8508a57%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-936">Элемент **NormalizeDateTime**, который указывает преобразования представление даты и времени значения, полученные из внешней системы в другое представление.</span><span class="sxs-lookup"><span data-stu-id="d5526-936">A **NormalizeDateTime** element that specifies the conversion of the date and time representation of a value obtained from an external system into another representation.</span></span> <br/> |
|<span data-ttu-id="d5526-937">NormalizeString</span><span class="sxs-lookup"><span data-stu-id="d5526-937">NormalizeString</span></span>  <br/> |<span data-ttu-id="d5526-938">Элемент **NormalizeString**, который указывает преобразования строковое представление значения, полученного из внешней системы в другое представление.</span><span class="sxs-lookup"><span data-stu-id="d5526-938">A **NormalizeString** element that specifies the conversion of the string representation of a value obtained from an external system into another representation.</span></span> <br/> |
   
 <span data-ttu-id="d5526-939">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-939">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-940">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-940">**Element**</span></span>|<span data-ttu-id="d5526-941">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-941">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-942">Элемент TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-942">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-943">Элемент **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-943">The **TypeDescriptor** element.</span></span> <br/> |
   

## <a name="lobsystem-element"></a><span data-ttu-id="d5526-944">Элемент бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="d5526-944">LobSystem element</span></span>
<span data-ttu-id="d5526-945"><a name="bkmk_LobSystem"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-945"></span></span>

<span data-ttu-id="d5526-946">Представляет внешний источник данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-946">Represents an external data source.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-947">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-947">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-948">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-948">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystem Type = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystem>
```

<span data-ttu-id="d5526-949">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-949">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-950">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-950">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-951">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-951">**Attribute**</span></span>|<span data-ttu-id="d5526-952">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-952">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-953">Тип</span><span class="sxs-lookup"><span data-stu-id="d5526-953">Type</span></span>  <br/> |<span data-ttu-id="d5526-954">Тип **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="d5526-954">The type of the **LobSystem**.</span></span>  <br/> <span data-ttu-id="d5526-955">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-955">Required.</span></span>  <br/> <span data-ttu-id="d5526-956">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-956">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-957">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-957">Value</span></span></p></th><th><p><span data-ttu-id="d5526-958">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-958">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-959">База данных</span><span class="sxs-lookup"><span data-stu-id="d5526-959">Database</span></span></p></td><td><p><span data-ttu-id="d5526-960">Представленный внешний источник данных представляет собой базу данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-960">The represented external data source is a database.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-961">DotNetAssembly</span><span class="sxs-lookup"><span data-stu-id="d5526-961">DotNetAssembly</span></span></p></td><td><p><span data-ttu-id="d5526-962">Представленный внешнего источника данных представляют собой набор классов .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d5526-962">The represented external data source is a set of .NET Framework classes.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-963">WCF</span><span class="sxs-lookup"><span data-stu-id="d5526-963">Wcf</span></span></p></td><td><p><span data-ttu-id="d5526-964">Представленный внешнего источника данных является конечной точки службы WCF.</span><span class="sxs-lookup"><span data-stu-id="d5526-964">The represented external data source is a WCF Service endpoint.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-965">WebService</span><span class="sxs-lookup"><span data-stu-id="d5526-965">WebService</span></span></p></td><td><p><span data-ttu-id="d5526-p137">Представленный внешний источник данных  это веб-службы. Это был удален, вместо этого использовать WCF.</span><span class="sxs-lookup"><span data-stu-id="d5526-p137">The represented external data source is a Web service. This has been deprecated, use WCF instead.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-968">Пользовательский сервер</span><span class="sxs-lookup"><span data-stu-id="d5526-968">Custom</span></span></p></td><td><p><span data-ttu-id="d5526-969">Представленный внешний источник данных имеет настраиваемого соединителя, реализованные для управления подключения и для передачи данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-969">The represented external data source has a custom connector implemented to manage the connection and data transfer.</span></span></p></td></tr></tbody></table>|
|<span data-ttu-id="d5526-970">Name</span><span class="sxs-lookup"><span data-stu-id="d5526-970">Name</span></span>  <br/> |<span data-ttu-id="d5526-971">Имя **бизнес-системы**.</span><span class="sxs-lookup"><span data-stu-id="d5526-971">The name of the **LobSystem**.</span></span>  <br/> <span data-ttu-id="d5526-972">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-972">Required.</span></span>  <br/> <span data-ttu-id="d5526-973">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-973">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-974">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-974">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-975">По умолчанию отображаемое имя **бизнес-системы**.</span><span class="sxs-lookup"><span data-stu-id="d5526-975">The default display name of the **LobSystem**.</span></span>  <br/> <span data-ttu-id="d5526-976">Необязательный.</span><span class="sxs-lookup"><span data-stu-id="d5526-976">Optional.</span></span>  <br/> <span data-ttu-id="d5526-977">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-977">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-978">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-978">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-979">Указывает, используются ли часто **бизнес-системы** .</span><span class="sxs-lookup"><span data-stu-id="d5526-979">Specifies whether the **LobSystem** is frequently used.</span></span> <span data-ttu-id="d5526-980">Если часто используемые службы подключения к бизнес-данных (BDC) кэширует **бизнес-системы**.</span><span class="sxs-lookup"><span data-stu-id="d5526-980">If frequently used, Business Data Connectivity (BDC) service caches the **LobSystem**.</span></span>  <br/> <span data-ttu-id="d5526-981">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-981">Optional.</span></span>  <br/> <span data-ttu-id="d5526-982">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-982">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-983">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-983">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-984">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-984">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-985">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-985">**Element**</span></span>|<span data-ttu-id="d5526-986">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-986">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-987">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-987">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-988">Локализованные имена **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="d5526-988">The localized names of the **LobSystem**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-989">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-989">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-990">Задает свойства **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="d5526-990">Specifies the properties of an **LobSystem**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-991">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-991">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-992">Указывает список управления доступом (ACL) **LobSystem**.</span><span class="sxs-lookup"><span data-stu-id="d5526-992">Specifies the access control list (ACL) of an **LobSystem**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-993">Элемент Proxy в объекте LobSystem (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-993">Proxy Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ec2e7b0-156f-ff4a-a87b-fe5764e4875b%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-994">Прокси предоставленного пользователем идентичен, которая будет создана, если этот элемент не был задан.</span><span class="sxs-lookup"><span data-stu-id="d5526-994">Specifies a user-provided proxy that is identical to the one that would be generated if this element was not present.</span></span>  <br/> |
| [<span data-ttu-id="d5526-995">Элемент LobSystemInstances в элементе LobSystem (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-995">LobSystemInstances Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-996">Задает внешнюю систему экземпляров данной внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-996">Specifies the external system instances for this external system.</span></span>  <br/> |
| [<span data-ttu-id="d5526-997">Элемент Entities в LobSystem (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-997">Entities Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/fa121ed1-160a-03c9-df42-851ddc2528d5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-998">Указывает внешних типов контента в этом внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-998">Specifies the external content types in this external system.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-999">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-999">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1000">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1000">**Element**</span></span>|<span data-ttu-id="d5526-1001">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1001">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1002">Элемент LobSystems в модели (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1002">LobSystems Element in Model (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1003">Задает список внешних систем в этой модели.</span><span class="sxs-lookup"><span data-stu-id="d5526-1003">Specifies a list of external systems in this model.</span></span>  <br/> |
   

## <a name="lobsysteminstance-element"></a><span data-ttu-id="d5526-1004">Элемент бизнес-системы</span><span class="sxs-lookup"><span data-stu-id="d5526-1004">LobSystemInstance element</span></span>
<span data-ttu-id="d5526-1005"><a name="bkmk_LobSystemInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1005"></span></span>

<span data-ttu-id="d5526-1006">Задает экземпляр внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1006">Specifies an external system instance.</span></span>
  
    
    
 <span data-ttu-id="d5526-1007">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1007">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1008">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1008">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystemInstance Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </LobSystemInstance>
```

<span data-ttu-id="d5526-1009">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1009">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1010">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1010">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1011">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1011">**Attribute**</span></span>|<span data-ttu-id="d5526-1012">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1012">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1013">Имя</span><span class="sxs-lookup"><span data-stu-id="d5526-1013">Name</span></span>  <br/> |<span data-ttu-id="d5526-1014">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1014">Required.</span></span>  <br/> <span data-ttu-id="d5526-1015">Имя экземпляра внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1015">The name of the external system instance.</span></span>  <br/> <span data-ttu-id="d5526-1016">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1016">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1017">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-1017">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-1018">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1018">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1019">По умолчанию отображаемое имя экземпляра внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1019">The default display name of the external system instance.</span></span>  <br/> <span data-ttu-id="d5526-1020">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1020">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1021">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-1021">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-1022">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1022">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p139">Указывает, используется ли этот экземпляр внешней системы часто. Если параметр имеет значение **true**, Служба подключения к бизнес-данным (BDC) кэширует экземпляра внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-p139">Specifies whether this external system instance is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches the external system instance.  </span></span><br/> <span data-ttu-id="d5526-1025">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1025">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1026">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1026">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1027">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1027">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1028">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1028">**Element**</span></span>|<span data-ttu-id="d5526-1029">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1029">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1030">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1030">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1031">Локализованные имена данного экземпляра внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1031">The localized names of this external system instance.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1032">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1032">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1033">Свойства этого экземпляра внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1033">The properties of this external system instance.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1034">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1034">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1035">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1035">**Element**</span></span>|<span data-ttu-id="d5526-1036">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1036">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1037">Элемент LobSystemInstances в элементе LobSystem (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1037">LobSystemInstances Element in LobSystem (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/122e419a-0497-afdf-1117-a82ab429f3eb%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1038">Список экземпляров внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1038">A list of external system instances.</span></span>  <br/> |
   

## <a name="lobsysteminstances-element"></a><span data-ttu-id="d5526-1039">Элемент LobSystemInstances</span><span class="sxs-lookup"><span data-stu-id="d5526-1039">LobSystemInstances element</span></span>
<span data-ttu-id="d5526-1040"><a name="bkmk_LobSystemInstances"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1040"></span></span>

<span data-ttu-id="d5526-1041">Указывает список экземпляров внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1041">Specifies a list of external system instances.</span></span>
  
    
    
 <span data-ttu-id="d5526-1042">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1042">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1043">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1043">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystemInstances></LobSystemInstances>
```

<span data-ttu-id="d5526-1044">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1044">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1045">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1045">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1046">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1046">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1047">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1047">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1048">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1048">**Element**</span></span>|<span data-ttu-id="d5526-1049">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1049">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1050">Элемент LobSystemInstance в элементе LobSystemInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1050">LobSystemInstance Element in LobSystemInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1051">Экземпляр внешней системы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1051">An external system instance.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1052">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1052">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1053">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1053">**Element**</span></span>|<span data-ttu-id="d5526-1054">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1054">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1055">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1055">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1056">Внешняя система.</span><span class="sxs-lookup"><span data-stu-id="d5526-1056">An external system.</span></span>  <br/> |
   

## <a name="lobsystems-element"></a><span data-ttu-id="d5526-1057">Элемент бизнес-системам</span><span class="sxs-lookup"><span data-stu-id="d5526-1057">LobSystems element</span></span>
<span data-ttu-id="d5526-1058"><a name="bkmk_LobSystems"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1058"></span></span>

<span data-ttu-id="d5526-1059">Указывает список элементов **LobSystem** модели.</span><span class="sxs-lookup"><span data-stu-id="d5526-1059">Specifies a list of **LobSystem** elements of a model.</span></span>
  
    
    
 <span data-ttu-id="d5526-1060">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1060">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1061">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1061">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LobSystems></LobSystems>
```

<span data-ttu-id="d5526-1062">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1062">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1063">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1063">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1064">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1064">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1065">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1065">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1066">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1066">**Element**</span></span>|<span data-ttu-id="d5526-1067">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1067">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1068">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1068">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1069">Элемент **LobSystem**, указывающее, внешней системе.</span><span class="sxs-lookup"><span data-stu-id="d5526-1069">A **LobSystem** element that specifies a external system.</span></span> <br/> |
   
 <span data-ttu-id="d5526-1070">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1070">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1071">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1071">**Element**</span></span>|<span data-ttu-id="d5526-1072">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1072">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1073">Элемент Model (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1073">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1074">Определение приложения (модели BDC).</span><span class="sxs-lookup"><span data-stu-id="d5526-1074">An application definition (BDC model).</span></span>  <br/> |
   

## <a name="localizeddisplayname-element"></a><span data-ttu-id="d5526-1075">Элемент LocalizedDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-1075">LocalizedDisplayName element</span></span>
<span data-ttu-id="d5526-1076"><a name="bkmk_LocalizedDisplayName"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1076"></span></span>

<span data-ttu-id="d5526-1077">Локализованное имя.</span><span class="sxs-lookup"><span data-stu-id="d5526-1077">Specifies a localized name.</span></span>
  
    
    
 <span data-ttu-id="d5526-1078">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1078">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1079">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1079">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LocalizedDisplayName LCID = "Integer"> </LocalizedDisplayName>
```

<span data-ttu-id="d5526-1080">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1080">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1081">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1081">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1082">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1082">**Attribute**</span></span>|<span data-ttu-id="d5526-1083">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1083">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1084">Код языка</span><span class="sxs-lookup"><span data-stu-id="d5526-1084">LCID</span></span>  <br/> |<span data-ttu-id="d5526-1085">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1085">Required.</span></span>  <br/> <span data-ttu-id="d5526-1086">Идентификатор код языка (LCID).</span><span class="sxs-lookup"><span data-stu-id="d5526-1086">The language code identifier (LCID).</span></span>  <br/> <span data-ttu-id="d5526-1087">Тип атрибута: **Integer**</span><span class="sxs-lookup"><span data-stu-id="d5526-1087">Attribute type: **Integer**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1088">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1088">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-1089">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1089">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1090">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1090">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1091">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1091">**Element**</span></span>|<span data-ttu-id="d5526-1092">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1092">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1093">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1093">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1094">Элемент **LocalizedDisplayNames**, содержащий этот **LocalizedDisplayName**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1094">The **LocalizedDisplayNames** element that contains this **LocalizedDisplayName**.</span></span>  <br/> |
   

## <a name="localizeddisplaynames-element"></a><span data-ttu-id="d5526-1095">Элемент LocalizedDisplayNames</span><span class="sxs-lookup"><span data-stu-id="d5526-1095">LocalizedDisplayNames element</span></span>
<span data-ttu-id="d5526-1096"><a name="bkmk_LocalizedDisplayNames"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1096"></span></span>

<span data-ttu-id="d5526-1097">Задает список локализованные имена **MetadataObject**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1097">Specifies a list of localized names of a **MetadataObject**.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-1098">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1098">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1099">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1099">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<LocalizedDisplayNames></LocalizedDisplayNames>
```

<span data-ttu-id="d5526-1100">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1100">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1101">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1101">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1102">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1102">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1103">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1103">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1104">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1104">**Element**</span></span>|<span data-ttu-id="d5526-1105">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1105">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1106">Элемент LocalizedDisplayName в элементе LocalizedDisplayNames (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1106">LocalizedDisplayName Element in LocalizedDisplayNames (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/93fb80ef-6347-b463-da90-4980d872678e%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1107">Локализованное имя.</span><span class="sxs-lookup"><span data-stu-id="d5526-1107">A localized name.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1108">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1108">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1109">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1109">**Element**</span></span>|<span data-ttu-id="d5526-1110">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1110">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1111">Элемент Model (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1111">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1112">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1112">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1113">Элемент LobSystemInstance в элементе LobSystemInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1113">LobSystemInstance Element in LobSystemInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1114">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1114">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1115">Элемент Identifier в элементе Identifiers (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1115">Identifier Element in Identifiers (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1116">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1116">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1117">Элемент FilterDescriptor в элементе FilterDescriptors (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1117">FilterDescriptor Element in FilterDescriptors (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1118">Элемент Parameter в элементе Parameters (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1118">Parameter Element in Parameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1119">Элемент TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1119">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1120">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1120">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1121">Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1121">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1122">Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1122">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1123">Элемент Action в Actions (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1123">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1124">Элемент ActionParameter в элементе ActionParameters (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1124">ActionParameter Element in ActionParameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="metadataobject-element"></a><span data-ttu-id="d5526-1125">Элемент метаданных (MetadataObject)</span><span class="sxs-lookup"><span data-stu-id="d5526-1125">MetadataObject element</span></span>
<span data-ttu-id="d5526-1126"><a name="bkmk_MetadataObject"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1126"></span></span>

 <span data-ttu-id="d5526-1127">**Пространство имен**</span><span class="sxs-lookup"><span data-stu-id="d5526-1127">**Namespace:**</span></span>
  
    
    
 <span data-ttu-id="d5526-1128">**Схема:**</span><span class="sxs-lookup"><span data-stu-id="d5526-1128">**Schema:**</span></span>
  
    
    



```XML

```

<span data-ttu-id="d5526-1129">В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-1129">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1130">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1130">**Attributes**</span></span>
  
    
    
 <span data-ttu-id="d5526-1131">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1131">**Child elements**</span></span>
  
    
    
 <span data-ttu-id="d5526-1132">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1132">**Parent element**</span></span>
  
    
    

## <a name="method-element"></a><span data-ttu-id="d5526-1133">Элемент Method</span><span class="sxs-lookup"><span data-stu-id="d5526-1133">Method element</span></span>
<span data-ttu-id="d5526-1134"><a name="bkmk_Method"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1134"></span></span>

<span data-ttu-id="d5526-1135">Задает метод для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-1135">Specifies a method of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-1136">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1136">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1137">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1137">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Method IsStatic = "Boolean" LobName = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Method>
```

<span data-ttu-id="d5526-1138">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1138">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1139">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1139">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1140">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1140">**Attribute**</span></span>|<span data-ttu-id="d5526-1141">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1141">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1142">IsStatic</span><span class="sxs-lookup"><span data-stu-id="d5526-1142">IsStatic</span></span>  <br/> |<span data-ttu-id="d5526-1143">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1143">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p140">Задает необходимость использования при выполнении этого метода внешнего элемента ( **EntityInstance**) в качестве контекста выполнения. Если присвоено значение **true**, этот метод является статическим и не требует отдельного элемента **EntityInstance** для определения контекста выполнения. Если присвоено значение **false**, метод является методом экземпляра и требует элемент **EntityInstance** для определения контекста выполнения. </span><span class="sxs-lookup"><span data-stu-id="d5526-p140">Specifies whether the execution of this method requires an external item ( **EntityInstance**) to serve as a context for execution. If set to **true**, the method represents a static method and does not require a specific **EntityInstance** to provide context for execution. If set to **false**, the method represents an instance method and requires an **EntityInstance** to provide the context for execution. </span></span><br/> <span data-ttu-id="d5526-1147">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1147">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1148">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1148">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1149">LobName</span><span class="sxs-lookup"><span data-stu-id="d5526-1149">LobName</span></span>  <br/> |<span data-ttu-id="d5526-1150">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1150">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1151">Имя операции внешней системы, которая представлена этим методом.</span><span class="sxs-lookup"><span data-stu-id="d5526-1151">The name of the operation defined in the external system that is represented by this method.</span></span>  <br/> <span data-ttu-id="d5526-1152">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1152">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1153">Имя</span><span class="sxs-lookup"><span data-stu-id="d5526-1153">Name</span></span>  <br/> |<span data-ttu-id="d5526-1154">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1154">Required.</span></span>  <br/> <span data-ttu-id="d5526-1155">Имя метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1155">The name of this method.</span></span>  <br/> <span data-ttu-id="d5526-1156">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1156">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1157">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-1157">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-1158">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1158">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1159">Установленное по умолчанию отображаемое имя метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1159">The default display name of the method.</span></span>  <br/> <span data-ttu-id="d5526-1160">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1160">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1161">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-1161">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-1162">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1162">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p141">Задает частоту использования этого метода. Если установлено значение **true**, в службе Служба подключения к бизнес-данным (BDC) выполняется кэширование этого метода в памяти.</span><span class="sxs-lookup"><span data-stu-id="d5526-p141">Specifies whether this method is used frequently. If set to **true**, Business Data Connectivity (BDC) service caches this method in memory.  </span></span><br/> <span data-ttu-id="d5526-1165">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1165">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1166">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1166">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1167">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1167">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1168">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1168">**Element**</span></span>|<span data-ttu-id="d5526-1169">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1169">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1170">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1170">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1171">Локализованные отображаемые имена метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1171">The localized display names of the method.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1172">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1172">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1173">Свойства метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1173">The properties of the method.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1174">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1174">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1175">Список управления доступом (ACL) для этого метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1175">The access control list (ACL) of this method.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1176">Элемент FilterDescriptors в элементе Method (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1176">FilterDescriptors Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/33d8e418-ddbb-e1ac-b145-836ed9f36e5c%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1177">Дескрипторы фильтра для этого метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1177">The filter descriptors of the method.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1178">Элемент Parameters в методе (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1178">Parameters Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-p142">Параметры метода. Метод содержит не более одного возвращаемого параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-p142">The parameters of the method. A method cannot have more than one return parameter.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1181">Элементы "экземпляры метода" в методе (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1181">MethodInstances Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1182">Экземпляры метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1182">The method instances of the method.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1183">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1183">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1184">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1184">**Element**</span></span>|<span data-ttu-id="d5526-1185">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1185">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1186">Элемент Methods в элементе Entity (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1186">Methods Element in Entity (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/42a24b32-bd97-4067-2e25-681d876d29fd%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1187">Список методов для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-1187">A list of methods of an external content type.</span></span>  <br/> |
   

## <a name="methodinstance-element"></a><span data-ttu-id="d5526-1188">Элемент экземпляра метода</span><span class="sxs-lookup"><span data-stu-id="d5526-1188">MethodInstance element</span></span>
<span data-ttu-id="d5526-1189"><a name="bkmk_MethodInstance"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1189"></span></span>

<span data-ttu-id="d5526-1190">Указывает **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1190">Specifies a **MethodInstance**.</span></span>
  
    
    
 <span data-ttu-id="d5526-1191">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1191">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1192">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1192">**Schema:** BDCMetadata</span></span>
  
    
    
<span data-ttu-id="d5526-1193">Следующих двух случаях в модели BDC привести  [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception%28v=vs.110%29.aspx) во время выполнения:</span><span class="sxs-lookup"><span data-stu-id="d5526-1193">The following two cases in a BDC model result in an  [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception%28v=vs.110%29.aspx) at run time:</span></span>
  
    
    

- <span data-ttu-id="d5526-1194">Два **SpecificFinder** экземпляры метода, которые возвращают один и тот же набор полей.</span><span class="sxs-lookup"><span data-stu-id="d5526-1194">Two **SpecificFinder** method instances that return the same set of fields.</span></span>
    
  
- <span data-ttu-id="d5526-1195">Два **SpecificFinder** экземпляры метода, у которых такое же число полей и использующих одинаковое число полей с другой экземпляр метода, такие как **Finder**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1195">Two **SpecificFinder** method instances that have the same number of fields and that share the same number of fields with another method instance, such as a **Finder**.</span></span>
    
  



```XML
<MethodInstance Type = "Strig" Default = "Boolean" ReturnParameterName = "String" ReturnTypeDescriptorName = "String" ReturnTypeDescriptorLevel = "Integer" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </MethodInstance>
```

<span data-ttu-id="d5526-1196">В разделах ниже приводится описание атрибутов, дочерних и родительских элементов.</span><span class="sxs-lookup"><span data-stu-id="d5526-1196">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1197">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1197">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1198">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1198">**Attribute**</span></span>|<span data-ttu-id="d5526-1199">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1199">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1200">**Type**</span><span class="sxs-lookup"><span data-stu-id="d5526-1200">**Type**</span></span> <br/> |<span data-ttu-id="d5526-1201">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1201">Required.</span></span>  <br/> <span data-ttu-id="d5526-1202">Указывает тип **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1202">Specifies the type of the **MethodInstance**.</span></span>  <br/> <span data-ttu-id="d5526-1203">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-1203">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-1204">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-1204">Value</span></span></p></th><th><p><span data-ttu-id="d5526-1205">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-1205">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-1206">Служба поиска</span><span class="sxs-lookup"><span data-stu-id="d5526-1206">Finder</span></span></p></td><td><p><span data-ttu-id="d5526-p143">Тип **MethodInstance**, который можно вызвать для возврата коллекции ноль или больше **EntityInstances** определенного **Entity**. входные данные **Finder** определяется **FilterDescriptors**, содержащиеся в **Method**, содержащий **Finder**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p143">A type of **MethodInstance** that can be called to return a collection of zero or more **EntityInstances** of a particular **Entity**. **Finder** input is defined by the **FilterDescriptors** that are contained in the **Method** that contains the **Finder**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1209">SpecificFinder</span><span class="sxs-lookup"><span data-stu-id="d5526-1209">SpecificFinder</span></span></p></td><td><p><span data-ttu-id="d5526-p144">Тип **MethodInstance**, который можно вызвать для возврата определенного **EntityInstance** определенных **Entity**, учитывая его **EntityInstanceId**. входные данные **SpecificFinder** определен и упорядоченные по **Identifiers**, связанных с **Entity**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p144">A type of **MethodInstance** that can be called to return a specific **EntityInstance** of a specific **Entity** given its **EntityInstanceId**. **SpecificFinder** input is defined and ordered by the **Identifiers** that are associated with the **Entity**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1212">GenericInvoker</span><span class="sxs-lookup"><span data-stu-id="d5526-1212">GenericInvoker</span></span></p></td><td><p><span data-ttu-id="d5526-p145">Тип **MethodInstance**, который можно вызывать для выполнения определенных задач из внешней системы. **GenericInvoker** ввода и вывода относится только к **Method**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p145">A type of **MethodInstance** that can be called to perform a specific task in an external system. **GenericInvoker** input and output is specific to the **Method**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1215">IdEnumerator</span><span class="sxs-lookup"><span data-stu-id="d5526-1215">IdEnumerator</span></span></p></td><td><p><span data-ttu-id="d5526-p146">Тип **MethodInstance**, который можно вызвать для возврата значения **Field**, которые представляют идентификатор **EntityInstances** определенных **Entity**. Входные данные **IdEnumerator** определяется **FilterDescriptors**, содержащиеся в метод, который содержит **IdEnumerator** для получения списка идентификаторов, которые являются уникальные ключи для каждого объекта, который должен быть доступен для поиска. Этот экземпляр метода позволяет внешним данным поиска в SharePoint Server. </span><span class="sxs-lookup"><span data-stu-id="d5526-p146">A type of **MethodInstance** that can be called to return the **Field** values that represent the identity of **EntityInstances** of a specific **Entity**. The **IdEnumerator** input is defined by the **FilterDescriptors** that are contained in the method that contains the **IdEnumerator** to get the list of IDs, which are the unique keys for each entity that should be searchable. This method instance enables external data search in SharePoint Server.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1219">ChangedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="d5526-1219">ChangedIdEnumerator</span></span></p></td><td><p><span data-ttu-id="d5526-1220">Тип **MethodInstance**, которые могут вызываться для извлечения **EntityInstanceIds** **EntityInstances**, были изменены за внешней системы времени.</span><span class="sxs-lookup"><span data-stu-id="d5526-1220">A type of **MethodInstance** that can be called to retrieve **EntityInstanceIds** of **EntityInstances** that were modified in an external system after a specified time.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1221">DeletedIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="d5526-1221">DeletedIdEnumerator</span></span></p></td><td><p><span data-ttu-id="d5526-1222">Тип **MethodInstance**, которые могут вызываться для извлечения **EntityInstanceIds** **EntityInstances**, были удалены из внешней системы через указанное время.</span><span class="sxs-lookup"><span data-stu-id="d5526-1222">A type of **MethodInstance** that can be called to retrieve **EntityInstanceIds** of **EntityInstances** that were deleted from an external system after the specified time.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1223">Скалярные</span><span class="sxs-lookup"><span data-stu-id="d5526-1223">Scalar</span></span></p></td><td><p><span data-ttu-id="d5526-p147">**MethodInstance**, которое возвращает значение типа single, можно вызвать во внешней системе. Например можно использовать экземпляр скалярные метода для получения всех продаж, сделанных до определенной даты из внешней системы. **Entities** иметь экземпляры скалярные метод ноль или больше. </span><span class="sxs-lookup"><span data-stu-id="d5526-p147">A **MethodInstance** that returns a single value that you can invoke in the external system. For example, you can use a scalar method instance to get the total sales made to date from the external system. **Entities** have zero or more scalar method instances.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1227">AccessChecker</span><span class="sxs-lookup"><span data-stu-id="d5526-1227">AccessChecker</span></span></p></td><td><p><span data-ttu-id="d5526-1228">Тип **MethodInstance**, который можно вызывать для получения разрешений, для которых есть вызывающего участника безопасности для каждого из коллекции **EntityInstances**, выявленные с указанным **EntityInstanceIds**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1228">A type of **MethodInstance** that can be called to retrieve the permissions that the calling security principal has for each of a collection of **EntityInstances** that are identified by the specified **EntityInstanceIds**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1229">Автор</span><span class="sxs-lookup"><span data-stu-id="d5526-1229">Creator</span></span></p></td><td><p><span data-ttu-id="d5526-p148">Тип **MethodInstance**, которые могут вызываться для создания **EntityInstance**. Набор полей, которые необходимы для создания **EntityInstance** называется представление создателя. </span><span class="sxs-lookup"><span data-stu-id="d5526-p148">A type of **MethodInstance** that can be called to create an **EntityInstance**. The set of fields that are required to create the **EntityInstance** is referred to as the Creator View.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1232">Удаления</span><span class="sxs-lookup"><span data-stu-id="d5526-1232">Deleter</span></span></p></td><td><p><span data-ttu-id="d5526-1233">Тип **MethodInstance**, который можно вызывать для удаления **EntityInstance** с указанным **EntityInstanceId**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1233">A type of **MethodInstance** that can be called to delete an **EntityInstance** with a specified **EntityInstanceId**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1234">Обновления</span><span class="sxs-lookup"><span data-stu-id="d5526-1234">Updater</span></span></p></td><td><p><span data-ttu-id="d5526-p149">Тип **MethodInstance**, который можно вызывать для обновления **EntityInstance**, определяемую средством указанного **EntityInstanceId**. Набор полей, которые требуются для обновления **EntityInstance** называется Updater представления. Набор полей, значения которого должен передаваться перед их изменением называется PreUpdater представления. </span><span class="sxs-lookup"><span data-stu-id="d5526-p149">A type of **MethodInstance** that can be called to update an **EntityInstance** identified by a specified **EntityInstanceId**. The set of fields that is required to update the **EntityInstance** is known as the Updater View. The set of fields whose values should be passed before they are changed is known as the PreUpdater View.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1238">StreamAccessor</span><span class="sxs-lookup"><span data-stu-id="d5526-1238">StreamAccessor</span></span></p></td><td><p><span data-ttu-id="d5526-1239">Тип **MethodInstance**, которые могут вызываться для извлечения поля **EntityInstance** в виде поток данных в байтах.</span><span class="sxs-lookup"><span data-stu-id="d5526-1239">A type of **MethodInstance** that can be called to retrieve a field of an **EntityInstance** in the form of a data stream of bytes.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1240">Binarysecuritydescriptoraccessor используется</span><span class="sxs-lookup"><span data-stu-id="d5526-1240">BinarySecurityDescriptorAccessor</span></span></p></td><td><p><span data-ttu-id="d5526-p150">Тип **MethodInstance**, которые могут вызываться для извлечения последовательность байтов из внешней системы. Последовательность байтов системной описывается набор из участников безопасности и связанные разрешения, которые каждого участника безопасности для **EntityInstance** определила с указанным **EntityInstanceId**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p150">A type of **MethodInstance** that can be called to retrieve a sequence of bytes from an external system. The system-specific byte sequence describes a set of security principals and the associated permissions that each security principal has for the **EntityInstance** identified by a specified **EntityInstanceId**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1243">Метод BulkSpecificFinder</span><span class="sxs-lookup"><span data-stu-id="d5526-1243">BulkSpecificFinder</span></span></p></td><td><p><span data-ttu-id="d5526-1244">Тип **MethodInstance**, который можно вызвать для возврата набора определенных **EntityInstances** **Entity**набора соответствующего **EntityInstanceIds**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1244">A type of **MethodInstance** that can be called to return a set of specific **EntityInstances** of an **Entity**, given a set of corresponding **EntityInstanceIds**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1245">BulkIdEnumerator</span><span class="sxs-lookup"><span data-stu-id="d5526-1245">BulkIdEnumerator</span></span></p></td><td><p><span data-ttu-id="d5526-p151">Тип **MethodInstance**, которые могут вызываться для извлечения минимальные сведения о внешние элементы, соответствующие заданным удостоверения. Для оптимизации синхронизации кэширования данных можно использовать этот экземпляр метода. Этот метод должен возвращать только удостоверения и сведения о версии внешних элементов, которые соответствуют заданным **Identities**, который вызывающему приложению можно сравнить с локальной версией для определения наличия изменений и если да, запросить измененных элементов внешнего обновлять кэшированные данные. </span><span class="sxs-lookup"><span data-stu-id="d5526-p151">A type of **MethodInstance** that can be called to retrieve minimal information about the external items corresponding to the given identities. This method instance can be used to optimize synchronization of cached data. This method should return only the identities and version information of the external items that correspond to given **Identities**, which the calling application can compare with the local version to identify if anything has changed, and if so, request the changed external items to update the cached data.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="d5526-1249">**Значение по умолчанию**</span><span class="sxs-lookup"><span data-stu-id="d5526-1249">**Default**</span></span> <br/> |<span data-ttu-id="d5526-1250">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-1250">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1251">Указывает, является ли **MethodInstance** по умолчанию среди всех **MethodInstances**, совместно использующих типа внутри содержащей внешнего типа контента ( **Entity**).</span><span class="sxs-lookup"><span data-stu-id="d5526-1251">Specifies whether the **MethodInstance** is the default among all **MethodInstances** that share its type within the containing external content type ( **Entity**).</span></span>  <br/> <span data-ttu-id="d5526-1252">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-1252">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-1253">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1253">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1254">**ReturnParameterName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1254">**ReturnParameterName**</span></span> <br/> |<span data-ttu-id="d5526-1255">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-1255">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p152">Имя **Parameter**, содержащий **ReturnTypeDescriptor** из **MethodInstance**. Атрибут **Direction** **Parameter** должен быть атрибут **ParameterDirection** со значением **Out**, **InOut**или **Return**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p152">The name of the **Parameter** that contains the **ReturnTypeDescriptor** of the **MethodInstance**. The **Direction** attribute of the **Parameter** must be a **ParameterDirection** attribute with a value of **Out**, **InOut**, or **Return**.  </span></span><br/> <span data-ttu-id="d5526-1258">Этот атрибут должен быть указан для всех типов **MethodInstances** за исключением **GenericInvoker**, **Creator**, **Deleter**и **Updater**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1258">This attribute must be specified for all types of **MethodInstances** except **GenericInvoker**, **Creator**, **Deleter**, and **Updater**.</span></span>  <br/> <span data-ttu-id="d5526-1259">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1259">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1260">**ReturnTypeDescriptorLevel**</span><span class="sxs-lookup"><span data-stu-id="d5526-1260">**ReturnTypeDescriptorLevel**</span></span> <br/> |<span data-ttu-id="d5526-1261">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-1261">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p153">Это рекомендуется. Вместо этого используйте **ReturnTypeDescriptorPath**.</span><span class="sxs-lookup"><span data-stu-id="d5526-p153">This has been deprecated. Use the **ReturnTypeDescriptorPath** instead. </span></span><br/> <span data-ttu-id="d5526-1264">Тип атрибута: **Integer**</span><span class="sxs-lookup"><span data-stu-id="d5526-1264">Attribute type: **Integer**</span></span> <br/> |
|<span data-ttu-id="d5526-1265">**ReturnTypeDescriptorPath**</span><span class="sxs-lookup"><span data-stu-id="d5526-1265">**ReturnTypeDescriptorPath**</span></span> <br/> |<span data-ttu-id="d5526-1266">Необязательное.</span><span class="sxs-lookup"><span data-stu-id="d5526-1266">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1267">Точками путь **TypeDescriptor** связи.</span><span class="sxs-lookup"><span data-stu-id="d5526-1267">The dotted path of the **TypeDescriptor** of the Association.</span></span> <br/> <span data-ttu-id="d5526-1268">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1268">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1269">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-1269">**Name**</span></span> <br/> |<span data-ttu-id="d5526-1270">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1270">Required.</span></span>  <br/> <span data-ttu-id="d5526-1271">Указывает имя **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1271">Specifies the name of the **MethodInstance**.</span></span>  <br/> <span data-ttu-id="d5526-1272">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1272">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1273">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1273">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="d5526-1274">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1274">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1275">Задает отображаемое имя по умолчанию для **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1275">Specifies the default display name for the **MethodInstance**.</span></span>  <br/> <span data-ttu-id="d5526-1276">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1276">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1277">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="d5526-1277">**IsCached**</span></span> <br/> |<span data-ttu-id="d5526-1278">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1278">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1279">Указывает, используется ли **MethodInstance** часто.</span><span class="sxs-lookup"><span data-stu-id="d5526-1279">Specifies whether the **MethodInstance** is used frequently.</span></span> <br/> <span data-ttu-id="d5526-1280">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1280">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1281">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1281">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1282">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1282">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1283">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1283">**Element**</span></span>|<span data-ttu-id="d5526-1284">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1284">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1285">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1285">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1286">Локализованные отображаемые имена **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1286">The localized display names of the **MethodInstance**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1287">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1287">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1288">Свойства **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1288">The properties of the **MethodInstance**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1289">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1289">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1290">Списки управления доступом (ACL) из **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1290">The access control lists (ACLs) of the **MethodInstance**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1291">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1291">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1292">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1292">**Element**</span></span>|<span data-ttu-id="d5526-1293">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1293">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1294">Элементы "экземпляры метода" в методе (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1294">MethodInstances Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/dae3aeae-e72a-0b52-1348-f5e5cd31109f%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1295">Элемент **MethodInstances**, содержащий этот **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1295">The **MethodInstances** element that contains this **MethodInstance**.</span></span>  <br/> |
   

## <a name="methodinstances-element"></a><span data-ttu-id="d5526-1296">Элемент "экземпляр метода"</span><span class="sxs-lookup"><span data-stu-id="d5526-1296">MethodInstances element</span></span>
<span data-ttu-id="d5526-1297"><a name="bkmk_MethodInstances"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1297"></span></span>

<span data-ttu-id="d5526-1298">Указывает список связей и экземпляров метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1298">Specifies a list of associations and method instances of a method.</span></span>
  
    
    
 <span data-ttu-id="d5526-1299">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1299">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1300">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1300">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<MethodInstances></MethodInstances>
```

<span data-ttu-id="d5526-1301">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1301">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1302">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1302">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1303">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1303">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1304">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1304">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1305">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1305">**Element**</span></span>|<span data-ttu-id="d5526-1306">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1306">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1307">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1307">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1308">Связь.</span><span class="sxs-lookup"><span data-stu-id="d5526-1308">An association.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1309">Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1309">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1310">Экземпляр метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1310">A method instance.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1311">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1311">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1312">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1312">**Element**</span></span>|<span data-ttu-id="d5526-1313">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1313">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1314">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1314">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1315">Метод, которому принадлежит этот экземпляр метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1315">The method that this method instance belongs to.</span></span>  <br/> |
   

## <a name="methods-element"></a><span data-ttu-id="d5526-1316">Элемент Methods</span><span class="sxs-lookup"><span data-stu-id="d5526-1316">Methods element</span></span>
<span data-ttu-id="d5526-1317"><a name="bkmk_Methods"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1317"></span></span>

<span data-ttu-id="d5526-1318">Задает список методов для внешнего типа контента.</span><span class="sxs-lookup"><span data-stu-id="d5526-1318">Specifies a list of methods of an external content type.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-1319">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1319">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1320">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1320">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Methods></Methods>
```

<span data-ttu-id="d5526-1321">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1321">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1322">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1322">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1323">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1323">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1324">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1324">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1325">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1325">**Element**</span></span>|<span data-ttu-id="d5526-1326">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1326">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1327">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1327">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1328">Задает метод.</span><span class="sxs-lookup"><span data-stu-id="d5526-1328">Specifies a method.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1329">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1329">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1330">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1330">**Element**</span></span>|<span data-ttu-id="d5526-1331">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1331">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1332">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1332">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1333">Внешний тип контента, которому принадлежит этот список методов.</span><span class="sxs-lookup"><span data-stu-id="d5526-1333">The external content type that this list of methods belongs to.</span></span>  <br/> |
   

## <a name="model-element"></a><span data-ttu-id="d5526-1334">Элемент модели</span><span class="sxs-lookup"><span data-stu-id="d5526-1334">Model element</span></span>
<span data-ttu-id="d5526-1335"><a name="bkmk_Model"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1335"></span></span>

<span data-ttu-id="d5526-p154">Задает корневой элемент, представляющий определения приложения. Модели определять внешние типы контента, содержащиеся в внешних приложений.</span><span class="sxs-lookup"><span data-stu-id="d5526-p154">Specifies the root element that represents an application definition. Models define external content types that are contained by external applications.</span></span> 
  
    
    
 <span data-ttu-id="d5526-1338">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1338">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1339">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1339">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Model Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Model>
```

<span data-ttu-id="d5526-1340">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1340">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1341">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1341">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1342">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1342">**Attribute**</span></span>|<span data-ttu-id="d5526-1343">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1343">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1344">Имя</span><span class="sxs-lookup"><span data-stu-id="d5526-1344">Name</span></span>  <br/> |<span data-ttu-id="d5526-1345">Имя **Model**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1345">The name of the **Model**.</span></span>  <br/> <span data-ttu-id="d5526-1346">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1346">Required.</span></span>  <br/> <span data-ttu-id="d5526-1347">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1347">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1348">DefaultDisplayName</span><span class="sxs-lookup"><span data-stu-id="d5526-1348">DefaultDisplayName</span></span>  <br/> |<span data-ttu-id="d5526-1349">Отображаемое имя по умолчанию **Model**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1349">The default display name of the **Model**.</span></span>  <br/> <span data-ttu-id="d5526-1350">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1350">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1351">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1351">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1352">IsCached</span><span class="sxs-lookup"><span data-stu-id="d5526-1352">IsCached</span></span>  <br/> |<span data-ttu-id="d5526-p155">Указывает, используется ли **Model** часто. Если установлено значение **true**, **Model** кэшируется с Служба подключения к бизнес-данным (BDC). </span><span class="sxs-lookup"><span data-stu-id="d5526-p155">Specifies whether the **Model** is used frequently. If this is set to **true**, then the **Model** is cached by the Business Data Connectivity (BDC) service. </span></span><br/> <span data-ttu-id="d5526-1355">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1355">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1356">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1356">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1357">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1357">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1358">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1358">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1359">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1359">**Element**</span></span>|<span data-ttu-id="d5526-1360">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1360">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1361">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1361">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1362">Локализованные имена **Model**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1362">The localized names of the **Model**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1363">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1363">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1364">Свойства **Model**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1364">The properties of the **Model**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1365">Элемент AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1365">AccessControlList Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/b7f97740-5d2c-f91a-1028-10e2890d4a99%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1366">Список управления доступом (ACL) из **Model**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1366">The access control list (ACL) of the **Model**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1367">Элемент LobSystems в модели (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1367">LobSystems Element in Model (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d9bf0ca9-fb79-e3a5-cc84-9510d93798cb%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1368">**LobSystems**, содержащиеся в этом **Model**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1368">The **LobSystems** contained inside this **Model**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1369">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1369">**Parent element**</span></span>
  
    
    
<span data-ttu-id="d5526-1370">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1370">None</span></span>
  
    
    

## <a name="normalizedatetime-element"></a><span data-ttu-id="d5526-1371">Элемент NormalizeDateTime</span><span class="sxs-lookup"><span data-stu-id="d5526-1371">NormalizeDateTime element</span></span>
<span data-ttu-id="d5526-1372"><a name="bkmk_NormalizeDateTime"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1372"></span></span>

<span data-ttu-id="d5526-p156">Задает правило, которое используется для преобразования представления значения даты и времени в другое представление. Например это правило можно указать преобразование значения, представленного в формате UTC в локальный часовой пояс.</span><span class="sxs-lookup"><span data-stu-id="d5526-p156">Specifies the rule used to convert the representation of a date and time value to another representation. For example, this rule can specify converting a value represented in Coordinated Universal Time (UTC) into a local time zone.</span></span> 
  
    
    
 <span data-ttu-id="d5526-1375">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1375">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1376">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1376">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<NormalizeDateTime LobDateTimeMode = "String"> </NormalizeDateTime>
```

<span data-ttu-id="d5526-1377">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1377">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1378">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1378">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1379">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1379">**Attribute**</span></span>|<span data-ttu-id="d5526-1380">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1380">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1381">**LobDateTimeMode**</span><span class="sxs-lookup"><span data-stu-id="d5526-1381">**LobDateTimeMode**</span></span> <br/> |<span data-ttu-id="d5526-1382">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1382">Required.</span></span>  <br/> <span data-ttu-id="d5526-1383">Указывает преобразования для применения.</span><span class="sxs-lookup"><span data-stu-id="d5526-1383">Specifies the conversion to apply.</span></span>  <br/> <span data-ttu-id="d5526-1384">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-1384">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-1385">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-1385">Value</span></span></p></th><th><p><span data-ttu-id="d5526-1386">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-1386">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-1387">UTC</span><span class="sxs-lookup"><span data-stu-id="d5526-1387">UTC</span></span></p></td><td><p><span data-ttu-id="d5526-p157">Значение, полученных из внешней системы  в формате UTC (время по Гринвичу). Если получено значение **Local**, он преобразуется в формате UTC. BDC отправляет UTC во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="d5526-p157">The value that is received from the external system is UTC (Coordinated Universal Time). If the value received is **Local**, it is converted to UTC. BDC sends UTC to the external system.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1391">Local</span><span class="sxs-lookup"><span data-stu-id="d5526-1391">Local</span></span></p></td><td><p><span data-ttu-id="d5526-p158">Значение, полученных из внешней системы: **Local**. Если значение, полученных из внешней системы **Local**, его будут преобразованы в формате UTC. BDC отправляет **Local** во внешней системе. </span><span class="sxs-lookup"><span data-stu-id="d5526-p158">The value received from the external system is **Local**. If the value received from the external system is **Local**, then it will be converted to UTC. BDC sends **Local** to the external system.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1395">Не определено.</span><span class="sxs-lookup"><span data-stu-id="d5526-1395">Unspecified</span></span></p></td><td><p><span data-ttu-id="d5526-p159">Значение, отправленные с внешней системы не указан тип. BDC предполагается, что значение задается в формате UTC с помощью перезаписи вид быть UTC. BDC отправляет UTC значения как не указан тип во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="d5526-p159">The value sent by the external system has Unspecified kind. BDC assumes the value is in UTC by overwriting the kind to be UTC. BDC sends UTC values as Unspecified kind to the external system.</span></span></p></td></tr></tbody></table>
|
   
 <span data-ttu-id="d5526-1399">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1399">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-1400">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1400">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1401">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1401">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1402">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1402">**Element**</span></span>|<span data-ttu-id="d5526-1403">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1403">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1404">Элемент Interpretation в элементе TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1404">Interpretation Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1405">Элемент **Interpretation**, указывающее, правил, применяемых к данным, которые хранятся в структуры данных, представленного **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1405">An **Interpretation** element that specifies the rules to apply to the data that is stored in the data structures represented by a **TypeDescriptor**.</span></span>  <br/> |
   

## <a name="normalizestring-element"></a><span data-ttu-id="d5526-1406">Элемент NormalizeString</span><span class="sxs-lookup"><span data-stu-id="d5526-1406">NormalizeString element</span></span>
<span data-ttu-id="d5526-1407"><a name="bkmk_NormalizeString"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1407"></span></span>

<span data-ttu-id="d5526-1408">Задает параметр для метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1408">Specifies a parameter of a method.</span></span>
  
    
    
 <span data-ttu-id="d5526-1409">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1409">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1410">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1410">**Schema:** BDCMetadata</span></span>
  
    
    



```XML

```

<span data-ttu-id="d5526-1411">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1411">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1412">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1412">**Attributes**</span></span>
  
    
    
 <span data-ttu-id="d5526-1413">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1413">**Child elements**</span></span>
  
    
    
 <span data-ttu-id="d5526-1414">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1414">**Parent element**</span></span>
  
    
    

## <a name="parameter-element"></a><span data-ttu-id="d5526-1415">Элемент параметра</span><span class="sxs-lookup"><span data-stu-id="d5526-1415">Parameter element</span></span>
<span data-ttu-id="d5526-1416"><a name="bkmk_Parameter"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1416"></span></span>

<span data-ttu-id="d5526-1417">Задает параметр для метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1417">Specifies a parameter of a method.</span></span>
  
    
    
 <span data-ttu-id="d5526-1418">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1418">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1419">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1419">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Parameter Direction = "String" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </Parameter>
```

<span data-ttu-id="d5526-1420">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1420">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1421">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1421">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1422">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1422">**Attribute**</span></span>|<span data-ttu-id="d5526-1423">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1423">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1424">Direction</span><span class="sxs-lookup"><span data-stu-id="d5526-1424">Direction</span></span>  <br/> |<span data-ttu-id="d5526-1425">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1425">Required.</span></span>  <br/> <span data-ttu-id="d5526-1426">Направление параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1426">The direction of the parameter.</span></span>  <br/> <span data-ttu-id="d5526-1427">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-1427">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-1428">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-1428">Value</span></span></p></th><th><p><span data-ttu-id="d5526-1429">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-1429">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-1430">Поддержка IPv6</span><span class="sxs-lookup"><span data-stu-id="d5526-1430">In</span></span></p></td><td><p><span data-ttu-id="d5526-1431">Представленный **Parameter** является входным параметром.</span><span class="sxs-lookup"><span data-stu-id="d5526-1431">The represented **Parameter** is an input parameter.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1432">Выходной</span><span class="sxs-lookup"><span data-stu-id="d5526-1432">Out</span></span></p></td><td><p><span data-ttu-id="d5526-1433">Параметр представленного является выходного параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1433">The represented parameter is an output parameter.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1434">Вход</span><span class="sxs-lookup"><span data-stu-id="d5526-1434">InOut</span></span></p></td><td><p><span data-ttu-id="d5526-1435">Параметр представленного является входных и выходных параметров.</span><span class="sxs-lookup"><span data-stu-id="d5526-1435">The represented parameter is an input and output parameter.</span></span> <span data-ttu-id="d5526-1436">В C# они соответствуют «**ссылка**».</span><span class="sxs-lookup"><span data-stu-id="d5526-1436">In C#, these correspond to "**ref**".</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1437">Возврат</span><span class="sxs-lookup"><span data-stu-id="d5526-1437">Return</span></span></p></td><td><p><span data-ttu-id="d5526-1438">Параметр представленного является возвращаемого параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1438">The represented parameter is a return parameter.</span></span></p></td></tr></tbody></table>
|<span data-ttu-id="d5526-1439">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-1439">**Name**</span></span> <br/> |<span data-ttu-id="d5526-1440">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1440">Required.</span></span>  <br/> <span data-ttu-id="d5526-1441">Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1441">The name of the parameter.</span></span>  <br/> <span data-ttu-id="d5526-1442">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1442">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1443">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1443">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="d5526-1444">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1444">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1445">Отображаемое имя по умолчанию для параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1445">The default display name of the parameter.</span></span>  <br/> <span data-ttu-id="d5526-1446">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1446">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1447">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="d5526-1447">**IsCached**</span></span> <br/> |<span data-ttu-id="d5526-1448">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1448">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1449">Указывает, используется ли **Parameter** часто.</span><span class="sxs-lookup"><span data-stu-id="d5526-1449">Specifies whether the **Parameter** is used frequently.</span></span> <br/> <span data-ttu-id="d5526-1450">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1450">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1451">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1451">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1452">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1452">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1453">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1453">**Element**</span></span>|<span data-ttu-id="d5526-1454">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1454">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1455">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1455">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1456">Локализованные имена параметр.</span><span class="sxs-lookup"><span data-stu-id="d5526-1456">The localized names of the parameter.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1457">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1457">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1458">Свойства параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1458">The properties of the parameter.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1459">Дескриптор типа</span><span class="sxs-lookup"><span data-stu-id="d5526-1459">TypeDescriptor</span></span>](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> |<span data-ttu-id="d5526-1460">Корневой дескриптор типа параметра.</span><span class="sxs-lookup"><span data-stu-id="d5526-1460">The root type descriptor of the parameter.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1461">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1461">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1462">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1462">**Element**</span></span>|<span data-ttu-id="d5526-1463">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1463">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1464">Элемент Parameters в методе (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1464">Parameters Element in Method (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/343f4c25-e122-1a4c-2b80-bb8f25e3cc82%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1465">Элемент **Parameters**, содержащий этот параметр.</span><span class="sxs-lookup"><span data-stu-id="d5526-1465">The **Parameters** element that contains this parameter.</span></span> <br/> |
   

## <a name="parameters-element"></a><span data-ttu-id="d5526-1466">Параметры элемента</span><span class="sxs-lookup"><span data-stu-id="d5526-1466">Parameters element</span></span>
<span data-ttu-id="d5526-1467"><a name="bkmk_Parameters"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1467"></span></span>

<span data-ttu-id="d5526-1468">Указывает список параметров метода.</span><span class="sxs-lookup"><span data-stu-id="d5526-1468">Specifies a list of parameters of a method.</span></span>
  
    
    

  
    
    
 <span data-ttu-id="d5526-1469">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1469">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1470">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1470">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Parameters></Parameters>
```

<span data-ttu-id="d5526-1471">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1471">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1472">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1472">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1473">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1473">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1474">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1474">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1475">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1475">**Element**</span></span>|<span data-ttu-id="d5526-1476">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1476">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1477">Элемент Parameter в элементе Parameters (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1477">Parameter Element in Parameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1478">Параметр.</span><span class="sxs-lookup"><span data-stu-id="d5526-1478">A parameter.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1479">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1479">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1480">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1480">**Element**</span></span>|<span data-ttu-id="d5526-1481">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1481">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1482">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1482">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1483">Метод, к которой принадлежит этих параметров.</span><span class="sxs-lookup"><span data-stu-id="d5526-1483">The method these parameters belong to.</span></span>  <br/> |
   

## <a name="properties-element"></a><span data-ttu-id="d5526-1484">Элемент Properties</span><span class="sxs-lookup"><span data-stu-id="d5526-1484">Properties element</span></span>
<span data-ttu-id="d5526-1485"><a name="bkmk_Properties"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1485"></span></span>

<span data-ttu-id="d5526-1486">Указывает список свойств объекта метаданных.</span><span class="sxs-lookup"><span data-stu-id="d5526-1486">Specifies a list of properties of a metadata object.</span></span>
  
    
    
 <span data-ttu-id="d5526-1487">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1487">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1488">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1488">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Properties></Properties>
```

<span data-ttu-id="d5526-1489">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1489">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1490">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1490">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1491">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1491">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1492">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1492">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1493">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1493">**Element**</span></span>|<span data-ttu-id="d5526-1494">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1494">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1495">Элемент Property в свойствах (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1495">Property Element in Properties (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/2e6e8d5d-ef3b-c536-f3d1-ad2039b92c24%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1496">Задает свойство.</span><span class="sxs-lookup"><span data-stu-id="d5526-1496">Specifies a property.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1497">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1497">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1498">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1498">**Element**</span></span>|<span data-ttu-id="d5526-1499">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1499">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1500">Элемент Model (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1500">Model Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d7823090-b20d-2c96-c359-081c055d0e65%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1501">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1501">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1502">Элемент LobSystemInstance в элементе LobSystemInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1502">LobSystemInstance Element in LobSystemInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a0c37891-ef4f-58af-445c-5ff4d5ad6cef%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1503">Элемент Entity в элементе Entities (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1503">Entity Element in Entities (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/a8455bc4-12d8-85e0-146e-5d1d8579e1f5%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1504">Элемент Identifier в элементе Identifiers (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1504">Identifier Element in Identifiers (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/c4abf09b-10b6-0007-9214-35d5fe675be7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1505">Элемент Method в элементе Methods (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1505">Method Element in Methods (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/70e87a9e-4959-0a7b-3f37-ddec36473ff4%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1506">Элемент FilterDescriptor в элементе FilterDescriptors (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1506">FilterDescriptor Element in FilterDescriptors (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/8ce0a852-38f9-75d2-8258-27c57418f53c%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1507">Элемент Parameter в элементе Parameters (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1507">Parameter Element in Parameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/811cad0b-ba71-8be0-0765-3e0dec18a0d3%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1508">Дескриптор типа</span><span class="sxs-lookup"><span data-stu-id="d5526-1508">TypeDescriptor</span></span>](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
| [<span data-ttu-id="d5526-1509">Элемент TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1509">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1510">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1510">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1511">Элемент MethodInstance в элементе MethodInstances (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1511">MethodInstance Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/577ff9d0-706b-be7d-af5b-883e137cada8%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1512">Элемент AssociationGroup в элементе AssociationGroups (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1512">AssociationGroup Element in AssociationGroups (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/db30622e-3c2b-2735-9360-a702196cbcff%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1513">Элемент Action в Actions (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1513">Action Element in Actions (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/f58b96c0-77a8-69d3-8710-fff03d4970b9%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1514">Элемент ActionParameter в элементе ActionParameters (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1514">ActionParameter Element in ActionParameters (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/1f5fa96a-1bff-f007-984d-a644cbbb2648%28Office.15%29.aspx) <br/> ||
   

## <a name="property-element"></a><span data-ttu-id="d5526-1515">Элемент Property</span><span class="sxs-lookup"><span data-stu-id="d5526-1515">Property element</span></span>
<span data-ttu-id="d5526-1516"><a name="bkmk_Property"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1516"></span></span>

<span data-ttu-id="d5526-1517">Указывает имя и тип свойства объекта метаданных.</span><span class="sxs-lookup"><span data-stu-id="d5526-1517">Specifies the name and type of a property of a metadata object.</span></span>
  
    
    
 <span data-ttu-id="d5526-1518">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1518">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1519">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1519">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Property Name = "String" Type = "String"> </Property>
```

<span data-ttu-id="d5526-1520">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1520">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1521">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1521">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1522">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1522">**Attribute**</span></span>|<span data-ttu-id="d5526-1523">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1523">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1524">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-1524">**Name**</span></span> <br/> |<span data-ttu-id="d5526-1525">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1525">Required.</span></span>  <br/> <span data-ttu-id="d5526-1526">Задает имя свойства.</span><span class="sxs-lookup"><span data-stu-id="d5526-1526">Specifies the name of the property.</span></span>  <br/> <span data-ttu-id="d5526-1527">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1527">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1528">**Type**</span><span class="sxs-lookup"><span data-stu-id="d5526-1528">**Type**</span></span> <br/> |<span data-ttu-id="d5526-1529">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1529">Required.</span></span>  <br/> <span data-ttu-id="d5526-1530">Указывает тип данных свойства.</span><span class="sxs-lookup"><span data-stu-id="d5526-1530">Specifies data type of the property.</span></span>  <br/> <span data-ttu-id="d5526-1531">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1531">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1532">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1532">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-1533">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1533">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1534">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1534">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1535">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1535">**Element**</span></span>|<span data-ttu-id="d5526-1536">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1536">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1537">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1537">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1538">Элемент **Properties**, содержащий это свойство.</span><span class="sxs-lookup"><span data-stu-id="d5526-1538">The **Properties** element that contains this property.</span></span> <br/> |
   

## <a name="proxy-element"></a><span data-ttu-id="d5526-1539">Элемент прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="d5526-1539">Proxy element</span></span>
<span data-ttu-id="d5526-1540"><a name="bkmk_Proxy"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1540"></span></span>

<span data-ttu-id="d5526-p161">Прокси предоставленного пользователем идентичен, которая будет создана, если этот элемент не был задан. Используется для повышения производительности путем удаления нагрузка создания прокси-сервера. Чтобы указать настраиваемые бизнес-логики, который подключается к внешней системы, необходимо использовать сборки подключения .NET тип внешних систем.</span><span class="sxs-lookup"><span data-stu-id="d5526-p161">Specifies a user-provided proxy that is identical to the one that would be generated if this element was not present. This is used to improve performance by removing the proxy generation overhead. To specify custom business logic that connects to an external system, .NET Connectivity Assembly type external systems must be used.</span></span>
  
    
    
 <span data-ttu-id="d5526-1544">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1544">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1545">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1545">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Proxy></Proxy>
```

<span data-ttu-id="d5526-1546">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1546">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1547">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1547">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1548">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1548">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1549">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1549">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-1550">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1550">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1551">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1551">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1552">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1552">**Element**</span></span>|<span data-ttu-id="d5526-1553">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1553">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1554">Элемент LobSystem в LobSystems (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1554">LobSystem Element in LobSystems (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/d4e58d7d-a628-8093-97fe-7c3136e8f6f2%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1555">Элемент **LobSystem**, к которому применяется этот прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="d5526-1555">The **LobSystem** element that this proxy applies to.</span></span> <br/> |
   

## <a name="right-element"></a><span data-ttu-id="d5526-1556">Элемент вправо</span><span class="sxs-lookup"><span data-stu-id="d5526-1556">Right element</span></span>
<span data-ttu-id="d5526-1557"><a name="bkmk_Right"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1557"></span></span>

<span data-ttu-id="d5526-1558">Разрешение доступа к одной записи управления доступом (ACE).</span><span class="sxs-lookup"><span data-stu-id="d5526-1558">Specifies a single access permission for an access control entry (ACE).</span></span>
  
    
    
 <span data-ttu-id="d5526-1559">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1559">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1560">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1560">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<Right BdcRight = "String"> </Right>
```

<span data-ttu-id="d5526-1561">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1561">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1562">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1562">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1563">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1563">**Attribute**</span></span>|<span data-ttu-id="d5526-1564">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1564">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1565">BdcRight</span><span class="sxs-lookup"><span data-stu-id="d5526-1565">BdcRight</span></span>  <br/> |<span data-ttu-id="d5526-1566">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1566">Required.</span></span>  <br/> <span data-ttu-id="d5526-1567">Разрешения, доступные для участника безопасности, удерживая вправо.</span><span class="sxs-lookup"><span data-stu-id="d5526-1567">The permission available to the security principal holding the right.</span></span>  <br/> <span data-ttu-id="d5526-1568">В следующей таблице приведен список возможных значений этого атрибута.</span><span class="sxs-lookup"><span data-stu-id="d5526-1568">The following table lists the possible values for this attribute.</span></span>  <br/> <table width="50%" cellspacing="2" cellpadding="5" frame="lhs"><thead><tr><th><p><span data-ttu-id="d5526-1569">Значение</span><span class="sxs-lookup"><span data-stu-id="d5526-1569">Value</span></span></p></th><th><p><span data-ttu-id="d5526-1570">Описание</span><span class="sxs-lookup"><span data-stu-id="d5526-1570">Description</span></span></p></th></tr></thead><tbody><tr><td><p><span data-ttu-id="d5526-1571">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1571">None</span></span></p></td><td><p><span data-ttu-id="d5526-1572">Нет разрешений.</span><span class="sxs-lookup"><span data-stu-id="d5526-1572">No permissions.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1573">Выполнение</span><span class="sxs-lookup"><span data-stu-id="d5526-1573">Execute</span></span></p></td><td><p><span data-ttu-id="d5526-1574">Участник безопасности, представленного имеет разрешения на вызов **MethodInstance**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1574">The represented security principal has the permission to invoke a **MethodInstance**.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1575">Изменить</span><span class="sxs-lookup"><span data-stu-id="d5526-1575">Edit</span></span></p></td><td><p><span data-ttu-id="d5526-1576">Представленный участника безопасности имеет разрешение на изменение атрибутов объекта метаданных или ее отношения с другими объектами метаданных.</span><span class="sxs-lookup"><span data-stu-id="d5526-1576">The represented security principal has permission to change the attributes of a metadata object or its relationship to other metadata objects.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1577">SetPermissions</span><span class="sxs-lookup"><span data-stu-id="d5526-1577">SetPermissions</span></span></p></td><td><p><span data-ttu-id="d5526-1578">Представленный участника безопасности имеет разрешение на изменение набор разрешений для объекта метаданных.</span><span class="sxs-lookup"><span data-stu-id="d5526-1578">The represented security principal has permission to change the set of permissions for a metadata object.</span></span></p></td></tr><tr><td><p><span data-ttu-id="d5526-1579">SelectableInClients</span><span class="sxs-lookup"><span data-stu-id="d5526-1579">SelectableInClients</span></span></p></td><td><p><span data-ttu-id="d5526-p162">Участника безопасности, представленного имеет разрешение на выбор эти права ссылается на объект метаданных. Если пользователь не имеет этого разрешения, объект метаданных не должна быть доступно для выбора.</span><span class="sxs-lookup"><span data-stu-id="d5526-p162">The represented security principal has permission to select the metadata object this right refers to. If a user does not have this permission, the metadata object should not be selectable.</span></span></p></td></tr></tbody></table>
|
   
 <span data-ttu-id="d5526-1582">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1582">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-1583">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1583">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1584">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1584">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1585">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1585">**Element**</span></span>|<span data-ttu-id="d5526-1586">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1586">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1587">Элемент AccessControlEntry в AccessControlList (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1587">AccessControlEntry Element in AccessControlList (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/85e24489-0a6b-dfda-fb03-474fe7b0d947%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1588">Элемент **AccessControlEntry**, содержащий эти права.</span><span class="sxs-lookup"><span data-stu-id="d5526-1588">The **AccessControlEntry** element that contains this right.</span></span> <br/> |
   

## <a name="sourceentity-element"></a><span data-ttu-id="d5526-1589">Элемент SourceEntity</span><span class="sxs-lookup"><span data-stu-id="d5526-1589">SourceEntity element</span></span>
<span data-ttu-id="d5526-1590"><a name="bkmk_SourceEntity"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1590"></span></span>

<span data-ttu-id="d5526-1591">Указывает источник внешнего типа контента из **Association**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1591">Specifies a source external content type of an **Association**.</span></span>
  
    
    
 <span data-ttu-id="d5526-1592">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1592">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1593">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1593">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<SourceEntity Namespace = "String" Name = "String"> </SourceEntity>
```

<span data-ttu-id="d5526-1594">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1594">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1595">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1595">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1596">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1596">**Attribute**</span></span>|<span data-ttu-id="d5526-1597">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1597">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1598">Пространство имен</span><span class="sxs-lookup"><span data-stu-id="d5526-1598">Namespace</span></span>  <br/> |<span data-ttu-id="d5526-1599">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1599">Required.</span></span>  <br/> <span data-ttu-id="d5526-1600">Пространство имен внешнего типа контента, который является источником **Association**, содержащий данный элемент.</span><span class="sxs-lookup"><span data-stu-id="d5526-1600">The namespace of the external content type that is the source of the **Association** that contains this element.</span></span> <br/> <span data-ttu-id="d5526-1601">Тип атрибута: String</span><span class="sxs-lookup"><span data-stu-id="d5526-1601">Attribute type: String</span></span>  <br/> |
|<span data-ttu-id="d5526-1602">Имя</span><span class="sxs-lookup"><span data-stu-id="d5526-1602">Name</span></span>  <br/> |<span data-ttu-id="d5526-1603">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1603">Required.</span></span>  <br/> <span data-ttu-id="d5526-1604">Имя внешнего типа контента, который является источником **Association**, содержащий данный элемент.</span><span class="sxs-lookup"><span data-stu-id="d5526-1604">The name of the external content type that is the source of the **Association** that contains this element.</span></span> <br/> <span data-ttu-id="d5526-1605">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1605">Attribute type: **String**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1606">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1606">**Child elements**</span></span>
  
    
    
<span data-ttu-id="d5526-1607">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1607">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1608">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1608">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1609">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1609">**Element**</span></span>|<span data-ttu-id="d5526-1610">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1610">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1611">Элемент Association в элементе MethodInstances (схемы BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1611">Association Element in MethodInstances (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9659a1f5-1b12-03ef-f9e3-5c9904cc5dd0%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1612">**Association**, содержащий данный элемент.</span><span class="sxs-lookup"><span data-stu-id="d5526-1612">The **Association** that contains this element.</span></span> <br/> |
   

## <a name="typedescriptor-element"></a><span data-ttu-id="d5526-1613">Элемент дескриптор типа</span><span class="sxs-lookup"><span data-stu-id="d5526-1613">TypeDescriptor element</span></span>
<span data-ttu-id="d5526-1614"><a name="bkmk_TypeDescriptor"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1614"></span></span>

<span data-ttu-id="d5526-1615">Указывает **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1615">Specifies a **TypeDescriptor**.</span></span>
  
    
    
 <span data-ttu-id="d5526-1616">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1616">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1617">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1617">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<TypeDescriptor TypeName = "String" LobName = "String" IdentifierEntityNamespace = "String" IdentifierEntityName = "String" IdentifierName = "String" ForeignIdentifierAssociationName = "String" ForeignIdentifierAssociationEntityName = "String" ForeignIdentifierAssociationEntityNamespace = "String" AssociatedFilter = "String" IsCollection = "Boolean" ReadOnly = "Boolean" CreatorField = "Boolean" UpdaterField = "Boolean" PreUpdaterField = "Boolean" Significant = "Boolean" Name = "String" DefaultDisplayName = "String" IsCached = "Boolean"> </TypeDescriptor>
```

<span data-ttu-id="d5526-1618">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1618">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1619">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1619">**Attributes**</span></span>
  
    
    


|<span data-ttu-id="d5526-1620">**Атрибут**</span><span class="sxs-lookup"><span data-stu-id="d5526-1620">**Attribute**</span></span>|<span data-ttu-id="d5526-1621">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1621">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="d5526-1622">**Имя типа**</span><span class="sxs-lookup"><span data-stu-id="d5526-1622">**TypeName**</span></span> <br/> |<span data-ttu-id="d5526-1623">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1623">Required.</span></span>  <br/> <span data-ttu-id="d5526-1624">Идентификатор типа данных, представленного **TypeDescriptor**структуры данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-1624">The identifier of the data type of the data structure that is represented by the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="d5526-1625">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1625">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1626">**LobName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1626">**LobName**</span></span> <br/> |<span data-ttu-id="d5526-1627">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1627">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p163">Структура данных, представленного **TypeDescriptor**. По умолчанию значение этого атрибута  имя **TypeDescriptor**. Например с именем «CN1A» структура данных системы бизнес-(LOB) можно представить в виде **TypeDescriptor** атрибутом **Name**, равное "Customer Name", если атрибут **LobName** этот **TypeDescriptor** равен "CN1A". </span><span class="sxs-lookup"><span data-stu-id="d5526-p163">The data structure that is represented by the **TypeDescriptor**. The default value of this attribute is the name of the **TypeDescriptor**. For example, a line-of-business (LOB) system data structure named "CN1A" can be represented by a **TypeDescriptor** with **Name** attribute equal to "Customer Name", if the **LobName** attribute of this **TypeDescriptor** is equal to "CN1A". </span></span><br/> <span data-ttu-id="d5526-1631">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1631">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1632">**IdentifierEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="d5526-1632">**IdentifierEntityNamespace**</span></span> <br/> |<span data-ttu-id="d5526-1633">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1633">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p164">Пространство имен внешнего типа контента, который содержит идентификатор, который ссылается на **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Identifier**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **IdentifierEntityName** и **IdentifierName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  это пространство имен внешнего типа контента, который содержит метод, содержащий параметр, содержащий **TypeDescriptor**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p164">The namespace of the external content type that contains the identifier that the **TypeDescriptor** references. If the **TypeDescriptor** does not reference an **Identifier**, this attribute must not be present. When this attribute is present, the **IdentifierEntityName** and **IdentifierName** attributes must also be present. The default value of this attribute is the namespace of the external content type that contains the method containing the parameter that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="d5526-1638">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1638">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1639">**Identifierentityname выполните следующие действия**</span><span class="sxs-lookup"><span data-stu-id="d5526-1639">**IdentifierEntityName**</span></span> <br/> |<span data-ttu-id="d5526-1640">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1640">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p165">Имя **Entity**, содержащий **Identifier**, который ссылается c **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Identifier**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **IdentifierEntityNamespace** и **IdentifierName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  имя **Entity**, содержащий **Method**, содержащий **Parameter**, содержащий **TypeDescriptor**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p165">The name of the **Entity** that contains the **Identifier** that the c **TypeDescriptor** references. If the **TypeDescriptor** does not reference an **Identifier**, this attribute must not be present. When this attribute is present, the **IdentifierEntityNamespace** and **IdentifierName** attributes must also be present. The default value of this attribute is the name of the **Entity** that contains the **Method** containing the **Parameter** that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="d5526-1645">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1645">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1646">**IdentifierName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1646">**IdentifierName**</span></span> <br/> |<span data-ttu-id="d5526-1647">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1647">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p166">Имя **Identifier** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Identifier**, этот атрибут не должна быть указан. </span><span class="sxs-lookup"><span data-stu-id="d5526-p166">The name of the **Identifier** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Identifier**, this attribute must not be present.  </span></span><br/> <span data-ttu-id="d5526-1650">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1650">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1651">**ForeignIdentifierAssociationName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1651">**ForeignIdentifierAssociationName**</span></span> <br/> |<span data-ttu-id="d5526-1652">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1652">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p167">Имя **Association** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Association**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, атрибут **IdentifierName** также должен быть указан. Атрибут **ForeignIdentifierAssociationName** должен быть указан при **Identifier**, на который ссылается этот **TypeDescriptor** относится к **Association**и **Identifier** находится исходный **Entity** из **Association**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p167">The name of the **Association** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Association**, this attribute must not be present. When this attribute is present, the **IdentifierName** attribute must also be present. The **ForeignIdentifierAssociationName** attribute must be specified when the **Identifier** referenced by this **TypeDescriptor** is related to an **Association**, and the **Identifier** is contained by a source **Entity** of the **Association**.  </span></span><br/> <span data-ttu-id="d5526-1657">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1657">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1658">**ForeignIdentifierAssociationEntityName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1658">**ForeignIdentifierAssociationEntityName**</span></span> <br/> |<span data-ttu-id="d5526-1659">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1659">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p168">Имя **Entity**, содержащий **Association** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Association**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **ForeignIdentifierAssociationEntityNamespace** и **ForeignIdentifierAssociationName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  имя **Entity**, содержащий **Method**, содержащий **Parameter**, содержащий **TypeDescriptor**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p168">The name of the **Entity** that contains the **Association** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Association**, this attribute must not be present. When this attribute is present, the **ForeignIdentifierAssociationEntityNamespace** and **ForeignIdentifierAssociationName** attributes must also be present. The default value of this attribute is the name of the **Entity** that contains the **Method** containing the **Parameter** that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="d5526-1664">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1664">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1665">**ForeignIdentifierAssociationEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="d5526-1665">**ForeignIdentifierAssociationEntityNamespace**</span></span> <br/> |<span data-ttu-id="d5526-1666">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1666">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p169">Пространство имен **Entity**, содержащий **Association** ссылается **TypeDescriptor**. Если **TypeDescriptor** не ссылаются на **Association**, этот атрибут не должна быть указан. Если этот атрибут отсутствует, **ForeignIdentifierAssociationEntityName** и **ForeignIdentifierAssociationName** атрибуты должны присутствовать. По умолчанию значение этого атрибута  это пространство имен **Entity**, содержащий **Method**, содержащий **Parameter**, содержащий **TypeDescriptor**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p169">The namespace of the **Entity** that contains the **Association** referenced by the **TypeDescriptor**. If the **TypeDescriptor** does not reference an **Association**, this attribute must not be present. When this attribute is present, the **ForeignIdentifierAssociationEntityName** and **ForeignIdentifierAssociationName** attributes must also be present. The default value of this attribute is the namespace of the **Entity** that contains the **Method** containing the **Parameter** that contains the **TypeDescriptor**.  </span></span><br/> <span data-ttu-id="d5526-1671">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1671">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1672">**AssociatedFilter**</span><span class="sxs-lookup"><span data-stu-id="d5526-1672">**AssociatedFilter**</span></span> <br/> |<span data-ttu-id="d5526-1673">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1673">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p170">Имя **FilterDescriptor**, связанный с **TypeDescriptor**. Если **TypeDescriptor** не связан с **FilterDescriptor** этого атрибута должно отсутствовать. </span><span class="sxs-lookup"><span data-stu-id="d5526-p170">The name of a **FilterDescriptor** that is associated with the **TypeDescriptor**. If the **TypeDescriptor** is not associated with a **FilterDescriptor** this attribute must not be present. </span></span><br/> <span data-ttu-id="d5526-1676">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1676">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1677">**IsCollection**</span><span class="sxs-lookup"><span data-stu-id="d5526-1677">**IsCollection**</span></span> <br/> |<span data-ttu-id="d5526-1678">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1678">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1679">Указывает, представляет ли **TypeDescriptor** структуру данных single или коллекцию структур данных.</span><span class="sxs-lookup"><span data-stu-id="d5526-1679">Specifies whether the **TypeDescriptor** represents a single data structure or a collection of data structures.</span></span> <br/> <span data-ttu-id="d5526-1680">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-1680">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-1681">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1681">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1682">**Только для чтения**</span><span class="sxs-lookup"><span data-stu-id="d5526-1682">**ReadOnly**</span></span> <br/> |<span data-ttu-id="d5526-1683">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1683">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p171">Указывает, можно ли изменить данные, хранящиеся в структуре данных, представленного **TypeDescriptor**. Этот атрибут не должно быть указано, если значение атрибута **Direction** **Parameter**, содержащий **TypeDescriptor**  "In". </span><span class="sxs-lookup"><span data-stu-id="d5526-p171">Specifies whether the data stored by the data structure represented by the **TypeDescriptor** can be modified. This attribute must not be specified if the value of the **Direction** attribute of the **Parameter** that contains the **TypeDescriptor** is "In". </span></span><br/> <span data-ttu-id="d5526-1686">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-1686">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-1687">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1687">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1688">**CreatorField**</span><span class="sxs-lookup"><span data-stu-id="d5526-1688">**CreatorField**</span></span> <br/> |<span data-ttu-id="d5526-1689">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1689">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1690">Указывает, представляет ли поле для **MethodInstances** типа **Creator**, содержащихся в **Method**, содержащий **Parameter**, содержащий **TypeDescriptor** **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1690">Specifies whether the **TypeDescriptor** represents a field for **MethodInstances** of type **Creator** that are contained by the **Method** that contains the **Parameter** containing the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="d5526-1691">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-1691">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-1692">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1692">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1693">**UpdaterField**</span><span class="sxs-lookup"><span data-stu-id="d5526-1693">**UpdaterField**</span></span> <br/> |<span data-ttu-id="d5526-1694">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1694">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p172">Указывает, представляет ли поле для **MethodInstances** типа **Updater**, содержащихся в **Method**, содержащий **Parameter**, содержащий **TypeDescriptor** **TypeDescriptor**. Если этот атрибут является атрибутом **PreUpdaterField** не должен быть указан. </span><span class="sxs-lookup"><span data-stu-id="d5526-p172">Specifies whether the **TypeDescriptor** represents a field for **MethodInstances** of type **Updater** that are contained by the **Method** that contains the **Parameter** containing the **TypeDescriptor**. When this attribute is specified, a **PreUpdaterField** attribute must not be specified. </span></span><br/> <span data-ttu-id="d5526-1697">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-1697">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-1698">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1698">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1699">**PreUpdaterField**</span><span class="sxs-lookup"><span data-stu-id="d5526-1699">**PreUpdaterField**</span></span> <br/> |<span data-ttu-id="d5526-1700">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1700">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p173">Указывает, является ли структура данных, представленного **TypeDescriptor** хранит последнее значение данных, полученных из внешней системы поля для **MethodInstances** типа **Updater**. Если этот атрибут является атрибутом **UpdaterField** не должен быть указан. </span><span class="sxs-lookup"><span data-stu-id="d5526-p173">Specifies whether data structure represented by the **TypeDescriptor** stores the latest data value received from the external system of a field for **MethodInstances** of type **Updater**. When this attribute is specified, a **UpdaterField** attribute must not be specified. </span></span><br/> <span data-ttu-id="d5526-1703">Значение по умолчанию: **false**</span><span class="sxs-lookup"><span data-stu-id="d5526-1703">Default value: **false**</span></span> <br/> <span data-ttu-id="d5526-1704">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1704">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1705">**Significant**</span><span class="sxs-lookup"><span data-stu-id="d5526-1705">**Significant**</span></span> <br/> |<span data-ttu-id="d5526-1706">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1706">Optional.</span></span>  <br/> <span data-ttu-id="d5526-p174">Указывает, включены ли значения, хранящиеся в структуре данных, представленного в этом **TypeDescriptor** в расчете хэш-код или для сравнения значения, хранящиеся в структуры данных. Например, **TypeDescriptor**, представляющее фамилии клиента учитывается при определении ли записи был изменен и поэтому он имеет значение, тогда как **TypeDescriptor**, представляющий дату, на котором последние записи клиента изменения обычно не учитывается для определения, были ли изменены записи, и его не значительные. </span><span class="sxs-lookup"><span data-stu-id="d5526-p174">Specifies whether values stored by the data structure represented by this **TypeDescriptor** are included in calculating a hash code or comparing values stored in the data structures. For example, a **TypeDescriptor** representing a customer's last name is taken into account when determining whether a record has been modified, and so it is significant, whereas the **TypeDescriptor** representing the date on which the customer record is last modified typically is not taken into account to determine whether a record has been modified, and so it is not significant. </span></span><br/> <span data-ttu-id="d5526-1709">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1709">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1710">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1710">Attribute type: **Boolean**</span></span> <br/> |
|<span data-ttu-id="d5526-1711">**Name**</span><span class="sxs-lookup"><span data-stu-id="d5526-1711">**Name**</span></span> <br/> |<span data-ttu-id="d5526-1712">Обязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1712">Required.</span></span>  <br/> <span data-ttu-id="d5526-1713">Имя **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1713">The name of the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="d5526-1714">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1714">Attribute type: **String**</span></span> <br/> <span data-ttu-id="d5526-1715">**Примечание**: имя **дескриптор типа** не должно содержать специальные символы для косой черты («/»), period (".»), или открывающей скобки (» [»).</span><span class="sxs-lookup"><span data-stu-id="d5526-1715">**Note**: The name of a **TypeDescriptor** should not contain the special characters for forward slash ("/"), period ("."), or opening bracket ("[").</span></span>          |
|<span data-ttu-id="d5526-1716">**DefaultDisplayName**</span><span class="sxs-lookup"><span data-stu-id="d5526-1716">**DefaultDisplayName**</span></span> <br/> |<span data-ttu-id="d5526-1717">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1717">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1718">Отображаемое имя **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1718">The display name of the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="d5526-1719">Тип атрибута: **String**</span><span class="sxs-lookup"><span data-stu-id="d5526-1719">Attribute type: **String**</span></span> <br/> |
|<span data-ttu-id="d5526-1720">**IsCached**</span><span class="sxs-lookup"><span data-stu-id="d5526-1720">**IsCached**</span></span> <br/> |<span data-ttu-id="d5526-1721">Необязательный атрибут.</span><span class="sxs-lookup"><span data-stu-id="d5526-1721">Optional.</span></span>  <br/> <span data-ttu-id="d5526-1722">Указывает, используется ли **TypeDescriptor** часто.</span><span class="sxs-lookup"><span data-stu-id="d5526-1722">Specifies whether the **TypeDescriptor** is used frequently.</span></span> <br/> <span data-ttu-id="d5526-1723">Значение по умолчанию: **true**</span><span class="sxs-lookup"><span data-stu-id="d5526-1723">Default value: **true**</span></span> <br/> <span data-ttu-id="d5526-1724">Тип атрибута: **Boolean**</span><span class="sxs-lookup"><span data-stu-id="d5526-1724">Attribute type: **Boolean**</span></span> <br/> |
   
 <span data-ttu-id="d5526-1725">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1725">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1726">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1726">**Element**</span></span>|<span data-ttu-id="d5526-1727">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1727">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1728">Элемент LocalizedDisplayNames в MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1728">LocalizedDisplayNames Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/3202aecf-f98f-20cb-1fdd-f3a054cb24aa%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1729">Локализованные имена **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1729">The localized names of the **TypeDescriptor**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1730">Элемент Properties в элементе MetadataObject (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1730">Properties Element in MetadataObject (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/9901904f-96ee-0cbb-64a9-c2aad9d72128%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1731">Свойства **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1731">The properties of the **TypeDescriptor**.</span></span>  <br/> <span data-ttu-id="d5526-p175">Если **TypeDescriptor** имеет тип **System.String**, элемент **Properties** может содержать **Property** из типа **System.Int32** с атрибутом **Name**, равным **Size**. Значение **Property** указывает ожидаемый Максимальная длина строки значения структуры данных, описываемые в этом **TypeDescriptor**. </span><span class="sxs-lookup"><span data-stu-id="d5526-p175">When the **TypeDescriptor** is of type **System.String**, the **Properties** element can contain a **Property** of type **System.Int32** with the **Name** attribute set to **Size**. The value of the **Property** specifies the expected maximum string length of the value of the data structure described by this **TypeDescriptor**.  </span></span><br/> |
| [<span data-ttu-id="d5526-1734">Элемент Interpretation в элементе TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1734">Interpretation Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/730f9590-ab40-85b8-eb97-8fd9d8e33c8a%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1735">Правила для данных, сохраненных в структуре данных, представленного **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1735">The rules for the data stored by the data structure represented by the **TypeDescriptor**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1736">Элемент DefaultValues в элементе TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1736">DefaultValues Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/635295d1-0f85-6308-976b-d0cb483dece6%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1737">Значения по умолчанию **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1737">The default values of the **TypeDescriptor**.</span></span>  <br/> |
| [<span data-ttu-id="d5526-1738">Элемент TypeDescriptors в TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1738">TypeDescriptors Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1739">Дочерние **TypeDescriptors** **TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1739">The child **TypeDescriptors** of the **TypeDescriptor**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1740">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1740">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1741">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1741">**Element**</span></span>|<span data-ttu-id="d5526-1742">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1742">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1743">Элемент TypeDescriptors в TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1743">TypeDescriptors Element in TypeDescriptor (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/322b2d3f-c92d-3c24-9f22-07b56396275b%28Office.15%29.aspx)||
   

## <a name="typedescriptors-element"></a><span data-ttu-id="d5526-1744">Элемент дескрипторы типов</span><span class="sxs-lookup"><span data-stu-id="d5526-1744">TypeDescriptors element</span></span>
<span data-ttu-id="d5526-1745"><a name="bkmk_TypeDescriptors"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1745"></span></span>

<span data-ttu-id="d5526-1746">Задает список **TypeDescriptors** родительский объект TypeDescriptor.</span><span class="sxs-lookup"><span data-stu-id="d5526-1746">Specifies a list of **TypeDescriptors** of a parent TypeDescriptor.</span></span>
  
    
    
 <span data-ttu-id="d5526-1747">**Пространство имен:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span><span class="sxs-lookup"><span data-stu-id="d5526-1747">**Namespace:** `http://schemas.microsoft.com/windows/2007/BusinessDataCatalog`</span></span>
  
    
    
 <span data-ttu-id="d5526-1748">**Схема:** BDCMetadata</span><span class="sxs-lookup"><span data-stu-id="d5526-1748">**Schema:** BDCMetadata</span></span>
  
    
    



```XML
<TypeDescriptors></TypeDescriptors>
```

<span data-ttu-id="d5526-1749">В следующем разделе описываются атрибуты, дочерние элементы и родительские элементы.</span><span class="sxs-lookup"><span data-stu-id="d5526-1749">The following sections describe attributes, child elements, and parent elements.</span></span>
  
    
    
 <span data-ttu-id="d5526-1750">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="d5526-1750">**Attributes**</span></span>
  
    
    
<span data-ttu-id="d5526-1751">Нет</span><span class="sxs-lookup"><span data-stu-id="d5526-1751">None</span></span>
  
    
    
 <span data-ttu-id="d5526-1752">**Дочерние элементы**</span><span class="sxs-lookup"><span data-stu-id="d5526-1752">**Child elements**</span></span>
  
    
    


|<span data-ttu-id="d5526-1753">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1753">**Element**</span></span>|<span data-ttu-id="d5526-1754">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1754">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1755">Элемент TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1755">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> |<span data-ttu-id="d5526-1756">**TypeDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="d5526-1756">A **TypeDescriptor**.</span></span>  <br/> |
   
 <span data-ttu-id="d5526-1757">**Родительский элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1757">**Parent element**</span></span>
  
    
    


|<span data-ttu-id="d5526-1758">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="d5526-1758">**Element**</span></span>|<span data-ttu-id="d5526-1759">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d5526-1759">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="d5526-1760">Элемент TypeDescriptor (схема BDCMetadata)</span><span class="sxs-lookup"><span data-stu-id="d5526-1760">TypeDescriptor Element (BDCMetadata Schema)</span></span>](http://msdn.microsoft.com/library/ae423de8-c13b-aea5-d47b-17ef786fb5a7%28Office.15%29.aspx) <br/> ||
| [<span data-ttu-id="d5526-1761">Дескриптор типа</span><span class="sxs-lookup"><span data-stu-id="d5526-1761">TypeDescriptor</span></span>](http://msdn.microsoft.com/library/30e38d7f-af18-20ec-45ab-0bece071ce67.aspx) <br/> ||
   

## <a name="see-also"></a><span data-ttu-id="d5526-1762">См. также</span><span class="sxs-lookup"><span data-stu-id="d5526-1762">See also</span></span>
<span data-ttu-id="d5526-1763"><a name="bkmk_Addres"> </a></span><span class="sxs-lookup"><span data-stu-id="d5526-1763"></span></span>


-  [<span data-ttu-id="d5526-1764">Изменения в схеме модели BDC для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1764">Changes in the BDC model schema for SharePoint</span></span>](changes-in-the-bdc-model-schema-for-sharepoint.md)
    
  
-  [<span data-ttu-id="d5526-1765">Внешние типы контента в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1765">External content types in SharePoint</span></span>](external-content-types-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d5526-1766">Начало работы с помощью клиентской объектной модели с внешними данными в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1766">Get started using the client object model with external data in SharePoint</span></span>](get-started-using-the-client-object-model-with-external-data-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d5526-1767">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1767">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d5526-1768">Новые возможности служб Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1768">What's new in Business Connectivity Services in SharePoint</span></span>](what-s-new-in-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d5526-1769">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1769">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="d5526-1770">Справочник по программистов Business Connectivity Services для SharePoint</span><span class="sxs-lookup"><span data-stu-id="d5526-1770">Business Connectivity Services programmers reference for SharePoint</span></span>](business-connectivity-services-programmers-reference-for-sharepoint.md)
    
  
