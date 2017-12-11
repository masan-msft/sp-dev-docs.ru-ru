---
title: "Синтаксис выражений триггер в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: b8ecbc4a50a26dfa03a612946186ee5a01a6bcc6
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="trigger-expressions-syntax-in-sharepoint"></a><span data-ttu-id="bfb0f-102">Синтаксис выражений триггер в SharePoint</span><span class="sxs-lookup"><span data-stu-id="bfb0f-102">Trigger expressions syntax in SharePoint</span></span>
<span data-ttu-id="bfb0f-103">Сведения о выражениях триггер, которые можно использовать для создания условия запуска для настройки вызов веб-службы в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-103">Learn about trigger expressions you can use to create trigger conditions to configure the web service callout in SharePoint.</span></span> 
## <a name="elements-used-in-the-syntax-of-trigger-expressions"></a><span data-ttu-id="bfb0f-104">Элементы, используемые в синтаксисе триггер выражений</span><span class="sxs-lookup"><span data-stu-id="bfb0f-104">Elements used in the syntax of trigger expressions</span></span>
<span data-ttu-id="bfb0f-105"><a name="SP15triggerex_elements"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-105"></span></span>

<span data-ttu-id="bfb0f-106">Элементы, которые могут использоваться в выражении триггер являются:</span><span class="sxs-lookup"><span data-stu-id="bfb0f-106">Elements that can be used in a trigger expression are:</span></span>
  
    
    

- <span data-ttu-id="bfb0f-107">Операторы</span><span class="sxs-lookup"><span data-stu-id="bfb0f-107">Operators</span></span>
    
  
- <span data-ttu-id="bfb0f-108">Управляемый доступ к свойству значение</span><span class="sxs-lookup"><span data-stu-id="bfb0f-108">Managed property value access</span></span>
    
  
- <span data-ttu-id="bfb0f-109">Литералы</span><span class="sxs-lookup"><span data-stu-id="bfb0f-109">Literals</span></span>
    
  
- <span data-ttu-id="bfb0f-110">Функции</span><span class="sxs-lookup"><span data-stu-id="bfb0f-110">Functions</span></span>
    
  
- <span data-ttu-id="bfb0f-111">Константы</span><span class="sxs-lookup"><span data-stu-id="bfb0f-111">Constants</span></span>
    
> [!NOTE] 
> <span data-ttu-id="bfb0f-112">[!Примечание] Строка " **Null**" зарезервирован для значение **Null**.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-112">The string " **Null**" is reserved for the value **Null**.</span></span> 
  
    
    


## <a name="operators-in-trigger-expression-syntax"></a><span data-ttu-id="bfb0f-113">Операторы в синтаксис выражений триггер</span><span class="sxs-lookup"><span data-stu-id="bfb0f-113">Operators in trigger expression syntax</span></span>
<span data-ttu-id="bfb0f-114"><a name="SP15triggerex_operators"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-114"></span></span>

<span data-ttu-id="bfb0f-p101">В таблице 1 описаны операторы, поддерживаемые язык выражений триггер, содержащий приоритет, по убыванию. Операторы в одной категории имеют одинаковый приоритет. Несколько операторов имеет две версии их синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-p101">Table 1 describes the operators supported by the trigger expression language, with order of precedence being from highest to lowest. Operators in the same category have equal precedence. Several operators have two versions of their syntax.</span></span>
  
    
    

<span data-ttu-id="bfb0f-118">**В таблице 1. Поддерживаемые операторы для синтаксис выражений триггер**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-118">**Table 1. Supported operators for trigger expression syntax**</span></span>


