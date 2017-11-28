---
title: "Тип настраиваемого поля в объектная модель SharePoint"
ms.date: 11/03/2017
ms.openlocfilehash: 550669c2e1cb7e766f93ed1ae00fc0962421bace
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
<a name="custom-field-type-in-the-sharepoint-add-in-model"></a>Тип настраиваемого поля в объектная модель SharePoint
================================================

<a name="summary"></a>Summary
-------

Выбор подхода для обеспечения работы настраиваемого конечного пользователя отличается новой модели надстройки SharePoint от был с кодом полного доверия. В типичных полного доверия кода (FTC) / сценарий решения фермы, настраиваемые типы полей были созданы с помощью кода на сервере объектной модели SharePoint путем наследования от одного из классов встроенных типов полей для создания файла развертывания типов полей (XML). Эти компоненты были развернуты через решений SharePoint. 

В сценарии модели надстройки SharePoint каждый раз пользовательское реализуются с помощью обработки на стороне клиента. В этот подход файлы JavaScript, используемых для реализации работы настраиваемого конечного пользователя. Удаленный подготовки шаблон развертывает файлы JavaScript и регистрирует их с полями SharePoint через свойство JSLink.

С точки зрения конечного пользователя, и возможность/результат выглядит так же.

Вот несколько примеров настраиваемого типа поля, который реализует Google карты. Эти поступают из примера PnP [Branding.JSLink](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink) Office 365.

**Google карты эскизов отображается в представлении списка:**

![Два представления карты Google, отражающая точка расположении Microsoft территории и расположение области.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps.png)

**Встроенное редактирование отображение большего эскиза карты Google:**
![сопоставляет два Google. Отображение точка расположении территории Microsoft со ссылкой выберите расположение, другие представление со значениями области расположение территории корпорации Майкрософт со ссылкой на изменение фигуры одно представление.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Edit.png)

