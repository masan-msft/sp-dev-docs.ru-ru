---
title: "Настройка результатов поиска в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 1b30f6df-643a-4570-ae5c-d3d8df5609b8
ms.openlocfilehash: e14e8f47074b9277167b7049c0d9ddb1d335416c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="customizing-search-results-in-sharepoint"></a><span data-ttu-id="d0209-102">Настройка результатов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d0209-102">Customizing search results in SharePoint</span></span>
<span data-ttu-id="d0209-103">Узнайте, как для группировки схожих элементов или удаление повторяющихся элементов в списке поиска результатов в SharePoint, эти результаты можно представить в виде краткие и для чтения.</span><span class="sxs-lookup"><span data-stu-id="d0209-103">Learn how to group similar items or remove duplicate items in a search result set in SharePoint so you can display these results in a concise, readable way.</span></span>
<span data-ttu-id="d0209-104">В результатах поиска группировки сворачивает два или более аналогичные элементов в результате поиска со значением для их отображения удобства чтения для пользователя.</span><span class="sxs-lookup"><span data-stu-id="d0209-104">In search results, grouping collapses two or more similar items in a search result set to make their display more readable for a user.</span></span> <span data-ttu-id="d0209-105">Удаления дубликатов из результатов поиска является частью группировки, где элементов, которые являются идентичными или почти идентичен удаляются из набора результатов.</span><span class="sxs-lookup"><span data-stu-id="d0209-105">Duplicate removal of search results is a part of grouping, where items that are identical or nearly identical are removed from the result set.</span></span> <span data-ttu-id="d0209-106">В зависимости от настроек, заданных администратором SharePoint пользователь может иметь возможность более поздней версии развернуть набора результатов поиска и просмотреть результаты для отдельных, которые были свернуты.</span><span class="sxs-lookup"><span data-stu-id="d0209-106">Depending on the settings set by the SharePoint administrator, the user might be able to expand the search result set later and see the individual results that were collapsed.</span></span>
  
    
    

<span data-ttu-id="d0209-107">Ниже приведены примеры способов группы результатов поиска:</span><span class="sxs-lookup"><span data-stu-id="d0209-107">The following are examples of ways to group search results:</span></span>
- <span data-ttu-id="d0209-108">Дублируется определение, где почти идентичен документы удаляются из набора результатов.</span><span class="sxs-lookup"><span data-stu-id="d0209-108">Duplicate detection, where nearly identical documents are removed from the result set.</span></span>
    
  
- <span data-ttu-id="d0209-109">Сайт свертывание, где показано наиболее подходящих элементов, обнаруженных в каждом сайте в наборе результатов.</span><span class="sxs-lookup"><span data-stu-id="d0209-109">Site collapsing, where only the most relevant item found in each site is shown in the result set.</span></span>
    
  
- <span data-ttu-id="d0209-110">Набор документов свертывание, где отображается только один сбора данных для каждой библиотеки документов в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d0209-110">Document set collapsing, where only one hit is displayed for each document library in SharePoint.</span></span>
    
  
<span data-ttu-id="d0209-111">Можно указать критерии Свертывание или повторений программным путем с помощью следующих свойств  [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) в объектной модели запросов:</span><span class="sxs-lookup"><span data-stu-id="d0209-111">You can specify the criteria for collapsing or duplicate trimming programmatically by using the following  [KeywordQuery](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx) properties within the Query object model:</span></span>
-  [<span data-ttu-id="d0209-112">CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="d0209-112">CollapseSpecification</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.CollapseSpecification.aspx)
    
  
-  [<span data-ttu-id="d0209-113">TrimDuplicates</span><span class="sxs-lookup"><span data-stu-id="d0209-113">TrimDuplicates</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.Query.TrimDuplicates.aspx)
    
  
-  [<span data-ttu-id="d0209-114">TrimDuplicatesOnProperty</span><span class="sxs-lookup"><span data-stu-id="d0209-114">TrimDuplicatesOnProperty</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesOnProperty.aspx)
    
  
-  [<span data-ttu-id="d0209-115">TrimDuplicatesKeepCount</span><span class="sxs-lookup"><span data-stu-id="d0209-115">TrimDuplicatesKeepCount</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesKeepCount.aspx)
    
  
-  [<span data-ttu-id="d0209-116">TrimDuplicatesIncludeId</span><span class="sxs-lookup"><span data-stu-id="d0209-116">TrimDuplicatesIncludeId</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.TrimDuplicatesIncludeId.aspx)
    
  

