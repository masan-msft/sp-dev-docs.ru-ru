---
title: "Как получить URL-адрес библиотеки страниц"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d9922e4b-4948-4c4a-a8ca-1623168143a3
ms.openlocfilehash: c1ad399ddf59d928ca46356be1fc762b2312443e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-retrieve-the-url-of-a-pages-library"></a><span data-ttu-id="6e7d5-102">Как: получить URL-адрес библиотеки страниц</span><span class="sxs-lookup"><span data-stu-id="6e7d5-102">How to: Retrieve the URL of a Pages library</span></span>
<span data-ttu-id="6e7d5-103">Узнайте, как получить URL-адрес для список страниц для публикации веб-сайта в семействе сайтов, которые отличаются от текущего контекста.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-103">Learn how to retrieve the URL for the pages list for a publishing web in a site collection that differs from the current context.</span></span>
## <a name="core-concepts-to-know-for-retrieving-the-url-of-a-pages-list"></a><span data-ttu-id="6e7d5-104">Основные понятия, которые необходимо знать для получения URL-адрес страницы списка</span><span class="sxs-lookup"><span data-stu-id="6e7d5-104">Core concepts to know for retrieving the URL of a Pages list</span></span>
<span data-ttu-id="6e7d5-105"><a name="SP15_Core_Concepts_URL_MP"> </a></span><span class="sxs-lookup"><span data-stu-id="6e7d5-105"><a name="SP15_Core_Concepts_URL_MP"> </a></span></span>

<span data-ttu-id="6e7d5-p101">При разработке пользовательских приложений для сайтов публикации, можно заметить, что в объектной модели  [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) не предоставляет способ получить URL-адрес для списка страниц публикации веб-сайта в семействе сайтов, которые отличаются от текущего контекста. Несмотря на то, что класс **PublishingWeb** переносит класс [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) для активации экземпляры, которые имеют функции публикации, класс не предназначен для использования для создания экземпляра **SPWeb** настраиваемых объектов вне текущего контекста.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-p101">When developing custom applications for publishing sites, you may notice that the  [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) object model does not expose a way to retrieve the URL for the Pages list of a publishing web in a site collection that differs from the current context. Although the **PublishingWeb** class wraps the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) class for instances that have the publishing feature activated, the class is not intended to be used to instantiate **SPWeb** objects outside of the current context.</span></span>
  
    
    
<span data-ttu-id="6e7d5-p102">Если вам потребуется получить URL-адрес для список страниц для разных веб-приложения, можно запросить свойство  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) . Поскольку объект [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx)  это объект [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) сайта публикации, можно запросить свойство [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) и записать его содержимое консольное приложение. Если запись `Key = vti_pageslistname, Value = {the URL to the Pages library}` возвращается в консоли, *{URL-адрес в библиотеку страниц}*   URL-адрес страницы списка.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-p102">If you need to retrieve the URL for the Pages list for a different web application, you can query the  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) property. Since the [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) object is the [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) object of a publishing site, you can query the [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) property and write its contents to a console application. If the entry `Key = vti_pageslistname, Value = {the URL to the Pages library}` is returned in the console, *{the URL to the Pages library}*  is the Pages list URL.</span></span>
  
    
    

<span data-ttu-id="6e7d5-111">**В таблице 1. Основные понятия, которые для получения URL-адрес библиотеки страниц**</span><span class="sxs-lookup"><span data-stu-id="6e7d5-111">**Table 1. Core concepts for retrieving the URL of a Pages library**</span></span>


|<span data-ttu-id="6e7d5-112">**Название статьи**</span><span class="sxs-lookup"><span data-stu-id="6e7d5-112">**Article title**</span></span>|<span data-ttu-id="6e7d5-113">**Описание**</span><span class="sxs-lookup"><span data-stu-id="6e7d5-113">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="6e7d5-114">Библиотека страниц</span><span class="sxs-lookup"><span data-stu-id="6e7d5-114">Pages Library</span></span>  <br/> |<span data-ttu-id="6e7d5-115">Библиотека документов, которая содержит все страницы содержимого для сайта публикации.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-115">A document library that contains all the content pages for a publishing site.</span></span>  <br/> |
| [<span data-ttu-id="6e7d5-116">SPWeb</span><span class="sxs-lookup"><span data-stu-id="6e7d5-116">SPWeb</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) <br/> |<span data-ttu-id="6e7d5-117">Представляет SharePoint Foundation веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-117">Represents a SharePoint Foundation website.</span></span>  <br/> |
| [<span data-ttu-id="6e7d5-118">Properties</span><span class="sxs-lookup"><span data-stu-id="6e7d5-118">Properties</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) <br/> |<span data-ttu-id="6e7d5-119">Возвращает объект  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) с метаданными для текущего веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-119">Gets a  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) object with metadata for the current website.</span></span> <br/> |
| [<span data-ttu-id="6e7d5-120">SPPropertyBag</span><span class="sxs-lookup"><span data-stu-id="6e7d5-120">SPPropertyBag</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) <br/> |<span data-ttu-id="6e7d5-121">Сохранение произвольных пар ключей и значений, которые содержат параметры настраиваемого свойства.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-121">Stores arbitrary key and value pairs that contain custom property settings.</span></span>  <br/> |
| [<span data-ttu-id="6e7d5-122">PublishingWeb</span><span class="sxs-lookup"><span data-stu-id="6e7d5-122">PublishingWeb</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) <br/> |<span data-ttu-id="6e7d5-123">Обеспечивает поведение публикации для экземпляра **SPWeb**, которая поддерживает публикацию.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-123">Provides publishing behavior for an instance of **SPWeb** that supports publishing.</span></span> <br/> |
   

