---
title: "Интеграция расположение и карты функциональные возможности в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 10d4a904-ed27-4513-8c20-d2098aebf22c
ms.openlocfilehash: 8cbacc1860687f7c9880e50ac31da046985f5370
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="integrating-location-and-map-functionality-in-sharepoint"></a><span data-ttu-id="69ab3-102">Интеграция расположение и карты функциональные возможности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-102">Integrating location and map functionality in SharePoint</span></span>
<span data-ttu-id="69ab3-103">Узнайте, как интегрировать сведения о местоположении и карт в списки SharePoint и веб-расположение и мобильных приложений для SharePoint, с помощью нового поля географического расположения и путем создания собственных типов полей на основе географического расположения, на основании географического расположения.</span><span class="sxs-lookup"><span data-stu-id="69ab3-103">Learn how to integrate location information and maps in SharePoint lists and location-based web and mobile apps for SharePoint, by using the new Geolocation field, and by creating your own Geolocation-based field types based on Geolocation.</span></span>
## <a name="what-are-the-location-and-map-features-in-sharepoint"></a><span data-ttu-id="69ab3-104">Что такое расположение и карты возможности в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-104">What are the location and map features in SharePoint?</span></span>
<span data-ttu-id="69ab3-105"><a name="SP15Integrateloc_what"> </a></span><span class="sxs-lookup"><span data-stu-id="69ab3-105"></span></span>

<span data-ttu-id="69ab3-106">SharePoint представлен новый тип поля с именем географического расположения, которая позволяет добавлять комментарии к списки SharePoint, содержащие сведения о расположении.</span><span class="sxs-lookup"><span data-stu-id="69ab3-106">SharePoint introduces a new field type named Geolocation that enables you to annotate SharePoint lists with location information.</span></span> <span data-ttu-id="69ab3-107">В столбцах типа географического расположения можно ввести сведения о расположении в виде пары Широта и долгота координат в десятичное градусов или получить координаты текущее расположение пользователя в браузере, если он реализует интерфейс API географического расположения W3C.</span><span class="sxs-lookup"><span data-stu-id="69ab3-107">In columns of type Geolocation, you can enter location information as a pair of latitude and longitude coordinates in decimal degrees or retrieve the coordinates of the user's current location from the browser if it implements the W3C Geolocation API.</span></span> <span data-ttu-id="69ab3-108">В списке SharePoint расположение на карте корневых объектов на базе службы Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="69ab3-108">In the list, SharePoint displays the location on a map powered by Bing Maps.</span></span> <span data-ttu-id="69ab3-109">Кроме того новое представление с именем представления карты отображает элементы списка в виде значков канцелярской кнопки на Bing Maps Ajax управления V7 с элементами списка как карточек в левой панели.</span><span class="sxs-lookup"><span data-stu-id="69ab3-109">In addition, a new view named Map View displays the list items as pushpins on a Bing Maps Ajax control V7 with the list items as cards on the left pane.</span></span> <span data-ttu-id="69ab3-110">На рисунке 1 приведены возможности расположение и карты по умолчанию в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="69ab3-110">Figure 1 summarizes the default location and map features in SharePoint.</span></span> <span data-ttu-id="69ab3-111">Друг с другом поля географического расположения и представления карты позволяют предоставить Пространственные контекста какие-либо сведения по интеграции данных из SharePoint в сопоставления качества и позволяют пользователям вступать в новых способов в web и мобильных приложений и решений.</span><span class="sxs-lookup"><span data-stu-id="69ab3-111">Together, the Geolocation field and the Map View enable you to give a spatial context to any information by integrating data from SharePoint into a mapping experience, and let your users engage in new ways in your web and mobile apps and solutions.</span></span>
  
    
    

