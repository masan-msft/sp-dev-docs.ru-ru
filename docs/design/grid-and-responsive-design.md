---
title: "Сетка SharePoint и адаптивный дизайн"
ms.date: 9/25/2017
ms.openlocfilehash: 1025e1863d03bad9056d74c87307a7a1e4c8f103
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-grid-and-responsive-design"></a>Сетка SharePoint и адаптивный дизайн
 
Адаптивные интерфейсы легко масштабируются на различных устройствах, чтобы содержимое лучше отображалась на экранах разных размеров. Адаптивный дизайн также избавляет от необходимости создавать несколько версий страниц сайта для поддержки различных устройств.  

В рекомендациях по проектированию адаптивных страниц в среде разработки SharePoint используется система адаптивной сетки, основанная на [Office UI Fabric](https://dev.office.com/fabric). В этой статье описываются базовая система сетки страниц и пограничные значения, или ключевые размеры экрана, при использовании которых будет меняться разметка страниц. 


![Страница SharePoint на нескольких устройствах](../images/design-grid-responsive-overview.png)



## <a name="page-type-grids"></a>Сетки для страниц 

Для каждой страницы в среде разработки SharePoint могут действовать собственные правила касательно ее применения к адаптивной сетке Fabric. Благодаря этому каждая страница будет хорошо выглядеть независимо от того, для какого устройства она разработана, а интерфейс будет оптимизирован для соответствующей среды. Базовая сетка в классических средах SharePoint представляет собой структуру из 12 столбцов. Количество столбцов и интервал между ними регулируются в соответствии с шириной экрана. 

В следующих разделах представлена базовая структура сетки, применяемая на страницах SharePoint разных типов, чтобы помочь вам лучше понять, как сетка регулируется в соответствии с потребностями интерфейса и устройства.


![Схема сетки с двенадцатью столбцами](../images/design-grid_diagram.png)



### <a name="team-sites"></a>Сайты групп

Область содержимого для сайта группы закреплена в левой части экрана. На сайтах групп есть область навигации в левой части страницы, поэтому веб-части на сетке и функции расплавления не занимают пространство, выделенное для области навигации. Максимальная ширина области содержимого на сайте группы составляет 1204 пикселя, а минимальный размер — 320 пикселей для поддержки мобильных устройств.

![Сайт группы](../images/design-grid-team-site.png)

В приведенных ниже примерах показано, как сетка регулируется между ключевыми значениями на сайте группы.

#### <a name="small-320-x-568"></a>Малый (320 x 568)
Страница малого размера содержит одну центрированную область столбцов с полями по 20 пикселей слева и справа.

![Малая сетка сайта группы](../images/design-grid-Team-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a>Средний (480 x 854)
Страница среднего размера содержит 12 столбцов с интервалами по 16 пикселей.

![Средняя сетка сайта группы](../images/design-grid-Team-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a>Крупный (640 x 1024)
Страница большого размера содержит 12 столбцов с интервалами по 24 пикселя.

![Крупная сетка сайта группы](../images/design-grid-Team-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a>XL (1024 x 768)
Страница размера XL содержит двенадцать столбцов с интервалами по 24 пикселя.

![Сетка размера XL на сайте группы](../images/design-grid-Team-site-XL-Canvas-24px-gutters.png)

#### <a name="xxl-1366-x-768"></a>XXL (1366 x 768)
Страница размера XXL содержит двенадцать столбцов с интервалами по 32 пикселя.

![Сетка размера XXL на сайте группы](../images/design-grid-Team-site–XXL-Canvas-32px-gutters.png)

#### <a name="xxxl-1920-x-1080"></a>XXXL (1920 x 1080)
Страница размера XXXL содержит двенадцать столбцов с интервалами по 32 пикселя.

![Сетка размера XXXL на сайте группы](../images/design-grid-Team-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="team-site-multicolumn-pages-and-web-parts"></a>Страницы с несколькими столбцами и веб-части на сайтах групп
Веб-части горизонтально масштабируются в соответствии с разметкой страницы. В приведенном ниже примере показано, как размер веб-части регулируется, чтобы оставить место для области навигации слева.

![Страница с несколькими столбцами и веб-частями на сайте группы](../images/design-grid-Team-site-web-parts.png)


### <a name="communication-sites"></a>Сайты для общения

Сайты для общения содержат верхнюю область навигации и центрированную область содержимого. Максимальная ширина области содержимого на сайте для общения составляет 1204 пикселей, а минимальный размер — 320 пикселей для поддержки мобильных устройств.

![Сайт для общения](../images/design-grid-communication_site.png)

В приведенных ниже примерах показано, как сетка регулируется между ключевыми значениями на сайте для общения.

#### <a name="small-320-x-568"></a>Малый (320 x 568)
Страница малого размера содержит одну центрированную область столбцов с полями по 20 пикселей слева и справа.

![Сетка малого размера на сайте для общения](../images/design-grid-Communication-site-S-Canvas-no-column.png)

#### <a name="medium-480-x-854"></a>Средний (480 x 854)
Страница среднего размера содержит 12 столбцов с интервалами по 16 пикселей.

![Сетка среднего размера на сайте для общения](../images/design-grid-Communication-site-M-Canvas-16px-gutters.png)

#### <a name="large-640-x-1024"></a>Крупный (640 x 1024)
Страница большого размера содержит 12 столбцов с интервалами по 24 пикселя.

![Сетка большого размера на сайте для общения](../images/design-grid-Communication-site-L-Canvas-24px-gutters.png)

#### <a name="xl-1024-x-768"></a>XL (1024 x 768)
Страница размера XL содержит двенадцать столбцов с интервалами по 24 пикселя.

![Сетка размера XL на сайте для общения](../images/design-grid-Communication-site-XL-Canvas-24px-gutters.png)


#### <a name="xxl-1366-x-768"></a>XXL (1366 x 768)
Страница размера XXL содержит двенадцать столбцов с интервалами по 32 пикселя.

![Сетка размера XXL на сайте для общения](../images/design-grid-Communication-site-XXL-Canvas-32px-gutters-maxwidth-1204.png)


#### <a name="xxxl-1920-x-1080"></a>XXXL (1920 x 1080)
Страница размера XXXL содержит двенадцать столбцов с интервалами по 32 пикселя.

![Сетка размера XXXL на сайте для общения](../images/design-grid-Communication-site-XXXL-Canvas-32px-gutters-maxwidth-1204.png)

#### <a name="communication-site-multicolumn-pages-and-web-parts"></a>Страницы с несколькими столбцами и веб-части на сайтах для общения
Веб-части горизонтально масштабируются в соответствии с разметкой страницы. В этом примере показаны сайт для общения и веб-части для макетов с 1–3 столбцами.

![Страница с несколькими столбцами и веб-частями на сайте для общения](../images/design-grid-Communciation-site-web-parts.png)



## <a name="breakpoints"></a>Пограничные значения 

Для плавного перехода между размерами экрана пользовательский интерфейс SharePoint должен адаптировать разметку при следующих пограничных значениях ширины: 

- 320;
- 1024;
- 1366;
- 1920.
 
При использовании этих пограничных значений следует учитывать, как после оптимизации окна просмотра содержимое сместится к ближайшему пограничному значению. Обратите внимание на то, что эта схема представлена исключительно в качестве иллюстрации и не является точной.


![Схема SharePoint с пограничными значениями](../images/design-grid-breakpoints.png)


Адаптивная сетка на сайтах групп и сайтах для общения регулируется при переходе от больших пограничных значений к значениям для мобильных приложений. Таким образом, сайт оптимизируется для устройства и размера его экрана. В приведенной ниже таблице описываются размеры сетки при различных пограничных значениях для размеров экранов популярных устройств.



| Ширина окна | Устройство                  | Пограничное значение | Столбцы | Интервал | Максимальное количество столбцов на раздел |
|--------------|-------------------------|------------|---------|--------|-------------------------|
| 320          | iPhone 5/SE, 320 x 568     | Малый      | 1       | Н/д    | 1                       |
| 480          | Устройство с 6-дюймовым экраном               | Средний     | 1       | Н/д    | 1                       |
| 640          | Устройство с 8-дюймовым экраном               | Крупный      | 12      | 16     | 2                       |
| 768          | iPad с книжной ориентацией, 768 x 1024  | Крупный      | 12      | 24     | 2                       |
| 1024         | iPad с альбомной ориентацией, 1024 x 768 | Очень крупный    | 12      | 24     | 3                       |
| 1368         | Surface Pro 3, 1368 x 912  | XXL   | 12      | 32     | 3                       |
| 1440         | Surface Pro 4, 1440 x 960  | XXL   | 12      | 32     | 3                       |
| 1600         | Веб-браузер, 1600 x 900            | XXL   | 12      | 32     | 3                       |
| 1920         | Веб-браузер, 1920 x 1080           | XXXL  | 12      | 32     | 3                       |

## <a name="see-also"></a>См. также

- [Набор инструментов и ресурсы для дизайна](https://developer.microsoft.com/en-us/fabric#/resources)

