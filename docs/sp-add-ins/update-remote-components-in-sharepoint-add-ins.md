---
title: "Обновление удаленных компонентов в надстройках SharePoint"
description: "Узнайте, как обновлять удаленные веб-приложения и базы данных в надстройках SharePoint."
ms.date: 11/02/2017
ms.prod: sharepoint
ms.openlocfilehash: c8d74f691253b882846411d671ac808f67bcd057
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2017
---
# <a name="update-remote-components-in-sharepoint-add-ins"></a><span data-ttu-id="81a47-103">Обновление удаленных компонентов в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="81a47-103">Update remote components in SharePoint Add-ins</span></span>

<span data-ttu-id="81a47-104">Прежде чем приступать, ознакомьтесь со статьей [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), в том числе с перечисленными в ней предварительными требованиями и основными понятиями.</span><span class="sxs-lookup"><span data-stu-id="81a47-104">Before you begin, be familiar with [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in it.</span></span>

<span data-ttu-id="81a47-105">Существует много различий между платформами и клиентскими системами, поэтому в целом можно предоставить только очень общие рекомендации по обновлению удаленных компонентов.</span><span class="sxs-lookup"><span data-stu-id="81a47-105">For the most part, only very general advice can be provided for updating the remote components because of the wide differences in platforms and tenancy systems.</span></span> <span data-ttu-id="81a47-106">Следующий раздел содержит некоторые инструкции.</span><span class="sxs-lookup"><span data-stu-id="81a47-106">The following section provides some guidance.</span></span>

<span data-ttu-id="81a47-107">В случае надстройки SharePoint, размещаемой у поставщика, удаленные компоненты можно обновить, следуя рекомендациям по обновлению платформы, на которой размещены компоненты.</span><span class="sxs-lookup"><span data-stu-id="81a47-107">For a provider-hosted SharePoint Add-in, you update the remote components by using the best update practices of the platform on which the components are hosted.</span></span> <span data-ttu-id="81a47-108">Удаленные компоненты надстройки, размещаемой у поставщика, устанавливаются отдельно от самой надстройки SharePoint, поэтому обновляются они тоже отдельно.</span><span class="sxs-lookup"><span data-stu-id="81a47-108">Just as the remote components of a provider-hosted add-in are installed separately from the installation of the SharePoint Add-in itself, they are also updated separately.</span></span> <span data-ttu-id="81a47-109">Факторы, на которые необходимо обратить внимание:</span><span class="sxs-lookup"><span data-stu-id="81a47-109">Some points to consider:</span></span>

- <span data-ttu-id="81a47-110">Обновленные удаленные компоненты должны продолжать работать со всеми предыдущими версиями надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="81a47-110">The updated remote components should continue to work with all earlier versions of the SharePoint Add-in.</span></span>

- <span data-ttu-id="81a47-111">Если для своих удаленных компонентов вы внедрили систему обособления клиента, помните, что различные клиенты могут использовать несколько версий надстройки, а для отдельных клиентов даже могут быть установлены различные версии на различных веб-сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="81a47-111">If you implemented a tenancy isolation system for your remote components, keep in mind that different tenants might be using multiple versions of your add-in, and a specific tenant might even have different versions installed on various SharePoint websites.</span></span>

<span data-ttu-id="81a47-112">В случае надстройки SharePoint, размещаемой у поставщика, которая использует Базу данных SQL Microsoft Azure, существует несколько методов обновления базы данных.</span><span class="sxs-lookup"><span data-stu-id="81a47-112">For a provider-hosted SharePoint Add-in that uses Microsoft Azure SQL Database or SQL Server, there are multiple methods for updating the database.</span></span> <span data-ttu-id="81a47-113">Сначала прочтите статью [Обновление приложения на уровне данных](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span><span class="sxs-lookup"><span data-stu-id="81a47-113">To get started, see [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="81a47-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81a47-114">Next steps</span></span>

<span data-ttu-id="81a47-115">Вернитесь к разделу [Основные шаги по обновлению надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из указанных ниже статей, чтобы узнать, как обновить компоненты надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="81a47-115">Return to [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>

-  [<span data-ttu-id="81a47-116">Обновление компонентов сайта надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="81a47-116">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
-  [<span data-ttu-id="81a47-117">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="81a47-117">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
-  [<span data-ttu-id="81a47-118">Создание обработчика событий обновления в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="81a47-118">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)

## <a name="see-also"></a><span data-ttu-id="81a47-119">См. также</span><span class="sxs-lookup"><span data-stu-id="81a47-119">See also</span></span>

-  [<span data-ttu-id="81a47-120">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="81a47-120">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
-  [<span data-ttu-id="81a47-121">Процесс обновления надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="81a47-121">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process.md) 
    
 