> <span data-ttu-id="69ab3-112">**Примечание:** Пакет MSI с именем SQLSysClrTypes.msi необходимо установить на каждый интерфейсный веб-сервер SharePoint для просмотра значения поля географического расположения или данных в виде списка.</span><span class="sxs-lookup"><span data-stu-id="69ab3-112">**Note:** An MSI package named SQLSysClrTypes.msi must be installed on every SharePoint front-end web server to view the geolocation field value or data in a list.</span></span> <span data-ttu-id="69ab3-113">Этот пакет устанавливает компоненты, которые реализуют новые типы идентификатор геометрии, geography и иерархии в SQL Server 2008.</span><span class="sxs-lookup"><span data-stu-id="69ab3-113">This package installs components that implement the new geometry, geography, and hierarchy ID types in SQL Server 2008.</span></span> <span data-ttu-id="69ab3-114">По умолчанию этот файл установлен для SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="69ab3-114">By default, this file is installed for SharePoint Online.</span></span> <span data-ttu-id="69ab3-115">Тем не менее он не является локальных развертываний SharePoint.</span><span class="sxs-lookup"><span data-stu-id="69ab3-115">However, it is not for an on-premises deployment of SharePoint.</span></span> <span data-ttu-id="69ab3-116">Необходимо быть членом группы администраторов фермы для выполнения этой операции.</span><span class="sxs-lookup"><span data-stu-id="69ab3-116">You must be a member of the Farm Administrators group to perform this operation.</span></span> <span data-ttu-id="69ab3-117">Загрузить SQLSysClrTypes.msi, можно в статье [Microsoft SQL Server 2008 R2 пакета дополнительных компонентов SP1](http://www.microsoft.com/en-us/download/details.aspx?id=26728) для SQL Server 2008 или [Пакета дополнительных компонентов Microsoft SQL Server 2012](http://www.microsoft.com/en-us/download/details.aspx?id=29065)для SQL Server 2012 в центре загрузки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="69ab3-117">To download SQLSysClrTypes.msi, see  [Microsoft SQL Server 2008 R2 SP1 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=26728) for SQL Server 2008, or [Microsoft SQL Server 2012 Feature Pack](http://www.microsoft.com/en-us/download/details.aspx?id=29065)for SQL Server 2012 in the Microsoft Download Center.</span></span> 
  
    
    


<span data-ttu-id="69ab3-118">**Рисунок 1. обобщением представление по умолчанию, расположение и функции сопоставления**</span><span class="sxs-lookup"><span data-stu-id="69ab3-118">**Figure 1.Summarized view of the default location and map features**</span></span>

  
    
    

  
    
    
![Расположение по умолчанию и функции сопоставления](../images/SP15Con_HowToAddGeolocationColumn_fig.png)
  
    
    

  
    
    

  
    
    

## <a name="what-can-you-do-with-the-location-and-map-features"></a><span data-ttu-id="69ab3-120">Что можно делать с функциями карты и расположение</span><span class="sxs-lookup"><span data-stu-id="69ab3-120">What can you do with the location and map features?</span></span>
<span data-ttu-id="69ab3-121"><a name="SP15Integrateloc_do"> </a></span><span class="sxs-lookup"><span data-stu-id="69ab3-121"></span></span>

<span data-ttu-id="69ab3-122">Расположение и карты возможности в SharePoint предоставляют уникальные возможности для разработчиков для включения расположение, карты и признаков близости поиска в своих web и мобильных приложений и решений.</span><span class="sxs-lookup"><span data-stu-id="69ab3-122">The location and map features in SharePoint provide unique opportunities for developers to incorporate location, maps, and proximity search features into their web and mobile apps and solutions.</span></span> <span data-ttu-id="69ab3-123">В таблице 1 представлены некоторые basic задачи, которые помогут вам интегрировать сведения о местоположении и сопоставлять функциональных возможностей приложений и решений.</span><span class="sxs-lookup"><span data-stu-id="69ab3-123">Table 1 contains some basic tasks that help you integrate location and map features in your apps and solutions.</span></span>
  
    
    

<span data-ttu-id="69ab3-124">**В таблице 1. Обзор задач по интеграции расположение Basic и сопоставляет функциональные возможности**</span><span class="sxs-lookup"><span data-stu-id="69ab3-124">**Table 1. Basic tasks for integrating location and maps functionality**</span></span>


|<span data-ttu-id="69ab3-125">**Задача**</span><span class="sxs-lookup"><span data-stu-id="69ab3-125">**Task**</span></span>|<span data-ttu-id="69ab3-126">**Описание**</span><span class="sxs-lookup"><span data-stu-id="69ab3-126">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="69ab3-127">Как: задать ключ карт Bing на уровне веб-серверы и фермы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-127">How to: Set the Bing Maps key at the web and farm level in SharePoint</span></span>](how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint.md) <br/> |<span data-ttu-id="69ab3-128">SharePoint использует Bings карты для отображения карты расположения.</span><span class="sxs-lookup"><span data-stu-id="69ab3-128">SharePoint uses Bings Maps to render the map of the location.</span></span> <span data-ttu-id="69ab3-129">Чтобы иметь возможность использовать функцию Bing Maps, необходимо создать ключ Bing Maps и установить ключ на уровне веб-сайте или фермы.</span><span class="sxs-lookup"><span data-stu-id="69ab3-129">To be able to use the Bing Maps feature, you need to create a Bing Maps key and set the key at the web or farm level.</span></span> <span data-ttu-id="69ab3-130">В статье показаны различные способы можно задать ключ в SharePoint и по выбору какой вариант.</span><span class="sxs-lookup"><span data-stu-id="69ab3-130">The article shows the various ways you can set the key in SharePoint and when to choose which option.</span></span> <span data-ttu-id="69ab3-131">Сообщение об ошибке видеть на карте, если вы не используете допустимый ключ Bing Maps, или если ключ не установлен на сайте, в котором перечислены или на уровне фермы.</span><span class="sxs-lookup"><span data-stu-id="69ab3-131">You see an error message on the map if you do not use a valid Bing Maps key or if a key is not set at the web that contains the list or at the farm level.</span></span>  <br/> |
| [<span data-ttu-id="69ab3-132">Как: Добавление столбца географического расположения списка программными средствами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-132">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md) <br/> |<span data-ttu-id="69ab3-p105">В столбце географического расположения недоступен в списках SharePoint для пользователей по умолчанию. Чтобы добавить столбец к списку SharePoint, необходимо писать код. В этом разделе процедура добавления поля географического расположения в список программными средствами.</span><span class="sxs-lookup"><span data-stu-id="69ab3-p105">The Geolocation column is not available in SharePoint lists for users, by default. To add the column to a SharePoint list, you need to write code. In this topic, learn how to add the Geolocation field to a list programmatically.</span></span>  <br/> |
| [<span data-ttu-id="69ab3-136">Как: расширение типа поля географического расположения, с использованием обработки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="69ab3-136">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md) <br/> |<span data-ttu-id="69ab3-137">Можно обеспечить отрисовку по умолчанию пользовательского интерфейса (UI.md), логику и поведение поля географического расположения, путем создания настраиваемых типов полей, производных от поля географического расположения.</span><span class="sxs-lookup"><span data-stu-id="69ab3-137">You can provide your own rendering to default user interface (UI.md), logic, and behavior of the Geolocation field by creating custom field types that derive from the Geolocation field.</span></span> <span data-ttu-id="69ab3-138">SharePoint упрощает создание настраиваемых типов полей, позволяя выполнить JavaScript, предоставляя новое свойство JSLink в класс поля географического расположения, которая указывает настраиваемых JS-файла, который отображает поле.</span><span class="sxs-lookup"><span data-stu-id="69ab3-138">SharePoint simplifies the creation of custom field types by enabling you to run JavaScript by providing a new JSLink property in the Geolocation field class, which points to a custom .js file that renders the field.</span></span>  <br/> <span data-ttu-id="69ab3-139">**Примечание:** Перечислены JSLink, свойство не поддерживается в опросе или событий.</span><span class="sxs-lookup"><span data-stu-id="69ab3-139">**Note:** The JSLink property is not supported on Survey or Events lists.</span></span> <span data-ttu-id="69ab3-140">Календарь SharePoint — это список событий.</span><span class="sxs-lookup"><span data-stu-id="69ab3-140">A SharePoint calendar is an Events list.</span></span>           |
   

## <a name="additional-resources"></a><span data-ttu-id="69ab3-141">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="69ab3-141">Additional resources</span></span>
<span data-ttu-id="69ab3-142"><a name="SP15Integrateloc_addlresources"> </a></span><span class="sxs-lookup"><span data-stu-id="69ab3-142"></span></span>


-  [<span data-ttu-id="69ab3-143">Как: Добавление столбца географического расположения списка программными средствами в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-143">How to: Add a Geolocation column to a list programmatically in SharePoint</span></span>](how-to-add-a-geolocation-column-to-a-list-programmatically-in-sharepoint.md)
    
  
-  [<span data-ttu-id="69ab3-144">Как: задать ключ карт Bing на уровне веб-серверы и фермы в SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-144">How to: Set the Bing Maps key at the web and farm level in SharePoint</span></span>](how-to-set-the-bing-maps-key-at-the-web-and-farm-level-in-sharepoint.md)
    
  
-  [<span data-ttu-id="69ab3-145">Как: расширение типа поля географического расположения, с использованием обработки на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="69ab3-145">How to: Extend the Geolocation field type using client-side rendering</span></span>](how-to-extend-the-geolocation-field-type-using-client-side-rendering.md)
    
  
-  [<span data-ttu-id="69ab3-146">Как: интеграция карт с помощью приложения для Windows Phone и списки SharePoint</span><span class="sxs-lookup"><span data-stu-id="69ab3-146">How to: Integrate maps with Windows Phone apps and SharePoint lists</span></span>](how-to-integrate-maps-with-windows-phone-apps-and-sharepoint-lists.md)
    
  
-  [<span data-ttu-id="69ab3-147">Использование типа поля расположения SharePoint в мобильных приложениях</span><span class="sxs-lookup"><span data-stu-id="69ab3-147">Use the SharePoint location field type in mobile applications</span></span>](http://technet.microsoft.com/ru-ru/library/fp161355%28v=office.15%29.aspx)
    
  
