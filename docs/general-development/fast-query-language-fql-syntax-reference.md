---
title: "Руководство по синтаксису языка запросов FAST (FQL)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bd98a41b-623c-41d4-a15d-26c0d4ba4311
ms.openlocfilehash: cb907c3d043f95d79d117bb8bf11afc0a8c5c822
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="fast-query-language-fql-syntax-reference"></a><span data-ttu-id="50a7e-102">Справочник по синтаксису языка запросов FAST (FQL)</span><span class="sxs-lookup"><span data-stu-id="50a7e-102">FAST Query Language (FQL) syntax reference</span></span>
<span data-ttu-id="50a7e-103">Узнайте, как создавать сложные поисковые запросы для службы поиска в SharePoint с помощью языка запросов FAST (FQL).</span><span class="sxs-lookup"><span data-stu-id="50a7e-103">Learn about constructing complex search queries for Search in SharePoint using the FAST Query Language (FQL).</span></span> <span data-ttu-id="50a7e-104">В этом справочнике описываются элементы запроса FQL и использование спецификаций свойств, выражений с маркерами и операторов в запросах FQL.</span><span class="sxs-lookup"><span data-stu-id="50a7e-104">Learn about constructing complex search queries for sp15searchshort using the FAST Query Language (FQL). This reference describes the elements of an FQL query and how to use property specifications, token expressions, and operators in your FQL queries.</span></span>
## <a name="introduction-to-fql-and-query-language-subexpressions-and-expressions-in-sharepoint"></a><span data-ttu-id="50a7e-105">Общие сведения об FQL, частях выражений и выражениях языка запросов в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50a7e-105">Introduction to FQL and query language subexpressions and expressions in SharePoint Server 2013</span></span>
<span data-ttu-id="50a7e-106"><a name="SP15FQL_about"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-106"></span></span>

<span data-ttu-id="50a7e-107">Язык FAST-запросов (FQL)  это мощный язык запросов, который позволяет разработчикам выполнять точный поиск и сужать область поиска до значений, которые относятся к конкретному управляемого свойству или полнотекстовому индексу.</span><span class="sxs-lookup"><span data-stu-id="50a7e-107">The FAST Query Language (FQL) is a powerful query language that enables developers to perform exact searches and to narrow the scope of your search to values that belong to a specific managed property or a full-text index.</span></span>
  
    
    
<span data-ttu-id="50a7e-108">Выражение языка запросов может содержать вложенные части выражения, которые включают термины запроса, спецификации свойств и операторы, описанные в таблице 1.</span><span class="sxs-lookup"><span data-stu-id="50a7e-108">A query language expression can contain nested subexpressions that include query terms, property specifications, and operators, as described in Table 1.</span></span>
  
    
    

<span data-ttu-id="50a7e-109">**Таблица 1. Части выражений в выражениях языка запросов**</span><span class="sxs-lookup"><span data-stu-id="50a7e-109">**Table 1. Subexpressions in query language expressions**</span></span>


|<span data-ttu-id="50a7e-110">**Элемент**</span><span class="sxs-lookup"><span data-stu-id="50a7e-110">**Item**</span></span>|<span data-ttu-id="50a7e-111">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-111">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="50a7e-112">Выражения с маркерами</span><span class="sxs-lookup"><span data-stu-id="50a7e-112">Token expressions</span></span>  <br/> |<span data-ttu-id="50a7e-113">Один или несколько поисковых терминов, фраз или числовых значений в запросе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-113">One or more query terms, phrases, or numeric values to search for in a query.</span></span>  <br/> |
|<span data-ttu-id="50a7e-114">Спецификация свойства</span><span class="sxs-lookup"><span data-stu-id="50a7e-114">Property specification</span></span>  <br/> |<span data-ttu-id="50a7e-115">Свойство или полнотекстовый индекс, соответствующий затрагиваемому выражению.</span><span class="sxs-lookup"><span data-stu-id="50a7e-115">A property or full-text index to match with the affected expression.</span></span>  <br/> |
|<span data-ttu-id="50a7e-116">Операторы</span><span class="sxs-lookup"><span data-stu-id="50a7e-116">Operators</span></span>  <br/> |<span data-ttu-id="50a7e-117">Ключевые слова, определяющие логические операции (например, **AND**, **OR**) или другие ограничения для операндов (например, **FILTER**).</span><span class="sxs-lookup"><span data-stu-id="50a7e-117">Keywords that specify Boolean operations (such as **AND**, **OR**) or other constraints to operands (such as **FILTER**.)</span></span>  <br/> |
   

### <a name="fql-query-example"></a><span data-ttu-id="50a7e-118">Пример FQL-запроса</span><span class="sxs-lookup"><span data-stu-id="50a7e-118">FQL query example</span></span>

<span data-ttu-id="50a7e-119">Следующий пример запроса FQL служит для поиска терминов "hello" и "world" в управляемом свойстве **body** индексированного элемента:</span><span class="sxs-lookup"><span data-stu-id="50a7e-119">The following FQL query example searches for the terms "hello" and "world" in the **body** managed property of an indexed item:</span></span>
  
    
    
 `body:string("hello world", mode="and")`
  
    
    
<span data-ttu-id="50a7e-120">В этом примере происходит указанный ниже процесс.</span><span class="sxs-lookup"><span data-stu-id="50a7e-120">In the example:</span></span>
  
    
    

-  <span data-ttu-id="50a7e-121">`body:` ограничивает область запроса текстом управляемого свойства в данном элементе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-121">`body:` limits the scope of the query to the body managed property within the item.</span></span>
    
  
-  <span data-ttu-id="50a7e-122">`"hello world"`  операнд для оператора **STRING**, указывающий поисковые термины.</span><span class="sxs-lookup"><span data-stu-id="50a7e-122">`"hello world"` is the operand to the **STRING** operator, which indicates the terms to search for.</span></span>
    
  
-  <span data-ttu-id="50a7e-123">`mode="and"` указывает, что логический оператор запроса **AND** будет применен к `"hello world"`.</span><span class="sxs-lookup"><span data-stu-id="50a7e-123">`mode="and"` indicates that the logical query operator **AND** will be applied to `"hello world"`.</span></span>
    
  
<span data-ttu-id="50a7e-124">Длина FQL-запросов ограничена 2048 символами.</span><span class="sxs-lookup"><span data-stu-id="50a7e-124">The length of FAST Query Language queries is limited to 2,048 characters.</span></span>
  
    
    

## <a name="property-specification-in-fql"></a><span data-ttu-id="50a7e-125">Спецификация свойств в FQL</span><span class="sxs-lookup"><span data-stu-id="50a7e-125">Property specification in FQL</span></span>
<span data-ttu-id="50a7e-126"><a name="property_specification"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-126"></span></span>

<span data-ttu-id="50a7e-p102">Спецификация свойств ограничивает область затрагиваемых выражений определенными областями индексированного содержимого. Эта область может быть определена полнотекстовым индексом или управляемым свойством.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p102">A property specification limits the scope of the affected expression to specific regions of the indexed content. Such a region can be identified by a full-text index or a managed property.</span></span> 
  
    
    
<span data-ttu-id="50a7e-p103">Управляемые свойства типа **Text** или **YesNo** считаются текстом. Все остальные типы управляемых свойств, в том числе тип **Datetime**, считаются числовыми значениями.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p103">Managed properties of type **Text** and **YesNo** are evaluated as text. All other managed property types, including the **Datetime** type, are evaluated as numeric values.</span></span>
  
    
    
<span data-ttu-id="50a7e-131">Если не включить спецификацию свойства для выражения, поисковая система будет использовать полнотекстовый индекс по умолчанию, определенный в схеме индекса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-131">If you don't include a property specification for an expression, the search engine attempts to match the default full-text index defined in the index schema.</span></span>
  
    
    
<span data-ttu-id="50a7e-132">После имени свойства всегда должно стоять двоеточие (оператор **In**), а числовые операторы всегда должны включать спецификацию свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-132">The property name must always precede a colon ( **In** operator), and numeric operators must always include a property specification.</span></span>
  
    
    
<span data-ttu-id="50a7e-133">Спецификация свойства (оператор **In**) может быть применена к следующим сущностям запроса:</span><span class="sxs-lookup"><span data-stu-id="50a7e-133">A property specification (the **In** Operator) may be applied to the following query entities:</span></span>
  
    
    

- <span data-ttu-id="50a7e-134">Одиночному термину или фразе, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="50a7e-134">A single term or phrase, as follows:</span></span>

    `author:shakespeare`
    
    `title:"to be or not to be"`
- <span data-ttu-id="50a7e-135">Оператору, например **STRING**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="50a7e-135">An operator, for example, the **STRING** operator, as follows:</span></span>
```
    title:string("to be or not to be")
```
    In this case the property specification applies to the complete operator expression.

### <a name="examples"></a><span data-ttu-id="50a7e-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-136">Examples</span></span>

<span data-ttu-id="50a7e-137">Выражения с маркерами в FQL</span><span class="sxs-lookup"><span data-stu-id="50a7e-137">Each of the following expressions matches items that have both "much" and "nothing" in the **title** managed property.</span></span>

 `title:and(much, nothing)`

 `and(title:much, title:nothing)`

 `title:string("much nothing", mode="and")`

## <a name="token-expressions-in-fql"></a><span data-ttu-id="50a7e-138">Выражения с маркерами на языке FQL</span><span class="sxs-lookup"><span data-stu-id="50a7e-138">Token expressions in FQL</span></span>
<span data-ttu-id="50a7e-139"><a name="token_expressions"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-139"></span></span>

<span data-ttu-id="50a7e-140">Текстовое выражение с маркером может быть одним словом или фразой, заключенной в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="50a7e-140">Token expressions are words, phrases, or numeric values that are matched against the index.</span></span>
  
    
    
<span data-ttu-id="50a7e-141">Числовое выражение с маркером может быть одним значением или диапазоном значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-141">A text token expression can be a single word or a phrase enclosed in double quotation marks.</span></span>
  
    
    
<span data-ttu-id="50a7e-142">Выражения с подстановочными знаками</span><span class="sxs-lookup"><span data-stu-id="50a7e-142">A numeric token expression can be a single value or a value range expression.</span></span>
  
    
    

### <a name="wildcard-expressions"></a><span data-ttu-id="50a7e-143">Выражения с подстановочными знаками</span><span class="sxs-lookup"><span data-stu-id="50a7e-143">Wildcard expressions</span></span>

<span data-ttu-id="50a7e-144">Выражение с подстановочными знаками — это термин или фраза, включающие знак звездочки ("**\***"). Звездочка соответствует любому количеству символов (или их отсутствию), за исключением пробелов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-144">A wildcard expression indicates a single term or phrase that includes the Asterisk ("*") character; asterisk implies a match of zero or more characters, excluding whitespace. FQL supports prefix search for individual text managed properties and full-text indexes.</span></span> <span data-ttu-id="50a7e-145">Язык FQL поддерживает поиск по префиксу для отдельных текстовых управляемых свойств и полнотекстовых индексов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-145">FAST Query Language (FQL) supports wildcard search for individual text managed properties and full-text indexes.</span></span>
  
    
    

#### <a name="wildcard-expression-examples"></a><span data-ttu-id="50a7e-146">Примеры выражений с подстановочными знаками</span><span class="sxs-lookup"><span data-stu-id="50a7e-146">Wildcard expression examples</span></span>

<span data-ttu-id="50a7e-147">Выражения с числовыми терминами</span><span class="sxs-lookup"><span data-stu-id="50a7e-147">The following is a list of valid uses of wildcard expressions in FQL:</span></span>
  
    
    

-  `text*`
    
  
-  `string("this examp*")`
    
  

### <a name="numeric-term-expressions"></a><span data-ttu-id="50a7e-148">Выражения с числовыми терминами</span><span class="sxs-lookup"><span data-stu-id="50a7e-148">Numeric term expressions</span></span>
<span data-ttu-id="50a7e-149"><a name="fql_token_numeric"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-149"></span></span>

<span data-ttu-id="50a7e-p105">Каждое выражение с числовым термином должно включать спецификацию свойства совместимого типа схемы индекса. В таблице 2 перечислены числовые типы данных, которые можно использовать в FQL.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p105">Each numeric term expression must include a property specification of a compatible index schema data type. Table 2 lists the numeric data types that can be used in FQL.</span></span> 
  
    
    

<span data-ttu-id="50a7e-152">**Тип FQL**</span><span class="sxs-lookup"><span data-stu-id="50a7e-152">**Table 2. Numeric data types that can be used in FQL**</span></span>


|<span data-ttu-id="50a7e-153">**Совместимые типы схем индекса**</span><span class="sxs-lookup"><span data-stu-id="50a7e-153">**FQL type**</span></span>|<span data-ttu-id="50a7e-154">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-154">**Compatible index schema types**</span></span>|<span data-ttu-id="50a7e-155">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-155">**Description**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="50a7e-156">**Integer**</span><span class="sxs-lookup"><span data-stu-id="50a7e-156">**Int**</span></span> <br/> |<span data-ttu-id="50a7e-157">64-разрядное целое число.</span><span class="sxs-lookup"><span data-stu-id="50a7e-157">**Integer**</span></span> <br/> |<span data-ttu-id="50a7e-158">64-битное целое число.</span><span class="sxs-lookup"><span data-stu-id="50a7e-158">64 bit integer.</span></span>  <br/> |
|<span data-ttu-id="50a7e-159">**Double**</span><span class="sxs-lookup"><span data-stu-id="50a7e-159">**Float**</span></span> <br/> |<span data-ttu-id="50a7e-160">64-разрядное число с плавающей запятой двойной точности.</span><span class="sxs-lookup"><span data-stu-id="50a7e-160">**Double**</span></span> <br/> |<span data-ttu-id="50a7e-161">64-битное число с плавающей запятой (двойная точность).</span><span class="sxs-lookup"><span data-stu-id="50a7e-161">64-bit (double precision) floating point.</span></span>  <br/> |
|<span data-ttu-id="50a7e-162">128-разрядное десятичное число.</span><span class="sxs-lookup"><span data-stu-id="50a7e-162">**Decimal**</span></span> <br/> |<span data-ttu-id="50a7e-163">128-разрядное десятичное число.</span><span class="sxs-lookup"><span data-stu-id="50a7e-163">**Decimal**</span></span> <br/> |<span data-ttu-id="50a7e-164">128-битное десятичное число</span><span class="sxs-lookup"><span data-stu-id="50a7e-164">128-bit decimal</span></span>  <br/> |
|<span data-ttu-id="50a7e-165">Значение даты и времени.</span><span class="sxs-lookup"><span data-stu-id="50a7e-165">**Datetime**</span></span> <br/> |<span data-ttu-id="50a7e-166">Значение даты и времени.</span><span class="sxs-lookup"><span data-stu-id="50a7e-166">**Datetime**</span></span> <br/> |<span data-ttu-id="50a7e-167">За счет поддержки даты и времени в FQL над их значениями можно выполнять те же числовые операции, что и над другими числовыми значениями.</span><span class="sxs-lookup"><span data-stu-id="50a7e-167">A date and time value.</span></span>  <br/><span data-ttu-id="50a7e-168">Выражения запросов даты и времени</span><span class="sxs-lookup"><span data-stu-id="50a7e-168">The date/time support in FQL enables the same numeric operations on date/time values as on other numeric values.</span></span>  <br/> |
   

#### <a name="date-and-time-query-expressions"></a><span data-ttu-id="50a7e-169">Выражения запросов даты и времени</span><span class="sxs-lookup"><span data-stu-id="50a7e-169">Date and time query expressions</span></span>
<span data-ttu-id="50a7e-170"><a name="fql_token_datetime"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-170"></span></span>

<span data-ttu-id="50a7e-171">В запросах поддерживаются следующие совместимые со стандартом ISO 8601 форматы **datetime**:</span><span class="sxs-lookup"><span data-stu-id="50a7e-171">FQL provides the **datetime** data type for date and time.</span></span>
  
    
    
