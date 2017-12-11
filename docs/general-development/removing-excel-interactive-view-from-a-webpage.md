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
# <a name="removing-excel-interactive-view-from-a-webpage"></a>Удаление интерактивного представления Excel с веб-страницы

Интерактивное представление Excel возможность отключена. Если введено интерактивное представление Excel в веб-страницу, его можно удалить путем удаления `<script>` тег и заполнитель `<a>` тегов для кнопки из HTML-код веб-страницы.
  
    
    

Чтобы удалить `<script>` тега, поиск и удаление следующий HTML-код.


```HTML

<script src="http://r.office.microsoft.com/r/rlidExcelButton?v=1&amp;amp;kip=1" type="text/javascript"></script>
```

Чтобы удалить заполнитель `<a>` поиск тегов, <a> тегов, расположенных непосредственно перед любым <table> элементы в HTML. Так как <a> теги можно настраивать, анализировать HTML для первой части строки, чтобы найти все экземпляры кнопки.


```HTML
<a href="#" name="MicrosoftExcelButton" data-xl-tableTitle="" data-xl-buttonStyle="Standard" data-xl-fileName="Book1" data-xl-attribution="" ></a>
```


## <a name="workarounds"></a>Методы обхода

Мы рекомендуем вам для [внедрения Excel в веб-страницы](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU) в качестве альтернативы.
  
    
    

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>


-  [Службы Excel в SharePoint](excel-services-in-sharepoint.md)
    
  
-  [Внедрение книги Excel в блог](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  

