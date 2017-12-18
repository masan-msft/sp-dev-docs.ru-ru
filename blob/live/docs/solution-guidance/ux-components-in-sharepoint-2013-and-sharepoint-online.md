---
title: "Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online"
ms.date: 11/03/2017
ms.openlocfilehash: aa78ba8feb6783b7cd442e8af718808867182435
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="ux-components-in-sharepoint-2013-and-sharepoint-online"></a><span data-ttu-id="a9c20-102">Компоненты взаимодействия с пользователями в SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a9c20-102">UX Components in SharePoint 2013 and SharePoint Online</span></span>

<span data-ttu-id="a9c20-103">Использование провайдера надстройки SharePoint для компонентов пользовательского интерфейса пользовательского элемента управления в SharePoint 2013 и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="a9c20-103">Use provider-hosted SharePoint Add-ins to control user experience (UX) components in SharePoint 2013 and SharePoint Online.</span></span>

<span data-ttu-id="a9c20-104">_**Область применения:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="a9c20-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

## <a name="in-this-section"></a><span data-ttu-id="a9c20-105">В этом разделе</span><span class="sxs-lookup"><span data-stu-id="a9c20-105">In this section</span></span>

|<span data-ttu-id="a9c20-106">**Статья**</span><span class="sxs-lookup"><span data-stu-id="a9c20-106">**Article**</span></span>|<span data-ttu-id="a9c20-107">**Показано, как для**</span><span class="sxs-lookup"><span data-stu-id="a9c20-107">**Shows you how to**</span></span>|
|:-----|:-----|
|[<span data-ttu-id="a9c20-108">Настройка интерфейса пользователя с помощью SharePoint у поставщика надстроек</span><span class="sxs-lookup"><span data-stu-id="a9c20-108">Customize the UX by using SharePoint provider-hosted add-ins</span></span>](customize-the-ux-by-using-sharepoint-provider-hosted-add-ins.md)|<span data-ttu-id="a9c20-109">Используйте размещение у поставщика надстроек, создавать и изменять страницы, макеты и других артефактов SharePoint SharePoint и, настройки пользовательского интерфейса на размещение веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a9c20-109">Use provider-hosted add-ins that create and modify SharePoint pages, layouts, and other SharePoint artifacts and that customize the user experience on host sites.</span></span>|
|[<span data-ttu-id="a9c20-110">Создание элементов управления пользовательского интерфейса с помощью SharePoint у поставщика надстроек</span><span class="sxs-lookup"><span data-stu-id="a9c20-110">Create UX controls by using SharePoint provider-hosted add-ins</span></span>](create-ux-controls-by-using-sharepoint-provider-hosted-add-ins.md)|<span data-ttu-id="a9c20-111">Использование JavaScript и клиентской объектной модели (CSOM) для создания элементов управления пользовательского интерфейса для отображения в размещенном у поставщика надстроек, которые взаимодействуют с размещение веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="a9c20-111">Use JavaScript and the client object model (CSOM) to create UX controls for display in provider-hosted add-ins that interact with host sites.</span></span> <span data-ttu-id="a9c20-112">Примеры включают средства выбора таксономии, меню таксономии и элементов управления средства выбора людей.</span><span class="sxs-lookup"><span data-stu-id="a9c20-112">The examples include taxonomy picker, taxonomy menu, and people picker controls.</span></span>|
|[<span data-ttu-id="a9c20-113">Отображать сведения о из сайта узла с помощью веб-виджеты Office</span><span class="sxs-lookup"><span data-stu-id="a9c20-113">Display information from a host site by using Office Web Widgets</span></span>](display-information-from-a-host-site-by-using-office-web-widgets.md)|<span data-ttu-id="a9c20-114">Использование экспериментального [пакетов NuGet виджетов Office Web](http://msdn.microsoft.com/en-us/library/office/dn636913%28v=office.15%29.aspx) надстроек размещением у поставщика. Сюда входят средства выбора людей и виджетов представления списка.</span><span class="sxs-lookup"><span data-stu-id="a9c20-114">Use the experimental [Office Web Widgets NuGet package](http://msdn.microsoft.com/en-us/library/office/dn636913%28v=office.15%29.aspx) in provider-hosted add-ins. These include the people picker and list view widgets.</span></span>|
|[<span data-ttu-id="a9c20-115">Улучшения производительности в SharePoint размещение у поставщика в надстройках</span><span class="sxs-lookup"><span data-stu-id="a9c20-115">Improve performance in SharePoint provider-hosted add-ins</span></span>](improve-performance-in-sharepoint-provider-hosted-add-ins.md)|<span data-ttu-id="a9c20-116">Использование файлов cookie HTML5 и HTTP для кэширования данных и сократить число вызовов служб SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a9c20-116">Use HTML5 and HTTP cookies to cache data and reduce the number of calls to SharePoint services.</span></span>|

## <a name="see-also"></a><span data-ttu-id="a9c20-117">См. также</span><span class="sxs-lookup"><span data-stu-id="a9c20-117">See also</span></span>
<span data-ttu-id="a9c20-118"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="a9c20-118"></span></span>

- [<span data-ttu-id="a9c20-119">Фирменная символика и решения для SharePoint 2013 и SharePoint Online по подготовке сайта</span><span class="sxs-lookup"><span data-stu-id="a9c20-119">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
    
- [<span data-ttu-id="a9c20-120">Добавление настраиваемой ленты на сайт SharePoint</span><span class="sxs-lookup"><span data-stu-id="a9c20-120">Add a custom ribbon to your SharePoint site</span></span>](Add-a-custom-ribbon-to-your-SharePoint-site.md)
    
- [<span data-ttu-id="a9c20-121">Надстройки составного бизнеса для SharePoint 2013 и SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="a9c20-121">Composite business add-ins for SharePoint 2013 and SharePoint Online</span></span>](Composite-buisness-apps-for-SharePoint.md)