**Диалоговое окно включения встроенная Правка:**
![карты Google отображение фигуры территории корпорации Майкрософт. Считывает текст на изображении, щелкните на карте, чтобы поместить маркерами и создание фигуры. Завершить, щелкнув на первый маркер. Перетащите каждый из маркеров вокруг или щелкните Дополнительные параметры. Кнопка очистки соответствия выше можно использовать для удаления всех маркеров.](https://github.com/SharePoint/PnP/blob/master/Samples/Branding.JSLink/readme-images/GoogleMaps_Shape_Edit.png)

<a name="high-level-guidelines"></a>Рекомендации по высокого уровня
---------------------

Как правило эскиз мы предлагаем для обеспечения высокого уровня следующие рекомендации для реализации обработки на стороне клиента.

- Для реализации настраиваемые типы полей используйте файлы JavaScript и обработки на стороне клиента.
- Шаблон удаленного подготовки для развертывания файлов JavaScript и зарегистрировать их с полями SharePoint или веб-частей представления списка.
- Регистрация файлов JavaScript с ядром стратегия минимальной загрузки (MDS), чтобы убедиться, что модуль MDS принять во внимание файлов JavaScript пользовательской визуализации.
- Установка для свойства JSLink хост-сайта требуется по крайней мере полное разрешение на уровне веб-, поэтому этот подход не подходит для надстроек в магазине SharePoint

<a name="options-to-implement-client-side-rendering-with-javascript-files-via-the-jslink-property"></a>Параметры для реализации обработки на стороне клиента с помощью файлов JavaScript через свойство JSLink
----------------------------------------------------------------------------------------

У вас есть две возможности для реализации обработки на стороне клиента с помощью файлов JavaScript через свойство JSLink.

- Присвойте свойству JSLink на веб-часть представления списка, который отображает список SharePoint. 
- Присвойте свойству JSLink для поля SharePoint. 
- Присвойте свойству JSLink для типа контента SharePoint. 
    

<a name="set-the-jslink-property-on-a-list-view-web-part-that-renders-a-view-of-a-sharepoint-list"></a>Присвойте свойству JSLink на веб-часть представления списка, который отображает представление списка SharePoint
-----------------------------------------------------------------------------------------
В этот параметр, задайте свойству JSLink на WebPartDefinition.
    
- **Такой подход специально не создать настраиваемый тип поля на уровне SPField.**
    + Таким образом, *пользовательской визуализации применяется только в веб-часть представления списка, где присвойте свойству JSLink*.
- Такой подход позволяет изменять с отображением для одного или нескольких полей SharePoint за один раз.
- Этот подход может быть выполнено с помощью декларативного кода с помощью серверного объектной модели SharePoint, с помощью клиентской объектной модели SharePoint (CSOM) или через PowerShell.
    + Мы рекомендуем использовать на сервере объектной модели SharePoint, клиентской объектной модели SharePoint или PowerShell для свойства JSLink с помощью удаленного подготовки шаблон.

**Когда это подходит?**

При необходимости для определения конкретного представления для данных списков SharePoint и изменения представления для более одного поля SharePoint это является хорошим выбором.

**Приступая к работе**

Следующий пример задает свойство JSLink на веб-часть представления списка SharePoint.

- [Branding.ClientSideRendering (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
    + Включает в себя 9 примеров, присвойте свойству JSLink на веб-часть представления списка SharePoint и объяснение реализации каждого примера.
    + Метод RegisterJStoWebPart задает свойство JSLink списка представления веб-части. 

<a name="set-the-jslink-property-for-a-sharepoint-field"></a>Задайте для свойства JSLink для поля SharePoint
----------------------------------------------

В этот параметр, задайте свойству JSLink на SPField.
    
- **Такой подход специально регистрирует свойство JSLink на уровне SPField.**
    + Таким образом, *пользовательской визуализации будут применяться везде, где отображается SPField*.
- Такой подход позволяет изменить визуализации для одного поля SharePoint.
- Этот подход может быть выполнено с помощью декларативного кода с помощью серверного объектной модели SharePoint, с помощью клиентской объектной модели SharePoint или через PowerShell.
    + Мы рекомендуем использовать на сервере объектной модели SharePoint, клиентской объектной модели SharePoint или PowerShell для свойства JSLink с помощью удаленного подготовки шаблон.

**Когда это подходит?**

Если вам необходимо определить определенного представления для указанного поля SharePoint и убедитесь, что представление всегда используется при отображении поля, это является хорошим выбором.

**Приступая к работе**

Следующие статьи показано, как задать свойство JSLink на SPField.

- [С помощью свойства JSLink, чтобы изменить способ отображения поля или представления в SharePoint 2013 (Тобиаса Zimmergren)](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [С помощью JSLink с SharePoint 2013 (журнал MSDN)](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)

<a name="challenges-with-implementing-client-side-rendering-with-javascript-files-via-the-jslink-property"></a>Проблемы, связанные с с реализация обработки на стороне клиента с помощью файлов JavaScript через свойство JSLink
------------------------------------------------------------------------------------------------

При разработке компонентов настраиваемой обработки на стороне клиента, следует помнить следующее.

- Не все поля SharePoint может быть переопределен с помощью свойства JSLink.
    + TaxonomyField является хорошим примером.
- JSLink поддерживает несколько токенов.
    + _layouts
    + _SITE
    + _siteCollection
    + _siteCollectionLayouts
    + _siteLayouts
- Файлы JSLink JavaScript можно регистрировать с помощью платформы SharePoint скрипта на запросами (укладки ДЕРНА) для отложенной загрузки файла.
    - Используйте тег (d) в конце JSLink URL-адрес для регистрации файла с укладки ДЕРНА.
 
    ```
    ~sitecollection/Style Library/JSLink-Samples/DependentFields.js(d)
    ```
- Для загрузки нескольких файлов JavaScript через свойство JSLink.
    + Это особенно удобно, если у вас есть библиотека файлов JavaScript, которые реализуют вашей обработки на стороне клиента.
    + Рекомендуется использовать этот подход, когда для мобильных устройств, так как она позволяет обеспечить только что JavaScript, необходимых для реализации обработки на стороне клиента данное поле SharePoint.
    + Использование | символ в отдельные файлы JavaScript, который вы хотите загрузить. 
    
    ```
    ~sitecollection/Style Library/JSLink-Samples/MainLibrary.js|~sitecollection/Style Library/JSLink-Samples/SpecificField.js**(d)**
    ```

<a name="related-links"></a>Ссылки по теме
=============
- [Свойство SPField.JSLink (документы API MSDN)](https://msdn.microsoft.com/en-us/library/microsoft.sharepoint.spfield.jslink.aspx)
- [С помощью свойства JSLink, чтобы изменить способ отображения поля или представления в SharePoint 2013 (Тобиаса Zimmergren)](http://zimmergren.net/technical/sp-2013-using-the-spfield-jslink-property-to-change-the-way-your-field-is-rendered-in-sharepoint-2013)
- [С помощью JSLink с SharePoint 2013 (журнал MSDN)](https://msdn.microsoft.com/en-us/magazine/dn745867.aspx)
- Руководств по [http://aka.ms/OfficeDevPnPGuidance](http://aka.ms/OfficeDevPnPGuidance "Руководств")
- Справочные материалы в библиотеке MSDN по [http://aka.ms/OfficeDevPnPMSDN](http://aka.ms/OfficeDevPnPMSDN "Справочные материалы в библиотеке MSDN")
- Видеозаписи по [http://aka.ms/OfficeDevPnPVideos](http://aka.ms/OfficeDevPnPVideos "видео")

<a name="related-pnp-samples"></a>Примеры связанных с ними PnP
===================

- [Branding.ClientSideRendering (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.ClientSideRendering)
- [Branding.JSLink (O365 PnP образец)](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.JSLink)
- Примеры и содержимое в https://github.com/SharePoint/PnP

<a name="applies-to"></a>Применимо к
==========
- Office 365 нескольких клиентов (MT)
- Office 365 выделенных (D) *частично*
- SharePoint 2013 в локальной — *частично*

*Шаблоны для выделенных и локальной идентичны с помощью надстройки SharePoint методики модели, но возможных технологий, которые могут использоваться отличаются.*