<span data-ttu-id="50a7e-172">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="50a7e-172">The following ISO 8601-compatible **datetime** formats are supported in queries:</span></span>
  
    
    

- <span data-ttu-id="50a7e-173">YYYY-MM-DDThh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="50a7e-173">YYYY-MM-DD</span></span> 
    
  
- <span data-ttu-id="50a7e-174">YYYY-MM-DDThh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="50a7e-174">YYYY-MM-DDThh:mm:ss</span></span> 
    
  
- <span data-ttu-id="50a7e-175">ГГГГ-ММ-ДДTчч:мм:ссZ</span><span class="sxs-lookup"><span data-stu-id="50a7e-175">YYYY-MM-DDThh:mm:ssZ</span></span> 
    
  
- <span data-ttu-id="50a7e-176">ГГГГ-ММ-ДДTчч:мм:ссfrZ</span><span class="sxs-lookup"><span data-stu-id="50a7e-176">YYYY-MM-DDThh:mm:ssfrZ</span></span>
    
  
<span data-ttu-id="50a7e-177">В этих форматах **datetime**:</span><span class="sxs-lookup"><span data-stu-id="50a7e-177">In these **datetime** formats:</span></span>
  
    
    

-  <span data-ttu-id="50a7e-178">_ГГГГ_ — это четырехзначный год.</span><span class="sxs-lookup"><span data-stu-id="50a7e-178">_YYYY_ specifies a four-digit year.</span></span>
    
    > <span data-ttu-id="50a7e-179">**Примечание.** Можно указывать только четырехзначные годы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-179">**Note** Only four-digit years are supported.</span></span> 
-  <span data-ttu-id="50a7e-p106">_ММ_ — двузначный номер месяца. Например, 01 обозначает январь.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p106">_MM_ specifies a two-digit month. For example, 01 = January.</span></span>
    
  
-  <span data-ttu-id="50a7e-182">Параметр  _DD_ задает двузначное значение дня месяца (от 01 до 31).</span><span class="sxs-lookup"><span data-stu-id="50a7e-182">_DD_ specifies a two-digit day of the month (01 through 31).</span></span>
    
  
-  <span data-ttu-id="50a7e-183">Параметр  _T_ обозначает букву "T".</span><span class="sxs-lookup"><span data-stu-id="50a7e-183">_T_ specifies the letter "T".</span></span>
    
  
-  <span data-ttu-id="50a7e-p107">Параметр  _hh_ обозначает часы в формате двух цифр (от 00 до 23). Обозначения a.m. и p.m. не допускаются.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p107">_hh_ specifies a two-digits hour (00 through 23); A.M./P.M. indication is not allowed.</span></span>
    
  
-  <span data-ttu-id="50a7e-186">Параметр  _mm_ обозначает минуты в формате двух цифр (от 00 до 59).</span><span class="sxs-lookup"><span data-stu-id="50a7e-186">_mm_ specifies a two-digit minute (00 through 59).</span></span>
    
  
-  <span data-ttu-id="50a7e-187">_сс_ — двузначное число секунд (от 00 до 59).</span><span class="sxs-lookup"><span data-stu-id="50a7e-187">_ss_ specifies a two-digit second (00 through 59).</span></span>
    
  
-  <span data-ttu-id="50a7e-p108">Все значения даты и времени необходимо указывать в часовом поясе UTC (другое название  GMT). Идентификатор часового пояса UTC (символ "Z" в конце) указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p108">_fr_ specifies an optional fraction of seconds, _ss_; between 1 to 7 digits that follows the **.** after the seconds. For example, 2012-09-27T11:57:34.1234567.</span></span>
    
  
<span data-ttu-id="50a7e-p109">Все значения даты и времени необходимо указывать в часовом поясе UTC (другое название  GMT). Идентификатор часового пояса UTC (символ "Z" в конце) указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p109">All date/time values must be specified according to the UTC (Coordinated Universal Time), also known as GMT (Greenwich Mean Time) time zone. The UTC time zone identifier (a trailing "Z" character) is optional.</span></span>
  
    
    

### <a name="reserved-words-special-characters-and-escaping"></a><span data-ttu-id="50a7e-193">Зарезервированные слова, специальные знаки и escape-символы</span><span class="sxs-lookup"><span data-stu-id="50a7e-193">Reserved words, special characters, and escaping</span></span>
<span data-ttu-id="50a7e-194"><a name="fql_token_numeric"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-194"></span></span>

<span data-ttu-id="50a7e-195">Чтобы представить любое из этих слов в виде терминов в выражении запроса, их необходимо заключить в двойные кавычки, как показано в следующих примерах:</span><span class="sxs-lookup"><span data-stu-id="50a7e-195">The following words are reserved within FQL.</span></span>
  
    
    
`and, or, any, andnot, count, decimal, rank, near, onear, int, in32, int64, float, double, datetime, max, min, range, phrase, scope, filter, not, string, starts-with, ends-with, equals, words, xrank.`
  
    
    
<span data-ttu-id="50a7e-196">Чтобы представить любое из этих слов в виде терминов в выражении запроса, их необходимо заключить в двойные кавычки, как показано в следующих примерах:</span><span class="sxs-lookup"><span data-stu-id="50a7e-196">If you want to express any of these words as terms in a query expression, you must enclose them in double quotation marks as shown in the following examples:</span></span> 
  
    
    

-  `or("any", "and", "xrank")`
    
  
-  `string("any and xrank", mode="OR")`
    
  
-  `phrase(this, is, a, "phrase")`
    
  

> <span data-ttu-id="50a7e-197">**Совет.** В зарезервированных словах и символах не учитывается регистр, но для совместимости с будущими версиями рекомендуем использовать символы нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="50a7e-197">Reserved words and characters are not case-sensitive, but using lowercase characters are recommended for future compatibility.</span></span> 
  
    
    

<span data-ttu-id="50a7e-p110">Разметка терминов запросов выполняется в соответствии с вашими региональными параметрами. В процессе разметки удаляются некоторые специальные символы. Так как специальные символы удалены, следующие FQL-выражения эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="50a7e-p110">FQL does not always require a string to be enclosed in double quotation marks. For example,  `and(cat, dog)` is valid FQL even though `cat` and `dog` are not in double quotation marks. However, we recommend that you use double quotation marks to avoid conflicts with reserved words.</span></span>
  
    
    
<span data-ttu-id="50a7e-p111">Разметка терминов запросов выполняется в соответствии с вашими региональными параметрами. В процессе разметки удаляются некоторые специальные символы. Так как специальные символы удалены, следующие FQL-выражения эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="50a7e-p111">The query terms are tokenized according to your locale setting. The tokenization process removes certain special characters. Because special characters are removed, the following FQL expressions are equivalent.</span></span>
  
    
    
 `and("[king]", "<queen>")`
  
    
    
 `and("king", "queen")`
  
    
    
<span data-ttu-id="50a7e-p112">Операторы FQL</span><span class="sxs-lookup"><span data-stu-id="50a7e-p112">When a query includes terms from user input or another application, use the  `string("<query terms>", mode="AND|OR|PHRASE")` operator to avoid conflict with reserved words in the query language. You must also remove possible double quotation marks from the user-provided query.</span></span>
  
    
    

## <a name="fql-operators"></a><span data-ttu-id="50a7e-206">Операторы FQL</span><span class="sxs-lookup"><span data-stu-id="50a7e-206">FQL Operators</span></span>
<span data-ttu-id="50a7e-207"><a name="fql_operators"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-207"></span></span>

<span data-ttu-id="50a7e-p113">В данном синтаксисе:</span><span class="sxs-lookup"><span data-stu-id="50a7e-p113">FAST Query Language (FQL) operators are keywords that specify Boolean operations or other constraints to operands. The FQL operator syntax is as follows:</span></span>
  
    
    
 `[property-spec:]operator(operand [,operand]* [, parameter="value"]*)`
  
    
    
<span data-ttu-id="50a7e-210">В этом синтаксисе:</span><span class="sxs-lookup"><span data-stu-id="50a7e-210">In the syntax:</span></span>
  
    
    

-  <span data-ttu-id="50a7e-211">_operator_  это ключевое слово, обозначающее операцию, которую необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="50a7e-211">_property-spec_ is an optional property specification followed by the "in" operator.</span></span>
    
  
-  <span data-ttu-id="50a7e-212">_operand_  это выражение с термином или другой оператор.</span><span class="sxs-lookup"><span data-stu-id="50a7e-212">_operator_ is a keyword that specifies an operation to perform.</span></span>
    
  
-  <span data-ttu-id="50a7e-213">_parameter_  это имя значения, которое изменяет поведение оператора.</span><span class="sxs-lookup"><span data-stu-id="50a7e-213">_operand_ is a term expression or another operator.</span></span>
    
  
-  <span data-ttu-id="50a7e-214">_value_  это значение для имени параметра.</span><span class="sxs-lookup"><span data-stu-id="50a7e-214">_parameter_ is the name of a value that changes the behavior of the operator.</span></span>
    
  
-  <span data-ttu-id="50a7e-215">Регистр имен операторов, имен и текстовых значений параметров не учитывается. Пробелы в теле оператора допускаются, но игнорируются, если они не заключены в двойные кавычки. Длина FQL-запросов ограничена 2048 символами.</span><span class="sxs-lookup"><span data-stu-id="50a7e-215">_value_ is the value to use for the parameter name.</span></span>
    
  
<span data-ttu-id="50a7e-p114">В таблице 3 перечислены типы операторов, поддерживаемые FQL.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p114">Operator names, parameter names, and parameter text values are case-insensitive. White space is allowed within the operator body, but is ignored unless it is enclosed in double quotation marks. The length of FAST Query Language queries is limited to 2,048 characters.</span></span>
  
    
    
<span data-ttu-id="50a7e-219">В таблице 3 перечислены типы операторов, поддерживаемые в языке FQL.</span><span class="sxs-lookup"><span data-stu-id="50a7e-219">Table 3 lists the types of operators supported by FQL.</span></span> 
  
    
    

<span data-ttu-id="50a7e-220">**Тип**</span><span class="sxs-lookup"><span data-stu-id="50a7e-220">**Table 3. FQL supported operator types**</span></span>


