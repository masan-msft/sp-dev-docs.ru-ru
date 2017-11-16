---
title: "Разработка веб-части SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: fdee0792f486ebb792d5aaf8d8c7993cdd273324
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="designing-a-sharepoint-web-part"></a>Разработка веб-части SharePoint

Перед разработкой веб-части SharePoint следует знать, как [создавать страницы на сайте SharePoint](authoring-pages.md). Если вы еще не сделали этого, создайте страницу и добавьте на нее веб-части нескольких типов. Важно понимать, как упростить и ускорить подготовку новой веб-части к работе с помощью компонентов и стилей Office Fabric.

При разработке веб-частей важно владеть понятиями, описанными в следующих статьях:

- [Типы областей свойств и их применение](#property-pane-types)
- [Реактивные и нереактивные веб-части](reactive-and-nonreactive-web-parts.md)
- [Названия и описания](web-part-titles-and-descriptions.md)
- [Резервные варианты и заполнители](placeholders-and-fallbacks.md)


## <a name="property-pane-types"></a>Типы областей свойств

Вы можете использовать области свойств трех типов для оформления и разработки веб-частей, соответствующих потребностям вашего бизнеса и клиентов.

Чтобы открыть область для настройки параметров веб-части, нажмите **Изменить**. С помощью этой области можно включать и отключать функции, выбирать источник и макет, а также задавать параметры. Редактируйте содержимое веб-части в самой веб-части, а не в области свойств.

Ширина области свойств составляет 320 пикселей. При ее открытии выполняется автоматическое расплавление страницы.

### <a name="single-pane"></a>Одиночная область
Одиночная область используется для простых веб-частей с небольшим количеством настраиваемых свойств.


![Одиночная область](../images/design-web-part-single.png)


### <a name="accordion-pane"></a>Область-гармошка
Область-гармошка используется для размещения групп свойств с большим количеством вариантов, образующих длинный прокручивающийся список. Например, у вас может быть три группы с названиями "Свойства", "Внешний вид" и "Макет", по десять компонентов в каждой.

Используйте области-гармошки, если требуется добавить классификацию в сложную веб-часть.

![Область-гармошка](../images/design-web-part-accordion-group.png)


**Пример групп области-гармошки, где открыта последняя область**


![Область-гармошка, где открыта последняя область](../images/design-web-part-accordion-last-open.png)


**Пример групп области-гармошки, где открыты две группы**

![Область-гармошка, где открыты две группы](../images/design-web-part-accordion-two-open.png)



### <a name="steps-pane"></a>Ступенчатая область

Ступенчатая область используется для группирования свойств на нескольких этапах или страницах, если веб-часть требуется настраивать в линейном порядке, а также если параметры, выбранные на первом этапе, влияют на то, какие параметры отображаются на втором или третьем. 

**Этап 1 в ступенчатой области**

На этапе 1 кнопка "Назад" отключена, а кнопка "Далее" включена.

![Ступенчатая область, где включена кнопка "Далее"](../images/design-web-part-step-pane-01.png)


**Этап 2 в ступенчатой области** 

На этапе 2 кнопки "Назад" и "Далее" включены.

![Ступенчатая область, где включены кнопки "Назад" и "Далее"](../images/design-web-part-step-pane-02.png)


**Этап 3 в ступенчатой области** 

На этапе 3 кнопка "Далее" отключена, а кнопка "Назад" включена.

![Ступенчатая область, где включена кнопка "Назад"](../images/design-web-part-step-pane-03.png)