|<span data-ttu-id="bfb0f-119">**Категория**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-119">**Category**</span></span>|<span data-ttu-id="bfb0f-120">**Выражение**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-120">**Expression**</span></span>|<span data-ttu-id="bfb0f-121">**Описание**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-121">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bfb0f-122">Унарный</span><span class="sxs-lookup"><span data-stu-id="bfb0f-122">Unary</span></span>  <br/> |-  <br/> <span data-ttu-id="bfb0f-123">!, НЕ</span><span class="sxs-lookup"><span data-stu-id="bfb0f-123">!, NOT</span></span>  <br/> |<span data-ttu-id="bfb0f-124">Арифметические отрицания</span><span class="sxs-lookup"><span data-stu-id="bfb0f-124">Arithmetic negation</span></span>  <br/> <span data-ttu-id="bfb0f-125">Логического отрицания</span><span class="sxs-lookup"><span data-stu-id="bfb0f-125">Logical negation</span></span>  <br/> |
|<span data-ttu-id="bfb0f-126">Умножения</span><span class="sxs-lookup"><span data-stu-id="bfb0f-126">Multiplicative</span></span>  <br/> |*  <br/> /  <br/> <span data-ttu-id="bfb0f-127">%, mod</span><span class="sxs-lookup"><span data-stu-id="bfb0f-127">%, mod</span></span>  <br/> |<span data-ttu-id="bfb0f-128">Умножение</span><span class="sxs-lookup"><span data-stu-id="bfb0f-128">Multiplication</span></span>  <br/> <span data-ttu-id="bfb0f-129">Подразделение</span><span class="sxs-lookup"><span data-stu-id="bfb0f-129">Division</span></span>  <br/> <span data-ttu-id="bfb0f-130">Остаток</span><span class="sxs-lookup"><span data-stu-id="bfb0f-130">Remainder</span></span>  <br/> |
|<span data-ttu-id="bfb0f-131">ADDITIVE</span><span class="sxs-lookup"><span data-stu-id="bfb0f-131">Additive</span></span>  <br/> |+  <br/> -  <br/> &amp;  <br/> |<span data-ttu-id="bfb0f-132">Добавление</span><span class="sxs-lookup"><span data-stu-id="bfb0f-132">Addition</span></span>  <br/> <span data-ttu-id="bfb0f-133">Вычитание</span><span class="sxs-lookup"><span data-stu-id="bfb0f-133">Subtraction</span></span>  <br/> <span data-ttu-id="bfb0f-134">Объединение строк</span><span class="sxs-lookup"><span data-stu-id="bfb0f-134">String concatenation</span></span>  <br/> |
|<span data-ttu-id="bfb0f-135">Реляционные</span><span class="sxs-lookup"><span data-stu-id="bfb0f-135">Relational</span></span>  <br/> |<span data-ttu-id="bfb0f-136">=, ==</span><span class="sxs-lookup"><span data-stu-id="bfb0f-136">=, ==</span></span>  <br/> <span data-ttu-id="bfb0f-137">! = <></span><span class="sxs-lookup"><span data-stu-id="bfb0f-137">!=, <></span></span>  <br/> <  <br/> >  <br/> <=  <br/> >=  <br/> |<span data-ttu-id="bfb0f-138">Равенство</span><span class="sxs-lookup"><span data-stu-id="bfb0f-138">Equality</span></span>  <br/> <span data-ttu-id="bfb0f-139">Неравенство</span><span class="sxs-lookup"><span data-stu-id="bfb0f-139">Inequality</span></span>  <br/> <span data-ttu-id="bfb0f-140">Меньше</span><span class="sxs-lookup"><span data-stu-id="bfb0f-140">Less than</span></span>  <br/> <span data-ttu-id="bfb0f-141">Больше</span><span class="sxs-lookup"><span data-stu-id="bfb0f-141">Greater than</span></span>  <br/> <span data-ttu-id="bfb0f-142">Меньше или равно</span><span class="sxs-lookup"><span data-stu-id="bfb0f-142">Less than or equal</span></span>  <br/> <span data-ttu-id="bfb0f-143">Больше или равно</span><span class="sxs-lookup"><span data-stu-id="bfb0f-143">Greater than or equal</span></span>  <br/> |
|<span data-ttu-id="bfb0f-144">Логическое И</span><span class="sxs-lookup"><span data-stu-id="bfb0f-144">Logical AND</span></span>  <br/> |<span data-ttu-id="bfb0f-145">&amp; &amp;, AND</span><span class="sxs-lookup"><span data-stu-id="bfb0f-145">&amp;&amp;, AND</span></span>  <br/> |<span data-ttu-id="bfb0f-146">Логическое И</span><span class="sxs-lookup"><span data-stu-id="bfb0f-146">Logical AND</span></span>  <br/> |
|<span data-ttu-id="bfb0f-147">Логическое ИЛИ</span><span class="sxs-lookup"><span data-stu-id="bfb0f-147">Logical OR</span></span>  <br/> | <span data-ttu-id="bfb0f-148">OR</span><span class="sxs-lookup"><span data-stu-id="bfb0f-148">OR</span></span>  <br/> |<span data-ttu-id="bfb0f-149">Логическое ИЛИ</span><span class="sxs-lookup"><span data-stu-id="bfb0f-149">Logical OR</span></span>  <br/> |
   

