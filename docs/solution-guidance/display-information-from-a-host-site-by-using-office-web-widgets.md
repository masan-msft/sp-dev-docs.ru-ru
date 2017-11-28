---
title: "Отображать сведения о из сайта узла с помощью веб-виджеты Office"
ms.date: 11/03/2017
ms.openlocfilehash: 4554a56d4d7036a948cc1c992793efdf7325268d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2017
---
# <a name="display-information-from-a-host-site-by-using-office-web-widgets"></a><span data-ttu-id="8a2d5-102">Отображать сведения о из сайта узла с помощью веб-виджеты Office</span><span class="sxs-lookup"><span data-stu-id="8a2d5-102">Display information from a host site by using Office Web Widgets</span></span>

<span data-ttu-id="8a2d5-103">Реализации мини-приложения Office Web элементов управления в SharePoint размещение у поставщика в надстройке для отображения информации из сайта узла.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-103">Implement Office Web Widget controls in a SharePoint provider-hosted add-in to display information from a host site.</span></span>

<span data-ttu-id="8a2d5-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="8a2d5-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="8a2d5-105">Веб-виджеты Office можно использовать для отображения информации из сайта SharePoint хостингом в контексте размещение у поставщика в надстройке.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-105">You can use Office Web Widgets to display information from a SharePoint-hosted site in the context of a provider-hosted add-in.</span></span> <span data-ttu-id="8a2d5-106">Веб-виджеты Office — это набор элементов управления, которые предназначены для поиска и обрабатываются как элементы управления, размещенные в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-106">Office Web Widgets are a set of controls that are designed to look and behave like SharePoint-hosted controls.</span></span> <span data-ttu-id="8a2d5-107">Элементы управления представляют собой пакет [NuGet](https://www.nuget.org/) , содержащей [веб-виджеты Office библиотеки](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span><span class="sxs-lookup"><span data-stu-id="8a2d5-107">The controls are provided as a [NuGet](https://www.nuget.org/) package, which provides the [Office Web Widgets library](http://www.nuget.org/packages/Microsoft.Office.WebWidgets.Experimental/).</span></span>

<span data-ttu-id="8a2d5-108">**Осторожность:**  Веб-виджеты Office — это компонент сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-108">**Caution:**  Office Web Widgets are a third-party feature.</span></span> <span data-ttu-id="8a2d5-109">Так как они имеют ряд ограничений, их следует используйте с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-109">Because they have some limitations, use them with caution.</span></span> <span data-ttu-id="8a2d5-110">Для получения дополнительных сведений см.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-110">For more information, see:</span></span>

<span data-ttu-id="8a2d5-111">Пример [Core.OfficeWebWidgets](https://github.com/SharePoint/PnP/tree/dev/Components/Core.OfficeWebWidgets) показано, как реализовать средства выбора людей и элементов управления представления списка, которые включены в библиотеку веб-виджеты Office.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-111">The [Core.OfficeWebWidgets](https://github.com/SharePoint/PnP/tree/dev/Components/Core.OfficeWebWidgets) sample shows you how to implement the people picker and list view controls that are included in the Office Web Widgets library.</span></span> <span data-ttu-id="8a2d5-112">Этот пример надстройки вставляет элементы управления в HTML-код начальной страницы и затем выполняется настройка элементов управления, с помощью файла JavaScript app.js, расположенного в папке Scripts проекта.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-112">This sample add-in inserts the controls into the HTML of the start page, and then configures the controls using the app.js JavaScript file that is located in the project's Scripts folder.</span></span>

<span data-ttu-id="8a2d5-113">Примера запустите страницы показан элемент управления средства выбора людей.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-113">The sample start page shows the people picker control.</span></span> <span data-ttu-id="8a2d5-114">На этой странице можно добавить несколько пользователей, и он содержит два текстовых поля для ввода данных пользователем.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-114">This page allows you to add multiple users, and it contains two text boxes for user input.</span></span>

<span data-ttu-id="8a2d5-115">**На рисунке 1. Страницы Пуск демонстрационная версия средства выбора людей**</span><span class="sxs-lookup"><span data-stu-id="8a2d5-115">**Figure 1. People picker demo start page**</span></span>

![Страница запуска демонстрационная версия средства выбора людей](media/display-information-from-a-host-site-by-using-office-web-widgets/2d6c1585-9615-45c4-b931-a2e0e7d57b3d.png)

<span data-ttu-id="8a2d5-117">Следующий код из файла Default.aspx в веб-проект содержит элемент управления "Выбор людей" внутри `<div>` тег.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-117">The following code from the Default.aspx file of the web project includes the people picker control inside a  `<div>` tag.</span></span>

```
<div id="peoplePickerBackupSiteOwners" data-office-control="Office.Controls.PeoplePicker" data-office-options=
      '{ "placeholder" : "Please choose one or more backup site owner", 
      "allowMultipleSelections" : true,
      "onChange" : handleSiteOwnerBackupChange}'>
</div>

```

<span data-ttu-id="8a2d5-118">На начальной странице также отображается элемент управления представления списка, который может отображать списков из веб-сайт и web-надстройки на сайте SharePoint.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-118">The start page also displays the list view control, which can display lists from both the host web and the add-in web of the SharePoint site.</span></span>

<span data-ttu-id="8a2d5-119">**На рисунке 2. Страница запуска элемента управления представления списка**</span><span class="sxs-lookup"><span data-stu-id="8a2d5-119">**Figure 2. List view control start page**</span></span>

![Страница запуска элемента управления представления списка](media/display-information-from-a-host-site-by-using-office-web-widgets/c8bc86d4-6cae-4dc0-94a4-97a0e5a49c7d.png)

<span data-ttu-id="8a2d5-121">Следующий HTML-код из файла Default.aspx состоит из двух `<div>` тегов для отображения двух экземпляров списка просмотра элемента управления.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-121">The following HTML from the Default.aspx file includes two  `<div>` tags for displaying the two instances of the list view control.</span></span>

```
The list view widget can show (currently no inline editing) data from a list on the add-in web:<br />
<div id="listViewAppWeb"></div>
        <br /><br />
        But the same applies for a list on the host web web:<br />
        <div id="listViewHostWeb"></div>
```

<span data-ttu-id="8a2d5-122">Следующий код в файле app.js создаются два экземпляра элемента управления представления списка.</span><span class="sxs-lookup"><span data-stu-id="8a2d5-122">The following code from the app.js file creates the two instances of the list view control.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="8a2d5-123">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8a2d5-123">Additional resources</span></span>
<span data-ttu-id="8a2d5-124"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="8a2d5-124"></span></span>

- [<span data-ttu-id="8a2d5-125">Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8a2d5-125">UX Components in SharePoint 2013 and SharePoint Online</span></span>](ux-components-in-sharepoint-2013-and-sharepoint-online.md)
