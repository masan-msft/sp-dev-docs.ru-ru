---
title: "Реактивные и нереактивные веб-части SharePoint"
description: "Реактивные веб-части выполняются полностью на стороне клиента. Нереактивные веб-части содержат элементы, для работы которых требуется сервер."
ms.date: 01/23/2018
ms.openlocfilehash: 74d1ccfd1ed882d5efbdd8181ac44ceb1a1674eb
ms.sourcegitcommit: 0ad5aeee2c5efc47eb57e050581e4f411c4be643
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2018
---
# <a name="reactive-and-nonreactive-sharepoint-web-parts"></a>Реактивные и нереактивные веб-части SharePoint

Реактивные веб-части работают только на стороне клиента. Нереактивные веб-части содержат элементы, для работы которых необходим сервер. Рекомендуем создавать реактивные веб-части SharePoint, так как они больше соответствуют модели пользовательского интерфейса и принципам WYSIWYG для разработки. Однако в некоторых случаях создавать реактивные веб-части может быть невозможно или невыгодно.


## <a name="reactive-web-parts"></a>Реактивные веб-части

Реактивные веб-части выполняются полностью на стороне клиента. Это означает, что каждый компонент, настроенный в области свойств, отражает изменения, внесенные в веб-части на странице. Например, снятие флажка "Выполненные задачи" скрывает это представление в веб-части "Список дел".

<img alt="A reactive web part" src="../images/design-reactive-01.png" width="850">

## <a name="nonreactive-web-parts"></a>Нереактивные веб-части
Нереактивные веб-части работают не только на стороне клиента. Как правило, одному или нескольким свойствам требуется выполнить вызов, чтобы задать, получить или сохранить данные на сервере. Для нереактивных веб-частей следует включить кнопку **Применить** в нижней части области свойств.

Вы также можете назначить кнопке **Применить** более конкретное действие. <!-- Is this a reference to an image? (design-wp-pp-non-reactive.png) -->

<img alt="A nonreactive web part with Apply and Cancel buttons" src="../images/design-reactive-02.png" width="850">

<br/>

В приведенных ниже примерах показаны нереактивные веб-части в контексте [трех разных областей свойств](design-a-web-part.md).

**Пример одиночной области**

<img alt="A nonreactive web part with a single pane property structure" src="../images/design-reactive-03.png" width="850">

<br/>

**Пример групп элементов "аккордеон"**

<img alt="A nonreactive web part with an according groups pane property structure" src="../images/design-reactive-04.png" width="850">

<br/>

**Пример области с пошаговым представлением**

<img alt="A nonreactive web part with a steps pane property structure" src="../images/design-reactive-05.png" width="850">

## <a name="see-also"></a>См. также

- [Разработка прекрасных решений для SharePoint](design-guidance-overview.md)