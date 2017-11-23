---
title: "REST API для служб Excel"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 32033fea-873c-4781-900a-6946906066b0
ms.openlocfilehash: 9672a0013f82b2878cda45a8936cade24aa29412
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="excel-services-rest-api"></a><span data-ttu-id="5c45c-102">REST API для служб Excel</span><span class="sxs-lookup"><span data-stu-id="5c45c-102">Excel Services REST API</span></span>

<span data-ttu-id="5c45c-103">Этот раздел содержит информацию об API передачи репрезентативного состояния (REST) в службах Excel и его использовании.</span><span class="sxs-lookup"><span data-stu-id="5c45c-103">This section contains information about the Representational State Transfer (REST) API in Excel Services and explains how to use it.</span></span>
  
    
    


> <span data-ttu-id="5c45c-104">**Примечание.** REST API служб Excel применим к локальным развертываниям SharePoint и SharePoint 2016.</span><span class="sxs-lookup"><span data-stu-id="5c45c-104">**Note:** The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises.</span></span> <span data-ttu-id="5c45c-105">Для учетных записей Office 365 для образования, Office 365 бизнес и Office 365 корпоративный используйте REST API Excel, входящие в состав конечной точки [Microsoft Graph](http://graph.microsoft.io/ru-ru/docs/api-reference/v1.0/resources/excel
> ).</span><span class="sxs-lookup"><span data-stu-id="5c45c-105">Note The Excel Services REST API applies to SharePoint and SharePoint 2016 on-premises. For Office 365 Education, Business, and Enterprise accounts, use the Excel REST APIs that are part of the  [Microsoft Graph](http://graph.microsoft.io/ru-ru/docs/api-reference/v1.0/resources/excel
) endpoint.</span></span>
  
    
    


## <a name="related-sections"></a><span data-ttu-id="5c45c-106">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="5c45c-106">Related sections</span></span>


 [<span data-ttu-id="5c45c-107">Интерфейс API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="5c45c-107">Excel Services REST API Overview</span></span>](excel-services-rest-api-overview.md)
  
    
    
> <span data-ttu-id="5c45c-108">Сведения о REST API в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-108">Learn about the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-109">Структура базового URI и путь</span><span class="sxs-lookup"><span data-stu-id="5c45c-109">Basic URI Structure and Path</span></span>](basic-uri-structure-and-path.md)
  
    
    
> <span data-ttu-id="5c45c-110">Узнайте, как составлять структуру URI и путь для команд службы REST в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-110">Learn how to construct the URI structure and path for the REST service commands in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-111">Обнаружение в API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="5c45c-111">Discovery in Excel Services REST API</span></span>](discovery-in-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="5c45c-112">Сведения о механизмах обнаружения, встроенных в REST API в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-112">Learn about the discovery mechanisms built into the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-113">Ресурсы URI для интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="5c45c-113">Resources URI for Excel Services REST API</span></span>](resources-uri-for-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="5c45c-114">Узнайте, на какие сущности можно ссылаться напрямую с помощью REST API в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-114">Learn the entities that you can link directly to by using the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-115">Получение диапазонов с помощью канала Atom и HTML-фрагмента</span><span class="sxs-lookup"><span data-stu-id="5c45c-115">Getting Ranges Using Atom Feed and HTML Fragment</span></span>](getting-ranges-using-atom-feed-and-html-fragment.md)
  
    
    
> <span data-ttu-id="5c45c-116">Узнайте, как получать доступ к диапазонам  веб-каналам Atom и фрагментам HTML  с помощью REST API в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-116">Learn to access ranges—Atom feeds and HTML fragments—by using the REST API in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-117">Пример URI для интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="5c45c-117">Sample URI For Excel Services REST API</span></span>](sample-uri-for-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="5c45c-118">Пример URI для команд службы REST в Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-118">Provides a sample URI for the REST service commands in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-119">Доступ к схеме</span><span class="sxs-lookup"><span data-stu-id="5c45c-119">Accessing a Schema</span></span>](accessing-a-schema.md)
  
    
    
> <span data-ttu-id="5c45c-120">Узнайте, как получать доступ к схеме службы REST в Службы Excel и просматривать ее.</span><span class="sxs-lookup"><span data-stu-id="5c45c-120">Learn how to access and look at a schema for the REST service in Excel Services.</span></span>
    
  
 [<span data-ttu-id="5c45c-121">Неподдерживаемые функции интерфейса API REST служб Excel</span><span class="sxs-lookup"><span data-stu-id="5c45c-121">Unsupported Features in Excel Services REST API</span></span>](unsupported-features-in-excel-services-rest-api.md)
  
    
    
> <span data-ttu-id="5c45c-122">Список некоторых важных функций, которые в настоящее время не поддерживаются или не работают в REST API Службы Excel.</span><span class="sxs-lookup"><span data-stu-id="5c45c-122">Lists some of the more important features that are currently not supported or working in the Excel Services REST API.</span></span>
    
  
 [<span data-ttu-id="5c45c-123">Расширенные сценарии и дополнительные примеры</span><span class="sxs-lookup"><span data-stu-id="5c45c-123">Advanced Scenarios and Additional Samples</span></span>](advanced-scenarios-and-additional-samples.md)
  
    
    
> <span data-ttu-id="5c45c-124">Описание некоторых сложных сценариев REST и ссылки на дополнительные примеры.</span><span class="sxs-lookup"><span data-stu-id="5c45c-124">Describes some advanced REST scenarios and provides links to additional samples.</span></span>
    
  

