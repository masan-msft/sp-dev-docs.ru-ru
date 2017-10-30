---
title: "Удаление интерактивное представление Excel из веб-страницы"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 407b3aa3-7286-462b-905f-811a3b7f3f1c
ms.openlocfilehash: bb8372a12f8f33fcfca26c1917ac6e1800d1c80e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="removing-excel-interactive-view-from-a-webpage"></a><span data-ttu-id="68b82-102">Удаление интерактивное представление Excel из веб-страницы</span><span class="sxs-lookup"><span data-stu-id="68b82-102">Removing Excel Interactive View from a webpage</span></span>

<span data-ttu-id="68b82-103">Интерактивное представление Excel возможность отключена.</span><span class="sxs-lookup"><span data-stu-id="68b82-103">The Excel Interactive View feature has been disabled.</span></span> <span data-ttu-id="68b82-104">Если введено интерактивное представление Excel в веб-страницу, его можно удалить путем удаления `<script>` тег и заполнитель `<a>` тегов для кнопки из HTML-код веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="68b82-104">If you have inserted an Excel Interactive View into your web page, you can remove it by removing the  `<script>` tag and the placeholder `<a>` tags for the button from the HTML of your web page.</span></span>
  
    
    

<span data-ttu-id="68b82-105">Чтобы удалить `<script>` тега, поиск и удаление следующий HTML-код.</span><span class="sxs-lookup"><span data-stu-id="68b82-105">To remove the  `<script>` tag, search for and delete the following HTML.</span></span>


```HTML

<script src="http://r.office.microsoft.com/r/rlidExcelButton?v=1&amp;amp;kip=1" type="text/javascript"></script>
```

<span data-ttu-id="68b82-106">Чтобы удалить заполнитель `<a>` поиск тегов, <a> тегов, расположенных непосредственно перед любым</span><span class="sxs-lookup"><span data-stu-id="68b82-106">To remove the placeholder  `<a>` tags, find <a> tags that are located directly before any</span></span> <table> <span data-ttu-id="68b82-107">элементы в HTML.</span><span class="sxs-lookup"><span data-stu-id="68b82-107">elements in your HTML.</span></span> <span data-ttu-id="68b82-108">Так как <a> теги можно настраивать, анализировать HTML для первой части строки, чтобы найти все экземпляры кнопки.</span><span class="sxs-lookup"><span data-stu-id="68b82-108">Because <a> tags are customizable, parse your HTML for the first part of the string to find all the instances of the button.</span></span>


```HTML
<a href="#" name="MicrosoftExcelButton" data-xl-tableTitle="" data-xl-buttonStyle="Standard" data-xl-fileName="Book1" data-xl-attribution="" ></a>
```


## <a name="workarounds"></a><span data-ttu-id="68b82-109">Методы обхода</span><span class="sxs-lookup"><span data-stu-id="68b82-109">Workarounds</span></span>

<span data-ttu-id="68b82-110">Мы рекомендуем вам для [внедрения Excel в веб-страницы](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU) в качестве альтернативы.</span><span class="sxs-lookup"><span data-stu-id="68b82-110">We encourage you to  [embed Excel into your web pages ](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU) as an alternative.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="68b82-111">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="68b82-111">Additional resources</span></span>
<span data-ttu-id="68b82-112"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="68b82-112"></span></span>


-  [<span data-ttu-id="68b82-113">Службы Excel в SharePoint</span><span class="sxs-lookup"><span data-stu-id="68b82-113">Excel Services in SharePoint</span></span>](excel-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="68b82-114">Внедрение книги Excel в блог</span><span class="sxs-lookup"><span data-stu-id="68b82-114">Embed an Excel workbook on your blog</span></span>](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  