## <a name="collapse-similar-search-results-using-the-collapsespecification-property"></a><span data-ttu-id="d0209-117">Сворачивание аналогичное результатов поиска с помощью свойства CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="d0209-117">Collapse similar search results using the CollapseSpecification property</span></span>
<span data-ttu-id="d0209-118"><a name="bk_collapse_specification"> </a></span><span class="sxs-lookup"><span data-stu-id="d0209-118"></span></span>

<span data-ttu-id="d0209-119">Принимает свойства **CollapseSpecification**, параметр _Spec_, который может содержать несколько полей, разделенных запятыми или пробела, который вычисляется вместе задать критерии, используемые для сворачивания.</span><span class="sxs-lookup"><span data-stu-id="d0209-119">The **CollapseSpecification** property takes a _Spec_ parameter that can contain multiple fields separated either by a comma or a space, which evaluated together specify a set of criteria used for collapsing.</span></span>
  
    
    
 <span data-ttu-id="d0209-120">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-120">**Syntax**</span></span>
  
    
    
 `CollapseSpecification = Spec`
  
    
    
<span data-ttu-id="d0209-121">В следующей таблице приведены поля параметр  _Spec_.</span><span class="sxs-lookup"><span data-stu-id="d0209-121">The following table lists the fields of the  _Spec_ parameter.</span></span>
  
    
    

<span data-ttu-id="d0209-122">**В таблице 1. Поля со спецификациями параметров**</span><span class="sxs-lookup"><span data-stu-id="d0209-122">**Table 1. Spec parameter fields**</span></span>


|<span data-ttu-id="d0209-123">**Элемент в параметре**</span><span class="sxs-lookup"><span data-stu-id="d0209-123">**Element in parameter**</span></span>|<span data-ttu-id="d0209-124">**Описание**</span><span class="sxs-lookup"><span data-stu-id="d0209-124">**Description**</span></span>|
|:-----|:-----|
| <span data-ttu-id="d0209-125">_Spec_</span><span class="sxs-lookup"><span data-stu-id="d0209-125">_Spec_</span></span> <br/> | `Subspec(<space>Subspec)*` <br/> |
| <span data-ttu-id="d0209-126">_Subspec_</span><span class="sxs-lookup"><span data-stu-id="d0209-126">_Subspec_</span></span> <br/> | `Prop(','Prop)*[':'Dups]` <br/> |
| <span data-ttu-id="d0209-127">_Prop_</span><span class="sxs-lookup"><span data-stu-id="d0209-127">_Prop_</span></span> <br/> |<span data-ttu-id="d0209-p102">Управляемое свойство или псевдонима управляемого свойства.  _Prop_ без учета регистра. Управляемое свойство, которое должно быть возможность запроса и возможность сортировки или refineable.</span><span class="sxs-lookup"><span data-stu-id="d0209-p102">A valid managed property or an alias of a managed property.  _Prop_ is case-insensitive. The managed property must be queryable and either sortable or refineable. </span></span><br/> |
| <span data-ttu-id="d0209-131">_Dups_</span><span class="sxs-lookup"><span data-stu-id="d0209-131">_Dups_</span></span> <br/> |<span data-ttu-id="d0209-p103">Целое число, указывающее количество элементов для сохранения. Значение по умолчанию  1.</span><span class="sxs-lookup"><span data-stu-id="d0209-p103">An integer specifying the number of items to retain. The default value is 1.</span></span>  <br/> |
| _<space>_ <br/> |<span data-ttu-id="d0209-134">Свойства объединяются с помощью оператора **OR**.</span><span class="sxs-lookup"><span data-stu-id="d0209-134">Properties are combined by using the **OR** operator.</span></span> <br/> |
| <span data-ttu-id="d0209-135">_,_</span><span class="sxs-lookup"><span data-stu-id="d0209-135"></span></span> <br/> |<span data-ttu-id="d0209-136">Свойства объединяются с помощью оператора **AND**.</span><span class="sxs-lookup"><span data-stu-id="d0209-136">Properties are combined by using the **AND** operator.</span></span> <br/> |
| _*_ <br/> |<span data-ttu-id="d0209-137">Указывает число элементов.</span><span class="sxs-lookup"><span data-stu-id="d0209-137">Indicates more items.</span></span>  <br/> |
| <span data-ttu-id="d0209-138">_() or []_</span><span class="sxs-lookup"><span data-stu-id="d0209-138">_() or []_</span></span> <br/> |<span data-ttu-id="d0209-139">Указывает дополнительные элементы.</span><span class="sxs-lookup"><span data-stu-id="d0209-139">Indicates optional items.</span></span>  <br/> |
   
