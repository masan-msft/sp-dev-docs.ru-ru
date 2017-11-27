---
title: "Получение URL-адрес библиотеки страниц"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d9922e4b-4948-4c4a-a8ca-1623168143a3
ms.openlocfilehash: 8f132495459b0b581be648942c81dbf60382cac0
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="retrieve-the-url-of-a-pages-library"></a>Получение URL-адрес библиотеки страниц

Узнайте, как получить URL-адрес для список страниц для публикации веб-сайта в семействе сайтов, которые отличаются от текущего контекста.

## <a name="core-concepts-to-know-for-retrieving-the-url-of-a-pages-list"></a>Основные понятия, которые необходимо знать для получения URL-адрес страницы списка
<a name="SP15_Core_Concepts_URL_MP"> </a>

При разработке пользовательских приложений для сайтов публикации, можно заметить, что в объектной модели  [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) не предоставляет способ получить URL-адрес для списка страниц публикации веб-сайта в семействе сайтов, которые отличаются от текущего контекста. Несмотря на то, что класс **PublishingWeb** переносит класс [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) для активации экземпляры, которые имеют функции публикации, класс не предназначен для использования для создания экземпляра **SPWeb** настраиваемых объектов вне текущего контекста.
  
    
    
Если вам потребуется получить URL-адрес для список страниц для разных веб-приложения, можно запросить свойство  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) . Поскольку объект [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx)  это объект [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) сайта публикации, можно запросить свойство [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) и записать его содержимое консольное приложение. Если запись `Key = vti_pageslistname, Value = {the URL to the Pages library}` возвращается в консоли, *{URL-адрес в библиотеку страниц}*   URL-адрес страницы списка.
  
    
    

**В таблице 1. Основные понятия, которые для получения URL-адрес библиотеки страниц**


|**Название статьи**|**Описание**|
|:-----|:-----|
|Библиотека страниц  <br/> |Библиотека документов, которая содержит все страницы содержимого для сайта публикации.  <br/> |
| [SPWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.aspx) <br/> |Представляет SharePoint Foundation веб-сайта.  <br/> |
| [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) <br/> |Возвращает объект  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) с метаданными для текущего веб-сайта. <br/> |
| [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) <br/> |Сохранение произвольных пар ключей и значений, которые содержат параметры настраиваемого свойства.  <br/> |
| [PublishingWeb](https://msdn.microsoft.com/library/Microsoft.SharePoint.Publishing.PublishingWeb.aspx) <br/> |Обеспечивает поведение публикации для экземпляра **SPWeb**, которая поддерживает публикацию. <br/> |
   

## <a name="retrieve-the-url-of-a-pages-list-for-a-publishing-web-in-a-site-collection-that-differs-from-the-current-context"></a>Получение URL-адрес список страниц для публикации веб-сайта в семействе сайтов, которые отличаются от текущего контекста
<a name="SP15_Code_URL_Pages_List"> </a>

В этом примере консольное приложение получает доступ к свойству  [Properties](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPWeb.Properties.aspx) , итерацию по коллекции и записывает каждую пару ключ значение на консоль.
  
    
    

### <a name="to-query-the-spwebproperties-property-for-the-url-to-the-pages-list"></a>Запрос свойства SPWeb.Properties для URL-адреса в список страниц


1. Написание консольное приложение.
    
  
2. Просмотра выходных данных в консоль.
    
  

## <a name="example-query-spwebproperties-property-for-the-url-to-the-pages-list"></a>Пример: Свойства SPWeb.Properties запроса для URL-адреса в список страниц
<a name="SP15_Example_SPWeb_Properties"> </a>

Приложение запрашивает объект  [SPPropertyBag](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPPropertyBag.aspx) , итерацию его записи словаря и записывает эти записи на консоль.
  
    
    

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

Выходные данные, это приложение выводит на консоль изменяется в соответствии с веб-сайта для веб-сайта, но он может выглядеть следующим образом:
  
    
    



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


## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Создание сайтов для SharePoint](build-sites-for-sharepoint.md)
    
  

