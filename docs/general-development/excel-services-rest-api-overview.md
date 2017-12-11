---
title: "Интерфейс API REST служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 5872f311-e180-4578-ac80-2519c1081951
ms.openlocfilehash: 624336e751c28d7bacce26f88e6d9f7dc570c93c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="excel-services-rest-api-overview"></a><span data-ttu-id="56bed-102">Интерфейс API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="56bed-102">Excel Services REST API Overview</span></span>

<span data-ttu-id="56bed-p101">API-интерфейс REST в Службы Excel появился в версии Microsoft SharePoint Server 2010. С помощью API-интерфейса REST можно обращаться к частям или элементам книги напрямую через URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="56bed-p101">The REST API in Excel Services is new in Microsoft SharePoint Server 2010. By using the REST API, you can access workbook parts or elements directly through a URL.</span></span>
  
> [!NOTE]
> <span data-ttu-id="56bed-105">API REST служб Excel применяется к SharePoint и SharePoint 2016 локально.</span><span class="sxs-lookup"><span data-stu-id="56bed-105">The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="56bed-106">Для учетных записей для Office 365 Education, Business и Enterprise,, используйте интерфейсы API REST Excel, входят в состав [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="56bed-106">For For Office 365 Education, Business, and Enterprise accounts,, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/en-us/docs/api-reference/v1.0/resources/excel) endpoint.</span></span>
  
    
    


<span data-ttu-id="56bed-107">Службы REST основаны на двух требованиях:</span><span class="sxs-lookup"><span data-stu-id="56bed-107">REST services are based on two requirements:</span></span>
  
    
    


- <span data-ttu-id="56bed-108">Схема адресации, используемая для обнаружения сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="56bed-108">An addressing scheme used to locate networked resources</span></span>
    
  
- <span data-ttu-id="56bed-109">Методология для возврата представлений этих ресурсов</span><span class="sxs-lookup"><span data-stu-id="56bed-109">A methodology for returning representations of these resources</span></span>
    
  
<span data-ttu-id="56bed-p103">Службы REST предназначены для работы с ресурсами. REST разделяет данные на ресурсы, каждому ресурсу присваивается URL-адрес, и стандартные операции реализуются для ресурсов, что обеспечивает выполнение таких операций, как создание, извлечение, обновление и удаление.</span><span class="sxs-lookup"><span data-stu-id="56bed-p103">REST services are resource-centric. With REST, data is divided into resources, each resource is given a URL, and standard operations are implemented on the resources, which enable operations like creation, retrieval, update, and deletion.</span></span> 

> [!NOTE]
> <span data-ttu-id="56bed-112">[!Примечание] Дополнительные сведения о разнице между службами REST и настраиваемыми веб-службами см. в статье, посвященной  [настраиваемой службе или службе RESTful](http://msdn.microsoft.com/en-us/magazine/dd882522.aspx).</span><span class="sxs-lookup"><span data-stu-id="56bed-112">For more information about the difference between REST services and custom Web services, see  [Custom Service or RESTful Service](http://msdn.microsoft.com/en-us/magazine/dd882522.aspx).</span></span> 
  
    
    

<span data-ttu-id="56bed-p104">API-интерфейс REST для Службы Excel позволяет выполнять операции с книгами Excel посредством использования операций, указанных в стандарте HTTP. Это обеспечивает гибкий, безопасный и сравнительно простой механизм для доступа к контенту Службы Excel и манипулирования им.Механизмы обнаружения, встроенные в API-интерфейс REST Службы Excel, также позволяют разработчикам и пользователям просматривать контент книги вручную или программно, путем предоставления каналов  [Atom](http://tools.ietf.org/html/rfc4287), содержащих сведения об элементах в определенной книге. Некоторые примеры ресурсов, доступ к которым возможен через API-интерфейс REST: диаграммы, таблицы и сводные таблицы.Использование канала Atom, предоставляемого API-интерфейсом REST, упрощает получение нужных данных. Канал содержит просматриваемые элементы, позволяющие любому фрагменту кода обнаруживать, какие элементы существуют в книге.Сведения о доступе к службе REST и образцы URI для службы REST в Службы Excel см. в статьях  [Структура базового URI и путь](basic-uri-structure-and-path.md) и [Пример URI для интерфейса API REST служб Excel](sample-uri-for-excel-services-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="56bed-p104">A REST API for Excel Services enables operations against Excel workbooks by using operations specified in the HTTP standard. This allows for a flexible, secure, and simpler mechanism to access and manipulate Excel Services content.The discovery mechanisms built into the Excel Services REST API also enable developers and users to explore the content of the workbook manually or programmatically by supplying an  [Atom](http://tools.ietf.org/html/rfc4287) feed that contains information about the elements that reside in a specific workbook. Some examples of the resources that you can access through the REST API are charts, PivotTables, and tables.Using the Atom feed provided by the REST API is an easier way of getting to the data that you care about. The feed contains traversable elements that enable any piece of code to discover what elements exist in a workbook. For information about accessing the REST service and obtaining sample URIs for the REST service in Excel Services, see  [Basic URI Structure and Path](basic-uri-structure-and-path.md) and [Sample URI For Excel Services REST API](sample-uri-for-excel-services-rest-api.md).</span></span>