<span data-ttu-id="d0209-p104">Если поля в  _Spec_, разделенных запятыми, поля объединяются с помощью оператора **AND**. При выполнении всех указанных полей свернуты элементы.</span><span class="sxs-lookup"><span data-stu-id="d0209-p104">If the fields in  _Spec_ are separated by commas, the fields are combined by using the **AND** operator. If all of the specified fields are matched, the items are collapsed.</span></span>
  
    
    
<span data-ttu-id="d0209-p105">С другой стороны Если поля в  _Spec_, разделенных пробелами, поля (или _Subspecs_) объединяются с помощью расширения, включая оператор **AND** и **OR** оператор. Например выражение, например `Category:3 Product:2` во внутреннем преобразуется в следующие выражения `(Category AND Product) OR (Category)` со счетчиком для каждого из них; Поэтому не более двух предыдущее и три последних. Элементы свернуты при выполнении некоторых из указанного поля.</span><span class="sxs-lookup"><span data-stu-id="d0209-p105">In contrast, if the fields in  _Spec_ are separated by spaces, the fields (or _Subspecs_) are combined by using an expansion that includes both the **AND** operator and **OR** operator. For example, an expression such as `Category:3 Product:2` is internally transformed to the following expression `(Category AND Product) OR (Category)` with a counter for each; hence a maximum of two of the former and three of the latter. Items are collapsed if some of the specified fields are matched.</span></span>
  
    
    

### <a name="examples-of-using-collapsespecification"></a><span data-ttu-id="d0209-145">Примеры использования CollapseSpecification</span><span class="sxs-lookup"><span data-stu-id="d0209-145">Examples of using CollapseSpecification</span></span>

<span data-ttu-id="d0209-p106">В следующей таблице показаны каталог продукции компании Contoso. Далее задайте примеры использования этого каталога, чтобы показать, как работает свойство **CollapseSpecification**.</span><span class="sxs-lookup"><span data-stu-id="d0209-p106">The following table shows a product catalog from the Contoso company. The next set of examples use this catalog to show how the **CollapseSpecification** property works.</span></span>
  
    
    


