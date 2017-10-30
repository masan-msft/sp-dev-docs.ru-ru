---
title: "Настройка среды разработки для BCS в SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d83c8a43-49dd-47eb-94d4-23aa2cf71a9a
ms.openlocfilehash: ccd96046c91dae94fb68d5a38cf7a8546f38f284
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="setting-up-a-development-environment-for-bcs-in-sharepoint"></a><span data-ttu-id="da3ee-102">Настройка среды разработки для BCS в SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-102">Setting up a development environment for BCS in SharePoint</span></span>
<span data-ttu-id="da3ee-103">Сведения о настройке среды разработки для разработки решений SharePoint и надстройки SharePoint с помощью Business Connectivity Services (BCS).</span><span class="sxs-lookup"><span data-stu-id="da3ee-103">Learn about setting up a development environment for developing SharePoint solutions and SharePoint Add-ins using Business Connectivity Services (BCS).</span></span>
<span data-ttu-id="da3ee-104">Решения SharePoint и надстройки SharePoint можно создать с помощью службы BCS на клиентском компьютере или на компьютере сервера, в зависимости от типа решения, которое создается.</span><span class="sxs-lookup"><span data-stu-id="da3ee-104">You can create SharePoint solutions and SharePoint Add-ins by using BCS on a client computer or on a server computer, depending on the type of solution you are building.</span></span>
  
    
    


## <a name="building-server-based-solutions-and-sharepoint-add-ins"></a><span data-ttu-id="da3ee-105">Разработка решений на стороне сервера и Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-105">Building server-based solutions and SharePoint Add-ins</span></span>
<span data-ttu-id="da3ee-106"><a name="SP15SettingupdevenvBCS_server"> </a></span><span class="sxs-lookup"><span data-stu-id="da3ee-106"></span></span>

<span data-ttu-id="da3ee-107">Как правило большинство решений BCS и приложения будет размещаться в среде сервера.</span><span class="sxs-lookup"><span data-stu-id="da3ee-107">Typically, the majority of BCS solutions and apps will be hosted in a server environment.</span></span> <span data-ttu-id="da3ee-108">Эти решения сервера и приложения предоставляют наибольшую гибкость со всеми компонентами BCS в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="da3ee-108">These server solutions and apps provide the greatest amount of flexibility with all of the features of BCS in SharePoint.</span></span>
  
    
    
<span data-ttu-id="da3ee-109">Для решения на основе сервера как правило, лучше разрабатывать решения на локальном компьютере, где установлен SharePoint и, когда решение построения и тестирования, его развертывание на рабочем сервере.</span><span class="sxs-lookup"><span data-stu-id="da3ee-109">For server-based solutions, it is usually best to develop the solution on a local computer where SharePoint is installed and then, when the solution is built and tested, deploy it to the production server.</span></span> <span data-ttu-id="da3ee-110">Среда разработки можно установить на любом узла рабочей станции или на один или несколько виртуальных компьютеров, работающих под управлением Windows Server 2008 с пакетом обновления 2.</span><span class="sxs-lookup"><span data-stu-id="da3ee-110">You can install a development environment on either a host workstation or on one or more virtual computers that are running Windows Server 2008 Service Pack 2.</span></span>
  
    
    

### <a name="setting-up-an-environment-to-build-sharepoint-add-ins"></a><span data-ttu-id="da3ee-111">Настройка среды для построения Надстройки SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-111">Setting up an environment to build SharePoint Add-ins</span></span>

<span data-ttu-id="da3ee-112">Среда, используемая для разработки приложений с BCS  это то же, как для разработки любого Надстройка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="da3ee-112">The environment that you use for developing apps with BCS is the same as for developing any SharePoint Add-in.</span></span> 
  
    
    
<span data-ttu-id="da3ee-113">В этой статье описывается установка компонентов разработки среды, включая операционной системы, SharePoint, Visual Studio 2012 и инструменты разработчика Office для Visual Studio 2012, следуйте инструкциям в [Set up общие среды разработки для SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="da3ee-113">To learn how to install the components of a development environment, including the operating system, SharePoint, Visual Studio 2012, and Office Developer Tools for Visual Studio 2012, follow the instructions in  [Set up a general development environment for SharePoint](set-up-a-general-development-environment-for-sharepoint.md).</span></span>
  
    
    

## <a name="building-client-based-solutions"></a><span data-ttu-id="da3ee-114">Разработка решений на базе клиента</span><span class="sxs-lookup"><span data-stu-id="da3ee-114">Building client-based solutions</span></span>
<span data-ttu-id="da3ee-115"><a name="SP15SettingupdevenvBCS_client"> </a></span><span class="sxs-lookup"><span data-stu-id="da3ee-115"></span></span>

<span data-ttu-id="da3ee-116">Решения на основе клиентских включить клиентские приложения Office 2013 для доступа к от внешних данных, решения SharePoint или добавить в SharePoint можно.</span><span class="sxs-lookup"><span data-stu-id="da3ee-116">Client-based solutions enable Office 2013 client applications to access the same external data that a SharePoint solution or SharePoint Add-in can.</span></span> <span data-ttu-id="da3ee-117">Это можно сделать при помощи кода с помощью кэш клиента BCS.</span><span class="sxs-lookup"><span data-stu-id="da3ee-117">You can do this by implementing code using the BCS Client Cache.</span></span> <span data-ttu-id="da3ee-118">Клиентские компоненты общаться с BCS через код на стороне клиента и кэш клиента.</span><span class="sxs-lookup"><span data-stu-id="da3ee-118">The client components communicate with BCS through client-side code and the client cache.</span></span> <span data-ttu-id="da3ee-119">Благодаря этому сотрудники клиентские приложения Office с большого объема данных, которые доступны через внешние типы контента SharePoint.</span><span class="sxs-lookup"><span data-stu-id="da3ee-119">This provides Office client applications with the rich data that is available to SharePoint through external content types.</span></span>
  
    
    
<span data-ttu-id="da3ee-120">Так как эти решения не требуют кода, можно использовать SharePoint Designer 2013 и Office 2013.</span><span class="sxs-lookup"><span data-stu-id="da3ee-120">Because these solutions don't require code, you can use SharePoint Designer 2013 and Office 2013.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="da3ee-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="da3ee-121">Additional resources</span></span>
<span data-ttu-id="da3ee-122"><a name="SP15SettingupdevenvBCS_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="da3ee-122"></span></span>


-  [<span data-ttu-id="da3ee-123">Настройка локальной среды разработки надстроек SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-123">Set up an on-premises development environment for SharePoint Add-ins</span></span>](http://msdn.microsoft.com/library/b0878c12-27c9-4eea-ae3b-7e79e5a8838d%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="da3ee-124">Начало работы со службами Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-124">Get started with Business Connectivity Services in SharePoint</span></span>](get-started-with-business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da3ee-125">Business Connectivity Services в SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-125">Business Connectivity Services in SharePoint</span></span>](business-connectivity-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da3ee-126">Обзор разработки решений с помощью SharePoint</span><span class="sxs-lookup"><span data-stu-id="da3ee-126">SharePoint development overview</span></span>](sharepoint-development-overview.md)
    
  

