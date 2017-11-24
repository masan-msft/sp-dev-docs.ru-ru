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
# <a name="removing-excel-interactive-view-from-a-webpage"></a>Удаление интерактивное представление Excel из веб-страницы

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
  
    
    

## <a name="additional-resources"></a>Дополнительные ресурсы
<a name="bk_addresources"> </a>


-  [Службы Excel в SharePoint](excel-services-in-sharepoint.md)
    
  
-  [Внедрение книги Excel в блог](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  
