---
title: "Специальные возможности при разработке веб-части SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: 55dcf68b350ca7ae004a1caad958f623394551be
ms.sourcegitcommit: b05e9f1edb1a23b07b7986655fac92c24dd62f5a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
<!--Based on how rough this content is in it's current state, i'm going to pull it from this initial release so we can edit and better prepare. -->




# <a name="accessibility-in-sharepoint-web-part-design"></a>Специальные возможности при разработке веб-части SharePoint

При разработке веб-части SharePoint важно создать одинаковые возможности для всех пользователей, в том числе для пользователей с ограничениями зрения, слуха, подвижности, речи и способности к восприятию информации. Специальные возможности нужны не только людям с ограничениями, но и в тех ситуациях, когда использование устройства затруднено. Если они обеспечены, разработка выполнена качественно.

## <a name="accessibility-guidelines"></a>Рекомендации по специальным возможностям

<!-- Make sure that this is an external resource that folks can access. Original link was to a OneNote file. -->
Все продукты Майкрософт должны соответствовать требованиям, приведенным в [стандартах Майкрософт, касающихся специальных возможностей](https://microsoft.sharepoint.com/teams/msenable/Pages/MASDetails.aspx
"Ссылка на стандарты Майкрософт, касающиеся специальных возможностей").  

<!-- Fabric components are not designed to be accessible already? And, shouldn't components that aren't based on Fabric also be accessible? -->

