---
title: "Нестандартная обработка контента с использованием выноски веб-службы \"Обогащение контента\""
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: bdda92c8-9c8d-416e-9a6b-4a9373686fa0
ms.openlocfilehash: 621505bfb2ee7c406d55cad2c76061bdd4cb7114
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="custom-content-processing-with-the-content-enrichment-web-service-callout"></a>Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"
Узнайте о вызов повышения качества контента веб-службы в SharePoint, который позволяет разработчикам создавать внешние веб-службы для изменения управляемых свойств для обхода элементов во время обработки контента.
Поиск в SharePoint позволяет пользователям изменение управляемого свойства для обхода элементов перед их индексации путем вызова в работе веб-службе внешнего повышения качества контента. Возможность изменения управляемых свойств для элементов во время обработки контента функция полезна, если для выполнения задач, таких как очистка данных, извлечение сущностей, классификации и тегов.
  
    
    


**На рисунке 1. Повышения качества контента в процессе обработки контента**

  
    
    

  
    
    
![Обогащение контента при обработке контента](../images/SP15_Content_Enrichment.gif)
  
    
    
На рисунке 1 показана часть процесса, который выполняется в компонент обработки контента. Веб-служба повышения качества контента  это служба на основе SOAP, можно создать для получения выноски от клиента веб-службы в компонент обработки контента. Основываясь на рисунке 1, клиент веб-службы , относится к оператор обогащение контента в компонент; обработки контентавеб-служба относится к реализации веб-служба SOAP.Веб-служба получает настраиваемые полезных данных из компонента обработки контента. Затем результирующий ответ от веб-службы объединяется для обхода элементов перед добавлением в индекс поиска.Клиент веб-службы для работы с управляемыми свойствами, которые можно настроить как входные свойства или свойства выходных данных. Входные свойства, передаются в веб-службе. Вывод свойств возвращаются веб-службой. Некоторые управляемые свойства являются скрытыми или доступны только для чтения и не может отправленных веб-службы или полученных от веб-службы. Сведения о том, как проверить, какие управляемые свойства доступны только для чтения в разделе  [Вывод списка всех только для чтения управляемых свойств для повышения качества контента веб-службы](#SP15contentprocess_read-only_managed_properties) .
    
> **Важные:** Действие выноски повышения качества контента можно настроить только с конечной одного веб-службы. Любой тип отказоустойчивость или возможности для поддержки нескольких реализаций маршрутизации должны обрабатываться разработчиком, реализация веб-службы. Кроме того разработчик может иметь различные веб-службами, размещенных на разных конечные точки; Тем не менее в любой момент времени, можно использовать только один из этих конечных точек в конфигурации. 
  
    
    


## <a name="content-enrichment-web-service-contract"></a>Контракт службы web повышения качества контента
<a name="SP15webservcallout_enrich"> </a>

Клиент веб-службы  это клиент SOAP (версия 1.1) RPC с предварительно заданных поведение. Контракт службы web имеет следующие характеристики:
  
    
    

- Компонент обработки контента отправляет вызов SOAP RPC настраиваемая конечной точки по протоколу HTTP.
    
  
- Полезные данные содержит массив объектов свойства.
    
  
- Веб-службы выполняет некоторые настраиваемой логики на массив объектов, свойств и возвращает массив объектов измененного или нового свойства.
    
  
- Веб-службы необходимо отправки ответа клиенту веб-службы в течение заданного периода ожидания.
    
  
- Нет определенных механизмов проверки подлинности и шифрования, поддерживаются как часть контракта. Тем не менее, можно применять собственные безопасности механизм транспорта.
    
  

## <a name="configuring-the-content-enrichment-web-service-client"></a>Настройка клиента повышения качества контента веб-службы
<a name="content_enrichment_configuration"> </a>

Чтобы настроить клиент веб-службы, используйте следующие командлеты Windows PowerShell:
  
    
    

-  [Get-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219783%28office.15%29.aspx)
    
  
-  [Set-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219659%28office.15%29.aspx)
    
  
-  [Remove-SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219742%28office.15%29.aspx)
    
  
-  [Новый SPEnterpriseSearchContentEnrichmentConfiguration](http://technet.microsoft.com/en-us/library/jj219502%28office.15%29.aspx)
    
  
В таблице 1 перечислены свойства, которые можно настроить через Windows PowerShell командлеты, указанным выше.
  
    
    

**В таблице 1. Свойства, которые настраиваются для клиента с помощью командлетов Windows PowerShell**


|**Свойство конфигурации**|**Описание**|**Значение по умолчанию**|
|:-----|:-----|:-----|
|**Endpoint** <br/> |URL-адрес внешнего веб-службы.  <br/> |empty  <br/> |
|**InputProperties** <br/> |Управляемые свойства, которые получает внешние веб-службы.  <br/> |empty  <br/> |
|**OutputProperties** <br/> |Управляемые свойства, возвращает внешних веб-службы.  <br/> |empty  <br/> |
|**Timeout** <br/> |Количество времени до раз службы web извлечения в миллисекундах.  <br/> В зависимости от **FailureMode** элемент не удается обработать или предупреждения, записывается в журнал ULS. <br/> |5000 миллисекунд; Допустимый диапазон [100, 30000].  <br/> |
|**SendRawData** <br/> |Включает или отключает отправке необработанных данных в веб-службу.  <br/> |false  <br/> |
|**MaxRawDataSize** <br/> |Максимальный размер необработанных данных, отправляемых в веб-службу в килобайтах (КБ). Если двоичные данные элемента превышает это ограничение, элемент не отправляются. Это не запрещает **InputProperties** отправку и **OutputProperties** получению. <br/> |5120 КБ.  <br/> |
|**FailureMode** <br/> |Управляет поведением клиента веб-службы, при возникновении ошибки. Если **FailureMode** **ERROR**, всех проблем, возникающих при обработке повышения качества контента отправлять неудавшегося обратного вызова для этого конкретного элемента. <br/> Если **FailureMode** **WARNING**, индексируются элемент без каких-либо изменений веб-службой и предупреждения, записывается в журнал ULS.  <br/> |Ошибка  <br/> |
|**DebugMode** <br/> |Режим, если параметр имеет значение **true** позволяет клиента повышения качества контента для отправки все управляемые свойства клиенту без ожидания все свойства в ответ. Все настроенные **Trigger** свойств, **InputProperties** и **OutputProperties** свойства игнорируются. <br/> |false  <br/> |
|**Trigger** <br/> |Предикат **Boolean**, который выполняется на всех элементов для обхода. Если предикат принимает значение **true**, эту запись отправляется в веб-службу. В противном случае элемент передается через в индекс поиска. <br/> |empty  <br/> |
   

### <a name="how-to-list-all-read-only-managed-properties-for-the-content-enrichment-web-service"></a>Вывод списка всех только для чтения управляемых свойств для повышения качества контента веб-службы
<a name="SP15contentprocess_read-only_managed_properties"> </a>

Некоторые управляемые свойства доступны только для чтения и не может быть выходных данных из веб-службы. Эти свойства можно отобразить с помощью  [Get-SPEnterpriseSearchServiceApplication](http://technet.microsoft.com/en-us/library/ff608050%28office.15%29.aspx) и [Get-SPEnterpriseSearchMetadataManagedProperty](http://technet.microsoft.com/en-us/library/ff607560%28office.15%29.aspx)Windows PowerShell командлетов, показано в следующем примере:
  
    
    

```

$ssa = Get-SPEnterpriseSearchServiceApplication
Get-SPEnterpriseSearchMetadataManagedProperty -SearchApplication $ssa  | ?{$_.IsReadOnly -or $_.MappingDisallowed -or $_.DeleteDisallowed}

```


## <a name="about-trigger-conditions-for-configuring-the-web-service-callout"></a>Об условиях запуска по настройке вызов веб-службы
<a name="SP15contentprocess_trigger"> </a>

Условие запуска - это выражение, которое используется для настройки вызов веб-службы. Если триггер условие имеет значение **true**, клиент веб-службы выполняет выноски для этой записи. Если триггер условие имеет значение **false**, клиент веб-службы не выполняет выноски и передает для обхода элементов в индекс поиска. Кроме того, если условие не триггер настроен; все элементы, передаются в веб-службы.
  
    
    
Условия запуска используйте язык выражений ссылаться на значения управляемого свойства. Операторы и функции в язык выражений можно использовать для создания простых и сложных триггер условий, можно определить, когда следует выполнить вызов веб-службы. 
  
    
    
В таблице 2 приведены примеры условия запуска.
  
    
    

**В таблице 2. Примеры условие триггер для настройки вызов повышения качества контента веб-службы**


|**Выражение**|**Описание**|**Требования**|
|:-----|:-----|:-----|
|MP1 > 2  <br/> |Возвращает **true**, если значение управляемого свойства с именем MP1 больше 2. <br/> |MP1 должны иметь числовой тип.  <br/> |
|IsNull(MP2)  <br/> |Возвращает **true**, если управляемое свойство с именем MP2 не отображается для элемента для обхода или empty и null. <br/> |MP2 может быть любого типа.  <br/> |
|StartsWith(MP1, "sample") и MP2! = 18  <br/> |Возвращает **true**, если значение в управляемом свойстве MP1 начинается с "Пример" и значение управляемого свойства MP2 не 18. <br/> |MP1 должен иметь тип **string** и MP2 должен быть числовым типом. <br/> |
|IsDay (MP1, 2009 г., 12, 24)  <br/> |Проверяет, содержит ли управляемое свойство MP1 **DateTime** на 24 декабря 2009 г. <br/> |MP1 должен иметь тип **DateTime**.  <br/> |
   
Элементы, которые могут использоваться в выражении триггер и список функций, поддерживаемых в разделе [триггер синтаксис выражений в SharePoint](trigger-expressions-syntax-in-sharepoint.md) .
  
    
    

## <a name="implementing-the-content-enrichment-external-web-service"></a>Реализация повышения качества контента внешние веб-службы
<a name="SP15contentprocess_implement"> </a>

Базовой реализации выполните следующие действия: 
  
    
    

1. Включите **Microsoft.Office.Server.Search.ContentProcessingEnrichment.dll**, расположенный в `C:\\Program Files\\Microsoft Office Servers\\15.0\\Search\\Applications\\External` в проект в качестве ссылки.
    
  
2. Реализация **IContentProcessingEnrichmentService** как веб-службы.
    
  

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Настройка службы поиска в SharePoint](configure-search-in-sharepoint.md)
    
  
-  [Нестандартная обработка контента с использованием выноски веб-службы "Обогащение контента"](custom-content-processing-with-the-content-enrichment-web-service-callout.md)
    
  
