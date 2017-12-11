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
# <a name="trigger-expressions-syntax-in-sharepoint"></a>Синтаксис выражений триггер в SharePoint
Сведения о выражениях триггер, которые можно использовать для создания условия запуска для настройки вызов веб-службы в SharePoint. 
## <a name="elements-used-in-the-syntax-of-trigger-expressions"></a>Элементы, используемые в синтаксисе триггер выражений
<a name="SP15triggerex_elements"> </a>

Элементы, которые могут использоваться в выражении триггер являются:
  
    
    

- Операторы
    
  
- Управляемый доступ к свойству значение
    
  
- Литералы
    
  
- Функции
    
  
- Константы
    
> [!NOTE] 
> [!Примечание] Строка " **Null**" зарезервирован для значение **Null**. 
  
    
    


## <a name="operators-in-trigger-expression-syntax"></a>Операторы в синтаксис выражений триггер
<a name="SP15triggerex_operators"> </a>

В таблице 1 описаны операторы, поддерживаемые язык выражений триггер, содержащий приоритет, по убыванию. Операторы в одной категории имеют одинаковый приоритет. Несколько операторов имеет две версии их синтаксиса.
  
    
    

**В таблице 1. Поддерживаемые операторы для синтаксис выражений триггер**


|**Категория**|**Выражение**|**Описание**|
|:-----|:-----|:-----|
|Унарный  <br/> |-  <br/> !, НЕ  <br/> |Арифметические отрицания  <br/> Логического отрицания  <br/> |
|Умножения  <br/> |*  <br/> /  <br/> %, mod  <br/> |Умножение  <br/> Подразделение  <br/> Остаток  <br/> |
|ADDITIVE  <br/> |+  <br/> -  <br/> &amp;  <br/> |Добавление  <br/> Вычитание  <br/> Объединение строк  <br/> |
|Реляционные  <br/> |=, ==  <br/> ! = <>  <br/> <  <br/> >  <br/> <=  <br/> >=  <br/> |Равенство  <br/> Неравенство  <br/> Меньше  <br/> Больше  <br/> Меньше или равно  <br/> Больше или равно  <br/> |
|Логическое И  <br/> |&amp; &amp;, AND  <br/> |Логическое И  <br/> |
|Логическое ИЛИ  <br/> | OR  <br/> |Логическое ИЛИ  <br/> |
   

## <a name="managed-property-access-in-trigger-expressions"></a>Управляемые свойства access в выражениях триггер
<a name="SP15triggerex_managed"> </a>

Управляемые свойства для обхода элементов ссылается их имя; Имя не входит в кавычки ("") и задается с учетом регистра.
  
    
    

## <a name="literals-in-trigger-expressions"></a>Литералы в выражениях триггер
<a name="SP15triggerex_literals"> </a>

Следующие типы данных могут быть выражены как литералы: **String**, **Int32**, **Double**и **Boolean**.
  
    
    

## <a name="functions-in-trigger-expressions"></a>Функции в выражениях триггер
<a name="SP15triggerex_functions"> </a>

Широкий набор функций, включающих от математические функции, такие как  `Floor` функций для использования с определенными типами данных, таких как `Lists`. Можно использовать эти функции по отдельности или можно вкладывать их.
  
    
    

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
    
  

## <a name="constants-in-trigger-expressions"></a>Константы в выражениях триггер
<a name="SP15triggerex_constants"> </a>

Существует два набора константы, которые могут использоваться с помощью определенных функций: **DatePartConstant** и **RegexOptionConstant**. В таблице 2 приведены два примера эти константы и где их можно использовать.
  
    
    

**В таблице 2. Константы выражение триггер и использования в SharePoint**


|**Группа констант**|**Примеры**|**Использование**|
|:-----|:-----|:-----|
|**DatePartConstant** <br/> |**Day**, **Month**, **Year**, **Hour**, **Minute**, **Second**.  <br/> |С помощью функции **GetDatePart** <br/> |
|**RegexOptionConstant** <br/> |**IgnoreCase** <br/> |С помощью функции **IsMatch**, **Match**, **ReplaceRegex**и **IndexOfRegex**. <br/> |
   

## <a name="see-also"></a>См. также
<a name="SP15triggerex_addresources"> </a>


-  [Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  
-  [Как: используйте вызов повышения качества контента веб-службы для SharePoint Server](how-to-use-the-content-enrichment-web-service-callout-for-sharepoint-server.md)
    
  

  
    
    