## <a name="managed-property-access-in-trigger-expressions"></a><span data-ttu-id="bfb0f-150">Управляемые свойства access в выражениях триггер</span><span class="sxs-lookup"><span data-stu-id="bfb0f-150">Managed property access in trigger expressions</span></span>
<span data-ttu-id="bfb0f-151"><a name="SP15triggerex_managed"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-151"></span></span>

<span data-ttu-id="bfb0f-152">Управляемые свойства для обхода элементов ссылается их имя; Имя не входит в кавычки ("") и задается с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-152">Managed properties in the crawled items are referenced by their name; the name is not in quotation marks ("") and is case-sensitive.</span></span>
  
    
    

## <a name="literals-in-trigger-expressions"></a><span data-ttu-id="bfb0f-153">Литералы в выражениях триггер</span><span class="sxs-lookup"><span data-stu-id="bfb0f-153">Literals in trigger expressions</span></span>
<span data-ttu-id="bfb0f-154"><a name="SP15triggerex_literals"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-154"></span></span>

<span data-ttu-id="bfb0f-155">Следующие типы данных могут быть выражены как литералы: **String**, **Int32**, **Double**и **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-155">The following data types can be expressed as literals: **String**, **Int32**, **Double**, and **Boolean**.</span></span>
  
    
    

## <a name="functions-in-trigger-expressions"></a><span data-ttu-id="bfb0f-156">Функции в выражениях триггер</span><span class="sxs-lookup"><span data-stu-id="bfb0f-156">Functions in trigger expressions</span></span>
<span data-ttu-id="bfb0f-157"><a name="SP15triggerex_functions"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-157"></span></span>

<span data-ttu-id="bfb0f-p102">Широкий набор функций, включающих от математические функции, такие как  `Floor` функций для использования с определенными типами данных, таких как `Lists`. Можно использовать эти функции по отдельности или можно вкладывать их.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-p102">A wide collection of functions ranging from mathematical functions such as  `Floor` to functions for use with particular data types, such as `Lists`. You can use these functions individually or you can nest them.</span></span>
  
    
    

-  `bool? ListContains<T>(IList<T> list, T obj)`
    
  
-  `int? Count<TElement>(IList<TElement> list)`
    
  
-  `TElement Item<TElement>(IList<TElement> list, int? index)`
    
  
-  `bool IsInsideRange(DateTime? date, long? fromTicks, long? toTicks)`
    
  
-  `DateTime Now()`
    
  
-  `DateTime? ToDate(string date, string format)`
    
  
-  `int? Day(DateTime? date)`
    
  
-  `int? DayOfWeek(DateTime? date)`
    
  
-  `int? DayOfYear(DateTime? date)`
    
  
-  `int? GetDatePart(DateTime? date, DatePartConstant datePartConstant)`
    
  
-  `int? Hour(DateTime? date)`
    
  
-  `int? Minute(DateTime? date)`
    
  
-  `int? Month(DateTime? date)`
    
  
-  `int? Quarter(DateTime? date)`
    
  
-  `int? Second(DateTime? date)`
    
  
-  `int? Year(DateTime? date)`
    
  
-  `long? GetDateDiff(DateTime? occursFirst, DateTime? occursLast, DatePartConstant datePartConstant)`
    
  
-  `string Extension(string arg)`
    
  
-  `string FileName(string arg)`
    
  
-  `string FileName(string arg, bool? excludeExtension)`
    
  
-  `bool IsNull(object value)`
    
  
-  `bool? IsDate(string input, string format)`
    
  
-  `object IfThenElse(bool? condition, object thenBranch, object elseBranch)`
    
  
-  `decimal? Ceiling(decimal? number)`
    
  
-  `decimal? Floor(decimal? number)`
    
  
-  `double? Ceiling(double? number)`
    
  
-  `double? Floor(double? number)`
    
  
-  `double? Sqrt(double? number)`
    
  
-  `bool? Contains(string arg, string contained)`
    
  
-  `bool? EndsWith(string arg, string suffix)`
    
  
-  `bool? IsMatch(string input, string pattern)`
    
  
-  `bool? IsMatch(string input, string pattern, int? start, RegexOptionConstant options)`
    
  
-  `bool? IsMatch(string input, string pattern, RegexOptionConstant options)`
    
  
-  `bool? IsNullOrEmpty(string input)`
    
  
-  `bool? StartsWith(string arg, string prefix)`
    
  
-  `int? IndexOf(string arg, string toFind)`
    
  
-  `int? IndexOfRegex(string input, string regex)`
    
  
-  `int? LastIndexOf(string arg, string toFind)`
    
  
-  `int? Length(string arg)`
    
  
-  `string Match(string input, string pattern)`
    
  
-  `string Match(string input, string pattern, int? start, int? length, RegexOptionConstant options)`
    
  
-  `string Match(string input, string pattern, int? start, RegexOptionConstant options)`
    
  
-  `string Match(string input, string pattern, RegexOptionConstant options)`
    
  
-  `string Substring(string arg, int? start)`
    
  
-  `string Substring(string arg, int? start, int? length)`
    
  
-  `string ToLower(string arg)`
    
  
-  `string Trim(string value)`
    
  

