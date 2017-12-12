---
title: "Отображать сведения о из сайта узла с помощью веб-виджеты Office"
ms.date: 11/03/2017
ms.openlocfilehash: b981754845acf967f9a0beb23dd9f0a73186a6ed
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="display-information-from-a-host-site-by-using-office-web-widgets"></a>Отображать сведения о из сайта узла с помощью веб-виджеты Office

Реализации мини-приложения Office Web элементов управления в SharePoint размещение у поставщика в надстройке для отображения информации из сайта узла.

_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_

Веб-виджеты Office можно использовать для отображения информации из сайта SharePoint хостингом в контексте размещение у поставщика в надстройке. Веб-виджеты Office — это набор элементов управления, которые предназначены для поиска и обрабатываются как элементы управления, размещенные в SharePoint. Элементы управления представляют собой пакет [NuGet](https://www.nuget.org/) , содержащей [веб-виджеты Office библиотеки](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).

**Осторожность:**  Веб-виджеты Office — это компонент сторонних производителей. Так как они имеют ряд ограничений, их следует используйте с осторожностью. Для получения дополнительных сведений см.

Пример [Core.OfficeWebWidgets](https://github.com/SharePoint/PnP/tree/dev/Components/Core.OfficeWebWidgets) показано, как реализовать средства выбора людей и элементов управления представления списка, которые включены в библиотеку веб-виджеты Office. Этот пример надстройки вставляет элементы управления в HTML-код начальной страницы и затем выполняется настройка элементов управления, с помощью файла JavaScript app.js, расположенного в папке Scripts проекта.

Примера запустите страницы показан элемент управления средства выбора людей. На этой странице можно добавить несколько пользователей, и он содержит два текстовых поля для ввода данных пользователем.

**На рисунке 1. Страницы Пуск демонстрационная версия средства выбора людей**

![Страница запуска демонстрационная версия средства выбора людей](media/display-information-from-a-host-site-by-using-office-web-widgets/2d6c1585-9615-45c4-b931-a2e0e7d57b3d.png)

Следующий код из файла Default.aspx в веб-проект содержит элемент управления "Выбор людей" внутри `<div>` тег.

```
<div id="peoplePickerBackupSiteOwners" data-office-control="Office.Controls.PeoplePicker" data-office-options=
      '{ "placeholder" : "Please choose one or more backup site owner", 
      "allowMultipleSelections" : true,
      "onChange" : handleSiteOwnerBackupChange}'>
</div>

```

На начальной странице также отображается элемент управления представления списка, который может отображать списков из веб-сайт и web-надстройки на сайте SharePoint.

**На рисунке 2. Страница запуска элемента управления представления списка**

![Страница запуска элемента управления представления списка](media/display-information-from-a-host-site-by-using-office-web-widgets/c8bc86d4-6cae-4dc0-94a4-97a0e5a49c7d.png)

Следующий HTML-код из файла Default.aspx состоит из двух `<div>` тегов для отображения двух экземпляров списка просмотра элемента управления.

```
The list view widget can show (currently no inline editing) data from a list on the add-in web:<br />
<div id="listViewAppWeb"></div>
        <br /><br />
        But the same applies for a list on the host web web:<br />
        <div id="listViewHostWeb"></div>
```

Следующий код в файле app.js создаются два экземпляра элемента управления представления списка.

```
 var listViewAppWeb = new Office.Controls.ListView(document.getElementById("listViewAppWeb"),
          {
                     listUrl: appWebUrl + "/_api/web/lists/getbytitle('Announcements')"
           });

var listViewHostWeb = new Office.Controls.ListView(document.getElementById("listViewHostWeb"),
           {
                     listUrl: spHostUrl + "/_api/web/lists/getbytitle('Site Pages')"
           });
```

## <a name="see-also"></a>См. также
<a name="bk_addresources"> </a>

- [Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
