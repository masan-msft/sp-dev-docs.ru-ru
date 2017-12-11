---
title: "Удаление интерактивного представления Excel с веб-страницы"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 407b3aa3-7286-462b-905f-811a3b7f3f1c
ms.openlocfilehash: d91eefbcbb34967acca01da89d60a914d681a46b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="removing-excel-interactive-view-from-a-webpage"></a><span data-ttu-id="b0f0c-102">Удаление интерактивного представления Excel с веб-страницы</span><span class="sxs-lookup"><span data-stu-id="b0f0c-102">Removing Excel Interactive View from a webpage</span></span>

<span data-ttu-id="b0f0c-103">Интерактивное представление Excel возможность отключена.</span><span class="sxs-lookup"><span data-stu-id="b0f0c-103">The Excel Interactive View feature has been disabled.</span></span> <span data-ttu-id="b0f0c-104">Если введено интерактивное представление Excel в веб-страницу, его можно удалить путем удаления `<script>` тег и заполнитель `<a>` тегов для кнопки из HTML-код веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="b0f0c-104">If you have inserted an Excel Interactive View into your web page, you can remove it by removing the  `<script>` tag and the placeholder `<a>` tags for the button from the HTML of your web page.</span></span>
  
    
    

<span data-ttu-id="b0f0c-105">Чтобы удалить `<script>` тега, поиск и удаление следующий HTML-код.</span><span class="sxs-lookup"><span data-stu-id="b0f0c-105">To remove the  `<script>` tag, search for and delete the following HTML.</span></span>


```HTML

<script src="http://r.office.microsoft.com/r/rlidExcelButton?v=1&amp;amp;kip=1" type="text/javascript"></script>
```

<span data-ttu-id="b0f0c-106">Чтобы удалить заполнитель `<a>` поиск тегов, <a> тегов, расположенных непосредственно перед любым</span><span class="sxs-lookup"><span data-stu-id="b0f0c-106">To remove the placeholder  `<a>` tags, find <a> tags that are located directly before any</span></span> <table> <span data-ttu-id="b0f0c-107">элементы в HTML.</span><span class="sxs-lookup"><span data-stu-id="b0f0c-107">elements in your HTML.</span></span> <span data-ttu-id="b0f0c-108">Так как <a> теги можно настраивать, анализировать HTML для первой части строки, чтобы найти все экземпляры кнопки.</span><span class="sxs-lookup"><span data-stu-id="b0f0c-108">Because <a> tags are customizable, parse your HTML for the first part of the string to find all the instances of the button.</span></span>


```HTML
<a href="#" name="MicrosoftExcelButton" data-xl-tableTitle="" data-xl-buttonStyle="Standard" data-xl-fileName="Book1" data-xl-attribution="" ></a>
```


## <a name="workarounds"></a><span data-ttu-id="b0f0c-109">Методы обхода</span><span class="sxs-lookup"><span data-stu-id="b0f0c-109">Workarounds</span></span>

<span data-ttu-id="b0f0c-110">Мы рекомендуем вам для [внедрения Excel в веб-страницы](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU) в качестве альтернативы.</span><span class="sxs-lookup"><span data-stu-id="b0f0c-110">We encourage you to  [embed Excel into your web pages ](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU) as an alternative.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="b0f0c-111">См. также</span><span class="sxs-lookup"><span data-stu-id="b0f0c-111">See also</span></span>
<span data-ttu-id="b0f0c-112"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="b0f0c-112"></span></span>


-  [<span data-ttu-id="b0f0c-113">Службы Excel в SharePoint</span><span class="sxs-lookup"><span data-stu-id="b0f0c-113">Excel Services in SharePoint</span></span>](excel-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="b0f0c-114">Внедрение книги Excel в блог</span><span class="sxs-lookup"><span data-stu-id="b0f0c-114">Embed an Excel workbook on your blog</span></span>](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  

