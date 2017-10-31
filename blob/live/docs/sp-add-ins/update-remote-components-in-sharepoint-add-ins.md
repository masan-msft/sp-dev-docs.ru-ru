---
title: "Обновление удаленных компонентов в надстройках SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: a15890881bb4269ef21e5a2f22865509e9834750
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="update-remote-components-in-sharepoint-add-ins"></a><span data-ttu-id="0c11d-102">Обновление удаленных компонентов в надстройках SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-102">Update remote components in SharePoint Add-ins</span></span>
<span data-ttu-id="0c11d-103">Узнайте, как обновлять удаленные веб-приложения и базы данных в надстройках SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c11d-103">Update the remote web applications and databases in a SharePoint Add-in.</span></span>
 

 <span data-ttu-id="0c11d-p101">**Примечание.** В настоящее время идет процесс замены названия "приложения для SharePoint" названием "надстройки SharePoint". Во время этого процесса в документации и пользовательском интерфейсе некоторых продуктов SharePoint и средств Visual Studio может по-прежнему использоваться термин "приложения для SharePoint". Дополнительные сведения см. в статье [Новое название приложений для Office и SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="0c11d-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 


## <a name="prerequisites-for-updating-the-remote-components-of-a-sharepoint-add-in"></a><span data-ttu-id="0c11d-107">Необходимые условия для обновления удаленных компонентов надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-107">Prerequisites for updating the remote components of a SharePoint Add-in</span></span>
<span data-ttu-id="0c11d-108"><a name="Prerequistes"> </a></span><span class="sxs-lookup"><span data-stu-id="0c11d-108"><a name="Prerequistes"> </a></span></span>

<span data-ttu-id="0c11d-109">Ознакомьтесь со статьей [Обновление надстроек SharePoint](update-sharepoint-add-ins.md), в том числе с перечисленными в ней предварительными требованиями и основными понятиями.</span><span class="sxs-lookup"><span data-stu-id="0c11d-109">Be familiar with  [Update SharePoint Add-ins](update-sharepoint-add-ins.md) and the prerequisites and core concepts listed in it.</span></span>
 

 

## <a name="update-remote-components"></a><span data-ttu-id="0c11d-110">Обновление удаленных компонентов</span><span class="sxs-lookup"><span data-stu-id="0c11d-110">Update remote components</span></span>
<span data-ttu-id="0c11d-111"><a name="UpdateRemote"> </a></span><span class="sxs-lookup"><span data-stu-id="0c11d-111"><a name="UpdateRemote"> </a></span></span>

<span data-ttu-id="0c11d-p102">В связи с большим количеством различий между платформами и клиентскими системами в целом можно предоставить только очень общие рекомендации по обновлению удаленных компонентов. В следующих двух разделах приведены некоторые инструкции.</span><span class="sxs-lookup"><span data-stu-id="0c11d-p102">For the most part, only very general advice can be provided for updating the remote components because of the wide differences in platforms and tenancy systems. The following two sections provide some guidance.</span></span>
 

 

### <a name="update-remote-components-in-a-provider-hosted-add-in"></a><span data-ttu-id="0c11d-114">Обновление удаленных компонентов в надстройке, размещаемой у поставщика</span><span class="sxs-lookup"><span data-stu-id="0c11d-114">Update remote components in a provider-hosted add-in</span></span>
<span data-ttu-id="0c11d-115"><a name="UpdateProviderHosted"> </a></span><span class="sxs-lookup"><span data-stu-id="0c11d-115"><a name="UpdateProviderHosted"> </a></span></span>

<span data-ttu-id="0c11d-p103">Для обновления удаленных компонентов надстройки SharePoint с размещением у поставщика следует использовать лучшие процедуры обновления платформы, на которой размещены компоненты. Точно так же как удаленные компоненты надстройки с размещением у поставщика установлены отдельно от самой надстройки SharePoint, обновляются они тоже отдельно. При этом необходимо помнить о следующем.</span><span class="sxs-lookup"><span data-stu-id="0c11d-p103">For a provider-hosted SharePoint Add-in, you update the remote components using the best update practices of the platform on which the components are hosted. Just as the remote components of a provider-hosted add-in are installed separately from the installation of the SharePoint Add-in itself, they are also updated separately. Some points to consider:</span></span>
 

 

- <span data-ttu-id="0c11d-119">Обновленные удаленные компоненты должны продолжать функционировать со всеми предыдущими версиями надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c11d-119">The updated remote components should continue to work with all earlier versions of the SharePoint Add-in.</span></span>
    
 
- <span data-ttu-id="0c11d-120">Если для своих удаленных компонентов вы внедрили систему обособления клиента, помните, что различные клиенты могут использовать несколько версий надстройки, а для отдельных клиентов даже могут быть установлены различные версии на различных веб-сайтах SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c11d-120">If you implemented a tenancy isolation system for your remote components, keep in mind that different tenants might be using multiple versions of your add-in, and a specific tenant might even have different versions installed on various SharePoint websites.</span></span>
    
 
<span data-ttu-id="0c11d-p104">В случае надстройки SharePoint с размещением у поставщика, которая использует База данных SQL Microsoft Azure или SQL Server, существует несколько методов обновления базы данных. Для начала см. статью  [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c11d-p104">For a provider-hosted SharePoint Add-in that uses Microsoft Azure SQL Database or SQL Server, there are multiple methods for updating the database. To get started, see  [Upgrade a Data-tier Application](http://msdn.microsoft.com/library/c117df94-f02b-403f-9383-ec5b3ac3763c.aspx).</span></span>
 

 

## <a name="next-steps"></a><span data-ttu-id="0c11d-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0c11d-123">Next steps</span></span>
<span data-ttu-id="0c11d-124"><a name="Next"> </a></span><span class="sxs-lookup"><span data-stu-id="0c11d-124"><a name="Next"> </a></span></span>

<span data-ttu-id="0c11d-125">Вернитесь к разделу  [Основные действия при обновлении надстройки](update-sharepoint-add-ins.md#MajorAppUpgradeSteps) или перейдите непосредственно к одной из следующих статей, чтобы узнать, как обновить следующий важный компонент надстройки SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0c11d-125">Return to  [Major steps in updating an add-in](update-sharepoint-add-ins.md#MajorAppUpgradeSteps), or go directly to one of the following articles to learn how to update the next major component of your SharePoint Add-in.</span></span>
 

 

-  [<span data-ttu-id="0c11d-126">Обновление компонентов сайта надстройки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-126">Update add-in web components in SharePoint</span></span>](update-add-in-web-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="0c11d-127">Обновление компонентов хост-сайта в SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-127">Update host web components in SharePoint</span></span>](update-host-web-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="0c11d-128">Создание обработчика событий обновления для надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-128">Create a handler for the update event in SharePoint Add-ins</span></span>](create-a-handler-for-the-update-event-in-sharepoint-add-ins.md)
    
 

## <a name="additional-resources"></a><span data-ttu-id="0c11d-129">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0c11d-129">Additional resources</span></span>
<span data-ttu-id="0c11d-130"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="0c11d-130"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="0c11d-131">Обновление надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-131">Update SharePoint Add-ins</span></span>](update-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="0c11d-132">Процесс обновления надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="0c11d-132">SharePoint Add-ins update process</span></span>](sharepoint-add-ins-update-process.md)
    
 