|<span data-ttu-id="d0209-148">**Категория**</span><span class="sxs-lookup"><span data-stu-id="d0209-148">**Category**</span></span>|<span data-ttu-id="d0209-149">**Продукт**</span><span class="sxs-lookup"><span data-stu-id="d0209-149">**Product**</span></span>|<span data-ttu-id="d0209-150">**Variant**</span><span class="sxs-lookup"><span data-stu-id="d0209-150">**Variant**</span></span>|<span data-ttu-id="d0209-151">**Название**</span><span class="sxs-lookup"><span data-stu-id="d0209-151">**Title**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d0209-152">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-152">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-153">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-153">WWI</span></span>  <br/> |<span data-ttu-id="d0209-154">Черный X 0196 19W</span><span class="sxs-lookup"><span data-stu-id="d0209-154">19W X0196 Black</span></span>  <br/> |<span data-ttu-id="d0209-155">Компьютер 1</span><span class="sxs-lookup"><span data-stu-id="d0209-155">Computer 1</span></span>  <br/> |
|<span data-ttu-id="d0209-156">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-156">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-157">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-157">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-158">12 M1201 красный</span><span class="sxs-lookup"><span data-stu-id="d0209-158">12 M1201 Red</span></span>  <br/> |<span data-ttu-id="d0209-159">Компьютер 2</span><span class="sxs-lookup"><span data-stu-id="d0209-159">Computer 2</span></span>  <br/> |
|<span data-ttu-id="d0209-160">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-160">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-161">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-161">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-162">15,4 Вт Технический M1548</span><span class="sxs-lookup"><span data-stu-id="d0209-162">15.4W M1548 White</span></span>  <br/> |<span data-ttu-id="d0209-163">Компьютер 3</span><span class="sxs-lookup"><span data-stu-id="d0209-163">Computer 3</span></span>  <br/> |
|<span data-ttu-id="d0209-164">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-164">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-165">Proseware</span><span class="sxs-lookup"><span data-stu-id="d0209-165">Proseware</span></span>  <br/> |<span data-ttu-id="d0209-166">19 x 910 черный</span><span class="sxs-lookup"><span data-stu-id="d0209-166">19 X910 Black</span></span>  <br/> |<span data-ttu-id="d0209-167">Компьютер 4</span><span class="sxs-lookup"><span data-stu-id="d0209-167">Computer 4</span></span>  <br/> |
|<span data-ttu-id="d0209-168">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-168">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-169">Proseware</span><span class="sxs-lookup"><span data-stu-id="d0209-169">Proseware</span></span>  <br/> |<span data-ttu-id="d0209-170">Laptop19 X 910 черный</span><span class="sxs-lookup"><span data-stu-id="d0209-170">Laptop19 X910 Black</span></span>  <br/> |<span data-ttu-id="d0209-171">Компьютер 5</span><span class="sxs-lookup"><span data-stu-id="d0209-171">Computer 5</span></span>  <br/> |
|<span data-ttu-id="d0209-172">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-172">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-173">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-173">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-174">2,33 XD233 серебро</span><span class="sxs-lookup"><span data-stu-id="d0209-174">2.33 XD233 Silver</span></span>  <br/> |<span data-ttu-id="d0209-175">Компьютер 6</span><span class="sxs-lookup"><span data-stu-id="d0209-175">Computer 6</span></span>  <br/> |
|<span data-ttu-id="d0209-176">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-176">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-177">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-177">WWI</span></span>  <br/> |<span data-ttu-id="d0209-178">2,33 x черный 2330</span><span class="sxs-lookup"><span data-stu-id="d0209-178">2.33 X2330 Black</span></span>  <br/> |<span data-ttu-id="d0209-179">Компьютер 7</span><span class="sxs-lookup"><span data-stu-id="d0209-179">Computer 7</span></span>  <br/> |
|<span data-ttu-id="d0209-180">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-180">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-181">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-181">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-182">1.60 Технический ED160</span><span class="sxs-lookup"><span data-stu-id="d0209-182">1.60 ED160 White</span></span>  <br/> |<span data-ttu-id="d0209-183">Компьютер 8</span><span class="sxs-lookup"><span data-stu-id="d0209-183">Computer 8</span></span>  <br/> |
|<span data-ttu-id="d0209-184">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-184">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-185">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-185">WWI</span></span>  <br/> |<span data-ttu-id="d0209-186">3.0 серебро M0300</span><span class="sxs-lookup"><span data-stu-id="d0209-186">3.0 M0300 Silver</span></span>  <br/> |<span data-ttu-id="d0209-187">Компьютер 9</span><span class="sxs-lookup"><span data-stu-id="d0209-187">Computer 9</span></span>  <br/> |
   

  
    
    

#### <a name="example-group-by-category"></a><span data-ttu-id="d0209-188">Пример: группа по категориям</span><span class="sxs-lookup"><span data-stu-id="d0209-188">Example: group by Category</span></span>

