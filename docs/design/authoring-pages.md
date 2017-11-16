---
title: "Разработка страниц на сайте SharePoint"
ms.date: 9/25/2017
ms.openlocfilehash: 349de6ef579d2313ddaa27a178cab9c31654e223
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="authoring-pages-in-a-sharepoint-site"></a>Разработка страниц на сайте SharePoint

Разработка страниц в SharePoint — это простой процесс, тем не менее требующий знакомства со средой SharePoint, а также понимания того, для каких целей и для какой аудитории создается страница. Приступая к разработке, полезно следовать нескольким базовым принципам, например "начинайте с простого" и "развивайте то, что работает". Кроме того, полезно регулярно напоминать себе о своей аудитории и целях, которых вы пытаетесь помочь ей достичь.

<!-- Do we have content about the design principles that we can link to here? -->

У интерфейса создания страниц SharePoint есть два режима. 

- В режиме правки авторы страниц могут добавлять и настраивать веб-части, чтобы добавлять содержимое на страницу.
- В режиме публикации группа или аудитория может просматривать содержимое и работать с веб-частями. 

## <a name="edit-mode"></a>Режим правки

При создании страницы пользователям доступен пользовательский интерфейс разработки для добавления и настройки содержимого страницы. 


![Элемент управления "Поле ввода"](../images/design-authoring-edit-01.png)

![Элемент управления "Поле ввода" с указателем, наведенным на выделенный элемент](../images/design-authoring-edit-02.png)


### <a name="add-hint-and-toolbox"></a>Подсказка о добавлении и панель элементов

Подсказка о добавлении — это горизонтальная линия со значком "плюс", которая отображается при выделении веб-части или наведении указателя мыши на нее и указывает на то, что авторы могут добавлять веб-части на свою страницу. Когда пользователь нажимает значок "плюс", открывается панель элементов. Панель элементов содержит все веб-части, которые можно добавить на страницу.

![Подсказка и панель элементов с инструментами](../images/design-authoring-add-hint.png)


### <a name="toolbar"></a>Панель инструментов

Вертикальная панель инструментов и ограничивающий прямоугольник входят в состав платформы для каждой веб-части и предоставляются страницей. Для каждой веб-части на панели инструментов есть действия редактирования и удаления. 

![Развернутая панель инструментов](../images/design-authoring-toolbar.png)


### <a name="active-and-hover-states"></a>Активное и плавающее состояния

В активном и плавающем состояниях обычно отображаются линии подсказок синего цвета или основного цвета темы сайта.

![Плавающее и активное состояние](../images/design-authoring-active-hover-01.png)

По умолчанию веб-часть окружена серым ограничивающим прямоугольником, но при наведении указателя или выборе веб-части его цвет меняется на синий или основной цвет темы сайта.

![Ограничивающий прямоугольник в активном и неактивном состояниях](../images/design-authoring-active-hover-02.png)


### <a name="contextual-edits"></a>Контекстная правка

Создавайте для веб-частей интерфейс в режиме WYSIWYG, чтобы пользователи могли указывать сведения и добавлять содержимое, которое будет отображаться при публикации. Это содержимое следует добавлять на странице, чтобы пользователь понимал, как оно будет отображаться. Например, заголовки и описания следует вводить там, где будет отображаться текст, а новые задачи следует добавлять и редактировать в контексте страницы.

![Элемент формы для контекстной правки](../images/design-authoring-contextual-edits.png)


### <a name="item-level-edits"></a>Правка на уровне элементов

Пользовательский интерфейс веб-части может меняться. Например, текст может превращаться в текстовое поле, а при отображении интерфейса можно менять порядок элементов и отмечать задачи в веб-части. Вы можете включить интерактивные функции веб-частей в режиме правки, режиме чтения или в обоих режимах в зависимости от целей разработки.

![Правка на уровне элемента с выбранным состоянием](../images/design-authoring-item-level.png)


### <a name="property-panes"></a>Области свойств

Области свойств вызываются с помощью значка **Правка** на панели инструментов. Области свойств в первую очередь должны содержать параметры конфигурации для включения и отключения компонентов, которые либо отображаются на странице, либо вызывают службу для отображения содержимого. 

![Развернутая панель](../images/design-authoring-panes.png)


## <a name="published-mode"></a>Режим публикации

После публикации страницы пользовательский интерфейс редактирования отключается для посетителей страницы. Чтобы продолжить ее редактировать, пользователь может нажать кнопку **Изменить** в правом верхнем углу панели команд.

![Выделенная кнопка "Опубликовать"](../images/design-authoring-published.png)


## <a name="mobile-view"></a>Мобильное представление

Все страницы SharePoint являются [адаптивными](grid-and-responsive-design.md), то есть их содержимое можно просматривать на мобильных устройствах. При разработке веб-части важно понимать, как новые страницы сайтов SharePoint отображаются на разных устройствах.



![Мобильное представление сайта](../images/design-authoring-mobile.png)