## <a name="retrieve-the-url-of-a-pages-list-for-a-publishing-web-in-a-site-collection-that-differs-from-the-current-context"></a><span data-ttu-id="6e7d5-124">Получение URL-адрес список страниц для публикации веб-сайта в семействе сайтов, которые отличаются от текущего контекста</span><span class="sxs-lookup"><span data-stu-id="6e7d5-124">Retrieve the URL of a Pages list for a publishing web in a site collection that differs from the current context</span></span>
<span data-ttu-id="6e7d5-125"><a name="SP15_Code_URL_Pages_List"> </a></span><span class="sxs-lookup"><span data-stu-id="6e7d5-125"><a name="SP15_Code_URL_Pages_List"> </a></span></span>

<span data-ttu-id="6e7d5-126">В этом примере консольное приложение получает доступ к свойству  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) , итерацию по коллекции и записывает каждую пару ключ значение на консоль.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-126">This example console application accesses the  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) property, iterates through the collection, and writes each key/value pair to the console.</span></span>
  
    
    

### <a name="to-query-the-spwebproperties-property-for-the-url-to-the-pages-list"></a><span data-ttu-id="6e7d5-127">Запрос свойства SPWeb.Properties для URL-адреса в список страниц</span><span class="sxs-lookup"><span data-stu-id="6e7d5-127">To query the SPWeb.Properties property for the URL to the Pages list</span></span>


1. <span data-ttu-id="6e7d5-128">Написание консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-128">Write the console application.</span></span>
    
  
2. <span data-ttu-id="6e7d5-129">Просмотра выходных данных в консоль.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-129">View the output in the console.</span></span>
    
  

## <a name="example-query-spwebproperties-property-for-the-url-to-the-pages-list"></a><span data-ttu-id="6e7d5-130">Пример: Свойства SPWeb.Properties запроса для URL-адреса в список страниц</span><span class="sxs-lookup"><span data-stu-id="6e7d5-130">Example: Query SPWeb.Properties property for the URL to the Pages list</span></span>
<span data-ttu-id="6e7d5-131"><a name="SP15_Example_SPWeb_Properties"> </a></span><span class="sxs-lookup"><span data-stu-id="6e7d5-131"><a name="SP15_Example_SPWeb_Properties"> </a></span></span>

<span data-ttu-id="6e7d5-132">Приложение запрашивает объект  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) , итерацию его записи словаря и записывает эти записи на консоль.</span><span class="sxs-lookup"><span data-stu-id="6e7d5-132">The application queries the  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) object, iterates through its dictionary entries, and writes those entries to the console.</span></span>
  
    
    

```cs

using System;
using System.Collections;
using Microsoft.SharePoint;
using Microsoft.SharePoint.Utilities;

namespace Test
{
    class Program
    {
        static void Main(string[] args)
        {
            using (SPSite site = new SPSite("http://localhost"))
            {
                using (SPWeb web = site.OpenWeb())
                {
                    SPPropertyBag props = web.Properties;
                    foreach (DictionaryEntry de in props)
                    {
                        Console.WriteLine("Key = {0}, Value = {1}", de.Key, de.Value);
                    }
                }
            }
            Console.ReadLine();
        }
    }
}

```

<span data-ttu-id="6e7d5-133">Выходные данные, это приложение выводит на консоль изменяется в соответствии с веб-сайта для веб-сайта, но он может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6e7d5-133">The output that this application prints to the console varies from website to website, but it might look like the following:</span></span>
  
    
    



```

Key = vti_associatemembergroup, Value = 5
Key = vti_extenderversion, Value = 14.0.0.4016
Key = vti_associatevisitorgroup, Value = 4
Key = vti_associategroups, Value = 5;4;3
Key = vti_createdassociategroups, Value = 3;4;5
Key = vti_siteusagetotalbandwidth, Value = 547
Key = vti_siteusagetotalvisits, Value = 9
Key = vti_associateownergroup, Value = 3
Key = vti_defaultlanguage, Value = en-us
Key = vti_pageslistname, Value = {the URL to the Pages list}
```


## <a name="additional-resources"></a><span data-ttu-id="6e7d5-134">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6e7d5-134">Additional resources</span></span>
<span data-ttu-id="6e7d5-135"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="6e7d5-135"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="6e7d5-136">Создание сайтов для SharePoint</span><span class="sxs-lookup"><span data-stu-id="6e7d5-136">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  