<span data-ttu-id="d0209-p107">Во-первых, сгруппировать элементы, в зависимости от **Category** и Показать двух верхних (следовательно `"Category:2"`) для каждой группы. Отобразите соответствующее число уникальных для каждого **Category**(следовательно "Продукта: 1") **Products**.</span><span class="sxs-lookup"><span data-stu-id="d0209-p107">First, group the items based on **Category** and show the top two (hence `"Category:2"`) for each group. Then, for each **Category**, show a corresponding number of unique (hence "Product:1") **Products**.</span></span>
  
    
    
 <span data-ttu-id="d0209-191">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-191">**Syntax**</span></span>
  
    
    
 `CollapseSpecification="Category:2 Product:1"`
  
    
    
<span data-ttu-id="d0209-192">Это должен возвращать следующие результаты.</span><span class="sxs-lookup"><span data-stu-id="d0209-192">This should return the following results.</span></span>
  
    
    


|<span data-ttu-id="d0209-193">**Категория**</span><span class="sxs-lookup"><span data-stu-id="d0209-193">**Category**</span></span>|<span data-ttu-id="d0209-194">**Продукт**</span><span class="sxs-lookup"><span data-stu-id="d0209-194">**Product**</span></span>|<span data-ttu-id="d0209-195">**Variant**</span><span class="sxs-lookup"><span data-stu-id="d0209-195">**Variant**</span></span>|<span data-ttu-id="d0209-196">**Название**</span><span class="sxs-lookup"><span data-stu-id="d0209-196">**Title**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d0209-197">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-197">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-198">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-198">WWI</span></span>  <br/> |<span data-ttu-id="d0209-199">Черный X 0196 19W</span><span class="sxs-lookup"><span data-stu-id="d0209-199">19W X0196 Black</span></span>  <br/> |<span data-ttu-id="d0209-200">Компьютер 1</span><span class="sxs-lookup"><span data-stu-id="d0209-200">Computer 1</span></span>  <br/> |
|<span data-ttu-id="d0209-201">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-201">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-202">Adventure</span><span class="sxs-lookup"><span data-stu-id="d0209-202">Adventure</span></span>  <br/> |<span data-ttu-id="d0209-203">12 M1201 красный</span><span class="sxs-lookup"><span data-stu-id="d0209-203">12 M1201 Red</span></span>  <br/> |<span data-ttu-id="d0209-204">Компьютер 2</span><span class="sxs-lookup"><span data-stu-id="d0209-204">Computer 2</span></span>  <br/> |
|<span data-ttu-id="d0209-205">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-205">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-206">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-206">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-207">2,33 XD233 серебро</span><span class="sxs-lookup"><span data-stu-id="d0209-207">2.33 XD233 Silver</span></span>  <br/> |<span data-ttu-id="d0209-208">Компьютер 6</span><span class="sxs-lookup"><span data-stu-id="d0209-208">Computer 6</span></span>  <br/> |
|<span data-ttu-id="d0209-209">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-209">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-210">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-210">WWI</span></span>  <br/> |<span data-ttu-id="d0209-211">2,33 x черный 2330</span><span class="sxs-lookup"><span data-stu-id="d0209-211">2.33 X2330 Black</span></span>  <br/> |<span data-ttu-id="d0209-212">Компьютер 7</span><span class="sxs-lookup"><span data-stu-id="d0209-212">Computer 7</span></span>  <br/> |
   
<span data-ttu-id="d0209-213">Чтобы свернуть результаты поиска с помощью свойства **CollapseSpecification**, используйте следующий код.</span><span class="sxs-lookup"><span data-stu-id="d0209-213">Use the following code to collapse the search results by using the **CollapseSpecification** property.</span></span>
  
    
    



```cs

using (var context = new ClientContext("http://localhost"))
{
    var query = new KeywordQuery(context)
        {
            QueryText = "Title:Computer",
            CollapseSpecification = "Category:3 Product:1",
        };

    var executor = new SearchExecutor(context);
    var results = executor.ExecuteQuery(query);

    context.ExecuteQuery();

    foreach (var result in results.Value[0].ResultRows)
    {
        Console.WriteLine(result["Title"]);
    }
}

```