|<span data-ttu-id="50a7e-221">**Тип**</span><span class="sxs-lookup"><span data-stu-id="50a7e-221">**Type**</span></span>|<span data-ttu-id="50a7e-222">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-222">**Description**</span></span>|<span data-ttu-id="50a7e-223">Строка</span><span class="sxs-lookup"><span data-stu-id="50a7e-223">**Operators**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="50a7e-224">String</span><span class="sxs-lookup"><span data-stu-id="50a7e-224">String</span></span>  <br/> |<span data-ttu-id="50a7e-p115">Позволяет указывать операции запросов в строке терминов. Этот оператор чаще всего используется с текстовыми терминами.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p115">Enables you to specify query operations on a string of terms. This is the most common operator to use on text terms.</span></span>  <br/> | <span data-ttu-id="50a7e-227">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-227">[STRING](fast-query-language-fql-syntax-reference.md#fql_string_operator)</span></span> <br/> |
|<span data-ttu-id="50a7e-228">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-228">Boolean</span></span>  <br/> |<span data-ttu-id="50a7e-229">Позволяет объединять термины и части выражений в запросе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-229">Enables you to combine terms and sub-expressions in a query.</span></span>  <br/> | <span data-ttu-id="50a7e-230">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-230">[AND](fast-query-language-fql-syntax-reference.md#fql_and_operator),  [OR](fast-query-language-fql-syntax-reference.md#fql_or_operator),  [ANY](fast-query-language-fql-syntax-reference.md#fql_any_operator),  [ANDNOT](fast-query-language-fql-syntax-reference.md#fql_andnot_operator),  [NOT](fast-query-language-fql-syntax-reference.md#fql_not_operator),  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator),  [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator)</span></span> <br/> |
|<span data-ttu-id="50a7e-231">Компонент ранжирования с учетом расположения</span><span class="sxs-lookup"><span data-stu-id="50a7e-231">Proximity</span></span>  <br/> |<span data-ttu-id="50a7e-232">Позволяет указывать удаленность от терминов запроса в соответствующей текстовой последовательности.</span><span class="sxs-lookup"><span data-stu-id="50a7e-232">Enables you to specify the proximity of the query terms in a matching sequence of text.</span></span>  <br/> | <span data-ttu-id="50a7e-233">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-233">[NEAR](fast-query-language-fql-syntax-reference.md#fql_near_operator),  [ONEAR](fast-query-language-fql-syntax-reference.md#fql_onear_operator),  [PHRASE](fast-query-language-fql-syntax-reference.md#fql_phrase_operator),  [STARTS-WITH](fast-query-language-fql-syntax-reference.md#fql_startswith_operator),  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator),  [EQUALS](fast-query-language-fql-syntax-reference.md#fql_equals_operator)</span></span> <br/> |
|<span data-ttu-id="50a7e-234">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-234">Numeric</span></span>  <br/> |<span data-ttu-id="50a7e-235">Позволяет указывать числовые условия в запросе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-235">Enables you to specify numeric conditions in the query.</span></span>  <br/> | <span data-ttu-id="50a7e-236">Релевантность</span><span class="sxs-lookup"><span data-stu-id="50a7e-236">[RANGE](fast-query-language-fql-syntax-reference.md#fql_range_operator) , [INT](fast-query-language-fql-syntax-reference.md#fql_int_operator),  [FLOAT](fast-query-language-fql-syntax-reference.md#fql_float_operator),  [DATETIME](fast-query-language-fql-syntax-reference.md#fql_datetime_operator),  [DECIMAL](#fql_decimal_operator)</span></span> <br/> |
|<span data-ttu-id="50a7e-237">Важность</span><span class="sxs-lookup"><span data-stu-id="50a7e-237">Relevance</span></span>  <br/> |<span data-ttu-id="50a7e-238">Позволяет повлиять на оценку релевантности запроса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-238">Enables you to impact the relevance evaluation of a query.</span></span>  <br/> | <span data-ttu-id="50a7e-239">[XRANK](fast-query-language-fql-syntax-reference.md#fql_xrank_operator) и [FILTER](fast-query-language-fql-syntax-reference.md#fql_filter_operator)</span><span class="sxs-lookup"><span data-stu-id="50a7e-239">[XRANK](fast-query-language-fql-syntax-reference.md#fql_xrank_operator) and  [FILTER](fast-query-language-fql-syntax-reference.md#fql_filter_operator)</span></span> <br/> |
   
<span data-ttu-id="50a7e-240">В таблице 4 представлен список поддерживаемых операторов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-240">Table 4 provides a list of the supported operators.</span></span>
  
    
    

<span data-ttu-id="50a7e-241">**Оператор**</span><span class="sxs-lookup"><span data-stu-id="50a7e-241">**Table 4. FQL supported operators**</span></span>


|<span data-ttu-id="50a7e-242">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-242">**Operator**</span></span>|<span data-ttu-id="50a7e-243">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-243">**Description**</span></span>|<span data-ttu-id="50a7e-244">**Тип**</span><span class="sxs-lookup"><span data-stu-id="50a7e-244">**Type**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-245">Возвращает только элементы, которые соответствуют всем операндам [AND](fast-query-language-fql-syntax-reference.md#fql_and_operator).</span><span class="sxs-lookup"><span data-stu-id="50a7e-245">[AND](fast-query-language-fql-syntax-reference.md#fql_and_operator)</span></span> <br/> |<span data-ttu-id="50a7e-246">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-246">Returns only items that match all **AND** operands.</span></span> <br/> |<span data-ttu-id="50a7e-247">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-247">Boolean</span></span>  <br/> |
| <span data-ttu-id="50a7e-248">Возвращает только элементы, которые соответствуют первому операнду и не соответствуют последующим операндам.</span><span class="sxs-lookup"><span data-stu-id="50a7e-248">[ANDNOT](fast-query-language-fql-syntax-reference.md#fql_andnot_operator)</span></span> <br/> |<span data-ttu-id="50a7e-249">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-249">Returns only items that match the first operand and that don't match the subsequent operands.</span></span>  <br/> |<span data-ttu-id="50a7e-250">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-250">Boolean</span></span>  <br/> |
| [<span data-ttu-id="50a7e-251">ANY</span><span class="sxs-lookup"><span data-stu-id="50a7e-251">ANY</span></span>](fast-query-language-fql-syntax-reference.md#fql_any_operator) <br/> |<span data-ttu-id="50a7e-252">Аналогичен оператору **OR**, но на динамический ранг (степень релевантности в результирующем наборе) не влияет ни количество совпадающих операндов, ни расстояние между терминами в элементе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-252">Similar to the **OR** operator except that the dynamic rank (the relevance score in the result set) is affected by neither the number of operands that match nor the distance between the terms in the item.</span></span> <br/> |<span data-ttu-id="50a7e-253">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-253">Boolean</span></span>  <br/> |
| <span data-ttu-id="50a7e-254">Позволяет указывать, сколько терминов запроса должен включать элемент, чтобы он был возвращен в качестве результата. Операндом может быть один термин запроса, фраза или термин запроса с подстановочными знаками.</span><span class="sxs-lookup"><span data-stu-id="50a7e-254">[COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator)</span></span> <br/> |<span data-ttu-id="50a7e-p116">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-p116">Enables you to specify the number of query term occurrences an item must include to be returned as a result. The operand may be a single query term, a phrase, or wildcard query term.</span></span>  <br/> |<span data-ttu-id="50a7e-257">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-257">Boolean</span></span>  <br/> |
| <span data-ttu-id="50a7e-258">Позволяет явно задавать тип числовых значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-258">[DATETIME](fast-query-language-fql-syntax-reference.md#fql_datetime_operator)</span></span> <br/> |<span data-ttu-id="50a7e-259">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-259">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="50a7e-p117">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-p117">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-262">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-262">Numeric</span></span>  <br/> |
| <span data-ttu-id="50a7e-263">Позволяет явно задавать тип числовых значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-263">[DECIMAL](fast-query-language-fql-syntax-reference.md#fql_decimal_operator)</span></span> <br/> |<span data-ttu-id="50a7e-264">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-264">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="50a7e-p118">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-p118">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-267">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-267">Numeric</span></span>  <br/> |
| <span data-ttu-id="50a7e-268">Указывает необходимость наличия слова или фразы в конце управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-268">[ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator)</span></span> <br/> |<span data-ttu-id="50a7e-269">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-269">Specifies that a word or phrase must appear in the end of a managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-270">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-270">Proximity</span></span>  <br/> |
| <span data-ttu-id="50a7e-271">Указывает, что слово или фраза должна точно соответствовать управляемому свойству.</span><span class="sxs-lookup"><span data-stu-id="50a7e-271">[EQUALS](fast-query-language-fql-syntax-reference.md#fql_equals_operator)</span></span> <br/> |<span data-ttu-id="50a7e-272">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-272">Specifies that a word or phrase term or phrase must provide an exact token match with the managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-273">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-273">Proximity</span></span>  <br/> |
| <span data-ttu-id="50a7e-274">Используется для запроса метаданных или других структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="50a7e-274">[FILTER](fast-query-language-fql-syntax-reference.md#fql_filter_operator)</span></span> <br/> |<span data-ttu-id="50a7e-275">Релевантность</span><span class="sxs-lookup"><span data-stu-id="50a7e-275">Used to query metadata or other structured data.</span></span>  <br/> |<span data-ttu-id="50a7e-276">Релевантность</span><span class="sxs-lookup"><span data-stu-id="50a7e-276">Relevance</span></span>  <br/> |
| <span data-ttu-id="50a7e-277">Позволяет явно задавать тип числовых значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-277">[FLOAT](fast-query-language-fql-syntax-reference.md#fql_float_operator)</span></span> <br/> |<span data-ttu-id="50a7e-278">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-278">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="50a7e-p119">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-p119">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-281">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-281">Numeric</span></span>  <br/> |
| <span data-ttu-id="50a7e-282">Позволяет явно задавать тип числовых значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-282">[INT](fast-query-language-fql-syntax-reference.md#fql_int_operator)</span></span> <br/> |<span data-ttu-id="50a7e-283">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-283">Provides explicit typing of numeric values.</span></span>  <br/> <span data-ttu-id="50a7e-p120">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-p120">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-286">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-286">Numeric</span></span>  <br/> |
| [<span data-ttu-id="50a7e-287">NEAR</span><span class="sxs-lookup"><span data-stu-id="50a7e-287">NEAR</span></span>](fast-query-language-fql-syntax-reference.md#fql_near_operator) <br/> |<span data-ttu-id="50a7e-288">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-288">Restricts the result set to items that have  `N` terms within a certain distance of one another.</span></span> <br/> |<span data-ttu-id="50a7e-289">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-289">Proximity</span></span>  <br/> |
| <span data-ttu-id="50a7e-290">Возвращает только термины, которые не включают операнд.</span><span class="sxs-lookup"><span data-stu-id="50a7e-290">[NOT](fast-query-language-fql-syntax-reference.md#fql_not_operator)</span></span> <br/> |<span data-ttu-id="50a7e-291">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-291">Returns only items that exclude the operand.</span></span>  <br/> |<span data-ttu-id="50a7e-292">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-292">Boolean</span></span>  <br/> |
| [<span data-ttu-id="50a7e-293">ONEAR</span><span class="sxs-lookup"><span data-stu-id="50a7e-293">ONEAR</span></span>](fast-query-language-fql-syntax-reference.md#fql_onear_operator) <br/> |<span data-ttu-id="50a7e-p121">Расстояние </span><span class="sxs-lookup"><span data-stu-id="50a7e-p121">The ordered variant of **NEAR**, and requires an ordered match of the terms. The **ONEAR** operator can be used to restrict the result set to items that have `N` terms within a certain distance of Returns only items that don't match the operand. The operand may be any valid FQL expression.one another. </span></span><br/> |<span data-ttu-id="50a7e-297">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-297">Proximity</span></span>  <br/> |
| [<span data-ttu-id="50a7e-298">OR</span><span class="sxs-lookup"><span data-stu-id="50a7e-298">OR</span></span>](fast-query-language-fql-syntax-reference.md#fql_or_operator) <br/> |<span data-ttu-id="50a7e-299">Возвращает только те элементы, которые совпадают по крайней мере с одним из операндов выражения **OR**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-299">Returns only items that match at least one of the **OR** operands.</span></span> <span data-ttu-id="50a7e-300">Совпадающим элементам назначается более высокий динамический ранг (степень релевантности в результирующем наборе), если обнаружено больше совпадающих операндов выражения **OR**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-300">Returns only items that match at least one of the OR operands. Items that match will get a higher dynamic rank (relevance score in the result set) if more of the **OR** operands match.</span></span> <br/> |<span data-ttu-id="50a7e-301">Логический</span><span class="sxs-lookup"><span data-stu-id="50a7e-301">Boolean</span></span>  <br/> |
| <span data-ttu-id="50a7e-302">Возвращает только элементы, которые соответствуют определенной строке маркеров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-302">[PHRASE](fast-query-language-fql-syntax-reference.md#fql_phrase_operator)</span></span> <br/> | <span data-ttu-id="50a7e-303">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-303">Returns only items that match an exact string of tokens.</span></span> <br/> |<span data-ttu-id="50a7e-304">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-304">Proximity</span></span>  <br/> |
| <span data-ttu-id="50a7e-305">Позволяет использовать выражения соответствия диапазонам. Оператор [RANGE](fast-query-language-fql-syntax-reference.md#fql_range_operator) используется для числовых управляемых свойств и управляемых свойств даты и времени.</span><span class="sxs-lookup"><span data-stu-id="50a7e-305">[RANGE](fast-query-language-fql-syntax-reference.md#fql_range_operator)</span></span> <br/> | <span data-ttu-id="50a7e-p123">Числовой </span><span class="sxs-lookup"><span data-stu-id="50a7e-p123">Enables range matching expressions. The **RANGE** operator is used for numeric and date/time managed properties. </span></span><br/> |<span data-ttu-id="50a7e-308">Числовой</span><span class="sxs-lookup"><span data-stu-id="50a7e-308">Numeric</span></span>  <br/> |
| <span data-ttu-id="50a7e-309">Указывает необходимость расположения слова или фразы в начале управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-309">[STARTS-WITH](fast-query-language-fql-syntax-reference.md#fql_startswith_operator)</span></span> <br/> |<span data-ttu-id="50a7e-310">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-310">Specifies that a word or phrase must appear in the start of a managed property.</span></span>  <br/> |<span data-ttu-id="50a7e-311">Расстояние</span><span class="sxs-lookup"><span data-stu-id="50a7e-311">Proximity</span></span>  <br/> |
| <span data-ttu-id="50a7e-312">Задает логическое условие соответствия для текстовой строки.</span><span class="sxs-lookup"><span data-stu-id="50a7e-312">[STRING](fast-query-language-fql-syntax-reference.md#fql_string_operator)</span></span> <br/> |<span data-ttu-id="50a7e-313">Строка</span><span class="sxs-lookup"><span data-stu-id="50a7e-313">Define a Boolean matching condition to a text string.</span></span>  <br/> |<span data-ttu-id="50a7e-314">Строка</span><span class="sxs-lookup"><span data-stu-id="50a7e-314">String</span></span>  <br/> |
| <span data-ttu-id="50a7e-315">Позволяет повысить динамический рейтинг элементов на основе наличия определенных терминов. Выражение [XRANK](fast-query-language-fql-syntax-reference.md#fql_xrank_operator) содержит один компонент, который должен совпадать, и один или несколько компонентов, которые только увеличивают динамический рейтинг.</span><span class="sxs-lookup"><span data-stu-id="50a7e-315">[XRANK](fast-query-language-fql-syntax-reference.md#fql_xrank_operator)</span></span> <br/> |<span data-ttu-id="50a7e-p124">Релевантность </span><span class="sxs-lookup"><span data-stu-id="50a7e-p124">Enables you to boost the dynamic rank of items based on certain term occurrences without changing which items match the query. A **XRANK** expression contains one component that must be matched, and one or more components that contribute only to dynamic ranking. </span></span><br/> |<span data-ttu-id="50a7e-318">Релевантность</span><span class="sxs-lookup"><span data-stu-id="50a7e-318">Relevance</span></span>  <br/> |
   

> <span data-ttu-id="50a7e-319">**Примечание.** В SharePoint оператор **RANK** является нерекомендуемым и больше не оказывает никакого влияния.</span><span class="sxs-lookup"><span data-stu-id="50a7e-319">**NOTE** In SharePoint 2013, the **RANK** operator is deprecated and will no longer have any effect. Use XRANK instead.</span></span> <span data-ttu-id="50a7e-320">Используйте вместо него оператор **XRANK**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-320">Use **XRANK** instead.</span></span>
  
    
    


### <a name="and"></a><span data-ttu-id="50a7e-321">AND</span><span class="sxs-lookup"><span data-stu-id="50a7e-321">AND</span></span>
<span data-ttu-id="50a7e-322"><a name="fql_and_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-322"></span></span>

<span data-ttu-id="50a7e-p126">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p126">Returns only items that match all **AND** operands. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-325">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-325">Syntax</span></span>

 `and(operand, operand [, operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-326">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-326">Parameters</span></span>

<span data-ttu-id="50a7e-327">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-327">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-328">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-328">Examples</span></span>

<span data-ttu-id="50a7e-329">ANDNOT</span><span class="sxs-lookup"><span data-stu-id="50a7e-329">The following expression matches items for which the default full-text index contains "cat", "dog", and "fox".</span></span>
  
    
    
 `and(cat, dog, fox)`
  
    
    

### <a name="andnot"></a><span data-ttu-id="50a7e-330">ANDNOT</span><span class="sxs-lookup"><span data-stu-id="50a7e-330">ANDNOT</span></span>
<span data-ttu-id="50a7e-331"><a name="fql_andnot_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-331"></span></span>

<span data-ttu-id="50a7e-p127">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p127">Returns only items that match the first operand and that don't match the subsequent operands. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-334">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-334">Syntax</span></span>

 `andnot(operand, operand [,operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-335">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-335">Parameters</span></span>

<span data-ttu-id="50a7e-336">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-336">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-337">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-337">Examples</span></span>

 <span data-ttu-id="50a7e-p128">**Пример 2.** Следующее выражение соответствует элементам, для которых полнотекстовый индекс по умолчанию содержит слово "cat" и не содержит ни "dog", ни "chihuahua".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p128">**Example 1.** The following expression matches items for which the default full-text index contains "cat" but not "dog".</span></span>
  
    
    
 `andnot(cat, dog)`
  
    
    
 <span data-ttu-id="50a7e-p129">ANY</span><span class="sxs-lookup"><span data-stu-id="50a7e-p129">**Example 2.** The following expression matches items for which the default full-text index contains "dog" but neither "beagle" nor "chihuahua".</span></span>
  
    
    
 `andnot(dog, beagle, chihuahua)`
  
    
    

### <a name="any"></a><span data-ttu-id="50a7e-342">ANY</span><span class="sxs-lookup"><span data-stu-id="50a7e-342">ANY</span></span>
<span data-ttu-id="50a7e-343"><a name="fql_any_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-343"></span></span>


> <span data-ttu-id="50a7e-344">**Примечание.** В SharePoint оператор **ANY** является нерекомендуемым.</span><span class="sxs-lookup"><span data-stu-id="50a7e-344">**Note:** In SharePoint, the **ANY** operator is deprecated.</span></span> <span data-ttu-id="50a7e-345">Используйте вместо него оператор **OR**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-345">Use the **OR** operator instead.</span></span>
  
    
    

<span data-ttu-id="50a7e-p131">Компонент динамического рейтинга для этой части запроса основан на наиболее подходящем термине в выражении [ANY](fast-query-language-fql-syntax-reference.md#fql_or_operator).</span><span class="sxs-lookup"><span data-stu-id="50a7e-p131">Similar to the  [OR](fast-query-language-fql-syntax-reference.md#fql_or_operator) operator except that the dynamic rank (the relevance score in the result set) is affected by neither the number of operands that match nor the distance between the terms in the item. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    
<span data-ttu-id="50a7e-348">Динамический компонент ранжирования для этой части запроса основан на самом подходящем термине из выражения **ANY**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-348">The dynamic ranking component for this part of the query is based on the best matching term within the **ANY** expression.</span></span>
  
    
    

> <span data-ttu-id="50a7e-349">**Примечание.** Отличие от оператора **OR** заключается только в ранжировании в рамках результирующего набора.</span><span class="sxs-lookup"><span data-stu-id="50a7e-349">The difference from **OR** is related only to the ranking within the result set. The same total set of items will match the query.</span></span> <span data-ttu-id="50a7e-350">Запросу будет соответствовать тот же общий набор элементов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-350">The difference from OR is related only to the ranking within the result set. The same total set of items will match the query.</span></span>
  
    
    


#### <a name="syntax"></a><span data-ttu-id="50a7e-351">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-351">Syntax</span></span>

 `any(operand, operand [,operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-352">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-352">Parameters</span></span>

<span data-ttu-id="50a7e-353">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-353">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-354">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-354">Examples</span></span>

 <span data-ttu-id="50a7e-355">Если индекс содержит и "cat", и "dog", но слово "cat" считается лучшим соответствием, динамический рейтинг элемента будет основан на слове "cat" без учета "dog".</span><span class="sxs-lookup"><span data-stu-id="50a7e-355">The following expression matches items for which the default full-text index contains "cat" or "dog".</span></span>
  
    
    
<span data-ttu-id="50a7e-356">COUNT</span><span class="sxs-lookup"><span data-stu-id="50a7e-356">If the index contains both "cat" and "dog", but "cat" is considered a better match, the 'item's dynamic rank will be based on "cat" with no consideration given to "dog".</span></span>
  
    
    
 `any(cat, dog)`
  
    
    

### <a name="count"></a><span data-ttu-id="50a7e-357">COUNT</span><span class="sxs-lookup"><span data-stu-id="50a7e-357">COUNT</span></span>
<span data-ttu-id="50a7e-358"><a name="fql_count_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-358"></span></span>

<span data-ttu-id="50a7e-p133">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p133">Specifies the of number query term occurrences an item must include for the item to be returned as a result. The operand may be a single query term, a phrase, or a wildcard query term.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-361">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-361">Syntax</span></span>

 `property-spec:count(operand [,from=<numeric value>, to=<numeric value>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-362">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-362">Parameters</span></span>



|<span data-ttu-id="50a7e-363">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-363">**Parameter**</span></span>|<span data-ttu-id="50a7e-364">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-364">**Value**</span></span>|<span data-ttu-id="50a7e-365">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-365">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-366">_From_</span><span class="sxs-lookup"><span data-stu-id="50a7e-366">_From_</span></span> <br/> | <span data-ttu-id="50a7e-367">_\<числовое_значение\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-367">_\<<numeric_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-368">Если параметр  _from_ не указан, нижнего предела не будет.</span><span class="sxs-lookup"><span data-stu-id="50a7e-368">The value of the  _from_ parameter must be a positive integer that specifies the minimum number of times that the specified operand must be matched.</span></span> <br/> <span data-ttu-id="50a7e-369">_to_</span><span class="sxs-lookup"><span data-stu-id="50a7e-369">If the  _from_ parameter is not specified, no lower limit will exist.</span></span> <br/> |
| <span data-ttu-id="50a7e-370">_to_</span><span class="sxs-lookup"><span data-stu-id="50a7e-370">_to_</span></span> <br/> | <span data-ttu-id="50a7e-371">_\<числовое_значение\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-371"> <numeric_value></span></span> <br/> |<span data-ttu-id="50a7e-372">Значение параметра _to_ должно быть положительным целым числом, задающим максимальное количество совпадений указанного операнда (не включая верхнюю границу).</span><span class="sxs-lookup"><span data-stu-id="50a7e-372">The value of the  _from_ parameter must be a positive integer that specifies the minimum number of times that the specified operand must be matched.</span></span> <span data-ttu-id="50a7e-373">Например, значение **11** параметра _to_ обозначает не более 10 совпадений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-373">For example, a _to_ value of **11** specifies 10 times or fewer.</span></span> <br/> <span data-ttu-id="50a7e-374">Если параметр _to_ не задан, верхняя граница отсутствует.</span><span class="sxs-lookup"><span data-stu-id="50a7e-374">If the  _to_ parameter is not specified, no upper limit will exist.</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="50a7e-375">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-375">Examples</span></span>

 <span data-ttu-id="50a7e-p135">**Пример 2.** Следующее выражение соответствует элементам, содержащим по крайней мере 5, но менее 10 слов "cat".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p135">**Example 1.** The following expression matches at least 5 occurrences of the word "cat".</span></span>
  
    
    
 `count(cat, from=5)`
  
    
    
 <span data-ttu-id="50a7e-p136">**Пример 3.** Каждое из следующих выражений соответствует элементам, содержащим по крайней мере 3 определенных слова, и этим словом может быть "cat" или "dog".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p136">**Example 2.** The following expression matches at least 5 but not 10 or more occurrences of the word "cat".</span></span>
  
    
    
 `count(cat, from=5, to=10)`
  
    
    
 <span data-ttu-id="50a7e-p137">Следующая таблица содержит примеры соответствия и несоответствия строковых значений и состояний управляемого свойства для примера 3.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p137">**Example 3.** Each of the following expressions matches at least 3 occurrences of a certain word, and that word can be either "cat" or "dog".</span></span>
  
    
    
 `count(or(cat, dog), from=3)count(string("cat dog", mode="or"), from=3)`
  
    
    
<span data-ttu-id="50a7e-382">В приведенной ниже таблице представлены примеры строковых значений управляемых свойств и указано, соответствуют ли они двум выражениям из примера 3.</span><span class="sxs-lookup"><span data-stu-id="50a7e-382">The following table contains examples of managed property string values and states whether they match the two expressions in Example 3.</span></span>
  
    
    


|<span data-ttu-id="50a7e-383">**Текст**</span><span class="sxs-lookup"><span data-stu-id="50a7e-383">**Match?**</span></span>|<span data-ttu-id="50a7e-384">Да</span><span class="sxs-lookup"><span data-stu-id="50a7e-384">**Text**</span></span>|
|:-----|:-----|
|<span data-ttu-id="50a7e-385">Да</span><span class="sxs-lookup"><span data-stu-id="50a7e-385">Yes</span></span>  <br/> |<span data-ttu-id="50a7e-386">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-386">My cat likes my dog, but my dog hates my cat.</span></span>  <br/> |
|<span data-ttu-id="50a7e-387">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-387">No</span></span>  <br/> |<span data-ttu-id="50a7e-388">DATETIME</span><span class="sxs-lookup"><span data-stu-id="50a7e-388">My bird likes my newt, but my dog hates my cat.</span></span>  <br/> |
   

### <a name="datetime"></a><span data-ttu-id="50a7e-389">DATETIME</span><span class="sxs-lookup"><span data-stu-id="50a7e-389">DATETIME</span></span>
<span data-ttu-id="50a7e-390"><a name="fql_datetime_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-390"></span></span>

<span data-ttu-id="50a7e-p138">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p138">Provides explicit typing of date/time numeric values. The operand is a date/time string formatted according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="50a7e-p139">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p139">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-395">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-395">Syntax</span></span>

 `datetime(<date/time string>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-396">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-396">Parameters</span></span>

<span data-ttu-id="50a7e-397">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-397">Not applicable.</span></span>
  
    
    

### <a name="decimal"></a><span data-ttu-id="50a7e-398">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="50a7e-398">DECIMAL</span></span>
<span data-ttu-id="50a7e-399"><a name="fql_decimal_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-399"></span></span>

<span data-ttu-id="50a7e-p140">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p140">Provides explicit typing of decimal values. The operand is a decimal value according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="50a7e-p141">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p141">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-404">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-404">Syntax</span></span>

 `decimal(<decimal point value>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-405">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-405">Parameters</span></span>

<span data-ttu-id="50a7e-406">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-406">Not applicable.</span></span>
  
    
    

### <a name="ends-with"></a><span data-ttu-id="50a7e-407">ENDS-WITH</span><span class="sxs-lookup"><span data-stu-id="50a7e-407">ENDS-WITH</span></span>
<span data-ttu-id="50a7e-408"><a name="fql_endswith_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-408"></span></span>

<span data-ttu-id="50a7e-409">Для числовых управляемых свойств сопоставление границ не поддерживается. Для них поддерживается только точное соответствие и соответствие диапазона значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-409">Specifies that a word or phrase must appear in the end of a managed property (boundary matching).</span></span>
  
    
    
<span data-ttu-id="50a7e-p142">Сопоставление границ не поддерживается для числовых управляемых свойств. С такими свойствами всегда выполняется сопоставление по точному значению или диапазону значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p142">Boundary matching is not supported on numeric managed properties. Numeric managed properties will always be subject to exact or value range matching.</span></span> 
  
    
    
<span data-ttu-id="50a7e-p143">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p143">Some applications may require that you are able to perform an exact match of a managed property. For example, this may be a **product name** managed property, where the full name of one product is a substring of another product name.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-414">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-414">Syntax</span></span>

 `ends-with(<term or phrase>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-415">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-415">Parameters</span></span>

<span data-ttu-id="50a7e-416">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-416">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-417">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-417">Examples</span></span>

<span data-ttu-id="50a7e-p144">Примечания</span><span class="sxs-lookup"><span data-stu-id="50a7e-p144">The following expression matches items with the values "Mr Adam Jones" and "Adam Jones" in the "author" managed property. It will not match items with the value "Adam Jones sr".</span></span>
  
    
    
 `author:ends-with("adam jones")`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-420">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-420">Remarks</span></span>

<span data-ttu-id="50a7e-p145">Чтобы применить запросы сопоставления границ, необходимо настроить соответствующее управляемое свойство в схеме индекса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p145">Boundary matching can be applied to all the text of the managed property, or to individual strings within a managed property that contains a list of string values, for example, a list of names. In this case, you may want to match the exact content of each string, and to avoid query matching across string boundaries.</span></span> 
  
    
    
<span data-ttu-id="50a7e-423">Включив для управляемого свойства функцию сопоставления границ, можно выполнять следующие действия:</span><span class="sxs-lookup"><span data-stu-id="50a7e-423">To apply boundary match queries, you must configure the relevant managed property in the index schema.</span></span> 
  
    
    
<span data-ttu-id="50a7e-424">использовать запросы явного сопоставления границ;</span><span class="sxs-lookup"><span data-stu-id="50a7e-424">By enabling the Boundary Match feature for the managed property, you can do the following:</span></span> 
  
    
    

- <span data-ttu-id="50a7e-425">запретить поиск соответствия фраз за границами строки. Для управляемых свойств, содержащих несколько строк, эта функция блокирует поиск соответствия слов до или после указателя границы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-425">Use explicit boundary match queries.</span></span> 
    
  
- <span data-ttu-id="50a7e-p146">EQUALS</span><span class="sxs-lookup"><span data-stu-id="50a7e-p146">Prevent phrases from matching across string boundaries. For managed properties that contain multiple strings, this feature will ensure that a string does not match words before or after a boundary indication.</span></span>
    
  

### <a name="equals"></a><span data-ttu-id="50a7e-428">EQUALS</span><span class="sxs-lookup"><span data-stu-id="50a7e-428">EQUALS</span></span>
<span data-ttu-id="50a7e-429"><a name="fql_equals_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-429"></span></span>

<span data-ttu-id="50a7e-430">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-430">Specifies that a word or phrase must provide an exact token match with the managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-431">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-431">Syntax</span></span>

 `equals(<term or phrase>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-432">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-432">Parameters</span></span>

<span data-ttu-id="50a7e-433">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-433">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-434">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-434">Examples</span></span>

<span data-ttu-id="50a7e-p147">Примечания</span><span class="sxs-lookup"><span data-stu-id="50a7e-p147">The following example will match items with the values "Adam Jones" in the "author" managed property. It will not match items with the values "Adam Jones sr" or "Mr Adam Jones".</span></span>
  
    
    
 `author:equals("adam jones")`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-437">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-437">Remarks</span></span>

<span data-ttu-id="50a7e-438">FILTER</span><span class="sxs-lookup"><span data-stu-id="50a7e-438">See also  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator).</span></span>
  
    
    

### <a name="filter"></a><span data-ttu-id="50a7e-439">FILTER</span><span class="sxs-lookup"><span data-stu-id="50a7e-439">FILTER</span></span>
<span data-ttu-id="50a7e-440"><a name="fql_filter_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-440"></span></span>

<span data-ttu-id="50a7e-441">Используется для запросов метаданных или других структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="50a7e-441">Used to query metadata or other structured data.</span></span> 
  
    
    
<span data-ttu-id="50a7e-442">Использование оператора **FILTER** автоматически обеспечивает реализацию для запроса следующего:</span><span class="sxs-lookup"><span data-stu-id="50a7e-442">Using the **FILTER** operator automatically implies the following for the specified query:</span></span>
  
    
    

- <span data-ttu-id="50a7e-443">лингвистика будет отключена (linguistics="OFF");</span><span class="sxs-lookup"><span data-stu-id="50a7e-443">Linguistics will be set to linguistics="OFF".</span></span>
    
  
- <span data-ttu-id="50a7e-444">рейтинг будет отключен;</span><span class="sxs-lookup"><span data-stu-id="50a7e-444">Ranking will be disabled.</span></span>
    
  
- <span data-ttu-id="50a7e-445">в сводке с выделенными совпадениями для результата запроса не будет использоваться выделение запросов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-445">No query highlighting will be used in the hit highlighted summary for the query result hit.</span></span>
    
  

> <span data-ttu-id="50a7e-446">**Совет.** Если оператор **STRING** используется в выражении **FILTER**, по умолчанию лингвистическая обработка отключается.</span><span class="sxs-lookup"><span data-stu-id="50a7e-446">**TIP** If you use the **STRING** operator inside a **FILTER** expression, by default, linguistics is disabled. You can enable linguistics processing within each STRING expression inside FILTER by using the operand .</span></span> <span data-ttu-id="50a7e-447">Вы можете включить лингвистическую обработку в каждом выражении **STRING** внутри оператора **FILTER** с помощью операнда `linguistics="ON"`.</span><span class="sxs-lookup"><span data-stu-id="50a7e-447">TIP If you use the STRING operator inside a FILTER expression, by default, linguistics is disabled. You can enable linguistics processing within each **STRING** expression inside **FILTER** by using the operand `linguistics="ON"`.</span></span> 
  
    
    


#### <a name="syntax"></a><span data-ttu-id="50a7e-448">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-448">Syntax</span></span>

 `filter(<any valid FQL operator expression>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-449">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-449">Parameters</span></span>

<span data-ttu-id="50a7e-450">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-450">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-451">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-451">Examples</span></span>

<span data-ttu-id="50a7e-p149">Примечания</span><span class="sxs-lookup"><span data-stu-id="50a7e-p149">The following expression matches items that have a **Title** managed property that contains "sonata" and a **Doctype** managed property that contains only the token "audio". No linguistic matching will be performed on "audio". Because the **FILTER** token will be used to match "audio", that text will not be highlighted in the hit highlighted summary.</span></span>
  
    
    
 `and(title:sonata, filter(doctype:equals("audio")))`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-455">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-455">Remarks</span></span>

<span data-ttu-id="50a7e-456">Если необходимо ограничить запрос, чтобы он соответствовал по крайней мере одному из большого набора целых значений в числовом свойстве, вы можете сделать это двумя функционально эквивалентными способами:</span><span class="sxs-lookup"><span data-stu-id="50a7e-456">If you must restrict your query to match at least one of a large set of integer values in a numeric property, you can express this in two functionally equivalent ways:</span></span> 
  
    
    

-  `and(string("hello world"), filter(property-spec:or(1, 20, 453, ... , 3473)))`
    
  
-  `and(string("hello world"), filter(property-spec:int("1 20 453 ... 3473", mode="or")))`
    
  
<span data-ttu-id="50a7e-p150">Если вам необходимо отфильтровать большой набор значений, рекомендуем использовать числовые значения вместо строковых и выразить свои запросы с помощью оптимизированного синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p150">The second example uses the **INT** operator by using a string with the set of numeric values in double quotation marks. This provides a significantly better query performance when filtering with a large set of numeric values.</span></span>
  
    
    
<span data-ttu-id="50a7e-459">FLOAT</span><span class="sxs-lookup"><span data-stu-id="50a7e-459">If you must filter a large set of values, you should consider using numeric values instead of string values, and express your queries by using the optimized syntax.</span></span>
  
    
    

### <a name="float"></a><span data-ttu-id="50a7e-460">FLOAT</span><span class="sxs-lookup"><span data-stu-id="50a7e-460">FLOAT</span></span>
<span data-ttu-id="50a7e-461"><a name="fql_float_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-461"></span></span>

<span data-ttu-id="50a7e-p151">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p151">Provides explicit typing of floating point numeric values. The operand is a floating point value according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="50a7e-p152">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p152">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-466">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-466">Syntax</span></span>

 `float(<floating point value>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-467">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-467">Parameters</span></span>

<span data-ttu-id="50a7e-468">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-468">Not applicable.</span></span>
  
    
    

### <a name="int"></a><span data-ttu-id="50a7e-469">INT</span><span class="sxs-lookup"><span data-stu-id="50a7e-469">INT</span></span>
<span data-ttu-id="50a7e-470"><a name="fql_int_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-470"></span></span>

<span data-ttu-id="50a7e-p153">Явное преобразование типа необязательно и обычно не требуется. Тип термина запроса определяется в соответствии с типом целевого числового управляемого свойства.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p153">Provides explicit typing of integer values. The operand is an integer value according to the syntax specified in  [Token expressions in FQL](fast-query-language-fql-syntax-reference.md#token_expressions).</span></span>
  
    
    
<span data-ttu-id="50a7e-p154">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p154">The explicit type conversion is optional and usually is not needed. The type of the query term is detected according to the type of the target numeric managed property.</span></span>
  
    
    
<span data-ttu-id="50a7e-p155">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p155">The **INT** operator can also be used to express a set of integer values as arguments to Boolean FQL operators. This provides a performance efficient way to provide a set of integer values in a query, as the values that are passed by using the **INT** operator are not parsed by the FQL query parser but passed directly to the query matching component.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-477">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-477">Syntax</span></span>

 `int(<integer value>)`
  
    
    
 `int("value, value, ??? , value")`
  
    
    
<span data-ttu-id="50a7e-p156">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-p156">The first syntax specifies a single integer. The second syntax specifies a comma-separated list of integer values enclosed in double quotation marks.</span></span>
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-480">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-480">Parameters</span></span>

<span data-ttu-id="50a7e-481">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-481">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-482">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-482">Examples</span></span>

<span data-ttu-id="50a7e-483">NEAR</span><span class="sxs-lookup"><span data-stu-id="50a7e-483">If you need to restrict your query to match at least one of a large set of integer values in a numeric property, you can express this by using the **INT** operator:</span></span>
  
    
    
 `and(string("hello world"), filter(id:int("1 20 49 124 453 985 3473", mode="or")))`
  
    
    

### <a name="near"></a><span data-ttu-id="50a7e-484">NEAR</span><span class="sxs-lookup"><span data-stu-id="50a7e-484">NEAR</span></span>
<span data-ttu-id="50a7e-485"><a name="fql_near_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-485"></span></span>

<span data-ttu-id="50a7e-486">Порядок терминов запроса для сопоставления не играет роли, важно только расстояние.</span><span class="sxs-lookup"><span data-stu-id="50a7e-486">Restricts the result set to items that have  _N_ terms within a certain distance of one another.</span></span>
  
    
    
<span data-ttu-id="50a7e-487">При сопоставлении не учитывается порядок терминов запроса, только расстояние.</span><span class="sxs-lookup"><span data-stu-id="50a7e-487">The order of the query terms is not important for the matching, only the distance.</span></span> 
  
    
    
<span data-ttu-id="50a7e-488">С операторами **NEAR** можно совмещать любое количество терминов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-488">Any number of terms can be combined with the **NEAR** operators.</span></span>
  
    
    
 <span data-ttu-id="50a7e-489">Операндами выражения **NEAR** могут быть отдельные термины, фразы или логические выражения с операторами **OR** или **ANY**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-489">**NEAR** operands may be single terms, phrases, or Boolean **OR** or **ANY** operator expressions. Wildcards are accepted.</span></span> <span data-ttu-id="50a7e-490">Подстановочные знаки поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="50a7e-490">Wildcards are accepted.</span></span>
  
    
    
<span data-ttu-id="50a7e-491">Если несколько операндов в операторе **NEAR** совпадают с одним и тем же индексированным маркером, то они считаются смежными.</span><span class="sxs-lookup"><span data-stu-id="50a7e-491">If multiple operands of the **NEAR** operator match the same indexed token, they are considered near one another.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-492">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-492">Syntax</span></span>

 `near(arg, arg [, arg]* [, N=<numeric value>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-493">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-493">Parameters</span></span>



|<span data-ttu-id="50a7e-494">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-494">**Parameter**</span></span>|<span data-ttu-id="50a7e-495">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-495">**Value**</span></span>|<span data-ttu-id="50a7e-496">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-496">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-497">_N_</span><span class="sxs-lookup"><span data-stu-id="50a7e-497">_N_</span></span> <br/> | <span data-ttu-id="50a7e-498">_\<числовое_значение\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-498">_\<<numeric_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-499">Задает максимальное количество слов, которые могут отображаться между терминами (явное расстояние).</span><span class="sxs-lookup"><span data-stu-id="50a7e-499">Specifies the maximum number of words that is allowed to appear between the terms (explicit proximity).</span></span>  <br/> <span data-ttu-id="50a7e-500">Если оператор **NEAR** включает более двух операндов, то максимальное количество слов между терминами (_N_) рассчитывается в пределах целого выражения.</span><span class="sxs-lookup"><span data-stu-id="50a7e-500">If **NEAR** includes more than two operands, the maximum number of words allowed between the terms (_N_) is counted within the whole expression.</span></span>  <br/> <span data-ttu-id="50a7e-501">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-501">Default: **4**</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="50a7e-502">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-502">Examples</span></span>

 <span data-ttu-id="50a7e-p158">**Пример 2.** Следующее выражение соответствует строкам, которые содержат слова "cat", "dog", "fox" и "wolf", если их разделяет не более четырех индексированных маркеров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p158">**Example 1.** The following expression matches strings that contain both "cat" and "dog" if no more than four indexed tokens (default) separate them.</span></span>
  
    
    
 `near(cat, dog)`
  
    
    
 <span data-ttu-id="50a7e-p159">В следующей таблице приведены примеры соответствия и несоответствия строковых значений и состояний управляемого свойства для примера 2.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p159">**Example 2.** The following expression matches strings that contain "cat", "dog", "fox", and "wolf" if no more than four indexed tokens separate them.</span></span>
  
    
    
 `near(cat, dog, fox, wolf)`
  
    
    
<span data-ttu-id="50a7e-507">В приведенной ниже таблице представлены примеры строковых значений управляемых свойств и указано, соответствуют ли они предыдущему выражению из примера 2.</span><span class="sxs-lookup"><span data-stu-id="50a7e-507">The following table contains examples of managed property string values and states whether they match the previous expression in Example 2.</span></span>
  
    
    


|<span data-ttu-id="50a7e-508">**Текст**</span><span class="sxs-lookup"><span data-stu-id="50a7e-508">**Match?**</span></span>|<span data-ttu-id="50a7e-509">Да</span><span class="sxs-lookup"><span data-stu-id="50a7e-509">**Text**</span></span>|
|:-----|:-----|
|<span data-ttu-id="50a7e-510">Да</span><span class="sxs-lookup"><span data-stu-id="50a7e-510">Yes</span></span>  <br/> |<span data-ttu-id="50a7e-511">Да (с выделением корней)</span><span class="sxs-lookup"><span data-stu-id="50a7e-511">The picture shows a cat, a dog, a fox, and a wolf.</span></span>  <br/> |
|<span data-ttu-id="50a7e-512">Dogs, foxes, and wolves are canines, but cats are felines.</span><span class="sxs-lookup"><span data-stu-id="50a7e-512">Yes (with stemming)</span></span>  <br/> |<span data-ttu-id="50a7e-513">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-513">Dogs, foxes, and wolves are canines, but cats are felines.</span></span>  <br/> |
|<span data-ttu-id="50a7e-514">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-514">No</span></span>  <br/> |<span data-ttu-id="50a7e-515">Следующее выражение соответствует всем строкам из предыдущей таблицы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-515">The picture shows a cat with a dog, a fox, and a wolf.</span></span>  <br/> |
   
<span data-ttu-id="50a7e-516">Примечания</span><span class="sxs-lookup"><span data-stu-id="50a7e-516">The following expression matches all the strings in the previous table.</span></span>
  
    
    
 `near(cat, dog, fox, wolf, N=5)`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-517">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-517">Remarks</span></span>

 <span data-ttu-id="50a7e-518">**Рекомендации касательно расстояния между терминами NEAR и ONEAR**</span><span class="sxs-lookup"><span data-stu-id="50a7e-518">**NEAR/ONEAR term distance considerations**</span></span>
  
    
    
 <span data-ttu-id="50a7e-p160">_NEAR_ или **ONEAR** работают в тексте с разметкой. Это значит, что специальные символы, например запятая (" **,** "), десятичная точка (" _._ "), двоеточие (" **:** ") или точка с запятой (" **;** "), будут рассматриваться как пробел. Термин "расстояние" относится к маркерам в индексированном тексте.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p160">_N_ indicates the maximum number of words that are allowed to appear between the query terms within the matching segment of the item. If **NEAR** or **ONEAR** includes more than two operands, the maximum number of words allowed between the query terms ( _N_) is counted within the segment of the item matching all the **NEAR** or **ONEAR** terms.</span></span>
  
    
    
 <span data-ttu-id="50a7e-521">Операторы **NEAR** и **ONEAR** работают с текстом, преобразованным в маркеры.</span><span class="sxs-lookup"><span data-stu-id="50a7e-521">**NEAR** or **ONEAR** operates on tokenized text.</span></span> <span data-ttu-id="50a7e-522">Это означает, что специальные знаки, такие как запятая ("**,**"), точка ("**.**"),</span><span class="sxs-lookup"><span data-stu-id="50a7e-522">This means that special characters such as comma (" **,** "), period (" **.**</span></span> <span data-ttu-id="50a7e-523">двоеточие ("**:**") или точка с запятой ("**;**"), будут рассматриваться как пробелы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-523">"), colon (" **:** "), or semicolon (" **;** ") will be treated as white space.</span></span> <span data-ttu-id="50a7e-524">Термин "расстояние" относится к маркерам в индексированном тексте.</span><span class="sxs-lookup"><span data-stu-id="50a7e-524">The term "distance" relates to tokens within the indexed text.</span></span>
  
    
    
<span data-ttu-id="50a7e-525">Если оператор **ONEAR** или **NEAR** используется с равными операндами, он будет работать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="50a7e-525">If you use **ONEAR** or **NEAR** with equal operands, the operator will work as follows:</span></span>
  
    
    
 `near(a, a, n=x)`
  
    
    
<span data-ttu-id="50a7e-526">Этот запрос всегда будет возвращать значение **true**, если в контексте встречается по крайней мере один экземпляр символа "`a`".</span><span class="sxs-lookup"><span data-stu-id="50a7e-526">This query will always return **true** if at least one instance of '' `a`'' appears within the context.</span></span> <span data-ttu-id="50a7e-527">Это также означает, что оператор **NEAR** невозможно использовать в качестве оператора **COUNT**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-527">This also means that **NEAR** cannot be used as a **COUNT** operator.</span></span> <span data-ttu-id="50a7e-528">Дополнительные сведения о подсчете вхождений терминов см. в описании оператора [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator).</span><span class="sxs-lookup"><span data-stu-id="50a7e-528">For more information about counting term occurrences, see the [COUNT](fast-query-language-fql-syntax-reference.md#fql_count_operator) operator.</span></span>
  
    
    
 <span data-ttu-id="50a7e-529">Оператор **NEAR**, применяемый к фразам, также сопоставляет перекрывающиеся фразы в тексте.</span><span class="sxs-lookup"><span data-stu-id="50a7e-529">**NEAR** applied to phrases will also match overlapping phrases in the text.</span></span>
  
    
    
<span data-ttu-id="50a7e-530">Если маркер в соответствующем сегменте совпадает с несколькими операндами выражения **NEAR** или **ONEAR**, то запрос будет сопоставлен, даже если количество несовпадающих маркеров в соответствующем сегменте превышает значение _N_ в выражении с оператором **NEAR** или **ONEAR**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-530">If a token in the matching segment matches more than one operand to the **NEAR** or **ONEAR** expression, the query may match even if the number of nonmatching tokens within the matching segment exceeds the value of '_N_' in the **NEAR** or **ONEAR** operator expression. For example, an overlap can be overlapping phrases. If the number of token overlap matches is 'O', the query will match if not more than 'N+O' non-matching tokens appear within the matching segment of the item.</span></span> <span data-ttu-id="50a7e-531">Допустим, в тексте имеются перекрывающиеся фразы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-531">For example, an overlap can be overlapping phrases.</span></span> <span data-ttu-id="50a7e-532">Если количество совпадений перекрывающихся маркеров составляет `O`, то запрос сопоставляется, если в соответствующем сегменте элемента имеется не более `N+O` несовпадающих маркеров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-532">If the number of token overlap matches is ' `O`', the query will match if not more than ' `N+O`' non-matching tokens appear within the matching segment of the item.</span></span> 
  
    
    
<span data-ttu-id="50a7e-533">**NEAR или ONEAR с оператором NOT**</span><span class="sxs-lookup"><span data-stu-id="50a7e-533">**NEAR or ONEAR with NOT**</span></span>
  
    
    
<span data-ttu-id="50a7e-p164">Оператор **NOT** невозможно использовать в операторах **NEAR** и **ONEAR**. Ниже представлен неправильный синтаксис FQL.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p164">The **NOT** operator cannot be used inside the **NEAR** or **ONEAR** operator. The following is incorrect FQL syntax:</span></span>
  
    
    
 `near(audi,not(bmw),n=2)`
  
    
    

### <a name="not"></a><span data-ttu-id="50a7e-536">NOT</span><span class="sxs-lookup"><span data-stu-id="50a7e-536">NOT</span></span>
<span data-ttu-id="50a7e-537"><a name="fql_not_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-537"></span></span>

<span data-ttu-id="50a7e-p165">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p165">Returns only items that don't match the operand. The operand may be any valid FQL expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-540">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-540">Syntax</span></span>

 `not(operand)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-541">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-541">Parameters</span></span>

<span data-ttu-id="50a7e-542">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-542">Not applicable.</span></span>
  
    
    

### <a name="onear"></a><span data-ttu-id="50a7e-543">ONEAR</span><span class="sxs-lookup"><span data-stu-id="50a7e-543">ONEAR</span></span>
<span data-ttu-id="50a7e-544"><a name="fql_onear_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-544"></span></span>

<span data-ttu-id="50a7e-p166">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p166">The ordered variant of **NEAR**, and requires an ordered match of the terms. The **ONEAR** operator can be used to restrict the result set to items that have _N_ terms within a certain distance of one another.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-547">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-547">Syntax</span></span>

 `onear(arg, arg [, arg]* [, N=<numeric value>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-548">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-548">Parameters</span></span>



|<span data-ttu-id="50a7e-549">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-549">**Parameter**</span></span>|<span data-ttu-id="50a7e-550">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-550">**Value**</span></span>|<span data-ttu-id="50a7e-551">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-551">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-552">_N_</span><span class="sxs-lookup"><span data-stu-id="50a7e-552">_N_</span></span> <br/> | <span data-ttu-id="50a7e-553">_\<числовое_значение\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-553">_\<<numeric_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-554">Задает максимальное количество слов между терминами (явное расстояние).</span><span class="sxs-lookup"><span data-stu-id="50a7e-554">Specifies the maximum number of words that are allowed to appear between the terms (explicit proximity).</span></span>  <br/> <span data-ttu-id="50a7e-555">Если выражение **ONEAR** содержит более двух операндов, то максимальное число слов между терминами (_N_) рассчитывается в пределах целого выражения.</span><span class="sxs-lookup"><span data-stu-id="50a7e-555">If **ONEAR** includes more than two operands, the maximum number of words allowed between the terms (_N_) is counted within the whole expression.</span></span>  <br/> <span data-ttu-id="50a7e-556">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-556">Default: **4**</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="50a7e-557">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-557">Examples</span></span>

 <span data-ttu-id="50a7e-p167">В следующей таблице приведены примеры соответствия и несоответствия строковых значений и состояний управляемого свойства для предыдущего выражения.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p167">**Example 1.** The following expression matches all the occurrences of the words "cat", "dog", "fox", and "wolf" that appears in order, if no more than four indexed tokens separate them.</span></span>
  
    
    
 `onear(cat, dog, fox, wolf)`
  
    
    
<span data-ttu-id="50a7e-560">В приведенной ниже таблице представлены примеры строковых значений управляемых свойств и указано, соответствуют ли они предыдущему выражению.</span><span class="sxs-lookup"><span data-stu-id="50a7e-560">The following table contains examples of managed property string values, and states whether they match the previous expression.</span></span>
  
    
    


|<span data-ttu-id="50a7e-561">**Текст**</span><span class="sxs-lookup"><span data-stu-id="50a7e-561">**Match?**</span></span>|<span data-ttu-id="50a7e-562">Да</span><span class="sxs-lookup"><span data-stu-id="50a7e-562">**Text**</span></span>|
|:-----|:-----|
|<span data-ttu-id="50a7e-563">Да</span><span class="sxs-lookup"><span data-stu-id="50a7e-563">Yes</span></span>  <br/> |<span data-ttu-id="50a7e-564">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-564">The picture shows a cat, a dog, a fox, and a wolf.</span></span>  <br/> |
|<span data-ttu-id="50a7e-565">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-565">No</span></span>  <br/> |<span data-ttu-id="50a7e-566">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-566">Dogs, foxes, and wolves are canines, but cats are felines.</span></span>  <br/> |
|<span data-ttu-id="50a7e-567">Нет</span><span class="sxs-lookup"><span data-stu-id="50a7e-567">No</span></span>  <br/> |<span data-ttu-id="50a7e-568">На этом рисунке показаны кошка с собакой, лиса и волк.</span><span class="sxs-lookup"><span data-stu-id="50a7e-568">The picture shows a cat with a dog, a fox, and a wolf.</span></span>  <br/> |
   
 <span data-ttu-id="50a7e-p168">**Пример 3.** Следующее выражение соответствует тексту из первой и третей строк предыдущей таблицы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p168">**Example 2.** The following expression matches (with stemming) the text in the second row of the previous table.</span></span>
  
    
    
 `onear(dog, fox, wolf, cat, N=5)`
  
    
    
 <span data-ttu-id="50a7e-p169">Примечания</span><span class="sxs-lookup"><span data-stu-id="50a7e-p169">**Example 3.** The following expression matches the text in the first and third rows of the preceding table.</span></span>
  
    
    
 `onear(cat, dog, fox, wolf, N=5)`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-573">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-573">Remarks</span></span>

<span data-ttu-id="50a7e-574">OR</span><span class="sxs-lookup"><span data-stu-id="50a7e-574">See also  [NEAR](fast-query-language-fql-syntax-reference.md#fql_near_operator).</span></span>
  
    
    

### <a name="or"></a><span data-ttu-id="50a7e-575">OR</span><span class="sxs-lookup"><span data-stu-id="50a7e-575">OR</span></span>
<span data-ttu-id="50a7e-576"><a name="fql_or_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-576"></span></span>

<span data-ttu-id="50a7e-p170">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p170">Returns only items that match at least one of the **OR** operands. Items that match will get a higher dynamic rank (relevance score in the result set) if more of the **OR** operands match. The operands may be a single term or any valid FQL sub-expression.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-580">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-580">Syntax</span></span>

 `or(operand, operand [,operand]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-581">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-581">Parameters</span></span>

<span data-ttu-id="50a7e-582">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-582">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-583">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-583">Examples</span></span>

<span data-ttu-id="50a7e-p171">PHRASE</span><span class="sxs-lookup"><span data-stu-id="50a7e-p171">The following expression matches all the items for which the default full-text index contains either "cat" or "dog". If an item's default full-text index contains both "cat" and "dog", it will match and have a higher dynamic rank than it would if it contained only one of the tokens.</span></span>
  
    
    
 `or(cat, dog)`
  
    
    

### <a name="phrase"></a><span data-ttu-id="50a7e-586">PHRASE</span><span class="sxs-lookup"><span data-stu-id="50a7e-586">PHRASE</span></span>
<span data-ttu-id="50a7e-587"><a name="fql_phrase_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-587"></span></span>

<span data-ttu-id="50a7e-588">Ищет точную строку маркеров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-588">Searches for an exact string of tokens.</span></span> 
  
    
    
<span data-ttu-id="50a7e-p172">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p172">The **PHRASE** operands can be single terms. Wildcards are accepted.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-591">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-591">Syntax</span></span>

 `phrase(term [, term]*)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-592">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-592">Parameters</span></span>

<span data-ttu-id="50a7e-593">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-593">Not applicable.</span></span>
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-594">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-594">Remarks</span></span>

<span data-ttu-id="50a7e-595">RANGE</span><span class="sxs-lookup"><span data-stu-id="50a7e-595">See also  [STRING](fast-query-language-fql-syntax-reference.md#fql_string_operator).</span></span>
  
    
    

### <a name="range"></a><span data-ttu-id="50a7e-596">RANGE</span><span class="sxs-lookup"><span data-stu-id="50a7e-596">RANGE</span></span>
<span data-ttu-id="50a7e-597"><a name="fql_range_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-597"></span></span>

<span data-ttu-id="50a7e-p173">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p173">Use the **RANGE** operator for numeric and date/time managed properties. The operator enables range matching expressions.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-600">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-600">Syntax</span></span>

 `range(start, stop [,from="GE"|"GT"] [,to="LE"|"LT"])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-601">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-601">Parameters</span></span>



|<span data-ttu-id="50a7e-602">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-602">**Parameter**</span></span>|<span data-ttu-id="50a7e-603">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-603">**Value**</span></span>|<span data-ttu-id="50a7e-604">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-604">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-605">_start_</span><span class="sxs-lookup"><span data-stu-id="50a7e-605">_start_</span></span> <br/> | <span data-ttu-id="50a7e-606">_\<числовое_значение\>\\</span><span class="sxs-lookup"><span data-stu-id="50a7e-606"> <numeric_value></span></span>|<span data-ttu-id="50a7e-607">\<значение_даты_и_времени\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-607"><date/time_value>_</span></span> <br/> |<span data-ttu-id="50a7e-608">Начальное значение диапазона.</span><span class="sxs-lookup"><span data-stu-id="50a7e-608">Start value for the range.</span></span>  <br/> <span data-ttu-id="50a7e-609">**stop**</span><span class="sxs-lookup"><span data-stu-id="50a7e-609">To specify that the range has no lower bound, use the reserved word **min**.</span></span> <br/> |
| <span data-ttu-id="50a7e-610">_stop_</span><span class="sxs-lookup"><span data-stu-id="50a7e-610">_stop_</span></span> <br/> | <span data-ttu-id="50a7e-611">_\<числовое_значение\>\\</span><span class="sxs-lookup"><span data-stu-id="50a7e-611"> <numeric_value></span></span>|<span data-ttu-id="50a7e-612">\<значение_даты_и_времени\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-612"><date/time_value>_</span></span> <br/> |<span data-ttu-id="50a7e-613">Конечное значение диапазона.</span><span class="sxs-lookup"><span data-stu-id="50a7e-613">End value for the range.</span></span>  <br/> <span data-ttu-id="50a7e-614">**from**</span><span class="sxs-lookup"><span data-stu-id="50a7e-614">To specify that the range has no upper bound, use the reserved word **max**.</span></span> <br/> |
| <span data-ttu-id="50a7e-615">_from_</span><span class="sxs-lookup"><span data-stu-id="50a7e-615">_from_</span></span> <br/> |<span data-ttu-id="50a7e-616">**GE\\</span><span class="sxs-lookup"><span data-stu-id="50a7e-616">**GE</span></span>|<span data-ttu-id="50a7e-617">GT**</span><span class="sxs-lookup"><span data-stu-id="50a7e-617">GT**</span></span> <br/> | <span data-ttu-id="50a7e-618">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="50a7e-618">Optional parameter that indicates the open or close start interval.</span></span> <br/>  <span data-ttu-id="50a7e-619">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="50a7e-619">Valid values:</span></span> <br/><ul><li> <span data-ttu-id="50a7e-620">**GT**  больше начального значения (> начало интервала).</span><span class="sxs-lookup"><span data-stu-id="50a7e-620">**GE** Greater than or equal to the start value (>= start of interval).</span></span> </li><li> <span data-ttu-id="50a7e-621">Значение по умолчанию: **GE**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-621">**GT** Greater than the start value (> start of interval).</span></span> </li></ul>  <span data-ttu-id="50a7e-622">**to**</span><span class="sxs-lookup"><span data-stu-id="50a7e-622">Default: **GE**</span></span>  |
| <span data-ttu-id="50a7e-623">_to_</span><span class="sxs-lookup"><span data-stu-id="50a7e-623">_to_</span></span> <br/> |<span data-ttu-id="50a7e-624">**LE\\</span><span class="sxs-lookup"><span data-stu-id="50a7e-624">**LE</span></span>|<span data-ttu-id="50a7e-625">LT**</span><span class="sxs-lookup"><span data-stu-id="50a7e-625">LT**</span></span> <br/> | <span data-ttu-id="50a7e-626">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="50a7e-626">Optional parameter that indicates the open or close end interval.</span></span> <br/>  <span data-ttu-id="50a7e-627">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="50a7e-627">Valid values:</span></span> <br/><ul><li> <span data-ttu-id="50a7e-628">**LT**  меньше конечного значения (< конец интервала).</span><span class="sxs-lookup"><span data-stu-id="50a7e-628">**LE** Less than or equal to the end value (<= end of interval).</span></span> </li><li> <span data-ttu-id="50a7e-629">Значение по умолчанию: **LT**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-629">**LT** Less than the end value (< end of interval).</span></span> </li></ul>  <span data-ttu-id="50a7e-630">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-630">Default: **LT**</span></span> |
   

#### <a name="examples"></a><span data-ttu-id="50a7e-631">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-631">Examples</span></span>

<span data-ttu-id="50a7e-632">STARTS-WITH</span><span class="sxs-lookup"><span data-stu-id="50a7e-632">The following expression matches a description property starting with the phrase "olympic games" appearing in items with a size of at least 10 000 bytes.</span></span>
  
    
    
 `and(size:range(10000, max), description:starts-with("olympic games"))`
  
    
    

### <a name="starts-with"></a><span data-ttu-id="50a7e-633">STARTS-WITH</span><span class="sxs-lookup"><span data-stu-id="50a7e-633">STARTS-WITH</span></span>
<span data-ttu-id="50a7e-634"><a name="fql_startswith_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-634"></span></span>

<span data-ttu-id="50a7e-635">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-635">Specifies a word or phrase that must appear at the start of a managed property.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-636">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-636">Syntax</span></span>

 `starts-with(<term or phrase>)`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-637">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-637">Parameters</span></span>

<span data-ttu-id="50a7e-638">Неприменимо.</span><span class="sxs-lookup"><span data-stu-id="50a7e-638">Not applicable.</span></span>
  
    
    

#### <a name="examples"></a><span data-ttu-id="50a7e-639">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-639">Examples</span></span>

<span data-ttu-id="50a7e-p174">Примечания</span><span class="sxs-lookup"><span data-stu-id="50a7e-p174">The following expression will match items with the values "Adam Jones sr" and "Adam Jones" in the **author** managed property. It will not match items with the value "Mr Adam Jones".</span></span>
  
    
    
 `author:starts-with("adam jones")`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-642">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-642">Remarks</span></span>

<span data-ttu-id="50a7e-643">STRING</span><span class="sxs-lookup"><span data-stu-id="50a7e-643">For additional remarks on boundary matching, see  [ENDS-WITH](fast-query-language-fql-syntax-reference.md#fql_endswith_operator).</span></span>
  
    
    

### <a name="string"></a><span data-ttu-id="50a7e-644">STRING</span><span class="sxs-lookup"><span data-stu-id="50a7e-644">STRING</span></span>
<span data-ttu-id="50a7e-645"><a name="fql_string_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-645"></span></span>

<span data-ttu-id="50a7e-646">Операнд  сопоставляемая текстовая строка (один или более терминов). Строка может сопровождаться любым количеством параметров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-646">Defines a Boolean matching condition to a text string.</span></span>
  
    
    
<span data-ttu-id="50a7e-p175">Операнд — сопоставляемая текстовая строка (один или более терминов). Строка может сопровождаться любым количеством параметров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p175">The operand is a text string (one or more terms) that is to be matched. The string is followed by zero or more parameters.</span></span> 
  
    
    
<span data-ttu-id="50a7e-p176">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-p176">The **STRING** operator can also be used as a type conversion. The query `string("24.5")`, for example, will treat the numeric value "24.5" as a text string.</span></span>
  
    
    

#### <a name="syntax"></a><span data-ttu-id="50a7e-651">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-651">Syntax</span></span>

 `string("<text string>"`
  
    
    
 ` [, mode=<mode>]`
  
    
    
 ` [, n=<near>]`
  
    
    
 ` [, weight=<n>]`
  
    
    
 ` [, linguistics=<on|off>]`
  
    
    
 ` [, wildcard=<on|off>])`
  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-652">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-652">Parameters</span></span>



|<span data-ttu-id="50a7e-653">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-653">**Parameter**</span></span>|<span data-ttu-id="50a7e-654">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-654">**Value**</span></span>|<span data-ttu-id="50a7e-655">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-655">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-656">_mode_</span><span class="sxs-lookup"><span data-stu-id="50a7e-656">_mode_</span></span> <br/> | <span data-ttu-id="50a7e-657">_\<режим\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-657">_\<Mode\>_</span></span> <br/> | <span data-ttu-id="50a7e-658">Параметр _mode_ указывает, как оценивать значение \<строки текста\>.</span><span class="sxs-lookup"><span data-stu-id="50a7e-658">The _mode_ parameter specifies how to evaluate the \<text string\> value.</span></span> <span data-ttu-id="50a7e-659">Ниже представлен список допустимых значений.</span><span class="sxs-lookup"><span data-stu-id="50a7e-659">The following list shows valid values.</span></span> <br/> <span data-ttu-id="50a7e-660">**"PHRASE"** - `phrase(term [,term]*)`</span><span class="sxs-lookup"><span data-stu-id="50a7e-660">**"PHRASE"** - `phrase(term [,term]*)`</span></span> <br/> <table><tr><th><span data-ttu-id="50a7e-661">**Mode**</span><span class="sxs-lookup"><span data-stu-id="50a7e-661">**Mode**</span></span></th><th><span data-ttu-id="50a7e-662">**Эквивалентное выражение с оператором**</span><span class="sxs-lookup"><span data-stu-id="50a7e-662">**Equivalent operator expression**</span></span></th></tr><tr><td><span data-ttu-id="50a7e-663">**"PHRASE"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-663">**"PHRASE"**</span></span>  </td><td> `phrase(term [,term]*)` </td></tr><tr><td><span data-ttu-id="50a7e-664">**"AND"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-664">**"AND"**</span></span> </td><td> `and(term, term [,term]*)` </td></tr><tr><td><span data-ttu-id="50a7e-665">**"OR"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-665">**"OR"**</span></span> </td><td> `or(term, term [,term]*)` </td></tr><tr><td><span data-ttu-id="50a7e-666">**"ANY"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-666">**"ANY"**</span></span> </td><td> `any(term, term [,term]*)` </td></tr><tr><td><span data-ttu-id="50a7e-667">**"NEAR"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-667">**"NEAR"**</span></span> </td><td> `near(term, term [,term]*, N)` </td></tr><tr><td><span data-ttu-id="50a7e-668">**"ONEAR"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-668">**"ONEAR"**</span></span> </td><td> `onear(term, term [,term]*, N)` </td></tr></table><br/><span data-ttu-id="50a7e-669">Значение по умолчанию: **"PHRASE"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-669">Default: **"PHRASE"**</span></span> |
| _n_ <br/> | <span data-ttu-id="50a7e-670">_\<числовое_значение\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-670"> <numeric_value></span></span> <br/> |<span data-ttu-id="50a7e-671">Этот параметр задает максимальное расстояние между терминами для выражения _mode_= **"NEAR"** или _mode_= **"ONEAR"**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-671">|This parameter indicates the maximum term distance for  _mode_= **"NEAR"** or _mode_= **"ONEAR"**.</span></span> <br/> <span data-ttu-id="50a7e-672">Приведенные ниже выражения эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="50a7e-672">The following expressions are equivalent:</span></span>  <br/>  `string("hello world", mode="NEAR", n=5)` <br/>  `near(hello, world, n=5)` <br/> <span data-ttu-id="50a7e-673">Значение по умолчанию: **4**</span><span class="sxs-lookup"><span data-stu-id="50a7e-673">Default: **4**</span></span> <br/> |
| <span data-ttu-id="50a7e-674">_weight_</span><span class="sxs-lookup"><span data-stu-id="50a7e-674">_weight_</span></span> <br/> | <span data-ttu-id="50a7e-675">_\<числовое_значение\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-675"> <numeric_value></span></span> <br/> |<span data-ttu-id="50a7e-676">Этот параметр содержит положительное числовое значение, указывающее вес для динамического ранжирования.</span><span class="sxs-lookup"><span data-stu-id="50a7e-676">This parameter is a positive numeric value indicating term weight for dynamic ranking.</span></span>  <br/> <span data-ttu-id="50a7e-p178">При ранжировании термин с более низким значением веса имеет меньшую ценность, термин с более высоким значением  более высокую. Если вес термина равен нулю, то данный термин не влияет на динамическое рейтинг.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p178">A lower value indicates that a term should contribute less to the ranking. A higher value indicates that a term should contribute more to the ranking. A value of zero for the weight parameter specifies that a term should not affect dynamic rank.  </span></span><br/> <span data-ttu-id="50a7e-680">Параметр _weight_ применяется ко всем терминам в выражении **STRING**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-680">The  _weight_ parameter applies to all the terms in the **STRING** expression.</span></span> <br/> <span data-ttu-id="50a7e-681">**СОВЕТ.** Параметр weight влияет только на запросы полнотекстового индекса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-681">The weight parameter will affect only full-text index queries.</span></span>           <span data-ttu-id="50a7e-682">Значение по умолчанию: **100**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-682">Default: **100**.</span></span> <br/> |
| <span data-ttu-id="50a7e-683">_linguistics_</span><span class="sxs-lookup"><span data-stu-id="50a7e-683">_linguistics_</span></span> <br/> |<span data-ttu-id="50a7e-684">**on\\</span><span class="sxs-lookup"><span data-stu-id="50a7e-684">on</span></span>|<span data-ttu-id="50a7e-685">off**</span><span class="sxs-lookup"><span data-stu-id="50a7e-685">off**</span></span> <br/> |<span data-ttu-id="50a7e-686">Отключает или включает все лингвистические функции для строк (лемматизацию, синонимы, проверку правописания), если они включены для запроса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-686">Disables/enables all linguistics features for the string (lemmatization, synonyms, spelling checking) if they are enabled for the query.</span></span>  <br/> <span data-ttu-id="50a7e-687">Вы можете использовать данный параметр, чтобы отключить лингвистическую обработку для данного термина или строки, но чтобы при этом термин или строка все равно приняли участие в рейтинге.</span><span class="sxs-lookup"><span data-stu-id="50a7e-687">You can use this parameter to switch off linguistic processing for a given term or string while you still want the term or string to contribute to ranking.</span></span>  <br/> <span data-ttu-id="50a7e-688">Значение по умолчанию: **"ON"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-688">Default: **"ON"**</span></span> <br/> |
| <span data-ttu-id="50a7e-689">_wildcard_</span><span class="sxs-lookup"><span data-stu-id="50a7e-689">_Wildcard_</span></span> <br/> |<span data-ttu-id="50a7e-690">**on\\</span><span class="sxs-lookup"><span data-stu-id="50a7e-690">on</span></span>|<span data-ttu-id="50a7e-691">off**</span><span class="sxs-lookup"><span data-stu-id="50a7e-691">off**</span></span> <br/> | <span data-ttu-id="50a7e-692">Этот параметр управляет расширением терминов в _\<текстовой строке\>_ с помощью подстановочных знаков.</span><span class="sxs-lookup"><span data-stu-id="50a7e-692">This parameter controls wildcard expansion of terms inside the _\<text string\>_.</span></span> <span data-ttu-id="50a7e-693">Этот параметр переопределяет все настройки подстановочных знаков в параметрах запроса и позволяет включать или отключать расширенные подстановочные знаки в определенных частях запроса.</span><span class="sxs-lookup"><span data-stu-id="50a7e-693">This parameter controls wildcard expansion of terms inside the <text string>. This setting overrides any wildcard settings in query parameters, and allows extended wildcard characters to be enabled or disabled on specific parts of the query.</span></span>  <br/>  <span data-ttu-id="50a7e-694">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="50a7e-694">The following are valid values:</span></span> <br/><ul><li> <span data-ttu-id="50a7e-695">**"ON"**. Указывает на то, что символ "\*" оценивается как подстановочный знак.</span><span class="sxs-lookup"><span data-stu-id="50a7e-695">**"ON"**  Specifies that the character "*\*" is evaluated as wildcard. A "*" character matches zero or more characters.</span></span> <span data-ttu-id="50a7e-696">Символ "\*" соответствует любому количеству символов (начиная с нуля).</span><span class="sxs-lookup"><span data-stu-id="50a7e-696">A "\*" character matches zero or more characters.</span></span>  </li><li> <span data-ttu-id="50a7e-697">**"OFF"**. Указывает на то, что символы "\*" не оцениваются как подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="50a7e-697">**"OFF"**  Specifies that the characters "*\*" is not evaluated as wildcard.</span></span>  </li></ul>  <span data-ttu-id="50a7e-698">Значение по умолчанию: **"ON"**</span><span class="sxs-lookup"><span data-stu-id="50a7e-698">Default: **"ON"**</span></span> <br/> |
   

> <span data-ttu-id="50a7e-699">**Примечание.** В SharePoint параметры _minexpansion_, _maxexpansion_ и _annotation_class_ для оператора **STRING** устарели.</span><span class="sxs-lookup"><span data-stu-id="50a7e-699">**NOTE** In SharePoint 2013 the  _minexpansion_,  _maxexpansion_ and _annotation_class_ parameters for the **STRING** operator are obsolete.</span></span>
  
    
    


#### <a name="examples"></a><span data-ttu-id="50a7e-700">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-700">Examples</span></span>

 <span data-ttu-id="50a7e-p182">**Пример 1.** Так как режимом строки по умолчанию является " **PHRASE** ", все представленные ниже выражения возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p182">**Example 1.** Because the default string mode is " **PHRASE** ", each of the following expressions returns the same results.</span></span>
  
    
    
 `"what light through yonder window breaks"string("what light through yonder window breaks")string("what light through yonder window breaks", mode="phrase")phrase(what, light, through, yonder, window, breaks)`
  
    
    
 <span data-ttu-id="50a7e-p183">**Пример 2.** Следующее строковое выражение маркера и операторное выражение **AND** возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p183">**Example 2.** The following string token expression and the **AND** operator expression return the same results.</span></span>
  
    
    
 `string("cat dog fox", mode="and")and(cat, dog, fox)`
  
    
    
 <span data-ttu-id="50a7e-p184">**Пример 3.** Следующее строковое выражение маркера и операторное выражение **OR** возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p184">**Example 3.** The following string token expression and **OR** operator expression return the same results.</span></span>
  
    
    
 `string("coyote saguaro", mode="or")or(coyote, saguaro)`
  
    
    
 <span data-ttu-id="50a7e-p185">**Пример 4.** Следующее строковое выражение маркера и операторное выражение **ANY** возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p185">**Example 4.** The following string token expression and **ANY** operator expression return the same results.</span></span>
  
    
    
 `string("coyote saguaro", mode="any")any(coyote, saguaro)`
  
    
    
 <span data-ttu-id="50a7e-p186">**Пример 5.** Следующее строковое выражение маркера и операторное выражение **NEAR** возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p186">**Example 5.** The following string token expression and **NEAR** operator expression return the same results.</span></span>
  
    
    
 `string("coyote saguaro", mode="near")near(coyote, saguaro)`
  
    
    
 <span data-ttu-id="50a7e-p187">**Пример 6.** Следующее строковое выражение маркера и операторное выражение **NEAR** возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p187">**Example 6.** The following string token expression and **NEAR** operator expression return the same results.</span></span>
  
    
    
 `string("cat dog fox wolf", mode="near", N=4)near(cat, dog, fox, wolf, N=4)`
  
    
    
 <span data-ttu-id="50a7e-p188">**Пример 7.** Следующее строковое выражение маркера и операторное выражение **ONEAR** возвращают одинаковые результаты.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p188">**Example 7.** The following string token expression and **ONEAR** operator expression return the same results.</span></span>
  
    
    
 `string("cat dog fox wolf", mode="onear")onear(cat, dog, fox, wolf)`
  
    
    
 <span data-ttu-id="50a7e-p189">**Пример 8.** Следующее строковое выражение маркера соответствует слову "nobler" с отключенной функцией лингвистики, поэтому другие формы данного слова (например, "ennobling") не сопоставляются с использованием выделения корней.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p189">**Example 8.** The following string token expression matches the word "nobler" with linguistic features disabled, so other forms of the word (such as "ennobling") are not matched by using stemming.</span></span>
  
    
    
 `string("nobler", linguistics="off")`
  
    
    
 <span data-ttu-id="50a7e-p190">**Пример 9.** Следующее выражение соответствует элементам, которые содержат слово "cat" или "dog ", однако динамический рейтинг для элементов с вхождениями слова "dog" увеличивается больше, чем для элементов с вхождениями слова "cat".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p190">**Example 9.** The following expression matches items that contain either "cat" or "dog ", but the expression increases the dynamic rank of items that contain "dog" more than items that contain "cat".</span></span>
  
    
    
 `or(string("cat", weight="200"), string("dog", weight="500"))`
  
    
    

#### <a name="remarks"></a><span data-ttu-id="50a7e-719">Заметки</span><span class="sxs-lookup"><span data-stu-id="50a7e-719">Remarks</span></span>

 <span data-ttu-id="50a7e-720">**Релевантный вес для динамического ранжирования**</span><span class="sxs-lookup"><span data-stu-id="50a7e-720">**Relevance weight for dynamic ranking**</span></span>
  
    
    
<span data-ttu-id="50a7e-p191">Параметр **weight** предназначен в основном для запросов **OR**. Кроме того, он может несколько повлиять на запросы **AND**. Алгоритм динамического рейтинга подразумевает, что различные термины по-разному вовлекаются в процесс ранжирования в зависимости от того, в каком месте термина появилось совпадение.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p191">The main effect of the **weight** parameter is for **OR** queries. It can also have some effect on **AND** queries. The dynamic rank algorithm can imply that different terms give different rank contribution depending on where in the item the term match occurs.</span></span>
  
    
    
<span data-ttu-id="50a7e-p192">Различия в степени вовлечения в рейтинг основываются на частоте терминов и обратной частоте элементов. Например:</span><span class="sxs-lookup"><span data-stu-id="50a7e-p192">The difference in rank contribution can also be based on term frequency and inverse item frequency. The following is an example:</span></span>
  
    
    

- <span data-ttu-id="50a7e-726">Запрос:  `and(string("a"), string("b", weight=200))`.</span><span class="sxs-lookup"><span data-stu-id="50a7e-726">Query:  `and(string("a"), string("b", weight=200))`</span></span>
    
  
- <span data-ttu-id="50a7e-727">Схема индекса: вес управляемого свойства **title** выше, чем вес управляемого свойства **body**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-727">Index schema: The **title** managed property has more weight than the **body** managed property.</span></span>
    
  
- <span data-ttu-id="50a7e-728">Элемент индекса 1 содержит термин "a" в свойстве "title" и термин "b" в свойстве "body".</span><span class="sxs-lookup"><span data-stu-id="50a7e-728">Index item 1 includes term 'a' in the title and term 'b' in the body.</span></span> 
    
  
- <span data-ttu-id="50a7e-729">Элемент индекса 2 содержит термин "a" в свойстве "body" и термин "b" в свойстве "title".</span><span class="sxs-lookup"><span data-stu-id="50a7e-729">Index item 2 includes term 'a' in the body and term 'b' in the title.</span></span> 
    
  
<span data-ttu-id="50a7e-730">В данном примере элемент 2 получит более высокое значение общего рейтинга, так как элементы с более высоким вовлечением в динамический рейтинг получают еще большее повышение ранга.</span><span class="sxs-lookup"><span data-stu-id="50a7e-730">In this example, item 2 will get the highest total rank, as the items with higher dynamic rank contribution will get even more boost.</span></span>
  
    
    

> <span data-ttu-id="50a7e-731">**Совет.** Бонус для относительных терминов (положительный или отрицательный) применяется к динамическому компоненту ранжирования для общего ранга.</span><span class="sxs-lookup"><span data-stu-id="50a7e-731">**Tip:** The relative term boost (positive or negative) is applied to the dynamic rank component of the total rank.</span></span> <span data-ttu-id="50a7e-732">Однако вес терминов не влияет на бонус за расстояние между словами.</span><span class="sxs-lookup"><span data-stu-id="50a7e-732">However, proximity boost (distance between words) rank calculations are not affected by the term weighting.</span></span> <span data-ttu-id="50a7e-733">Относительный вес не всегда подразумевает, что общий ранг элемента меняется в соответствии с указанным процентом.</span><span class="sxs-lookup"><span data-stu-id="50a7e-733">The relative weighting does not always imply that the total rank for the item is modified according to the percentage given.</span></span> <span data-ttu-id="50a7e-734">Приведенный ниже запрос ищет термины "peter", "paul" и "mary". При этом термин "peter" оказывает на ранг вдвое большее влияние, чем два других термина.</span><span class="sxs-lookup"><span data-stu-id="50a7e-734">The following query will search for the terms "peter", "paul", or "mary", where "peter" will have twice as much rank contribution as the two other terms.</span></span> >  `or(peter, string("paul mary", mode="OR", weight=50))`
  
    
    

 <span data-ttu-id="50a7e-735">**Обработка строк со специальными знаками**</span><span class="sxs-lookup"><span data-stu-id="50a7e-735">**Handling strings with special characters**</span></span>
  
    
    
<span data-ttu-id="50a7e-p194">Специальные символы, такие как запятая (","), точка с запятой (";"), двоеточие (":"), десятичная точка ("."), минус ("-"), подчеркивание ("_") или косая черта ("/"), считаются пустым местом внутри строкового выражения, заключенного в двойные кавычки. Это относится к процессу выделения маркеров. Они также подразумевают неявное фразирование маркеров, разделенных этими символами.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p194">Special characters such as comma (","), semicolon (";"), colon (":"), period ("."), minus ("-"), underline ("_"), or forward slash ("/") are treated as white space inside a string expression enclosed in double quotation marks. This is related to the tokenization process. These characters also imply an implicit phrasing of the tokens separated by these characters.</span></span> 
  
    
    
<span data-ttu-id="50a7e-739">Следующие выражения запросов эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="50a7e-739">The following query expressions are equivalent.</span></span>
  
    
    
 `title:string("animals birds", mode="phrase")title:"animals/birds"title:string("animals/birds", mode="and")title:string("animals/birds", mode="or")`
  
    
    
<span data-ttu-id="50a7e-740">Следующие выражения запросов эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="50a7e-740">The following query expressions are equivalent.</span></span>
  
    
    
 `title:or(string("animals birds", mode="phrase"), string("animals insects", mode="phrase"))title:string("animals/birds animals/insects", mode="or")`
  
    
    
<span data-ttu-id="50a7e-741">Следующие выражения запросов эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="50a7e-741">The following query expressions are equivalent.</span></span>
  
    
    
 `body:string("help contoso com", mode="phrase")body:string("help@contoso.com")`
  
    
    
 <span data-ttu-id="50a7e-742">**Соответствие фразе, разделенной на маркеры**</span><span class="sxs-lookup"><span data-stu-id="50a7e-742">**Tokenized phrase matching**</span></span>
  
    
    
<span data-ttu-id="50a7e-743">Вы можете искать точную строку маркеров, используя оператор **STRING** с параметром _mode_="phrase" или оператор **PHRASE**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-743">You can search for an exact string of tokens by using the **STRING** operator with _mode_="phrase" or the **PHRASE** operator.</span></span>
  
    
    
<span data-ttu-id="50a7e-744">Все подобные операции с фразами подразумевают сопоставление фраз в виде маркеров.</span><span class="sxs-lookup"><span data-stu-id="50a7e-744">All such phrase operations imply a tokenized phrase match.</span></span> <span data-ttu-id="50a7e-745">Это означает, что специальные знаки, такие как запятая ("**,**"), точка с запятой ("**;**"), двоеточие ("**:**"), подчеркивание ("\_"), знак "минус" ("**-**") и косая черта ("**/**"), рассматриваются как пробелы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-745">All such phrase operations imply a tokenized phrase match. This means that special characters such as comma (" **,** "), semicolon (" **;** "), colon (" **:** "), underscore (" \_ "), minus (" **-** "), or forward slash (" **/** ") are treated as white space. This is related to the tokenization process.</span></span> <span data-ttu-id="50a7e-746">Это связано с процессом преобразования в маркеры.</span><span class="sxs-lookup"><span data-stu-id="50a7e-746">This is related to the tokenization process.</span></span>
  
    
    

### <a name="xrank"></a><span data-ttu-id="50a7e-747">XRANK</span><span class="sxs-lookup"><span data-stu-id="50a7e-747">XRANK</span></span>
<span data-ttu-id="50a7e-748"><a name="fql_xrank_operator"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-748"></span></span>

<span data-ttu-id="50a7e-p196">Повышение динамического ранга элементов основано на вхождениях определенных терминов в пределах  _match expression_ без изменения элементов, соответствующих запросу. Выражение **XRANK** состоит из одного компонента, который должен удовлетворять выражению ( _match expression_) и одного или нескольких компонентов, которые участвуют только в динамическом рейтинге ( _rank expression_). Чтобы выражение XRANK было допустимым, для него должен быть указан хотя бы **один** из параметров, за исключением _n_.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p196">Boosts the dynamic rank of items based on certain term occurrences within the  _match expression_, without changing which items match the query. An **XRANK** expression consists of one component that must be matched, the _match expression_, and one or more components that contribute only to dynamic ranking, the  _rank expression_. At least **one** of the parameters, excluding _n_, must be specified for an XRANK expression to be valid.</span></span>
  
    
    
 <span data-ttu-id="50a7e-p197">_Match expressions_ может быть любым допустимым FQL-выражением, включая вложенные выражения **XRANK**. _Rank expressions_ может быть любым допустимым FQL-выражением без выражения **XRANK**. Если ваши FQL-запросы имеют несколько операторов **XRANK**, итоговое выражение динамического рейтинга рассчитывается как сумма повышений по всем операторам **XRANK**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p197">_Match expressions_ may be any valid FQL expression, including nested **XRANK** expressions. _Rank expressions_ may be any valid FQL expression without **XRANK** expressions. If your FQL queries have multiple **XRANK** operators, the final dynamic rank value is calculated as a sum of boosts across all **XRANK** operators.</span></span>
  
    
    

> <span data-ttu-id="50a7e-755">**Примечание.** В SharePoint Server 2010 у оператора **XRANK** есть два параметра: _boost_ и _boostall_. Для него используется следующий синтаксис: `xrank(operand, rank-operand [, rank-operand]* [,boost=n] [,boostall=yes])`.</span><span class="sxs-lookup"><span data-stu-id="50a7e-755">**Note:** In SharePoint Server 2010, the **XRANK** operator had two parameters: _boost_ and _boostall_, as well as the following syntax:  `xrank(operand, rank-operand [, rank-operand]* [,boost=n] [,boostall=yes])`.</span></span> <span data-ttu-id="50a7e-756">Этот синтаксис и соответствующие параметры являются нерекомендуемыми в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50a7e-756">This syntax along with its parameters is deprecated in SharePoint.</span></span> <span data-ttu-id="50a7e-757">Рекомендуем использовать новый синтаксис и его параметры.</span><span class="sxs-lookup"><span data-stu-id="50a7e-757">We recommend the use of the new syntax and parameters instead.</span></span> 
  
    
    


#### <a name="syntax"></a><span data-ttu-id="50a7e-758">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="50a7e-758">Syntax</span></span>

 `xrank(<match expression> [, <rank-expression>]*, rank-parameter[, rank-parameter]*)`
  
    
    

#### <a name="formula"></a><span data-ttu-id="50a7e-759">Формула</span><span class="sxs-lookup"><span data-stu-id="50a7e-759">Formula</span></span>


  
    
    
![Формула для оператора XRANK](../images/XRANKFormula.gif)
  
    
    

  
    
    

  
    
    

#### <a name="parameters"></a><span data-ttu-id="50a7e-761">Параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-761">Parameters</span></span>



|<span data-ttu-id="50a7e-762">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-762">**Parameter**</span></span>|<span data-ttu-id="50a7e-763">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-763">**Value**</span></span>|<span data-ttu-id="50a7e-764">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-764">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-765">_N_</span><span class="sxs-lookup"><span data-stu-id="50a7e-765">_N_</span></span> <br/> | <span data-ttu-id="50a7e-766">_\<целое_число\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-766">_\<<integer_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-767">Задает количество результатов, для которых вычисляются статистические данные.</span><span class="sxs-lookup"><span data-stu-id="50a7e-767">Specifies the number of results to compute statistics from.</span></span>  <br/> <span data-ttu-id="50a7e-768">Этот параметр не влияет на количество результатов, на которые влияет динамический рейтинг. С его помощью из вычисления статистики просто исключаются ненужные элементы.</span><span class="sxs-lookup"><span data-stu-id="50a7e-768">This parameter does not affect the number of results that the dynamic rank contributes to; it is just a means to exclude irrelevant items from the statistics calculations.</span></span>  <br/> <span data-ttu-id="50a7e-p199"> Значение по умолчанию: **0**. Нулевое значение означает *все документы*  . </span><span class="sxs-lookup"><span data-stu-id="50a7e-p199">Default: **0**. A zero value carries the sematic of *all documents*  . </span></span><br/> |
| <span data-ttu-id="50a7e-771">_Nb_</span><span class="sxs-lookup"><span data-stu-id="50a7e-771">_Nb_</span></span> <br/> | <span data-ttu-id="50a7e-772">_\<значение_с_плавающей_запятой\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-772">_\<<float_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-p200">Параметр  _nb_ относится к нормированному увеличению. Этот параметр определяет коэффициент, на который умножается произведение дисперсии и среднего арифметического значений рейтингов в наборе результатов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p200">The  _nb_ parameter refers to normalized boost. This parameter specifies the factor that is multiplied with the product of the variance and average score of the rank values of the results set. </span></span><br/>  <span data-ttu-id="50a7e-775">Параметр  _f_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="50a7e-775">_f_ in the XRANK formula.</span></span> <br/> |
   
<span data-ttu-id="50a7e-p201">Как правило нормированное увеличение ( _nb_)  это единственный изменяемый параметр. Этого параметра достаточно, чтобы понижать или повышать рейтинг отдельного элемента, не учитывая стандартное отклонение.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p201">Typically normalized boost,  _nb_, is the only parameter that is modified. This parameter provides the necessary control to promote or demote a particular item, without taking standard deviation into account.</span></span> 
  
    
    

#### <a name="advanced-parameters"></a><span data-ttu-id="50a7e-778">Расширенные параметры</span><span class="sxs-lookup"><span data-stu-id="50a7e-778">Advanced parameters</span></span>

<span data-ttu-id="50a7e-p202">Доступны также дополнительные параметры, указанные ниже. Но обычно они не используются.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p202">The following advanced parameters are also available. However, typically they aren't used.</span></span>
  
    
    


|<span data-ttu-id="50a7e-781">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="50a7e-781">**Parameter**</span></span>|<span data-ttu-id="50a7e-782">**Значение**</span><span class="sxs-lookup"><span data-stu-id="50a7e-782">**Value**</span></span>|<span data-ttu-id="50a7e-783">**Описание**</span><span class="sxs-lookup"><span data-stu-id="50a7e-783">**Description**</span></span>|
|:-----|:-----|:-----|
| <span data-ttu-id="50a7e-784">_cb_</span><span class="sxs-lookup"><span data-stu-id="50a7e-784">_cb_</span></span> <br/> | <span data-ttu-id="50a7e-785">_\<значение_с_плавающей_запятой\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-785">_\<<float_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-786">Параметр _cb_ указывает постоянный бонус.</span><span class="sxs-lookup"><span data-stu-id="50a7e-786">The  _cb_ parameter refers to constant boost.</span></span> <br/> <span data-ttu-id="50a7e-787">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-787">Default: **0**.</span></span> <br/>  <span data-ttu-id="50a7e-788">Параметр  _a_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="50a7e-788">_a_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="50a7e-789">_stdb_</span><span class="sxs-lookup"><span data-stu-id="50a7e-789">_stdb_</span></span> <br/> | <span data-ttu-id="50a7e-790">_\<значение_с_плавающей_запятой\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-790">_\<<float_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-791">Параметр _stdb_ указывает бонус со стандартным отклонением.</span><span class="sxs-lookup"><span data-stu-id="50a7e-791">The  _stdb_ parameter refers to standard deviation boost.</span></span> <br/> <span data-ttu-id="50a7e-792">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-792">Default: **0**.</span></span> <br/>  <span data-ttu-id="50a7e-793">Параметр  _e_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="50a7e-793">_e_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="50a7e-794">_avgb_</span><span class="sxs-lookup"><span data-stu-id="50a7e-794">_avgb_</span></span> <br/> | <span data-ttu-id="50a7e-795">_\<значение_с_плавающей_запятой\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-795">_\<<float_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-p203">Параметр _avgb_ указывает средний бонус. Этот показатель умножается на среднее значение ранга в результирующем наборе. </span><span class="sxs-lookup"><span data-stu-id="50a7e-p203">The  _avgb_ parameter refers to average boost. This factor is multiplied with the average rank value of the results set. </span></span><br/> <span data-ttu-id="50a7e-798">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-798">Default: **0**.</span></span> <br/>  <span data-ttu-id="50a7e-799">Параметр  _d_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="50a7e-799">_d_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="50a7e-800">_rb_</span><span class="sxs-lookup"><span data-stu-id="50a7e-800">_rb_</span></span> <br/> | <span data-ttu-id="50a7e-801">_\<значение_с_плавающей_запятой\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-801">_\<<float_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-p204">Параметр _rb_ указывает бонус в диапазоне. Этот показатель умножается на диапазон значений ранга в результирующем наборе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p204">The  _rb_ parameter refers to range boost. This factor is multiplied with the range of rank values in the results set. </span></span><br/> <span data-ttu-id="50a7e-804">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-804">Default: **0**.</span></span> <br/>  <span data-ttu-id="50a7e-805">Параметр  _b_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="50a7e-805">_b_ in the XRANK formula.</span></span> <br/> |
| <span data-ttu-id="50a7e-806">_pb_</span><span class="sxs-lookup"><span data-stu-id="50a7e-806">_pb_</span></span> <br/> | <span data-ttu-id="50a7e-807">_\<значение_с_плавающей_запятой\>_</span><span class="sxs-lookup"><span data-stu-id="50a7e-807">_\<<float_value>\>_</span></span> <br/> |<span data-ttu-id="50a7e-p205">Параметр  _pb_ задает увеличение в процентах. Этот коэффициент умножается на собственный рейтинг элемента в сравнении с минимальным значением в наборе.</span><span class="sxs-lookup"><span data-stu-id="50a7e-p205">The  _pb_ parameter refers to percentage boost. This factor is multiplied with the item's own rank compared to the minimum value in the corpus. </span></span><br/> <span data-ttu-id="50a7e-810">Значение по умолчанию: **0**.</span><span class="sxs-lookup"><span data-stu-id="50a7e-810">Default: **0**.</span></span> <br/>  <span data-ttu-id="50a7e-811">Параметр  _c_ в формуле XRANK.</span><span class="sxs-lookup"><span data-stu-id="50a7e-811">_c_ in the XRANK formula.</span></span> <br/> |
   

#### <a name="examples"></a><span data-ttu-id="50a7e-812">Примеры</span><span class="sxs-lookup"><span data-stu-id="50a7e-812">Examples</span></span>

 <span data-ttu-id="50a7e-p206">**Пример 1.** Следующее выражение сопоставляет элементы, для которых полнотекстовый индекс по умолчанию содержит "cat" или "dog". Выражение увеличивает на постоянную величину 100 динамический рейтинг элементов, содержащих также термин "thoroughbred".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p206">**Example 1.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 for items that also contain "thoroughbred".</span></span>
  
    
    
 `xrank(or(cat, dog), thoroughbred, cb=100)`
  
    
    
 <span data-ttu-id="50a7e-p207">**Пример 2.** Следующее выражение сопоставляет элементы, для которых полнотекстовый индекс по умолчанию содержит термины "cat" или "dog". Выражение увеличивает динамический рейтинг элементов на нормированную величину 1,5 для элементов, содержащих также термин "thoroughbred".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p207">**Example 2.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a normalized boost of 1.5 for items that also contain "thoroughbred".</span></span>
  
    
    
 `xrank(or(cat, dog), thoroughbred, nb=1.5)`
  
    
    
 <span data-ttu-id="50a7e-p208">**Пример 3.** Следующее выражение сопоставляет элементы, для которых полнотекстовый индекс по умолчанию содержит термины "cat" или "dog". Выражение увеличивает динамический рейтинг элементов на постоянную величину 100 и нормированную величину 1,5 для элементов, содержащих также термин "thoroughbred".</span><span class="sxs-lookup"><span data-stu-id="50a7e-p208">**Example 3.** The following expression matches items for which the default full-text index contains either "cat" or "dog". The expression increases dynamic rank of those items with a constant boost of 100 and a normalized boost of 1.5, for items that also contain "thoroughbred".</span></span>
  
    
    
 `xrank(or(cat, dog), thoroughbred, cb=100, nb=1.5)`
  
    
    
 <span data-ttu-id="50a7e-p209">**Пример 4.** Следующее выражение сопоставляет все элементы, содержащие термин "animals", и увеличивает динамический рейтинг следующим образом:</span><span class="sxs-lookup"><span data-stu-id="50a7e-p209">**Example 4.** The following expression matches all items containing the term "animals", and boosts dynamic rank as follows:</span></span>
  
    
    

- <span data-ttu-id="50a7e-824">динамический рейтинг элементов, содержащих термин "dogs", увеличивается на 100 баллов;</span><span class="sxs-lookup"><span data-stu-id="50a7e-824">Dynamic rank of items that contain the term "dogs" is boosted by 100 points.</span></span>
    
  
- <span data-ttu-id="50a7e-825">динамический рейтинг элементов, содержащих термин "cats", увеличивается на 200 баллов;</span><span class="sxs-lookup"><span data-stu-id="50a7e-825">Dynamic rank of items that contain the term "cats" is boosted by 200 points.</span></span>
    
  
- <span data-ttu-id="50a7e-826">динамический рейтинг элементов, содержащих и термин "dogs", и термин "cats", увеличивается на 300 баллов.</span><span class="sxs-lookup"><span data-stu-id="50a7e-826">Dynamic rank of items that contain both the terms "dogs" and "cats" is boosted by 300 points.</span></span>
    
  
 `xrank(xrank(animals, dogs, cb=100), cats, cb=200)`
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="50a7e-827">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="50a7e-827">Additional resources</span></span>
<span data-ttu-id="50a7e-828"><a name="SP15FQL_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="50a7e-828"></span></span>


-  [<span data-ttu-id="50a7e-829">Построение запросов поиска в SharePoint</span><span class="sxs-lookup"><span data-stu-id="50a7e-829">Building search queries in SharePoint</span></span>](building-search-queries-in-sharepoint.md)
    
  