## <a name="constants-in-trigger-expressions"></a><span data-ttu-id="bfb0f-160">Константы в выражениях триггер</span><span class="sxs-lookup"><span data-stu-id="bfb0f-160">Constants in trigger expressions</span></span>
<span data-ttu-id="bfb0f-161"><a name="SP15triggerex_constants"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-161"></span></span>

<span data-ttu-id="bfb0f-p103">Существует два набора константы, которые могут использоваться с помощью определенных функций: **DatePartConstant** и **RegexOptionConstant**. В таблице 2 приведены два примера эти константы и где их можно использовать.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-p103">There are two sets of constants that can be used with specific functions: **DatePartConstant** and **RegexOptionConstant**. Table 2 lists the two examples of these constants and where you can use them.</span></span>
  
    
    

<span data-ttu-id="bfb0f-164">**В таблице 2. Константы выражение триггер и использования в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-164">**Table 2. Trigger expression constants and usage in SharePoint**</span></span>


|<span data-ttu-id="bfb0f-165">**Группа констант**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-165">**Group of constants**</span></span>|<span data-ttu-id="bfb0f-166">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-166">**Examples**</span></span>|<span data-ttu-id="bfb0f-167">**Использование**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-167">**Usage**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="bfb0f-168">**DatePartConstant**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-168">**DatePartConstant**</span></span> <br/> |<span data-ttu-id="bfb0f-169">**Day**, **Month**, **Year**, **Hour**, **Minute**, **Second**.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-169">**Day**, **Month**, **Year**, **Hour**, **Minute**, **Second**.</span></span>  <br/> |<span data-ttu-id="bfb0f-170">С помощью функции **GetDatePart**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-170">With the **GetDatePart** function</span></span> <br/> |
|<span data-ttu-id="bfb0f-171">**RegexOptionConstant**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-171">**RegexOptionConstant**</span></span> <br/> |<span data-ttu-id="bfb0f-172">**IgnoreCase**</span><span class="sxs-lookup"><span data-stu-id="bfb0f-172">**IgnoreCase**</span></span> <br/> |<span data-ttu-id="bfb0f-173">С помощью функции **IsMatch**, **Match**, **ReplaceRegex**и **IndexOfRegex**.</span><span class="sxs-lookup"><span data-stu-id="bfb0f-173">With the **IsMatch**, **Match**, **ReplaceRegex**, and **IndexOfRegex** functions.</span></span> <br/> |
   

## <a name="see-also"></a><span data-ttu-id="bfb0f-174">См. также</span><span class="sxs-lookup"><span data-stu-id="bfb0f-174">See also</span></span>
<span data-ttu-id="bfb0f-175"><a name="SP15triggerex_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bfb0f-175"></span></span>


-  [<span data-ttu-id="bfb0f-176">Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"</span><span class="sxs-lookup"><span data-stu-id="bfb0f-176">Custom content processing with the Content Enrichment web service callout</span></span>](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  
-  [<span data-ttu-id="bfb0f-177">Как: используйте вызов повышения качества контента веб-службы для SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="bfb0f-177">How to: Use the Content Enrichment web service callout for SharePoint Server</span></span>](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md)
    
  

  
    
    