#### <a name="example-group-by-category-and-product"></a><span data-ttu-id="d0209-214">Пример: группа по категориям и продукта</span><span class="sxs-lookup"><span data-stu-id="d0209-214">Example: group by Category and Product</span></span>

<span data-ttu-id="d0209-p108">Во-первых группы элементов, на основе **Category** и **Product**. Затем щелкните Показать каждого уникальную комбинацию.</span><span class="sxs-lookup"><span data-stu-id="d0209-p108">First, group the items based on both **Category** and **Product**. Then, show each unique combination.</span></span>
  
    
    
 <span data-ttu-id="d0209-217">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-217">**Syntax**</span></span>
  
    
    
 `CollapseSpecification="Category,Product:1"`
  
    
    
<span data-ttu-id="d0209-218">Это должен возвращать следующие результаты.</span><span class="sxs-lookup"><span data-stu-id="d0209-218">This should return the following results.</span></span>
  
    
    


|<span data-ttu-id="d0209-219">**Категория**</span><span class="sxs-lookup"><span data-stu-id="d0209-219">**Category**</span></span>|<span data-ttu-id="d0209-220">**Продукт**</span><span class="sxs-lookup"><span data-stu-id="d0209-220">**Product**</span></span>|<span data-ttu-id="d0209-221">**Variant**</span><span class="sxs-lookup"><span data-stu-id="d0209-221">**Variant**</span></span>|<span data-ttu-id="d0209-222">**Название**</span><span class="sxs-lookup"><span data-stu-id="d0209-222">**Title**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="d0209-223">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-223">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-224">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-224">WWI</span></span>  <br/> |<span data-ttu-id="d0209-225">Черный X 0196 19W</span><span class="sxs-lookup"><span data-stu-id="d0209-225">19W X0196 Black</span></span>  <br/> |<span data-ttu-id="d0209-226">Компьютер 1</span><span class="sxs-lookup"><span data-stu-id="d0209-226">Computer 1</span></span>  <br/> |
|<span data-ttu-id="d0209-227">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-227">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-228">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-228">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-229">12 M1201 красный</span><span class="sxs-lookup"><span data-stu-id="d0209-229">12 M1201 Red</span></span>  <br/> |<span data-ttu-id="d0209-230">Компьютер 2</span><span class="sxs-lookup"><span data-stu-id="d0209-230">Computer 2</span></span>  <br/> |
|<span data-ttu-id="d0209-231">Ноутбуки</span><span class="sxs-lookup"><span data-stu-id="d0209-231">Laptops</span></span>  <br/> |<span data-ttu-id="d0209-232">Proseware</span><span class="sxs-lookup"><span data-stu-id="d0209-232">Proseware</span></span>  <br/> |<span data-ttu-id="d0209-233">19 x 910 черный</span><span class="sxs-lookup"><span data-stu-id="d0209-233">19 X910 Black</span></span>  <br/> |<span data-ttu-id="d0209-234">Компьютер 4</span><span class="sxs-lookup"><span data-stu-id="d0209-234">Computer 4</span></span>  <br/> |
|<span data-ttu-id="d0209-235">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-235">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-236">AdventureWorks</span><span class="sxs-lookup"><span data-stu-id="d0209-236">Adventure Works</span></span>  <br/> |<span data-ttu-id="d0209-237">2,33 XD233 серебро</span><span class="sxs-lookup"><span data-stu-id="d0209-237">2.33 XD233 Silver</span></span>  <br/> |<span data-ttu-id="d0209-238">Компьютер 6</span><span class="sxs-lookup"><span data-stu-id="d0209-238">Computer 6</span></span>  <br/> |
|<span data-ttu-id="d0209-239">Настольные ПК.</span><span class="sxs-lookup"><span data-stu-id="d0209-239">Desktops</span></span>  <br/> |<span data-ttu-id="d0209-240">WWI</span><span class="sxs-lookup"><span data-stu-id="d0209-240">WWI</span></span>  <br/> |<span data-ttu-id="d0209-241">2,33 x черный 2330</span><span class="sxs-lookup"><span data-stu-id="d0209-241">2.33 X2330 Black</span></span>  <br/> |<span data-ttu-id="d0209-242">Компьютер 7</span><span class="sxs-lookup"><span data-stu-id="d0209-242">Computer 7</span></span>  <br/> |
   

