---
title: "Справочник по API-Интерфейс REST BCS для SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 364fb8d7-87d9-4be7-affd-90caba3cd0c0
ms.openlocfilehash: f33adf455a216d1a7dba82832d9bcf7051068cb0
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="bcs-rest-api-reference-for-sharepoint"></a>Справочник по API-Интерфейс REST BCS для SharePoint

  
    
    
![Ссылки и библиотеки класса](../images/mod_icon_badge_reference.png)
  
    
    

  
    
    

  
    
    
Содержит сведения о создании представлений состояния (REST) URL-адреса для доступа и работы с внешними источниками данных с помощью Business Connectivity Services (BCS) в SharePoint.
## <a name="using-restful-apis-to-access-external-data-in-sharepoint"></a>Использование интерфейсов API RESTful для доступа к внешним данным в SharePoint
<a name="bkmk_Overview"> </a>

Интерфейс REST, предоставляемых SharePoint позволяет получить доступ к большинству ресурсов SharePoint через специально созданный URL-адрес. Эта архитектура использует Business Connectivity Services (BCS) для предоставления доступа к внешним данным.
  
    
    
Так же, как и для доступа к элементам списка стандартных можно приступить к внешним данным с построения URL-адресов.
  
    
    

> **Примечание:** Доступ к сущностей через BDC непосредственно не указан. Для работы с внешними данными, необходимо создать внешний список и использовать URL-адреса REST для доступа к элементам списка, содержащихся во внешнем списке. 
  
    
    

Поддерживаемые HTTP-команды для работы с внешними списками, **GET**, **PUT**, **POST**и **DELETE**.
  
    
    
В отличие от обычных списками невозможно создать внешний список, использующий REST. Необходимо выполнить, путем создания модели BDC и внешнего списка с помощью Visual Studio 2012.
  
    
    
Сведения, приведенные в таблице 1 показано, как для создания URL-адреса REST и соответствующие вызовы объектной модели клиента для доступа и работы с данными из внешних источников данных.
  
    
    

**В таблице 1. RESTful форматы URL-адрес для доступа к внешним данным**


|**URL-адрес**|**Описание**|**Метод HTTP**|
|:-----|:-----|:-----|
| `http://[sharepointsite]/_api` <br/> |Базовое все запросы REST. В виртуальном каталоге _api сопоставляется позвонить в client.svc, где используется клиентская объектная модель.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/web/title` <br/> |Получает название текущего веб-сайта.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists` <br/> |Извлечение всех списков на сайте  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')` <br/> |Извлекает метаданные для указанного списка.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')/items` <br/> |Извлечение элементов списка в заданном списке.  <br/> |GET  <br/> |
| `http://[sharepointsite]/_api/lists/getbytitle('listname')?select=Title` <br/> |Извлечение названия определенный список.  <br/> |GET  <br/> |
   

## <a name="constructing-query-strings-for-filtering-data"></a>Создание строки запроса для фильтрации данных
<a name="bkmk_constructquery"> </a>

Чтобы ограничить количество возвращаемых данных или сделать его более относится к пользователю, можно использовать операции фильтрации, найденные в таблице 2.
  
    
    

**В таблице 2. Операторы для фильтрации данных**


|**Оператор**|**Описание**|
|:-----|:-----|
|eq  <br/> |Равняется  <br/> **Примечание:** При использовании **EQ** для фильтрации условия фильтра передаются во внешней системе, где происходит фильтрация на сервере.          |
|Gt  <br/> |(больше)  <br/> **Примечание:** При использовании оператора **GT** выполняется фильтрация только со стороны клиента. > Например: `web/lists/getByTitle('ListName')/Items?$select=Title&amp;$filter=AverageRating gt 3` возвращает все заголовки со средним рейтинг более чем 3.          |
   

> **Примечание:** Для получения столбцов, которые являются частью связь, необходимо явно включить столбец в URL-адрес, с помощью **$select** в строке запроса.
  
    
    


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bkmk_AdditionalResources"> </a>


-  [Business Connectivity Services в SharePoint](business-connectivity-services-in-sharepoint.md)
    
  
-  [Выполнение базовых операций с использованием конечных точек SharePoint REST](http://msdn.microsoft.com/library/e3000415-50a0-426e-b304-b7de18f2f7d9%28Office.15%29.aspx)
    
  
-  [Использование операций запросов OData в запросах REST SharePoint](http://msdn.microsoft.com/library/d4b5c277-ed50-420c-8a9b-860342284b72%28Office.15%29.aspx)
    
  
-  [SharePoint: выполнение основных операций доступа к данным в приложениях с помощью REST](http://code.msdn.microsoft.com/SharePoint-Perform-335d925b)
    
  
-  [Выбор правильного набора API в SharePoint](choose-the-right-api-set-in-sharepoint.md)
    
  
-  [Выполнение базовых операций с использованием кода библиотеки JavaScript в SharePoint](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
