---
title: "Интерфейс API REST служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5872f311-e180-4578-ac80-2519c1081951
ms.openlocfilehash: d6b5abba5dea4a47bd52b7615594afbdb5e59794
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-rest-api-overview"></a>Интерфейс API REST служб Excel

API-интерфейс REST в Службы Excel появился в версии Microsoft SharePoint Server 2010. С помощью API-интерфейса REST можно обращаться к частям или элементам книги напрямую через URL-адрес.
  
    
    


> **Примечание:** API REST служб Excel применяется к SharePoint и SharePoint 2016 локально. Для учетных записей для Office 365 Education, Business и Enterprise,, используйте интерфейсы API REST Excel, входят в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel) конечной точки.
  
    
    


Службы REST основаны на двух требованиях:
  
    
    


- Схема адресации, используемая для обнаружения сетевых ресурсов
    
  
- Методология для возврата представлений этих ресурсов
    
  
Службы REST предназначены для работы с ресурсами. REST разделяет данные на ресурсы, каждому ресурсу присваивается URL-адрес, и стандартные операции реализуются для ресурсов, что обеспечивает выполнение таких операций, как создание, извлечение, обновление и удаление. 
> **Примечание:** Дополнительные сведения о различиях между службы REST и настраиваемые веб-службы можно [настраиваемой службы или службы RESTful](http://msdn.microsoft.com/en-us/magazine/dd882522.aspx). 
  
    
    

API-интерфейс REST для Службы Excel позволяет выполнять операции с книгами Excel посредством использования операций, указанных в стандарте HTTP. Это обеспечивает гибкий, безопасный и сравнительно простой механизм для доступа к контенту Службы Excel и манипулирования им.Механизмы обнаружения, встроенные в API-интерфейс REST Службы Excel, также позволяют разработчикам и пользователям просматривать контент книги вручную или программно, путем предоставления каналов  [Atom](http://tools.ietf.org/html/rfc4287), содержащих сведения об элементах в определенной книге. Некоторые примеры ресурсов, доступ к которым возможен через API-интерфейс REST: диаграммы, таблицы и сводные таблицы.Использование канала Atom, предоставляемого API-интерфейсом REST, упрощает получение нужных данных. Канал содержит просматриваемые элементы, позволяющие любому фрагменту кода обнаруживать, какие элементы существуют в книге.Сведения о доступе к службе REST и образцы URI для службы REST в Службы Excel см. в статьях  [Структура базового URI и путь](basic-uri-structure-and-path.md) и [Пример URI для интерфейса API REST служб Excel](sample-uri-for-excel-services-rest-api.md).