## <a name="trim-duplicate-search-results-using-the-trimduplicates-property"></a><span data-ttu-id="d0209-243">Обрезки результатов поиска дубликатов, с помощью свойства TrimDuplicates</span><span class="sxs-lookup"><span data-stu-id="d0209-243">Trim duplicate search results using the TrimDuplicates property</span></span>
<span data-ttu-id="d0209-244"><a name="bk_trim_duplicates"> </a></span><span class="sxs-lookup"><span data-stu-id="d0209-244"></span></span>

<span data-ttu-id="d0209-p109">Позволяет указать для удаления повторяющихся поиска результаты из результат установил ли **TrimDuplicates**. **TrimDuplicates**  **true** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d0209-p109">Use **TrimDuplicates** to specify whether to trim away the duplicate search results from the result set. **TrimDuplicates** is **true** by default.</span></span>
  
    
    
<span data-ttu-id="d0209-247">При использовании **TrimDuplicates** с **TrimDuplicatesOnProperty** или желательно **CollapseSpecification** **TrimDuplicates** задано значение **false**.</span><span class="sxs-lookup"><span data-stu-id="d0209-247">If you use **TrimDuplicates** with either **TrimDuplicatesOnProperty** or preferably **CollapseSpecification**, **TrimDuplicates** is set to **false**.</span></span>
  
    
    
 <span data-ttu-id="d0209-248">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-248">**Syntax**</span></span>
  
    
    
 `TrimDuplicates = <$true | $false>`
  
    
    

### <a name="trim-duplicate-search-results-using-the-trimduplicatesonproperty-property"></a><span data-ttu-id="d0209-249">Обрезки результатов поиска дубликатов, с помощью свойства TrimDuplicatesOnProperty</span><span class="sxs-lookup"><span data-stu-id="d0209-249">Trim duplicate search results using the TrimDuplicatesOnProperty property</span></span>
<span data-ttu-id="d0209-250"><a name="bk_trim_duplicates_on_property"> </a></span><span class="sxs-lookup"><span data-stu-id="d0209-250"></span></span>

<span data-ttu-id="d0209-p110">Используйте **TrimDuplicatesOnProperty**, чтобы указать, будет ли для использования не по умолчанию управляемого свойства в качестве основы для удаления повторений. Значение по умолчанию  **DocumentSignature** управляемых свойств. Управляемое свойство, которое должен иметь тип **Integer** или **String**. С помощью управляемого свойства, который представляет группировку элементов, этот компонент можно использовать для сворачивания поля.</span><span class="sxs-lookup"><span data-stu-id="d0209-p110">Use **TrimDuplicatesOnProperty** to specify whether to use a non-default managed property as the basis for duplicate trimming. The default value is the **DocumentSignature** managed property. The managed property must be of type **Integer** or **String**. By using a managed property that represents a grouping of items, you can use this feature for field collapsing.</span></span>
  
    
    
 <span data-ttu-id="d0209-255">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-255">**Syntax**</span></span>
  
    
    
 `TrimDuplicatesOnProperty = <managed property>`
  
> [!NOTE]
> <span data-ttu-id="d0209-256">В SharePoint используйте **CollapseSpecification** , где это возможно.</span><span class="sxs-lookup"><span data-stu-id="d0209-256">In SharePoint, use **CollapseSpecification** wherever possible.</span></span> <span data-ttu-id="d0209-257">**TrimDuplicatesOnProperty** доступна только в целях обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="d0209-257">**TrimDuplicatesOnProperty** is available for backward compatibility only.</span></span>
  
    
    


### <a name="trim-duplicate-search-results-using-the-trimduplicateskeepcount-property"></a><span data-ttu-id="d0209-258">Обрезки результатов поиска дубликатов, с помощью свойства TrimDuplicatesKeepCount</span><span class="sxs-lookup"><span data-stu-id="d0209-258">Trim duplicate search results using the TrimDuplicatesKeepCount property</span></span>
<span data-ttu-id="d0209-259"><a name="bk_trim_duplicates_keep_count"> </a></span><span class="sxs-lookup"><span data-stu-id="d0209-259"></span></span>