Если вы создаете диалоговое окно, средство выбора файлов или любой другой компонент [Office UI Fabric](https://dev.office.com/fabric#/components), следуйте инструкциям из этой статьи для обеспечения специальных возможностей в отношении содержимого. 

<!-- Not sure why we have that link? It currently goes to the OneNote file. Where is the Common UI Controls content? Is that related to accessibility? -->

[Стандартные элементы управления пользовательского интерфейса](https://microsoft.sharepoint.com/teams/STS/_layouts/OneNote.aspx?id=%2Fteams%2FSTS%2FShared%20Documents%2FSP%20Accessibility%2FAccessibility%20Guidance&wd=target%28Accessibility%20101.one%7C0005C142-938C-4411-B543-B9F4199E19B3%2FEverything%20you%20need%20to%20know%20about%20Accessibility%7CE099AFE3-8804-4E1F-BA50-99493AB8A3D0%2F%29 "Ссылка на стандартные элементы управления пользовательского интерфейса")

## <a name="accessibility-testing"></a>Проверка специальных возможностей

<!-- FYI, I added links. Can we assume that our target audience uses the Edge browser? -->

Сначала проверьте веб-часть, используя [экранный диктор](https://support.microsoft.com/ru-RU/help/22798/windows-10-narrator-get-started) и Microsoft Edge, затем — при помощи [JAWS](http://www.freedomscientific.com/Products/Blindness/JAWS).

Экранный диктор и Microsoft Edge соответствуют стандартам. Используя эту комбинацию инструментов, вы с большей вероятностью обнаружите проблемы. С ее помощью можно подтвердить, что сайт соответствует стандартам в отношении специальных возможностей. 

JAWS — лидер рынка среди средств чтения с экрана. JAWS включает компоненты, позволяющие улучшить специальные возможности некоторых веб-сайтов и недоступные в других средствах чтения с экрана. Поэтому тестирование при помощи JAWS не всегда гарантирует, что сайт соответствует всем требованиям к специальным возможностям. 
 
Вы также можете определить сочетание браузера и средства чтения с экрана, которое охватывает наибольшую долю рынка для вашего веб-сайта.

<!-- Delete? This doesn't seem like text that should be in externally published docs? 
When suppliers test with JAWS, we ask them to repro identified bugs with Narrator and Edge. In the case a bug does not repro with Narrator/Edge it is sent to Mary Smith who works with VFO for a Jaws specific fix. 
-->

## <a name="keyboard-navigation"></a>Навигация с помощью клавиатуры

<!-- Is this section telling people how to navigate via a keyboard, or how to design to optimize for keyboard navigation? If the former, . -->

Для некоторых пользователей навигация по сайту с помощью клавиатуры более доступна. Опытные пользователи тоже часто обращаются к этому способу навигации. Можно использовать сочетания клавиш (например, клавишу табуляции — для открытия элементов управления на странице, а клавиши со стрелками — для перехода между ними).

### <a name="navigation-between-controls"></a>Навигация между элементами управления

Каждому элементу управления соответствует позиция табуляции. В отношении элемента управления применяются приведенные ниже правила.

- Обычно первая позиция табуляции — это верхняя левая область элемента управления, а последняя позиция — его нижняя правая область.
- На модальных поверхностях последней позицией табуляции должны быть действия фиксации.
- В списках первая позиция табуляции должна быть первым элементом списка, далее идут команды, а затем — навигация, настройки и т. д.

<!-- We should make sure the content in the accessibility topic is accessibible. ;) Please describe the information that the image conveys; something like this (also consider making the image an actual screen shot, that might be more clear):

In the following image:
The first tab is the list item.
The second tab is the command.
The third tab is the navigation.
-->
![Изображение, на котором показаны позиции табуляции на странице SharePoint](https://i.imgur.com/Vn3VosN.png)

### <a name="navigation-within-a-control"></a>Навигация в элементе управления

Вы можете использовать клавиши со стрелками для перемещения между частями элемента управления (например, пунктами меню, командами на панели команд или элементами списка).

<!-- This image is not very clear. Do you need to have the "blank" list box on the left? -->

![Использование клавиш со стрелками для навигации в элементе управления](https://i.imgur.com/vF0Nk73.png)

### <a name="selecting-the-current-item"></a>Выбор текущего элемента

Используйте клавишу пробела, чтобы выбрать или отменить выбор элемента, который в настоящее время находится в фокусе в элементе управления.

![Выбор элемента списка при помощи клавиши пробела](https://i.imgur.com/j3fBKPl.png)

### <a name="run-a-control"></a>Запуск элемента управления

Нажмите клавишу **ВВОД**, чтобы запустить элемент управления.

![Нажатие клавиши ВВОД для запуска элемента управления](https://i.imgur.com/s0nMPdT.png)

### <a name="leave-a-control"></a>Выход из элемента управления

Нажмите клавишу **ESC**, чтобы выйти из элемента управления и вернуться к контейнеру.

![Выход из элемента управления и возвращение к контейнеру с помощью клавиши ESC](https://i.imgur.com/uD99zIX.png)

### <a name="go-to-the-first-or-last-item"></a>Переход к первому или последнему элементу

Нажмите клавишу **HOME** или **END**, чтобы перейти сразу к первому или последнему элементу списка, меню и т. д.

![Переход к первому или последнему элементу списка с помощью клавиши HOME или END](https://i.imgur.com/gGKsh74.png)


## <a name="screen-reader-navigation"></a>Навигация при помощи средства чтения с экрана

Пользователи с нарушениями зрения полагаются на средства чтения с экрана для навигации по пользовательскому интерфейсу сайта. 

<!-- Narrator isn't a third-party product. This image needs more text/explanation; please also clarify the alt text. Is this section important, or can it be removed, given the previous mention of testing with Narrator and JAWS? Again, the intent/target audience for this information isn't clear - is it for the user, or the designer? Can you explain why this information is important from the designer's POV? -->

![Навигация при помощи средства чтения с экрана на странице SharePoint](https://i.imgur.com/ar23o3X.png)

## <a name="alt-text-and-transcripts"></a>Замещающий текст и текстовые записи

Замещающий текст позволяет добавлять описания изображений, которые могут быть использованы средствами чтения с экрана. Это удобно для людей с нарушениями зрения, которые не могут получать информацию визуально. Проследите, чтобы замещающий текст был описательным, так как некоторые устройства для чтения получают передаваемую изображением информацию, используя средство чтения с экрана. 

Не полагайтесь только на цвет, чтобы передать смысл. Полагайтесь и на цвет, и на форму.

Для полного соответствия стандартам в отношении специальных возможностей добавьте на сайт замещающий текст и полную текстовую запись аудио- и видеоконтента.

## <a name="minimum-readable-contrast"></a>Минимальная контрастность для читаемости

Минимальный уровень контрастности необходим, чтобы помочь пользователям с нарушениями зрения ознакомиться с содержимым страницы. Важно также улучшить читаемость в условиях низкой освещенности и бликов. 

<!-- Convert this image into a table, for accessibility. ;) -->

![Выбор нейтрального цвета, а также цвета темы и оповещений с минимальной контрастностью для читаемости текста](https://i.imgur.com/L7pSF1w.png)


## <a name="high-contrast"></a>Высокая контрастность

При выборе цвета компонентов и состояний на сайте ориентируйтесь на высококонтрастные цвета. Компьютеры с Windows могут только определить, работает ли ПК с высокой контрастностью или с высокой контрастностью белого. По этой причине используйте по умолчанию высокую контрастность черного для высококонтрастной темы любого цвета, кроме белого.

<!-- In the left part of the image, I think the title should be "High Contrast Black". -->

![Параметры высококонтрастного черного и высококонтрастного белого](https://i.imgur.com/qvTFzd4.png)