<span data-ttu-id="d0209-p112">Позволяет указать число документов, сохраняемых при **TrimDuplicates**  это **true** **TrimDuplicatesKeepCount**. Если **TrimDuplicates** основано на управляемое свойство, которое можно использовать в качестве идентификатора группы, например идентификатор сайта, можно управлять число результатов, возвращаемых для каждой группы. Возвращаемые элементы, с наибольшим динамического ранга в каждой группе.</span><span class="sxs-lookup"><span data-stu-id="d0209-p112">Use **TrimDuplicatesKeepCount** to specify the number of documents to retain when **TrimDuplicates** is **true**. If **TrimDuplicates** is based on a managed property that can be used as a group identifier, for example a site ID, you can control how many results are returned for each group. The items returned are those with the highest dynamic rank within each group.</span></span>
  
    
    
 <span data-ttu-id="d0209-263">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-263">**Syntax**</span></span>
  
    
    
 `TrimDuplicatesKeepCount = <number>`
  
    
    

### <a name="retrieve-duplicate-search-results-using-the-trimduplicatesincludeid-property"></a><span data-ttu-id="d0209-264">Получение результатов поиска дубликатов, с помощью свойства TrimDuplicatesIncludeId</span><span class="sxs-lookup"><span data-stu-id="d0209-264">Retrieve duplicate search results using the TrimDuplicatesIncludeId property</span></span>
<span data-ttu-id="d0209-265"><a name="bk_trim_duplicates_include_id"> </a></span><span class="sxs-lookup"><span data-stu-id="d0209-265"></span></span>

<span data-ttu-id="d0209-266">Использование **TrimDuplicatesIncludeId** для получения копии документа, когда **TrimDuplicates** **true** и **TrimDuplicatesOnProperty** или **CollapseSpecification** задано значение **false**.</span><span class="sxs-lookup"><span data-stu-id="d0209-266">Use **TrimDuplicatesIncludeId** to retrieve the duplicates of a document when **TrimDuplicates** is **true** and **TrimDuplicatesOnProperty** or **CollapseSpecification** is set to **false**.</span></span>
  
    
    
<span data-ttu-id="d0209-267">Идентификатор документа,  _docid_используется для извлечения дубликатов определенного документа.</span><span class="sxs-lookup"><span data-stu-id="d0209-267">The document ID,  _docid_, is used to retrieve the duplicates of a particular document.</span></span>
  
    
    
 <span data-ttu-id="d0209-268">**Синтаксис**</span><span class="sxs-lookup"><span data-stu-id="d0209-268">**Syntax**</span></span>
  
    
    
 `TrimDuplicatesIncludeId = <docid>`
  
> [!NOTE]
> <span data-ttu-id="d0209-269">_Fcoid_ управляемого свойства в FAST Search Server 2010 for SharePoint заменена _docid_ управляемых свойств в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d0209-269">The  _fcoid_ managed property in FAST Search Server 2010 for SharePoint has been replaced with the _docid_ managed property in SharePoint.</span></span>
  
    
    


## <a name="see-also"></a><span data-ttu-id="d0209-270">См. также</span><span class="sxs-lookup"><span data-stu-id="d0209-270">See also</span></span>
<span data-ttu-id="d0209-271"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="d0209-271"></span></span>


-  [<span data-ttu-id="d0209-272">KeywordQuery</span><span class="sxs-lookup"><span data-stu-id="d0209-272">KeywordQuery</span></span>](https://msdn.microsoft.com/library/Microsoft.Office.Server.Search.Query.KeywordQuery.aspx)
    
  
-  [<span data-ttu-id="d0209-273">Обзор схемы поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="d0209-273">Overview of the search schema in SharePoint</span></span>](http://technet.microsoft.com/en-us/library/jj219669%28office.15%29.aspx)
    
  

  
    
    

